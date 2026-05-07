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
description: "Find troubleshooting information for common authentication, indexing, and configuration errors with the SharePoint Server Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the SharePoint Server connector

The SharePoint Server Microsoft 365 Copilot connector allows users in your organization to search for and reason over content stored in a SharePoint Server farm across Microsoft Search, Copilot Search, Copilot Chat, and declarative agents. This article provides troubleshooting information for common errors you might encounter when you deploy or use the SharePoint Server connector.

To verify setup information to help troubleshoot errors, see [Set up SharePoint Server](sharepoint-server-admin-setup.md) and [Deploy the SharePoint Server connector](sharepoint-server-deployment.md).

## Common issues

You might encounter the following issues when you deploy or use the SharePoint Server connector.

| Stage | Symptom or issue | Resolution |
|:------------ |:------------ |:------------ |
| Connection setup | Graph Connector Agent dropdown is empty and shows "Could not find any on-prem agent" error | No agent is registered to your tenant. Install and register the Microsoft Graph connector agent, and then refresh the agent list.<br /><br />For details, see [Install and configure the Microsoft Graph connector agent](connector-agent.md). |
| Connection setup | 401 Unauthorized | When using Microsoft Entra ID OIDC authentication, the `ScopedClientIdentifier` property is likely not set on the `SPTrustedIdentityTokenIssuer`.<br /><br />Run `Get-SPTrustedIdentityTokenIssuer` to check the current value, and then follow the steps in [Configure the scoped client identifier](sharepoint-server-admin-setup.md#configure-the-scoped-client-identifier). |
| Connection setup | Authorization fails | Verify that the account has at least **Full Read** permission at the Web Application level in SharePoint Server. For the indexing account, we recommend full control or SharePoint Server farm administrator role. For details, see [Configure authentication](sharepoint-server-admin-setup.md#configure-authentication). |
| Connection setup | Microsoft Entra ID OIDC authentication not working | Verify prerequisites: the Microsoft Graph connector agent must be version 3.1.2.0 or later, and SharePoint Server must be Subscription Edition patched to the November 2024 build (16.0.17928.20238) or later. For details, see [Set up Microsoft Entra ID OIDC authentication](sharepoint-server-admin-setup.md#set-up-microsoft-entra-id-oidc-authentication). |
| Post connection setup | Items skipped during crawl | The indexing account doesn't have permission to the skipped items. Grant the account full control access at the Web Application level in SharePoint Server or make it a SharePoint Server farm administrator. |
| Post connection setup | Custom properties not appearing | Property names must exactly match the column names in SharePoint and are case-sensitive. The connector silently skips unrecognized property names. Also verify that you didn't exceed the 128-property limit, and note that custom properties aren't supported when multiple site collections are included in a single connection. |
| Post connection setup | Connection shows Ready status but many items are not indexed. Crawl errors in the connection pane reference some network issues. | If the environment in which the Microsoft Graph connector agent is set up uses an outbound proxy, the agent's crawl requests to your SharePoint Server may be routed through the proxy as well, which can't reach your SharePoint Server. Configure proxy bypass for your SharePoint Server hostnames. For details, see the proxy bypass note in [Recommended configuration](connector-agent.md#recommended-configuration). |
| Post connection setup | Users can't see content in Copilot or Search | If you're using the **Only people with access to the content in the data source** permission mode, Active Directory identities must be synced with Microsoft Entra ID. For details, see [Sync Active Directory to Microsoft Entra ID](sharepoint-server-admin-setup.md#sync-active-directory-to-microsoft-entra-id). |
| Post connection setup | <a id="refresh-token-expired"></a>Indexed items drop to zero after some time | If your connection uses Microsoft Entra ID OIDC authentication, this issue or error may be caused by a Conditional Access Sign-in Frequency policy. If such a policy applied to the Microsoft Entra ID account used to authorize the connection has a Sign-in frequency shorter than the connector's full crawl interval, the refresh token can expire before the next full crawl renews it.<br /><br />To check your current full crawl interval, go to **Copilot** > **Connectors** > **Your Connections** in the Microsoft 365 admin center, select your connection, and review the **Refresh Settings** section (shown as **Full refresh interval**). The default is 24 hours unless you customized it during connection setup.<br /><br />To check if such a Conditional Access policy exists, sign in to the [Microsoft Entra admin center](https://entra.microsoft.com), go to **Entra ID** > **Conditional Access** > **Policies**, find the policy that applies to that account, and under **Access controls** > **Session** > **Sign-in frequency** review the value.<br /><br />If the Sign-in frequency is shorter than your full crawl interval, apply one of these mitigations:<ul><li>Increase the Sign-in frequency to at least twice your full crawl interval (for example, 48 hours for the default 24-hour full crawl).</li><li>Exclude that account from the Conditional Access Sign-in Frequency policy governing it.</li><li>Enable incremental crawl on a shorter interval so the agent refreshes the token more often. To change crawl settings, edit your connection in the Microsoft 365 admin center and go to the **Sync** tab.</li></ul>Then edit the connection in the Microsoft 365 admin center and select **Authorize** again on the **Setup** tab to issue a new refresh token.<br /><br />For more information, see [Configure adaptive session lifetime policies](https://learn.microsoft.com/entra/identity/conditional-access/howto-conditional-access-session-lifetime). |

## Related content

- [SharePoint Server connector overview](sharepoint-server-overview.md)
- [Configure SharePoint Server](sharepoint-server-admin-setup.md)
- [Deploy the SharePoint Server connector](sharepoint-server-deployment.md)
