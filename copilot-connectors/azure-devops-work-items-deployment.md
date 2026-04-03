---
title: "Deploy the Azure DevOps Work Items connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: vivg
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 03/09/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the Azure DevOps Work Items Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Azure DevOps Work Items connector

The Azure DevOps Work Items connector indexes work items - such as user stories, tasks, bugs, and features - from your Azure DevOps Services organization into Microsoft 365. This guide describes the steps to deploy and customize the connector.

For Azure DevOps configuration information, see [Set up the Azure DevOps environment for connector ingestion](azure-devops-work-items-admin-setup.md).

## Prerequisites

Before you deploy the Azure DevOps Work Items connector, make sure that the Azure DevOps environment is configured in your organization, and that you meet the following prerequisites:

- You must be a Microsoft 365 admin.
- You identified the Azure DevOps organization to index.
- You configured a crawl service account in Azure DevOps that has at least the required read permissions for all projects and area paths to be indexed.

## Deploy the connector

To add the Azure DevOps Work Items connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **Azure DevOps Work Items**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated content source. You can accept the default **Azure DevOps Work Items** display name or customize it as appropriate for your organization.

### Set instance URL

Provide your Azure DevOps organization name. The Azure DevOps organization name is the segment after `https://dev.azure.com/`. For example:

- URL: `https://dev.azure.com/contoso`  
- Organization: `contoso`

Only the organization name is required—don't provide the full URL.

### Choose authentication type

To sync work items from Azure DevOps, choose one of the supported authentication methods and complete the required setup:

- **Federated Credential (recommended)** - Uses a service principal to crawl content.
- **Microsoft Entra ID OAuth** - Uses the signed‑in Microsoft 365 admin account.

#### Federated Credential (recommended)

Federated Credential uses a Microsoft‑published enterprise application as the crawl service account. You must grant this service principal the necessary permissions in Azure DevOps.

##### Confirm that the service principal app is provisioned

