---
title: "GitLab Issues Cloud connector troubleshooting"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 01/20/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the GitLab Issues Cloud Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the GitLab Issues Cloud connector

The GitLab Issues Cloud Microsoft 365 Copilot connector allows your organization to index issue data stored in GitLab.com and makes that information available in Microsoft 365 Copilot and Microsoft Search. This article provides troubleshooting information for common errors that you might encounter when you deploy the GitLab Issues Cloud connector.

## GitLab Issues Cloud connector troubleshooting

The following table lists common errors, their possible causes, and recommended resolutions.

| Error message | Possible reason | Resolution |
|---------------|-----------------|------------|
| **Having trouble? Try signing in again.** | The sign-in attempt in the popup window was unsuccessful.| Try signing in again. If the issue persists, reauthorize the connector in the Microsoft 365 admin center. |
| **The account doesn't have permission to access this data source.** | The authentication was successful, but the GitLab account lacks the necessary permissions or scopes such as `read_api`.| Make sure the authentication account has access to the GitLab projects whose issues you want to index, that it can read issues in those projects, and that the correct scopes (for example, `read_api`) are granted. Update the credentials if needed. |
| **Failed to connect to GitLab.** | The GitLab server is unreachable due to network issues, incorrect GitLab URL, or firewall settings. | Confirm that GitLab is accessible from your environment, verify network connectivity, and check firewall configuration. |
| **The crawler account does not have permissions for the item.** | The crawler account lacks read access to the GitLab project or its issues. | Verify that the crawler account can view issues in the relevant GitLab projects. If issue visibility depends on project-level permissions (such as repository membership), ensure those permissions are granted, and confirm that authentication credentials are current. |

## Related content

- [GitLab Issues Cloud connector overview](gitlab-issues-cloud-overview.md)
- [Deploy the GitLab Issues Cloud connector](gitlab-issues-cloud-deployment.md)
