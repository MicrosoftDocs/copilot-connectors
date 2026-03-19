---
title: "Set up the Egnyte service for Egnyte Microsoft 365 Copilot connector ingestion"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: anggao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 12/16/2025
ms.localizationpriority: Medium
description: "Get the steps that the Egnyte admin needs to complete for your organization to configure the Egnyte Microsoft 365 Copilot connector."
---

# Set up the Egnyte service for Egnyte connector ingestion

The Egnyte Microsoft 365 Copilot connector allows your organization to index files stored in Egnyte so users can retrieve them through Microsoft 365 Copilot and Microsoft Search. This article describes the Egnyte service configuration that Egnyte admins must complete before your organization can deploy the [Egnyte connector](egnyte-overview.md). These steps ensure that Microsoft 365 can authenticate with your Egnyte domain, access required APIs, and ingest content securely.

For information about how to deploy the connector in Microsoft 365, see  
[Deploy the Egnyte connector](egnyte-deployment.md).

## Setup checklist

The following checklist lists the steps involved in configuring the environment and setting up the connector prerequisites.

> [!NOTE]
> You must have an Egnyte admin role in your organization's Egnyte domain to complete these steps.

| Task | Role |
|------|------|
| [Register an Egnyte developer account](#register-an-egnyte-developer-account) | Egnyte admin |
| [Create a new app for the Egnyte connector](#create-a-new-app-for-the-egnyte-connector) | Egnyte admin |
| [Get the client ID (API key) and secret](#get-the-client-id-key-and-secret) | Egnyte admin |
| [Request an API rate increase](#request-a-rate-increase-from-egnyte) | Egnyte admin |
| [Enable API access](#enable-api-access-and-confirm-required-settings) | Egnyte admin |

## Register an Egnyte developer account

To create the API key and secret required for the connector, you need an Egnyte developer account. To register an Egnyte developer account:

1. Go to the [Egnyte developer portal](https://developers.egnyte.com/member/register). 
2. Register with an admin email for your Egnyte domain.

## Create a new app for the Egnyte connector

To register the connector app:

1. Sign in to the developer portal with your Egnyte developer account, and from the account menu, open **Apps**.
2. In **My Apps**, select **+ NEW APP**.  
3. Complete the required app registration fields:

    - **Egnyte Domain**: Enter only the domain prefix (for example, if your Egnyte URL is `https://<your-domain>.egnyte.com`, enter `your-domain`).
    - **Registered OAuth Redirect URI**:
      - Microsoft 365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`
      - Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
    - **Application Type**: Select **Publicly Available Application** (required for authentication from the Microsoft 365 admin center).
    - **APIs**: Enable the APIs required for your scenario:
      - **Prod Collaborate: Egnyte Public REST API**
      - **Prod_SnG: Egnyte Secure and Govern Public API**

:::image type="content" alt-text="Screenshot of the app registration fields." source="media/egnyte/egnyte-app-registration.png" lightbox="media/egnyte/egnyte-app-registration.png":::

## Get the client ID (key) and secret

After Egnyte approves your API settings:

1. In the Egnyte developer portal, go to **API Keys**.
2. Copy the **Client ID (Key)** and **Secret**.

Use these credentials when you configure the connector in the Microsoft 365 admin center.

:::image type="content" alt-text="Screenshot of the API key and secret for an Egnyte app." source="media/egnyte/egnyte-client-id.png" lightbox="media/egnyte/egnyte-client-id.png":::

## Request a rate increase from Egnyte

The connector syncs data from Egnyte to Microsoft Graph. Egnyte imposes API rate limits that vary by plan.

To avoid ingestion failures:

- Sign in to your Egnyte developer account and check your current API rate limits.
- Review the [Public API usage restrictions](https://helpdesk.egnyte.com/hc/articles/17683455594125-Public-API-Usage-Restrictions-by-Plan) for Egnyte.   
- If you need higher limits, contact Egnyte support.

## Enable API access and confirm required settings

To ensure that your connector can authenticate and crawl Egnyte data:

- **API access**: Confirm that the required APIs are enabled for your app.
- **Domain configuration**: Make sure that the domain in the developer app matches your Egnyte tenant.
- **Redirect URIs**: Verify that your redirect URI matches the appropriate Microsoft 365 environment.
- **Application type**: Make sure that **Publicly Available Application** is selected.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Egnyte connector](egnyte-deployment.md)