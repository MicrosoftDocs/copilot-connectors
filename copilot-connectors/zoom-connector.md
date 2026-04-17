--- 
title: "Zoom Meetings connector (preview)" 
ms.author: lauragra
author: vivg
manager: ereza
audience: Admin
ms.audience: Admin 
ms.topic: install-set-up-deploy
ms.service: copilot-connectors 
ms.localizationpriority: medium 
description: "Set up the Zoom Meetings Microsoft 365 Copilot connector." 
ms.date: 04/17/2026
---

# Zoom Meetings connector (preview)

The Zoom Meeting Microsoft 365 Copilot connector enables your organization to index meeting-related artifacts, such as transcripts and metadata, and allow the meeting owners to search for such information in Microsoft 365 Copilot and Microsoft Search clients.

[!INCLUDE [connector-preview-access](includes/connector-preview-access.md)]

## Capabilities
- Index meeting-related data such as transcripts, meeting details, key points, and summary. 
- Enable your users to ask questions related to their Zoom meetings in Copilot. 
   - What are the action items from a specific meeting?
   - What are the outcomes of a specific meeting?
   - Summary of several meetings with a specific participant or on a specific subject.
- Use [semantic search in Copilot](/microsoftsearch/semantic-index-for-copilot) to enable users to find relevant content based on keywords, personal preferences, and social connections.

## Limitations
- The M365 Copilot connector app in the Zoom Marketplace is currently not available in the European Union (EU). 
- Zoom API rate limits can affect a full data refresh. For more information, see [Zoom rate limits](https://developers.zoom.us/docs/api/rate-limits/).

## Prerequisites

- You must be an AI administrator for your organization's Microsoft 365 tenant.
- To connect to your Zoom meetings data, you must have a paid Zoom plan (**Business** or **Enterprise**) with cloud recording enabled. 
- A Zoom account administrator must authenticate and provide consent to create the connection.

## Deploy the connector

### Set display name 
A display name identifies each citation in Copilot to help users easily recognize the associated file or item. The display name also signifies trusted content and is used as a [content source filter](/MicrosoftSearch/custom-filters#content-source-filters). You can accept the **Zoom Meetings** customize it to a name that users in your organization recognize.

### Authentication

- Select **OAuth 2.0**.
- Select **Authorize** and authenticate to Zoom by signing in with a Zoom administrator account.
- Complete the OAuth consent flow to grant the connector access to the required Zoom APIs.


### Roll out to limited audience
To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](staged-rollout.md).

### Agree to the terms
Check the box next to the Notice section.

### Create the connection

Choose **Create** to deploy the connection. The Zoom Meetings connector starts indexing content right away.

The following values are set by default:

- **Users**
   - Access permissions: Only the **meeting owner** in Zoom has access to the meeting’s data in Microsoft Graph.
   - Map identities: Data source identities mapped using Microsoft Entra IDs.
- **Content**
   - Manage properties: To check default properties and their schema, select **Custom Setup** > **Content**.
- **Crawl**
   - Incremental crawl: Every 15 minutes.
   - Full crawl: Every day.

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

## Customize settings (optional)

You can customize the default values for the {connector name} connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

The Zoom Meetings connector supports access permissions only for the original owner of a meeting in Zoom. 

#### Mapping identities

The default method for mapping your data source identities with Microsoft Entra ID is by checking whether the Email ID of Zoom users is same as the user principal name (UPN) or email of the users in Microsoft Entra ID. If  this configuration doesn't work for your organization, you can provide a custom mapping formula. For more information, see [Map non-Entra IDs](map-non-entra-id.md).

### Customize content settings

#### Manage properties

You can add or remove properties from your Zoom data source, assign a schema to each property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. The following table lists properties that are selected by default.

|Source property |Semantic label|Description|Schema|
|--- | ---- | --- | ---|
|Agenda| | Agenda of the meeting, if the meeting host included one when scheduling the meeting. | Search|
|Duration | |The recording duration. | Query, Search|
|Host | Created by | Meeting host’s name. | Query, Retrieve, Search|
|MeetingUUID | | The meeting's universally unique identifier. | Query|
|Participants | Authors | List of participants. | Retrieve|
|PlayRecordingUrl | url | A direct web link for streaming and viewing a Zoom meeting recording within a browser.	| Query, Retrieve|
|StartTime | Created date time | The start time of the recording. | Query, Refine, Retrieve|
|Topic | Title |	The title provided by the meeting host to summarize the subject or purpose of the Zoom meeting.	| Query, Retrieve|
|Transcript | | Text-based record of the spoken content of the meeting. | Search|
|WorkflowState | | | Retrieve|

### Sync

The refresh interval determines how often your data syncs between the data source and the Zoom Meetings connector index. The following values are the default values:

- Incremental crawl: Every 15 minutes
- Full crawl: Every day

Adjust the default values to meet the needs of your organization. For more information, see [Guidelines for sync settings](deployment-overview.md#guidelines-for-crawl-settings).

## Related content

- [Set up Copilot connectors in the Microsoft 365 admin center](deployment-overview.md)
- [Manage connectors](manage-connector.md)