---
ms.date: 04/22/2026
title: "SharePoint Server connector overview"
ms.author: venk
author: venk
manager: srramam
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Learn about the capabilities, limitations, and use cases for the SharePoint Server Microsoft 365 Copilot connector."
---

# SharePoint Server connector overview

The SharePoint Server Microsoft 365 Copilot connector enables users in your organization to search for and reason over content stored in a SharePoint Server farm across Microsoft Search, Copilot Search, Copilot Chat, and declarative agents. It can crawl documents and site pages from SharePoint Server 2016, 2019, and Subscription Edition (SPSE) farms.

## Why use the SharePoint Server connector to index your data?

Organizations that use SharePoint Server for document management and collaboration often have valuable knowledge that isn't accessible through Microsoft 365 experiences. The SharePoint Server Copilot connector bridges this gap by integrating SharePoint Server content into Microsoft 365. Employees can search for and reason over documents and site pages through Microsoft Search, Copilot Search, and Copilot Chat - without leaving their flow of work.

The SharePoint Server Copilot connector provides the following benefits:

- **Get Copilot on content you've spent years building** — Bring AI-powered search and reasoning to documents and site pages in SharePoint Server - no migration, no rebuilding, no waiting.
- **Employees have questions, not search queries** — Natural language in Copilot Chat surfaces the right SharePoint Server content, even when users don't know what it's called or where it lives.
- **Backed by Microsoft 365's enterprise compliance boundary** — Indexed content is processed within Microsoft's compliance infrastructure - the same environment trusted by regulated industries for Teams, Exchange, and SharePoint Online.
- **Designed for enterprise networks** — The Microsoft Graph connector agent runs inside your network with outbound-only connections to Microsoft 365. No inbound firewall rules, no changes to your security perimeter.

### Use cases

The following table lists common use cases for the SharePoint Server connector.

| Department or role | Use case | Business benefit |
| --------------- | -------- | ---------------- |
| HR | Ask Copilot Chat questions about employee handbooks, leave policies, and benefits guides | Employees self-serve HR answers without calling HR. |
| Legal & compliance | Reason over contract libraries, compliance frameworks, and regulatory filings | Faster contract review, audit prep, and compliance checks. |
| IT operations | Retrieve runbooks, architecture docs, and disaster recovery plans via Copilot Chat | Faster incident response; new staff get up to speed without hunting for docs. |
| Operations & quality | Surface SOPs, work instructions, and quality audit findings at the point of need | Operators find the right procedure faster, reducing errors. |
| Engineering & R&D | Reason over design specs, technical specifications, test reports, and validation protocols | Faster access to technical knowledge; reduced duplication across projects. |
| Finance | Search financial policies, budget templates, and audit prep documents | Faster policy lookup during audits and budget cycles. |
| Executive & leadership | Synthesize strategic plans, board presentations, and business reviews | Surface insights across multiple strategy documents in seconds. |

## Example prompts

The following sample prompts show the type of queries users can issue against the SharePoint Server content in Copilot Chat.

**HR**

- What are the steps for an employee to submit a Family and Medical Leave Act (FMLA) request?
- Which HR policy documents covering compensation and benefits were revised in Q1 2026?
- Draft a manager briefing on the rules for scheduling weekend shifts for unionized hourly employees at the Chicago plant, drawing from the collective bargaining agreement and overtime policy documents.

**Legal & compliance**

- How does our SOX compliance policy define segregation of duties for financial system access?
- Which regulatory examination response documents relate to the Q3 2025 FINRA audit?
- Summarize the commitments made to the regulator in the 2025 FINRA examination and identify what evidence of completion is documented in the corrective action plan.

**IT operations**

- What are the steps to restore service after a database failover on the customer-facing API?
- List all security hardening procedures updated after the February 2026 security audit.
- Analyze the post-implementation review reports from last quarter and summarize recurring issues by change category, highlighting any that should be escalated to the CAB.

**Operations & quality**

