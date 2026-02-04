---
title: "GitLab Merge Requests Cloud Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 01/30/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the GitLab Merge Requests Cloud Microsoft 365 Copilot connector."
---

# GitLab Merge Requests Cloud Microsoft 365 Copilot connector overview

The GitLab Merge Requests Cloud Microsoft 365 Copilot connector allows your organization to index merge requests from GitLab projects hosted on GitLab.com and make them discoverable across Microsoft 365 Copilot and Microsoft Search. It surfaces key merge request information—such as review status, approvals, CI results, and discussions—so developers and stakeholders can retrieve and act on this context directly in Microsoft 365.

## Why use the GitLab Merge Requests Cloud connector to index your data?

Use this connector to unlock GitLab merge request data where your teams already collaborate. Common scenarios include: 

- Empower developers and project managers to quickly find, review, and track merge requests across GitLab projects.
- Enable engineering leaders and stakeholders to monitor code review progress, merge readiness, and development status.
- Support compliance and audit teams with visibility into merge activity, approvals, and change history.
- Facilitate knowledge sharing and collaboration by making merge request information accessible through Microsoft 365 Copilot and Microsoft Search.

## Build agents with the GitLab Merge Requests Cloud connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Agent prompts

The following examples show prompts that agent builders can use to help users retrieve information from GitLab Merge Requests Cloud: 

- **Engineering:**
  - Show all open merge requests for the Contoso Payments project.
  - List merge requests merged in the last 30 days.
  - Find merge requests assigned to me. 
- **Quality assurance:**
  - Which merge requests are pending review in the organization? 
  - List merge requests that require QA approval. 
- **Compliance and audit:**
  - Summarize the status of merge requests for the Fabrikam/Inventory project.
  - List merge requests merged in the last 30 days for audit purposes. 

## GitLab Merge Requests Cloud connector capabilities and limitations

The GitLab Merge Requests Cloud connector enables users to: 

- Perform natural language queries in Copilot to locate merge requests by title, labels, status, and assignees.
- Review merge request context such as approvals, CI pipeline results, and threaded discussions without switching tools. 
- Monitor merge readiness and track review progress across multiple projects. 

The GitLab Merge Requests Cloud connector has the following limitations:  

- Ingestion throughput and freshness are subject to GitLab API rate limits and environment load. 
- Deployment requires a GitLab OAuth 2.0 application with the **read_api**, **read_repository**, and **read_user** scopes. 

## Data types indexed from GitLab Merge Requests Cloud

The connector indexes the following data types and surfaces them in Copilot and Microsoft Search. The following table lists the core types and how they appear in experiences. 

| Data type | Examples of properties | How it appears in Copilot and search |
|---|---|---|
| Merge requests | Title, description, author, assignees, reviewers, labels, timestamps | Copilot and search results reference the merge request with key metadata to support review and follow‑up. |
| Approvals and reviewers | Required approvals, approvers, approval status | Responses can summarize who approved and what remains to be approved.  |
| CI pipelines and status | Pipeline status, latest run, checks | Copilot can report whether the merge request has passing checks and highlight blocking failures.  |
| Comments and discussions | Threads, participants, timestamps | Responses can include relevant discussion context to assist decision‑making. |
| Labels and metadata | Labels, project, repository, web URL | Used as facets and refiners in search and to ground Copilot answers. |

## Permissions model and access control

Visibility of indexed content respects your configuration in the Microsoft 365 admin center: you can scope results to **Only people with access to this data source** (default) or make them visible to **Everyone**. Identity mapping aligns GitLab identities to Microsoft Entra ID using email, sign in, or name; if direct mapping fails, you can apply regex-based transforms. For more information, see [Map Microsoft Entra identities](/microsoft-365-copilot/connectors/map-aad).

## Next step

> [!div class="nextstepaction"]  
> [Deploy the GitLab Merge Requests Cloud connector](gitlab-merge-requests-cloud-deployment.md)