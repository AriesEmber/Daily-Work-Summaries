# Field Note: Scoped Tools and the Span-of-Control Problem (2026-05-07)

The central tension of the day was architectural: how to expose clinical data to an AI agent without overwhelming it. Five meetings touched three distinct initiative phases, but the through-line was tool decomposition. A monolithic orchestrator that retrieves any clinical data sounds elegant until an agent must document how to call it. Scoped tools with prescriptive instructions proved the pattern that works.

## The Work

### Agent Tool Surface

The agent approach review meeting addressed a patient routing and screening system. A colleague reported that a previous tumor board project had exposed a clinical data orchestrator directly to an agent. The orchestrator's poor documentation forced the team to write explicit calling instructions, which defeated the purpose of using an agent in the first place. The workaround became the architecture.

The team referenced a recent paper from a clinical informatics research lab that demonstrates exposing individual FHIR APIs as separate tools rather than bundling them into a universal retrieval function. The FHIR-AgentBench benchmark documented in Lee et al. (2025) evaluates exactly this pattern: 2,931 real-world clinical questions against agents retrieving data from FHIR resources. The benchmark reveals that intricate resource structures and reasoning chains critically affect performance. Scoped tools (notes, labs, orders as separate functions) reduce this complexity.

The team adopted a rough guideline of limiting agents to approximately ten tools maximum, borrowing from emergency response span-of-control principles. Anthropic's Building Effective Agents guide (2024) reinforces this intuition: clear documentation, example usage, and edge case handling matter more than tool count, but proliferation without discipline leads to retrieval failures. The poka-yoke principle applies. Absolute filepaths beat relative ones. Prescriptive instructions beat flexible-but-ambiguous interfaces.

A secondary tension emerged: whether a custom tool-calling architecture is justified when a prompt to the chat UI API achieves 90 to 95 percent accuracy. If the simpler approach works, complexity is overhead. The team did not resolve this. Evaluation remains unclear when routing criteria are user-configurable and change frequently.

### Research Application Architecture

A separate meeting initiated design for a research study intake and management application. The previous prototype built on a survey data capture tool had outgrown its capabilities. The team will build standalone.

GCP was selected as the initial cloud environment, with an explicit design principle: environment-agnostic tooling (Docker, Terraform) for portability to other providers. The Hoang et al. (2023) work on federated learning across heterogeneous healthcare environments describes exactly this pattern. Infrastructure-agnostic design enables collaboration across institutions with different computing stacks. The research application may eventually span affiliated entities, and portability is cheaper to build in than to retrofit.

The application will handle PHI, PII, and high-risk budgetary information. Authentication requires university single sign-on as primary, with support for a children's hospital affiliate. Role-based access via authority manager was deferred to post-V1, which is defensible scoping but will require revisiting.

Agent configuration files (system prompts, tool definitions) will be managed through CI/CD pipelines rather than SharePoint. Version control and security outweigh convenience. A colleague demonstrated a URL ingestion process that follows links in documents and indexes referenced content for a knowledge base. Policy documents flow through SharePoint with approval workflows before vector database ingestion.

### Architecture Review Board Approvals

Three solutions received board approval. A radiology workflow tracking system will migrate from physical servers to virtual machines; an Active Directory waiver was signed with remediation expected by March 2027. Two 3D medical imaging products for surgical planning will migrate from the School of Medicine data center to healthcare organization infrastructure.

The third approval was more significant: an autonomous medical coding pilot targeting radiology professional billing. The vendor claims 90 percent automation rate and 96 percent accuracy using LLM technology. The Hartnett et al. (2026) study on LLM-based medical coding found that fully automated unsupervised coding with local open-source models is not yet reliable and recommends human-in-the-loop approaches. The pilot's 95 percent accuracy threshold for production acceptance aligns with this caution. Model drift monitoring and retraining schedules remain undefined.

## Patterns and Frameworks

The FHIR-AgentBench benchmark (Lee et al., 2025) demonstrates that exposing individual FHIR APIs as discrete tools produces better agent performance than monolithic retrieval. The benchmark's 2,931 real-world clinical questions provide an evaluation framework the team can reference when designing tool surfaces. The architectural design decisions framework documented in Hu (2026) identifies five recurring dimensions in agent harnesses, with registry-oriented tool systems remaining dominant while MCP-based extensions emerge.

For medical coding automation, the Hartnett et al. (2026) study establishes current accuracy limits: human-in-the-loop remains the recommended pattern until models demonstrate sustained reliability above organizational thresholds.

The APPFLx framework (Hoang et al., 2023) provides a reference architecture for infrastructure-agnostic healthcare systems. The principle of designing for heterogeneous computing environments applies to multi-cloud portability as much as to federated learning.

## Decisions and Open Items

**Decisions:**

- Agent tools: scoped (separate functions for notes, labs, orders) rather than monolithic orchestrators
- Agent tool limit: approximately ten tools maximum
- Research application: GCP initial environment with Docker/Terraform for portability
- Research application: three-tier deployment (DEV, UAT/Stage, PRD)
- Research application: agent configuration managed through CI/CD, not SharePoint
- Marketing data platform: will target next-generation Databricks platform, not legacy warehouse

**Open Items:**

- Agent design: evaluation approach unclear when criteria are user-configurable
- Autonomous coding: 95 percent accuracy threshold for production; validation pending
- Autonomous coding: model drift monitoring not yet defined
- Research application: AI Hub (Azure) versus native GCP models decision deferred
- Research application: migration path for in-flight studies undecided

## What I'm Taking Forward

The PhysicianBench paper and its GitHub repository warrant review for patterns on exposing FHIR APIs as discrete agent tools. The evaluation gap for user-configurable routing criteria remains unaddressed.

## Further Reading

1. Anthropic. (2024). *Building effective agents*. https://www.anthropic.com/research/building-effective-agents

2. Hartnett, P., Huang, C.-C., Hartnett, S., & Hartnett, D. (2026). Leveraging large language models to extract and translate medical information in doctors' notes for health records and diagnostic billing codes. *arXiv preprint*.

3. Hoang, T.-H., Fuhrman, J., Madduri, R., Li, M., Chaturvedi, P., Li, Z., Kim, K., Ryu, M., Chard, R., Huerta, E. A., & Giger, M. (2023). Enabling end-to-end secure federated learning in biomedical research on heterogeneous computing environments with APPFLx. *arXiv:2312.08701*.

4. Hu, W. (2026). Architectural design decisions in AI agent harnesses. *arXiv:2604.18071*.

5. Lee, G., Bach, E., Yang, E., Pollard, T., Johnson, A., Choi, E., Jia, Y., & Lee, J. H. (2025). FHIR-AgentBench: Benchmarking LLM agents for realistic interoperable EHR question answering. *ML4H 2025 Proceedings*. arXiv:2509.19319.

---

Author: Elvis Jones, Senior Solutions Architect for Clinical AI at an academic medical center.
Doctoral candidate in big data analytics at Colorado Technical University.
LinkedIn: https://www.linkedin.com/in/elvis-jones-mba-pmp/
GitHub: https://github.com/AriesEmber
