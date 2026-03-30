---
title: "GitHub Cloud Pull Requests Microsoft 365 Copilot connector overview"
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
description: "Learn about the capabilities, limitations, and use cases for the GitHub Cloud Pull Requests Copilot connector."
---

# GitHub Cloud Pull Requests Microsoft 365 Copilot connector overview

The GitHub Cloud Pull Requests Microsoft 365 Copilot connector enables organizations to index pull requests stored in GitHub repositories and make them searchable in Microsoft 365 Copilot and Microsoft Search experiences. By integrating GitHub data, users can retrieve information about pull requests directly within Copilot, streamlining collaboration and decision-making for development teams.

## Why use the GitHub Cloud Pull Requests connector to index your data?

This connector is designed for organizations that want to surface GitHub pull request data in Microsoft 365. Common scenarios include:

- Empower developers and project managers to quickly find and review pull requests across repositories.
- Allow business decision makers to track code review progress and project status.
- Support compliance and audit teams with visibility into repository activity.
- Facilitate knowledge sharing and collaboration by making pull request information accessible in Copilot and Microsoft Search.

## Build agents with the GitHub Cloud Pull Requests connector

Developers can use this connector as a knowledge source in declarative agents built with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/copilot-studio-agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that users can use to retrieve information from the GitHub Cloud Pull Requests connector.

**Engineering**

- Show all open pull requests for the Contoso Payments repository.
- List pull requests merged in the last 30 days.
- Find pull requests assigned to me.

**Quality Assurance**

- Which pull requests are pending review in the organization?
- List pull requests that require QA approval.

**Compliance and audit**
- Summarize the status of pull requests for the Fabrikam/Inventory project.
- List pull requests merged in the last 30 days for audit purposes.

## GitHub Cloud Pull Requests connector capabilities and limitations

The GitHub Cloud Pull Requests connector provides the following capabilities:

- Index GitHub pull requests for search and retrieval in Copilot and Microsoft Search.
- Maintain GitHub access control lists (ACLs) and user permissions for secure access.
- Customize crawl frequency and indexing preferences.
- Map GitHub user identities to Microsoft Entra ID for accurate permission enforcement.
- Configure incremental and full crawls for up-to-date indexing.
- Support webhook-based automation for real-time updates (preview).

The connector has the following limitations:

- Doesn't support indexing GitHub CI/CD pipelines beyond status indexing.
- On-premises/self-hosted GitHub instances aren't supported.
- Comments and commit information aren't crawled.
- Designed for GitHub Enterprise; Free or Team plans might have limited functionality.
- Single sign-on (SSO) isn't supported during connector configuration.
- Only content up to 30 MB in size is supported. Larger content isn't indexed. In most cases, pull request content is under this limit.
- For security reasons, the connector doesn't support the indexing of organizations where all repositories are public. To unblock this scenario, contact Microsoft support.

## Data types indexed from GitHub Cloud Pull Requests

The connector indexes pull request metadata, including:

- Content
- Labels
- Description
- Timestamps

Indexed data is surfaced in Copilot and Microsoft Search, allowing users to query and retrieve pull request information efficiently.

## Permissions model and access control

Permissions are enforced by mapping GitHub user identities to Microsoft Entra ID properties (email, sign-in, name). Admins can configure identity mapping and set repository access restrictions. The connector respects organization-level permissions to ensure that users only see repositories they're authorized to access. 

For enterprises that use the Bring Your Own Key (BYOK) model instead of Enterprise Managed Users (EMU), each user must enable the permission to share the required identity field in their GitHub account settings.

## Next step

> [!div class="nextstepaction"]
> [Deploy the GitHub Cloud Pull Requests connector](github-cloud-pull-requests-deployment.md)
