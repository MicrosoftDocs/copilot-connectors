---
title: Troubleshoot issues with the GitHub Cloud Issues Microsoft 365 Copilot connector
description: "Learn about troubleshooting the GitHub Cloud Issues Microsoft 365 Copilot connector."
author: Lauragra
ms.author: lauragra
ms.reviewer: lauragra
manager: calvind
ms.date: 11/20/2025
ms.service: copilot-connectors
ms.topic: concept-article
---

# Troubleshoot issues with the GitHub Cloud Issues Microsoft 365 Copilot connector

The GitHub Cloud Issues Microsoft 365 Copilot connector enables your organization to index GitHub issues so they can be surfaced in Microsoft 365 Copilot and Microsoft Search experiences. This article provides troubleshooting information for common errors that you might encounter when you deploy or use the connector.

To verify GitHub configuration information to help troubleshoot errors, see [Set up the GitHub service for GitHub Cloud Issues connector ingestion](github-cloud-issues-admin-setup.md).

## GitHub Cloud Issues connector troubleshooting

The following table lists common errors and steps to resolve them.

| Error message or issue | Possible cause | Resolution |
|-------------------------|---------------|------------|
| **Authentication failed** | Incorrect client ID, client secret, or private key used during setup. | Verify that the GitHub App credentials match the values in your GitHub App configuration. Regenerate the client secret if necessary. |
| **SSO login not supported** | Attempting to authenticate using single sign-on (SSO) during connector setup. | Sign in with a GitHub account that doesn't require SSO for configuration. |
| **Insufficient permissions** | GitHub App doesn't have the required permissions. | Make sure that the GitHub App has read-only permissions for Administration, Metadata, Issues, Members, and Email addresses. |
| **Crawl failures after IP restriction** | Firewall rules block connector IP ranges. | Add the connector’s IP ranges to your allowlist. For details, see [Firewall settings](github-cloud-issues-admin-setup.md#configure-firewall-settings). |
| **Identity mapping errors** | GitHub user identities don't match Microsoft Entra ID properties. | Configure identity mapping using email, sign in, or name. Use regex transformations if direct mapping fails. |
| **Rate limit exceeded** | Too many requests from a single GitHub user account. | Use separate user accounts for OAuth authentication to distribute API calls. |

## Related content

- [GitHub Cloud Issues connector overview](github-cloud-issues-overview.md)
- [Deploy the GitHub Cloud Issues connector](github-cloud-issues-deployment.md)
