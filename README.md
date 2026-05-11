# Daily Work Summaries

A public work journal by **Elvis Jones**, Senior Solutions Architect for Clinical AI at an academic medical center. Doctoral candidate in big data analytics and quantum computing at Colorado Technical University.

This repository documents the day-to-day reality of designing, governing, and shipping AI and machine learning systems inside a regulated clinical healthcare environment. Architecture decisions, vendor evaluations, governance reviews, retrieval and LLM evaluation work, and the ambiguous middle of building production AI in a hospital setting.

## About the Author

Elvis Jones is a Senior Solutions Architect focused on clinical AI infrastructure at an academic medical center. His work spans:

- Clinical AI platform architecture on Azure
- LLM evaluation and classification in EHR settings, including GPT-4o and Claude model families
- AI governance, safety, and compliance in HIPAA-regulated environments
- Retrieval architectures for clinical knowledge, including engram-inspired patterns and VaultRAG-style systems
- Quantum computing for healthcare classification problems (dissertation work, including amplitude amplification and variational quantum classifiers)
- Crossover background: U.S. Army EOD, government chemical munitions disposal, AI safety

Other surfaces:

- LinkedIn: https://www.linkedin.com/in/elvisjones/
- Personal site: forthcoming
- ORCID: forthcoming
- arXiv author page: forthcoming

## What This Repository Is

A daily journal of architecture work in clinical AI. Each entry captures a single business day and includes:

- **Activities.** Meetings, technical discussions, code reviews, architecture sessions, vendor calls.
- **Topics discussed.** Subjects examined that day with enough context to be readable on their own.
- **Decisions and outcomes.** What was decided, what is owned by whom, and what the rationale was.
- **Open items.** Unresolved questions and blockers carried forward.
- **Follow-ups.** Action items, research threads, and references worth pursuing.
- **Lessons learned.** Patterns, insights, and observations distilled from the day.

Entries publish daily on business days, with a weekly synthesis on Mondays.

## Topics Covered

The recurring subject matter of this journal:

**Clinical AI infrastructure.** Designing AI platforms that meet the operational, security, and compliance requirements of an academic medical center. Tradeoffs between managed services, self-hosted infrastructure, and hybrid patterns. Reference architectures for Azure-based clinical AI deployments.

**LLM evaluation in healthcare.** Classification, summarization, and retrieval tasks against clinical text. Eval design, ground truth curation, and the practical realities of measuring model performance on protected health information. Comparative work across GPT, Claude, and open-weight model families.

**AI governance in regulated environments.** What governance actually looks like when you have to ship. Risk frameworks, model approval workflows, audit and observability requirements, the interaction between IRB review and engineering velocity, and the gap between published responsible-AI principles and production reality.

**Retrieval and knowledge architectures.** Patterns for clinical knowledge retrieval, including hierarchical retrieval, hybrid search, and emerging approaches inspired by biological memory systems. Notes on engram-style retrieval, VaultRAG-style content stores, and the engineering required to make retrieval defensible in clinical contexts.

**Vendor and platform evaluation.** Notes from real vendor evaluations: Anthropic Enterprise, Microsoft Copilot variants, Databricks, AWS healthcare offerings, and the surrounding tooling ecosystem. What works, what does not, what the contracts actually say.

**Quantum computing for classification.** Dissertation-track work on amplitude amplification, variational quantum classifiers, and the question of where quantum methods earn their place in healthcare data analytics.

**AI safety in high-stakes settings.** Practical safety considerations when AI systems touch clinical workflows. Crossover lessons from a prior career in explosive ordnance disposal and chemical munitions handling.

## Why This Is Public

Healthcare AI is a field where the problems are complex, the stakes are high, best practices are still emerging, and very few practitioners write publicly about the day-to-day reality. Most public material is either polished conference talks or curated LinkedIn posts. This journal sits in the gap. It is the unedited middle: the ambiguous requirements, the vendor negotiations, the governance reviews, the debugging sessions, the architectural tradeoffs that never appear in case studies.

The intended readers are other architects, engineers, and AI practitioners working in healthcare and other regulated industries. If the problems you face are like the ones documented here, the journal is meant to be useful to you.

## What This Is Not

All content is sanitized before publication. The repository contains no:

- Names of colleagues, managers, or stakeholders
- Company, hospital, or health system names
- Proprietary project names or internal codenames
- Internal URLs, ticket numbers, or system identifiers
- PHI, PII, or anything that could identify a patient

Resemblance to specific organizations or individuals is coincidental.

## Contact

If you work in clinical AI, healthcare IT, AI governance, or enterprise machine learning and want to discuss anything you see here, reach out via LinkedIn.

## Disclaimer

These summaries are a personal work journal and reflect the author's observations only. They do not represent the views, policies, or positions of any employer. All identifying information has been removed.
