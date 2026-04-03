---
title: "Bitbucket Knowledge connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 01/27/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Bitbucket Knowledge Microsoft 365 Copilot connector."
---

# Bitbucket Knowledge connector overview

The Bitbucket Knowledge Microsoft 365 Copilot connector integrates documentation files stored in Bitbucket into Microsoft 365. When you configure the connector and index documentation from Bitbucket repositories, users can discover and retrieve Markdown (.md) and text (.txt) knowledge files directly through Copilot, Copilot Search, and Microsoft Search. This indexing helps teams access engineering runbooks, onboarding guides, architecture notes, and operational documentation without leaving their Microsoft 365 workflow.

## Why use the Bitbucket Knowledge connector to index your data?

Organizations frequently store documentation in Bitbucket, including runbooks, onboarding instructions, deployment guides, and architecture notes. These documents are often stored alongside source code in `.md` and `.txt` formats. This information can be difficult to find outside developer tools. Employees across functions might not know which repository the documentation is stored in or might not have time to navigate folder structures.

The Bitbucket Knowledge connector brings this documentation into Microsoft 365. Employees can search and ask questions in natural language and receive answers grounded in trusted repository documentation, without switching tools.

Common benefits include:

- **Boosts productivity** by allowing users to access repo documentation directly from Microsoft 365 apps.
- **Improves decision-making** by surfacing authoritative documentation through Copilot.
- **Accelerates request fulfillment** by allowing IT and engineering teams to retrieve runbooks instantly.
- **Enhances collaboration** by helping teams discover and reuse existing documentation.
- **Strengthens onboarding and training** by making it easy for new users to summarize and learn from repository materials.
- **Preserves security and compliance** by respecting Bitbucket permissions and access boundaries.

### Use cases

The following table lists common use cases for the Bitbucket Knowledge connector.

| **Department/role**      | **Use case**  | **Business benefit** |
|--------------------------|--------------------------------------|----------------|
| IT support/operations  | Retrieve runbooks and troubleshooting guides via Copilot        | Faster ticket resolution; improved consistency.            |
| Engineering/DevOps     | Search deployment guides and architecture notes                  | Reduced context switching; faster completion.               |
| Security/compliance    | Locate security procedures and remediation documentation         | Faster response; better audit readiness.                   |
| Product management       | Discover feature documentation and operational constraints        | Better alignment; fewer handoff gaps.                     |
| New hires/managers     | Summarize onboarding guides and internal workflows               | Faster ramp up; reduced dependency on individuals.        |

## Build agents with the Bitbucket Knowledge connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that agent builders can use to help their users retrieve information from Bitbucket documentation.

**IT support/operations:**
- Find the runbook for resolving VPN connectivity issues and summarize the steps.
- What troubleshooting guides do we have for Outlook sync errors?

**Engineering/DevOps:**
- Summarize the deployment process for Service A and include links to the relevant documents.
- What are the rollback steps for the production release pipeline?

**Security/compliance:**
- Where is the incident response procedure documented, and what are the escalation steps?
- Summarize our secrets rotation policy and link to the source documentation.

**Product/cross-functional:**
- What are the dependencies and limitations documented for Project Orion?
- Summarize the latest architecture guidelines for microservices and link to the docs.

## Bitbucket Knowledge connector capabilities and limitations

The Bitbucket Knowledge connector enables users to:

- Index Bitbucket documentation files, including `.md` and `.txt` formats.
- Use natural-language queries in Copilot to retrieve and summarize documentation.
- Access answers grounded in repository content, with reference links back to source files.
- Apply customizable crawl behavior for incremental and full indexing.
- Rely on repository access controls to enforce permissions in Microsoft 365.

The Bitbucket Knowledge connector has the following limitations:

- Only `.md` and `.txt` files are indexed; other file types aren't included.
- Only cloud-based Bitbucket instances are supported; on-premises instances aren't supported.
- Identity mapping between Bitbucket and Microsoft Entra ID is required for proper permissions enforcement.
- The **LastModifiedBy** field might be blank in some cases if Git changes weren't mapped at crawl time.

## Data types indexed from Bitbucket

The following table describes the data types that the connector indexes and how they're surfaced in Microsoft 365 applications.

| **Bitbucket content type** | **Indexed and surfaced in Copilot and search**                                        |
|----------------------------|----------------------------------------------------------------------------------------|
| Markdown files (.md)       | Documentation such as READMEs, architecture docs, runbooks, onboarding guides, notes. |
| Text files (.txt)          | Plain-text guides, troubleshooting notes, configuration instructions.                  |

## Permissions model and access control

You can configure the Bitbucket Knowledge connector so that only users who have access to an item in Bitbucket can see it in Copilot responses and search results. The connector honors Bitbucket repository permissions and file-level access controls.

### User identity mapping

To enforce permissions accurately, the connector maps Bitbucket user identities to Microsoft Entra ID identities. Admins can configure identity mapping based on:

- Full name mapping
- Public name mapping
- Regex transformations (for example, `{0}@your-domain`)

This mapping helps to ensure secure, accurate permission enforcement across Microsoft 365 experiences.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Bitbucket Knowledge connector](bitbucket-knowledge-deployment.md)