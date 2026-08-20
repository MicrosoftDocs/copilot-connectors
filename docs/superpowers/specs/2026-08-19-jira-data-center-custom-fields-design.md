# Jira Data Center custom fields documentation design

## Scope

Update the **Manage properties** section of `copilot-connectors/jira-data-center-deployment.md` with two additions:

1. A separate table of supported custom fields, recommended schema attributes, and the earliest supporting Graph Connector Agent (GCA) version.
2. A complete **Add custom properties** procedure that reuses the five existing Jira screenshots.

Keep the existing default-properties table and all later sections unchanged.

## Custom fields table

Immediately after the existing default-properties table, explain that the Jira Data Center Copilot connector also supports the following custom fields. Add this three-column table in the source order from ADO Work Item 7756256:

| Custom field | Attributes (recommended) | Earliest supported GCA version |
| :--- | :--- | :--- |
| Sprint | Query, Retrieve, Refine (optional) | 3.1.23.0 |
| Fix Version | Query, Retrieve | 3.1.23.0 |
| Customer Name/s | Query, Retrieve | 4.0.0.0 |
| Support Owner | Query, Retrieve | 4.0.0.0 |
| Affects Version/s | Query, Retrieve | 4.0.0.0 |
| SLA | Query, Retrieve | 4.0.0.0 |
| Time to resolution | Query, Retrieve | 4.0.0.0 |
| Region | Query, Retrieve | 4.0.0.0 |
| First Response | Query, Retrieve | 4.0.0.0 |
| Request Type | Query, Retrieve | 4.0.0.0 |
| Approver | Query, Retrieve | 4.0.0.0 |
| Resolution | Query, Retrieve | 4.0.3.0 |

Don't include the struck-through `LinkedIssues / IssueLinks` row. Don't publish ADO Work Item IDs, pull request IDs, or the internal ECS status associated with Resolution.

## Add custom properties procedure

Immediately after the custom-fields table and before **Customize sync intervals**, add a `#### Add custom properties` subsection. Use Jira Data Center wording and these five ordered steps:

1. Select the **Content** tab to open the content and property settings.
2. In the properties section, select **Add property**.
3. From the available fields, select the field to add.
4. Select the appropriate schema options, which determine whether the field is searchable, queryable, retrievable, or refinable.
5. Review the property configuration and select **Save**.

Place the matching screenshot after each step, from `media/jira-cloud/addcustomproperty1.png` through `media/jira-cloud/addcustomproperty5.png`. Use standard Markdown lightbox image syntax so the screenshots render in both ordinary Markdown previews and Microsoft Learn. Alt text must describe the visible action or state.

## Terminology and validation

Normalize the ADO schema terms to the article's public terminology: `Queryable` becomes `Query`, `Retrievable` becomes `Retrieve`, and `Refinable (optional)` becomes `Refine (optional)`.

Verify that:

- The existing default table is unchanged.
- The new table has exactly 12 unique three-column data rows in source order.
- The version distribution is two rows at 3.1.23.0, nine rows at 4.0.0.0, and one row at 4.0.3.0.
- `LinkedIssues`, `IssueLinks`, ADO/PR IDs, and the ECS status aren't published.
- The procedure has exactly five ordered steps and five matching image references.
- The custom-fields table and procedure appear before **Customize sync intervals**.
- Markdown whitespace validation passes.
