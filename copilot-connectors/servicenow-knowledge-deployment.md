---
title: "Deploy the ServiceNow Knowledge Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 09/25/2025
ms.localizationpriority: Medium
description: "Find information about how to deploy the ServiceNow Knowledge Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the ServiceNow Knowledge Copilot connector

The ServiceNow Knowledge Copilot connector enables organizations to surface ServiceNow knowledge base (KB) articles within Microsoft 365 Copilot experiences. This article describes the steps to deploy and customize the ServiceNow Knowledge connector.

For general information about Copilot connector deployment, see [Set up connectors in the Microsoft 365 admin center](/microsoftsearch/configure-connector).

For advanced ServiceNow configuration information, see [Set up the ServiceNow Knowledge service for connector ingestion](servicenow-knowledge-admin-setup.md).

## Prerequisites

The following table summarizes the steps to configure the ServiceNow environment and deploy the ServiceNow Knowledge connector.

| Role | Task |
| ---- | ---- |
| ServiceNow admin | [Configure the environment](servicenow-knowledge-admin-setup.md#configure-the-environment) |
| ServiceNow admin | [Set up prerequisites](servicenow-knowledge-admin-setup.md#set-up-connector-prerequisites) |
| Microsoft 365 admin | [Deploy the connector in the Microsoft 365 admin center](#deploy-the-connector) |
| Microsoft 365 admin | [Customize connector settings](#customize-settings) (optional) |

Before you deploy the connector, make sure that the following prerequisites are met:

- You are a Microsoft 365 admin.
- You have access to a configured ServiceNow instance.
- REST API access is enabled for the required ServiceNow tables.
- ACLs are configured to allow read access for the connector.
- You have identified the ServiceNow instance URL.

## Deploy the connector

To add the ServiceNow Knowledge connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
2. Go to the **Connectors** tab, and in the left pane, choose **Gallery**.
3. From the list of available connectors, choose **ServiceNow Knowledge**.

### Set display name

The display name is used to identify references in Copilot responses and helps users recognize the associated file or item. It also signifies trusted content and is used as a content source filter.

You can accept the default **ServiceNow** display name or customize it to use a name that users in your organization recognize.

For more information, see [Enhance Copilot discovery of connector content](enhancing-microsoft-copilot-discovery-with-graph-connector-content.md).

### Set instance URL

To connect to your ServiceNow site, use your site URL, which is typically the following:
`https://.service-now.com`

You can find your instance name in the ServiceNow admin dashboard or by checking the sign in URL used by your organization.

### Choose flow based on user criteria

The ServiceNow Knowledge connector supports two flows for user criteria permissions: **Simple** and **Advanced**. The default is **Simple**. If your ServiceNow instance uses **Advanced Scripts** in your knowledge base or article-level user criteria, use the **Advanced** flow. This ensures accurate permissions handling when content is ingested into Microsoft Graph.

### Choose authentication type

Choose the authentication method that aligns with your organization's security policies. The ServiceNow connector supports the following authentication types:

- **Basic Authentication** - Enter the username and password of a ServiceNow account with the **knowledge** role to authenticate to your instance.
- **OAuth 2.0** (recommended) - For details, see [Set up OAuth configuration](servicenow-knowledge-admin-setup.md#set-up-oauth-configuration).
- **Microsoft Entra ID OpenID Connect**

#### Microsoft Entra ID OpenID Connect

To use Microsoft Entra ID OpenID Connect:

1. Register a new app as a single tenant in Microsoft Entra ID. A redirect URI isn't required. For more information, see [Register an application](/azure/active-directory/develop/quickstart-register-app#register-an-application). 
2. Copy the **Application (client) ID** and **Directory (tenant) ID** for the app.
3. Create a client secret for the app and save it securely. For details, see see [Creating a client secret](/azure/active-directory/develop/quickstart-register-app#add-a-client-secret). 
4. Use the following PowerShell cmlets to retrieve the service principal object ID.
 
```powershell
    Install-Module -Name Az -AllowClobber -Scope CurrentUser
```

```powershell
    Connect-AzAccount
```

```powershell
    Get-AzADServicePrincipal -ApplicationId "Application-ID"
```
5. In your ServiceNow instance, register a new OAuth OIDC entity. For details, see [Create an OAuth OIDC provider](https://docs.servicenow.com/bundle/xanadu-platform-security/page/administer/security/task/add-OIDC-entity.html). Use the values listed in the following table in the registration form; leave other fields as default.

| Field | Description | Value |
| --- | --- | --- |
| Name | A unique name for the OAuth OIDC entity. | Microsoft Entra ID |
| Client ID | From Microsoft Entra ID registration | Application (client) ID |
| Client Secret | From Microsoft Entra ID registration | Client secret |

6. In the **OAuth OIDC Provider Configuration** field, select the search icon, and then select **New**.

7. Fill out OIDC provider configuration form as follows:

| Field | Value |
| --- | --- |
|  OIDC Provider |  Microsoft Entra ID |
|  OIDC Metadata URL | Use the following URL: `https\://login.microsoftonline.com/"<tenandId">/.well-known/openid-configuration`.<br/><br/>Replace "tenantID" with the Directory (tenant) ID. |
|  OIDC Configuration Cache Life Span |  120 |
|  Application | Global |
|  User Claim | sub |
|  User Field | User ID |
|  Enable JTI claim verification | Disabled |

8. Choose **Submit** to save the configuration.

9. Create a ServiceNow account. For details, see [Create a user in ServiceNow](https://docs.servicenow.com/bundle/xanadu-platform-administration/page/administer/users-and-groups/task/t_CreateAUser.html). Use the following values; leave other fields as default:

| Field | Recommended value |
| --- | --- |
| User ID | Service Principal ID | 
| Web service access only | Checked |

10. Assign the **Knowledge** role to the ServiceNow account. For details, see [Assign a role to a user](https://docs.servicenow.com/bundle/xanadu-platform-administration/page/administer/users-and-groups/task/t_AssignARoleToAUser.html). Use the **Application ID** and **Client secret** in the admin center configuration wizard to authenticate with Microsoft Entra ID OpenID Connect.

### Add API namespace (optional)

If you're using the **Advanced** flow, enter the API namespace that you created in your ServiceNow instance. For details, see [Set up REST API](servicenow-knowledge-admin-setup.md#set-up-rest-api). 

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to.

Choose **Create** to deploy the connection. The ServiceNow Knowledge Copilot connector starts indexing content right away.

The following table lists the default values that are set. To customize these values, see [Customize settings](#customize-settings).

| Category | Setting | Default value |
|----------|---------|---------------|
| Users | Access permissions | Only people with access to the content in the data source. |
| Users | Map identities |  Data source identities mapped using Microsoft Entra IDs. |
| Content | Query string | `active=true^workflow_state=published` |
| Content | Manage properties | To see default properties and schemas, see [Manage properties](#manage-properties). |
| Sync | Incremental crawl | Frequency: Every 15 minutes |
| Sync | Full crawl | Frequency: Every day |

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings

You can customize the default values for the ServiceNow Knowledge connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

The ServiceNow Knowledge Copilot connector supports the following user search permissions:

- Everyone
- Only people with access to this data source (default)
 
If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to it. 

If a knowledge article doesn't have a user criterion applied, it appears in the results for everyone in the organization.

The ServiceNow Knowledge connector treats permissions in the following way:

  - If an article has `Can Read` criteria, those are applied during ingestion. Knowledge base-level `Can Read` or `Can Contribute` criteria are ignored.
  - If both article and knowledge base have `Cannot Read` criteria, both are honored.
  - If a user is part of the article-level `Can Read` criteria but not the knowledge base-level, they might still see the article in Microsoft 365 surfaces even if they can't access it in ServiceNow. To prevent this, remove the user from the article-level `Can Read` criteria.

By default, ServiceNow maps email IDs to Microsoft Entra ID (UPN or Mail). You can provide a custom mapping formula if your organization uses different identity attributes. For more information, see [Map non-Microsoft Entra ID identities](map-non-aad.md).

### Customize content settings

#### Query string

ServiceNow uses the following default filter: `active=true^workflow_state=published`.

You can modify this filter to index only specific articles based on your organizational needs. Use ServiceNow’s encoded query string builder to create custom filters.

#### Manage properties

You can manage properties in the following ways:

- Add or remove properties to index from ServiceNow.
- Define [schema attributes](configure-connector.md#search-schema-attributes) for each property, including whether the property is:
    - Searchable
    - Queryable
    - Retrievable
    - Refinable
- Assign [semantic labels](configure-connector.md#semantic-labels-for-source-properties) and aliases to improve search relevance.
- Customize the **AccessUrl** property to reflect your organization’s URL format.

The following table lists the properties that the ServiceNow Knowledge connector indexes by default.

|Property |Semantic Label |Description |Schema Attributes|
|---|---|---|---|
|AccessUrl| url | The target URL of the item in the data source. | Retrieve |
|Active| | A bBoolean field indicating if the article is currently active and can be viewed or searched by users. | |
|ArticleType | | The format of the article, often an HTML or Wiki type. | Query |
|Author| Authors | All the people who participated/collaborated on the item in the data source | Query, Refine Retrieve |
|CanReadUserCriteria | | Provides the user criteria which defines the audience that has access to view the article. | |
|CannotReadUserCriteria | |  Provides the user criteria which defines the audience that is explicitly denied access to view the article. | |
|CmdbCi | | A reference to a Configuration Item (CI) from the CMDB, linking the article to a specific asset or service. | Query, Retrieve, Search |
|Description | | A brief summary of the article's content, which helps users understand what the article is about from search results. | Retrieve, Search |
|Direct | | This field's function is not a common and is likely a customization. | |
|DisableCommenting | | A boolean field to prevent users from adding comments to the article | |
|DisableSuggesting | |  A boolean field to prevent users from suggesting changes to the article. Removes 'Flag Article' button from the article | |
|DisplayAttachments | | A boolean field that controls whether attachments are displayed on the article's page. | |
|EntityType | | The type of entity the article is about (Knowledge) | Query, Refine, Retrieve |
|Flagged | | A boolean field that is set to 'true' if a user has flagged the article for review due to an issue with its content. | Query |
|GeneratedWithNowAssist | | A flag that indicates if the article was created with the help of ServiceNow's AI assistant. | Query |
|HelpfulCount | | The number of times users have marked the article as helpful. | |
|IconUrl |IconUrl |Icon URL that represents the article's category or type. | Retrieve |
|Image | |  A reference to an image used for the article's thumbnail displays next to short description | |
|InstrumentationMetadata | |  A field that stores technical metadata about the article's creation and usage. | |
|ItemPath | | The path of the article within the knowledge base hierarchy. | Query, Refine, Retrieve, Search |
|KbCategory | | The category the article belongs to within its knowledge base. | Query, Retrieve, Search |
|KbKnowledgeBase | |  The knowledge base the article is stored in. | Query, Retrieve, Search |
|KbKnowledgeBaseUrl | | A URL linking to the knowledge base | Query, Retrieve |
|Meta | |  A field to add search keywords (meta tags) to the article to improve search engine results. | |
|MetaDescription | | A short description used in search engine results | Retrieve, Search |
|Number | |  A unique identifier automatically assigned to the knowledge article, such as 'KB0000001' | Query, Retrieve, Search |
|PreviewContent | | The content used for a quick preview of the article. | Retrieve |
|Published | | A date/time stamp indicating when the article was published and made visible to users. | Query, Retrieve |
|Rating | | The average rating given to the article by users. | Query, Retrieve |
|ReplacementArticle | | A field that points to a newer, more up-to-date article that has replaced this one. | |
|Retired | | A date/time stamp for when the article was retired | |
|Roles | |  Specifies which user roles can view or search the article. If empty, all users can see | |
|ShortDescription | Title | The title of the item that you want to be shown in Copilot and other search experiences | Query, Retrieve, Search|
|Source | | The source task from which the article originated, can be another record in ServiceNow (like an incident or problem). | Query |
|SysClassName | | Identifies the template for the knowledge. Knowledge for standard templates, Other values can be FAQ, How to, and so on. | |
|SysCreatedBy | Created by | Name of the person who created the article | Query, Refine, Retrieve|
|SysCreatedOn | Created date time |Data and time that the article was created | Query, Refine, Retrieve|
|SysDomain | | The domain to which the knowledge article belongs in a multi-domain instance | |
|SysDomainPath | | System-generated string that represents the hierarchical path of a knowledge article's domain. | |
|SysId | | The unique 32-character ID for the article, used for backend identification. | Query, Retrieve |
|SysModCount | | The number of times the article has been modified. | Retrieve |
|SysTags | | Keywords or tags that can be added to the article to improve searchability and organization. | Query, Refine, Retrieve, Search |
|SysUpdatedBy | Last modified by | Name of the person who most recently edited the article. | Query, Refine, Retrieve|
|SysUpdatedOn | Last modified date time | Date and time when the item was last modified | Query, Refine, Retrieve|
|SysViewCount | | The number of times the article has been viewed. | Query, Retrieve |
|TaxonomyTopic | | A reference to a topic in a defined taxonomy, used for a structured organization. | Query, Retrieve, Search |
|Topic | |  Another field for article categorization | Query, Retrieve, Search |
|UseCount | |  The number of times the article has been attached to another record, like an incident or problem. | |
|ValidTo | | The expiration date of the article. After this date, article will not be returned in search result | Query, Retrieve |
|ViewAsAllowed | | Allow a permitted user to search and view this article as another user | |
|WorkflowState| |  The current state of the article in its lifecycle, such as 'Draft', 'Review', 'Published', or 'Retired'. | Query, Refine, Retrieve |
|Content `Content`| |  The main body of the article, where the detailed information is written. | Search |

#### Customize AccessURL property

You can customize the **AccessURL** property according to the needs of your organization; for example, if the URL for ServiceNow KB articles is different from the ServiceNow URL in your organization, you can update the value of the **AccessURL** property accordingly. For more information, see [Customize values for certain schema properties](configure-connector.md#customize-values-for-certain-schema-properties).

### Customize sync intervals

Configure the sync schedule to keep indexed content up to date:

- **Full crawl** – Reindexes all content. The default frequency is daily.
- **Incremental crawl** – Syncs only changed content. The default frequency is every 15 minutes.

For more information, see [Guidelines for sync settings](configure-connector.md#guidelines-for-sync-settings).

## Related content

- [ServiceNow Knowledge connector overview](servicenow-knowledge-overview.md)
- [Set up the ServiceNow service for connector ingestion](servicenow-knowledge-admin-setup.md)
- [Troubleshoot issues with the ServiceNow Knowledge connector](servicenow-knowledge-troubleshooting.md)