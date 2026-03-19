---
title: Google Drive Microsoft 365 Copilot connector overview
description: Learn about the Google Drive Microsoft 365 Copilot connector, including its capabilities, limitations, and how it works with Microsoft 365 Copilot and Microsoft Search.
ms.topic: overview
ms.service: copilot-connectors
ms.author: lauragra
author: lauragra
manager: calvind
ms.date: 12/15/2025
---

# Google Drive Microsoft 365 Copilot connector overview

The Google Drive Microsoft 365 Copilot connector enables your organization to index files stored in Google Drive and make them available in Microsoft 365 Copilot and Microsoft 365 Search. By connecting Google Drive to Microsoft 365, users can find and interact with Google Drive content by using natural language queries and Copilot experiences.

## Why use the Google Drive connector?

Organizations often store critical documents in Google Drive. The Google Drive connector brings this content into Microsoft 365, allowing users to:

- Search Google Drive files directly from Microsoft 365 Copilot and Microsoft 365 Search.
- Maintain existing Google Drive access controls (ACLs) for secure content delivery.
- Enable richer workflows by integrating Google Drive content with Microsoft Copilot Studio plugins.

## Build agents with the Google Drive connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/copilot-studio-agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Eaxmple prompts

The following examples show prompts users can use to retrieve information from Google Drive.

**File search and discovery**

- Find the latest project plan in Google Drive.
- Show me all Google Drive files shared by [colleague's name].
- List all Google Drive documents modified in the last week.
- List all files in Google Drive larger than 50 MB.

**File analysis and summaries**

- Summarize the contents of the file Q4 Roadmap from Google Drive.
- Compare the two most recent versions of the Requirements document in Google Drive.

**Sharing and permissions**

- Who last edited the file Marketing Strategy in Google Drive.
- What permissions are set on the Budget file in Google Drive.
- Show me Google Drive files I own but didn't share with anyone.

**Access and linking**

- Retrieve the link to the folder Team Resources in Google Drive.

## Capabilities

The Google Drive connector provides the following capabilities:

- **Semantic search**: Access Google Drive files by using natural language queries.
- **Access control**: Retains ACLs defined in Google Drive.
- **Customizable crawl frequency**: Configure incremental and full crawls to keep data fresh.
- **Workflow integration**: Use Google Drive content in Copilot Studio workflows.

## Limitations

The Google Drive connector has the following limitations:

- Comments and replies in Google Drive files aren't indexed.
- Folder-level metadata isn't indexed.

## Data types indexed from the Google Drive connector

The Google Drive connector indexes the following Google Drive file properties.

| Property                | Label                  | Description                                                   |
|-------------------------|------------------------|---------------------------------------------------------------|
| `file.name`            | Title                 | File name                                                    |
| `file.fileExtension`   | ItemType              | File type                                                    |
| `file.description`     | Description           | Short description of the file                                |
| `file.size`            | Size                  | Size in bytes                                                |
| `file.parents`         | ParentId              | ID of the parent folder                                      |
| `file.owners`          | createdBy/authors     | Owners of the file                                         |
| `file.webViewLink`     | URL                   | Link to open the file in Google Drive                       |
| `file.createdTime`     | createdDateTime       | File creation time                                           |
| `file.modifiedTime`    | lastModifiedDateTime  | Last modified time                                           |
| `file.lastModifyingUser`| lastModifiedBy       | Last user who modified the file                              |
| `folders.name`         | containerName         | Name of the shared drive                                     |
| `folders.webViewLink`  | containerURL          | URL to access the parent folder                              |

## Custom data filters

The Google Drive connector includes the following custom data filter for Copilot Search:

- Folder

## Permissions model and access control

The connector supports two identity mapping options:

- **Microsoft Entra ID (Entra ID)**: Use when Google Drive user emails match Entra ID user principal names (UPNs).
- **Non-Entra ID mapping**: Use regex-based mapping when emails differ from UPNs.

Set access permissions to:

- **Only people with access to this data source** (recommended)
- **Everyone** (all indexed data appears in search results for all users)

## Next step

> [!div class="nextstepaction"]
> [Deploy the Google Drive connector](google-drive-deployment.md)
