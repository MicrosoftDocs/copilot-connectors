---
title: "WordPress.com connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: rantang
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 12/11/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the WordPress.com Microsoft 365 Copilot connector."
---

# WordPress.com connector overview

The WordPress.com Microsoft 365 Copilot connector indexes published posts and pages from WordPress.com websites so users can discover and use that content in Microsoft 365 Copilot and Microsoft Search experiences. After admins configure the connection and data is indexed, users can search for published posts and pages directly in Copilot and other Microsoft Search clients.

## Why use the WordPress.com connector to index your data?

Organizations that publish information on WordPress.com often need that content to be accessible where work happens. Indexing WordPress.com content into Microsoft 365 enables employees to find and reuse authoritative pages and posts without switching tools, improving workflow efficiency and decision-making.

The following table summarizes common scenarios and benefits for different roles.

| Department/role | Use case | Business benefit |
|----|----|----|
| IT support/help desk | Retrieve troubleshooting documentation | Faster issue resolution, improved consistency. |
| Marketing/sales | Access the latest product pages and campaign information | Consistent messaging, faster external responses. |
| Executives/managers | Summarize policy and project updates | Accelerated decisions, greater visibility. |
| All employees | Summarize onboarding guides, policies, FAQs | Self‑service discovery and application of organizational knowledge. |

## Build agents with the WordPress.com connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that users can use to retrieve information from the content indexed by the connector:

- Find the dental benefit page.
- Find pages related to data privacy compliance.
- Find pages about employee onboarding.
- Summarize the key points of the mentorship program.
- Create a checklist for the new hire onboarding process using all relevant SOP webpages.

## WordPress.com connector capabilities and limitations

The WordPress.com connector enables users to:

- Index published posts and pages from WordPress.com websites.
- Choose what data to index, including posts or pages and posts associated with specific categories.
- Customize crawl frequency to fit data refresh needs.
- Create workflows using this connection and plugins from Microsoft Copilot Studio.
- Use semantic search to help users find relevant content.

The WordPress.com connector has the following limitations:

- It doesn't index comments.
- It doesn't crawl user identities or access permissions; all indexed published pages and posts are visible to all Microsoft 365 users in your tenant.
- It supports WordPress.com only; WordPress.org scenarios require different solutions.
- Platform rate limits might slow large crawls (for VIP customers, up to 10 requests/second; limits for non‑VIP customers are typically lower).

## Data types indexed from WordPress.com

By default, the connector indexes WordPress.com pages and posts so they can be used in Copilot and Microsoft Search.

## Permissions model and access control

Because the connector doesn't ingest user identities or permissions, all published posts and pages indexed by the connector are available to all Microsoft 365 users in your tenant from Microsoft Search and Copilot. Admins can validate the connection with a limited audience before wider rollout by using staged rollout features.

## Next step

> [!div class="nextstepaction"]
> [Deploy the WordPress.com connector](wordpress-deployment.md)
