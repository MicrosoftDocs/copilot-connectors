---
title: "Adobe Experience Manager Assets Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: rantang
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 12/09/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Adobe Experience Manager Assets Microsoft 365 Copilot connector."
---

# Adobe Experience Manager Assets Microsoft 365 Copilot connector overview

The Adobe Experience Manager (AEM) Assets Copilot connector indexes published assets from your AEM Assets instance so users can discover, preview, and reuse brand‑approved content directly in Microsoft 365 Copilot and Microsoft Search across Microsoft 365. This integration helps reduce app‑switching and ensures that teams work with authoritative, on‑brand materials.

## Why use the Adobe Experience Manager Assets connector to index your data?

Many organizations rely on AEM Assets as their central digital asset management (DAM) system for brand libraries—images, videos, documents, design files, and reusable creative elements. The connector removes silos by integrating published assets into Microsoft 365 so people can quickly discover, preview, and reuse approved content in their daily tools. Common benefits include:

- **Centralized asset discovery:** Surface AEM‑managed, published digital assets across Microsoft 365 (Copilot, Microsoft Search) to ensure access to authoritative, on‑brand content.
- **Brand consistency at scale:** Find approved logos, product images, templates, and campaign materials for use in Word, PowerPoint, Teams, and more.
- **Enhanced productivity:** Use natural‑language across Copilot to search, reference, summarize, and preview assets without leaving Microsoft 365.

The following table lists use cases for different audiences. 

| Department/Role      | Use case | Business benefit |
|----------------------|----------|------------------|
| Marketing & Brand     | Locate and utilize current assets, streamline collaboration on marketing projects, and access the latest materials directly through Copilot. | Ensures campaigns use current, accurate assets.               |
| Sales & Pre‑Sales     | Assemble proposals and decks using product visuals, case‑study PDFs, and datasheets sourced from AEM Assets in Copilot and Microsoft Search. | Accelerates proposal creation and improves personalization.    |
| All employees         | Self‑serve authoritative, reusable assets (templates, icon sets, product photos) via Microsoft Search and Copilot. | Reduces context switches; improves consistency across deliverables. |

## Build agents with the Adobe Experience Manager Assets connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Eaxmple prompts

The following examples show prompts that agent builders can use to help their users retrieve information from Adobe Experience Manager Assets:

- Find latest assets for the summer promotion campaign.
- Find approved logo set and brand guidelines PDF.
- Find product hero images for Brand X.
- Find assets for APAC region product launch.

## Adobe Experience Manager Assets connector capabilities and limitations

The Adobe Experience Manager Assets connector allows users to:

- Index the published assets of your AEM Assets instance.
- Customize crawl frequency to fit your data refresh needs.
- Create workflows using this connection with plugins from Copilot Studio.
- Apply ingestion filters based on page paths (exact matches and regular-expression phrase matches).
- Apply ingestion filters based on metadata properties (standard and custom) using JSON paths and operators.
- Use [Semantic search in Copilot](/microsoft-365/copilot/connectors/semantic-index-for-copilot) to help users find relevant content.

The Adobe Experience Manager Assets connector has the following limitations:

- Doesn't crawl user identities or access permissions; all published assets indexed by this connector are visible to all Microsoft 365 users in the tenant (from Microsoft Search or Copilot).
- Supports Adobe Experience Manager Assets (Cloud) only; other AEM solutions such as Sites require separate connectors.

## Data types indexed from Adobe Experience Manager Assets

By default, the connector indexes published assets across common formats (for example, PDF, PNG, JPG, and other supported file types) so they can be discovered in Copilot and Microsoft Search. This indexing ensures that every published digital asset in your AEM Assets instance is reusable within Microsoft 365 workflows.

## Permissions model and access control

By default, all published assets indexed with the connector are visible to all Microsoft 365 users in your tenant, from Microsoft Search or Copilot. Admins can optionally stage rollout to validate with a limited audience before broad deployment and use content filtering (paths and metadata) to select which assets are indexed.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Adobe Experience Manager Assets connector](adobe-experience-manager-assets-deployment.md)
