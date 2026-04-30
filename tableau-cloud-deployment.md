---
title: "Deploy the Tableau Cloud connector"
ms.author:
author:
manager:
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 04/30/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the Tableau Cloud Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Tableau Cloud connector

The Tableau Cloud Copilot connector integrates Tableau Cloud items into Microsoft 365 experiences so users can discover and use published analytics content in Copilot, Copilot Search, and Microsoft Search.

This article describes the steps to deploy and customize the Tableau Cloud connector.

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You are a Search admin for your organization's Microsoft 365 tenant.
- You have Tableau Cloud site admin access.
- Your Tableau Cloud environment is configured with a Connected App that uses Direct Trust.
- You have the required Tableau Connected App values: Connected App Client ID, Connected App Secret ID, and Connected App Secret Key.
- You have an admin user email for Tableau Cloud that can access the sheets that you want to index.

> [!NOTE]
> The connector supports Tableau Cloud only. Tableau Server is not supported. Sheets in personal space are not indexed.

## Deploy the connector

To add the Tableau Cloud connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **Tableau Cloud**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

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

5. Choose **Create**, then enable the connected app.
6. On the connected app details page, choose **Generate New Secret**.
7. Save the **Client ID**, **Secret ID**, and **Secret Value**.
8. In the connector authentication pane in Microsoft 365 admin center, provide the required values:

| Field | Description |
|---|---|
| User | Admin user email. Use the admin account that configured Tableau Connected Apps with Direct Trust. |
| Connected App Client ID | Client ID from the Tableau Connected App. |
| Connected App Secret ID | Secret ID from the Tableau Connected App. |
| Connected App Secret Key | Secret value from the Tableau Connected App. |

### Roll out

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

When you use **Only people with access to this data source**, the connector applies permission evaluation logic similar to Tableau ACL behavior so content is not overshared.

#### Map identities

When you use **Only people with access to this data source**, choose the identity type that matches your tenant:

- **Microsoft Entra ID**: Use this option when Tableau user email addresses match Microsoft Entra user principal names (UPN).
- **Non-AAD**: Use this option when Tableau user email addresses do not match Microsoft Entra UPN values. Configure regex-based identity mapping for this case.

Updates to users or groups that govern access permissions are synced during full crawls only.

### Customize content settings

#### Query string

By default, the connector indexes all published Tableau Cloud sheets in supported project scopes, excluding sheets in personal space. You can use content ingestion filters to narrow the indexed content.

#### Manage properties

You can review and configure indexed properties, including schema attributes, semantic labels, and aliases.

| Property | Semantic label | Description | Schema attributes |
|---|---|---|---|
| CreatedAt | Created date time | Timestamp when the sheet was created. | Query, Retrieve |
| IconUrl | IconUrl | Icon URL for worksheet, dashboard, or story item types. | Retrieve |
| ItemPath | ItemPath | Hierarchical project path of the Tableau item. | Query, Retrieve, Search |
| LastModifiedBy | Last modified by | User who last modified the sheet. | Query, Retrieve, Search |
| Name | Title | Display name of the sheet. | Query, Retrieve, Search |
| ProjectName | None | Parent project name for the sheet. | Query, Search |
| SheetType | ItemType | Sheet type, such as worksheet, dashboard, or story. | Query, Refine, Retrieve |
| SheetUrl | URL | Direct link to the sheet in Tableau. | Retrieve |
| Tags | Tags | Tags assigned to the sheet. | Query, Refine, Retrieve |
| UpdatedAt | Last modified date time | Timestamp of the most recent change. | Query, Retrieve |
| WorkbookName | ContainerName | Workbook that contains the sheet. | Query, Retrieve, Search |
| WorkbookUrl | ContainerUrl | URL of the workbook that contains the sheet. | Retrieve |

### Customize sync intervals

You can customize two refresh intervals:

- Full crawl
- Incremental crawl

By default, incremental crawl runs every 15 minutes and full crawl runs every day.

For more information, see [Guidelines for sync settings](deployment-overview.md#guidelines-for-sync-settings).

## Related content

- [Tableau Cloud connector overview](tableau-cloud-connector-overview.md)
- [Troubleshoot issues with the Tableau Cloud connector](tableau-cloud-connector-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](deployment-overview.md)
