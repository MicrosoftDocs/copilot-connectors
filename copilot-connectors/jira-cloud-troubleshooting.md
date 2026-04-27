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

# Jira Cloud connector troubleshooting

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

### Project or issue not crawled - Jira Cloud

Use this scenario when a Jira project or issue doesn't appear in the connector content set.

1. Confirm the project is in scope.
   - Open the Jira connector in the Microsoft 365 admin center.
   - Go to `Edit -> Content` and expand **Choose projects and filter data**.
   - Verify whether the connection crawls the entire site or specific projects.
   - Capture a screenshot of the configuration.

2. Verify that the connector account can access the project and issue in Jira.
   - Sign in using the connector authentication account.
   - Open the project and capture a screenshot.
   - Open the issue directly and confirm it loads successfully.
   - If the issue cannot be opened, this indicates a Jira permissions issue.

3. Confirm project permissions using Permission helper.
   - Navigate to `Project settings -> Permissions`.
   - Open **Permission helper**.
   - Select the connector account and an issue.
   - Select **Browse Projects** and submit.
   - Capture screenshots of the result.
 :::image type="content" source="media/jira-cloud/jirapermissionhelper.png" alt-text="Screenshot of a Jira permission helper." lightbox="media/jira-cloud/jirapermissionhelper.png":::

4. If only one issue is missing, check issue-level restrictions.
   - Open the issue and verify whether a different security level is applied.
   - Capture screenshots of the issue details and security configuration if applicable.

5. Confirm whether the issue is pending ingestion.
   - Record the issue creation time.
   - Compare it with the expected crawl timing.

### Issue indexed but not searchable due to permissions - Jira Cloud

Use this scenario when an issue has been crawled and indexed, but isn't returned due to access issues.

1. Confirm that the issue is present in the index.
   - Open Index Browser and search using the exact issue ID.
   - Capture screenshots showing the item and access result.

2. Verify access using Jira Permission helper.
   - Navigate to `Project settings -> Permissions`.
   - Open **Permission helper**.
   - Select the affected user and issue.
   - Select **Browse Projects** and submit.
   - Capture screenshots showing the result and granting group or role.
 :::image type="content" source="media/jira-cloud/jirapermissionhelper.png" alt-text="Screenshot of a Jira permission helper." lightbox="media/jira-cloud/jirapermissionhelper.png":::

3. Review the project permission scheme.
   - Capture entries related to issue visibility.
   - Record group names and project roles.

4. If access is role-based, collect role details.
   - Open:
     `https://<your-jira-site>.atlassian.net/rest/api/3/project/<projectKey>/role`
   - Record the role URL and `roleId`.

5. Compare Jira access with Index Browser.
   - Document whether access is granted or denied in both.
   - Identify mismatches between expected and actual access.

### Issue-level security not working - Jira Cloud

Use this scenario when issue-level security isn't enforced as expected.

1. Confirm that an issue security level is assigned.
   - Open the issue and capture the assigned security level.
 :::image type="content" source="media/jira-cloud/issuelevelsecurity.png" alt-text="Screenshot of an issue level security." lightbox="media/jira-cloud/issuelevelsecurity.png":::

2. Capture the issue security scheme.
   - Open the issue configuration and navigate to security settings.
   - Capture the scheme name, levels, and associated rules.
 :::image type="content" source="media/jira-cloud/issuelevelsecurityscheme.png" alt-text="Screenshot of an issue level security scheme." lightbox="media/jira-cloud/issuelevelsecurityscheme.png":::

3. Compare Jira security with Index Browser behavior.
   - Capture screenshots showing access results for the affected user.

**Note:** Configurations that rely on **Group custom field values** aren't currently supported.

### Oversharing - Jira Cloud

Use this scenario when a user can access content they shouldn't have access to.

If Index Browser shows `access denied`:

1. Confirm whether access was recently removed in Jira.
2. Update the issue content, such as editing the summary or description.
3. Wait for the next crawl and propagation.
4. Test again using the same user.
5. Test another issue the user hasn't accessed before.

If Index Browser shows `access granted`:

1. Confirm that the user can't open the issue in Jira.
2. Capture the Jira permission configuration that should deny access.
3. Capture Index Browser showing `access granted`.

### Error code 1010 - external group quota - Jira Cloud

Use this scenario when error code `1010` indicates the tenant has reached the external group quota.

`External groups per Microsoft 365 tenant has reached the 100,000 quota.`

This typically occurs when a large number of external groups are created during ACL ingestion.

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
