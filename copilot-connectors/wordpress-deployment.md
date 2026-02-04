---
title: "Deploy the WordPress.com Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: rantang
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 12/11/2025
ms.localizationpriority: Medium
description: "Find information about how to deploy the WordPress.com Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the WordPress.com Microsoft 365 Copilot connector

The WordPress.com Microsoft 365 Copilot connector indexes published posts and pages from WordPress.com websites so users can discover and use that content in Microsoft 365 Copilot and Microsoft Search experiences. This article describes the steps to deploy and customize the WordPress.com connector. After you create the connection, Copilot and Microsoft Search can surface published posts and pages from your WordPress.com–built websites.

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You're a Microsoft 365 search admin or an administrator with permissions to create Copilot connectors.
- You have your organization's WordPress.com website URL.
- You have OAuth 2.0 credentials in the WordPress.com Developer Center for the site or sites that you plan to index.

## Deploy the connector

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
2. Go to the **Connectors** tab, and in the left pane, choose **Gallery**.
3. From the list of available connectors, choose **WordPress.com**.

### Set display name

The display name is used to identify references in Copilot responses so users can recognize the associated item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default WordPress.com display name or customize the value to use a name that users in your organization recognize. For more information about display names and descriptions, see [Enhance Copilot discovery of connector content](/microsoft-365-copilot/connectors/enhancing-microsoft-copilot-discovery-with-graph-connector-content).

### Set instance URL

Enter the WordPress.com website URL for the site whose published posts and pages you want to index (for example, `https://contoso.wordpress.com`). Use the canonical site address.

### Choose authentication type

Use WordPress.com OAuth 2.0 for authentication. A WordPress.com site admin creates an OAuth application in the [WordPress.com Developer Center](https://developer.wordpress.com/apps/new/). The connector uses the client ID and client secret to authorize crawl access. OAuth 2.0 allows applications to interact with blogs on WordPress.com–built sites running Jetpack. For more information, see [WordPress.com OAuth 2.0](https://developer.wordpress.com/docs/oauth2/).

Use the information in the following table to fill out the OAuth application form. All the fields listed are required.

| Field | Description | Recommended value |
|----|----|---|
| Name | Unique value that identifies the application that you require OAuth access for. | Microsoft Search and Copilot |
| Description | A short description of the OAuth client. | Use an appropriate description. |
| Website URL | The URL to an informational home page about your application. | Your WordPress.com–built website URL. |
| Redirect URL | The callback URL that the authorization server redirects to. | Microsoft 365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`<br /><br />Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback` |
| Type | Application app type. | Web |

After the OAuth app is created, enter the client ID and client secret in the connector, and then authenticate with a WordPress.com site admin account to grant crawl permissions.

### Roll out

To validate the connector before you deploy it to your organization, you can roll it out to a limited audience. Choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](/microsoft-365-copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The WordPress.com connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----|----|
| Users | Access permissions: Because the connector doesn't ingest WordPress.com identities or page permissions, all indexed published posts and pages are visible to all Microsoft 365 users in your tenant from Copilot and Microsoft Search. |
| Content | Index content: All published posts and pages are selected by default.<br />Filters: You can choose to index posts or pages, and you can include post categories. |
| Sync | Incremental crawl: Every 15 minutes.<br />Full crawl: Every day. |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the WordPress.com connector settings. On the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

WordPress.com content indexed by the connector is visible tenant‑wide. The connector doesn't crawl identities or page‑level permissions.

#### Mapping identities

Not applicable. The connector doesn't crawl WordPress.com user identities.

### Customize content settings

#### Content filter

Specify whether to index posts, pages, or both. You can also filter posts by categories. To verify property values and filters before you publish changes, choose **Preview data**.

#### Manage properties

The connector indexes the properties listed in the following table by default. The table lists semantic labels and typical schema settings.

| Property | Semantic label | Description | Schema attributes |
|----|----|----|----|
| Author | Authors | Name of the author of the post or page. | Search, Query, Retrieve |
| AuthorEmail | (none) | Email of the author of the post or page. | Search, Retrieve |
| Categories | (none) | Categories applied to posts (not available for pages). | Query, Retrieve, Refine |
| Content | (none) | Body content of posts or pages. | Search, Retrieve |
| Created | Created date time | Date and time the item was created. | Query, Retrieve |
| CreatedBy | Created by | Creator of the item. | Search, Query, Retrieve |
| Excerpt | (none) | Summary of post or page content. | Search, Retrieve |
| IconUrl | IconUrl | URL of the icon. | Retrieve |
| Id | (none) | Unique identifier of the post or page. | Query, Retrieve |
| Likes | (none) | Number of likes for the post or page. | Query, Retrieve |
| Slug | (none) | URL‑friendly identifier for the post or page. | Query, Retrieve, Search |
| Tags | (none) | Tags applied to the post or page. | Query, Retrieve, Search |
| Title | Title | Title of the post or page. | Query, Retrieve, Search |
| Type | (none) | Content type (Post or Page). | Query, Retrieve, Refine, Search |
| Updated | Last modified date time | Date and time the item was last modified. | Query, Retrieve |
| UpdatedBy | Last modified by | Most recent editor of the item. | Search, Query, Retrieve |
| Url | url | Target URL of the item. | Retrieve |

### Customize sync intervals

You can configure full and incremental crawls to meet your data refresh needs. By default, incremental crawls run every 15 minutes, and full crawls run daily. 

For more information, see [Guidelines for sync settings](/microsoft-365-copilot/connectors/deployment-overview#guidelines-for-sync-settings).

## Related content

- [WordPress.com connector overview](wordpress-overview.md)
- [Troubleshoot issues with the WordPress.com connector](wordpress-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365-copilot/connectors/deployment-overview)
