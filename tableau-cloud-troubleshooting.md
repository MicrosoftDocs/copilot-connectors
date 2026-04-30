---
title: "Troubleshoot issues with the Tableau Cloud connector"
ms.author:
author:
manager:
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 04/30/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Tableau Cloud Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Tableau Cloud connector

The Tableau Cloud Copilot connector integrates Tableau Cloud content into Microsoft 365 experiences, including Copilot, Copilot Search, and Microsoft Search.

This article provides troubleshooting information for common errors that you might encounter when you deploy the Tableau Cloud connector.

## Tableau Cloud connector troubleshooting

You might encounter the following errors when you deploy the Tableau Cloud connector or when the connector indexes data.

| Deployment step | Error or message | Possible reason | Resolution |
|---|---|---|
| Connection settings | Can't authenticate with the data source. | The Tableau Cloud instance URL is incorrect, or authentication values are invalid. | Verify the Tableau Cloud site URL format and confirm that User, Connected App Client ID, Connected App Secret ID, and Connected App Secret Key values are correct. |
| Connection settings | Don't have permission to access this data source. | The Tableau Cloud account or connected app doesn't have sufficient permissions to access sheets. | Use a Tableau Cloud site admin account, confirm the connected app is enabled, regenerate secret values if needed, and verify access to target projects and sheets. |

## Related content

- [Tableau Cloud connector overview](tableau-cloud-connector-overview.md)
- [Deploy the Tableau Cloud connector](tableau-cloud-connector-deployment.md)
