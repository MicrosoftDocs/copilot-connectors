---
title: "Shortcut Story Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 01/15/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Shortcut Story Microsoft 365 Copilot connector."
---

# Shortcut Story Microsoft 365 Copilot connector overview

The Shortcut Story Microsoft 365 Copilot connector empowers your organization to index and search Shortcut stories across your enterprise. After you configure and deploy the connector, it automatically crawls Shortcut stories, making them easily discoverable through Microsoft 365 Copilot and any Microsoft Search client. 

## Why use the Shortcut Story connector to index your data?

Organizations use the Shortcut Story connector to:

- Enable enterprise-wide search and discovery of Shortcut stories.
- Integrate Shortcut story data into Copilot and Microsoft Search experiences.
- Support workflows and plugins built in Microsoft Copilot Studio.
- Enhance semantic search capabilities for Shortcut content.

Common use cases include:

- Project management teams surfacing Shortcut stories for status updates.
- Engineering teams retrieving story details for sprint planning.
- Support teams accessing Shortcut stories for troubleshooting and knowledge sharing.

## Build agents with the Shortcut Story connector

Developers can use the Shortcut Story connector as a knowledge source in declarative agents built with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Agent prompts

Agent builders can use the following prompts to help users retrieve information from Shortcut stories by department or role:

| Department      | Example prompt                                                      |
|-----------------|--------------------------------------------------------------------|
| Project Management    | Show all Shortcut stories assigned to my team this month.     |
| Engineering     | List stories with the 'Blocked' label in the current sprint.        |
| Support         | Find Shortcut stories updated in the last week for product X.      |

## Shortcut Story connector capabilities and limitations

The Shortcut Story connector enables users to:

- Index stories from your Shortcut workspace.
- Customize crawl frequency for story updates.
- Create workflows using this connection and plugins from Microsoft Copilot Studio.
- Use semantic search in Microsoft 365 Copilot to find relevant Shortcut content.

The connector has the following limitations:

- Only stories from the most recent two-year period are crawled.
- Comments and customized fields in Shortcut are not indexed.

## Data types indexed from Shortcut

The connector indexes the following Shortcut story properties:

- Blocked
- CreatedBy
- CreatedOn
- Description
- DueDate
- EpicId
- EpicName
- Estimate
- Id
- IterationId
- IterationName
- Labels
- Name
- Owners
- StoryType
- TeamName
- Url
- UpdatedBy
- UpdatedOn
- Workspace



The connector doesn't index comments or customized fields.

## Permissions model and access control

Access to indexed Shortcut stories is controlled as follows:

- Only users with access to content in the Shortcut data source can view indexed stories.
- Data source identities are mapped using Microsoft Entra IDs.
- Admins can configure access permissions and map identities during connector setup.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Shortcut Story connector](shortcut-story-deployment.md)
