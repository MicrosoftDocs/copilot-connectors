---
title: "Deploy the Shortcut Story connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 01/15/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the Shortcut Story Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Shortcut Story connector

The Shortcut Story connector allows your organization to index Shortcut stories and make them discoverable in Microsoft 365 Copilot and Microsoft Search. This article describes the steps to deploy and customize the Shortcut Story connector.

## Prerequisites

Before you deploy the Shortcut Story connector, make sure that:

- You have Microsoft 365 admin permissions.
- You have a valid Shortcut API token generated from your Shortcut workspace.
- The Shortcut instance URL is available: `https://api.app.shortcut.com`.

### Get the Shortcut workspace API token

Follow these steps to generate an API token:

- Sign in to your Shortcut account.
- Choose your Shortcut workspace.
- Go to **Settings** > **My Account** > **API Token**.
- Generate a token by providing a token name.
- Record the token securely for later use.

## Deploy the connector

To add the Shortcut Story connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
2. Choose the **Gallery** tab.
3. From the list of available connectors, search for or choose **Shortcut Story**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **Shortcut** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Set instance URL

The Shortcut instance URL is always the following URL:

`https://api.app.shortcut.com`

### Choose authentication type

Choose **API Key** and enter the API token that you generated from your Shortcut workspace.

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The Shortcut connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|---------------|
| Users | Access permissions: Only users with access to content in the data source. Identities mapped using Microsoft Entra IDs. |
| Content | Default property schema applied to Shortcut story fields. |
| Sync | Incremental crawl runs every 15 minutes; full crawl runs every day. |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Shortcut connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

You can specify which users can access indexed Shortcut stories. By default, **Only users with access to the data source** is selected. You can change the value to allow **Everyone** in your organization to view results from the data source.

#### Map identities

Map Shortcut data source identities to Microsoft Entra IDs to ensure proper access control.

### Customize content settings

#### Manage properties

You can view and manage the properties that the connector indexes. Assign schema attributes (searchable, queryable, retrievable, refinable), change semantic labels, and add aliases.

| Source property | Label         | Description                                              | Schema                |
|-----------------|--------------|----------------------------------------------------------|-----------------------|
| Blocked         |              |                                                          | Retrieve, Search      |
| CreatedBy       | Created by    | The user who created the item                            | Retrieve, Search      |
| CreatedOn       | Created date  | Date and time that the item was created                  | Query, Retrieve       |
| Description     | Content       | Description of story                                     | Search                |
| DueDate         |              |                                                          | Query, Retrieve       |
| EpicId          |              |                                                          | Query, Retrieve       |
| EpicName        |              |                                                          | Query, Retrieve       |
| Estimate        |              |                                                          | Query, Retrieve       |
| Id              |              |                                                          | Query, Retrieve       |
| IterationId     |              |                                                          | Query, Retrieve       |
| IterationName   |              |                                                          | Search, Query, Retrieve|
| Labels          |              |                                                          | Retrieve, Search      |
| Name            | Title         | The title of the item shown in Copilot and search        | Query, Retrieve       |
| Owners          |              |                                                          | Query, Retrieve       |
| StoryType       |              |                                                          | Query, Retrieve       |
| TeamName        |              |                                                          | Query, Refine         |
| Url             | url           | The target URL of the item in the data source            | Search                |
| UpdatedBy       |              |                                                          | Retrieve, Search      |
| UpdatedOn       | Last modified | Date and time that the item was last modified            | Query, Retrieve       |
| Workspace       |              |                                                          | Query, Refine, Retrieve|


Use the **Preview data** button to verify sample values of selected properties and query filters.

### Customize sync intervals

You can change the default refresh intervals to meet the needs of your organization:

- **Incremental crawl**: Default is every 15 minutes.
- **Full crawl**: Default is every day.

For more information, see [Guidelines for crawl settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

#### Rate limits

The following table lists the rate limits that apply to the Shortcut Story connector.

| Approximate number of items | Approximate time to complete ingestion |
|------------------------------|----------------------------------------|
| Up to 20,000 | Less than 1 hour |
| Up to 100,000 | Less than 5 hours |
| 100,000 – 1,000,000 | 5 hours to 2 days |
| 1,000,000 or more | 2 days or more (varies by environment load) |

## Related content

- [Shortcut Story connector overview](shortcut-story-overview.md)
- [Troubleshoot issues with the Shortcut Story connector](shortcut-story-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)
