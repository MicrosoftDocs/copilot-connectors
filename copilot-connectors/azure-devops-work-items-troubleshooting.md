---
title: "Azure DevOps Work Items connector troubleshooting"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: vivg
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 12/18/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Azure DevOps Work Items Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Azure DevOps Work Items connector

The Azure DevOps Work Items connector indexes work items—such as user stories, tasks, bugs, and features—from Azure DevOps Services into Microsoft 365 so users can search and retrieve work tracking data directly in Copilot and Microsoft Search. This article provides troubleshooting information for common issues you might encounter when you deploy or manage the connector.

## Azure DevOps Work Items connector troubleshooting

The following table lists common errors and recommended troubleshooting steps.

| Issue | Description | Troubleshooting steps |
|-------|-------------|------------------------|
| Crawl account lacks required permissions | The connector relies on the signed-in Microsoft 365 admin account (crawl account) to query Azure DevOps using delegated OAuth. If this account lacks permissions, indexing fails. | - Confirm the crawl account has **Basic** access in Azure DevOps.<br>- Confirm the account is added to all projects that must be indexed.<br>- Add the account to **Project Administrators** (recommended) or **Project Readers** (minimum).<br>- Verify that the account has *View project-level information* and *View analytics* permissions for each project. |
| Work items not appearing in Copilot or Search | Only work items accessible to the crawl account can be indexed. Missing permissions or restricted area paths prevents ingestion. | - Validate that the crawl account has *View work items in this node* permission for the relevant Area Paths.<br>- Confirm the account can open the work items directly in Azure DevOps.<br>- Recheck project and team membership. |
| OAuth authentication fails | OAuth-based delegated access requires the Microsoft Entra app to be configured correctly. | - Confirm that all required delegated permissions are granted:<br>  `vso.analytics`, `vso.graph`, `vso.identity`, `vso.project`, `vso.variablegroups_read`, `vso.work`.<br>- Verify the redirect URI matches your cloud environment:<br>  - M365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`<br>  - M365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`<br>- Make sure ID tokens are enabled under implicit/hybrid flows.<br>- Confirm the client secret is valid and isn't expired. |
| Connector can't read items from certain projects | The connector crawls only the content the crawl account can access. If a project is missing, permissions are usually the cause. | - Make sure that the crawl account is added to each project.<br>- If using minimal privileges, confirm that the account has at least **Project Readers** membership.<br>- Review project-level permissions for mismatches or inherited restrictions. |
| Incremental crawl is slow or incomplete | Incremental crawl performance depends on Azure DevOps webhook configuration. | - Add the crawl account to **Project Administrators** to allow webhook creation.<br>- Confirm that webhook creation is allowed in your Azure DevOps organization.<br>- Validate that webhooks are firing by checking project-level service hooks. |
| Access denied errors during ingestion | Azure DevOps restricts access by permission type and area path. | - Confirm the crawl account can open the affected item in Azure DevOps.<br>- Recheck Area Path permissions.<br>- Validate that the correct identity is being mapped through Microsoft Entra ID. |
| Connector fails immediately after configuration | Misconfiguration of the Entra app or incorrect organization name can cause early failures. | - Make sure that only the **organization name** (not the full URL) is entered.<br>- Validate the Application (client) ID and client secret.<br>- Confirm the correct cloud redirect URI is set. |

## Related content

- [Azure DevOps Work Items connector overview](azure-devops-work-items-overview.md)  
- [Deploy the Azure DevOps Work Items connector](azure-devops-work-items-deployment.md)
