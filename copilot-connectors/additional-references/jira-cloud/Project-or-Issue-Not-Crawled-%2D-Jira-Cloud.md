[[_TOC_]]

# Project or Issue Not Crawled - Jira Cloud

Use this guide when a Jira project or issue does not appear in the connector content set.

Follow the steps in this document to troubleshoot the issue and collect the information required for Microsoft support  if the issue is not resolved.

## Typical symptoms

- A project is expected to appear in Copilot, but none of its issues appear in search or Copilot.
- Some projects are crawled, but one specific project is missing.
- Most issues in a project are present, but one specific issue is missing.

## Step-by-step checks

### Step 1. Confirm the project is in scope

Open the Jira connector in the Microsoft 365 admin center, go to `Edit -> Content`, expand `Choose projects and filter data`, and confirm whether:

- The connection is configured to crawl the entire Jira site, or
- The project is explicitly included in the project list.

Save a screenshot of the connection configuration showing the selected projects.

### Step 2. Check whether the connector account can open the issue in Jira

Sign in as the connector authentication account, or use an account with the same Jira permissions as the connector creation account, then:

1. Open the project in Jira and save a screenshot.
2. Open the issue directly by issue key and confirm whether the issue page loads successfully. Save a screenshot.

If the issue cannot be opened in Jira, the root cause is a Jira permissions issue rather than a Microsoft Search ingestion issue.

### Step 3. Check project access for the connector account

Confirm that the connector creation account has the permissions required to browse the project and view issues.

Open the project and navigate to:

1. `Project settings -> Permissions`
2. Click `Permission helper` in the upper-right corner.
3. Select the user who authenticated the connection.
4. Select an issue in the project.
5. Select `Browse Projects` and submit.
6. Save screenshots of the result.
![JiraPermissionHelper](./JiraPermissionHelper.png)

Also collect:

- The connector creation account `accountId`: open the user menu in the upper-right corner, select `Profile`, and record the profile URL.
![jiraUserProfile](./JiraUserProfile.png)

### Step 4. If only one issue is missing, check issue-level restrictions

Open the issue and verify whether it has a security setting that differs from the rest of the project.

Collect:

- A screenshot of the issue details panel showing the security level, if present
- A screenshot of the project issue security configuration, if issue security is enabled

### Step 5. Confirm that the issue is not waiting for an initial crawl

Collect:

- The issue creation time
- The time at which the issue was expected to become searchable

This helps determine whether the issue was never discovered or is simply pending the next crawl cycle.

## Required screenshots

- Connector configuration showing project selection
- Jira project page
- Jira issue page or access error page
- Project permissions page
- Issue security field, if applicable

## Suggested incident summary template

When creating a ticket, include:

- Jira site URL:
- Connection ID:
- Project ID: open `https://<your-jira-site>.atlassian.net/rest/api/3/project/<projectKey>`
- Issue ID: open `https://<your-jira-site>.atlassian.net/rest/api/3/issue/<issueKey>?fields=id,key,project`
- Connection creation used auth account:
- Repro time:
- Can the connector account open the project in Jira:
- Can the connector account open the issue in Jira:
- Attached screenshots:
