---
title: "ServiceNow Catalog Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: mayanksethi
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 12/09/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the ServiceNow Catalog Microsoft 365 Copilot connector."
---

# ServiceNow Catalog Microsoft 365 Copilot connector overview

The ServiceNow Catalog Microsoft 365 Copilot connector enables your organization to index catalog items from ServiceNow and make them discoverable across Microsoft 365 experiences, including Microsoft 365 Copilot, Copilot Search, and Microsoft Search. By integrating catalog data into Microsoft Graph, users can interact with catalog items using natural language prompts, which improves service request workflows and operational efficiency.

## Why use the ServiceNow Catalog connector to index your data?

The ServiceNow Catalog connector is ideal for organizations that want to surface IT and business service requests in Microsoft 365. Organizations can use the connector to:

- Surface all critical information about hardware, software, or access to services directly in Copilot.
- Reduce time to fulfillment by making catalog items searchable and actionable.
- Enhance visibility into available services across departments such as IT, HR, and Facilities.

### Use cases

Allow your users to ask questions related to your IT services workflows in Copilot, such as:

- Show me details for Elitebook HP laptop.
- What software licenses are available for new employees?
- Show me the available mobile devices for staff.

## Build agents with the ServiceNow Catalog connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Copilot Studio agent builder](/microsoft-365-copilot/extensibility/copilot-studio-agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit). These agents can:

- Answer user questions about catalog items.
- Guide users through service request processes.
- Provide contextual responses based on catalog metadata.

### Agent prompts

The following examples show prompts that agent builders can use to help users retrieve information from ServiceNow Catalog.

| Department | Example Prompts |
| ---------- | --------------- |
| IT | Show me available laptops for new employees. |
| HR | What onboarding services are available?<br>Request ergonomic equipment. |
| Facilities | Request a badge replacement.<br>Schedule a workspace move. |

## ServiceNow Catalog connector capabilities and limitations

The ServiceNow Catalog connector enables users to:

- Perform natural language queries to discover catalog items.
- Search for catalog items using semantic search in Copilot.
- View catalog items based on user criteria permissions, including evaluation of advanced scripts.
- View the ServiceNow URL defined by their organization in Copilot responses.
- View associated catalog form fields (variables) and their choices for enhanced contextual search and responses in Copilot. 

Before you deploy the connector, consider the following limitations:

- Hierarchical permissions aren't supported. This means that catalog category-level user criteria are ignored and only item-level user criteria are considered when permissions for catalog items are evaluated. 
- Attachments and custom widget-based forms aren't indexed.
- The incremental crawl only updates the changed content, not permissions. Permissions are synced only with a full crawl. 
- The connector supports evaluating permissions based only on user criteria or role-based permissions. It doesn't support reading access control list (ACL) rules for items, user criteria, or any table. 

## Data types indexed from ServiceNow Catalog

The connector indexes the following data types:

- **Catalog items** (`sc_cat_item`)

Indexed properties include title, description, category, price, delivery time, owner, and more. 

## Permissions model and access control

The connector supports two access models:

- **Everyone**: Catalog items are visible to all users.
- **Only people with access to this data source**: Visibility is restricted based on ServiceNow user criteria.

Admins can map ServiceNow identities to Microsoft Entra IDs by using default or custom mapping rules. Permissions are evaluated during full crawls and reflected in search results and Copilot responses.

## Next step

> [!div class="nextstepaction"]
> [Deploy the ServiceNow Catalog connector](servicenow-catalog-deployment.md)
