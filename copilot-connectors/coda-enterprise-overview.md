---
title: "Coda Enterprise Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: irenehuang
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 12/16/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Coda Enterprise Microsoft 365 Copilot connector."
---

# Coda Enterprise Microsoft 365 Copilot connector overview

The Coda Enterprise Microsoft 365 Copilot connector allows your organization to index documents and pages from your Coda Enterprise environment. After you configure the connector, users can search and retrieve Coda content directly from Microsoft 365 Copilot and Microsoft Search. The connector maintains Coda access controls to ensure that users can only see content they have permission to view.

## Why use the Coda Enterprise connector to index your data?

Use the Coda Enterprise connector to make Coda content discoverable across Microsoft 365 experiences. Common use cases include:

- Help users quickly find information stored in Coda documents and pages through natural language queries in Copilot.
- Support enterprise knowledge discovery by indexing project documentation, policies, procedures, and team workspaces stored in Coda.
- Provide unified search across Microsoft 365 and Coda so users don't need to switch between apps to locate content.
- Apply content filters to selectively index Coda content based on your organization’s requirements, such as time-based filtering.
- Use semantic search enhancements to help users identify the most relevant Coda documents.

### Use cases

The following table lists potential use cases for the connector.

| **Department/role** | **Use case** | **Business benefit** |
|---------------------|--------------|----------------------|
| People/HR | Summarize onboarding guides, policies, and FAQs. | Faster onboarding, reduced dependency on HR staff. |
| Engineering/Product | Access design docs, retrospectives, and deployment guides. | Reduced context switching, faster execution. |
| Project Management | Query release plans, status reports, and team wikis. | Better alignment, faster planning cycles. |
| Sales/Marketing | Discover case studies, messaging docs, and campaign plans. | Improved collaboration, reduced duplicated work. |

## Build agents with the Coda Enterprise connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Eaxmple prompts

The following examples show prompts that agent builders can use to help their users retrieve information from Coda Enterprise:

- Find the most recently updated Coda documents related to our Q4 planning.
- Show me the Coda pages authored by our design team in the past month.
- Summarize the content of the Customer feedback Coda workspace.
- List all documents in the Coda workspace owned by me.
- Retrieve the URL for the Coda document titled Engineering Roadmap.

## Coda Enterprise connector capabilities and limitations

The Coda Enterprise connector enables users to:

- Index documents and pages from a Coda Enterprise environment while maintaining access control.
- Use content filters to index only selected Coda content.
- Apply semantic search in Copilot to improve content relevance.
- Retrieve Coda content through Microsoft 365 Copilot and Microsoft Search.

The Coda Enterprise connector has the following limitations:

- Only the Coda Enterprise edition is supported. Coda Free, Pro, and Team editions aren't supported due to API restrictions.
- Documents larger than 125 MB can't be exported via the Coda API.
- Coda API request limits might affect large-scale indexing unless filters or multiple connections are configured.

## Data types indexed from Coda Enterprise

The connector indexes documents and pages from your Coda Enterprise organization. Indexed content includes:

- Document metadata such as title, authors, owner, timestamps, and workspace information.
- Document content from the main body of each Coda document for search indexing.
- Container information, such as folder or workspace names and URLs.

The connector uses semantic enrichment where supported, enabling enhanced retrieval in Copilot.

## Permissions model and access control

Permissions for Coda Enterprise content follow the access control model defined in Coda:

- Content is visible only to users who have access to it in Coda.
- Access permissions can be configured for **Everyone** or **Only people with access to this data source**.
- Identity mapping uses Microsoft Entra ID by default. If email identifiers differ, admins can configure custom mapping rules.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Coda Enterprise connector](coda-enterprise-deployment.md)
