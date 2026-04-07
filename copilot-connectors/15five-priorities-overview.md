---
title: "15Five Priorities connector overview"
ms.author: lauragra
author: wangchen
manager: zezhangzhao
ms.reviewer: wangchen
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 04/07/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the 15Five Priorities Microsoft 365 Copilot connector."
---

# 15Five Priorities connector overview

The 15Five Priorities Microsoft 365 Copilot connector enables your organization to index 15Five priority data so the data surfaces in Microsoft 365 Copilot and Microsoft Search experiences. 

## Why use the 15Five Priorities connector

The 15Five Priorities Microsoft 365 Copilot connector enables your organization to index 15Five priority data so the data surfaces in Microsoft 365 Copilot and Microsoft Search experiences.

Organizations can use this connector to support the following scenarios:

- Enable users to discover employee priorities by using semantic search in Microsoft 365 Copilot.
- Surface priority status and ownership information in Microsoft Search results.
- Create workflows that use priority data by integrating with Microsoft Copilot Studio plugins.

## Build agents with the 15Five Priorities connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that users can use to retrieve information from 15Five Priorities:

| Department | Example prompt |
|------------|----------------|
| Dynamics 365 Human Resources | What priorities has my team submitted? |
| Management | Show the current status of priorities for my direct reports. |
| Leadership | Summarize employee priorities across my organization. |

## 15Five Priorities connector capabilities and limitations

This connector enables users to:

- Access 15Five priorities by using semantic search.
- Retrieve priority descriptions and status information in Copilot responses.
- Use indexed priority data in workflows created with Microsoft Copilot Studio plugins.

This connector has the following limitation:

- Only the employee and their direct manager can access the priority data by using Microsoft 365 Copilot and Microsoft Search.

## Data types indexed from 15Five Priorities

The following properties are indexed from the 15Five Priorities data source.

| Source property | Label | Description |
|-----------------|--------|-------------|
| Text | Not applicable | Description of the priority. |
| Status | Not applicable | Status of the priority. |
| UserEmail | Not applicable | Email of the priority submitter. |
| ManagerEmail | Not applicable | Email of the manager of the submitter. |
| CreateTime | createdDateTime | The time at which the priority was created. |
| UpdateTime | lastModifiedDateTime | The last time the priority was modified. |

## Permissions model and access control

The source system determines access permissions for indexed priority data. You can choose whether indexed data is visible to everyone in the organization or only to users who have access to the data source.

## Next step

> [!div class="nextstepaction"]
> [Deploy the connector](15five-priorities-deployment.md)