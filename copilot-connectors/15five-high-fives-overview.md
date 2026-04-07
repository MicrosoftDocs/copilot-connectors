---
title: "15Five High Fives connector overview"
ms.author: lauragra
author: wangchen
manager: zezhangzhao
ms.reviewer: wangchen
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 04/06/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the 15Five High Fives Microsoft 365 Copilot connector."
---

# 15Five High Fives connector overview

The 15Five High Fives Microsoft 365 Copilot connector enables your organization to index 15Five high-five data to make it available to Microsoft 365 Copilot and Microsoft Search. 

## Why use the 15Five High Fives connector

Organizations can use this connector to support the following scenarios:

- Enable employees to discover recognition and feedback shared across the organization.
- Improve visibility into team appreciation and engagement signals.
- Retrieve High Fives content through semantic search in Microsoft 365 Copilot.
- Use indexed recognition data to inform people-focused insights and workflows.

## Build agents with the 15Five High Fives connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that users can use to retrieve information from the 15Five High Fives connector.

| Role | Prompt |
|------|--------|
| Manager | Show recent high fives received by my team members. |
| HR | Find examples of employee recognition shared across departments. |
| Team lead | Who has received high fives this month for collaboration? |
| Employee | Show the most recent high fives shared in my organization. |

## 15Five High Five connector capabilities and limitations

This connector enables users to:

- Access 15Five High Fives content through semantic search.
- Retrieve recognition data within Microsoft 365 Copilot and Microsoft Search.
- Customize crawl frequency to match data refresh needs.
- Create workflows by using this connection and plugins from Microsoft Copilot Studio.

This connector has the following limitation:

- It indexes only public high fives.

## Data types indexed from 15Five High Fives

The 15Five High Fives data source indexes the following properties.

| Source property | Label | Description |
|-----------------|--------|-------------|
| Text | Not applicable | Description of the high-five content. |
| CreatorEmail | Not applicable | Email of the user who gives a high five. |
| CreatorName | createdBy | Name of the user who gives a high five. |
| Receivers | Not applicable | Names of the users who receive a high five. |
| CreateTime | createdDateTime | The time when the high five was created. |
| UpdateTime | lastModifiedDateTime | The last time the high five was modified. |

## Permissions model and access control

All Microsoft 365 users in your tenant can see 15Five High Fives data indexed through the 15Five High Fives connector in Microsoft Search or Microsoft 365 Copilot.

## Next step

> [!div class="nextstepaction"]
> [Deploy the 15Five High Fives connector](15five-high-fives-deployment.md)