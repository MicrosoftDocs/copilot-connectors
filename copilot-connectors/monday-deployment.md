---
title: "Deploy the monday.com Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: huichunli
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 01/13/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the monday.com Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and rollout guidance."
---

# Deploy the monday.com Microsoft 365 Copilot connector

The monday.com Microsoft 365 Copilot connector integrates monday.com items into the Microsoft 365 ecosystem, allowing Microsoft 365 Copilot, Copilot Search, and Microsoft Search to surface project and task data from monday.com across Microsoft 365 experiences.

This article describes how to deploy and configure the monday.com connector in the Microsoft 365 admin center.

## Prerequisites

Before you deploy the monday.com connector, make sure that you meet the following prerequisites:

- You're an AI administrator for your organization.
- You have access to your organization’s monday.com instance URL (for example, `https://contoso.monday.com`).
- You have the required permissions in monday.com to create or manage OAuth applications.
- You understand your monday.com plan limits, including daily API call limits.

## Deploy the connector

To add the monday.com connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, select **Copilot** > **Connectors**.
1. Go to the **Connectors** tab, and then select **Gallery**.
1. From the list of available connectors, select **monday.com**.

### Set display name

The display name is used to identify references in Copilot responses and search results to help users recognize the source of the content. The display name also indicates trusted content and is used as a content source filter.

You can accept the default **monday** display name, or customize it to use a name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

### Set instance URL

Enter the instance URL of your monday.com tenant. The URL typically follows this format:

- `https://<your-instance>.monday.com`

### Choose authentication type

The monday.com connector supports the following authentication options:

- OAuth (recommended).
- OAuth 2.0 with a customized monday.com app.

#### OAuth (recommended)

With OAuth authentication, you install and authorize the Microsoft 365 Copilot monday app in your monday.com workspace. During authorization, you sign in to monday.com and grant read permissions required for content ingestion.

This option requires minimal configuration and is recommended for most organizations.

