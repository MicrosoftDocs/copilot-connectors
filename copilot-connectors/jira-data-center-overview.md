---
title: "Jira Data Center Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: neocheng
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 12/17/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Jira Data Center Microsoft 365 Copilot connector."
---

# Jira Data Center Microsoft 365 Copilot connector overview

The Jira Data Center Microsoft 365 Copilot connector allows your organization to index Jira Data Center issues and related project data so they become discoverable and actionable in Microsoft 365 experiences. By integrating securely with your on-premises Jira Data Center environment through the Microsoft Graph Connector Agent, the connector allows users to retrieve, summarize, and analyze project and issue information directly in Microsoft 365 Copilot and Microsoft Search.

This connector is designed for organizations that maintain Jira Data Center on-premises and want to bring issue tracking, project health, and engineering workflows into Microsoft 365 while preserving existing security and permission structures.

## Why use the Jira Data Center connector to index your data?

Organizations that use Jira Data Center often face siloed information across project teams, engineering systems, and business processes. The Jira Data Center connector helps break down these silos so users can easily discover and interact with Jira content in Microsoft 365. Common benefits include:

- **Boost productivity:** Employees can access Jira issue status directly within Microsoft 365 apps, reducing context switching.
- **Improve decision-making:** Unified search across Jira and Microsoft tools provides faster access to project status and blockers.
- **Accelerate issue resolution:** Support teams can quickly retrieve bug details and related items from Copilot.
- **Preserve security:** The connector respects the Jira Data Center permission model, including issue-level security and project roles, so only authorized users see sensitive content.

## Build agents with the Jira Data Center connector

Developers can use the Jira Data Center connector as a data source in declarative agents built with:

- [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio)
- [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder)
- [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit)

### Example prompts

The following examples show prompts that agent builders can use to help their users retrieve information from Jira Data Center:

- Summarize the open issues in project Alpha.
- Show me all high-priority bugs filed this week.
- List the issues assigned to me that are blocked.
- Give me a summary of critical blockers in the current sprint.

## Jira Data Center connector capabilities and limitations

The Jira Data Center connector allows users to:

- Perform natural language queries about Jira issues and projects.
- Retrieve engineering, project management, and support-related items across Jira Data Center.
- Use semantic search to find issues, tasks, bugs, or stories based on descriptive queries.
- Surface project and issue details in Copilot responses and across Microsoft Search.
- Maintain data security by honoring Jira’s issue-level security and project permissions.

The Jira Data Center connector has the following limitations:

- The connector supports Jira Data Center **version 8.14 and later**.
- The connector can't evaluate certain permission types, such as `Any logged-in user`, `Application access`, or some custom-field–based permission types. When permissions can't be resolved, access is denied to prevent oversharing.
- Identity mapping requires Microsoft Entra ID–aligned email addresses or manual regex mapping for non-Entra ID environments.

## Data types indexed from Jira Data Center

The following table describes the Jira Data Center content types that the connector indexes.

The following table lists supported content types and how they appear in Copilot and search results.

| Jira content type | Indexed and surfaced in Copilot and search |
|-------------------|---------------------------------------------|
| **Issues**        | Core work items such as Stories, Bugs, and Tasks. Indexed fields include Summary, Description, Priority, Status, Assignee, Project, and timestamps. |
| **Projects**      | Project metadata including Project Name and Key. |

## Permissions model and access control

The Jira Data Center connector enforces access control by aligning with Jira’s native permission hierarchy. This prevents oversharing of sensitive data and ensures only authorized users can view issues in Copilot and Microsoft Search.

The connector evaluates permissions using the following hierarchy:

1. **Issue security level (highest priority):** If an issue has an issue security level configured, access is restricted to users, groups, or roles explicitly included in the configuration.

2. **Project-level permissions:** If no issue security level is defined, access falls back to the project’s permission scheme. Users must have the **Browse Projects** permission for the corresponding project. The connector supports resolving:
   - Project roles
   - Groups
   - Current Assignee
   - Reporter
   - Project Lead
   - Single users

If permissions are defined using unsupported assignment types, the connector blocks access for safety.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Jira Data Center connector](jira-data-center-deployment.md)