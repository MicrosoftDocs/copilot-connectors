---
title: "GitHub Cloud Issues connector overview"
description: "Learn about the capabilities, limitations, and use cases for the GitHub Cloud Issues Microsoft 365 Copilot connector."
author: Lauragra
ms.author: lauragra
ms.reviewer: dannyyao
manager: calvind
audience: Admin
ms.audience: Admin
ms.date: 06/02/2026
ms.service: copilot-connectors
ms.topic: concept-article
ms.localizationpriority: Medium
---

# GitHub Cloud Issues connector overview

The GitHub Cloud Issues Microsoft 365 Copilot connector integrates GitHub issue data into Microsoft 365. By using this connector, Copilot, Copilot Search, and Microsoft Search can surface relevant issues directly within apps like Teams, Outlook, and SharePoint.

When you configure the GitHub Cloud Issues connector for your organization and index data from your GitHub.com repositories, users can search and reason over issues in Microsoft Search, Microsoft 365 Copilot, and Copilot Search. This capability helps development teams track work, triage bugs, and understand project status without leaving their flow of work in Microsoft 365.

## Why use the GitHub Cloud Issues connector to index your data?

For many engineering teams, GitHub Issues is the primary system of record for feature requests, bugs, and operational work items. However, this information is often siloed in GitHub, which makes it harder for PMs, engineers, support, and stakeholders to understand what's happening without switching between tools. The GitHub Cloud Issues Copilot connector indexes issues from GitHub.com so that developers, PMs, support staff, and engineering leaders can discover and summarize relevant issues within Microsoft 365. Users can ask natural-language questions - such as "What are the open bugs in the elysia repo?" - and receive grounded, contextual responses with links back to the original issues in GitHub.

The GitHub Cloud Issues connector provides the following benefits:

- **Improves work visibility** – PMs, engineers, and leaders can surface open issues, priorities, and status from within Teams, Outlook, or SharePoint.
- **Accelerates triage and decision-making** – Copilot can group, summarize, and highlight issue trends (for example, recurring production bugs) to support faster, data-driven decisions.
- **Reduces context switching** – Users discover and summarize issues directly in Copilot instead of manually filtering in GitHub.
- **Enhances cross-team collaboration** – Support, ops, and product teams can reference live GitHub issues in their Microsoft 365 conversations, reducing misalignment and duplicate tracking.
- **Strengthens release management** – Engineering leadership can quickly identify release-blocking issues, milestone status, and customer-requested features.
- **Preserves security and compliance** – The connector honors GitHub access controls so that only authorized users see issues from private repos and restricted projects.

### Use cases

The following table lists common use cases for the GitHub Cloud Issues connector. The example prompts are based on real customer query patterns.

| Department/role | Use case | Business benefit |
| --- | --- | --- |
| Engineering | Find the issue about "Error analyzing large collection" in the elysia repo. | Locate the specific bug report instantly so engineers can investigate without searching GitHub manually. |
| Engineering | Show issues about the Gemini API. | Group related bug reports across repos to identify systemic problems. |
| Engineering | Summarize the issue about "Image cannot be displayed in chat". | Compress long issue threads into actionable summaries that engineers can use to scope work. |
| Engineering | Find issues mentioning "no matching distribution found". | Surface install/dependency issues quickly so they can be reproduced and resolved. |
| DevOps/SRE | Find issues with more than 16 comments. | Identify hot, contentious, or high-engagement issues that may need leadership attention. |
| IT support/Help desk | Find the GitHub issue about "Python Backend – Error with Gemini API". | Resolve user tickets faster by surfacing the matching existing issue and its discussion. |
| IT support/Help desk | Find the GitHub closed issue about the example link. | Quickly confirm whether a reported problem has already been resolved. |
| Product management | Find open issues in the elysia repository. | See the current backlog at a glance to prioritize the next milestone. |
| Product management | Summarize issues in milestone swift-chat-4 sorted by creation time. | Prepare milestone reviews without manually exporting from GitHub. |
| Product management | What are the issues with due date 2025-12-20? | Plan around deadlines and identify schedule risks early. |
| Engineering leadership | Find issues closed by afc163 and sort by modification date. | Recognize contributor impact and review recent closures for retrospectives. |
| Engineering leadership | Show issue #38 and all PRs related to it. | Trace work items end-to-end (issue → PR → release) for status reporting. |
| Engineering leadership | Tell me about the issues closed in H1 2025. | Generate period summaries for QBRs and leadership updates. |
| Security/compliance | Find issues that hellohejinyu commented "try Modal?" on. | Trace specific discussion threads for audit or follow-up. |

## Build agents with the GitHub Cloud Issues connector

