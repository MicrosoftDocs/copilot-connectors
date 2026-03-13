---
ms.date: 12/02/2025
title: "Set up the Confluence On-premises Service for Connector Ingestion"
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.localizationpriority: Medium
description: "Get the steps that the Confluence admin needs to complete to configure the service for your organization so you can enable the Confluence On-premises Microsoft 365 Copilot connector."
---

# Set up the Confluence on-premises service for connector ingestion

The Confluence On-Premises connector enables Microsoft 365 to index and retrieve content from self-hosted Confluence Data Center or Server instances. It brings enterprise wiki content into Microsoft Search and Copilot, enhancing visibility and usability within the Microsoft 365 ecosystem.

This article provides information about the configuration steps that Confluence admins need to complete in order for your organization to deploy the Confluence On-premises connector for your organization, including configuring the environment and setting up prerequisites for the [Confluence On-premises connector](confluence-onpremises-overview.md).

For information about how to deploy the connector, see [Deploy the Confluence On-premises connector](confluence-onpremises-deployment.md).

## Setup checklist

The following checklists list the steps involved in configuring the environment and setting up the connector prerequisites.

### Configure the environment

| Task | Role |
| ---- | ---- |
| [Identify the instance URL](#configure-the-confluence-environment) | Confluence admin |
| [Review the spaces and pages configuration](#review-the-confluence-spaces-and-pages-configuration) | Confluence admin |
| [Define attribute mapping](#define-confluence-attribute-mapping) | Confluence admin |
| [Configure user access permissions](#configure-user-access-permissions) | Confluence admin |
| [Add descriptions to spaces and pages](#add-descriptions-for-spaces-and-pages) | Confluence admin |
| [Configure servers for high availability](#configure-confluence-servers-for-high-availability) | Confluence admin |
| [Enable JavaScript on the Apache server](#enable-javascript-on-the-apache-server) | Confluence admin |
| [Configure Entra ID sync in Crowd](#configure-entra-id-sync-in-crowd) | Confluence admin |
| [Check API throttling configurations](#check-api-throttling-configurations-to-manage-compute-resources) | Confluence admin |

### Set up prerequisites

| Task | Role |
| ---- | ---- |
| [Create service account](#create-service-account) | Confluence admin |
| [Identify item count for ingestion](#identify-item-count-for-ingestion) | Confluence admin |
| [Provision an OAuth endpoint](#provision-an-oauth-endpoint) | Confluence admin |
| [Add IP address to allow list](#add-ip-address-to-allow-list) | Confluence admin/Network admin |
| [Install the Confluence connector plugin](#install-the-confluence-connector-plugin) | Confluence admin |
| [Validate Copilot indexing](#validate-copilot-indexing-for-confluence) | Confluence admin |

## Configure the Confluence environment

The following sections describe the admin tasks to configure the Confluence environment to enable and optimize the connection.

### Identify the Confluence instance URL

The Confluence On-premises instance URL generally has the following format:

- `https://<your-company-domain>/confluence`

To identify the instance URL for Confluence on-premises:

- In the Confluence admin console, go to **General configuration** > **Server base URL**.

Alternatively, to get the instance URL:

- Open Confluence in your web browser.
- Copy the address from your browser's address bar.
    - If you're viewing the dashboard, the site URL is part of the address that comes before `/index-action` or `/#` (for example, `/#popular`, `/#recently-worked`).
    - If you're viewing a page or blog post, the site URL is the part of the address that comes before `/display` or `/pages`. 

The following are examples of Confluence on-premises site URLs:

- `https://www.myconfluence.com`
- `https://confluence.mycompany.com`
- `https://mycompany.com/confluence`
- `https://myjirasite.com/wiki`
- `https://confluence.mycompany:443`

> [!NOTE]
> If your Confluence URL includes `https://<organization_name>.atlassian.net`, you're using Confluence Cloud, not Confluence On-premises.

### Review the Confluence spaces and pages configuration

To optimize indexing and search results, review the configuration of spaces and pages in both Confluence Cloud and Confluence Data Center. This helps to ensure that search results across Microsoft 365 are complete, secure, and aligned with user expectations.

In Confluence Data Center, verify that the required plugin is installed and that the Microsoft Graph connector agent can access the spaces and pages you want to index. Confirm that permissions, page status (published or draft), and label usage are set to include only relevant content.

### Define Confluence attribute mapping

The default method for mapping your data source identities to Microsoft Entra ID is to determine whether the email address of each Confluence user matches the user principal name (UPN) or email address in Microsoft Entra ID. If this default mapping doesn’t meet your organization's needs, you can define a custom mapping formula.

For more information about mapping identities that aren’t in Microsoft Entra ID, see [Map your non-Azure AD identities](/microsoft-365-copilot/connectors/map-non-entra-id).

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

### Configure Confluence servers for high availability

You can deploy Confluence Data Center in a highly available configuration by using a hardware load balancer. Make sure to record the Confluence web URL and verify that all clients on the internal network can access it.

The Microsoft Graph Connector Agent must be configured to communicate with the load-balanced Confluence web URL, not individual nodes. This ensures consistent access and failover support. Verify that the load-balanced URL is accessible from the internal network where the Graph Connector Agent is hosted.

<!--
The following example shows a clustered deployment that uses a hardware load balancer to distribute traffic across Confluence nodes. The Copilot connector that connects to the Confluence instance must be able to communicate with the hardware load balancer.

[Placeholder for Data Center diagram]
-->
For more information, see [Clustering with Confluence Data Center](https://confluence.atlassian.com/doc/clustering-with-confluence-data-center-790795847.html).

### Enable JavaScript on the Apache server

To ensure that the Confluence consent screen displays correctly, verify the TCP connector configuration for the app's web interface in the `<confluence-install-dir>/conf/server.xml` file.

Open the `<confluence-install-dir>/conf/server.xml` file and add the missing `secure="true"` attribute to the connector associated with Confluence’s base URL, as shown in the following example.

```xml
<Connector port="8090" connectionTimeout="20000" redirectPort="8443"
    maxThreads="48" minSpareThreads="10"
    enableLookups="false" acceptCount="10" debug="0" URIEncoding="UTF-8"
    protocol="org.apache.coyote.http11.Http11NioProtocol"
    scheme="https" secure="true" proxyName="<CONFLUENCE_PROXY_NAME_HERE>" proxyPort="443"
    compression="on" compressibleMimeType="text/html,text/xml,text/plain,text/css,applicat" />
```

### Configure Entra ID sync in Crowd

You can configure Microsoft Entra ID as a directory in Crowd. When you configure Microsoft Entra ID, all changes to your users, groups, and memberships sync between Microsoft Entra ID and Crowd periodically, or whenever you request it. You can view information about your users directly in Crowd by using the User browser and Group browser.

For more information, see [Configuring Microsoft Entra ID](https://confluence.atlassian.com/crowd060/configuring-microsoft-entra-id-1442841864.html).

### Check API throttling configurations to manage compute resources

Copilot connectors throttle requests at a rate of 25 requests per second. If you configured API throttling to limit request volume, this setting can affect the duration of a full crawl.

To reduce the number of requests sent by the connector, you can submit a support request. Be sure to include the following configuration details from your Confluence Data Center server:

- Requests allowed per node
- Maximum requests

## Set up prerequisites

The following sections describe the prerequisite steps to complete before deploying the Confluence connector.

### Create service account

To enable the Confluence connector to update items regularly, configure a service account with read access to specific Confluence knowledge tables.

Make sure the service account has read permissions for the following required tables:
- Spaces

Grant read permissions on all applicable tables. For more information, see [Give users admin permissions](https://support.atlassian.com/user-management/docs/give-users-admin-permissions/).

> [!IMPORTANT]
> Make the service account a Confluence Global Administrator. Confluence Global Administrators have full administrative permissions. To verify the permissions:
> 
> - Go to **Administration** > **General Configuration** > **Global Permissions**.
> - Look for the group **Confluence-administrators**. This group has all permissions enabled: Can Use, Personal Space, Create Space, Confluence Administrator, and System Administrator.
>
> Any user who creates a token must be a member of this group.

> [!NOTE]
> Changes to the service account can affect data synchronization with Microsoft 365. If the account is modified, you might need to reauthenticate the connector in Microsoft 365.

#### OAuth failure due to invalid credentials

If the Microsoft 365 admin isn't also a Confluence On-premises admin, the connection authorization fails with the error "Invalid connection credentials". To resolve this error, the Microsoft 365 admin can follow these steps:

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
    > [!Note]
    > If pasting is disabled, type `allow pasting` in the console first, then paste the command again.
1. A success message appears in the connection creation screen, and the **Create** button becomes active.
1. You can now close the pop-up window.

### Identify item count for ingestion

To verify the expected item count for ingestion across all applicable connectors in your Confluence On-premises instance:

1. Go to **Administration** > **Confluence Administration**.
1. Select **General Configuration**.
1. Choose **System Information**.
1. Search for **Confluence Usage**. This section provides detailed metrics about your Confluence instance.

You can also access the system information directly at: `https://<yoursitename>/confluence/admin/systeminfo.action`.

### Provision an OAuth endpoint

To authenticate and synchronize content from Confluence on-premises, you can choose from three supported methods:

- **OAuth 2.0 (recommended)** - Register an app and configure an incoming link.
- **Basic authentication** - Use your Confluence username and password.
- **OAuth 1.0a** - Generate a public/private key pair and set up an application link in Confluence.

To set up OAuth 2.0 (recommended):

1. Go to **Administration** > **General configuration** > **Application links**.
1. Select **Create link**.
1. Choose **External application**, and then select **Incoming** as the direction.
1. Set the scope to **Admin**.
1. Enter the redirect URL: `https://gcs.office.com/v1.0/admin/oauth/callback`.

### Add IP address to allow list

To ensure that the connector can access Confluence APIs, add the required Microsoft 365 IP addresses to the allow list in your firewall, proxy, or other network configurations.

For Confluence on-premises, make sure that the server hosting your Confluence on-premises instance can reach all required Microsoft 365 URLs and IP addresses. For more information, see [IP Firewall rules](deployment-overview.md#ip-firewall-rules).

### Configure a machine for the connector agent

To connect to Confluence On-premises, deploy a virtual or physical machine for the Microsoft Graph Connector Agent. Make sure the machine can connect to the Confluence load balancer and meets the following hardware and software requirements.

**Supported operating systems**

- Windows 10
- Windows Server 2016 R2 and later

**Required software**

- .NET Framework 4.7.2
- .NET Core Desktop Runtime 8.0 (x64)

**Hardware requirements**

- 8 cores at 3 GHz
- 16 GB RAM
- 40 GB disk space for up to 5 million items
- Additional 7 GB per million items beyond the initial 5 million

**Network requirements**

- Network access to the Confluence data source
- Internet access over port 443

### Install the Confluence connector plugin

To connect Confluence Data Center to the Confluence connector, you must install the Confluence Graph Connector plugin. Because Confluence Data Center is hosted on-premises and doesn’t support native cloud APIs, the plugin is required to enable secure external indexing. The plugin acts as a bridge between the Microsoft Graph Connector Agent and your Confluence instance. It allows the agent to authenticate, access, and extract structured content—including spaces, pages, titles, metadata, and labels—while respecting Confluence's permission model.

Without the plugin, the connector can't query Confluence Data Center content in a permission-aware or structured way. The plugin ensures that Copilot, Copilot Search, and Microsoft Search deliver secure, relevant, and personalized search experiences across Microsoft 365.

To install the plugin:

1. Download the app from [Microsoft Graph Connectors for Confluence On-prem | Atlassian Marketplace](https://marketplace.atlassian.com/apps/1234846/microsoft-graph-connectors-for-confluence-on-prem?tab=overview&hosting=datacenter).
1. Sign in to your Confluence system.
1. Go to **Settings** > **Manage apps**.
1. Choose **Upload app**.
1. Choose the downloaded file and proceed.

> [!NOTE]
> The plugin is supported for Confluence versions later than 8.0.

### Validate Copilot indexing for Confluence

To confirm that Microsoft 365 Copilot can access the required content from Confluence, follow these validation steps:

1. Review whether all required items are synced to Microsoft, based on the prerequisites.
2. Go to the **Connector details** page.
3. Verify that the index count matches the page count in the configured Confluence space.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Confluence On-premises connector](confluence-onpremises-deployment.md)
