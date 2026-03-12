---
title: "Deploy the ServiceNow Knowledge Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: mayanksethi
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 03/11/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the ServiceNow Knowledge Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the ServiceNow Knowledge Copilot connector

The ServiceNow Knowledge Copilot connector enables organizations to surface ServiceNow knowledge base (KB) articles within Microsoft 365 Copilot experiences. This article describes the steps to deploy and customize the ServiceNow Knowledge connector.

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

- You're a Microsoft 365 admin.
- You have access to a configured ServiceNow instance.
- REST API access is enabled for the required ServiceNow tables.
- Access control lists (ACLs) are configured to allow read access for the connector.
- You identified the ServiceNow instance URL.

## Deploy the connector

To add the ServiceNow Knowledge connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
2. Go to the **Connectors** tab, and in the left pane, choose **Gallery**.
3. From the list of available connectors, choose **ServiceNow Knowledge**.

### Set display name

The display name is used to identify references in Copilot responses and helps users recognize the associated file or item. It also signifies trusted content and is used as a content source filter.

You can accept the default **ServiceNow** display name or customize it to use a name that users in your organization recognize.

For more information, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

### Choose flow based on user criteria

The ServiceNow Knowledge connector supports two flows for user criteria permissions: **Simple** (default) and **Advanced**. Both flows evaluate knowledge base (parent)-level and article (child)-level user criteria.

The default is **Simple**. In this flow, advanced script-based user criteria aren't evaluated.

