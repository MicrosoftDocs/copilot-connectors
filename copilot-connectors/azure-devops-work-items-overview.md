---
title: "Azure DevOps Work Items connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: vivg
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 12/11/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Azure DevOps Work Items Microsoft 365 Copilot connector."
---

# Azure DevOps Work Items connector overview

The Azure DevOps Work Items Microsoft 365 Copilot connector indexes work items from your Azure DevOps Services instance - such as user stories, tasks, bugs, and features - into Microsoft 365. This index allows users to search and retrieve work tracking data directly in Microsoft Search and Microsoft 365 Copilot, streamlining access to development insights across the organization.

## Why use the Azure DevOps Work Items connector to index your data?

Organizations benefit from this connector by surfacing Azure DevOps work tracking data in everyday Microsoft 365 experiences. Common use cases include:

- Unified project visibility across engineering and business teams.
- Faster issue resolution by enabling natural-language queries about bugs and tasks.
- Cross-functional insights for product managers and support teams.
- Knowledge retention through searchable historical work items.

## Build agents with the Azure DevOps Work Items connector

Developers can use this connector as a knowledge source in declarative agents built with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following table lists examples of prompts that users can use to retrieve information from the Azure DevOps Work Items connector.

| Role/Department           | Example prompt                                                                 |
|---------------------------|--------------------------------------------------------------------------------|
| Software Engineer         | Find all open bugs assigned to me in the Fabrikam Web Portal project.         |
| Project Manager           | Summarize the status of all user stories in the Q4 Release epic.              |
| Quality Assurance         | List the high-priority bugs that were fixed in the last sprint.               |
| Product Owner             | What are the top backlog items in the Mobile App project and who owns them?   |
| Support Lead              | Show any work items tagged as `customer issue` that were resolved this week.  |

## Azure DevOps Work Items connector capabilities and limitations

The Azure DevOps Work Items connector allows users to:

- Index Azure DevOps work items into Microsoft 365.
- Ask natural-language questions about work items in Copilot.
- Use semantic search to find relevant work items based on context.

The Azure DevOps Work Items connector has the following limitations:

- Supports only Azure DevOps Services (cloud); doesn't support on-premises versions.
- Indexes only one Azure DevOps organization per connector instance.
- Indexes only work items (not code, pipelines, or wikis).

## Data types indexed from Azure DevOps Work Items

The Azure DevOps Work Items connector indexes the following properties:

- Title, Description, State, AssignedTo, Tags
- CreatedBy, CreatedDate, ChangedBy, ChangedDate
- WorkItemType, Priority, AreaPath, TeamProject
- URL for direct access to the work item

These properties are searchable and retrievable in Copilot and Microsoft Search. The connector also supports default result layouts and semantic labels for enhanced search experiences.

## Custom data filters

The Azure DevOps Work Items connector includes the following custom data filters for Copilot Search:

- Area Path
- Assigned to

## Permissions model and access control

Admins can configure access control as:

- **Everyone**: Indexed data is visible to all users.
- **Only people with access**: Indexed data is visible only to users with Azure DevOps permissions.

Identity mapping is handled via Microsoft Entra ID. Group membership changes are reflected during full crawls.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Azure DevOps Work Items connector](azure-devops-work-items-deployment.md)
