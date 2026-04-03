---
title: "Zendesk Help Center connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: ang.gao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 11/24/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Zendesk Help Center Copilot connector."
---

# Zendesk Help Center connector overview

The Zendesk Help Center Microsoft 365 Copilot connector enables organizations to index published articles from Zendesk Help Center (also known as Zendesk Guide). After you configure the connector, users can discover and search for support content directly within Microsoft 365 Copilot and Microsoft Search experiences. This integration allows end users to ask questions and reference Zendesk articles without leaving Microsoft 365.

## Why use the Zendesk Help Center connector to index your data?

The Zendesk Help Center connector helps organizations centralize support knowledge and improve discoverability for users. Common use cases include:

- Provide employees with instant access to support articles and product information.
- Allow natural language queries for troubleshooting, policies, and product details.
- Support customer service teams with up-to-date knowledge base content.
- Enhance self-service support by surfacing relevant Zendesk articles in Copilot and Microsoft Search.

## Build agents with the Zendesk Help Center connector

Developers can use the Zendesk Help Center connector as a knowledge source in declarative agents built with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/copilot-studio-lite), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts users can use to retrieve information from Zendesk Help Center:

- What is the return policy for apparels?
- What are the product specifications for the Surface Laptop?
- How can I upgrade my subscription?

## Zendesk Help Center connector capabilities and limitations

The Zendesk Help Center connector enables users to:

- Index published articles from Zendesk Help Center (Guide).
- Perform natural language queries related to support topics and product information.
- Use semantic search in Copilot and Microsoft Search to find relevant content based on context, keywords, and user preferences.
- Enforce permissions so users only see search results for documents they can access. When a user selects a search result, Zendesk Help Center enforces access permissions.

The connector has the following limitations:

- Community posts and topics from Zendesk Guide aren't indexed.
- File attachments within articles aren't supported.

## Data types indexed from Zendesk Help Center

The connector indexes the following data types:

- Knowledge base articles: Main body, title, author, category, labels, created/updated dates, and URLs.
- Properties: AuthorId, Body (content), CategoryId, CategoryName, HtmlUrl (URL), LabelNames, Locale, SectionId, SectionName, SourceLocale, Title, UpdateDate, UserSegmentId, VoteCount, and VoteSum.

## Permissions model and access control

Admins can configure access permissions so that indexed data appears in search results for either all users or only users with access to the data source. The connector supports mapping Zendesk user identities to Microsoft Entra ID using email addresses. Custom mapping formulas are available for organizations with different identity structures.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Zendesk Help Center connector](zendesk-help-center-deployment.md)
