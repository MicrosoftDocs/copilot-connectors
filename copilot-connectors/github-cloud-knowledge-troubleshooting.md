---
title: "Troubleshoot issues with the GitHub Cloud Knowledge Microsoft 365 Copilot connector"
ms.author: lauragra
author: Lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 11/20/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the GitHub Cloud Knowledge Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the GitHub Cloud Knowledge Microsoft 365 Copilot connector

The GitHub Cloud Knowledge Microsoft 365 Copilot connector enables organizations to index markdown and text files from GitHub repositories into Microsoft 365 Copilot and Microsoft Search experiences. This article provides troubleshooting information for common errors that you might encounter when deploying or managing the connector.

To verify GitHub configuration information to help troubleshoot errors, see [Set up the GitHub service for GitHub Cloud Knowledge connector ingestion](github-cloud-knowledge-admin-setup.md).

## GitHub Cloud Knowledge connector troubleshooting

The following table lists common errors and steps to resolve them:

| Error message or issue | Possible cause | Resolution |
|-------------------------|---------------|------------|
| **Authentication failed** | Incorrect client ID, client secret, or private key | Verify that the GitHub app credentials are correct. Regenerate the client secret if needed. For details, see [Set up the GitHub service](github-cloud-knowledge-admin-setup.md). |
| **SSO not supported** | GitHub authentication flow doesn't support single sign-on (SSO) during setup | Make sure that enterprise-managed users sign in before performing setup actions. |
| **No data indexed** | API access not enabled or incorrect repository selection | Confirm that your GitHub instance is accessible via API and that the correct repositories are selected in the connector configuration. |
| **Permission mapping errors** | GitHub identities not mapped to Microsoft Entra ID | Review identity mapping settings. Use email, sign-in, or name mapping options. If direct mapping fails, apply regex transformations. |
| **Rate limit exceeded** | OAuth authentication using a single account | Use separate user accounts for OAuth authentication to avoid hitting GitHub rate limits. |
| **Case-sensitive search issues** | Repository and file names are case-sensitive | When using Index Browser or troubleshooting search results, be sure to match the casing for repository and file names. |

## Related content

- [GitHub Cloud Knowledge connector overview](github-cloud-knowledge-overview.md)
- [Deploy the GitHub Cloud Knowledge connector](github-cloud-knowledge-deployment.md)
