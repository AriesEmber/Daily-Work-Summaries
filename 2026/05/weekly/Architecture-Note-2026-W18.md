# Architecture Note: Span of Control in Agentic Systems and the Productization Boundary (Week 18, 2026)

The week surfaced two connected architectural arguments. The first concerns how many tools an LLM agent can reliably orchestrate before reliability degrades. The second concerns where to draw the boundary between an internal platform and its productized derivative. Both reduce to the same underlying question: when does adding scope to a system create liability rather than capability? The week's meetings tested these boundaries through concrete design decisions on clinical AI agents and a knowledge transfer engagement for platform productization.

## Tool Decomposition and the Span of Control Principle

Thursday's agentic design review established a design constraint: no agent should have access to more than five to ten tools, and each tool must carry clear semantic meaning. The rationale emerged from direct observation. When an agent is given access to a monolithic orchestrator capable of retrieving any data type (notes, labs, orders, imaging), reliability degrades. The orchestrator's comprehensive capability becomes a liability because the agent lacks semantic cues to select appropriate retrieval strategies.

This finding aligns with Anthropic's engineering guidance on agent-computer interface design. The guidance emphasizes that tool design quality matters more than tool count, recommending that developers "invest as much effort in agent-computer interfaces as human-computer interfaces" (Anthropic, 2024). The SWE-bench case study in that guidance documents how requiring absolute filepaths eliminated errors that occurred with relative paths. Small changes to tool interface design yielded disproportionate reliability improvements.

The analogy to incident management is instructive. The National Incident Management System establishes that no supervisor should manage more than seven direct reports during emergency response (Federal Emergency Management Agency, 2017). This span of control principle emerged from coordination failures during the 1970 California wildfires and was refined after 9/11. The principle exists because cognitive load limits effective coordination regardless of the supervisor's competence.

The week's design decision applied this principle to tool-calling architectures. Decomposing a monolithic Fire orchestrator into scoped tools (notes retrieval, laboratory values, orders, imaging) provides the agent with decision-relevant structure. The agent can reason about which category of clinical data to retrieve rather than navigating a generic "retrieve anything" interface.

The ReAct framework documented by Yao et al. (2022) provides additional grounding. By interleaving reasoning traces with tool calls, ReAct demonstrated a 34% absolute improvement in success rate on ALFWorld benchmarks compared to methods that separate reasoning from action. The framework "overcomes issues of hallucination and error propagation prevalent in chain-of-thought reasoning by interacting with a simple Wikipedia API" (Yao et al., 2022). The implication for clinical AI is that interpretable reasoning-action loops require tools with clear semantic boundaries.

The evaluation framework discussion on Thursday raised a related question: how should organizations handle deployment when evaluation cost scales with criteria configurability? A novel framing emerged treating rigorous evaluation as an opt-in service rather than a deployment prerequisite. Clinical teams with publication motivations may invest in detailed annotation and evaluation infrastructure. Operational teams may accept deployment with explicit acknowledgment of uncharacterized failure modes. This mirrors the pharmaceutical distinction between approved indications and off-label use.

## Platform Productization and Organizational Boundary Management

Wednesday's executive strategy session clarified the structure of a healthcare organization's effort to productize an internal clinical AI platform. The healthcare organization will own a new entity. An external vendor specializing in pharmaceutical IT will handle containerization and implementation. The internal team's role is knowledge transfer only; the external team determines the productized architecture.

Friday's knowledge transfer session operationalized this boundary. The session covered Fire orchestration patterns, asynchronous chunking for long clinical documents, and model routing strategies. The discussion of context window management was particularly detailed: the platform implements an 80% threshold per user message with conditional compression when approaching limits. These patterns work within the internal environment but require architectural decisions about what translates to a productized offering versus what remains implementation-specific.

The decision to maintain a separate codebase and infrastructure for the product entity reflects a common pattern in healthcare IT productization. Delta Sharing provides a reference model for this kind of boundary management. The Databricks documentation describes Delta Sharing as enabling "secure data sharing with other organizations regardless of the computing platforms they use" through an open protocol that separates compute from storage governance (Databricks, 2024). Recipients access data in read-only format through pre-signed short-lived URLs without requiring data replication.

The productization architecture faces a similar question: how do you share capability without sharing implementation? The knowledge transfer sessions are documenting patterns (Fire pagination, binary object retrieval, token limit management) that the external team can reimagent in their own infrastructure. The IP transfer includes these patterns as licensable knowledge, not as runnable code.

