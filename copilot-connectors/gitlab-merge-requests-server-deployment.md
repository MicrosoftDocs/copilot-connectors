---
title: "Deploy the GitLab Merge Requests Server Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 01/22/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the GitLab Merge Requests Server Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the GitLab Merge Requests Server Microsoft 365 Copilot connector

The GitLab Merge Requests Server Microsoft 365 Copilot connector integrates merge request metadata from GitLab Self‑Managed (Server) into Microsoft 365. After deployment, the connector indexes merge request titles, descriptions, labels, statuses, timestamps, authors, assignees, reviewers, milestones, and project context. This indexing enables users to search, summarize, and retrieve merge request insights using Microsoft 365 Copilot, Copilot Search, and Microsoft Search.

This article describes the steps to deploy and customize the GitLab Merge Requests Server connector.

## Prerequisites

Before you deploy the GitLab Merge Requests Server connector, make sure that your organization meets the following prerequisites:

- Confirm that your GitLab Server instance is accessible through the GitLab REST API.
- Generate a **client ID** and **client secret** from GitLab for OAuth 2.0 authentication.
- The authentication user account must have access to repositories, issues, merge requests, knowledge files, and wiki pages.
- The client ID and client secret must include the following scopes:
    - `read_api`
    - `read_repository`
    - `read_user`
- Users who access indexed GitLab data must have corresponding Microsoft Entra ID identities for permission mapping.
- Configure the appropriate redirect URL when creating the GitLab OAuth application:
    - **Microsoft 365 Enterprise:**  `https://gcs.office.com/v1.0/admin/oauth/callback`
    - **Microsoft 365 Government:**  `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
- For self‑managed GitLab environments, make sure that:
    - You have GitLab version 17.7 or later.
    - The Microsoft Graph connector agent version 3.1.8.0 or later is installed on a server that can connect to the GitLab instance.
    - The authentication account must have administrative privileges to enable access control list (ACL) crawling.
- For best performance, adjust [GitLab rate limits](https://docs.gitlab.co.jp/ee/user/admin_area/settings/user_and_ip_rate_limits.html#:%7E:text=On%20the%20left%20sidebar%2C%20select%20Settings%20%3E%20Network%2C,period%20per%20IP%20value.%20Defaults%20to%203600.%20Optional.) as recommended:
    - User and IP rate limits: Uncheck **Enable authenticated API request rate limit** and **Enable authenticated web request rate limit**. 
    - Files API rate limits: Uncheck **Enable authenticated API request rate limit**. 
    - Deprecated API rate limits: Uncheck **Enable authenticated API request rate limit**. 
    - Users API rate limits: Set **Max requests per 10 minutes per user** to a high value (for example, 100000). 
    - Groups API and Projects API rate limits: Set all values to 0 to disable limits. 
    - Members API rate limits: Set to 0. 

### Rate-limit recommendations

Use the guidelines in the following table to choose rate-limit settings based on the approximate number of GitLab merge requests.

| Approximate number of items | Recommended rate-limit setting | Approximate time to complete ingestion |
|------------------------------|--------------------------------|----------------------------------------|
| Up to 100,000 | Use default ratelimit settings (7200/hour) | Hours to 1 day |
| 100,000 to 1,000,000 | Use default ratelimit settings (7200/hour) | 2 days to 1 week |
| 1,000,000 or more | Use default ratelimit settings (7200/hour) | 1–2 weeks (varies by environment load) |

## Deploy the connector

To add the **GitLab Merge Requests Server connector** for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot > Connectors**.
2. Go to the **Connectors** tab and select **Gallery**.
3. From the list of available connectors, select **GitLab Merge Requests Server**.

### Set display name

The display name identifies references in Copilot responses and helps users recognize the associated content source. You can accept the default **GitLab Merge Requests Server** display name or customize it.

For more information about connector display names, see [Enhance Copilot discovery of connector content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Set instance URL

Specify the base URL of your GitLab Server instance. This URL is used by the connector to access merge request data through GitLab’s REST APIs. Use the following format:

`https://<your-gitlab-server>/`

### Choose Graph Connector Agent

Select the Microsoft Graph connector agent your organization uses to ingest GitLab content. The agent must be installed on a computer that can reach your GitLab Server instance.

### Choose authentication type

The GitLab Merge Requests Server connector supports **OAuth 2.0** authentication. Enter your **client ID** and **client secret**, and then choose **Authorize** to complete the OAuth flow.

For information about how to create a GitLab OAuth app, see [Configure GitLab as an OAuth 2.0 authentication identity provider](https://docs.gitlab.com/integration/oauth_provider/).

### Roll out

To roll out the connector to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users or groups. For more information, see [Staged rollout for Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

The GitLab Merge Requests Server connector begins indexing content immediately after deployment.

To customize the connection, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review its status in the **Connectors** section of the Microsoft 365 admin center.

## Customize settings (optional)

You can customize the default values for the GitLab Merge Requests Server connector settings. To customize settings, choose **Custom setup** on the connector page.

### Customize user settings

#### Access permissions

Choose whether indexed data is visible to:

- **Only people with access to this data source** (default)
- **Everyone**

If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to them. If you choose **Everyone**, indexed data appears in the search results for all users. 

#### Map identities

Map GitLab user identities to Microsoft Entra ID. Options include:

- **Email**: Maps GitLab email to Microsoft Entra ID user properties. 
- **Login**: Maps GitLab logins with Microsoft Entra ID user properties. 
- **Name**: Maps GitLab name with Microsoft Entra ID user properties. 

If direct mapping fails, use regular expressions (regex) to transform the data. For example: `[a-zA-Z0-9]+`. For more information, see [Map Microsoft Entra identities](map-entra-id.md). 

### Customize content settings

On the **Data** tab, you can verify property mappings in the sample data for metadata such as content, labels, description, and timestamps. 

#### Query string

You can configure a time‑range filter for the connector. The default setting is **365 days**.

#### Manage properties

You can add or remove available properties from the data source, assign a schema to the property (searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. 

### Customize sync intervals

Configure full and incremental crawl intervals. The default values are:

- **Incremental crawl:** Every 15 minutes  
- **Full crawl:** Daily  

For more information, see [Guidelines for sync settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [GitLab Merge Requests Server connector overview](gitlab-merge-requests-server-overview.md)
- [Troubleshoot issues with the GitLab Merge Requests Server connector](gitlab-merge-requests-server-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)