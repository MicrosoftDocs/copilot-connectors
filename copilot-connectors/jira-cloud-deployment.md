---
title: "Deploy the Jira Cloud Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 03/19/2026
ms.localizationpriority: medium
description: "Find information about how to deploy the Jira Cloud Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Jira Cloud Microsoft 365 Copilot connector

The Jira Cloud Microsoft 365 Copilot connector allows your organization to index Jira issues. After you configure the connector and index content from the Jira site, users can search for those items in Microsoft Search and Microsoft 365 Copilot experiences.

This article describes the steps to deploy and customize the Jira Cloud connector.

> [!IMPORTANT]
> The Jira Cloud Copilot connector supports only Jira cloud-hosted instances. This connector doesn't support Jira Server and Jira Data Center versions.

For Jira Cloud service configuration information, see [Set up the Jira Cloud service for connector ingestion](jira-cloud-admin-setup.md).

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be the search admin for your organization's Microsoft 365 tenant.
- Make sure that you know the Jira Cloud instance URL for your organization. To connect to your Jira data, you need your organization's Jira instance URL.
- To connect to Jira and allow the Jira Cloud connector to update issues regularly, you need a service account with the following permissions granted to it.

| Permission | Type | Usage |
| :--- | :--- | :--- |
| Browse projects | Project permission | Crawling Jira issues. This permission is required for the projects that need to be indexed. |
| Issue level security permissions | Issue-level security | Crawling different issue types. This permission is optional. |
| Browse users and groups | Global permission | Security trimming based on access permissions of search results. This permission is required if you select the Only people with access to this data source user setting; otherwise, it's optional. |
| Administer Jira | Global permission | Security trimming based on access permissions of search results. This permission is required if you select the Only people with access to this data source user setting; otherwise, it's optional. |

## Deploy the connector

To add the Jira Cloud connector for your organization:

1.  In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
2.  Go to the **Connectors** tab, and in the left pane, choose **Gallery**.
3.  From the list of available connectors, choose **Jira Cloud**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **Jira Cloud** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery with Microsoft 365 Copilot connectors content](./enhance-copilot-discovery.md).

### Set instance URL

To connect to your Jira cloud data, you need your organization's Jira instance URL. Your organization's Jira instance URL typically looks like the following URL: `https://<your-organization-domain>.atlassian.net`.

If you don't have an instance already, see [Atlassian Jira](https://www.atlassian.com/software/jira) to create a test instance.

### Choose authentication type

To authenticate and sync issues from Jira, choose one of the following supported authentication methods:

