---
title: Personal sync connectors overview
description: Get an overview of Personal sync Microsoft 365 Copilot connectors.
author: Lauragra
ms.author: lauragra
manager: calvind
ms.reviewer: vivg
ms.service: copilot-connectors
ms.date: 06/22/2026
ms.topic: overview
ms.localizationpriority: medium
ms.audience: Admin
---

# Personal sync connectors overview

> [!IMPORTANT]
> Personal sync connectors are currently in preview and available to a limited set of customers.

Microsoft 365 Copilot supports personal sync Copilot connectors so that individual users can bring their own external content into Copilot in a self-serve manner. By using a personal sync connector, each user authenticates to an external data source with their own credentials. Only the content that the user can access is synchronized and indexed into Microsoft Graph. The user is both the person who sets up the connection and the only person who can retrieve its content from the third-party source.

Unlike tenant configured sync connectors that an admin configures once for an entire tenant, users set up personal sync connectors per user. They're designed for sources where tenant-wide admin deployment isn't practical.

Personal sync connectors are Microsoft-published connectors only.

## What are personal sync connectors?

Personal sync Copilot connectors:

- Synchronize a user's external content into Microsoft Graph, scoped to that individual user.
- Connect by using the user's own identity, credentials, and consent in a self-serve manner.
- Make the user's connected content discoverable across Microsoft 365 Copilot experiences with Microsoft Graph relevance and security.
- Appear in the Microsoft 365 admin center as pre-enabled connectors that admins can make visible, hide, or disable for the tenant.
- When a user disconnects or an admin disables the connector, the indexed content is removed and synchronization stops.

## Supported Copilot experiences

Microsoft 365 Copilot supports personal sync connectors in the following experiences:

- Microsoft 365 Copilot Chat
- Microsoft 365 Copilot Search

## Supported data sources

The following connectors support the personal configuration model:

| Connector   | Crawled entities   | Crawl scope   |
|-------------|---------------|---------------|
| Confluence cloud | Wikis and blog posts | Crawls a user's complete personal space. For shared spaces, the connector crawls content that was created or modified in the past 90 days. |
| Jira cloud | Issues (Work Items) | The connector crawls work items that were created or modified in the past 90 days. |

Microsoft plans to add more data sources in future releases.

## How to connect and use personal sync connectors

1. Configure a personal sync connector from either the Microsoft 365 Copilot desktop app or [Web client](https://m365.cloud.microsoft/).

   > [!NOTE]
   > New personal sync connectors go through a seven-day admin review period before users can see them. If you don't see a connector, check with your admin.

1. Select the **+** button > **Change data sources**. Discover a connector in the **Change Sources** popup.

:::image type="content" source="media/personal-sync-connectors/add-change-sources.png" alt-text="Screenshot of the add button with change sources option" lightbox="media/personal-sync-connectors/add-change-sources.png":::

1. Select **Connect** and authenticate to the external data source with your own credentials. Accept the terms of connecting to the external data source.

:::image type="content" source="media/personal-sync-connectors/change-sources-popup.png" alt-text="Screenshot of the Change sources popup showing available data sources including connectors with Connect buttons" lightbox="media/personal-sync-connectors/change-sources-popup.png":::

1. The connector synchronizes your content into Microsoft Graph and notifies you when it's ready to use. Initial indexing can take 30 minutes to a few hours depending on the volume of content. Afterward, an incremental sync runs about every 15 minutes, with a full sync about every 7 days.

1. Copilot can use the synchronized content for your queries. It returns only content you have permission to see in the source.

You can disconnect at any time by going to **Settings** > **Sources**. Disconnecting removes the indexed content and stops synchronization.

## Related content

- [Manage personal sync connectors](manage-personal-sync-connectors.md)
- [Microsoft 365 Copilot connectors overview](overview.md)