If your ServiceNow instance uses **Advanced Scripts** in your knowledge base or article-level user criteria, use the **Advanced** flow. This flow evaluates script-based user criteria by calling the Scripted REST API in ServiceNow, which ensures accurate permissions handling when content is ingested into Microsoft Graph. For the **Advanced** option to work properly, you need to [Set up REST API](servicenow-knowledge-admin-setup.md#set-up-rest-api).

### Set instance URL

To connect to your ServiceNow site, use your site URL, which is typically the following format:
`https://<instance-name>.service-now.com`

You can find your instance name in the ServiceNow admin dashboard or by checking the sign in URL used by your organization.

### Choose authentication type

Choose the authentication method that aligns with your organization's security policies. The ServiceNow connector supports the following authentication types:

- **Federated Auth** (recommended) - For details, see [Federated Auth](#federated-auth-federated-identity-credentials)
- **Basic authentication** - Enter the username and password of a ServiceNow account with the **knowledge** role to authenticate to your instance.
- **OAuth 2.0** - For details, see [OAuth 2.0](#oauth-20).
- **Microsoft Entra ID OpenID Connect** - For details, see [Microsoft Entra ID OpenID Connect](#microsoft-entra-id-openid-connect).

#### Federated Auth (Federated Identity Credentials)

Federated Auth uses a Microsoft application with OpenID Connect (OIDC) so that the connector authenticates to your ServiceNow instance without storing or rotating a client secret. Before you begin, make sure you have:

- A ServiceNow admin account with privileges to create OIDC providers and users.
- Your Microsoft Entra tenant ID (Directory ID), available from the Azure portal under **Microsoft Entra ID** > **Overview**.

#### Step 1: Get the service principal object ID

You need the Service Principal Object ID of the first-party connector application in your tenant. This is the Object ID of the service principal (enterprise application), not a new app registration.

**Option A: PowerShell (recommended)**

1. Install the Azure PowerShell module (if not already installed):
    ```powershell
    Install-Module -Name Az -AllowClobber -Scope CurrentUser
    ```
2. Sign in to your Azure account:
    ```powershell
    Connect-AzAccount
    ```
3. Retrieve the service principal by using the application ID provided by Microsoft:
    ```powershell
    Get-AzADServicePrincipal -ApplicationId "933838e2-bec1-440f-a634-9363c82e5b6d"
    ```
4. From the output, copy the **Id** value. This is the service principal object ID.

**Option B: Microsoft Graph API**

1. Call the service principals endpoint:

    ```http
    GET https://graph.microsoft.com/v1.0/servicePrincipals?$filter=appId eq '933838e2-bec1-440f-a634-9363c82e5b6d'
    ```

2. In the JSON response, copy the **id** field. This is the service principal object ID.

> [!TIP]
> If you get a permissions error in Graph Explorer, select **Modify Permissions** and grant consent for the required permissions.

#### Step 2: Create the OIDC provider in ServiceNow

1. In ServiceNow, go to **All** > **System OAuth** > **Application Registry**.
2. Select **New**.
3. The configuration steps differ depending on your ServiceNow version.

    **For Yokohama and earlier versions**
    - Choose **Configure an OIDC provider to verify ID tokens**.
    
    **For Zurich and later versions**
    - Select **New Inbound Integration Experience** > **New Integration**.
    - Choose **Third party ID token issued by OIDC supporting identity provider**.

4. Fill in the fields as described in the OIDC provider configuration tables below.

**OIDC provider configuration**

Use the following values in the registration form.

| Field | Value |
| --- | --- |
| Name | Microsoft Entra ID |
| Provider name | Microsoft Entra ID (select existing or create new) |
| Client ID | `933838e2-bec1-440f-a634-9363c82e5b6d` |
| Active | Checked |

Under **OAuth OIDC Provider Configuration**, determine whether a Microsoft Entra ID option already appears in the **OIDC Provider** dropdown. If it exists, select it. If not, select **Create a new configuration** and provide the following values.

| Field | Value |
| --- | --- |
| OIDC Provider Configuration Name | Microsoft Entra ID |
| OIDC Metadata URL | `https://login.microsoftonline.com/<tenantId>/v2.0/.well-known/openid-configuration` (replace `<tenantId>` with your Microsoft Entra tenant ID) |
| OIDC Configuration Cache Lifespan | 120 |
| User Claim | sub or oid |
| User Field | User ID |
| Enable JTI Verification | Disabled |

Under **Auth Scope**, select **useraccount**, and enable **Allow access only to APIs in selected scope**.

#### Step 3: Create the ServiceNow integration user

1. In ServiceNow, go to **All** > **User Administration** > **Users**.
2. Select **New**.
3. Set the following fields.

| Field | Value |
| --- | --- |
| User ID | Service principal object ID from Step 1 |
| Identity Type | Machine |
| Active | Checked |

4. Save the user record.

**Assign roles to the integration user**

Open the user record and, in the **Roles** related list, add these roles: `catalog_admin`, `user_criteria_admin`, `user_admin`.

> [!NOTE]
> If you assigned a customer role to the service account you created for crawling and connection setup, add that custom role to this integration user.

#### Verification

After completing all three steps:

1. **OIDC provider** — Go to **System OAuth** > **Application Registry** and confirm the Microsoft Entra ID entry is **Active** with the correct Client ID and metadata URL.
2. **Integration user** — Go to **User Administration** > **Users**, find the user by the service principal object ID, and confirm that the correct roles are assigned.
3. **Connector setup** — When you configure the connector in the Microsoft 365 admin center, select **Federated Auth** as the authentication method and provide your ServiceNow instance URL. The connector authenticates using the OIDC token issued by Microsoft Entra ID.

#### OAuth 2.0

Provision an OAUTH endpoint in your ServiceNow instance for the ServiceNow Knowledge connector to access. For more information, for pervious versions of ServiceNow, see [Create an endpoint for clients to access the instance](https://www.servicenow.com/docs/bundle/xanadu-platform-security/page/administer/security/task/t_CreateEndpointforExternalClients.html); for Zurich versions, see [Configure an OAuth authorization code grant](https://www.servicenow.com/docs/r/platform-security/authentication/configure-an-oauth-authorization-code-grant.html).

Use the information in the following table to complete the endpoint creation form.

| Field | Description | Recommended value |
|   --- | --- | --- |
| Name | Unique value that identifies the application that you require OAuth access for. | Microsoft Search |
| Client ID | A read-only, autogenerated unique ID for the application. The instance uses the client ID when it requests an access token. | NA |
| Client secret | With this shared secret string, the ServiceNow instance and Microsoft Search authorize communications with each other. | Follow security best practices by treating the secret as a password. |
| Redirect URL | A required callback URL that the authorization server redirects to. | For **M365 Enterprise**: https://<span>gcs.office.</span>com/v1.0/admin/oauth/callback,</br> For **M365 Government**: https://<span>gcsgcc.office.<span>com/v1.0/admin/oauth/callback |
| Logo URL | A URL that contains the image for the application logo. | NA |
| Active | Select the check box to make the application registry active. | Set to active |
| Refresh token lifespan | The number of seconds that a refresh token is valid. By default, refresh tokens expire in 100 days (8,640,000 seconds). | 31,536,000 (one year) |
| Access token lifespan | The number of seconds that an access token is valid. | 43,200 (12 hours) |
| Auth Scope | The level of access an application has to a resource. | useraccount |


Enter the client ID and client secret to connect to your instance. After you connect, use a ServiceNow account credential to authenticate permission to crawl. The account should at least have the **knowledge** role. For information about the table records and index user criteria permissions to provide read access to, see [Set up permissions to index items](servicenow-knowledge-admin-setup.md#create-service-account-and-set-up-permissions-to-index-items).

#### Microsoft Entra ID OpenID Connect

To use Microsoft Entra ID OpenID Connect:

1. Register a new app as a single tenant in Microsoft Entra ID. A redirect URI isn't required. For more information, see [Register an application](/azure/active-directory/develop/quickstart-register-app#register-an-application). 
1. Copy the **Application (client) ID** and **Directory (tenant) ID** for the app.
1. Create a client secret for the app and save it securely.
    - Go to **Manage** > **Certificates and secrets**.
    - Choose **new client secret**.
    - Provide a name and choose **Save**.
1. Use the following PowerShell cmdlets to retrieve the service principal object ID.
 
    ```powershell
        Install-Module -Name Az -AllowClobber -Scope CurrentUser
    ```
    
    ```powershell
        Connect-AzAccount
    ```
    
    ```powershell
        Get-AzADServicePrincipal -ApplicationId "Application-ID"
    ```

    Replace "Application-ID" with the Application (client) ID of the application you registered in step 2. Note the value of the ID object from the PowerShell output; this value is the Service Principal Object ID.

    Alternatively, you can retrieve the information from the Microsoft Entra admin center: 

    a. On the app registration, go to **Overview**.
    b. Choose **managed application in local directory**.
    c. Choose the URL and copy the **ObjectID**. This is the Service Principal Object ID.


1. In your ServiceNow instance, register a new OAuth OIDC entity. For details, see [Create an OAuth OIDC provider](https://docs.servicenow.com/bundle/xanadu-platform-security/page/administer/security/task/add-OIDC-entity.html). Use the values listed in the following table in the registration form; leave the default values for the other fields.

| Field | Description | Value |
| --- | --- | --- |
| Name | A unique name for the OAuth OIDC entity. | Microsoft Entra ID |
| Client ID | From Microsoft Entra ID registration | Application (client) ID |
| Client Secret | From Microsoft Entra ID registration | Client secret |

> [!NOTE]
> After you create the OAuth OIDC entity, the client secret is generated automatically in ServiceNow. Replace this client secret with the client secret generated in the Microsoft Entra Admin center. 

6. In the **OAuth OIDC Provider Configuration** field, select the search icon, and then select **New**.

7. Fill out OIDC provider configuration form as follows:

    | Field | Value |
    | --- | --- |
    |  OIDC Provider |  Microsoft Entra ID |
    |  OIDC Metadata URL | Use the following URL: `https://login.microsoftonline.com/<tenantId>/.well-known/openid-configuration `.<br/><br/>Replace `<tenantId>` with the Directory (tenant) ID. |
    |  OIDC Configuration Cache Life Span |  120 |
    |  Application | Global |
    |  User Claim | sub |
    |  User Field | User ID |
    |  Enable JTI claim verification | Disabled |

   Set **Auth Scope** to the user account.

9. Choose **Submit** to save the configuration.

10. Create a ServiceNow account. For details, see [Create a user in ServiceNow](https://docs.servicenow.com/bundle/xanadu-platform-administration/page/administer/users-and-groups/task/t_CreateAUser.html). Use the following values; leave other fields as default:

| Field | Recommended value |
| --- | --- |
| User ID | Service Principal ID | 
| Web service access only | Checked |

10. Assign the **Knowledge** role to the ServiceNow account. For details, see [Assign a role to a user](https://docs.servicenow.com/bundle/xanadu-platform-administration/page/administer/users-and-groups/task/t_AssignARoleToAUser.html). Use the **Application ID** as the Client ID and **Client secret** in the admin center configuration wizard to authenticate with Microsoft Entra ID OpenID Connect.

> [!NOTE]
> Don't turn on **Assignment required**. For more information, see [Properties of an enterprise application - Microsoft Entra ID](/entra/identity/enterprise-apps/application-properties#assignment-required).

### Add API namespace

If you're using the **Advanced** flow, enter the API namespace that you created in your ServiceNow instance. For details, see [Set up REST API](servicenow-knowledge-admin-setup.md#set-up-rest-api). 

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout](staged-rollout.md).

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

After you create your connection, you can review the status (including count of indexed users & articles) in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/). When the connection status is **Ready**, you can validate the connection by providing the `sys_id` of any knowledge article and verifying its user permissions. For more information, see [Search and validate indexed content](indexed-content.md).

## Customize settings

You can customize the default values for the ServiceNow Knowledge connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

The ServiceNow Knowledge Copilot connector supports the following user search permissions:

- Everyone
- Only people with access to this data source (default)
 
If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to it. 

> [!NOTE]
> If a knowledge article and its knowledge base don't have any `Can Read` user criteria applied, the article appears in the results for everyone in the organization, provided that the `glide.knowman.block_access_with_no_user_criteria` property is set to `false` in your ServiceNow instance. If this property is `true`, or if the service account doesn't have access to the `sys_properties` table (in which case the connector defaults to `true`), articles without user criteria are blocked from appearing in search results. For more information, see [Set up hierarchical permissions](servicenow-knowledge-admin-setup.md#set-up-hierarchical-permissions).

#### Map identities

By default, ServiceNow maps email IDs to Microsoft Entra ID (UPN or Mail). You can provide a custom mapping formula if your organization uses different identity attributes. For more information, see [Map non-Microsoft Entra ID identities](map-non-entra-id.md).

### Customize content settings

#### Query string

ServiceNow uses the following default filter: `active=true^workflow_state=published`.

You can modify this filter to index only specific articles based on your organizational needs. Use ServiceNow’s encoded query string builder to create custom filters. For more information, see [Generate an encoded query string through a filter](https://www.servicenow.com/docs/bundle/xanadu-platform-user-interface/page/use/using-lists/task/t_GenEncodQueryStringFilter.html).

#### Manage properties

You can manage properties in the following ways:

- Add properties to index from ServiceNow.
- Customize the **AccessUrl** property to reflect your organization’s URL format.

The following table lists the properties that the ServiceNow Knowledge connector indexes by default.

> [!NOTE]
> You can view but you can't edit the schema attributes (Searchable, Queryable, Retrievable, Refinable), semantic labels, and aliases for these default properties. You can, however, add more custom properties and edit the property attributes when you create the connection. After you create the connection, you can't edit the property attributes. 

|Property |Semantic Label |Description |Schema Attributes|
|---|---|---|---|
|AccessUrl| url | The target URL of the item in the data source. | Retrieve |
|Active| | A Boolean field that indicates whether the article is currently active and can be viewed or searched by users. | |
|ArticleType | | The format of the article, often an HTML or Wiki type. | Query |
|Author| Authors | All the people who participated/collaborated on the item in the data source | Query, Refine Retrieve |
|CanReadUserCriteria | | Provides the user criteria that define the audience that has access to view the article. | |
|CannotReadUserCriteria | |  Provides the user criteria that define the audience that is explicitly denied access to view the article. | |
|CmdbCi | | A reference to a Configuration Item (CI) from the CMDB, linking the article to a specific asset or service. | Query, Retrieve, Search |
|Description | | A brief summary of the article's content, which helps users understand what the article is about from search results. | Retrieve, Search |
|EntityType | | The type of entity the article is about (Knowledge) | Query, Refine, Retrieve |
|HelpfulCount | | The number of times users marked the article as helpful. | |
|IconUrl |IconUrl |Icon URL that represents the article's category or type. | Retrieve |
|ItemPath | | The path of the article within the knowledge base hierarchy. | Query, Refine, Retrieve, Search |
|KbCategory | | The category the article belongs to within its knowledge base. | Query, Retrieve, Search |
|KbKnowledgeBase | |  The knowledge base the article is stored in. | Query, Retrieve, Search |
|KbKnowledgeBaseUrl | | A URL linking to the knowledge base | Query, Retrieve |
|MetaDescription | | A short description used in search engine results | Retrieve, Search |
|Number | |  A unique identifier automatically assigned to the knowledge article, such as 'KB0000001' | Query, Retrieve, Search |
|PreviewContent | | The content used for a quick preview of the article. | Retrieve |
|Published | | A date/time stamp indicating when the article was published and made visible to users. | Query, Retrieve |
|Rating | | The average rating given to the article by users. | Query, Retrieve |
|ShortDescription | Title | The title of the item that you want to be shown in Copilot and other search experiences | Query, Retrieve, Search|
|SysClassName | | Identifies the template for the knowledge. Knowledge for standard templates, Other values can be FAQ, How to, and so on. | |
|SysCreatedBy | Created by | Name of the person who created the article | Query, Refine, Retrieve|
|SysCreatedOn | Created date time |Date and time that the article was created | Query, Refine, Retrieve|
|SysDomain | | The domain to which the knowledge article belongs in a multi-domain instance | |
|SysId | | The unique 32-character ID for the article, used for backend identification. | Query, Retrieve |
|SysModCount | | The number of times the article was modified. | Retrieve |
|SysTags | | Keywords or tags that can be added to the article to improve searchability and organization. | Query, Refine, Retrieve, Search |
|SysUpdatedBy | Last modified by | Name of the person who most recently edited the article. | Query, Refine, Retrieve|
|SysUpdatedOn | Last modified date time | Date and time when the item was last modified | Query, Refine, Retrieve|
|SysViewCount | | The number of times the article was viewed. | Query, Retrieve |
|TaxonomyTopic | | A reference to a topic in a defined taxonomy, used for a structured organization. | Query, Retrieve, Search |
|Topic | |  Another field for article categorization | Query, Retrieve, Search |
|UseCount | |  The number of times the article was attached to another record, like an incident or problem. | |
|ValidTo | | The expiration date of the article. After this date, article won't be returned in search result | Query, Retrieve |
|WorkflowState| |  The current state of the article in its lifecycle, such as 'Draft', 'Review', 'Published', or 'Retired'. | Query, Refine, Retrieve |
|Content `Content`| |  The main body of the article, where the detailed information is written. | Search |

#### Customize AccessURL property

To define a custom expression for the **AccessURL** property: 

1. On the **Content** tab, go to **Manage properties**.
2. In the **Properties** table, select the **AccessURL** property.
3. In the side panel, under **Default expression**, enter your custom expression in the **New default expression** field. Use `${PropertyName}` syntax for dynamic values. For example: `https://instancedomain.service-now.com/sp?id=kb_article&sys_id=${SysId}`.
4. Select **Save changes**.
5. To preview the result, select **Preview data** and scroll to the customized property.

> [!NOTE]
> - You must create a new ServiceNow Knowledge connection to customize the **AccessURL** property. Editing an existing connection to customize the schema property isn't currently supported.   

You can override the default expression for specific knowledge articles by using rules based on property filters. To add a rule: 
1. Under **Set additional rules to configure expressions**, select **Add new rule**.
2. In the rule panel:
   - Choose a filter property (for example, Category).
   - Enter one or more values (comma-separated, case-sensitive).
   - Define the custom expression for those values. 
3. Select **Save changes**.
4. To preview, select **Preview data** and scroll to the customized property. 

> [!NOTE]
> If multiple rules apply to an item, the first rule in the list is used. Changes take effect after the next full crawl.

For more information, see [Customize values for certain schema properties](deployment-overview.md#customize-values-for-certain-schema-properties).

### Customize sync intervals

Configure the sync schedule to keep indexed content up to date:

- **Full crawl** – Reindexes all content, removes deleted content, and updates all permissions. The default frequency is daily.
- **Incremental crawl** – Syncs changed content and recomputes permissions for those changed articles and article-level permission changes. Doesn't update user-to-criteria mappings (identity sync) or permissions for articles where knowledge base (parent) level permissions changed. The default frequency is every 15 minutes.

> [!IMPORTANT]
> - Identities (group memberships created between users and user criteria) are only updated during full crawls. Incremental crawls don't update identities or group memberships.
> - During the first full crawl, identity sync (such as reading users, user criteria, and mapping of users to user criteria such as group memberships) runs first, followed by content sync. This ensures that the right permissions are mapped to the ingested items.
> - During subsequent periodic full crawls, content and identity sync happens in parallel. The periodic full crawl is complete when both content and identity sync is finished.
> -  The periodic full crawls are faster than the first full crawls because the first crawl includes first-time discovery and ingestion of users, user criteria, and their mapping and content items. Periodic full crawls recrawl all content and recompute permissions, but ingestion is faster because items already exist in the index. Identity sync uses differential updates, only pushing membership changes to Microsoft Graph. 

For more information, see [Guidelines for crawl settings](deployment-overview.md#guidelines-for-crawl-settings).

## Related content

- [ServiceNow Knowledge connector overview](servicenow-knowledge-overview.md)
- [Set up the ServiceNow service for connector ingestion](servicenow-knowledge-admin-setup.md)
- [Troubleshoot issues with the ServiceNow Knowledge connector](servicenow-knowledge-troubleshooting.md)