- How does the standard operating procedure define the line changeover process on the packaging line?
- Which quality procedure documents were revised following the ISO 9001 surveillance audit in Q4 2025?
- Analyze the internal audit findings against the process control plan and generate a summary of non-conforming production steps with their associated corrective procedures.

**Engineering & R&D**

- What are the operating temperature limits specified in the design specification for the thermal management module?
- List all design verification test reports and validation protocols revised since the design freeze in February 2026.
- Analyze the design history file and verification test reports in SharePoint to identify open verification gaps and draft a remediation status summary by requirement.

**Finance**

- What approval thresholds does our capital expenditure policy require for business unit sign-off?
- Summarize which business units are tracking behind plan based on the quarterly business reviews and budget variance reports in SharePoint, and list any approved cost-reduction commitments.

**Executive & leadership**

- What does the board-approved risk appetite statement say about our tolerance for cybersecurity incidents?
- List all capital investment proposals reviewed by the steering committee in H1 2026.
- Synthesize the divisional business review presentations and quarterly management reports in SharePoint into an executive briefing on performance variances and committed recovery actions.

## Build agents with the SharePoint Server connector

Apart from Copilot Chat, organizations can use this connector as a knowledge source in declarative agents. While there are multiple ways to build declarative agents in Microsoft 365, SharePoint Server is currently only supported through the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit) in Visual Studio Code. The toolkit lets you set up the agent in a few easy steps by authoring a [declarative agent manifest](/microsoft-365/copilot/extensibility/declarative-agent-manifest-1.6).

## Connector capabilities and limitations

The SharePoint Server connector has the following key capabilities:

- **Indexes documents and site pages** – Crawls SharePoint documents and site pages along with permissions.
- **Respects SharePoint permissions** – Users who don't have access to an item in SharePoint can't see it in their Microsoft Search results or Copilot Chat / Declarative Agent responses (subject to how the connection is setup).
- **Configurable content scope** – Lists all available site collections that an admin can choose to include for indexing based on the specified instance URL. Includes an exclusion feature to exclude certain sites from indexing.
- **Works across Microsoft Search, Copilot Search, Copilot Chat, and Declarative Agents** – Connector content is available across Microsoft Search, Copilot Search, Copilot Chat, and Declarative Agents.

The SharePoint Server connector has the following limitations:

- **Supports documents and site pages only** – The connector only supports indexing documents and site pages.
- **Site-level exclusions only** – Exclusion rules exclude only the specified sites. They can't be used to exclude certain lists, libraries, or content types inside a site.
- **No staged rollout** – [Staged rollout](staged-rollout.md) is not supported in SharePoint Server connections.
- **Declarative agent limitations** – SharePoint Server is currently only supported as a knowledge source in declarative agents through the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit) in Visual Studio Code.
- **No custom engine agent support** – Creating custom engine agents in Microsoft Copilot Studio using the SharePoint Server connector content is not supported.

## Item types indexed from SharePoint Server

The SharePoint Server connector indexes the following item types.

| Item type | Description |
|-----------|-------------|
| Documents | Files stored in SharePoint Document Libraries, including Word, Excel, PowerPoint, PDF, and other supported file formats. |
| Site pages | Pages stored in the SharePoint Site Pages library, including wiki pages and modern pages. |

## Access permissions model

The SharePoint Server connector supports two access permission modes that control which users can see indexed content in Copilot Chat, Copilot Search, declarative agents, and Microsoft Search results:

- **Only people with access to the content in the data source (recommended)** – Users see only content they have permission to access in SharePoint. Requires Active Directory identities to be synced with Microsoft Entra ID.
- **Everyone** – All users in your organization can see the indexed content, regardless of their SharePoint permissions.

> [!NOTE]
> SharePoint Server doesn't support distribution lists as access control lists (ACLs) in SharePoint Server. If your SharePoint permissions include groups that contain nested distribution lists, members of those distribution lists might gain unintended access to content through the connector.

## Next step

> [!div class="nextstepaction"]
> [Configure SharePoint Server](sharepoint-server-admin-setup.md)
