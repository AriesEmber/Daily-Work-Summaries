# Summary of Tuesday 2026-05-06

---

## Scope

2026-05-06. Processed: 8 meeting transcripts, 4 supplementary notes files.

---

## Activities

- Implementation team huddle (09:00-09:25):
  - Brief check-in on implementations and deployed solutions status.

- Consultant orientation call (09:30-10:00):
  - Met with a consultant who will help manage the external vendor onboarding process for a clinical AI product.
  - Clarified that the consultant is not starting a spin-off company but rather contracting through a consulting firm to assist the team.
  - The healthcare organization is forming a new company to license and commercialize internally developed clinical AI products.
  - A third-party vendor won the RFP and will serve as the implementation arm for productization.
  - Knowledge transfer sessions scheduled to begin Friday and continue over approximately 10 weeks.
  - The Friday session will include introductions, document repository overview, and architecture orientation.

- DevOps collaboration monthly session (10:00-11:00):
  - Discussed PTU (provisioned throughput units) management; deleted unused PTUs and secured allocations for a newer model version.
  - A model version showed a 70% failure rate in testing; assigned a team member to investigate.
  - New network subnets have been provisioned; the production VNet still needs finalization on whether to connect to the analytics backend.
  - Staging VNet is not provisioned yet; team members are working on it pending security approval.
  - Owner access to a subscription was silently removed; a request was submitted to restore it, requiring a written justification.
  - Target timeline: have engineers start migrating workloads to the new environment by month three to align with the new fiscal year.
  - Discussed serverless functions (Azure Function Apps) being outside current infrastructure-as-code scope; plan to codify them once new environments are ready.
  - Proposed locking data science team out of production portal access to enforce infrastructure-as-code discipline; decision deferred until environments are promoted to production.
  - Identified need for an Azure Monitor workspace for App Insights dashboards.

- Explorations huddle (11:00-11:45):
  - Reviewed two product initiatives (a referral automation tool and a patient routing tool).
  - Data scientists reported difficulty understanding the problem statement and scope for both products.
  - Product manager needs to consolidate slide decks and product requirements documents.
  - For the referral tool: the goal is to build a solution that works across 15 service lines using an 80/20 approach rather than custom solutions per service line.
  - Need 20-30 examples per service line to design prompts and evaluate accuracy.
  - For the patient routing tool: the workflow differs across sites; need to understand current processes before determining if a single technical solution can serve all use cases.
  - Discussed automation enhancement deployment challenges: breaking changes exist in code but no clear path to promote them to production.
  - Current CI/CD pipeline deploys to staging environments that do not reflect production data.
  - Proposed a "silent deployment" process where new logic runs in parallel without writing results to the production system.
  - Action items: design a shadow environment, create a runbook for silent deployments, and update CI/CD pipelines.

- Team all-hands ad hoc session (11:51-13:00):
  - Senior leadership provided context on a new commercialization entity being formed by the healthcare organization.
  - The entity will license IP for clinical AI products and other innovations.
  - The implementation vendor is a healthcare-focused technical firm that won an RFP process.
  - The commercialization entity is still being formed; currently hiring a CTO and evaluating a CEO position.
  - Rationale: create a sustainable funding mechanism for technology innovation as hospital margins face pressure.
  - Leadership emphasized this is a dissemination mechanism, not a venture-backed startup.
  - The team's primary focus remains hospital production deployments; external commercialization is a one-way handoff.
  - Knowledge transfer is expected to be time-limited (approximately six hours of documented content).

- Research informatics technical meeting (14:00-14:30):
  - Reviewed RAG (retrieval-augmented generation) implementation for a research support chatbot.
  - The system uses a vector database with both sparse and dense embeddings.
  - A SharePoint-based content approval workflow automatically ingests approved documents into the RAG pipeline daily.
  - Adding a UAT namespace to allow content testing before promotion to production.
  - Updated infrastructure to support the centralized AI hub API changes and project-specific token provisioning.
  - Demonstrated agentic capabilities allowing the chatbot to execute research platform API calls within guardrails.
  - Memory compaction summarizes conversation context when it exceeds token limits.
  - Discussed whether to use native cloud tooling versus third-party vector database; current choice was based on low startup cost.
  - Suggested considering embedding on the fly or MapReduce-style chunking as alternatives to RAG for some use cases.
  - The team may move toward a standalone application rather than embedding functionality in the research platform.

- Transfusion project touchpoint (14:30-15:00):
  - No substantive content recorded in transcript.

