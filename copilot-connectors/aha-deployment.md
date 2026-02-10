---
title: "Deploy the Aha! Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 02/09/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the Aha! Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Aha! Microsoft 365 Copilot connector

The Aha! Features and Ideas Microsoft 365 Copilot connectors empower your organization to index and search Aha! features and ideas across your enterprise. This article describes the steps to deploy and customize the Aha! connector.

For advanced Aha! configuration information, see [Set up the Aha! service for connector ingestion](aha-admin-setup.md).

## Prerequisites

Before you deploy the Aha! connector, make sure that the Aha! environment is configured in your organization. The following table summarizes the steps to configure the Aha! environment and deploy the connector.

| Task | Role |
|------|------|
| [Configure the environment](aha-admin-setup.md) | Aha! admin |
| [Deploy the connector in the Microsoft 365 admin center](#deploy-the-connector) | Microsoft 365 admin |
| [Customize connector settings](#customize-settings-optional) (optional) | Microsoft 365 admin |

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be a Microsoft 365 admin.
- You have the Aha! instance URL (for example, `https://contoso.aha.io`).
- You created an Aha! OAuth application and have the client ID and client secret.
- Network and API access are enabled for Microsoft 365 Copilot IP addresses.

## Deploy the connector

To add the Aha! connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
2. Choose the **Gallery** tab.
3. From the list of available connectors, choose **Aha!**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **Aha!** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](/microsoftsearch/enhancing-microsoft-copilot-discovery-with-graph-connector-content).

### Set instance URL

Provide the Aha! instance URL. The URL follows the format `https://<company>.aha.io`.

### Choose authentication type

The Aha! connector uses OAuth 2.0 for authentication. To configure:

- Create an Aha! OAuth application in the Aha! developer console.
- Enter the client ID and client secret obtained during OAuth app registration.
- Use the redirect URI:
  - For Microsoft 365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`
  - For Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](/microsoftsearch/staged-rollout-for-graph-connectors).

Choose **Create** to deploy the connection. The Aha! Copilot connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|---------------|
| Users | Access permissions: Only users with access to the content in the data source. Identities mapped using Microsoft Entra IDs. |
| Content | Default properties indexed for features and ideas. |
| Sync | Incremental crawl runs every 15 minutes; full crawl runs every day. |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Aha! connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

The Asana connector supports the following user access permissions:

- **Only people with access to this data source** (default)
- **Everyone**

If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to it.

#### Map identities

Map Aha! identities to Microsoft Entra IDs for secure access control.

### Customize content settings

#### Manage properties

You can add or remove properties, assign semantic labels, and configure schema attributes. 

The following properties are indexed by default for Aha! Features.

| Default property     | Label                   | Description                                                                 | Schema                         |
|----------------------|-------------------------|-----------------------------------------------------------------------------|--------------------------------|
| assignToUser         |                         | The user to whom the feature is assigned.                                    | Search                         |
| assignToUserEmail    |                         | Email address of the assigned user.                                          | Search                         |
| createTime           | Created date time       | Date and time when the feature was created in the data source.              | Query, Retrieve                |
| createdBy            | Created by              | The user who created the feature.                                            | Query, Retrieve, Search        |
| description          | Content                 | The description of the feature.                                              | Search                         |
| dueDate              |                         | The target completion date for the feature.                                  | Query                          |
| epicName             |                         | The name of the epic the feature belongs to.                                 | Retrieve, Search               |
| id                   |                         | Unique identifier of the feature.                                            | Query, Retrieve                |
| link                 |                         | A link or reference to the feature.                                         | Query, Retrieve, Search        |
| name                 | Title                   | The title of the feature shown in Copilot and search experiences.            | Query, Retrieve, Search        |
| reference            |                         | Internal or external reference identifier.                                   | Query                          |
| releaseName          |                         | The name of the associated release.                                          | Search                         |
| score                |                         | A numerical or qualitative score associated with the feature.                | Query, Search                  |
| startDate            |                         | The planned start date of the feature.                                       | Query                          |
| status               |                         | The current state of the feature (For example planned, in progress, complete).     | Query, Refine, Search          |
| tag                  |                         | Tags or labels associated with the feature.                                 | Query, Retrieve, Search        |
| updateTime           | Last modified date time | Date and time when the feature was last updated in the data source.          | Query, Retrieve                |
| url                  | url                     | The target URL of the feature in the data source.                            | Retrieve, Search               |

The following properties are indexed by default for Aha! Ideas.

| Default property     | Label                     | Description                                                                 | Schema                         |
|----------------------|---------------------------|-----------------------------------------------------------------------------|--------------------------------|
| assignToUser         |                           | The user to whom the idea is assigned.                                       | Query, Search                  |
| assignToUserEmail    |                           | Email address of the assigned user.                                          | Query, Search                  |
| categories           |                           | Categories or groups associated with the idea.                               | Query, Retrieve                |
| createTime           | Created date time         | Date and time when the idea was created in the data source.                  | Query, Retrieve                |
| createdBy            | Created by                | The user who created the idea.                                               | Query, Retrieve, Search        |
| description          | Content                   | The description or details of the idea.                                      | Search                         |
| iconUrl              | IconUrl                   | URL of the icon representing the idea.                                      | Retrieve                       |
| id                   |                           | Unique identifier of the idea.                                               | Query, Retrieve                |
| link                 |                           | A link or reference to the idea.                                             | Query, Retrieve, Search        |
| name                 | Title                     | The title of the idea shown in Copilot and other search experiences.         | Query, Retrieve, Search        |
| reference            |                           | Internal or external reference identifier.                                  | Query                          |
| score                |                           | A numerical or qualitative score indicating importance or relevance.         | Query, Search                  |
| status               |                           | The current state of the idea (for example new, planned, shipped).                 | Query, Refine, Retrieve        |
| updateTime           | Last modified date time   | Date and time when the idea was last updated in the data source.             | Query, Retrieve                |
| url                  | url                       | The target URL of the idea in the data source                               | Retrieve, Search               |
| votes                |                           | The number of votes submitted for the idea.                                  | Query, Retrieve                |


### Customize sync intervals

You can customize the sync intervals for full crawl and incremental crawl. Default values:

- Incremental crawl: Every 15 minutes
- Full crawl: Every day

For more information, see [Guidelines for sync settings](/microsoftsearch/configure-connector#guidelines-for-sync-settings).

#### Rate limits

The following table lists the rate limits that apply to the Aha! connector (for both features and ideas).

| Approximate number of items | Approximate time to complete ingestion |
|-----------------------------|----------------------------------------|
| Up to 10,000                | Up to 1 hour                           |
| 10,000 to 300,000           | Hours to 1 day                         |
| 300,000 to 2,000,000        | 2 days to 1 week                       |
| 2,000,000 or more           | 1–2 weeks (varies by environment load) |

## Related content

- [Aha! connector overview](aha-overview.md)
- [Troubleshoot issues with the Aha! connector](aha-troubleshooting.md)
