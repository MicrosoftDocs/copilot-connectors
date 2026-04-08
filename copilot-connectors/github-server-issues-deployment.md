---
title: "Deploy the GitHub Server Issues connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 12/15/2025
ms.localizationpriority: Medium
description: "Find information about how to deploy the GitHub Server Issues Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the GitHub Server Issues connector

The GitHub Server Issues Microsoft 365 Copilot connector integrates GitHub issue data into Microsoft 365. This article describes the steps to deploy and customize the GitHub Server Issues connector. 

For advanced GitHub configuration information, see [Set up the GitHub service for connector ingestion](github-server-issues-admin-setup.md).

## Prerequisites

Before you deploy the GitHub Server Issues connector, make sure that the GitHub environment is configured in your organization. The following table summarizes the steps to configure the GitHub environment and deploy the connector:

| Task                                      | Role                     |
|-------------------------------------------|--------------------------|
| [Configure the environment](github-server-issues-admin-setup.md) | GitHub admin            |
| [Deploy the connector in the Microsoft 365 admin center](#deploy-the-connector) | Microsoft 365 admin     |
| [Customize connector settings](#customize-settings-optional) (optional) | Microsoft 365 admin     |

Before you deploy the connector, make sure that you meet the following prerequisites:
- You're a Microsoft 365 admin.
- Your GitHub Enterprise Server instance is accessible via API.
- A GitHub app is created and installed for authentication.
- The Microsoft Graph Connector Agent is installed on a device with access to the GitHub instance (version 3.1.11.0 or later).
- Users who access indexed GitHub data have corresponding Microsoft Entra ID identities for permission mapping.

## Deploy the connector

To add the GitHub Server Issues connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
2. Choose the **Gallery** tab.
3. From the list of available connectors, choose **GitHub Server Issues**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. You can accept the default **GitHub Server Issues** display name or customize the value to use a display name that users in your organization recognize.

For more information, see [Enhance Copilot discovery of connector content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Set instance URL

Enter the instance URL of your GitHub Enterprise Server. This URL is the root domain of your internal GitHub server. For example: `https://github.<your-domain>.com`

### Choose authentication type

The connector supports the following authentication types:

- **GitHub app (on behalf of user)**: Recommended for most scenarios. Enter your client ID and client secret from the GitHub app and authorize access.
- **GitHub app (installation)**: Use a private key generated from your GitHub app. Enter the client ID and organization name, and upload the private key. Note that this authentication type is currently in preview. To use this authentication type, contact Microsoft support.

For information about how to create a GitHub app, see [Use a custom GitHub app for authentication](github-server-issues-admin-setup.md#use-a-custom-github-app-for-authentication).

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The GitHub Server Issues Copilot connector starts indexing content right away.

The following table lists the default values that are set when you deploy the connector.

| Category | Default value |
|----------|---------------|
| Users    | Identity mapping based on GitHub email, sign in, or name |
| Content  | Time-range filter set to 365 days |
| Sync     | Incremental crawl every 15 minutes; full crawl daily |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the GitHub Server Issues connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions
Configure access permissions to ensure that only authorized users can view GitHub issues in Copilot and Microsoft Search.

#### Mapping identities
To ensure that permissions are applied correctly, map GitHub user identities to Microsoft Entra ID. Choose one of the following options for mapping:

  - **Email:** Maps GitHub email to Microsoft Entra ID user properties.
  - **Login:** Maps GitHub logins with Microsoft Entra ID user properties.
  - **Name:** Maps GitHub name with Microsoft Entra ID user properties.

If direct mapping fails, use regular expressions (regex) to transform the data. For example: `[a-zA-Z0-9]+`. For more information, see [Map Microsoft Entra identities](/microsoft-365/copilot/connectors/map-entra-id).

If the organization admin sets default member permissions to restrict repository access, the connector respects this setting. Users can't view organization repositories unless they're explicitly added as collaborators.

For enterprises that use the BYOU model (instead of Enterprise Managed Users), each user must enable the permission to share the specific user identity field required for mapping in their GitHub account settings to allow identity mapping.

### Customize content settings

#### Content filter

You can configure a time-range filter for the connector. The default setting is 365 days.

#### Manage properties

Verify property mappings in the sample data for metadata such as **content**, **labels**, **description**, and **timestamps**.

### Customize sync intervals

You can configure incremental and full crawls. The default values are:
- Incremental crawl runs every 15 minutes.
- Full crawl runs daily.

For more information, see [Guidelines for crawl settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content
- [GitHub Server Issues connector overview](github-server-issues-overview.md)
- [Troubleshoot issues with the GitHub Server Issues connector](github-server-issues-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)
