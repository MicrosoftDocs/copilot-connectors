---
title: "GitHub Server Pull Requests connector overview"
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
description: "Learn about the capabilities, limitations, and use cases for the GitHub Server Pull Requests Microsoft 365 Copilot connector."
---

# GitHub Server Pull Requests connector overview

The GitHub Server Pull Requests Microsoft 365 Copilot connector integrates pull request data from GitHub Enterprise Server into Microsoft 365. By using this connector, Copilot, Copilot Search, and Microsoft Search can surface relevant pull requests directly within apps like Teams, Outlook, and SharePoint.

When you configure the GitHub Server Pull Requests connector for your organization and index data from your GitHub Enterprise Server repositories, users can discover, summarize, and reason over pull request information directly from Microsoft Search, Microsoft 365 Copilot, and Copilot Search. This indexing gives engineering teams faster access to work-in-progress changes, code review insights, and release readiness signals - without switching applications.

## Why use the GitHub Server Pull Requests connector to index your data?

Modern software development teams rely on pull requests (PRs) to manage work, collaborate on changes, and assess release readiness. However, PR data is often siloed in GitHub Enterprise Server, requiring engineers, PMs, DevOps, SREs, and stakeholders to manually search across repositories to locate relevant PRs. The GitHub Server Pull Requests connector indexes PR metadata from your GitHub Enterprise Server so users can search, filter, and summarize PRs directly from Microsoft 365. By using Copilot, users can ask natural-language questions such as "What open PRs are waiting for review in our payments service?" and receive grounded, actionable responses with links back to GitHub.

The GitHub Server Pull Requests connector provides the following benefits:

- **Accelerates code reviews** – Surface PRs by status, label, milestone, author, or reviewer so reviewers spend less time hunting for what needs attention.
- **Improves release management** – Identify PRs targeting release branches, milestones, or due dates to assess readiness and unblock deployments.
- **Reduces context switching** – Developers and stakeholders stay in Microsoft 365 while referencing GitHub work, instead of jumping between tools.
- **Supports cross-functional collaboration** – PMs, support, and leadership can track engineering progress without needing deep GitHub fluency.
- **Improves auditability** – Compliance and audit teams can trace merged PRs, contributors, and timestamps across repositories.
- **Preserves security and compliance** – The connector honors GitHub repository and team permissions so users only see PRs from repos they can already access in GitHub.

### Use cases

The following table lists common use cases for the GitHub Server Pull Requests connector. The example prompts are based on real customer query patterns.

| Department/role | Use case | Business benefit |
| --- | --- | --- |
| Engineering | Find the PR about "Docker Compose setup for app". | Locate a specific change by topic instantly, even when the user doesn't remember the PR number. |
| Engineering | Show PRs about "Release v0.2.5". | Group all PRs related to a release for review and changelog generation. |
| Engineering | Explain PR #47 in swift-chat. | Get a quick summary of a specific PR—description, status, reviewers—without opening GitHub. |
| Engineering | Find PRs created by EmilyyyLiu. | Spotlight contributions from specific engineers for reviews, recognition, or follow-up. |
| Engineering | Find the latest created PRs. | See the freshest work-in-progress across the org at a glance. |
| DevOps/SRE | List PRs targeting the release branch and summarize their readiness. | Build a single-prompt release readiness view for go/no-go calls. |
| DevOps/SRE | Which PRs include infrastructure or configuration changes based on metadata or labels? | Surface infra-impacting changes for review before they land. |
| Quality assurance | Find closed PRs with the label "dependencies" in swift-chat. | Identify dependency upgrades that need regression testing. |
| Quality assurance | What are the open PRs with the "dependencies" label? | Surface dependency PRs that still need review and validation. |
| Release management | What's the status of PRs with milestones being "swift-chat-2"? | Quickly assess milestone readiness for go/no-go decisions. |
| Release management | Find swift-chat PRs due by September 2025. | Identify PRs at risk of missing target dates so they can be expedited or descoped. |
| Release management | What are the latest merged PRs? | Build release notes and changelogs from recent merges with one prompt. |
| Compliance/audit | Show latest updated PRs and group them by assignees. | Generate workload distribution snapshots for audits or rebalancing. |
| Engineering leadership | Provide a summary of high-priority PRs across teams. | Get a leadership-ready cross-team status snapshot. |
| Engineering leadership | Which PRs are open the longest, and who owns them? | Detect stalled work and accountability gaps. |
| Cross-team collaboration | What is the PR about "Support Dark Mode on Android, iOS and Mac" and related projects? | Connect PRs to broader initiatives and downstream impact for planning. |

## Build agents with the GitHub Server Pull Requests connector

