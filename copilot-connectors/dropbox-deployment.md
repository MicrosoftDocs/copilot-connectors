---
title: "Deploy the Dropbox connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: ang.gao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 12/16/2025
ms.localizationpriority: Medium
description: "Find information about how to deploy the Dropbox Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Dropbox connector

This article describes the steps to deploy and customize the Dropbox connector. For general information about Copilot connector deployment, see [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview).

For Dropbox configuration information, see [Set up the Dropbox service for connector ingestion](dropbox-admin-setup.md).

## Prerequisites

Before you deploy the Dropbox connector, make sure that the Dropbox environment is configured in your organization. The following table summarizes the steps to configure the Dropbox environment and deploy the connector.

| Task | Role |
|------|------|
| [Configure the Dropbox environment](dropbox-admin-setup.md) | Dropbox admin |
| [Deploy the connector](#deploy-the-connector) | Microsoft 365 admin |
| [Customize connector settings](#customize-settings-optional) (optional) | Microsoft 365 admin |

Before you deploy the connector, make sure that you meet the following prerequisites:

- You're a Microsoft 365 admin.
- You have the Dropbox app key and app secret from the Dropbox App Console.
- You verified that required OAuth redirect URLs and API scopes are configured.

## Deploy the connector

To add the Dropbox connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **Dropbox**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **Dropbox** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Choose authentication type

Enter the app key and app secret you obtained from your Dropbox App Console. OAuth 2.0 authentication is required for this connector.

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The Dropbox Copilot connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|---------------|
| Users | All files accessible to anyone in Dropbox are visible to all Microsoft 365 users in your tenant. |
| Content | Files that were last updated within the past three years are indexed by default. |
| Sync | Incremental crawl: Every 4 hours<br>Full crawl: Every day |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Dropbox connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

Choose whether indexed data appears for everyone or only for people with access to the data source. If you select **Only people with access to this data source**, you can map identities using Microsoft Entra ID or non-Entra ID options.

#### Map identities

If Dropbox email IDs match Microsoft Entra ID user principal names (UPNs), select **Microsoft Entra ID**. Otherwise, use the non-Entra ID option and provide a mapping regular expression.

### Customize content settings

#### Content filter 

You can specify what content is crawled:

- **Crawl team folder only:** Crawl files in team folders only. Files stored in team member (private) folders aren't crawled.
- **Time range:** Crawl only files with last modified dates that fall within the selected time range.

#### Manage properties

You can add or remove properties from your Dropbox data source. Assign schema attributes such as **searchable**, **queryable**, **retrievable**, or **refinable**. The following properties are indexed by default.

| Property | Semantic Label | Description | Schema Attributes |
|----------|----------------|-------------|--------------------|
| CreatedBy | Created by | Email address of the creator | Query, Retrieve, Search |
| FileExtension | File extension | File name extension | Query, Refine, Retrieve |
| IconUrl | Icon URL | URL of the icon | Retrieve |
| ItemPath |  | The hierarchical path that identifies the location of an item within its source | Query, Refine, Retrieve, Search |
| ItemType |  | The file extension of the item | Query, Refine, Retrieve, Search |
| LastModifiedBy | Last modified by | Email address of the last modifier | Query, Retrieve, Search |
| LastModifiedTime | Last modified date time | Date and time of last modification | Query, Refine, Retrieve |
| Name | File name | The file name | Query, Retrieve, Search |
| ParentFolderName |  | The name of the file's parent folder | Query, Retrieve, Search |
| PreviewUrl | URL | URL for web preview of the shared file | Retrieve |
| Size | File size | File size in bytes | Query, Retrieve |

### Customize sync intervals

The following sync intervals are configured by default:

- Incremental crawl: Every 4 hours
- Full crawl: Every day

You can adjust these schedules to fit your data refresh needs.

For more information, see [Guidelines for sync settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [Dropbox connector overview](dropbox-overview.md)
- [Troubleshoot issues with the Dropbox connector](dropbox-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)
