---
ms.date: 05/20/2026
title: "Deploy the PagerDuty Schedules connector in the Microsoft 365 Admin Center"
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

# Deploy the PagerDuty Schedules connector in the Microsoft 365 admin center (preview)

The PagerDuty Schedules Microsoft 365 Copilot connector integrates PagerDuty schedule data into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface schedule information directly within apps like Teams, Outlook, and SharePoint.

This article describes the steps to deploy, customize, and manage the PagerDuty Schedules Copilot connector. For general information about Copilot connector deployment, see [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview).

[!INCLUDE [conector-preview-access](includes/connector-preview-access.md)]

## Prerequisites

To deploy the connector, you must meet the following prerequisites:

- You must be an admin for your organization's Microsoft 365 tenant.
- You must have a PagerDuty account with administrator permissions.
- You must have authentication credentials with the appropriate access for both Microsoft 365 and PagerDuty.

## Set up PagerDuty OAuth app

Before deploying the connector, you need to register an OAuth 2.0 app in PagerDuty to obtain the client credentials required for connector authentication.

### Register an OAuth 2.0 app in PagerDuty

To register an OAuth 2.0 app in PagerDuty:

1. Sign in to your PagerDuty account with administrator permissions.
1. Navigate to **Integrations** > **Developer Mode**.
1. If Developer Mode is not enabled, enable it to access app registration.
1. Choose **Create New App**.
1. In the app registration form, provide the following information:
   - **App Name**: Enter a descriptive name such as "Microsoft 365 Copilot Connector"
   - **Description**: Enter a description such as "OAuth app for Microsoft 365 Copilot connector integration"
   - **Category**: Select **Integration**

1. Select **Scoped OAuth** as the OAuth type.

For more information about OAuth functionality in PagerDuty, see [OAuth Functionality](https://developer.pagerduty.com/docs/oauth-functionality) and [Register an App](https://developer.pagerduty.com/docs/register-an-app) in the PagerDuty developer documentation.

### Configure redirect URLs

OAuth 2.0 authentication requires redirect URLs (also called callback URLs) to complete the authorization flow. The redirect URL varies based on your Microsoft 365 environment.

In your PagerDuty OAuth app settings, add the appropriate redirect URL for your environment:

- **For Microsoft 365 Enterprise**: `https://gcs.office.com/v1.0/admin/oauth/callback`
- **For Microsoft 365 Government**: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`

> [!IMPORTANT]
> Make sure that you use the correct redirect URL for your environment. Using an incorrect redirect URL prevents the OAuth authorization flow from completing successfully.

### Configure OAuth scopes

The PagerDuty Schedules connector requires specific OAuth scopes to access schedule data. In your OAuth app settings in PagerDuty, select the following scopes:

| Scope | Access level | Description |
| ----- | ------------ | ----------- |
| Audit records | Read Access | Required to access audit log information for schedules. |
| Schedules | Read Access | Required to read schedule data including on-call rotations and coverage information. |
| Teams | Read Access | Required when Advanced Permissions is enabled to enforce team-based access controls. |
| Users | Read Access | Required to map PagerDuty users to Microsoft 365 identities for permission enforcement. |

> [!NOTE]
> The connector requires read-only access. Write or delete permissions are not required.

### Get Client ID and Client Secret

After configuring your OAuth app:

1. Choose **Save** to create the app.
1. In the app settings, copy the **Client ID** and **Client Secret**. You need these values when deploying the connector in the Microsoft 365 admin center.

> [!IMPORTANT]
> Store the Client ID and Client Secret securely. You need these credentials to authenticate the connector during deployment.

## Deploy the connector

To add the PagerDuty Schedules connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Connectors** tab, and in the left pane, choose **Gallery**.
1. From the list of available connectors, choose **PagerDuty Schedules**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated schedule or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **PagerDuty Schedules** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery with Microsoft 365 Copilot connectors content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Set instance REST API URL

PagerDuty allows customers to choose the geographic service region of the PagerDuty data centers that host their account. To connect to your PagerDuty service, use the REST API URL that corresponds to your service region:

- **For the US service region**: `https://api.pagerduty.com`
- **For the EU service region**: `https://api.eu.pagerduty.com`

To identify your PagerDuty service region, sign in to your PagerDuty account and review the URL in your browser address bar. For the US region, your URL typically appears as `https://[your-subdomain].pagerduty.com`. For the EU region, your URL typically appears as `https://[your-subdomain].eu.pagerduty.com`.

For more information, see [Service regions](https://support.pagerduty.com/main/docs/service-regions) in the PagerDuty documentation.

### Choose authentication type

The PagerDuty Schedules connector uses OAuth 2.0 for authentication. To authenticate and synchronize schedule data from PagerDuty:

1. Select **OAuth 2.0** as the authentication type.
1. Enter the **Client ID** that you obtained from your PagerDuty OAuth app registration.
1. Enter the **Client Secret** that you obtained from your PagerDuty OAuth app registration.
1. Choose **Authorize** to initiate the OAuth authorization flow.
1. Sign in to PagerDuty with your administrator account when prompted.
1. Review the requested permissions and choose **Authorize** to grant access.

> [!NOTE]
> Select **Scoped OAuth** when configuring your PagerDuty app registration to ensure proper authentication.

### Roll out to a limited audience

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

### Customize sync settings

The PagerDuty Schedules connector supports full crawl only. Incremental crawl is not available for this connector.

The default schedule for the full crawl is set to **Every day**. This means that the connector re-indexes all schedule data within the configured date range once per day.

You can adjust the full crawl schedule to fit your data refresh needs:

- If schedules change frequently in your organization, consider maintaining the daily full crawl frequency.
- If schedules are relatively static, you can reduce the crawl frequency to every few days or weekly.

To adjust the crawl schedule:

1. In the connector settings, navigate to the **Sync** section.
1. Under **Full crawl**, choose the desired frequency from the dropdown.
1. Choose **Save** to apply the changes.

> [!NOTE]
> Changes to the crawl frequency affect how quickly updates to PagerDuty schedules are reflected in Copilot and Microsoft Search results.

## Manage your connector

After you publish your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/). For more information, see [Manage your connector](manage-connector.md).

The connector status page shows the following information:

- **Last crawl status**: Indicates whether the most recent crawl completed successfully or encountered errors.
- **Items indexed**: The number of schedule items currently indexed and available in Copilot and Microsoft Search.
- **Crawl history**: A log of recent crawl operations, including start time, duration, and results.

If the connector encounters errors, see [Troubleshoot the PagerDuty Schedules connector](pagerduty-schedules-troubleshooting.md) for resolution steps.

## Next step

> [!div class="nextstepaction"]
> [Troubleshoot the PagerDuty Schedules connector](pagerduty-schedules-troubleshooting.md)
