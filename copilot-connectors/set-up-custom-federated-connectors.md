---
title: Set up custom federated connectors
description: Learn how to build, authenticate, and deploy a custom federated connector that brings your organization's proprietary data into Microsoft 365 Copilot through the Model Context Protocol (MCP).
author: lauragra
ms.author: lauragra
ms.manager: calvind
ms.reviewer: mansipakhale
ms.topic: how-to
ms.service: copilot-connectors
ms.localizationpriority: Medium
ms.date: 05/01/2026
---

# Set up custom federated connectors


Many organizations have proprietary systems, internal databases, and line-of-business applications that hold critical operational data. By using custom federated connectors, you can bring this data into Microsoft 365 Copilot by using Model Context Protocol (MCP), unlocking real-time access and natural language interaction for your organization's unique workflows. After you connect your data source, users can interact with the data in real time by using natural language - just as they do with Microsoft 365 data.

A custom federated connector starts with a Model Context Protocol (MCP) server that exposes read-only tools to safely surface your data. The MCP server acts as a bridge between Microsoft 365 Copilot and your internal systems. To keep access secure and user-scoped, custom federated connectors use industry-standard authentication.

## Prerequisites

Before you begin, make sure you have the following items:

- An **MCP server** URL with read-only tools exposed (for example, `search`, `fetch`, or `query`).
- **Admin permissions**
  - Global Administrator or AI Administrator role in the [Microsoft 365 admin center](https://admin.microsoft.com/).
  - An appropriate Microsoft Entra admin role for single sign-on (SSO) authentication.
  - Access to the [Teams Developer Portal](https://dev.teams.microsoft.com/).
- **Authentication setup**
  - If your data source requires authentication, [set up authentication](#set-up-authentication) before you create the connector.

## Set up authentication

Custom federated connectors support two authentication methods. Choose the method that matches your data source.

| Method | Use case | Setup required |
|---|---|---|
| **Microsoft Entra SSO** | Users authenticate with their Microsoft 365 credentials. | Microsoft Entra app registration and Teams Developer Portal registration. |
| **OAuth 2.0** | Users authenticate with a third-party identity provider. | OAuth app in the source system and Teams Developer Portal registration. |

### Microsoft Entra SSO

Microsoft Entra SSO simplifies access management by letting users sign in to your MCP server with their existing Microsoft Entra credentials, so they don't need extra credentials. To use this option, your MCP server or API must use Microsoft Entra ID for access control.

To set up Microsoft Entra SSO:

1. [Update the Microsoft Entra app registration](/microsoft-365/copilot/extensibility/api-plugin-authentication#update-the-microsoft-entra-app-registration).
1. [Add the new token audience to your API](/microsoft-365/copilot/extensibility/api-plugin-authentication#add-the-new-token-audience-to-your-api).
1. [Register an SSO client in the Teams Developer Portal](/microsoft-365/copilot/extensibility/api-plugin-authentication#register-an-sso-client-in-teams-developer-portal).

When registration finishes, the Teams Developer Portal generates a **Microsoft Entra SSO registration ID**. Copy this ID - you need it when you configure the connector.

### OAuth 2.0

Use OAuth 2.0 when your data source authenticates with an external identity provider.

#### Register your app with the OAuth 2.0 provider

Before you begin, register your app with your OAuth 2.0 provider to get a client ID and secret. If your provider requires you to specify allowed redirect URIs during app registration, include the following URI:

```
https://teams.microsoft.com/api/platform/v1.0/oAuthRedirect
```

Copy the following credentials from your OAuth provider:

- **Client ID**
- **Client secret**

#### Register the OAuth app in the Teams Developer Portal

1. Sign in to the [Teams Developer Portal](https://dev.teams.microsoft.com/).
1. Select **Tools** > **OAuth Client Registration**.
1. Select **+ New OAuth connection**.
1. Enter the connection details:

   | Field | Value |
   |---|---|
   | **Name** | A descriptive name for your data source. |
   | **Client ID** | The client ID from your OAuth provider. |
   | **Client secret** | The client secret from your OAuth provider. |
   | **Authorization endpoint** | The URL your app uses to [request an authorization code](/entra/identity-platform/v2-oauth2-auth-code-flow#request-an-authorization-code). |
   | **Token endpoint** | The URL your app uses to [redeem a code for an access token](/entra/identity-platform/v2-oauth2-auth-code-flow#redeem-a-code-for-an-access-token). |
   | **Refresh endpoint** | The URL your app uses to [refresh the access token](/entra/identity-platform/v2-oauth2-auth-code-flow#refresh-the-access-token). |
   | **Scopes** | The permission scopes that your API defines for access. |

1. (Optional) Enable **Proof Key for Code Exchange (PKCE)** if your OAuth provider supports it.
1. Select **Save**.

   :::image type="content" source="media/federated-connectors/oauth-client-registration-form.png" alt-text="Screenshot of the OAuth client registration form in the Teams Developer Portal, showing the App settings, Restrict usage, and OAuth settings sections." lightbox="media/federated-connectors/oauth-client-registration-form.png":::

After the registration is saved, the Teams Developer Portal displays the **OAuth client registration ID**. Copy this ID—you'll need it when you configure the connector.

:::image type="content" source="media/federated-connectors/oauth-registration-id.png" alt-text="Screenshot of the OAuth client registration confirmation page, with the registration ID highlighted." lightbox="media/federated-connectors/oauth-registration-id.png":::

## Create the connector

After you set up authentication, create the connector in the Microsoft 365 admin center.

1. Sign in to the [Microsoft 365 admin center](https://admin.microsoft.com/).
1. In the left pane, select **Copilot** > **Connectors**.
1. Select the **Gallery** tab.
1. Under **Created by your org**, find the **Create a new connector** tile and select **Add**.

   :::image type="content" source="media/federated-connectors/admin-center-connectors-gallery.png" alt-text="Screenshot of the Connectors page in the Microsoft 365 admin center, with the Gallery tab and the Create a new connector tile highlighted." lightbox="media/federated-connectors/admin-center-connectors-gallery.png":::

1. On the **Custom connector** page, under **Connect to MCP server**, select **Add**.

   :::image type="content" source="media/federated-connectors/connect-to-mcp-server.png" alt-text="Screenshot of the Custom connector page, with the Connect to MCP server option highlighted." lightbox="media/federated-connectors/connect-to-mcp-server.png":::

1. Enter the following information about your connector.

    | Field | Description | Example |
    |---|---|---|
    | **Display name** | The user-facing name for your connector. | Company Intranet |
    | **Base URL** | Your MCP server endpoint. | `https://mcp.contoso.com` |

1. Enter the registration ID that matches the authentication method you set up previously:

    - For **Microsoft Entra SSO**, enter the **SSO registration ID** from the Teams Developer Portal.
    - For **OAuth 2.0**, enter the **OAuth registration ID** from the Teams Developer Portal.

1. Select **Save** to create the connector.

## Manage the connector

After you create a connector, it appears in the **Your Connections** list. From there, you can roll it out to users and manage its lifecycle.

### Stage the rollout

You can deploy the connector to selected users or groups before you release it to everyone in the tenant:

1. Select your connector.
1. Select **Staged rollout**.
1. Choose **Users** or **Groups**.
1. Add the test users or groups.
1. When you're ready to release the connector, select **Deploy to all users**.

### Enable, disable, or delete the connector

From the **Your Connections** list, you can take the following actions.

| Action | Result |
|---|---|
| **Enable** | Makes the connector available to its assigned audience. |
| **Disable** | Pauses the connector without removing its configuration. |
| **Delete** | Permanently removes the connector and its configuration. |

> [!NOTE]
> Changes to a connector can take up to 15 minutes to take effect.

## Related content

- [Model Context Protocol (MCP) overview](https://modelcontextprotocol.io/)
- [Federated connectors overview](federated-connectors-overview.md)
- [Manage federated connectors](manage-federated-connectors.md)
- [Submit a federated connector](submit-federated-connector.md)
