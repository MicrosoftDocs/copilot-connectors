---
title: "GitHub Server Issues connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 06/02/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the GitHub Server Issues Microsoft 365 Copilot connector."
---

# GitHub Server Issues connector overview

The GitHub Server Issues Microsoft 365 Copilot connector integrates GitHub issue data from GitHub Enterprise Server into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface relevant issues directly within apps like Teams, Outlook, and SharePoint.

When you configure the GitHub Server Issues connector for your organization and index data from your GitHub Enterprise Server repositories, users can search and reason over issues in Microsoft Search, Microsoft 365 Copilot, and Copilot Search. This capability helps development teams track work, triage bugs, and understand project status without leaving their flow of work in Microsoft 365.

## Why use the GitHub Server Issues connector to index your data?

For many engineering teams, GitHub Issues is the primary system of record for feature requests, bugs, and operational work items. However, this information is often siloed in GitHub Enterprise Server, which makes it harder for PMs, engineers, support, and stakeholders to understand what's happening without switching between tools. The GitHub Server Issues Copilot connector indexes issues from GitHub Enterprise Server so that developers, PMs, support staff, and engineering leaders can discover and summarize relevant issues within Microsoft 365. Users can ask natural-language questions—such as "What are the open bugs for the checkout service?"—and receive grounded, contextual responses with links back to the original issues in GitHub.

The GitHub Server Issues connector provides the following benefits:

- **Improves work visibility** – PMs, engineers, and leaders can surface open issues, priorities, and status from within Teams, Outlook, or SharePoint.
- **Accelerates triage and decision-making** – Copilot can group, summarize, and highlight issue trends (for example, recurring production bugs) to support faster, data-driven decisions.
- **Enhances cross-team collaboration** – Support and operations teams can reference GitHub issues in their Microsoft 365 conversations, reducing misalignment and duplicate tracking.
- **Reduces context switching** – Users can discover and summarize issues directly in Copilot, instead of manually searching and filtering in GitHub.
- **Strengthens release management** – Engineering leadership can identify release-blocking issues, milestone status, and customer-requested features at a glance.
- **Preserves security and compliance** – The connector honors GitHub access controls so that only authorized users see data from private repos and restricted projects.

### Use cases

The following table lists common use cases for the GitHub Server Issues connector. The example prompts are based on real customer query patterns.

| Department/role | Use case | Business benefit |
| --- | --- | --- |
| Engineering | Find the issue about "Error analyzing large collection" in the elysia repo. | Locate the specific bug report instantly so engineers can investigate without searching GitHub manually. |
| Engineering | Show issues about the Gemini API. | Group related bug reports across repos to identify systemic problems. |
| Engineering | Summarize the issue about "Image cannot be displayed in chat". | Compress long issue threads into actionable summaries that engineers can use to scope work. |
| DevOps/SRE | List the open incidents tagged "production" or "sev1" and summarize their current status. | Provide a single-prompt incident status view for ops standups. |
| DevOps/SRE | Find issues with more than 16 comments. | Identify hot, contentious, or high-engagement issues that may need leadership attention. |
| IT support/Help desk | Find the GitHub issue about "Python Backend – Error with Gemini API". | Resolve user tickets faster by surfacing the matching existing issue and its discussion. |
| IT support/Help desk | Find the GitHub closed issue about the example link. | Quickly confirm whether a reported problem has already been resolved. |
| Product management | Find open issues in the elysia repository. | See the current backlog at a glance to prioritize the next milestone. |
| Product management | Summarize issues in milestone swift-chat-4 sorted by creation time. | Prepare milestone reviews without manually exporting from GitHub. |
| Product management | What are the issues with due date 2025-12-20? | Plan around deadlines and identify schedule risks early. |
| Engineering leadership | Show issue #38 and all PRs related to it. | Trace work items end-to-end (issue → PR → release) for status reporting. |
| Engineering leadership | Tell me about the issues closed in H1 2025. | Generate period summaries for QBRs and leadership updates. |
| Security/compliance | Find issues that hellohejinyu commented "try Modal?" on. | Trace specific discussion threads for audit or follow-up. |

## Build agents with the GitHub Server Issues connector

