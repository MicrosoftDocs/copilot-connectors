---
title: "Dropbox Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: ang.gao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 11/24/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Dropbox Microsoft 365 Copilot connector."
---

# Dropbox Microsoft 365 Copilot connector overview

The Dropbox connector for Microsoft 365 Copilot allows your organization to index Dropbox content — including team folders, shared folders, and private folders — and surface the content in Microsoft 365 Copilot and Microsoft Search experiences.

> [!NOTE]
> Currently, only Dropbox Advanced and Enterprise plans are supported.

## Why use the Dropbox connector to index your data?

Organizations use Dropbox to store and share files across teams. When you deploy the Dropbox connector, you can:

- Surface Dropbox content in Microsoft 365 Copilot responses and Microsoft Search.
- Enable semantic search across Dropbox files without duplicating data.
- Maintain the Dropbox permission model for secure access.
- Improve productivity by integrating Dropbox content into workflows in Teams, Outlook, and SharePoint.

Common use cases include:

- Find team documents stored in Dropbox from within Microsoft 365 apps.
- Build custom workflows that combine Dropbox content with other enterprise data sources.

## Build agents with the Dropbox connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/copilot-studio-agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Agent prompts

The following examples show prompts that users can use to retrieve information from Dropbox:

- Summarize files in the shared Dropbox folder for the product launch.
- List all team Dropbox files modified in the last seven days.

## Dropbox connector capabilities and limitations

The Dropbox connector provides the following capabilities:

- Access Dropbox files by using semantic search.
- Preserve your organization’s access control lists (ACLs).
- Configure custom crawl frequencies.
- Build workflows using this connection and plugins available in Microsoft Copilot Studio.

The Dropbox connector has the following limitations:

- Folders, comments, and replies aren't indexable.
- Only files located in team member folders and team folders are supported.
- Content in Dropbox Paper isn't crawled.
- Content in Google documents (Docs, Sheets, Slides) isn't crawled.
- Access control lists (ACLs) based on shared file links aren't supported.

## Data types indexed from Dropbox

The Dropbox connector indexes:

- Files in team folders
- Files in shared folders
- Files in private folders

Indexed content appears in Microsoft 365 Copilot responses and Microsoft Search results, based on Dropbox permissions.

## Permissions model and access control

The Dropbox connector enforces the Dropbox permission model. Users only see content they’re authorized to access in Dropbox. During OAuth authorization, the connector requests scopes to:

- View Dropbox files and folders
- View Dropbox sharing settings, group memberships, and activity logs
- View basic accounts and team information

## Next step

> [!div class="nextstepaction"]
> [Deploy the Dropbox connector](dropbox-deployment.md)
