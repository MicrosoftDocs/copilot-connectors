---
ms.date: 03/30/2026
title: "SharePoint Server Copilot connector overview"
ms.author: misvenso
author: antarikshp
manager: harshkum
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Learn about the capabilities, limitations, and use cases for the SharePoint Server Copilot connector."
---

# SharePoint Server Copilot connector overview

The SharePoint Server Microsoft 365 Copilot connector allows users in your organization to search for content stored in an on-premises SharePoint Server farm or use the content in Copilot for specific use cases and scenarios. It crawls documents and site pages from SharePoint on-premises farms. On-premises versions of SharePoint Server 2016, 2019, and Subscription Edition (SPSE) are supported.

When you configure the SharePoint Server connector for your organization and index data from SharePoint on-premises, users can search for SharePoint content in Microsoft Search and Microsoft 365 Copilot.

> [!NOTE]
> Active Directory synchronization is a prerequisite for enabling security trimming in SharePoint Server content search. For more information, see [Microsoft Entra Connect Sync: Understand and customize synchronization](/entra/identity/hybrid/connect/how-to-connect-sync-whatis).

[!INCLUDE [conector-preview-access](includes/connector-preview-access.md)]

## Why use the SharePoint Server connector to index your data?

Organizations that use SharePoint Server on-premises for document management and collaboration often have valuable knowledge that isn't accessible through Microsoft 365 experiences. The SharePoint Server Copilot connector bridges this gap by integrating on-premises SharePoint content into Microsoft 365, allowing employees to surface documents and pages through Copilot and Microsoft Search—in everyday apps like Teams, Outlook, or SharePoint—without leaving their flow of work.

The SharePoint Server Copilot connector provides the following benefits:

- **Boosts productivity** - Employees access on-premises SharePoint content directly within Microsoft 365 apps, reducing time spent searching and switching platforms.
- **Improves decision-making** - Unified search across on-premises SharePoint and Microsoft 365 tools ensures faster access to institutional knowledge, enabling more informed and timely decisions.
- **Enables Copilot over on-premises content** - Users can ask Copilot questions about, summarize, or create content from documents stored in SharePoint Server.
- **Preserves security and compliance** - The connector respects SharePoint Server permissions to ensure that content is only visible to authorized users.

### Use cases

The following table lists common use cases for the SharePoint Server connector.

| Department/role | Use case | Business benefit |
| --------------- | -------- | ---------------- |
| All employees | Search for on-premises documents from Microsoft 365 | Reduced context switching, faster access to content. |
| IT support/help desk | Retrieve runbooks and guides stored in SharePoint Server | Faster ticket resolution. |
| Legal/compliance | Access policy documents and compliance content | Improved governance and auditability. |
| HR/People | Summarize onboarding materials and policies stored in SharePoint | Faster onboarding, reduced dependency on HR staff. |
| Engineering/DevOps | Query design docs and technical guides stored on-premises | Faster execution, reduced duplication. |

## Build agents with the SharePoint Server connector

