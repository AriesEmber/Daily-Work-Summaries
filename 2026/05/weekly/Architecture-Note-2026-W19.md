# Architecture Note: Platform as Program and the Multi-Tenancy Imperative (Week 19, 2026)

The week of May 11 through 15 surfaced two architectural arguments that ran through nearly every meeting: first, that foundational data platforms cannot be governed as projects with end dates, and second, that multi-tenant access across organizational boundaries must be designed as a first-class concern rather than bolted on after initial deployment. These threads connected a data lakehouse initiative, a clinical AI platform handoff, a research environment design, and enterprise architecture governance discussions.

## Platform Thinking Versus Project Thinking

A senior stakeholder said it directly on Friday: "This is a program, not a project." The statement emerged during enterprise architecture follow-up for a data platform initiative now in its conceptual phase. The governance board asked for quantitative success metrics. The team offered one concrete number: cost savings from retiring an external analytics vendor. That metric is measurable but says nothing about whether the platform enables new capability.

The tension is structural. Project governance frameworks assume bounded scope, fixed deliverables, and milestone-based funding. Platform initiatives inherit the continuous character described in the Microsoft Cloud Adoption Framework, which positions cloud governance as "a continuous process" requiring "ongoing monitoring, evaluation, and updates to adapt to new technologies, evolving risks, and changing requirements" (Microsoft, 2025). The framework's RACI matrix approach clarifies accountability: the governance team is accountable for policy development while platform and workload teams are responsible for implementation. What the framework does not solve is how to fund work that never finishes.

The capability maturity model framing surfaced repeatedly as a potential measurement instrument. The team discussed a six-level scale (manual, repeatable, standardized, measured, automated, autonomous) with assessments every six months. This echoes the Software Engineering Institute's CMMI lineage, though applied to data operations. The DAMA-DMBOK offers a more domain-appropriate lens, framing maturity through data governance, integration, and interoperability functions (DAMA International, 2017). Both frameworks share an insight: maturity is measured by the repeatability and adaptiveness of process, not by the completion of deliverables.

The lakehouse architecture itself embodies this program-not-project logic. As described by Lorica et al. (2020), the pattern combines transactional guarantees from data warehouses with the flexibility of data lakes: ACID transactions, schema enforcement, direct BI support, decoupled storage and compute, open formats, support for diverse data types, and end-to-end streaming. The appeal for an academic medical center is the promise of a single platform supporting both research analytics and operational reporting. But that promise is capability, not delivery. The platform never ships; it continuously enables.

The financial modeling discussion on Wednesday added another layer. The team examined NPV, ROI, and payback period for deployed AI automations. Three were recommended for expansion; one was flagged for strategic scoring review. A question emerged: does AI-specific cost attribution create unfair scrutiny compared to traditional clinical decision support tools that rarely face the same measurement burden? The broader pattern is that new capabilities inherit measurement requirements their predecessors avoided, even when the comparison is apples to oranges.

## Multi-Tenancy as Architecture Driver

Three separate initiatives this week grappled with access patterns across organizational boundaries. The data platform must serve healthcare operations, academic research, and affiliated institutions. The research platform must authenticate students, staff, and external collaborators across healthcare and academic identity providers. The clinical AI spinoff must parameterize deployments for multiple customer sites. Each arrived at a similar architectural response: identity federation as a foundational requirement, not an enhancement.

The data platform discussion introduced enclave provisioning as an automated workflow. A service request triggers resource group creation with appropriate access controls and compute restrictions. The enclave model aligns with Dehghani's (2022) data mesh principle of domain-oriented decentralized ownership, where research teams would manage their own analytical data products within a self-serve infrastructure platform. The self-serve data infrastructure concept maps directly to the proposed automation: teams provision and manage their own workspaces without centralized data engineering bottlenecks.

The Databricks Unity Catalog documentation describes the underlying governance choice: organizations must choose between managed governance (where the platform controls both access and storage lifecycle) and external governance (where the platform controls permissions only) depending on source characteristics (Databricks, 2025). The three-level namespace (catalog.schema.object) enables consistent governance across diverse asset types while row-level security using identity passthrough enforces access control at query time. These are not features to be added later; they are foundational decisions that shape every subsequent design choice.

The research platform discussion on Friday identified the same pattern from a different direction. Multi-institutional access is required for healthcare system staff, academic medical school researchers, affiliated facilities, and students. The legacy SSO platform is being deprecated. Identity provider federation is under investigation, with a scheduled meeting to address full platform access patterns. The question of how to authenticate users from five different organizational identity stores is not a security add-on; it is the architecture.

