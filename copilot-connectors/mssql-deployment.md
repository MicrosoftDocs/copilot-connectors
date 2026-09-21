---
title: "Deploy the Azure SQL and Microsoft SQL Server connectors"
description: "Learn how to deploy and customize the Azure SQL and Microsoft SQL Server Microsoft 365 Copilot connectors in the Microsoft 365 admin center."
author: danipocket
ms.author: danielabo
manager: calvind
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: microsoft-365-copilot-connectors
ms.date: 08/17/2026
ms.localizationpriority: Medium
---

# Deploy the Azure SQL and Microsoft SQL Server connectors

This article describes how to deploy the Azure SQL and Microsoft SQL Server Microsoft 365 Copilot connectors, which index records from an on-premises SQL Server database or a database hosted in your Azure SQL instance.

Before you begin, ensure the database admin completes the steps in [Set up the Azure SQL and Microsoft SQL Server services](mssql-admin-setup.md).

## Prerequisites

Complete the following tasks before you create the connection.

| Task | Role | Applies to |
|---|---|---|
| Install and configure the Microsoft Graph connector agent | Server or infrastructure admin | Microsoft SQL Server only |
| Create a service account with read permissions | Database admin | Both connectors |
| Register an app in Microsoft Entra ID and generate a client secret | Microsoft Entra admin | Azure SQL only |
| Add the registered app to the database and grant db_datareader | Database admin | Azure SQL only |
| Add Microsoft 365 client IP ranges to the firewall | Database or network admin | Azure SQL only |

In addition:

- You must be the **AI administrator** for your organization's Microsoft 365 tenant.
- **Install the Microsoft Graph connector agent** (only applicable for the Microsoft SQL Server Copilot connector). To access your Microsoft SQL Server, you must install and configure the connector agent. See [Install the Microsoft Graph connector agent](connector-agent.md) to learn more.
- **Service account**. To connect to your SQL database and allow the Copilot connector to update records regularly, you need a service account with read permissions granted to the service account.

## Deploy the connector

To add the Azure SQL or Microsoft SQL Server connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, select **Copilot** > **Connectors**.
1. Select the **Gallery** tab.
1. From the list of available connectors, select **Azure SQL** or **Microsoft SQL Server**.

### Set display name

