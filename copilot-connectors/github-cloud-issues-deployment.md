---
title: Deploy the GitHub Cloud Issues Microsoft 365 Copilot connector
description: "Find information about how to deploy the GitHub Cloud Issues Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
author: Lauragra
ms.author: lauragra
ms.reviewer: lauragra
manager: calvind
ms.date: 12/02/2025
ms.service: copilot-connectors
ms.topic: concept-article
---

# Deploy the GitHub Cloud Issues Microsoft 365 Copilot connector

The GitHub Cloud Issues Microsoft 365 Copilot connector enables your organization to index GitHub issues so they can be surfaced in Microsoft 365 Copilot and Microsoft Search experiences. This article describes the steps to deploy and customize the connector in the Microsoft 365 admin center.

For advanced GitHub configuration information, see [Set up the GitHub service for connector ingestion](github-cloud-issues-admin-setup.md).

## Prerequisites

Before you deploy the GitHub Cloud Issues connector, make sure that the GitHub Cloud environment is configured in your organization. The following table summarizes the steps to configure the environment and deploy the connector.

| Task | Role |
| ---- | ---- |
| [Configure the environment](github-cloud-issues-admin-setup.md) | GitHub admin |
| [Deploy the connector in the Microsoft 365 admin center](#deploy-the-connector) | Microsoft 365 admin |
| [Customize connector settings](#customize-settings-optional) (optional) | Microsoft 365 admin |

Before you deploy the GitHub Cloud Issues connector, make sure that:

- You're a Microsoft 365 admin.
- Your GitHub environment is configured and accessible via API.
- A GitHub App is created for authentication with the required permissions.
- Users who access indexed GitHub data have corresponding Microsoft Entra ID identities for permission mapping.
- For enterprise-managed users who authenticate via single sign-on (SSO), accounts are signed in before setup. The GitHub authentication flow doesn't support SSO during configuration.

## Deploy the connector

To add the GitHub Cloud Issues connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **GitHub Cloud Issues**.

### Set display name

The display name identifies references in Copilot responses and helps users recognize the associated content source. You can accept the default **GitHub Cloud Issues** display name or customize it.

For more information, see [Enhance Copilot discovery of connector content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Choose authentication type

The connector supports the following authentication types:

- **OAuth (Recommended)**: To use OAuth authentication:

    - Install the [GitHub Issues GitHub app](https://github.com/apps/m365-connector-github-issues) in the GitHub organization.
    - Choose a display name that helps users recognize the connection.
    - Enter your organization name.
    - Choose **Authorize** to sign in and grant access.
    
    > [!NOTE]
    > This authentication method is currently in preview.

- **Customized GitHub app (on behalf of user)**: Enter your client ID and client secret from the GitHub app and authorize access.
- **Customized GitHub app (installation)**: Use a private key generated from your GitHub app. Enter the client ID and organization name, and upload the private key.

For information about how to create a GitHub app, see [Use a custom GitHub app for authentication](github-cloud-issues-admin-setup.md#use-a-custom-github-app-for-authentication-optional).

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups. For more information, see [Staged rollout for Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The GitHub Cloud Issues connector starts indexing content immediately.

The following table lists the default values that are set when you deploy the connector.

| Category | Default value |
|----------|---------------|
| Users    | Identity mapping based on email |
| Content  | Issues indexed with metadata, labels, and timestamps |
| Sync     | Incremental crawl every 15 minutes; full crawl daily |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the GitHub Cloud Issues connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

Specify which users and groups have access to indexed GitHub content.

#### Mapping identities

To ensure that permissions are applied correctly, map GitHub user identities to Microsoft Entra ID. Choose one of the following options for mapping:

  - **Email:** Maps GitHub email to Microsoft Entra ID user properties.
  - **Login:** Maps GitHub logins with Microsoft Entra ID user properties.
  - **Name:** Maps GitHub name with Microsoft Entra ID user properties.

If direct mapping fails, use regular expressions (regex) to transform the data. For example: `[a-zA-Z0-9]+`. For more information, see [Map Microsoft Entra identities](/microsoft-365/copilot/connectors/map-entra-id).

If the organization admin sets default member permissions to restrict repository access, the connector respects this setting. Users can't view organization repositories unless they're explicitly added as collaborators.

For enterprises that use the Bring Your Own Key (BYOK) model instead of Enterprise Managed Users (EMU), each user must enable the permission to share the required identity field in their GitHub account settings. This step ensures proper identity mapping between GitHub and your organization’s directory.

### Customize content settings

On the Content tab, you can verify property mappings in the sample data for metadata such as content, labels, description, and timestamps.

#### Content filter

You can configure a time-range filter for the connector. The default setting is 365 days.

#### Manage properties

You can add or remove available properties from the data source, assign a schema to the property (searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. The connector indexes the following properties by default.

| Property    | Semantic Label | Description                | Schema Attributes |
|-------------|---------------|-----------------------------|-------------------|
| title       | Title         | Issue title                 | Searchable        |
| description | Content       | Issue description           | Searchable        |
| labels      | Tags          | Issue labels                | Refinable         |
| timestamps  | Date          | Created and updated dates   | Sortable          |

### Customize sync intervals

Configure the full and incremental crawl sync intervals. The following are the default values:

- **Incremental crawl:** Every 15 minutes
- **Full crawl:** Daily

You can adjust these intervals to meet your organization's needs. For more information, see [Guidelines for sync settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [GitHub Cloud Issues connector overview](github-cloud-issues-overview.md)
- [Troubleshoot issues with the GitHub Cloud Issues connector](github-cloud-issues-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)
