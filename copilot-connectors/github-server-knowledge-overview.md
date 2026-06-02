---
title: "GitHub Server Knowledge connector overview"
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
description: "Learn about the capabilities, limitations, and use cases for the GitHub Server Knowledge Microsoft 365 Copilot connector."
---

# GitHub Server Knowledge connector overview

The GitHub Server Knowledge Microsoft 365 Copilot connector integrates knowledge stored in GitHub Enterprise Server repositories—including markdown files, wiki pages, and blogs—into Microsoft 365. By using this connector, Copilot, Copilot Search, and Microsoft Search can surface relevant technical documentation directly within apps like Teams, Outlook, and SharePoint.

When you configure the GitHub Server Knowledge connector for your organization and index data from your GitHub Enterprise Server repositories, users can search GitHub knowledge in Microsoft Search, Microsoft 365 Copilot, and Copilot Search. This connector is designed for organizations with large GitHub Enterprise Server estates that need higher crawl throughput than the cloud-API-based connector can provide.

## Why use the GitHub Server Knowledge connector to index your data?

Engineering organizations that run GitHub Enterprise Server keep substantial amounts of institutional knowledge—architecture decisions, runbooks, contribution guides, internal wikis, and engineering blogs—directly in their repositories. However, this content is typically siloed from the productivity tools where employees spend most of their day. The GitHub Server Knowledge Copilot connector indexes markdown files, wiki pages, and blogs from your GitHub Enterprise Server instance so that engineers, PMs, support staff, and new hires can ask Copilot questions in natural language—such as "How do I set up the elysia repository?"—and receive grounded responses with links back to the source content in GitHub.

The GitHub Server Knowledge connector provides the following benefits:

- **Boosts engineering productivity** – Developers retrieve internal documentation and best practices from inside Copilot, Teams, and Outlook without switching to GitHub.
- **Accelerates onboarding** – New hires can summarize wikis, READMEs, and contribution guides in a single Copilot prompt instead of clicking through repos.
- **Improves operational responsiveness** – IT and support teams quickly access troubleshooting guides and runbooks during incident response.
- **Enhances cross-team knowledge sharing** – Documentation written in one team's repo becomes discoverable across the organization through Microsoft Search and Copilot.
- **Scales for large organizations** – The connector's Microsoft Graph connector agent–based model invokes `git clone` operations directly against your GitHub Enterprise Server, providing higher crawl throughput than the cloud API–based connector.
- **Preserves security and compliance** – The connector respects GitHub repository visibility and team permissions; users only see content they can already access in GitHub.

### Use cases

The following table lists common use cases for the GitHub Server Knowledge connector. The example prompts are based on real customer query patterns.

| Department/role | Use case | Business benefit |
| --- | --- | --- |
| All | Where can I find the README for the swift-chat repository? | Surface authoritative project documentation instantly, reducing time spent navigating GitHub. |
| All | Summarize the README for the elysia repository. | Compress long onboarding docs into a quick summary so users can ramp up faster. |
| Engineering/DevOps | How do I set up the environment for the elysia repository? | Provide step-by-step setup grounded in the repo's own documentation, reducing setup errors. |
| Engineering/DevOps | What environment variables are required to run tests in the elysia repository? | Pull configuration details directly from the repo so engineers don't have to dig through folders. |
| Engineering/DevOps | Show me a code snippet for sending emails in the elysia repository. | Surface concrete in-repo code examples to accelerate implementation. |
| Engineering/DevOps | Retrieve blog posts tagged "security" from our GitHub knowledge base. | Help engineers find best practices and announcements published as internal blog posts. |
| New hires/contributors | How do I contribute to the swift-chat repository? | Surface CONTRIBUTING guides and contribution policies in one prompt, reducing onboarding friction. |
| New hires/contributors | List onboarding documentation for new developers. | Aggregate scattered onboarding material into a single Copilot answer. |
| IT support/Help desk | Find troubleshooting guides for our internal tools. | Help support engineers retrieve troubleshooting content quickly during ticket resolution. |
| Product/program management | Summarize all documents in the drawer repository. | Generate a high-level briefing on a repo's documentation footprint for status updates. |
| Engineering leadership | Show me the latest wiki updates for the engineering team. | Quickly review recent changes to engineering knowledge for governance and awareness. |
| Security/compliance | Show me documentation accessible to amazon-auto and me in the drawer repository. | Confirm shared documentation scope between collaborators while respecting GitHub permissions. |

## Build agents with the GitHub Server Knowledge connector

