---
title: "Veeva QualityDocs Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: overview
ms.service: copilot-connectors
ms.localizationpriority: Medium
description: "Learn about the Veeva QualityDocs Microsoft 365 Copilot connector, including capabilities, use cases, and benefits for quality, regulatory, manufacturing, and supply-chain teams."
ms.date: 03/18/2026
---

# Veeva QualityDocs Microsoft 365 Copilot connector overview

The Veeva QualityDocs Microsoft 365 Copilot connector integrates Veeva QualityDocs content into Microsoft 365, allowing Microsoft 365 Copilot and Microsoft Search to surface relevant SOPs, work instructions, policies, CAPAs, batch records, and other GxP documents directly within apps like Teams, Outlook, and SharePoint. By pairing Microsoft's AI capabilities with QualityDocs as the single source of truth for controlled quality documents, the connector improves audit readiness, reduces cycle times for changes, and supports more consistent, compliant documentation practices across quality, regulatory, manufacturing, and supply-chain teams.

## Why use the Veeva QualityDocs connector to index your data?

Organizations in life sciences and other regulated industries rely on Veeva QualityDocs as the central repository for SOPs, work instructions, policies, batch records, and quality agreements. However, this controlled content often lives in a separate system from day-to-day collaboration tools, leading to fragmented search experiences, duplicated procedures, and extra effort to prepare audits and inspections. The Veeva QualityDocs Copilot connector addresses these problems by integrating QualityDocs content into Microsoft 365. This integration allows employees to surface controlled quality documents through Copilot and Microsoft Search—in everyday apps like Teams, Outlook, or SharePoint—without leaving their flow of work. The result is a more connected quality knowledge ecosystem that supports compliance while driving productivity and collaboration.

### Key benefits

The Veeva QualityDocs Copilot connector provides the following benefits:

- Boosts quality and operations productivity. Teams can find and summarize SOPs, work instructions, policies, CAPAs, and batch records, instead of manually navigating folders and multiple systems.
- Improves audit and inspection readiness. Copilot can reason over indexed QualityDocs content to highlight gaps, compare versions, and help draft responses to regulatory queries, improving right-first-time outcomes.
- Accelerates document authoring and review. Automated summarization, grammar and clarity checks, and terminology suggestions based on existing procedures help authors and reviewers iterate faster while maintaining GxP compliance.
- Enhances cross-functional collaboration. Quality, manufacturing, regulatory, and supply-chain teams all reference the same controlled documents directly from Microsoft 365, reducing duplication and misalignment between systems.
- Strengthens training and change management. Training and Learning and Development teams can build role-based training materials from up-to-date SOPs and work instructions in QualityDocs, helping to ensure that staff are trained on the latest approved versions.
- Preserves security and compliance. The connector respects the QualityDocs granular permission model and ACLs, ensuring that sensitive quality content is only visible to authorized users.

### Use cases

The following table lists common use cases for the Veeva QualityDocs connector.

| Department/role           | Use case    | Business benefit |
|---------------------------|--------------------------------|--------------------------------|
| Quality Assurance (QA)    | Summarize recently revised SOPs, work instructions, or CAPA procedures.  | Faster understanding of changes, better deviation and CAPA handling. |
| Manufacturing/Operations  | Retrieve step-by-step work instructions and batch records for a product or line. | Reduced downtime, more consistent execution on the shop floor. |
| Regulatory Affairs        | Identify procedures referencing specific regulations (for example, ICH Q9 or 21 CFR Part 211). | Improved regulatory readiness and easier inspection preparation. |
| Quality Control/Labs    | Find testing procedures, sampling instructions, or lab-related SOPs linked to a product or method. | Faster access to controlled methods; fewer errors in lab execution. |
| Training/L&D            | Generate role-based training outlines from SOPs, policies, and WIs stored in QualityDocs. | Reduced training-development time; training aligned to controlled docs. |
| Supply chain/Site quality | Summarize global vs. local procedures affecting suppliers and external manufacturers. | Clearer hand-offs, better control over outsourced activities. |
| Executives/managers       | Ask Copilot for summaries of key quality procedures, recent revisions, or audit-relevant changes. | Faster decision-making and oversight of quality-system health. |

## Build agents with the Veeva QualityDocs connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Eaxmple prompts

Agent builders can use the following prompts to help users retrieve and reason over information from Veeva QualityDocs:

