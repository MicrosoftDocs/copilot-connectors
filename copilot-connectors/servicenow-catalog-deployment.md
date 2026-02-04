---
title: "Deploy the ServiceNow Catalog Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.reviewer: mayanksethi
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 12/09/2025
ms.localizationpriority: Medium
description: "Find information about how to deploy the ServiceNow Catalog Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the ServiceNow Catalog Microsoft 365 Copilot connector

The ServiceNow Catalog Microsoft 365 Copilot connector enables your organization to index catalog items from ServiceNow and makes them discoverable in Microsoft 365 experiences, including Copilot and Microsoft Search. This article describes the steps to deploy and customize the connector.

For general information about Copilot connector deployment, see [Set up Copilot connectors in the Microsoft 365 admin center](/microsoftsearch/configure-connector).

For advanced ServiceNow configuration information, see [Set up the ServiceNow Catalog service for connector ingestion](servicenow-catalog-admin-setup.md).

## Prerequisites

Before you deploy the ServiceNow Catalog connector, make sure that your ServiceNow environment is configured correctly. The following table summarizes the steps to configure the ServiceNow Catalog environment and deploy the connector.

| Role | Task |
| ---- | ---- |
| ServiceNow admin | [Configure the environment](servicenow-catalog-admin-setup.md#configure-the-servicenow-environment) |
| ServiceNow admin/Network admin | [Set up prerequisites](servicenow-catalog-admin-setup.md#set-up-connector-prerequisites) |
| Microsoft 365 admin | [Deploy the connector in the Microsoft 365 admin center](#deploy-the-connector) |
| Microsoft 365 admin | [Customize connector settings](#customize-settings-optional) (optional) |

Before you deploy the connector, make sure that you meet the following prerequisites:

- You're a Microsoft 365 admin.
- You have the ServiceNow instance URL.
- You created a ServiceNow service account with read access to required tables.
- The network firewall allows access to Microsoft connector IP ranges.
- You provisioned OAuth or OpenID Connect credentials, if applicable.
- You populated the description and short description fields for catalog items.

## Deploy the connector

To add the ServiceNow Catalog connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Go to the **Connectors** tab, and in the left pane, choose **Gallery**.
1. From the list of available connectors, choose **ServiceNow Catalog**.

### Set display name

The display name identifies references in Copilot responses and helps users recognize trusted content. You can accept the default **ServiceNow** display name or customize it to match your organization's terminology.

For more information, see [Enhance Copilot discovery of connector content](/microsoftsearch/enhancing-microsoft-copilot-discovery-with-graph-connector-content).

### Choose flow based on user criteria 

The ServiceNow Catalog connector supports two flows for user criteria permissions: **Simple** and **Advanced**. 

The default is **Simple**. In this flow, advanced script-based user criteria aren't considered while evaluating catalog item permissions. 

If your ServiceNow instance uses **Advanced Scripts** in your catalog category or catalog item user criteria, use the **Advanced** flow. This flow ensures accurate permissions handling when content is ingested into Microsoft Graph. For more information, see [Check for advanced scripts](servicenow-catalog-admin-setup.md#check-for-advanced-scripts-in-servicenow). 

### Set instance URL

To connect to your ServiceNow site, use your organization’s instance URL, which is typically the following URL:

`https://<your-organization-name>.service-now.com`

If your organization uses a custom portal (for example, ESC or SP), provide the correct URL during setup. For help with identifying your instance URL, contact your ServiceNow admin or check your portal configuration.

### Choose authentication type

Choose one of the following authentication methods:

- **Basic authentication**: Use a ServiceNow account with the `catalog` role. Enter the username and password directly in the connector setup.
- **OAuth 2.0 (recommended)**: Configure an OAuth endpoint in ServiceNow and provide client ID and secret. For details, see [OAuth 2.0](#oauth-20).
- **Microsoft Entra ID OpenID Connect**: Use registered application credentials from Microsoft Entra ID. For details, see [Microsoft Entra ID OpenID Connect](#microsoft-entra-id-openid-connect).

#### OAuth 2.0

To use ServiceNow OAuth for authentication:

- A ServiceNow admin must provision an OAuth endpoint in your ServiceNow instance. For more information, see [Create an endpoint for clients to access the instance](https://www.servicenow.com/docs/bundle/xanadu-platform-security/page/administer/security/task/t_CreateEndpointforExternalClients.html).
- Provide the following values in the endpoint creation form.

  | Field             | Description | Recommended value |
  |-------------------|-------------|-------------------|
  | Name              | Unique value that identifies the application that you require OAuth access for.  | Microsoft Search  |
  | Client ID         | A read-only, autogenerated unique ID for the application. The instance uses the client ID when it requests an access token. | Autogenerated    |
  | Client secret     | With this shared secret string, the ServiceNow instance and Microsoft Search authorize communications with each other.  | Treat as password |
  | Redirect URL      | A required callback URL that the authorization server redirects to.  | For Microsoft 365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`<br><br>For Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback` |
  | Logo URL | A URL that contains the image for the application logo. | NA |
  | Active            | Select the check box to make the application registry active. | Checked           |
  | Refresh token lifespan | The number of seconds that a refresh token is valid. By default, refresh tokens expire in 100 days (8,640,000 seconds).  | 31,536,000 seconds (one year) |
  | Access token lifespan  | The number of seconds that an access token is valid.  | 43,200 seconds (12 hours) |

- Enter the client ID and client secret in the connector setup.
- Use a ServiceNow account credential with at least the `catalog` role to authenticate crawl permissions.

#### Microsoft Entra ID OpenID Connect

To use Microsoft Entra ID OpenID Connect:

1. **Register a new application** in Microsoft Entra ID. For more information, see [Register an application](/entra/identity-platform/quickstart-register-app#register-an-application).
   - Select single-tenant organizational directory.
   - Note the Application (client) ID and Directory (tenant) ID.

1. **Create a client secret** and save it securely. For more information, see [Creating a client secret](/entra/identity-platform/quickstart-register-app#add-a-client-secret).
    - Go to **Manage** > **Certificates and secrets**. 
    - Choose **new client secret**. 
    - Provide a name and choose **Save**.

1. **Retrieve the Service Principal Object Identifier** by using PowerShell.

   ```powershell
   Install-Module -Name Az -AllowClobber -Scope CurrentUser
   Connect-AzAccount
   Get-AzADServicePrincipal -ApplicationId "<Application-ID>"
   ```

    Replace "Application-ID" with the Application (client) ID of the application you registered in step 2. Note the value of the ID object from the PowerShell output; this value is the Service Principal Object ID.

    Alternatively, you can retrieve the information from the Microsoft Entra admin center: 
    a. On the app registration, go to **Overview**. 
    b. Choose **managed application in local directory**. 
    c. Choose the URL and copy the **ObjectID**. This is the Service Principal Object ID.

1. In your ServiceNow instance, register the ServiceNow application. For details, see [Create an OAuth OIDC provider](https://www.servicenow.com/docs/bundle/xanadu-platform-security/page/administer/security/task/add-OIDC-entity.html). Use the values listed in the following table in the registration form; leave the default values for the other fields. 

    | Field | Description | Value |
    |-------|-------------|-------|
    | Name | A unique name for the OAuth OIDC entity. | Microsoft Entra ID |
    | Client ID | From Microsoft Entra ID registration | Application (client) ID |
    | Client secret | From Microsoft Entra ID registration | Client secret |

    > [!NOTE]
    > After you create the OAuth OIDC entity, the client secret is generated automatically in ServiceNow. Replace this client secret with the client secret generated in the Microsoft Entra Admin center. 

1. In the **OAuth OIDC Provider Configuration** field, select the search icon, and then select **New**. Fill out OIDC provider configuration form as follows.

    | Field | Value |
    |-------|-------|
    |OIDC Provider | Microsoft Entra ID |
    |OIDC Metadata URL | `https://login.microsoftonline.com/<tenantId>/.well-known/openid-configuration` |
    |OIDC OIDC Configuration Cache Life Span Application | Global |
    |User Claim | sub |
    |User Field | User ID |
    |Enable JTI claim verification | Disabled | 

1. Choose **Submit** to save the configuration. 

1. Create a ServiceNow account. For details, see [Create a user in ServiceNow](https://docs.servicenow.com/bundle/xanadu-platform-administration/page/administer/users-and-groups/task/t_CreateAUser.html). Use the following values; leave other fields as default.

    | Field | Recommended value |
    |-------|-------------------|
    |User ID | Service Principal ID |
    |Web service access only | Checked |

1. Assign the **Catalog** role to the ServiceNow account. For details, see Assign a role to a user. Use the **Application ID** as the Client ID and **Client secret** in the admin center configuration wizard to authenticate with Microsoft Entra ID OpenID Connect. 

> [!NOTE]
> `Assignment required` must not be enabled. For more information, see [Properties of an enterprise application](/entra/identity/enterprise-apps/application-properties#assignment-required). 

### Add API namespace

If you're using the **Advanced** flow, enter the API namespace that you created in your ServiceNow instance. For details, see [Set up REST API](servicenow-catalog-admin-setup.md#set-up-rest-api). 

### Roll out

To validate the connector before a full deployment, roll it out to a limited audience:

1. Select the toggle next to **Rollout to limited audience**.
1. Specify the users or groups for pilot rollout.

For more information, see [Staged rollout for Copilot connectors](/microsoftsearch/staged-rollout-for-graph-connectors).

Choose **Create** to deploy the connection. The ServiceNow Catalog connector begins indexing content immediately.

After you create your connection, you can review the status (including count of indexed users and items) in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

When the connection status is ready, you can validate the indexed content item using the index browser by providing the `sys_id` of any catalog item that you want to test for and checking its permissions for users. For more information, see [Search and validate indexed content](connectors-index-search.md).

The following sections list default values that are set. To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

#### Users

- **Access permissions**: Only people with access to content in data source.
- **Identity mapping**: Data source identities mapped using Microsoft Entra IDs.

#### Content

- **Query filter*:** Indexed content is filtered based on the following default query: `active=true^workflow_state=published`
- **Indexed properties:** For a list of the default properties and schema, see [Manage indexed properties](#manage-indexed-properties).


#### Sync

- **Incremental crawl**: Every 15 minutes.
- **Full crawl**: Every day.

## Customize settings (optional)

You can customize the default values for the ServiceNow Catalog connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

The ServiceNow Catalog connector supports the following user search permissions:

- **Everyone**
- **Only people with access to this data source** (default)

If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to it as per the user criteria.

> [!Important]
> - If a catalog item is not enabled with a user criterion, it appears in the results for everyone in the organization.
> - In ServiceNow, both catalog item-level and category-level user criteria are considered when read permissions are assessed for a user. However, the ServiceNow Catalog connector currently doesn't read category-level permissions.
>     - If the catalog item contains the `Available For` user criteria, they are stamped on the catalog item during ingestion and Catalog Category `Available for`/`Not Available For` user criteria are ignored.
>     - If the catalog item contains the `Not available for` user criteria, and if the corresponding catalog category also contains some `Not available for` user criteria, both the user criteria are stamped on the catalog item.
>     - If a user is part of the `Available for` user criteria at the catalog item level but not a part of the `Available for` user criteria at the catalog category level, the user doesn't have access to the catalog item in ServiceNow but does have access to the catalog item in Copilot, Microsoft Search, and other Microsoft 365 surfaces. The workaround is to remove the user from the `Available for` user criteria at the catalog item level.


#### Map identities

By default, ServiceNow maps users' email IDs in ServiceNow to their corresponding Microsoft Entra ID (UPN or Mail). You can provide a custom mapping formula if your organization uses different identity attributes. For more information, see [Map non-Microsoft Entra ID identities](map-non-aad.md).

### Customize content settings

To customize the content, on the **Content** tab, you can:

- Modify the query string to filter catalog items.
- Select and manage indexed properties and set them as searchable, retrievable, and refinable.
- Customize the **AccessUrl** property to match your organization’s portal format. For example: `https://instancedomain.service-now.com/sp?id=sc_cat_item&sys_id=${SysId}`.
- Define rules to customize URLs based on catalog category.
- Preview sample data to validate property values and filters.

#### Query string 

ServiceNow uses the following default filter: `active=true^workflow_state=published`.

You can modify this filter to index only specific catalog items based on your organizational needs. Use ServiceNow's encoded query string builder to create custom filters. For more information, see [Generate an encoded query string through a filter](https://www.servicenow.com/docs/bundle/xanadu-platform-user-interface/page/use/using-lists/task/t_GenEncodQueryStringFilter.html).


#### Manage indexed properties

The following properties are indexed by default. These properties affect how users can search, filter, and view catalog items in Microsoft 365 Copilot.

> [!NOTE]
> You can view but you can't edit the schema attributes (Searchable, Queryable, Retrievable, Refinable), semantic labels, and aliases for the default properties. You can, however, add more custom properties and edit the attributes for those properties, but only when you set up the connection. After you create the connection, you can't edit any property attributes.

| **Property** | **Semantic label** | **Description** | **Schema attributes** |
|----|----|----|----|
| AccessUrl | url | Target URL of the item in the data source | Retrieve |
| Active |  | Indicates whether the catalog item is active | Query |
| Authors | Authors | People who collaborated on the item | Query, Retrieve, Search |
| Category |  | Category within the catalog | Query, Retrieve |
| Delivery Time |  | Estimated fulfillment time | Query, Retrieve, Search |
| Description | Content | Description of the catalog item | Search |
| EntityType |  | Entity type for catalog items | Query, Refine, Retrieve |
| IconUrl | IconUrl | Icon representing the item’s category or type | Retrieve |
| ItemPath |  | Path or location within the catalog hierarchy | Query, Refine, Retrieve |
| Model |  | Model associated with the item | Query, Retrieve, Search |
| Name | Title | Title of the item | Retrieve, Search |
| Owner |  | Responsible user or group | Query, Refine, Retrieve |
| Price |  | Cost of the item | Query, Retrieve |
| ScCatalogs |  | Specific catalog the item belongs to | Query, Retrieve |
| ShortDescription |  | Brief summary of the item | Retrieve, Search |
| SysCreatedBy | Created by | Creator of the item | Query, Retrieve |
| SysCreatedOn | Created date time | Creation timestamp | Query, Retrieve |
| SysId |  | Unique identifier | Query, Retrieve, Search |
| SysTags |  | Tags for categorization and filtering | Query, Refine, Retrieve |
| SysUpdatedBy | Last modified by | Last editor of the item | Query, Retrieve |
| SysUpdatedOn | Last modified date time | Last modification timestamp | Query, Retrieve |
| TaxonomyTopic |  | Topic from defined taxonomy | Query, Retrieve, Search |
| Type |  | Type of catalog item (Item, Task, Bundle, etc.) | Query, Retrieve |
| Vendor |  | External vendor or supplier | Query, Retrieve, Search |

#### Set a default expression for AccessURL

To define a custom expression for the **AccessURL** property:

1. On the **Content** tab, go to **Manage properties**.
1. In the **Properties** table, select the `AccessURL` property.
1. In the side panel, under **Default expression**, enter your custom expression in the **New default expression** field.
    Use `${PropertyName}` syntax for dynamic values. For example: `https://instancedomain.service-now.com/sp?id=sc_cat_item&sys_id=${SysId}`.
1. Select **Save changes**.
1. To preview the result, select **Preview data** and scroll to the customized property.

> [!NOTE]
> To customize the **AccessURL** schema property, you need to create a new ServiceNow Catalog connection for your connector. Editing the **AccessURL** property for an existing connection isn't currently supported.


#### Add rules for conditional expressions

You can override the default expression for specific catalog items using rules based on property filters. To add a rule:

1. Under **Set additional rules to configure expressions**, select **Add new rule**.
1. In the rule panel:
    - Choose a filter property (for example, Category).
    - Enter one or more values (comma-separated, case-sensitive).
    - Define the custom expression for those values.
1. Select **Save changes**.
1. To preview, select **Preview data** and scroll to the customized property.

> [!NOTE]
> If multiple rules apply to an item, the first rule in the list is used. Changes take effect after the next full crawl.

For more information, see [Customize values for certain schema properties](configure-connector.md#customize-values-for-certain-schema-properties).

### Customize sync intervals

You can define the frequency of incremental and full crawls:

- **Full crawl** – Reindexes all content, removes deleted content, and updates all permissions. The default frequency is daily.
- **Incremental crawl** – Syncs only changed content, not permissions updates. The default frequency is every 15 minutes.

> [!NOTE]
> - Identities (users/groups) or access permissions are only updated during full crawls.
> - Incremental crawls don't update access permissions or group memberships.
> - During the first full crawl, identity sync (reading users, user criteria, and mapping of users to user criteria such as group memberships) runs first, followed by content sync. This ensures that the right permissions are mapped to the ingested items. 
> - During subsequent full crawls, content and identity sync happens in parallel. The full crawl is complete when both content and identity sync are completed. 
> - Subsequent full crawls are faster than the first full crawl. The first crawl includes first-time discovery and ingestion of users, user criteria, and their mapping and content items. Subsequent full crawls only ingest the newly discovered items, users, and user criteria. 


For more information about full and incremental crawls, see [Guidelines for sync settings](/microsoftsearch/configure-connector#guidelines-for-sync-settings).

## Related content

- [ServiceNow Catalog connector overview](servicenow-catalog-overview.md)
- [Troubleshoot issues with the ServiceNow Catalog connector](servicenow-catalog-troubleshooting.md)
- [Set up Copilot connectors in the admin center](/microsoftsearch/configure-connector)
