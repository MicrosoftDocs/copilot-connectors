---
title: "Galileo by The Josh Bersin Company connector overview"
ms.author: xupzhou
author: xupzhou
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 09/11/2026
ms.localizationpriority: Medium
description: "Learn how the Galileo by The Josh Bersin Company Microsoft 365 Copilot connector brings research-backed HR guidance into Microsoft 365 Copilot."
---

# Galileo by The Josh Bersin Company connector overview

The Galileo by The Josh Bersin Company Microsoft 365 Copilot connector brings The Josh Bersin Company research library into Microsoft 365. The connector indexes the research in Microsoft Graph so users can discover and use research-backed HR guidance in Microsoft 365 Copilot, Copilot Search, and Microsoft Search.

The library contains several thousand items, including research reports, articles, executive briefs, HR terminology, course descriptions, global employment guides, and selected partner content. The Josh Bersin Company refreshes the library daily as new research is published. No administrator action is required for these content updates.

## Why use the Galileo by The Josh Bersin Company connector?

Organizations can use the connector to:

- Access trusted HR research and workforce insights without leaving Microsoft 365.
- Ground Copilot responses in The Josh Bersin Company research and provide citations to source content.
- Give HR professionals, people leaders, and recruiters research-backed guidance in the flow of work.
- Support HR strategy, talent acquisition, learning and development, leadership, performance management, compensation, HR technology, skills, and workforce-planning scenarios.
- Combine Galileo research with organizational context through a declarative agent, while honoring each user's existing Microsoft 365 permissions.

## Build agents with the Galileo by The Josh Bersin Company connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

For guidance on building declarative agents with the Galileo by The Josh Bersin Company connector, see [Build declarative agents for Galileo by The Josh Bersin Company](galileo-declarative-agents.md). The guide provides reference configurations for the **Galileo by Josh Bersin** agent and the **Galileo Context Advisor** agent.

### Example prompts

Users can ask questions such as:

- What does The Josh Bersin Company research say about building a skills-based organization?
- What are the key principles for effective performance management?
- What does the research say about psychological safety, and what should a manager do first?
- Create an outline for an annual HR strategy grounded in The Josh Bersin Company research.
- Draft a communication about an organizational change using research-backed best practices.

## Data freshness

The Josh Bersin Company publishes content updates to the Galileo library daily. By default, the connector performs a full refresh every day. Administrators can change the **Recurrence** setting to use another frequency, such as every second week. After the initial index completes, subsequent refreshes bring newly published and updated research into Microsoft 365 without further administrator action.

## Galileo by The Josh Bersin Company connector capabilities and limitations

The Galileo by The Josh Bersin Company connector enables users to:

- Index research content and its metadata from the Galileo library.
- Search item content, file names, industries, names, and topics by default.
- Query and retrieve metadata such as creation and modification times, file extensions, file names, item IDs, industries, names, and topics by default.
- Open source items and retrieve their associated icons by using the indexed link properties.
- Customize the full-refresh recurrence to control how often data is refreshed.

The Galileo by The Josh Bersin Company connector has the following limitations by default:

- The `Content` property is searchable but isn't queryable, retrievable, or refinable.
- The `CreatedTime`, `FileExtension`, `Id`, and `ModifiedTime` properties aren't searchable or refinable.


## Data types indexed from the Galileo by The Josh Bersin Company connector

The connector indexes research items from the Galileo library with the following content and metadata:

- Content: Includes the searchable main body content of each research item.
- Identification and display information: Includes the item ID, name, file name, and file extension.
- Classification information: Includes industries and topics, which support search, query, retrieval, and result refinement by default.
- Date and time information: Includes the creation and last-modified times.
- Links: Includes the source item URL and its associated icon URL.
- File information: Includes the source item size in bytes. The `Size` property has no schema attributes by default.

Indexed Galileo content is surfaced in Microsoft 365 Copilot, Copilot Search, and Microsoft Search, making it available to users in the configured rollout audience.

## Permissions model and access control

Permissions to Galileo content in Copilot and search results are managed as follows:

- Only users in the connector rollout audience can access indexed Galileo items.
- The connector rollout audience is the maximum audience for all downstream experiences. A user outside this audience can see a shared agent but can't retrieve grounded Galileo results.
- Each user needs a Microsoft 365 Copilot license to interact with Galileo content through Copilot.

## Next step

> [!div class="nextstepaction"]
> [Set up Galileo by The Josh Bersin Company](galileo-admin-setup.md)
