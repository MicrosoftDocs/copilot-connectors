---
title: "Deploy the DataStax connector"
ms.author: kailiang
author: Kai-Cloud
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 08/15/2025
ms.localizationpriority: medium
description: "Find information about how to deploy the DataStax Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the DataStax connector

The DataStax connector indexes records from your DataStax Astra DB collections into Microsoft 365. This guide describes the steps to deploy and customize the connector.

[!INCLUDE [conector-preview-access](includes/connector-preview-access.md)]

## Prerequisites

Before you deploy the DataStax connector, make sure that you meet the following prerequisites:

- You must be the AI administrator for your organization's Microsoft 365 tenant.
- To connect to your DataStax database, you need the DataStax API Endpoint and database ID.
- To connect to DataStax and allow the Copilot connector to update DataStax tasks regularly, you need an application token with read permissions.

## Deploy the connector

To add the DataStax connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **DataStax**.

### Set display name

The display name identifies each citation in Copilot and helps users easily recognize the associated file or item. The display name also signifies trusted content and is used as a [content source filter](/microsoftsearch/custom-filters#content-source-filters).

A default value is provided. You can customize it to a name that users in your organization recognize.

### Set DataStax API Endpoint

To connect to your DataStax database, you need the DataStax API Endpoint. The endpoint can be found in the overview of your database and is typically the following: `https://<your-database-id>-<region>.apps.astra.datastax.com`.

### Set DataStax database ID

To connect to your DataStax database, you need the DataStax database ID. The database ID can be found in the overview of your database.

### Choose authentication type

To sync data from DataStax, you need to authenticate using a DataStax Application Token.

#### DataStax Application Token

A DataStax admin needs to generate the application token for the database with a proper user role, such as using "Read Only User".

[![Screenshot that shows the DataStax API Endpoint, Database ID and Generate Token in the Astra DB overview.](media/datastax/datastax-api-endpoint.png)](media/datastax/datastax-api-endpoint.png#lightbox)

Copy the generated application token from the token details, which is typically a long string that starts with "AstraCS:...". Paste it in the connector setup. Choose **Authorize**, and use the same token to authenticate permission to crawl.

### Roll out to a limited audience

Deploy the connection to a limited user base if you want to validate it in Copilot and other Search surfaces before you roll it out to a broader audience. For more information, see [Staged rollout for connectors](staged-rollout.md).

At this point, you're ready to create the connection for DataStax. Choose **Create** to publish your connection and index articles from your DataStax account.

For other settings, like **Access permissions**, **Schema**, and **Crawl frequency**, default values are set based on what works best with DataStax data.

| Users | Description |
|----|---|
| Access permissions | Only people with access to content in Data source. |
| Map identities | Data source identities mapped using Microsoft Entra IDs. |

| Content | Description |
|---|---|
| Manage properties | For information about the default properties and their schema, see [Manage properties](#manage-properties). |

| Sync | Description |
|---|---|
| Full crawl | Runs every day. |

## Custom setup

In custom setup you can edit any of the default values for users, content, and sync.

### Users

[![Screenshot that shows Users tab where you can configure access permissions and user mapping rules.](media/datastax/DataStax-users-tab.png)](media/datastax/DataStax-users-tab.png#lightbox)

#### Access permissions

The DataStax Copilot connector supports search permissions visible to **Everyone** or **Only people with access to this data source**. If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to them.

#### Mapping identities

The default method to map your data source identities with Microsoft Entra ID is to verify that the email ID of DataStax users is the same as the user principal name (UPN) of the users in Microsoft Entra ID. If the default mapping doesn't work for your organization, you can provide a custom mapping formula. For more information, see [Map your non-Azure AD Identities](map-non-entra-id.md).

To identify which option is best for your organization:

1. Choose the **Microsoft Entra ID** option if the email ID of DataStax users is the *same* as the UPN in Microsoft Entra ID.
2. Choose the **Non-Microsoft Entra ID** option if the email ID of DataStax users is *different* than the users' UPN and email in Microsoft Entra ID.

### Content

[![Screenshot that shows Content tab where you can configure properties and schema.](media/datastax/DataStax-content-tab.png)](media/datastax/DataStax-content-tab.png#lightbox)

#### Manage properties

To view available properties from your DataStax data source, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias in the property. Some properties are selected by default.

|Default property|Label|Description|Schema|
|:---|:---|:---|:---|
| Collection | Not applicable | The collection name | Query, Retrieve, Search. |
| Content | Not applicable | The record in the collection | Search. |
| IconUrl | IconUrl | The icon url of the record | Retrieve. |
| Id | url | The record ID in the collection | Query, Retrieve. |
| Keyspace | Not applicable | The keyspace for the collection | Query, Retrieve, Search. |
| Title | Title | The title created by combining the collection name and the record ID  | Query, Retrieve, Search. |

#### Preview data

Use the preview results button to verify the sample values of the selected properties and query filter.

### Sync

[![Screenshot that shows Sync tab where you can configure crawl frequency.](media/datastax/DataStax-sync-tab.png)](media/datastax/DataStax-sync-tab.png#lightbox)

The refresh interval determines how often your data syncs between the data source and the DataStax Copilot connector index. The DataStax connector only supports the refresh interval - full crawl. For more information, see [refresh settings](deployment-overview.md#guidelines-for-crawl-settings).

You can change the default values of the refresh interval.

## Next steps

After you publish your connection, you can review the status in the **Connectors** section of the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

## Related content

- [DataStax connector overview](datastax-connector-overview.md)
- [Troubleshoot issues with the DataStax connector](datastax-connector-troubleshooting.md)