Developers can use this connector as a knowledge source in declarative agents they build with [Microsoft Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/copilot-studio-agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

By connecting GitHub Issues to these agents, you can build experiences that:

- Answer questions about current issue load and priorities.
- Summarize related issues for a given feature or incident.
- Help teams plan sprints and releases using live issue data.

### Example prompts

The following examples show prompts that agent builders can use to help users retrieve information from GitHub Cloud Issues. The prompts reflect real patterns from customer usage.

**Engineering**

- Find the issue about "Error analyzing large collection".
- Summarize the issue about "Image cannot be displayed in chat".
- Find issues mentioning "Inconsistent Documentation".
- Explain issue #56 in swift-chat.

**DevOps/SRE**

- Find issues with more than 16 comments.
- Show issues with 8 to 9 comments.
- Find issues mentioning "Error importing thinc/numpy dependencies when running `elysia start`".

**IT support/Help desk**

- Find the GitHub issue about "Python Backend – Error with Gemini API".
- Find the GitHub closed issue about the example link.
- Find issue #31 in a repository with description "Python package".

**Product management**

- Find open issues in the elysia repository.
- Summarize issues in milestone swift-chat-4 and sort by creation time.
- What are the issues with due date 2025-12-20?
- Find issues with the milestone "elysia-4".

**Engineering leadership**

- Find issues closed by afc163 and sort by modification date.
- Show issue #38 and all PRs related to it.
- Tell me about the issues closed in H1 2025.
- Summarize and create a document about issues created on September 5, 2025.

**Cross-entity workflows**

- List issues in milestone elysia-10 and their related PRs, and draft an email to summarize it.
- Find all PRs related to issue #31 in the elysia repo and draft a document to summarize it.
- Find issues closed by afc163 and summarize related emails in a doc.

## GitHub Cloud Issues connector capabilities and limitations

The GitHub Cloud Issues connector has the following key capabilities:

- **Indexes GitHub issues** – Crawls issue title, body/description, labels, state (open/closed), assignees, milestones, due dates, and comments from your configured GitHub.com organizations and repositories.
- **Integrates with Copilot** – Enables Copilot, Copilot Search, and Microsoft Search to retrieve and summarize issue data. Users can ask questions in natural language and get grounded answers with citations back to the issue in GitHub.
- **Maintains GitHub access control** – The connector honors GitHub's repository visibility and team permissions, so users only see issues from repositories they have access to in GitHub.
- **Configurable content scope and crawl behavior** – Admins choose which organizations and repositories to include, and can customize crawl frequency and indexing preferences.

The GitHub Cloud Issues connector has the following limitations:

- **GitHub Cloud only** – On-premises or self-hosted GitHub instances aren't supported. Use the [GitHub Server Issues connector](github-server-issues-overview.md) for GitHub Enterprise Server.
- **No CI/CD pipeline indexing** – GitHub Actions and CI/CD pipelines aren't indexed beyond any basic status information that might appear in issue fields.
- **Optimized for GitHub Enterprise** – The connector is designed for GitHub Enterprise. Functionality on Free or Team plans might be limited.
- **30-MB content size limit** – Only content up to 30 MB in size is supported. In most cases, issue content is well under this limit.
- **All-public-repository organizations not supported** – For security reasons, the connector doesn't support indexing organizations where all repositories are public. To unblock this scenario, contact Microsoft support.
- **Permission updates latency** – Changes to GitHub repository or team access aren't reflected immediately in the Copilot index; updates are picked up during the next full crawl.

## Data types indexed from GitHub Cloud Issues

The following table describes the data types that the connector indexes and how the content surfaces in Copilot and search results.

| GitHub entity | Indexed and surfaced in Copilot and search |
| --- | --- |
| **Issues** | Core issue fields such as title, body/description, labels, state (open/closed), assignees, milestones, and due dates. These fields appear in search results and as referenced items in Copilot responses. |
| **Issue comments** | Comment text on issues, used by Copilot to answer questions grounded in issue discussions. |
| **Issue metadata** | Properties such as repository name, organization, item path, organization URL, creation and update timestamps, and issue number, used to improve ranking, filtering, and summarization. |

## Permissions model and access control

You can configure the GitHub Cloud Issues connector so that only users who have access to a GitHub repository can see its issues in Copilot responses and search results. The connector enforces the GitHub permission model as follows:

- **Repository and team permissions** – If a repository is private or restricted to specific teams or users, only those authorized users can see issues from that repository. If a repository is visible to a wider group in your organization, its issues are discoverable to that audience in Copilot and Microsoft Search. Content that can't be mapped to a valid permission context is hidden to prevent accidental exposure.

- **User identity mapping** – The connector maps GitHub user accounts to Microsoft Entra ID identities to enforce permissions. If GitHub user emails match their Microsoft Entra ID UPNs, the mapping is automatic. If they differ, admins can provide a mapping rule using email, sign-in (login), or name. If direct mapping fails, you can use regular expressions (regex) to transform identity data.

- **Visible to everyone option** – You can choose not to enforce per-user permissions (setting the connector to index content as **Visible to everyone**). In that case, all indexed GitHub issues are searchable by any user in the tenant. For most scenarios, we recommend the restricted mode so that results mirror GitHub permissions.

> [!IMPORTANT]
> When you authenticate using OAuth (the recommended authentication method), the connector authorizes whichever GitHub account is currently signed in to your browser session. Before you start the OAuth flow, make sure you're signed in to the **correct** GitHub account—the one that has access to the organizations and repositories you intend to index. If you have multiple GitHub accounts, sign out of the others first, or use a separate browser profile or an InPrivate/incognito window to avoid accidentally authorizing the wrong account.

## Next step

> [!div class="nextstepaction"]
> [Deploy the GitHub Cloud Issues connector](github-cloud-issues-deployment.md)
