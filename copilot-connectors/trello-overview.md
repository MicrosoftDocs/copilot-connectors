---
title: "Trello connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: anggao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 04/09/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Trello Microsoft 365 Copilot connector."
---

# Trello connector overview

The Trello Microsoft 365 Copilot connector enables your organization to index Trello cards so users can discover, access, and use Trello content directly within Microsoft 365 experiences. By integrating Trello with Microsoft 365 Copilot and Microsoft Search, users can find cards from designated Trello workspaces without leaving the apps they use every day, including Teams, Outlook, and SharePoint.

## Why use the Trello connector to index your data?

Organizations use Trello to collaborate, plan, and manage projects. Indexing Trello cards with the Trello connector helps organizations:

- Surface Trello content in Microsoft 365 Copilot responses and Microsoft Search.
- Enable semantic search across indexed cards without duplicating content.
- Maintain Trello's permission model for secure access.
- Improve productivity by integrating Trello into daily workflows.
- Build custom workflows that combine Trello data with other enterprise systems.

Common use cases include:

- Finding cards stored in Trello within Microsoft 365 apps.
- Retrieving action items or planning artifacts stored on Trello cards.
- Combining Trello data with other indexed sources in custom agents or workflows.

## Build agents with the Trello connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that users can use to retrieve information from Trello:

- Summarize the content in the brainstorm for \<project\>.
- List all action items on the board for CY26 planning.

## Trello connector capabilities and limitations

The connector enables users to:

- Index public cards from Trello workspaces.
- Perform semantic search across Trello card content in Copilot and Microsoft Search.
- Discover relevant Trello content within Microsoft 365 experiences.
- Create workflows by using Trello data in Copilot Studio agents.
- Customize crawl frequency for indexed Trello data.

The connector has the following limitations:

- Doesn't index comments.
- Copilot returns only card URLs in search results and chat responses. Workspace or board URLs aren't supported.

## Data types indexed from Trello

The Trello connector indexes card-based content from Trello workspaces, including:

- Card titles
- Card descriptions
- Due dates
- Assigned members
- Board names
- Labels or tags
- Creation and last modified dates
- Card URLs

## Permissions model and access control

The connector preserves Trello’s permission model. Only users who have access to a card in Trello can see that card in Microsoft 365 Copilot and Microsoft Search.

Identity mapping uses Microsoft Entra ID. If the email address of a Trello user matches the user’s Microsoft Entra user principal name (UPN) or email, default mappings apply. Organizations can configure custom mappings if needed.

## Next step

> [!div class="nextstepaction"]
> [Deploy the connector](trello-deployment.md)