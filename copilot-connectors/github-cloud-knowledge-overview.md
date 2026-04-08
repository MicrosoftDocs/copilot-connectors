---
title: "GitHub Cloud Knowledge connector overview"
ms.author: lauragra
author: Lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 01/20/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the GitHub Cloud Knowledge Copilot connector."
---

# GitHub Cloud Knowledge connector overview

The GitHub Cloud Knowledge Microsoft 365 Copilot connector enables organizations to index markdown and text files from GitHub repositories into Microsoft 365 Copilot and Microsoft Search experiences. By integrating GitHub content with Microsoft 365, users can access project documentation and technical guides directly in familiar apps, reducing context switching and improving productivity.

## Why use the GitHub Cloud Knowledge connector to index your data?

The GitHub Cloud Knowledge connector is ideal for organizations that use GitHub for documentation, project files, or content management. You can use the connector to:

- Make project documentation searchable in Microsoft 365.
- Allow users to ask Copilot questions such as:
  - How do I set up Project Alpha?
  - Where can I find the deployment instructions?
  - What is the architecture overview for this project?
- Summarize key sections in project documentation for quick reference.

## Build agents with the GitHub Cloud Knowledge connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/copilot-studio-agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that agent builders can use to help their users retrieve information from the GitHub Cloud Knowledge connector.

| Role           | Example prompt |
|---------------|----------------|
| Developer     | Summarize the architecture overview for Project Alpha. |
| Project Manager | List all deployment steps for the latest release. |
| Support Engineer | Where can I find troubleshooting instructions for the API integration? |

## GitHub Cloud Knowledge connector capabilities and limitations

The GitHub Cloud Knowledge connector enables users to:

- Index GitHub Cloud repositories, markdown, and text files to make project documentation accessible in Microsoft 365.
- Perform natural language queries in Copilot to retrieve technical guides and documentation.
- Use semantic search to find relevant content based on keywords, preferences, and social connections.
- Summarize project documentation for quick reference.

The GitHub Cloud Knowledge connector has the following limitations:

- Only repository metadata, markdown, and text files are indexed. Issues, pull requests, and comments aren't indexed.
- Only Markdown and text files up to 30 MB in size are supported. Larger files aren't indexed.
- For security reasons, the connector doesn't support the indexing of organizations where all repositories are public. To unblock this scenario, contact Microsoft support.

> [!NOTE]
> If your organization requires a higher crawl throughput, use the [GitHub Server Knowledge connector](github-server-knowledge-overview.md) instead. The GitHub Server Knowledge connector uses a Microsoft Graph Connector Agent-based model to invoke Git clone operations and crawl directly against your GitHub.com organization. This provides improved crawl performance for large-scale organizations.

## Data types indexed from GitHub Cloud Knowledge

The connector indexes the following data types.

| Data type           | Description                          |
|---------------------|--------------------------------------|
| Markdown files      | Project documentation and guides    |
| Text files          | Technical notes and instructions    |
| Repository metadata | Basic repository information        |

Indexed content appears in Microsoft 365 Copilot responses and Microsoft Search results.

## Permissions model and access control

The connector enforces GitHub permissions when displaying search results. Indexed data can be visible to:

- **Only people with access to this data source** (default): Results appear only for users who have access in GitHub.
- **Everyone**: Results appear for all users in the organization.

Identity mapping between GitHub and Microsoft Entra ID is required for accurate permission enforcement. Mapping options include:

- Email
- Sign in
- Name

If direct mapping fails, you can use regular expressions (regex) to transform identity data.

## Next step

> [!div class="nextstepaction"]
> [Deploy the GitHub Cloud Knowledge connector](github-cloud-knowledge-deployment.md)
