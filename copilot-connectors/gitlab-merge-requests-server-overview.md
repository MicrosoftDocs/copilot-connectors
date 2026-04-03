---
title: "GitLab Merge Requests Server connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 01/22/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the GitLab Merge Requests Server Microsoft 365 Copilot connector."
---

# GitLab Merge Requests Server connector overview

The GitLab Merge Requests Server Microsoft 365 Copilot connector integrates merge request data from GitLab Self-Managed (Server) into Microsoft 365. After you configure the connector and index GitLab content, users can discover, summarize, and retrieve merge request information directly from Microsoft Search, Microsoft 365 Copilot, and Copilot Search. This indexing enables engineering teams to quickly access work-in-progress changes, code review insights, release readiness information, and repository activity without leaving Microsoft 365.

## Why use the GitLab Merge Requests Server connector to index your data?

Modern software development teams rely on merge requests in GitLab to manage collaboration, review code changes, and control release quality. However, merge request data is often siloed within GitLab projects and groups, requiring engineers, program managers, DevOps teams, site reliability engineers (SREs), and stakeholders to manually navigate multiple repositories to find relevant information.

The GitLab Merge Requests Server connector addresses this challenge by indexing merge request metadata from your GitLab Self-Managed instance. When the data is indexed, users can search, filter, and summarize merge requests directly within Microsoft 365.

Common use cases include:

- Accelerate code reviews: Surface merge requests by status, label, milestone, assignee, or project.
- Improve release management: Identify merge requests targeting release branches or blocking deployments.
- Support cross-functional collaboration: Enable PMs, support teams, and leadership to track engineering progress without GitLab expertise.
- Reduce context switching: Allow developers and stakeholders to stay within Microsoft 365 while referencing GitLab work.

Users can also ask Copilot natural language questions such as "Which open merge requests are waiting for review in our payments service?" to get grounded, actionable answers with direct links to GitLab.

## Build agents with the GitLab Merge Requests Server connector

Developers can use this connector as a knowledge source in declarative agents built with:
- [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio)
- [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder)
- [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit)

By incorporating GitLab merge request data into agents, developers enable users to:
- Retrieve and summarize merge requests waiting for review.
- Identify merge requests linked to features, milestones, or infrastructure changes.
- Gain visibility into engineering progress during planning and release cycles.

### Example prompts

The following examples show prompts that agent builders can use to help users retrieve information from GitLab Merge Requests Server:

**Engineering**
- What open merge requests are currently waiting for review in the checkout service?
- Summarize draft merge requests created this week for the backend project.
- Which merge requests are assigned to me, and what is their current status?

**DevOps/SRE**
- List merge requests targeting the release branch and summarize their readiness.
- Which merge requests include infrastructure or configuration changes based on labels?
- What merge requests are blocking the upcoming production deployment?

**IT support/Help desk**
- Find merge requests related to internal tooling updates and summarize the expected impact.
- Which merge requests are tracking improvements to the developer environment?

**Product management**
- Summarize merge requests linked to the next milestone across core projects.
- Which open merge requests correspond to features planned for the next release?

**Engineering leadership**
- Provide a summary of high-priority merge requests across teams.
- Which merge requests are open the longest, and who owns them?

## GitLab Merge Requests Server connector capabilities and limitations

The GitLab Merge Requests Server connector enables users to:

- Index merge requests from GitLab repositories, including metadata and contextual information.
- Enable Microsoft Search and Microsoft 365 Copilot to efficiently retrieve and summarize merge request data.
- Maintain GitLab access control lists (ACLs) and user permissions to ensure role-based visibility.
- Allow administrators to customize crawl frequency and indexing preferences for merge request data.

The GitLab Merge Requests Server connector has the following limitations:

- The connector doesn't support indexing GitLab CI/CD pipelines beyond basic status metadata associated with merge requests.
- Code diffs, file-level changes, inline comments, commit messages, and commit-level details aren’t indexed.
- Banning users isn’t supported as a permission rule. As a workaround, remove users from GitLab groups to revoke access.
- Restricting group or project access by IP address isn’t supported. Create private groups or projects to manage access.
- Due to stability issues identified during internal testing, support for the Planner role is deprecated. Access is restricted to Reporter roles and higher.
- For GitLab Server connectors, access to merge requests in public projects with visibility restricted to project members is limited to Reporter roles and higher.

## Data types indexed from GitLab Merge Requests Server

The connector indexes the following GitLab merge request content:

- Merge request titles and descriptions  
- Merge request status (open, closed, merged, draft)  
- Labels and milestones  
- Authors, assignees, and reviewers  
- Timestamps (created, updated, merged)  
- Associated project and group metadata  

Indexed content appears in Microsoft 365 Copilot and Microsoft Search results, allowing users to discover and summarize GitLab merge request information directly within Microsoft 365 apps.

## Permissions model and access control

Administrators can configure access control for indexed GitLab data using Microsoft Entra ID identity mapping.

You can choose one of the following access models:

- **Only people with access to this data source (default):** Search results appear only for users who have access to the GitLab repositories.
- **Everyone:** Indexed GitLab knowledge is visible to all users in Microsoft 365 search results.

Supported identity mapping options include:

- Email  
- Username  
- Name  

If direct mapping fails, administrators can use regular expressions (regex) to transform identity attributes. Email visibility settings and domain inconsistencies in GitLab can affect mapping accuracy.

## Next step

> [!div class="nextstepaction"]
> [Deploy the GitLab Merge Requests Server connector](gitlab-merge-requests-server-deployment.md)
