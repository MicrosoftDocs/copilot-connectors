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
ms.date: 03/09/2026
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

## Identify the Azure DevOps organization URL

Identify the Azure DevOps organization URL. For example:

- Azure DevOps URL: `https://dev.azure.com/contoso`
- Organization name: `contoso`

Only the organization name is required for the connector configuration.

## Enable API access

Make sure that Azure DevOps REST APIs are enabled for the organization so the connector can query work items, identities, analytics, and project metadata.

## Identify the crawl account

The connector supports two authentication methods:

- **Federated Credential (recommended)** – Uses a Microsoft-published Microsoft Entra service principal as the crawl service account. The permissions granted to this service principal in Azure DevOps determine what the connector can index.
- **Microsoft Entra ID OAuth** – Uses delegated OAuth where the signed-in Microsoft 365 admin account acts as the crawl service account. In this case, the Azure DevOps permissions assigned to that admin account determine what the connector can index.

If you use Microsoft Entra ID OAuth, make sure the Microsoft 365 admin account that configures the connector:

- Has access to **Copilot** > **Connectors** in the Microsoft 365 admin center.
- Can be added to the Azure DevOps organization and projects that you want to index.

## Grant Azure DevOps access to the crawl account

Grant the crawl account the necessary permissions in Azure DevOps:

- Assign **Basic** access level.
- Add the service principal (or user) to each project to be indexed.
- Add the service principal (or user) to the **Project Administrators** group (recommended) to allow webhook configuration for faster incremental crawl. 
- If that isn't feasible, add the user to the **Project Readers** group (minimum requirement).

The following table lists the permissions that must be granted to the crawl service account.

| Permission name | Permission type | Required to |
|------------------|------------------|---------------|
| View project-level information | Project permission | Crawl Azure DevOps work items (required) |
| View analytics | Project permission | Crawl Azure DevOps work items (required) |
| View work items in this node | Area path permission | Crawl work items for permitted area paths (optional) |

## Validate the permissions

Validate that the crawl account appears in the appropriate Azure DevOps security groups (Project Administrators or Project Readers). Confirm that the account can view the projects and area paths expected for indexing.

## Next step

> [!div class="nextstepaction"]  
> [Deploy the Azure DevOps Work Items connector](azure-devops-work-items-deployment.md)
