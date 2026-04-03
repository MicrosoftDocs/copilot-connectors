---
ms.date: 10/08/2019
title: "Troubleshooting the Azure SQL and Microsoft SQL Server connectors."
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Troubleshooting the Azure SQL and Microsoft SQL Microsoft 365 Copilot connectors."
---

# Troubleshooting the Azure SQL and Microsoft SQL connectors

The following are common errors observed while configuring the connectors, or during crawling, and their possible reasons.

| Configuration step | Error message | Possible reasons |
|:------------ |:----------- |:------------ |
| Full crawl | `Error from database server: A transport-level error has occurred when receiving results from the server.` | Arises due to network issues. It is recommended to check network logs using [Microsoft network monitor](https://www.microsoft.com/download/details.aspx?id=4865) and reach out to Microsoft customer support. |
| Full crawl | `Column column_name returned from full crawl SQL query contains non-alphanumeric character` | Nonalphanumeric characters (like underscores) are not allowed in column names in the SELECT clause. Use aliases to rename columns and remove nonalphanumeric characters (Example - SELECT column_name AS columnName). |

If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).

