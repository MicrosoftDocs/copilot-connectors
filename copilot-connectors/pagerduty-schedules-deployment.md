---
ms.date: 05/26/2026
title: "Deploy the PagerDuty Schedules connector"
ms.author: wangchen
author: wangchen
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.localizationpriority: Medium
description: "Find information about how to deploy the PagerDuty Schedules Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the PagerDuty Schedules connector (preview)

The PagerDuty Schedules Microsoft 365 Copilot connector integrates PagerDuty schedule data into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface schedule information directly within apps like Teams, Outlook, and SharePoint.

This article describes the steps to deploy, customize, and manage the PagerDuty Schedules Copilot connector. For general information about Copilot connector deployment, see [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview).

For advanced PagerDuty service configuration, see [Set up the PagerDuty service for connector ingestion](pagerduty-schedules-admin-setup.md).

[!INCLUDE [conector-preview-access](includes/connector-preview-access.md)]

## Prerequisites

Before you deploy the PagerDuty Schedules connector, make sure that the PagerDuty environment is configured in your organization. The following table summarizes the steps to configure the PagerDuty environment and deploy the connector.

| Task | Role |
| ---- | ---- |
| [Configure the PagerDuty environment](pagerduty-schedules-admin-setup.md#configure-the-pagerduty-environment) | PagerDuty admin |
| [Set up OAuth prerequisites](pagerduty-schedules-admin-setup.md#set-up-oauth-prerequisites) | PagerDuty admin |
| [Deploy the connector in the Microsoft 365 admin center](#deploy-the-connector) | Microsoft 365 admin |
| [Customize connector settings](#customize-settings-optional) (optional) | Microsoft 365 admin |

Before you deploy the connector, make sure that you meet the following prerequisites:

- You're an admin for your organization's Microsoft 365 tenant.
- You have a PagerDuty account with administrator permissions.
- You must have completed the PagerDuty OAuth app setup and obtained the Client ID and Client Secret. For more information, see [Set up the PagerDuty service for connector ingestion](pagerduty-schedules-admin-setup.md).

## Deploy the connector

To add the PagerDuty Schedules connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Select the **Connectors** tab. In the left pane, select **Gallery**.
1. From the list of available connectors, select **PagerDuty Schedules**.

### Set display name

The display name identifies references in Copilot responses to help users recognize the associated schedule or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **PagerDuty Schedules** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery with Microsoft 365 Copilot connectors content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Set instance REST API URL

PagerDuty allows customers to choose the geographic service region of the PagerDuty data centers that host their account. To connect to your PagerDuty service, use the REST API URL that corresponds to your service region:

- **For the US service region**: `https://api.pagerduty.com`
- **For the EU service region**: `https://api.eu.pagerduty.com`

To identify your PagerDuty service region, sign in to your PagerDuty account and review the URL in your browser address bar. For the US region, your URL typically appears as `https://[your-subdomain].pagerduty.com`. For the EU region, your URL typically appears as `https://[your-subdomain].eu.pagerduty.com`.

For more information, see [Service regions](https://support.pagerduty.com/main/docs/service-regions) in the PagerDuty documentation.

### Choose authentication type

The PagerDuty Schedules connector uses OAuth 2.0 for authentication. To authenticate the connector:

1. Select **OAuth 2.0** as the authentication type.
1. Enter the **Client ID** that you obtained from your PagerDuty OAuth app registration.
1. Enter the **Client Secret** that you obtained from your PagerDuty OAuth app registration.
1. Choose **Authorize** to initiate the OAuth authorization flow.
1. Sign in to PagerDuty with your administrator account when prompted.
1. Review the requested permissions and choose **Authorize** to grant access.

> [!NOTE]
> If you haven't completed the OAuth app setup in PagerDuty, see [Set up the PagerDuty service for connector ingestion](pagerduty-schedules-admin-setup.md) for detailed instructions.

### Roll out

Deploy the connection to a limited set of users to validate it in Copilot and other search surfaces before you roll it out to a broader audience. For more information, see [Staged rollout for Microsoft 365 Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to.

To deploy the connector, choose **Create** in the Microsoft 365 admin center. The PagerDuty Schedules Copilot connector starts indexing schedules from your PagerDuty account right away.

The following table lists the default values that are set. These values work best with PagerDuty schedule data.

| Category | Setting | Default value |
|----------|---------|---------------|
| Users | Access permissions | Only people with access to the content in the data source |
| Users | Map identities | Data source identities mapped using Microsoft Entra IDs |
| Content | Days Before | 7 days |
| Content | Days After | 7 days |
| Content | Manage properties | For default properties and schemas, see [Manage properties](#manage-properties) |
| Sync | Full crawl | Frequency: Every day |

To customize these values, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the PagerDuty Schedules connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

The PagerDuty Schedules connector supports the following user search permissions:

- Everyone
- Only people with access to this data source (default)

If you choose **Everyone**, indexed schedule data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed schedule data appears in the search results for users who have access to it in PagerDuty.

> [!NOTE]
> When Advanced Permissions is enabled in PagerDuty, only members of the teams linked to a specific schedule can access and search for that schedule in Microsoft Search and Microsoft 365 Copilot. For more information about Advanced Permissions, see [Advanced Permissions](https://support.pagerduty.com/main/docs/advanced-permissions) in the PagerDuty documentation.

If you choose **Only people with access to this data source**, you also need to choose whether your PagerDuty account has Microsoft Entra ID provisioned users or non-Entra ID users:

- Choose the Microsoft Entra ID option if the email ID of PagerDuty users is same as the user principal name (UPN) in Microsoft Entra ID.
- Choose the non-Entra ID option if the email ID of PagerDuty users is different from the UPN in Microsoft Entra ID. For more information about identity mapping, see [Map your non-Entra ID identities](map-non-entra-id.md).

### Customize content settings

You can customize the content that the PagerDuty Schedules connector indexes by configuring the following parameters.

#### Content filter

The PagerDuty Schedules connector provides two parameters to specify the date range for crawling schedule content:

- **Days Before**: The number of days before today to include in the crawl.
- **Days After**: The number of days after today to include in the crawl.

The crawl start date is calculated as **(Today – Days Before)** and the crawl end date is calculated as **(Today + Days After)**.

For example:
- If **Days Before** is set to 7 and **Days After** is set to 14, the connector indexes schedule entries from 7 days ago to 14 days in the future.
- The default values are **Days Before = 7** and **Days After = 7**, providing a two-week window centered on the current date.

You can adjust these values to fit your organization's needs. Consider setting longer ranges if your teams plan on-call schedules further in advance, or shorter ranges if you only need visibility into immediate coverage.

#### Manage properties

The PagerDuty Schedules connector indexes the following properties from PagerDuty schedules. To view available properties, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, or add an alias to the property. Some properties are selected by default.

| Source property | Label | Description |
| --------------- | ----- | ----------- |
| Id | Not applicable | Unique ID of the schedule in PagerDuty. |
| HtmlUrl | `url` | URL of the schedule in PagerDuty. This link takes users directly to the schedule in PagerDuty. |
| IconUrl | `IconUrl` | URL of the icon associated with the schedule. |
| Coverage | Not applicable | The percentage of the configured time range covered by this schedule. |
| CreatedBy | `createdBy` | The name of the user who created the schedule. |
| CreatedDateTime | `createdDateTime` | The time at which the schedule was created. |
| Description | Not applicable | The description of the schedule. |
| FinalSchedule | Not applicable | A list of entries in the final schedule, including the on-call user, start time, and end time for each entry. |
| LastModifiedBy | `lastModifiedBy` | The name of the user who last modified the schedule. |
| LastModifiedDateTime | `lastModifiedDateTime` | The time at which the schedule was last modified. |
| Name | `title` | The name of the schedule. This is the primary identifier shown in search results and Copilot responses. |
| Summary | Not applicable | A short-form, server-generated string by PagerDuty that provides succinct, important information about the schedule. |
| Timezone | Not applicable | The time zone of the schedule. |
| Usage | Not applicable | The escalation policies associated with the schedule. |

> [!TIP]
> Consider making the **Description**, **Name**, and **Summary** properties searchable to improve the relevance of Copilot responses when users query for schedule information.

### Customize sync intervals

The PagerDuty Schedules connector supports only full crawl. Incremental crawl isn't available for this connector.

The default schedule for the full crawl is set to **Every day**. This setting means that the connector reindexes all schedule data within the configured date range once per day.

You can adjust the full crawl schedule to fit your data refresh needs:

- If schedules change frequently in your organization, consider maintaining the daily full crawl frequency.
- If schedules are relatively static, reduce the crawl frequency to every few days or weekly.

To adjust the crawl schedule:

1. In the connector settings, go to the **Sync** section.
1. Under **Full crawl**, select the desired frequency from the dropdown.
1. Select **Save** to apply the changes.

> [!NOTE]
> Changes to the crawl frequency affect how quickly updates to PagerDuty schedules are reflected in Copilot and Microsoft Search results.

## Related content

- [PagerDuty Schedules connector overview](pagerduty-schedules-overview.md)
- [Set up the PagerDuty service for connector ingestion](pagerduty-schedules-admin-setup.md)
- [Troubleshoot issues with the PagerDuty Schedules connector](pagerduty-schedules-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](deployment-overview.md)
