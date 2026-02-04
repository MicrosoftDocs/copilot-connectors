---
title: "GitHub Server Issues Microsoft 365 Copilot connector overview"
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
description: "Learn about the capabilities, limitations, and use cases for the GitHub Server Issues Microsoft 365 Copilot connector."
---

# GitHub Server Issues Microsoft 365 Copilot connector overview

The GitHub Server Issues Microsoft 365 Copilot connector integrates GitHub issue data into Microsoft 365. When you deploy this connector, Microsoft 365 Copilot and Microsoft Search experiences can surface relevant issues directly within apps like Teams, Outlook, and SharePoint. When you index data from GitHub Enterprise repositories, users can search and reason over issues in Copilot and Microsoft Search. This capability helps development teams track work, triage bugs, and understand project status without leaving their flow of work.

## Why use the GitHub Server Issues connector to index your data?

For many engineering teams, GitHub Issues is the primary system of record for feature requests, bugs, and operational work items. However, this information is often siloed in GitHub. This makes it harder for PMs, engineers, support, and stakeholders to understand what's happening without switching between tools. The GitHub Issues Copilot connector indexes issues from GitHub Enterprise so that developers, PMs, support staff, and engineering leaders can discover and summarize relevant issues within Microsoft 365. Users can ask natural-language questions—such as "What are the open bugs for the checkout service?"—and receive grounded, contextual responses with links back to the original issues in GitHub.

### Connector benefits

The GitHub Server Issues connector provides the following benefits to your organization:

- **Improves work visibility** – PMs, engineers, and leaders can surface open issues, priorities, and status from within Teams, Outlook, or SharePoint.
- **Accelerates triage and decision-making** – Copilot can group, summarize, and highlight issue trends (for example, recurring production bugs) to support faster, data-driven decisions.
- **Enhances collaboration across teams** – Support and operations teams can reference GitHub issues in their Microsoft 365 conversations, reducing misalignment and duplicate tracking.
- **Reduces context switching** – Users can discover and summarize issues directly in Copilot, instead of manually searching and filtering in GitHub.
- **Preserves security and compliance** – The connector honors GitHub access controls so that only authorized users see data from private repos and restricted projects.

### Use cases

The following table lists common use cases for the GitHub Server Issues connector.

| Department/role        | Use case         | Business benefit  |
|------------------------|------------------|-------------------|
| Engineering            | Ask Copilot for open bugs, prioritized issues, or blockers for a specific service or repository. | Faster understanding of current work; reduced time spent filtering and searching in GitHub. |
| DevOps/SRE           | Summarize production incidents, recurring errors, or reliability-related issues across repos. | Improved incident review, better identification of reliability trends. |
| IT support/Help desk | Surface user-reported issues, linked tickets, and current status from GitHub. | Quicker responses to internal stakeholders; fewer duplicate tickets. |
| Product management     | Review feature requests, backlog items, and status grouped by labels, milestones, or assignees. | Better prioritization and roadmap decisions based on live issue data. |
| Engineering leadership | Get Copilot summaries of critical bugs, high-priority issues, and release-blocking items. | Faster decision-making and improved release readiness assessments. |

## Build agents with the GitHub Server Issues connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

By connecting GitHub Issues to these agents, you can build experiences that:
- Answer questions about current issue load and priorities.
- Summarize related issues for a given feature or incident.
- Help teams plan sprints and releases using live issue data.

### Agent prompts

The following examples show prompts that agent builders can use to help their users retrieve information from GitHub Server Issues:

#### Engineering
- What are the open bugs for the checkout service, and who owns them?
- Summarize the issues labeled performance created in the last seven days.
- Which issues are blocking the next release for Project Alpha?

#### DevOps/SRE
- List the open incidents tagged production or sev1 and summarize their current status.
- What recurring error patterns can you see from issues labeled database in the last month?
- Summarize the follow-up tasks created after the last production incident.

#### IT Support/Help Desk
- Find GitHub issues linked to VPN or single sign-on (SSO) problems and summarize their current status.
- Which issues are tracking user-reported authentication problems, and what's the ETA for resolution?

#### Product Management
- Summarize all open feature requests labeled vNext for Project Alpha.
- What are the top customer-requested features based on issues labeled customer-request?
- Which issues are currently scoped into the next milestone for the mobile app?

#### Engineering leadership
- Give me a summary of all critical open bugs across our top three services.
- What high-priority issues are at risk of missing the current milestone?

## GitHub Server Issues connector capabilities and limitations

By using the GitHub Server Issues connector, you can:

- Index issues from supported GitHub Enterprise repositories so you can discover and summarize them in Microsoft 365 experiences.
- Enable Microsoft Search and Copilot to retrieve GitHub data efficiently. Users can search for issues by using Microsoft Search and ask Copilot questions grounded in GitHub issue data, such as: "What are the open issues assigned to me in the payments repo?" or "Summarize the issues labeled accessibility created this quarter."
- Maintain GitHub access control lists (ACLs) and user permissions. The connector honors GitHub's ACLs and repository permissions, so users only see issues from repositories they have access to in GitHub.
- Configure crawl and indexing behavior. You can customize how often issue updates are synced, which repositories or organizations to include, and which labels or states (open/closed) to prioritize for indexing.

The connector has the following limitations:

- The connector doesn't support indexing GitHub CI/CD pipelines beyond any basic status information that might appear in issue fields or metadata. Detailed pipeline runs, logs, and configuration aren't indexed.
- The connector is designed and optimized for GitHub Enterprise scenarios. Organizations using GitHub Free or GitHub Team plans might experience limited functionality or reduced support, depending on available APIs and platform features.
- For security reasons, the connector doesn't support the indexing of organizations where all repositories are public. To unblock this scenario, contact Microsoft support.

## Data types indexed from GitHub Issues

The following table describes the data types that the connector indexes and how the content surfaces in Copilot and search results.

| GitHub entity   | Indexed and surfaced in Copilot and search |
|-----------------|--------------------------------------------|
| Issues          | Core issue fields such as title, body/description, labels, state (open/closed), assignees, milestones, and basic metadata. These fields appear in search results and as referenced items in Copilot responses. |
| Issue metadata  | Properties such as repository name, organization, creation and update timestamps, and issue number, used to improve ranking, filtering, and summarization. |

## Permissions model and access control

You can configure the GitHub Server Issues connector so that only users who have access to a GitHub repository can see its issues in Copilot responses and search results. The connector enforces the GitHub permission model as follows:

- If a repository is private or restricted to specific teams or users, only those authorized users can see issues from that repository.
- If a repository is visible to a wider group within your organization, its issues are discoverable to that audience in Copilot and Microsoft Search.
- To avoid accidental data exposure, the connector doesn't show content that can't be mapped to a valid permission context.

The connector maps GitHub user accounts to Microsoft 365 (Microsoft Entra ID) identities to accurately evaluate permissions, as follows:

- If GitHub user emails match their Microsoft Entra ID user principal names (UPNs), the connector automatically maps them.
- If they differ, admins can configure identity mapping rules so that the correct Microsoft 365 identity is associated with each GitHub account. This mapping ensures that GitHub repository and organization permissions are applied when Copilot or Microsoft Search retrieves issue data.

## Next step

> [!div class="nextstepaction"]
> [Deploy the GitHub Server Issues connector](github-server-issues-deployment.md)
