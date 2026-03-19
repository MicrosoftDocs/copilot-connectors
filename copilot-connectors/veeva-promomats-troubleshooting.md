---
title: "Veeva PromoMats Microsoft 365 Copilot connector troubleshooting"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 12/02/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Veeva PromoMats Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Veeva PromoMats Microsoft 365 Copilot connector

The Veeva PromoMats Microsoft 365 Copilot connector enables organizations to index and surface approved promotional marketing materials and related compliant content from Veeva Vault PromoMats into the Microsoft 365 ecosystem. 

This article provides troubleshooting information for common errors that you might encounter when you deploy the Veeva PromoMats connector.

## Veeva PromoMats connector troubleshooting

The following table lists common errors that can occur when you configure the Veeva PromoMats Microsoft 365 Copilot connector.

| Error   | Description | Resolution |
|---------|-------------|------------|
| `INVALID_SESSION_ID`    | Authentication session expired or invalid.          | Reauthenticate with valid credentials.                                     |
| `INSUFFICIENT_ACCESS`   | User lacks permissions to access files.             | Verify user roles and access control lists (ACLs) in Veeva Vault.                                 |
| `API_LIMIT_EXCEEDED`    | Too many API requests made in a short period.       | Adjust crawl frequency or retry after some time.                           |
| Missing Properties or Documents | Required metadata properties aren't enabled. | Make sure that metadata properties are enabled in Veeva Vault and test retrieval. |

To view more error types, select the connection and choose **Error details** > **Error code**. For more information, see [Monitor your connections](./manage-connector.md).

## Related content

- [Veeva PromoMats connector overview](veeva-promomats-overview.md)
- [Deploy the Veeva PromoMats connector](veeva-promomats-deployment.md)
