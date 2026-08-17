---
title: "Set up the BambooHR service for BambooHR connector ingestion"
ms.author: danielabo
author: danipocket
manager: calvind
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: microsoft-365-copilot-connectors
ms.date: 08/17/2026
ms.localizationpriority: Medium
description: "Get the steps that the BambooHR admin needs to complete for your organization to configure the BambooHR Microsoft 365 Copilot connector."
---

# Set up the BambooHR service for connector ingestion

The BambooHR Microsoft 365 Copilot connector indexes employee profiles from BambooHR into Microsoft Graph, making them accessible across Microsoft 365 experiences including Microsoft 365 Copilot and Microsoft Search. This article provides information about the configuration steps that BambooHR admins need to complete in order for your organization to deploy the [BambooHR connector](bamboohr-overview.md).

For information about how to deploy the connector, see [Deploy the BambooHR connector](bamboohr-deployment.md).

## Setup checklist

The following checklist lists the steps involved in configuring the BambooHR environment and setting up the connector prerequisites.

| Task | Role |
|------|------|
| [Create a BambooHR developer account](#create-a-bamboohr-developer-account) | BambooHR admin |
| [Register a BambooHR application](#register-a-bamboohr-application) | BambooHR admin |
| [Configure redirect URLs](#configure-redirect-urls) | BambooHR admin |
| [Select application scopes](#select-application-scopes) | BambooHR admin |
| [Obtain client credentials](#obtain-client-credentials) | BambooHR admin |

## Create a BambooHR developer account

1. Go to the [BambooHR developer portal](https://developers.bamboohr.com/).
2. Sign in with your existing BambooHR developer account credentials, or create a new developer account.

> [!NOTE]
> The developer portal is separate from your main BambooHR instance and is used specifically for creating and managing API applications that integrate with BambooHR.

## Register a BambooHR application

1. In the developer portal, create a new BambooHR app.
2. Enter a unique application name, such as "Microsoft 365 Copilot connector" or your organization's name.

[![Screenshot of Add application.](media/bamboohr-connector/bamboohr-add-application.png)](media/bamboohr-connector/bamboohr-add-application.png#lightbox)

## Configure redirect URLs

1. In the app details section, add the redirect URL that Microsoft 365 uses to communicate with BambooHR during authentication.
2. Copy and paste the following URL: `https://gcs.office.com/v1.0/admin/oauth/callback`

[![Screenshot of App Details.](media/bamboohr-connector/bamboohr-application-details.png)](media/bamboohr-connector/bamboohr-application-details.png#lightbox)

[![Screenshot of Redirect URLs form.](media/bamboohr-connector/bamboohr-redirect-uri.png)](media/bamboohr-connector/bamboohr-redirect-uri.png#lightbox)

## Select application scopes

In the application scopes section, select the required permissions with read-only access to ensure the connector can retrieve the necessary profile information:

| Category | Required scopes |
|----------|----------------|
| Claims | email, openid |
| Employee | employee, employee:contact, employee:identification, employee:job, employee:management, employee:name, employee_directory, sensitive_employee:protected_info |
| Miscellaneous | field, offline_access, public.user |
| Reports | report |

:::image type="content" source="media/bamboohr-connector/bamboohr-select-scopes.png" alt-text="Screenshot of Select Scopes." lightbox="media/bamboohr-connector/bamboohr-select-scopes.png":::

[![Screenshot of Scope Selection.](media/bamboohr-connector/bamboohr-scope-selection.png)](media/bamboohr-connector/bamboohr-scope-selection.png#lightbox)

## Obtain client credentials

1. Go to the **App credentials** section.
2. Record the **App client ID** and **App client secret**. Use these credentials to authenticate the Microsoft 365 connector with your BambooHR application during setup.

:::image type="content" source="media/bamboohr-connector/bamboohr-client-id-and-secret.png" alt-text="Screenshot of Client ID and Client Secret section." lightbox="media/bamboohr-connector/bamboohr-client-id-and-secret.png":::

## Next step

> [!div class="nextstepaction"]
> [Deploy the BambooHR connector](bamboohr-deployment.md)
