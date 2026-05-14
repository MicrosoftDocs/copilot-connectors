---

title: "PagerDuty Incidents connector (preview)" 
ms.author: wangchen
author: wangchen
manager: zezhangzhao
audience: Admin
ms.audience: Admin 
ms.topic: install-set-up-deploy
ms.service: copilot-connectors 
ms.localizationpriority: Medium 
description: "Set up the PagerDuty Incidents Copilot connector for Microsoft Search and Microsoft 365 Copilot." 
ms.date: 05/15/2026
---

# PagerDuty Incidents Copilot connector (preview)

The PagerDuty Incidents Copilot connector enables your organization to index PagerDuty incidents data to make it available to Microsoft 365 Copilot and Microsoft Search. 

[!INCLUDE [conector-preview-access](includes/connector-preview-access.md)]

## Capabilities
- Access PagerDuty incidents in Copilot using the power of Semantic search.
- Retain ACLs defined by your organization.
- Customize your crawl frequency.
- Create workflows by using this connection and plugins from Microsoft Copilot Studio.

## Prerequisites
1. Create a PagerDuty account with administrator permission in the PagerDuty application.
2. Add a new app in PagerDuty with OAuth 2.0 functionality enabled. For more information, see [OAuth Functionality](https://developer.pagerduty.com/docs/oauth-functionality) and [Register an App](https://developer.pagerduty.com/docs/register-an-app).
3. Select 'Scoped OAuth' in PagerDuty new app registration setting page.
4. Use the following links for the field 'Redirect URL' in PagerDuty new app registration setting page.
   
   - For M365 Enterprise, use `https://gcs.office.com/v1.0/admin/oauth/callback)`
   
   - For M365 Government, use `(https://gcsgcc.office.com/v1.0/admin/oauth/callback)`

7. Select the following scopes in PagerDuty new app registration setting page.

   - Audit records – Read Access

   - Schedules – Read Access

   - Teams – Read Access

   - Users – Read Access

   - Incidents - Read Access
     
   - Incident Types - Read Access

8. After you successfully complete app registration in PagerDuty, copy Client ID and Client Secret.

## Get started

### 1. Choose display name   
Choose a display name that helps users easily recognize associated files or items in a Copilot response.

### 2. Add the Instance REST API URL
PagerDuty allows customers to choose the geographic service region of the PagerDuty data centers that host their account. 

- For the US service region, the REST API URL is (https://api.pagerduty.com).
- For the EU service region, the REST API URL is (https://api.eu.pagerduty.com).

For more information, see [Service regions](https://support.pagerduty.com/main/docs/service-regions).

### 3. Choose authentication type
Enter the Client ID and Client Secret you obtained from your PagerDuty app registration setting.

### 4. Roll out to a limited audience
Deploy this connection to a limited user base to validate it in Copilot and other search surfaces before you roll it out to a broader audience.

## Custom setup 
In custom setup, you can edit any of the default values for users, content, and sync.

### Users 

#### Access permissions

Determine which users in your organization can access each item in Copilot or Search surfaces. Choose whether indexed data is visible to everyone in the organization or only to users who have access to the data source.

### Content 

#### Content filter

Two extra parameters can be used to specify the date range for crawling incidents content in PagerDuty.

- Since (Month)

The date range to crawl incident content in PagerDuty. The crawl start date is (Today - Since) and the crawl end date is Today.

#### Manage properties
To view available properties, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias in the property. Some properties are selected by default.

|Source property|Label|Description|
|:---- |:---- |:---- |
|AcknowledgedBy | Not applicable | The users who acknowledged the incident. |
|AssignedTo | Not applicable | The users assigned to the incident. |
|ConferenceNumber | Not applicable | The conference number for the incident. |
|ConferenceUrl | Not applicable | The conference URL for the incident. |
|Content | `CONTENT` | The content of the incident. |
|CreatedDateTime | `createdDateTime` | The time at which the incident was created. |
|EscalationPolicyName | Not applicable | The name of the escalation policy associated with the incident. |
|HtmlUrl | `url` | URL of the incident in PagerDuty. |
|IconUrl | `IconUrl` |  |
|Id | Not applicable | Unique ID of the incident. |
|IncidentKey | Not applicable | The incident key. |
|IncidentNumber | Not applicable | The incident number. |
|IncidentType | Not applicable | The type of the incident. |
|LastModifiedDateTime | `lastModifiedDateTime` | The time at which the incident was last modified. |
|LastStatusChangeAt | Not applicable | The time at which the incident status was last changed. |
|LastStatusChangeBy | Not applicable | The user who last changed the incident status. |
|Priority | Not applicable | The priority of the incident. |
|ResolveReason | Not applicable | The reason the incident was resolved. |
|ResolvedAt | Not applicable | The time at which the incident was resolved. |
|ServiceName | Not applicable | The name of the service associated with the incident. |
|Status | Not applicable | The status of the incident. |
|Summary | Not applicable | A short-form, server-generated string by PagerDuty that provides succinct, important information about the incident. |
|Teams | Not applicable | The teams associated with the incident. |
|Title | `title` | The title of the incident. |
|Urgency | Not applicable | The urgency of the incident. |


### Sync 
Both full crawl and incremental crawl are supported by PagerDuty Incidents Copilot connector. The default schedule of the full crawl is set for every day. If needed, you can adjust these schedules to fit your data refresh needs. 

## Troubleshooting

The following are common errors that can occur and how to resolve them.

1. Your security credentials have expired for this session. Please go back and sign in again with your Client ID and Client secret.
Credential info expires. Create a new app id in PagerDuty app registration setting and copy the latest Client ID and Client secret from the setting tab to authenticate.

1. Invalid credentials detected. Please check the credential info and check the permission scopes of the PagerDuty App.
Common credential error. Go back to the PagerDuty app registration setting and check if the Client ID and Client secret have the correct permission scope.

## Next steps
After you publish your connection, you can review the status in the **Connectors** section of the [admin center](https://admin.microsoft.com). For more information, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, contact [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).
