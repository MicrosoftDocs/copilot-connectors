---
title: "Deploy the Miro Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: anggao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 01/28/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the Miro Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Miro Microsoft 365 Copilot connector

The Miro Microsoft 365 Copilot connector allows your organization to index Miro boards so users can discover, access, and use Miro content directly within Microsoft 365 experiences. This article describes the steps to deploy and customize the Miro connector.

For Miro configuration information, see [Set up the Miro service for connector ingestion](miro-admin-setup.md).

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You're a Microsoft 365 admin.
- You completed the [Miro service configuration](miro-admin-setup.md) steps.
- You recorded the Miro **client ID**, **client secret**, and **company ID**.
- Your Miro user account has the required admin roles.

## Deploy the connector

To add the Miro connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, select **Copilot** > **Connectors**.
1. Select the **Gallery** tab.
1. From the list of connectors, select **Miro**.

### Set display name

The display name is used to identify references in Copilot responses. The display name helps users recognize trusted content and acts as a content source filter.

You can use the default **Miro** display name or customize it to a name that users in your organization recognize.

### Set Company ID

The Company ID (Organization ID) is the unique identifier for your organization’s Miro account. It appears in the URL when you view your settings in the Miro dashboard. Use this identifier when you configure the connector.

> [!NOTE]
> You can only associate the connection with one Company ID. If your Miro workspace includes more than one Company ID, create a separate connection for each.

### Choose authentication type

The connector uses OAuth 2.0 authentication.

The following authentication values from your Miro app are required:

- **Client ID**
- **Client secret**

Add these values and choose **Authorize**. 

For more information, see [Get started with OAuth 2.0 and Miro](https://developers.miro.com/docs/getting-started-with-oauth).

### Roll out

You can roll out the connector to a limited audience before deploying broadly. To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups.

Choose **Create** to deploy the connection. The Miro Copilot connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|---------------|
| Users | Access permissions: Only people with access to the content in the data source<br>Map identities: Data source identities mapped using Microsoft Entra IDs |
| Content | Manage properties: Default properties and schema applied. |
| Sync | Full crawl frequency: Every day |

To customize these values, select **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review its status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Miro connector settings. To customize settings, on the connector page in the admin center, select **Custom setup**.

### Customize user settings

#### Access permissions

The Miro connector supports search permissions visible to:

- **Everyone**
- **Only people with access to this data source**

If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to it. Choose the appropriate scope based on your organization’s needs.

#### Map identities

The default identity mapping verifies that the email ID of Miro users matches the Microsoft Entra user principal name (UPN) or email.

If the default mapping doesn't work for your organization, you can provide a custom mapping formula. For more information, see [Map your non-Entra ID identities](map-non-entra-id.md).

To identify which option is best for your organization:

- Choose the **Microsoft Entra ID** option if the email ID of Miro users is the same as the users' UPN or email in Microsoft Entra ID.
- Choose the **Non-Microsoft Entra ID** option if the email ID of Miro users is different from the users' UPN and email in Microsoft Entra ID.

### Customize content settings

#### Manage properties

To add or remove available properties from your Miro data source, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), and change the semantic label and add an alias to the property. The following table lists the properties that the connector indexes by default.

| Property | Semantic label | Description | Schema attributes |
|----------|----------------|-------------|-------------------|
| Body | n/a | n/a | Search |
| CreatedAt | Created date time | Date and time that the item was created | Query, Retrieve |
| CreatedBy | Created by | User who created the item | Query, Retrieve, Search |
| Description | n/a | n/a | Query, Retrieve |
| Id | n/a | n/a | Query, Retrieve |
| ModifiedAt | Last modified date time | Date and time the item was last modified | Query, Retrieve |
| ModifiedBy | Last modified by | User who made the last modification | Query, Retrieve, Search |
| Name | Title | Title shown in Copilot and search | Query, Retrieve, Search |
| Team | n/a | n/a | Query, Retrieve |
| ViewLink | URL | Target URL of the item in the data source | Query, Retrieve |

Choose **Preview results** to verify sample values of selected properties and query filters.

### Customize sync intervals

The sync interval determines how often your data is synced between the Miro data source and the index. Only full crawl refresh intervals are supported. You can adjust the default value as needed.

For more information, see [Guidelines for sync settings](/microsoft-365-copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [Miro connector overview](miro-overview.md)  
- [Troubleshoot issues with the Miro connector](miro-troubleshooting.md)  
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365-copilot/connectors/deployment-overview)