Developers can use this connector as a knowledge source in declarative agents they build with [Microsoft Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

By connecting GitHub Issues to these agents, you can build experiences that:

- Answer questions about current issue load and priorities.
- Summarize related issues for a given feature or incident.
- Help teams plan sprints and releases using live issue data.

### Example prompts

The following examples show prompts that agent builders can use to help users retrieve information from GitHub Server Issues. The prompts reflect real patterns from customer usage.

**Engineering**

- Find the issue about "Error analyzing large collection".
- Summarize the issue about "Image cannot be displayed in chat".
- Find issues mentioning "Inconsistent Documentation".
- Explain issue #56 in swift-chat.

**DevOps/SRE**

- List the open incidents tagged "production" or "sev1" and summarize their current status.
- Find issues with more than 16 comments.
- Find issues mentioning "Error importing thinc/numpy dependencies when running `elysia start`".

**IT support/Help desk**

- Find the GitHub issue about "Python Backend – Error with Gemini API".
- Find the GitHub closed issue about the example link.
- Find issue #31 in a repository with description "Python package".

**Product management**

- Find open issues in the elysia repository.
- Summarize issues in milestone swift-chat-4 sorted by creation time.
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

## GitHub Server Issues connector capabilities and limitations

The GitHub Server Issues connector has the following key capabilities:

- **Indexes GitHub issues** – Crawls issue title, body/description, labels, state (open/closed), assignees, milestones, due dates, and comments from your configured GitHub Enterprise Server organizations and repositories.
- **Integrates with Copilot** – Enables Copilot, Copilot Search, and Microsoft Search to retrieve and summarize issue data. Users can ask questions in natural language and get grounded answers with citations back to the issue in GitHub.
- **Maintains GitHub access control** – The connector honors GitHub's repository visibility and team permissions, so users only see issues from repositories they have access to in GitHub.
- **Configurable content scope and crawl behavior** – Admins choose which organizations and repositories to include, and can customize crawl frequency and indexing preferences.

The GitHub Server Issues connector has the following limitations:

- **GitHub Enterprise Server only** – This connector is for GitHub Enterprise Server (on-premises/self-hosted) instances. For GitHub.com, use the [GitHub Cloud Issues connector](github-cloud-issues-overview.md).
- **No CI/CD pipeline indexing** – GitHub Actions and CI/CD pipelines aren't indexed beyond any basic status information that might appear in issue fields.
- **Optimized for GitHub Enterprise** – Organizations on GitHub Free or Team plans might experience limited functionality.
- **All-public-repository organizations not supported** – For security reasons, the connector doesn't support indexing organizations where all repositories are public. To unblock this scenario, contact Microsoft support.

## Data types indexed from GitHub Server Issues

The following table describes the data types that the connector indexes and how the content surfaces in Copilot and search results.

| GitHub entity | Indexed and surfaced in Copilot and search |
| --- | --- |
| **Issues** | Core issue fields such as title, body/description, labels, state (open/closed), assignees, milestones, and due dates. These fields appear in search results and as referenced items in Copilot responses. |
| **Issue comments** | Comment text on issues, used by Copilot to answer questions grounded in issue discussions. |
| **Issue metadata** | Properties such as repository name, organization, item path, organization URL, creation and update timestamps, and issue number, used to improve ranking, filtering, and summarization. |

## Permissions model and access control

You can configure the GitHub Server Issues connector so that only users who have access to a GitHub repository can see its issues in Copilot responses and search results. The connector enforces the GitHub permission model as follows:

- **Repository and team permissions** – If a repository is private or restricted to specific teams or users, only those authorized users can see issues from that repository. If a repository is visible to a wider group in your organization, its issues are discoverable to that audience in Copilot and Microsoft Search. To avoid accidental data exposure, the connector doesn't show content that can't be mapped to a valid permission context.

- **User identity mapping** – The connector maps GitHub user accounts to Microsoft Entra ID identities to accurately evaluate permissions. If GitHub user emails match their Microsoft Entra ID UPNs, the connector automatically maps them. If they differ, admins can configure identity mapping rules using email, sign-in (login), or name. Optional regex rules can transform identity attributes for consistent matching.

> [!IMPORTANT]
> When you authenticate using OAuth (the recommended authentication method), the connector authorizes whichever GitHub account is currently signed in to your browser session. Before you start the OAuth flow, make sure you're signed in to the **correct** GitHub account—the one that has access to the organizations and repositories you intend to index. If you have multiple GitHub accounts, sign out of the others first, or use a separate browser profile or an InPrivate/incognito window to avoid accidentally authorizing the wrong account.

## Next step

> [!div class="nextstepaction"]
> [Deploy the GitHub Server Issues connector](github-server-issues-deployment.md)
