---
title: "Azure SQL and Microsoft SQL Server connectors overview"
description: "Learn how the Azure SQL and Microsoft SQL Server Microsoft 365 Copilot connectors index database records for Microsoft 365 Copilot and Microsoft Search."
author: danipocket
ms.author: danielabo
manager: calvind
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: microsoft-365-copilot-connectors
ms.date: 08/17/2026
ms.localizationpriority: Medium
---

# Azure SQL and Microsoft SQL Server connectors overview

By using the Microsoft SQL Server or Azure SQL Microsoft 365 Copilot connectors, your organization can discover and index data from an on-premises SQL Server database or a database hosted in your Azure SQL instance in the cloud. The connector indexes specified content in Microsoft Search and Microsoft 365 Copilot. To keep the index up to date with source data, it supports periodic full and incremental crawls. By using these SQL connectors, you can also restrict access to search results for certain users.

## Why use the Azure SQL and Microsoft SQL Server connectors to index your data?

Relational databases hold structured business records - orders, cases, inventory, and customer data - that users can't reach from Copilot on their own. Indexing that content brings it into the same answers as the rest of your organization's data.

- Surface structured database records alongside documents, email, and other indexed content in Copilot and Microsoft Search.
- Define what gets indexed with a SQL query, so you reuse existing SQL skills instead of mapping to a fixed schema.
- Preserve row-level access control by mapping the access control columns that already exist in your data.
- Keep the index current without manual effort by scheduling full and incremental crawls.

## Build agents with the Azure SQL and Microsoft SQL Server connectors

After you index your database content, users can ask questions about those records in Copilot, and you can ground custom agents in the same data.

### Example prompts

> [!NOTE]
> Example prompts are illustrative. Validate and adjust them to match your schema and content.

- What's the status of order 12?
- Show me the orders created for Contoso this month.
- Summarize the orders that were opened in the last week.
- Which orders is the sales team responsible for?
- Find records that were created before March 2019 and are still open.

## Azure SQL and Microsoft SQL Server connector capabilities and limitations

The connectors have the following capabilities:

- Index records from your Microsoft SQL Server or Azure SQL database by using a SQL query.
- Specify access permissions for every record with a list of users or groups added in the SQL query.
- Enable your end users to ask questions related to indexed records in Copilot.
- Use [Semantic search in Copilot](/microsoftsearch/semantic-index-for-copilot) to enable users to find relevant content based on keywords, personal preferences, and social connections.

The connectors have the following limitations:

- Microsoft SQL Server Copilot connector: the on-premises database must run SQL Server version 2008 or later.
- Azure SQL Copilot connector: the Microsoft 365 subscription and the Azure subscription that hosts the Azure SQL database must be within the same Microsoft Entra ID. Cross-tenant data flow isn't supported.
- To support high crawl speed and better performance, the connector supports only OLTP (Online Transaction Processing) workloads. OLAP (Online Analytical Processing) workloads that don't execute the provided SQL query within a 40-second timeout aren't supported.
- ACLs support only User Principal Name (UPN), Microsoft Entra ID, or Active Directory (AD) security identifier (SID).
- Indexing rich content inside database columns isn't supported. Examples of such content are HTML, JSON, XML, blobs, and documents referenced by links stored in database columns.

## Data types indexed from Azure SQL and Microsoft SQL Server

The connectors don't index a fixed set of item types. Instead, they index the rows that your full crawl SQL query returns. Every column named in the `SELECT` clause becomes a source property that you can annotate in the search schema.

The following table summarizes the SQL data types that the Microsoft SQL Server and Azure SQL Copilot connectors support, and the indexing data type that each one maps to. To learn more about the data types that Microsoft 365 Copilot connectors support for indexing, see the documentation on [property resource types](/graph/api/resources/externalconnectors-externalconnection).

| Category | Source data type | Indexing data type |
|---|---|---|
| Date and time | date, datetime, datetime2, smalldatetime | datetime |
| Exact numeric | bigint, int, smallint, tinyint | int64 |
| Exact numeric | bit | boolean |
| Approximate numeric | float, real | double |
| Character string | char, varchar, text | string |
| Unicode character strings | nchar, nvarchar, ntext | string |
| String collection | char, varchar, text | stringcollection |
| Other data types | uniqueidentifier | string |

To index a column as a string collection, you need to cast a string to the string collection type. Select **Edit datatypes** in the full crawl settings, select the appropriate columns as **StringCollection**, and specify a delimiter to split the string.

For any other data type that isn't directly supported, cast the column explicitly to a supported data type.

## Permissions model and access control

The SQL Copilot connectors control access at the individual record level. You supply access control lists (ACLs) as columns in the full crawl SQL query, and you map those columns when you configure the connection. If your ACL information is stored in a separate table, join that table in your query.

Four access control mechanisms are available:

- **AllowedUsers**: the list of user IDs who can access the search results for a record.
- **AllowedGroups**: the group of users who can access the search results for a record.
- **DeniedUsers**: the list of users who don't have access to the search results for a record. Everyone else retains access.
- **DeniedGroups**: the groups that don't have access to the search results for a record. Everyone else retains access.

Deny takes precedence over allow. Each ACL column is expected to be a multivalued column, with values separated by a character such as a semicolon (;) or comma (,); you specify that character in the **value separator** field.

The following ID types are supported for use as ACLs:

- **User Principal Name (UPN)**: the name of a system user in an email address format, such as `john.doe@domain.com`. Security groups in Microsoft Entra don't have a UPN and can't be mapped with this option.
- **Microsoft Entra ID**: the object ID that every user or group has in Microsoft Entra ID, such as `e0d3ad3d-0000-1111-2222-3c5f5c52ab9b`.
- **Active Directory (AD) Security ID**: the immutable, unique security identifier that every user and group has in an on-premises AD setup, such as `S-1-5-21-3878594291-2115959936-132693609-65242`.

You can apply these permissions with the **Only people with access to this data source** option, or override them to make your content visible to **Everyone**.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Azure SQL and Microsoft SQL Server connectors](mssql-deployment.md)
