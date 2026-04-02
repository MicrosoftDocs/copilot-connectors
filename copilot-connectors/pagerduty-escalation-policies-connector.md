---

title: "PagerDuty Escalation Policies connector (preview)" 
ms.author: wangchen
author: wangchen
manager: zezhangzhao
audience: Admin
ms.audience: Admin 
ms.topic: install-set-up-deploy
ms.service: copilot-connectors 
ms.localizationpriority: Medium 
description: "Set up the PagerDuty Escalation Policies Copilot connector for Microsoft Search and Microsoft 365 Copilot." 
ms.date: 08/15/2025
---

# PagerDuty Escalation Policies Copilot connector (preview)
The PagerDuty Escalation Policies Copilot connector enables your organization to index PagerDuty escalation policy data to make it available to Microsoft 365 Copilot and Microsoft Search. 

[!INCLUDE [conector-preview-access](includes/connector-preview-access.md)]

## Capabilities
- Access PagerDuty escalation policies in Copilot using the power of Semantic search.
- Retain ACLs defined by your organization.
- Customize your crawl frequency.
- Create workflows using this connection and plugins from Microsoft Copilot Studio.

## Limitations
- When Advanced Permissions is enabled in PagerDuty, only members of the teams linked to a specific escalation policy can access and search for that escalation policy in Microsoft Search and Microsoft 365 Copilot.
- A PagerDuty Business or Enterprise plan license is required to index the following data properties: createdBy, createdDateTime, lastModifiedBy, and lastModifiedDateTime.

## Prerequisites
Before you create a PagerDuty Escalation Policies Copilot connector, complete the following steps:

1. Create a PagerDuty account with administrator permission in the PagerDuty app.
2. Add a new app in PagerDuty with OAuth 2.0 functionality enabled. For more information, see [OAuth Functionality](https://developer.pagerduty.com/docs/oauth-functionality) and [Register an App](https://developer.pagerduty.com/docs/register-an-app).
3. Select 'Scoped OAuth' in PagerDuty new app registration setting page.
4. Use the following links for the field 'Redirect URL' in PagerDuty new app registration setting page.

   - For M365 Enterprise, use `https://gcs.office.com/v1.0/admin/oauth/callback`
   
   - For M365 Government, use `https://gcsgcc.office.com/v1.0/admin/oauth/callback`

7. Select the following scopes in PagerDuty new app registration setting page.

   - Audit records – Read Access
   - Escalation Policies – Read Access
   - Teams – Read Access
   - Users – Read Access

8. After you successfully complete app registration in PagerDuty, copy Client ID and Client Secret.

## Get started

### 1. Configure display name   
Choose a display name that helps users easily recognize associated files or items in a Copilot response.

### 2. Add the instance REST API URL
PagerDuty allows customers to choose the geographic service region of the PagerDuty data centers that host their account. 

- For the US service region, the REST API URL is https://api.pagerduty.com.
- For the EU service region, the REST API URL is https://api.eu.pagerduty.com.

For more information, see [Service regions](https://support.pagerduty.com/main/docs/service-regions).

### 3. Provide authentication type
Enter the Client ID and Client Secret you obtained from your PagerDuty app registration setting.

### 4. Roll out to a limited audience
Deploy this connection to a limited user base to validate it in Copilot and other search surfaces before you roll it out to a broader audience.

## Custom setup 
In custom setup you can edit any of the default values for users, content, and sync. 

### Users 

### Access permissions
Determine which users in your organization can access each item in Copilot or Search surfaces. Choose whether indexed data is visible to everyone in the organization or only to users who have access to the data source.

### Content 

#### Manage properties
You can add or remove available properties from your PagerDuty Escalation Policy data source. Assign a schema, change the semantic label, and add an alias to the property. The following properties are indexed by default.

|Source property|Label|Description|
|:--- |:---- |:--- |
|Id |Not applicable  | Unique ID of the escalation policy. |
|HtmlUrl |`url`  | URL of the escalation policy in PagerDuty. |
|CreatedBy |`createdBy`  | The name of the user who created the escalation policy. |
|CreatedTime | `createdDateTime` | The time at which the escalation policy was created. |
|LastModifiedBy	| `lastModifiedBy` | The name of the user who last modified the escalation policy. |
|LastModifiedTime	| `lastModifiedDateTime` | The time at which the escalation policy was last modified. |
|Name	| `title` | The name of the escalation policy. |
|Summary	| Not applicable | A short-form, server-generated string by PagerDuty that provides succinct, important information about an object suitable for primary labeling of an entity in a client. In many cases, it's identical to `name`, though it is not intended to be an identifier. |
|Description	| Not applicable         | Escalation policy description. |
|RuleDetail	| Not applicable         | This property is a list of entries in the escalation policy, including the number of minutes before an unacknowledged incident escalates away from this rule, and the targets an incident should be assigned to upon reaching the rule. |
|UsedByServices	| Not applicable | The services associated with the escalation policy. |

### Sync 
The PagerDuty Escalation Policies Copilot connector only supports full crawl. The default schedule of the full crawl is set for every day. If needed, you can adjust these schedules to fit your data refresh needs. 

## Troubleshooting
The following are common errors that can occur and how to resolve them.

1. Your security credentials have expired for this session. Please go back and sign in again with your Client ID and Client secret.
Credential info expires. Create a new app ID in the PagerDuty app registration setting and copy the latest Client ID and Client secret from **settings** to authenticate.

2. Invalid credentials detected. Please check the credential info and check the permission scopes of the PagerDuty App.
Common credential error. Go back to the PagerDuty app registration setting and check if the Client ID and Client secret have the correct permission scope.

## Next steps
After you publish your connection, you can review the status in the **Connectors** section of the [admin center](https://admin.microsoft.com). For more information, see [Manage your connector](manage-connector.md).
If you have issues or want to provide feedback, contact [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).
