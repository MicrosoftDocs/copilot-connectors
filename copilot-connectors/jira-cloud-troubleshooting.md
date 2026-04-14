---
title: "Troubleshoot issues with the Jira Cloud connector"
description: "Learn how to troubleshoot common issues with the Jira Cloud Microsoft 365 Copilot connector, including error messages, possible causes, and resolution steps."
ms.author: lauragra
author: lauragra
manager: calvind
ms.topic: troubleshooting
ms.service: copilot-connectors
ms.date: 11/19/2025
ms.localizationpriority: medium
---

# Troubleshoot issues with the Jira Cloud connector

This article provides troubleshooting guidance for the Jira Cloud Microsoft 365 Copilot connector, including common error messages, possible causes, and resolution steps. To verify Jira Cloud configuration information, see [Set up the Jira Cloud service for connector ingestion](jira-cloud-admin-setup.md).

## Common error messages

The following table lists common errors that can occur during connector configuration or crawling, along with possible reasons.

| Step | Error message | Possible reason |
|------|---------------|----------------|
| **Connection settings** | The request is malformed or incorrect. | Incorrect Jira site URL. |
| **Connection settings** | Unable to reach the Jira cloud service for your Jira site. | Incorrect Jira site URL. |
| **Connection settings** | The client doesn't have permission to perform the action. | Invalid API token provided for Basic authentication. |
| **Connection settings** | "Something went wrong" error in OAuth pop-up window. | The scopes granted to the OAuth app don't match. The mismatched scopes are listed in the pop-up window. |
| **Crawl time (post-configuration)** | Can't authenticate with the data source. Verify the credentials associated with this data source are correct. | The user doesn't have one or more permissions required to crawl Jira. |
| **Crawl time (post-configuration)** | You don't have permission to access this data source. You can contact the owner of this data source to request permission. | If using OAuth, the app scopes might have changed, or the app might have expired or been deleted.<br>If using Basic authentication, the API token might have expired or been deleted. |
| **Crawl time (post-configuration)** | Error code: 1003 - You don't have permission to access this data source.<br>Detailed error code: 7612 | The crawl account doesn't have **Browse projects** permission for the listed project (shown in the **Item ID** column). |

## Issue resolution steps

Use the following steps to help resolve issues:

- Verify that the Jira Cloud instance URL is correct and resolves to your Jira dashboard.
- Confirm that the service account has the required permissions:
  - **Browse projects** (required)
  - Issue-level security and user/group browsing permissions for security trimming (optional)
- For OAuth issues:
  - Check that all required scopes are granted.
  - Verify that the callback URL is correct: `https://gcs.office.com/v1.0/admin/oauth/callback`
- For Basic authentication:
  - Regenerate the API token if it expired or was deleted.
  - Confirm that the username and token match the Jira account used for crawling.

## Scenario-specific troubleshooting guides

If the error table and resolution steps above do not resolve your issue, use the appropriate scenario guide below for step-by-step troubleshooting and instructions on what to collect before contacting Microsoft support.

- [Project or Issue Not Crawled - Jira Cloud](Project-or-Issue-Not-Crawled-%2D-Jira-Cloud.md)
- [Issue Indexed but Not Searchable Due to Permissions - Jira Cloud](Issue-Indexed-but-Not-Searchable-Due-to-Permissions-%2D-Jira-Cloud.md)
- [Oversharing - Jira Cloud](Oversharing-%2D-Jira-Cloud.md)
- [Error Code 1010 - External Group Quota - Jira Cloud](Error-Code-1010-%2D-External-Group-Quota-%2D-Jira-Cloud.md)
- [Issue-Level Security Not Working - Jira Cloud](Issue-Level-Security-Not-Working-%2D-Jira-Cloud.md)

## Minimum information to collect before opening a support ticket

Regardless of the scenario, collect the following information before contacting Microsoft support:

- Jira site URL (for example, `https://contoso.atlassian.net`)
- Connection name and connection ID from the Microsoft 365 admin center
- Affected user `accountId`
- Affected issue ID
- Affected project ID
- Time of the latest reproduction in UTC
- Screenshots of the relevant Jira settings and the Copilot or Index Browser result

## How to collect Jira identifiers

### Project ID

If the project ID isn't visible in the Jira UI, open the following URL while signed in:

`https://<your-jira-site>.atlassian.net/rest/api/3/project/<projectKey>`

Record the returned `id`, `key`, and `name`.

### Issue ID

If you only know the issue key, open:

`https://<your-jira-site>.atlassian.net/rest/api/3/issue/<issueKey>?fields=id,key,project`

Record the top-level issue `id`, the issue `key`, and the `project.id`.

### Project role ID

If the incident involves role-based permissions, open:

`https://<your-jira-site>.atlassian.net/rest/api/3/project/<projectKey>/role`

This returns role names mapped to URLs. The numeric value at the end of each role URL is the `roleId`.

### Permission scheme ID

If the incident involves project permissions, open:

`https://<your-jira-site>.atlassian.net/rest/api/2/project/<projectKey>/permissionscheme?expand=user`

Record the permission scheme `id` and the `BROWSE_PROJECTS` entries.

### Issue security scheme ID

If the incident involves issue-level security, open:

`https://<your-jira-site>.atlassian.net/rest/api/2/project/<projectKey>/issuesecuritylevelscheme`

Record the scheme `id` and all configured issue security levels.

## Screenshot checklist

Depending on the incident, attach screenshots of the following:

- The Jira issue page showing the issue key
- The Jira project settings page
- Project permissions or Permission helper output
- Issue security configuration
- The affected user's membership in groups or project roles
- Index Browser result showing access granted or access denied
- The Copilot result, including the time and query text

## Related content

- [Jira Cloud connector overview](jira-cloud-overview.md)
- [Set up the Jira Cloud service for connector ingestion](jira-cloud-admin-setup.md)
- [Deploy the Jira Cloud connector](jira-cloud-deployment.md)
