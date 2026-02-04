---
title: "Deploy the GitLab Knowledge Server Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 01/26/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the GitLab Knowledge Server Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the GitLab Knowledge Server Microsoft 365 Copilot connector

The GitLab Knowledge Server Microsoft 365 Copilot connector allows your organization to index knowledge content stored in GitLab self-managed (on-premises) instances and make it available in Microsoft 365 Copilot and Microsoft Search experiences. This article describes the steps to deploy and customize the GitLab Knowledge Server connector.

## Prerequisites

Before you deploy the GitLab Knowledge Server connector, make sure that you meet the following prerequisites:

- The GitLab Server (self‑managed) instance is accessible through the GitLab REST API.
- You generated a client ID and client secret in GitLab for OAuth 2.0 authentication.
- The authentication account has access to repositories, wiki pages, and documentation files.
- The OAuth application includes the following scopes: `read_api`, `read_repository`, `read_user`.
- Users who access indexed GitLab knowledge have matching Microsoft Entra ID identities for permission mapping.
- The redirect URL is correctly configured when creating the GitLab OAuth application:
  - **Microsoft 365 Enterprise**: `https://gcs.office.com/v1.0/admin/oauth/callback`
  - **Microsoft 365 Government**: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
- Your GitLab version is 17.7 or later.
- Microsoft Graph connector agent version 3.1.8.0 or later is installed on a server with network access to the GitLab instance.
- API rate limits are configured according to GitLab recommendations for connector performance:
    - User and IP rate limits: Uncheck **Enable authenticated API request rate limit** and **Enable authenticated web request rate limit**. 
    - Files API rate limits: Uncheck **Enable authenticated API request rate limit**. 
    - Deprecated API rate limits: Uncheck **Enable authenticated API request rate limit**. 
    - Users API rate limits: Set **Max requests per 10 minutes per user** to a high value (such as 100000). 
    - Groups API rate limits: Set all values to 0 to disable limits. 
    - Projects API rate limits: Set all values to 0 to disable limits. 
    - Members API rate limits: Set to 0. 

### Rate limit recommendations

Use the guidelines in the following table to choose rate-limit settings based on the approximate number of GitLab knowledge items.

| Approximate number of items | Recommended rate-limit setting | Approximate time to complete ingestion |
|------------------------------|--------------------------------|----------------------------------------|
| Up to 100,000 | Increase rate limit to 9,000 requests/hour | Hours to one day |
| 100,000 to 1,000,000 | Increase rate limit to 15,000 requests/hour | Two days to one week |
| 1,000,000 or more | Increase rate limit to 15,000 requests/hour | 1–2 weeks (varies by environment load) |

## Deploy the connector

To add the GitLab Knowledge Server connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot > Connectors**.
2. Choose the **Gallery** tab.
3. From the list of available connectors, choose **GitLab Knowledge Server**.

### Set display name

The display name identifies references in Copilot responses and helps users recognize the associated content source. You can accept the default **GitLab Knowledge Server** name or customize it for your organization.

### Set instance URL

Specify the base URL of your GitLab Server instance. This URL is the GitLab endpoint that the connector uses to access documentation and repository content through the GitLab REST APIs. Provide the root URL of your self-managed GitLab installation (for example, `https://gitlab.contoso.com`).

### Choose Microsoft Graph connector agent

Select the Microsoft Graph connector agent that manages how GitLab Knowledge data is ingested into Microsoft 365. 

### Choose authentication type

The GitLab Knowledge Server connector supports **OAuth 2.0** authentication. Provide the client ID and client secret from your GitLab application, then select **Authorize**.

For GitLab application setup, make sure that the authentication account has sufficient repository and wiki access for the connector to crawl content.

### Roll out

To roll out the connector to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to deploy the connection to. 

Choose **Create** to deploy the connection. The GitLab Knowledge Server connector begins indexing content immediately.

The following table lists the default values that are set.

| Category | Default value |
|----------|----------------|
| Users | All eligible Microsoft 365 users |
| Content | All supported GitLab knowledge objects (Markdown, wikis, documentation) |
| Sync | Incremental crawl every 15 minutes; full crawl daily |

To customize these values, choose **Custom setup**.

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for GitLab Knowledge Server connector settings. To customize these values, open the connector page in the admin center and choose **Custom setup**.

### Customize user settings

#### Access permissions

Choose whether indexed GitLab knowledge is visible to:

- **Only people with access to this data source** (default)
- **Everyone**

If you choose the default option, indexed content appears only for users with GitLab access permissions. Choosing **Everyone** makes the content visible to all users via your organization’s Microsoft Search and Copilot experiences.

#### Map identities

To ensure that GitLab permissions are honored, map GitLab user identities to Microsoft Entra ID using one of the following:

- **Email**
- **Login**
- **Name**

If direct mapping fails, use regular expressions (regex) to transform the data. For example: `[a-zA-Z0-9]+`. For more information, see [Map Microsoft Entra identities](map-aad.md). 

### Customize content settings

On the **Data** tab, you can verify property mappings in the sample data for metadata such as content, labels, description, and timestamps. 

#### Manage properties

You can add or remove available properties from the data source, assign a schema to the property (searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. 

### Customize sync intervals

The following sync intervals are available:

- **Incremental crawl**: Default is every 15 minutes.
- **Full crawl**: Default is daily.

You can adjust these intervals to meet your organization's needs. For more information, see [Guidelines for sync settings](configure-connector.md#guidelines-for-sync-settings). 

## Related content

- [GitLab Knowledge Server connector overview](gitlab-knowledge-server-overview.md)
- [Troubleshoot issues with the GitLab Knowledge Server connector](gitlab-knowledge-server-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoftsearch/configure-connector)