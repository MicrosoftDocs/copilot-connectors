---
title: "monday.com Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: huichunli
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 01/13/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the monday.com Microsoft 365 Copilot connector."
---

# monday.com Microsoft 365 Copilot connector overview

The monday.com Microsoft 365 Copilot connector enables organizations to index monday.com items, boards, groups, and workspace metadata into Microsoft Graph. After you deploy the connector, monday.com content is surfaced in Microsoft 365 Copilot, Copilot Search, and Microsoft Search  experiences and within apps like Microsoft Teams, Outlook, and SharePoint. This integration helps users discover, summarize, and work with project and task data without leaving Microsoft 365.

## Why use the monday.com connector to index your data?

Many organizations rely on monday.com as a central work operating system for managing projects, workflows, and collaboration. However, monday.com content is typically siloed within its own platform. The monday.com connector makes this data discoverable, referenceable, and usable directly in Microsoft 365.

Key benefits that the connector provides include:

- **Centralized content discovery:** Surface monday.com boards, items, and related metadata in Microsoft 365 search and Copilot experiences, reducing the need to switch between platforms.
- **Improved productivity:** Enable users to search for, reference, and interact with monday.com content using natural language queries in Copilot and Microsoft Search.
- **Faster insights and decision-making:** Allow users to summarize project status, identify pending or overdue tasks, and generate insights based on monday.com data.

The following table lists common use cases for the connector.

| Department or role | Use case | Benefit |
|-------------------|----------|---------|
| Project managers | Find boards or tasks related to specific initiatives. | Faster coordination and visibility. |
| Team members | Retrieve tasks assigned to them. | Reduced context switching and time savings. |
| Leadership | Review summaries of project progress, including pending and overdue work. | Better executive decision-making. |

## Build agents with the monday.com connector

Developers can use the monday.com connector as a knowledge source in declarative agents built with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Eaxmple prompts

The following examples show prompts that users can use to retrieve information from monday.com:

- Find the board for the Q2 marketing campaign.
- List all tasks assigned to me on the Product Launch board.
- Summarize the Website Redesign task from the Design board.

## monday.com connector capabilities and limitations

The monday.com connector enables users to:

- Index boards, groups, items, and workspace metadata from monday.com.
- Retrieve project and task information using natural language queries in Copilot.
- Generate summaries and insights for tasks, including pending work and overdue items.
- Maintain existing monday.com access controls so that users only see content they're authorized to access.
- Customize crawl frequency to balance freshness and API usage.

The monday.com connector has the following limitations:

- Only active boards, groups, and items are indexed.
- Content is crawled on behalf of the OAuth-authorized user, and only items that the authorized user can access are indexed.
- Items that aren't accessible to the authorized user in monday.com aren't indexed.

## Data types indexed from monday.com

The connector indexes monday.com items (tasks or records) along with their associated metadata, including board, group, and workspace details. Indexed content can appear in Copilot responses, Copilot Search, and Microsoft Search results across Microsoft 365.

## Permissions model and access control

The monday.com Microsoft 365 Copilot connector fully respects monday.com access control lists (ACLs), including:

- Public and private boards
- User-based permissions
- Viewer and editor roles

Indexed content is only visible to Microsoft 365 users who have access to the corresponding item in monday.com. The connector also supports email-based identity mapping to enforce permissions correctly.

## Next step

> [!div class="nextstepaction"]
> [Deploy the monday.com connector](monday-deployment.md)
