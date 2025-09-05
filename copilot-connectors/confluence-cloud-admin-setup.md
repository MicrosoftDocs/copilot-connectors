---
ms.date: 09/05/2025
title: "Set up the Confluence Cloud Service for Connector Ingestion"
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: install-set-up-deploy
ms.service: mssearch
ms.localizationpriority: Medium
description: "Get the steps that the Confluence admin needs to complete to configure the service for your organization so you can enable the Confluence Cloud Microsoft 365 Copilot connector."
---

# Set up the Confluence Cloud service for connector ingestion

The Confluence Cloud Microsoft 365 Copilot connector integrates Confluence content into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface relevant wiki pages, blogs, and attachments directly within apps like Teams, Outlook, and SharePoint.

This article provides information about the configuration steps that Confluence admins need to complete to set up Confluence Cloud for your organization, including configuring the environment and setting up prerequisites for the [Confluence Cloud connector](confluence-cloud-connector-overview.md).

For information about how to deploy the connector, see [Deploy the Confluence Cloud connector](confluence-cloud-connector-deployment.md).

## Setup checklist

The following checklists lists the step involved in configuring the environment and setting up the connector prerequisites.

### Configure the environment

| Task | Role | Status |
| ---- | ------ | ------- |
| [Identify the instance URL](#configure-the-confluence-environment) | Confluence admin |  |
| [Review the spaces and pages configuration](#review-the-confluence-spaces-and-pages-configuration) | Confluence admin |  |
| [Define attribute mapping](#define-confluence-attribute-mapping) | Confluence admin |  |
| [Configure user access permissions](#configure-user-access-permissions) | Confluence admin |  |
| [Add descriptions to spaces and pages](#add-descriptions-for-spaces-and-pages) | Confluence admin |  |
| [Configure Entra ID sync in Crowd](#configure-entra-id-sync-in-crowd) | Confluence admin |  |

### Set up prerequisites

| Task | Role | Status |
| ---- | ------ | ------- |
| [Create service account](#create-service-account) | Confluence admin |  |
| [Identify item count for ingestion](#identify-item-count-for-ingestion) | Confluence admin |  |
| [Set up CQL for advanced search](#set-up-cql-for-advanced-search) | Confluence admin |  |
| [Provision an OAuth endpoint](#provision-an-oauth-endpoint) | Confluence admin |  |
| [Add IP address to allow list](#add-ip-address-to-allow-list) | Confluence admin/Network admin |  |
| [Validate Copilot indexing](#validate-copilot-indexing-for-confluence) | Confluence admin |  |

## Configure the Confluence environment

The following sections describe the admin tasks to configure the Confluence environment to enable and optimize the connection.

### Identify the Confluence instance URL

The Confluence Cloud instance URL generally has the following format:

- `https://<organization_name>.atlassian.net/wiki`

To identify the instance URL for Confluence Cloud:

1. Sign in to your [Confluence](https://admin.atlassian.com) account.
1. Choose **Product URLs**.
1. Under **Default URLs**, locate your site name and product.
 
You can also view the URL in your browser when you're using Confluence Cloud.

### Review the Confluence spaces and pages configuration

To optimize indexing and search results, review the configuration of spaces and pages in both Confluence Cloud and Confluence Data Center. This helps to ensure that search results across Microsoft 365 are complete, secure, and aligned with user expectations.

In Confluence Cloud, make sure spaces follow clear naming conventions, use labels consistently, and apply permissions that match the intended visibility for Copilot, Copilot Search, and Microsoft Search. Organize pages in a logical hierarchy, and use meaningful titles and metadata to improve search accuracy.

### Define Confluence attribute mapping

The default method for mapping your data source identities to Microsoft Entra ID is to determine whether the email address of each Confluence user matches the user principal name (UPN) or email address in Microsoft Entra ID. If this default mapping doesn’t meet your organization's needs, you can define a custom mapping formula.

For more information about mapping identities that aren’t in Microsoft Entra ID, see [Map your non-Azure AD identities](/MicrosoftSearch/map-non-aad).

### Configure user access permissions

Confluence administrators can integrate LDAP directories—such as Microsoft Entra ID—to centrally manage user access and permissions. By syncing LDAP groups into Confluence, administrators can assign those groups to spaces and pages to control view and edit access to align with enterprise-wide identity governance.

You can use synced nested groups to manage access control lists (ACLs), provided the nested group's members are part of a Confluence user group.

The following table provides a comparison of LDAP groups and Confluence native groups for Confluence user access permissions.

| Feature | LDAP groups | Confluence native groups |
| ------- | ----------- | ------------------------ |
| Source | Managed in an external directory | Managed within Confluence |
| Sync | Synced periodically via user directory configuration | Created and maintained manually by Confluence admins |
| Scalability | Highly scalable for enterprise use | Suitable for small teams or Confluence-only setups |
| Access control | Automatically reflects directory changes | Requires manual updates |
| Audit and compliance | Aligned with IT policies and compliance frameworks | Decentralized control |

### Add descriptions for spaces and pages

Copilot uses the descriptions and short descriptions in Confluence to semantically match spaces and pages with user prompts. If descriptions are missing, the relevance of Copilot responses is reduced. Be sure to add descriptions and short descriptions for spaces and pages in your Confluence instance.

### Configure Entra ID sync in Crowd

You can configure Microsoft Entra ID as a directory in Crowd. When you configure Microsoft Entra ID, all changes to your users, groups, and memberships sync between Microsoft Entra ID and Crowd periodically, or whenever you request it. You can view information about your users directly in Crowd by using the User browser and Group browser.

For more information, see [Configuring Microsoft Entra ID](https://confluence.atlassian.com/crowd060/configuring-microsoft-entra-id-1442841864.html).


## Set up connector prerequisites

The following sections describe the prerequisite steps to complete before deploying the Confluence connector.

### Create service account

To enable the Confluence connector to update items regularly, configure a service account with read access to specific Confluence knowledge tables.

Make sure the service account has read permissions for the following required tables:
- Spaces

Grant read permissions on all applicable tables. For more information, see [Give users admin permissions](https://support.atlassian.com/user-management/docs/give-users-admin-permissions/).

> [!NOTE]
> Changes to the service account can affect data synchronization with Microsoft 365. If the account is modified, you might need to reauthenticate the connector in Microsoft 365.

Make sure that the service account is correctly configured. If no page-level restrictions exist, the connector checks space-level permissions and serves content as follows:

- If anonymous access is enabled for a space, its content is visible to all users in your tenant.
- If anonymous access is disabled, space-level permissions are enforced.
- If no space-level permissions are defined, the content isn't visible to any users in your tenant.

> [!NOTE]
> Permissions are managed only at the space and page level. Parent page permissions aren't considered.

#### OAuth failure due to invalid credentials

If the Microsoft 365 admin isn't also a Confluence Cloud admin, the connection authorization fails with the error "Invalid connection credentials". To resolve this error, the Microsoft 365 admin can follow these steps:

1. Open an InPrivate browsing window and sign in to the admin portal using your credentials.
1. In the admin portal, select the Confluence data source and begin creating the connection.
1. For **Authentication**, select OAuth 2.0.
1. Enter the client ID and client secret of the app created by the Confluence admin.
1. Select **Authorize**. A pop-up window opens.
1. Copy the URL from the pop-up and share it with the Confluence admin.
1. Ask the Confluence admin to sign in to their Confluence account and approve the request. After approval, a blank screen appears—this confirms success.
1. After the Confluence admin confirms approval, return to the pop-up window.
1. Right-click the pop-up window and select **Inspect** > **Console**.
1. In the console, paste the following command: `window.opener.postMessage({type: 'oauthFinish', isSuccess: true}, '*')`
    > **Note:** If pasting is disabled, type `allow pasting` in the console first, then paste the command again.
1. A success message appears in the connection creation screen, and the **Create** button becomes active.
1. You can now close the pop-up window.

### Identify item count for ingestion

To verify the expected item count for ingestion across all applicable connectors in Confluence Cloud:

1. Go to `https://<Confluence instance name>.atlassian.net/wiki/admin/space-reports`.
1. Under **Space report**, select **Create report**.
1. Select **Download** to export the report.
1. Open the downloaded .csv file.
1. In the **Content Count** column, review the number of pages that will sync in each space.

> [!Note]
> AI-generated content in the report might be inaccurate. Review the content before proceeding.

To verify the expected item count for ingestion across all applicable connectors in your Confluence On-premises instance:

1. Go to **Administration** > **Confluence Administration**.
1. Select **General Configuration**.
1. Choose **System Information**.
1. Search for **Confluence Usage**. This section provides detailed metrics about your Confluence instance.

You can also access the system information directly at: `https://<yoursitename>/confluence/admin/systeminfo.action`

### Set up CQL for advanced search

To retrieve pages from a specific space in Confluence Cloud that have certain labels and were last modified within a defined timeframe, use Confluence Query Language (CQL).

Include the following components in your query:

- **Space key** - Identifies the space you want to search.
- **Page type** - Filters results to include only pages.
- **Labels** - Filters pages by one or more labels.
- **Last modified date** - Limits results to pages modified within a specific timeframe.

The following example shows a CQL query.

`CQLtype = page AND space = "SPACEKEY" AND label in ("label1", "label2") AND lastmodified >= "2025-01-01"`

In the previous example:

- `type` = page: Returns only pages.
- `space` = "SPACEKEY": Replace "SPACEKEY" with the actual key for your space.
- `label` in ("label1", "label2"): Returns pages with either label1 or label2.
- `lastmodified` >= "2025-01-01": Returns pages modified on or after January 1, 2025.

You can adjust the date format to `yyyy-MM-dd` or `yyyy-MM-dd HH:mm` to include time.

> [!TIP]
> - For label filtering, use label in (...) to match multiple labels.
> - For date functions, CQL supports dynamic functions like `startOfYear()` or `endOfMonth()` to simplify date filtering. For example, `lastmodified >= startOfYear()` returns pages modified since the beginning of the current year.

To run the query using the Confluence Cloud REST API, use the following POST request.

```http
curl -u yourUsername:yourPassword \
     -X POST "https://your-confluence-url/rest/api/search" \
     -H "Content-Type: application/json" \
     -d '{
           "cql": "type=page AND space=\"SPACEKEY\" AND label=\"your-label\" AND lastmodified >= \"2025-01-01\"",
           "limit": 25,
           "start": 0
         }'
```

Replace:

- `yourUsername` and `yourPassword` with your credentials or use token-based authentication.
- `https://your-confluence-url` with your Confluence base URL.
- `SPACEKEY` with your space key.
- `your-label` with the desired label.
- Adjust the date and pagination as needed.

### Provision an OAuth endpoint

To enable the Confluence Cloud connector to access your Confluence Cloud instance, a Confluence administrator must provision an OAuth endpoint to enable the Microsoft Search app and Microsoft 365 Copilot to access the instance.

For detailed instructions, see [Register an app in Confluence Cloud]().

Use the following table to determine which scopes to select when you configure access through the Confluence API.

| Scope name | Code |
| ---------- | ---- |
| View content details<br />View details regarding content and its associated properties. | read:content-details:confluence|
| View audit records<br />View and export audit records for Confluence events. | read:audit-log:confluence |
| View pages<br />View page content. | read:page:confluence |
| View groups<br />View details about groups including its members. | read:group:confluence |
| View user details<br />View user details.  | read:user:confluence |
| View spaces<br />View space details. | read:space:confluence |
| View content summaries<br />View information about the content. Note that this does not provide access to the content itself. | read:content.metadata:confluence |


### Add IP address to allow list

To ensure that the connector can access Confluence APIs, add the required Microsoft 365 IP addresses to the allow list in your firewall, proxy, or other network configurations.

For Confluence Cloud, if your network configuration blocks access to Confluence APIs, make sure the IP addresses listed in the following documentation pages are allowed:

- [IP Firewall rules](configure-connector.md#ip-firewall-rules)
- [IP addresses and domains to allowlist in your corporate firewall](https://support.atlassian.com/security-and-access-policies/docs/specify-ip-addresses-for-product-access/)

### Validate Copilot indexing for Confluence

To confirm that Microsoft 365 Copilot can access the required content from Confluence, follow these validation steps:

1. Review whether all required items are synced to Microsoft, based on the prerequisites.
2. Go to the **Connector details** page.
3. Verify that the index count matches the page count in the configured Confluence space.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Confluence Cloud connector](confluence-cloud-connector-deployment.md)