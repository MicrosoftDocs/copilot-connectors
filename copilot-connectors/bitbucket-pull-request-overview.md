---
title: "Bitbucket Pull Request Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 01/16/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Bitbucket Pull Request Microsoft 365 Copilot connector."
---

# Bitbucket Pull Request Microsoft 365 Copilot connector overview

The Bitbucket Pull Request Microsoft 365 Copilot connector integrates Bitbucket pull request content into Microsoft 365, allowing Copilot, Copilot Search, and Microsoft Search to surface relevant pull requests and engineering context directly within apps like Teams, Outlook, and SharePoint. When you configure the Bitbucket Pull Request connector for your organization and index pull request data from Bitbucket, users can search for PRs in Microsoft Search and ask Copilot questions in natural language, and get answers grounded in pull request titles, descriptions, discussions, and metadata, with reference links back to the source.

## Why use the Bitbucket Pull Request connector to index your data?

Pull requests contain critical engineering knowledge: what changed, why it changed, who reviewed it, and what tradeoffs were discussed. But PR context is often siloed inside developer tools, making it harder for engineers and cross-functional teams to find decisions, track implementation progress, and respond quickly to incidents. The Bitbucket Pull Request connector addresses this challenge by bringing PR knowledge into Microsoft 365 experiences. This indexing allows teams to retrieve the right change context through Copilot and unified search without leaving their day-to-day collaboration tools.

The Bitbucket Pull Request Copilot connector provides the following benefits:
- Boosts productivity – Users can find PRs and review context directly in Microsoft 365 apps, reducing time spent navigating repositories and browser tabs.
- Improves decision-making – Copilot can summarize PR intent, review feedback, and key decisions, helping teams align faster.
- Accelerates issue resolution – During incidents, teams can quickly locate PRs related to a regression, fix, or configuration change.
- Enhances collaboration – Product, engineering, and operations teams gain shared visibility into what’s being changed and why.
- Strengthens onboarding and knowledge transfer – New hires and managers can use Copilot to understand system evolution by exploring PR history and rationale.
- Preserves security and compliance – The connector respects Bitbucket permissions so only authorized users can access PR content.

## Use cases

The following table lists common use cases for the Bitbucket Pull Request connector.

| Department/role        | Use case                                                                 | Business benefit                        |
|------------------------|--------------------------------------------------------------------------|-----------------------------------------|
| Engineering/DevOps   | Find PRs related to a feature, service, or incident and summarize key changes | Faster troubleshooting and iteration     |
| Release management     | Track merged PRs related to a release and summarize readiness            | Better planning, fewer surprises        |
| Product management     | Ask Copilot for the latest updates to PRs associated with a roadmap initiative | Improved visibility and coordination    |
| Security / compliance  | Locate PRs related to security fixes and summarize what changed          | Faster remediation tracking and audits  |
| Executives / managers  | Summarize progress across teams by surfacing merged/active PRs           | Better visibility, faster decisions     |

## Build agents with the Bitbucket Pull Request connector

Developers can use this connector as a knowledge source in declarative agents they build with [Microsoft Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio, [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or [the Microsoft 365 Agents Toolkit](/microsoft-365/copilot/extensibility/build-declarative-agents).

### Eaxmple prompts

The following examples show prompts that agent builders can use to help their users retrieve pull request information from Bitbucket:

- **Engineering / DevOps**
  - Find the PR that introduced the new authentication flow and summarize the key changes and rationale.
  - Summarize the discussion and key decisions from the PR related to timeout errors.
- **Release management**
  - List PRs merged in the last two weeks that mention "vNext" and summarize what shipped.
  - What are the open PRs related to the Q1 release and what are their blockers?
- **Product management**
  - Summarize the latest PR activity related to Project Orion.
  - What are the main dependencies mentioned in PR discussions for the new feature rollout?
- **Security / compliance**
  - Find PRs that mention "CVE-" and summarize the remediation work.
  - Summarize PRs that changed access control logic in the last month.
- **Managers**
  - Summarize PR progress across the platform team for this week.
  - What are the most frequently discussed risks across recent PR reviews?

## Bitbucket Pull Request connector capabilities and limitations

The Bitbucket Pull Request connector enables users to:

- Index pull request content – Crawls Bitbucket pull requests, including titles, descriptions, and associated metadata needed for retrieval and summarization.
- Integrate with Copilot – Enables Copilot, Copilot Search, and Microsoft Search to find and use pull request content. Users can ask natural-language questions and receive grounded answers with reference links back to the source PR.
- Respect Bitbucket permissions – Enforces Bitbucket access control lists (ACLs) so only authorized users can see pull request results.
- Configure sync – Admins can customize crawl frequency and indexing preferences, including incremental and full crawls.

The Bitbucket Pull Request connector has the following limitations:

- Pull requests only – This connector indexes pull requests only and doesn't index other Bitbucket content types (for example, source code files, wikis, or documentation files).
- Limited pipeline indexing – Doesn’t support indexing Bitbucket CI/CD pipelines beyond status indexing.
- Cloud-only support – On-premises/self-hosted Bitbucket instances aren’t currently supported.
- LastModifiedBy might be blank in some cases – If Git changes aren't mapped to a Bitbucket user account before an incremental crawl, the LastModifiedBy field might remain empty until mapping is completed and content is recrawled.
- Identity mapping requirement – The connector relies on mapping Bitbucket user identities to Microsoft Entra ID identities for permission enforcement. If identities don’t align, users might not see expected PR results.

## Data types indexed from Bitbucket

The Bitbucket Pull Request connector indexes the following content types so they can be used in Copilot, Copilot Search, and Microsoft Search:

| Bitbucket content type | Indexed and surfaced in Copilot and search |
|-----------------------|--------------------------------------------|
| Pull requests         | PR titles, descriptions, and metadata used for search and Copilot retrieval, enabling summarization and Q&A grounded in PR content. |

## Custom data filters

The Bitbucket Pull Request connector can support filtering experiences in Copilot Search based on pull request metadata (for example, repository, PR state, author, or labels depending on the metadata mapping). This filtering allows users to narrow results and quickly find relevant PRs.

## Permissions model and access control

You can configure the Bitbucket Pull Request connector to enforce that only users who have access to a Bitbucket pull request can see it in Copilot responses and search results. The connector honors Bitbucket access controls so that results mirror source permission boundaries.

### User identity mapping

To enforce permissions, the connector maps Bitbucket user identities to Microsoft 365 (Microsoft Entra ID) identities. Due to Bitbucket API limitations, identity mapping might rely on non-email attributes such as:
- Full name mapping
- Public name mapping
- Regex transformation (for example, reconstructing an email address using `{0}@<your-domain>`)

This mapping ensures that PR results returned through Copilot and Microsoft Search are correctly scoped to each user’s permitted access.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Bitbucket Pull Request connector](bitbucket-pull-request-deployment.md)
