---
ms.date: 05/20/2026
title: "Set up the PagerDuty Service for Connector Ingestion"
ms.author: wangchen
author: wangchen
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.localizationpriority: Medium
description: "Get the steps that the PagerDuty admin needs to complete to configure the service for your organization so you can enable the PagerDuty Schedules Microsoft 365 Copilot connector."
---

# Set up the PagerDuty service for connector ingestion (preview)

The PagerDuty Schedules Microsoft 365 Copilot connector integrates PagerDuty schedule data into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface schedule information directly within apps like Teams, Outlook, and SharePoint.

This article provides information about the configuration steps that PagerDuty admins need to complete to set up PagerDuty for your organization, including configuring the environment and setting up prerequisites for the [PagerDuty Schedules connector](pagerduty-schedules-overview.md).

For information about how to deploy the connector, see [Deploy the PagerDuty Schedules connector](pagerduty-schedules-deployment.md).

[!INCLUDE [conector-preview-access](includes/connector-preview-access.md)]

## Setup checklist

The following checklists list the steps involved in configuring the environment and setting up the connector prerequisites.

### Configure the environment

| Task | Role | Status |
| ---- | ---- | ------ |
| [Identify the PagerDuty instance URL](#configure-the-pagerduty-environment) | PagerDuty admin | |
| [Review service regions](#review-service-regions) | PagerDuty admin | |
| [Configure Advanced Permissions (optional)](#configure-advanced-permissions) | PagerDuty admin | |
| [Define attribute mapping](#define-pagerduty-attribute-mapping) | PagerDuty admin | |

### Set up prerequisites

| Task | Role | Status |
| ---- | ---- | ------ |
| [Create a PagerDuty account with admin permissions](#create-pagerduty-admin-account) | PagerDuty admin | |
| [Register an OAuth 2.0 app in PagerDuty](#register-an-oauth-20-app-in-pagerduty) | PagerDuty admin | |
| [Configure OAuth scopes](#configure-oauth-scopes) | PagerDuty admin | |
| [Set up redirect URLs](#set-up-redirect-urls) | PagerDuty admin | |
| [Validate connector access](#validate-connector-access) | PagerDuty admin | |

## Configure the PagerDuty environment

The following sections describe the admin tasks to configure the PagerDuty environment to enable and optimize the connection.

### Identify the PagerDuty instance URL

PagerDuty allows customers to choose the geographic service region of the PagerDuty data centers that host their account. The instance REST API URL varies based on your service region:

- **US service region**: `https://api.pagerduty.com`
- **EU service region**: `https://api.eu.pagerduty.com`

To identify your PagerDuty instance URL:

1. Sign in to your [PagerDuty](https://www.pagerduty.com) account.
1. Review the URL in your browser address bar to determine your region.
1. For the US region, your URL typically appears as `https://[your-subdomain].pagerduty.com`.
1. For the EU region, your URL typically appears as `https://[your-subdomain].eu.pagerduty.com`.

For more information, see [Service regions](https://support.pagerduty.com/main/docs/service-regions) in the PagerDuty documentation.

### Review service regions

Make sure that you identify the correct service region for your PagerDuty instance. The REST API endpoint you configure in the connector must match your service region:

- If your organization uses the US service region, use `https://api.pagerduty.com`
- If your organization uses the EU service region, use `https://api.eu.pagerduty.com`

Using the incorrect API endpoint prevents the connector from accessing your PagerDuty data.

### Configure Advanced Permissions

PagerDuty Advanced Permissions provide granular control over which users can view specific schedules. When Advanced Permissions is enabled, you can restrict schedule visibility to specific teams.

> [!NOTE]
> When Advanced Permissions is enabled in PagerDuty, only members of the teams linked to a specific schedule can access and search for that schedule in Microsoft Search and Microsoft 365 Copilot.

To configure Advanced Permissions in PagerDuty:

1. Sign in to your PagerDuty account with administrator permissions.
1. Navigate to **People** > **Teams**.
1. Review your team structure and ensure that teams are properly configured.
1. For each schedule, verify which teams have access.
1. Adjust team assignments as needed to align with your organization's access control requirements.

For more information about Advanced Permissions, see [Advanced Permissions](https://support.pagerduty.com/main/docs/advanced-permissions) in the PagerDuty documentation.

### Define PagerDuty attribute mapping

The default method for mapping your data source identities to Microsoft Entra ID is to determine whether the email address of each PagerDuty user matches the user principal name (UPN) or email address in Microsoft Entra ID. If this default mapping doesn't meet your organization's needs, you can define a custom mapping formula.

For more information about mapping identities that aren't in Microsoft Entra ID, see [Map your non-Azure AD identities](/microsoft-365/copilot/connectors/map-non-entra-id).

## Set up connector prerequisites

The following sections describe the prerequisite steps to complete before deploying the PagerDuty Schedules connector.

### Create PagerDuty admin account

To configure the PagerDuty Schedules connector, you need a PagerDuty account with administrator permissions. This account is required to:

- Register an OAuth 2.0 app in PagerDuty
- Configure API access scopes
- Authorize the connector to access your PagerDuty data

Make sure that you have access to a PagerDuty account with the **Account Owner** or **Admin** role before proceeding.

### Register an OAuth 2.0 app in PagerDuty

The PagerDuty Schedules connector uses OAuth 2.0 for authentication. You need to register an app in PagerDuty to obtain the client credentials required for connector setup.

To register an OAuth 2.0 app in PagerDuty:

1. Sign in to your PagerDuty account with administrator permissions.
1. Navigate to **Integrations** > **Developer Mode**.
1. If Developer Mode is not enabled, enable it to access app registration.
1. Choose **Create New App**.
1. In the app registration form, provide the following information:
   - **App Name**: Enter a descriptive name such as "Microsoft 365 Copilot Connector"
   - **Description**: Enter a description such as "OAuth app for Microsoft 365 Copilot connector integration"
   - **Category**: Select **Integration**

1. Select **Scoped OAuth** as the OAuth type.
1. Configure the redirect URLs (see [Set up redirect URLs](#set-up-redirect-urls)).
1. Configure the required OAuth scopes (see [Configure OAuth scopes](#configure-oauth-scopes)).
1. Choose **Save** to create the app.
1. After the app is created, copy the **Client ID** and **Client Secret**. You need these values when deploying the connector in the Microsoft 365 admin center.

> [!IMPORTANT]
> Store the Client ID and Client Secret securely. You need these credentials to authenticate the connector during deployment.

For more information about OAuth functionality in PagerDuty, see [OAuth Functionality](https://developer.pagerduty.com/docs/oauth-functionality) and [Register an App](https://developer.pagerduty.com/docs/register-an-app) in the PagerDuty developer documentation.

### Configure OAuth scopes

The PagerDuty Schedules connector requires specific OAuth scopes to access schedule data. When configuring your OAuth app in PagerDuty, select the following scopes:

| Scope | Access level | Description |
| ----- | ------------ | ----------- |
| Audit records | Read Access | Required to access audit log information for schedules. |
| Schedules | Read Access | Required to read schedule data including on-call rotations and coverage information. |
| Teams | Read Access | Required when Advanced Permissions is enabled to enforce team-based access controls. |
| Users | Read Access | Required to map PagerDuty users to Microsoft 365 identities for permission enforcement. |

To configure these scopes:

1. In your OAuth app settings in PagerDuty, navigate to the **OAuth Scopes** section.
1. Select each of the required scopes listed in the table above.
1. Make sure that **Read Access** is selected for each scope.
1. Choose **Save** to apply the scope configuration.

> [!NOTE]
> The connector requires read-only access. Write or delete permissions are not required.

### Set up redirect URLs

OAuth 2.0 authentication requires redirect URLs (also called callback URLs) to complete the authorization flow. The redirect URL varies based on your Microsoft 365 environment.

In your PagerDuty OAuth app settings, add the appropriate redirect URL for your environment:

- **For Microsoft 365 Enterprise**: `https://gcs.office.com/v1.0/admin/oauth/callback`
- **For Microsoft 365 Government**: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`

To configure the redirect URL:

1. In your OAuth app settings in PagerDuty, locate the **Redirect URLs** field.
1. Enter the appropriate redirect URL for your Microsoft 365 environment.
1. Choose **Add** or **Save** to apply the configuration.

> [!IMPORTANT]
> Make sure that you use the correct redirect URL for your environment. Using an incorrect redirect URL prevents the OAuth authorization flow from completing successfully.

### Validate connector access

After completing the OAuth app registration, validate that the configuration is correct:

1. Verify that the **Client ID** and **Client Secret** are available and stored securely.
1. Verify that the correct redirect URL is configured for your Microsoft 365 environment.
1. Verify that all required OAuth scopes are enabled.
1. Test the OAuth authorization flow by attempting to authenticate with the connector during deployment.

If you encounter authentication errors during deployment, review the following:

- Verify that the Client ID and Client Secret are entered correctly in the connector configuration.
- Verify that the redirect URL matches your Microsoft 365 environment (Enterprise or Government).
- Verify that all required OAuth scopes are enabled in the PagerDuty app settings.
- Check that your PagerDuty account has administrator permissions.

## Next step

> [!div class="nextstepaction"]
> [Deploy the PagerDuty Schedules connector](pagerduty-schedules-deployment.md)
