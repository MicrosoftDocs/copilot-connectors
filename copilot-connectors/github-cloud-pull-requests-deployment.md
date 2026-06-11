---
title: Deploy the GitHub Cloud Pull Requests connector
description: Find information about how to deploy the GitHub Cloud Pull Requests Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options.
ms.topic: how-to
ms.service: copilot-connectors
author: lauragra
ms.author: lauragra
manager: calvind
ms.date: 12/02/2025
ms.localizationpriority: Medium
---

# Deploy the GitHub Cloud Pull Requests connector

The GitHub Cloud Pull Requests Microsoft 365 Copilot connector enables your organization to index pull requests stored in GitHub repositories into Microsoft 365 Copilot and Microsoft Search experiences. This article describes the steps to deploy and customize the connector. For general information about Copilot connector deployment, see [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview).

For advanced GitHub configuration information, see [Set up the GitHub service for connector ingestion](github-cloud-pull-requests-admin-setup.md).

## Prerequisites

Before you deploy the GitHub Cloud Pull Requests connector, make sure that the GitHub environment is configured in your organization. The following table summarizes the steps to configure the GitHub environment and deploy the connector.

| Task | Role |
|------|------|
| [Identify the GitHub organization name](github-cloud-pull-requests-admin-setup.md#identify-the-github-organization-name) | GitHub admin |
| [Ensure API access to the target GitHub instance](github-cloud-pull-requests-admin-setup.md#ensure-api-access-to-the-target-github-instance) | GitHub admin |
| [Deploy the connector](#deploy-the-connector) | Microsoft 365 admin |
| [Customize connector settings](#customize-settings-optional) (optional) | Microsoft 365 admin |

Before you deploy the connector, make sure that you meet the following prerequisites:

- You're a Microsoft 365 admin.
- Your GitHub instance is accessible via API.
- A GitHub App is created and configured for authentication.
- The account used for authentication has access to the repositories and pull requests to be indexed.
- Users who access indexed GitHub data have corresponding Microsoft Entra ID identities for permission mapping.

## Deploy the connector

To add the GitHub Cloud Pull Requests connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **GitHub Cloud Pull Requests**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **GitHub Cloud Pull Requests** display name or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery with Microsoft 365 Copilot connectors content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Choose authentication type

The connector supports the following authentication types:

- **OAuth (Recommended)**: To use OAuth authentication:

    - Install the [GitHub Pull Requests GitHub app](https://github.com/apps/m365-connector-github-prs) in the GitHub organization.
    - Choose a display name that helps users recognize the connection.
    - Enter your organization name.
    - Choose **Authorize** to sign in and grant access.
    
    > [!NOTE]
    > This authentication method is currently in preview.

- **Customized GitHub app (on behalf of user)**: Enter your client ID and client secret from the GitHub app and authorize access.
- **Customized GitHub app (installation)**: Use a private key generated from your GitHub app. Enter the client ID and organization name, and upload the private key.

For information about how to create a GitHub app, see [Use a custom GitHub app for authentication](github-cloud-pull-requests-admin-setup.md#use-a-custom-github-app-for-authentication-optional).


### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The GitHub Cloud Pull Requests Copilot connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|---------------|
| Users    | Identity mapping based on GitHub email |
| Content  | Pull request metadata (title, description, labels, timestamps) |
| Sync     | Incremental crawl every 15 minutes; full crawl daily |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the GitHub Cloud Pull Requests connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

Choose whether indexed data is visible to:

- **Only people with access to this data source** (default)
- **Everyone**

If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to them. If you choose **Everyone**, indexed data appears in the search results for all users.

#### Mapping identities

To ensure correct permission enforcement, map GitHub user identities to Microsoft Entra ID. The following are the options:
  - **Email:** Maps GitHub email to Microsoft Entra ID user properties.
  - **Login:** Maps GitHub logins with Microsoft Entra ID user properties.
  - **Name:** Maps GitHub name with Microsoft Entra ID user properties.

If direct mapping fails, use **regular expressions (regex)** to transform the data. For example: `[a-zA-Z0-9]+`

If the organization admin sets default member permissions to restrict repository access, the connector respects this setting. Users can't view organization repositories unless they're explicitly added as collaborators.

For enterprises that use the Bring Your Own Key (BYOK) model instead of Enterprise Managed Users (EMU), each user must enable the permission to share the required identity field in their GitHub account settings. This step ensures proper identity mapping between GitHub and your organization’s directory.

### Customize content settings

On the **Content** tab, you can verify property mappings in the sample data for metadata such as content, labels, description, and timestamps.

#### Time-range filter

You can configure a time-range filter. The default setting is 365 days.

#### Manage properties

You can add or remove properties, assign schema attributes, and define semantic labels. The following properties are indexed by default.

| Property | Semantic label | Description | Schema attributes |
|----------|----------------|-------------|--------------------|
| title | Title | Pull request title | Searchable |
| description | Content | Pull request description | Searchable |
| labels | Tags | Labels applied to pull request | Searchable |
| createdDate | Created | Date pull request was created | Searchable, Sortable |

### Customize sync intervals

The refresh interval determines how often your data is synced. You can customize the following default values:

- Incremental crawl: Every 15 minutes
- Full crawl: Daily

For more information, see [Guidelines for crawl settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [GitHub Cloud Pull Requests connector overview](github-cloud-pull-requests-overview.md)
- [Troubleshoot issues with the GitHub Cloud Pull Requests connector](github-cloud-pull-requests-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)
