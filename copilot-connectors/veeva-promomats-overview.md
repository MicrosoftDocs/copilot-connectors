---
title: "Veeva PromoMats Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 03/18/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Veeva PromoMats Microsoft 365 Copilot connector."
---

# Veeva PromoMats Microsoft 365 Copilot connector overview

The Veeva PromoMats Microsoft 365 Copilot connector enables organizations to index and surface approved promotional marketing materials and related compliant content from Veeva Vault PromoMats into the Microsoft 365 ecosystem. After the connector is configured, content stored in PromoMats is accessible in apps such as Microsoft Teams, Outlook, and SharePoint via Microsoft 365 Copilot and Microsoft Search experiences. This integration supports faster content creation, reuse, review, and distribution by making compliant marketing content, localization-ready assets, and regulatory-reviewed documents available directly within Microsoft 365 workflows. 

The connector integrates the Vault PromoMats built-in permission model to ensure that users only access authorized content. It supports content analysis and preparation to help maintain brand consistency and improve efficiency throughout the content lifecycle.

## Why use the Veeva PromoMats connector to index your data?

Organizations in the life sciences and regulated-content domains often face challenges such as knowledge silos (promo-assets, localization libraries, regulatory-approved messaging), inefficient search across Vault and other systems, content duplication, and the need to ensure compliance while accelerating time-to-market. The PromoMats connector addresses these challenges by bringing PromoMats content into Microsoft Graph, allowing Copilot or Microsoft Search to find, summarize, and surface the content in everyday apps without switching context.

The benefits of using the Veeva PromoMats connector include:

- **Boosts productivity** – Marketing, medical affairs, regulatory-review, and localization teams can access PromoMats content directly within Microsoft 365 apps, reducing time spent switching systems.
- **Improves decision-making** – Unified search across PromoMats and Microsoft tools ensures faster access to compliant content, approved messaging, and campaign assets.
- **Accelerates content lifecycle** – Teams can reuse existing compliant assets, summarize messaging, and generate new versions faster, from asset creation and review/MLR approval to localization and field deployment.
- **Enhances collaboration and reuse** – Cross-functional teams (marketing, sales, regulatory, localization) discover and utilize the same approved assets, reducing duplication and ensuring brand consistency across regions.
- **Preserves security and compliance** – The connector honors the Vault PromoMats built-in permissions and access control list (ACL) model so that users only see content they're authorized to access.

## Build agents with the Veeva PromoMats connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Eaxmple prompts

The following table provides examples of prompts that agent builders can use to help users retrieve information from Veeva PromoMats.

| Scenario | Example prompt |
|----------|----------------|
| Content generation | Generate personalized content for customer interactions based on the latest research documents stored in PromoMats. |
| Content tagging | Suggest tags that can be used with the selected promotional content to make it easier to manage and retrieve going forward. |
| HTML email generation | Create HTML emails generated automatically from pre-provided HTML templates and documents stored in PromoMats. |
| Pre-call planning | Summarize relevant information and prepare materials for sales representatives before customer meetings. |
| AI-assisted content reuse | Identify appropriate tags, translation, and localization to improve the reuse of content. |
| Content consistency | Create new promotional materials, ensuring consistency with existing content. |
| Pre-MLR AI-assisted reviews | Review grammar, spelling, and semantics, and cross-validate the following promotional documents. |
| Document summarization | Summarize key points from regulatory documents to ensure all team members are informed of the latest compliance requirements. |
| Meeting preparation | Prepare a script for an upcoming meeting based on recent customer email threads and PromoMats documents. |
| Support claim process | Find claims that can be reused, made about the efficacy of drugs, to ensure they're medically and legally validated and approved. |

## Veeva PromoMats connector capabilities and limitations

The Veeva PromoMats connector enables users to:

- Index promotional marketing materials stored in PromoMats (documents, approved assets, metadata) and surface them via Microsoft Graph so that Copilot and Microsoft Search can use them.
- Enable natural-language queries and summaries of PromoMats content, with link-backs to source assets, when used by Copilot.
- Respect the Vault PromoMats permission and ACL model so that only authorized users see content they have access to.
- Support configurable indexing scope, allowing admins to define which content (assets, versions, metadata) to include—such as filtering by metadata, document state, or time.
- Improve the searchability of promotional documents by using advanced Microsoft 365 search capabilities.
- Gain insights and recommendations from indexed data to enhance workflow efficiency, including checking the usage of specific phrases in PromoMats documents.
- Maintain data privacy and availability by supporting ACL permissions and document-level permissions, simplifying the permission model and reducing the risk of misconfiguration.
- Use query string conditions to precisely control the synchronization of articles, ensuring efficient indexing.

The Veeva PromoMats connector has the following limitations:

- Only indexes the latest version of documents/assets in PromoMats (historical versions might not be surfaced).
- Supported file types are primarily text-based (Microsoft 365 documents, PDFs); nontext files such as .png, .jpg, or video files aren't supported.
- Each document can include up to 4 MB of parsed (extracted) text for ingestion and indexing. In most .docx, .pptx, and .pdf files, the extracted text represents roughly 10% of the original file size, which allows many documents of 30–40 MB to be fully indexed. For other file types, this ratio might differ. If the extracted text exceeds the 4 MB limit, only the first portion is indexed, which might result in partial coverage and incomplete answers in Copilot and Search.
- The connector works when content is in PromoMats in the cloud (Vault) and might require more setup steps for customized or nonstandard vaults.
- Updates to user or group permissions in PromoMats might not be reflected immediately in the index (depending on crawl cadence)—there might be a delay before new access restrictions are honored.
- The indexing speed is constrained by the API rate limits imposed by the Veeva platform. If you have a high volume of documents, you might experience longer completion times. 
- Document fields set to be hidden on the Veeva platform aren't indexed.

## Data types indexed from PromoMats

The connector ingests key content types from PromoMats so they become available in Copilot and Microsoft Search. At a high level, it indexes:

- Approved promotional marketing documents and assets (white papers, case studies, campaigns, email/HTML templates, localization variants) stored in PromoMats.
- Associated metadata (tags, version status, approval state, region/locale indicators) that enable filtering and intelligent retrieval.

After the data is indexed, these items become searchable via Copilot in Microsoft 365 applications (Teams, SharePoint, Outlook) and can be included in AI-generated responses or summaries.

## Permissions model and access control

You can configure the PromoMats connector so that only users who have view-access to a given asset in Vault PromoMats can see it in Copilot responses or search results. The model works as follows:

- **Vault permissions/access control lists (ACLs)**: If a document or asset in PromoMats is restricted (for example, to certain groups, regions, or roles), the connector respects those permissions so that only authorized users can see it.
- **User identity mapping**: The connector requires that PromoMats user identities map to the organization's Microsoft Entra ID identities. If the identities don't automatically match, admins can configure custom user mappings to ensure that access permissions are enforced.
- **Visible to everyone option**: In scenarios where content is nonconfidential and open for all, the connector admin can choose to relax per-user restrictions and index content as **visible to all**.
- **Access-change latency**: Changes to permissions in PromoMats might not instantly reflect in the index; if a permission is revoked, there can be a delay until the next full crawl.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Veeva PromoMats connector](veeva-promomats-deployment.md)
