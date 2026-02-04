---
title: "Freshservice Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: wangchen
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 11/25/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Freshservice Microsoft 365 Copilot connector."
---

# Freshservice Microsoft 365 Copilot connector overview

The Freshservice Microsoft 365 Copilot connector enables your organization to index Freshservice solution article data to make it available to Microsoft 365 Copilot and Microsoft Search. This connector is designed for Microsoft 365 administrators or anyone who configures, runs, and monitors the Freshservice Copilot connector.

## Why use the Freshservice connector to index your data?

The Freshservice connector allows organizations to unlock knowledge stored in Freshservice solution articles and make it accessible through Copilot and Microsoft Search. Common scenarios include:

- Improve onboarding by summarizing guides, policies, and FAQs for new employees.
- Allow IT support teams to retrieve troubleshooting steps or runbooks directly from Freshservice.
- Allow engineering and DevOps teams to access design documents, retrospectives, and deployment guides.
- Support product management with quick access to release plans, feature specifications, and team wikis.
- Help sales and marketing teams discover case studies, messaging documents, and campaign plans.
- Empower executives and managers to ask Copilot for summaries of policy or project updates for faster decision-making.

The following table lists common use cases for the Freshservice connector.

| Department/role      | Use case    | Business benefit|
|----------------------|-------------|-----------------|
| People               | Summarize onboarding guides, policies, FAQs          | Faster onboarding; reduced dependency on HR staff. |
| IT support/help desk | Retrieve troubleshooting steps or runbooks from Freshservice via Copilot | Faster ticket resolution; improved consistency. |
| Engineering/DevOps   | Access design docs, retrospectives, deployment guides| Reduced context switching; faster execution. |
| Product management   | Query release plans, feature specs, team wikis       | Better alignment; faster planning cycles. |
| Sales/marketing      | Discover case studies, messaging docs, campaign plans| Improved collaboration; reduced duplicated work. |
| Executives/managers  | Ask Copilot for summaries of policy or project updates| Faster decision-making; better visibility. |

## Build agents with the Freshservice connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/copilot-studio-agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Agent prompts

The following are examples of prompts that agent builders can use to help users retrieve information from Freshservice:

- Summarize the onboarding guide for new hires.
- Retrieve the latest troubleshooting steps for password reset issues.
- List all deployment guides for the engineering team.
- Show recent policy updates relevant to managers.
- Find case studies related to our latest marketing campaign.

## Freshservice connector capabilities and limitations

The Freshservice connector enables users to:

- Access Freshservice solution articles using the power of semantic search.
- Customize crawl frequency to fit organizational needs.
- Create workflows by using this connection and plugins from Microsoft Copilot Studio.

The Freshservice connector has the following limitation:

- Solution articles are indexed only if they're stored in folders set to be visible to **All**.

## Data types indexed from Freshservice

The connector indexes Freshservice solution articles, including the following properties.

| Property           | Label/Field           | Description                                 |
|--------------------|----------------------|---------------------------------------------|
| Id                 | Not applicable       | Unique ID of the solution article.          |
| url                | `url`                | URL of the solution article.                |
| Title              | `title`              | Title of the solution article.              |
| CreatedOn          | `createdDateTime`    | The time when the solution article was created. |
| LastModifiedOn     | `lastModifiedDateTime` | The time when the solution article was last modified. |
| LastModifiedUser   | `lastModifiedBy`     | The name of the user who last modified the solution article. |
| FolderUrl          | `containedUrl`       | The URL of the folder containing the solution article. |
| FolderName         | `containerName`      | The name of the folder containing the solution article. |
| Author             | `createdBy`          | The name of the user who created the solution article. |
| CategoryName       |                      | The category the folder belongs to.   |
| DescriptionText    |                      | The content of the solution article.        |
| Keywords           |                      | The keywords of the solution article.       |
| Tags               |                      | The tags associated with the solution article. |

## Permissions model and access control

Only public solution articles with folder visibility set to **All** are indexed using the Freshservice Copilot connector. These solution articles are visible to all Microsoft 365 users in your tenant, from Microsoft Search or Copilot.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Freshservice connector](freshservice-deployment.md)