TEFCA provides another reference model for federated governance across organizational boundaries. The framework establishes "a universal floor for interoperability" through a network-of-networks model where Qualified Health Information Networks serve as connection points (Office of the National Coordinator for Health Information Technology, 2024). By December 2025, TEFCA had facilitated nearly 500 million health record exchanges. The three-tier structure (Common Agreement, Trusted Exchange Framework, QHIN Technical Framework) separates legal contracts from technical specifications, allowing organizations to maintain implementation autonomy while meeting baseline requirements.

The week's data platform discussions employed a similar pattern. Delta sharing with enclave isolation enables research teams to query production data without ETL duplication. Unity Catalog provides the governance layer. The question of how IRB workflows integrate with enclave provisioning remains open, but the architectural pattern is established: separate the governance model from the compute model.

## Decisions and Outcomes

- Cloud environment selection: GCP for initial research platform development; container orchestration preserves Azure migration path
- Agent tool design: decompose monolithic orchestrator into scoped, semantically meaningful tools (5-10 maximum per agent)
- Productization structure: separate codebase and infrastructure for spin-off product entity; internal team provides knowledge transfer only
- Data platform pattern: Delta sharing with enclave isolation; Unity Catalog for governance; treat agent configuration as code
- Authentication: support multiple identity providers for affiliated organization access across research platform

## Open Questions

- How does evaluation cost scale when end users can modify eligibility criteria weekly? Is opt-in rigorous evaluation economically viable?
- Where does the boundary between the internal platform's evolution and the productized fork get managed over time?
- How do IRB workflows integrate with enclave provisioning for the data platform?
- What silent deployment or shadow environment process should govern clinical automation enhancements?

## What I'm Taking Forward

The 5-10 tool limit is a testable hypothesis. The next design review should measure whether reliability improves when Fire data retrieval is decomposed into semantically scoped tools versus a single comprehensive orchestrator.

## Further Reading

1. Anthropic. (2024). *Building effective agents*. Anthropic Engineering. https://www.anthropic.com/engineering/building-effective-agents

2. Databricks. (2024). *Delta Sharing: An open protocol for secure data sharing*. https://docs.databricks.com/en/delta-sharing/index.html

3. Federal Emergency Management Agency. (2017). *National Incident Management System* (3rd ed.). U.S. Department of Homeland Security. https://www.fema.gov/sites/default/files/2020-07/fema_nims_doctrine-2017.pdf

4. Gao, Y., Xiong, Y., Gao, X., Jia, K., Pan, J., Bi, Y., Dai, Y., Sun, J., Wang, M., & Wang, H. (2024). Retrieval-augmented generation for large language models: A survey. *arXiv preprint arXiv:2312.10997*. https://arxiv.org/abs/2312.10997

5. Guo, T., Chen, X., Wang, Y., Chang, R., Pei, S., Chawla, N. V., Wiest, O., & Zhang, X. (2024). Large language model based multi-agents: A survey of progress and challenges. *arXiv preprint arXiv:2402.01680*. https://arxiv.org/abs/2402.01680

6. Office of the National Coordinator for Health Information Technology. (2024). *Trusted Exchange Framework and Common Agreement (TEFCA)*. U.S. Department of Health and Human Services. https://www.healthit.gov/topic/interoperability/trusted-exchange-framework-and-common-agreement-tefca

7. Singhal, K., Tu, T., Gottweis, J., Sayres, R., Wulczyn, E., Hou, L., ... & Natarajan, V. (2023). Towards expert-level medical question answering with large language models. *arXiv preprint arXiv:2305.09617*. https://arxiv.org/abs/2305.09617

8. Wang, L., Ma, C., Feng, X., Zhang, Z., Yang, H., Zhang, J., ... & Wen, J.-R. (2024). A survey on large language model based autonomous agents. *arXiv preprint arXiv:2308.11432*. https://arxiv.org/abs/2308.11432

9. Xiong, G., Jin, Q., Lu, Z., & Zhang, A. (2024). Benchmarking retrieval-augmented generation for medicine. *arXiv preprint arXiv:2402.13178*. https://arxiv.org/abs/2402.13178

10. Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2023). ReAct: Synergizing reasoning and acting in language models. *Proceedings of the International Conference on Learning Representations*. https://arxiv.org/abs/2210.03629

---
Author: Elvis Jones, Senior Solutions Architect for Clinical AI at an academic medical center.
Doctoral candidate in big data analytics at Colorado Technical University.
LinkedIn: https://www.linkedin.com/in/elvis-jones-mba-pmp/
GitHub: https://github.com/AriesEmber
