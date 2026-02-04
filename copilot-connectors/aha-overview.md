---
title: "Aha! Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 01/08/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Aha! Microsoft 365 Copilot connector."
---

# Aha! Microsoft 365 Copilot connector overview

The Aha! Features and Ideas Microsoft 365 Copilot connectors empower your organization to index and search Aha! features and ideas across your enterprise. After you configure the connector, it automatically crawls Aha! features and ideas and makes them discoverable through Microsoft 365 Copilot and any Microsoft Search client. This indexing allows users to find relevant product management content and drive collaboration across teams.

## Why use the Aha! connector to index your data?

The Aha! connector is designed for organizations that use Aha! to manage product features and ideas. Common scenarios and use cases include:

- Enable product managers and engineering teams to quickly search for and retrieve Aha! features and ideas from within Microsoft 365 Copilot.
- Support cross-functional teams by surfacing Aha! content in Copilot and Microsoft Search experiences.
- Streamline workflows by making Aha! data available for automation and agent-driven actions.

## Build agents with the Aha! connector

Developers can use the Aha! connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Agent prompts

The following examples show prompts that users can use to retrieve information from Aha!:

- List all features assigned to me in Aha!.
- Show ideas with the highest number of votes.
- Find features planned for the next release.
- Retrieve ideas created by my team last quarter.

## Aha! connector capabilities and limitations

The Aha! connector enables users to:

- Index features and ideas from your Aha! workspace.
- Customize crawl frequency to control how often data is refreshed.
- Create workflows using this connection and plugins from Microsoft Copilot Studio.
- Use semantic search in Copilot to enable users to find relevant content.

The Aha! connector has the following limitations:

- The connector doesn't index comments.
- The connector doesn't index customized fields.

## Data types indexed from Aha!

The connector indexes the following data types from Aha!:

- Features: Includes properties such as assigned user, created date, description, epic name, status, tags, and more.
- Ideas: Includes properties such as assigned user, categories, created date, description, status, votes, and more.

Indexed content is surfaced in Microsoft 365 Copilot and Microsoft Search results, making it accessible to users with appropriate permissions.

## Permissions model and access control

Permissions to Aha! data in Copilot and search results are managed as follows:

- Only users with access to the content in the Aha! data source can view indexed items.
- Data source identities are mapped using Microsoft Entra IDs to ensure secure access control.
- Access permissions and identity mapping can be customized during connector setup.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Aha! connector](aha-deployment.md)
