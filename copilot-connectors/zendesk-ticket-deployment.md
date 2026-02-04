---
title: "Deploy the Zendesk Ticket Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: anggao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 01/14/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the Zendesk Ticket Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Zendesk Ticket Microsoft 365 Copilot connector

The Zendesk Ticket Microsoft 365 Copilot connector allows your organization to index tickets from Zendesk. After you configure the connector, users can search for these tickets from Zendesk in Microsoft 365 Copilot and from any Microsoft Search client.

This article describes the steps to deploy and customize the Zendesk Ticket connector.

## Prerequisites

Before you deploy the Zendesk Ticket connector, make sure that you meet the following prerequisites:

- You must be the **Microsoft 365 search admin** for your organization's tenant.
- To connect to your Zendesk Ticket data, you need your organization's Zendesk instance URL, which is typically:  
  `https://<your-organization-domain>.zendesk.com`. If you don't have an instance URL, see [How do I create a Support trial account?](https://support.zendesk.com/hc/en-us/articles/4408823799962-How-do-I-create-a-Support-trial-account).
- To connect to Zendesk Ticket and allow the connector to update tickets regularly, you need a service account with read permissions. The account must have the Admin role to avoid permission issues for identity data (users, groups, organizations).

## Deploy the connector

To add the Zendesk Ticket connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
2. Choose the **Gallery** tab.
3. From the list of available connectors, choose **Zendesk Ticket**.

### Set display name

The display name identifies each citation in Copilot to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter. You can accept the default **Zendesk Ticket** display name or customize it to a name that users in your organization recognize.

### Set instance URL

Provide your Zendesk instance URL in the format:  
`https://<your-organization-domain>.zendesk.com`

### Choose authentication type

The connector uses OAuth 2.0 for secure access. A Zendesk administrator must create an OAuth client in the [Zendesk Admin Center](https://support.zendesk.com/hc/en-us/articles/4581766374554-Using-Zendesk-Admin-Center#topic_hfg_dyz_1hb). For details, see [Managing access to the Zendesk API](https://support.zendesk.com/hc/articles/4408889192858-Managing-access-to-the-Zendesk-API#topic_mmh_gm1_2yb).

Use the following values when you create the OAuth client.

| Field        | Description                                               | Recommended value |
|-------------|-----------------------------------------------------------|--------------------|
| Client name | Unique value that identifies the application              | Microsoft Search   |
| Description | (Optional) A short description of the OAuth client        | Use an appropriate description. |
| Company     | The name of your company                                  | Use an appropriate value. |
| Logo        | Image for the application logo                            | Any appropriate logo or default. |
| Client kind | Choose between Confidential and Public OAuth client       | Confidential       |
| Redirect URL| Callback URL for authorization server                     | For **Microsoft 365 Enterprise**: `https://gcs.office.com/v1.0/admin/oauth/callback`<br><br>For **Microsoft 365 Government**: `https://gcsgcc.office.com/v1.0/admin/oauth/callback` |

Enter the client ID and secret to connect to your instance. After you connect, use a Zendesk account credential to authenticate permission to crawl.

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups. For more information, see [Staged rollout for Copilot connectors](/microsoft-365-copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The Zendesk Ticket connector starts indexing content right away.

The following tables list the default values that are set.

| Category | Setting            | Description                                      |
|--------------------|--------------------------------------------------|
| Users | Access permissions | Only people with access to content in data source|
| Users | Map identities     | Data source identities mapped using Microsoft Entra IDs |
| Content | Manage properties | Default properties and schema applied            |
| Crawl | Incremental crawl | Frequency: Every 15 minutes                     |
| Crawl | Full crawl        | Frequency: Every day                            |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Zendesk Ticket connector settings. When you choose **Custom setup**, you see three tabs: **Users**, **Content**, and **Crawl**.

### Customize user settings

#### Access permissions

The Zendesk Ticket Copilot connector supports **Everyone** or **Only people with access to this data source** search permissions. If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to them.

#### Map identities

The default method for mapping your data source identities with Microsoft Entra ID is to verify that the email ID of Zendesk users is the same as the user principal name (UPN) or email address of the users in Microsoft Entra. If the default mapping doesn't work for your organization, you can provide a custom mapping formula. For more information, see [Map your non-Entra ID identities](/microsoft-365-copilot/connectors/map-non-entra-id).

To identify which option to choose:

-	Choose the **Microsoft Entra ID** option if the Zendesk users' email ID is the same as the UPN or email in Microsoft Entra ID.
-	Choose the **Non-Microsoft Entra ID** option if the Zendesk users' email ID is different from the UPN and email in Microsoft Entra ID.

### Customize content settings

#### Manage properties

You can add or remove available properties from your Zendesk Ticket, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. The following table lists the properties that are selected by default.

| Source property | Label | Description | Schema |
|-----------------|-------|-------------|--------|
| Assignee | assignedToPeople | | Query, Refine, Retrieve, Search |
| Brand | | | Query, Retrieve, Search |
| Collaborators | authors | | Query, Retrieve, Search |
| CreateDate | createdDateTime | Date and time that the item was created in the data source | Query, Refine, Retrieve |
| Description | | | Search, Retrieve |
| DueDate | DueDate | | Query, Refine, Retrieve |
| EmailCcs | | | Query, Retrieve, Search |
| ExternalId | | | Query, Retrieve, Search |
| Followers | | | Query, Retrieve, Search |
| Group | itemParentId | | Query, Refine, Retrieve, Search |
| IconUrl | iconUrl | | Retrieve |
| Id | secondaryId | | Query, Retrieve, Search |
| Organization | | | Query, Retrieve, Search |
| Priority | priority | | Query, Refine, Retrieve, Search |
| ProblemId | | | Query, Retrieve, Search |
| Recipient | | | Query, Retrieve, Search |
| Requester | reportedBy | | Query, Retrieve, Search |
| Status | state | | Query, Refine, Retrieve, Search |
| Subject | title | The title of the item that you want shown in Copilot and other search experiences | Query, Retrieve, Search |
| Submitter | createdBy | | Query, Retrieve, Search |
| Tags | tags | | Query, Refine, Retrieve, Search |
| Type | itemType | | Query, Refine, Retrieve, Search |
| UpdateDate | lastModifiedDateTime | Date and time the item was last modified in the data source. | Query, Refine, Retrieve |
| Url | | | Query, Retrieve, Search |
| ViaChannel | | | Query, Retrieve, Search |
| ViewUrl | url | The target URL of the item in the data source | Query, Retrieve, Search |
| ViaSourceFromAddress | | | Query, Retrieve, Search |
| ViaSourceFromName | | | Query, Retrieve, Search |
| ViaSourceToAddress | | | Query, Retrieve, Search |
| ViaSourceToName | | | Query, Retrieve, Search |

Use the **Preview results** button to verify sample values of the selected properties.

### Customize crawl intervals

The refresh interval determines how often your data is synced between the data source and the Zendesk Ticket Copilot connector index. You can change the default refresh intervals for full and incremental crawls. For more information, see [Guidelines for sync settings](/microsoft-365-copilot/connectors/deployment-overview#guidelines-for-sync-settings).

## Related content

- [Zendesk Ticket connector overview](zendesk-ticket-overview.md)
- [Troubleshoot issues with the Zendesk Ticket connector](zendesk-ticket-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365-copilot/connectors/deployment-overview)
