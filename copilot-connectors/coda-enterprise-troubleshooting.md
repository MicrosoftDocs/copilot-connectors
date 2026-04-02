---
title: "Coda Enterprise connector troubleshooting"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: irenehuang
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 12/16/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Coda Enterprise Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Coda Enterprise connector

The Coda Enterprise connector allows your organization to index documents and pages from Coda Enterprise. This article provides troubleshooting information for common issues you might encounter when you deploy or use the Coda Enterprise connector.

## Coda Enterprise connector troubleshooting

The following table lists common issues and recommended troubleshooting steps.

| Issue | Explanation | Recommended steps |
|-------|-------------|-------------------|
| Unsupported Coda edition | The connector supports only the Coda Enterprise edition. Free, Pro, and Team editions aren't supported due to Coda API limitations. | Verify that your Coda environment is licensed for the Enterprise edition. Confirm with your Coda admin or Coda support. |
| API token errors | API tokens might be missing, invalid, or associated with insufficient permissions. | Ensure a Coda Org Admin generated the API token. Confirm the token was created under **Account settings** > **API settings**. Use the default token scopes (Doc or table, Read and write). |
| Large documents not indexed | Documents over 125 MB can't be exported through the Coda API. | Reduce document size below 125 MB or split large documents into multiple smaller files. |
| High API usage or rate limiting | Coda imposes API limits per user/IP, which might affect large indexing operations. | Apply a content filter to limit the time range of indexed items. Consider setting up multiple connections to distribute the load. |
| Missing or incomplete search results | Content might be excluded due to time range settings, permissions, or sync intervals. | Verify content filters under **Custom setup** > **Data** > **Content filter**. Confirm permissions and identity mapping settings. Review incremental and full crawl frequency settings. |
| Incorrect user access in search results | Users might see content they should or shouldn't have access to. | Review Access permissions settings. Confirm identity mapping alignment between Coda email IDs and Microsoft Entra UPNs. Provide a custom mapping formula if needed. |
| Slow indexing or delayed updates | Full and incremental crawl settings might affect how quickly updates appear. | Check **Custom setup > Crawl**. Adjust incremental crawl frequency if freshness is a priority. |

## Related content

- [Coda Enterprise connector overview](coda-enterprise-overview.md)
- [Deploy the Coda Enterprise connector](coda-enterprise-deployment.md)
