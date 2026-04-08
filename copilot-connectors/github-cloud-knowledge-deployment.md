---
title: "Deploy the GitHub Cloud Knowledge connector"
ms.author: lauragra
author: Lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 12/02/2025
ms.localizationpriority: Medium
description: "Find information about how to deploy the GitHub Cloud Knowledge Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the GitHub Cloud Knowledge connector

The GitHub Cloud Knowledge connector enables organizations to index markdown and text files from GitHub repositories into Microsoft 365 Copilot and Microsoft Search experiences. This article describes the steps to deploy and customize the connector. For general information about Copilot connector deployment, see [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview).

For advanced GitHub configuration information, see [Set up the GitHub service for connector ingestion](github-cloud-knowledge-admin-setup.md).

## Prerequisites

Before you deploy the GitHub Cloud Knowledge connector, make sure that the GitHub Cloud environment is configured in your organization. The following table summarizes the steps to configure the environment and deploy the connector.

| Task | Role |
| ---- | ---- |
| [Configure the environment](github-cloud-knowledge-admin-setup.md) | GitHub admin |
| [Deploy the connector](#deploy-the-connector) | Microsoft 365 admin |
| [Customize connector settings](#customize-settings-optional) (optional) | Microsoft 365 admin |

Before you deploy the GitHub Cloud Knowledge connector, make sure that:

- You're a Microsoft 365 admin for your organization.
- Your GitHub instance is accessible via API.
- A GitHub App is created and configured for authentication.
- Users who access indexed GitHub data have corresponding Microsoft Entra ID identities for permission mapping.
- For enterprise-managed users who authenticate via single sign-on (SSO), the account is signed in before setup. The GitHub authentication flow doesn't support SSO.

## Deploy the connector

To add the GitHub Cloud Knowledge connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **GitHub Cloud Knowledge**.

### Set display name

The display name identifies references in Copilot responses and signifies trusted content. You can accept the default **GitHub Cloud Knowledge** display name, or choose a name that users in your organization recognize.

For more information, see [Enhance Copilot discovery of connector content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Set instance URL

Enter the GitHub organization URL that the connector will index. For example:

`https://github.com/<organization-name>`

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

For information about how to create a GitHub app, see [Use a custom GitHub app for authentication](github-cloud-knowledge-admin-setup.md#use-a-custom-github-app-for-authentication-optional).

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups. For more information, see [Staged rollout for Microsoft 365 Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The GitHub Cloud Knowledge connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|---------------|
| Users    | Only people with access to this data source |
| Content  | Markdown and text files from selected repositories |
| Sync     | Incremental crawl every 15 minutes; full crawl daily |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com).

## Customize settings (optional)

You can customize the default values for the GitHub Cloud Knowledge connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

Choose whether indexed data is visible to:

- **Only people with access to this data source** (default)
- **Everyone**

If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to them. If you choose **Everyone**, indexed data appears in the search results for all users.

#### Mapping identities

To ensure that permissions are applied correctly, map GitHub user identities to Microsoft Entra ID. Choose one of the following options for mapping:

  - **Email:** Maps GitHub email to Microsoft Entra ID user properties.
  - **Login:** Maps GitHub logins with Microsoft Entra ID user properties.
  - **Name:** Maps GitHub name with Microsoft Entra ID user properties.

If direct mapping fails, use regular expressions (regex) to transform the data. For example: `[a-zA-Z0-9]+`. For more information, see [Map Microsoft Entra identities](/microsoft-365/copilot/connectors/map-entra-id).

If the organization admin sets default member permissions to restrict repository access, the connector respects this setting. Users can't view organization repositories unless they're explicitly added as collaborators.

For enterprises that use the Bring Your Own Key (BYOK) model instead of Enterprise Managed Users (EMU), each user must enable the permission to share the required identity field in their GitHub account settings. This step ensures proper identity mapping between GitHub and your organization’s directory.

### Customize content settings

On the **Content** tab, you can verify property mappings in the sample data for metadata such as content, labels, description, and timestamps.

Choose the repositories and file types (Markdown files, text documents) you want to make searchable.

#### Manage properties

You can add or remove properties, assign schema attributes, and define semantic labels. The following properties are indexed by default:

| Property      | Semantic Label | Description                     | Schema Attributes |
|---------------|---------------|---------------------------------|-------------------|
| File name     | Title         | Name of the file               | Searchable, Retrievable |
| Repository    | Source        | GitHub repository name         | Searchable, Queryable |
| Content       | Body          | Markdown or text file content  | Searchable, Retrievable |

### Customize sync intervals

The refresh interval determines how often your data is synced. Default values:

- Incremental crawl: Every 15 minutes
- Full crawl: Daily

You can change these values as needed. For more information, see [Guidelines for crawl settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [GitHub Cloud Knowledge connector overview](github-cloud-knowledge-overview.md)
- [Troubleshoot issues with the GitHub Cloud Knowledge connector](github-cloud-knowledge-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)