Developers can use this connector as a knowledge source in declarative agents they build with [Microsoft Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that agent builders can use to help users retrieve information from GitHub Server Knowledge. The prompts reflect real patterns from customer usage.

**Engineering/DevOps**

- How do I set up the environment for the elysia repository?
- What environment variables are required while running tests in the elysia repository?
- Where is the API reference for user and tree managers in the elysia repository?
- Show me a JavaScript code example for validating email in the elysia repository.

**New hires and contributors**

- How do I contribute to the swift-chat repository?
- Where are the contribution rules for the swift-chat repository?
- List onboarding documentation for new developers.
- Summarize CONTRIBUTING.md for the elysia repository.

**IT support/Help desk**

- Find troubleshooting guides for our internal tools.
- Where can I find troubleshooting instructions for the API integration?
- Retrieve blog posts tagged "security" from our GitHub knowledge base.

**Product/program management**

- Summarize all documents in the drawer repository.
- How many documents are in each repository, and what are the first-step docs to start understanding them?
- Show me the latest wiki updates for the engineering team.

**Cross-team collaboration**

- Show me documentation accessible to xrkffgg and me in the drawer repository.
- Find the intro for the elysia repository and create the summary as an email draft.

## GitHub Server Knowledge connector capabilities and limitations

The GitHub Server Knowledge connector has the following key capabilities:

- **Indexes core repository knowledge** – Crawls markdown (`.md`) files, wiki pages, blogs, and basic repository metadata from GitHub Enterprise Server.
- **Integrates with Copilot** – Enables Copilot, Copilot Search, and Microsoft Search to find and use GitHub documentation. Users ask questions in natural language and get grounded answers with citations back to the source.
- **High crawl throughput** – Uses a Microsoft Graph connector agent–based model that invokes `git clone` operations to crawl directly against your GitHub Enterprise Server instance, providing better performance for large-scale organizations than the API-only model.
- **Respects GitHub permissions** – The connector only shows content to users who already have access to the underlying repository in GitHub. Repository visibility, organization access, and team-based permissions are honored.
- **Configurable content scope and crawl behavior** – Admins can choose which organizations and repositories to include and adjust crawl frequency to match organizational needs.

The GitHub Server Knowledge connector has the following limitations:

- **GitHub Enterprise Server only** – Designed specifically for GitHub Enterprise Server (on-premises/self-hosted) instances. GitHub.com (cloud-hosted) isn't supported by this connector; use the [GitHub Cloud Knowledge connector](github-cloud-knowledge-overview.md) for that scenario.
- **Documentation files only** – Only repository metadata, markdown, wiki pages, and blogs are indexed. Issues, pull requests, and comments aren't indexed by this connector; use the corresponding [GitHub Server Issues](github-server-issues-overview.md) or [GitHub Server Pull Requests](github-server-pull-requests-overview.md) connectors for those.
- **No CI/CD pipeline indexing** – GitHub Actions and other CI/CD pipelines aren't indexed beyond status information.
- **All-public-repository organizations not supported** – For security reasons, the connector doesn't support indexing organizations where all repositories are public. To unblock this scenario, contact Microsoft support.
- **GitHub.com not supported** – GitHub.com (including Free or Team plans) isn't supported by this connector. For GitHub.com, use the [GitHub Cloud Knowledge connector](github-cloud-knowledge-overview.md).

## Data types indexed from GitHub Server Knowledge

The connector indexes the following content types so they can be used in Copilot, Copilot Search, and Microsoft Search.

| GitHub content type | Indexed and surfaced in Copilot and search |
| --- | --- |
| **Markdown files** (`.md`) | README files, architecture overviews, contribution guides, and other documentation. The connector indexes file titles and body text. |
| **Wiki pages** | Native GitHub wikis associated with repositories, used for long-form internal documentation. |
| **Blogs and text documentation** | Engineering blogs and supporting text documentation surfaced through GitHub. |
| **Repository metadata** | Basic repository information such as repository name, organization, and file path, used to improve ranking, filtering, and citations. |

## Permissions model and access control

You can configure the GitHub Server Knowledge connector so that only users who have access to a GitHub Enterprise Server repository can see that repository's documentation in Copilot responses and search results. The connector enforces the GitHub permission model.

You can control permissions in the following ways:

- **Repository and team permissions** – Private repositories appear only for users with explicit repository access. Organization-level and team-based access restrictions are honored. Content that can't be mapped to a valid permission context is hidden to prevent accidental exposure.

- **User identity mapping** – The connector maps GitHub user accounts to Microsoft Entra ID identities. If GitHub user emails match their Microsoft Entra ID UPNs, the mapping is automatic. If they differ, admins can provide a mapping rule using email, sign-in (login), or name. If direct mapping fails, you can use regular expressions (regex) to transform identity data. For personal accounts, email domain variations and visibility settings can affect mapping accuracy.

- **Visible to everyone option** – You can choose not to enforce per-user permissions (setting the connector to index content as **Visible to everyone**). In that case, all indexed GitHub documentation is searchable by any user in the tenant. For most scenarios, use the restricted mode so that results mirror GitHub permissions.

> [!IMPORTANT]
> When you authenticate by using OAuth (the recommended authentication method), the connector authorizes whichever GitHub account is currently signed in to your browser session. Before you start the OAuth flow, make sure you're signed in to the **correct** GitHub account - the one that has access to the organizations and repositories you intend to index. If you have multiple GitHub accounts, sign out of the others first, or use a separate browser profile or an InPrivate/incognito window to avoid accidentally authorizing the wrong account.

## Next step

> [!div class="nextstepaction"]
> [Deploy the GitHub Server Knowledge connector](github-server-knowledge-deployment.md)
