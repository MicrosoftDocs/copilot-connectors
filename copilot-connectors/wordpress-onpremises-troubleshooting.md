---
title: "Troubleshoot issues with the WordPress.org Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: rantang
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 12/12/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the WordPress.org Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the WordPress.org Microsoft 365 Copilot connector

With the WordPress.org Microsoft 365 Copilot connector for WordPress.org websites, your organization can index published posts and pages so users can discover that content in Microsoft 365 Copilot and Microsoft Search experiences. After you configure the connector and index content, end users can search for those published posts and pages from Copilot and Microsoft Search clients.

This article provides troubleshooting information for common errors that you might encounter when you deploy the WordPress.org connector.

## WordPress.org connector troubleshooting

The following table lists common errors and how to resolve them.

| Deployment step | Error or error message | Possible reason | Resolution |
|---|---|---|---|
| Connection settings | Can't authenticate with the data source. | The WordPress.org–built website URL or credentials are incorrect, or application passwords aren’t enabled. | Verify the site URL, confirm **basic authentication** is configured, and use an admin account with a valid **application password** for REST API access. |
| Connection settings | Don't have permission to access this data source. | The account used doesn’t have privileges to create or use application passwords. | Use a WordPress admin account that can create and manage **application passwords**; then reenter credentials for the connector. |
| Graph connector agent | Unable to select or use the Graph connector agent; connection fails. | The **Microsoft Graph connector agent** isn’t installed, configured, or can’t reach the WordPress.org instance. | Install the agent, select the correct configuration in the connector, and ensure network connectivity from the agent host to your WordPress.org site. Restart the agent if needed. |
| Content ingestion filters | Expected pages or posts are missing from results. | Index filters are too restrictive (for example, indexing **posts** only or limiting to certain **categories**). | Review ingestion filters, include both **posts** and **pages** if desired, and expand category selections. Use **Preview results** to validate. |
| Sync schedule | Content isn’t updating on the expected cadence. | Crawl schedules aren’t aligned with business needs. | Check **incremental crawl** (default: every 15 minutes) and **full crawl** (default: every day) and adjust the schedules in **Custom setup**. |
| Throughput and performance | Crawl is slow or throttled. | WordPress REST API rate limits are constraining ingestion. | Increase allowed request rates (for example, >50 requests/second) if server capacity permits, or stagger crawls to reduce contention. |

## Related content

- [WordPress.org connector overview](wordpress-onpremises-overview.md)
- [Deploy the WordPress.org connector](wordpress-onpremises-deployment.md)