1. Install the Microsoft 365 Copilot monday app on your monday Workspaces via this [link](https://auth.monday.com/oauth2/authorize?client_id=1347fa4e96575c4b06f577e8fd06407b&response_type=install).

1. Review the workspaces you want to use and the corresponding Microsoft 365 Copilot access level before you choose the install button in the pop-up window.

1.  Choose **Authorize** to sign in and grant access.

#### OAuth 2.0 with customized app

With OAuth 2.0, you create and configure your own OAuth app in the monday.com Developer Center. You record the client ID and client secret, enable required read scopes, configure redirect URLs, and promote the app to live status before you use it with the connector.

Use this option when your organization requires a custom OAuth app configuration.

1. Sign in your monday.com account and go to the **monday.com Developer Center**.

    :::image type="content" source="media/monday-deployment/monday-dev-center.png" alt-text="Screenshot of the monday.com Developer Center page." lightbox="media/monday-deployment/monday-dev-center.png":::

1. Choose **Create app**.

    :::image type="content" source="media/monday-deployment/create-app.png" alt-text="Screenshot of the Create app button in the monday.com Developer Center." lightbox="media/monday-deployment/create-app.png":::

1. In the **General Settings** section, locate and note down your **client ID** and **client secret**.

    :::image type="content" source="media/monday-deployment/general-settings.png" alt-text="Screenshot of the General Settings section showing client ID and client secret." lightbox="media/monday-deployment/general-settings.png":::

1. In the **Build** section, open the **OAuth & permission** tab, choose the **Scopes** tab, and enable all read permissions.

    :::image type="content" source="media/monday-deployment/read-permissions.png" alt-text="Screenshot of the OAuth & permission tab with Scopes subtab showing read permissions." lightbox="media/monday-deployment/read-permissions.png":::

1. Go to the **Redirect URLs** tab, enter the following redirect URLs, and choose **Save Scopes**.

    - **For Microsoft 365 Enterprise:** `https://gcs.office.com/v1.0/admin/oauth/callback` 
    - **For Microsoft 365 Government:** `https://gcsgcc.office.com/v1.0/admin/oauth/callback`

    :::image type="content" source="media/monday-deployment/redirect-urls.png" alt-text="Screenshot of the Redirect URLs subtab with URL input fields." lightbox="media/monday-deployment/redirect-urls.png":::

1.  Choose **Promote to Live** to activate the app.

    :::image type="content" source="media/monday-deployment/promote-to-live.png" alt-text="Screenshot of the Promote to Live button." lightbox="media/monday-deployment/promote-to-live.png":::

Next:

1.  Enter your client ID and client secret from monday.com.
1.  Choose **Authorize** to sign in and grant access.
1.  Grant the required API scopes.

### Roll out

You can deploy the connector to a limited audience to validate results in Copilot and Microsoft Search before you make the connector available more broadly.

To roll out to a limited set of users:

- Turn on **Rollout to limited audience**.
- Specify the users or groups that can access the connector content.

When you’re ready, choose **Create** to publish the connection. The connector starts indexing content right away.

The monday.com connector provides default settings that are optimized for typical monday.com usage. The following table lists the default values that are set when you create the connection:

| Category | Setting | Default value |
| --- | --- | --- |
| Users | Access permissions | Only people with access to this data source. |
| Users | Identity mapping | Data source identities mapped using Microsoft Entra ID. |
| Content | Index content | All boards and items, excluding personal spaces. For a list of properties, see [Customize content settings](#customize-content-settings). |
| Crawl | Incremental crawl | Every four hours. |
| Crawl | Full crawl | Every day. |

These values help balance content freshness while respecting monday.com API limits.

To customize the default values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values after you create the connection by choosing **Custom setup**. Custom setup includes the following tabs:

- **Users**
- **Content**
- **Crawl**

### Customize user settings

#### Access permissions

The monday.com Copilot connector supports data visible to **Only people with access to this data source (recommended)** or **Everyone**. If you choose **Everyone**, indexed data appears in the search results for all users.

#### Map identities

To ensure correct permission enforcement, map monday.com user identities to Microsoft Entra ID.

- Choose the Microsoft Entra ID option if the email ID of monday.com users is same as the user principal name (UPN) of users in Microsoft Entra ID.
- Choose the non-Entra ID option if the email ID of monday.com users is different from the UPN of users in Microsoft Entra ID.

> [!IMPORTANT]
> - If you choose Microsoft Entra ID as the type of identity source, the connector maps the email IDs of users from monday.com directly to the **UPN** property from Microsoft Entra ID.
> - If you chose **non-Entra ID** for the identity type, provide the mapping regular expression from email ID to UPN. For more information, see [Map your non-Entra ID identities](map-non-entra-id.md). 
> - Updates to users or groups that govern access permissions are synced in full crawls only. Incremental crawls don't currently support processing updates to permissions.

### Customize content settings

#### Content ingestion filters 

You can choose what data you want to index. Use the regex expression of WorkSpaces to select your data before it's indexed to control what data is searchable. The following examples show how to use regex expressions to select specific workspaces.

| **Scenario** | **Example workspace names** | **Regex expression** | **Notes** |
|----|----|----|----|
| Exact match for a single workspace | workspace1 | ^workspace1\$ | Exact match of workspace1 |
| Fuzzy match for a single workspace | team-marketing-q1 | .\*marketing.\* | Matches any workspace that contains marketing in the name |
| Exact match for multiple workspaces | workspace1, workspace2 | ^(workspace1\|workspace2)\$ | Matches exactly workspace1 or workspace2 |
| Fuzzy match for multiple workspaces | workspace-marketing, workspace-sales | ^workspace-\[a-z\]+\$ | Matches any workspace starting with workspace- and letters |
| Fuzzy match for multiple keywords in name | workspace-engineering, workspace-sales-q4 | .\*(eng\|sales).\* | Matches workspaces that contain engineering or sales in the name |

Choose **Preview results** to verify sample values of the selected properties and filters.

#### Manage properties

Check available properties from your monday.com instance. Assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), review the semantic label, and add an alias to the property. The following table lists properties that are selected by default.

| **Default Property** | **Label** | **Description** | **Schema** |
|----|----|----|----|
| Authors | Authors | The author of the items | Query, Retrieve, Search |
| BoardDescription | None | Description of the board. | Retrieve, Search. |
| BoardID | None | Unique identifier for the board. | Query, Retrieve. |
| BoardName | None | Name of the board. | Query, Retrieve, Search, Refine |
| BoardUrl | None | URL link to the board. | Query, Retrieve. |
| Content | CONTENT | Merge all columns and corresponding values of the item. | Search. |
| CreatedBy | Created by | User who created the item. | Query, Retrieve, Search |
| CreatedDateTime | Created date time | Timestamp when the item was created. | Query, Retrieve. |
| GroupID | None | Unique identifier for the group. | Query, Retrieve. |
| GroupName | None | Name of the group. | Query, Retrieve, Search. |
| IconUrl | IconUrl | URL related to the icon. | Retrieve |
| ItemPath | None | Path of the item. | Query, Retrieve, Search, Refine. |
| ItemTerminology | None |  | Query, Retrieve, Refine. |
| LastModifiedBy | Last modified by | User of the last modification. | Query, Retrieve, Search. |
| LastModifiedDateTime | Last modified date time | Timestamp of the last modification. | Query, Retrieve. |
| Title | Title | Title of the task item. | Query, Retrieve, Search. |
| URL | url | URL related to the item. | Retrieve. |
| WorkspaceDescription | None | Description of the workspace. | Retrieve, Search. |
| WorkspaceID | None | Unique identifier for the workspace. | Query, Retrieve. |
| WorkspaceName | None | Name of the workspace. | Query, Retrieve, Search, Refine. |

##### Content property

The **Content** field contains a JSON object that represents all the columns and their corresponding values for a given item. Each key in the JSON object corresponds to a column name (such as Assignee or Status), and each value holds the specific data for that item. The following example shows how an item and its **Content** field are structured.

:::image type="content" source="media/monday-deployment/content-field.png" alt-text="Screenshot of an example item showing the Content field structure with columns and values." lightbox="media/monday-deployment/content-field.png":::

```JSON
{  
"Assignee": "QC",  
"Status": "Not Started",  
"Date": "Apr 2",  
"Priority": "Medium",  
"Labels": "Benefits, Flexible"  
}
```

### Customize crawl intervals

The connector supports two crawl types:

- **Incremental crawl**, which captures recent changes.
- **Full crawl**, which refreshes all indexed content.

By default, incremental crawls run every four hours and full crawls run daily. You can adjust these values, but consider monday.com daily API call limits if you configure more frequent sync schedules. 

> [!IMPORTANT]
> **monday.com daily API call limits**
>
> monday.com enforces daily API call limits that vary by plan. All API calls made by the connector count toward this daily limit. The following call limits apply:
>
> - Standard/Basic plan: 1,000 API calls per day
> - Free/Trial: 200 API calls per day
> - Pro and Enterprise plans support higher limits
>
> For more information, see [Rate limits](https://developer.monday.com/api-reference/docs/rate-limits#daily-call-limit).
>
> If crawl frequency is set too high, your organization might reach monday.com daily API limits, which can result in crawl failures.

For more information, see [Guidelines for sync settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [monday.com connector overview](monday-overview.md)
- [Troubleshoot issues with the monday.com connector](monday-troubleshooting.md)
