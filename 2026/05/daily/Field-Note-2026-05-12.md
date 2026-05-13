# Field Note: Enterprise Data Platform Architecture and the Lakehouse Question (2026-05-12)

The central tension of the day was how to define success for an enterprise data platform when the architecture itself is still conceptual. Three meetings converged on platform design patterns: a lakehouse-based federation model presented to the enterprise architecture board, a research enclave provisioning workflow, and a fast-pass governance framework proposed to accelerate architecture engagement. Each thread raised the same question in different form: how do you measure value when the capability is the asset?

## The Work

The enterprise architecture review session centered on a next-generation data platform proposal built around multi-cloud federation using a lakehouse pattern. The conceptual architecture combines analytical and operational workloads in a unified storage layer, following the model documented by Armbrust et al. (2021) in which data lakes gain transactional guarantees and schema enforcement without sacrificing support for unstructured data or machine learning workloads. The review identified a gap: the project charter remains unsigned, and the enterprise architecture board cannot complete its evaluation without that formalization.

A related discussion addressed research enclave provisioning. The architecture team walked through three workflow diagrams covering consumer onboarding, usage lifecycle, and internal asset development. The enclave model aligns with Dehghani's (2022) data mesh principle of domain-oriented decentralized ownership, where research teams would manage their own analytical data products within a self-serve infrastructure platform. The group agreed to add an explicit definition of the data enclave concept to architecture documentation, recognizing that the term carries different meanings across stakeholder groups.

### Architecture Team Engagement

The afternoon working session surfaced a recurring challenge: solution architecture teams engage projects too late to influence design decisions. The proposal was a fast-pass framework that incentivizes early engagement by offering expedited review for projects that involve architecture teams during ideation. This pattern mirrors the governance principle of shifting architectural decisions left in the delivery lifecycle, though the execution plan and metrics remain undefined.

The same session addressed medical device reference architecture for laboratory analyzers. Compliance challenges with embedded operating systems and vendor-managed firmware led to a proposed umbrella exception approach for device security standards. The goal is faster governance without per-device security reviews for equipment classes that share common risk profiles.

### Clinical AI Adoption

The morning roadmap sync reviewed adoption metrics for an AI clinical assistant, now at 2,671 activated users. User feedback themes included missing structured data (flow sheets, vital signs) and recency errors, both tied to the underlying data retrieval architecture rather than the model itself. A recent model update introduced downstream impacts requiring prompt conversion support, a reminder that model versioning creates maintenance burden across dependent systems.

## Patterns and Frameworks

The lakehouse architecture pattern, as defined by Lorica et al. (2020) and formalized by Armbrust et al. (2021) at CIDR, provides the conceptual foundation for the proposed data platform. The pattern combines eight capabilities: ACID transactions, schema enforcement, direct BI integration, decoupled compute, open storage formats, support for diverse data types, multi-workload execution, and real-time streaming. The appeal for an academic medical center is the promise of a single platform supporting both research analytics and operational reporting.

Dehghani's (2022) data mesh principles offer a complementary lens for the enclave provisioning model. The self-serve data infrastructure concept maps directly to the proposed automated lifecycle management, where research teams provision and manage their own workspaces without centralized data engineering bottlenecks. The federated computational governance principle addresses the tension between domain autonomy and enterprise-wide interoperability standards.

## Decisions and Open Items

- Dashboard baseline: Target publishing adoption dashboard by end of next week after collecting team feedback by Monday. Owner: analytics lead.
- Drug lookup tool: Approved for pilot with administrative staff using cloud-based authentication. Owner: application team.
- Data platform review: Cannot complete until project charter is signed. Owner: project lead.
- Enclave definition: Add explicit definition of data enclave concept to architecture documentation. Owner: solution architect.
- Diagram standard: Architecture team will use a standardized initial deployment view format for reviews. Owner: architecture lead.

**Open:**
- Success metrics for data platform remain qualitative; quantitative measures need business stakeholder input.
- Automation pipeline error handling logic requires code review to address patient drop-off issue.
- Cross-affiliate access request workflow between separate service desk instances remains undefined.
- Fast-pass governance framework details not yet defined; execution plan and metrics pending.

## What I'm Taking Forward

The data platform review cannot proceed without a signed charter, but the architecture itself needs measurable success criteria before that charter will close. The question for tomorrow is whether the metrics conversation can happen in parallel or must sequence after charter approval.

## Further Reading

1. Armbrust, M., Ghodsi, A., Xin, R., & Zaharia, M. (2021). Lakehouse: A new generation of open platforms that unify data warehousing and advanced analytics. *Proceedings of the 11th Annual Conference on Innovative Data Systems Research (CIDR 2021)*. https://www.cidrdb.org/cidr2021/papers/cidr2021_paper17.pdf

2. Dehghani, Z. (2022). Data mesh principles and logical architecture. *martinfowler.com*. https://martinfowler.com/articles/data-mesh-principles.html

3. Lorica, B., Armbrust, M., Xin, R., Zaharia, M., & Ghodsi, A. (2020, January 30). What is a data lakehouse? *Databricks Blog*. https://www.databricks.com/blog/2020/01/30/what-is-a-data-lakehouse.html

---
Author: Elvis Jones, Senior Solutions Architect for Clinical AI at an academic medical center.
Doctoral candidate in big data analytics at Colorado Technical University.
LinkedIn: https://www.linkedin.com/in/elvis-jones-mba-pmp/
GitHub: https://github.com/AriesEmber
