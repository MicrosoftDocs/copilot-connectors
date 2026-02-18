---
title: "Deploy the GitLab Issues Server Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 01/21/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the GitLab Issues Server Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the GitLab Issues Server Microsoft 365 Copilot connector

The GitLab Issues Server Microsoft 365 Copilot connector integrates GitLab issue data into Microsoft 365. When you deploy this connector, Microsoft 365 Copilot and Microsoft Search can surface relevant GitLab issues directly in apps such as Teams, Outlook, and SharePoint. This article describes the steps to deploy and configure the GitLab Issues Server connector.

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- Confirm your GitLab instance is accessible via API.
- Generate a **client ID** and **client secret** from GitLab for authentication.
- Make sure that the authentication account has access to repositories, issues, merge requests, knowledge files, and wiki pages.
- Make sure that the GitLab OAuth scopes include the following scopes: `read_api`, `read_repository`, `read_user`.
- Make sure that users who access indexed GitLab data have Microsoft Entra ID identities for permission mapping.
- Set the correct redirect URLs during GitLab authentication setup:
  - Microsoft 365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`
  - Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
- For self-managed GitLab instances, make sure that:
  - You have GitLab version 17.7 or later.
  - You have the Microsoft Graph connector agent version 3.1.8.0 or later installed on a server with access to GitLab.
  - The authentication account has administrative privileges for access control list (ACL) crawling.
- For best performance, adjust [GitLab rate limits](https://docs.gitlab.co.jp/ee/user/admin_area/settings/user_and_ip_rate_limits.html#:%7E:text=On%20the%20left%20sidebar%2C%20select%20Settings%20%3E%20Network%2C,period%20per%20IP%20value.%20Defaults%20to%203600.%20Optional.) as recommended:
    - User and IP rate limits: Uncheck **Enable authenticated API request rate limit** and **Enable authenticated web request rate limit**. 
    - Files API rate limits: Uncheck **Enable authenticated API request rate limit**. 
    - Deprecated API rate limits: Uncheck **Enable authenticated API request rate limit**. 
    - Users API rate limits: Set **Max requests per 10 minutes per user** to a high value (for example, 100000). 
    - Groups API and Projects API rate limits: Set all values to 0 to disable limits. 
    - Members API rate limits: Set to 0. 

### Rate-limit recommendations

Use the guidelines in the following table to choose rate-limit settings based on the approximate number of GitLab issues.

| Approximate number of items | Recommended rate‑limit setting | Approximate ingestion time |
|---|---|---|
| Up to 100,000 | 20,000 requests/hour | Hours to one day |
| 100,000 to 1,000,000 | 25,000 requests/hour | Two days to one week |
| 1,000,000 or more | 25,000 requests/hour | 1–2 weeks (varies by environment load) |

## Deploy the connector

To add the GitLab Issues Server connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **GitLab Issues Server**.

### Set display name

The display name identifies references in Copilot responses and helps users recognize the associated content source.  
You can accept the default **GitLab Issues Server** display name or customize it.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

### Set instance URL

Provide the base URL of your GitLab Server instance. The base URL is the URL the connector uses to access issue data through the GitLab REST APIs.

### Choose Graph Connector Agent

Select the Microsoft Graph connector agent that manages GitLab data ingestion into Microsoft 365. For more information, see [Microsoft Graph connector agent](connector-agent.md).

### Choose authentication type

The GitLab Issues Server connector supports **OAuth 2.0**. Enter the GitLab **client ID** and **client secret**, and then choose **Authorize**.

### Roll out

To roll out the connector to a limited audience, choose the toggle next to **Rollout to limited audience** and specify users or groups.  

Choose **Create** to deploy the connection. The GitLab Issues Server connector starts indexing content right away.

To customize the connection, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional)

After you create your connection, you can review its status in **Copilot** > **Connectors** in the Microsoft 365 admin center.

## Customize settings (optional)

You can customize the default values for the GitLab Issues Server connector settings. To customize settings, choose **Custom setup** on the connector page.

### Customize user settings

#### Access permissions

Choose whether indexed data is visible to:

- Only people with access to this data source (default)
- Everyone

If you choose **Only people with access to this data source**, indexed data appears only for authorized users. If you choose **Everyone**, indexed data appears for all users.

#### Map identities

Map GitLab user identities to Microsoft Entra ID. Options include:

- **Email**: Maps GitLab email to Microsoft Entra ID user properties. 
- **Login**: Maps GitLab logins with Microsoft Entra ID user properties. 
- **Name**: Maps GitLab name with Microsoft Entra ID user properties. 

If direct mapping fails, use regular expressions (regex) to transform the data. For example: `[a-zA-Z0-9]+`. For more information, see [Map Microsoft Entra identities](map-entra-id.md). 

### Customize content settings

On the **Data** tab, you can verify property mappings in the sample data for metadata such as content, labels, description, and timestamps. 

#### Content filter

You can configure a time-range filter for the connector. The default setting is 365 days. 

#### Manage properties

You can add or remove available properties from the data source, assign a schema to the property (searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. 

### Customize sync intervals

Configure the **full** and **incremental** crawl sync intervals. The following are the default values:

- Incremental crawl: Every 15 minutes  
- Full crawl: Daily

Adjust the intervals based on your organization's needs.

## Related content

- [GitLab Issues Server connector overview](gitlab-issues-server-overview.md)  
- [Troubleshoot issues with the GitLab Issues Server connector](gitlab-issues-server-troubleshooting.md) 
