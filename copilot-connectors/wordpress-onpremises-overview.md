---
title: "WordPress.org connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: rantang
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 12/12/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the WordPress.org Microsoft 365 Copilot connector."
---

# WordPress.org connector overview

With the WordPress.org Microsoft 365 Copilot connector for WordPress websites, your organization can index published posts and pages so users can discover that content in Microsoft 365 Copilot and Microsoft Search experiences. After you configure the connector and index content,  users can search for those published posts and pages from Copilot and Microsoft Search clients.

## Why use the WordPress.org connector to index your data?

Many organizations rely on WordPress.org as their public site, knowledge base, or publishing platform, but content can be siloed and hard to search across tools. The WordPress.org Copilot connector integrates WordPress.org–built website content into Microsoft 365 so employees can access and reuse pages and posts directly in their workflow.

The following are common use cases for the connector:

- Centralized discovery of published pages and posts across Microsoft 365 tools to reduce context switching.
- Summarize, analyze, and generate insights from site content using natural language prompts to accelerate knowledge sharing.

## Build agents with the WordPress.org connector

Developers can use this connector as a knowledge source in declarative agents built with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that agent builders can use to help their users retrieve information from WordPress.org websites:

- Find the dental benefit page.
- Find pages related to data privacy compliance.
- Find pages about employee onboarding.
- Summarize the key points of the mentorship program.
- Create a checklist for the new hire onboarding process using all relevant SOP webpages.

## WordPress.org connector capabilities and limitations

The WordPress.org connector enables users to:

- Index published posts and pages of your WordPress.org website.
- Choose what data to index (posts or pages) and filter posts by categories.
- Customize crawl frequency to align with refresh needs.
- Create workflows using this connection and plugins from Copilot Studio.
- Use semantic search in Copilot to help users find relevant content.

The WordPress.org connector has the following limitations:

- Comments aren’t indexed.
- User identities and access permissions aren’t crawled. All indexed published pages or posts are visible to all Microsoft 365 users in your tenant from Microsoft Search or Copilot.
- Supports WordPress.org only. WordPress.com requires a separate cloud connector.
- Ingestion throughput depends on your WordPress REST API rate limit. Performance improves with higher allowable request rates (for example, >50 requests/second) when server capacity permits.

## Data types indexed from WordPress.org

By default, the connector crawls published **posts** and **pages** from WordPress.org websites so they can be used in Copilot and Microsoft Search results.

## Permissions model and access control

The connector doesn't enforce access permissions from the source. All published pages or posts indexed using the WordPress.org connector are visible to all Microsoft 365 users in your tenant. You can validate the connection with a limited audience before broad rollout using staged deployment and control **which** content is indexed with ingestion filters.

## Next step

> [!div class="nextstepaction"]
> [Deploy the WordPress.org connector](wordpress-onpremises-deployment.md)
