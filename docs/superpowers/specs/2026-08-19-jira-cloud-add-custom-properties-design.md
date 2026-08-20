# Jira Cloud: Add custom properties documentation design

## Scope

Add an English-language **Add custom properties** section to `copilot-connectors/jira-cloud-deployment.md` immediately before **Manage customized properties**.

## Content design

The section guides an administrator through five ordered steps. Each step names the relevant UI control and explains the purpose or expected outcome:

1. Open the **Content** tab to access content and property settings.
2. Select **Add property** to begin adding a Jira field.
3. Select the field to include from the available fields.
4. Select the schema options that determine whether the field is searchable, queryable, retrievable, or refinable.
5. Review the configuration and select **Save**.

Each numbered step is followed by its matching screenshot, from `media/jira-cloud/addcustomproperty1.png` through `media/jira-cloud/addcustomproperty5.png`. Image alt text describes the visible action or state for accessibility.

## Style and validation

Use Microsoft Learn Markdown conventions already present in the article, sentence-style headings, bold UI labels, concise imperative language, and repository-relative image paths. Verify heading placement, ordered-list rendering, image references, and the final diff.
