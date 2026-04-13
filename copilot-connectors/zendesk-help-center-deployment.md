---
title: "Deploy the Zendesk Help Center connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: ang.gao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 11/24/2025
ms.localizationpriority: Medium
description: "Find information about how to deploy the Zendesk Help Center Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Zendesk Help Center connector

The Zendesk Help Center Microsoft 365 Copilot connector enables your organization to index published articles from Zendesk Help Center (also known as Zendesk Guide). After you configure the connector, users can search for these articles in Microsoft 365 Copilot and Microsoft Search clients. 

This article describes the steps to deploy and customize the Zendesk Help Center connector. For general information about Copilot connector deployment, see [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview).

## Prerequisites

Before you deploy the Zendesk Help Center connector, make sure that you meet the following prerequisites:

- You must be the AI administrator for your organization's Microsoft 365 tenant.
- You need your organization's Zendesk Help Center instance URL. The typical format is `https://<your-organization-domain>.zendesk.com`. If you don't have an instance, see [How do I create a Support trial account](https://support.zendesk.com/hc/articles/4408823799962-How-do-I-create-a-Support-trial-account).
- You need a service account with read permissions. The service account must have either the Admin, Agent, or *Light agent role. The Contributor role doesn't allow read permissions in Zendesk.

## Deploy the connector

To add the Zendesk Help Center connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **Zendesk Help Center**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter. You can accept the default **Zendesk Help Center** display name, or customize the value to use a display name that users in your organization recognize. 

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Set instance URL

To connect to your Zendesk Help Center data, you need your organization's Zendesk Help Center instance URL. The typical format is `https://<your-organization-domain>.zendesk.com`.

### Choose authentication type

The Zendesk Help Center connector supports the following authentication type:

- **Zendesk OAuth** (recommended): A Zendesk admin must create an OAuth client in the Zendesk Admin Center. For details, see [Managing access to the Zendesk API](https://support.zendesk.com/hc/articles/4408889192858-Managing-access-to-the-Zendesk-API).

Enter the client ID (unique identifier) and client secret to connect to your instance. After you connect, use a Zendesk account credential to authenticate permission to crawl.

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The Zendesk Help Center Copilot connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|---------------|
| Users    | Only people with access to content in data source. |
| Content  | Data source identities mapped using Microsoft Entra IDs. |
| Sync     | Incremental crawl: Every 15 mins.<br>Full crawl: Every day. |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Zendesk Help Center connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

The Zendesk Help Center Copilot connector supports search permissions visible to **Everyone** or **Only people with access to this data source**. If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to them.

#### Mapping identities

The default method for mapping your data source identities with Microsoft Entra ID is by checking whether the email ID of Zendesk users is the same as the user principal name (UPN) or email of users in Microsoft Entra ID. If the default mapping doesn't work for your organization, you can provide a custom mapping formula.

### Customize content settings

#### Manage properties

You can add or remove available properties from your Zendesk Help Center, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. The following table lists the properties that are selected by default.

| Property        | Semantic Label | Description                                               | Schema Attributes         |
|-----------------|---------------|-----------------------------------------------------------|--------------------------|
| Authors        |               | Name all the people who participated/collaborated         | Query, Retrieve          |
| Body            | Content       | The main body of the article                              | Search                   |
| CategoryId      |               |                                                           | Query, Retrieve          |
| CategoryName    |               |                                                           | Query, Retrieve          |
| HtmlUrl         | url           | The target URL of the item in the data source             | Query, Retrieve, Search  |
| LabelNames      |               |                                                           | Query, Retrieve, Search  |
| Locale          |               |                                                           | Query, Retrieve, Search  |
| SectionId       |               |                                                           | Query, Retrieve          |
| SectionName     |               |                                                           | Query, Retrieve          |
| SourceLocale    |               |                                                           | Query, Retrieve, Search  |
| Title           | Title         | The title of the item shown in Copilot and search         | Query, Retrieve, Search  |
| UpdateDate      | Last modified date time | Date and time the item was last modified in the data source | Query, Retrieve          |
| UserSegmentId   |               |                                                           | Query, Retrieve          |
| VoteCount       |               |                                                           | Query, Retrieve          |
| VoteSum         |               |                                                           | Query, Retrieve          |

### Customize sync intervals

The refresh interval determines how often your data is synced between the data source and the Zendesk Help Center Copilot connector index. There are two types of refresh intervals:

- **Incremental crawl:** Every 15 minutes.
- **Full crawl:** Every day.

For more information, see [Guidelines for crawl settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [Zendesk Help Center connector overview](zendesk-help-center-overview.md)
- [Troubleshoot issues with the Zendesk Help Center connector](zendesk-help-center-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)