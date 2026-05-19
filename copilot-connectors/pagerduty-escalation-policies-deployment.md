---
title: "Deploy the PagerDuty Escalation Policies connector"
ms.author: wangchen
author: wangchen
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 08/15/2025
ms.localizationpriority: Medium
description: "Find information about how to deploy the PagerDuty Escalation Policies Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the PagerDuty Escalation Policies connector

The PagerDuty Escalation Policies Microsoft 365 Copilot connector integrates PagerDuty escalation policy data into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface relevant escalation policy information directly within apps like Microsoft Teams, Outlook, and SharePoint. This article describes the steps to deploy and customize the PagerDuty Escalation Policies connector.

[!INCLUDE [conector-preview-access](includes/connector-preview-access.md)]

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be a Microsoft 365 admin.
- You must have a PagerDuty account with administrator permission in the PagerDuty app.
- The PagerDuty environment must be configured to allow API access.
- For advanced features, a PagerDuty Business or Enterprise plan license is required to index audit-related properties (createdBy, createdDateTime, lastModifiedBy, lastModifiedDateTime).

### Configure PagerDuty OAuth application

Before you deploy the connector, you must create an OAuth application in PagerDuty:

1. In PagerDuty, add a new app with OAuth 2.0 functionality enabled. For more information, see [OAuth Functionality](https://developer.pagerduty.com/docs/oauth-functionality) and [Register an App](https://developer.pagerduty.com/docs/register-an-app).
2. Select **Scoped OAuth** in the PagerDuty new app registration setting page.
3. Use the following links for the **Redirect URL** field in the PagerDuty new app registration setting page:
   - For M365 Enterprise, use: `https://gcs.office.com/v1.0/admin/oauth/callback`
   - For M365 Government, use: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
4. Select the following scopes in the PagerDuty new app registration setting page:
   - **Audit records** – Read Access
   - **Escalation Policies** – Read Access
   - **Teams** – Read Access
   - **Users** – Read Access
5. After you successfully complete app registration in PagerDuty, copy the **Client ID** and **Client Secret**.

## Deploy the connector

To add the PagerDuty Escalation Policies connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
2. Choose the **Gallery** tab.
3. From the list of available connectors, choose **PagerDuty Escalation Policies**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated escalation policy or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **PagerDuty Escalation Policies** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Set instance REST API URL

PagerDuty allows customers to choose the geographic service region of the PagerDuty data centers that host their account.

- For the US service region, the REST API URL is: `https://api.pagerduty.com`
- For the EU service region, the REST API URL is: `https://api.eu.pagerduty.com`

For more information, see [Service regions](https://support.pagerduty.com/main/docs/service-regions).

### Choose authentication type

The PagerDuty Escalation Policies connector supports the following authentication type:

- **OAuth 2.0** (recommended): Secure and scalable authentication using PagerDuty's OAuth flow.

To use **PagerDuty OAuth** for authentication, enter the **Client ID** and **Client Secret** you obtained from your PagerDuty app registration setting in the prerequisites section.

### Roll out to a limited audience

Deploy this connection to a limited user base to validate it in Copilot and other search surfaces before you roll it out to a broader audience.

## Custom setup

In custom setup you can edit any of the default values for users, content, and sync.

### Users

#### Access permissions

Determine which users in your organization can access each item in Copilot or Search surfaces. Choose whether indexed data is visible to everyone in the organization or only to users who have access to the data source.

**Important**: When Advanced Permissions is enabled in PagerDuty, only members of the teams linked to a specific escalation policy can access and search for that escalation policy in Microsoft Search and Microsoft 365 Copilot.

### Content

#### Manage properties

You can add or remove available properties from your PagerDuty Escalation Policy data source. Assign a schema, change the semantic label, and add an alias to the property. The following properties are indexed by default.

| Source property     | Label                | Description |
|:--------------------|:---------------------|:------------|
| Id                  | Not applicable       | Unique ID of the escalation policy. |
| HtmlUrl             | `url`                | URL of the escalation policy in PagerDuty. |
| CreatedBy           | `createdBy`          | The name of the user who created the escalation policy. |
| CreatedTime         | `createdDateTime`    | The time at which the escalation policy was created. |
| LastModifiedBy      | `lastModifiedBy`     | The name of the user who last modified the escalation policy. |
| LastModifiedTime    | `lastModifiedDateTime` | The time at which the escalation policy was last modified. |
| Name                | `title`              | The name of the escalation policy. |
| Summary             | Not applicable       | A short-form, server-generated string by PagerDuty that provides succinct, important information about an object suitable for primary labeling of an entity in a client. In many cases, it's identical to `name`, though it is not intended to be an identifier. |
| Description         | Not applicable       | Escalation policy description. |
| RuleDetail          | Not applicable       | This property is a list of entries in the escalation policy, including the number of minutes before an unacknowledged incident escalates away from this rule, and the targets an incident should be assigned to upon reaching the rule. |
| UsedByServices      | Not applicable       | The services associated with the escalation policy. |

### Sync

The PagerDuty Escalation Policies Copilot connector only supports full crawl. The default schedule of the full crawl is set for every day. If needed, you can adjust these schedules to fit your data refresh needs.

## Next steps

After you publish your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com). For more information, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, contact [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).

## Related content

- [PagerDuty Escalation Policies connector overview](pagerduty-escalation-policies-overview.md)
- [Troubleshoot issues with the PagerDuty Escalation Policies connector](pagerduty-escalation-policies-troubleshooting.md)
