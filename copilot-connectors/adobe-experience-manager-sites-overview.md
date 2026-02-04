---
title: "Adobe Experience Manager Sites Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: rantang
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 12/10/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Adobe Experience Manager Sites Microsoft 365 Copilot connector."
---

# Adobe Experience Manager Sites Microsoft 365 Copilot connector overview

With the Adobe Experience Manager Sites Microsoft 365 Copilot connector, your organization can index published webpages from Adobe Experience Manager (AEM) Sites so people can discover and use them across Microsoft 365 Copilot and Microsoft Search. After configuration and indexing, end users can search for those published webpages in Copilot and any Microsoft Search client, helping teams reuse trusted web content without switching tools.

## Why use the Adobe Experience Manager Sites connector to index your data?

Many organizations publish customer-facing and internal sites in AEM. These pages often contain canonical product information, announcements, and help content that employees need at their fingertips. The AEM Sites connector brings those published webpages into Copilot and Microsoft Search so people can:

- Find authoritative site content from within Microsoft 365 and reference it directly in Copilot responses.
- Reduce context switching by querying AEM Sites content alongside other Microsoft 365 sources.
- Build workflows that tap AEM Sites content via Copilot Studio.

### Use cases

The following are common use cases for the Adobe Experience Manager Sites connector:

- Marketing and web teams validate messaging by querying the latest published pages in Copilot.
- Support and field teams surface how-to pages and announcements from AEM Sites during customer conversations.
- Content strategists connect site sections to agent workflows through Copilot Studio.

## Build agents with the Adobe Experience Manager Sites connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Agent prompts

The following examples show prompts that agent builders can use to help their users retrieve information from Adobe Experience Manager Sites:

- Find the latest published page for the Contoso Q3 campaign.
- Show site pages that match the path `/content/contoso/products/*`.
- Summarize the product overview page and extract key specs.
- List pages tagged with `release-notes` published in the last week.

## Adobe Experience Manager Sites connector capabilities and limitations

The Adobe Experience Manager Sites connector enables users to:

- Index published webpages from AEM Sites.
- Configure ingestion filters based on page paths (exact matches and Java regular expressions).
- Customize crawl frequency for full and incremental crawls.
- Create workflows using this connection and plugins from Copilot Studio.
- Improve discovery with semantic search in Copilot.

The Adobe Experience Manager Sites connector has the following limitations:

- Comments aren't indexed.
- User identities and access permissions aren't crawled. All published webpages that are indexed are visible to all Microsoft 365 users in your tenant.

## Data types indexed from Adobe Experience Manager Sites

By default, the connector indexes published pages and their associated properties (for example, title, description, navigation title, tags, link, and timestamps). 

The **Manage properties** settings expose default properties—such as **Title**, **Description**, **Navigation Title**, **Tags**, **Link**, **CreatedTime**, **ModifiedTime**, and **PublishedTime**—and allow admins to adjust schema flags (searchable, queryable, retrievable) to shape how content appears in results.

## Permissions model and access control

All published webpages indexed by the AEM Sites connector are visible to all Microsoft 365 users in your tenant from Microsoft Search or Copilot. If you want to validate the connection with a smaller population before you deploy it, roll the connector out to a limited audience.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Adobe Experience Manager (AEM) Sites connector](adobe-experience-manager-sites-deployment.md)
