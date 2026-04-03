---
title: "Deploy the WordPress.org connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: rantang
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 12/12/2025
ms.localizationpriority: Medium
description: "Find information about how to deploy the WordPress.org Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the WordPress.org connector

Use the WordPress.org Microsoft 365 Copilot connector to index published posts and pages from WordPress.org websites so users can discover this content in Copilot and Microsoft Search. This article describes the steps to deploy and customize the connector.

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You're the AI administrator for your organization's Microsoft 365 tenant.
- You have the URL of your WordPress.org website.
- You have an admin account for your WordPress.org website with permission to create an application password (used for REST API authentication with external services).
- You installed and configured the [Microsoft Graph connector agent](/microsoft-365/copilot/connectors/connector-agent) on a host that can reach your WordPress.org instance.

## Deploy the connector

To add the WordPress.org connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **WordPress.org**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated item. The display name also signifies trusted content and is used as a content source filter.  
You can accept the default **WordPress.org** display name or customize the value to a name that users in your organization recognize. For more information, see [Enhance Copilot discovery of connector content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Set instance URL

Provide the WordPress.org website URL that you want the connector to crawl. This URL is the canonical site address used by your WordPress instance.

### Choose Microsoft Graph connector agent

Select the configured **Microsoft Graph connector agent** that bridges your WordPress.org instance and the connector APIs.

### Choose authentication type

The connector supports **basic authentication** using a WordPress **application password**. To enable and configure application passwords in WordPress, see the [Application Passwords integration guide](https://make.wordpress.org/core/2020/11/05/application-passwords-integration-guide/).

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to validate the connector before broad deployment. For more information, see [Staged rollout for Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The WordPress.org Copilot connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|---|---|
| Users | All published pages and posts indexed by the WordPress.org connector are visible to all Microsoft 365 users in your tenant from Microsoft Search or Copilot. |
| Content – Index content | All published posts and pages are selected by default. |
| Content – Manage properties | A default schema is applied to commonly used WordPress properties (see **Customize settings** for details). |
| Sync – Incremental crawl | Every 15 minutes. |
| Sync – Full crawl | Every day. |

To customize these values, choose **Custom setup** on the connector page.

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the WordPress.org connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

The connector doesn't crawl source identities or enforce item‑level permissions. All indexed published pages and posts are visible to all Microsoft 365 users in your tenant from Microsoft Search or Copilot.

### Customize content settings

#### Content ingestion filters

Specify conditions for indexed content. For example, choose whether to index **posts** or **pages**, and filter posts by specific **categories**. To verify property values and filters, choose **Preview results**.

#### Manage properties

You can add or remove properties from your WordPress.org data source, assign a schema (searchable, queryable, retrievable, refinable), change the semantic label, and add aliases. The following table lists common properties and their default schema attributes.

The following table lists default properties and their schema.

| Property | Semantic label | Description | Schema attributes |
|---|---|---|---|
| Author | Authors | Name of the person designated as the author of the post or page. | Search, Query, Retrieve |
| Categories | — | Categories associated with posts (not available for pages). | Query, Retrieve, Refine |
| Content | — | Body content of posts or pages. | Search, Retrieve |
| Created | Created date time | Date and time the item was created in WordPress. | Query, Retrieve |
| CreatedBy | Created by | User who created the post or page. | Search, Query, Retrieve |
| Excerpt | — | Summary of the post or page content. | Search, Retrieve |
| Id | — | Unique identifier of the post or page. | Query, Retrieve |
| Tags | — | Tags associated with the post or page. | Query, Retrieve, Refine |
| Title | Title | Title of the post or page as shown in Copilot and search experiences. | Search, Query, Retrieve |
| Type | — | Item type: **Post** or **Page**. | Search, Query, Retrieve, Refine |
| Updated | Last modified date time | Date and time the item was last modified. | Query, Retrieve |
| UpdatedBy | Last modified by | User who most recently edited the item. | Search, Query, Retrieve |
| Url | url | Target URL of the item in WordPress. | Retrieve |

### Customize sync intervals

Configure **Full crawl** and **Incremental crawl** schedules to fit your refresh needs. By default, incremental crawl runs every 15 minutes and full crawl runs every day. For more information, see [Guidelines for sync settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [WordPress.org connector overview](wordpress-onpremises-overview.md)
- [Troubleshoot issues with the WordPress.org connector](wordpress-onpremises-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)
