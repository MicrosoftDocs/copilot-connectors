---
title: "Deploy the PagerDuty Incidents connector"
ms.author: wangchen
author: wangchen
manager: zezhangzhao
ms.reviewer: lauragra
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 06/03/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the PagerDuty Incidents Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the PagerDuty Incidents connector

The PagerDuty Incidents Copilot connector enables your organization to index PagerDuty incidents data to make it available to Microsoft 365 Copilot and Microsoft Search.

This article describes the steps to deploy and customize the PagerDuty Incidents connector.

[!INCLUDE [conector-preview-access](includes/connector-preview-access.md)]

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You're a Microsoft 365 admin.
- You have a PagerDuty account with administrator permission in the PagerDuty application.
- You added a new app in PagerDuty with OAuth 2.0 functionality enabled. For more information, see [OAuth Functionality](https://developer.pagerduty.com/docs/oauth-functionality) and [Register an App](https://developer.pagerduty.com/docs/register-an-app).
- You selected **Scoped OAuth** in the PagerDuty new app registration setting page.
- You set the **Redirect URL** in the PagerDuty new app registration setting page:
  - For Microsoft 365 Enterprise, use `https://gcs.office.com/v1.0/admin/oauth/callback`.
  - For Microsoft 365 Government, use `https://gcsgcc.office.com/v1.0/admin/oauth/callback`.
- You selected the following scopes in the PagerDuty new app registration setting page:
  - Audit records – Read Access
  - Schedules – Read Access
  - Teams – Read Access
  - Users – Read Access
  - Incidents – Read Access
  - Incident Types – Read Access
- You copied the **Client ID** and **Client Secret** from your completed PagerDuty app registration.

## Deploy the connector

To add the PagerDuty Incidents connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **PagerDuty Incidents**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **PagerDuty Incidents** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

### Set instance URL

PagerDuty customers can choose the geographic service region for the PagerDuty data centers that host their account. Enter the Instance REST API URL for your region:

- For the US service region, the REST API URL is `https://api.pagerduty.com`.
- For the EU service region, the REST API URL is `https://api.eu.pagerduty.com`.

For more information, see [Service regions](https://support.pagerduty.com/main/docs/service-regions).

### Choose authentication type

The PagerDuty Incidents connector uses OAuth 2.0 to authenticate with PagerDuty.

- **OAuth 2.0** (recommended) — Enter the **Client ID** and **Client Secret** that you copied from your PagerDuty app registration.

### Roll out

Deploy this connection to a limited user base to validate it in Copilot and other search surfaces before you roll it out to a broader audience.

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](staged-rollout.md).

Choose **Create** to deploy the connection. The PagerDuty Incidents Copilot connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|---------------|
| Users    | Indexed data is visible only to users who have access to the data source in PagerDuty. |
| Content  | A default set of incident properties is indexed. The **Since (Month)** content filter defines the date range used to crawl incidents (start date = Today − Since; end date = Today). |
| Sync     | Full crawl runs every day. Incremental crawl is also supported. |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the PagerDuty Incidents connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

The PagerDuty Incidents connector supports the following user search permissions:

- Only people with access to this data source (default)
- Everyone
 
If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, search results respect the same permissions that are set for the data source.

If you choose **Only people with access to this data source**, you also need to choose whether your PagerDuty instance has Microsoft Entra ID-provisioned users or non-Entra ID users:

- Choose the Microsoft Entra ID option if the email ID of PagerDuty users is the same as the user principal name (UPN) in Microsoft Entra ID.
- Choose the non-Entra ID option if the email ID of PagerDuty users is different from the UPN in Microsoft Entra ID.

> [!NOTE]
> - If you choose Microsoft Entra ID as the identity source, the connector maps user email IDs from PagerDuty to the UPN property in Microsoft Entra ID.
> - If you choose non-Entra ID as the identity source, provide a regular expression to map email ID to UPN. For more information, see [Map your non-Entra ID identities](map-non-entra-id.md).
> - Updates to users or groups that govern access permissions are synced in full crawls only. Incremental crawls don't currently support processing updates to permissions.

### Customize content settings

#### Query string

Use the **Since (Month)** content filter to specify the date range for crawling incidents in PagerDuty. The crawl start date is **Today − Since**, and the crawl end date is **Today**. Adjust this value to widen or narrow the historical window of incident content that is indexed.

#### Manage properties

To view available properties, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias in the property. Some properties are selected by default.

| Property | Semantic Label | Description | Schema Attributes |
|---|---|---|---|
| AcknowledgedBy | Not applicable | The users who acknowledged the incident. |  |
| AssignedTo | Not applicable | The users assigned to the incident. |  |
| ConferenceNumber | Not applicable | The conference number for the incident. |  |
| ConferenceUrl | Not applicable | The conference URL for the incident. |  |
| Content | `CONTENT` | The content of the incident. |  |
| CreatedDateTime | `createdDateTime` | The time at which the incident was created. |  |
| EscalationPolicyName | Not applicable | The name of the escalation policy associated with the incident. |  |
| HtmlUrl | `url` | URL of the incident in PagerDuty. |  |
| IconUrl | `IconUrl` |  |  |
| Id | Not applicable | Unique ID of the incident. |  |
| IncidentKey | Not applicable | The incident key. |  |
| IncidentNumber | Not applicable | The incident number. |  |
| IncidentType | Not applicable | The type of the incident. |  |
| LastModifiedDateTime | `lastModifiedDateTime` | The time at which the incident was last modified. |  |
| LastStatusChangeAt | Not applicable | The time at which the incident status was last changed. |  |
| LastStatusChangeBy | Not applicable | The user who last changed the incident status. |  |
| Priority | Not applicable | The priority of the incident. |  |
| ResolveReason | Not applicable | The reason the incident was resolved. |  |
| ResolvedAt | Not applicable | The time at which the incident was resolved. |  |
| ServiceName | Not applicable | The name of the service associated with the incident. |  |
| Status | Not applicable | The status of the incident. |  |
| Summary | Not applicable | A short-form, server-generated string by PagerDuty that provides succinct, important information about the incident. |  |
| Teams | Not applicable | The teams associated with the incident. |  |
| Title | `title` | The title of the incident. |  |
| Urgency | Not applicable | The urgency of the incident. |  |

### Customize sync intervals

The PagerDuty Incidents connector supports both full crawl and incremental crawl. By default, the full crawl runs every day. If needed, you can adjust these schedules to fit your data refresh needs.

For more information, see [Guidelines for sync settings](deployment-overview.md#guidelines-for-crawl-settings).

## Related content

- [PagerDuty Incidents connector overview](pagerduty-incidents-overview.md)
- [Troubleshoot issues with the PagerDuty Incidents connector](pagerduty-incidents-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](deployment-overview.md)