1. Go to the [Microsoft Entra admin center](https://entra.microsoft.com/).
2. Search for **Graph Connector Federated Credential App** or use the app ID: `933838e2-bec1-440f-a634-9363c82e5b6d`.
3. If the app isn’t provisioned, open the Copilot connectors page in the Microsoft 365 admin center. Provisioning can take several hours.

##### Grant the Microsoft Entra app access to Azure DevOps projects

Grant the service principal access to the Azure DevOps projects you want to index.

1. Go to [Azure DevOps](https://dev.azure.com/) and select the organization.
2. Select **Organization settings**.
3. In the left pane, under **General**, select **Users**.
4. Select **Add users**.
5. In **Users or Service Principals**, enter the app ID: `933838e2-bec1-440f-a634-9363c82e5b6d`.
6. Assign the **Basic** access level, select the projects to index, and add the app to the **Project Administrators** group (or an equivalent group). Clear the option to send an email invitation.

##### Configure Federated Credential authentication

Select **Federated Credential** as the authentication type and authenticate when prompted.

#### Microsoft Entra ID OAuth

Microsoft Entra ID OAuth uses the signed‑in Microsoft 365 admin account as the crawl service account. To allow the connector to access Azure DevOps and update work items, grant the required permissions.

##### Confirm that your Azure DevOps organization is connected to Microsoft Entra

The connector can only index work items from an Azure DevOps organization that’s linked to your tenant’s Microsoft Entra ID.

1. Go to [Azure DevOps](https://dev.azure.com/) and select the organization.
2. Select **Organization settings**.
3. In the left pane, under **General**, select **Microsoft Entra**.
4. Confirm that the organization is connected to your tenant’s Microsoft Entra account.

> [!NOTE]
> The admin who creates the connection must have **Read** access to the relevant project.

##### Create an app in Microsoft Entra ID

1. Sign in to the [Azure portal](https://portal.azure.com) with admin credentials.
2. Go to **Microsoft Entra ID** > **Identity** > **Applications** > **App registrations**, then select **New registration**.
3. Enter a name for the app and select **Register**.
4. Note the **Application (client) ID**—you use it to grant project access in Azure DevOps.

##### Configure API permissions

1. In the app registration, select **API permissions**.
2. Choose **Add a permission** > **Azure DevOps** > **Delegated permissions**.
3. Add the following permissions (all under **vso**):
   - **vso.analytics** – Analytics (read)  
   - **vso.graph** – Graph (read)  
   - **vso.identity** – Identity (read)  
   - **vso.project** – Project and team (read)  
   - **vso.variablegroups_read** – Variable Groups (read)  
   - **vso.work** – Work items (read)
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

##### Authenticate the Microsoft Entra app with a crawl account

When you're signed in as an admin, the Microsoft Entra app is automatically authenticated via single sign-on. Microsoft Entra ID issues an access token to the app, which includes the user's identity and the delegated permissions you granted. The app can access only the data and actions that the signed-in admin user is authorized to access.

### Roll out

To roll out the connector to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users or groups to roll the connector out to. This allows you to validate the connector before a full deployment. For more information, see [Staged rollout for Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The Azure DevOps Work Items connector begins indexing content immediately.

The following table lists the default values that are set.

| Category | Default value |
|----------|----------------|
| Users | Only people with access to the content in the data source. Data source identities mapped using Microsoft Entra IDs.|
| Content | All projects are indexed. |
| Sync | Full crawl every day. Incremental crawl every 15 minutes.|

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the Microsoft 365 admin center.

## Customize settings (optional)

You can customize the default settings for the Azure DevOps Work Items connector by choosing **Custom setup** in the connector page.

### Customize user settings

#### Access permissions

The Azure DevOps Work Items connector supports the following search permissions:

- **Visible to everyone** 
- **Only people with access to this data source**

If you choose **Visible to everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to it.

> [!NOTE]
> Updates to groups governing access permissions are synced in full crawls only. Incremental crawls don't support the  processing of updates to permissions.

#### Map identities

Identity mapping ensures that Azure DevOps identities map correctly to Microsoft Entra ID users. The connector uses delegated access and automatically aligns identities through the signed-in Microsoft 365 admin account.

### Customize content settings

#### Manage properties

You can add or remove properties from your Azure DevOps data source, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. The following table lists the properties that are indexed by default.

| Property | Semantic label | Description | Schema attributes |
|----------|----------------|-------------|------------------|
| AreaPath | | The area path to the work item | Query, Retrieve, Search |
| AssignedTo | | Name of person the work item is assigned to | Query, Retrieve, Search |
| Authors | Authors | | Retrieve |
| ChangedBy | Last modified by | Person name who last modified the work item | Query, Retrieve |
| ChangedDate | Last modified date time | | Query, Retrieve |
| CreatedBy | Created by | Person name who created the work item | Query, Retrieve, Search |
| CreatedDate | Created date time | Timestamp when work item was created | Query, Retrieve |
| Description | Content | Description of work item | Search |
| IconUrl | IconUrl | | Retrieve |
| Id | | Work item ID | Query, Retrieve, Search |
| Priority | | Priority of work item | Query, Retrieve |
| ReproSteps | | Steps to reproduce a condition described in work item | | 
| State | | Current state of the work item | Query, Retrieve, Search |
| Tags | | | Query, Retrieve, Search |
| TeamProject | | | Retrieve |
| Title | Title | Title of the work item | Retrieve, Search |
| URL | url | URL of the work item | Retrieve |
| WorkItemType | | | Query, Retrieve, Search |

### Customize sync intervals

You can adjust how frequently the connector crawls your Azure DevOps organization. The following sync intervals are available:

- **Full crawl:** Recrawls the entire Azure DevOps dataset.
- **Incremental crawl:** Recrawls only updated items.

The default sync settings are optimized for most organizations.

For more information, see [Guidelines for sync settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-sync-settings).

## Related content

- [Azure DevOps Work Items connector overview](azure-devops-work-items-overview.md)
- [Troubleshoot issues with the Azure DevOps Work Items connector](azure-devops-work-items-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)

