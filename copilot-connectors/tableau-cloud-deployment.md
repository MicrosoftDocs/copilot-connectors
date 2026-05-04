---
title: "Deploy the Tableau Cloud connector"
ms.author: danielabo
author: danipocket
manager: calvind
ms.reviewer: lauragra
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 04/30/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the Tableau Cloud Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Tableau Cloud connector

The Tableau Cloud Microsoft 365 Copilot connector integrates Tableau Cloud items into Microsoft 365 experiences so users can discover and use published analytics content in Copilot, Copilot Search, and Microsoft Search. This article describes the steps to deploy and customize the Tableau Cloud connector.


## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be an AI Administrator for your organization’s Microsoft 365 tenant.
- You must have Tableau Cloud site admin access.
- Your Tableau Cloud environment must be configured with a connected app that uses direct trust.
- You must have the required Tableau connected app values: client ID, app secret ID, and secret key.
- You must have an admin user email for Tableau Cloud that can access the sheets you want to index.


## Deploy the connector

To add the Tableau Cloud connector for your organization:
- In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
- Choose the **Gallery** tab.
- From the list of available connectors, choose **Tableau Cloud**.

### Set display name

The display name identifies references in Copilot responses, so users can recognize the associated file or item. The display name also signifies trusted content and acts as a content source filter.

You can accept the default **Tableau Cloud** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

### Set instance URL

Enter your Tableau Cloud site instance URL. The URL typically uses the following format:

`https://<your-domain>.online.tableau.com/#/site/<site-name>`

### Choose authentication type

Use Tableau Connected Apps with Direct Trust to authenticate the connector.

To configure and use Direct Trust authentication:

1. Sign in to Tableau Cloud as a site admin.
1. Go to **Settings** > **Connected Apps**.
1. Choose **New Connected App** > **Direct Trust**.
1. In the connected app form, provide the required settings:

| Field | Description | Recommended value |
|---|---|---|
| Connected app name | Unique value that identifies the app that requires Direct Trust. | Microsoft Search and Copilot |
| Access level | Controls which content can be embedded. | All projects (or Only one project, if required) |
| Domain allowlist | Domains where content can be embedded. | All domains |

1. Choose **Create**, then enable the connected app.
1. On the connected app details page, choose **Generate New Secret**.
1. Save the **Client ID**, **Secret ID**, and **Secret Value**.
1. In the connector authentication pane in Microsoft 365 admin center, provide the required values:

| Field | Description |
|---|---|
| User | Admin user email. Use the admin account that configured Tableau Connected Apps with Direct Trust. |
| Connected App Client ID | Client ID from the Tableau Connected App. |
| Connected App Secret ID | Secret ID from the Tableau Connected App. |
| Connected App Secret Value | Secret value from the Tableau Connected App. |

### Rollout

Roll out to a limited audience first if you want to validate the connector behavior in Copilot and Search before a broader rollout.

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](staged-rollout.md).

Choose **Create** to deploy the connection. The Tableau Cloud Copilot connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|---------------|
| Users | Access permissions: Only people with access to this data source. Identity mapping: Data source identities mapped using Microsoft Entra IDs. |
| Content | All sheets except sheets in personal space. |
| Sync | Incremental crawl every 15 minutes. Full crawl every day. |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Tableau Cloud connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

The Tableau Cloud connector supports these access options:

- **Only people with access to this data source** (recommended)
- **Everyone**

If you choose **Everyone**, indexed data appears in search results for all users.

When you use **Only people with access to this data source**, the connector applies permission evaluation logic similar to Tableau ACL behavior so content isn't overshared.

#### Map identities

When you use **Only people with access to this data source**, choose the identity type that matches your tenant:

- **Microsoft Entra ID**: Use this option when Tableau user email addresses match Microsoft Entra user principal names (UPN).
- **Non-AAD**: Use this option when Tableau user email addresses don't match Microsoft Entra UPN values. Configure regex-based identity mapping for this case.

Updates to users or groups that govern access permissions sync during full crawls only.

### Customize content settings

#### Query string

By default, the connector indexes all published Tableau Cloud sheets in supported project scopes, excluding sheets in personal space. Use content ingestion filters to narrow the indexed content.

#### Manage properties

Review and configure indexed properties, including schema attributes, semantic labels, and aliases.

| Property | Semantic label | Description | Schema attributes |
|---|---|---|---|
| createdAt | created date time | Timestamp when the sheet was created. | Query, Retrieve |
| iconUrl | iconUrl | Icon URL for worksheet, dashboard, or story item types. | Retrieve |
| itemPath | itemPath | Hierarchical project path of the Tableau item. | Query, Retrieve, Search |
| lastModifiedBy | last modified by | User who last modified the sheet. | Query, Retrieve, Search |
| name | Title | Display name of the sheet. | Query, Retrieve, Search |
| projectName | none | Parent project name for the sheet. | Query, Search |
| sheetType | itemType | Sheet type, such as worksheet, dashboard, or story. | Query, Refine, Retrieve |
| sheetUrl | uRL | Direct link to the sheet in Tableau. | Retrieve |
| tags | Tags | Tags assigned to the sheet. | Query, Refine, Retrieve |
| updatedAt | last modified date time | Timestamp of the most recent change. | Query, Retrieve |
| workbookName | containerName | Workbook that contains the sheet. | Query, Retrieve, Search |
| workbookUrl | containerUrl | URL of the workbook that contains the sheet. | Retrieve |

### Customize sync intervals

You can configure full and incremental crawls based on scheduling options. The default values are:

- Full crawl - Every 15 minutes.
- Incremental crawl - Every day.

By default, incremental crawl runs every 15 minutes and full crawl runs every day.

Adjust these schedules to fit your data refresh needs. For more information, see [Guidelines for sync settings](deployment-overview.md#guidelines-for-crawl-settings).

## Related content

- [Tableau Cloud connector overview](tableau-cloud-overview.md)
- [Troubleshoot issues with the Tableau Cloud connector](tableau-cloud-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](deployment-overview.md)
