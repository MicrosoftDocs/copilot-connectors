---
title: "Deploy the Confluence On-premises Microsoft 365 Copilot connector"
description: "Find information about how to deploy the Confluence On-premises Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 02/09/2026
ms.localizationpriority: Medium
---

# Deploy the Confluence On-premises Copilot connector

The Confluence On-premises connector enables Microsoft 365 to index and retrieve content from self-hosted Confluence Data Center or Server instances. It brings enterprise wiki content into Microsoft Search and Copilot, enhancing visibility and usability within the Microsoft 365 ecosystem.

This article describes the steps to deploy, customize, and troubleshoot the Confluence On-premises connector. For general information about Copilot connector deployment, see [Set up Copilot connectors in the Microsoft 365 admin center](deployment-overview.md). 

For advanced Confluence On-premises configuration information, see [Set up the Confluence On-premises service for connector ingestion](confluence-on-premises-admin-setup.md). 

## Prerequisites

Before you deploy the Confluence On-premises connector, make sure that the Confluence environment is configured in your organization. The following table summarizes the steps to configure the Confluence environment and deploy the connector.

| Role | Task |
| ---- | ---- |
| Confluence admin | [Configure the environment]() | 
| Confluence admin/Network admin  | [Set up prerequisites]() |
| Microsoft 365 admin | [Deploy the connector in the Microsoft 365 admin center](#deploy-the-confluence-on-premises-copilot-connector) |
| Microsoft 365 admin | [Customize connector settings](#customize-settings) (optional) |

Before you deploy the connector, make sure that the following prerequisites are met:

- You must be a Microsoft 365 admin.
- Install the [Graph Connector Agent (GCA)](graph-connector-agent.md) on a Windows computer on the same network as the Confluence server.
- Install the Confluence On-prem plugin from the [Atlassian Marketplace](https://marketplace.atlassian.com/apps/1234846?tab=reviews&hosting=datacenter).
- Validate that the [Confluence Mobile Web Plugin](https://marketplace.atlassian.com/apps/1218250/mobile-plugin-for-confluence-data-center?hosting=server&tab=overview) is installed and enabled.
- Ensure authentication credentials are available with Confluence admin permissions.
- Confirm that your Confluence version is 8.0 or higher.

## Deploy the connector

To add the Confluence On-premises connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
2. Choose the **Gallery** tab.
3. From the list of available connectors, choose **Confluence On-premises**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **Confluence On-premises** display name, or customize the value to use a name that users in your organization recognize.

For more information, see [Enhance Copilot discovery with Microsoft 365 Copilot connectors content](enhancing-microsoft-copilot-discovery-with-graph-connector-content.md)

### Set instance URL

To connect to your Confluence site, use your organization's site instance URL. The typical format is:

- `https://<your-company-domain>/confluence`

To find your instance URL:

- In the Confluence Admin Console, go to **General Configuration** > **Server Base URL**.

### Choose authentication type

The connector supports the following authentication methods:

- **Basic authentication**: Use Confluence username and password.
- **OAuth 1.0a**: Generate a public/private key pair and create an application link. For more information, see [OAuth](https://developer.atlassian.com/server/jira/platform/oauth/#step-1--configure-jira).
- **OAuth 2.0 (recommended)**: Register an incoming application link with admin scope.

> [!IMPORTANT]
> Confluence Data Center versions 10.0 and later currently only support the  **Basic authentication** and **OAuth 1.0a** authentication methods.

For OAuth 2.0 setup:

1. Go to **Administration** > **General configuration** > **Application links**.
2. Select **Create link** > **External application** > **Incoming**.
3. Set scope to **Admin**.
4. Use the following redirect URL: `https://gcs.office.com/v1.0/admin/oauth/callback`.

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](/microsoft-365-copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The Confluence On-premises Copilot connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Setting | Default Value |
|----------|----------------|
| Users    | Access permissions | Only people with access to content in the data source. |
| Users    | Map identities | Data source identities are mapped using Microsoft Entra IDs. |
| Content  | Include/exclude space | All spaces included. |
| Content  | Manage properties | For default properties and schemas, see [Manage properties](#customize-content-settings). |
| Sync     | Incremental crawl | Every 15 minutes.
| Sync     | Full crawl | Daily. |

To customize these values, see [Customize settings](#customize-settings).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings

You can customize the default values for the Confluence On-premises connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

The Confluence Cloud connector supports the following user search permissions:

- **Everyone**: Indexed data is visible to all users.
- **Only people with access**: Indexed data is visible only to users with access in Confluence.

In Confluence On-premises, security permissions for users and groups are defined via space permissions and page restrictions. The permission evaluation occurs as follows:

- Retrieve the permission configuration from the page-level restrictions.
- Retrieve the permission configuration from the parent page restrictions.
- Retrieve the permission configuration from the space permissions.
- Compute the intersection of the previous three configurations to determine the effective permission on the page. This final permission set is synchronized to Microsoft 365 Copilot.

> [!IMPORTANT]
> - For Microsoft Graph Connector Agent versions earlier than 3.1.14, anonymous access settings defined at the space level aren't considered.
> - For versions of the Microsoft Graph Connector Agent starting with version 3.1.14, anonymous access settings defined at the space level are considered.

If you choose **Only people with access to this data source**, choose whether your Confluence site has Microsoft Entra ID provisioned users or non-Microsoft Entra ID users:

- **Microsoft Entra ID**: Choose this option if Confluence email IDs match user principal names (UPNs) in Microsoft Entra ID.
- **Non-Microsoft Entra ID**: Choose this option if Confluence email IDs don't match UPNs. Use regex to map email IDs to UPNs.

Updates to permissions are synced only during full crawls.

### Customize content settings

You can customize content settings in the following ways:

- Include or exclude specific spaces by using the space filter option. Each space has a space key identifier that forms part of the URL for that space. For more information, see [Space keys](https://confluence.atlassian.com/doc/space-keys-829076188.html).
- Specify a date range for document indexing. You can Filter pages by **Last Created Date** or **Last Modified Date**.
- Add or remove properties from the data source, assign a schema to properties (searchable, queryable, retrievable, refinable), and change semantic labels associated with properties. The following table lists the default properties.

|Source property|Label|Schema|
|----|----|----|
|Author|authors|Query, Retrieve|
|Content| |Search|
|CreatedByName|Created by|Search, Query, Retrieve|
|CreatedOn|Created date time|Query, Retrieve|
|Id| |Query, Retrieve|
|PageTree| |Retrieve|
|SpaceName| |Search, Query, Retrieve|
|Title|title|Search, Retrieve|
|UpdatedByName|lastModifiedBy|Retrieve|
|UpdatedOn|lastModifiedDateTime|Query, Retrieve, Refine|
|URL|url|Retrieve|

### Customize sync intervals

You can adjust the synchronization frequency:

- **Incremental crawl**: Syncs new and modified content. Incremental crawls don't pick up ACL changes or deleted items. Default is every 15 minutes.
- **Full crawl**: Performs a complete synchronization of all content. Full crawls detect deleted items and sync access control list (ACL) changes. Default is daily.

For more information, see [Guidelines for sync settings](deployment-overview.md#guidelines-for-sync-settings).

## Related content

- [Confluence On-premises connector overview](confluence-onpremises-overview.md)
- [Troubleshoot issues with the Confluence On-premises connector](confluence-onpremises-troubleshooting.md)
