---
title: "Troubleshoot issues with the Adobe Experience Manager Assets connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: rantang
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 12/09/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Adobe Experience Manager Assets Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Adobe Experience Manager Assets connector

The Adobe Experience Manager Assets Microsoft 365 Copilot connector integrates Adobe Experience Manager (AEM) Assets content into the Microsoft 365 ecosystem. This integration allows Copilot and Microsoft Search experiences to surface published assets. 

This article provides troubleshooting information for common errors that you might encounter when you deploy the connector.

## Adobe Experience Manager Assets connector troubleshooting

You might encounter the following errors when you deploy the connector or when the connector indexes data. This sentence ends with a period.

| Deployment step      | Error or error message                        | Possible reason |
|-----------------------|----------------------------------------------|-----------------|
| Connection settings   | Can't authenticate with the data source.    | Verify that your Adobe Experience Cloud instance author environment and publish environment URLs are correct and verify that your credentials are valid. |
| Connection settings   | Don't have permission to access this data source. | To connect to Adobe Experience Manager Assets and allow the connector to update published assets regularly, you need a technical account with credentials to access published assets and metadata. The technical account is a secure, service-based account for external access. For details, see [Generate access tokens for server-side APIs](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis). |

## Related content

- [Adobe Experience Manager Assets connector overview](adobe-experience-manager-assets-overview.md)
- [Deploy the Adobe Experience Manager Assets connector](adobe-experience-manager-assets-deployment.md)
