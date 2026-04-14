---
title: "Deploy the Jira Cloud connector"
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 04/142026
ms.localizationpriority: medium
description: "Find information about how to deploy the Jira Cloud Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Jira Cloud connector

The Jira Cloud Microsoft 365 Copilot connector allows your organization to index Jira issues. After you configure the connector and index content from the Jira site, users can search for those items in Microsoft Search and Microsoft 365 Copilot experiences.

This article describes the steps to deploy and customize the Jira Cloud connector.

> [!IMPORTANT]
> The Jira Cloud Copilot connector supports only Jira cloud-hosted instances. This connector doesn't support Jira Server and Jira Data Center versions.

For Jira Cloud service configuration information, see [Set up the Jira Cloud service for connector ingestion](jira-cloud-admin-setup.md).

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be the search admin for your organization's Microsoft 365 tenant.
- You must complete the the steps to [Set up the Jira Cloud service for connector ingestion](jira-cloud-admin-setup.md).
- You have the Jira Cloud instance URL.
- You have the authentication values for the authentication method that you plan to use:
    - Basic authentication: Jira username and API token.
    - OAuth 2.0: Client ID and client secret.

## Deploy the connector

To add the Jira Cloud connector for your organization:

1.  In the Microsoft 365 admin center, in the left pane, select **Copilot** > **Connectors**.
2.  Go to the **Connectors** tab, and in the left pane, select **Gallery**.
3.  From the list of available connectors, select **Jira Cloud**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **Jira Cloud** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery with Microsoft 365 Copilot connectors content](./enhance-copilot-discovery.md).

### Set instance URL

To connect to your Jira cloud data, enter your organization's Jira instance URL. The URL is typically `https://<your-organization-domain>.atlassian.net`.

### Choose authentication type

Choose one of the following supported authentication methods:

- **Basic authentication**: Enter the Jira username and API token for the service account that you prepared in Jira Cloud.
- **Atlassian Jira OAuth 2.0 (recommended)**: Enter the client ID and client secret from the OAuth 2.0 app that you created in Atlassian.

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Microsoft 365 Copilot connectors](staged-rollout.md).

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

For the Jira-side permission and profile visibility requirements that support this setting, see [Set up the Jira Cloud service for connector ingestion](jira-cloud-admin-setup.md).

#### Map identities

The default method for mapping your data source identities with Microsoft Entra ID is to make the email ID of Jira users the same as the user principal name (UPN) or email address of the users in Microsoft Entra ID. If the default mapping doesn't work for your organization, you can provide a custom mapping formula. For more information, see [Map your non-Microsoft Entra ID identities](./map-non-entra-id.md).

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

Users can access `https://<your-organization-domain>.atlassian.net/rest/api/2/field` and review the returned data.

#### Preview data

Use the preview results button to verify the sample values of the selected properties and query filter.

### Customize sync intervals

The refresh interval determines how often your data is synced between the data source and the Jira Cloud Copilot connector index. The following are the two types of refresh intervals:

- **Incremental crawl**: Every 15 mins
- **Full crawl**: Every day

You can change the default values of the refresh interval. For more information, see [Guidelines for crawl settings](deployment-overview.md#guidelines-for-crawl-settings).


## API endpoints

The following table lists the API endpoints that the connector calls to crawl data and the permissions required for each endpoint.

  | HTTP Method | Endpoint | OAuth 2.0 Scope | Used For |
  |-------------|----------|-----------------|----------|
  | GET | `/rest/api/3/mypermissions` | `read:permission:jira` | Verify user permissions|
  | GET | `/rest/api/2/field` | `read:field:jira`, `read:avatar:jira`, `read:project-category:jira`, `read:project:jira`, `read:field-configuration:jira` |  Get issue fields metadata |
  | GET | `/rest/api/2/search?jql={0}&startAt={1}&maxResults={2}&fields={3}&expand=renderedFields,changelog` | `read:issue-details:jira`,`read:jql:jira`,`read:issue-meta:jira`, `read:issue.changelog:jira` | Search issues with JQL, rendered fields, and changelog |
  | GET | `/rest/api/3/search/jql` | `read:issue-details:jira`, `read:jql:jira`, `read:group:jira`, `read:field:jira` | Post-based JQL search (v3) |
  | GET | `/rest/api/3/search/jql?jql=id={0}&fields=attachment,comment&maxResults=1` | `read:issue-details:jira`, `read:jql:jira`, `read:attachment:jira`, `read:comment:jira`, `read:comment.property:jira`  | Get issue comments and attachments in single call |
  | GET | `/rest/api/3/project/search?expand=lead&startAt={0}&maxResults={1}&status=live&action=browse` | `read:project:jira` | Get projects list with browse filter (v3) |
  | GET | `/rest/api/3/project/{0}?expand=lead` | `read:project:jira` | Get single project by ID or key |
  | GET | `/rest/api/2/project/{0}/permissionscheme?expand=user` | `read:permission-scheme:jira` | Get project permission scheme  |
  | GET | `/rest/api/2/project/{0}/issuesecuritylevelscheme` | `read:issue-security-scheme:jira` | Get issue security level scheme for project |
  | GET | `/rest/api/2/issuesecurityschemes/{0}/members?startAt={1}&maxResults={2}` | `read:issue-security-level:jira` | Get issue security scheme members |
  | GET | `/rest/api/2/role` | `read:role:jira` | Get all project roles |
  | GET | `/rest/api/2/role/{0}` | `read:role:jira` | Get specific project role details |
  | GET | `/rest/api/2/project/{0}/role/{1}` | `read:project-role:jira` | Get project-specific role actors |
  | GET | `/rest/api/3/group/bulk?{0}startAt={1}&maxResults={2}` | `read:group:jira` | Get groups in bulk |
  | GET | `/rest/api/2/group/member?groupname={0}&startAt={1}&maxResults={2}` | `read:group:jira` | Get group members by name  |
  | GET | `/rest/api/2/group/member?groupId={0}&startAt={1}&maxResults={2}` | `read:group:jira` | Get group members by ID  |
  | GET | `/rest/api/2/user?accountId={0}` | `read:user:jira` | Get single user details |
  | GET | `/rest/api/3/user/bulk` | `read:user:jira` | Get bulk user details |
  | GET | `/rest/api/2/users?startAt={0}&maxResults={1}` | `read:user:jira` | Get list of users with pagination |
  | GET | `/rest/api/3/applicationrole` | `read:application-role:jira` | Get application roles|
  | GET | `{contentUrl}` (attachment download) | `read:attachment:jira` | Download attachment binary content |

## Related content

- [Atlassian Jira Cloud connector overview](jira-cloud-overview.md)
- [Troubleshoot issues with the Atlassian Jira Cloud connector](jira-cloud-troubleshooting.md)
- [Jira result layout](jira-result-layout.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)
