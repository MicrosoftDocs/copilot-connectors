---
title: "GitHub Server Pull Requests Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 12/15/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the GitHub Server Pull Requests Microsoft 365 Copilot connector."
---

# GitHub Server Pull Requests Microsoft 365 Copilot connector overview

The GitHub Server Pull Requests Microsoft 365 Copilot connector integrates pull request data from GitHub Enterprise Server into Microsoft 365. After you configure the connector and index GitHub content, users can discover, summarize, and retrieve pull request information directly from Microsoft Search, Microsoft 365 Copilot, and Copilot Search. This indexing gives engineering teams faster access to work‑in‑progress changes, code review insights, release information, and repository activity—without switching applications.

## Why use the GitHub Server Pull Requests connector to index your data?

Modern software development teams rely on pull requests to manage work, collaborate on changes, and assess release readiness. However, pull request data is often siloed in GitHub, requiring engineers, program managers (PMs), DevOps, SREs, and stakeholders to manually search across repositories to locate relevant PRs.

The GitHub Server Pull Requests connector addresses this challenge by indexing pull request metadata from your GitHub Enterprise Server. Users can search, filter, and summarize PRs directly from Microsoft 365. With Copilot, users can ask natural‑language questions such as "What open PRs are waiting for review in our payments service?" and receive grounded, actionable responses with links back to GitHub.

Common use cases include:

- **Accelerate code reviews:** Surface PRs by status, label, milestone, or team.
- **Improve release management:** Identify PRs targeting release branches or blocking deployments.
- **Support cross‑functional collaboration:** Help PMs, support teams, and leadership track engineering progress.
- **Reduce context switching:** Let developers and stakeholders stay within Microsoft 365 while referencing GitHub work.

## Build agents with the GitHub Server Pull Requests connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

By incorporating GitHub pull request data into agents, developers allow users to:

- Retrieve and summarize PRs waiting for review.
- Identify PRs tied to feature work, milestones, or infrastructure changes.
- Provide visibility into engineering progress during planning and release cycles.

### Example prompts

The following examples show prompts that agent builders can use to help users retrieve information from GitHub Server Pull Requests.

#### Engineering
- What open PRs are currently waiting for review in the checkout service?
- Summarize draft pull requests created this week for the backend repository.
- Which PRs are assigned to me, and what is their current status?

#### DevOps / SRE
- List PRs targeting the release branch and summarize their readiness.
- Which PRs include infrastructure or configuration changes based on metadata or labels?
- What PRs are blocking the upcoming production deployment?

#### IT support / Help desk
- Find PRs related to internal tooling updates and summarize the expected impact.
- What pull requests are tracking improvements to the developer environment?

#### Product management
- Summarize PRs linked to the vNext milestone across core repositories.
- Which open PRs correspond to features planned for the next release?

#### Engineering leadership
- Provide a summary of high‑priority PRs across teams.
- Which PRs are open the longest, and who owns them?

## GitHub Server Pull Requests connector capabilities and limitations

The GitHub Server Pull Requests connector allows users to:

- Perform natural‑language queries over pull request metadata.
- Retrieve pull request details such as titles, descriptions, labels, milestones, authors, reviewers, assignees, and timestamps.
- Surface repository‑level context such as organization and repository metadata.
- Maintain GitHub access controls to ensure only authorized users see private repository PRs.
- Use Microsoft 365 Copilot and Microsoft Search to summarize and explore PR data efficiently.
- Customize crawl frequency, identity mapping, and indexing preferences.

The GitHub Server Pull Requests connector has the following limitations:

- Doesn't index code diffs, file changes, inline comments, commit messages, or commit‑level details.
- CI/CD pipelines beyond basic status metadata aren't indexed.
- On‑premises or self‑hosted GitHub instances that don't meet API accessibility requirements aren't supported.
- Requires GitHub Enterprise; GitHub Free or Team plans might have reduced compatibility.
- Comments, threaded discussions, and linked artifacts aren't crawled.
- For security reasons, the connector doesn't support the indexing of organizations where all repositories are public. To unblock this scenario, contact Microsoft support.

## Data types indexed from GitHub Server Pull Requests

The following table describes the data types indexed by the connector.

| GitHub entity | Indexed and surfaced in Copilot and search |
|---------------|---------------------------------------------|
| Pull request metadata | Title, body/description, labels, state (open/closed), author, reviewers, assignees, milestones, timestamps |
| Repository metadata | Repository name, organization, and contextual fields used for ranking and filtering PRs |

The following data types aren't indexed: code diffs, file changes, comments, commit details, CI/CD pipelines, or linked artifacts.

## Permissions model and access control

The connector enforces GitHub's permission model to ensure that users only see pull request information they're authorized to view.

Repository and team permissions include:

- Private repository pull requests appear only for users with repository access.
- Organization‑level or team‑based access restrictions are honored.
- Content that can't be mapped to a valid identity is hidden to prevent exposure.

User identity mapping includes:

- Automatic mapping when GitHub email addresses match Microsoft Entra ID.
- Support for mapping by email, sign-in, or name.
- Optional regular expression rules to transform identity attributes for consistent matching.
- Manual fallback mapping when automatic mapping fails.
- Requirements for users to share the appropriate identity attributes in scenarios such as the Bring Your Own User (BYOU) model.

## Next step

> [!div class="nextstepaction"]
> [Deploy the GitHub Server Pull Requests connector](github-server-pull-requests-deployment.md)
