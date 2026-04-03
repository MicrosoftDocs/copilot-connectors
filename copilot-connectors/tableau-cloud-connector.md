--- 
title: "Tableau Cloud connector(preview)" 
ms.author: lauragra
author: lauragra
manager: jecui
audience: Admin
ms.audience: Admin 
ms.topic: install-set-up-deploy
ms.service: copilot-connectors 
ms.localizationpriority: Medium 
description: "Set up the Tableau Cloud  Microsoft 365 Copilot connector" 
ms.date: 08/15/2025
---

# Tableau Cloud  connector (preview)

With the Tableau Cloud  Microsoft 365 Copilot connector, your organization can index Tableau sheets in your Tableau Cloud. After you configure the connector and index content from Tableau Cloud, end users can search for those sheets in Microsoft 365 Copilot and from any Microsoft Search client.

[!INCLUDE [conector-preview-access](includes/connector-preview-access.md)]

## Capabilities
- Index sheets of your Tableau Cloud and supports ingestion filters based on top-level projects.
- Retain access control lists (ACLs) defined by your organization.
- Customize your crawl frequency.
- Create workflows using this connection and plugins from Microsoft Copilot Studio.  
- Use [Semantic search in Copilot](/microsoftsearch/semantic-index-for-copilot) to enable users to find relevant content.

## Limitations
- Sheets in personal space can't be indexed.

## Prerequisites
- You must be the **AI administrator** for your organization's Microsoft 365 tenant.

