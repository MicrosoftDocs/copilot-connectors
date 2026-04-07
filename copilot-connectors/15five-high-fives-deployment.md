---
title: "Deploy the 15Five High Fives connector"
ms.author: lauragra
author: wangchen
manager: zezhangzhao
ms.reviewer: wangchen
audience: Admin
ms.audience: Admin
ms.topic: install-set-up-deploy
ms.service: copilot-connectors
ms.date: 04/06/2026
ms.localizationpriority: Medium
description: "Deploy the 15Five High Fives Microsoft 365 Copilot connector for your organization."
---

# Deploy the 15Five High Fives connector

The 15Five High Fives Microsoft 365 Copilot connector enables your organization to index 15Five high-five data so the data surfaces in Microsoft 365 Copilot and Microsoft Search experiences. This article describes the steps to deploy and customize the 15Five High Fives connector for your organization.

## Prerequisites

Complete the following prerequisites before you deploy the connector:

- Create a 15Five account with HR administrator permission.
- As an HR administrator, go to the Integrations admin setting page in 15Five and create a company API key to get the access token.

## Deploy the connector

To add the 15Five High Fives connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **15Five High Fives**.

### Set display name

The display name identifies references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **15Five High Fives** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

### Set instance URL

Enter your 15Five instance URL. The default 15Five instance URL is `https://my.15five.com`.

### Choose authentication type

In the **Authentication type** box, select **API Key** and enter the access token that you got from your 15Five company API keys setting.

### Roll out 

Deploy this connection to a limited user base to validate it in Microsoft 365 Copilot and other Microsoft Search experiences before you roll it out to a broader audience.

To roll out to a limited audience, select the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](staged-rollout.md).

Select **Create** to deploy the connection. The 15Five High Fives connector starts indexing content right away.

## Customize settings (optional)

You can customize the default values for the 15Five High Fives settings. To customize settings, on the connector page in the admin center, select **Custom setup**.

### Customize user settings

All 15Five High Fives data indexed through the connector is visible to all Microsoft 365 users in your tenant in Microsoft Search or Microsoft 365 Copilot.

### Customize content settings

You can add or remove available properties from your 15Five data source. You can also:

- Assign a schema.
- Change the semantic label.
- Add an alias to a property.

The following properties are indexed by default.

| Source property | Label | Description |
|-----------------|--------|-------------|
| Text | Not applicable | Description of the high-five content. |
| CreatorEmail | Not applicable | Email of the user who gives a high five. |
| CreatorName | createdBy | Name of the user who gives a high five. |
| Receivers | Not applicable | Name of the users who receive a high five. |
| CreateTime | createdDateTime | The time at which the high five was created. |
| UpdateTime | lastModifiedDateTime | The last time the high five was modified. |

### Customize sync intervals

You can configure full and incremental crawls based on scheduling options. The following values are the default values:

- Incremental crawl - Every 15 minutes.
- Full crawl - Every day.

Adjust these schedules to fit your data refresh needs. For more information, see [Guidelines for sync settings](deployment-overview.md#guidelines-for-sync-settings).

## Related content

- [15Five High Fives connector overview](15five-high-fives-overview.md)
- [Troubleshoot issues with the 15Five High Fives connector](15five-high-fives-troubleshooting.md)