---
title: "DataStax connector troubleshooting"
ms.author: danielabo
author: danipocket
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 08/15/2025
ms.localizationpriority: medium
description: "Find troubleshooting information for the DataStax Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the DataStax connector

The DataStax connector indexes records from your DataStax Astra DB collections into Microsoft 365 so users can search and retrieve database data directly in Copilot and Microsoft Search. This article provides troubleshooting information for common issues you might encounter when you deploy or manage the connector.

[!INCLUDE [conector-preview-access](includes/connector-preview-access.md)]

## DataStax connector troubleshooting

The following table lists common errors and recommended troubleshooting steps.

| Issue | Description | Troubleshooting steps |
|-------|-------------|------------------------|
| Authentication fails | The application token might be invalid, expired, or lack the required permissions. | - Confirm that the application token was generated with at least "Read Only User" permissions.<br>- Verify the token starts with "AstraCS:..." and is complete.<br>- Generate a new application token if the current one has expired.<br>- Ensure the token has access to all collections you want to index. |
| API Endpoint connection fails | The DataStax API Endpoint might be incorrect or inaccessible. | - Verify the API Endpoint format: `https://<your-database-id>-<region>.apps.astra.datastax.com`.<br>- Confirm the database ID is correct and matches your Astra DB instance.<br>- Check that your organization's firewall allows outbound connections to DataStax.<br>- Verify the database is active and not paused or terminated. |
| Records not appearing in Copilot or Search | Only records accessible with the configured token can be indexed. Missing permissions or incorrect collections prevent ingestion. | - Validate that the application token has read access to the target collections.<br>- Confirm the keyspace and collection names are correctly configured.<br>- Check that the database contains records in the specified collections.<br>- Review the connector status in the admin center for crawl errors. |
| Incomplete indexing | Some collections or records might not be indexed if permissions are restricted. | - Verify the application token has access to all required collections.<br>- Check for any collection-level access restrictions in DataStax.<br>- Review the connector logs in the admin center for specific errors.<br>- Ensure the database connection remains stable during crawling. |
| Connector fails immediately after configuration | Misconfiguration of the API Endpoint, database ID, or application token can cause early failures. | - Make sure that the API Endpoint includes the complete URL format.<br>- Validate the database ID matches the ID shown in your Astra DB overview.<br>- Confirm the application token is correctly copied without truncation.<br>- Check that all required fields are filled during connector setup. |
| Slow crawl performance | Large databases or network issues can impact crawl speed. | - Verify your network connection to DataStax is stable.<br>- Check if the database is experiencing performance issues.<br>- Consider limiting the scope of indexed collections if the database is very large.<br>- Review the crawl frequency settings and adjust if necessary. |
| Identity mapping issues | Users might not see results if identity mapping between DataStax and Microsoft Entra ID is incorrect. | - Confirm that user email IDs in DataStax match the User Principal Name (UPN) in Microsoft Entra ID.<br>- If emails don't match, configure a custom mapping formula.<br>- Verify that the identity mapping option (Microsoft Entra ID or Non-Microsoft Entra ID) is correctly selected.<br>- Test identity mapping with a known user account. |

## Related content

- [DataStax connector overview](datastax-connector-overview.md)
- [Deploy the DataStax connector](datastax-connector-deployment.md)
- [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support)
