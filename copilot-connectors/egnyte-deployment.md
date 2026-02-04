---
title: "Deploy the Egnyte Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: anggao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 12/16/2025
ms.localizationpriority: Medium
description: "Find information about how to deploy the Egnyte Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Egnyte Microsoft 365 Copilot connector

The Egnyte Microsoft 365 Copilot connector allows your organization to index files stored in Egnyte so users can retrieve them through Microsoft 365 Copilot and Microsoft Search. This article describes the steps to deploy and customize the Egnyte Microsoft 365 Copilot connector.

For advanced Egnyte configuration information, see  
[Set up the Egnyte service for connector ingestion](egnyte-admin-setup.md).

## Prerequisites

Before you deploy the Egnyte connector, make sure your Egnyte environment is configured and that you meet the following prerequisites:

- Egnyte admin permissions in your Egnyte domain.
- An Egnyte developer account with a registered application.
- A valid **client ID** and **secret** generated in the Egnyte developer portal.
- A confirmed API rate limit appropriate for your expected crawl volume.
- Microsoft 365 admin permissions to deploy connectors.

## Deploy the connector

To add the Egnyte connector for your organization:

1. In the Microsoft 365 admin center, go to **Copilot** > **Connectors**.
2. Select the **Connectors** tab, and then choose **Gallery**.
3. From the list of available connectors, select **Egnyte**.

### Set display name

The display name appears in Copilot responses and helps users recognize content coming from Egnyte.  
You can accept the default **Egnyte** display name or customize it to something more recognizable for your organization.

For more information about display names and descriptions, see [Enhance Copilot discovery of connector content](/microsoft-365-copilot/connectors/enhancing-microsoft-copilot-discovery-with-graph-connector-content).

### Set instance URL

Enter your Egnyte domain in the following format:

`https://.egnyte.com`

This domain must match the domain configured in your Egnyte developer application.

### Choose authentication type

The following authentication type is supported:

- **OAuth 2.0 using Client ID and Secret** (recommended)

Enter the **client ID** and **secret** from your Egnyte developer account. Make sure these values match the credentials assigned to the app that was created as a **Publicly Available Application** in the Egnyte developer portal.

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](/microsoft-365-copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The Egnyte connector starts indexing content right away.

The following table lists the default values that are configured for the Egnyte connector.

| Category | Setting | Default value |
|---------|---------|----------------|
| Users | Access permissions | All files accessible to any Egnyte user are visible to all Microsoft 365 users in your tenant. |
| Content | Index content | All published files are selected by default. |
| Content | Manage properties | Default Egnyte properties are indexed automatically. |
| Sync | Incremental crawl | Every 4 hours |
| Sync | Full crawl | Every day |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize user, content, or sync settings for the Egnyte connector.

### Customize user settings

#### Access permissions

Choose how Egnyte data should appear in Microsoft 365:

- **Only people with access to this data source** (recommended)  
- **Everyone**

If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, you need to choose whether your users are Microsoft Entra ID provisioned users or non-Microsoft Entra ID users. For more information, see [Mapping identities](#mapping-identities).

#### Mapping identities

Choose whether your users are Microsoft Entra ID provisioned users or non-Microsoft Entra ID users:

- Choose the Microsoft Entra ID option if the email ID of Egnyte users is the same as the user principal name (UPN) of users in Microsoft Entra ID.
- Choose the non-Microsoft Entra ID option if the email ID of Egnyte users is different from the UPN of users in Microsoft Entra ID.

> [!IMPORTANT]
> If you choose Microsoft Entra ID, the connector maps the email IDs of users from Egnyte to the UPN property from Microsoft Entra ID.
> If you choose non-Microsoft Entra ID, provide a regular expression to map identities from email ID to UPN. For more information, see [Map your non-Microsoft Entra ID identities](/microsoft-365-copilot/connectors/map-non-entra-id).
> Updates to users or groups that govern access permissions are synced in full crawls only. Incremental crawls don't currently support processing updates to permissions.

### Customize content settings

#### Content filter

Select the time range for the data to be indexed. The default value is the last one year.

#### Manage properties

You can add or remove properties from your Egnyte data source, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to a property. The following table lists the properties that are added by default.

| Property | Semantic label | Description | Schema |
|----------|----------------|-------------|--------|
| checksum | — | Checksum of the current version used to detect changes | Query |
| size | — | Size of the file in bytes | Query |
| path | — | Full file path | Query, Retrieve, Search |
| name | fileName | File name | Query, Retrieve, Search |
| locked | — | Lock status | Query, Retrieve, Search |
| entry_id | — | ID of the file version | — |
| group_id | — | ID representing the file entity | — |
| parent_id | — | ID of the parent folder | — |
| last_modified | lastModifiedDateTime | Last modified time | Query, Retrieve, Search |
| uploaded_by | createdBy | User who uploaded the version | Query, Retrieve, Search |
| uploaded | — | Upload time | Query, Retrieve |
| num_versions | — | Total number of versions | — |
| url | url | URL for the file | Retrieve |
| content | — | File content | Search |
| file extension | fileExtension | File extension | Query, Retrieve, Search |

### Customize sync intervals

You can adjust the crawl frequency to fit your data refresh needs:

- **Incremental crawl:** Default is every 4 hours.
- **Full crawl:** Default is every day.

Choose a schedule that balances content freshness with Egnyte API rate limits.

For more information, see [Guidelines for sync settings](/microsoft-365-copilot/connectors/deployment-overview#guidelines-for-sync-settings).


## Related content

- [Egnyte connector overview](egnyte-overview.md)
- [Troubleshoot issues with the Egnyte connector](egnyte-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365-copilot/connectors/deployment-overview)
