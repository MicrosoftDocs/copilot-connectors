--- 

title: "Trello connector (preview)" 
ms.author: anggao
author: ms-anggao
manager: jecui
audience: Admin
ms.audience: Admin 
ms.topic: install-set-up-deploy
ms.service: copilot-connectors 
ms.localizationpriority: Medium 
description: "Set up the Trello Microsoft 365 Copilot connector." 
ms.date: 08/15/2025
---

# Trello connector (preview)

The Trello Microsoft 365 Copilot connector allows your organization to index cards from Trello. After you configure the connector, users can search for these tickets from Trello in Microsoft 365 Copilot and from any Microsoft Search client.

[!INCLUDE [conector-preview-access](includes/connector-preview-access.md)]

## Capabilities

- Index public cards from your Trello Workspace.
- Customize your crawl frequency.  
- Create workflows by using this connection and actions from Microsoft Copilot Studio.  
- Use [Semantic search in Copilot](/microsoft-365/copilot/connectors/semantic-index-for-copilot) to enable users to find relevant content.

## Limitations

- Doesn't index comments.
- Only public cards indexed through the Trello Copilot connector are visible to all Microsoft 365 users in your tenant via Microsoft Search or Copilot.

## Prerequisites

### 1. Trello developer account and app registration

Create or use an existing Trello account to access the developer portal. Register your application on `https://trello.com/power-ups/admin` to get your API credentials. For more information, see [Authorizing With Trello's REST API](https://developer.atlassian.com/cloud/trello/guides/rest-api/authorization/).  

### 2. Get your API key and secret

After you register your app, go to the **API key** tab to get the unique app key and secret. These credentials are required to sign OAuth requests as part of the OAuth 1.0a flow.

## Get Started

### 1. Display name

The display name identifies each citation in Copilot to help users recognize the associated file or item. The display name also signifies trusted content and is used as a [content source filter](/microsoft-365/copilot/connectors/custom-filters#Content-source-filters). A default value is provided for this field; you can customize it to a name that users in your organization recognize.

### 2. Authentication Type

**Trello OAuth**
Enter the Consumer key and Private secret you got from your Trello app console. For more information, see [Authorizing With Trello's REST API](https://developer.atlassian.com/cloud/trello/guides/rest-api/authorization/).

### 3. Roll out to limited audience

Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before you expand the rollout to a broader audience. For more information, see [Staged rollout for Copilot connectors](staged-rollout.md).

Now you're ready to create the connection for Trello. Choose **Create** to publish your connection and index tickets from your Trello account.

For other settings, like **Access permissions**, **Schema**, and **Crawl frequency**, default values are set based on what works best with Trello data.

| Users | Description |
|----|---|
| Access permissions | Default access permission is set to be visible to everyone. |

| Content | Description |
|---|---|
| Manage properties | To check default properties and their schema. |

| Sync | Description |
|---|---|
| Incremental crawl | Frequency: Every 15 mins |
| Full crawl | Frequency: Every day |

If you want to edit any of these values, choose **Custom Setup**.

## Custom setup

Custom setup is for admins who want to edit the default values for settings listed. When you choose **Custom Setup**, you see three more tabs - **Users**, **Content**, and **Sync**.

### Users

#### Access permissions

The Trello Copilot connector allows your organization to index cards from Trello. After you configure the connector, users can search for these tickets from Trello in Microsoft 365 Copilot and from any Microsoft Search client.

### Content

#### Manage properties

You can add or remove available properties from your Trello, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. The following table lists the properties that are selected by default.

|Source property|Label|Description|Schema|
|---|---|---|---|
| BoardName |  |  |  |
| BoardUrl |  |  |  |
| Closed |  |  |  |
| DateLastActivity | Last modified date time | Date and time the item was last modified in the data source. | Query, Retrieve |
| Description |  |  | Search |
| Due |  |  | Query, Retrieve |
| DueComplete |  |  |  |
| Id |  |  | Query, Retrieve |
| LabelName |  |  | Query, Retrieve, Search |
| Name | Title | The title of the item that you want shown in Copilot and other search experiences | Query, Retrieve, Search |
| Start | Created date time | Date and time that the item was created in the data source | Query, Retrieve |
| Url | url | The target URL of the item in the data source | Query, Retrieve, Search |

#### Preview data

Use the preview results button to verify the sample values of the selected properties and query filter.

### Sync

The refresh interval determines how often your data is synced between the data source and the Trello Copilot connector index. There are two types of refresh intervals: full crawl and incremental crawl. For more information, see [refresh settings](deployment-overview.md#guidelines-for-crawl-settings).

You can change the default values of the refresh interval.

## Next steps

After you publish your connection, you can review the status in the **Connectors** section of the [admin center](https://admin.microsoft.com). For more information, see [Manage your connector](manage-connector.md).

For help and support, see [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).
