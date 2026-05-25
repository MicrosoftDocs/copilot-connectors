---
title: "Airtable connector overview (preview)"
ms.author: kailiang
author: Kai-Cloud
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 05/21/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Airtable Microsoft 365 Copilot connector."
---

# Airtable connector overview (preview)

The Airtable Microsoft 365 Copilot connector integrates Airtable records into Microsoft 365. This integration allows Copilot, Copilot Search, and Microsoft Search to surface relevant record information directly within apps like Microsoft Teams, Outlook, and SharePoint. When you configure the Airtable connector for your organization and index data from Airtable bases, users can search for Airtable records in Microsoft Search, Microsoft 365 Copilot, and Copilot Search. The connector improves project tracking, operational visibility, and overall productivity.

> [!NOTE]
> The Airtable connector is currently in preview. Connector functionality and requirements are subject to change.

## Why use the Airtable connector to index your data?

Organizations that use Airtable to manage projects, operations, and structured data often face challenges surfacing that information alongside the content their teams work with every day. The Airtable connector addresses these challenges by integrating Airtable records into Microsoft 365. This integration allows employees to find Airtable records through Copilot, Copilot Search, and Microsoft Search, within everyday apps like Teams, Outlook, or SharePoint, without leaving their flow of work.

The Airtable connector provides the following benefits:

- **Boosts productivity** – Access Airtable records directly within Microsoft 365 apps, reducing time spent switching platforms.
- **Improves decision-making** – Unified search across Airtable and Microsoft tools ensures faster access to record information.
- **Enhances collaboration** – Teams can easily track and reference records across bases without leaving Microsoft 365.
- **Preserves security and compliance** – The connector respects Airtable permissions so that content is only visible to authorized users.

### Common use cases

| Department/role | Use case | Business benefit |
|---|---|---|
| Project management | Summarize the status of in-progress projects and upcoming milestones. | Improved planning and prioritization. |
| Operations | Look up deliverable owners, due dates, and completion rates. | Faster handoffs and clearer accountability. |
| Engineering/Program management | Identify projects with risk flags or budget exposure. | Earlier escalation of at-risk work. |

## Build agents with the Airtable connector

Developers can use this connector as a knowledge source in declarative agents they build with the [Copilot Studio full experience](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), the [Copilot Studio lite experience](/microsoft-365/copilot/extensibility/copilot-studio-agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that agent builders can use to help their users retrieve information from Airtable.

**Project management**

- Summarize the status of all in-progress projects and their project managers.
- What are the upcoming milestones for the Cloud Infrastructure Optimization project?
- List projects that are flagged as high risk and their budgets.

**Operations**

- Show open deliverables for the Mobile Application Redesign project and their owners.
- What deliverables are due in the next 30 days across all projects?
- Summarize the milestone completion rate for each active project.

**Program management**

- Which projects are over budget or behind schedule based on the latest status?
- List projects sorted by end date and highlight any with no milestones completed.

## Airtable connector capabilities and limitations

The Airtable connector enables users to:

- Index Airtable records from selected bases and tables.
- Perform natural language queries in Copilot to retrieve record information.
- Use semantic search to find relevant content based on keywords and context.
- Access record data directly within Microsoft 365 apps.

The Airtable connector has the following limitations:

- Doesn't index attachments or record comments.
- Doesn't index views, automations, interfaces, or other entities beyond records.
- Requires identity mapping if Airtable user emails differ from Microsoft Entra ID user principal names (UPNs).
- Permission updates might take time to reflect, as changes are applied during scheduled crawls.

## Data types indexed from Airtable

The Airtable connector indexes record-level data so you can use it in Copilot, Copilot Search, and Microsoft Search. By default, the connector crawls all accessible bases in your Airtable enterprise account.

| Airtable data type | Indexed and surfaced in Copilot and search |
|---|---|
| Records | Record fields, including the primary field, created date, and field values across supported field types. |
| Tables | Table name and table ID for context and filtering. |
| Bases | Base name and base ID for context and filtering. |

## Permissions model and access control

The Airtable connector enforces that only users who have access to a record in Airtable can see it in Copilot responses and search results. Permissions are based on workspace, base, and table access in Airtable. Identity mapping ensures that Airtable users are correctly matched to Microsoft Entra ID accounts. Admins can choose to index content as visible to everyone or enforce per-user permissions.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Airtable connector](airtable-deployment.md)
