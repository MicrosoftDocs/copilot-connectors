---
title: "GitLab Issues Cloud connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 01/20/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the GitLab Issues Cloud Microsoft 365 Copilot connector."
---

# GitLab Issues Cloud connector overview

The GitLab Issues Cloud Microsoft 365 Copilot connector allows your organization to index issue data stored in GitLab.com and make that information available in Microsoft 365 Copilot and Microsoft Search. GitLab issues represent work items used to plan, track, and coordinate development, project, and operational tasks. By bringing GitLab issue data into Microsoft 365, teams can retrieve issue details, discussions, assignments, and context without leaving their Microsoft 365 workflows.

## Why use the GitLab Issues Cloud connector to index your data?

Organizations use the GitLab Issues Cloud connector to improve visibility into development and project workflows and to reduce context switching across tools. Common scenarios include:

- Enable developers to quickly find GitLab issue details, discussions, and assignments directly in Microsoft Teams or Outlook.
- Allow project managers and engineering leads to track milestones, priorities, and blockers using Copilot summaries.
- Support IT, site reliability engineering (SRE), and support teams by retrieving historical issues during incident investigation and troubleshooting.
- Help engineering managers and leadership gain visibility into issue trends, risks, and overall project health.
- Improve cross-functional collaboration by making GitLab issues discoverable through Microsoft Search.

## Build agents with the GitLab Issues Cloud connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that agent builders can use to help their users retrieve information from GitLab Issues Cloud:

| Role | Example prompt |
|------|----------------|
| Developer | Show me all open GitLab issues assigned to me in the last seven days. |
| Project manager | Summarize high-priority GitLab issues for the current release milestone. |
| Support agent | Find GitLab issues related to API error code 500 and summarize their resolutions. |
| Engineering manager | Give me a summary of blocked GitLab issues and their owners. |
| SRE / Ops | List recent GitLab issues related to production incidents and outages. |

## GitLab Issues Cloud connector capabilities and limitations

The GitLab Issues Cloud connector allows users to:

- Index GitLab issues for retrieval in Microsoft Search and Microsoft 365 Copilot.
- Perform natural language queries over issue details, metadata, labels, and timelines.
- Maintain GitLab access control lists (ACLs) and user permissions when serving search and Copilot responses.
- Customize crawl frequency and indexing preferences.

The connector has the following limitations:

- Banning users isn't supported as a permission rule. As a workaround, remove users from groups.
- Restricting group access by IP address isn't supported. Create private groups instead.
- Due to stability considerations found during testing, Planner role support is deprecated. Access is limited to Reporter roles and higher.

## Data types indexed from GitLab Issues Cloud

The connector indexes issue data stored in GitLab.com, including:

- Issue titles, descriptions, and comments
- Labels, milestones, and priorities
- Timestamps, authors, and assignees
- Metadata such as issue state, related merge requests, and associated repositories

Indexed data is surfaced through Microsoft Search and is available to Copilot experiences that your organization enables.

## Permissions model and access control

The connector respects GitLab ACLs. Only users with access to issues in GitLab see those issues in their Microsoft 365 search results or Copilot responses unless the admin chooses to make indexed data visible to everyone. Identity mapping between GitLab and Microsoft Entra ID can be configured using email, sign in, or name attributes, with optional regex transformation.

## Next step

> [!div class="nextstepaction"]
> [Deploy the GitLab Issues Cloud connector](gitlab-issues-cloud-deployment.md)
