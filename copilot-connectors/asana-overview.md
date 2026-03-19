---
title: "Asana Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: Kai-Cloud
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 10/23/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Asana Microsoft 365 Copilot connector."
---

# Asana Microsoft 365 Copilot connector overview

The Asana Microsoft 365 Copilot connector integrates Asana tasks into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface relevant task information directly within apps like Microsoft Teams, Outlook, and SharePoint. When you configure the Asana connector for your organization and index data from Asana workspaces, users can search for Asana tasks in Microsoft Search, Microsoft 365 Copilot, and Copilot Search. The connector improves project tracking, task visibility, and overall productivity.

## Why use the Asana connector to index your data?

Organizations that use Asana for project and task management often face challenges in consolidating task information across multiple tools. The Asana connector addresses these challenges by integrating Asana tasks into Microsoft 365. This integration allows employees to surface Asana tasks through Copilot, Copilot Search, and Microsoft Search—within everyday apps like Teams, Outlook, or SharePoint—without leaving their flow of work.

The Asana connector provides the following benefits:

- **Boosts productivity** – Access Asana tasks directly within Microsoft 365 apps, reducing time spent switching platforms.
- **Improves decision-making** – Unified search across Asana and Microsoft tools ensures faster access to task information.
- **Enhances collaboration** – Teams can easily track and manage tasks across projects without leaving Microsoft 365.
- **Preserves security and compliance** – The connector respects Asana permissions to ensure that sensitive content is only visible to authorized users.

### Common use cases

| Department/role       | Use case                                             | Business benefit                          |
|-----------------------|------------------------------------------------------|-------------------------------------------|
| Project management     | Summarize upcoming tasks and deadlines across projects | Improved planning and prioritization      |
| Engineering/DevOps   | Identify unassigned or overdue tasks                | Better workload distribution and accountability |
| Operations             | Track task completion trends                        | Enhanced operational efficiency           |

## Build agents with the Asana connector

Developers can use this connector as a knowledge source in declarative agents they build with the [Copilot Studio full experience](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), the [Copilot Studio lite experience](/microsoft-365/copilot/extensibility/copilot-studio-agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Eaxmple prompts

The following examples show prompts that agent builders can use to help their users retrieve information from Asana.

**Project Management**

- Summarize all tasks tagged as blockers across all projects.
- What are the key tasks and their deadlines for the current quarter?
- List overdue tasks and their assigned owners for escalation.

**Engineering/DevOps**

- Summarize all overdue tasks across active projects and highlight critical blockers.
- What are the open tasks in the microservice project this week?
- Summarize the tasks related to the new microservices deployment and their owners.

**Operations**

- List all tasks from the last retrospective and their completion status.
- What are the upcoming tasks scheduled for the next two weeks in the Operations project?

## Asana connector capabilities and limitations

The Asana connector enables users to:

- Index Asana tasks from connected workspaces.
- Perform natural language queries in Copilot to retrieve task-related information.
- Use semantic search to find relevant content based on keywords and context.
- Access task data directly within Microsoft 365 apps.

The Asana connector has the following limitations:

- Doesn't index custom fields.
- Doesn't index Goals, Portfolios, or other entities under Insights.
- Requires identity mapping if Asana user emails differ from Microsoft Entra ID user principal names (UPNs).
- Permission updates might take time to reflect, as changes are applied during scheduled crawls.

## Data types indexed from Asana

The Asana connector indexes key task-related data so it can be used in Copilot, Copilot Search, and Microsoft Search. By default, the connector crawls all Asana tasks in your Asana workspace.

| Asana data type | Indexed and surfaced in Copilot and search |
|------------------|---------------------------------------------|
| Tasks  | Task details, including name, description, due date, assignee, associated projects, and so on. |
| Projects  | Project name, project ID, sections, and so on. |
| Comments  | Comments text, creator, created date, and so on. |
| Attachments  | Attachment name, attachment content, uploaded by, and so on. |

## Permissions model and access control

The Asana connector enforces that only users who have access to a task in Asana can see it in Copilot responses and search results. Permissions are based on workspace access settings in Asana. Identity mapping ensures that Asana users are correctly matched to Microsoft Entra ID accounts. Admins can choose to index content as visible to everyone or enforce per-user permissions.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Asana connector](asana-deployment.md)