The display name identifies each citation in Copilot, so users can easily recognize the associated file or item. The display name also signifies trusted content, and acts as a [content source filter](/microsoftsearch/custom-filters#content-source-filters). A default value is present for this field, but you can customize it to a name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

### Set instance URL

To connect to your SQL data, you need your SQL server address and database name.

### Choose authentication type

#### Microsoft Entra ID OpenID Connect (OIDC)

The Azure SQL Copilot connector only supports Microsoft Entra ID OpenID Connect (OIDC) authentication to connect to the database. Enter the application (client) ID and client secret of the app that you registered during service setup. To create these values, see [Set up the Azure SQL and Microsoft SQL Server services](mssql-admin-setup.md).

#### Windows authentication

For the Microsoft SQL Server Copilot connector, the connection is made through the Microsoft Graph connector agent. If you use Windows authentication, the user with which you're trying to sign in needs to have interactive sign-in rights to the machine where the connector agent is installed. For more information, see [login policy management](/windows/security/threat-protection/security-policy-settings/allow-log-on-locally#policy-management).

> [!NOTE]
> The available authentication options depend on whether you're configuring Azure SQL or Microsoft SQL Server.

### Roll out

Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before expanding the rollout to a broader audience. To learn more about limited rollout, see [staged rollout](staged-rollout.md).

## Customize settings (optional)

### Customize user settings

#### Access permissions

Use the **Only people with access to this data source** option to restrict access to users or groups as selected in the full crawl query, or override it to make your content visible to **Everyone**.

#### Map identities

Choose the various access control (ACL) columns that specify the access control mechanism, and select the column name you specified in the full crawl SQL query. Deny takes precedence over allow permissions.

Each ACL column should be a multivalued column. Separate multiple ID values with separators such as a semicolon (;), comma (,), or other characters. Specify the separator in the **value separator** field.

The following ID types are supported for use as ACLs:

- **User Principal Name (UPN)**: a UPN is the name of a system user in an email address format, such as `john.doe@domain.com`, and consists of the username, the @ separator, and the domain name. Security groups in Microsoft Entra don't have a UPN and can't be mapped with this option.
- **Microsoft Entra ID**: in Microsoft Entra ID, every user or group has an object ID that looks something like `e0d3ad3d-0000-1111-2222-3c5f5c52ab9b`.
- **Active Directory (AD) Security ID**: in an on-premises AD setup, every user and group has an immutable, unique security identifier that looks something like `S-1-5-21-3878594291-2115959936-132693609-65242`.

### Customize content settings

#### Query string

To search your database content, you must specify SQL queries when you configure the connector. These SQL queries need to name all the database columns that you want to index (source properties), including any SQL joins that you need to perform to get all the columns. To restrict access to search results, you must specify access control lists (ACLs) within the SQL queries.

**Full crawl query (required)**

The full crawl query selects all the columns or properties that need to be presented in Microsoft 365 Copilot or Search, and optionally the ACL columns that restrict access to specific users or groups. To get all the columns that you need, you can join multiple tables.

Select data columns as shown in this example `SELECT` clause:

```sql
SELECT orderId, orderTitle, orderDesc, allowedUsers, allowedGroups, deniedUsers, deniedGroups, createdDateTime, isDeleted
```

The SQL Copilot connectors don't allow column names with nonalphanumeric characters in the `SELECT` clause. Remove any nonalphanumeric characters from column names by using an alias, such as `SELECT column_name AS columnName`.

**Watermark (required)**

To prevent overloading the database, the connector batches and resumes full crawl queries by using a full crawl watermark column. The connector uses the value of the watermark column to fetch each subsequent batch and resume querying from the last checkpoint.

Create query snippets for watermarks as shown in these examples:

- `WHERE (CreatedDateTime > @watermark)`. Use the reserved keyword `@watermark` to cite the watermark column name. If the sort order of the watermark column is ascending, use `>`; otherwise, use `<`.
- `ORDER BY CreatedDateTime ASC`. Sort on the watermark column in ascending or descending order.

Specify the data type of the watermark column so the connector can fetch the first batch of rows. For example, if `CreatedDateTime` is the watermark column, the data type is `DateTime`, and the first query fetches the first N rows by using `CreatedDateTime > January 1, 1753 00:00:00`, the minimum value of the DateTime data type. After the first batch is fetched, the highest value of `CreatedDateTime` returned in the batch is saved as the checkpoint when rows are sorted in ascending order.

**Incremental crawl query (optional)**

Provide a SQL query to run an incremental crawl of the database. With this query, the connector determines any changes to the data since the last incremental crawl. As in the full crawl, select all columns for which you want the **Query**, **Search**, **Retrieve**, or **Refine** options, and specify the same set of ACL columns that you specified in the full crawl query. The incremental crawl query resembles the full crawl query, except that the watermark column is typically a modified-date column such as `ModifiedDateTime`.

**Soft delete (optional)**

In a SQL record system, a soft delete is a technique where, instead of physically removing a record from a database, you mark it as deleted by setting a specific flag or column. To delete soft-deleted rows from the index during the incremental crawl, specify the soft-delete column name and the value that indicates the row is deleted.

#### Manage properties

The SQL connector picks up all columns specified in the full crawl SQL query as source properties for ingestion. In this step, you define the search schema for your content by defining the search annotations - **Search**, **Retrieve**, **Query**, and **Refine** - for the selected source properties, and by assigning semantic labels and aliases to enhance search relevance. To learn more about search schema, see the documentation on [guidelines for manage properties](deployment-overview.md#guidelines-for-manage-properties).

Because the connector indexes the columns returned by your full crawl query, there are no default properties to map. Review the generated source properties and set the appropriate **Search**, **Retrieve**, **Query**, and **Refine** annotations and semantic labels for your scenario.

### Customize sync intervals

The refresh interval determines how often your data syncs between the data source and the Copilot connector index. By default, incremental crawl runs every 15 minutes if you configure it, and full crawl runs every day. If needed, adjust these schedules to fit your data refresh needs.

You're now ready to create the connection for Azure SQL or Microsoft SQL Server. Select **Create** to publish your connection and index data from your database.

## Related content

- [Azure SQL and Microsoft SQL Server connectors overview](mssql-overview.md)
- [Troubleshoot the Azure SQL and Microsoft SQL Server connectors](mssql-troubleshooting.md)
- [Deploy a Microsoft 365 Copilot connector](deployment-overview.md)
