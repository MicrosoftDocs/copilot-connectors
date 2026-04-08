---
title: "Deploy the Bitbucket Pull Request connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 01/16/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the Bitbucket Pull Request Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Bitbucket Pull Request connector

The Bitbucket Pull Request Microsoft 365 Copilot connector integrates Bitbucket pull request content into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface relevant pull requests and engineering context directly within Microsoft 365. This article describes the steps to deploy and customize the Bitbucket Pull Request connector.

## Prerequisites

Before you deploy the Bitbucket Pull Request connector, make sure that you meet the following prerequisites:

- You're a Microsoft 365 admin.
- Your Bitbucket instance is accessible via API.
- The user account used for authentication has access to the repositories, pull requests, and knowledge files to be indexed.
- Users who access indexed Bitbucket data have corresponding **Microsoft Entra ID** identities for permission mapping.
- Set up an OAuth consumer on Bitbucket:
  1. Go to your workspace page on Bitbucket.
  2. Choose the gear icon on the top right corner and select **Workspace settings**.
  3. On the left pane, under **Workflows**, select **OAuth Consumers**.
  4. Choose **Add consumer** and provide the redirect URL:
    - For Microsoft 365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`
    - For Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
  5. Allow the key to have the following permissions configured to read issues:
    - Account
    - Repositories
    - Pull requests
  6. Save the configuration and copy the key and secret values.

We recommend that you use separate user accounts for OAuth authentication with each connection, as Bitbucket's rate limit is calculated individually per user.

## Deploy the connector

To add the Bitbucket Pull Request connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
2. Choose the **Gallery** tab.
3. From the list of available connectors, choose **Bitbucket Pull Request**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. You can accept the default **Bitbucket Pull Request** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

### Set instance URL

Enter the URL of your Bitbucket instance. For example: `https://bitbucket.org/testinstance`.

### Choose authentication type

To authenticate, choose **OAuth 2.0**:

- Enter your client ID by using the key from your Bitbucket OAuth consumer, and the client secret by using the corresponding OAuth consumer secret.
- Choose **Authorize** to sign in and grant access.
- Choose **Authorize** again to grant the required access permissions.

### Roll out to limited audience

Before you deploy the connector, test the connection with a limited user base in Copilot and Microsoft Search. To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to.

Choose **Create** to deploy the connection. The Bitbucket Pull Request Copilot connector starts indexing content right away.

The following default values are set:

- **User**: Identity mapping uses Bitbucket public names mapped to Microsoft Entra ID properties. If direct mapping fails, use regex transformations.
- **Data**: Indexes pull requests and associated metadata.
- **Crawl**:
  - Incremental crawl runs **every 15 minutes** by default.
  - Full crawl runs **daily** to ensure up-to-date indexing.

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Bitbucket Pull Request connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions
Configure access permissions to make sure that only authorized users can view indexed content. You have the following options:

- **Only people with access to this data source** (default): Indexed data appears only for users who have access to it.
- **Everyone**: Indexed data appears in search results for all users.

#### Map identities
Map Bitbucket user identities to Microsoft Entra ID identities. Options include:

- Full name mapping
- Public name mapping
- Regex transformation (for example, `{0}@<your-domain>`)

### Customize content settings

#### Manage properties
Verify property mappings in sample data for metadata such as **content**, **label**, and **description**. To test sample data, choose **Preview data**.

### Customize sync intervals
You can configure **incremental** and **full** crawls. The following are the default values:

- Incremental crawl: every 15 minutes
- Full crawl: daily

For more information, see [Guidelines for crawl settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [Bitbucket Pull Request connector overview](bitbucket-pull-request-overview.md)
- [Troubleshoot issues with the Bitbucket Pull Request connector](bitbucket-pull-request-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)
