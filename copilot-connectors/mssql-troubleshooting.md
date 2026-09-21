---
title: "Troubleshoot issues with the Azure SQL and Microsoft SQL Server connectors"
description: "Find troubleshooting information for common errors with the Azure SQL and Microsoft SQL Server Microsoft 365 Copilot connectors."
author: danipocket
ms.author: danielabo
manager: calvind
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: microsoft-365-copilot-connectors
ms.date: 08/17/2026
ms.localizationpriority: Medium
---

# Troubleshoot issues with the Azure SQL and Microsoft SQL Server connectors

The Azure SQL and Microsoft SQL Server connectors index database records from on-premises SQL Server databases and Azure SQL instances into Microsoft 365 Copilot and Microsoft Search. This article provides troubleshooting information for common errors that you might encounter when you deploy the Azure SQL and Microsoft SQL Server connectors.

To verify Azure SQL or Microsoft SQL Server configuration information to help troubleshoot errors, see [Set up the Azure SQL and Microsoft SQL Server services](mssql-admin-setup.md).

## Azure SQL and Microsoft SQL Server connector troubleshooting

| Configuration step | Error message | Possible reasons |
|:---|:---|:---|
| Full crawl | `Error from database server: A transport-level error has occurred when receiving results from the server.` | Arises due to network issues. Check network logs by using [Microsoft Network Monitor](https://www.microsoft.com/download/details.aspx?id=4865) and contact Microsoft customer support. |
| Full crawl | `Column column_name returned from full crawl SQL query contains non-alphanumeric character` | The SELECT clause column names can't contain nonalphanumeric characters, such as underscores. Use aliases to rename columns and remove nonalphanumeric characters (Example: `SELECT column_name AS columnName`). |

## Related content

- [Azure SQL and Microsoft SQL Server connectors overview](mssql-overview.md)
- [Deploy the Azure SQL and Microsoft SQL Server connectors](mssql-deployment.md)
- [Set up the Azure SQL and Microsoft SQL Server services](mssql-admin-setup.md)
