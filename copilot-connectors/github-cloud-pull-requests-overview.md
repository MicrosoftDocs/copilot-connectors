---
title: "GitHub Cloud Pull Requests connector overview"
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
description: "Learn about the capabilities, limitations, and use cases for the GitHub Cloud Pull Requests Microsoft 365 Copilot connector."
---

# GitHub Cloud Pull Requests connector overview

The GitHub Cloud Pull Requests Microsoft 365 Copilot connector integrates pull request data from GitHub.com into Microsoft 365. This integration enables Copilot, Copilot Search, and Microsoft Search to surface relevant pull requests directly within apps like Teams, Outlook, and SharePoint.

When you configure the GitHub Cloud Pull Requests connector for your organization and index data from your GitHub.com repositories, users can search, summarize, and reason over pull requests in Microsoft Search, Microsoft 365 Copilot, and Copilot Search. This indexing gives engineering teams faster access to work-in-progress changes, code review insights, and release readiness signals - without switching applications.

## Why use the GitHub Cloud Pull Requests connector to index your data?

Modern software development teams rely on pull requests (PRs) to manage work, collaborate on changes, and assess release readiness. However, PR data is often siloed in GitHub, requiring engineers, PMs, DevOps, SREs, and stakeholders to manually search across repositories to locate relevant PRs. The GitHub Cloud Pull Requests connector indexes PR metadata from your GitHub.com organizations so users can search, filter, and summarize PRs directly from Microsoft 365. Users can ask Copilot natural-language questions such as "What open PRs are waiting for review in our payments service?" and receive grounded, actionable responses with links back to GitHub.

The GitHub Cloud Pull Requests connector provides the following benefits:

- **Accelerates code reviews** – Surface PRs by status, label, milestone, author, or reviewer so reviewers spend less time hunting for what needs attention.
- **Improves release management** – Identify PRs targeting release branches, milestones, or due dates to assess readiness and unblock deployments.
- **Reduces context switching** – Developers and stakeholders stay in Microsoft 365 while referencing GitHub work, instead of jumping between tools.
- **Supports cross-functional collaboration** – PMs, support, and leadership can track engineering progress without needing deep GitHub fluency.
- **Improves auditability** – Compliance and audit teams can trace merged PRs, contributors, and timestamps across repositories.
- **Preserves security and compliance** – The connector honors GitHub repository and team permissions so users only see PRs from repos they can already access in GitHub.

### Use cases

The following table lists common use cases for the GitHub Cloud Pull Requests connector. The example prompts are based on real customer query patterns.

| Department/role | Use case | Business benefit |
| --- | --- | --- |
| Engineering | Find the PR about "Docker Compose setup for app". | Locate a specific change by topic instantly, even when the user doesn't remember the PR number. |
| Engineering | Show PRs about "Release v0.2.5". | Group all PRs related to a release for review and changelog generation. |
| Engineering | Explain PR #47 in swift-chat. | Get a quick summary of a specific PR—description, status, reviewers—without opening GitHub. |
| Engineering | Find PRs created by EmilyyyLiu. | Spotlight contributions from specific engineers for reviews, recognition, or follow-up. |
| Engineering | Find the latest created PRs. | See the freshest work-in-progress across the org at a glance. |
| Quality assurance | Find closed PRs with the label "dependencies" in swift-chat. | Identify dependency upgrades that need regression testing. |
| Quality assurance | What are the open PRs with the "dependencies" label? | Surface dependency PRs that still need review and validation. |
| Release management | What's the status of PRs with milestones being "swift-chat-2"? | Quickly assess milestone readiness for go/no-go decisions. |
| Release management | Find swift-chat PRs due by September 2025. | Identify PRs at risk of missing target dates so they can be expedited or descoped. |
| Release management | What are the latest merged PRs? | Build release notes and changelogs from recent merges with one prompt. |
| Compliance/audit | Show latest updated PRs and group them by assignees. | Generate workload distribution snapshots for audits or rebalancing. |
| Compliance/audit | Find closed PRs with the tag "dependencies" in swift-chat and bucket by month. | Produce time-series views of dependency hygiene for compliance reporting. |
| Engineering leadership | Summarize and prioritize a set of PR URLs across the swift-chat repository. | Triage a batch of in-flight changes for leadership reviews. |
| Cross-team collaboration | What is the PR about "Support Dark Mode on Android, iOS and Mac" and related projects? | Connect PRs to broader initiatives and downstream impact for planning. |

## Build agents with the GitHub Cloud Pull Requests connector

