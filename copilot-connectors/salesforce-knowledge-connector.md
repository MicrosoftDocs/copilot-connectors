--- 
title: "Salesforce Knowledge connector for Microsoft Search and Microsoft 365 Copilot" 
ms.author: rerabo
author: vivg
manager: ereza
audience: Admin
ms.audience: Admin 
ms.topic: install-set-up-deploy
ms.service: copilot-connectors 
ms.localizationpriority: medium 
description: "Set up the Salesforce Knowledge Microsoft 365 Copilot connector for Microsoft Search and Microsoft 365 Copilot" 
ms.date: 12/25/2025
---

# Salesforce Knowledge Copilot connector

The Salesforce Knowledge Copilot connector allows your organization to index articles from Salesforce Knowledge. After you configure the connector, end users can search for Knowledge articles from Salesforce in Microsoft 365 Copilot and from any Microsoft Search client. 

## Capabilities
- Index Salesforce Knowledge articles.
- Enable users within the company to ask questions in natural language using Copilot and receive answers based on articles in Salesforce. Examples:
   - What are the steps for processing a refund?
   - What is the escalation procedure for high-priority cases?
   - What are the latest updates to our product warranty policy?
- Use [Semantic search in Copilot](/microsoft-365-copilot/connectors/semantic-index-for-copilot) to enable users to find relevant content based on keywords, personal preferences, and social connections.

## Limitations
- The Salesforce Knowledge connector currently supports permissions based only on knowledge entity access. It does not support data category-based permissions, field-level security (FLS), or sharing rules.
- Supports only articles and items written in English.
- Only published items are indexed.

## Prerequisites

>[!NOTE]
>Make sure that the Salesforce account used to log in for the Salesforce Knowledge Copilot connector is the same as the account already logged into Salesforce.

**Required Salesforce Permissions**

To configure the Salesforce Knowledge connector, the following permissions are required:
- API Enabled
- View Setup and Configuration
- Allow View Knowledge
- Read access for the Knowledge entity

**Obtain Salesforce Knowledge Connector Credentials**

To connect to your Salesforce instance, you need your Salesforce instance URL, the client ID, and the client secret for OAuth 2.0 authentication. The following steps explain how you or your Salesforce administrator can get this information from your Salesforce account:

