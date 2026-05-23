---
ms.date: 05/20/2026
title: "Troubleshoot issues with the DataStax connector (preview)"
ms.author: kailiang
author: Kai-Cloud
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Find troubleshooting information for the DataStax Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the DataStax connector (preview)

The DataStax Microsoft 365 Copilot connector integrates DataStax Astra DB collections into Microsoft 365, enabling Copilot and Microsoft Search to surface database records directly within apps like Teams, Outlook, and SharePoint.

This article provides troubleshooting information for common errors that you might encounter when you deploy the DataStax connector.

[!INCLUDE [connector-preview-access](includes/connector-preview-access.md)]

## DataStax connector troubleshooting

You might encounter the following errors when you deploy the DataStax connector or when the connector indexes data.

| Error or issue | Possible cause | Recommended action |
| --- | --- | --- |
| **The request is malformed or incorrect** | Incorrect DataStax API Endpoint format. | Verify that you're using the correct API Endpoint format: `https://<your-database-id>-<region>.apps.astra.datastax.com`. Check that the database ID and region are correct. |
| **Unable to reach the DataStax service** | Incorrect API Endpoint or network connectivity issue. | Verify that the API Endpoint is correct. Check that your network allows outbound connections to DataStax Astra DB endpoints. Verify that the database is active in your DataStax account. |
| **Database ID not found** | Incorrect database ID entered during configuration. | Verify that the database ID matches the ID shown in your DataStax Astra DB database overview. The database ID is case-sensitive. |
| **Invalid credentials detected** | Incorrect or expired application token. | Verify that the complete application token starting with `AstraCS:...` is copied without truncation. Generate a new token if the current one has expired. |
| **The client doesn't have permission to perform the action** | Application token doesn't have sufficient permissions. | Verify that the application token has at least **Read Only User** permissions in DataStax Astra DB. Check that the token has access to all collections you want to index. |
| **Authentication token format invalid** | Application token is truncated or contains extra characters. | Verify that the complete application token is copied without any spaces, line breaks, or additional characters. |
| **No items indexed** | Database has no collections, collections are empty, or the connector doesn't have access. | Verify that your DataStax Astra DB database contains collections with records. Check that the application token has read access to the collections. |
| **Partial data indexed** | The application token doesn't have access to all collections. | Verify that the application token has read permissions for all collections you want to index. Review the connector logs for specific errors about inaccessible collections. |
| **Crawl failed with API rate limit error** | DataStax API rate limits exceeded. | Reduce the crawl frequency in the connector settings. Contact DataStax support if rate limits are consistently exceeded. |
| **Users see records they shouldn't have access to** | Access permissions set to **Everyone** in connector configuration. | Change the access permissions setting to **Only people with access to this data source** in the connector configuration. |
| **Users don't see records they should have access to** | Identity mapping between DataStax and Microsoft Entra ID is incorrect. | Verify that user email addresses in DataStax match Microsoft Entra ID user principal names (UPNs). If they don't match, configure identity mapping. For more information, see [Map your non-Entra ID identities](map-non-entra-id.md). |
| **Records appear without proper titles or content** | Property mapping configuration issue. | Review the property mappings in the connector settings. Verify that the **Title** and **Content** properties are correctly mapped. |
| **Search results don't include expected database records** | Collections not included in indexing scope or search properties not configured. | Verify that all required collections are accessible to the application token. Check that searchable properties are correctly configured. Review the crawl history. |

## Related content

- [DataStax connector overview](datastax-overview.md)
- [Deploy the DataStax connector](datastax-deployment.md)
