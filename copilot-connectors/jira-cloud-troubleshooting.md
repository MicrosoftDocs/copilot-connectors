---
title: "Troubleshoot issues with the Jira Cloud connector"
description: "Learn how to troubleshoot common issues with the Jira Cloud Microsoft 365 Copilot connector, including error messages, possible causes, and resolution steps."
ms.author: lauragra
author: lauragra
manager: calvind
ms.topic: troubleshooting
ms.service: copilot-connectors
ms.date: 04/14/2026
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

## Scenario-specific troubleshooting steps

### Project or issue not crawled - Jira Cloud

Use this scenario when a Jira project or issue doesn't appear in the connector content.

- Confirm the project is included in the connector configuration in the Microsoft 365 admin center.
- Verify that the connector account can open the project and the issue in Jira.
- Confirm that the connector account has **Browse projects** permission by using Permission helper.  
  ![JiraPermissionHelper](copilot-connectors/media/JiraPermissionHelper.png)
- If only one issue is missing, verify whether the issue has a different issue-level security configuration.
- Confirm whether the issue was recently created and might still be pending the next crawl cycle.

### Issue indexed but not searchable due to permissions - Jira Cloud

Use this scenario when an issue has been crawled but isn't returned in Copilot or Microsoft Search.

- Confirm that the issue is present in the index by using Index Browser.
- Use Jira Permission helper to verify how access is granted to the affected user.  
  ![JiraPermissionHelper](copilot-connectors/media/JiraPermissionHelper.png)
- Review the project permission scheme and identify the group or role that grants access.
- If access is granted through a project role, collect the role identifier.
- Compare the Jira permission result with the Index Browser result to identify mismatches.

### Issue-level security not working - Jira Cloud

Use this scenario when issue-level security isn't enforced as expected.

- Confirm that the issue has an assigned issue security level.  
  ![IssueLevelSecurity](copilot-connectors/media/IssueLevelSecurity.png)
- Capture the issue security scheme and the configured security levels.  
  ![IssueLevelSecurityScheme](copilot-connectors/media/IssueLevelSecurityScheme.png)
- Compare the expected Jira access with the Index Browser access result.

[!Note]: Configurations that rely on **Group custom field values** aren't currently supported.

### Oversharing - Jira Cloud

Use this scenario when a user can access Jira content they shouldn't have access to.

If Index Browser shows `access denied`:

- Update the issue content, for example by editing the summary or description.
- Wait for the next crawl and propagation cycle.
- Test access again for the same user.
- Validate the behavior with another issue the user hasn't previously accessed.

If Index Browser shows `access granted`:

- Confirm that the user can't open the issue in Jira.
- Capture the Jira permission configuration that should deny access.
- Capture Index Browser showing `access granted` for the affected user.

### Error code 1010 - external group quota - Jira Cloud

Use this scenario when error code `1010` indicates that the tenant has reached the external group quota.

`External groups per Microsoft 365 tenant has reached the 100,000 quota.`

- Request a quota increase for external groups in the Microsoft 365 tenant.

## Information to collect to open a support ticket

Regardless of the scenario, collect the following information before you contact Microsoft support:

- Jira site URL (for example, `https://contoso.atlassian.net`)
- Connection name and connection ID from the Microsoft 365 admin center
- Affected user `accountId`
- Affected issue ID
- Affected project ID
- Time of the latest reproduction in UTC
- Screenshots of the relevant Jira settings and the Copilot or Index Browser result

### Collect Jira identifiers

#### Project ID

If the project ID isn't visible in the Jira UI, open the following URL while signed in:

`https://<your-jira-site>.atlassian.net/rest/api/3/project/<projectKey>`

Record the returned `id`, `key`, and `name`.

#### Issue ID

If you only know the issue key, open:

`https://<your-jira-site>.atlassian.net/rest/api/3/issue/<issueKey>?fields=id,key,project`

Record the top-level issue `id`, the issue `key`, and the `project.id`.

#### Project role ID

If the incident involves role-based permissions, open:

`https://<your-jira-site>.atlassian.net/rest/api/3/project/<projectKey>/role`

This request returns role names mapped to URLs. The numeric value at the end of each role URL is the `roleId`.

#### Permission scheme ID

If the incident involves project permissions, open:

`https://<your-jira-site>.atlassian.net/rest/api/2/project/<projectKey>/permissionscheme?expand=user`

Record the permission scheme `id` and the `BROWSE_PROJECTS` entries.

#### Issue security scheme ID

If the incident involves issue-level security, open:

`https://<your-jira-site>.atlassian.net/rest/api/2/project/<projectKey>/issuesecuritylevelscheme`

Record the scheme `id` and all configured issue security levels.

### Screenshot checklist

Depending on the incident, attach screenshots of the following items:

- The Jira issue page that shows the issue key
- The Jira project settings page
- Project permissions or Permission helper output
- Issue security configuration
- The affected user's membership in groups or project roles
- Index Browser result that shows access granted or access denied
- The Copilot result, including the time and query text

## Related content

- [Jira Cloud connector overview](jira-cloud-overview.md)
- [Set up the Jira Cloud service for connector ingestion](jira-cloud-admin-setup.md)
- [Deploy the Jira Cloud connector](jira-cloud-deployment.md)
