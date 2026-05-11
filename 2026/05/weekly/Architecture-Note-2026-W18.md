# Architecture Note: Agent Discipline and Architecture Transfer (Week 18, 2026)

The week posed two architectural questions that connect through the problem of encoding tacit knowledge into transferable structure. The first question: how do you design an agent's tool surface so it remains reliable in clinical settings? The second: how do you transfer architectural understanding of a system built for one institution to a team that must rebuild it for multiple deployment contexts? Both required moving from implicit developer intuition toward explicit design constraints that survive the handoff to someone who was not in the room when the original decisions were made.

## Scoped Tools and the Span-of-Control Discipline

Thursday's agent architecture review surfaced a pattern that had been building all week. A colleague reported that a previous project had exposed a clinical data orchestrator directly to an agent. The orchestrator could retrieve any data type from the EHR, which seemed elegant in design. In practice, the tool's poor documentation forced the team to write explicit calling instructions for the agent, which defeated the purpose of using an agent in the first place. The workaround became the architecture.

The FHIR-AgentBench benchmark from Lee et al. (2025) illuminates why this happens. Their evaluation of 2,931 real-world clinical questions against agents retrieving data from FHIR resources demonstrated that intricate resource structures and multi-step reasoning chains critically affect performance. Exposing individual FHIR APIs as separate tools (notes, labs, orders) rather than bundling them into a universal retrieval function reduced this complexity. The benchmark provides empirical grounding for what the team discovered through trial: scoped tools with prescriptive instructions outperform flexible-but-ambiguous interfaces.

The team adopted a rough guideline of limiting agents to approximately ten tools maximum, borrowing from emergency response management's span-of-control principle. Anthropic's Building Effective Agents guide (2024) reinforces this intuition, though from a different angle. Their guidance emphasizes that tool definitions deserve as much prompt engineering attention as overall prompts. The poka-yoke principle applies: absolute filepaths beat relative ones, and prescriptive instructions beat open-ended interfaces. The SWE-bench implementation from Anthropic spent more time optimizing tools than the overall prompt.

Hu's empirical study of 70 agent-system projects (2026) provides additional context. The research identifies five recurring architectural dimensions: subagent architecture, context management, tool systems, safety mechanisms, and orchestration. Registry-oriented tool systems remain dominant, with formalized tool-registration boundaries aligning with broader ecosystem goals. The pattern of deeper coordination correlating with explicit context services suggests that agent reliability emerges from structural discipline, not capability breadth.

A secondary tension emerged during Thursday's discussion: whether a custom tool-calling architecture is justified when a simple prompt to the chat completion API achieves 90 to 95 percent accuracy. If the simpler approach works, the agentic complexity is overhead. The team did not resolve this question. Evaluation remains unclear when routing criteria are user-configurable and change frequently. The RAG literature offers partial guidance. Ke et al. (2024) demonstrated that an LLM-RAG pipeline for preoperative medicine achieved 91.4% accuracy when grounded in 35 clinical guidelines, matching human clinician performance. But their success depended on a curated, bounded knowledge base. Dynamic criteria create evaluation scope questions that static benchmarks do not address.

## Productization as Architecture Transfer

Friday's knowledge transfer session with the implementation partner brought the week's second thread into focus. The healthcare organization is commercializing its clinical AI tool through a newly formed spinoff entity. The implementation partner provides engineering capacity for productization while the parent organization retains ownership. The question is not code sharing; the partner will maintain a separate codebase. The question is how to transfer architectural patterns and operational lessons that are not documented anywhere.

The two-hour kickoff session addressed the full stack: authentication via SMART on FHIR following the HL7 v2.2.0 specification, real-time data fetching through FHIR APIs, tokenization and chunking for large patient records, routing to multiple LLM providers through a proxy gateway, and persistence in blob storage and document databases. The SMART App Launch specification establishes OAuth 2.0-based patterns for client applications to authorize, authenticate, and integrate with FHIR-based data systems. For user-facing applications with launch context (such as sharing the currently selected patient from an EHR session), the specification defines the SMART App Launch pattern. For headless or automated applications, it defines SMART Backend Services. These patterns are transferable; the implementation partner can reference the same specification.

The most technically significant discussion centered on context compression. Patient records routinely exceed two million tokens, requiring a map-reduce style approach. The system chunks the record, compresses each chunk independently, then consolidates the compressed outputs. This pattern appears in recent prompt compression research. Hu et al. (2026) describe BEAVER, a hierarchical prompt compression method that shifts from linear token removal to structure-aware selection, achieving 26.4x latency improvement on 128k contexts. Berton et al. (2025) present CompLLM, which divides context into segments for independent compression with linear scaling. The clinical AI system's approach follows the segment-then-consolidate pattern, though the specific implementation details remain proprietary.

