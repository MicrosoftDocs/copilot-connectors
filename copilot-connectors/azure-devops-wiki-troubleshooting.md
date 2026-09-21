---
title: "Azure DevOps Wiki connector troubleshooting"
ms.author: danielabo
author: danipocket
manager: calvind
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: microsoft-365-copilot-connectors
ms.date: 08/20/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Azure DevOps Wiki Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Azure DevOps Wiki connector

The Azure DevOps Wiki connector indexes project wikis and code wikis from Azure DevOps Services into Microsoft 365 so users can search and retrieve wiki content directly in Copilot and Microsoft Search. This article provides troubleshooting information for common issues you might encounter when you deploy or manage the connector.

To verify Azure DevOps configuration information to help troubleshoot errors, see [Set up the Azure DevOps service for connector ingestion](azure-devops-wiki-admin-setup.md).

## Azure DevOps Wiki connector troubleshooting

The following table lists common errors and recommended troubleshooting steps.

| Issue | Description | Troubleshooting steps |
|-------|-------------|------------------------|
| Invalid credentials at connection settings | `Invalid credentials detected. Try signing in with a different account or check the permissions for your account` | Third-party application access via OAuth might be disabled. Follow the steps to [manage security policies](/azure/devops/organizations/accounts/change-application-access-policies?view=azure-devops#manage-a-policy&preserve-view=true) to enable OAuth. |
| Bad state in OAuth pop-up | `Bad state` message in OAuth pop-up window with URL stating `error=InvalidScope` | Wrong scopes provided to the registered app. Verify that all required API permissions are granted. |
| 400 Bad request in OAuth pop-up | `400 - Bad request` message in OAuth pop-up window | Incorrect App ID. Verify the Application (client) ID. |
| Bad request on API request | `BadRequest: Bad request on API request` message in OAuth pop-up window | Incorrect client secret. Regenerate and update the client secret. |
| Permission denied during crawl | `The account associated with the connector doesn't have permission to access the item.` | The registered app doesn't have any of the required OAuth scopes. Verify API permissions. |
| Data source access denied during crawl | `You don't have permission to access this data source. You can contact the owner of this data source to request permission.` | Third-party application access via OAuth is disabled. Follow steps to [manage security policies](/azure/devops/organizations/accounts/change-application-access-policies?view=azure-devops#manage-a-policy&preserve-view=true) to enable OAuth. |
| Expired credentials during crawl | `Credentials associated with this data source have expired. Renew the credentials and then update the connection` | The registered app might be deleted or the client secret expired. Regenerate the secret or re-register the app. |
| Item inaccessible during crawl | `Item listed but no longer accessible or no longer exists` | The crawling account might be missing **Basic** access level. Crawls fail with Stakeholder access. Verify the access level. |

## Related content

- [Azure DevOps Wiki connector overview](azure-devops-wiki-overview.md)
- [Deploy the Azure DevOps Wiki connector](azure-devops-wiki-deployment.md)
