--- 
title: "Azure DevOps Wiki Microsoft 365 Copilot connector" 
ms.author: vivg 
author: vivg 
manager: harshkum 
audience: Admin
ms.audience: Admin 
ms.topic: how-to
ms.service: mssearch 
ms.localizationpriority: Medium 
search.appverid: 
- BFB160 
- MET150 
- MOE150 
description: "Set up the Azure DevOps Wiki Microsoft 365 Copilot connector"
ms.date: 03/09/2026
---

# Azure DevOps Wiki Microsoft 365 Copilot connector

The Azure DevOps Wiki Microsoft 365 Copilot connector allows your organization to index wikis in its instance of the Azure DevOps service. After you configure the connector, end users can search for project wikis and code wikis from Azure DevOps in Microsoft Search and Microsoft 365 Copilot.

This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors an Azure DevOps Wiki Copilot connector.

>[!IMPORTANT]
>The Azure DevOps Wiki Copilot connector supports only the Azure DevOps cloud service. It doesn't support Azure DevOps Server 2019, TFS 2018, TFS 2017, TFS 2015, and TFS 2013.

## Capabilities
- Index wikis from Azure DevOps
- Enable your end users to ask questions related to project wikis and code wikis.
- Use [Semantic search in Copilot](semantic-index-for-copilot.md) to enable users to find relevant content based on keywords, personal preferences, and social connections.

## Limitations
- The connector only indexes one ADO organization per connection. 

## Custom data filters

The Azure DevOps Wiki connector includes the following custom data filters for Copilot Search:

- Area Path
- Assigned to

