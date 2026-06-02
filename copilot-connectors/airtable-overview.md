---
title: "Airtable connector overview (preview)"
ms.author: kailiang
author: Kai-Cloud
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 05/27/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Airtable Microsoft 365 Copilot connector."
---

# Airtable connector overview (preview)

The Airtable Microsoft 365 Copilot connector integrates Airtable records into Microsoft 365. This integration allows Copilot, Copilot Search, and Microsoft Search to surface relevant record information directly within apps like Microsoft Teams, Outlook, and SharePoint. When you configure the Airtable connector for your organization and index data from Airtable bases, users can search for Airtable records in Microsoft 365 experiences. The connector improves project tracking, operational visibility, and overall productivity.

> [!NOTE]
> The Airtable connector is currently in preview. Connector functionality and requirements are subject to change.

## Why use the Airtable connector to index your data?

Organizations that use Airtable to manage projects, operations, and structured data often face challenges surfacing that information alongside the content their teams work with every day. The Airtable connector addresses these challenges by integrating Airtable records into Microsoft 365. This integration allows employees to find Airtable records within Copilot and everyday apps like Teams, Outlook, or SharePoint, without leaving their flow of work.

The Airtable connector provides the following benefits:

- **Boosts productivity** – Access Airtable records directly within Microsoft 365 apps, reducing time spent switching platforms.
- **Improves decision-making** – Unified search across Airtable and Microsoft tools ensures faster access to record information.
- **Enhances collaboration** – Teams can easily track and reference records across bases without leaving Microsoft 365.
- **Preserves security and compliance** – The connector respects Airtable permissions so that content is only visible to authorized users.

## Build agents with the Airtable connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that users can use to retrieve information from Airtable:

- "Show me all active projects in Airtable."
- "What are the high-priority tasks assigned to me in Airtable?"
- "Find Airtable records created in the last week."
- "Summarize the status of all marketing campaigns in Airtable."
- "What are the key deliverables for Q2 in our Airtable project tracker?"

## Airtable connector capabilities and limitations

The Airtable connector enables you to:

- Index Airtable records from selected bases and tables.
- Perform natural language queries in Copilot to retrieve record information.
- Use semantic search to find relevant content based on keywords and context.
- Access record data directly within Microsoft 365 apps.

The Airtable connector has the following limitations:

- It doesn't index attachments or record comments.
- It doesn't index views, automations, interfaces, or other entities beyond records.
- It requires identity mapping if Airtable user emails differ from Microsoft Entra ID user principal names (UPNs).

## Data types indexed from Airtable

The Airtable connector indexes record-level data. By default, the connector crawls all accessible bases in your Airtable enterprise account.

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
