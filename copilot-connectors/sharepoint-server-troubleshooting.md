---
ms.date: 03/30/2026
title: "Troubleshoot issues with the SharePoint Server connector"
ms.author: misvenso
author: antarikshp
manager: harshkum
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Find troubleshooting information for the SharePoint Server Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the SharePoint Server connector

This article covers common errors you might encounter when deploying or running the SharePoint Server connector, and steps to resolve them.

- For authentication and OIDC setup errors, see [Set up the SharePoint Server service for connector ingestion](sharepoint-server-admin-setup.md).
- For errors during the Microsoft 365 admin center deployment steps, see [Deploy the SharePoint Server connector](sharepoint-server-deployment.md).

## SharePoint Server connector troubleshooting

You might encounter the following errors when you deploy the SharePoint Server connector or when the connector indexes data.

| Deployment step | Error | Resolution |
|:------------ |:------------ |:------------ |
| Authentication | 401 Unauthorized | When using Entra ID OIDC authentication, the `ScopedClientIdentifier` property is likely not set on the `SPTrustedIdentityTokenIssuer`. Run `Get-SPTrustedIdentityTokenIssuer` to check the current value, then follow the steps in [Configure the scoped client identifier](sharepoint-server-admin-setup.md#configure-the-scoped-client-identifier). |
| Authentication | Sign-in fails | Verify the account has at least **Full Read** permission at the SharePoint Web Application level. For the indexing account, full control or farm admin role is recommended. See [Configure authentication](sharepoint-server-admin-setup.md#configure-authentication). |
| Indexing | Items skipped during crawl | The indexing account doesn't have permission to the skipped items. Grant the account full control access at the Web Application level or make it a farm administrator. |
| Indexing | Custom properties not appearing | Property names must exactly match the column names in SharePoint (case-sensitive). The connector silently skips unrecognized property names. Also verify you haven't exceeded the 128-property limit, and note that custom properties aren't supported when multiple site collections are included in a single connection. |

## Related content

- [SharePoint Server connector overview](sharepoint-server-overview.md)
- [Set up the SharePoint Server service for connector ingestion](sharepoint-server-admin-setup.md)
- [Deploy the SharePoint Server connector](sharepoint-server-deployment.md)
