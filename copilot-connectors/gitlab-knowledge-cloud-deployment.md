---
title: Deploy the GitLab Knowledge Cloud connector
description: Learn how to deploy and configure the GitLab Knowledge Cloud Microsoft 365 Copilot connector, including prerequisites, required permissions, and steps to connect your GitLab environment.
author: Lauragra
ms.author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.reviewer: raynezou
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 01/23/2026
ms.localizationpriority: Medium
---

# Deploy the GitLab Knowledge Cloud connector

The GitLab Knowledge Cloud Microsoft 365 Copilot connector enables your organization to index documentation, wikis, and knowledge artifacts stored in GitLab to make it available in Microsoft 365 Copilot and Microsoft Search experiences. This article describes the steps to deploy and customize the GitLab Knowledge Cloud connector.

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be a Microsoft 365 admin.
- Confirm that your GitLab instance is accessible via API.
- Generate a **client ID** and **client secret** from GitLab.
- Make sure that the authentication account has access to repositories, wikis, runbooks, documentation, and knowledge files.
- The client ID and client secret must include the following scopes:
  - `read_api`
  - `read_repository`
  - `read_user`
- Users who access indexed GitLab data must have corresponding Microsoft Entra ID identities for permission mapping.
- Set the appropriate redirect URLs during GitLab authentication setup:
  - **Microsoft 365 Enterprise:** `https://gcs.office.com/v1.0/admin/oauth/callback`
  - **Microsoft 365 Government:** `https://gcsgcc.office.com/v1.0/admin/oauth/callback`

## Deploy the connector

To add the GitLab Knowledge Cloud connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **GitLab Knowledge Cloud**.

### Set display name

The display name identifies references in Copilot responses and helps users recognize the content source. You can accept the default **GitLab Knowledge Cloud** display name, or customize it.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

### Choose authentication type

The GitLab Knowledge Cloud connector supports **OAuth 2.0** authentication. Choose **OAuth 2.0**, enter your **client ID** and **client secret**, and choose **Authorize**.

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The GitLab Knowledge Cloud connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|---------|---------------|
| Users | Only people with access to this data source |
| Content | Last 365 days of content indexed |
| Sync | Incremental: 15 minutes; Full: daily |

To customize these values, choose **Custom setup**.

After you create your connection, you can review the status in the **Connectors** section of the Microsoft 365 admin center.

## Customize settings (optional)

You can customize the default values for the GitLab Knowledge Cloud connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

Choose one of the following options:

- **Only people with access to this data source** (default)
- **Everyone**

If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to them. If you choose **Everyone**, indexed data appears in the search results for all users. 

#### Map identities

To ensure that permissions are applied correctly, map GitLab user identities to Microsoft Entra ID. Choose one of the following options for mapping: 

- **Email:** Maps GitLab email to Microsoft Entra ID user properties. 
- **Login:** Maps GitLab logins with Microsoft Entra ID user properties. 
- **Name:** Maps GitLab name with Microsoft Entra ID user properties. 

If direct mapping fails, use regular expressions (regex) to transform the data. For example: `[a-zA-Z0-9]+`. For more information, see [Map Microsoft Entra identities](map-entra-id.md). 

### Customize content settings

On the **Data** tab, you can verify property mappings in the sample data for metadata such as content, labels, description, and timestamps. 

#### Content filter

You can configure a time-range filter for the connector. The default setting is 365 days. 

#### Manage properties

You can add or remove available properties from the data source, assign a schema to the property (searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. 

### Customize sync intervals

Configure sync intervals for full and incremental crawls:

- **Incremental crawl:** Default is every 15 minutes.  
- **Full crawl:** Default is daily.  

You can adjust these intervals to meet your organization's needs. For more information, see [Guidelines for sync settings](deployment-overview.md#guidelines-for-crawl-settings).

The following table lists the rate limits for GitLab Knowledge Cloud connector content ingestion.

| Approximate number of items | Approximate time to complete ingestion |
|------------------------------|----------------------------------------|
| Up to 100,000 | Within 6 hours |
| 100,000 to 1,000,000 | 6 hours to 3 days |
| 1,000,000 or more | 3 days–2 weeks (varies by environment load) |

## Related content

- [GitLab Knowledge Cloud connector overview](gitlab-knowledge-cloud-overview.md)
- [Troubleshoot issues with the GitLab Knowledge Cloud connector](gitlab-knowledge-cloud-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)