- **Configure Connected Apps with Direct Trust in Tableau**: To connect to Tableau Cloud and enable the Tableau Cloud Copilot connector to sync sheets regularly, you need to configure and enable Connected Apps with Direct Trust on your Tableau site, using credentials that can access the sheets. Tableau Connected Apps provide a seamless and secure authentication experience by establishing an explicit trust relationship between your Tableau Cloud site and external applications. Find more details [here](https://help.tableau.com/current/online/en-us/connected_apps_direct.htm?_gl=1*9bs6y1*_ga*MTk1OTAyNzg0MS4xNzIxMTIwMzA4*_ga_8YLN0SNXVS*MTczNTE5MzU5OS4zNC4xLjE3MzUyMDA1ODEuMC4wLjA.).

## Get started

### 1. Display name 
A display name is used to identify each citation in Copilot, helping users easily recognize the associated file or item. Display name also signifies trusted content. The display name is also used as a [content source filter](/microsoftsearch/custom-filters#content-source-filters). A default value is present for this field, but you can customize it to a name that users in your organization recognize.

### 2. Tableau Cloud Site URL
A Tableau Cloud site URL typically looks like `https://<your-domain>.online.tableau.com/#/site/<site-name>`

### 3. Authentication Type
To enable and configure the Connected Apps with Direct Trust for Tableau Cloud, use the following steps to use Tableau Connected Apps with Direct Trust for authentication.

**Step 1: Create a Tableau Connected Apps with Direct Trust**

Create a connected app from Tableau Cloud's Settings page.

1. As a site admin, sign in to Tableau Cloud.
2. From the left pane, select **Settings > Connected Apps**.

   :::image type="content" alt-text="Screenshot that shows the navigation path to the apps configuration in Tableau." source="media/tableau-cloud/tableau-navigation-to-settings-apps.png" lightbox="media/tableau-cloud/tableau-navigation-to-settings-apps.png":::

3. Select the **New Connected App** button drop-down arrow and select **Direct Trust**.
4. Use the information in the following table to fill out the **Create Connected App dialog box**.

   | Field | Description | Recommended Value |
   | --- | --- | --- |
   | Connected app name| Unique value that identifies the application that you require Direct Trust for. | Microsoft Search and Copilot |
   | Access Level | To control which views or metrics can be embedded, select "All projects" or "Only one project". All projects: This option enables the content in all projects to be embedded. Only one project: This option enables only the content in the specified project to be embedded. If the specified project contains nested projects, embedding content in those nested projects is not enabled. |"All project" or "Only one project" |
   | Domain allowlist|the domains where views or metrics can be embedded|All domains |

   When finished, select the **Create** button.

   :::image type="content" alt-text="Screenshot that shows the Tableau direct trust configuration." source="media/tableau-cloud/tableau-direct-trust-configuration.png" lightbox="media/tableau-cloud/tableau-direct-trust-configuration.png":::

5. Next to the connected app's name, select the actions menu and select **Enable**.

   :::image type="content" alt-text="Screenshot that shows how to enable the Tableau App." source="media/tableau-cloud/tableau-enable-app.png" lightbox="media/tableau-cloud/tableau-enable-app.png":::

**Step 2: Generate a secret**

1. On the detail page of the connected app you created in Step 1, select the **Generate New Secret** button.

   :::image type="content" alt-text="Screenshot that shows how to generate a secret for the Tableau App." source="media/tableau-cloud/tableau-generate-a-secret.png" lightbox="media/tableau-cloud/tableau-generate-a-secret.png":::

2. Make note of the **Secret ID**，**Secret Value** and **Client ID** to use in Step 3 below.

**Step 3: Enter the required fields of Tableau Copilot connector authentication**.

Enter the User, Connected App Client ID, Connected App Secret ID and Connected App Secret Key to connect to your Tableau Cloud Site. 

:::image type="content" alt-text="Screenshot that shows the authentication process for Tableau Copilot connector." source="media/tableau-cloud/tableau-gc-auth.png" lightbox="media/tableau-cloud/tableau-gc-auth.png":::

Refer to the following table to learn the descriptions of the required fields of Tableau Copilot connector authentication

| Field | Description |
| --- | --- |
| User| The admin user email. Recommend to fill the email of an admin user who configured the Tableau Connected Apps with Direct Trust. |
| Connected App Client ID| **Client ID** of the Tableau Connected Apps with Direct Trust, refer to the value noted in the Step 2 above. |
| Connected App Secret ID| **Secret ID** of the Tableau Connected Apps with Direct Trust, refer to the value noted in the Step 2 above. |
| Connected App Secret Key| **Secret Value** of the Tableau Connected Apps with Direct Trust, refer to the value noted in the Step 2 above. |

### 4. Staged rollout to a limited audience
Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before expanding the rollout to a broader audience.

At this point, you're ready to create the connection for Tableau Cloud. You can click the **Create** button to publish your connection and index sheets from your Tableau Cloud Site. 

For other settings, like Access Permissions, Data inclusion rules, Schema, Crawl frequency, etc., we set defaults based on what works best with Tableau Cloud data. The default values are as follows: 

| Page | Settings | Default values |
| --- | ---- | --- |
| Users | Access permissions | Only people with access to this data source. |
| Users | Map Identities |Data source identities mapped using Microsoft Entra IDs. |
| Content | Index content | All sheets, except the sheets in personal space. |
| Content | Manage properties | To check default properties and their schema, [click here](#content). |
| Sync | Incremental crawl | Frequency: Every 15 mins |
| Sync | Full crawl | Frequency: Every day |

If you want to edit any of these values, you need to choose **Custom setup**.

## Custom setup 

Custom setup is for those admins who want to edit the default values for settings. Once you select **Custom setup**, you should see three other tabs – **Users**, **Content**, and **Sync**. 

### Users 

**Access permissions**

The Tableau Cloud Copilot connector supports data visible to **Only people with access to this data source (recommended)** or Everyone. If you choose Everyone, indexed data appears in the search results for all users. 

>[!NOTE]
> Tableau's ACL system uses a layered evaluation mechanism to calculate users' effective permissions. When you select "**Only people with access to this data source**" while configuring the Tableau Cloud Copilot connector, the connector applies a logic similar to Tableau's native ACL system. This mechanism ensures that the content indexed by the Copilot connector is **not overshared** with users who don't have appropriate permissions within Tableau Cloud Sites. This image shows the specific rules are applied to determine which permissions govern the content and which users are authorized to access it.
> 
> :::image type="content" alt-text="Diagram that shows the workflow of Tableau Copilot connector ACL." source="media/tableau-cloud/tableau-connector-acl-workflow.png" lightbox="media/tableau-cloud/tableau-connector-acl-workflow.png":::
>
> - For admin users, they're always ALLOWED.
> - If the user is a "denied user", part of a "denied group" or in a "denied group set", the user is DENIED.
> - If the user is a project leader or a content owner, the user is ALLOWED.
> - If the user is an "allowed user", part of an "allowed group" or in an "allowed group set", the user is ALLOWED.
> - If none of the above conditions are satisfied, the user is DENIED.

If you choose Only people with access to this data source, you need to further choose whether your Tableau Cloud Site has Microsoft Entra ID provisioned users or non-AAD users. 
To identify which option is suitable for your organization: 

1. Choose **Microsoft Entra ID** if the email ID of Tableau Cloud users is same as the UserPrincipalName (UPN) of users in Microsoft Entra ID. 

2. Choose **non-AAD** if the email ID of Tableau Cloud users is **different** from the UserPrincipalName (UPN) of users in Microsoft Entra ID.

   >[!Important]
   >- If you choose Microsoft Entra ID as the type of identity source, the connector maps the email IDs of users obtained from Tableau Cloud directly to UPN property from Microsoft Entra ID.
   >- If you chose "non-AAD" for the identity type see Map your non-Azure AD Identities for instructions on mapping the identities. You can use this option to provide the mapping regular expression from email ID to UPN.
   >- Updates to users or groups governing access permissions are synced in full crawls only. Incremental crawls do not currently support the processing of updates to permissions.

### Content 

#### Content ingestion filters   

You can choose what data you want to index. All sheets within the selected top-level project of your Tableau Cloud Site are indexed. Use the preview results button to verify the sample values of the selected properties and filters. 

Use the preview results button to verify the sample values of the selected properties and filters. 

#### Manage properties

Here, you can check available properties from your Tableau Cloud. Assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. The default selected properties are listed as follows.

| Properties     | Semantic Label            | Schema                  | Description                                                                                   |
| -------------- | ------------------------- | ----------------------- | --------------------------------------------------------------------------------------------- |
| CreatedAt      | `Created date time`       | Query, Retrieve         | The timestamp indicating when the sheet was originally created.                   |
| IconUrl        | `IconUrl`                 | Retrieve                | URL of the icon associated with the different sheet types (e.g., worksheet, dashboard, story), used for display purposes.             |
| LastModifiedBy | `Last modified by`        | Query, Retrieve, Search | The user who last modified the sheet.
| Name           | `Title`                   | Query, Retrieve, Search | The title or display name of the sheet.                                           |
| ProjectName    | None                      | Query, Search           | The name of the parent project under which the sheet resides.                            |
| SheetType      | None                      | Query, Refine, Retrieve | The type of sheet, e.g., worksheet, dashboard, story. |
| SheetUrl       | `url`                     | Retrieve                | Direct URL link to open the sheet in Tableau.                                                 |
| Tags           | None                      | Query, Refine, Retrieve | Tags assigned to the sheet.                       |
| TopProjectName | None                      | Query, Search           | The name of the top-level project that contains the sheet.                 |
| UpdatedAt      | `Last modified date time` | Query, Retrieve         | The timestamp of the most recent modification to the sheet.                       |
| WorkbookName   | None                      | Query, Search           | The name of the workbook that contains the sheet.                                             |


### Sync 

You can configure full and incremental crawls based on the scheduling options present here. By default, incremental crawl is set for every 15 minutes, and full crawl is set for every day. If needed, you can adjust these schedules to fit your data refresh needs.

## Troubleshooting
After publishing your connection, you can review the status in the **Connectors** section of the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, contact [Microsoft Graph](https://developer.microsoft.com/graph/support).