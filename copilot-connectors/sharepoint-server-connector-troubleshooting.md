---
ms.date: 04/22/2026
title: "Troubleshoot issues with the SharePoint Server connector"
ms.author: venk
author: venk
manager: srramam
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Resolve common authentication, indexing, and configuration errors for the SharePoint Server Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the SharePoint Server connector

This article covers common errors you might encounter when deploying or running the SharePoint Server connector, and steps to resolve them.

- For authentication and OIDC setup errors, see [Configure SharePoint Server](sharepoint-server-admin-setup.md).
- For errors during the Microsoft 365 admin center deployment steps, see [Deploy the SharePoint Server connector](sharepoint-server-deployment.md).

## Common errors

You might encounter the following errors when you deploy the SharePoint Server connector or when the connector indexes content.

| Deployment step | Error | Resolution |
|:------------ |:------------ |:------------ |
| Setup | No Graph Connector Agent available | No agent is registered to your tenant. Install and register the Microsoft Graph connector agent, and then refresh the agent list. See [Install and configure the Microsoft Graph connector agent](connector-agent.md). |
| Authentication | 401 Unauthorized | When using Microsoft Entra ID OIDC authentication, the `ScopedClientIdentifier` property is likely not set on the `SPTrustedIdentityTokenIssuer`. Run `Get-SPTrustedIdentityTokenIssuer` to check the current value, and then follow the steps in [Configure the scoped client identifier](sharepoint-server-configuration.md#configure-the-scoped-client-identifier). |
| Authentication | Authorization fails | Verify the account has at least **Full Read** permission at the Web Application level in SharePoint Server. For the indexing account, full control or SharePoint Server farm administrator role is recommended. See [Configure authentication](sharepoint-server-configuration.md#configure-authentication). |
| Authentication | Microsoft Entra ID OIDC authentication not working | Verify prerequisites: the Microsoft Graph connector agent must be version 3.1.2.0 or later, and SharePoint Server must be Subscription Edition patched to the November 2024 build (16.0.17928.20238) or later. See [Set up Microsoft Entra ID OIDC authentication](sharepoint-server-configuration.md#set-up-microsoft-entra-id-oidc-authentication). |
| Indexing | Items skipped during crawl | The indexing account doesn't have permission to the skipped items. Grant the account full control access at the Web Application level in SharePoint Server or make it a SharePoint Server farm administrator. |
| Indexing | Custom properties not appearing | Property names must exactly match the column names in SharePoint (case-sensitive). The connector silently skips unrecognized property names. Also verify you didn't exceed the 128-property limit, and note that custom properties aren't supported when multiple site collections are included in a single connection. |
| Post-indexing | Users can't see content in Copilot or Search | If you're using the **Only people with access to the content in the data source** permission mode, Active Directory identities must be synced with Microsoft Entra ID. See [Sync Active Directory to Microsoft Entra ID](sharepoint-server-configuration.md#sync-active-directory-to-microsoft-entra-id). |

## Related content

- [SharePoint Server connector overview](sharepoint-server-overview.md)
- [Configure SharePoint Server](sharepoint-server-admin-setup.md)
- [Deploy the SharePoint Server connector](sharepoint-server-deployment.md)
