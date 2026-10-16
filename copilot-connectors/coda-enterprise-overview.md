---
title: "Superhuman Docs Enterprise connector overview"
ms.author: jasonjoh
author: jasonjoh
manager: calvind
ms.reviewer: irenehuang
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.date: 10/08/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Superhuman Docs Enterprise Microsoft 365 Copilot connector."
---

<!-- cSpell:ignore irenehuang -->

# Superhuman Docs Enterprise connector overview

The Superhuman Docs Enterprise Microsoft 365 Copilot connector enables your organization to index documents and pages from your Superhuman Docs Enterprise environment. After you configure the connector, users can search and retrieve Superhuman Docs content directly from Microsoft 365 Copilot and Microsoft Search. The connector maintains Superhuman Docs access controls to ensure that users can only see content they have permission to view.

## Why use the Superhuman Docs Enterprise connector to index your data?

Use the Superhuman Docs Enterprise connector to make Superhuman Docs content discoverable across Microsoft 365 experiences. Common use cases include:

- Help users quickly find information stored in documents and pages in Superhuman Docs through natural language queries in Copilot.
- Support enterprise knowledge discovery by indexing project documentation, policies, procedures, and team workspaces stored in Superhuman Docs.
- Provide unified search across Microsoft 365 and Superhuman Docs so users don't need to switch between apps to locate content.
- Apply content filters to selectively index Superhuman Docs content based on your organization’s requirements, such as time-based filtering.
- Use semantic search enhancements to help users identify the most relevant documents in Superhuman Docs.

### Use cases

The following table lists potential use cases for the connector.

| **Department/role** | **Use case** | **Business benefit** |
|---------------------|--------------|----------------------|
| People/HR | Summarize onboarding guides, policies, and FAQs. | Faster onboarding, reduced dependency on HR staff. |
| Engineering/Product | Access design docs, retrospectives, and deployment guides. | Reduced context switching, faster execution. |
| Project Management | Query release plans, status reports, and team wikis. | Better alignment, faster planning cycles. |
| Sales/Marketing | Discover case studies, messaging docs, and campaign plans. | Improved collaboration, reduced duplicated work. |

## Build agents with the Superhuman Docs Enterprise connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that agent builders can use to help their users retrieve information from Superhuman Docs Enterprise:

- Find the most recently updated documents in Superhuman Docs related to our Q4 planning.
- Show me the Superhuman Docs pages authored by our design team in the past month.
- Summarize the content of the Customer feedback workspace in Superhuman Docs.
- List all documents in the Superhuman Docs workspace that I own.
- Retrieve the URL for the document titled Engineering Roadmap in Superhuman Docs.

## Superhuman Docs Enterprise connector capabilities and limitations

The Superhuman Docs Enterprise connector enables users to:

- Index documents and pages from a Superhuman Docs Enterprise environment while maintaining access control.
- Use content filters to index only selected Superhuman Docs content.
- Apply semantic search in Copilot to improve content relevance.
- Retrieve Superhuman Docs content through Microsoft 365 Copilot and Microsoft Search.

The Superhuman Docs Enterprise connector has the following limitations:

- Only the Superhuman Docs Enterprise edition is supported. Free, Pro, and Team editions aren't supported due to API restrictions.
- You can't export documents larger than 125 MB through the Superhuman Docs API.
- Superhuman Docs API request limits might affect large-scale indexing unless you configure filters or multiple connections.

## Data types indexed from Superhuman Docs Enterprise

The connector indexes documents and pages from your Superhuman Docs Enterprise organization. Indexed content includes:

- Document metadata such as title, authors, owner, timestamps, and workspace information.
- Document content from the main body of each document in Superhuman Docs for search indexing.
- Container information, such as folder or workspace names and URLs.

The connector uses semantic enrichment where supported, enabling enhanced retrieval in Copilot.

## Permissions model and access control

Permissions for Superhuman Docs Enterprise content follow the access control model defined in Superhuman Docs:

- Content is visible only to users who have access to it in Superhuman Docs.
- Access permissions can be configured for **Everyone** or **Only people with access to this data source**.
- Identity mapping uses Microsoft Entra ID by default. If email identifiers differ, admins can configure custom mapping rules.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Superhuman Docs Enterprise connector](coda-enterprise-deployment.md)
