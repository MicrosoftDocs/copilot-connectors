---
title: "GitHub Server Knowledge connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 12/15/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the GitHub Server Knowledge Microsoft 365 Copilot connector."
---

# GitHub Server Knowledge connector overview

The GitHub Server Knowledge Microsoft 365 Copilot connector enables organizations to index knowledge stored in GitHub Enterprise repositories—including markdown files, wiki pages, and blogs—so users can search and retrieve information via Microsoft Search and Microsoft 365 Copilot. After you configure the connector and index data, content from GitHub surfaces directly within Microsoft 365 apps such as Teams, Outlook, and SharePoint. This data supports collaboration and knowledge discovery across your organization.

## Why use the GitHub Server Knowledge connector to index your data?

The GitHub Server Knowledge connector is designed for organizations that want to make technical documentation, wikis, and knowledge bases stored in GitHub easily discoverable within Microsoft 365. Common use cases include:

- Allow engineers and technical writers to quickly find internal documentation and best practices.
- Support IT and support teams with access to troubleshooting guides and operational knowledge.
- Facilitate onboarding by surfacing organizational knowledge in Copilot and Microsoft Search.
- Empower business decision makers to access technical insights and project information.

## Build agents with the GitHub Server Knowledge connector

Developers can use this connector as a knowledge source in declarative agents built with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

Agent builders can use prompts to help users retrieve information from GitHub Server Knowledge. Example prompts include:

- Show me the latest wiki updates for the engineering team.
- Find troubleshooting guides for our internal tools.
- List onboarding documentation for new developers.
- Retrieve blog posts tagged with 'security' from our GitHub knowledge base.

## GitHub Server Knowledge connector capabilities and limitations

The GitHub Server Knowledge connector enables users to:

- Index markdown files, wiki pages, and blogs from GitHub Enterprise repositories.
- Perform natural language queries in Copilot and Microsoft Search to retrieve relevant GitHub content.
- Maintain GitHub access control lists (ACLs) and user permissions for indexed data.
- Customize crawl frequency and indexing preferences to suit organizational needs.
- Map GitHub user identities to Microsoft Entra ID for accurate permission enforcement.

The connector has the following limitations:

- The connector doesn't support indexing GitHub CI/CD pipelines beyond status indexing.
- The connector is designed specifically for GitHub Enterprise Server (on-premises/self-hosted) instances. GitHub.com (cloud-hosted) and non-Enterprise plans aren't supported.
- Users on Free or Team plans might experience limited functionality or reduced support.
- For security reasons, the connector doesn't support the indexing of organizations where all repositories are public. To unblock this scenario, contact Microsoft support.

## Data types indexed from GitHub Server Knowledge

The connector indexes the following data types:

- Markdown files (.md)
- Wiki pages
- Blogs and text documentation

Indexed content is surfaced in Copilot and Microsoft Search results, allowing users to discover and interact with organizational knowledge directly within Microsoft 365 apps.

## Permissions model and access control

Administrators can set permissions for indexed GitHub data using Microsoft Entra ID mapping. The connector supports two access models:

- **Only people with access to this data source** (default): Indexed data appears in search results only for users who have access in GitHub.
- **Everyone**: Indexed data appears in search results for all users.

Identity mapping options include:

- Email: Maps GitHub email to Microsoft Entra ID user properties.
- Login: Maps GitHub sign in to Microsoft Entra ID user properties.
- Name: Maps GitHub name to Microsoft Entra ID user properties.

If direct mapping fails, you can use regular expressions (regex) to transform identity data. For personal accounts, email domain variations and visibility settings can affect mapping accuracy.

## Next step

> [!div class="nextstepaction"]
> [Deploy the GitHub Server Knowledge connector](github-server-knowledge-deployment.md)
