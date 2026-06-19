---
name: Connector Content Workflow
description: Plan, write, and review a new connector documentation set using the connector-content-orchestrator agent
argument-hint: Connector name and source doc paths
agent: connector-content-orchestrator
---

Run the connector content workflow for this repository.

Use the slash-command argument as the initial request and then collect or confirm the required inputs.

Required inputs:
- Source material path(s) or links
- Connector name

Execution requirements:
1. Run planner first and produce `.docops/connector-content-plan.md`.
2. Pause for approval of the plan summary before writing.
3. Run writer to execute approved changes.
4. Run reviewer and iterate fixes until result is Pass or Pass with Info-only warnings.
5. Stop after 3 review-revision cycles and surface unresolved blockers.

Final response format:
- Files created
- Files deleted
- Files modified
- TOC updates
- Redirection updates
- Review result
- Remaining `{TODO: ...}` placeholders
- Suggested next steps