- Summarize the key changes in the most recently revised cleaning validation SOP in Veeva QualityDocs and highlight the impact on the packaging line.
- Based on recent audit observations, suggest updates to our deviation management procedure using related CAPA and deviation SOPs stored in QualityDocs.
- Summarize the work instructions and critical steps for the tablet compression process from the latest approved procedures in QualityDocs.
- Identify all batch record templates for Product X and summarize the key differences between the global procedure and site-specific variants.
- List procedures in Veeva QualityDocs that reference ICH Q9 or 21 CFR Part 211 and summarize their main controls.
- Draft an initial response to a regulatory inspection query using relevant SOPs and policies stored in QualityDocs.
- Prepare a role-based training presentation for new QA associates using related policies, SOPs, and work instructions from Veeva QualityDocs.
- Generate an updated training module that explains the latest change-control procedure, drawing on the most recent SOP revision in QualityDocs.
- Identify procedures that govern supplier qualification and quality agreements, and summarize key obligations for external manufacturers.
- Summarize the key differences between the global product-release procedure and a local site procedure that is stored in QualityDocs.
- Summarize the top 10 quality procedures most recently revised in Veeva QualityDocs and highlight any themes that might affect audit readiness.
- Identify patterns where required regulatory phrases are missing or inconsistent across SOPs, and suggest areas for continuous improvement.

## Connector capabilities and limitations

The Veeva QualityDocs connector has the following key capabilities:

- Quickly understand SOPs, work instructions, policies, CAPAs, and batch records by generating AI-powered summaries to support quality and regulatory actions.
- Use semantic search, filters, and suggested queries to make QualityDocs content easier to discover across Teams, Outlook, and SharePoint.
- Surface patterns such as repeated terminology or missing required phrases in procedures, supporting continuous improvement and standardization.
- Access QualityDocs content alongside emails, Teams chats, and SharePoint files, giving users a more complete view of quality information when using Copilot.
- Automatically enforce ACLs and document-level permissions, reducing the risk of misconfigured access and accidental exposure of controlled documents.
- Include only relevant documents using query-string conditions, enabling targeted and efficient indexing.

The connector has the following limitations:

- Supported file types are primarily text-based (Microsoft 365 documents, PDFs); nontext files such as .png, .jpg, or video files aren't supported.
- Each document can include up to 4 MB of parsed (extracted) text for ingestion and indexing. In most .docx, .pptx, and .pdf files, the extracted text represents roughly 10% of the original file size, which allows many documents of 30–40 MB to be fully indexed. For other file types, this ratio might differ. If the extracted text exceeds the 4 MB limit, only the first portion is indexed, which might result in partial coverage and incomplete answers in Copilot and Search.
- The indexing speed is constrained by the API rate limits imposed by the Veeva platform. If you have a high volume of documents, you might experience longer completion times. 
- Document fields set to be hidden on the Veeva platform aren't indexed.

## Data types indexed from QualityDocs

The Veeva QualityDocs connector indexes key quality and manufacturing content types so they can be used in Copilot and Microsoft Search. It pulls both document content and rich metadata (such as lifecycle, owning facility, product, reference-model category, and review frequency) to enable precise filtering and retrieval.

## Permissions model and access control

You can configure the Veeva QualityDocs connector to ensure that only users who have access to a QualityDocs item can see it in Copilot responses and search results. The system uses the Veeva QualityDocs access control list (ACL) and document-level permissions as the source of truth.

- Veeva Vault permissions and document-level controls: The connector adheres to the ACLs defined in Veeva QualityDocs. Only users with view permissions in QualityDocs can see the indexed content in Microsoft 365. Admins can optionally allow all users access to all indexed content, although this approach isn’t recommended for regulated repositories.
- User identity mapping: The connector relies on mapping Veeva QualityDocs user identities (for example, Federated ID) to Microsoft Entra ID user accounts. Make sure that the Microsoft Entra UPN matches the Federated ID used in QualityDocs, or configure custom identity mapping so security permissions can be enforced.
- Visible to everyone option: In Microsoft 365 admin center, you can choose whether indexed data is visible only to people with access to the data source (recommended for GxP content) or visible to everyone in the tenant. For QualityDocs, we recommend using the ACL-based mode to maintain compliance.
- Sync and permission update behavior: By default, the connector runs daily full crawls, during which it refreshes both content and permissions. Changes to groups or permissions in Veeva Vault might not appear immediately in search and are typically reflected after the next full crawl. There can be a short delay before new access settings are fully enforced in Copilot experiences.


## Next step

> [!div class="nextstepaction"]
> [Deploy the Veeva QualityDocs connector](veeva-qualitydocs-deployment.md)

