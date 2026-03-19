---
ms.date: 03/10/2026
title: "Troubleshoot issues with the ServiceNow Knowledge Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: mayanksethi
audience: Admin 
ms.audience: Admin
ms.topic: article
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Find troubleshooting information for the ServiceNow Knowledge Copilot connector."
---

# Troubleshoot issues with the ServiceNow Knowledge Copilot connector

The ServiceNow Knowledge Microsoft 365 Copilot connector allows organizations to index ServiceNow knowledge articles into Microsoft 365 Copilot and search experiences. This article provides troubleshooting information for common errors that you might encounter when you deploy the ServiceNow Knowledge connector.

To verify ServiceNow configuration information to help troubleshoot errors, see [Set up the ServiceNow service for connector ingestion](/microsoft-365/copilot/connectors/servicenow-knowledge-admin-setup).

## Can't find ServiceNow Knowledge articles in Copilot or Microsoft Search

To troubleshoot this issue:

1. Determine whether the user searching for the article has the [required permissions to access the ServiceNow Knowledge articles.](/microsoft-365/copilot/connectors/servicenow-knowledge-admin-setup#create-service-account-and-set-up-permissions-to-index-items)

1. Determine whether the user is correctly mapped to a Microsoft Entra identity. Mapping issues show as a 2006 error on the **Error** tab. Check the user mapping formula and update as needed.

    :::image type="content" source="media/servicenow-knowledge-troubleshooting/error-tab.png" alt-text="Screenshot of the Error tab showing mapping issues with 2006 error code.":::

1. Determine whether an advanced script in any of the user criteria grant access to the article. Advanced scripts aren't currently supported. If you're using advanced scripts, be sure to select **Advanced flow** when you set up the connection and [Set up the REST API](/microsoft-365/copilot/connectors/servicenow-knowledge-admin-setup#set-up-rest-api).

1. Use the [User criteria diagnostics](https://docs.servicenow.com/bundle/washingtondc-servicenow-platform/page/product/knowledge-management/concept/diagnose-knowledge-user-criteria.html) tool in ServiceNow to see if the service account has access to the item in ServiceNow

1. Use the [Access Analyzer tool in ServiceNow](https://www.servicenow.com/docs/bundle/zurich-platform-security/page/integrate/identity/task/view-permissions-for-a-user.html) to debug further if the service account user  missed access to any particular table, field, or record (for example, the `user_criteria` table). If you find any access control list (ACL) or role that blocks access to a required table, field, or record, provide the required roles and ACLs to the service account.

1. If you can't identify the root cause, contact the [Copilot connector support team](mailto:MicrosoftGraphConnectorsFeedback@service.microsoft.com) and provide the following details:

    - Tenant ID
    - Connection ID
    - Article Sys ID
    - Knowledge base Sys ID
    - For the knowledge base, collect:
        - List of user criteria `sys_id` available in the `kb_uc_can_read_mtom` (Who Can Read Knowledge Base) table
        - List of user criteria `sys_id` available in the `kb_uc_cannot_read_mtom` (Who Can't Read Knowledge Base) table
        - List of user criteria `sys_id` available in the `kb_uc_cannot_contribute_mtom` (Who Can't Contribute To Knowledge Base) table
        - List of user criteria `sys_id` available in the `kb_uc_can_contribute_mtom`
    - For the item `sys_id`, share:
        - List of user criteria `sys_id` in the `can_read_user_criteria` field of the article
        - List of user criteria `sys_id` in the `cannot_read_user_criteria` field of the article

    When the required access is provided in ServiceNow, start a full crawl for the configured ServiceNow connection.

## Missing access to certain tables

Without the right access, the crawler might not index all content and might not grant permissions accurately. You must be a ServiceNow admin to troubleshoot this issue.

Use the following steps to validate table permissions by using REST API Explorer:

1. Impersonate the crawling account you created in your ServiceNow instance.

    Make sure that the account has the following roles: `rest_api_explorer` and `web_service_admin`.

1. Go to **System Web Services** \> **REST** \> **REST API Explorer**.

1. Select one of the tables mentioned in the error message.

    :::image type="content" source="media/servicenow-knowledge-troubleshooting/select-table.png" alt-text="Screenshot of the REST API Explorer showing table selection." lightbox="media/servicenow-knowledge-troubleshooting/select-table.png":::

1.  Set `sysparm_limit` to 10 (to limit results for testing).

    :::image type="content" source="media/servicenow-knowledge-troubleshooting/sysparm-field.png" alt-text="Screenshot of the sysparm_limit field set to 10." lightbox="media/servicenow-knowledge-troubleshooting/sysparm-field.png":::

1.  Choose **Send**.

1.  Review the response:

    - **If you receive a 403 Status Code** and an error message that states that you're not authorized to access the table, see [Grant table access](/microsoft-365/copilot/connectors/granting-table-access-servicenow) to provide table-level access.
    
    - **If you receive a 200 Status Code** but the response body contains empty results (for example, no fields), row access exists but field-level access is missing. To grant field-level access, see [Grant field-level access](/microsoft-365/copilot/connectors/granting-table-access-servicenow#grant-field-level-access).

       :::image type="content" source="media/servicenow-knowledge-troubleshooting/response-body.png" alt-text="Screenshot of the response body showing empty results." lightbox="media/servicenow-knowledge-troubleshooting/response-body.png":::

If you don't see the table name in the dropdown, you might not have access to the table itself.

Alternatively, you can use a browser to verify access:

1.  Open a private browser window.
1.  Enter the following URL (replace placeholders with the right values): `https://<instance-url>/api/now/table/<table_name>?sysparm_limit=10`.
1.  When prompted, sign in by using the credentials of the crawling account.
1.  Review the response. If no response or an error appears, the account doesn't have the necessary access.

When the required access is provided in ServiceNow, start a full crawl for the configured ServiceNow connection.

## Articles without user criteria not appearing in search results

If knowledge articles that have no user criteria applied aren't appearing in Copilot or Microsoft Search results, verify that the service account has read access to the `sys_properties` table in ServiceNow.

The connector reads two system properties to determine how to handle articles without user criteria:

- `glide.knowman.apply_article_read_criteria`
- `glide.knowman.block_access_with_no_user_criteria`

If the service account can't read these properties, the connector defaults to the most restrictive settings, which blocks articles without explicit user criteria from appearing in search results. No error is shown in the admin center when this happens.

To resolve this issue:

 1. Grant the service account read access to the `sys_properties` table. For more information, see [Grant table access to a service account in ServiceNow](/microsoftsearch/granting-table-access-servicenow-knowledge).
 2. After granting access, start a full crawl for the configured ServiceNow connection.

> [!NOTE] 
> This access applies to both Simple and Advanced flows.

## Issue reading all user criteria from ServiceNow

Sometimes content access can be restricted because the service account isn't reading all user criteria. This issue can happen if you use the `gs.getUserId()` or the `gs.getUser()` function within any user criteria. If you use these functions, update the user criteria to remove them. ServiceNow recommends using the `user_id`.

:::image type="content" source="media/servicenow-knowledge-troubleshooting/user-criteria.png" alt-text="Screenshot of user criteria showing the use of gs.getUserId() function." lightbox="media/servicenow-knowledge-troubleshooting/user-criteria.png":::

Also, if you're experiencing performance issues related to the use of the `getAllUserCriteria()` function or are concerned about using a deprecated API, consider using the following alternative script when you [Set up the REST API](/microsoft-365/copilot/connectors/servicenow-knowledge-admin-setup#set-up-rest-api).

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
       userCriteriaGr.addQuery('active', true); // Select active records
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


## Unable to sign in due to single sign-on enabled ServiceNow instance

If your organization uses single sign-on (SSO) to ServiceNow, you might have trouble signing in with the service account. You can bring up a username and password-based authentication by adding *login.do* to the ServiceNow instance URL. For example: `https://<your-organization-domain>.service-now.com./login.do`.

## Can't connect with the ServiceNow instance

A forbidden or unauthorized response in connection status can occur for the following reasons:

- **Incorrect account password:** If you use Basic authentication, the credentials you provided might be incorrect. Check the credentials again.

    If you use OAuth2.0, verify that the account password is correct and wasn't reset. The ServiceNow Knowledge connector uses an access token fetched on behalf of the service account for the crawl. The access token refreshes every 12 hours. You might need to reauthenticate the connection if you change the password.

- **Table access permissions:** Verify that the service account has the required access to the tables, as described in [Create service account and set up permissions to index items](servicenow-knowledge-admin-setup.md#create-service-account-and-set-up-permissions-to-index-items). Verify that the service account has read access to all the tables in the column.

- **The ServiceNow instance is behind a firewall:** The ServiceNow Knowledge connector might not be able to reach your ServiceNow instance if it's behind a network firewall. You must allow access to the connector service. The following table lists the public IP address range for the connector service for each region. Add the IP address to your network allow list.

    | Environment | Region | Range |
    |---|---|---|
    | PROD | North America | 52.250.92.252/30, 52.224.250.216/30 |
    | PROD | Europe | 20.54.41.208/30, 51.105.159.88/30 |
    | PROD | Asia Pacific | 52.139.188.212/30, 20.43.146.44/30 |

## Change the URL of the knowledge article

The ServiceNow Knowledge connector allows you to customize the URL of the knowledge articles as per the needs of your organization. For more information, see [Customize AccessURL property](/microsoft-365/copilot/connectors/servicenow-knowledge-deployment#customize-accessurl-property).

> [!NOTE]
> Currently, you can't edit the URL property for an existing connection. You can only customize the URL when you initially set up the connection. If you have an existing connection, create a new connection and follow the steps to customize the URL.

## Issues with Only people with access to this data source permission

### Unable to choose Only people with access to this data source

The **Only people with access to this data source** option might be unavailable if the service account lacks read permissions to the required tables. Make sure that the account can read tables related to user criteria permissions.

### User mapping failures

ServiceNow user accounts that don't have a corresponding Microsoft 365 user in Microsoft Entra ID fail to map. Service accounts and nonuser accounts are expected to fail mapping. You can view mapping failures in the identity stats area of the connection detail window and download logs from the **Error** tab.

## Logout Successful window appears when you complete the OAuth process

When you complete the OAuth process, a **Logout successful** window might appear without prompting for ServiceNow credentials.

By default, ServiceNow tries to connect by using Microsoft 365 admin credentials through single sign-on (SSO) from a browser authentication. This default setting can cause the connection to fail. As a result, the **Logout successful** window appears.

:::image type="content" source="media/servicenow-knowledge-troubleshooting/logout-successful.png" alt-text="Screenshot of the Logout successful window." lightbox="media/servicenow-knowledge-troubleshooting/logout-successful.png":::

To resolve this issue:

1.  Open a private browser window and sign in with your ServiceNow credentials.
1.  In a new tab, sign in to the Microsoft 365 admin center. This step allows ServiceNow SSO to sign out and switch credentials if needed.
1.  Try the OAuth configuration again. The following window should appear to authorize the connection:

    :::image type="content" source="media/servicenow-knowledge-troubleshooting/oauth-authorization.png" alt-text="Screenshot of the OAuth authorization window." lightbox="media/servicenow-knowledge-troubleshooting/oauth-authorization.png":::

## Issue with OIDC based authorization

Customers with tightened security controls on Entra ID might enable the [Assignment required](/entra/identity/enterprise-apps/application-properties#assignment-required) option on the Enterprise application registered for OpenID Connect (OIDC). This causes the following error during the authorization phase of connector setup:

`Failed to authenticate using client credentials. Please check the client ID, secret, and scope configuration. If the issue persists, contact your data source administrator or Microsoft Support. Error from the data source while getting the token: Error Description: AADSTS501051: Application '\<AppID\>'(\<App Name\>) is not assigned to a role for the application '\<AppID\>'(\<App Name\>). Trace ID: \<GUID\> Correlation ID: \<GUID\> Timestamp: \<Timestamp\>, Error: invalid_grant.`

To resolve this issue, disable the option in Microsoft Entra ID:

1. In the Microsoft Entra admin center, go to **Enterprise Apps** \> **All apps**.
2. Choose the app you registered for OIDC and choose to **Properties** \> **Turn off Assignment required**. \> Save.
3. Choose **Save**.

## Related content

- [ServiceNow Knowledge connector overview](servicenow-knowledge-overview.md)
- [ServiceNow Knowledge connector deployment guide](servicenow-knowledge-deployment.md)
- [Set up the ServiceNow service for connector ingestion](servicenow-knowledge-admin-setup.md)