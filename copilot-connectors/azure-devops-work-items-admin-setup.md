---
title: "Set up the Azure DevOps service for Azure DevOps Work Items connector ingestion"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: vivg
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 12/19/2025
ms.localizationpriority: Medium
description: "Get the steps that the Azure DevOps admin needs to complete for your organization to configure the Azure DevOps Work Items Microsoft 365 Copilot connector."
---

# Set up the Azure DevOps service for Azure DevOps Work Items connector ingestion

The Azure DevOps Work Items Microsoft 365 Copilot connector indexes work items from your Azure DevOps Services instance—such as user stories, tasks, bugs, and features—into Microsoft 365. This article provides information about the configuration steps that Azure DevOps admins and Microsoft 365 admins must complete to deploy the Azure DevOps Work Items connector. For information about how to deploy the connector, see [Deploy the Azure DevOps Work Items connector](azure-devops-work-items-deployment.md).

## Setup checklist

The following checklist lists the steps involved in configuring the environment and setting up the connector prerequisites.

| Task | Role |
|------|------|
| [Identify Azure DevOps organization](#identify-the-azure-devops-organization-url) | Azure DevOps admin |
| [Enable API access](#enable-api-access) | Azure DevOps admin |
| [Identify the crawl account](#identify-the-crawl-account) | Azure DevOps admin |
| [Grant Azure DevOps access to the crawl account](#grant-azure-devops-access-to-the-crawl-account) | Azure DevOps admin |
| [Validate the permissions](#validate-the-permissions) | Azure DevOps admin |
| [Configure the Microsoft Entra application](#configure-the-microsoft-entra-application-for-oauth) | Azure DevOps admin |

## Identify the Azure DevOps organization URL

Identify the Azure DevOps organization URL. For example:

- Azure DevOps URL: `https://dev.azure.com/contoso`
- Organization name: `contoso`

Only the organization name is required for the connector configuration.

## Enable API access

Make sure that Azure DevOps REST APIs are enabled for the organization so the connector can query work items, identities, analytics, and project metadata.

## Identify the crawl account

The connector uses delegated Microsoft Entra ID OAuth. The crawl account represents the signed‑in Microsoft 365 admin who configures the connector. The Azure DevOps permissions for this account determine what the connector can index.

Make sure to use a Microsoft 365 admin account that:

- Has access to **Copilot** > **Connectors** in the Microsoft 365 admin center.
- Can be added to your Azure DevOps organization and projects.

## Grant Azure DevOps access to the crawl account

Grant the crawl account the necessary permissions in Azure DevOps:

- Assign **Basic** access level.
- Add the user to each project to be indexed.
- Add the user to the **Project Administrators** group (recommended) to allow webhook configuration for faster incremental crawl. 
- If that isn't feasible, add the user to the **Project Readers** group (minimum requirement).

The following table lists the permissions that must be granted.

| Permission name | Permission type | Required to |
|------------------|------------------|---------------|
| View project-level information | Project permission | Crawl Azure DevOps work items (required) |
| View analytics | Project permission | Crawl Azure DevOps work items (required) |
| View work items in this node | Area path permission | Crawl work items for permitted area paths (optional) |

## Validate the permissions

Validate that the crawl account appears in the appropriate Azure DevOps security groups (Project Administrators or Project Readers). Confirm that the account can view the projects and area paths expected for indexing.

## Configure the Microsoft Entra application for OAuth

Before you configure OAuth, verify that your ADO organization is linked to your Microsoft Entra tenant.

1. Go to [Azure DevOps](https://dev.azure.com/) and select your organization.
2. Select **Organization settings**.
3. In the left pane, under **General**, select **Microsoft Entra**.
4. Confirm that the organization is connected to your tenant's Microsoft Entra account.

> [!NOTE]
> The Search admin who creates the connection to Microsoft Entra must have **Read** access to the relevant ADO project.

### Create an app registration in Microsoft Entra ID

1. Sign in to the [Azure portal](https://portal.azure.com/) using an admin account for your tenant.
2. Go to **Microsoft Entra ID** > **Identity** > **Applications** > **App registrations**.
3. Select **New registration**.
4. Enter a name for the app and select **Register**.
5. Copy the **Application (client) ID**. You'll use this ID to grant the app access to ADO projects.

### Configure API permissions

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

### Configure authentication settings

1. In the app registration, select **Authentication**.
2. Select **Add a platform** and choose **Web**.
3. Under **Redirect URIs**, add the URI for your cloud environment:
   - **M365 Enterprise**: `https://gcs.office.com/v1.0/admin/oauth/callback`
   - **M365 Government**: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
4. Under **Implicit grant and hybrid flows**, select **ID tokens**.
5. Select **Configure** to save the settings.

### Create a client secret

1. In the app registration, select **Certificates and secrets**.
2. Under **Client secrets**, select **New client secret**.
3. Choose an expiration period and create the secret.
4. Copy the **Value** of the secret and store it securely. You can't view it again after you leave the page.

Use the client secret and the application (client) ID when configuring the connector in the Microsoft 365 admin center.

### Authenticate the Microsoft Entra app with a crawl account

When you're signed in as an admin, the Microsoft Entra app is automatically authenticated through single sign-on. Microsoft Entra ID issues an access token to the app, which includes the user's identity and the delegated permissions you've granted. The app can access only the data and actions that the signed-in admin user is authorized to access.

## Next step

> [!div class="nextstepaction"]  
> [Deploy the Azure DevOps Work Items connector](azure-devops-work-items-deployment.md)
