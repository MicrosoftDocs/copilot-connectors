---
title: "Azure File Share connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 12/15/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Azure File Share Microsoft 365 Copilot connector."
---

# Azure File Share connector overview

The Azure File Share Microsoft 365 Copilot connector integrates Azure File Share content into Microsoft 365, allowing Microsoft 365 Copilot and Microsoft Search experiences to surface relevant files and folders directly in apps like Teams, Outlook, and SharePoint. When you configure the connector and index content from your file shares, users can search enterprise file-share data in Microsoft 365 without switching between tools. The connector brings more consistent information management and improved discovery, and preserves New Technology File System (NTFS)-based security trimming.

## Why use the Azure File Share connector to index your data?

Organizations commonly use Azure File Share to store project documents, shared drives, operational content, financial workbooks, contracts, and archives. Because these shares often sit outside the day-to-day collaboration experience, users struggle to find the latest version or navigate complex Universal Naming Convention (UNC) paths. This fragmentation creates duplicate content, inconsistent access, and slower decision-making.

The Azure File Share connector addresses these challenges by integrating file-share content directly into Microsoft 365 so that users can access it through Copilot, Copilot Search, and Microsoft Search without leaving their flow of work. This unified search experience reduces context switching and helps standardize how teams discover and use shared content while continuing to respect NTFS permissions.

The Azure File Share connector provides the following benefits:

- **Boosts productivity**: Employees access Azure File Share documents directly within Microsoft 365 apps, reducing time spent navigating UNC paths or switching tools.
- **Improves decision-making**: Unified search across Azure File Share and Microsoft 365 enables faster access to project plans, operating documents, and financial models.
- **Accelerates request fulfillment**: IT or support teams retrieve procedures, runbooks, and reference documents faster through natural language queries in Copilot.
- **Enhances collaboration**: Teams discover reusable templates, contracts, reports, and archives, reducing duplicate content across the organization.
- **Supports content migration**: Unified search helps identify what to migrate, archive, or retire as organizations modernize legacy file shares.
- **Preserves security and compliance**: NTFS permission trimming ensures users see only the files and folders they’re authorized to access.

The following table lists common use cases for the Azure File Share connector.

| **Department or role** | **Use case** | **Business benefit** |
|------------------------|--------------|-----------------------|
| Project teams/PMO | Search project folders for timelines, RAID logs, and status decks via Copilot. | Faster project reporting. |
| Finance | Retrieve budget workbooks, monthly close binders, and audit schedules. | Improved financial visibility. |
| Legal/procurement | Locate standard templates and executed agreements. | More consistent contracting. |
| IT/infrastructure | Find runbooks, change records, and configuration docs. | Faster incident response. |
| HR/people teams | Access policy documents, forms, and archives. | Easier policy discovery. |
| Executives/managers | Ask Copilot to summarize key reports or slide decks. | Faster decision-making. |

## Build agents with the Azure File Share connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit). Once Azure File Share content is indexed into Microsoft Graph, agents can perform semantic search, summarization, comparisons, and content generation across file-share content.

### Example prompts

The following examples show prompts that agent builders can use to help their users retrieve information from Azure File Share:

**IT/operations**

- Summarize the latest change management runbook from the IT operations share, highlighting prerequisites and rollback steps.
- Find all incident response procedures for a specific system outage and summarize recommended troubleshooting flows.

**Project management/PMO**

- List the most recent project plans and status reports for a migration initiative and summarize deadlines and risks.
- Summarize a RAID log and surface links to related spreadsheets or slide decks stored on the project share.

**Finance**

- Retrieve the latest quarterly forecast workbook and summarize major variances.
- Find all Excel files that reference specific budget assumptions and summarize the differences.

**Legal/procurement**

- List templates on the legal share and summarize key differences.
- Summarize executed agreements for a supplier, including renewal and termination clauses.

**HR/people teams**

- Summarize current remote work and travel policy documents.
- Identify historical versions of the code of conduct and summarize major changes.

**Executives/managers**

- Summarize monthly business-unit performance reports stored on the executive share.
- Find all slide decks matching a keyword and summarize key decisions.

## Azure File Share connector capabilities and limitations

The Azure File Share connector enables users to:

- Perform natural language queries over Azure File Share content within Microsoft Search and Copilot.
- Access content securely because the connector integrates NTFS permissions with Microsoft Entra ID through the Microsoft Graph Connector Agent.
- Benefit from regular full crawls (daily by default) that keep indexed content up to date.
- Retrieve semantic results across file content, metadata, directory structure, and NTFS access control lists (ACLs).

The Azure File Share connector has the following limitations:

- Files up to 100 MB are indexed, with up to 4 MB of text extracted.
- Supported file formats include Microsoft Office files, PDFs, text files, and JSON files; nontext formats (such as images and videos) are excluded.
- Files the connector agent account can't read aren't indexed or displayed.
- Crawl performance can vary based on content type, file size, and network conditions. For more information, see [Understand and optimize Azure file share performance](/azure/storage/files/understand-performance). 

## Data types indexed from Azure File Share

The following table describes the data types that the connector indexes.

| **Azure File Share content type** | **Indexed and surfaced in Copilot and search** |
|----------------------------------|-------------------------------------------------|
| Microsoft Office documents | Word, Excel, PowerPoint, and other Office files. Content and metadata (file name, path, owner, last modified) are indexed. |
| PDFs | Text content (up to 4 MB) and key properties are indexed. |
| Text files | Plain-text content such as logs, configuration notes, and README files is indexed and can be summarized. |
| JSON files | Structured JSON content is indexed and searchable. |

## Permissions model and access control

You can configure the Azure File Share connector so that only users who have access to a file or folder in Azure File Share can see it in Copilot or Microsoft Search. The connector enforces NTFS ACLs combined with Microsoft Entra ID identities as the source of truth.

- **NTFS permissions**: The connector reads NTFS ACLs on files and folders and enforces those permissions in Microsoft 365.
- **User identity mapping**: The Graph Connector Agent uses Windows authentication to map user access; you should align file-share permissions with Microsoft Entra ID identities.
- **Visible to everyone option**: Admins can broaden access, but retaining NTFS-based permission trimming is recommended for most scenarios.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Azure File Share connector](azure-file-share-deployment.md)