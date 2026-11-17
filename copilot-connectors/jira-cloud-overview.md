---
title: "Jira Cloud connector overview"
description: "Learn about the Jira Cloud Microsoft 365 Copilot connector, its capabilities, limitations, data indexed, permissions model, and how to build agents."
ms.author: lauragra
author: lauragra
manager: calvind
ms.topic: overview
ms.service: copilot-connectors
ms.date: 12/15/2025
ms.localizationpriority: medium
---
# Jira Cloud connector overview

The Jira Cloud Microsoft 365 Copilot connector enables your organization to index Jira Cloud issues and make them searchable in Microsoft 365 experiences, including Microsoft 365 Copilot and Microsoft Search experiences. When you integrate Jira Cloud with Microsoft 365, users can quickly discover issues, projects, and related data, improving productivity and collaboration.

> [!IMPORTANT]
> The connector supports **Jira Cloud-hosted instances** only. Jira Server and Jira Data Center versions aren't supported.

## Why use the Jira Cloud connector to index your data?

The Jira Cloud connector crawls Jira Cloud data and indexes issues (tickets) to allow users to:

- Search Jira issues directly in Microsoft 365 Copilot and Microsoft Search.
- Ask Copilot questions related to project tracking, support queries, or task execution, such as:
  - Find the issue with the mobile app not loading.
  - Look for Jira tasks reported by John to update documentation about API migration.
  - Summarize CP-1234.

The connector uses semantic search to help users find relevant content based on keywords, preferences, and social connections.

The following examples are potential use cases for the Jira Cloud connector:

- Quickly locate Jira issues without leaving Microsoft 365.
- Summarize issue details in Copilot for reporting or decision-making.
- Allow project managers and developers to stay informed about tasks and blockers.

## Build agents with the Jira Cloud connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/copilot-studio-agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that users can use to retrieve information from the Jira Cloud connector.

- **Project tracking**
  - Show all Jira issues assigned to me that are due this week.
  - Summarize the status of project Alpha based on Jira issues.

- **Issue details**
  - Give me the details of issue DESK-101, including priority and assignee.
  - What are the blockers for the API migration task in Jira?

- **Reporting**
  - Generate a summary of all high-priority bugs reported in the last seven days.
  - List Jira tasks created by John in the past month.

- **Collaboration**
  - Find Jira issues that mention "mobile app performance" and share with the team.
  - Show unresolved issues in the customer support project.

## Capabilities

The Jira Cloud connector provides the following capabilities:

- Index Jira Cloud issues across projects.
- Enable natural language queries in Copilot for project and task-related information.
- Support incremental and full crawls for data freshness.
- Provide customizable schema for properties like title, description, status, and assignee.

## Limitations

The Jira Cloud connector has the following limitations:

- The connector doesn't support Jira Server or Jira Data Center.
- Attachments aren't indexed.
- The connector doesn't support the **Any user logged in** application role for granting issue access.

## Data types indexed from Jira Cloud

The connector indexes Jira Cloud issues and their associated metadata, including:

- **Title**
- **Issue description**
- **Issue status**
- **Project name**
- **Created and updated dates**
- **Assignee name**
- **Priority**

Custom fields can also be indexed. If a selected custom field is missing from some issue types, the field is ingested as `NULL`.

## Custom data filters

The Jira Cloud connector includes the following custom data filters for Copilot Search:

- Assignee
- Project

## Permissions model and access control

The connector supports two search permission modes:

- **Everyone**: Indexed data appears in search results for all users.
- **Only people with access to this data source**: Indexed data appears only for users who have access in Jira.

To enable security trimming, the connector requires:

- Jira user email IDs for mapping to Microsoft Entra ID.
- Appropriate Jira permissions, such as:
  - **Browse projects** (mandatory for crawling issues)
  - **Issue-level security permissions** (optional)
  - **Browse users and groups** (optional for security trimming)

## Next step

> [!div class="nextstepaction"]
> [Deploy the Jira Cloud connector](jira-cloud-deployment.md)

