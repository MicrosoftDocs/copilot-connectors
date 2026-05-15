---
title: Set up the Jira Cloud service for Jira Cloud connector ingestion
description: Get the steps that the Jira Cloud admin needs to complete for your organization to configure the Jira Cloud Microsoft 365 Copilot connector.
author: lauragra
ms.author: lauragra
manager: calvind
ms.reviewer: jecui
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 05/15/2026
---

# Set up the Jira Cloud service for Jira Cloud Copilot connector ingestion

The Jira Cloud connector for Microsoft 365 Copilot and Microsoft Search enables your organization to index and search Jira Cloud content directly within Microsoft 365 experiences. By integrating Jira Cloud with Microsoft 365, users can discover issues, projects, and other Jira data through Copilot and Microsoft Search, improving productivity and collaboration.

This article describes the Jira Cloud configuration that you must complete before you deploy the Jira Cloud Copilot connector in the Microsoft 365 admin center.

For information about how to deploy the connector, see [Deploy the Jira Cloud connector](jira-cloud-deployment.md).

## Prerequisites

Before you begin, make sure that you meet the following prerequisites:

- You must be a **Jira Cloud site admin**.
- Confirm that Jira REST APIs are enabled and accessible.
- Make sure that your organization allows outbound connections to Microsoft Graph connector IPs if network restrictions apply.
- Make sure that you have access to the [Atlassian Developer Console](https://developer.atlassian.com/console/myapps/).

## Setup checklist

| Task | Role |
|------|------|
| [Identify the Jira Cloud instance URL](#identify-the-jira-cloud-instance-url) | Jira admin |
| [Enable API access](#enable-api-access) | Jira admin |
| [Create a service account and grant permissions](#create-a-service-account-and-grant-permissions) | Jira admin |
| [Choose an authentication method](#choose-an-authentication-method) | Jira admin |
| [Review profile visibility for identity mapping](#review-profile-visibility-for-identity-mapping) | Jira admin |
| [Estimate content scope](#estimate-content-scope) | Jira admin |

## Identify the Jira Cloud instance URL

The Jira Cloud instance URL is required when you deploy the connector in the Microsoft 365 admin center. To identify the Jira Cloud instance URL:

- Sign in to your Jira Cloud account at `https://<yourcompany>.atlassian.net`.
- From the dashboard, note the **base URL** in the browser address bar. For example: `https://<yourcompany>.atlassian.net`.

> [!NOTE]
> - Don't use a project-specific URL (such as `/browse/PROJ-123`).
> - Test the URL in a browser to confirm that it resolves to your Jira dashboard.

## Enable API access

Verify that Jira Cloud REST APIs are enabled by default and that no API restrictions or app allowlists prevent access.

If your organization uses network-level restrictions, add the Microsoft Graph connector IPs to the allowlist.

## Create a service account and grant permissions

Create a dedicated Jira Cloud account for the connector instead of using a personal account.

To create the service account:

- Sign in to the [Atlassian Admin Console](https://admin.atlassian.com/) as an organization or site admin.
- Go to **Directory** > **Users**.
- Choose **Invite users** and enter a dedicated email address, such as `jira-connector@contoso.com`.
- Under **Products**, select **Jira Software**.
- Don't assign admin or project admin roles unless they're required for your indexing or security trimming scenario.

Grant the service account the permissions required for the connector.

| Permission | Type | Required when |
| :--- | :--- | :--- |
| Browse projects | Project permission | Required for all projects that you want to index. |
| Issue level security permissions | Issue-level security | Required only if the indexed projects use issue-level security. |
| Browse users and groups | Global permission | Required when the connector is configured to show results only to people who have access to the source data. |
| Administer Jira | Global permission | Required when the connector is configured to show results only to people who have access to the source data. |

## Choose an authentication method

To authenticate and sync issues from Jira, choose one of the following supported authentication methods:

*   **OAuth (recommended)** 
*   **Customized Atlassian Jira OAuth 2.0**

To use the Jira OAuth for authentication:

    1.  Register an app in Atlassian Jira so Microsoft Search and Microsoft 365 Copilot can access the instance. For more information, see [Enable OAuth 2.0](https://developer.atlassian.com/cloud/jira/platform/oauth-2-3lo-apps/#enabling-oauth-2-0--3lo-).
    1.  Sign in to the [Atlassian Developer console](https://developer.atlassian.com/console/myapps/) with your Atlassian Jira admin account.
    1.  Choose **Create** and select **OAuth 2.0 integration**.
    1.  Provide an appropriate name for the application and create the new app.
    1.  On the left navigation pane, go to **Permissions**. Select **Add** for **Jira API** and select **Configure**. Under **Granular Permissions**, add the required scopes.

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

    1.  On the left navigation pane, go to **Authorization** to add the callback URL:
        - For Microsoft 365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`
        - For Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
    1.  Select **Save**.
    1.  In the left pane, go to **Settings** to get the client ID and secret. Complete the connection settings step by using the Client ID and Secret.

    > [!NOTE]
    > - For more information about Jira permissions, see [Jira scopes for OAuth 2.0](https://developer.atlassian.com/cloud/jira/platform/scopes-for-oauth-2-3LO-and-forge-apps/#list-of-scopes).
    > - The original (classic) OAuth permissions for Jira Cloud are deprecated. For more information, see the [changelog announcement](https://developer.atlassian.com/cloud/jira/platform/changelog/#CHANGE-517).

## Review profile visibility for identity mapping

The Jira Cloud Copilot connector supports search permissions visible to **Everyone** or **Only people with access to this data source**. If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to them.

> [!IMPORTANT]
>  If you plan to configure the connector with **Only people with access to this data source**, the Jira Cloud Copilot connector must be able to read a user's email ID in Jira to appropriately assign security permissions in Microsoft Search and Microsoft 365 Copilot. This requirement means you need to ensure one of the following conditions:
>
> - All users select the **Anyone** option for their profile visibility settings. To learn more about profile visibility settings, see [Update your profile and visibility settings](https://support.atlassian.com/atlassian-account/docs/update-your-profile-and-visibility-settings/).
> - For organizations that use [managed accounts](https://support.atlassian.com/user-management/docs/what-are-managed-accounts/):
>   - All users select the managed account setting in profile visibility settings.
>   - Users who aren't part of the managed account (same as crawling account) select **Anyone** in their profile visibility settings.
>   - The crawling account used during connection configuration has the managed account domain.

## Estimate content scope

Determine the number of projects and issues to index. For instances with more than 10,000 issues:

- Enable incremental sync.
- Plan for throttling.
- Full indexing can take several hours. Schedule the initial sync during off-business hours.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Jira Cloud connector](jira-cloud-deployment.md)
