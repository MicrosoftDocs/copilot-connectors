# Jira Cloud custom fields table design

## Scope

Update the **Manage properties** section of `copilot-connectors/jira-cloud-deployment.md` to distinguish supported custom fields from the existing table of default properties.

## Content design

Keep the existing default-properties table unchanged. Immediately below it, add a sentence explaining that the Jira Cloud Copilot connector also supports the following custom fields, followed by a separate two-column table with **Custom field** and **Attributes** columns.

Add these 12 rows in the order used by ADO Work Item 7756256:

| Custom field | Attributes |
| :--- | :--- |
| Sprint | Query, Retrieve, Refine (optional) |
| Fix Version | Query, Retrieve |
| Customer Name/s | Query, Retrieve |
| Support Owner | Query, Retrieve |
| Affects Version/s | Query, Retrieve |
| SLA | Query, Retrieve |
| Time to resolution | Query, Retrieve |
| Region | Query, Retrieve |
| First Response | Query, Retrieve |
| Request Type | Query, Retrieve |
| Approver | Query, Retrieve |
| Resolution | Query, Retrieve |

Don't include `LinkedIssues / IssueLinks`, which is struck through in the ADO source. Don't publish internal implementation Work Item IDs, pull request IDs, or GCA version details.

## Terminology and validation

Normalize the ADO schema terms to match the existing public table: `Queryable` becomes `Query`, `Retrievable` becomes `Retrieve`, and `Refinable (optional)` becomes `Refine (optional)`.

Verify that the existing default table is unchanged, the new table contains exactly 12 unique custom fields in source order, `LinkedIssues` and `IssueLinks` don't appear, every row has two columns, and Markdown whitespace validation passes.
