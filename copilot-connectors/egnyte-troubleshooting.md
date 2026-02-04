---
title: "Egnyte Microsoft 365 Copilot connector troubleshooting"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: anggao
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 12/16/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Egnyte Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Egnyte Microsoft 365 Copilot connector

The Egnyte Microsoft 365 Copilot connector integrates your Egnyte content into Microsoft 365 so that Copilot and Microsoft Search can surface files and insights directly within experiences such as Teams, Outlook, and SharePoint. This article provides troubleshooting guidance for common issues you might encounter when you deploy or use the Egnyte connector.

To verify Egnyte configuration settings during troubleshooting, see  
[Set up the Egnyte service for Egnyte connector ingestion](egnyte-admin-setup.md).

## Egnyte connector troubleshooting

The following table lists common errors and recommended troubleshooting steps.

| Error | Troubleshooting steps |
|-------|------------------------|
| **Can't reach this instance URL** | The instance URL is unreachable. Verify that the URL is correct in the Egnyte developer portal and that it’s accessible from your network. |
| **No valid app info found for API key** | The Client ID is incorrect or no longer valid. Copy the correct Client ID from the Egnyte developer portal and update your connector settings. |
| **InvalidConnectionCredentials** | Credentials are rejected due to invalid values. Reenter the Client ID and Secret in the Microsoft 365 admin center and verify that the app has the correct permission scopes in the Egnyte developer portal. |
| **Crawling failed with error code 9009** | This error commonly indicates that your Egnyte API rate limit was reached. Request a rate‑limit increase from Egnyte, then retry the crawl. |
| **Crawling failed with error code 3002** | A file contains annotations that are too large to ingest, resulting in a Request Payload is Too Large error. This is a known platform issue that's being addressed. |
| **Incorrect request type GET for resource owner flow** | This error can occur if the API key is registered under the wrong flow. Ensure the API key is created as a **Publicly Available Application (Implicit Grant Flow)**. Contact Egnyte support if the key needs to be corrected. |

## Related content

- [Egnyte connector overview](egnyte-overview.md)  
- [Deploy the Egnyte connector](egnyte-deployment.md)