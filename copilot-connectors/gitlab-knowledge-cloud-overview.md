---
title: GitLab Knowledge Cloud Microsoft 365 Copilot connector overview
description: Learn about the capabilities, limitations, and use cases for the GitLab Knowledge Cloud Microsoft 365 Copilot connector.
author: Lauragra
ms.author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.reviewer: raynezou
ms.date: 01/23/2026
ms.localizationpriority: Medium
ms.service: copilot-connectors
ms.topic: concept-article
---

# GitLab Knowledge Cloud Microsoft 365 Copilot connector overview

The GitLab Knowledge Cloud Microsoft 365 Copilot connector indexes documentation and knowledge artifacts stored in GitLab projects on GitLab.com. These assets typically include project wikis, readme files, architecture and design documents, onboarding guides, runbooks, and other Markdown‑based knowledge used to document processes, systems, and best practices. These artifacts capture institutional knowledge and provide long‑term reference for engineering, operations, and cross‑functional teams.

## Why use the GitLab Knowledge Cloud connector to index your data?

The GitLab Knowledge Cloud connector enables organizations to index GitLab‑hosted documentation and make it available in Microsoft 365 Copilot and Microsoft Search. This indexing allows users to discover, summarize, and reuse engineering and operational knowledge directly within their Microsoft 365 workflows.

Common scenarios include:

- **Developer productivity:** Enable developers to quickly find architecture decisions, API documentation, and contribution guidelines from GitLab without leaving Teams or Copilot.
- **Onboarding and enablement:** Help new engineers or support staff discover onboarding guides, runbooks, and team standards stored in GitLab.
- **Operational excellence:** Allow site reliability engineering (SRE) and IT teams to retrieve troubleshooting guides, incident runbooks, and postmortem documentation during live investigations.
- **Project and technical alignment:** Support engineering leads and architects by summarizing design documents and technical proposals across multiple GitLab projects.
- **Enterprise knowledge discovery:** Make GitLab‑hosted documentation discoverable through Microsoft Search for improved cross‑team and cross‑function collaboration.

## Build agents with the GitLab Knowledge Cloud connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Agent prompts

The following examples show prompts that agent builders can use to help their users retrieve information from GitLab Knowledge Cloud.

| Role | Example prompt |
| ------ | ---------------- |
| Developer | Find GitLab documentation that explains the authentication flow for our API. |
| Project manager | Summarize GitLab wiki pages related to the current project's architecture and scope. |
| Support agent | Look up GitLab runbooks related to handling API timeout issues and summarize the recommended steps. |
| Engineering manager | Give me a summary of design documents in GitLab related to the new billing platform. |
| SRE/Ops | Find GitLab documentation related to production incident response and outage recovery procedures. |

## GitLab Knowledge Cloud connector capabilities and limitations

The GitLab Knowledge Cloud connector enables users to:

- Retrieve GitLab knowledge assets such as wikis, README files, design documents, and runbooks through natural‑language queries in Copilot.
- Discover and summarize authoritative engineering and operational documentation preserved in GitLab repositories.
- Surface project‑owned knowledge in Microsoft Search for cross‑team collaboration.

The connector has the following limitations:

- Indexing speed varies based on item volume and GitLab rate‑limiting constraints.
- Full crawl and incremental crawl intervals depend on GitLab API availability and organizational settings.

## Data types indexed from GitLab Knowledge Cloud

The connector indexes Markdown‑based knowledge artifacts stored in GitLab projects, including:

- Wiki pages  
- README files  
- Architecture and design documents  
- Onboarding guides  
- Runbooks and operational documentation

Indexed content is surfaced in Microsoft 365 Copilot responses and Microsoft Search results, enabling summarization, reasoning, and retrieval across all connected GitLab knowledge.

## Permissions model and access control

To ensure correct access control, GitLab user identities can be mapped to Microsoft Entra ID using:

- Email  
- Login 
- Name  
- Regex transformations, when required

Visibility options include:

- **Only people with access to this data source** (default)  
- **Everyone**

Mapped permissions ensure that only users with matching entitlement in GitLab can access the corresponding indexed knowledge in Copilot.

## Next step

> [!div class="nextstepaction"]  
> [Deploy the GitLab Knowledge Cloud connector](gitlab-knowledge-cloud-deployment.md)
