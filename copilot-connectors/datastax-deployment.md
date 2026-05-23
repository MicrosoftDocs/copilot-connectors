---
ms.date: 05/20/2026
title: "Deploy the DataStax connector (preview)"
ms.author: kailiang
author: Kai-Cloud
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Find information about how to deploy the DataStax Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the DataStax connector (preview)

The DataStax Microsoft 365 Copilot connector integrates DataStax Astra DB collections into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface database records directly within apps like Teams, Outlook, and SharePoint.

This article describes the steps to deploy, customize, and manage the DataStax Copilot connector. For general information about Copilot connector deployment, see [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview).

[!INCLUDE [connector-preview-access](includes/connector-preview-access.md)]

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be an admin for your organization's Microsoft 365 tenant.
- You must have access to a DataStax Astra DB database.
- You must have a DataStax application token with read permissions for the database.
- You must have the DataStax API Endpoint and database ID for your database.

## Deploy the connector

To add the DataStax connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, select **Copilot** > **Connectors**.
1. Select the **Gallery** tab.
1. From the list of available connectors, select **DataStax**.

### Set display name

The display name identifies references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a [content source filter](/microsoftsearch/custom-filters#content-source-filters).

You can accept the default **DataStax** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

### Set DataStax API endpoint

Enter the DataStax API Endpoint to connect to your DataStax database. The API Endpoint is typically in the following format:

`https://<your-database-id>-<region>.apps.astra.datastax.com`

Where:

- `<your-database-id>` is the unique identifier for your database
- `<region>` is the geographic region where your database is hosted (for example, `us-east-1`, `eu-west-1`)

You can find the API Endpoint in your DataStax Astra DB database overview page under the **Connect** or **API** section.

### Set DataStax database ID

Enter the DataStax database ID to specify which database the connector should access. The database ID is a unique identifier for your Astra DB database. You can find the database ID in the DataStax Astra DB database overview page.

### Choose authentication type

The DataStax connector uses **DataStax Application Token** for authentication.

#### Generate an application token in DataStax

Before you can authenticate the connector, you need to generate an application token in DataStax Astra DB:

1. Sign in to your [DataStax Astra DB](https://astra.datastax.com) account.
1. Go to your database overview page.
1. Find the **Token Management** or **Generate Token** section.
1. Select **Generate Token** or **Create Token**.
1. Choose a role for the token:
   - **Recommended**: Use the **Read Only User** role to give read access to database collections.
   - Make sure the role has enough permissions to access all collections you want to index.
1. Select **Generate Token** to create the token.
1. Copy the generated application token right away. The token usually starts with `AstraCS:...` and is a long string.

> [!IMPORTANT]
> Store the application token securely. You need this token to authenticate the connector during deployment. The token is shown only once during generation.

#### Authenticate the connector

To authenticate and synchronize database records from DataStax:

1. Select **DataStax Application Token** as the authentication type.
1. Paste the application token that you generated in DataStax Astra DB.
   - The token starts with `AstraCS:...`
   - Make sure you copy the entire token without truncation.
1. Select **Authorize** to validate the token and establish the connection.

> [!NOTE]
> The application token must have at least **Read Only User** permissions to access database collections.

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](staged-rollout.md).

Choose **Create** to deploy the connection. The DataStax connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value                                             |
|----------|-----------------------------------------------------------|
| Users    | Only people with access to the content in the data source |
| Content  | All database collections and records                      |
| Sync     | Full crawl every day                                      |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the DataStax connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

The DataStax connector supports the following user search permissions:

- Everyone
- Only people with access to this data source (default)

If you choose **Everyone**, indexed database data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed database data appears in the search results for users who have access to it.

#### Map identities

If you choose **Only people with access to this data source**, you need to choose whether your DataStax account has Microsoft Entra ID provisioned users or non-Entra ID users:

- Choose the Microsoft Entra ID option if the email ID of DataStax users is the same as the user principal name (UPN) in Microsoft Entra ID.
- Choose the non-Entra ID option if the email ID of DataStax users is different from the UPN in Microsoft Entra ID. For more information about identity mapping, see [Map your non-Entra ID identities](map-non-entra-id.md).

### Customize content settings

#### Manage properties

The DataStax connector indexes the following properties from DataStax Astra DB collections.

| Property | Semantic Label | Description | Schema Attributes |
| -------- | -------------- | ----------- | ----------------- |
| Collection | Not applicable | The collection name where the record is stored. | Query, Retrieve, Search |
| Content | Not applicable | The record content in the collection. | Search |
| iconUrl | iconUrl | The icon URL associated with the record. | Retrieve |
| Id | url | The unique record ID in the collection. This serves as the URL to identify the record. | Query, Retrieve |
| Keyspace | Not applicable | The keyspace for the collection. | Query, Retrieve, Search |
| Title | title | The title created by combining the collection name and the record ID. This is the primary identifier shown in search results and Copilot responses. | Query, Retrieve, Search |

> [!TIP]
> Consider making the **Content** and **Title** properties searchable to improve the relevance of Copilot responses when users query for database information.

#### Preview data

Use the **Preview results** button to verify the sample values of the selected properties. This step helps you confirm that the connector is indexing the expected data from your DataStax collections.

### Customize sync intervals

The DataStax connector supports only full crawl. Incremental crawl isn't available for this connector.

The default schedule for the full crawl is set to **Every day**.

You can adjust the full crawl schedule to fit your data refresh needs. If your database collections change frequently, keep the daily full crawl frequency. If your database content is relatively static, you can reduce the crawl frequency to every few days.

For more information, see [Guidelines for sync settings](deployment-overview.md#guidelines-for-sync-settings).

## Related content

- [DataStax connector overview](datastax-overview.md)
- [Troubleshoot issues with the DataStax connector](datastax-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](deployment-overview.md)
