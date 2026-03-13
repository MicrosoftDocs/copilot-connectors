---
title: "Bitbucket Knowledge Microsoft 365 Copilot connector troubleshooting"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 01/27/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Bitbucket Knowledge Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Bitbucket Knowledge Microsoft 365 Copilot connector

The Bitbucket Knowledge connector indexes Markdown (.md) and text (.txt) files from your Bitbucket Cloud repositories so users can retrieve documentation through Copilot, Copilot Search, and Microsoft Search. This article provides troubleshooting information for common issues you might encounter when deploying or indexing content with the Bitbucket Knowledge connector.

## Bitbucket Knowledge connector troubleshooting

The following table lists common errors you might encounter when you configure or use the Bitbucket Knowledge connector, along with possible causes and recommended resolutions.

| **Error message** | **Possible cause** | **Resolution** |
|-------------------|--------------------|----------------|
| **Data source unreachable** | The connector can't reach the Bitbucket API due to network issues or a Bitbucket service outage. | Check the Bitbucket status page and confirm network availability. Retry the operation after the service stabilizes. |
| **Source throttling crawl** | Too many API requests to the Bitbucket API resulted in HTTP 429 responses. | The connector automatically retries with exponential backoff. If the issue persists, reduce the crawl frequency or distribute indexing load across multiple OAuth users. |
| **Authentication error** | OAuth token is invalid, expired, or missing. App credentials might be incorrect. | Reauthenticate using valid Bitbucket OAuth credentials. Verify that the OAuth consumer key and secret are correct. |
| **Authorization error** | Insufficient permissions to access the workspace or repositories (HTTP 403). | Ensure the OAuth app has **account**, **repositories**, and **pull request** permissions. Confirm the authenticated user has read access to all selected repositories. |
| **Credentials expired** | The OAuth refresh token is invalid or expired. | Reauthenticate to generate new OAuth tokens. Confirm that OAuth access wasn’t revoked in Bitbucket settings. |
| **Identity mapping errors** | Bitbucket user identities (full name or public name) don’t match Microsoft Entra ID properties. | Configure identity mapping using full name, public name, or a regex transformation to align user identities. |
| **No searchable items found when previewing content** | The selected repositories contain no `.md` or `.txt` files, or the preview query returned no results. | Confirm that the repositories include documentation files. Ensure that folders such as `/docs`, `/runbooks`, or `/onboarding` contain Markdown or text files. |
| **Internal error** | An unexpected error occurred during indexing. | Check connector logs for details. If the issue persists, contact Microsoft support. |

## Related content

- [Bitbucket Knowledge connector overview](bitbucket-knowledge-overview.md)
- [Deploy the Bitbucket Knowledge connector](bitbucket-knowledge-deployment.md)