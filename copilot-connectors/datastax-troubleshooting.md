---
ms.date: 05/20/2026
title: "Troubleshoot issues with the DataStax Copilot connector (preview)"
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

# Troubleshoot issues with the DataStax Copilot connector (preview)

The DataStax Microsoft 365 Copilot connector integrates DataStax Astra DB collections into Microsoft 365, enabling Copilot and Microsoft Search to surface database records directly within apps like Teams, Outlook, and SharePoint.

This article provides troubleshooting information for common errors that you might encounter when you deploy the DataStax connector.

[!INCLUDE [connector-preview-access](includes/connector-preview-access.md)]

## DataStax connector troubleshooting

You might encounter the following errors when you deploy the DataStax connector or when the connector indexes data.

| Deployment step | Error or error message | Possible reason | Resolution |
|:------------ |:------------ |:------------ |:------------ |
| Connection settings | The request is malformed or incorrect. | Incorrect DataStax API Endpoint format. | Verify that you're using the correct API Endpoint format: `https://<your-database-id>-<region>.apps.astra.datastax.com`. Check that the database ID and region are correct. For more information, see [Set DataStax API Endpoint](datastax-deployment.md#set-datastax-api-endpoint). |
| Connection settings | Unable to reach the DataStax service. | Incorrect API Endpoint or network connectivity issue. | Verify that the API Endpoint is correct and complete. Check that your network allows outbound connections to DataStax Astra DB endpoints. Verify that the database is active and not paused or terminated in your DataStax account. |
| Connection settings | Database ID not found. | Incorrect database ID entered during configuration. | Verify that the database ID matches the ID shown in your DataStax Astra DB database overview. The database ID is case-sensitive and must be entered exactly as shown. For more information, see [Set DataStax database ID](datastax-deployment.md#set-datastax-database-id). |
| Authentication | Invalid credentials detected. | Incorrect or expired application token entered during authentication setup. | Verify that the application token is copied correctly from your DataStax token details. Make sure that the entire token starting with `AstraCS:...` is copied without truncation. If the token has expired, generate a new application token. For more information, see [Generate an application token in DataStax](datastax-deployment.md#generate-an-application-token-in-datastax). |
| Authentication | The client doesn't have permission to perform the action. | Application token doesn't have sufficient permissions. | Verify that the application token has at least **Read Only User** permissions in DataStax Astra DB. Check that the token has access to all collections you want to index. For more information, see [Generate an application token in DataStax](datastax-deployment.md#generate-an-application-token-in-datastax). |
| Authentication | Your security credentials have expired for this session. | Application token has expired. | Generate a new application token in DataStax Astra DB with the appropriate permissions. Update the connector configuration with the new token. For more information, see [Generate an application token in DataStax](datastax-deployment.md#generate-an-application-token-in-datastax). |
| Authentication | Authentication token format invalid. | Application token is truncated or contains extra characters. | Verify that the complete application token is copied from DataStax without any spaces, line breaks, or additional characters. The token should start with `AstraCS:` and be a continuous string. |
| Crawl | No items indexed. | Database has no collections, collections are empty, or the connector doesn't have access. | Verify that your DataStax Astra DB database contains collections with records. Check that the application token has read access to the collections. Verify that the database is active. Review the connector status in the admin center for specific errors. |
| Crawl | Partial data indexed. | The application token doesn't have access to all collections. | Verify that the application token has read permissions for all collections you want to index. Check for any collection-level access restrictions in DataStax. Review the connector logs in the Microsoft 365 admin center for specific errors about inaccessible collections. |
| Crawl | Crawl failed with API rate limit error. | DataStax API rate limits exceeded. | Reduce the crawl frequency in the connector settings. Contact DataStax support if rate limits are consistently exceeded. Consider limiting the number of collections being indexed if your database is very large. |
| Crawl | Slow crawl performance. | Large database or network latency issues. | Verify that your network connection to DataStax is stable. Check if the database is experiencing performance issues in the DataStax console. Consider adjusting the crawl frequency if performance issues persist. |
| Permissions | Users see records they shouldn't have access to. | Access permissions set to **Everyone** in connector configuration. | Change the access permissions setting to **Only people with access to this data source** in the connector configuration. For more information, see [Customize user settings](datastax-connector-deployment.md#customize-user-settings). |
| Permissions | Users don't see records they should have access to. | Identity mapping between DataStax and Microsoft Entra ID is incorrect. | Verify that user email addresses in DataStax match Microsoft Entra ID user principal names (UPNs). If they don't match, configure a custom identity mapping. For more information, see [Map your non-Entra ID identities](map-non-entra-id.md). |
| Content | Records appear without proper titles or content. | Property mapping configuration issue. | Review the property mappings in the connector settings. Verify that the **Title** and **Content** properties are correctly mapped. For more information, see [Manage properties](datastax-connector-deployment.md#manage-properties). |
| Content | Search results don't include expected database records. | Collections not included in indexing scope or search properties not configured. | Verify that all required collections are accessible to the application token. Check that searchable properties are correctly configured. Review the crawl history to ensure recent crawls completed successfully. |

## Common resolution steps

If you encounter errors with the DataStax connector, try the following general resolution steps:

1. **Verify DataStax Astra DB access**: Make sure that your DataStax Astra DB database is active and accessible.

1. **Check application token configuration**: Review your application token settings to ensure:
   - The token has at least **Read Only User** permissions
   - The complete token is entered without truncation
   - The token hasn't expired
   - The token has access to all collections you want to index

1. **Verify API Endpoint and database ID**: Confirm that you're using the correct API Endpoint format (`https://<your-database-id>-<region>.apps.astra.datastax.com`) and the correct database ID from your DataStax Astra DB overview.

1. **Check network connectivity**: Verify that your network allows outbound HTTPS connections to DataStax Astra DB endpoints.

1. **Review connector logs**: In the Microsoft 365 admin center, review the crawl history and error logs for specific error messages that can help identify the issue.

1. **Verify collection access**: Ensure that the collections you want to index exist in your DataStax Astra DB database and contain records.

1. **Check property mappings**: Review the property mapping configuration to ensure that all required properties are correctly mapped and searchable.

1. **Reconfigure the connector**: If errors persist, consider deleting and recreating the connector with updated configuration settings.

## Contact support

If you have issues or want to provide feedback after trying the troubleshooting steps in this article, contact [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).

When contacting support, provide the following information:

- Connector name and version
- Error messages from the connector logs
- Screenshots of the error (if applicable)
- Steps you've already taken to troubleshoot the issue
- DataStax Astra DB database ID
- Information about your DataStax database configuration (number of collections, approximate record count)

## Related content

- [DataStax connector overview](datastax-connector-overview.md)
- [Deploy the DataStax connector](datastax-connector-deployment.md)
