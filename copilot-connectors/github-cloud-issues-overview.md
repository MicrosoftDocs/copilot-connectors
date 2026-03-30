---
title: GitHub Cloud Issues Microsoft 365 Copilot connector overview
description: "Learn about the capabilities, limitations, and use cases for the GitHub Cloud Issues Microsoft 365 Copilot connector."
author: Lauragra
ms.author: lauragra
ms.reviewer: lauragra
manager: calvind
ms.date: 12/15/2025
ms.service: copilot-connectors
ms.topic: concept-article
---

# GitHub Cloud Issues Microsoft 365 Copilot connector overview

The GitHub Cloud Issues Microsoft 365 Copilot connector enables your organization to index issues stored in GitHub so they can be surfaced in Microsoft 365 Copilot and Microsoft Search experiences. After you configure and deploy the connector, users can search and retrieve GitHub issues data directly in Microsoft 365.


## Why use the GitHub Cloud Issues connector to index your data?

Organizations use the GitHub Cloud Issues connector to:

- Make GitHub issue data discoverable in Microsoft 365 Copilot responses.
- Enable Microsoft Search to return relevant GitHub issue content.
- Improve productivity by reducing context switching between GitHub and Microsoft 365.

Common use cases include:

- Developers can quickly find GitHub issue details without leaving Microsoft Teams or Outlook.
- Project managers can track issue progress directly in Copilot.
- Support teams can access GitHub issue history during troubleshooting.

## Build agents with the GitHub Cloud Issues connector

Developers can use this connector as a knowledge source in declarative agents they build with:

- [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio)
- [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/copilot-studio-agent-builder)
- [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit)

### Example prompts

The following table lists examples of prompts that users can use to retrieve information from the GitHub Cloud Issues connector.

| Role            | Example prompt |
|-----------------|----------------|
| Developer       | Show me all open GitHub issues assigned to me in the last seven days. |
| Project Manager | Summarize high-priority GitHub issues for the release milestone. |
| Support Agent   | Find GitHub issues related to error code 500 in the API. |

## GitHub Cloud Issues connector capabilities and limitations

The GitHub Cloud Issues connector enables users to:

- Index GitHub issues from supported organizations.
- Maintain GitHub access control lists (ACLs) and user permissions for secure access.
- Customize crawl frequency and indexing preferences.

The connector has the following limitations:

- On-premises or self-hosted GitHub instances aren't supported.
- GitHub CI/CD pipelines aren't indexed beyond status information.
- The connector is designed for GitHub Enterprise. The functionality for Free or Team GitHub plans might be limited.
- Only content up to 30 MB in size is supported. Larger content isn't indexed. In most cases, issue content is under this limit.
- For security reasons, the connector doesn't support the indexing of organizations where all repositories are public. To unblock this scenario, contact Microsoft support.

## Data types indexed from GitHub Cloud Issues

The connector indexes the following data type.

| Data type | Description |
|-----------|-------------|
| Issues    | Includes issue title, description, labels, timestamps, and metadata. |

Indexed content is available in Microsoft 365 Copilot responses and Microsoft Search results.

## Permissions model and access control

The connector enforces GitHub permissions and maps them to Microsoft Entra ID identities. To ensure correct permission enforcement:

- Map GitHub user identities to Microsoft Entra ID using email, sign in, or name.
- If direct mapping fails, use regular expressions (regex) to transform identity data.
- The connector respects organization-level repository access restrictions.

## Next step

> [!div class="nextstepaction"]
> [Deploy the GitHub Cloud Issues connector](github-cloud-issues-deployment.md)