The clinical AI platform facing partner handoff showed the commercial expression of the same pattern. Databricks notebook configuration files were flagged as customer-specific, requiring parameterization. The repository contains Terraform definitions, UI with backend-for-frontend pattern, FHIR orchestrator, LLM gateway, and pipeline orchestration. The partner will serve multiple deployment sites. Configuration externalization for site-specific variation is not convenience; it is the difference between a product and a one-off implementation.

The FHIR-first pivot in the clinical data repository connects these threads. The team moved from CCD-based data loading to a FHIR-first approach after identifying CCD limitations. FHIR's design philosophy, as described in the HL7 specification, emphasizes composition over constraint: resources combine through references rather than constraining a complex universal model (HL7 International, 2024). The 80/20 rule embedded in FHIR (building a base resource set satisfying the majority of common use cases with extension mechanisms for the rest) maps to the flexibility requirements the platform encountered. More practically, the US Core Implementation Guide defines mandatory data elements for US Realm implementation, aligning with USCDI standards required by ONC certification (HL7 US Realm Steering Committee, 2025).

## Token Economics as Capacity Constraint

A secondary thread worth noting: the clinical AI platform discussion revealed that token-per-minute limits constrain automation scaling more than compute capacity. At 800 API calls per patient for FHIR orchestration, with some records exceeding 80 million tokens annually, the 100,000 automation target requires careful rate management. The team converged on forking automation infrastructure from the interactive UI within two months. This separation protects the clinician experience during high automation load by ensuring batch processes cannot starve interactive requests of API capacity.

The pattern reflects established practice in agent orchestration. Anthropic's guidance on building effective agents distinguishes workflows (predefined orchestration paths) from agents (dynamic process direction) and identifies workload governance through clear stopping conditions, sandboxed testing, and human feedback checkpoints before production deployment (Anthropic, 2024). The vendor's decision to fork automation from interactive infrastructure implements a physical separation that the orchestration literature often accomplishes through logical queueing.

## Decisions and Outcomes

- Architecture review board presentation scheduled for 2026-05-28 with seven solutions presenting
- Data platform review cannot complete until project charter is signed; will proceed as informational
- Automation infrastructure to be forked from interactive UI within two months
- Google Ads connector approved for pilot pending PHI confirmation; HIPAA workloads await GA on 2026-07-31
- Excel plugin confirmed HIPAA compliant for limited tactical use
- Repository handoff to external partner to proceed via GitHub organization access
- FHIR store proceeding with 1,000 patient validation using FHIR-first approach

## Open Questions

- How to operationalize capability maturity model assessment into specific criteria before the 2026-05-28 ARB presentation
- Identity management discussion with school of medicine scheduled for next Wednesday; full platform access patterns depend on this conversation
- Whether the AI financial framework methodology can be documented for broader adoption across teams
- Governance process for external data access via data marketplace concept not yet defined
- Provider location master does not exist in standardized form; multi-year timeline acknowledged

## What I'm Taking Forward

The capability maturity model framing offers a path forward for measuring platform progress, but assessment criteria remain unoperationalized. The architecture review board presentation may force that conversation.

## Further Reading

1. Anthropic. (2024, December 19). Building effective agents. https://www.anthropic.com/research/building-effective-agents

2. DAMA International. (2017). *DAMA-DMBOK: Data management body of knowledge* (2nd ed.). Technics Publications. https://www.dama.org/cpages/body-of-knowledge

3. Databricks. (2025). Unity Catalog. In *Databricks Documentation*. https://docs.databricks.com/en/data-governance/unity-catalog/index.html

4. Dehghani, Z. (2020, December 3). Data mesh principles and logical architecture. martinfowler.com. https://martinfowler.com/articles/data-mesh-principles.html

5. HL7 International. (2024). FHIR overview (R5). https://www.hl7.org/fhir/overview.html

6. HL7 US Realm Steering Committee. (2025). US Core Implementation Guide v8.0.1. https://hl7.org/fhir/us/core/

7. Lorica, B., Armbrust, M., Xin, R., Zaharia, M., & Ghodsi, A. (2020, January 30). What is a data lakehouse? *Databricks Blog*. https://www.databricks.com/blog/2020/01/30/what-is-a-data-lakehouse.html

8. Microsoft. (2025). Build a cloud governance team. *Azure Cloud Adoption Framework*. https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/govern/build-cloud-governance-team

9. National Institute of Standards and Technology. (2023, January 26). AI Risk Management Framework 1.0. https://www.nist.gov/itl/ai-risk-management-framework

10. Office of the National Coordinator for Health Information Technology. (2025). Interoperability. HealthIT.gov. https://www.healthit.gov/topic/interoperability

---
Author: Elvis Jones, Senior Solutions Architect for Clinical AI at an academic medical center.
Doctoral candidate in big data analytics at Colorado Technical University.
LinkedIn: https://www.linkedin.com/in/elvis-jones-mba-pmp/
GitHub: https://github.com/AriesEmber