Developers can use this connector as a knowledge source in declarative agents they build with [Microsoft Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

> [!NOTE]
> Creating a declarative agent for SharePoint on-premises currently requires using Visual Studio Code and a manually authored [declarative agent manifest](/microsoft-365/copilot/extensibility/declarative-agent-manifest-1.6). Creating custom engine agents in Microsoft Copilot Studio using the SharePoint on-premises connector content is not supported.

### Example prompts

The following examples show prompts that agent builders can use to help their users retrieve information from SharePoint Server. Prompts progress from simple content search to complex reasoning and metadata-based filtering.

**People/HR**

- What are the steps for an employee to submit a Family and Medical Leave Act (FMLA) request?
- Show me all HR policy documents revised by the compensation team in Q1 2026.
- Based on the collective bargaining agreement and overtime policy documents on the HR site, what are the rules for scheduling weekend shifts for unionized hourly employees at the Chicago plant?

**IT Support/Help desk**

- What are the steps to provision access to the SAP ERP system for a new employee?
- Find all security hardening procedure documents updated by the infrastructure team after the February 2026 security audit.
- Based on the ITIL change management procedures and post-implementation review reports stored in SharePoint, which change categories require CAB approval and what issues were documented in reviews from last quarter?

**Engineering/DevOps**

- What does the standard operating procedure say about line changeover on the packaging line?
- Find all quality procedure documents updated by the process engineering team following the ISO 9001 surveillance audit in Q4 2025.
- Based on the process control plan documents and internal audit findings reports in SharePoint, which production steps were flagged as non-conforming in the last quality review and what corrective procedures are specified?

**Product management**

- What regulatory clearances are required for the Model X device listed in the product dossier?
- Find all design verification test reports and validation protocols updated by the regulatory affairs team since the design freeze in February 2026.
- Based on the risk management file and design history file stored in SharePoint, which product hazards have been classified as unacceptable under ISO 14971, and what risk control measures are documented to bring them within acceptable limits?

**Legal/Compliance**

- What does our SOX compliance policy say about segregation of duties for financial system access?
- Find all regulatory examination response documents filed by the compliance team since the Q3 2025 FINRA audit.
- Based on the regulatory examination findings report and the corrective action plan documents in SharePoint, what specific commitments were made to the regulator in the 2025 FINRA examination and what evidence of completion has been documented?

**Executives/managers**

- What does the board-approved risk appetite statement say about our tolerance for cybersecurity incidents?
- Find all capital investment proposals reviewed by the steering committee in H1 2026.
- Based on the divisional business review presentations and quarterly management reports stored in SharePoint, which business units are reporting the largest variance against their annual plan and what recovery actions have been committed to in their latest executive reviews?

## Connector capabilities and limitations

The SharePoint Server connector has the following key capabilities:

- **Indexes documents and web pages** – Crawls SharePoint documents and site pages along with permissions.
- **Respects SharePoint permissions** – Users who don't have permission to crawled items can't find those items in their Search or Copilot results.
- **Configurable content scope** – Lists all available site collections that an admin can choose to include for indexing. Includes an exclusion feature to exclude certain sites from indexing.
- **Integrates with Copilot** – Enables users to utilize connector content for Copilot queries and prompts.

The SharePoint Server connector has the following limitations:

- **Supports documents and web pages only** – The connector only supports indexing documents and web pages.
- **Site-level exclusions only** – Exclusion rules exclude only the specified sites. They can't be used to exclude certain lists, libraries, or content types inside a site.
- **No staged rollout** – [Staged rollout](staged-rollout.md) is not supported in SharePoint on-premises connections.
- **Declarative agent limitations** – Creating a declarative agent for SharePoint on-premises currently requires using Visual Studio Code and a manually authored [declarative agent manifest](/microsoft-365/copilot/extensibility/declarative-agent-manifest-1.6).
- **No custom engine agent support** – Creating custom engine agents in Microsoft Copilot Studio using the SharePoint on-premises connector content is not supported.

## Permissions model and access control

You can configure the SharePoint Server connector to enforce that only users who have access to a SharePoint item can see it in Copilot responses and search results. The connector supports the existing Access Control List (ACL) on given items.

The SharePoint on-premises connector supports the following permission options:

- **Only people with access to the content in the data source (recommended)** – Indexed data appears in the search results and is visible only to users who have permission to view it in SharePoint. Microsoft 365 experiences understand and honor Entra ID permissions. To support Access Control Lists on items, Active Directory identities and Entra ID identities must be synced.
- **Everyone** – The connection is open to everyone, and any user in your organization can see the content.

> [!NOTE]
> Copilot connectors support Users, Security Groups, and Distribution Lists. However, SharePoint Server does not support Distribution Lists as Access Control Lists. If there are nested distribution lists, members of those distribution lists may also get access to content through Graph connectors.

## Next step

> [!div class="nextstepaction"]
> [Set up the SharePoint Server service for connector ingestion](sharepoint-server-admin-setup.md)
