# Daily Summary of Wednesday 2026-05-07

## Scope

2026-05-07. Processed: 5 meeting transcripts, 5 meeting notes files.

---

## Activities

- **Solutions architecture review meeting (10:30-11:00):**
  - Kicked off architecture solutioning process for a marketing data platform initiative.
  - Introduced team members including the assigned solution architect, demand manager, PMO representative, and marketing stakeholders.
  - Clarified that the scope covers all phases of building a consolidated data space for the marketing team.
  - Confirmed the initiative will target the next-generation data platform (Databricks-based logical lakehouse) rather than the legacy enterprise data warehouse.
  - Reviewed the architecture review board process overview, including Enterprise Architecture Review prerequisites and required artifacts (project charter, BPMN diagrams, security review).
  - Discussed current interim access granted to marketing stakeholders through the existing data warehouse environment.
  - Identified a free Lakeflow Connector trial (expiring in June) for advertising platform data ingestion as a potential test case.
  - Agreed to establish a recurring meeting cadence for the project team.
  - Solution architect offered to draft BPMN workflow diagrams and assist with business process documentation.
  - A colleague shared access to a SharePoint repository containing data source lists and requirements documentation.

- **Architecture review board meeting (12:00-12:46):**
  - Reviewed and approved migration of a radiology workflow tracking system from physical servers to virtual machines in a new data center.
  - Noted the radiology system lacks Active Directory integration; waiver signed with remediation expected by March 2027.
  - The radiology system integrates with multiple clinical systems including the EHR shadow database via file share, patient data via HL7, and a vendor analytics platform.
  - Approved migration of 3D medical imaging software (two products for segmentation and mesh design) from the School of Medicine data center to the healthcare organization infrastructure.
  - Confirmed the 3D modeling solution supports FDA-cleared diagnostic workflows and serves surgical specialties including orthopedics, neurosurgery, and cardiothoracic surgery.
  - Noted storage requirements for 3D models are modest (under 500 GB with 30-day retention policy for PHI).
  - Reviewed and approved a pilot for autonomous medical coding software targeting radiology professional billing (approximately 625,000 coded accounts per year).
  - The autonomous coding solution uses LLM technology to process clinical documentation and return structured billing codes with expected 90% automation rate and 96% accuracy.
  - Noted the coding vendor is a startup founded through a university business school program; latest funding round was $46 million in November 2024.
  - Discussed that the EHR vendor has forthcoming similar capabilities, so the coding solution may be temporary.
  - All three solutions received board approval to proceed.

- **Agent approach review meeting (13:00-13:32):**
  - Discussed design approaches for a patient routing and screening system.
  - Reviewed concerns about exposing a clinical data orchestrator directly to an agent without prescriptive tool definitions.
  - A colleague shared that a previous tumor board project revealed the orchestrator was difficult for agents to use due to poor documentation; had to provide explicit calling instructions which defeats the purpose of using an agent.
  - Referenced a recent academic paper (PhysicianBench from a clinical informatics research lab) that demonstrates exposing individual FHIR APIs as separate tools rather than a monolithic orchestrator.
  - Agreed that tools given to agents should include prescriptive instructions and have scoped functionality (separate tools for notes, labs, orders rather than one universal data retrieval function).
  - Established a rough guideline of limiting agents to approximately 10 tools maximum, referencing emergency response span-of-control principles.
  - Discussed the tension between building flexible agent systems versus simpler prompt-based approaches that could achieve similar accuracy with less complexity.
  - If a prompt to the chat UI API achieves 90-95% accuracy, building a custom tool-calling architecture may not be justified.
  - Discussed evaluation challenges when routing criteria are user-configurable and subject to frequent change.
  - Proposed an opt-in/opt-out model for rigorous evaluation versus off-label use of AI tools.
  - Noted multiple product roadmaps exist across the team (five roadmaps managed by different people on a 12-person team), creating coordination challenges.
  - A colleague noted they are building a Python package to test different approaches for yes/no patient eligibility screening across multiple locations.
  - Discussed timeline: colleague transitioning back to clinical duties full-time around late October 2026 but hopes to stay on as a contractor part-time.

- **Architecture bi-weekly working session (15:00-15:05):**
  - Brief session with minimal substantive discussion captured.
  - Reference made to providing documentation for a different system.

- **Research administration architecture discussion (15:00-16:07):**
  - Initiated architecture design for a research study intake and management application.
  - Confirmed the previous prototype (built on a survey data capture tool) has outgrown its capabilities; team will build a standalone application.
  - A senior colleague was asked to lead the architecture design for this application.
  - Established target timeline: functional by October 2026 for testing, production rollout in January 2027.
  - Selected GCP as the initial cloud environment for rapid prototyping, with a design principle to use environment-agnostic tooling (Docker, Terraform) for future portability to other cloud providers.
  - Confirmed the application will handle PHI and PII, as well as high-risk budgetary and contract information; projects must be configured accordingly.
  - Discussed authentication requirements: university single sign-on as primary, with support needed for affiliated entities including a children's hospital.
  - Discussed workgroups versus authority manager for role-based access and delegation; authority manager is preferred but deferred to post-V1 phase.
  - Agreed on a three-tier environment structure: DEV, combined UAT/Stage, and Production.
  - Estimated Phase 1 scope at approximately 150 studies across 3 of 17 clinical research groups in oncology.
  - Total active studies across the organization estimated at approximately 2,000 at any given time; approximately 700 in cancer research alone.
  - Data retention varies by study protocol (some up to 10 years); no hard deletion requirements; plan to archive rather than delete.
  - Discussed starting with new studies only; migration path for in-flight studies remains undecided.
  - Discussed knowledge base content management: policy documents currently in SharePoint with an approval workflow before ingestion into the vector database.
  - Noted a colleague demonstrated a URL ingestion process that follows links in documents and indexes referenced content.
  - Decided agent configuration files (system prompts, tool definitions) should be managed through CI/CD pipelines rather than SharePoint for security and version control.
  - Discussed whether to use the central AI Hub (Azure-based) or native GCP models; decision deferred pending further exploration.
  - Confirmed weekly recurring meetings through early June.
  - Noted a hands-on session with the cloud vendor's AI team is scheduled for May 20, 2026.
  - Discussion of UI design testing: stakeholders want coordinator feedback but expressed concern the prototype is not ready; agreed to limit initial testing to two coordinators rather than six initially requested.
  - Concern raised that the design vendor may charge for a second round of testing if the first round feedback requires significant rework.