- Log in to your Salesforce instance and go to **Setup**.
- Navigate to Apps -> App Manager.
- Select **New connected app**.
- Click **Create External Client App**.
- Complete the API section as follows:
    - Select the checkbox for **Enable Oauth settings**.
    - Specify the Callback URL as: For **M365 Enterprise**: `https://gcs.office.com/v1.0/admin/oauth/callback`, for **M365 Government**: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
    - Select these required OAuth scopes.
        - Access and manage your data (API).
        - Perform requests on your behalf at any time (refresh_token, offline_access).
    - Select the checkbox for **Require secret for web server flow**.
    - Save the app.
      > [!div class="mx-imgBorder"]
      > [![Screenshot that shows API section in Salesforce instance after admin has entered all required configurations listed above.](media/salesforce-connector/sf1.png)](media/salesforce-connector/sf1.png#lightbox)

- Copy the consumer key and the consumer secret. This information is used as the client ID and the client secret when you configure the connection settings for your Salesforce Knowledge Copilot connector in the Microsoft 365 admin portal.
  > [!div class="mx-imgBorder"]
  > [![Screenshot that shows results returned by API section in Salesforce instance after admin has submitted all required configurations. Consumer Key is at top of left column and Consumer Secret is at top of right column.](media/salesforce-connector/clientsecret.png)](media/salesforce-connector/clientsecret.png#lightbox)
- Before closing your Salesforce instance, follow these steps to ensure that refresh tokens don't expire:
    - Go to Apps -> App Manager.
    - Find the app you created and select the drop-down on the right. Select **Manage**.
    - Select **edit policies**.
    - For the refresh token policy, select **Refresh token is valid until revoked**.
       > [!div class="mx-imgBorder"]
       > [![Screenshot that shows select the Refresh Token Policy named "Refresh token is valid until revoked ".](media/salesforce-connector/oauthpolicies.png)](media/salesforce-connector/oauthpolicies.png#lightbox)

You can now use the [Microsoft 365 Admin Center](https://admin.microsoft.com/) to complete the rest of the setup process for your Salesforce Knowledge Copilot connector.
     
## Get Started

### 1. Display name 
A display name is used to identify each citation in Copilot, helping users easily recognize the associated file or item. Display name also signifies trusted content. Display name is also used as a content source filter. A default value is present for this field, but you can customize it to a name that users in your organization recognize.

### 2. Salesforce Knowledge URL
Use your organization’s Salesforce Knowledge Instance URL. This URL is the specific web address used to access and interact with Salesforce Knowledge's API services for data retrieval, which typically looks like `https://[COMPANY_NAME].my.salesforce.com`

### 3. Authentication Type
For Salesforce Knowledge Copilot connector, use OAuth 2.0 for authentication. 

To authenticate, enter the Client ID and Client Secret. The Client ID is a unique identifier assigned to your application for making requests to the Salesforce Knowledge API. The Client Secret is a confidential key used alongside the Client ID to securely authenticate your application with the Salesforce Knowledge API.

The first time you've attempted to sign in with these settings, you'll get a pop-up asking you to log in to Salesforce with your admin username and password.

  >[!NOTE]
  >
  > - If the pop-up doesn't appear, it might be getting blocked in your browser, so you must allow pop-ups and redirects.
  > - Ensure that the Salesforce account being used to log in for the Graph connector is the same as the user already logged into Salesforce.
  > - Ensure the user logging in has all the necessary object permissions for the organization.
 
### 4. Roll out to limited audience
Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before expanding the rollout to a broader audience. To know more about limited rollout, see [staged rollout](staged-rollout.md).

At this point, you're ready to create the connection for Salesforce Knowledge. You can click on the "Create" button to publish your connection and index posts from your Salesforce Knowledge account.

For other settings, like **Access Permissions**, **Data Inclusion Rules**, **Schema**, **Crawl frequency**, default values are preconfigured and optimized for Salesforce Knowledge data. You can find the default values listed below:

| Users | Description |
|----|---|
| Access permissions | _Only people with access to content in Data source._ |
| Map Identities | _Data source identities mapped using Microsoft Entra IDs._ |

| Content | Description |
|---|---|
| Manage Properties | _To check default properties and their schema, see [content](#content)._ |

| Sync | Description |
|---|---|
| Incremental Crawl | _Frequency: Every 15 mins_ |
| Full Crawl | _Frequency: Every Day_ |

To modify any of these values, select the **Custom setup** option.

## Custom Setup

Custom setup is for admins who want to edit the default values for settings. Once you click on the 'Custom Setup' option, you see three other tabs: Users, Content, and Sync.

### Users
**Access Permissions**

The Salesforce Knowledge connector supports search permissions visible to **Everyone** or **Only people with access to this data source**. If you choose **Everyone**, indexed data will appear in the search results for all users. If you choose **Only people with access to this data source**, indexed data will appear in the search results for users who have access to them. Choose the one that is most appropriate for your organization.

**Mapping Identities**

You can choose to ingest Access Control Lists (ACLs) from your Salesforce instance or allow everyone in your organization to see search results from this data source. ACLs can include Microsoft Entra identities (users who are federated from Microsoft Entra ID to Salesforce), non-Azure AD identities (native Salesforce users who have corresponding identities in Microsoft Entra ID), or both.

>[!NOTE]
>If you use a third-party Identity Provider like Ping ID or secureAuth, you should select "non-Microsoft Entra" as the identity type.

If you chose to ingest an ACL from your Salesforce instance and selected "non-ME ID" for the identity type, see [Map your non-Microsoft Entra Identities](map-non-entra-id.md) for instructions on mapping the identities.

If you chose to ingest an ACL from your Salesforce instance and selected "ME-ID" for the identity type, see [Map your Microsoft Entra Identities](map-entra-id.md) for instructions on mapping the identities. To learn how to set up Microsoft Entra SSO for Salesforce, see this [tutorial](/azure/active-directory/saas-apps/salesforce-tutorial).

>[!NOTE]
>
> Updates to groups governing access permissions are synced in full crawls only. Incremental crawls don't support processing of updates to permissions.

In the following video, you will learn how to authenticate to your Salesforce instance, sync your non-Microsoft Entra identities with your Microsoft Entra identities, and apply the appropriate security settings to your Salesforce items. While this guide is specifically for the Salesforce CRM connector, the same steps can be applied to the Salesforce Knowledge connector.

> [!VIDEO https://www.youtube-nocookie.com/embed/SZYiFxZMKcM]

### Content

**Manage properties**

Here, you can add or remove available properties from your Salesforce Knowledge data source, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label and add an alias to the property. Properties that are selected by default are listed below:

**Source Property** | **Semantic Label** |**Description**| **Schema**
--- | ---- | --- | ---
ArticleId | | | Query, Retrieve 
ArticleNumber | | The unique number automatically assigned to the article when it's created. | Query, Retrieve 
ArticleType | | The type or category of the knowledge article (for example, FAQ, Support Article, How-To). | Retrieve 
CondensedBody | | Includes the Full content or main body of the article | Retrieve, Search 
CreatedById | | | Query, Retrieve, Search 
CreatedByName | createdBy | The user who initially created the article. | Query, Retrieve, Search 
CreatedDate | createdDateTime | Timestamp of when the article was initially created. | Query, Retrieve 
IconUrl | iconUrl | | Retrieve 
Language | | The language in which the article is written. | Retrieve 
LastModifiedById | | | Query, Retrieve, Search 
LastModifiedByName | lastModifiedBy | The user who last updated the article. | Query, Retrieve, Search 
LastModifiedDate | lastModifiedDateTime | Timestamp of the most recent update to the article. | Query, Retrieve 
LastPublishedDate | | The date when the article was last published. | Query, Retrieve 
LastPublishedVersionId | | | Query, Retrieve 
Summary | | A brief overview or abstract of the article's content. | Search 
Title | title | The main headline or title of the article. | Query, Retrieve, Search 
Url | url | Link to the article in Salesforce Knowledge. | Retrieve 
UrlName | | A unique URL-friendly name generated for the article. | Query, Retrieve 

### Sync

The refresh interval determines how often your data is synced between the data source and the Salesforce Knowledge Copilot connector index. There are two types of refresh intervals - full crawl and incremental crawl. For more information, see [refresh settings](deployment-overview.md#guidelines-for-crawl-settings).

## Troubleshooting

After you publish your connection, you can review the status in the **Connectors** section of the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md). 

### Finding items in Index Browser
If you want to investigate a specific Knowledge Article in the Index Browser, you’ll first need its **KnowledgeArticleId** (the master ID that links all versions of the article). Here’s how to get it from Salesforce:
1. Get the article version ID from the URL: Open the article in Salesforce. Copy the ID from the URL. For example: `/lightning/r/Knowledge__kav/kav1234567890ABC/view`. Here, `kav1234567890ABC` is the ID.
2. Open the [Developer Console](https://help.salesforce.com/s/articleView?id=platform.code_dev_console_opening.htm&type=5)
3. Run the SOQL Query: Go to the **Query Editor** tab and run the following query (replace with your ID).
     ```sql
     SELECT Id, KnowledgeArticleId, Title 
     FROM KnowledgeArticleVersion 
     WHERE Id = '<<KNOWLEDGE_URL_ID>>'
4. In the results, copy the `KnowledgeArticleId`
5. Enter this `KnowledgeArticleId` in the Index Browser to view all related indexed data.

If you have issues or want to provide feedback, see [Microsoft Graph support](https://developer.microsoft.com/graph/support).
