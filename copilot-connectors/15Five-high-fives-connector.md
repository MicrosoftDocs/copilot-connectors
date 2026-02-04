---

title: "15Five High Fives Microsoft 365 Copilot connector (preview)" 
ms.author: wangchen
author: wangchen
manager: zezhangzhao
audience: Admin
ms.audience: Admin 
ms.topic: install-set-up-deploy
ms.service: mssearch 
ms.localizationpriority: Medium 
description: "Set up the 15Five High Fives Microsoft 365 Copilot connector (preview)." 
ms.date: 08/15/2025
---

# 15Five High Fives Microsoft 365 Copilot connector (preview)

The 15Five High Fives Microsoft 365 Copilot connector enables your organization to index 15Five high-five data to make it available to Microsoft 365 Copilot and Microsoft Search. 

This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors the 15Five High Fives Copilot connector. 

[!INCLUDE [conector-preview-access](includes/connector-preview-access.md)]

## Capabilities
- Access 15Five high fives using the power of semantic search.
- Customize your crawl frequency.
- Create workflows by using this connection and plugins from Microsoft Copilot Studio.

## Limitations
- Only public high-fives are indexed.

## Prerequisites
- Create a 15Five account with HR administrator permission.
- As an HR administrator, go to the Integrations admin setting page in 15Five. Create a company API key and get the access token.

## Get started

### Choose display name   
Choose a display name that helps users easily recognize associated files or items in a Copilot response.

### Add the instance URL
The default 15Five instance URL is `https://my.15five.com`.

### Choose authentication type
Select the available authentication type and enter the access token you obtained from your 15Five company API keys setting.

### Roll out to a limited audience
Deploy this connection to a limited user base to validate it in Copilot and other search surfaces before you roll it out to a broader audience.

## Custom setup 

In custom setup you can edit any of the default values for users, content, and sync.

### Users 

#### Access permissions

All 15Five high-five data indexed via the 15Five High Fives Copilot connector is visible to all Microsoft 365 users in your tenant in Microsoft Search or Copilot.

### Content 

#### Manage properties

You can add or remove available properties from your 15Five data source. Assign a schema, change the semantic label, and add an alias to the property. The following properties are indexed by default.

|Source property|Label|Description|
|--- | ---- | --- |
|Text |Not applicable  | Description of the high-five content. |
|CreatorEmail |Not applicable  | Email of the user who gives a high five. |
|CreatorName | `createdBy` | Name of the user who gives a high five. |
|Receivers |Not applicable  | Name of the users who receive a high five. |
|CreateTime | `createdDateTime` | The time at which the high five was created. |
|UpdateTime	| `lastModifiedDateTime` | The last time the high five was modified. |

### Sync 
You can configure full and incremental crawls based on the scheduling options described. By default, incremental crawl is set for every 15 minutes, and full crawl is set for every day. You can adjust these schedules to fit your data refresh needs.

## Troubleshooting
The following are common errors that can occur and how to resolve them.

1. Your security credentials have expired for this session. Please go back and sign in again with your App key and App secret.
Credential information has expired. Create a new key in the 15Five integrations setting and copy the latest access token from **settings**  in 15Five to authenticate.

2. Invalid Credentials detected. Please check the credential info and the permission scopes of the 15Five App.
This is a common credential error. Go to the 15Five integrations setting and verify that the access token is correct.

## Next steps

After you publish your connection, you can review the status in the **Connectors** section of the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, see [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).
