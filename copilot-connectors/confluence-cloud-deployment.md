---
ms.date: 01/05/2026
title: "Deploy the Confluence Cloud connector in the Microsoft 365 Admin Center"
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.localizationpriority: Medium
description: "Find information about how to deploy the Confluence Cloud Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Confluence Cloud connector in the Microsoft 365 admin center

The Confluence Cloud Microsoft 365 Copilot connector integrates Confluence content into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface relevant wiki pages and blogs directly within apps like Teams, Outlook, and SharePoint.

This article describes the steps to deploy, customize, and troubleshoot the Confluence Cloud Copilot connector. For general information about Copilot connector deployment, see [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview).

For advanced Confluence Cloud configuration information, see [Set up the Confluence Cloud service for connector ingestion](confluence-cloud-admin-setup.md).

## Prerequisites

Before you deploy the Confluence Cloud connector, make sure that the Confluence environment is configured in your organization. The following table summarizes the steps to configure the Confluence environment and deploy the connector.

| Task | Role |
| ---- | ---- |
| [Configure the environment](confluence-cloud-admin-setup.md#configure-the-confluence-environment) | Confluence admin |
| [Set up prerequisites](confluence-cloud-admin-setup.md#set-up-connector-prerequisites) | Confluence admin/Network admin |
| [Deploy the connector in the Microsoft 365 admin center](#deploy-the-connector) | Microsoft 365 admin |
| [Customize connector settings](#customize-settings-optional) (optional) | Microsoft 365 admin |

To deploy the connector, you must meet the following prerequisites:

- You must be an admin for your organization's Microsoft 365 tenant.
- The service account used to crawl data from Confluence Cloud must have read access to the spaces and pages you want to index.
- You must have authentication credentials with the appropriate access for both Microsoft 365 and Confluence Cloud.
- You must be a Confluence admin, or have an Atlassian account with Confluence admin permissions, to register the OAuth integration in the Atlassian Developer console.

## Deploy the connector

To add the Confluence Cloud connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Connectors** tab, and in the left pane, choose **Gallery**.
1. From the list of available connectors, choose **Confluence Cloud**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **Confluence Cloud** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery with Microsoft 365 Copilot connectors content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Set instance URL

To connect to your Confluence site, use your site URL, which is typically the following: 
`https://<organization_name>.atlassian.net`.

The `<organization_name>` value is the unique identifier for your Confluence Cloud site.

### Choose authentication type

To authenticate and synchronize content from Confluence, choose one of the following authentication types:

- **OAuth 2.0 (recommended)** - This authentication type allows you to authenticate by using a Microsoft managed OAuth 2.0 app.
- **Basic authentication** - To authenticate by using basic auth, enter your username (usually your email address) and API token. To generate an API token, see [Manage API tokens for your Atlassian account](https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/).
- **OAuth 2.0 with customized app** - This authentication type allows you to authenticate by using your own OAuth 2.0 app. Register an OAuth 2.0 app in Confluence Cloud first so that Microsoft Search and Microsoft 365 Copilot can access the instance. For more information, see [Enabling OAuth 2.0 (3LO)](https://developer.atlassian.com/cloud/confluence/oauth-2-3lo-apps/#enabling-oauth-2-0--3lo-).

    To register the app:

    1. Sign in to the [Atlassian Developer console](https://developer.atlassian.com/console/myapps/) with your Atlassian Confluence admin account.
    1. Choose **Create** and select **OAuth 2.0 integration**.
    1. Provide a name for the application and create the new app.
    1. On the left pane, choose **Permissions**, and next to **Confluence API**, choose **Add**.
    1. Choose **Configure** > **Edit scopes**, and select the scopes listed in the following table.

        | Scope name      | Code                              | Description    |
        |----------------|------------------------------------|----------------|
        | View content details                           | read:content-details:confluence  | Crawl content that satisfies the criteria.                                           |
        | View groups                                     | read:group:confluence            | Access group permissions of content.                                     |
        | View user details                               | read:user:confluence             | Access individual user details to support permissions.                   |
        | View audit records                              | read:audit-log:confluence        | Access audit records for Confluence events to support permissions.       |
        | View pages                                      | read:page:confluence             | Access page content details to support permissions.                      |
        | View spaces                                     | read:space:confluence            | Access space details to support permissions.                             |
        | View content restrictions and space permissions | read:permission:confluence            | View content restrictions and space permissions.                             |
        | View content summaries                          | read:content.metadata:confluence | Access information about the content to support permissions.             |
        | View comments | read:comment:confluence       | View comments on pages or blog posts. |
        | View and download content attachments | read:attachment:confluence       | View and download attachments of a page or blog post that you have access to. |

    1. Choose **Save**.
    1. In the left pane, go to **Authorization**. Add the callback URL for Microsoft 365, as follows:
        - Microsoft 365 Enterprise - `https://gcs.office.com/v1.0/admin/oauth/callback`
        - Microsoft 365 Government - `https://gcsgcc.office.com/v1.0/admin/oauth/callback` 
    1. Choose **Save**.
    1. In the left pane, go to **Settings**. Copy the **Client ID** and **Secret**. Complete the connection settings step by using the **Client ID** and **Secret**.

> [!TIP]
> Make sure that the service account has view access to the Confluence content you want to index.

### Roll out

Deploy the connection to a limited set of users to validate it in Copilot and other search surfaces before you roll it out to a broader audience. For more information, see [Staged rollout for Microsoft 365 Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to.

To deploy the connector, choose **Create** in the Microsoft 365 admin center. The Confluence Cloud Copilot connector starts indexing pages from your Confluence account right away.

The following table lists the default values that are set. These values work best with Confluence data.

| Category | Setting | Default value |
|----------|---------|---------------|
| Users | Access permissions | Only people with access to the content in the data source. |
| Users | Map identities |  Data source identities mapped using Microsoft Entra IDs. |
| Content | Include/exclude space | All |
| Content | Manage properties | For default properties and schemas, see [Manage properties](#manage-properties). |
| Sync | Incremental crawl | Frequency: Every 15 minutes |
| Sync | Full crawl | Frequency: Every day |

To customize these values, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Confluence Cloud connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

The Confluence Cloud connector supports the following user search permissions:

- Everyone
- Only people with access to this data source (default)
 
If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, search results respect the same permission setup as the data source.

If you choose **Only people with access to this data source**, you also need to choose whether your Confluence site has Microsoft Entra ID provisioned users or non-Entra ID users:

- Choose the Microsoft Entra ID option if the email ID of Confluence users is same as the user principal name (UPN) in Microsoft Entra ID.
- Choose the non-Entra ID option if the email ID of Confluence users is different from the UPN in Microsoft Entra ID.

> [!NOTE]
> - If you choose Microsoft Entra ID as the identity source, the connector maps user email IDs from Confluence to the UPN property in Microsoft Entra ID.
> - If you choose non-Entra ID as the identity source, provide a regular expression to map email ID to UPN. For more information, see [Map your non-Entra ID identities](map-non-entra-id.md).
> - Updates to users or groups that govern access permissions are synced in full crawls only. Incremental crawls don't currently support processing updates to permissions.

### Customize content settings

You can customize what data is included and excluded and customize the default connector properties.

#### Include or exclude data

By default, the Confluence Cloud connector indexes all blogs and pages. You can include or exclude spaces that you want to index. For advanced scenarios, use a Confluence Query Language (CQL) string to specify conditions for syncing pages. For example, you can choose to index only the pages that were modified in the last two years. For more information, see [Advanced Searching using CQL](https://developer.atlassian.com/server/confluence/advanced-searching-using-cql/).

> [!TIP]
> You can use the CQL filter to index content modified after a certain time by using, for example, `lastModified >= "2024/12/31"`.

Choose **Preview results** to verify the sample values of the selected properties and CQL string.

#### Manage properties

To add or remove available properties from your Confluence Cloud connector, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. The following properties are indexed by default.

| Default property | Label | Description |
| ---------------- | ----- | ----------- |
| Authors | `authors` | The names of all the people who participated or collaborated on the item in the data source. |
| Content | — | The main body content of the item in the data source. |
| CreatedByName | `createdBy` | The person who created the item in the data source. |
| CreatedOn | `createdDateTime` | The date and time that the item was created in the data source. |
| IconUrl | `iconUrl` | URL of the icon. |
| Id | `secondaryId` | The Id of the item in the data source. |
| ItemPath | `itemPath` | Name of the space that the item belongs to in the data source. |
| Labels | — | A set of labels associated with the item to categorize, filter, or group similar items. |
| Likes | `numReactions` | Count of the likes on the item in the data source. |
| PageTree | — | Array of name of items/spaces that the item belongs to in the data source. Last object in array being the immediate parent. |
| SpaceDescription | — | Description of the space that the item belongs to in the data source. |
| SpaceName | `containerName` | Name of the space that the item belongs to in the data source. |
| SpaceURL | `containerUrl` | The direct URL to the container where the item resides, allowing quick access to its location. |
| Status | `state` | The current state of the item in the data source. |
| Title | `title` | The title of the item in the data source. |
| Type | `itemType` | The type or classification of the item in the data source that defines its purpose. |
| UpdatedByName | `lastModifiedBy` | The person who most recently edited the item in the data source. |
| UpdatedOn | `lastModifiedDateTime` | The date and time that the item was last modified in the data source. |
| Url | `url` | The target URL of the item in the data source. |

Choose the **Preview results** button to verify the selected properties and filters.

### Customize sync intervals

The refresh interval determines how often your data synchronizes between the data source and the Confluence Cloud connector index. Copilot connectors use two types of refresh intervals:


- **Full crawl** - Performs a complete synchronization of all content. Full crawls detect deleted items and sync access control list (ACL) changes. By default, full crawls run every 24 hours.
- **Incremental crawl** - Syncs new and modified content. Incremental crawls don't pick up ACL changes or deleted items. By default, incremental crawls run every 15 minutes.

You can change the default values of the refresh intervals. For more information, see [Guidelines for crawl settings](deployment-overview.md#guidelines-for-crawl-settings).

## API endpoints

The following table lists the API endpoints that the connector calls to crawl data and the permissions required for each endpoint.

| Endpoint | OAuth Scope  |
|----------|---------------------------|
| GET /wiki/rest/api/content/search | read:content-details:confluence |
| GET /wiki/rest/api/space | read:space:confluence |
| GET /wiki/rest/api/space/{spaceKey} | read:space:confluence |
| GET /wiki/rest/api/group | read:group:confluence |
| GET /wiki/rest/api/group/{groupId}/membersByGroupId | read:group:confluence, read:user:confluence |
| GET /wiki/rest/api/content/{id}/label | read:content-details:confluence |
| GET /wiki/rest/api/content/{id}/child/attachment | read:content-details:confluence |
| GET /wiki/rest/api/content/{id}/child/attachment/{attId}/download | read:attachment:confluence |
| GET /wiki/rest/api/content/{id}/child/comment | read:content-details:confluence |
| GET /wiki/rest/api/user/bulk | read:user:confluence |
| GET /wiki/api/v2/spaces | read:space:confluence |
| GET /wiki/api/v2/spaces/{id}/permissions | read:space:confluence |
| GET /wiki/api/v2/pages/{id}/inline-comments | read:comment:confluence |
| GET /wiki/api/v2/pages/{id}/footer-comments | read:comment:confluence |
| GET /wiki/api/v2/blogposts/{id}/inline-comments | read:comment:confluence |
| GET /wiki/api/v2/blogposts/{id}/footer-comments | read:comment:confluence |

## Related content

- [Confluence Cloud connector overview](confluence-cloud-overview.md)
- [Set up the Confluence Cloud service for connector ingestion](confluence-cloud-admin-setup.md)
- [Troubleshoot issues with the Confluence Cloud connector](confluence-cloud-troubleshooting.md)
- [Confluence Cloud result layout](confluence-cloud-result-layout.md)
