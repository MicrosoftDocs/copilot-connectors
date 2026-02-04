---
title: "Troubleshoot issues with the Adobe Experience Manager Sites Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: lauragra
ms.reviewer: rantang
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 12/10/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for common errors that you might encounter when you deploy the Adobe Experience Manager Sites Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Adobe Experience Manager Sites Microsoft 365 Copilot connector

With the Adobe Experience Manager Sites Microsoft 365 Copilot connector, your organization can index published webpages from Adobe Experience Manager (AEM) Sites so people can discover and use them across Microsoft 365 Copilot and Microsoft Search. This article provides troubleshooting information for common errors that you might encounter when you deploy the Adobe Experience Manager Sites connector or when the connector indexes data.

## Adobe Experience Manager Sites connector troubleshooting

You might encounter the following errors during connector deployment or indexing.

| Deployment step      | Error or error message                        | Possible reason |
|----------------------|-----------------------------------------------|-----------------|
| Connection settings  | Can't authenticate with the data source.     | Verify that your Adobe Experience Cloud instance author and publish environment URLs are correct and that your credentials are valid. |
| Connection settings  | Don't have permission to access this data source. | Make sure that you have an Adobe Experience Manager Sites technical account with credentials to access published webpages and metadata. The technical account is a secure, service-based account for external access. For more information, see [Generate access tokens for server-side APIs](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#generate-a-jwt-token-and-exchange-it-for-an-access-token). |
| Indexing             | Pages not appearing in Copilot or Microsoft Search. | Check ingestion filters for path or regex exclusions. Excluded paths take priority over included paths. Also verify crawl schedules for incremental and full crawls. |
| Indexing             | Incorrect or missing property values.        | Review property schema settings under **Manage properties**. Make sure that properties are marked as searchable, queryable, or retrievable as needed. |

## Related content

- [Adobe Experience Manager (AEM) Sites connector overview](adobe-experience-manager-sites-overview.md)
- [Deploy the Adobe Experience Manager (AEM) Sites connector](adobe-experience-manager-sites-deployment.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoftsearch/configure-connector)
