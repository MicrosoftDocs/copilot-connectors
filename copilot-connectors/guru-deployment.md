---
title: "Deploy the Guru connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: rantang
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 11/24/2025
ms.localizationpriority: Medium
description: "Find information about how to deploy the Guru Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Guru connector

The Guru Microsoft 365 Copilot connector integrates Guru content into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface relevant Guru Cards directly within apps like Teams, Outlook, and SharePoint. This article describes the steps to deploy and customize the Guru connector. 

## Prerequisites

Before you deploy the Guru connector, make sure that you meet the following prerequisites:
- You must be the **AI administrator** for your organization's Microsoft 365 tenant.
- **Guru Instance Admin Account**: To connect to your Guru instance and allow the Guru Microsoft 365 Copilot connector to update Guru cards regularly, you need an admin user account of your Guru instance with the permission to create a user token. Find more details [here](https://help.getguru.com/docs/gurus-api).

## Deploy the connector

To add the Guru connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **Guru**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter. You can accept the default **Guru** display name or customize the value to use a display name that users in your organization recognize. 

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Set instance URL

Provide the URL for your Guru instance. The typical structure is `https://app.getguru.com/` followed by your organization's instance identifier.

### Choose authentication type

The Guru connector supports Basic Authentication using a user token. We recommend using a Guru admin account to generate the user token. For more information, see [Guru API documentation](https://help.getguru.com/docs/gurus-api).

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The Guru Copilot connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|--------------|
| Users    | Only people with access to this data source. |
| Users    | Data source identities mapped using Microsoft Entra IDs. |
| Content  | All cards, except the cards in personal space. |
| Content  | To check default properties and their schema, see [Manage properties](#manage-properties). |
| Sync     | Incremental crawl: Every 15 minutes. |
| Sync     | Full crawl: Every day. |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Guru connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

The Guru connector supports two options for access permissions:

- **Everyone**: Indexed data appears in the search results for all users.
- **Only people with access to this data source** (default): Only users with access in Guru can see the content.

If you choose **Only people with access to this data source**, you need to choose whether your Guru instance has Microsoft Entra ID provisioned users or non-Entra ID users:

- Choose the **Microsoft Entra ID** option if the email ID of Guru users is the same as the user principal name (UPN) of users in Microsoft Entra ID.
- Choose the **non-Entra ID** option if the email ID of Guru users is different from the UPN of users in Entra ID.

If you choose Microsoft Entra ID as the identity source, the connector maps user email IDs from Guru to the UPN property in Microsoft Entra ID. If you choose non-Entra ID as the identity source, provide a regular expression to map email ID to UPN. For more information, see [Map your non-Entra ID identities](/microsoft-365/copilot/connectors/map-non-entra-id).

> [!NOTE]
> Updates to users or groups that govern access permissions are synced in full crawls only. Incremental crawls don't currently support processing updates to permissions.

### Customize content settings

You can customize what data is included and excluded and customize the default connector properties.

#### Content ingestion filters

You can choose what data you want to index. Use the Guru Query Language (GQL) to filter your data before it's indexed, allowing you to control what data is searchable. For example, you might use the GQL filter to index content modified after a certain time by using `lastModified > 2016-01-01T00:00:00.000-00:00`. 

For more information, see [Guru Query Language](https://developer.getguru.com/docs/guru-query-language).

Use the preview results button to verify the sample values of the selected properties and filters.

#### Manage properties

You can check the available properties from your Guru instance. Assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. The following table lists the properties that the connector indexes by default.

| **Default property** | **Semantic Label** | **Description** | **Schema attributes** |
|----------------------|--------------------|-----------------|
| Authors | authors | List of all the users who contributed to the card | Query, Retrieve, Search |
| CollectionDescription | | Description of the collection | Query, Retrieve, Search |
| CollectionLink | containerUrl | URL of the collection the card belongs to | Retrieve |
| CollectionName | containerName  | Name of the collection the card belongs to | Query, Retrieve, Search |
| Content | content | Rendered HTML content of the card | Search |
| CreatedTime | createdDateTime  | Date/Time when the card was created | Query, Retrieve |
| IconUrl | | URL of the icon | Retrieve |
| Itempath | itemPath  | The path of the item in the data source represented by `/` separated values. Holds the display value of each level in the hierarchy separated by `/`. | Query, Retrieve, Search |
| LastModifiedBy | lastModifiedBy | Email ID of the user who last updated the card | Query, Retrieve, Search |
| Link | url | URL of the item | Retrieve |
| ModifiedTime | lastModifiedDateTime | Date/Time when the card was last updated | Query, Retrieve, Refine |
| Owner | createdBy  | Email ID of the user who created the card | Query, Retrieve, Search |
| Status | state | Status of the card - verified or unverified | Query, Retrieve, Search, Refine |
| Title | title | Title of the card | Query, Retrieve, Search |
| Type | itemType | Type of the item (item type identifier for Guru cards) | Query, Retrieve, Search |

### Customize sync intervals

The refresh interval determines how often your data is synchronized between the data source and the Guru connector index. Copilot connectors use two types of refresh intervals:

- **Full crawl**: Default is every day.
- **Incremental crawl**: Default is every 15 minutes.

You can change the default values of the refresh intervals. For more information, see [Guidelines for crawl settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [Guru connector overview](guru-overview.md)
- [Guru connector troubleshooting](guru-troubleshooting.md)
