---
title: "Tableau Cloud connector overview"
ms.author: danielabo
author: danipocket
manager: calvind
ms.reviewer: lauragra
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 04/30/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Tableau Cloud Microsoft 365 Copilot connector."
---

# Tableau Cloud connector overview

The Tableau Cloud Copilot connector integrates Tableau Cloud sheets, including worksheets, dashboards, and stories, into Microsoft 365. After deployment, users can find and use Tableau Cloud analytics content in Copilot, Copilot Search, and Microsoft Search across apps such as Teams, Outlook, and SharePoint.

## Why use the Tableau Cloud connector to index your data?

Many organizations use Tableau Cloud as a primary analytics platform, but the content often remains isolated in Tableau sites and project hierarchies. The Tableau Cloud connector makes analytics content discoverable together with Microsoft 365 content, so users can find relevant dashboards and insights in their daily workflows.

The connector helps organizations:

- Improve discovery of analytics assets across the Microsoft 365 ecosystem.
- Reduce context switching between Microsoft 365 and Tableau Cloud.
- Speed up access to dashboards and reports needed for day-to-day work.
- Support faster decision-making with natural language experiences in Copilot.

The following table lists common use cases.

| Department or role | Use case | Benefit |
|---|---|---|
| Business analysts | Find dashboards related to specific KPIs or domains. | Faster access to analytics content |
| Team members | Retrieve sheets relevant to active projects. | Reduced context switching |
| Leadership | Get summaries of dashboards and key metrics. | Better decision support |

## Build agents with the Tableau Cloud connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that users can use to retrieve information from Tableau Cloud:

- Find Tableau Cloud dashboards related to Q1 sales.
- List Tableau Cloud sheets under the Marketing Analytics project.
- Summarize key insights from the Revenue Dashboard in Tableau.

## Tableau Cloud connector capabilities and limitations

The Tableau Cloud connector enables users to:

- Index published Tableau Cloud sheets, including worksheets, dashboards, and stories.
- Search Tableau Cloud analytics content from Microsoft 365 search and Copilot experiences.
- Apply semantic search in Copilot to retrieve relevant content based on keywords and context.
- Configure crawl frequency to balance freshness and performance.
- Build workflow and agent experiences in Copilot Studio using connector data.

The Tableau Cloud connector has the following limitations:

- Supports Tableau Cloud only; Tableau Server isn't supported.
- Doesn't index sheets in personal space.

## Data types indexed from Tableau Cloud

The connector indexes published Tableau Cloud sheets and associated metadata. You can surface and reference indexed content in Copilot, Copilot Search, and Microsoft Search.

By default, the connector crawls all published sheets in your Tableau Cloud instance, except sheets in personal space.

## Permissions model and access control

The Tableau Cloud connector respects Tableau Cloud access control behavior and layered permission evaluation. Microsoft 365 users can only see indexed content if they have access to the corresponding Tableau Cloud sheet.

The connector supports both of these identity mapping models:

- Microsoft Entra ID-based identity mapping.
- Non-AAD identity mapping through regex-based transformation.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Tableau Cloud connector](tableau-cloud-deployment.md)