## Prerequisites
- You must be the Search admin for your organization's Microsoft 365 tenant.
- To allow the connector to connect to your Azure DevOps organization, you must enable **Third-party application access via OAuth**. For more information, see [manage security policies](/azure/devops/organizations/accounts/change-application-access-policies?view=azure-devops#manage-a-policy&preserve-view=true) to learn more.

    ![Third-party application access via OAuth](media/ado-workitems-connector-security-policies.png)

- **Service Account**: To connect to Azure DevOps and allow the Azure DevOps Wiki Copilot connector to update wikis regularly, you need a service account with the following permissions granted to it. The service account is either the Microsoft-published service principal (for Federated Credential authentication) or the signed-in Microsoft 365 admin account (for Microsoft Entra ID OAuth authentication), depending on the authentication method selected.

    | Permission name | Permission type | Required for |
    | ------------ | ------------ | ------------ |
    | View project-level information | [Project permission](/azure/devops/organizations/security/permissions?view=azure-devops&tabs=preview-page#project-level-permissions&preserve-view=true) | Crawling Azure DevOps Wiki. This permission is **mandatory** for the projects that need to be indexed. |

>[!IMPORTANT]
>The crawl account must have **Basic** access level. To learn more about access levels in Azure DevOps, read [supported access levels](/azure/devops/organizations/security/access-levels).

## Get Started

[![Screenshot that shows connection creation screen for the Azure DevOps Wiki Copilot connector.](media/ado-wiki-create-page.png)](media/ado-wiki-create-page.png#lightbox)

### Choose display name 
A display name is used to identify each citation in Copilot, helping users easily recognize the associated file or item. Display name also signifies trusted content. Display name is also used as a [content source filter](/MicrosoftSearch/custom-filters#content-source-filters). A default value is present for this field, but you can customize it to a name that users in your organization recognize.

### Provide authentication type
To authenticate and sync wikis from Azure DevOps, choose **one of the two** supported methods:<br>

> - **Federated Credential (recommended)** – Uses a Microsoft-published Microsoft Entra service principal as the crawl service account. The permissions granted to this service principal in Azure DevOps determine what the connector can index.
> - **Microsoft Entra ID OAuth** – Uses delegated OAuth where the signed-in Microsoft 365 admin account acts as the crawl service account. In this case, the Azure DevOps permissions assigned to that admin account determine what the connector can index.

#### Federated Credential (recommended)

Federated Credential uses a Microsoft‑published enterprise application as the crawl service account. You must grant this service principal the necessary permissions in Azure DevOps.

##### Confirm that the service principal app is provisioned

1. Go to the [Microsoft Entra admin center](https://entra.microsoft.com/).
2. Search for **Graph Connector Federated Credential App** or use the app ID: `933838e2-bec1-440f-a634-9363c82e5b6d`.
3. If the app isn't provisioned, open the Copilot connectors page in the Microsoft 365 admin center. Provisioning can take several hours.

##### Grant the Microsoft Entra app access to Azure DevOps projects

Grant the service principal access to the Azure DevOps projects you want to index.

1. Go to [Azure DevOps](https://dev.azure.com/) and select the organization.
2. Select **Organization settings**.
3. In the left pane, under **General**, select **Users**.
4. Select **Add users**.
5. In **Users or Service Principals**, enter the app ID: `933838e2-bec1-440f-a634-9363c82e5b6d`.
6. Assign the **Basic** access level, select the projects to index, and add the app to the **Project Readers** group (or an equivalent group). Clear the option to send an email invitation.

##### Configure Federated Credential authentication

Select **Federated Credential** as the authentication type and authenticate when prompted.

#### Microsoft Entra ID OAuth

##### Make sure your ADO organization is connected to Microsoft Entra

The Azure DevOps Wiki Copilot connector only indexes content from an ADO organization connected with Microsoft Entra of your tenant. To ensure that your ADO organization is connected with Microsoft Entra account, use the following steps. 

1. Navigate to [Azure DevOps](https://dev.azure.com/) and select the required organization.
2. Select `Organization settings`.
3. On the left navigation pane, select `Microsoft Entra` under the 'General' header.
4. Ensure that the organization is connected to your tenant's Microsoft Entra account.

##### Create a Microsoft Entra ID app registration

1. Go to the [Azure portal](https://portal.azure.com) and sign in with admin credentials for the tenant.
2. Navigate to **Microsoft Entra ID** -> **Manage** -> **App registrations** from the navigation pane and select **New registration**.
3. Provide a name for the app and select **Register**.
4. Make a note of the Application (client) ID. This ID is used to grant the Microsoft Entra app access to projects in the ADO organization.
5. Open **API permissions** from the navigation pane and select **Add a permission**.
6. Select **Azure DevOps** and then **Delegated permissions**.
7. Search for the following permissions and select **Add permissions**. <br>
    a. Identity (read) <br>
    b. Code (read) <br>
    c. Entitlements (read) <br>
    d. Project and Team (read) <br>
    e. Graph (read) <br>
    f. MemberEntitlement Management (read) <br>
    g. Wiki (read)
8. Select **Grant admin consent for [TenantName]** and confirm by selecting **Yes**.
9. Check that the permissions are in the "**Granted**" state.
10. Open **Authentication** from the navigation pane. Select `Add a platform` and choose `Web`. Add one of the following URIs under "Redirect URIs":
    - For **M365 Enterprise**: `https://gcs.office.com/v1.0/admin/oauth/callback`
    - For **M365 Government**: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
11. Under **Implicit grant and hybrid flows**, check the option for `ID tokens (used for implicit and hybrid flows)` and click **Configure**.
12. From the navigation pane, select **Certificates and secrets** under **Manage**.
13. Select **New Client secret** and select an expiry period for the secret. Copy the generated secret (Value) and save it because it isn't shown again.
14. Use this Client secret and the application ID to configure the connector.

##### Grant the Microsoft Entra app access to projects in the ADO organization

You need to provide the Microsoft Entra app with the necessary access to the projects that need to be indexed using the following steps:

1. Navigate to [Azure DevOps](https://dev.azure.com/) and select the required organization.
2. Select `Organization settings`.
3. On the left navigation pane, select `Users` under the 'General' header.
4. Select `Add users`.
5. Copy the Application (client) ID obtained from the app to "Users or Service Principals".
6. Grant the `Basic` access level and select the projects to allow access to the index. Also, add to the `Project Reader` Azure DevOps group (or equivalent) to ensure access. Deselect the option to send email invitation to users.

### Select organization

Provide your Azure DevOps organization name. The Azure DevOps organization name is the segment after `https://dev.azure.com/`. For example:

- URL: `https://dev.azure.com/contoso`  
- Organization: `contoso`

Only the organization name is required—don't provide the full URL.

### Roll out to limited audience
Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before expanding the rollout to a broader audience. To know more about limited rollout, see [staged rollout](staged-rollout-for-graph-connectors.md).

At this point, you're ready to create the connection for Azure DevOps wikis. You can click **Create** to publish your connection and index wikis from your Azure DevOps organization.

For other settings, like **Access Permissions**, **Data Inclusion Rules**, **Schema**, **Crawl frequency**, etc., we have defaults based on what works best with ADO data. You can see the default values below:

| Users | Description |
|----|---|
| Access permissions | _Only people with access to content in Data source._ |
| Map Identities | _Data source identities mapped using Microsoft Entra IDs._ |

| Content | Description |
|---|---|
| Site projects | _All projects are indexed._ |
| Manage Properties | _To check default properties and their schema, see [content](#content)_ |

| Sync | Description |
|---|---|
| Incremental Crawl | _Frequency: Every 15 mins_ |
| Full Crawl | _Frequency: Every Day_ |

If you want to edit any of these values, you need to choose the "Custom Setup" 

## Custom Setup

Custom setup is for those admins who want to edit the default values for settings listed in the above table. Once you click on the "Custom Setup" option, you see three more tabs - Users, Content, and Sync.

### Users

[![Screenshot that shows Users tab where you can configure access permissions and user mapping rules.](media/ado-wiki-users-tab.png)](media/ado-wiki-users-tab.png#lightbox)

#### Access permissions

The Azure DevOps Wiki Copilot connector supports search permissions visible to **Everyone** or **Only people with access to this data source**. If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to it.

>[!NOTE]
>
> Updates to groups governing access permissions are synced in full crawls only. Incremental crawls don't support processing of updates to permissions.

### Content

[![Screenshot that shows Content tab where you can configure projects and connection schema.](media/ado-wiki-content-tab.png)](media/ado-wiki-content-tab.png#lightbox)

#### Choose projects

In this step, you specify the scope of data that you want to index using the Azure DevOps Wiki Copilot connector. You can then choose for the connection to index either the entire organization or specific projects within the selected organization.

If you choose to index the entire organization, wikis in all projects in the organization are indexed. New projects and wikis are indexed during the next crawl after they're created.

If you choose to index individual projects, only wikis in the selected projects are indexed.

#### Manage properties

Here, you can add or remove available properties from your Azure DevOps data source, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label and add an alias to the property. Properties that are selected by default are listed below.

|Source property|Label|Description|Schema|
|---|---|---|---|
| Authors | Authors | Name all the people who participated/collaborated on the item in the data source | Retrieve. |
| CommitId | | | |
| Content | Content | The content body of the wiki | Search. |
| GitItemPath | | | |
| IconUrl | IconUrl | Icon url that represents the wiki | Retrieve. |
| isParentPage | | | |
| LastPublishedAuthorEmail | Last modified by | | Retrieve. |
| LastPublishedDate | Last modified date time | Date and time the item was last modified in the data source | Retrieve. |
| Organization | | | Retrieve. |
| Path | | | |
| Project | | | Retrieve. |
| ProjectId | | | Retrieve. |
| RemoteURL | url | The URL of the wiki in the data source | Retrieve. |
| Title | Title | The title of the wiki page | Search, Retrieve. |
| Version | | | Retrieve. |
| WikiId | | | Retrieve. |
| WikiIdentifier | | | Retrieve. |
| WikiType | | | |

#### Preview data

Use the preview results button to verify the sample values of the selected properties.

### Sync

[![Screenshot that shows Sync tab where you can configure crawl frequency.](media/ado-wiki-sync-tab.png)](media/ado-wiki-sync-tab.png#lightbox)

The refresh interval determines how often your data is synced between the data source and the Azure DevOps Wiki Copilot connector index. There are two types of refresh intervals - full crawl and incremental crawl. For more information, see [refresh settings](configure-connector.md#guidelines-for-sync-settings).

You can change the default values of the refresh interval from here if you want to.

### Set up search result page

After publishing the connection, you need to customize the search results page with verticals and result types. To learn about customizing search results, review how to [manage verticals](manage-verticals.md) and [result types](manage-result-types.md).

You can also use the [sample result layout](azure-devops-wiki-connector-result-layout.md) for the Azure DevOps Wiki Copilot connector. Copy and paste the result layout JSON to get started.

## Troubleshooting
  
After publishing your connection, you can review the status in the **Connectors** section of the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

To troubleshoot issues, see [Troubleshooting](troubleshoot-azure-devops-wiki-connector.md).