Developers can use this connector as a knowledge source in declarative agents they build with [Microsoft Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

By incorporating GitHub Pull Request data into agents, developers allow users to:

- Retrieve and summarize PRs waiting for review.
- Identify PRs tied to feature work, milestones, or infrastructure changes.
- Provide visibility into engineering progress during planning and release cycles.

### Example prompts

The following examples show prompts that agent builders can use to help users retrieve information from GitHub Server Pull Requests. The prompts reflect real patterns from customer usage.

**Engineering**

- Find the PR about "Docker Compose setup for app".
- What is the PR about "Update README.md include badges"?
- Find PRs mentioning "Add Amazon Bedrock deepseek-r1 model support".
- Explain PR #47 in swift-chat.
- Find PRs created by EmilyyyLiu.

**DevOps/SRE**

- List PRs targeting the release branch and summarize their readiness.
- Which PRs include infrastructure or configuration changes based on metadata or labels?
- What PRs are blocking the upcoming production deployment?

**Quality assurance**

- Find closed PRs with the label "dependencies" in swift-chat.
- What are the open PRs with the "dependencies" label?
- Find closed PRs with the label "javascript" in swift-chat.

**Release management**

- What's the status of PRs with milestones being "swift-chat-2"?
- Find swift-chat PRs due by September 2025.
- Summarize open PRs due by 2025 with milestone swift-chat-9.
- What are the latest merged PRs?

**Engineering leadership**

- Provide a summary of high-priority PRs across teams.
- Which PRs are open the longest, and who owns them?
- Look at these PRs and count PRs per assignee so we can make sure the workload is balanced.

**Cross-entity workflows**

- Find PRs that fix issue #56 in swift-chat.
- Summarize PR #319 in drawer and its related email threads.
- Create a document about https://github.com/KCL-Benediction/drawer/pull/319.

## GitHub Server Pull Requests connector capabilities and limitations

The GitHub Server Pull Requests connector offers the following key capabilities:

- **Indexes pull request metadata** – Crawls PR titles, descriptions, labels, state (open/closed/merged), authors, reviewers, assignees, milestones, due dates, and timestamps from your configured GitHub Enterprise Server organizations and repositories.
- **Integrates with Copilot** – Enables Copilot, Copilot Search, and Microsoft Search to find and use PR data. Users can ask natural-language questions and get grounded answers with citations back to the PR in GitHub.
- **Maintains GitHub access control** – The connector honors GitHub repository visibility and team permissions, so users only see PRs from repositories they have access to in GitHub.
- **Configurable content scope and crawl behavior** – Admins choose which organizations and repositories to include, and can customize crawl frequency, identity mapping, and indexing preferences.

The GitHub Server Pull Requests connector has the following limitations:

- **GitHub Enterprise Server only** – This connector is for GitHub Enterprise Server (on-premises/self-hosted) instances that meet API accessibility requirements. For GitHub.com, use the [GitHub Cloud Pull Requests connector](github-cloud-pull-requests-overview.md).
- **No code diffs or commit details** – Code diffs, file changes, inline review comments, and commit-level details aren't indexed.
- **No CI/CD pipeline indexing** – CI/CD pipelines aren't indexed beyond basic status metadata that might appear on PRs.
- **No PR comments or threaded discussions** – Comments, threaded discussions, and linked artifacts beyond PR metadata aren't crawled.
- **Optimized for GitHub Enterprise** – Free or Team plans might have reduced compatibility.
- **All-public-repository organizations not supported** – For security reasons, the connector doesn't support indexing organizations where all repositories are public. To unblock this scenario, contact Microsoft support.

## Data types indexed from GitHub Server Pull Requests

The following table describes the data types that the connector indexes and how the content surfaces in Copilot and search results.

| GitHub entity | Indexed and surfaced in Copilot and search |
| --- | --- |
| **Pull request metadata** | Title, body/description, labels, state (open/closed/merged), author, reviewers, assignees, milestones, due dates, and timestamps. |
| **Repository metadata** | Repository name, organization, item path, and contextual fields used for ranking and filtering PRs. |

The following data types **aren't** indexed: code diffs, file changes, inline comments, commit details, CI/CD pipelines, or linked artifacts beyond PR metadata.

## Permissions model and access control

The connector enforces GitHub's permission model so that users only see pull request information they're authorized to view.

- **Repository and team permissions** – Private repository PRs appear only for users with explicit repository access. Organization-level and team-based access restrictions are honored. Content that can't be mapped to a valid identity is hidden to prevent exposure.

- **User identity mapping** – The connector maps GitHub user accounts to Microsoft Entra ID identities. Automatic mapping occurs when GitHub email addresses match Microsoft Entra ID. Admins can also map by email, sign-in (login), or name. Optional regex rules can transform identity attributes for consistent matching, and a manual fallback mapping is available when automatic mapping fails.

- **Bring Your Own User (BYOU) scenarios** – In scenarios such as Bring Your Own User, individual users may need to share the appropriate identity attributes in their GitHub account settings so the connector can map them to Microsoft Entra ID.

> [!IMPORTANT]
> When you authenticate using OAuth (the recommended authentication method), the connector authorizes whichever GitHub account is currently signed in to your browser session. Before you start the OAuth flow, make sure you're signed in to the **correct** GitHub account—the one that has access to the organizations and repositories you intend to index. If you have multiple GitHub accounts, sign out of the others first, or use a separate browser profile or an InPrivate/incognito window to avoid accidentally authorizing the wrong account.

## Next step

> [!div class="nextstepaction"]
> [Deploy the GitHub Server Pull Requests connector](github-server-pull-requests-deployment.md)
