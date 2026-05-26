---
title: "Deploy the PagerDuty Escalation Policies connector"
ms.author: wangchen
author: wangchen
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 05/26/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the PagerDuty Escalation Policies Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the PagerDuty Escalation Policies connector

The PagerDuty Escalation Policies Microsoft 365 Copilot connector integrates PagerDuty escalation policy data into Microsoft 365. When you deploy this connector, Copilot, Copilot Search, and Microsoft Search can surface relevant escalation policy information directly within apps like Microsoft Teams, Outlook, and SharePoint. 

This article describes the steps to deploy and customize the PagerDuty Escalation Policies connector.

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be a Microsoft 365 admin.
- You have a PagerDuty account with administrator permission in the PagerDuty app.
- The PagerDuty environment is configured to allow API access.
- For advanced features, a PagerDuty Business or Enterprise plan license is required to index audit-related properties (createdBy, createdDateTime, lastModifiedBy, lastModifiedDateTime).

### Configure PagerDuty OAuth application

Before you deploy the connector, create an OAuth application in PagerDuty:

1. In PagerDuty, add a new app with OAuth 2.0 functionality enabled. For more information, see [OAuth Functionality](https://developer.pagerduty.com/docs/oauth-functionality) and [Register an App](https://developer.pagerduty.com/docs/register-an-app).
1. Select **Scoped OAuth** in the PagerDuty new app registration setting page.
1. Use the following links for the **Redirect URL** field in the PagerDuty new app registration setting page:
   - For M365 Enterprise, use: `https://gcs.office.com/v1.0/admin/oauth/callback`
   - For M365 Government, use: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
1. Select the following scopes in the PagerDuty new app registration setting page:
   - **Audit records** – Read Access
   - **Escalation Policies** – Read Access
   - **Teams** – Read Access
   - **Users** – Read Access
1. After you successfully complete app registration in PagerDuty, copy the **Client ID** and **Client Secret**.

## Deploy the connector

To add the PagerDuty Escalation Policies connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, select **Copilot** > **Connectors**.
1. Select the **Gallery** tab.
1. From the list of available connectors, select **PagerDuty Escalation Policies**.

### Set display name

Use the display name to identify references in Copilot responses so users can recognize the associated escalation policy or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **PagerDuty Escalation Policies** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Set instance REST API URL

PagerDuty customers can choose the geographic service region for the PagerDuty data centers that host their account.

- For the US service region: `https://api.pagerduty.com`
- For the EU service region: `https://api.eu.pagerduty.com`

For more information, see [Service regions](https://support.pagerduty.com/main/docs/service-regions).

### Choose authentication type

The PagerDuty Escalation Policies connector supports the following authentication type:

- **OAuth 2.0** (recommended): Secure and scalable authentication by using PagerDuty's OAuth flow.

To use **PagerDuty OAuth** for authentication, enter the **Client ID** and **Client Secret** you obtained from your PagerDuty app registration settings in the prerequisites section.

### Roll out

To roll out to a limited audience, select the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](staged-rollout.md).

Select **Create** to deploy the connection. The PagerDuty Escalation Policies connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
| --- | --- |
| Users | All users in the organization can access indexed escalation policies |
| Content | All default properties are indexed |
| Sync | Full crawl runs daily |

To customize these values, select **Custom setup**. For more information, see [Customize settings (optional)](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the PagerDuty Escalation Policies connector settings. To customize settings, on the connector page in the admin center, select **Custom setup**.

### Customize user settings

#### Access permissions

Determine which users in your organization can access each item in Copilot or Search surfaces. Choose whether indexed data is visible to everyone in the organization or only to users who have access to the data source.

**Important**: When you enable Advanced Permissions in PagerDuty, only members of the teams linked to a specific escalation policy can access and search for that escalation policy in Microsoft Search and Microsoft 365 Copilot.

### Customize content settings

#### Manage properties

You can add or remove properties from your PagerDuty Escalation Policy data source. Assign a schema, change the semantic label, and add an alias to the property. The following properties are indexed by default.

| Source property | Label | Description |
| --- | --- | --- |
| Id | Not applicable | Unique ID of the escalation policy. |
| htmlUrl | `url` | URL of the escalation policy in PagerDuty. |
| createdBy | `createdBy` | The name of the user who created the escalation policy. |
| createdTime | `createdDateTime` | The time at which the escalation policy was created. |
| lastModifiedBy | `lastModifiedBy` | The name of the user who last modified the escalation policy. |
| lastModifiedTime | `lastModifiedDateTime` | The time at which the escalation policy was last modified. |
| name | `title` | The name of the escalation policy. |
| summary | Not applicable | A short-form, server-generated string by PagerDuty that provides succinct, important information about an object suitable for primary labeling of an entity in a client. In many cases, it's identical to `name`, though it is not intended to be an identifier. |
| description | Not applicable | Escalation policy description. |
| ruleDetail | Not applicable | This property is a list of entries in the escalation policy, including the number of minutes before an unacknowledged incident escalates away from this rule, and the targets an incident should be assigned to upon reaching the rule. |
| usedByServices | Not applicable | The services associated with the escalation policy. |

### Customize sync intervals

The PagerDuty Escalation Policies connector only supports full crawl. The default schedule of the full crawl is set for every day. If needed, you can adjust these schedules to fit your data refresh needs.

For more information, see [Guidelines for sync settings](deployment-overview.md#guidelines-for-sync-settings).

## Related content

- [PagerDuty Escalation Policies connector overview](pagerduty-escalation-policies-overview.md)
- [Troubleshoot issues with the PagerDuty Escalation Policies connector](pagerduty-escalation-policies-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](deployment-overview.md)
