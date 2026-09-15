---
title: "Deploy the Galileo by The Josh Bersin Company connector"
ms.author: xupzhou
author: xupzhou
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 09/11/2026
ms.localizationpriority: Medium
description: "Deploy, validate, and monitor the Galileo by The Josh Bersin Company Microsoft 365 Copilot connector."
---

# Deploy the Galileo by The Josh Bersin Company connector

The Galileo by The Josh Bersin Company Microsoft 365 Copilot connector indexes The Josh Bersin Company research library in Microsoft Graph. After deployment, authorized users can discover research in Microsoft 365 Copilot, Copilot Search, and Microsoft Search, and administrators can use the connection as a knowledge source for declarative agents.

This article describes how to configure, deploy, and validate the connector.

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- **Josh Bersin account**: You need a valid Josh Bersin license to access content. Contact The Josh Bersin Company to request the credentials required for access.
- **Service account**: You must be an admin for your organization's Microsoft 365 tenant.

For detailed setup requirements, see [Set up Galileo by The Josh Bersin Company for connector ingestion](galileo-admin-setup.md).

## Deploy the connector

To add the Galileo by The Josh Bersin Company connector for your organization:

1. In the [Microsoft 365 admin center](https://admin.microsoft.com/), in the left pane, select **Copilot** > **Connectors**.
1. Select the **Gallery** tab.
1. From the list of available connectors, select the Galileo connector.

> [!NOTE]
> Microsoft controls the connector tile name and logo. During a branding transition, the tile might appear as **JoshBersin** instead of **Galileo by The Josh Bersin Company**.

### Set display name

Enter the following display name exactly:

`Galileo by The Josh Bersin Company`

The display name helps users recognize Galileo as a trusted source in Copilot responses. Using the recommended name also makes support and agent configuration more consistent.

### Set instance URL

The Galileo data API endpoint is prefilled in the setup experience. Don't change this value unless your Josh Bersin Company onboarding contact directs you to do so.

### Choose authentication type

1. Under **Authentication**, select **OAuth 2.0 Client Credentials**.
1. Enter the client ID from your onboarding package.
1. Enter the client secret retrieved from the secure, expiring link.
1. Confirm that both credentials validate successfully.

If validation fails, reenter the values exactly as provided. If the secure link expired or the secret was revoked, request a replacement from your Josh Bersin Company contact.

### Roll out

1. Turn on **Rollout to limited audience**.
1. Select the Galileo access group created during setup.
1. Verify that the group contains only the intended pilot users.

> [!IMPORTANT]
> The connector rollout audience is the maximum audience for Galileo content in Microsoft 365. Share the declarative agents with this same group. Users outside this audience can't retrieve grounded Galileo results even if an agent is shared with them.

### Review and create the connection

1. Review Microsoft's data notice.
1. Select the acknowledgment.
1. Review the display name, endpoint, authentication, and rollout audience.
1. Select **Create**.

The connector starts syncing Galileo content into your tenant's index.

The following table lists the default values that are set.

| Category | Default value |
| --- | --- |
| Audience | Limited to the selected Galileo access group. |
| Content | Galileo research content and the default properties listed in [Manage properties](#manage-properties). |
| Sync | Full refresh runs every day. |

To customize these values, select **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create the connection, you can review its status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default properties for the Galileo connector. To customize settings, select **Custom setup** on the connector page in the Microsoft 365 admin center.

### Customize content settings

You can customize the properties that Galileo content uses in Microsoft 365 experiences.

#### Manage properties

To add or remove available properties from the Galileo connector, assign a schema to a property by defining whether the property is searchable, queryable, retrievable, or refinable. You can also change a semantic label or add an alias. The following properties are indexed by default.

| Properties | Semantic Label | Description | Schema |
| --- | --- | --- | --- |
| Content | CONTENT | Main body content of the item. | Search |
| CreatedTime | Created date time | Date and time when the item was created. | Query, Retrieve |
| FileExtension | File extension | File type extension of the source item. | Query, Retrieve |
| FileName | File name | Name of the source file. | Query, Retrieve, Search |
| IconLink | IconUrl | URL of the icon associated with the item. | Retrieve |
| Id |  | Unique identifier of the item in the Galileo data source. | Query, Retrieve |
| Industries |  | Industries associated with the item. | Query, Refine, Retrieve, Search |
| Link | url | URL that opens the item in the Galileo data source. | Retrieve |
| ModifiedTime | Last modified date time | Date and time when the item was last modified. | Query, Retrieve |
| Name | Title | Title of the item displayed in Copilot and search experiences. | Query, Retrieve, Search |
| Size |  | Size of the source item in bytes. |  |
| Topics | tags | HR topics covered by the document. | Query, Refine, Retrieve, Search |

Select **Preview results** to verify sample values for the selected properties before you create the connection.

> [!NOTE]
> Property selections and schema attributes affect how Galileo content can be searched, queried, returned, and refined in Microsoft 365 experiences. Review the schema before deployment to make sure that required properties remain selected.

### Customize sync intervals

By default, a full refresh runs every day. You can change the **Recurrence** setting to use another frequency, such as every second week.

For more information, see [Guidelines for crawl settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Verify the connection and initial index

1. In the Microsoft 365 admin center, go to **Copilot** > **Connectors**.
1. Open **Your connections**.
1. Locate the `Galileo by Josh Bersin` connection.
1. Confirm that the connection state changes to **Ready** and the type is **Synced**.
1. Confirm that the last sync time updates as crawls complete.

The first full index typically takes approximately two to three hours. The connection detail pane includes information such as:

- Number of indexed items.
- Registered schema and search properties.
- Last synchronization time.
- Daily full-crawl schedule.
- Item errors.
- An option to export the connection configuration as JSON.

A small number of item errors can occur during normal synchronization. The Josh Bersin Company monitors content-side issues. Investigate if the error count rises sharply or the connection state changes to **Failed**.

## Validate the deployment

Wait for the initial index to finish, and then have a licensed pilot user who belongs to the Galileo access group complete the following tests.

| Experience | Test | Expected result |
| --- | --- | --- |
| Microsoft Search | Search for a distinctive phrase such as `systemic HR maturity`. | Galileo items appear with source attribution for the connection. |
| Microsoft 365 Copilot Chat | Ask: `What does The Josh Bersin Company research say about skills-based organizations?` | The answer uses Galileo research and includes citations. |
| Microsoft 365 Copilot Chat | Ask: `Summarize current best practices for talent acquisition according to Bersin research.` | The answer is grounded in Galileo content and its citation links open successfully. |

If a test fails, verify:

- The connection is in the **Ready** state.
- The initial index is complete.
- The test user has a Microsoft 365 Copilot license.
- The test user is a member of the Galileo access group.
- The connector is configured with that group as its rollout audience.
- The network allows access to the citation content domain.

## Monitor ongoing synchronization

Galileo performs a daily full crawl to retrieve new and updated content. Administrators should periodically review:

- Connection state.
- Last successful sync.
- Indexed item count.
- Item-error trend.
- Pilot group membership.

If expected content is more than 48 hours out of date, compare item last-modified times and contact your Josh Bersin Company support contact.

For operational support, record the following information in your approved system of record:

- Connection display name and connection ID.
- Connection owner and backup administrator.
- Galileo access group name and owner.
- Date and result of initial validation.
- Expected daily crawl schedule.
- Credential storage location, without recording the secret itself.
- Exported connection configuration JSON, if allowed by your organization's policy.

## Next step

After the connector is ready and test prompts return grounded results, create the recommended declarative agents.

> [!div class="nextstepaction"]
> [Build declarative agents for Galileo by The Josh Bersin Company](galileo-declarative-agents.md)
