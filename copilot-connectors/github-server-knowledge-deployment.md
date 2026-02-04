---
title: "Deploy the GitHub Server Knowledge Microsoft 365 Copilot connector"
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
description: "Find information about how to deploy the GitHub Server Knowledge Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the GitHub Server Knowledge Microsoft 365 Copilot connector

The GitHub Server Knowledge connector integrates GitHub Enterprise knowledge into Microsoft 365, enabling Copilot and Microsoft Search to surface relevant wiki pages, markdown files, and blogs directly within apps like Teams, Outlook, and SharePoint. This article describes the steps to deploy and customize the connector.

For GitHub configuration information, see [Set up the GitHub service for connector ingestion](github-server-knowledge-admin-setup.md).

## Prerequisites

Before you deploy the GitHub Server Knowledge connector, make sure that the GitHub environment is configured in your organization. The following table summarizes the steps to configure the GitHub environment and deploy the connector:

| Task                                      | Role                     |
|-------------------------------------------|--------------------------|
| [Configure the GitHub environment](github-server-knowledge-admin-setup.md) | GitHub admin            |
| [Deploy the connector in the Microsoft 365 admin center](#deploy-the-connector) | Microsoft 365 admin     |
| [Customize connector settings](#customize-settings-optional) (optional) | Microsoft 365 admin     |

Before you deploy the connector, make sure that:

- You're a Microsoft 365 admin.
- Your GitHub Enterprise instance is accessible via API.
- A GitHub app is created and installed with the required permissions.
- The user account used for authentication has access to the repositories and knowledge to be indexed.
- Users who access indexed GitHub data have corresponding **Microsoft Entra ID** identities for permission mapping.
- The Microsoft Graph Connector Agent is installed on a device with access to the GitHub instance (version 3.1.11.0 or later).

## Deploy the connector

To add the GitHub Server Knowledge connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
2. Go to the **Connectors** tab, and in the left pane, choose **Gallery**.
3. From the list of available connectors, choose **GitHub Server Knowledge**.

### Set display name

The display name identifies references in Copilot responses and signifies trusted content. You can accept the default **GitHub Server Knowledge** display name, or customize it to a name that users in your organization recognize.

### Set instance URL

Enter the instance URL of your GitHub Enterprise server. This URL is typically the following format:

`https://github.<your-domain>.com`

### Choose authentication type

The connector supports the following authentication types:

- **GitHub app (on behalf of user)**: Recommended for most scenarios. Enter your client ID and client secret from the GitHub app and authorize access.
- **GitHub app (installation)**: Use a private key generated from your GitHub app. Enter the client ID and organization name, and upload the private key. Note that this authentication type is currently in preview. To use this authentication type, contact Microsoft support.

For information about how to create a GitHub app, see [Use a custom GitHub app for authentication](github-server-knowledge-admin-setup.md#use-a-custom-github-app-for-authentication).

### Roll out to a limited audience

Deploy this connection to a limited user base if you want to validate it in Copilot and Microsoft Search before you expand the rollout. To learn more, see [Staged rollout for Copilot connectors](/microsoft-365-copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The GitHub Server Knowledge connector starts indexing content right away.

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

The following table lists the default values that are set when you deploy the connector.

| **Category** | **Default value** |
|--------------|--------------------|
| Users        | Access permissions set to **Only people with access to this data source**. |
| Content      | Index Markdown files and text documentation from selected repositories. |
| Sync         | Incremental crawl every 15 minutes; full crawl daily. |

To customize these values, choose **Custom setup**. You can edit user permissions, manage property mappings, and adjust sync intervals.

## Customize settings (optional)

You can customize the default values for the GitHub Server Knowledge connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

Choose between:

- **Only people with access to this data source** (default)
- **Everyone**

#### Identity mapping

To ensure that permissions are applied correctly, map GitHub user identities to Microsoft Entra ID. Choose one of the following options for mapping:

- **Email:** Maps GitHub email to Microsoft Entra ID user properties.
- **Login:** Maps GitHub logins with Microsoft Entra ID user properties.
- **Name:** Maps GitHub name with Microsoft Entra ID user properties.

If direct mapping fails, use regular expressions (regex) to transform the data. For example: `[a-zA-Z0-9]+`. For more information, see [Map Microsoft Entra identities](/microsoft-365-copilot/connectors/map-entra-id).

If the organization admin sets default member permissions to restrict repository access, the connector respects this setting. Users can't view organization repositories unless they're explicitly added as collaborators.

For enterprises that use the BYOU model (instead of Enterprise Managed Users), each user must enable the permission to share the specific user identity field required for mapping in their GitHub account settings to allow identity mapping.

### Customize content settings

Choose the repositories and file types (Markdown files and text documentation) you want to make searchable.

#### Manage properties

You can add or remove available properties from your GitHub data source, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property.

#### Sync intervals

The refresh interval determines how often your data is synced between the data source and the connector index. The following are the default values:

- Incremental crawl: Every 15 minutes
- Full crawl: Daily

You can change these defaults in the **Sync** tab. For more information, see [Guidelines for sync settings](/microsoft-365-copilot/connectors/deployment-overview#guidelines-for-sync-settings).

## Related content

- [GitHub Server Knowledge connector overview](github-server-knowledge-overview.md)
- [Troubleshoot issues with the GitHub Server Knowledge connector](github-server-knowledge-troubleshooting.md)
