# Field Note: Financial Modeling and FHIR-First Architecture for Clinical AI (2026-05-13)

The day centered on two architectural tensions. The first: how to evaluate whether clinical AI automations merit continued investment when traditional ROI models may create unfair scrutiny compared to non-AI clinical decision support. The second: the transition from CCD-based data loading to a FHIR-first approach for a platform processing 22 to 25 million messages daily, with implications for an external partner handoff.

## The Work

### Financial Frameworks for AI Automation

The morning huddle examined a financial management framework for evaluating deployed automations. The framework calculates NPV, ROI, and payback period for four production automations, with cost allocations across implementation and steady-state phases. Three were recommended for expansion; one was flagged for strategic scoring review.

A key discussion emerged around whether AI-specific ROI analysis creates unfair scrutiny. Traditional clinical decision support tools rarely face the same granular cost attribution that AI automations receive. The question of evaluation equity is not unique to this organization. JAMIA recently published research on "Translating innovation into payment: A.I. reimbursement in U.S. health care," examining how existing payment models struggle to account for AI's value contribution (Colicchio et al., 2025). The broader pattern is that AI tools face measurement burdens that preceding technologies avoided.

Tool costs (inference costs) emerged as a significant driver, with one automation showing high costs due to model selection. A separate low-value lab automation showed alert rates of 2% versus an expected 10%, traced to threshold calibration differences. The team will adjust thresholds based on clinically validated stability definitions.

### FHIR-First Data Architecture

The data science lunch presentation covered a FHIR data store and underlying platform framework. The team pivoted from CCD-based data loading to a FHIR-first approach after identifying CCD limitations. This aligns with HL7's design philosophy for FHIR: composition over constraint, where resources combine through references rather than constraining a complex universal model (HL7 International, 2024). The 80/20 rule embedded in FHIR's design, building a base resource set satisfying the majority of common use cases with extension mechanisms for the rest, maps directly to the flexibility requirements the platform encountered.

The platform processes approximately 22 to 25 million messages per day through the enterprise service bus. Pilot validation of 10 patients was completed; the team is moving to 1,000 patient validation. Patient data loading triggers on hospital admissions, ED admissions, and a two-week appointment lookback. Care Everywhere data exchange limitations for external patients remain a constraint.

The US Core Implementation Guide v8.0.1 defines mandatory and Must Support data elements for US Realm FHIR implementation, with profiles mapped to the U.S. Core Data for Interoperability (USCDI) standards (HL7 US Realm Steering Committee, 2025). The platform's FHIR-first pivot positions it for compliance with these requirements.

### Platform Consolidation for Partner Handoff

The afternoon onboarding session demonstrated a consolidated repository containing platform infrastructure and application components. The repository includes Terraform definitions, UI with backend-for-frontend pattern, FHIR orchestrator in both container and serverless versions, LLM gateway configuration, and pipeline orchestration.

The team is migrating automations from serverless functions to container apps to support long-running executions. Data statistics showed an average of 1,500 tokens per patient, with 90% of referral data originating from external PDFs. The external partner will receive GitHub access to push the repository. Databricks notebook configuration files will be customer and site-specific.

The referral intake automation project scope covers approximately 470,000 referrals annually across 15 service lines. The key metric is time between referral and scheduling, currently averaging 12 days. Whether the automation should only provide information or also take actions (moving referrals to the scheduling queue) remains unresolved.

## Patterns and Frameworks

The financial modeling work connects to broader challenges in AI implementation economics. The NIST AI Risk Management Framework provides governance guidance for managing AI-associated risks to individuals, organizations, and society (NIST, 2024). However, NIST's framework addresses risk management rather than value attribution, which is the gap the team's strategic scorecard attempts to fill.

For the FHIR architecture, the HL7 specification's support for multiple exchange paradigms (REST APIs and beyond) and backward compatibility with HL7 RIM (without requiring implementers to have intimate knowledge of the RIM) provided the flexibility needed for the platform's transition (HL7 International, 2024).

## Decisions and Open Items

**Decisions:**
- Financial framework: Near-final cost models completed for four automations; three recommended for expansion, one flagged for strategic scoring review.
- Low-value lab automation: Will adjust thresholds based on clinically validated stability definitions.
- Referral automation project: Will proceed with data profiling before finalizing scope.
- FHIR store: Proceeding with 1,000 patient validation using FHIR-first approach.
- Repository handoff: External partner to provide GitHub organization access for repository push.

**Open Items:**
- Thresholds for the strategic scorecard (expand, enhance, monitor, retire) are not yet defined.
- Whether referral automation should take actions or only provide recommendations is unresolved.
- What percentage of external referrals have matching internal patient data is unknown.
- Whether Care Everywhere data requests can be automated or require human consent action remains unclear.
- FHIR store pilot evaluation discrepancies need review before scaling.

## What I'm Taking Forward

The tension between evaluation equity for AI versus non-AI clinical tools, and whether the financial framework methodology can be documented for broader adoption across teams.

## Further Reading

1. Colicchio, T. K., et al. (2025). Translating innovation into payment: A.I. reimbursement in U.S. health care. *Journal of the American Medical Informatics Association*. https://academic.oup.com/jamia

2. HL7 International. (2024). FHIR overview. https://www.hl7.org/fhir/overview.html

3. HL7 US Realm Steering Committee. (2025). US Core Implementation Guide v8.0.1. https://hl7.org/fhir/us/core/

4. National Institute of Standards and Technology. (2024). AI Risk Management Framework. https://www.nist.gov/artificial-intelligence

---
Author: Elvis Jones, Senior Solutions Architect for Clinical AI at an academic medical center.
Doctoral candidate in big data analytics at Colorado Technical University.
LinkedIn: https://www.linkedin.com/in/elvis-jones-mba-pmp/
GitHub: https://github.com/AriesEmber
