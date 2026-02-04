---
title: "Deploy the Adobe Experience Manager Sites Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: rantang
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 12/10/2025
ms.localizationpriority: Medium
description: "Find information about how to deploy the Adobe Experience Manager (AEM) Sites Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Adobe Experience Manager Sites Microsoft 365 Copilot connector

With the Adobe Experience Manager Sites Microsoft 365 Copilot connector, your organization can index published webpages from Adobe Experience Manager (AEM) Sites so people can discover and use them across Microsoft 365 Copilot and Microsoft Search. This article describes the steps to deploy and customize the Adobe Experience Manager Sites connector. 

## Prerequisites

Before you deploy the connector, make sure that:

- You're a Microsoft 365 search admin for your organization.
- You have your Adobe Experience Cloud instance author environment URL and publish environment URL:  
  - Author URL format: `https://author-p<PROGRAM_ID>-e<ENVIRONMENT_ID>.<REGION>.adobeaemcloud.com`  
  - Publish URL format: `https://publish-p<PROGRAM_ID>-e<ENVIRONMENT_ID>.<REGION>.adobeaemcloud.com`
- You have an Adobe Experience Manager Sites technical account with credentials to access published webpages and metadata. This secure, service-based account enables the connector to refresh content regularly. For more information, see [Generate access tokens for server-side APIs](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#generate-a-jwt-token-and-exchange-it-for-an-access-token).

## Deploy the connector

To add the Adobe Experience Manager Sites connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
2. Go to the **Connectors** tab, and in the left pane, choose **Gallery**.
3. From the list of available connectors, choose **Adobe Experience Manager (AEM) Sites**.

### Set display name

The display name identifies references in Copilot responses and acts as a trusted content source filter. You can accept the default name or customize it to something users recognize.

### Set instance URLs

Provide both the author and publish environment URLs for your Adobe Experience Cloud instance.

### Choose authentication type

The connector supports **technical account authentication** for Adobe Experience Cloud. Configure the technical account as described in [Generate access tokens for server-side APIs](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#generate-a-jwt-token-and-exchange-it-for-an-access-token).

### Roll out

To validate the connector before deployment, use a staged rollout. To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](/microsoft-365-copilot/connectors/staged-rollout-for-graph-connectors).

Choose **Create** to deploy the connection. The connector starts indexing published webpages immediately.

The following table lists the default values that are set.

| Category | Settings            | Default values |
|----------|----------------------|----------------|
| Users    | Access permissions   | All published webpages indexed using the AEM Sites connector are visible to all Microsoft 365 users in your tenant. |
| Content  | Index content        | All published pages are selected by default. |
| Content  | Manage properties    | Default schema settings apply to properties such as Title, Description, Navigation Title, Tags, Link, and timestamps. |
| Sync     | Incremental crawl    | Every 15 minutes |
| Sync     | Full crawl           | Every day |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review its status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Adobe Experience Manager Sites connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**. 

### Customize user settings

#### Access permissions

Currently, only published websites from your AEM Sites are indexed. All data indexed using the Adobe Experience Manager Sites connector is visible to all Microsoft 365 users in your tenant, from Microsoft Search or Copilot.

#### User identity mapping 

The connector maps Adobe Experience Cloud user accounts to Microsoft 365 (Microsoft Entra ID) identities. If Adobe Experience Cloud users' emails match their Entra ID user principal names (UPNs), this mapping is automatic. If they differ, you can provide a mapping rule to map identities in Adobe Experience Cloud to identities in Microsoft 365. Mapping rules ensure that the system provides appropriate activity signal to Adobe Experience Cloud content in responses.

### Customize content settings 

#### Content ingestion filters  

Content ingestion filters allow you to control which assets are indexed by defining inclusion and exclusion rules based on paths and metadata properties.

You can choose to include or exclude certain content paths.

**Content paths that should be fetched**
Only exact paths are supported. A valid content path must contain at least two levels, with `/content` as the root path.

**Content paths that should not be fetched**
Only support input Java regular expression for paths. Excluded paths take priority over included paths.

#### Manage properties

To check available standard properties from your Adobe Experience Manager Sites, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. The following standard properties are indexed by default.

| **Default property** | **Semantic label** | **Description** |
|----------------------|--------------------|-----------------|
| Contributors | Authors | The individuals who created or last modified the item. |
| CreatedBy | Created by | Date and time that the item was created in the data source. |
| CreatedTime | Created date time | Date and time that the item was created in the data source. |
| Description | Description | A brief summary of the page's content. |
| HtmlContent | Content | The content of static webpages, not available for dynamic webpages. |
| IconURL | IconUrl | URL of the icon. |
| ItemPath | ItemPath | The path of the item in the data source represented by `/` separated values. Holds the display value of each level in the hierarchy separated by `/`. |
| LastModifiedBy | Last modified by | Name of the person who most recently edited the item in the data source. |
| Link | URL | The target URL of the item in the data source. |
| ModifiedTime | Last modified date time | Date and time the item was last modified in the data source. |
| Nav Title | None | Navigation title is the title displayed in site navigation menus. |
| PageTitle | Title | The page title of the webpages. |
| PublishedBy | None | Name of the person who published the item in the data source. |
| PublishedTime | None | Date and time the item was published in the data source. |
| Subtitle | None | The subtitle of the items. |
| Title | None | The title of the items. |
| Type | ItemType | Usually pages for Adobe Experience Manager Sites. |
| Tags | Tags | Tags defined in AEM Sites metadata. In AEM, tags are organized hierarchically. |

### Customize sync intervals 

The refresh interval determines how often your data is synchronized between the data source and the Adobe Experience Manager Sites connector index. Copilot connectors use two types of refresh intervals: 

- Full crawl: Default value is every day.
- Incremental crawl: Default value is every 15 minutes.

For more information, see [Guidelines for sync settings](/microsoft-365-copilot/connectors/deployment-overview#guidelines-for-sync-settings).

## Related content

- [Adobe Experience Manager (AEM) Sites connector overview](adobe-experience-manager-sites-overview.md)
- [Troubleshoot issues with the Adobe Experience Manager (AEM) Sites connector](adobe-experience-manager-sites-troubleshooting.md)
