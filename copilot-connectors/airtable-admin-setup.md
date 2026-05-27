---
title: "Set up the Airtable service for connector ingestion (preview)"
ms.author: kailiang
author: Kai-Cloud
manager: zezhangzhao
ms.reviewer: 
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 05/27/2026
ms.localizationpriority: Medium
description: "Get the steps that the Airtable admin needs to complete for your organization to configure the Airtable Microsoft 365 Copilot connector."
---

# Set up the Airtable service for connector ingestion (preview)

The Airtable Microsoft 365 Copilot connector integrates Airtable records into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface relevant record information directly within apps like Microsoft Teams, Outlook, and SharePoint.

This article provides information about the configuration steps that Airtable admins need to complete in order for your organization to deploy the [Airtable connector](airtable-overview.md).

For information about how to deploy the connector, see [Deploy the Airtable connector](airtable-deployment.md).

> [!NOTE]
> The Airtable connector is currently in preview. Connector functionality and requirements are subject to change.

## Setup checklist

The following checklist lists the steps involved in configuring the environment and setting up the connector prerequisites.

| Task | Role |
| ---- | ---- |
| [Verify Airtable Enterprise plan](#verify-airtable-enterprise-plan) | Airtable admin |
| [Identify the Airtable Enterprise ID](#identify-the-airtable-enterprise-id) | Airtable admin |
| [Register an OAuth integration](#register-an-oauth-integration) | Airtable admin |
| [Allowlist the OAuth integration](#allowlist-the-oauth-integration) | Airtable admin |
| [Configure identity mapping](#configure-identity-mapping) | Airtable admin / Microsoft 365 admin |

## Configure the Airtable environment

The following sections describe the admin tasks to configure the Airtable environment to enable and optimize the connection.

### Verify Airtable Enterprise plan

Your Airtable account must be on an [Airtable Enterprise](https://airtable.com/pricing) plan. You need the Enterprise plan to register and allowlist OAuth integrations.

If your organization doesn't currently have an Enterprise plan, contact Airtable to upgrade your account.

### Identify the Airtable Enterprise ID

The Microsoft 365 Copilot connector requires your Airtable Enterprise ID to scope crawling and identity mapping to your enterprise account.

The Enterprise ID has the format `entXXXXXXXXXXXXXX` (for example, `entABC123def456GH`).

To find your Enterprise ID:

1. Sign in to the [Airtable Admin Hub](https://airtable.com/admin).
1. Copy the Enterprise ID from the URL: `https://airtable.com/admin/{enterpriseId}/...`.

Provide this Enterprise ID when you deploy the connector in the Microsoft 365 admin center.

## Set up connector prerequisites

The following sections describe the prerequisite steps to complete before you deploy the Airtable connector.

### Register an OAuth integration

The Airtable connector uses OAuth 2.0 for secure authentication. An Airtable admin must register an OAuth integration in the [Airtable Builder Hub](https://airtable.com/create/oauth).

> [!TIP]
> Create a dedicated service account in Airtable to register and authorize the integration, so the connection isn't tied to an individual user. You can also use a regular Airtable admin account.

To register the OAuth integration:

1. Sign in to the [Airtable Builder Hub](https://airtable.com/create/oauth).
1. Choose **Create integration**.
1. Complete the OAuth integration registration form using the information in the following table.

   | Field | Description | Recommended value |
   | --- | --- | --- |
   | Name | Display name for the OAuth integration. | `Microsoft 365 Copilot Connector` |
   | OAuth redirect URLs | Required callback URL that the authorization server redirects to. | `https://gcs.office.com/v1.0/admin/oauth/callback` |
   | Scopes | Read scopes that define what the connector can access. | Enable the following scopes: `data.records:read`, `schema.bases:read`, `user.email:read`, `workspacesAndBases:read`, `enterprise.groups:read`, `enterprise.user:read`, `enterprise.account:read`, `enterprise.auditLogs:read`, `enterprise.changeEvents:read`. |

   > [!IMPORTANT]
   > Enable only the read scopes listed in the table. Don't enable write or manage scopes.

1. Choose **Save** to create the integration.
1. Generate a **Client Secret** and copy both the **Client ID** and **Client Secret**. Store them securely; Airtable doesn't display the secret again.

You need to provide the Client ID and Client Secret when you deploy the connector in the Microsoft 365 admin center.

### Allowlist the OAuth integration

Airtable Enterprise accounts block third-party OAuth integrations by default. You must allowlist the OAuth integration to enable users to authorize the connector during the OAuth flow.

To allowlist the OAuth integration:

1. Sign in to the [Airtable Admin Hub](https://airtable.com/admin).
1. Go to **Settings** > **Integrations & development** > **Third party integration allowlist**.
1. Choose **Allow integration**.
1. Enter the **Client ID** of the integration you registered.
1. Select **Save**.

Without allowlisting, users can't authorize the connector during the OAuth flow.

### Configure identity mapping

The Airtable connector enforces that only users who have access to a record in Airtable can see it in Copilot responses and search results. Identity mapping ensures that Airtable users are correctly matched to Microsoft Entra ID accounts.

The default identity mapping method verifies that the email ID of Airtable users is the same as the user principal name (UPN) of the users in Microsoft Entra ID.

If the email ID of Airtable users is different than the UPN in Microsoft Entra ID, you need to provide a custom mapping formula. For more information, see [Map your non-Azure AD identities](map-non-entra-id.md).

To prepare for identity mapping:

- Verify that Airtable user email addresses match Microsoft Entra ID user principal names (UPNs), or
- Prepare a custom mapping formula if email addresses differ from UPNs.

You configure identity mapping in the Microsoft 365 admin center when you deploy the connector. For more information, see [Map identities](airtable-deployment.md#map-identities).

## Next step

> [!div class="nextstepaction"]
> [Deploy the Airtable connector](airtable-deployment.md)
