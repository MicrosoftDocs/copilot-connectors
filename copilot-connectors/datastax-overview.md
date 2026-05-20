---
ms.date: 05/20/2026
title: "DataStax Copilot connector overview (preview)"
ms.author: kailiang
author: Kai-Cloud
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Learn about the capabilities, limitations, and use cases for the DataStax Copilot connector."
---

# DataStax Copilot connector overview (preview)

The DataStax Microsoft 365 Copilot connector integrates DataStax Astra DB collections into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface database records directly within apps like Teams, Outlook, and SharePoint.

When you configure the DataStax connector for your organization and index content from DataStax Astra DB collections, users can search for database records in Microsoft Search, Microsoft 365 Copilot, and Copilot Search. The DataStax connector enables improved knowledge discovery, faster data retrieval, and enhanced decision-making based on vector database content.

[!INCLUDE [connector-preview-access](includes/connector-preview-access.md)]

## Why use the DataStax connector to index your data?

Organizations that use DataStax Astra DB for vector database management often face challenges accessing database content within their daily workflows. The DataStax Copilot connector addresses these problems by integrating Astra DB collections into Microsoft 365. This allows employees to surface database records through Copilot, Copilot Search, and Microsoft Search – in everyday apps like Teams, Outlook, or SharePoint – without leaving their flow of work. The result is more efficient data discovery and improved use of organizational knowledge stored in vector databases.

The DataStax Copilot connector provides the following benefits:

- **Accelerates information retrieval** - Users access database records directly within Microsoft 365 apps, reducing time spent switching between platforms and searching multiple systems.
- **Enhances decision-making** - Natural language queries against vector databases enable faster access to relevant data insights, supporting more informed and timely decisions.
- **Improves knowledge discovery** - Semantic search capabilities help users find contextually relevant database records even when they don't know exact search terms.
- **Streamlines workflows** - Integration with Copilot enables users to ask questions about database content in natural language, simplifying complex database queries.
- **Supports AI-powered applications** - Developers can build agents and applications that leverage DataStax collections as knowledge sources, extending the value of vector database content.
- **Maintains data security** - The connector enforces access controls to ensure database records are only visible to authorized users.

### Use cases

The following table lists common use cases for the DataStax connector.

| Department/role | Use case | Business benefit |
| --------------- | -------- | ---------------- |
| Product management | Recommend a product based on customer review texts and feature preferences stored in our database. | Surface product recommendations grounded in customer feedback data from vector databases, improving product strategy. |
| Marketing | Summarize sentiment trends from customer reviews in the DataStax collection for product X. | Generate marketing insights by analyzing customer sentiment patterns stored in vector databases. |
| Data science | Identify the most discussed topics in our customer feedback collection. | Discover trends and patterns in large datasets using natural language queries against vector databases. |
| Customer success | Find similar customer inquiries to this support ticket based on historical data. | Improve support response times by leveraging semantic similarity search across historical support data. |
| Content management | Show me all content items with similar themes to this document in our content database. | Enhance content discovery and reuse by finding semantically related items across large content collections. |
| Research | What are the most common patterns in our research findings database? | Accelerate research insights by querying vector database collections containing research data and findings. |

## Build agents with the DataStax connector

Developers can use this connector as a knowledge source in declarative agents they build with [Microsoft Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that agent builders can use to help their users retrieve information from DataStax Astra DB.

**Product management/Business analysis**

- Recommend a movie based on review texts and my interests from the movie reviews collection.
- Summarize the review text for movie Paa in the reviews database.
- Show me the top-rated items from the product reviews collection based on sentiment analysis.

**Data analysis/Research**

- Identify the movie that generates heated discussions based on review volume and sentiment.
- What are the most common themes in customer feedback stored in our reviews collection?
- Find patterns in user behavior data from the analytics collection for Q4.

**Marketing/Content**

- Show me content items similar to this document from our content database.
- Identify trending topics in customer reviews for use in marketing campaigns.
- What products receive the most positive sentiment in our feedback database?

**Customer success/Support**

- Find similar customer support cases to this inquiry based on historical data.
- Summarize common issues reported for product X from our support database.
- Show me resolution patterns for issues similar to this support ticket.

## Connector capabilities and limitations

The DataStax connector has the following key capabilities:

- **Indexes vector database collections** – Crawls DataStax Astra DB collections and indexes records for search and retrieval.
- **Integrates with Copilot** – Enables Copilot and Microsoft Search to find and use database records. Users can ask questions in natural language and get answers that include information from DataStax collections, with reference links back to the source.
- **Supports semantic search** – Leverages vector database capabilities to provide contextually relevant search results based on semantic similarity.
- **Configurable access control** – Admins can control whether indexed data is visible to everyone or restricted based on access permissions.
- **Flexible property mapping** – Supports customization of indexed properties including collection name, keyspace, record content, and custom titles.

The DataStax connector has the following limitations:

- **Supports Astra DB only** – This connector works with DataStax Astra DB (cloud-based vector database). It doesn't support non-vector databases or on-premises DataStax instances.
- **Preview status** – This connector is currently in preview and may have limited availability. Preview features are subject to change.
- **Full crawl only** – The connector only supports full crawl operations. Incremental crawl is not available, so all database records are re-indexed during each crawl cycle.
- **No Langflow support** – The connector doesn't index Langflow workflows or components.
- **Limited search vertical support** – The connector doesn't support search verticals, meaning results appear in the general search experience rather than dedicated search categories.

## Data types indexed from DataStax

The DataStax connector indexes database records so they can be used in Copilot, Copilot Search, and Microsoft Search. The connector crawls collections from DataStax Astra DB and indexes the following data.

| DataStax content type | Indexed and surfaced in Copilot and search |
| ----------------------- | ------------------------------------------ |
| **Collections** | Database collections containing records. The connector indexes collection metadata including names and keyspaces. |
| **Records** | Individual records within collections. The connector indexes record content and properties, making them searchable in Copilot responses and search results. |
| **Record metadata** | Record identifiers, collection associations, and custom properties defined in the database schema. |

## Permissions model and access control

You can configure the DataStax connector to control which users can see indexed database records in Copilot responses and search results.

The DataStax connector supports the following permission models:

- **Everyone** – If you choose this option, all indexed DataStax database records appear in search results for all users in your organization. Use this option for non-confidential database content that should be universally accessible.

- **Only people with access to this data source** – If you choose this option, the connector enforces access controls. Only users who have appropriate permissions can see database records in Copilot and Microsoft Search results. The system uses Microsoft Entra ID to map user identities and enforce permissions.

### User identity mapping

The connector maps DataStax user accounts to Microsoft 365 (Entra ID) identities:

- **Automatic mapping** - If DataStax users' emails match their Entra ID UPNs, identity mapping is automatic.
- **Custom mapping** - If email addresses differ, you can provide a mapping rule to map identities in DataStax to identities in Microsoft 365. For more information, see [Map your non-Entra ID identities](map-non-entra-id.md).

This ensures that the system provides appropriate access to DataStax content in responses based on user permissions.

## Next step

> [!div class="nextstepaction"]
> [Deploy the DataStax connector](datastax-deployment.md)
