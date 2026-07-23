---
ms.date: 05/20/2026
title: "DataStax connector overview (preview)"
ms.author: kailiang
author: Kai-Cloud
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: microsoft-365-copilot-connectors
ms.localizationpriority: medium
description: "Learn about the capabilities, limitations, and use cases for the DataStax Microsoft 365 Copilot connector."
---

# DataStax connector overview (preview)

The DataStax Microsoft 365 Copilot connector integrates DataStax Astra DB collections into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface database records directly within apps like Teams, Outlook, and SharePoint. When you configure the DataStax connector for your organization and index content from DataStax Astra DB collections, users can search for database records in Microsoft Search, Microsoft 365 Copilot, and Copilot Search.

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

Developers can use this connector as a knowledge source in declarative agents they build with [Microsoft Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

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

## DataStax connector capabilities and limitations

The DataStax connector enables users to:

- Index DataStax Astra DB collections and records for search and retrieval.
- Perform natural language queries in Copilot to retrieve database information.
- Use semantic search to find contextually relevant database records based on similarity.
- Access database content directly within Microsoft 365 apps.
- Configure access controls to restrict visibility based on permissions.

The DataStax connector has the following limitations:

- Supports Astra DB only. This connector works with DataStax Astra DB (cloud-based vector database) and doesn't support on-premises DataStax instances.
- Currently in preview and may have limited availability. Preview features are subject to change.
- Supports full crawl only. Incremental crawl is not available.
- Doesn't index Langflow workflows or components.
- Doesn't support search verticals.

## Data types indexed from DataStax

The DataStax connector indexes database records so they can be used in Copilot, Copilot Search, and Microsoft Search. The connector crawls collections from DataStax Astra DB and indexes the following data.

| DataStax data type | Indexed and surfaced in Copilot and search |
| ------------------ | ------------------------------------------- |
| Collections | Collection metadata including names and keyspaces. |
| Records | Individual records within collections, including record content and properties. |
| Record metadata | Record identifiers, collection associations, and custom properties. |

## Permissions model and access control

The DataStax connector enforces that only users who have access to database content can see it in Copilot responses and search results. Admins can configure the connector to control which users can see indexed database records.

The DataStax connector supports the following permission models:

- **Everyone** – All indexed DataStax database records appear in search results for all users in your organization.
- **Only people with access to this data source** – Only users who have appropriate permissions can see database records in Copilot and Microsoft Search results.

Identity mapping ensures that DataStax users are correctly matched to Microsoft Entra ID accounts. If DataStax user emails match their Entra ID user principal names (UPNs), identity mapping is automatic. If email addresses differ, admins can provide a mapping rule. For more information, see [Map your non-Entra ID identities](map-non-entra-id.md).

## Next step

> [!div class="nextstepaction"]
> [Deploy the DataStax connector](datastax-deployment.md)
