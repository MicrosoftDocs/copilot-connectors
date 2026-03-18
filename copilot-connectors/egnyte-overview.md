---
title: "Egnyte Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: anggao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 12/16/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Egnyte Microsoft 365 Copilot connector."
---

# Egnyte Microsoft 365 Copilot connector overview

The Egnyte Microsoft 365 Copilot connector allows your organization to index files stored in Egnyte so users can retrieve them through Microsoft 365 Copilot and Microsoft Search. After you configure the connector, users can quickly find Egnyte files directly from experiences such as Teams, Outlook, and SharePoint. This connector helps teams work more efficiently by unifying content discovery across Microsoft 365 and Egnyte while maintaining Egnyte’s permissions model.

## Why use the Egnyte connector to index your data?

Organizations use Egnyte to store, organize, and share files across teams. The Egnyte connector helps your organization:

- Surface Egnyte content in Microsoft 365 Copilot responses and Microsoft Search.
- Enable semantic search across Egnyte files without duplicating data.
- Maintain Egnyte permissions for secure access.
- Improve productivity by integrating Egnyte content into workflows in Teams, Outlook, and SharePoint.

Common use cases include:

- Find team documents stored in Egnyte without switching apps.
- Build custom workflows that use Egnyte content alongside other enterprise data sources.

## Build agents with the Egnyte connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Eaxmple prompts

The following examples show prompts that agent builders can use to retrieve information from Egnyte:

- Summarize files in the shared Egnyte folder for the product launch.
- List all team Egnyte files modified in the last seven days.

## Egnyte connector capabilities and limitations

The Egnyte connector allows users to:

- Access Egnyte files in Copilot by using semantic search.
- Customize the crawl frequency to manage sync behavior.
- Create workflows by using this connection and actions in Microsoft Copilot Studio.

The Egnyte connector has the following limitations:

- Doesn't index comments and replies.
- Large file annotations might cause ingestion errors.
- API rate limits can prevent successful crawl operations unless those limits are increased with Egnyte.

## Data types indexed from Egnyte

The connector indexes the following Egnyte data types:

- Files stored in your Egnyte domain.

Indexed content appears in Copilot answers and search results, subject to Egnyte access permissions.

## Permissions model and access control

The connector respects Egnyte's native permissions. Users only see content they're allowed to access in Egnyte. When admins configure the connector, they can choose between:

- **Everyone:** All indexed files appear in search results for all Microsoft 365 users.
- **Only people with access to this data source (recommended):** Users see only the content they have access to in Egnyte.

If Egnyte user emails don't match Microsoft Entra ID user principal names, you can configure identity mapping.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Egnyte connector](egnyte-deployment.md)
