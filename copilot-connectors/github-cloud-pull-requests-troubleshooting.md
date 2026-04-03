---
title: Troubleshoot issues with the GitHub Cloud Pull Requests connector
description: Find troubleshooting information for the GitHub Cloud Pull Requests Microsoft 365 Copilot connector, including common errors and steps to resolve them.
ms.topic: troubleshooting-general
ms.service: copilot-connectors
author: lauragra
ms.author: lauragra
manager: calvind
ms.date: 11/20/2025
ms.localizationpriority: Medium
---

# Troubleshoot issues with the GitHub Cloud Pull Requests connector

The GitHub Cloud Pull Requests Microsoft 365 Copilot connector enables your organization to index pull requests stored in GitHub repositories into Microsoft 365 Copilot and Microsoft Search experiences. This article provides troubleshooting information for common errors that you might encounter when you deploy or use the connector.

To verify GitHub configuration information to help troubleshoot errors, see [Set up the GitHub service for connector ingestion](github-cloud-pull-requests-admin-setup.md).

## GitHub Cloud Pull Requests connector troubleshooting

The following table lists common errors and possible resolutions for those errors.

| Error | Possible cause | Resolution |
|-------|----------------|------------|
| **Authentication failed** | Incorrect client ID, client secret, or private key. | Verify that the GitHub App credentials entered in the Microsoft 365 admin center match the values generated in GitHub. Regenerate the client secret if necessary. |
| **SSO sign in not supported** | GitHub authentication flow doesn't support single sign-on (SSO) during setup. | Ensure the account used for authentication is signed in directly to GitHub before configuring the connector. |
| **Insufficient permissions** | GitHub app permissions aren't set correctly. | Confirm that the GitHub app has **Read-only** permissions for Administration, Metadata, Pull Requests, Members, and Email addresses. |
| **Connector stopped crawling** | IP firewall restrictions block connector access. | Add the connector's IP ranges to the allowlist in your firewall settings. For details, see [Configure firewall settings](github-cloud-pull-requests-admin-setup.md#configure-firewall-settings). |
| **Identity mapping failed** | GitHub user identities don't match Microsoft Entra ID properties. | Review identity mapping settings in the connector configuration. Use email, sign-in, or name mapping, and apply regex transformations if needed. |
| **Rate limit exceeded** | GitHub API rate limits reached for the authenticated user. | Use separate user accounts for OAuth authentication with each connection to distribute API calls. |

## Related content

- [GitHub Cloud Pull Requests connector overview](github-cloud-pull-requests-overview.md)
- [Deploy the GitHub Cloud Pull Requests connector](github-cloud-pull-requests-deployment.md)
