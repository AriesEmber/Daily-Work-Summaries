# Field Note: Generalized Automation and the 80/20 Tradeoff (2026-05-06)

The day centered on a recurring architectural question: when does a generalized solution justify its complexity over bespoke implementations? This tension surfaced in discussions about referral triage automation across 15 service lines, RAG architecture selection for clinical documents, and a proposed value chain model for shifting architecture governance upstream. Each conversation circled the same tradeoff between upfront investment in generalization and the carrying cost of specialized solutions.

## The Work

### Clinical Workflow Automation: The 80/20 Approach

The referral triage automation discussion crystallized a strategic choice. Leadership requested a holistic approach across 15 service lines rather than building specialty-specific solutions. The target is prompts that work for 80% of cases across all service lines, with specialty requirements identified only after the generalized solution is validated. The volume is material: approximately 1,300 referrals per day flow through one central system, with additional referrals from internal work queues.

This approach aligns with patterns documented in healthcare AI deployment research. Zhou et al. (2023) note that successful medical LLM implementations tend to establish baseline capabilities before layering domain-specific adaptations. The 80/20 framing is a deliberate design constraint that forces the team to identify which features are truly specialty-dependent versus which are assumed to be.

The eligibility matcher conversation revealed a counterexample. Requirements remain unclear because multiple clinical stakeholders describe different use cases and workflows. The question of whether a single technical solution can span multiple care sites or whether each requires separate implementation remains open. This is the failure mode of premature generalization: when stakeholder alignment does not exist, building a generalized solution risks encoding the wrong abstractions.

### RAG Architecture Evaluation

The research platform walkthrough covered a RAG architecture for a research support chatbot using vector databases for document embeddings integrated with a SharePoint approval workflow. The technical discussion surfaced alternatives: MapReduce-style summarization for large clinical documents, and embedding on the fly for smaller document sets.

The distinction matters. Gao et al. (2023) describe three RAG development stages (Naive RAG, Advanced RAG, Modular RAG) and note that the tripartite foundation of retrieval, generation, and augmentation techniques must be matched to the use case. For smaller document sets, the overhead of maintaining a vector index may exceed the cost of runtime embedding. Ke et al. (2024) demonstrated that an LLM-RAG pipeline for preoperative medicine achieved 91.4% accuracy when grounded in 35 clinical guidelines, matching human clinician performance, but the success depended on a curated, bounded knowledge base.

The team is evaluating whether to rebuild the application as a standalone service rather than an extension of the current research platform. This is an architectural decoupling decision independent of the RAG versus alternatives question.

### Enhancement Deployment and the Silent Environment Gap

A process gap surfaced: enhancements to existing automations lack a clear deployment path. Breaking changes sit in a branch with no process to promote and test them. The team discussed the need for a silent deployment or shadow environment to test changes against production-like data.

This is a governance problem masquerading as an infrastructure problem. The action item to document current workload and enhancement backlog, then schedule a follow-up to define the silent deployment process, is the right sequence. Process definition before tooling.

### Architecture Value Chain Proposal

The architecture leadership meeting introduced a six-step value chain proposal: ideation, definition, decision, design, enablement, and planning. The intent is to shift architecture engagement earlier in the project lifecycle, particularly into ideation. The current governance process is perceived as a late-stage toll gate; the proposal distributes governance throughout the lifecycle.

Harmel-Law (2021) describes a decentralized decision-making framework centered on the Advice Process, where anyone can make architectural decisions provided they consult affected parties and subject matter experts beforehand. The proposed value chain echoes this pattern: rather than architecture as gatekeeper, architecture as facilitator embedded in conversations from ideation forward. The feedback requested (show input/output mappings between steps, clarify strategy alignment, consider sandbox environments) indicates the proposal is still in iteration.

### Clinical AI Commercialization

Clarification emerged on the new company structure for productizing an internal clinical AI tool. The healthcare organization will own the new entity; a consultant is managing the vendor relationship, not starting a spin-off company. A third-party vendor specializing in pharmaceutical IT will handle containerization and implementation. The new entity will license IP for multiple products, not just the clinical AI tool.

The internal team's role is knowledge transfer only. The external team determines the future productized architecture.

## Patterns and Frameworks

The day's discussions map to established patterns in healthcare AI and enterprise architecture:

The Anthropic agent architecture taxonomy (2024) distinguishes workflows (predefined code paths) from agents (LLMs dynamically controlling their own processes). The referral triage and eligibility matcher fall into the workflow category: the goal is automation with predictable paths, not autonomous reasoning. This distinction clarifies the design target.

The RAG survey literature (Gao et al., 2023) provides a framework for evaluating retrieval strategies. The team's discussion of MapReduce summarization versus RAG versus on-the-fly embedding reflects the Modular RAG concept, where retrieval and generation components are composed based on use case rather than applied as a monolithic pattern.

The architecture value chain proposal reflects a shift documented in enterprise architecture practice. Harmel-Law's Advice Process model treats architecture as distributed conversation rather than centralized review. The six-step value chain is an operationalization of this principle.

## Decisions and Open Items

**Decisions:**
- PTU allocation: Unused provisioned throughput units deleted; new units secured in two cloud regions.
- Production portal lockout: Team supports enforcing infrastructure-as-code by restricting portal access in the new environment.
- Architecture cross-training: Team agreed to rotate architects across portfolios more intentionally.

**Open items:**
- Model failure rate for newer version under investigation.
- Owner subscription access pending written justification.
- Serverless function modules not yet in infrastructure-as-code framework.
- Enhancement deployment process lacks defined workflow.
- Eligibility matcher requirements remain unclear across stakeholders.
- Architecture value chain proposal still iterating; strategy alignment step placement debated.

## What I'm Taking Forward

The 80/20 framing for referral automation is a design constraint worth testing: can a single prompt surface cover 80% of 15 service lines, and what does the specialty-specific 20% actually look like once measured?

## Further Reading

1. Anthropic. (2024, December 19). Building effective agents. https://www.anthropic.com/research/building-effective-agents

2. Gao, Y., Xiong, Y., Gao, X., Jia, K., Pan, J., Bi, Y., Dai, Y., Sun, J., Wang, M., & Wang, H. (2023). Retrieval-augmented generation for large language models: A survey. arXiv. https://arxiv.org/abs/2312.10997

3. Harmel-Law, A. (2021). Scaling architecture conversationally. martinfowler.com. https://martinfowler.com/articles/scaling-architecture-conversationally.html

4. Ke, Y., Jin, L., Elangovan, K., Abdullah, H. R., Liu, N., Sia, A. T. H., Soh, C. R., Tung, J. Y. M., Ong, J. C. L., & Ting, D. S. W. (2024). Development and testing of retrieval augmented generation in large language models: A case study report. arXiv. https://arxiv.org/abs/2402.01733

5. Zhou, H., Liu, F., Gu, B., Zou, X., Huang, J., Wu, J., Li, Y., Chen, S. S., Zhou, P., Liu, J., Hua, Y., Mao, C., You, C., Wu, X., Zheng, Y., Clifton, L., Li, Z., Luo, J., & Clifton, D. A. (2023). A survey of large language models in medicine: Progress, application, and challenge. arXiv. https://arxiv.org/abs/2311.05112

---
Author: Elvis Jones, Senior Solutions Architect for Clinical AI at an academic medical center.
Doctoral candidate in big data analytics at Colorado Technical University.
LinkedIn: https://www.linkedin.com/in/elvis-jones-mba-pmp/
GitHub: https://github.com/AriesEmber