- Architecture leadership meeting (15:00-16:00):
  - Shared context on the clinical AI commercialization initiative with the architecture team.
  - Clarified that the consulting firm engaged is a facilitator, not the owner of the spin-off entity.
  - The healthcare organization will own the commercialization entity; it will license IP and work with implementation partners.
  - Discussed cross-training opportunities for solution architects across portfolios.
  - Reviewed a six-step architecture value chain framework: ideate and explore, define and assess, decide and evaluate, design and realize, enable and manage, plan and institutionalize.
  - The goal is to shift architecture engagement earlier into ideation rather than focusing primarily on governance gates.
  - A senior leader is restructuring teams around business capabilities; architecture wants to be prepared for that shift.
  - Discussed establishing a formal ideation process; may partner with clinical informatics who already work in the ideation space.
  - Feedback: strategy development should be shown as an input to ideation rather than a separate final step; need to show mapping between steps.
  - Proposed pre-approved architecture patterns and configurations to enable proportional governance and self-service.

---

## Topics discussed

- Clinical AI product commercialization: A new entity is being formed to license and productize internally developed clinical AI solutions, with a third-party vendor serving as the implementation arm.
- Cloud infrastructure migration: New Azure environments are being provisioned with a target of starting workload migration in three months to align with the new fiscal year.
- PTU and model provisioning: Managed provisioned throughput units for LLM APIs; identified a failure issue with a newer model version.
- Enhancement deployment process: Current CI/CD pipelines do not support safe testing of breaking changes; a silent deployment pattern is needed.
- Referral automation scope: Aiming for an 80/20 solution that works across 15 service lines rather than bespoke solutions per service line.
- Patient routing tool requirements: The product scope is unclear; different sites have different workflows and criteria needs.
- RAG vs. alternative approaches: Discussed embedding on the fly and MapReduce-style chunking as alternatives to retrieval-augmented generation.
- Architecture value chain: A six-step lifecycle framework to shift architecture engagement toward ideation and away from governance focus.
- Ideation process development: Need to establish a formal ideation process in partnership with clinical informatics.
- Cross-training for architects: Exploring opportunities to rotate solution architects across portfolios to broaden experience.

---

## Decisions and outcomes

- PTU allocation: Secured provisioned throughput for a newer model version in both east and west regions. Owner: platform team.
- Subscription owner access: Request submitted to restore owner access; written justification required. Owner: DevOps lead.
- Friday knowledge transfer agenda: Will include introductions, document repository orientation, and architecture overview. Owner: solution architect.
- Enhancement deployment: Will design a silent deployment process and present proposal to integration team. Owner: data science team.
- Architecture value chain: Will iterate on the framework and present to senior leadership. Owner: architecture lead.

---

## Open items

- Model failure investigation: A newer model version is showing 70% failure rate; root cause under investigation.
- Staging VNet provisioning: Pending security approval; timeline unclear.
- Product requirements clarity: Data scientists still need consolidated requirements documents for both the referral tool and patient routing tool.
- Serverless function codification: Deferred until new environments are ready.
- Ideation process: Senior leader and architecture lead will collaborate on defining the process, but timeline not set.
- Research chatbot architecture: Decision pending on whether to build as standalone application or continue embedding in research platform.

---

## Possible follow-ups

- Schedule a working session to design the silent deployment process and shadow environment for automation enhancements.
- Request consolidated product requirements documents from the product manager for the referral and patient routing tools.
- Document the MapReduce-style chunking approach used by the data science team for potential application to the research chatbot.
- Follow up with clinical informatics about their ideation process and potential partnership.

---

## Source index

- Source 1 (2026-05-06, 09:00-09:25): Implementation team huddle meeting transcript.
- Source 2 (2026-05-06, 09:30-10:00): One-on-one consultant orientation meeting transcript and notes.
- Source 3 (2026-05-06, 10:00-11:00): DevOps collaboration monthly session transcript and notes.
- Source 4 (2026-05-06, 11:00-11:45): Explorations huddle meeting transcript and notes.
- Source 5 (2026-05-06, 11:51-13:00): Ad hoc team all-hands session transcript.
- Source 6 (2026-05-06, 14:00-14:30): Research informatics technical meeting transcript.
- Source 7 (2026-05-06, 14:30-15:00): Transfusion project touchpoint meeting metadata.
- Source 8 (2026-05-06, 15:00-16:00): Architecture leadership meeting transcript and notes.
