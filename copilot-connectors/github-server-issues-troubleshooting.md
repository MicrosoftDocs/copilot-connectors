---
title: "Troubleshoot issues with the GitHub Server Issues Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 12/04/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the GitHub Server Issues Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the GitHub Server Issues Microsoft 365 Copilot connector

The GitHub Server Issues Microsoft 365 Copilot connector integrates GitHub issue data into Microsoft 365. This article provides troubleshooting information for common errors that you might encounter when you deploy the GitHub Server Issues connector. 

To verify GitHub configuration information to help troubleshoot errors, see [Set up the GitHub service for connector ingestion](github-server-issues-admin-setup.md).

## GitHub Server Issues connector troubleshooting

The following table lists common scenarios, error messages, and guidance for resolving issues.

| Scenario     | Error | Resolution      |
|--------------|-------|-----------------|
| GitHub app not installed in target organization during test authentication | The GitHub app isn't installed in the selected organization. | Install the GitHub app in the organization settings before authorizing. |
| No GitHub organizations detected for OBO authentication during test | No organizations were found for the provided credentials. | Install the GitHub app in your organization's settings before authorizing. |
| Token retrieval failed during test authentication         | Unable to obtain an access token. | Verify and update your credentials.                                   |
| Missing required GitHub app permissions detected during test authentication | Missing required permissions.  | Be sure to grant all required GitHub app permissions. For details, see [Use a custom GitHub app for authentication](github-server-issues-admin-setup.md#use-a-custom-github-app-for-authentication).  |
| Test authentication request blocked by IP restriction     | The request was blocked due to IP restrictions.  | Add the GCS computer IP address to the allowlist.  |
| Invalid authentication type selected during connection creation | Invalid authentication type selected. | Use a supported authentication type.  |
| No searchable items found when previewing content    | Preview returned no results.  | Make sure that at least one searchable item exists.   |

## Related content

- [GitHub Server Issues connector overview](github-server-issues-overview.md)
- [Deploy the GitHub Server Issues connector](github-server-issues-deployment.md)
