---
title: "Deploy the Freshservice connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: wangchen
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 11/25/2025
ms.localizationpriority: Medium
description: "Find information about how to deploy the Freshservice Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Freshservice connector

The Freshservice Microsoft 365 Copilot connector enables your organization to index Freshservice solution article data and make it available to Microsoft 365 Copilot and Microsoft Search. This article describes the steps to deploy and customize the Freshservice connector. 

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be a Microsoft 365 admin.
- You need a Freshservice account with administrator permissions in the Freshservice application.
- You must have access to the API key from your Freshservice user profile settings. For more information, see [Where do I find my API key](https://support.freshservice.com/support/solutions/folders/50000000029).

## Deploy the connector

To add the Freshservice connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **Freshservice**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **Freshservice** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Set instance URL

Enter the domain URL of your Freshservice account. The typical structure is `https://<yourdomain>.freshservice.com`.

### Choose authentication type

Select the available authentication type and enter the API key you obtained from your Freshservice user profile setting page. The available authentication option is:

- API key authentication (recommended)

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The Freshservice Copilot connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|---------------|
| Users    | All Microsoft 365 users (for public solution articles with folder visibility set to All) |
| Content  | Solution articles stored in folders visible to All |
| Sync     | Full crawl scheduled daily (default); schedule can be adjusted as needed |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Freshservice connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

Only public solution articles with folder visibility set to **All** are indexed using the Freshservice Copilot connector. These solution articles are visible to all Microsoft 365 users in your tenant, from Microsoft Search or Copilot.

#### Mapping identities

Identity mapping isn't required for public solution articles. All indexed content is accessible to users.

### Customize content settings

#### Query string

The default query string retrieves all public solution articles from Freshservice folders with visibility set to All. You can customize the query string to filter content further if needed.

#### Manage properties

You can manage which properties are indexed from your Freshservice data source. The following table lists the properties that the connector indexes by default.

| Property           | Semantic Label        | Description                                 | Schema Attributes           |
|--------------------|----------------------|---------------------------------------------|-----------------------------|
| Id                 | Not applicable       | Unique ID of the solution article.          | Searchable, retrievable     |
| url                | `url`                | URL of the solution article.                | Searchable, retrievable     |
| Title              | `title`              | Title of the solution article.              | Searchable, retrievable     |
| CreatedOn          | `createdDateTime`    | The time when the solution article was created. | Searchable, retrievable     |
| LastModifiedOn     | `lastModifiedDateTime` | The time when the solution article was last modified. | Searchable, retrievable     |
| LastModifiedUser   | `lastModifiedBy`     | The name of the user who last modified the solution article. | Searchable, retrievable     |
| FolderUrl          | `containedUrl`       | The URL of the folder containing the solution article. | Searchable, retrievable     |
| FolderName         | `containerName`      | The name of the folder containing the solution article. | Searchable, retrievable     |
| Author             | `createdBy`          | The name of the user who created the solution article. | Searchable, retrievable     |
| CategoryName       |                      | The category the folder belongs to.   | Searchable, retrievable     |
| DescriptionText    |                      | The content of the solution article.        | Searchable, retrievable     |
| Keywords           |                      | The keywords of the solution article.       | Searchable, retrievable     |
| Tags               |                      | The tags associated with the solution article. | Searchable, retrievable     |

### Customize sync intervals

The Freshservice connector only supports full crawl. The default schedule of the full crawl is set for every day. You can adjust these schedules to fit your data refresh needs.

For more information, see [Guidelines for crawl settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [Freshservice connector overview](freshservice-overview.md)
- [Troubleshoot issues with the Freshservice connector](freshservice-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)
