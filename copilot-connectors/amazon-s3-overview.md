---
title: "Amazon S3 Microsoft 365 Copilot connector (preview)"
description: "Learn about the Amazon S3 connector for Microsoft 365 Copilot, including its benefits, use cases, capabilities, and limitations."
ms.author: lauragra
author: Kai-Cloud
manager: zezhangzhao
ms.topic: overview
ms.service: copilot-connectors
ms.localizationpriority: medium
ms.date: 12/02/2025
---

# Amazon S3 Microsoft 365 Copilot connector

The Amazon S3 Microsoft 365 Copilot connector integrates content from Amazon S3 buckets into Microsoft 365. It enables Microsoft 365 Copilot, Copilot Search, and Microsoft Search to surface relevant files directly within apps like Microsoft Teams, Outlook, and SharePoint.

After you configure the connector and index data from your Amazon S3 buckets, users can search for S3 content in Microsoft 365 Copilot, Copilot Search, and Microsoft Search. This integration helps improve operational efficiency, accelerate response times, and enhance collaboration across your organization.

[!INCLUDE [conector-preview-access](includes/connector-preview-access.md)]

## Why use the Amazon S3 connector to index your data?

Organizations that store documents and files in Amazon S3 often face challenges accessing and using the content efficiently. The Amazon S3 connector solves this problem by integrating S3 content into Microsoft 365, allowing employees to discover and use S3 files without leaving their flow of work.

The Amazon S3 connector provides the following benefits:

- **Boosts productivity** – Employees access S3 content directly within Microsoft 365 apps, reducing time spent switching platforms.
- **Improves decision-making** – Unified search across S3 and Microsoft tools ensures faster access to institutional knowledge.
- **Accelerates request fulfillment** – Support and operations teams resolve issues faster by retrieving documentation instantly via Copilot.
- **Enhances collaboration** – Cross-functional teams discover and reuse each other’s S3 content, reducing duplication and improving alignment.
- **Preserves security and compliance** – The connector respects configured permissions to ensure sensitive content is only visible to authorized users.

### Use cases

The following table lists common use cases for the Amazon S3 connector.

| Department/role     | Use case                                                       | Business benefit                                |
|---------------------|----------------------------------------------------------------|--------------------------------------------------|
| People / HR         | Summarize onboarding guides stored in S3                       | Faster onboarding, reduced dependency on HR staff |
| Sales / Marketing   | Access sales figures and reports from S3                       | Better decision-making and planning              |
| Executives / Managers | Get a high-level summary of project reports                  | Faster decision-making and improved visibility   |

## Build agents with the Amazon S3 connector

Developers can use this connector as a knowledge source in declarative agents built with:

- [Microsoft Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio)
- [Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/agent-builder)
- [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit)

### Eaxmple prompts

**People/HR**

- Summarize the onboarding documents for new hires stored in the HR S3 bucket, including links to the files.
- What are the latest updates to the remote work policy stored in Amazon S3?

**Sales/marketing**

- Summarize the messaging framework for the Contoso campaign stored in S3 and include links to related case studies.
- What are the key takeaways from the last marketing strategy documents in the S3 marketing bucket?

**Executives/managers**

- Summarize the latest project update reports across all teams stored in S3.
- What are the documented risks and mitigation plans for the upcoming launch in the S3 strategy folder?

## Amazon S3 connector capabilities and limitations

The Amazon S3 connector has the following key capabilities:

- **Indexes S3 content** – Crawls and indexes objects (documents, files) stored in Amazon S3 buckets.
- **Integrates with Copilot** – Enables natural language queries in Copilot and Microsoft Search that return relevant S3 content with reference links.
- **Supported file types** – Microsoft Office files, OpenDocument files, text-based files, PDFs, email files, images, and ZIP archives.

The Amazon S3 connector has the following limitations:

- **Bucket type restriction** – Only indexes files in general-purpose buckets.
- **Storage class limitation** – Doesn’t index files in Glacier Flexible Retrieval or Glacier Deep Archive.
- **File size limitation** – Only metadata is indexed for files larger than 20 MB.
- **Versioning** – Only the latest version of objects is indexed.
- **Restricted file types** – Audio, video, and other unsupported formats only have metadata indexed.

## Data types indexed from Amazon S3

The Amazon S3 connector indexes the following content types by default.

| S3 content type     | Indexed and surfaced in Copilot and search                     |
|---------------------|----------------------------------------------------------------|
| Documents and files | Full text indexed for supported file types; metadata indexed for large or restricted files. |

## Permissions model and access control

Due to current API **restrictions**, the Amazon S3 connector only supports the **visible to everyone** permission. All content indexed by the connector is visible to Microsoft 365 users.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Amazon S3 connector](amazon-s3-deployment.md)
