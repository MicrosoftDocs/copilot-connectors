---
title: "Unily Microsoft 365 Copilot connector" 
ms.author: rerabo
author: vivg
manager: ereza
audience: Admin
ms.audience: Admin 
ms.topic: install-set-up-deploy
ms.service: copilot-connectors 
ms.localizationpriority: medium 
description: "Set up the Unily Microsoft 365 Copilot connector." 
ms.date: 12/25/2025
---

# Unily Microsoft 365 Copilot connector

The Unily Microsoft 365 Copilot connector allows your organization to index content from the Unily intranet. After you configure the connector, end users can search for this content in Microsoft 365 Copilot and from any Microsoft Search client. 

## Capabilities
- Index Unily content (the following document types are supported: App, Doc Brand Asset, Image Brand Asset, FAQ, Form, Quiz, Idea, Location, Mandatory Read Article, Mandatory Read Doc, Media Content, Story, Knowledge Article, SitePageModern).
- Enable users within the company to ask questions in natural language using Copilot and receive answers based on content from Unily. Examples:
   - What are the company holidays for 2025?
   - What events are planned for National Heritage Month?
   - What training programs are available?
- Use [Semantic search in Copilot](/microsoft-365/copilot/connectors/semantic-index-for-copilot) to enable users to find relevant content based on keywords, personal preferences, and social connections.

## Limitations
- Currently, Copilot responses aren't customized for specific audiences as defined in Unily, such as utilizing the 'target audience' property.

## Prerequisites
- To create a new connection, you must be the AI administrator for your organization's Microsoft 365 tenant.
- To create a new connection, use your organization’s Unily instance URL. Contact Unily directly to obtain the correct URL. This URL is the specific web address used to access and interact with Unily API services for content retrieval, which usually looks like `https://[your-organization-name]-api.unily.com`.
- To complete the authentication, you need a Client ID and Client Secret. To get your Unily Client ID and Secret, contact Unily directly. A Unily instance may have multiple applications, each with different permissions. Ensure that you obtain the correct credentials for the application to be used for the Copilot connector.


## Get Started

### 1. Display name 
A display name is used to identify each citation in Copilot, helping users easily recognize the associated item. The display name also signifies trusted content. Display name is also used as a content source filter. A default value is present for this field, but you can customize it to a name that users in your organization recognize.

### 2. Unily URL
Use your organization’s Unily URL. This URL is the specific web address used to access Unily, which typically looks like https://[your-organization-name].unily.com

### 3. Authentication Type
For the Unily Copilot connector, use OAuth 2.0 for authentication.

To authenticate, enter the Client ID and Client Secret. The Client ID is a unique identifier assigned to your application for making requests to the Unily API. The Client Secret is a confidential key used alongside the Client ID to securely authenticate your application with the Unily API.
 
### 4. Roll out to limited audience
Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before expanding the rollout to a broader audience. To know more about limited rollout, see [staged rollout](staged-rollout.md).

At this point, you're ready to create the connection for Unily. You can click on the "Create" button to publish your connection and index posts from your Unily account.

## Custom Setup

Custom setup is for admins who want to edit the default values for settings. Once you click on the 'Custom Setup' option, you see three other tabs: Users, Content, and Sync.

### Users
#### Access Permissions
The Unily Copilot connector supports search permissions visible to **Only people with access to this data source** (default) or **Everyone**.

If you choose **Only people with access to this data source**, indexed data appears in search results only for users who have access to it in Unily. This means that if a user has access to specific content or a page in Unily, they see it in Copilot. If they don't have access, it doesn't appear for them in Copilot either.
If you choose **Everyone**, indexed data appears in the search results for all users.

#### Mapping Identities
To enforce correct permissions, you need to map user identities from Unily to Microsoft Entra ID (ME-ID). There are two options:
1. **Microsoft Entra ID (ME-ID) mapping (default):**<br>
By default, the system attempts to match users by comparing the **user's email in Unily** with either the **UserPrincipalName** (UPN) or **Mail** attribute in Microsoft Entra ID. This method works when the email addresses align between systems.
2. **Non-Microsoft Entra ID (non ME-ID) mapping (custom):** <br>
If the default mapping doesn't work for your organization (for example, if email formats differ) you can define a custom mapping formula to link users across systems.

[Click here](map-non-entra-id.md) to learn more about mapping non-Entra ID identities.

### Content

#### Manage properties

Here, you can add or remove available properties from your Unily data source, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. Properties that are selected by default are listed below:

|Default property|Semantic Label |Description|Schema|
|--- | ---- | --- | ---|
|Authors | Authors | Names of the content authors | Query, Retrieve, Search|
|Content | | The main body of the content, including all written information and details | Search|
|CreatedBy | The email address of the individual who initially created the entity | Query, Retrieve, Search|
|CreatedDate | Created date time | The specific date when the content was originally created | Retrieve|
|Date | | The date when the content was first made available to the public |
|Description | | A concise summary that provides an overview of the main points and purpose of the content | Retrieve, Search|
|DocumentType | | The type of the document within the Unily platform | Query, Retrieve|
|ID | | Post title | Query, Retrieve|
|LastModifiedDate | Last modified date time | The most recent date when the content was modified or updated | Retrieve|
|ParentId | | Post title | Retrieve|
|Title | Title | The heading or title that appears on the content page | Query, Retrieve, Search|
|UniqueId | | Post title | Query, Retrieve|
|Url | url | The link that directs to the specific page in Unily where the content is located | Retrieve|
|TargetAudience |  | The specific group of users that content is intended for | Query, Retrieve, Search|

### Sync

The refresh interval determines how often your data is synced between the data source and the Copilot connector index. There are two types of refresh intervals - full crawl and incremental crawl. For more information, see [refresh settings](deployment-overview.md#guidelines-for-crawl-settings).

## Troubleshooting

### Copilot does not recognize branded Unily Intranet names
To ensure optimal relevance and accuracy in Microsoft 365 Copilot responses, administrators should update the connector description to include the branded name of your organization’s Unily intranet. Many Unily customers rebrand their intranet, and Copilot prioritizes results more effectively when these branded names are explicitly listed in the connector description. To update this setting, go to **Admin Center → Copilot → Connectors**, select your Unily connection, choose **Edit description**, and add a clear reference to your Unily intranet’s branded name in the description. This helps Copilot recognize user queries that refer to the intranet by its custom name and improves the discoverability and ranking of Unily content.

After publishing your connection, you can review the status in the **Connectors** section of the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md). 

If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).