---

## Topics Discussed

- Marketing data platform consolidation and migration from legacy enterprise data warehouse to next-generation Databricks-based platform.
- Architecture review board solutioning process including required artifacts (project charter, BPMN diagrams, security review, architecture documentation).
- Radiology workflow system migration from physical to virtual servers with Active Directory remediation timeline.
- 3D medical imaging software standardization for surgical planning and anatomical modeling.
- Autonomous medical coding pilot using LLM technology for radiology professional billing with 90% automation rate target.
- Agentic system design patterns and tool exposure strategies for clinical AI applications.
- Comparison of monolithic orchestrator exposure versus scoped semantic tools for agent systems.
- Evaluation frameworks for AI systems with user-configurable criteria.
- Research administration application architecture including cloud environment selection, authentication, and deployment tiers.
- Knowledge base management and document ingestion workflows for AI-powered research guidance tools.
- CI/CD pipeline strategies for managing agent configuration and system prompts.
- UI testing readiness and vendor management for research application design.

---

## Decisions and Outcomes

- Marketing data platform: Will target next-generation data platform (Databricks), not legacy enterprise data warehouse. Owner: solution architect and demand manager.
- Marketing data platform: All phases will go through a single architecture review rather than separate reviews. Owner: solution architect.
- Marketing data platform: Recurring meeting cadence to be established. Owner: PMO representative.
- Architecture review board: Radiology workflow system migration approved. Owner: application owner.
- Architecture review board: 3D imaging software migration approved. Owner: application owner.
- Architecture review board: Autonomous coding pilot approved. Owner: revenue cycle team.
- Agent design: Tools should be scoped (separate tools for notes, labs, orders) rather than exposing monolithic orchestrators. Owner: unassigned.
- Agent design: Limit agents to approximately 10 tools maximum. Owner: unassigned.
- Research application: GCP selected as initial environment with environment-agnostic tooling principle. Owner: architecture team.
- Research application: Three-tier deployment structure (DEV, UAT/Stage, PRD). Owner: architecture team.
- Research application: Agent configuration managed through CI/CD, not SharePoint. Owner: architecture team.
- Research application: UI testing limited to two coordinators initially. Owner: project sponsors.
- Research application: Weekly meetings through early June. Owner: project sponsor.

---

## Open Items

- Marketing data platform: Signed project charter still needed as a required architecture review board artifact.
- Marketing data platform: Credentials needed to set up Lakeflow Connector trial for advertising platform data ingestion.
- Marketing data platform: Determine if the colleague leaving in two weeks will have a replacement for data operations support.
- Autonomous coding: Accuracy threshold of 95% required for production acceptance; validation pending.
- Autonomous coding: Model drift monitoring and retraining schedule not yet defined with vendor.
- Agent design: No clear decision on evaluation approach when criteria are user-configurable and frequently changing.
- Agent design: Product and evaluation roadmaps need alignment across multiple team roadmaps.
- Research application: Final decision pending on whether to use central AI Hub or native GCP models.
- Research application: Authority Manager integration deferred to post-V1 phase; team needs to learn this system.
- Research application: Migration path for in-flight studies remains undecided (question mark on backloading existing studies).
- Research application: Retention policy details vary by study; need confirmation on archival approach.

---

## Possible Follow-Ups

- Review the PhysicianBench paper and GitHub repository for patterns on exposing FHIR APIs as discrete agent tools.
- Follow up on Lakeflow Connector trial setup with marketing team once credentials are obtained.
- Request the agent platform comparison presentation from October 2025 for the research application team.
- Confirm attendance for the May 20 cloud vendor hands-on session on agent development.
- Clarify with product team the boundary between evaluated and off-label AI tool deployments.

---

## Source Index

- Source 1 (2026-05-07, 10:30-11:02): Solutions architecture review meeting transcript.
- Source 2 (2026-05-07, 10:30-11:02): Solutions architecture review meeting notes.
- Source 3 (2026-05-07, 12:00-12:46): Architecture review board meeting transcript.
- Source 4 (2026-05-07, 13:00-13:32): Agent approach review meeting transcript.
- Source 5 (2026-05-07, 13:00-13:32): Agent approach review meeting notes.
- Source 6 (2026-05-07, 15:00-15:05): Architecture bi-weekly working session transcript.
- Source 7 (2026-05-07, 15:00-16:07): Research administration architecture discussion transcript.
- Source 8 (2026-05-07, 15:00-16:07): Research administration architecture discussion notes.