Developers can use this connector as a knowledge source in declarative agents they build with [Microsoft Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/copilot-studio-agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

By incorporating GitHub pull request data into agents, developers allow users to:

- Retrieve and summarize PRs waiting for review.
- Identify PRs tied to feature work, milestones, or infrastructure changes.
- Provide visibility into engineering progress during planning and release cycles.

### Example prompts

The following examples show prompts that agent builders can use to help users retrieve information from GitHub Cloud Pull Requests. The prompts reflect real patterns from customer usage.

**Engineering**

- Find the PR about "Docker Compose setup for app".
- What is the PR about "Update README.md include badges"?
- Find PRs mentioning "Add Amazon Bedrock deepseek-r1 model support".
- Explain PR #47 in swift-chat.
- Find PRs created by EmilyyyLiu.

**Quality assurance**

- Find closed PRs with the label "dependencies" in swift-chat.
- What are the open PRs with the "dependencies" label?
- Find closed PRs with the label "javascript" in swift-chat.

**Release management**

- What's the status of PRs with milestones being "swift-chat-2"?
- Find swift-chat PRs due by September 2025.
- Summarize open PRs due by 2025 with milestone swift-chat-9.
- What are the latest merged PRs?

**Compliance/audit**

- Show the latest updated PRs and group them by assignees.
- Find closed PRs with the tag "dependencies" in swift-chat and bucket them by month.
- What are the completed PRs by thinkasany last year?

**Engineering leadership**

- Look at these PRs and count PRs per assignee so we can make sure the workload is balanced.
- Summarize and prioritize these PRs: `https://github.com/<org>/<repo>/pull/14`;`https://github.com/<org>/<repo>/pull/13`.
- Find latest created PRs and group them by creation time.

**Cross-entity workflows**

- Find PRs that fix issue #56 in swift-chat.
- Summarize PR #319 in drawer and its related email threads.
- Create a document about `https://github.com/<org>/<repo>/pull/319`.

## GitHub Cloud Pull Requests connector capabilities and limitations

The GitHub Cloud Pull Requests connector offers the following key capabilities:

- **Indexes pull request metadata** – Crawls PR titles, descriptions, labels, state (open, closed, or merged), authors, reviewers, assignees, milestones, due dates, and timestamps from your configured GitHub.com organizations and repositories.
- **Integrates with Copilot** – Enables Copilot, Copilot Search, and Microsoft Search to find and use PR data. Users can ask natural-language questions and get grounded answers with citations back to the PR in GitHub.
- **Maintains GitHub access control** – The connector honors GitHub repository visibility and team permissions, so users only see PRs from repositories they have access to in GitHub.
- **Configurable content scope and crawl behavior** – Admins choose which organizations and repositories to include, and can customize crawl frequency, identity mapping, and indexing preferences.
- **Supports webhook-based real-time updates (preview)** – Optional webhook-based automation keeps PR data up to date in near real time.

The GitHub Cloud Pull Requests connector has the following limitations:

- **GitHub Cloud only** – On-premises or self-hosted GitHub instances aren't supported. Use the [GitHub Server Pull Requests connector](github-server-pull-requests-overview.md) for GitHub Enterprise Server.
- **No code diffs or commit details** – Code diffs, file changes, inline review comments, and commit-level details aren't indexed.
- **No CI/CD pipeline indexing** – CI/CD pipelines aren't indexed beyond status information that might appear on PRs.
- **Optimized for GitHub Enterprise** – Free or Team plans might have limited functionality.
- **SSO not supported during configuration** – Single sign-on (SSO) isn't supported during connector configuration; the admin must complete OAuth by using a non-SSO sign-in.
- **30-MB content size limit** – Only content up to 30 MB in size is supported. In most cases, PR content is well under this limit.
- **All-public-repository organizations not supported** – For security reasons, the connector doesn't support indexing organizations where all repositories are public. To unblock this scenario, contact Microsoft support.

## Data types indexed from GitHub Cloud Pull Requests

The following table describes the data types that the connector indexes and how the content surfaces in Copilot and search results.

| GitHub entity | Indexed and surfaced in Copilot and search |
| --- | --- |
| **Pull request metadata** | Title, body/description, labels, state (open/closed/merged), author, reviewers, assignees, milestones, due dates, and timestamps. |
| **Repository metadata** | Repository name, organization, item path, and contextual fields used for ranking and filtering PRs. |

The connector doesn't index the following data types: code diffs, file changes, inline comments, commit details, CI/CD pipelines, or linked artifacts beyond PR metadata.

## Permissions model and access control

The connector enforces GitHub's permission model so that users only see pull request information they're authorized to view.

- **Repository and team permissions** – Private repository PRs appear only for users with explicit repository access. The connector honors organization-level and team-based access restrictions. It hides content that can't be mapped to a valid identity to prevent exposure.

- **User identity mapping** – The connector maps GitHub user accounts to Microsoft Entra ID identities to enforce permissions. If GitHub user emails match their Microsoft Entra ID UPNs, the mapping is automatic. If they differ, admins can configure a mapping rule using email, sign-in (login), or name. Optional regex rules can transform identity attributes for consistent matching, and a manual fallback mapping is available when automatic mapping fails.

- **Bring Your Own Key (BYOK) vs. Enterprise Managed Users (EMU)** – For enterprises that use BYOK rather than EMU, each user must enable the permission to share the required identity field in their GitHub account settings so the connector can map them to Microsoft Entra ID.

> [!IMPORTANT]
> When you authenticate by using OAuth (the recommended authentication method), the connector authorizes whichever GitHub account is currently signed in to your browser session. Before you start the OAuth flow, make sure you're signed in to the **correct** GitHub account. The account must have access to the organizations and repositories you intend to index. If you have multiple GitHub accounts, sign out of the others first, or use a separate browser profile or an InPrivate/incognito window to avoid accidentally authorizing the wrong account.

## Next step

> [!div class="nextstepaction"]
> [Deploy the GitHub Cloud Pull Requests connector](github-cloud-pull-requests-deployment.md)
