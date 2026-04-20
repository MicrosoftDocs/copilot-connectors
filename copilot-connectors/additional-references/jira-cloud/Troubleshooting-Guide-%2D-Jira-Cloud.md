[[_TOC_]]

# Jira Cloud Troubleshooting Guide

Use this guide to troubleshoot Jira Cloud content access or crawl issues in Microsoft 365, Microsoft Search, Copilot, or Index Browser.

The goal of each troubleshooting flow is to:

- Help you verify the relevant Jira Cloud configuration step by step.
- Help you collect the identifiers and screenshots needed for investigation.

## Use the right scenario guide

- [Project or Issue Not Crawled - Jira Cloud](Project-or-Issue-Not-Crawled-%2D-Jira-Cloud.md)
- [Issue Indexed but Not Searchable Due to Permissions - Jira Cloud](Issue-Indexed-but-Not-Searchable-Due-to-Permissions-%2D-Jira-Cloud.md)
- [Oversharing - Jira Cloud](Oversharing-%2D-Jira-Cloud.md)
- [Error Code 1010 - External Group Quota - Jira Cloud](Error-Code-1010-%2D-External-Group-Quota-%2D-Jira-Cloud.md)
- [Issue Level Security Not Working - Jira Cloud](Issue-Level-Security-Not-Working-%2D-Jira-Cloud.md)

## Minimum information to collect for any Jira Cloud incident

Before opening a ticket, collect the following:

- Jira site URL, for example `https://contoso.atlassian.net`
- Connection name and connection ID in Microsoft 365 admin center
- Affected user AccoutnId
- Affected issue id
- Affected project id
- Time of the latest reproduction in UTC
- Screenshots of the relevant Jira settings page and the Copilot or Index Browser result

## How to collect the most useful Jira identifiers

### Project ID

If you cannot find the project ID in the Jira UI, open this URL while signed in:

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

Depending on the incident, attach screenshots of:

- The Jira issue page showing the issue key
- The Jira project settings page
- Project permissions or Permission helper output
- Issue security configuration
- The affected user's membership in groups or project roles
- Index Browser result showing access granted or access denied
- The Copilot result, including time and query text

## Important note

These troubleshooting guides intentionally avoid connector implementation details. They focus only on what you can validate in Jira Cloud and what you should collect before opening a ticket.
