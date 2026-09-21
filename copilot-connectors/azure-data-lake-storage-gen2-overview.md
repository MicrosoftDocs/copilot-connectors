---
title: "Azure Data Lake Storage Gen2 connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: microsoft-365-copilot-connectors
ms.date: 07/22/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Azure Data Lake Storage Gen2 Microsoft 365 Copilot connector."
---

# Azure Data Lake Storage Gen2 connector overview

The Azure Data Lake Storage Gen2 Microsoft 365 Copilot connector indexes files stored in [Azure Blob Storage](/azure/storage/blobs/storage-blobs-introduction) and [Azure Data Lake Gen 2 Storage](/azure/storage/blobs/data-lake-storage-introduction) accounts. Users can discover and query that content through Microsoft 365 Copilot and Microsoft Search without leaving their flow of work. When you configure the connector and index content from your storage accounts, users can search enterprise data lake content in Microsoft 365 without switching between tools.

## Why use the Azure Data Lake Storage Gen2 connector to index your data?

Organizations commonly use Azure Data Lake Storage Gen2 and Azure Blob Storage to store large volumes of unstructured data, including documents, reports, data exports, and archives. Without the connector, users must navigate the Azure portal or Azure Storage Explorer to find content. This fragmentation creates duplicate content, inconsistent access, and slower decision-making.

The Azure Data Lake Storage Gen2 connector addresses these challenges by integrating storage account content directly into Microsoft 365 so that users can access it through Copilot, Copilot Search, and Microsoft Search without leaving their flow of work. The connector also supports ACL-based permission trimming for Azure Data Lake Gen 2 Storage sources, ensuring that users only see content they're authorized to access.

The Azure Data Lake Storage Gen2 connector provides the following benefits:

- **Boosts productivity**: Employees access data lake documents directly within Microsoft 365 apps, reducing time spent navigating the Azure portal or Storage Explorer.
- **Improves decision-making**: Unified search across Azure Storage and Microsoft 365 enables faster access to reports, analyses, and reference documents.
- **Accelerates data discovery**: Data engineering and analytics teams find data exports, documentation, and processing results faster through natural language queries in Copilot.
- **Enhances collaboration**: Teams discover reusable reports, templates, and archives, reducing duplicate content across the organization.
- **Preserves security and compliance**: ACL-based permission trimming for Azure Data Lake Gen 2 Storage ensures users see only the files they're authorized to access.

The following table lists common use cases for the Azure Data Lake Storage Gen2 connector.

| **Department or role** | **Use case** | **Business benefit** |
|------------------------|--------------|-----------------------|
| Data engineering | Search data lake folders for pipeline documentation, schema definitions, and processing logs. | Faster data pipeline troubleshooting. |
| Finance | Retrieve budget exports, monthly close reports, and audit schedules from storage containers. | Improved financial visibility. |
| Compliance | Locate compliance audit documents, regulatory filings, and retention records. | More consistent compliance management. |
| IT operations | Find configuration exports, infrastructure documentation, and backup logs. | Faster incident response. |
| Project teams | Access project reports, deliverables, and archived documentation stored in containers. | Easier project document discovery. |
| Executives | Ask Copilot to summarize key reports or data analyses stored in the data lake. | Faster decision-making. |

## Build agents with the Azure Data Lake Storage Gen2 connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit). Once Azure Data Lake Storage Gen2 content is indexed into Microsoft Graph, agents can perform semantic search, summarization, comparisons, and content generation across storage account content.

### Example prompts

The following examples show prompts that agent builders can use to help their users retrieve information from Azure Data Lake Storage Gen2:

- "Find the latest data export report stored in our Azure Data Lake."
- "Summarize the contents of the compliance audit PDF from the finance container."
- "List all Excel files in the analytics folder that were modified this quarter."
- "What are the key findings in the risk assessment document stored in our data lake?"
- "Show me the project documentation stored in the engineering container."

## Azure Data Lake Storage Gen2 connector capabilities and limitations

By using the Azure Data Lake Storage Gen2 connector, you can:

- Perform natural language queries over files stored in Azure Blob Storage and Azure Data Lake Gen2 Storage accounts.
- Index content from supported file types, including Word, PowerPoint, Excel, legacy Office formats, text, HTML, and PDF.
- Enforce access control list (ACL)–based security trimming for Azure Data Lake Gen2 Storage sources.
- Schedule incremental crawls (as frequently as every 15 minutes) and full crawls (weekly by default) to keep content current.
- Configure storage account queue notifications for near-real-time change awareness (optional).

The Azure Data Lake Storage Gen2 connector has the following limitations:

- Files must be 4 MB or less to be crawled.
- Binary files (images, videos) aren't supported.
- You can't reconfigure a published connection for Azure Blob Storage for Azure Data Lake Storage Gen2 (and vice versa); you need a new connection.
- ACL-based permission trimming is only available for Azure Data Lake Gen2 Storage; Azure Blob Storage connections expose all indexed content to everyone in the organization.
- The connector might skip Office files containing only images because no text content is returned.

## Data types indexed from Azure Data Lake Storage Gen2

The following table describes the data types that the connector indexes.

| **Content type** | **Indexed and surfaced in Copilot and search** |
|---|---|
| Word documents (.docx, .docm, .dotx, .dotm, .doc, .dot) | File content and metadata are indexed. |
| PowerPoint (.pptx, .pptm, .potm, .potx, .ppam, .ppsm, .ppsx) | Slide content and metadata are indexed. |
| Excel (.xlsx, .xlsm) | Workbook content and metadata are indexed. |
| PDF | Text content (up to 4 MB) and metadata are indexed. |
| Text files (.txt) | Plain-text content is indexed. |
| HTML | Text content is indexed. |
| Legacy Office formats (.doc, .dot, etc.) | Content and metadata are indexed. |

## Permissions model and access control

You can configure the Azure Data Lake Storage Gen2 connector to control who can see indexed content in Copilot and Microsoft Search.

- **Azure Data Lake Gen 2 Storage:** Admins can ingest access control lists (ACLs) so that search results are trimmed based on the signed-in user's Microsoft Entra ID permissions. Only users with access to an item in the data lake see it in Copilot and Search.
- **Azure Blob Storage:** ACLs aren't supported at the blob level. All indexed content is visible to everyone in the organization.
- Admins choose between **Everyone** and **Only people with access to this data source** during setup.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Azure Data Lake Storage Gen2 connector](azure-data-lake-storage-gen2-deployment.md)
