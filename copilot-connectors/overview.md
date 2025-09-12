---
title: "Microsoft 365 Copilot connectors overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.audience: Admin
ms.topic: overview
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Get an introduction to Microsoft 365 Copilot connectors, how they enhance Copilot, Copilot Search, and Microsoft Search experiences, and how they work with Copilot extensibility solutions."
ms.date: 09/09/2025
---

# What are Microsoft 365 Copilot connectors?

Microsoft 365 Copilot connectors enable your organization to bring external data into the intelligent experiences within Microsoft 365. Copilot connectors index content from external systems into Microsoft Graph and make it accessible search experiences and  AI-powered tools like Microsoft 365 Copilot, Copilot Search, and Microsoft Search.

By using connectors, you can surface information from across apps and data silos in a unified experience—whether in search results or Copilot answers—while maintaining the source system’s permissions. Connectors help bridge content silos and expand the knowledge base available to Microsoft 365.

## Key benefits of Copilot connectors

Copilot connectors provide the following key benefits:

- **Unified search** - External data appears alongside your emails, files, and SharePoint content. Users can search once in Microsoft 365 and get results from all connected sources.

- **More complete Copilot answers** - Copilot can retrieve and reason over all relevant company information—including content from systems like Salesforce or Confluence—when answering questions or performing tasks.

- **Security and compliance** - Connectors respect the source system's access controls. Only authorized users can view or use external content. After the data is indexed, it benefits from Microsoft 365's security, privacy, and compliance standards.

## How Copilot connectors work

A Copilot connector defines a connection to an external data source and syncs content into Microsoft 365. It uses the Microsoft Graph connectors API to ingest items into the Microsoft Graph index. Each item includes content, metadata (like title and URL), and an access control list (ACL) that enforces permissions.

After the content is ingested:

- **Unified index** - The item becomes part of your organization’s cloud search index. It's full-text searchable and processed by semantic indexing AI for relevance.

- **Permission-based filtering** - Search and Copilot only show items to users who have access in the source system.

- **Continuous sync** - Connectors periodically check for changes. New, updated, or deleted content is reflected in the index. Admins can configure sync frequency and trigger full crawls as needed.

Microsoft hosts the indexing pipeline in the cloud for most connectors. After setup, the process is automated. External content is stored securely in your tenant, and users only see what they're allowed to access.

## Prebuilt and custom connectors

Microsoft offers over 100 prebuilt connectors for popular services, including:

- **File sharing and content management** - Box, Dropbox, Google Drive, Confluence, MediaWiki, network file shares.

- **Enterprise apps and databases** - Salesforce, ServiceNow, Dynamics 365, Azure services, SQL/Oracle databases, SAP.

- **Other platforms** - Workday, Zendesk, Jira, and more.

To use a prebuilt connector, select the connector in the Microsoft 365 admin center, provide credentials and configuration details, and the Microsoft connector service handles the rest. Microsoft or certified partners maintain and update these connectors regularly.

If no prebuilt connector exists for your system, you can build a custom connector by using the [Microsoft 365 Agents Toolkit](/microsoft-365-copilot/extensibility/build-your-first-connector) or the [Microsoft Graph connectors API](/graph/connecting-external-content-connectors-api-overview). Building a custom connector requires a developer to define a schema, register the connection in Microsoft Entra ID, and write code to pull and push data.

For on-premises sources, you can use the [Graph Connector Agent]() to securely index local content.

Custom connectors offer flexibility but require maintenance. Use prebuilt connectors when possible, and reserve custom development for unique or critical sources.

## Microsoft 365 Copilot and connectors

The conversational Copilot Chat experience in Microsoft 365 Copilot, Teams, Outlook, and other Microsoft 365 apps use connector content to respond to user queries. When users ask questions or request help, Copilot retrieves data from internal and external sources.

For example, the user query "Give me a summary of the Contoso deal" might return details from a Salesforce record if that system is connected. Copilot cites the source and provides a quick summary without requiring the user to open Salesforce.

Connectors make Copilot Chat a more powerful assistant, capable of answering questions beyond Microsoft 365 content, via the following key features:

- **Multiturn conversation** - Follow-up questions stay in context and can pull from multiple connectors.

- **Content previews and links** - Users can open referenced items for more detail.

- **Read-only by default** - Copilot Chat can't write back to external systems unless the experience is extended with action connectors or plugins.

- **Security enforced** - Users only see content they're authorized to access.

## Copilot Search and connectors

[Microsoft 365 Copilot Search](/copilot/microsoft-365/microsoft-365-copilot-search) is an AI-powered enterprise search experience that helps users quickly find relevant information across Microsoft 365 and beyond. Copilot Search acts as a universal search layer that integrates seamlessly into the Microsoft 365 Copilot app across desktop, web, and mobile platforms. It automatically includes indexed connector content when generating responses—no extra setup required.

For example, if a user asks, "How do I file an expense report?", Copilot Search looks across Microsoft 365 and connected systems. If a relevant page is found in an internal finance wiki (via a connector), Copilot uses it to generate a concise answer with a citation.

Copilot connectors enhance the Copilot Search experience by providing the following benefits:

- **Unified indexing** - External data is indexed alongside Microsoft 365 content, enabling a single, comprehensive search experience.

- **Personalized results** - Signals from Microsoft Graph and connector-ingested data help tailor results based on user roles, behaviors, and organizational relationships.

- **Copilot extension** - A browser add-on that enhances search relevance by incorporating signals from external work-related sites—without tracking general browsing activity.

The extensive connector ecosystem makes Copilot Search an enterprise-wide knowledge discovery platform that helps users find what they need, when they need it—no matter where the data lives.

## Microsoft Search and connectors

After connectors are set up, users discover external content through Microsoft Search across Office.com, SharePoint, Outlook, Teams, Bing (work account), and other apps. Connectors enhance the Microsoft Search experience with the following features:

- **Integrated results** - External items appear in the **All** results view alongside internal content. Each result is labeled with its source (for example, Confluence VPN Access Policy) and opens in its native app.

- **Verticals and filters** - Admins can create custom search verticals (tabs) for specific connectors. Users can refine results by source or metadata properties.

- **Result display** - Connector results show a title, snippet, and metadata. Admins can customize layouts, but the default display is clean and consistent.

- **Contextual suggestions** - Connector content appears in features like Microsoft Editor or messaging extensions, helping users find and use external knowledge without switching apps.

Search relevance algorithms rank external and internal results equally, based on query match, freshness, and user context.

## Custom agents and extensibility

Connectors are essential knowledge sources for custom agents built with [Copilot Studio](/microsoft-365-copilot/extensibility/copilot-studio-experience) or the [Microsoft 365 Agents Toolkit](/microsoft-365-copilot/extensibility/build-declarative-agents). These agents are tailored to specific domains or tasks, such as IT help desk or sales support.

Connectors enhance agents for Copilot with the following features:

- **Domain-specific knowledge** - Agents can use Copilot connectors to answer questions from relevant sources.

- **Action-taking capability** - Agents can be extended with Power Platform connectors or API plugins to perform tasks (for example, reset passwords, create tickets).

Admins control which connectors and actions each agent can use to ensure governance and security.

For example, a Sales agent might use a Salesforce connector for data and a Power Platform connector to update records—all within a conversational interface.

## Related content

- [Connectors gallery](connectors-gallery.md)
- [Deploy connectors in the admin center](deployment-overview.md)