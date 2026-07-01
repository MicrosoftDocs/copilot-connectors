---
title: "Confluence On-premises connector overview"
description: "Learn about the capabilities, limitations, and use cases for the Confluence On-premises Copilot connector."
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 06/29/2026
ms.localizationpriority: Medium
---

# Confluence On-premises Copilot connector overview

The Confluence On-premises connector enables your organization to index and surface content from self-hosted Confluence Data Center or Server instances in Microsoft 365 Copilot and Microsoft Search. This connector helps users discover enterprise wiki content directly within Microsoft 365 apps such as Outlook, Teams, and SharePoint.

After setup, users can ask natural language questions about Confluence pages, retrieve architecture documentation, and access internal knowledge without switching platforms.

## Why use the Confluence On-premises connector to index your data?

Organizations use Confluence to manage internal documentation, project plans, and knowledge bases. The Confluence On-premises connector brings this valuable content into Microsoft 365, enabling:

- Unified search across Microsoft 365 and Confluence.
- Enhanced productivity by reducing context switching.
- Secure access to internal documentation through permission-aware indexing.

Common use cases include:

- Summarizing internal architecture documents.
- Finding onboarding guides or policy pages.
- Locating pages updated by specific team members.
- Surfacing content tagged with specific labels or topics.

## Build agents with the Confluence On-premises connector

Developers can use this connector as a knowledge source in declarative agents they build with [Microsoft Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that agent builders can use to help their users retrieve information from 

| Category | Example prompts |
| -------- | --------------- |
| HR & onboarding | Locate the page with the onboarding guide for new employees. |
| IT & security | Find all pages labeled with "security policy." |
| Project management | What do we have on file for our Q3 strategic initiatives? |
| Compliance | Summarize our internal documentation about GDPR handling. |
| Author queries | List all pages created by [user’s name]. |
| Time-based queries | Which documents were modified this week? |

## Confluence On-premises connector capabilities and limitations

The Confluence On-premises connector enables users to:

- Perform natural language queries across indexed Confluence pages.
- Retrieve content using semantic search.
- Index Confluence spaces and pages with metadata.
- Index comments and attachments on the pages.
- Filter content by space key and page creation or modification dates.
- Filter content by CQL.
- Map Confluence identities to Microsoft Entra ID for secure access.
- Configure incremental and full crawls for synchronization.

The Confluence On-premises connector has the following limitations:

- Blogs aren't indexed.
- Archived pages are excluded.
- Permission updates are only processed during full crawls.

## Data types indexed from Confluence On-premises

The connector indexes the following data types.

| Data type | Description | 
| --------- | ----------- |
| Pages | Published pages from Confluence spaces. |
| Metadata | Title, author, created and modified dates, labels, and space keys.| 
| Space info | Space name and space key used for filtering and organization. |

Indexed content appears in Microsoft Search and Copilot experiences, so users can retrieve relevant information by using natural language queries.

## Permissions model and access control

The connector supports two identity mapping options:

- **Microsoft Entra ID**: Maps Confluence user email to Microsoft Entra user principal name (UPN).
- **Non-Microsoft Entra ID**: Uses regular expressions to map Confluence email to Microsoft Entra UPN.

The system evaluates permissions by using:

- Page-level restrictions
- Parent page restrictions
- Space-level permissions

The system computes space name and space effective permission as the intersection of these configurations. For Microsoft Graph Connector Agent versions earlier than 3.1.14, the system doesn't consider anonymous access settings. Starting with Microsoft Graph Connector Agent version 3.1.14, the system considers anonymous access settings defined at the space level.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Confluence On-premises connector](confluence-onpremises-deployment.md)

