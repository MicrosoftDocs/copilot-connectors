---
title: "Set up the Veeva Vault service for Veeva On-Premises Microsoft 365 Copilot connector ingestion"
ms.author: danielabo
author: danipocket
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: microsoft-365-copilot-connectors
ms.date: 09/08/2026
ms.localizationpriority: Medium
description: "Set up Veeva Vault and Microsoft Entra for the Veeva On-Premises Microsoft 365 Copilot connector."
---

# Set up the Veeva Vault service for Veeva On-Premises Microsoft 365 Copilot connector ingestion

The Veeva On-Premises Microsoft 365 Copilot connector requires preparation in Veeva Vault and Microsoft Entra ID
before deployment.

This article provides information about the configuration steps that Veeva Vault admins need to complete in order
for your organization to deploy the [Veeva On-Premises connector](veeva-onpremise-overview.md).

For information about how to deploy the connector, see
[Deploy the Veeva On-Premises connector](veeva-onpremise-deployment.md).

## Setup checklist

The following checklist lists the steps involved in configuring the environment and setting up the connector
prerequisites.

| Task | Role |
| ---- | ---- |
| [Identify the Veeva Vault instance URL](#identify-the-veeva-vault-instance-url) | Veeva Vault admin |
| [Enable Direct Data API](#enable-direct-data-api) | Veeva Vault admin |
| [Register a Microsoft Entra application and create a client secret](#register-an-application-in-microsoft-entra-id) |  |
| [Configure a Veeva OAuth 2.0/OpenID Connect profile](#configure-oauth-20openid-connect-in-veeva-vault) | Veeva Vault admin |
| [Create a Vault SSO security policy and assign it to connector users](#create-a-security-policy-and-link-users) | Veeva Vault admin |
| [Prepare Vault users and identity mapping](#configure-vault-users-and-identity-mapping) | Veeva Vault admin and Microsoft Entra admin |
| [Deploy the connector](veeva-onpremise-deployment.md) ||


## Configure the Veeva Vault environment

The following sections describe the admin tasks to configure the Veeva Vault environment for the connection.

### Identify the Veeva Vault instance URL

The instance URL uses the format `https://<your-domain>.veevavault.com`. Record the URL for the Vault app that the
connection will index.


### Enable Direct Data API

Direct Data API is required and isn't enabled by default according to the source material. For limited-release
Vaults, go to **Admin** > **Settings** > **General Settings**, and select **Enable Direct Data API**. For more
information, see [Direct Data API](https://developer.veevavault.com/directdata/#direct-data-api).

If the option isn't available, ask your Veeva Vault administrator or Veeva support to verify feature availability.


## Set up connector prerequisites

The following sections describe the prerequisite steps to complete before deploying the Veeva On-Premises connector.

### Register an application in Microsoft Entra ID

1. In the Microsoft Entra admin center, go to **App registrations** > **New registration**.
1. Name the application and select **Accounts in this organizational directory only**.
1. Add the redirect URI for your environment:
   - Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`
   - Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
1. Under **Certificates & secrets**, create a client secret and store its value securely for connector registration
   and authorization.



### Configure OAuth 2.0/OpenID Connect in Veeva Vault

1. In Veeva Vault, go to **Admin** > **Settings** > **OAuth 2.0/OpenID Connect Profiles**.
1. Create a profile, set **Status** to **Active**, and select **Azure AD** as the provider.
1. Select **Upload AS metadata** > **Provide Authorization Server Metadata URL**.
1. Enter `https://login.microsoftonline.com/{tenant-id}/v2.0/.well-known/openid-configuration`, replacing
   `{tenant-id}` with your Microsoft Entra tenant ID.
1. Set **Identity is in another claim** to `upn`, and set **User ID Type** to **Federated ID**.
1. Under **Client Applications**, add the Microsoft Entra client ID as both the **Application Client ID** and
   **Authorization Server Client ID**.
1. Add the application scope required by your Vault configuration.
1. If **Perform strict Audience Restriction validation** is enabled, add the client ID to the **Audience** field.


### Create a security policy and link users

1. Go to **Admin** > **Settings** > **Security Policies** > **Create** > **Single sign-on**.
1. Provide a name and description, and set the policy status to **Active**.
1. Set the authentication type to **Single Sign-on** and select the OAuth 2.0/OpenID Connect profile. For more
   information, see [Configuring Single Sign-on](https://platform.veevavault.help/en/gr/13977/).
1. Set **eSignature Profile** to **None**.
1. Assign the policy to the connector administrator and applicable users under **Admin** > **Users & Groups**.
1. For each user, populate **Federated ID** with the matching Microsoft Entra UPN or other configured identity value.

### Configure Vault users and identity mapping

1. Identify the Vault users and groups whose documents will be indexed or accessed.
1. Make sure that each user has a Federated ID, UPN, email address, or other unique value that matches an active
   Microsoft Entra account.
1. Correct stale Vault identities that don't have a corresponding active Microsoft Entra account.
1. Prepare test users that represent the relevant Vault roles and groups.

During connector deployment, select the same source and Microsoft Entra properties when you configure identity
mapping. Mismatched properties can prevent authorized users from finding content or can produce validation errors.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Veeva On-Premises connector](veeva-onpremise-deployment.md)