The implementation partner asked detailed questions about containerization, security hardening, CI/CD processes, and deployment topology for external customers. These questions reflect the core challenge of productization: the original system was built for a single institution's identity provider, middleware stack, and model access arrangements. External customers will have different configurations. The APPFLx framework from Hoang et al. (2023) provides a reference pattern for infrastructure-agnostic healthcare systems. Their work on federated learning across heterogeneous computing environments demonstrates that designing for deployment variability from the start reduces retrofitting costs. Thursday's research application architecture session reached the same conclusion: Docker containerization with Terraform for environment provisioning enables portability across cloud providers.

The knowledge transfer is not about code. It is about encoding the decisions that are not visible in the code. Why does model selection follow token count thresholds rather than task type? Because evaluation runs against three months of production logs showed latency matters more than capability ceiling for clinical workflows. Why does the system use real-time FHIR retrieval rather than pre-indexing? Because data freshness requirements exceed what periodic indexing can guarantee. These rationales must be documented explicitly for the implementation partner to make appropriate modifications for different deployment contexts.

## Decisions and Outcomes

- Agent tool design: scoped tools (separate functions for notes, labs, orders) rather than monolithic orchestrators
- Agent tool limit: approximately ten tools maximum as a design constraint
- Knowledge transfer: architectural patterns and operational lessons transfer through documentation, not code sharing
- Research application: GCP initial environment with Docker and Terraform for portability to other providers
- Research application: agent configuration files managed through CI/CD pipelines, not SharePoint
- Autonomous billing coding pilot: approved with 95% accuracy threshold for production and model drift monitoring requirements
- Medical imaging workflow migration: approved with Active Directory waiver, remediation expected by March 2027

## Open Questions

- Agent evaluation: how do you measure system accuracy when routing criteria are user-configurable and change frequently?
- Context compression: the segment-then-consolidate pattern works, but the boundary between institution-specific implementation and transferable pattern requires documentation
- Productization scope: which security hardening items (TLS verification, JWT validation, hardcoded keys) are institution-specific versus transferable?
- Operations ownership: infrastructure operations ownership for the data platform remains unresolved pending follow-up with platform leadership

## What I'm Taking Forward

The FHIR-AgentBench dataset and evaluation suite warrant review for establishing a baseline before investing further in agentic architecture for clinical decision support.

## Further Reading

1. Anthropic. (2024). *Building effective agents*. https://www.anthropic.com/research/building-effective-agents

2. Berton, G., Unnikrishnan, J., Tran, S., & Shah, M. (2025). CompLLM: Compression for long context Q&A. *arXiv preprint*. https://arxiv.org/abs/2509.19228

3. Gao, Y., Xiong, Y., Gao, X., Jia, K., Pan, J., Bi, Y., Dai, Y., Sun, J., Wang, M., & Wang, H. (2023). Retrieval-augmented generation for large language models: A survey. *arXiv preprint*. https://arxiv.org/abs/2312.10997

4. HL7 International. (2023). SMART App Launch v2.2.0 (FHIR Implementation Guide). https://hl7.org/fhir/smart-app-launch/

5. Hoang, T.-H., Fuhrman, J., Madduri, R., Li, M., Chaturvedi, P., Li, Z., Kim, K., Ryu, M., Chard, R., Huerta, E. A., & Giger, M. (2023). Enabling end-to-end secure federated learning in biomedical research on heterogeneous computing environments with APPFLx. *arXiv preprint*. https://arxiv.org/abs/2312.08701

6. Hu, W. (2026). Architectural design decisions in AI agent harnesses. *arXiv preprint*. https://arxiv.org/abs/2604.18071

7. Hu, Z., Li, K., Fu, D., Zeng, C., Li, Y., Tang, Y., & Huang, J. (2026). BEAVER: A training-free hierarchical prompt compression method via structure-aware page selection. *arXiv preprint*. https://arxiv.org/abs/2603.19635

8. Ke, Y., Jin, L., Elangovan, K., Abdullah, H. R., Liu, N., Sia, A. T. H., Soh, C. R., Tung, J. Y. M., Ong, J. C. L., & Ting, D. S. W. (2024). Development and testing of retrieval augmented generation in large language models: A case study report. *arXiv preprint*. https://arxiv.org/abs/2402.01733

9. Lee, G., Bach, E., Yang, E., Pollard, T., Johnson, A., Choi, E., Jia, Y., & Lee, J. H. (2025). FHIR-AgentBench: Benchmarking LLM agents for realistic interoperable EHR question answering. *ML4H 2025 Proceedings*. https://arxiv.org/abs/2509.19319

---
Author: Elvis Jones, Senior Solutions Architect for Clinical AI at an academic medical center.
Doctoral candidate in big data analytics at Colorado Technical University.
LinkedIn: https://www.linkedin.com/in/elvis-jones-mba-pmp/
GitHub: https://github.com/AriesEmber
