# Field Note: Platform Maturity Assessment Without a Finish Line (2026-05-15)

The central tension on Friday was how to measure success for foundational data platform work that has no defined end state. Enterprise architecture stakeholders asked for quantitative goals, but the platform team operates in a mode where the outcome is capability, not delivery. The capability maturity model framing (manual, repeatable, standardized, automated, autonomous) surfaced repeatedly as a potential measurement instrument.

## The Work

### Measuring What Cannot End

The morning began with an enterprise architecture review follow-up focused on success metrics. A stakeholder pressed for quantitative targets rather than qualitative SLAs. The team identified one concrete number: cost savings from retiring an external analytics vendor. That metric has the virtue of being measurable but says nothing about platform capability itself.

The manager check-in afterward explored why traditional project metrics fail here. The initiative does not fit project structures with fixed end dates; a senior stakeholder advocated treating it as a program. The DAMA-DMBOK, the globally recognized framework for data management published by DAMA International, addresses this gap by framing data management as ongoing governance and practice rather than a one-time deliverable (DAMA International, 2017). The Microsoft Cloud Adoption Framework similarly positions cloud governance as "a continuous process" requiring "ongoing monitoring, evaluation, and updates to adapt to new technologies, evolving risks, and changing requirements" (Microsoft, 2025). Platform initiatives inherit that continuous character.

### Connector Strategy and Compliance Gates

The scrum of scrums covered multiple connector decisions. Google Ads connector remains in beta with HIPAA compliance expected at GA on 2026-07-31. Marketing must confirm the absence of PHI before pilot enablement. Workday connector options remain open pending a joint technical meeting to clarify whether data sharing or API integration is the appropriate pattern.

The Databricks Unity Catalog documentation describes this exact challenge: organizations must choose between managed governance (where the platform controls both access and storage lifecycle) and external governance (where the platform controls permissions only) depending on source characteristics (Databricks, 2025). The connector decisions reflect that choice point.

Excel plugin was confirmed HIPAA compliant. The decision to approve it for "limited tactical use" reflects a pattern seen throughout the day: governance gates that distinguish pilot, tactical, and production access tiers.

### Security Patterns and Marketplace Governance

Delta Sharing and catalog federation were discussed as mechanisms to segregate restricted datasets. Row-level security using identity passthrough was confirmed for the new platform. A data marketplace concept was introduced for accessing public and partner datasets, but governance process for external data access is not yet defined.

The Office of the National Coordinator for Health Information Technology (ONC) provides the authoritative backdrop here: the USCDI standard establishes "a standardized set of health data classes and constituent data elements" required for health information exchange (ONC, 2025). The information blocking regulations under the 21st Century Cures Act further require healthcare actors to avoid practices "likely to interfere with the access, exchange, or use of electronic health information" (ONC, 2025). Platform design must navigate between open data sharing mandates and security requirements.

### Research Platform Integrations

The afternoon research platform discussion identified four critical integrations: identity attributes API, protocol management system, research administration system, and survey tool. Future integrations include clinical trials management, service ticketing, and contract e-signature. Technical documentation of hosting locations, data types, and requirements was assigned in preparation for architecture review board submission.

The identity discussion connects to a scheduled Wednesday meeting with the school of medicine and affiliated university. Full platform access patterns depend on that conversation.

## Patterns and Frameworks

The capability maturity model referenced in the morning discussion (manual, repeatable, standardized, automated, autonomous) echoes the Software Engineering Institute's CMMI framework, though applied to data operations rather than software development. The DAMA-DMBOK provides a more domain-appropriate lens, framing maturity through data governance, integration, and interoperability functions. The Microsoft Cloud Adoption Framework offers a RACI matrix approach for clarifying accountability: the cloud governance team is accountable for policy development while platform and workload teams are responsible for implementation (Microsoft, 2025).

The NIST Cybersecurity Framework (CSF 2.0) provides a parallel maturity model for security domains, with tiers progressing from Partial to Risk Informed to Repeatable to Adaptive (NIST, 2024). These frameworks share a common insight: maturity is measured by the repeatability and adaptiveness of process, not by the completion of deliverables.

## Decisions and Open Items

**Decisions:**
- Architecture review board presentation scheduled for 2026-05-28
- Google Ads connector approved for pilot pending PHI confirmation; HIPAA workloads await GA
- Excel plugin confirmed HIPAA compliant for limited tactical use
- AI coding tool access approved via Kubernetes-hosted solution
- Marketing vendor technical discovery meeting to be scheduled

**Open items:**
- Identity management discussion with school of medicine scheduled for next Wednesday
- Workday connector decision pending joint technical meeting
- Data catalog tool (Purview) paused pending vendor conversations
- Single pane of glass test and production environments not yet provisioned
- CDC log retention for financial data source requires follow-up
- Provider location master does not exist in standardized form
- Data marketplace governance process not yet defined

## What I'm Taking Forward

The capability maturity model framing offers a path forward for measuring platform progress, but the team has not yet operationalized it into specific assessment criteria. The architecture review board presentation on 2026-05-28 may force that conversation.

## Further Reading

1. DAMA International. (2017). *DAMA-DMBOK: Data management body of knowledge* (2nd ed.). Technics Publications. https://www.dama.org/cpages/body-of-knowledge

2. Databricks. (2025). *Unity Catalog*. Databricks Documentation. https://docs.databricks.com/en/data-governance/unity-catalog/index.html

3. Microsoft. (2025). *Build a cloud governance team*. Azure Cloud Adoption Framework. https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/govern/build-cloud-governance-team

4. National Institute of Standards and Technology. (2024). *Cybersecurity framework (CSF 2.0)*. https://www.nist.gov/cyberframework

5. Office of the National Coordinator for Health Information Technology. (2025). *Interoperability*. HealthIT.gov. https://www.healthit.gov/topic/interoperability

---
Author: Elvis Jones, Senior Solutions Architect for Clinical AI at an academic medical center.
Doctoral candidate in big data analytics at Colorado Technical University.
LinkedIn: https://www.linkedin.com/in/elvis-jones-mba-pmp/
GitHub: https://github.com/AriesEmber
