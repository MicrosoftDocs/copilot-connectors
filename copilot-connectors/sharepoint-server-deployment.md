---
ms.date: 03/30/2026
title: "Deploy the SharePoint Server connector in the Microsoft 365 admin center"
ms.author: misvenso
author: antarikshp
manager: harshkum
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Find information about how to deploy the SharePoint Server Microsoft 365 Copilot connector in the Microsoft 365 admin center."
---

# Deploy the SharePoint Server connector in the Microsoft 365 admin center

This article describes how to deploy and customize the SharePoint Server Copilot connector in the Microsoft 365 admin center. For general deployment information, see [Set up Copilot connectors in the Microsoft 365 admin center](deployment-overview.md).

If you haven't completed environment setup yet, start with [Set up the SharePoint Server service for connector ingestion](sharepoint-server-admin-setup.md) before proceeding.

The connector setup has two phases:

- **Default setup** (required) — The initial creation screen where you provide a display name, SharePoint instance URL, connector agent, authentication credentials, and site collections. These fields must be filled in to create the connection.
- **Custom setup** (optional) — Available during creation or when editing an existing connection. Lets you configure access permissions, content exclusions, properties, and sync schedules. All settings are pre-configured with defaults that work for most deployments.

> [!NOTE]
> If you edit an existing connection later, it always opens in the custom setup view.

## Prerequisites

Before you deploy the SharePoint Server connector, make sure the following prerequisites are met. The following table summarizes the steps to configure the environment and deploy the connector.

