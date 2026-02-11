---
title: "Deploy the GitLab Merge Requests Cloud Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 01/30/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the GitLab Merge Requests Cloud Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the GitLab Merge Requests Cloud Microsoft 365 Copilot connector

The GitLab Merge Requests Cloud Microsoft 365 Copilot connector allows your organization to index merge request data stored in GitLab and make it available across Microsoft 365 Copilot and Microsoft Search experiences.

This article describes the steps to deploy and customize the GitLab Merge Requests Cloud connector.

## Prerequisites

Before you deploy the GitLab Merge Requests Cloud connector, make sure that your GitLab environment and Microsoft 365 environment meet the following prerequisites:

- Your GitLab instance must be accessible via API.
- Generate a **client ID** and **client secret** from GitLab for authentication.
- The authentication user account must have access to repositories, issues, merge requests, knowledge files, and wiki pages.
- The **client ID** and **client secret** must include the following scopes:
  - `read_api`
  - `read_repository`
  - `read_user`
- Users who access the indexed GitLab data must have corresponding **Microsoft Entra ID** identities for permission mapping.
- Make sure you configure appropriate redirect URLs during GitLab authentication setup:
  - **Microsoft 365 Enterprise**: `https://gcs.office.com/v1.0/admin/oauth/callback`
  - **Microsoft 365 Government**: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
- You must be a Microsoft 365 admin to deploy the connector.

## Deploy the connector

To add the GitLab Merge Requests Cloud connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **GitLab Merge Requests Cloud**.

### Set display name

The display name identifies references in Copilot responses to help users recognize the associated content source. You can accept the default **GitLab Merge Requests Cloud** display name or customize it.

### Choose authentication type

The connector supports **OAuth 2.0** authentication with GitLab. To authenticate:

1. Enter your **client ID** and **client secret**.
2. Select **Authorize** to complete the OAuth flow.

For more information, see [Configure GitLab as an OAuth 2.0 authentication identity provider](https://docs.gitlab.com/integration/oauth_provider/).

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to include. For more information, see [Staged rollout for Copilot connectors](/microsoft-365-copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The GitLab Merge Requests Cloud connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|---------------|
| Users | Only people with access to this data source. |
| Content | Default GitLab merge request metadata properties are indexed. |
| Sync | Incremental crawl every 15 minutes; full crawl daily. |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the GitLab Merge Requests Cloud connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

Choose whether indexed data is visible to:

- **Only people with access to this data source** (default)
- **Everyone**

If you choose **Only people with access to this data source**, indexed data appears only for users who have access in GitLab.

#### Map identities

To ensure permissions are applied correctly, map GitLab identities to Microsoft Entra ID. Choose one of the following options:

- **Email** – Maps GitLab emails to Entra ID user properties.
- **Sign in** – Maps GitLab usernames to Entra ID user properties.
- **Name** – Maps GitLab display names to Entra ID user properties.

If direct mapping fails, you can use regular expressions (regex) to transform values. For more information, see [Map Microsoft Entra identities](/microsoft-365-copilot/connectors/map-entra-id).

### Customize content settings

On the **Data** tab, you can verify property mappings in the sample data for metadata such as content, labels, description, and timestamps. 

#### Manage properties

You can add or remove available properties from the data source, assign a schema (searchable, queryable, retrievable, or refinable), change the semantic label, or add an alias.

### Customize sync intervals

Configure the full and incremental crawl sync intervals. The following are the default values:

- **Incremental crawl:** Every 15 minutes.
- **Full crawl:** Daily.

You can adjust these intervals to meet your organization’s needs. For more information, see  
[Guidelines for sync settings](/microsoft-365-copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

The following table lists the rate limits for the GitLab Merge Requests Cloud connector content ingestion.

| Approximate number of items | Approximate time to complete ingestion |
|------------------------------|----------------------------------------|
| Up to 100,000 | Within three hours |
| 100,000 to 1,000,000 | Within one day |
| 1,000,000 or more | One day to one week (varies by environment load) |

## Related content

- [GitLab Merge Requests Cloud connector overview](gitlab-merge-requests-cloud-overview.md)
- [Troubleshoot issues with the GitLab Merge Requests Cloud connector](gitlab-merge-requests-cloud-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365-copilot/connectors/deployment-overview)