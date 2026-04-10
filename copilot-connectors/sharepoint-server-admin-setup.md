---
ms.date: 03/30/2026
title: "Set up the SharePoint Server service for connector ingestion"
ms.author: misvenso
author: antarikshp
manager: harshkum
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Get the steps to configure the SharePoint Server on-premises environment to enable the SharePoint Server Microsoft 365 Copilot connector."
---

# Set up the SharePoint Server service for connector ingestion

Before you can deploy the SharePoint Server connector, you need to prepare your on-premises environment. This article covers installing the Microsoft Graph connector agent—a Windows service that acts as a secure bridge between your SharePoint farm and Microsoft 365—and configuring authentication prerequisites.

Complete the steps in this article before proceeding to [Deploy the SharePoint Server connector](sharepoint-server-deployment.md).

## Setup checklist

The following checklists describe the steps involved in configuring the environment and setting up the connector prerequisites.

### Configure the environment

| Task | Role |
| ---- | ------ |
| [Install the Microsoft Graph connector agent](#install-the-microsoft-graph-connector-agent) | SharePoint admin |
| [Review authentication options](#configure-authentication) | SharePoint admin |

### Set up prerequisites for Entra ID OIDC authentication

Complete these steps only if you plan to use Microsoft Entra ID OIDC authentication. If you're using Basic or Windows (NTLM) authentication, skip to [Deploy the SharePoint Server connector](sharepoint-server-deployment.md).

| Task | Role |
| ---- | ------ |
| [Install Microsoft Entra ID Connect](#install-microsoft-entra-id-connect) | Entra ID admin |
| [Set up OIDC with Microsoft Entra ID](#set-up-oidc-with-microsoft-entra-id) | Entra ID admin / SharePoint admin |
| [Configure Expose an API](#configure-expose-an-api) | Entra ID admin |
| [Configure the scoped client identifier](#configure-the-scoped-client-identifier) | SharePoint admin |

## Install the Microsoft Graph connector agent

The Microsoft Graph connector agent is a Windows service you install on your network. It crawls your SharePoint on-premises content locally and securely sends it to Microsoft 365 for indexing—without exposing your internal farm directly to the internet. The agent can be installed on the SharePoint server itself or on any machine with network access to the farm. See [Install the Microsoft Graph connector agent](connector-agent.md) for installation steps.

Each SharePoint web application can be configured as one connection. A single agent can serve multiple connections, but we recommend no more than three connections per agent to maintain a healthy ingestion rate.

The account used for indexing must have **full control** access at the SharePoint Web Application level, or be a **farm administrator** (which implicitly grants full control across all web applications). Farm administrator is the recommended choice for multi-web-application deployments. Items that the account doesn't have permission to are skipped during indexing.

## Configure authentication

The SharePoint Server connector supports the following authentication types:

- **Basic** - Not recommended. Included for compatibility with legacy systems, but may be removed in the future.
- **Windows (NTLM)** - Use the Domain\username format in the **Username** field. Only NTLM is currently supported; Kerberos is not supported.
- **Microsoft Entra ID OIDC** - Requires additional configuration described in the following sections.

> [!NOTE]
> At a minimum, the account used for authentication must have **Full Read** permission at the Web Application level in SharePoint, regardless of the authentication type selected. For the indexing account, we recommend granting full control at the Web Application level or making it a farm administrator. Active Directory Federation Services (ADFS) authentication is not supported.

If you're using Microsoft Entra ID OIDC authentication, complete the prerequisite steps in the following sections before deploying the connector.

## Set up Microsoft Entra ID OIDC authentication

> [!NOTE]
> The steps in this section are only required if you're using Microsoft Entra ID (OIDC) authentication. If you're using Windows or Basic authentication, skip this section and go to [Deploy the SharePoint Server connector](sharepoint-server-deployment.md).

OIDC (OpenID Connect) is a modern authentication protocol that lets SharePoint Server verify identities through Microsoft Entra ID, enabling token-based access and single sign-on without passing credentials directly. It's the most secure option, but requires the additional setup steps in this section.

Before using Microsoft Entra ID-based authentication, ensure the following prerequisites are met:

- Microsoft Entra ID-based authentication is supported for Graph Connector Agent versions 3.1.2.0 and above. Upgrade your agent before proceeding. See [Install the Microsoft Graph connector agent](connector-agent.md) to learn more.
- Microsoft Entra ID-based authentication is supported only for SharePoint Server Subscription Edition. Make sure the farm is patched to the November 2024 build (16.0.17928.20238) or later. Refer to [SharePoint Updates](/officeupdates/sharepoint-updates).
- You'll need to set up OpenID Connect (OIDC) with Microsoft Entra ID. Since OpenID Connect (OIDC) requires HTTPS, ensure your SharePoint web applications are configured to use HTTPS.

### Install Microsoft Entra ID Connect

1. [Download](https://www.microsoft.com/download/details.aspx?id=47594) Microsoft Entra ID Connect.
1. Follow the [steps](/entra/identity/hybrid/connect/how-to-connect-install-roadmap) to install Microsoft Entra ID Connect.

### Set up OIDC with Microsoft Entra ID

Set up and enable OpenID Connect (OIDC) with Microsoft Entra ID using the steps described in [Set up OIDC authentication in SharePoint Server with Microsoft Entra ID](/sharepoint/security-for-sharepoint-server/set-up-oidc-auth-in-sharepoint-server-with-msaad). This step requires you to set up a third-party application in your Azure portal. Ensure that you have admin rights to perform this step.

### Configure Expose an API

1. Browse to the Entra ID admin center and log on as an Entra ID admin.
1. Select **App Registrations**, and choose the application that you created to enable OIDC authentication for your SharePoint Server web app.
1. Go to **Expose an API**.
1. Select **Add** next to Application ID URI. Make sure the application ID URI matches your SharePoint Server web application URL.

   ![Screenshot that shows expose an API configuration.](media/sharepoint-server-connector/expose-an-api.png)

1. Select **Add a scope**, enter **user_impersonation** for the scope name, admin consent display name, and admin consent description. Make sure the **State** is set to **Enabled** and choose **Add scope**. This scope grants the connector permission to act on behalf of authenticated users when accessing SharePoint content, ensuring it retrieves only what each user is authorized to see.
1. Select **Add a client application**. Enter the Graph Connector Agent (GCA) client ID: **cb15c983-0c91-416f-8dc0-6c0e1de4ed42**.
1. Under **Authorized Scopes**, select the user_impersonation scope for your web app and select **Add application**.

   ![Screenshot that shows how to Add a Client Application.](media/sharepoint-server-connector/add-a-client-application.png)

### Configure the scoped client identifier

When using OIDC authentication with SharePoint Server, you must additionally set the `ScopedClientIdentifier` property on the `SPTrustedIdentityTokenIssuer` for the Copilot connector to authenticate and crawl your content. This property maps each SharePoint site URL to an Entra ID application registration (the app identity configured during your OIDC setup), so SharePoint knows which app is permitted to access each site.

> [!IMPORTANT]
> Setting the `ScopedClientIdentifier` is not required for OIDC to function in SharePoint Server itself, but it is mandatory for the connector. Without this mapping, SharePoint Server cannot verify the connector's identity for the site, resulting in a 401 Unauthorized error.

Before you begin, have the following ready:

- **Application ID URI**: Set in the [Configure Expose an API](#configure-expose-an-api) section above (for example, `api://xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`).
- **Token issuer name**: The name of the `SPTrustedIdentityTokenIssuer`—the SharePoint object that trusts your Entra ID identity provider—created in step 3 of your initial OIDC setup. If you don't remember the name, run `Get-SPTrustedIdentityTokenIssuer` without parameters to list all configured issuers.

Run the following PowerShell commands in the SharePoint Management Shell as a Farm Administrator:

```powershell
# Get the existing trusted identity token issuer
$t = Get-SPTrustedIdentityTokenIssuer -Identity "<TrustedIdentityTokenIssuerName>"

# (Optional) Verify the current ScopedClientIdentifier value
$t.ScopedClientIdentifier

# Add the scoped client identifier for the SharePoint site
# The .Add() method requires a Uri object (not a plain string) and the Application ID URI
$uri = New-Object System.Uri("<SharePointSiteUrl>")
$t.ScopedClientIdentifier.Add($uri, "<EntraIdAppIdentifierUri>")
$t.Update()
```

| Placeholder | Description | Example |
|---|---|---|
| `<TrustedIdentityTokenIssuerName>` | Name of the SPTrustedIdentityTokenIssuer created during OIDC setup | `OIDC Entra ID` |
| `<SharePointSiteUrl>` | URL of the SharePoint site collection | `https://sharepoint.contoso.com/` |
| `<EntraIdAppIdentifierUri>` | Application ID URI of the Entra ID app registration | `api://xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx` |

> [!TIP]
> If you are crawling multiple site collections (for example, `https://portal.contoso.com` and `https://hr.contoso.com`), you must run `$t.ScopedClientIdentifier.Add()` for each unique URL. You can either batch multiple `.Add()` calls and then run `$t.Update()` once, or call `$t.Update()` after each individual `.Add()`.

## Next step

> [!div class="nextstepaction"]
> [Deploy the SharePoint Server connector](sharepoint-server-deployment.md)
