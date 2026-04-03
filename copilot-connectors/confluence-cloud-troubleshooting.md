---
ms.date: 09/05/2025
title: "Troubleshoot issues with the Confluence Cloud connector"
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Confluence Cloud Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Confluence Cloud Copilot connector

The Confluence Cloud Microsoft 365 Copilot connector integrates Confluence content into Microsoft 365, enabling Copilot and Microsoft Search to surface relevant wiki pages, blogs, and attachments directly within apps like Teams, Outlook, and SharePoint.

The article provides troubleshooting information for common errors that you might encounter when you deploy the Confluence Cloud connector.

To verify Confluence Cloud configuration information to help troubleshoot errors, see [Set up the Confluence Cloud service for connector ingestion](confluence-cloud-admin-setup.md).

## Confluence Cloud connector troubleshooting

You might encounter the following errors when you deploy the Confluence Cloud connector or when the connector indexes data.

| Deployment step | Error or error message | Possible reason |
|:------------ |:------------ |:------------ |
| Connection settings | The request is malformed or incorrect. | Incorrect Confluence site URL. |
| Connection settings | Unable to reach the Confluence cloud service for your Confluence site. | Incorrect Confluence site URL. |
| Connection settings | The client doesn't have permission to perform the action. | Invalid API token provided for Basic auth. |
| Select properties | No error message and no preview results. | Verify that your [CQL query](confluence-cloud-admin-setup.md#set-up-cql-for-advanced-search) is valid. |

## Related content

- [Confluence Cloud connector overview](confluence-cloud-overview.md)
- [Deploy the Confluence Cloud connector](confluence-cloud-deployment.md)
- [Set up the Confluence Cloud service for connector ingestion](confluence-cloud-admin-setup.md)