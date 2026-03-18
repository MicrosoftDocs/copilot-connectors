---
title: "Deploy the GitLab Issues Cloud Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 01/20/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the GitLab Issues Cloud Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the GitLab Issues Cloud Microsoft 365 Copilot connector

The GitLab Issues Cloud connector allows your organization to index issues stored in GitLab and make them available in Microsoft 365 Copilot and Microsoft Search. This article describes the steps to deploy and customize the GitLab Issues Cloud connector.

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- Confirm that your GitLab instance is accessible via the GitLab API.
- Generate a **client ID** and **client secret** from GitLab for authentication.
- Make sure that the authentication account has access to the issues (and their associated projects or repositories) that you want to index.
- Make sure that the client ID and client secret include the following scopes:
  - `read_api`
  - `read_repository`
  - `read_user`
- Users who access indexed GitLab data must have corresponding Microsoft Entra ID identities for permissions mapping.
- Set the appropriate redirect URLs during GitLab authentication setup:
  - **Microsoft 365 Enterprise:** `https://gcs.office.com/v1.0/admin/oauth/callback`
  - **Microsoft 365 Government:** `https://gcsgcc.office.com/v1.0/admin/oauth/callback`

## Deploy the connector

To add the GitLab Issues Cloud connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **GitLab Issues Cloud**.

### Set display name

The display name identifies references in Copilot responses and helps users recognize the associated content source. You can accept the default **GitLab Issues Cloud** display name, or customize it to meet the needs of your organization.  

For more information, see [Enhance Copilot discovery of connector content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Set instance URL

Provide the GitLab instance URL. For GitLab Cloud, this URL is typically:

`https://gitlab.com`

### Choose authentication type

The connector supports **OAuth 2.0** for GitLab.

To authenticate:

- Enter the GitLab client ID and client secret.
- Choose **Authorize**.

For information about how to create OAuth apps in GitLab, see [Configure GitLab as an OAuth 2.0 authentication identity provider](https://docs.gitlab.com/ee/integration/oauth_provider.html).

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups. For more information, see [Staged rollout for Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The GitLab Issues Cloud connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|----------------|
| Users | Only people with access to this data source |
| Content | Time-range filter: 365 days |
| Sync | Incremental crawl: every 15 minutes<br>Full crawl: daily |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com).

## Customize settings (optional)

You can customize the default values for the GitLab Issues Cloud connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

Choose whether indexed data is visible to:

- **Only people with access to this data source** (default)
- **Everyone**

#### Map identities

To ensure permissions are applied correctly, map GitLab user identities to Microsoft Entra ID using:

- **Email:** Maps GitLab email to Microsoft Entra ID user properties. 
- **Login:** Maps GitLab logins with Microsoft Entra ID user properties. 
- **Name:** Maps GitLab name with Microsoft Entra ID user properties. 

If direct mapping fails, use regular expressions (regex) to transform the data. For example: `[a-zA-Z0-9]+`. For more information, see [Map Microsoft Entra identities](map-entra-id.md). 

### Customize content settings

#### Query string

Review or edit the default query string to refine which items are indexed.

#### Manage properties

You can add or remove available properties from the data source, assign a schema to the property (searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. The following table lists properties that the connector indexes by default.

| Property | Semantic label | Description | Schema attributes |
|----------|----------------|-------------|-------------------|
| title | Title | Issue title | Searchable, retrievable |
| description | Body | Issue description | Searchable, retrievable |
| labels | Tags | Issue labels | Queryable, refinable |
| author | Author | Issue author | Searchable, retrievable |
| created_at | Created date | Timestamp for creation | Queryable, retrievable |
| updated_at | Modified date | Timestamp for last update | Queryable, retrievable |

### Customize sync intervals

You can customize the full and incremental crawl intervals. The following are the default values:

- **Incremental crawl:** Every 15 minutes.
- **Full crawl:** Daily.

For more information, see [Guidelines for sync settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

#### Rate limits

The following table lists the rate limits that apply to the GitLab Issues Cloud connector.

| Approximate number of items | Approximate time to complete ingestion |
|------------------------------|----------------------------------------|
| Up to 100,000 | hours to 0.5 day |
| 100,000 to 1,000,000 | 0.5 days to 4 days |
| 1,000,000 or more | 4 days–2 weeks (varies by environment load) |

## Related content

- [GitLab Issues Cloud connector overview](gitlab-issues-cloud-overview.md)
- [Troubleshoot issues with the GitLab Issues Cloud connector](gitlab-issues-cloud-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)
