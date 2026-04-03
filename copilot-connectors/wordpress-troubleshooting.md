---
title: "Troubleshoot issues with the WordPress.com connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: rantang
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 12/11/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the WordPress.com Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the WordPress.com connector

The WordPress.com Microsoft 365 Copilot connector indexes published posts and pages from WordPress.com websites so users can discover and use that content in Microsoft 365 Copilot and Microsoft Search experiences. This article provides troubleshooting information for common errors that you might encounter when you deploy the WordPress.com connector or when the connector indexes data. 

## WordPress.com connector troubleshooting

The following table lists common issues, causes, and resolution steps for the WordPress.com connector.

| Deployment or crawl step | Error/symptom | Possible cause | Resolution |
|----|----|----|----|
| Connection settings | Can't authenticate with the data source. | Incorrect WordPress.com–built website URL or misconfigured OAuth 2.0 credentials (client ID/secret). | Verify the canonical site URL (for example, https://contoso.wordpress.com). Confirm the OAuth app values in WordPress.com and reenter the client ID and client secret in the connector. Authenticate with a WordPress.com site admin account. |
| Connection settings | Don't have permission to access this data source. | OAuth 2.0 isn’t enabled or a site admin didn't complete the authorization flow. | Ensure a site admin created the OAuth application in the WordPress.com Developer Center and approved the authorization flow. Rerun authentication using a site admin account. |
| Connection settings | Redirect URI mismatch during OAuth. | The OAuth app redirect URL doesn’t match the required Microsoft 365 callback. | In the OAuth app, set Microsoft 365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback` or Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`. Save and retry authorization. |
| Rollout | Users report no WordPress.com results in Copilot or Search. | The connection is rolled out to a limited audience and affected users aren’t included. | On the connector page, turn off Rollout to limited audience or add the required users/groups to the rollout list. Publish changes and allow the next crawl to complete. |
| Content | Comments aren’t indexed or visible. | The connector doesn’t index comments by design. | Use WordPress.com posts and pages as the authoritative content types. If comments contain critical information, move it into page or post content. |
| Content filters | Expected posts/pages are missing. | Filters are scoped to posts or pages, or only posts from specific categories are included. | Review Content selection and Filter indexed content settings. Use Preview results to validate property values (for example, categories) before publishing changes. |
| Crawl performance | Indexing is slow or HTTP 429 (rate limit) appears. | WordPress.com platform rate limits requests; VIP customers are capped at 10 requests/second and non‑VIP limits are typically lower. | Reduce concurrent crawl load (avoid frequent full crawls), allow more time for large sites, and rely on incremental crawls for ongoing updates. Retry after backoff when 429 is returned. |
| Visibility | All published content is visible to the tenant, contrary to expectations. | The connector doesn’t crawl user identities or page‑level permissions. | If you need scoped visibility, limit indexing via filters (for example, specific categories) or use separate connections per audience. Communicate tenant‑wide visibility to stakeholders. |
| Sync | Data isn’t updating as expected. | Default schedules are incremental: every 15 minutes and full: daily; recent changes might not be picked up yet. | Wait for the next incremental crawl or adjust Customize sync intervals to meet your refresh needs. Trigger a full crawl for major content changes. |

### Best practices

Apply the following guidance to reduce the likelihood of errors with the connector:

- When you create the OAuth application, make sure that the required fields (Name, Description, Website URL, Redirect URL, Type) are set correctly to avoid authentication errors.
- Use the display name and content source filter to help users identify WordPress.com content in Copilot and Microsoft Search.
- For large sites, plan crawls outside peak publishing windows to minimize rate‑limit throttling.

## Related content

- [WordPress.com connector overview](wordpress-overview.md)
- [Deploy the WordPress.com connector](wordpress-deployment.md)
