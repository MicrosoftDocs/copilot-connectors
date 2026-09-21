---
title: "GitHub Cloud Knowledge connector overview"
ms.author: lauragra
author: Lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 06/02/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the GitHub Cloud Knowledge Microsoft 365 Copilot connector."
---

# GitHub Cloud Knowledge connector overview

The GitHub Cloud Knowledge Microsoft 365 Copilot connector integrates GitHub repository documentation—including README files, markdown guides, and plain-text technical notes—into Microsoft 365. By using this connector, Copilot, Copilot Search, and Microsoft Search can surface relevant project knowledge directly within apps like Teams, Outlook, and SharePoint.

When you configure the GitHub Cloud Knowledge connector for your organization and index data from your GitHub.com repositories, users can search GitHub documentation in Microsoft Search, Microsoft 365 Copilot, and Copilot Search. The connector helps reduce time spent context-switching between GitHub and Microsoft 365 apps, accelerates onboarding for new engineers, and makes institutional engineering knowledge easier to discover.

## Why use the GitHub Cloud Knowledge connector to index your data?

Engineering organizations that rely on GitHub for source code typically also use GitHub as the system of record for project documentation, architecture notes, runbooks, and contribution guidelines. However, this content is often siloed from the productivity tools where employees spend most of their day. The GitHub Cloud Knowledge connector addresses this problem by indexing markdown and text files from your GitHub.com repositories into Microsoft 365. Developers, PMs, support engineers, and new hires can ask Copilot questions in natural language—such as "How do I set up Project Alpha?"—and receive grounded answers with links back to the source files in GitHub.

The GitHub Cloud Knowledge connector provides the following benefits:

- **Boosts developer productivity** – Engineers find setup guides, contribution rules, and architecture docs from inside Copilot, Teams, and Outlook without switching to GitHub.
- **Accelerates onboarding and ramp-up** – New hires can summarize README files, environment setup steps, and contributor guidelines with a single Copilot prompt.
- **Improves cross-team knowledge sharing** – Documentation written in one team's repository becomes discoverable across the organization through Microsoft Search and Copilot.
- **Reduces duplicate documentation** – Surfacing existing guides in everyday tools reduces the tendency for teams to recreate documentation that already lives in GitHub.
- **Strengthens consistency for AI-grounded answers** – Copilot answers are grounded in current repository documentation, with citations back to the source files.
- **Preserves security and compliance** – The connector respects GitHub repository visibility and team permissions; users only see content they already have access to in GitHub.

### Use cases

The following table lists common use cases for the GitHub Cloud Knowledge connector. The example prompts are based on real customer query patterns.

| Department/role | Use case | Business benefit |
| --- | --- | --- |
| All | Where can I find the README for the swift-chat repository? | Surface authoritative project documentation instantly, reducing time spent navigating GitHub. |
| All | Summarize the README for the elysia repository under the KCL-Benediction organization. | Compress long onboarding docs into a quick summary so users can ramp up faster. |
| Engineering/DevOps | How do I set up the environment for the elysia repository? | Provide step-by-step setup grounded in the repo's own documentation, reducing setup errors. |
| Engineering/DevOps | What environment variables are required to run tests in the elysia repository? | Pull configuration details directly from repo guides so engineers don't have to dig through folders. |
| Engineering/DevOps | Show me a code snippet for sending emails in the elysia repository under KCL-Benediction. | Surface concrete in-repo code examples to accelerate implementation. |
| Engineering/DevOps | Which payload formats does the API support in the elysia repository? | Bring API reference content into Copilot answers so engineers stay in flow. |
| New hires/contributors | How do I contribute to the swift-chat repository under the KCL-Benediction organization? | Surface CONTRIBUTING guides and contribution policies in one prompt, reducing onboarding friction. |
| New hires/contributors | What are the help guidelines for the elysia repository? | Help newcomers find contribution requirements and support channels without searching the repo manually. |
| Product/program management | Summarize all documents in the drawer repository. | Generate a high-level briefing on a repo's documentation footprint for status updates and reviews. |
| Product/program management | How many documents are in each repository, and what are the first-step docs to start understanding them? | Provide an at-a-glance map of available knowledge across repos to support onboarding and audits. |
| Support/help desk | Where can I find troubleshooting instructions for the API integration in repo X? | Help support engineers retrieve troubleshooting guides quickly during ticket resolution. |
| Technical writing | Find the CHANGELOG.md authored by xrkffgg in the drawer repository. | Locate change history by author for release notes or audit purposes. |
| Localization | Is there a Chinese README for the swift-chat repository? | Quickly identify localized documentation availability across repos. |
| Security/compliance | Show me documentation accessible to amazon-auto and me in the drawer repository. | Confirm shared documentation scope between collaborators while respecting GitHub permissions. |

## Build agents with the GitHub Cloud Knowledge connector

