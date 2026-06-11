---
title: "Deploy the Salesforce CRM connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 06/05/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the Salesforce CRM Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Salesforce CRM connector

The Salesforce CRM Microsoft 365 Copilot connector enables your organization to index Salesforce records, such as accounts, contacts, leads, opportunities, and cases, so users can discover that content in Copilot and Microsoft Search.

This article describes the steps to deploy and customize the Salesforce CRM connector.

For advanced Salesforce configuration information, see [Set up the Salesforce service for connector ingestion](salesforce-crm-admin-setup.md).

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be a Microsoft 365 admin.
- You have the Salesforce instance URL in the format `https://<domain>.my.salesforce.com`.
- You created a Salesforce connected app for OAuth 2.0 and have the consumer key and consumer secret.
- The Salesforce account used during connector authorization has required API and object permissions.

## Deploy the connector

To add the Salesforce CRM connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, select **Copilot** > **Connectors**.
1. Select the **Gallery** tab.
1. From the list of available connectors, select **Salesforce CRM**.

### Set display name

The display name identifies references in Copilot responses so users can recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **Salesforce CRM** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

### Set instance URL

For the instance URL, enter your Salesforce domain URL in the format `https://<domain>.my.salesforce.com`.

### Choose authentication type

The Salesforce CRM connector supports the following authentication type:

- **OAuth 2.0 (recommended)**

To authenticate:

1. Select **OAuth 2.0**.
1. Enter the client ID (consumer key) and client secret from Salesforce.
1. Select **Authorize** and complete the Salesforce sign-in prompt.

If the sign-in prompt doesn't appear, allow browser pop-ups and redirects.

### Roll out

To roll out to a limited audience, select the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](staged-rollout.md).

Select **Create** to deploy the connection. The Salesforce CRM connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|---------------|
| Users | Access permissions are set to only people with access to this data source. Identities are mapped by using Microsoft Entra ID. |
| Content | Accounts, contacts, leads, opportunities, and cases are indexed. No modified-time filter or SOQL filter is applied by default. |
| Sync | Incremental crawl runs every 15 minutes. Full crawl runs every day. |

To customize these values, select **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Salesforce CRM connector settings. To customize settings, on the connector page in the admin center, select **Custom setup**.

### Customize user settings

#### Access permissions

The Salesforce CRM connector supports search permissions visible to **Everyone** or **Only people with access to this data source**. If you choose **Everyone**, all users see the indexed data in the search results. If you choose **Only people with access to this data source**, only users who have access in Salesforce see the indexed data in search results.

#### Map identities

You can map both Microsoft Entra identities and non-Microsoft Entra identities from Salesforce ACLs.

To map non-Microsoft Entra identities, see [Map your non-Microsoft Entra identities](map-non-entra-id.md). To map Microsoft Entra identities, see [Map your Microsoft Entra identities](map-entra-id.md).

### Customize content settings

#### Query string

Use a Salesforce Object Query Language (SOQL) `WHERE` clause to limit indexed data to specific records or criteria. You can also set a modified-time window to index only records created or changed in a rolling period.

#### Manage properties

You can add or remove source properties and assign schema attributes to each property.

| Property | Semantic label | Description | Schema attributes |
|---|---|---|---|
| Authors | `authors` | Names of people who participated or collaborated on the item in Salesforce. | Retrieve |
| CreatedBy | `createdBy` | Name of the person who created the item. | Query, Retrieve |
| CreatedDate | `createdDateTime` | Date and time when the item was created. | Query, Retrieve |
| LastModifiedBy | `lastModifiedBy` | Name of the person who most recently edited the item. | Query, Retrieve |
| LastModifiedDateTime | `lastModifiedDateTime` | Date and time when the item was last modified. | Query, Retrieve |
| Name | `title` | Title shown in search and other experiences. | Query, Search, Retrieve |
| Url | `url` | Target URL for the item in Salesforce. | Retrieve |

### Customize sync intervals

You can customize both full crawl and incremental crawl intervals. The default values are a daily full crawl and a 15-minute incremental crawl.

For more information, see [Guidelines for crawl settings](deployment-overview.md#guidelines-for-crawl-settings).

## Related content

- [Salesforce CRM connector overview](salesforce-crm-overview.md)
- [Troubleshoot issues with the Salesforce CRM connector](salesforce-crm-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](deployment-overview.md)

