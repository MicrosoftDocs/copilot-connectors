---
title: "GitHub Server Pull Requests Microsoft 365 Copilot connector troubleshooting"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 12/08/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the GitHub Server Pull Requests Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the GitHub Server Pull Requests Microsoft 365 Copilot connector

The GitHub Server Pull Requests connector enables your organization to index pull request metadata from GitHub Enterprise Server and surface it in Microsoft 365 Copilot, Copilot Search, and Microsoft Search. This article provides troubleshooting information for common errors that you might encounter when deploying or indexing data with the GitHub Server Pull Requests connector.

To verify GitHub configuration prerequisites that may help troubleshoot errors, see  
[Set up the GitHub service for GitHub Server Pull Requests connector ingestion](github-server-pull-requests-admin-setup.md).

## GitHub Server Pull Requests connector troubleshooting

The following table lists common errors and possible resolutions.

| Scenario     | Error | Resolution      |
|--------------|-------|-----------------|
| GitHub app not installed in target organization during test authentication | The GitHub app isn't installed in the selected organization. | Install the GitHub app in the organization settings before authorizing. |
| No GitHub organizations detected for OBO authentication during test | No organizations were found for the provided credentials. | Install the GitHub app in your organization's settings before authorizing. |
| Token retrieval failed during test authentication         | Unable to obtain an access token. | Verify and update your credentials.                                   |
| Missing required GitHub app permissions detected during test authentication | Missing required permissions.  | Be sure to grant all required GitHub app permissions. For details, see [Use a custom GitHub app for authentication](github-server-pull-requests-admin-setup.md#use-a-custom-github-app-for-authentication).  |
| Test authentication request blocked by IP restriction     | The request was blocked due to IP restrictions.  | Add the GCS computer IP address to the allowlist.  |
| Invalid authentication type selected during connection creation | Invalid authentication type selected. | Use a supported authentication type.  |
| No searchable items found when previewing content    | Preview returned no results.  | Make sure that at least one searchable item exists.   |

## Related content

- [GitHub Server Pull Requests connector overview](github-server-pull-requests-overview.md)
- [Deploy the GitHub Server Pull Requests connector](github-server-pull-requests-deployment.md)