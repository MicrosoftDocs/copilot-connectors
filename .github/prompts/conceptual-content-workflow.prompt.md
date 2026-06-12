---
name: Conceptual Content Workflow
description: Plan, write, and review conceptual documentation updates using the conceptual-content-orchestrator agent
argument-hint: Scope, target files/folders, and source doc paths
agent: conceptual-content-orchestrator
---

Run the conceptual content workflow for this repository.

Use the slash-command argument as the initial request and then collect or confirm the required inputs.

Required inputs:
- Source material path(s) or links
- Work scope (create, update, or both)
- Target scope (files/folders/topics)

Execution requirements:
1. Run planner first and produce `.docops/conceptual-content-plan.md`.
2. Pause for approval of the plan summary before writing.
3. Run writer to execute approved changes.
4. Run reviewer and iterate fixes until result is Pass or Pass with Info-only warnings.
5. Stop after 3 review-revision cycles and surface unresolved blockers.

Final response format:
- Files created
- Files modified
- TOC/navigation updates
- Review result
- Remaining `{TODO: ...}` placeholders
- Suggested next steps