| Task | Role |
| ---- | ---- |
| [Install the Microsoft Graph connector agent](sharepoint-server-admin-setup.md#install-the-microsoft-graph-connector-agent) | SharePoint admin |
| [Configure authentication](sharepoint-server-admin-setup.md#configure-authentication) | SharePoint admin |
| [Deploy the connector in the Microsoft 365 admin center](#deploy-the-connector) | Microsoft 365 admin |
| [Customize connector settings](#customize-settings-optional) (optional) | Microsoft 365 admin |

To deploy the connector, you must meet the following prerequisites:

- The account used for indexing must have full control access to the SharePoint web applications, or be a farm admin.
- You must install and register the [Microsoft Graph connector agent](connector-agent.md) on a server with access to the SharePoint on-premises farm.
- If using Microsoft Entra ID OIDC authentication, complete all the steps in [Set up the SharePoint Server service for connector ingestion](sharepoint-server-admin-setup.md) before proceeding.

## Deploy the connector

To add the SharePoint Server Copilot connector for your organization, [add the SharePoint Server Copilot connector](https://admin.microsoft.com/adminportal/home#/microsoft-365/copilot/connectors/Connectors/add) in the Microsoft 365 admin center.

[![Screenshot that shows connection creation screen for Microsoft 365 Copilot connector for SharePoint Server.](media/sharepoint-server/firstscreen.png)](media/sharepoint-server/firstscreen.png#lightbox)

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter. A default value is present for this field, but you can customize it to a name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery with Microsoft 365 Copilot connectors content](enhance-copilot-discovery.md).

### Set SharePoint instance URL

Enter the URL for the SharePoint site or site collection in the format `https://{domain}/sites/{site-name}`. The connector identifies the site URL and lists all site collections present in that web application. Admins can choose from these site collections to index the content.

### Select Graph Connector Agent

Select from the list of available Graph Connector Agents registered to your tenant.

### Choose authentication type

Choose the authentication type from the drop-down menu of options. The supported options are:

- **Basic** - Not recommended. Included for compatibility with legacy systems.
- **Windows (NTLM)** - Use Domain\username format in the **Username** field. Only NTLM is currently supported; Kerberos is not supported.
- **Microsoft Entra ID OIDC** - Requires additional configuration. See [Set up the SharePoint Server service for connector ingestion](sharepoint-server-admin-setup.md) before using this option.

> [!NOTE]
> At a minimum, the account used for authentication must have **Full Read** permission at the Web Application level in SharePoint, regardless of the authentication type selected. Active Directory Federation Services (ADFS) authentication is not supported.

To authenticate with the provided credentials, select **Sign-in** to load the list of available site collections.

### Select site collections

Select which site collections you want to index. The site collections belong to the web application within the SharePoint URL provided. This list can be long based on the number of site collections available in the data source.

[![Screenshot that shows site collections available for the account.](media/sharepoint-server/siteselection.png)](media/sharepoint-server/siteselection.png#lightbox)

### Roll out

At this point, you're ready to create the connection for SharePoint. You can select **Create** to publish your connection and index the selected content.

The following table lists the default values that are set.

| Category | Setting | Default value |
|----------|---------|---------------|
| Users | Access permissions | Only people with access to the content in the data source. |
| Sync | Incremental crawl | Frequency: Every 15 minutes |
| Sync | Full crawl | Frequency: Every day |

To customize these values, see [Customize settings](#customize-settings-optional).

### Review connection status

Once the connection creation is successful, it starts indexing (syncing) the content. At this time, admins are asked to provide a description for the connection. The description helps Copilot discover the connection content better. The better the connection description for the intended content usage, the better Copilot's responses. The description is also useful for users to select the right connection for their Declarative Agents.

[![Screenshot that shows success screen.](media/sharepoint-server/successscreen.png)](media/sharepoint-server/successscreen.png#lightbox)

## Customize settings (optional)

You can customize the default values for the SharePoint Server connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

[![Screenshot that shows custom set up window.](media/sharepoint-server/customsetup.png)](media/sharepoint-server/customsetup.png#lightbox)

### Customize user settings

The SharePoint Server connector supports the following user search permissions:

- **Only people with access to the content in the data source (default)** – Indexed data appears in the search results and is visible only to users who have permission to view it in SharePoint.
- **Everyone** – The connection is open to everyone, and any user in your organization can see the content.

The connector honors the data source permissions. The SharePoint on-premises connector supports the existing Access Control List (ACL) on given items. Microsoft 365 experiences understand and honor Entra ID permissions. To support Access Control Lists on items, Active Directory identities and Entra ID identities must be synced.

> [!NOTE]
> Copilot connectors support Users, Security Groups, and Distribution Lists. However, SharePoint Server does not support Distribution Lists as Access Control Lists. If there are nested distribution lists, members of those distribution lists may also get access to content through Graph connectors.

[![Screenshot that shows users tab](media/sharepoint-server/userstabsp.png)](media/sharepoint-server/userstabsp.png#lightbox)

### Customize content settings

#### Exclude sites from indexing

Add the URLs of the sites you want to exclude from indexing. Exclusion rules work at the site or subsite level only. Don't add URLs to site contents like libraries or documents, as those exclusions are not honored. You can use the wildcard `*` at the end of a URL to exclude all contents of sites and subsites that begin with that URL.

If the URL ends with `/*`, then all URLs prefixed with the entered URL are excluded from indexing. For example, `abc.com/private/*` excludes `abc.com/private/terms.html` and all content inside `/private`. However, if you provide `abc.com/private/terms.html` as the URL to exclude, it is not honored because exclusion rules work only at the site or subsite level.

[![Screenshot that shows exclusion rules.](media/sharepoint-server/exclusionrulessp.png)](media/sharepoint-server/exclusionrulessp.png#lightbox)

#### Manage properties

Properties define what data is available for searching, querying, retrieving, and refining. From this setting, you can add or remove data source properties, assign a schema to a property (searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias. The following properties are indexed by default.

> [!TIP]
> For most deployments, the default properties are sufficient. Add custom properties only if your organization needs to search or filter on specific SharePoint columns.

| Source property | Label | Description | Schema |
|---|---|---|---|
| Content | | Content of the item | Search |
| CreatedBy | Created by | The owner who created the item | Query, Retrieve, Search |
| CreatedByUpn | | The User Principal Name (UPN) of the owner who created the item | Query, Retrieve, Search |
| CreatedTime | Created date time | Date and time that the item was created in the data source | Query, Retrieve |
| DocumentType | | The type of document | Retrieve |
| IcnUrl | IconUrl | Icon URL for the item type | Retrieve |
| LastAccessed | | Date and time that the item was last accessed | Query, Retrieve |
| LastModified | Last modified date time | Date and time that the item was last modified | Query, Retrieve |
| LastModifiedBy | Created by | The user who modified the item | Query, Retrieve |
| LastModifiedByUpn | | The User Principal Name (UPN) of the user who modified the item | Retrieve, Search |
| Name | Title | The title of the item that you want to show in Copilot and other search experiences | Query, Retrieve, Search |
| ObjectType | | The type of object as returned from the data source | Query, Retrieve, Search |
| Url | | Item URL | Retrieve |

You can add custom properties defined in your sites to better manage the search or Copilot outcomes for your users. To add a custom property, select **Add property** and specify the exact string from the data source. Define a property name and data type (String, StringCollection, DateTime, Boolean, Int64, or Double). Custom properties match the custom columns in SharePoint.

> [!IMPORTANT]
> Property names must match the column names in SharePoint exactly. The connector silently ignores any property name that doesn't match an existing column during crawling. Double-check spelling before saving.

> [!NOTE]
> A total of 128 properties are supported. If you are selecting multiple site collections in a single connection, only default properties are supported. If you want to support custom properties defined in a site, create a different connection and add custom properties for that site.

### Customize sync intervals

The refresh interval determines how often your data synchronizes between the data source and the SharePoint Server connector index. Copilot connectors use two types of refresh intervals:

- **Full crawl** - Frequency: Every day.
- **Incremental crawl** - Frequency: Every 15 minutes.

You can change the default values of the refresh intervals. For more information, see [Guidelines for crawl settings](deployment-overview.md#guidelines-for-crawl-settings).

## Set up search result page

After creating the connection, you need to customize the search results page with verticals and result types. To learn about customizing search results, review how to [manage verticals](/microsoftsearch/manage-verticals) and [result types](/microsoftsearch/manage-result-types).

## Next step

> [!div class="nextstepaction"]
> [Troubleshoot issues with the SharePoint Server connector](sharepoint-server-troubleshooting.md)

## Related content

- [SharePoint Server connector overview](sharepoint-server-overview.md)
- [Set up the SharePoint Server service for connector ingestion](sharepoint-server-admin-setup.md)
- [Troubleshoot issues with the SharePoint Server connector](sharepoint-server-troubleshooting.md)