Developers can use this connector as a knowledge source in declarative agents they build with [Microsoft Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/copilot-studio-agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that agent builders can use to help users retrieve information from the GitHub Cloud Knowledge connector. The prompts reflect real patterns from customer usage.

**Engineering/DevOps**

- How do I set up the environment for the elysia repository under the KCL-Benediction organization?
- What environment variables are required while running tests in the elysia repository?
- Where is the API reference for user and tree managers in the elysia repository?
- Show me a JavaScript code example for validating email in the elysia repository.

**New hires and contributors**

- How do I contribute to the swift-chat repository under the KCL-Benediction organization?
- Where are the contribution rules for the swift-chat repository?
- What's the requirement to join development in the elysia repository?
- Summarize CONTRIBUTING.md written by dannyjameswilliams.

**Product/program management**

- Summarize all documents in the drawer repository.
- How many documents are in each repository, and what are the first-step docs to start understanding them?
- Show me the latest created documents in our GitHub knowledge base.
- Show me documents in the elysia repository modified on 2025-09-05.

**Support and operations**

- Where can I see the changelog of the drawer repo under the KCL-Benediction organization?
- Find the CHANGELOG.md by xrkffgg in the drawer repository.
- What changed recently in the drawer repository under KCL-Benediction?

**Cross-team collaboration**

- Show me documentation accessible to xrkffgg and me in the drawer repository.
- Show me documents created between August 15 and August 18, 2025.
- Find the intro for the elysia repository and create the summary as an email draft.

## GitHub Cloud Knowledge connector capabilities and limitations

The GitHub Cloud Knowledge connector has the following key capabilities:

- **Indexes core repository documentation** – Crawls markdown (`.md`) and text (`.txt`) files in GitHub.com repositories, plus basic repository metadata.
- **Integrates with Copilot** – Enables Copilot, Copilot Search, and Microsoft Search to find and use GitHub documentation. Users ask questions in natural language and get grounded answers with citations back to the source file in GitHub.
- **Respects GitHub permissions** – The connector only shows content to users who already have access to the underlying repository in GitHub. It honors repository visibility, organization access, and team-based permissions.
- **Configurable content scope** – Admins can choose which organizations and repositories to include during connection setup and adjust crawl frequency to match organizational needs.

The GitHub Cloud Knowledge connector has the following limitations:

- **Documentation files only** – Only repository metadata, markdown, and text files are indexed. Issues, pull requests, comments, and other GitHub entities aren't indexed by this connector. To index those, use the corresponding [GitHub Cloud Issues](github-cloud-issues-overview.md) or [GitHub Cloud Pull Requests](github-cloud-pull-requests-overview.md) connectors.
- **30-MB file size limit** – Only markdown and text files up to 30 MB in size are supported. Larger files aren't indexed.
- **All-public-repository organizations not supported** – For security reasons, the connector doesn't support indexing organizations where all repositories are public. To unblock this scenario, contact Microsoft support.
- **Permission updates latency** – Changes to GitHub repository or team access aren't reflected immediately in the Copilot index. Permission updates are picked up during the next full crawl, not during incremental syncs.
- **Identity mapping requirement** – The connector relies on matching GitHub user identities to Microsoft Entra ID accounts to enforce permissions. If GitHub user emails don't match Microsoft Entra ID user principal names (UPNs), an admin must configure an identity mapping rule.

> [!NOTE]
> If your organization requires higher crawl throughput, use the [GitHub Server Knowledge connector](github-server-knowledge-overview.md) instead. The GitHub Server Knowledge connector uses a Microsoft Graph connector agent–based model to invoke `git clone` operations directly against your GitHub Enterprise Server instance, providing improved crawl performance for large-scale organizations.

## Data types indexed from GitHub Cloud Knowledge

The GitHub Cloud Knowledge connector indexes the following content types so they can be used in Copilot, Copilot Search, and Microsoft Search.

| GitHub content type | Indexed and surfaced in Copilot and search |
| --- | --- |
| **Markdown files** (`.md`) | Project documentation such as README files, architecture overviews, and contribution guides. The connector indexes file titles and body text. |
| **Text files** (`.txt`) | Plain-text technical notes, instructions, and supporting documentation. |
| **Repository metadata** | Basic repository information such as repository name, organization, and file path, used to improve ranking, filtering, and citations. |

## Permissions model and access control

You can configure the GitHub Cloud Knowledge connector so that only users who have access to a GitHub repository can see that repository's documentation in Copilot responses and search results. The connector enforces the GitHub permission model.

You can control permissions in the following ways:

- **Repository and team permissions** – Private repositories appear only for users with explicit repository access. Organization-level and team-based access restrictions are honored. Content that can't be mapped to a valid permission context is hidden to prevent accidental exposure.

- **Secret teams not supported** – The connector doesn't support access granted exclusively through GitHub [secret teams](https://docs.github.com/en/organizations/organizing-members-into-teams/setting-team-visibility). Users who have repository access only through a secret team might not see that repository's content in Copilot and search results. If your organization uses secret teams to manage repository access, ensure those users also have access through a visible team or are explicitly added as collaborators.

- **User identity mapping** – The connector maps GitHub user accounts to Microsoft Entra ID identities. If GitHub user emails match their Microsoft Entra ID UPNs, the mapping is automatic. If they differ, admins can provide a mapping rule using email, sign-in (login), or name. If direct mapping fails, you can use regular expressions (regex) to transform identity data. For more information, see [Map your non-Entra ID identities](map-non-entra-id.md).

- **Visible to everyone option** – You can choose not to enforce per-user permissions (setting the connector to index content as **Visible to everyone**). In that case, all indexed GitHub documentation is searchable by any user in the tenant. This works for non-confidential, public-style knowledge bases. For most scenarios, use the restricted mode so that results mirror GitHub permissions.

> [!IMPORTANT]
> When you authenticate by using OAuth (the recommended authentication method), the connector authorizes whichever GitHub account is currently signed in to your browser session. Before you start the OAuth flow, make sure you're signed in to the **correct** GitHub account - the one that has access to the organizations and repositories you intend to index. If you have multiple GitHub accounts, sign out of the others first, or use a separate browser profile or an InPrivate/incognito window to avoid accidentally authorizing the wrong account.

## Next step

> [!div class="nextstepaction"]
> [Deploy the GitHub Cloud Knowledge connector](github-cloud-knowledge-deployment.md)
