# Field Note: Agentic Workflow Prototyping and Governance Calibration (2026-05-04)

The day centered on two parallel tracks: evaluating early approaches to agentic system design for emerging products, and calibrating the architecture governance process to match review complexity with review effort. Both tracks share a common thread of deciding when to add structure and when simplicity suffices.

## The Work

### Agentic Workflow Design Evaluation

A colleague proposed an approach to building an agentic workflow using a notebook environment with initial prompts and tool calls. The proposal warranted a second perspective, so a follow-up meeting was scheduled to gather alternative viewpoints on the design.

This question of how to structure agent development is not trivial. The pattern of using notebooks as prototyping environments for agent behavior aligns with what Anthropic's engineering guidance describes as "prompt chaining," where tasks decompose into sequential steps with each LLM call processing prior outputs (Anthropic, 2024). However, notebooks can obscure the boundary between experimentation and production architecture. The ReAct framework documented by Yao et al. (2022) demonstrates that interleaving reasoning traces with tool calls improves interpretability and reduces hallucination, which suggests that whatever prototyping environment is chosen, it should preserve visibility into the reasoning-action loop.

Two emerging products also surfaced as needing clearer infrastructure and architecture requirements. The products are early enough that their agentic components remain undefined, creating a dependency between product scoping and technical architecture decisions.

### Vendor Knowledge Transfer

A vendor knowledge transfer project required clarification on which code version is being handed off, as development continues in parallel. The vendor is technically strong but has a learning curve on healthcare data. A clarification email was agreed upon as the next step.

This is a common coordination problem: handing off a moving target. The risk is that the vendor builds against an outdated version while the internal team continues to evolve the codebase. The resolution path is straightforward (send the clarification email), but the underlying tension between parallel development and clean handoff boundaries will persist throughout the engagement.

### Architecture Governance Calibration

The architecture team discussed whether vendor assessments without controversial elements need peer review. The determination was that straightforward assessments can route directly to a senior colleague, while complex project reviews should go through the full team during collaboration sessions. This is governance calibration: matching review depth to actual risk.

A separate discussion addressed confusion around technical architecture diagram formats. A senior colleague will meet with security stakeholders to clarify requirements. Diagram format questions often mask deeper disagreements about what the diagram is meant to communicate and to whom.

Cross-training for enterprise architecture review activities was also discussed. Principal architects will shadow the enterprise architect, building institutional knowledge beyond a single point of expertise.

### Solution Design Finalization

A solo work session focused on finalizing a solution design document for a logical data platform project. The goals section was updated based on the finalized project charter, and workflow diagram edits were made including renaming process boxes. The document incorporates feedback from the prior week's stakeholder review.

## Patterns and Frameworks

The agentic workflow discussion connects to several documented patterns. Wang et al. (2023) provide a unified framework for constructing LLM-based autonomous agents, identifying three core components: profiling, memory, and action. The notebook-based approach under evaluation appears to focus primarily on the action component (tool calls) without yet addressing how the agent will maintain memory or be profiled for specific tasks.

Guo et al. (2024) extend this to multi-agent systems, documenting how communication mechanisms and growth capacities become critical as agent complexity increases. For early-stage prototyping, single-agent patterns may suffice, but the architecture should anticipate multi-agent coordination if the products scale.

Anthropic's guidance on agent-computer interface (ACI) design is particularly relevant: "Invest as much effort in agent-computer interfaces as human-computer interfaces. Write tool descriptions like docstrings for junior developers, including examples, edge cases, and clear boundaries" (Anthropic, 2024). This suggests that the quality of tool definitions in the notebook prototype will determine whether the approach can evolve into production architecture or will need to be rebuilt.

## Decisions and Open Items

**Decisions:**
- Clarification email to vendor contacts regarding code version scope (owner: self)
- Complex project reviews to use Tuesday team collaboration sessions (owner: team)
- Senior colleague to clarify diagram requirements with security stakeholders
- Principal architects to shadow enterprise architect for cross-training

**Open Items:**
- Code version for vendor handoff not yet defined
- Infrastructure and architecture requirements for two new products are unclear
- Vendor feedback on proposed design is pending
- Replacement vendor for end-of-life system not identified
- Portfolio intelligence initiative awaiting leadership availability

## What I'm Taking Forward

The agentic workflow evaluation needs a decision framework: when does notebook-based prototyping serve the architecture, and when does it create technical debt that a production implementation must absorb?

## Further Reading

1. Anthropic. (2024). *Building effective agents*. Anthropic Engineering. https://www.anthropic.com/engineering/building-effective-agents

2. Guo, T., Chen, X., Wang, Y., Chang, R., Pei, S., Chawla, N. V., Wiest, O., & Zhang, X. (2024). Large language model based multi-agents: A survey of progress and challenges. *arXiv preprint arXiv:2402.01680*. https://arxiv.org/abs/2402.01680

3. Wang, L., Ma, C., Feng, X., Zhang, Z., Yang, H., Zhang, J., Chen, Z., Tang, J., Chen, X., Lin, Y., Zhao, W. X., Wei, Z., & Wen, J.-R. (2023). A survey on large language model based autonomous agents. *arXiv preprint arXiv:2308.11432*. https://arxiv.org/abs/2308.11432

4. Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2022). ReAct: Synergizing reasoning and acting in language models. *arXiv preprint arXiv:2210.03629*. https://arxiv.org/abs/2210.03629

---
Author: Elvis Jones, Senior Solutions Architect for Clinical AI at an academic medical center.
Doctoral candidate in big data analytics at Colorado Technical University.
LinkedIn: https://www.linkedin.com/in/elvis-jones-mba-pmp/
GitHub: https://github.com/AriesEmber
