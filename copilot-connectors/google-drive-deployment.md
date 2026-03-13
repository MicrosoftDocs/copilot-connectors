---
title: Deploy the Google Drive Microsoft 365 Copilot connector
description: Learn how to deploy and configure the Google Drive Microsoft 365 Copilot connector in the Microsoft 365 admin center.
ms.topic: how-to
ms.service: copilot-connectors
ms.author: lauragra
author: lauragra
manager: calvind
ms.date: 11/18/2025
---

# Deploy the Google Drive Microsoft 365 Copilot connector

Use this article to deploy the **Google Drive Microsoft 365 Copilot connector** in the Microsoft 365 admin center. The connector indexes Google Drive content and makes it available in Microsoft 365 Copilot and Microsoft Search.

For service configuration information, see [Set up the Google Workspace service for connector ingestion](google-drive-admin-setup.md).

## Prerequisites

Before you deploy the Google Drive connector, make sure that the Google Workspace environment is configured in your organization. The following table summarizes the steps to configure the environment and deploy the connector. 

| Task | Role |
| ---- | ---- |
| [Configure the environment](google-drive-admin-setup.md) | Google Workspace admin |
| [Deploy the connector](#deploy-the-connector) | Microsoft 365 admin |
| [Customize connector settings](#customize-settings-optional) (optional) | Microsoft 365 admin |

Before you deploy the connector, make sure that you meet the following prerequisites:

- You have a Google Workspace domain and administrator account.
- You created a Google Cloud service account with domain-wide delegation.
- The service account key is available in JSON format.
- The following OAuth scopes are added to the service account:
  - `https://www.googleapis.com/auth/admin.directory.user.readonly`
  - `https://www.googleapis.com/auth/admin.directory.group.readonly`
  - `https://www.googleapis.com/auth/drive.readonly`
  - `https://www.googleapis.com/auth/admin.reports.audit.readonly`

For details, see [Set up the Google Drive service for connector ingestion](google-drive-admin-setup.md).

## Deploy the connector

To add the Google Drive connector for your organization:

1. Sign in to the [Microsoft 365 admin center](https://admin.microsoft.com).
1. In the left pane, select **Copilot** > **Connectors**.
1. Go to the **Gallery** tab and select **Google Drive**.

### Set display name

Enter a display name to identify the connector in Copilot experiences. The display name also signifies trusted content and is used as a content source filter.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

### Google Workspace domain

Provide your organization's Google Workspace domain (for example, `your-company.com`). For more information, see [What is a domain](https://support.google.com/a/answer/177483?hl=en&ref_topic=3540977&sjid=7603839478714180429-AP).

### Administrator account email

Enter the email address of a Google Workspace administrator account, in the format `user@company.com`.

### Service account key

Paste the entire contents of the JSON key file you generated when you created the Google Cloud service account. For information about how to generate the service account key, see [Create a Google Cloud project](/microsoft-365-copilot/connectors/google-drive-admin-setup#create-a-google-cloud-project).

### Roll out 

Deploy the connector to a limited audience if you want to validate it in Copilot and other search surfaces before you deploy it to your organization. For more information, see [Staged rollout for Microsoft 365 Copilot connectors](/microsoft-365-copilot/connectors/staged-rollout).

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to.

Choose **Create** to deploy the connection. The Google Drive Copilot connector starts indexing content right away.

The following table lists the default values that are set.

| Page    | Setting             | Default value |
|---------|---------------------|---------------|
| Users   | Access permissions  | All files accessible to anyone in Google Drive are visible to all Microsoft 365 users in your tenant. |
| Content | Index content       | All accessible files and folders are selected by default. |
| Sync    | Incremental crawl   | Every 15 minutes |
| Sync    | Full crawl          | Every day |

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Google Drive connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

The Google Drive connector supports the following user search permissions:

- Everyone
- Only people with access to this data source (recommended)

If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to it, and you need to further choose how to map user identities:

  - **Microsoft Entra ID**: Use when Google Drive emails match Entra ID user principal names (UPNs). The connector maps the email IDs of users in Google Drive to the UPN property from Microsoft Entra ID.
  - **Non-Entra ID**: Use regex-based mapping when Google Drive emails differ from UPNs. For more information, see [Map non-Entra ID IDs](/microsoft-365-copilot/connectors/map-non-entra-id).

> [!NOTE]
> Updates to user or group access permissions are synced in full crawls only. Incremental crawls don't currently support the processing of updates to permissions.

### Customize content settings

#### Inclusion and exclusion

Use exclusion and inclusion rules to control what data Microsoft crawls from Google Drive. Exclusion rules allow Microsoft to crawl all content except the specified items, while inclusion rules limit crawling to only the specified items. If both rules are applied to the same content, that content isn't indexed because exclusion rules take priority.


#### Supported exclusion rules 

|	Exclusion type	|	Description	|
|	---	|	---	|
|	Shared Drive ID	|	Exclude content from being crawled by specifying shared drive IDs.	|	
|	Google Group	|	Files from group members’ personal drives and shared drives accessible to all group members are excluded from crawling.	|
|	Folder ID	|	Files within the specified folders (by folder ID) are excluded from crawling.	|


#### Supported inclusion rules 
|	Inclusion type	|	Description	|
|	---	|	---	|
|	Crawl shared drives only	|	Toggle on to crawl files from shared drives only.	|	
|	Google group	|	Only files from group members’ personal drives and shared drives accessible to all group members are crawled.	|
|	Shared Drive ID	|	Only allow Microsoft to crawl certain shared drives and underlying folders. No private drives are crawled unless a Google Group is specified in the inclusion rules.	|
|	Date range	|	Only files last modified within the selected time range are crawled. If the end date is left blank, Microsoft crawls the files created/modified after the start date. If the start date is left blank, Microsoft crawls the files created from the earliest time.	|

Shared drives are treated as folders. To get the shared drive ID, open the shared drive in Google Drive and copy the portion of the URL after drive.google.com/drive/folders/. Paste this ID into the content filter.

To exclude or include specific folders, you need the folder ID. Open the desired folder in Google Drive, then copy the part of the URL after drive.google.com/drive/folders/. Paste this ID into the content filter.


#### Manage properties

You can add or remove available properties from your Google Drive data source. Assign a schema, change the semantic label, and add an alias to the property. Some properties are indexed by default.

|	Default property	|	Label	|	Description	|	Schema	|
|	---	|	---	|	---	|	---	|
|	file.name	|	Title	|	File Name	|	Search, Query, Retrieve	|
|	file.fileExtension	|	ItemType	|	The type of indexed item	|	Query, Retrieve	|
|	file.description	|		|	A short description of the file.	|		|
|	file.fileExtension	|	fileExtension	|	Output only. The final component of fullFileExtension. This property is only available for files with binary content in Google Drive.	|	Query, Retrieve	|
|	file.size	|		|	Output only. Size in bytes of blobs and first-party editor files. Not populated for files that have no size, like shortcuts and folders.	|		|
|	file.parents	|	ParentId	|	The ID of the parent folder containing the file. A file can only have one parent folder; specifying multiple parents isn't supported.	|	Query, Retrieve	|
|	file.owners	|	createdBy	|	Output only. The owner of this file. Only certain legacy files might have more than one owner. This field isn't populated for items in shared drives.	|	Search, Query, Retrieve	|
|	file.owners	|	authors	|		|	Query, Retrieve	|
|	file.webViewLink	|	url	|	Output only. A link for opening the file in a relevant Google editor or viewer in a browser.	|	Retrieve	|
|	file.createdTime	|	createdDateTime	|	The time at which the file was created (RFC 3339 date-time).	|	Query, Retrieve	|
|	file.modifiedTime 	|	lastModifiedDateTime	|	The last time anyone modified the file (RFC 3339 date-time).	|	Query, Retrieve	|
|	file.lastModifyingUser	|	lastModifiedBy	|	Output only. The last user to modify the file. This field is only populated when a signed-in user made the last modification.	|	Search, Query, Retrieve	|
|	Created from fileExtension	|	iconUrl	|	A static, unauthenticated link to the file's icon.	|	Retrieve	|
|	folders.name	|	containerName	|	The name of the shared drive that the file belongs to 	|	Query, Retrieve	|
|	folders.webViewLink	|	containerURL	|	URL to access the parent folder	|	Query, Retrieve	|

### Customize sync settings

By default, incremental crawl is set for every 15 minutes, and full crawl is set for every day. You can adjust these schedules to fit your data refresh needs.

## Related content

- [Google Drive connector overview](google-drive-overview.md)
- [Set up the Google Workspace service for connector ingestion](google-drive-admin-setup.md)
- [Troubleshoot issues with the Google Drive connector](google-drive-troubleshooting.md)
