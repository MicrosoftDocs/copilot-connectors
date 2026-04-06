# Troubleshoot the Credly Microsoft 365 Copilot connector

This article helps Microsoft 365 administrators diagnose and resolve common issues with the Credly Microsoft 365 Copilot connector.

## Badges not appearing on user profiles

If Credly badges aren't showing on a user's Microsoft 365 profile card, check the following:

- **Email mismatch** &mdash; The connector relies on email address matching for identity resolution. The badge recipient's email in Credly must match their UPN or primary SMTP address in Microsoft Entra ID. If the user registered in Credly with a personal email or a misspelled address, their badges can't be mapped and are skipped during indexing. Verify that employees use their organization email in Credly.
- **Badge not accepted** &mdash; The connector only ingests badges that users have publicly accepted or shared on their Credly profiles. Unaccepted (private) badges aren't downloaded or indexed.
- **Inactive user** &mdash; The connector only indexes credentials for active users in your directory. If a user has left the organization or is marked as inactive, their Credly badges are filtered out.
- **Sync not completed** &mdash; After initial setup, wait for the first crawl cycle to complete. Incremental crawls run approximately every day and full crawls run weekly by default. Check the connector status on the **Connectors** page in the Microsoft 365 admin center to confirm the sync has completed.

## Copilot not returning Credly data

If Microsoft 365 Copilot doesn't surface badge or certification information when users ask questions:

- **Sync delay** &mdash; Newly earned badges require at least one successful crawl cycle before they're available to Copilot. Verify that the connector status shows a completed sync on the **Connectors** page in the Microsoft 365 admin center.
- **Citation source** &mdash; When Copilot cites information from a user's profile (including Credly-provided details), the source is listed as office.com rather than "Credly." Microsoft 365 aggregates profile data from multiple sources and attributes the response to the unified profile endpoint. This is expected behavior.

## Connection setup failures

If the connector fails during setup in the Microsoft 365 admin center:

- **Invalid Organization ID** &mdash; The Credly Organization ID must be a valid GUID obtained from the Credly Developers portal. Verify the format and value.
- **Expired or incorrect credentials** &mdash; Confirm that the Client ID and Client Secret are correct and haven't expired. If the Client Secret wasn't saved during creation, generate a new OAuth application in the Credly Developers portal.
- **Wrong API endpoint** &mdash; Verify the base URL for the Credly OAuth 2.0 token service. For production accounts, use `https://www.credly.com`. Sandbox environments use a different URL.

## Multiple Credly organizations

The connector can be configured for a single Credly Organization ID at a time. If your company manages multiple separate Credly organizations (for example, due to multiple subsidiaries), set up a separate connector instance for each Credly Organization ID in the Microsoft 365 admin center.

## Schema and customization limitations

The Credly connector uses a predefined set of profile attributes in Microsoft Graph (specifically the "Awards" and "Certifications" properties). Administrators can't add or remove properties in the connector's content schema in this release. All ingested badges are mapped to the existing profile fields.

## Related content

- [Credly connector overview](credly-connector-overview.md)
- [Deploy the Credly connector](credly-connector-deployment-guide.md)
- [Monitor Microsoft 365 Copilot connectors](https://learn.microsoft.com/en-us/microsoftsearch/manage-connector?source=recommendations)
