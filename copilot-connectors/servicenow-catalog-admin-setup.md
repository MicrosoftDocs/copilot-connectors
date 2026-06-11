---
title: "Set up the ServiceNow service for ServiceNow Catalog connector ingestion"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: mayanksethi
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 06/10/2026 
ms.localizationpriority: Medium
description: "Get the steps that the ServiceNow admin needs to complete for your organization to configure the ServiceNow Catalog Copilot connector."
---

# Set up the ServiceNow service for ServiceNow Catalog connector ingestion

This article provides information about the configuration steps that ServiceNow admins need to complete in order for your organization to deploy the ServiceNow Catalog connector. For information about how to deploy the connector, see [Deploy the ServiceNow Catalog connector](servicenow-catalog-deployment.md).

## Setup checklist

The following checklists list the steps involved in configuring the environment and setting up the connector prerequisites.

#### Configure the environment

| Task | Role |
|------|------|
| [Identify the instance URL](#identify-the-servicenow-instance-url) | ServiceNow admin |
| [Identify the portal configuration](#identify-the-servicenow-portal-configuration) | ServiceNow admin |
| [Define attribute mapping](#define-servicenow-attribute-mapping) | ServiceNow admin |
| [Check for advanced scripts and hierarchical permissions](#check-for-advanced-scripts-and-hierarchical-permissions-in-servicenow) | ServiceNow admin |
| [Verify that descriptions and short descriptions are populated](#verify-that-description-and-short-description-fields-for-all-catalog-items-are-populated) | ServiceNow admin |
| [Identify custom widget-based forms](#identify-custom-widget-based-catalog-forms) |

### Set up connector prerequisites

| Task | Role |
|------|------|
| [Create service account and set up permissions](#create-service-account-and-set-up-permissions-to-index-items) | ServiceNow admin |
| [Identify item count for ingestion](#identify-item-count-for-ingestion) | ServiceNow admin |
| [Set up REST API](#set-up-rest-api) | ServiceNow admin |
| [Set up hierarchical permissions](#set-up-hierarchical-permissions) | ServiceNow admin |
| [Add Microsoft 365 IP address to allowlist](#add-microsoft-365-ip-address-to-the-allowlist) | ServiceNow admin/Network admin |
| [Resolve issues with SSO configuration](#resolve-connector-setup-issues-with-servicenow-sso-configuration) | ServiceNow admin |

## Configure the ServiceNow environment

The following sections describe the admin tasks to configure the ServiceNow environment to enable and optimize the connection.

### Identify the ServiceNow instance URL

To connect the ServiceNow Catalog connector to your ServiceNow data, the Microsoft 365 admin needs your organization's ServiceNow instance URL. The URL typically follows the format:

`https://<your-organization-name>.service-now.com`

To verify the URL for your ServiceNow instance, check the ServiceNow admin dashboard or the sign in URL used by your organization. 

If you have a custom URL:

- In your ServiceNow instance, go to **All** > **Custom URL** > **Custom URLs**.

### Identify the ServiceNow portal configuration

By default, Copilot-generated links for ServiceNow Catalog items follow the standard format:

`https://<your-organization-name>.service-now.com/sp?id=sc_cat_item&sys_id=<sysid>`

If your organization uses a different URL, you can customize the URL when you deploy the connector. For more information, see [Customize connector settings](deployment-overview.md#customize-connector-settings-optional).

### Define ServiceNow attribute mapping

By default, Microsoft Entra ID maps identities from your data source by checking whether the email ID of ServiceNow users matches the user principal name (UPN) or **Mail** attribute in Microsoft Entra ID.

If this default mapping doesn’t meet your organization’s needs, you can define a custom mapping formula. For more information, see [Map your non-Entra ID identities](map-non-entra-id.md).

### Check for advanced scripts and hierarchical permissions in ServiceNow

Determine whether catalog items in your ServiceNow environment have Advanced scripts enabled in **User Criteria**.

This setting can affect indexing behavior and access control when content is surfaced in Microsoft 365 experiences like Copilot.

To determine whether any **User Criteria** has advanced scripts enabled, run the following API call:

`<ServiceNowURL>/api/now/table/user_criteria?advanced=true&sysparm_limit=1`

If your instance uses advanced script-based user criteria, select **Advanced flow** when you deploy the connector.

#### What are hierarchical permissions?

ServiceNow Catalog supports setting permissions at both the Catalog Category (parent) level and the individual catalog item (child) level. These permissions are evaluated together to determine whether a user has access to a catalog item. This model is referred to as hierarchical permissions.

Hierarchical permissions are supported for the ServiceNow Catalog connector. This feature isn't available in government or sovereign clouds or dedicated forests in multi-tenant environments. For more information, see [Set up hierarchical permissions](#set-up-hierarchical-permissions).

### Verify that description and short description fields for all catalog items are populated

Copilot uses descriptions and short descriptions to semantically match catalogs based on user prompts. Missing descriptions affect the relevance of Copilot responses. Be sure to populate both description and short description fields for all catalog items that you want to index.

### Identify custom widget-based catalog forms

Some ServiceNow environments use custom widget-based catalog forms to enhance the UI. Copilot connectors don't currently support indexing catalog items rendered through custom widget-based forms. As a workaround, create Knowledge Base articles with clear descriptions of the service and the custom catalog form URLs.

## Set up connector prerequisites

The following sections describe the prerequisite steps to complete before deploying the ServiceNow Catalog connector.

### Create service account and set up permissions to index items

To connect to ServiceNow and allow the ServiceNow Catalog connector to update items regularly, you need a service account with read access to specific ServiceNow table records. The following table lists the required table records.

|Feature | Read access required tables | Description |
|:--- | --- | --- |
|Index catalog items available to <em>Everyone</em> | sc_cat_item | For crawling catalog items. |
|Index catalog categories | sc_category | Read Catalog category information. |
|Index catalog item form fields (variables) | item_option_new | Stores catalog item variables (form fields) such as dropdowns, checkboxes, text fields, and so on. |
|Index variable choices | question_choice | Stores selectable options for catalog variables (for example, dropdown values). |  
|Index variable sets (if used) | item_option_set | Contains reusable variable sets linked to multiple catalog items. |
|Index item-variable relationships | sc_item_option_mtom | Defines many-to-many relationships between catalog items and variables. |
|Index and support user criteria permissions | sc_cat_item_user_criteria_mtom | Who can access this catalog item. |
| | sc_cat_item_user_criteria_no_mtom | Who can't access this catalog item. |
| | sc_category_user_criteria_mtom | Who can access this catalog category. |
| | sc_category_user_criteria_no_mtom | Who can't access this catalog category. |
| | user_criteria | Read user criteria permissions. |
|Index user related information | sys_user | Read user information. |
| | sys_user_has_role | Read role information of users. |
| | sys_user_grmember\** | Read group membership of users. |
| | sys_user_group | Read user group segments |
| | sys_user_role | Read user roles. |
| | cmn_location\** | Read user location information. |
| | cmn_department\** | Read user department information. |
| | core_company\** | Read user company attributes. |
|Index extended table properties (optional)\*** | sys_db_object | Read extended table details. |
| | 	sys_dictionary | 	Read extended table properties. |

\** Access to these tables are only required if simple flow is selected. If you select advanced flow for reading user criteria, you don't need to provide access to these tables. 

\*** If you want to index properties from extended tables of `sc_cat_item`, provide read access to `sys_dictionary` and `sys_db_object`. Access to these tables is optional. You can index `sc_cat_item` table properties without access to these two tables. 

You can create and assign a role for the service account you use to connect with Microsoft Search. For more information, see [Assign a role to a user](https://www.servicenow.com/docs/bundle/xanadu-platform-administration/page/administer/users-and-groups/task/t_AssignARoleToAUser.html). Read access to the tables can be assigned on the created role. 

You can also assign the following roles to the service account to ensure that catalog items get indexed without any blocking ACL issues. Assigning these roles is optional. 
- `catalog_admin`
- `user_criteria_admin`
- `user_admin`

For information about how to create a user, assign a role, and grant read permissions to all the applicable table records, see [Grant table access to a user in ServiceNow](/microsoft-365/copilot/connectors/granting-table-access-servicenow-catalog). 

If the service account doesn't have the required permissions - or if row or field-level permissions are restricted - specific items are excluded from indexing on the Microsoft side.

> [!NOTE]
> Don't explicitly apply `snc_read_only` to the service account. This role denies any write action to any table the user has access to. The account needs to write token and other authentication-related information into some tables. Because tokens are refreshed on a regular basis, this account can't be made read-only after initial authentication. The service account needs write access to the `oauth_credential` table for authentication.

If the service account doesn’t have access to the full User Criteria table, inconsistent behavior related to user permissions, including unintended content oversharing, can occur.

### Identify item count for ingestion

The following default filter is applied during indexing. If you need to make changes, edit the query string during connector setup. For more information, see [Customize query string](/microsoft-365/copilot/connectors/servicenow-knowledge-deployment#query-string). 

`type!=bundle^sys_class_name!=sc_cat_item_guide^type!=package^active=true` 

To verify the item count expected for ingestion:

1. Go to the following URL: `https://<instance-name>.service-now.com/api/now/table/sc_cat_item? sysparm_fields=sys_id&sysparm_query=type!=bundle^sys_class_name!=sc_cat_item_guide^type!=package^active=true`. This link opens a list of `sys_ids`.

    > [!NOTE]
    > If you edit the default query string for indexing selected articles, use the corresponding URL to reflect those query conditions.

1. Open Developer Tools in the same window and type the following code in the console window:

    ```dotnetcli
        fetch('<<same URL as in 1>>')
        .then(res => res.json())
        .then(data => console.log("Count of sys_ids:", data.result.length))
        .catch(err => console.error(err));
    ```

1. Note the item count.

When the connector is set up and item sync is completed, you can check the indexed item count against this expected count to verify that all articles are indexed. For more information, see [View connection statistics](view-details.md#view-connection-statistics).

### Set up REST API

To allow the connector to fetch advanced user criteria, create a scripted REST API in your ServiceNow instance. 

Elevate your role in ServiceNow to `security_admin`. 

To set up access control: 

1.  In ServiceNow, go to **All** > **System Security** > **Access Control (ACL)**. 
1.  Choose **New** to create a new ACL. 
1.  Set the following values: 

    **Type**: REST_Endpoint 
    **Operation**: Execute 
    **Name**: Microsoft Copilot 
    **Role**: admin *(or the same role assigned to the crawling account)* 

1.  Choose **Submit**. 

Create the scripted REST API: 

1.  Go to **All** > **System Web Services** > **Scripted Web Services** > **Scripted REST APIs**. 
1.  Choose **New**. 
1.  Enter the following information: 

    **Name**: Microsoft Copilot 
    **API ID**: microsoft_copilot 

1.  Choose **Submit**. 
1.  From the **Scripted REST API** list page, choose **Microsoft Copilot**. 
1.  Set **Default ACLs** to **Microsoft Copilot**. To avoid any issues with authorization, also add the **Scripted REST External Default** ACL. 

Add a resource to the API: 

1.  On the **Resources** tab, choose **New**. 
1.  Provide the following details: 

    **Name**: GetAllUserCriteria 
    **Relative Path**: /user_criteria 
    **Script**: Paste the following code: 

    ```javascript
    (function execute (/*RESTAPIRequest*/ request, /*RESTAPIResponse*/ response) {
       // Get query parameters from the request
       var queryParams = request.queryParams;
       // Extract the 'user' sys_id, ensure it's a string or null if not provided
       var userSysId = queryParams.user ? String(queryParams.user) : null;
       var result = []; // Initialize an empty array for the results
       // Check if userSysId was provided
       if (!userSysId) {
           gs.warn("UserCriteriaLoader API: 'user' parameter was not provided in the request.");
           response.setStatus(400);
           return { "error": "User sys_id is required." };
       }
       try {
           // Instantiate the UserCriteriaLoader
           var userCriteriaLoader = new sn_uc.UserCriteriaLoader();
           var userCriterias = [];
           var userCriteriaGr = new GlideRecord('user_criteria');
           userCriteriaGr.addQuery('active', true); // Select active records. You can also add any connection scope filter if required
           userCriteriaGr.query();
           while (userCriteriaGr.next()) {
               userCriterias.push(userCriteriaGr.getUniqueValue());
           }
           // Call the recommended API to get only matching criteria sys_ids
           var matchingCriteriaIds = sn_uc.UserCriteriaLoader.getMatchingCriteria(userSysId, userCriterias);
           // Return the array of matching criteria objects
           return matchingCriteriaIds;
       } catch (e) {
           // Log any errors that occur during the process
           gs.error("UserCriteriaLoader API: Error processing user criteria for user " + userSysId + ". Error: " + e.message);
           response.setStatus(500); // Internal Server Error
           return {
               error_message: "Error processing user criteria for user " + userSysId,
               error_details: e.message
           };
       }
    })(request, response);
    ```

1.  Make sure both of the following are checked: 

    **Requires authentication** 
    **Requires ACL authorization** 

1.  Make sure that **ACLs** is set to **Microsoft Copilot**. To avoid any issues with authorization, also add the **Scripted REST External Default** ACL. 
1.  Choose **Update**. 

To verify the setup: 

1.  Confirm that the following is the **Resource Path**: `/api/<API Namespace>/microsoft_copilot/user_criteria`. 
1.  Choose **Update** to save the configuration. 

The Microsoft 365 admin enters the **API Namespace** when they [deploy the ServiceNow Catalog connector](servicenow-catalog-deployment.md). In the following example, the API namespace is abcdef. 

`/api/abcdef/microsoft_copilot/user_criteria`

### Set up hierarchical permissions

Hierarchical permissions allow the ServiceNow Catalog connector to evaluate user permissions for any ServiceNow catalog item. The connector evaluates the user criteria applied at the catalog category (parent) and the catalog item (child) level according to the rules that ServiceNow uses. For more information about how ServiceNow evaluates article permission, see [Managing access to catalog category & catalog items](https://www.servicenow.com/docs/bundle/zurich-servicenow-platform/page/product/service-catalog-management/task/t_AppUserCritItemsCat.html).   

To set up hierarchical permissions, the service account used for ServiceNow Catalog connector setup needs read access to all the following tables to successfully evaluate the hierarchical ACLs:

  - `sc_cat_item_user_criteria_mtom` - Who can access this catalog item.
  - `sc_cat_item_user_criteria_no_mtom` - Who can't access this catalog item.
  - `sc_category_user_criteria_mtom` - Who can access this catalog category.
  - `sc_category_user_criteria_no_mtom` - Who can't access this catalog category.
  - `user_criteria` - Read user criteria permissions.
  - `sc_category` - Read Catalog category information. 

> [!NOTE]
> This access applies to both Simple and Advanced flows.

### Add Microsoft 365 IP address to the allowlist

If any network configurations—such as firewall or proxy settings—block access to ServiceNow, make sure to add the IP addresses listed in [IP firewall rules](deployment-overview.md#ip-firewall-rules) to the allowlist.

For information about ServiceNow-specific controls, see [IP Address Access Control](https://www.servicenow.com/docs/bundle/washingtondc-platform-security/page/administer/login/task/t_AccessControl.html).

### Resolve connector setup issues with ServiceNow SSO configuration

If your ServiceNow instance is configured with single sign-on (SSO), you might encounter the following issues during connector deployment:

- During the OAuth process, a **Logout successfully** window might appear without prompting for ServiceNow credentials.
- Microsoft 365 admin credentials might be used to authorize the ServiceNow connection instead of the intended service account.

By default, ServiceNow attempts to connect using Microsoft 365 admin credentials through SSO from a browser sign in. This behavior can cause the connection to fail and result in the **Logout successfully** message.

To resolve these issues:

1. Open a private browser window and sign in using the ServiceNow service account credentials.
2. In a new tab, sign in to the Microsoft 365 admin center using Microsoft 365 admin credentials.

    > [!NOTE]
    > The initial sign in might default to ServiceNow SSO. If that happens, switch to the correct credentials.

3. Retry the OAuth configuration. You should now see a window prompting you to authorize the connection using the service account credentials.

## Next step

> [!div class="nextstepaction"]
> [Deploy the ServiceNow Catalog connector](servicenow-catalog-deployment.md)