---
title: "Deploy the Azure DevOps Wiki connector"
ms.author: danielabo
author: danipocket
manager: calvind
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: microsoft-365-copilot-connectors
ms.date: 08/20/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the Azure DevOps Wiki Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Azure DevOps Wiki connector

The Azure DevOps Wiki connector indexes project wikis and code wikis from your Azure DevOps Services organization into Microsoft 365. This guide describes the steps to deploy and customize the connector.

For Azure DevOps configuration information, see [Set up the Azure DevOps environment for connector ingestion](azure-devops-wiki-admin-setup.md).

## Prerequisites

Before you deploy the Azure DevOps Wiki connector, make sure that the Azure DevOps environment is configured in your organization, and that you meet the following prerequisites:

- You must be a Microsoft 365 admin.
- You identified the Azure DevOps organization to index.
- You enabled Third-party application access via OAuth in the Azure DevOps organization.
- You configured a crawl service account in Azure DevOps that has at least the required read permissions for all projects to be indexed.

## Deploy the connector

To add the Azure DevOps Wiki connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **Azure DevOps Wiki**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated content source. You can accept the default **Azure DevOps Wiki** display name or customize it as appropriate for your organization.

### Set instance URL

Enter your Azure DevOps organization name. The Azure DevOps organization name is the segment that comes after `https://dev.azure.com/`. For example:

- URL: `https://dev.azure.com/contoso`
- Organization: `contoso`

Enter only the organization name—don't enter the full URL.

### Choose authentication type

To sync wikis from Azure DevOps, choose one of the supported authentication methods and complete the required setup:

- **Federated Credential (recommended)** - Uses a service principal to crawl content.
- **Microsoft Entra ID OAuth** - Uses the signed‑in Microsoft 365 admin account.

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

Microsoft Entra ID OAuth uses the signed‑in Microsoft 365 admin account as the crawl service account. To allow the connector to access Azure DevOps and index wikis, grant the required permissions.

##### Confirm that your Azure DevOps organization is connected to Microsoft Entra

The connector can only index wikis from an Azure DevOps organization that's linked to your tenant's Microsoft Entra ID.

