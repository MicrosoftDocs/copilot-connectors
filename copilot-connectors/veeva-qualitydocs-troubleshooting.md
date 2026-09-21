---
title: "Troubleshoot issues with the Veeva QualityDocs connector"
ms.author: dannyyao
author: dannyyaou
manager: jecui
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: microsoft-365-copilot-connectors
ms.date: 12/01/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Veeva QualityDocs Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Veeva QualityDocs connector

The Veeva QualityDocs Microsoft 365 Copilot connector enables organizations to index controlled quality documents—such as Standard Operating Procedures (SOPs), work instructions, policies, CAPAs, and batch records—from Veeva Vault QualityDocs into Microsoft Graph. 

This article provides troubleshooting information for common errors that you might encounter when you deploy the Veeva QualityDocs connector.

## Veeva QualityDocs connector troubleshooting

The following table lists common errors that can occur when you configure the Veeva QualityDocs Microsoft 365 Copilot connector.

| Error                   | Description      | Resolution |
|-------------------------|------------------|------------|
| `INVALID_SESSION_ID`    | Authentication session expired or invalid.        | Reauthenticate with valid credentials. |
| `INSUFFICIENT_ACCESS`   | User lacks permissions to access files.           | Verify user roles and ACLs in Veeva Vault.  |
| `API_LIMIT_EXCEEDED`    | Too many API requests made in a short period.     | Adjust crawl frequency or retry after some time. |
| Missing Properties or Documents | Required metadata properties are not enabled. | Make sure that metadata properties are enabled in Veeva Vault and test retrieval. |

To view more error types, select the connection and choose **error details** > **error code**. For more information, see [Monitor your connections](manage-connector.md).

## Related content

- [Veeva QualityDocs connector overview](veeva-qualitydocs-overview.md)
- [Deploy the Veeva QualityDocs connector](veeva-qualitydocs-deployment.md)
