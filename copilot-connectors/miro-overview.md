---
title: "Miro Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: anggao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 01/28/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Miro Microsoft 365 Copilot connector."
---

# Miro Microsoft 365 Copilot connector overview

The Miro Microsoft 365 Copilot connector allows your organization to index Miro boards so users can discover, access, and use Miro content directly within Microsoft 365 experiences. By integrating Miro with Microsoft 365 Copilot and Microsoft Search, users can find boards from designated Miro teams without leaving the apps they use every day, including Teams, Outlook, and SharePoint. The connector preserves Miro permissions, supports secure access, and makes Miro knowledge available in Copilot responses and search results.

## Why use the Miro connector to index your data?

Organizations use Miro to collaborate, brainstorm, plan projects, and capture team knowledge. Indexing Miro boards with the Miro connector helps organizations:

- Surface Miro content in Microsoft 365 Copilot responses and Microsoft Search.
- Enable semantic search across indexed boards without duplicating content.
- Maintain Miro's permission model for secure access.
- Improve productivity by integrating Miro into daily workflows.
- Build custom workflows that combine Miro data with other enterprise systems.

Common use cases include:

- Find team boards stored in Miro from within Microsoft 365 apps.
- Retrieve action items or planning artifacts stored on Miro boards.
- Combine Miro data with other indexed sources in custom agents or workflows.

## Build agents with the Miro connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Agent prompts

The following examples show prompts that agent builders can use to help their users retrieve information from Miro:

- Summarize the content in the board for \<project\>.
- List all action items on the board for CY26 planning.

## Miro connector capabilities and limitations

The Miro connector enables users to:

- List boards available to the user in a given Miro team.
- Fetch board metadata and textual content.
- List team members for identity and permissions mapping.
- Customize crawl frequency for full refresh.
- Use Miro content in Microsoft Copilot Studio workflows.
- Perform semantic search across supported Miro board content.

The Miro connector has the following limitations:

- Only content within sticky notes, shapes, frames, text, and embedded documents on a board is indexed.
- Comments and replies aren't indexed.
- Objects outside supported item types aren't included.

## Data types indexed from Miro

The connector indexes Miro board content and metadata, including textual elements, shapes, sticky notes, and frames. Indexed content is available to Copilot and Microsoft Search. The content is filtered according to Miro's permission model so that users only see content they have access to.

## Permissions model and access control

The connector preserves Miro’s permission model. Only users who have access to a board in Miro can see that board in Microsoft 365 Copilot and Microsoft Search.

Identity mapping uses Microsoft Entra ID. If the email address of a Miro user matches the user’s Microsoft Entra user principal name (UPN) or email, default mappings apply. Organizations can configure custom mappings if needed.

## Next step
> [!div class="nextstepaction"]
> [Deploy the Miro connector](miro-deployment.md)