*   **Basic authentication** - Enter your account's username (usually email ID) and API token to authenticate using basic auth. For information about how to generate an API token, see [Manage API tokens for your Atlassian account](https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/).
*   **Atlassian Jira OAuth 2.0 (recommended)** - To use the Jira OAuth for authentication:

    1.  Register an app in Atlassian Jira so the Microsoft Search app and Microsoft 365 Copilot can access the instance. For more information, see [Enable OAuth 2.0](https://developer.atlassian.com/cloud/jira/platform/oauth-2-3lo-apps/#enabling-oauth-2-0--3lo-).
    2.  Sign in to the [Atlassian Developer console](https://developer.atlassian.com/console/myapps/) with your Atlassian Jira admin account.
    3.  Choose **Create** and select **OAuth 2.0 integration**.
    4.  Provide an appropriate name for the application and create the new app.
    5.  Go to **Permissions** from the navigation pane on the left. Select **Add** for **Jira API** and select **Configure**. Under **Granular Permissions**, add the required scopes.

        | # | Scope name | Code |
        | :--- | :--- | :--- |
        | 1 | View fields | `read:field:jira` |
        | 2 | View avatars | `read:avatar:jira` |
        | 3 | View project categories | `read:project-category:jira` |
        | 4 | View projects | `read:project:jira` |
        | 5 | Read field configurations | `read:field-configuration:jira` |
        | 6 | View issue types | `read:issue-type:jira` |
        | 7 | View project properties | `read:project.property:jira` |
        | 8 | View users | `read:user:jira` |
        | 9 | View application roles | `read:application-role:jira` |
        | 10 | View groups | `read:group:jira` |
        | 11 | Read issue type hierarchies | `read:issue-type-hierarchy:jira` |
        | 12 | View project versions | `read:project-version:jira` |
        | 13 | View project components | `read:project.component:jira` |
        | 14 | View issue details | `read:issue-details:jira` |
        | 15 | View audit logs | `read:audit-log:jira` |
        | 16 | View issue meta | `read:issue-meta:jira` |
        | 17 | View project roles | `read:project-role:jira` |
        | 18 | View issue security levels | `read:issue-security-level:jira` |
        | 19 | View issue security schemes | `read:issue-security-scheme:jira` |
        | 20 | View permission schemes | `read:permission-scheme:jira` |
        | 21 | View permissions | `read:permission:jira` |
        | 22 | View attachments | `read:attachment:jira` |
        | 23 | View comments | `read:comment:jira` |
        | 24 | View comment properties | `read:comment.property:jira` |
        | 25 | View webhooks | `read:webhook:jira` |
        | 26 | View JQL | `read:jql:jira` |
        | 27 | Create and update webhooks | `write:webhook:jira` |
        | 28 | Delete webhooks | `delete:webhook:jira` |
        | 29 | View epics and related issues | `read:epic:jira-software` |

    6.  Go to **Authorization** from the navigation pane on the left to add the callback URL:
        a. For Microsoft 365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`
        b. For Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
    7.  Choose **Save**.
    8.  Go to **Settings** in the left pane to get the client ID and secret. Complete the connection settings step using the Client ID and Secret.

    > [!NOTE]
    > - For more information about Jira permissions, see [Jira scopes for OAuth 2.0](https://developer.atlassian.com/cloud/jira/platform/scopes-for-oauth-2-3LO-and-forge-apps/#list-of-scopes).
    > - The original (classic) OAuth permissions for Jira Cloud are deprecated. For more information, see the [changelog announcement](https://developer.atlassian.com/cloud/jira/platform/changelog/#CHANGE-517).

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Microsoft 365 Copilot connectors](https://learn.microsoft.com/en-us/microsoftsearch/staged-rollout-for-graph-connectors).

Choose **Create** to deploy the connection. The Jira Cloud Copilot connector starts indexing content right away.

The following are the default values for the connector:

**Users**

- **Access permissions**: Only people with access to content in Data source.
- **Map identities**: Data source identities mapped using Microsoft Entra IDs.

**Content**

- **Site projects**: All projects are indexed.
- **Filter data**: All issues are indexed. No time filter or JQL criteria is applied.
- **Manage Properties**: To check default properties and their schema, see Customize content settings

**Sync**

- **Incremental crawl**: Frequency: Every 15 mins
- **Full crawl**: Frequency: Every day

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Jira Cloud connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

The Jira Cloud Copilot connector supports search permissions visible to **Everyone** or **Only people with access to this data source**. If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to them.

In Atlassian Jira, security permissions are defined using project permission schemes containing site-level groups and project roles. Issue-level security can also be defined using issue-level permission schemes.

> **Important**
> The Jira Cloud Copilot connector must be able to read a user's email ID in Jira to appropriately assign security permissions in Microsoft Search and Microsoft 365 Copilot. This requires you to ensure either of the following:
>
> - All users should select the **Anyone** option for their profile visibility settings. To learn more about profile visibility settings, see [Update your profile and visibility settings](https://support.atlassian.com/atlassian-account/docs/update-your-profile-and-visibility-settings/).
> - For organizations that use [managed accounts](https://support.atlassian.com/user-management/docs/what-are-managed-accounts/):
> - All users must have the managed account setting selected in profile visibility settings.
> - Users who aren't part of the managed account (same as crawling account) must have **Anyone** selected in their profile visibility settings.
> - The crawling account used during connection configuration must have the managed account domain.

#### Map identities

The default method for mapping your data source identities with Microsoft Entra ID is to make the email ID of Jira users the same as the user principal name (UPN) or email address of the users in Microsoft Entra ID. If the default mapping doesn't work for your organization, you can provide a custom mapping formula. For more information, see [Map your non-Azure AD Identities](https://learn.microsoft.com/en-us/microsoftsearch/map-non-aad).

*   Choose the **Microsoft Entra ID** option if the email ID of Jira users is the same as the UPN of users in Microsoft Entra ID.
*   Choose the **Non-Microsoft Entra ID** option if the email ID of Jira users is different from the UPN and email of users in Entra ID.

> [!NOTE]
> Updates to groups that govern access permissions are synced in full crawls only. Incremental crawls don't support the processing of updates to permissions.

### Customize content settings

#### Choose projects and filter data

- **Site projects**: You can choose for the connection to index either the entire Jira site or specific projects only.
    - If you choose to index the entire Jira site, Jira issues in all projects on the site are indexed. New projects and issues are indexed during the next crawl after they're created.
    - If you choose individual projects, only Jira issues in the selected projects are indexed.

    > [!NOTE]
    > When you grant the **Browse projects** permission to a Jira project, the project is listed in the project selection and can be crawled. If a project is missing, check the permissions for your account.

- **Filter data**: You can choose to filter the Jira issues that are indexed in two ways:
    - Specify the issue modified time period. This option only indexes the Jira issues that are created or modified in the time period selected on a rolling basis based on the current crawl.
    - Use the JQL filter to index only specific Jira issue types by using `issueType in (Bug, Improvement)`.

#### Manage properties

You can add or remove available properties from your Jira data source, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. The following table lists the properties that are selected by default.

| Property | Label | Description | Attributes |
| :--- | :--- | :--- | :--- |
| Authors | Authors | Name all the people who participated/collaborated on the item | Retrieve |
| Created | Created date time | Date and time that the item was created in the data source | Query, Retrieve |
| IssueDescription | Content | The description of the issue | Search |
| IssueIconURL | IconUrl | Icon url that represents the issue type | Retrieve |
| IssueId | | | |
| IssueKey | | | |
| IssueLink | url | The target URL of the item in the data source | Query, Retrieve |
| IssueStatus | | | Query |
| IssueSummary | | | |
| ProjectName | | | Query |
| ReporterEmailId | Created by | | Retrieve |
| ReporterName | | | Query, Retrieve |
| Title | Title | The title of the item that you want shown in Copilot and other search experiences | Search, Query, Retrieve |
| Updated | Last modified date time | Date and time the item was last modified in the data source | Query, Retrieve |

> [!NOTE]
> *   The Jira Cloud Copilot connector can index both default issue fields and custom-created issue fields.
> *   If a selected custom-created field isn't present in some Jira issue type, the field is ingested as NULL (blank).
> *   The list of properties that you select affects how users can filter, search, and view results in Copilot.

#### Manage customized properties

To manage customized properties, ensure the following conditions are met:

1.  **Name** is not empty and not composed only of whitespace.
2.  **Key** is not empty and contains an underscore ("_").
3.  **Data type** is supported:
    - **Non-array types**: string, date, datetime, number, option
    - **Array types**: string, option, user
4.  **Name** does not start with "label_" or "Refinable" (reserved system prefixes).
5.  **Name** length is less than or equal to 26 characters.
6.  **Name** contains only letters and numbers (no special characters).

Users can access `{{Jira instance url}}/rest/api/2/field` and review the returned data.

#### Preview data

Use the preview results button to verify the sample values of the selected properties and query filter.

### Customize sync intervals

The refresh interval determines how often your data is synced between the data source and the Jira Cloud Copilot connector index. The following are the two types of refresh intervals:

- **Incremental crawl**: Every 15 mins
- **Full crawl**: Every day

You can change the default values of the refresh interval. For more information, see [Guidelines for sync settings](https://learn.microsoft.com/en-us/microsoftsearch/configure-connector#guidelines-for-sync-settings).

## Related content

- [Jira Cloud connector overview](https://learn.microsoft.com/en-us/microsoftsearch/jira-cloud-overview)
- [Troubleshoot issues with the Jira Cloud connector](https://learn.microsoft.com/en-us/microsoftsearch/jira-cloud-troubleshooting)
- [Set up Copilot connectors in the Microsoft 365 admin center](https://learn.microsoft.com/en-us/microsoftsearch/configure-connector)
