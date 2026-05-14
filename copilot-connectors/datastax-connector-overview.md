---
title: "DataStax connector overview"
ms.author: kailiang
author: Kai-Cloud
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 08/15/2025
ms.localizationpriority: medium
description: "Learn about the capabilities, limitations, and use cases for the DataStax Microsoft 365 Copilot connector."
---

# DataStax connector overview

The DataStax Microsoft 365 Copilot connector enables your organization to index records in your DataStax Astra DB collections. After you configure the connector and index content from the DataStax databases, users can search for those items in Microsoft 365 Copilot.

[!INCLUDE [conector-preview-access](includes/connector-preview-access.md)]

## Why use the DataStax connector to index your data?

Organizations benefit from this connector by surfacing DataStax Astra DB data in everyday Microsoft 365 experiences. Common use cases include:

- Unified access to vector database content across the organization.
- Natural-language queries to retrieve insights from database collections.
- Knowledge retention through searchable database records.
- Enhanced decision-making with AI-powered search over your DataStax data.

## Build agents with the DataStax connector

Developers can use this connector as a knowledge source in declarative agents built with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following table lists examples of prompts that users can use to retrieve information from the DataStax connector.

| Role/Department           | Example prompt                                                                 |
|---------------------------|--------------------------------------------------------------------------------|
| Business Analyst          | Recommend a movie based on review texts and my interests.                      |
| Content Manager           | Summarize the review text on movie Paa.                                        |
| Marketing Lead            | Identify the movie that generates heated discussions in our database.          |
| Product Manager           | Show me the top-rated items from the product reviews collection.               |
| Data Analyst              | What are the most common themes in customer feedback from our reviews?         |

## DataStax connector capabilities and limitations

The DataStax connector allows users to:

- Index records in DataStax Astra DB collections.
- Ask natural-language questions about database records in Copilot.
- Use semantic search to find relevant records based on context.

The DataStax connector has the following limitations:

- Doesn't index Non-Vector DB.
- Doesn't index Langflow.
- Doesn't support search verticals.

## Data types indexed from DataStax

The DataStax connector indexes the following properties:

- Collection name
- Record content
- Record ID
- Keyspace
- Title (created by combining collection name and record ID)
- Icon URL

These properties are searchable and retrievable in Copilot and Microsoft Search.

## Permissions model and access control

Admins can configure access control as:

- **Everyone** - All users in the organization can see indexed data in search results.
- **Only people with access to this data source** - Only users who have access to content in the DataStax data source can see indexed data in search results. Access permissions are mapped using Microsoft Entra IDs.

## Related content

- [Deploy the DataStax connector](datastax-connector-deployment.md)
- [Troubleshoot issues with the DataStax connector](datastax-connector-troubleshooting.md)
