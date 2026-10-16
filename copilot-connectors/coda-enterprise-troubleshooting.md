---
title: "Superhuman Docs Enterprise connector troubleshooting"
ms.author: jasonjoh
author: jasonjoh
manager: calvind
ms.reviewer: irenehuang
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.date: 10/08/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Superhuman Docs Enterprise Microsoft 365 Copilot connector."
---

<!-- cSpell:ignore irenehuang -->

# Troubleshoot issues with the Superhuman Docs Enterprise connector

The Superhuman Docs Enterprise connector enables your organization to index documents and pages from Superhuman Docs Enterprise. This article provides troubleshooting information for common issues you might encounter when you deploy or use the Superhuman Docs Enterprise connector.

## Superhuman Docs Enterprise connector troubleshooting

The following table lists common issues and recommended troubleshooting steps.

| Issue | Explanation | Recommended steps |
|-------|-------------|-------------------|
| Unsupported Superhuman Docs edition | The connector supports only the Superhuman Docs Enterprise edition. Free, Pro, and Team editions aren't supported due to Superhuman Docs API limitations. | Verify that your Superhuman Docs environment is licensed for the Enterprise edition. Confirm with your Superhuman Docs admin or Superhuman support. |
| API token errors | API tokens might be missing, invalid, or associated with insufficient permissions. | Ensure a Superhuman Docs Org Admin generated the API token. Confirm the token was created under **Account settings** > **API settings**. Use the default token scopes (Doc or table, Read and write). |
| Large documents not indexed | Documents over 125 MB can't be exported through the Superhuman Docs API. | Reduce document size to under 125 MB or split large documents into multiple smaller files. |
| High API usage or rate limiting | Superhuman Docs imposes API limits per user/IP, which might affect large indexing operations. | Apply a content filter to limit the time range of indexed items. Consider setting up multiple connections to distribute the load. |
| Missing or incomplete search results | Content might be excluded due to time range settings, permissions, or sync intervals. | Verify content filters under **Custom setup** > **Data** > **Content filter**. Confirm permissions and identity mapping settings. Review incremental and full crawl frequency settings. |
| Incorrect user access in search results | Users might see content they should or shouldn't have access to. | Review Access permissions settings. Confirm identity mapping alignment between Superhuman Docs email IDs and Microsoft Entra UPNs. Provide a custom mapping formula if needed. |
| Slow indexing or delayed updates | Full and incremental crawl settings might affect how quickly updates appear. | Check **Custom setup > Crawl**. Adjust incremental crawl frequency if freshness is a priority. |

## Related content

- [Superhuman Docs Enterprise connector overview](coda-enterprise-overview.md)
- [Deploy the Superhuman Docs Enterprise connector](coda-enterprise-deployment.md)
