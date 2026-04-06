# Credly Microsoft 365 Copilot connector overview

The **Credly Microsoft 365 Copilot connector** is a [people data connector](https://aka.ms/peopleconnectors) that indexes digital credential data from your organization's Credly platform into Microsoft 365. It ingests verified digital badges, awards, and certifications from Credly and enriches user profiles so that credential information is accessible across Microsoft 365 experiences, including Microsoft 365 Copilot and profile cards. By integrating Credly's digital credentials into the Microsoft Graph, the connector provides a unified, up-to-date view of employees' achievements within Microsoft 365.

> [!NOTE]
> The Credly connector is currently released as a Preview feature. Its functionality and requirements may change in future updates.

## Capabilities

The Credly connector provides several key features for integrating digital credential data into Microsoft 365.

### Credential indexing

The connector automatically ingests key information from your organization's Credly platform, including digital badge names, descriptions, issuing organization, issue dates, and other relevant metadata, into each user's Microsoft 365 profile. Employees' verified awards and certifications are represented in Microsoft 365 without manual data entry or duplication. The authoritative data remains in Credly.

### Enhanced Copilot responses

By incorporating Credly badge data, the connector enriches Microsoft 365 Copilot. End users can ask natural-language questions about colleagues' qualifications and recent achievements, and Copilot provides intelligent answers based on their Credly certifications and awards. For example, users might ask *"What certifications does Jane Doe have?"* or *"Who on my team has a project management badge?"*, and Copilot can respond with information drawn from Credly.

### Periodic synchronization

The connector keeps badge and certification information up to date. It performs incremental crawls approximately every day and full crawls weekly by default, so newly earned badges or updates in Credly are reflected in Microsoft 365. This frequent sync ensures that Copilot and profile data stay current as users earn new credentials.

### Profile integration

Credly badges and certifications appear directly on users' Microsoft 365 profile cards in a dedicated **Awards and Certifications** section. Each badge is displayed with its title and icon, and users can select a badge to view more details on Credly's site. This integration provides at-a-glance visibility of a person's accomplishments during everyday collaboration, for example, when hovering over a colleague's name in Outlook or the Copilot app.

### Automated identity matching

The connector maps each Credly badge to the correct user in your organization by matching the badge owner's email address with their Microsoft Entra ID account. Work email addresses in Credly must match the user's UPN or primary SMTP address in Entra ID for the credentials to be attributed to the right person.

> [!NOTE]
> When Copilot cites information from a user's profile (including Credly-provided details), the source is listed as office.com rather than "Credly." Microsoft 365 aggregates profile data from multiple sources (for example, a job title might come from Microsoft Entra ID while a certification comes from Credly) and attributes the response to the unified profile endpoint.

## Limitations

Before deploying the Credly connector, be aware of the following constraints in the current preview release.

- **Awards and certifications only** &mdash; The connector ingests only the award and certification (badge) information from Credly that users have chosen to publicly accept or share on their profiles. Other content from the Credly platform, such as unaccepted (private) badges, badge evidence, related skills, user social profiles, or non-credential data, isn't downloaded or indexed.
- **Access permissions** &mdash; All imported badge data is visible to all users in your organization by default. Granular, per-user or group filtering of Credly data isn't yet available. If a user has a profile in your directory, their Credly badges (if mapped) are visible on their profile to colleagues who can normally see their profile. Existing information barriers or privacy settings that prevent certain users from viewing others' profiles still apply.
- **Identity matching requirements** &mdash; The connector relies on email address matching for identity resolution. If a badge recipient's email in Credly doesn't correspond to any user in Microsoft Entra ID (for example, a personal email or misspelled address), those badges can't be mapped to a Microsoft 365 user profile and are skipped during indexing.
- **Fixed schema** &mdash; The connector uses a predefined set of profile attributes in Microsoft Graph to store badge data (specifically, the "Awards" and "Certifications" properties in the user profile schema). Administrators can't add or remove properties in the connector's content schema in this release.
- **Active users only** &mdash; The connector only indexes and displays credentials for active users in your directory. If a user leaves the organization or is marked as inactive, their badges and certifications from Credly are filtered out. Connector-provided data remains in a user's profile as long as the user is active and licensed in your Microsoft 365 tenant.
- **One Credly organization per connection** &mdash; The connector can be configured for a single Credly Organization ID at a time. If your company manages multiple separate Credly organizations (for example, due to multiple subsidiaries), you need to set up a separate connector instance for each Credly Organization ID.

## Related content

- [Deploy the Credly connector](credly-connector-deployment-guide.md)
- [Troubleshoot the Credly connector](credly-connector-troubleshoot.md)
- [Microsoft 365 Copilot connectors for people data](https://learn.microsoft.com/en-us/graph/peopleconnectors?source=recommendations)
- [Microsoft 365 Copilot connectors overview](https://learn.microsoft.com/en-us/microsoftsearch/connectors-overview?source=recommendations)
