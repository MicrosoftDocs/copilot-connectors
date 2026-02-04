---
title: "Deploy the Asana Microsoft 365 Copilot connector"
ms.author: lauragra
author: Kai-Cloud
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 10/23/2025
ms.localizationpriority: Medium
description: "Find information about how to deploy the Asana Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Asana Microsoft 365 Copilot connector

The Asana Microsoft 365 Copilot connector integrates Asana tasks into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface relevant task information directly within apps like Microsoft Teams, Outlook, and SharePoint. This article describes the steps to deploy and customize the Asana connector. 

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be a Microsoft 365 admin.
- You must have access to the Asana workspace you want to connect.
- The Asana environment must be configured to allow API access.
- Identity mapping must be configured if Asana user emails differ from Microsoft Entra ID user principal names (UPNs).

## Deploy the connector

To add the Asana connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
2. Choose the **Gallery** tab.
3. From the list of available connectors, choose **Asana**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **Asana** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](/microsoft-365-copilot/connectors/enhancing-microsoft-copilot-discovery-with-graph-connector-content).

### Set instance URL

Enter the URL of the Asana workspace you want to connect. The typical structure is:

`https://app.asana.com/`

### Choose authentication type

The Asana connector supports the following authentication type:

- **OAuth 2.0** (recommended): Secure and scalable authentication using Asana's OAuth flow.

To use **Asana OAuth** for authentication, an Asana admin must create an app in the [Asana developer console](https://app.asana.com/0/my-apps).

Use the information in the following table to complete the OAuth client creation form.

|Field | Description | Recommended value|
|--- | --- | ---|
|App name | Unique value that identifies the application for which you require OAuth access. | Microsoft Search|
|Which best describes what your app will do? | Describe the purpose of the app. | Get data out of Asana to create reports.|
|Redirect URL | A required callback URL that the authorization server redirects to. | For **Microsoft 365 Enterprise**: `https://gcs.office.com/v1.0/admin/oauth/callback`</br></br>For **Microsoft 365 Government**: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`|
|Permission scopes | Scopes define what your app can access and what kind of requests it can make. | Select `Full permissions`.|
|Manage distribution | Choose workspaces to be distributed. | Add specific workspaces that the connector can access or select **Any workspace**.|
   
Copy the client ID and client secret from the OAuth tab in the Asana app and paste them in the **Client ID** and **Client secret** fields. Choose **Authorize**, and use the same Asana admin account credentials to authenticate permission to crawl.

> [!NOTE]
> You need to authorize access to the Asana app in a popup window. Make sure that your browser permits popup windows or grants access if the popup window is blocked.

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to.

Choose **Create** to deploy the connection. The Asana Copilot connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Setting | Default value |
|----------|---------|---------------|
| Users | Access permissions | Only people with access to the content in the Data source. |
| Users | Map identities | Data source identities mapped using Microsoft Entra IDs. |
| Content | Manage properties | For information about the default properties and their schema, see [Customize content settings](#customize-content-settings). |
| Sync | Incremental crawl | Runs every 15 minutes. |
| Sync | Full crawl | Runs every day. |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Asana connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

The Asana connector supports the following user access permissions:

- Everyone
- Only people with access to this data source (default)

If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to it. 

In Atlassian Asana, security permissions are defined via project permission schemes that contain site-level groups and project roles. Task-level security can also be defined via task-level permission schemes.

#### Map identities

The default method to map your data source identities with Microsoft Entra ID is to verify that the email ID of Asana users is the same as the user principal name (UPN) of the users in Microsoft Entra ID. If the default mapping doesn't work for your organization, you can provide a custom mapping formula. For more information, see [Map your non-Azure AD Identities](map-non-entra-id.md).

To identify which option is best for your organization:

- Choose the **Microsoft Entra ID** option if the email ID of Asana users is the *same* as the UPN in Microsoft Entra ID.
- Choose the **Non-Microsoft Entra ID** option if the email ID of Asana users is *different* than the users' UPN and email in Microsoft Entra ID.

### Customize content settings

To can add or remove available properties from your Asana, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. 

The following table lists the properties that are indexed by default.

|Default property|Label|Description|
|---|---|---|
| Assignee | `assignedToPeople`| The people who should complete this task |
| Completed | `State` | Indicates whether the task is completed |
| CompletedAt |`ClosedDate` | Date and time that the task was completed |
| CompletedBy | `closedBy` | The person who completed the task |
| CreatedAt | `createdDateTime` | Date and time that the task was created |
| CreateBy | `createdBy` | The person who created this task |
| DueOn | `DueDate` | When this task should be completed |
| Gid | `SecondaryId` | Global ID of this task |
| ModifiedAt | `lastModifiedDateTime` | Date and time that the task was modified |
| Name | `Title` | Task name |
| Notes | `NA`  | Description of the task (content) |
| ProjectIds | `NA` | Project IDs |
| ProjectNames | `NA` | Project names |
| Tags | `Tags` | Tags assigned to this task |
| TaskUrl | `url` | The link of the task |
| WorkspaceName | `containerName` | Workspace name |
| Priority | `Priority` | Priority of the task |
| Severity | `Severity` | Severity level of the task |
| Sections | `NA` | Sections that this task belongs to |
| SectionIds | `NA` | Section IDs that this task belongs to |
| Likes | `NumReactions` | Number of likes on this task |

### Customize sync intervals

You can configure the frequency of full and incremental crawls:

- **Full crawl**: Recommended every 24 hours to ensure complete data refresh.
- **Incremental crawl**: Recommended every 15 minutes to capture recent changes.

For more information, see [Guidelines for sync settings](/microsoft-365-copilot/connectors/deployment-overview#guidelines-for-sync-settings).

## Related content

- [Asana Copilot connector overview](asana-overview.md)
- [Troubleshoot issues with the Asana connector](asana-troubleshooting.md)
- [Set up Copilot connectors in the admin center](/microsoft-365-copilot/connectors/deployment-overview)