1. Go to [Azure DevOps](https://dev.azure.com/) and select the organization.
2. Select **Organization settings**.
3. In the left pane, under **General**, select **Microsoft Entra**.
4. Confirm that the organization is connected to your tenant's Microsoft Entra account.

##### Create an app in Microsoft Entra ID

1. Sign in to the [Azure portal](https://portal.azure.com) with admin credentials.
2. Go to **Microsoft Entra ID** > **Identity** > **Applications** > **App registrations**, then select **New registration**.
3. Enter a name for the app and select **Register**.
4. Note the **Application (client) ID**—you use it to grant project access in Azure DevOps.

##### Configure API permissions

1. In the app registration, select **API permissions**.
2. Choose **Add a permission** > **Azure DevOps** > **Delegated permissions**.
3. Add the following permissions:
   - Identity (read)
   - Code (read)
   - Entitlements (read)
   - Project and Team (read)
   - Graph (read)
   - MemberEntitlement Management (read)
   - Wiki (read)
4. Select **Grant admin consent for \<TenantName\>** and confirm.
5. Verify that all permissions show the status **Granted**.

##### Configure authentication settings

1. In the app registration, select **Authentication**.
2. Select **Add a platform** and choose **Web**.
3. Under **Redirect URIs**, add the URI for your cloud environment:
   - **Microsoft 365 Enterprise**: `https://gcs.office.com/v1.0/admin/oauth/callback`
   - **Microsoft 365 Government**: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
4. Under **Implicit grant and hybrid flows**, select **ID tokens**.
5. Select **Configure** to save the settings.

##### Create a client secret

1. In the app registration, select **Certificates and secrets**.
2. Under **Client secrets**, select **New client secret**.
3. Choose an expiration period and create the secret.
4. Copy the **Value** of the secret and store it securely. You can't view it again after you leave the page.

Use the client secret and the application (client) ID when you configure the connector in the Microsoft 365 admin center.

### Roll out

To roll out the connector to a limited audience, select the toggle next to **Rollout to limited audience** and specify the users or groups to roll the connector out to. This approach helps you validate the connector before a full deployment. For more information, see [Staged rollout for Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The Azure DevOps Wiki connector begins indexing content immediately.

The following table lists the default values that are set.

| Category | Default value |
|----------|----------------|
| Users | Only people with access to the content in the data source. Data source identities mapped using Microsoft Entra IDs. |
| Content | All projects are indexed. |
| Sync | Full crawl every day. Incremental crawl every 15 minutes. |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the Microsoft 365 admin center.

## Customize settings (optional)

You can customize the default settings for the Azure DevOps Wiki connector by choosing **Custom setup** in the connector page.

### Customize user settings

#### Access permissions

The Azure DevOps Wiki connector supports the following search permissions:

- **Visible to everyone**
- **Only people with access to this data source**

If you choose **Visible to everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to it.

> [!NOTE]
> Updates to groups governing access permissions sync in full crawls only. Incremental crawls don't support the processing of updates to permissions.

#### Map identities

Identity mapping ensures that Azure DevOps identities map correctly to Microsoft Entra ID users. The connector uses delegated access and automatically aligns identities through the signed-in Microsoft 365 admin account.

### Customize content settings

#### Choose projects

Choose whether the connection indexes the entire organization or specific projects within the selected organization.

If you choose to index the entire organization, the connection indexes wikis in all projects in the organization. The connection indexes new projects and wikis during the next crawl after you create them.

If you choose to index individual projects, the connection indexes only wikis in the selected projects.

#### Manage properties

Add or remove properties from your Azure DevOps data source. Assign a schema to the property by defining whether a property is searchable, queryable, retrievable, or refinable. Change the semantic label, and add an alias to the property. The following table lists the properties that are indexed by default.

| Property | Semantic label | Description | Schema attributes |
|----------|----------------|-------------|-------------------|
| Authors | Authors | People who participated or collaborated on the item | Retrieve |
| Content | Content | The content body of the wiki | Search |
| IconUrl | IconUrl | Icon URL that represents the wiki | Retrieve |
| LastPublishedAuthorEmail | Last modified by | | Retrieve |
| LastPublishedDate | Last modified date time | Date and time the item was last modified | Retrieve |
| Organization | | | Retrieve |
| Project | | | Retrieve |
| ProjectId | | | Retrieve |
| RemoteURL | url | The URL of the wiki in the data source | Retrieve |
| Title | Title | The title of the wiki page | Search, Retrieve |
| Version | | | Retrieve |
| WikiId | | | Retrieve |
| WikiIdentifier | | | Retrieve |

Additional properties are available but not selected by default: CommitId, GitItemPath, isParentPage, Path, WikiType.

### Customize sync intervals

You can adjust how frequently the connector crawls your Azure DevOps organization. The following sync intervals are available:

- **Full crawl:** Recrawls the entire Azure DevOps dataset.
- **Incremental crawl:** Recrawls only updated items.

The default sync settings are optimized for most organizations.

For more information, see [Guidelines for crawl settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

### Set up search result page

After publishing the connection, customize the search results page with verticals and result types. To learn about customizing search results, see how to [manage verticals](/microsoftsearch/manage-verticals) and [result types](/microsoftsearch/manage-result-types).

You can also use the [sample result layout](azure-devops-wiki-connector-result-layout.md) for the Azure DevOps Wiki connector. Copy and paste the result layout JSON to get started.

## Related content

- [Azure DevOps Wiki connector overview](azure-devops-wiki-overview.md)
- [Troubleshoot issues with the Azure DevOps Wiki connector](azure-devops-wiki-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)
