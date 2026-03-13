---
title: "GitLab Knowledge Server Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 01/26/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the GitLab Knowledge Server Microsoft 365 Copilot connector."
---
# GitLab Knowledge Server Microsoft 365 Copilot connector overview

The GitLab Knowledge Server Microsoft 365 Copilot connector enables organizations to index knowledge content stored in GitLab self-managed (on-premises) instances—including Markdown files, wiki pages, and other documentation repositories—and make this content available through Microsoft Search and Microsoft 365 Copilot. After the connector is configured and data is indexed, GitLab knowledge appears directly in Microsoft 365 applications such as Teams, Outlook, and SharePoint. This indexing allows employees to discover and reuse organizational knowledge without leaving their daily workflow.

## Why use the GitLab Knowledge Server connector to index your data?

The GitLab Knowledge Server connector is designed for organizations that store technical documentation, internal wikis, and knowledge bases in GitLab repositories that want to make this information discoverable across Microsoft 365.

Common use cases include:

- Enable engineers and technical writers to quickly locate internal documentation, architecture notes, and best practices.
- Help IT and support teams access troubleshooting guides, runbooks, and operational documentation.
- Improve onboarding by surfacing internal knowledge for new employees through Copilot and Microsoft Search.
- Allow business and technical leaders to retrieve project documentation and technical context without navigating GitLab directly.

## Build agents with the GitLab Knowledge Server connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit). This knowledge allows custom agents to reason over GitLab-hosted knowledge and answer questions grounded in your organization's documentation.

### Eaxmple prompts

The following examples show prompts that agent builders can use to help users retrieve information from GitLab Knowledge Server:

- Show me the latest wiki updates for the platform engineering team.
- Find troubleshooting documentation for our internal services.
- List onboarding guides for new backend developers.
- Retrieve documentation tagged with *security* from our GitLab knowledge repositories.

## GitLab Knowledge Server connector capabilities and limitations

The GitLab Knowledge Server connector enables users to:

- Index GitLab repositories, wikis, and documentation.
- Retrieve GitLab data through Microsoft Search and Microsoft 365 Copilot.
- Maintain GitLab access control lists (ACLs) and enforce user permissions.
- Customize crawl frequency and indexing preferences.

The GitLab Knowledge Server connector has the following limitations:

- CI/CD pipelines aren’t supported beyond status indexing.
- Only `.md`, `.txt`, and wikis are indexed.
- Banning users isn't supported; remove users from groups instead.
- IP-based group access restrictions aren’t supported; use private groups.
- Support for the Planner role is deprecated; Reporter role or higher is required.
- For public projects restricted to project members, merge request access is set to Reporter and higher.

## Data types indexed from GitLab Knowledge Server

The connector indexes the following GitLab content types:

- Markdown files (`.md`)
- GitLab wiki pages
- Text-based documentation stored in repositories

Indexed content appears in Microsoft 365 Copilot and Microsoft Search results, helping users interact with GitLab knowledge directly within Microsoft 365 applications.

## Permissions model and access control

Administrators can configure access control for indexed GitLab data using Microsoft Entra ID identity mapping. The connector supports the following access model options:

- **Only people with access to this data source** (default): Search results appear only for users who have access to the corresponding GitLab repositories.
- **Everyone**: Indexed GitLab knowledge is visible to all users in Microsoft 365.

Identity mapping options include mapping by:

- Email  
- Login  
- Name  

If direct mapping fails, administrators can apply regular expressions (regex) to transform identity attributes. Email visibility settings and domain inconsistencies in GitLab might affect mapping accuracy.

## Next step

> [!div class="nextstepaction"]
> [Deploy the GitLab Knowledge Server connector](gitlab-knowledge-server-deployment.md)