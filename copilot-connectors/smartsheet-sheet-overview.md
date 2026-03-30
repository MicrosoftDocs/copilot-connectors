---
title: "Smartsheet Sheet Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: neocheng
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 01/14/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Smartsheet Sheet Microsoft 365 Copilot connector."
---

# Smartsheet Sheet Microsoft 365 Copilot connector overview

The Smartsheet Sheet Microsoft 365 Copilot connector allows your organization to index sheet content from Smartsheet. After you configure the connector, users can search for content from Smartsheet in Microsoft 365 Copilot and from any Microsoft Search client. This connector is designed for organizations that want to bring Smartsheet content into Microsoft 365 while preserving existing security and permission structures.

## Why use the Smartsheet Sheet connector to index your data?

Organizations that use Smartsheet often need to make project plans, schedules, and other sheet data accessible to users within their daily workflow. The Smartsheet Sheet connector helps bridge this gap. Common benefits include:

- **Unified search**: Enable users to find relevant Smartsheet content based on keywords, personal preferences, and social connections using [Semantic search in Copilot](/microsoftsearch/semantic-index-for-copilot).
- **Productivity**: Users can access sheet information directly within Microsoft 365 apps, reducing the need to switch between applications.
- **Security**: The connector supports access controls to ensure only authorized users see sensitive content.

## Build agents with the Smartsheet Sheet connector

Developers can use the Smartsheet Sheet connector as a data source in declarative agents built with Copilot Studio or Agent Builder in Microsoft 365 Copilot.

### Example prompts

The following examples show prompts that users can use to retrieve information from Smartsheet:

- Find the project plan sheet for the marketing launch.
- Show me sheets created by [User Name] last week.
- Search for sheets containing "budget" in the title.
- List the latest modified sheets in the "Engineering" workspace.

## Smartsheet Sheet connector capabilities and limitations

The Smartsheet Sheet connector allows users to:

- Index Smartsheet content from Smartsheet Pro and Business editions.
- Use semantic search to find relevant content.
- Surface sheet details in Copilot responses and across Microsoft Search.

The Smartsheet Sheet connector has the following limitations:

- **Editions**: Only content from the Smartsheet Pro and Business editions is indexed.

## Data types indexed from Smartsheet

The connector indexes the following properties from Smartsheet sheets.

| Property           | Description                        | Behaviors                |
|--------------------|------------------------------------|--------------------------|
| **Content**        | The content of the sheet.          | Search                   |
| **CreatedAt**      | Date and time that the item was created. | Query, Retrieve     |
| **CreatedBy**      | Name of the person who created the item. | Query, Retrieve, Search |
| **HasAttachment**  | Whether the item has an attachment. | Query, Retrieve         |
| **Id**             | The unique identifier of the item. | Query, Retrieve          |
| **ModifiedAt**     | Date and time the item was last modified. | Query, Retrieve    |
| **Name**           | File name.                         | Query, Retrieve, Search  |
| **SheetPermaLink** | The target URL of the item.        | Query, Retrieve, Search  |
| **Title**          | The title of the item shown in Copilot. | Query, Retrieve, Search |
| **WorkspaceName**  | The name of the workspace.         | Query, Retrieve, Search  |

## Permissions model and access control

The Smartsheet Sheet connector supports two access options to prevent oversharing of sensitive data:

- **Everyone**: Indexed data appears in the search results for all users.
- **Only people with access to this data source**: Indexed data appears in the search results only for users who have access to them in Smartsheet.

When you choose **Only people with access to this data source**, the connector maps identities between Smartsheet and Microsoft Entra ID to enforce permissions.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Smartsheet Sheet connector](smartsheet-sheet-deployment.md)
