---
title: "Deploy the 15Five Priorities connector"
ms.author: wangchen
author: wangchen
manager: zezhangzhao
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 04/07/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the 15Five Priorities Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the 15Five Priorities connector

The 15Five Priorities Microsoft 365 Copilot connector enables your organization to index 15Five priority data so the data surfaces in Microsoft 365 Copilot and Microsoft Search experiences. This article describes the steps to deploy and customize the 15Five Priorities connector.

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be a Microsoft 365 admin.
- You must have a 15Five account with HR administrator permissions.
- You must create a company API key and obtain the access token from the integrations admin settings page in 15Five.

## Deploy the connector

To add the connector for your organization:

- In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
- Choose the **Gallery** tab.
- From the list of available connectors, choose **15Five Priorities**.

### Set display name

The display name identifies references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default display name, or customize the value to use a display name that users in your organization recognize.

### Set instance URL

Enter your 15Five instance URL. The default 15Five instance URL is `https://my.15five.com`.

### Choose authentication type

The connector uses the following authentication option:

- Access token generated from your 15Five company API key.

In the **Authentication type** box, select **API Key** and enter the access token that you got from your 15Five company API keys setting.

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to.

Choose **Create** to deploy the connection. The Copilot connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|----------------|
| Users | Indexed data is visible to users based on access permissions defined in the 15Five source system. |
| Content | The connector indexes priority description, status, submitter email, manager email, created date and time, and last modified date and time. |
| Sync | Incremental crawl runs every 15 minutes and full crawl runs every day by default. |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the Microsoft 365 admin center.

## Customize settings (optional)

You can customize the default values for the connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

Determine which users in your organization can access each item in Copilot or Search surfaces. Choose whether indexed data is visible to everyone in the organization or only to users who have access to the data source.

### Customize content settings

#### Manage properties

You can add or remove available properties from your 15Five data source. Assign a schema to the property, change the semantic label, and add an alias to the property.

The following properties are available for configuration.

| Property | Semantic Label | Description | 
|----------|----------------|-------------|
| Text | Not applicable | Description of the priority. |
| Status | Not applicable | Status of the priority. |
| UserEmail | Not applicable | Email of the priority submitter. |
| ManagerEmail | Not applicable | Email of the manager of the submitter. |
| CreateTime | createdDateTime | The time at which the priority was created. |
| UpdateTime | lastModifiedDateTime | The last time the priority was modified. |

### Customize sync intervals

You can configure full and incremental crawls based on scheduling options. The following values are the default values:

- Incremental crawl - Every 15 minutes.
- Full crawl - Every day.

Adjust these schedules to fit your data refresh needs. For more information, see [Guidelines for sync settings](deployment-overview.md#guidelines-for-crawl-settings).

## Related content

- [15Five Priorities connector overview](15five-priorities-overview.md)
- [Troubleshoot issues with the 15Five Priorities connector](15five-priorities-troubleshooting.md)