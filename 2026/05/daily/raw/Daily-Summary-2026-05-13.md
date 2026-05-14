# Daily Summary of Tuesday 2026-05-13

---

## Scope

2026-05-13. Processed: 4 meeting transcripts, 4 markdown notes.

---

## Activities

- Implementation and deployed solutions huddle (09:00-09:31):
  - A colleague presented a financial management framework for evaluating deployed automations, including NPV, ROI, and payback period calculations.
  - Reviewed cost models for four production automations, with cost allocations across implementation and steady-state phases.
  - Discussed a strategic scorecard for hospital-facing impact, still under development.
  - Examined tool costs (inference costs) as a significant driver, with one automation showing high costs due to model selection.
  - Discussed whether AI-specific ROI analysis creates unfair scrutiny compared to non-AI clinical decision support tools.
  - Reviewed a low-value lab automation where alert rate was 2% versus an expected 10%, traced to threshold calibration differences.

- Explorations huddle (11:00-12:00):
  - Walked through a product requirements document for a referral intake and triage automation project.
  - Project scope covers approximately 470,000 referrals annually across 15 service lines.
  - Key metric is time between referral and scheduling, currently averaging 12 days.
  - Discussed difference between destination service lines (strategic investments) and other service lines.
  - Reviewed existing vendor alternative which only covers inbound messages and clinician-facing workflows, not administrative staff workflows.
  - Debated whether the automation should only provide information or also take actions (move referrals to scheduling queue).
  - Identified data profiling questions: what percentage of external referrals have internal data to generate meaningful summaries.

- Weekly data science lunch and check-in (12:00-12:58):
  - Presentation on the FHIR data store and underlying platform framework.
  - Platform processes approximately 22 to 25 million messages per day through the enterprise service bus.
  - Team pivoted from CCD-based data loading to a FHIR-first approach after identifying CCD limitations.
  - Pilot validation of 10 patients completed; moving to 1,000 patient validation next.
  - Discussed triggers for patient data loading: hospital admissions, ED admissions, and two-week appointment lookback.
  - Reviewed Care Everywhere data exchange limitations for external patients.
  - Platform uses object database technology with read-optimized caching for performance.

- Implementation partner onboarding session (13:00-15:00):
  - A colleague demonstrated a consolidated repository containing platform infrastructure and application components.
  - Repository includes Terraform definitions, UI with backend-for-frontend pattern, FHIR orchestrator (container and serverless versions), LLM gateway configuration, and pipeline orchestration.
  - Team is migrating automations from serverless functions to container apps to support long-running executions.
  - Discussed data statistics: average 1,500 tokens per patient, with 90% of referral data from external PDFs.
  - Coordinating GitHub access to push repository to external partner.
  - Discussed how Databricks notebook configuration files will be customer and site-specific.
  - Reviewed differences between automations that call LLM directly versus those requiring FHIR data orchestration first.

---

## Topics Discussed

- Financial modeling for AI automation ROI, including cost allocation across platform and individual automations.
- Strategic scorecard development for measuring hospital-facing impact beyond pure financial returns.
- Referral intake automation project requirements and architectural approach for multi-service-line deployment.
- Data availability for external referrals and whether internal EHR data exists to generate clinical summaries.
- FHIR store architecture and transition from CCD-based to FHIR-first data loading strategy.
- Platform infrastructure consolidation for handoff to external implementation partner.
- Container app migration strategy for automations requiring long-running execution.

---

## Decisions and Outcomes

- Financial framework: Near-final cost models completed for four automations; three recommended for expansion, one flagged for strategic scoring review. Owner: a colleague from the implementation team.
- Low-value lab automation: Will adjust thresholds based on clinically validated stability definitions. Owner: data science team.
- Referral automation project: Will proceed with data profiling to answer percentage questions before finalizing scope. Owner: data science team.
- FHIR store: Proceeding with 1,000 patient validation using FHIR-first approach. Owner: platform team.
- Repository handoff: External partner to provide GitHub organization access for repository push. Owner: engineering lead.

---

## Open Items

- Thresholds for the strategic scorecard (expand, enhance, monitor, retire) are not yet defined.
- Whether referral automation should take actions (move to scheduling queue) or only provide recommendations is unresolved.
- What percentage of external referrals have matching internal patient data is unknown; requires data profiling query.
- Whether Care Everywhere data requests can be automated or require human consent action remains unclear.
- FHIR store evaluation results from 10-patient pilot show discrepancies that need review before scaling.

---

## Possible Follow-Ups

- Run data profiling query on recent referrals to determine what percentage have internal EHR data matching the referral reason.
- Review FHIR store pilot evaluation results with platform team to understand discrepancy sources before 1,000 patient expansion.
- Investigate Care Everywhere consent workflow to determine if pre-arrival data fetch can be automated for transfer center patients.
- Document the financial framework methodology for future use by other teams evaluating automation investments.

---

## Source Index

- Source 1 (2026-05-13, 09:00-09:31): Implementation team weekly huddle transcript with presentation on automation financial modeling.
- Source 2 (2026-05-13, 11:00-12:00): Explorations team huddle transcript with PRD walkthrough for referral automation.
- Source 3 (2026-05-13, 12:00-12:58): Data science lunch meeting transcript with FHIR store and platform presentation.
- Source 4 (2026-05-13, 13:00-15:00): Implementation partner onboarding session transcript with repository walkthrough.
