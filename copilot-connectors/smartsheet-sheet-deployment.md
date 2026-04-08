---
title: "Deploy the Smartsheet Sheet connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: neocheng
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 01/14/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the Smartsheet Sheet Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Smartsheet Sheet connector

The Smartsheet Sheet Microsoft 365 Copilot connector allows your organization to index sheet content from Smartsheet so it becomes discoverable and actionable in Microsoft 365 Copilot and Microsoft Search experiences. This article describes the steps to deploy and customize the Smartsheet Sheet connector.

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- **Admin Role**: You must be the AI administrator for your organization's Microsoft 365 tenant.
- **Smartsheet instance region**: You need to know the region for your organization's Smartsheet instance:
- **Smartsheet account**: You need Smartsheet Sheet Access Tokens of System Admin Users to access published content and metadata.

## Deploy the connector

To add the Smartsheet Sheet connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
2. Choose the **Gallery** tab.
3. From the list of available connectors, choose **Smartsheet Sheet**.

### Set display name

Choose a display name that helps users easily recognize the associated file or item in a Copilot response. You can accept the default name or customize it.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

### Set Smartsheet Sheet instance region

The Smartsheet Sheet region is essential to correctly access and update data. Enter the URL that corresponds to your region:

- **Non-Europe**: `https://api.smartsheet.com`
- **Europe**: `https://api.smartsheet.eu`

### Choose authentication type

The connector supports Smartsheet Basic Authentication using an API access token:

- **API Access token owner email address**: Enter the email address of the API access token owner (must be a System Admin).
- **API Token**: Enter the API Token value generated from Smartsheet.
  - To generate a token, in Smartsheet, go to **Personal Settings** > **API Access**.
  - For more information, see [Generate an API key](https://aka.ms/gc_smartsheet_APItoken).

### Roll out

To validate the connection before a full rollout, select **Roll out to limited audience** and specify the users or groups for the staged deployment. For more information, see [Staged rollout for Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

Choose **Create** to deploy the connector. The Smartsheet Sheet connector starts indexing content right away.

The following table lists the default values that the connector applies.

Setting                | Default Value                                      |
------------------------|----------------------------------------------------|
**Access permissions** | Only people with access to content in Data source. |
**Map Identities**     | Data source identities mapped using Microsoft Entra IDs. |
**Incremental Crawl**  | Every 15 minutes.                                  |
**Full Crawl**         | Every day.                                         |

To customize these values, choose **Custom setup**.

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize settings for the Smartsheet Sheet connector.

### Customize user settings

#### Access permissions

The connector supports two access options:

- **Everyone**: Indexed data appears in search results for all users.
- **Only people with access to this data source** (recommended): Indexed data appears only for users who have access to it in Smartsheet.

#### Map identities

If you choose **Only people with access to this data source,** you must map identities:

- **Microsoft Entra ID**: Choose this option if the email ID of Smartsheet users is the same as the user principal name (UPN) or email of users in Microsoft Entra ID.
- **Non-Microsoft Entra ID**: Choose this option if the IDs differ. You can provide a custom mapping formula. For more information, see [Map your non-Entra ID identities](/microsoft-365/copilot/connectors/map-non-entra-id).

### Customize content settings

#### Filter data

You can select a time range for the content to be indexed. Only content with a **Last modified date time** within the selected range is indexed.

> [!NOTE]
> If you select **All time**, performance might be affected if the volume of content is large.

#### Manage properties

You can view available properties, assign schema attributes (searchable, queryable, retrievable, refinable), change semantic labels, and add aliases. The following table lists the data types that are indexed by default.

Property           | Description                        | Behaviors                |
--------------------|------------------------------------|--------------------------|
**Content**        | The content of the sheet.          | Search                   |
**CreatedAt**      | Date and time that the item was created. | Query, Retrieve     |
**CreatedBy**      | Name of the person who created the item. | Query, Retrieve, Search |
**HasAttachment**  | Whether the item has an attachment. | Query, Retrieve         |
**Id**             | The unique identifier of the item. | Query, Retrieve          |
**ModifiedAt**     | Date and time the item was last modified. | Query, Retrieve    |
**Name**           | File name.                         | Query, Retrieve, Search  |
**SheetPermaLink** | The target URL of the item.        | Query, Retrieve, Search  |
**Title**          | The title of the item shown in Copilot. | Query, Retrieve, Search |
**WorkspaceName**  | The name of the workspace.         | Query, Retrieve, Search  |

### Customize sync intervals

You can adjust the crawl frequency to fit your data refresh needs. The following are the default values:

- **Full crawl**: Every day
- **Incremental crawl**: Every 15 minutes

For more information, see [Guidelines for crawl settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [Smartsheet Sheet connector overview](smartsheet-sheet-overview.md)
- [Troubleshoot issues with the Smartsheet Sheet connector](smartsheet-sheet-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)
