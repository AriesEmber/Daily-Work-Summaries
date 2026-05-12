# Field Note: Infrastructure Separation and Data Governance Under Pressure (2026-05-11)

Two architecture problems dominated the day: protecting interactive clinical systems from batch automation workloads, and consolidating fragmented data environments under unified governance. Both share a common thread of isolation as a design tool, whether isolating compute to preserve responsiveness or isolating data enclaves to preserve compliance.

## The Work

### Automation Infrastructure Separation

The morning vendor architecture session continued work on an AI platform that processes patient data at scale. The platform faces a classic batch-versus-interactive tension: automation workloads can consume 800 API calls per patient, with some records exceeding 80 million tokens annually. When these long-running processes exhaust token-per-minute quotas, queue buildup threatens the clinician-facing interface.

The team converged on forking the automation infrastructure from the interactive UI within two months. This separation protects the clinician experience during high automation load by ensuring batch processes cannot starve interactive requests of API capacity. The pattern reflects established practice in agent orchestration, where workload isolation prevents resource contention between synchronous and asynchronous processing paths.

Code sharing arrangements also advanced. The vendor operates on-premises GitLab, requiring an external sharing mechanism. Security approval remains pending, with an assigned architect verifying requirements. An in-person session scheduled for Wednesday will allow deeper technical review.

### Data Platform Consolidation

The afternoon session addressed a fragmented data environment spanning an enterprise data warehouse vendor, EHR analytics on cloud fabric, and on-premises research clusters. The proposed platform unifies these under a lakehouse architecture with open formats, multi-cloud federation, and centralized catalog governance.

The conceptual architecture follows an ingest-model-enhance-transform-deliver framework. Enclave provisioning automates the creation of isolated data environments: a service request triggers resource group creation with appropriate access controls and compute restrictions. This workflow aligns with the governance model documented in Databricks Unity Catalog, which organizes assets through a three-level namespace (catalog.schema.object) and enforces least-privilege access by default.

Integration patterns received detailed review. Inbound paths include database connections, vendor data sharing, and SaaS application connectors. Outbound paths serve enterprise BI tools and consumer system data sharing. The Delta Sharing protocol enables cross-organizational exchange without data duplication.

A governance gap surfaced during the session: the platform team uses AI code generation tools without documented architecture or management visibility. The architecture team lacks access to the relevant GitHub repository to assess how these tools integrate with the platform.

### Architecture Review Board Scheduling

Cancelled sessions on the current week and May 21st have created a backlog. Seven presentations are now scheduled for May 28th, likely exceeding available meeting time. The team discussed extending the session or sequencing items across multiple dates.

The data platform project faces a specific constraint: its project charter remains unsigned. If the charter is not finalized by the review date, the presentation will proceed as informational rather than seeking approval, with a follow-up session scheduled once the charter is complete.

## Patterns and Frameworks

The automation infrastructure separation reflects the orchestrator-workers pattern documented in Anthropic's guidance on building effective agents. That framework emphasizes workload governance through clear stopping conditions, sandboxed testing, and human feedback checkpoints before production deployment. The vendor's decision to fork automation from interactive infrastructure implements a physical separation that the orchestration literature often accomplishes through logical queueing.

The data platform's enclave provisioning model implements the governance pillars described in Databricks Unity Catalog documentation: unified access control, automated lineage tracking, and data quality monitoring operate across a multi-cloud footprint spanning AWS, Azure, and GCP. The three-level namespace enables consistent governance across diverse asset types while the least-privilege model ensures users receive only the access their role requires.

The concern about undocumented AI code generation tools echoes findings from He et al.'s survey of large language models in healthcare, which identifies fairness, accountability, transparency, and ethics as primary obstacles to LLM adoption in clinical settings. Shadow tooling without architecture visibility represents an accountability gap that must be closed before the organization can govern AI-generated code alongside human-authored contributions.

## Decisions and Open Items

**Decisions:**
- Fork automation infrastructure from UI within two months (owner: platform team)
- Data platform ARB presentation proceeds as informational if charter remains unsigned
- In-person vendor session confirmed for Wednesday with recording for remote attendees

**Open items:**
- Security approval for external code repository sharing with vendor
- Project charter signature blocking full ARB approval
- Documentation gap on AI code generation tools used by platform team
- Seven ARB presentations scheduled for May 28th may require extended session

## What I'm Taking Forward

The platform team's use of AI code generation tools without documented architecture creates a governance blind spot. Obtaining access to their GitHub repository is the immediate next step before the organization can assess integration patterns and establish appropriate oversight.

## Further Reading

1. Anthropic. (2024). Building effective agents. https://www.anthropic.com/research/building-effective-agents

2. Databricks. (2024). Unity Catalog. In Databricks Documentation. https://docs.databricks.com/en/data-governance/unity-catalog/index.html

3. He, K., Mao, R., Lin, Q., Ruan, Y., Lan, X., Feng, M., & Cambria, E. (2023). A survey of large language models for healthcare: From data, technology, and applications to accountability and ethics. arXiv preprint arXiv:2310.05694. https://arxiv.org/abs/2310.05694

---
Author: Elvis Jones, Senior Solutions Architect for Clinical AI at an academic medical center.
Doctoral candidate in big data analytics at Colorado Technical University.
LinkedIn: https://www.linkedin.com/in/elvis-jones-mba-pmp/
GitHub: https://github.com/AriesEmber
