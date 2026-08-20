---
title: "Azure DevOps Wiki connector overview"
ms.author: danielabo
author: danipocket
manager: calvind
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: microsoft-365-copilot-connectors
ms.date: 08/20/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Azure DevOps Wiki Microsoft 365 Copilot connector."
---

# Azure DevOps Wiki connector overview

The Azure DevOps Wiki Microsoft 365 Copilot connector enables your organization to index wikis from its Azure DevOps Services instance—including project wikis and code wikis—into Microsoft 365. By using this index, users can search and retrieve wiki content directly in Microsoft Search and Microsoft 365 Copilot.

## Why use the Azure DevOps Wiki connector to index your data?

Organizations benefit from this connector by surfacing Azure DevOps wiki content in everyday Microsoft 365 experiences. Common use cases include:

- Unified wiki search across Azure DevOps projects within Microsoft 365.
- Faster onboarding by surfacing project documentation in Copilot.
- Cross-team knowledge sharing for engineering, product, and support teams.
- Searchable institutional knowledge stored in code wikis and project wikis.

## Build agents with the Azure DevOps Wiki connector

Developers can use this connector as a knowledge source in declarative agents built with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following table lists examples of prompts that users can use to retrieve information from the Azure DevOps Wiki connector.

| Role/Department | Example prompt |
|-----------------|----------------|
| Software Engineer | Find the architecture decision records in the Fabrikam project wiki. |
| Project Manager | Summarize the release process documentation from the Contoso wiki. |
| New Hire | What does the onboarding guide say about setting up my dev environment? |
| Support Engineer | Show me the troubleshooting runbook for the payment service from the wiki. |
| Technical Writer | List all wiki pages updated in the last month for the Mobile App project. |

## Azure DevOps Wiki connector capabilities and limitations

The Azure DevOps Wiki connector allows you to:

- Index project wikis and code wikis from Azure DevOps into Microsoft 365.
- Ask natural-language questions about project wikis and code wikis in Copilot.
- Use [semantic search in Copilot](/microsoftsearch/semantic-index-for-copilot) to find relevant content based on keywords, personal preferences, and social connections.

The Azure DevOps Wiki connector has the following limitations:

- Supports only Azure DevOps Services (cloud); doesn't support Azure DevOps Server 2019, TFS 2018, TFS 2017, TFS 2015, or TFS 2013.
- Indexes only one Azure DevOps organization per connection.

## Custom data filters

The Azure DevOps Wiki connector includes the following custom data filters for Copilot Search:

- Area Path
- Assigned to

## Data types indexed from Azure DevOps Wiki

The Azure DevOps Wiki connector indexes the following properties. The table lists the properties that are selected by default.

| Property | Semantic label | Description | Schema attributes |
|----------|----------------|-------------|-------------------|
| Authors | Authors | People who participated or collaborated on the item | Retrieve |
| Content | Content | The content body of the wiki | Search |
| IconUrl | IconUrl | Icon URL that represents the wiki | Retrieve |
| LastPublishedAuthorEmail | Last modified by | | Retrieve |
| LastPublishedDate | Last modified date time | Date and time the item was last modified | Retrieve |
| Organization | | | Retrieve |
| Project | | | Retrieve |
| ProjectId | | | Retrieve |
| RemoteURL | url | The URL of the wiki in the data source | Retrieve |
| Title | Title | The title of the wiki page | Search, Retrieve |
| Version | | | Retrieve |
| WikiId | | | Retrieve |
| WikiIdentifier | | | Retrieve |

The following properties are available but not selected by default: CommitId, GitItemPath, isParentPage, Path, WikiType.

## Permissions model and access control

Admins can configure access control as:

- **Everyone**: All users can see the indexed data.
- **Only people with access**: Only users with Azure DevOps permissions can see the indexed data.

Microsoft Entra ID handles identity mapping. Full crawls reflect group membership changes.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Azure DevOps Wiki connector](azure-devops-wiki-deployment.md)
