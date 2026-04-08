---
title: "Deploy the Bitbucket Knowledge connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 01/27/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the Bitbucket Knowledge Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Bitbucket Knowledge connector

The Bitbucket Knowledge Microsoft 365 Copilot connector integrates documentation files from your Bitbucket repositories into Microsoft 365. This integration allows Copilot, Copilot Search, and Microsoft Search to surface Markdown (.md) and text (.txt) documentation—including runbooks, onboarding guides, architecture notes, and operational workflows—directly within Microsoft 365 apps. This article describes the steps to deploy and customize the Bitbucket Knowledge connector.

## Prerequisites

Before you deploy the Bitbucket Knowledge connector, make sure that you meet the following prerequisites:

- You're a Microsoft 365 admin.
- Your Bitbucket Cloud instance is accessible via API.
- The user account used for authentication has access to the repositories and documentation files to be indexed.
- Users who access indexed Bitbucket content have corresponding **Microsoft Entra ID** identities for permission mapping.
- You set up an OAuth consumer in Bitbucket:

  1. Go to your workspace page on Bitbucket.
  2. Choose the gear icon on the top right and select **Workspace settings**.
  3. Under **Workflows**, select **OAuth consumers**.
  4. Choose **Add consumer**, and provide the redirect URL:
     - Microsoft 365 Enterprise:  
       `https://gcs.office.com/v1.0/admin/oauth/callback`
     - Microsoft 365 Government:  
       `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
  5. Allow the key to have these permissions:
     - Account  
     - Repositories  
     - Pull requests (required by Bitbucket API to access repo metadata)
  6. Save the configuration and copy the key and secret values.

We recommend using a dedicated user account for OAuth authentication for each connection to avoid rate‑limit constraints.

## Deploy the connector

To add the Bitbucket Knowledge connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
2. Choose the **Gallery** tab.
3. From the list of available connectors, choose **Bitbucket Knowledge**.

### Set display name

The display name identifies references in Copilot responses and helps users recognize the associated content source. You can accept the default **Bitbucket Knowledge** display name or customize it so it's familiar to your organization.

For more information, see [Enhance Copilot discovery of connector content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Set instance URL

Enter the URL of your Bitbucket Cloud workspace. For example:

`https://bitbucket.org/<your-workspace>`

### Choose authentication type

To authenticate, choose **OAuth 2.0**:

- Enter your client ID (OAuth consumer key).
- Enter your client secret (OAuth consumer secret).
- Choose **Authorize** to sign in and grant access.
- Choose **Authorize** again when prompted to approve repository-level permissions.

### Roll out

You can optionally roll out the connector to a limited audience before full deployment. To roll out to a limited audience, choose the toggle next to **Rollout to limited audience**, and specify the users and groups. For more information, see [Staged rollout for Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The Bitbucket Knowledge connector starts indexing content immediately.

The following table lists the default values that are set.

| Category | Default value |
|----------|----------------|
| **Users** | Identity mapping uses Bitbucket public names mapped to Microsoft Entra ID. Regex transformations can be used if needed. |
| **Content** | Indexes `.md` and `.txt` files from selected repositories. |
| **Sync** | Incremental crawl runs every **15 minutes**; full crawl runs **daily**. |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Bitbucket Knowledge connector settings. To customize settings, on the connector page, choose **Custom setup**.

### Customize user settings

#### Access permissions

You can control which users can see indexed content:

- **Only people with access to this data source** (default): Content appears only to users who have access in Bitbucket.
- **Everyone**: Indexed content is visible to all users.

#### Map identities

Map Bitbucket user identities to Microsoft Entra ID. You can configure:

- Full name mapping  
- Public name mapping  
- Regex transformation (for example, `{0}@your-domain`)  

### Customize content settings

#### Query string

You can configure the default query string to scope which repositories or folders are indexed. Narrowing folder paths is useful for teams that only want to index specific documentation directories such as `/docs`, `/runbooks`, or `/onboarding`.

#### Manage properties

Verify property mappings in sample data for metadata such as **content**, **label**, and **description**. To test sample data, choose **Preview data**.

### Customize sync intervals

You can configure the sync intervals:

- **Incremental crawl**: The default value is every 15 minutes.
- **Full crawl**: The default value is daily.

For more information, see [Guidelines for crawl settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [Bitbucket Knowledge connector overview](bitbucket-knowledge-overview.md)
- [Troubleshoot issues with the Bitbucket Knowledge connector](bitbucket-knowledge-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)
