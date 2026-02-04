---
title: "ServiceNow Catalog Microsoft 365 Copilot connector troubleshooting"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: mayanksethi
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 01/06/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the ServiceNow Catalog Copilot connector."
---

# Troubleshoot issues with the ServiceNow Catalog Microsoft 365 Copilot connector

The ServiceNow Catalog Microsoft 365 Copilot connector enables organizations to index service catalog items from ServiceNow into Microsoft Graph. Users can search for catalog items directly within Microsoft 365 experiences, including Copilot. This article provides troubleshooting information for common errors that you might encounter when you deploy the ServiceNow Catalog connector.

To verify ServiceNow configuration information to help troubleshoot errors, see [Set up the ServiceNow service for connector ingestion](servicenow-catalog-admin-setup.md).

## Unable to find ServiceNow Catalog item in Copilot or Microsoft Search

Use the following steps to troubleshoot and resolve the issue:

1.  Determine whether the user searching for the article has the [required permissions to access the ServiceNow Catalog items](servicenow-catalog-admin-setup.md#create-service-account-and-set-up-permissions-to-index-items).
2.  Determine whether the user is correctly mapped to a Microsoft Entra identity. Mapping issues show as a `2006` error on the **Error** tab. Check the user mapping formula and update as needed.
3.  Determine whether an advanced script in any of the user criteria grant access to the article. If so, then make sure you select Advanced flow during connection setup and [Set up REST API](servicenow-catalog-admin-setup.md#set-up-rest-api).
4.  Use the [User criteria diagnostics](https://docs.servicenow.com/bundle/washingtondc-servicenow-platform/page/product/knowledge-management/concept/diagnose-knowledge-user-criteria.html) tool in ServiceNow to verify that the service account has access to the item in ServiceNow.
5.  Use the [Access Analyzer tool in ServiceNow](https://www.servicenow.com/docs/bundle/zurich-platform-security/page/integrate/identity/task/view-permissions-for-a-user.html) to debug further if the service account user missed access to any table, field, or record (for example, `user_criteria` table). If you find any access control list (ACL) or role that blocks access to a required table, field, or record, provide the required roles and ACLs to the service account.
6.  If you can't identify the root cause, reach out to the [Copilot connector support team](mailto:MicrosoftGraphConnectorsFeedback@service.microsoft.com) with the following details:

    -  Tenant ID
    -  Connection ID
    -  Content Item Sys ID
    -  Catalog Category Sys ID
    -  For the catalog category:
        -  List of `sys_id` for user criteria available in the `sc_category_user_criteria_mtom` (Available for) field
        -  List of `sys_id` for user criteria available in the `sc_category_user_criteria_no_mtom` (Not available for) field
    -  For the catalog item `sys_id`, share:
        -  List of `sys_id` for user criteria available in the `sc_cat_item_user_criteria_mtom` (Available for) field
        -  List of `sys_id` for user criteria available in the `sc_cat_item_user_criteria_no_mtom` (Not available for) field

When the required access is provided in ServiceNow, start a full crawl for the configured ServiceNow Catalog connector connection.

## Missing access to certain tables 

Without the right access, the crawler might not index all content and might not grant permissions accurately. You must be a ServiceNow admin to troubleshoot this issue.

Use the following steps to validate table permissions by using REST API Explorer:

1.  Impersonate the crawling account you created in your ServiceNow instance.

    Make sure that the account has the following roles: `rest_api_explorer` and `web_service_admin`.

2.  Go to **System Web Services** \> **REST** \> **REST API Explorer**.
3.  Select one of the tables mentioned in the error message.

    :::image type="content" source="media/servicenow-catalog-troubleshooting/rest-api-explorer.png" alt-text="Screenshot of the REST API explorer page.":::

4.  Set `sysparm_limit` to 10 (to limit results for testing).

    :::image type="content" source="media/servicenow-catalog-troubleshooting/sysparm-light-field.png" alt-text="Screenshot of the REST API explorer with the sysparm_light field highlighted.":::

5.  Choose **Send**.
6.  Review the response:

   - If you receive a `403 Status Code` and an error message that states that you're not authorized to access the table, see [Grant table access](/microsoft-365-copilot/connectors/granting-table-access-servicenow) to provide table-level access.

   - If you receive a `200 Status Code` but the response body contains empty results (for example, no fields), row access exists but field-level access is missing. To grant field-level access, see [Grant field-level access](/microsoft-365-copilot/connectors/granting-table-access-servicenow#step-5-grant-field-level-access).

   :::image type="content" source="media/servicenow-catalog-troubleshooting/response-body.png" alt-text="Screenshot of the Response section.":::

   If you don't see the table name in the dropdown, it might indicate lack of access to the table itself.

   Alternatively, you can use a browser to verify access:

   1.  Open a private browser window.
   1.  Enter the following URL (replace placeholders with the right values): `https://\<instance-url\>/api/now/table/\<table_name\>?sysparm_limit=10`.
   1.  When prompted, sign in by using the credentials of the crawling account.
   1. Review the response. If no response or an error appears, the account doesn't have the necessary access.

When the required access is provided in ServiceNow, start a full crawl for the configured ServiceNow Catalog connector connection.

## Issue reading all user criteria from ServiceNow

Sometimes content access might be restricted because the service account doesn't read all user criteria. This issue can happen if you use the `gs.getUserId()` or `gs.getUser()` function within any user criteria. If you use these functions, update these user criteria to avoid them. ServiceNow recommends that the functions use `user_id`.

:::image type="content" source="media/servicenow-catalog-troubleshooting/script.png" alt-text="Screenshot of a script with instructions for implementing a specific user criteria evaluation, including guidelines to avoid certain functions and use a specific variable.":::

If it's not feasible to update the user criteria, a temporary workaround is available. Update the REST API script that supports the use of the `gs.getUserId()` function. 

Use the following script when you [Set up the REST API](servicenow-catalog-admin-setup.md#set-up-rest-api).


```javascript
(function execute (/*RESTAPIRequest*/ request, /*RESTAPIResponse*/ response) {
    // Get query parameters from the request
    var queryParams = request.queryParams;
    // Extract the 'user' sys_id, ensure it's a string or null if not provided
    var userSysId = queryParams.user ? String(queryParams.user) : null;
    // Check if userSysId was provided
    if (!userSysId) {
        gs.warn("UserCriteriaLoader API: 'user' parameter was not provided in the request.");
        response.setStatus(400);
        return { "error": "User sys_id is required." };
    }
    try {
        var userCriterias = [];
        var userCriteriaGr = new GlideRecord('user_criteria');
        userCriteriaGr.addQuery('active', true); // Select active records
        userCriteriaGr.query();
        while (userCriteriaGr.next()) {
            userCriterias.push(userCriteriaGr.getUniqueValue());
        }

        // Impersonate the logged in user
        var imp = new GlideImpersonate();
        // Store the original user who logged in to serviceUser variable, needed to end impersonation.
        var serviceUser = imp.impersonate(userSysId);

        // Call the recommended API to get only matching criteria sys_ids
        var matchingCriteriaIds = sn_uc.UserCriteriaLoader.getMatchingCriteria(userSysId, userCriterias);

        // End impersonation: Change it back to logged in user
        if (serviceUser) imp.impersonate(serviceUser);

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

## Unable to sign in due to SSO enabled ServiceNow instance

If your organization enabled single sign-on (SSO) for ServiceNow, you might encounter authentication issues with the service account. To bypass SSO and use username/password authentication, append `/login.do` to your ServiceNow instance URL, as shown in the following example.

`https://<your-organization>.service-now.com/login.do`

## Unauthorized or forbidden response to API request

### Check table access permissions

If you receive a forbidden or unauthorized response, verify that the service account has read access to all required tables. Make sure that the service account has read access to all columns in the tables listed in the [prerequisites](servicenow-catalog-admin-setup.md#set-up-connector-prerequisites).

### Change in account password

The connector uses an access token that refreshes every 12 hours. If the service account password changes after you publish the connection, reauthenticate the connection to avoid token failures.

### ServiceNow instance behind a firewall

If your ServiceNow instance is behind a firewall, the connector might not reach it. Add the connector service’s public IP address range to your ServiceNow network allow list.

| Environment | Region | IP range |
| ----------- | ------ | -------- |
| PROD | North America | 52.250.92.252/30, 52.224.250.216/30| 
| PROD        | Europe         | 20.54.41.208/30, 51.105.159.88/30   |
| PROD        | Asia Pacific   | 52.139.188.212/30, 20.43.146.44/30  |

### Access permissions not working as expected

If search results show incorrect access permissions, verify the user criteria configuration in ServiceNow. For more information, see [Applying user criteria to catalog items](https://www.servicenow.com/docs/bundle/xanadu-servicenow-platform/page/product/service-catalog-management/task/t_AppUserCritItemsCat.html).

## Unable to change the URL of an existing connection

When you deploy the ServiceNow Catalog connector, you can customize the URL of the catalog items based on the needs of your organization. Currently, you can't edit the **AccessURL** property for an existing connection. If you have an existing connection and you want to customize the URL, you have to create a new connection and customize the URL during setup. 

For more information, see [Set a default expression for AccessURL](/microsoft-365-copilot/connectors/servicenow-catalog-deployment#set-a-default-expression-for-accessurl).

## Issues with **Only people with access to this data source** permission

### Unable to choose **Only people with access to this data source**

The **Only people with access to this data source** option might be unavailable if the service account doesn't have read permissions to the required tables. Make sure that the account can read tables related to user criteria permissions.

### User mapping failures

ServiceNow user accounts that don’t have a corresponding Microsoft 365 user in Microsoft Entra ID fail to map. Service accounts and nonuser accounts are expected to fail mapping. You can view mapping failures in the identity stats area of the connection detail window and download logs from the **Error** tab.

## Logout successful window appears when you complete the OAuth process

When you complete the OAuth process, a **Logout successful** window might appear without prompting for ServiceNow credentials.

By default, ServiceNow tries to connect by using Microsoft 365 admin credentials through single sign-on (SSO) from a browser authentication. This default setting can cause the connection to fail. As a result, the **Logout successful** window appears.

:::image type="content" source="media/servicenow-catalog-troubleshooting/logout-successful.png" alt-text="Screenshot of the logout successful window.":::

To resolve this issue:

1.  Open a private browser window and sign in with your ServiceNow credentials.
2.  On a new tab, sign in to the Microsoft 365 admin center. This step allows ServiceNow SSO to sign out and switch credentials.
3.  Try the OAuth configuration again. The following window should appear to authorize the connection.

    :::image type="content" source="media/servicenow-catalog-troubleshooting/oauth-window.png" alt-text="Screenshot of the Oauth configuration window.":::

## Issue with OIDC-based authorization

Customers with tightened security controls on Entra ID might enable the [Assignment required](/entra/identity/enterprise-apps/application-properties#assignment-required) option on the enterprise application registered for OpenID Connect (OIDC). This option results in the following error during the authorization process when you deploy the connector:

`Failed to authenticate using client credentials. Please check the client ID, secret, and scope configuration. If the issue persists, contact your data source administrator or Microsoft Support. Error from the data source while getting the token: Error Description: AADSTS501051: Application '\<AppID\>'(\<App Name\>) is not assigned to a role for the application '\<AppID\>'(\<App Name\>). Trace ID: \<GUID\> Correlation ID: \<GUID\> Timestamp: \<Timestamp\>, Error: invalid_grant.`

To resolve the issue, disable the [Assignment required](/entra/identity/enterprise-apps/application-properties#assignment-required) option on the enterprise application:

1.  In the Microsoft Entra admin center, go to **Enterprise Apps** \> **All apps**.
2.  Select the app registered for OIDC and choose **Properties** \> **Turn off Assignment required** \> **Save**.

## Related content

- [ServiceNow Catalog connector overview](servicenow-catalog-overview.md)
- [ServiceNow Catalog connector deployment guide](servicenow-catalog-deployment.md)
- [Set up the ServiceNow service for connector ingestion](servicenow-catalog-admin-setup.md)
