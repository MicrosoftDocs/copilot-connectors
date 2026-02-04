---
title: "Troubleshoot issues with the GitLab Issues Server Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 01/21/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the GitLab Issues Server Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the GitLab Issues Server Microsoft 365 Copilot connector

The GitLab Issues Server Microsoft 365 Copilot connector integrates GitLab issue data into Microsoft 365. This article provides troubleshooting information for common errors that you might encounter when you deploy the GitLab Issues Server connector.  

## GitLab Issues Server connector troubleshooting

The following table lists common errors, possible causes, and recommended actions.

| Step | Error message | Possible reason | Resolution |
|------|---------------|-----------------|------------|
| Authentication | Having trouble? Try signing in again. | The sign‑in attempt in the popup window was unsuccessful. | Try again. Confirm correct GitLab OAuth credentials and retry authentication. |
| Authentication | The account doesn't have permission to access this data source. | Authentication succeeded, but the user lacks required GitLab permissions. Ensure that the `read_api` scope is granted and the user has access to selected repositories, issues, and wikis. | Update the GitLab OAuth scopes and confirm the account has project and group permissions. |
| Crawl initialization | Failed to connect to GitLab. | GitLab is unreachable due to network issues, incorrect server URL, or firewall restrictions. | Confirm the GitLab instance URL, verify the server is running, and ensure the Microsoft Graph Connector Agent can reach the GitLab server.  |
| Item fetching | The crawler account doesn't have permissions for the item. | The authentication account lacks read access for specific issues, repositories, or wiki pages. | Grant the account appropriate access to repositories, issues, or wiki pages in GitLab. |
| Authentication | Invalid authentication type selected. | The wrong authentication method was chosen. GitLab Issues Server supports OAuth 2.0. (Pattern derived from similar GitHub connector issues.) | Select OAuth 2.0 as the authentication type and retry. |
| Content preview | No searchable items found when previewing content. | GitLab returned no items matching the crawl configuration. | Ensure at least one searchable GitLab issue exists and confirm the connector query settings. |

## Related content

- [GitLab Issues Server connector overview](gitlab-issues-server-overview.md)  
- [Deploy the GitLab Issues Server connector](gitlab-issues-server-deployment.md)  
