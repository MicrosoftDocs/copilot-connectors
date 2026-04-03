---
title: "Set up the Miro service for Miro connector ingestion"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: anggao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 01/28/2026
ms.localizationpriority: Medium
description: "Get the steps that the Miro admin needs to complete for your organization to configure the Miro Microsoft 365 Copilot connector."
---

# Set up the Miro service for Miro connector ingestion

The Miro Microsoft 365 Copilot connector allows your organization to index boards from Miro. After you configure the connector, users can search for these boards from Miro in Microsoft 365 Copilot and from any Microsoft Search client.

This article provides information about the configuration steps that Miro admins need to complete before your organization deploys the [Miro connector](miro-overview.md).

For information about how to deploy the connector, see [Deploy the Miro connector](miro-deployment.md).

## Setup checklist

The following checklist lists the steps involved in setting up the Miro service.

| Task | Role |
|------|------|
| [Create a Developer team for your Miro account](#create-a-developer-team-for-your-miro-account) | Miro admin |
| [Create app in Miro](#create-your-app-in-miro) | Miro admin |
| [Grant Content Admin role](#grant-your-account-the-content-admin-role) | Miro company admin |
| [Install your app at company level](#install-your-app-at-the-company-level) | Miro company admin |

## Create a Developer team for your Miro account

Create or use an existing Miro account and [create a Developer team](https://miro.com/app/dashboard/?createDevTeam=1) for your active Miro account. If your organization uses the Miro Enterprise plan, use [Enterprise Developer teams](https://help.miro.com/hc/articles/4766759572114). Miro requires a Developer team to create and manage apps used for connector ingestion.

For more information, see [Create a Developer team](https://developers.miro.com/docs/create-a-developer-team).

## Create your app in Miro

1. Sign in to Miro and create a new app from [Your apps](https://miro.com/app/settings/user-profile/apps) in your profile settings. This app is used to authorize Microsoft 365 Copilot to index content from your Miro instance.

    :::image type="content" source="media/miro-admin-setup/your-apps.png" alt-text="Screenshot of the Miro app creation page." lightbox="media/miro-admin-setup/your-apps.png":::

2. Add the following permissions to the app:

    - boards: read  
    - identity: read  
    - team: read  
    - organizations: read  
    - organizations:teams: read  
    - projects: read  

    :::image type="content" source="media/miro-admin-setup/add-permissions.png" alt-text="Screenshot of the Miro app permissions settings." lightbox="media/miro-admin-setup/add-permissions.png":::
    
    These scopes let the connector read boards, team membership, identities, and metadata required for indexing.

3. Add the following values to the **Redirect URL for OAuth 2.0** field:

    - For Microsoft 365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`
    - For Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`

    These URLs allow Microsoft 365 to complete the OAuth flow and retrieve credentials.

    :::image type="content" source="media/miro-admin-setup/redirect-url.png" alt-text="Screenshot of the redirect URL configuration field." lightbox="media/miro-admin-setup/redirect-url.png":::

## Grant your account the Content Admin role

Your account must be a Miro company admin with **Content admin** privileges to configure and authorize ingestion.  
In the Miro admin console:

1. Select **Team Settings**.  
2. Go to **Users** > **Admin roles** > **Content admin**.  
3. Assign the role to the appropriate account.

:::image type="content" source="media/miro-admin-setup/admin-role.png" alt-text="Screenshot of the Miro admin roles assignment interface." lightbox="media/miro-admin-setup/admin-role.png":::

## Install your app at the company level

To install the app at the company level:

1. Open the Miro admin console.  
2. Go to **Apps and integrations**.  
3. Select **Add apps**, and then enter the client ID of the app you created.  
4. Choose **All teams** and approve requested permissions.

:::image type="content" source="media/miro-admin-setup/app-installation.png" alt-text="Screenshot of the Miro app installation page at company level." lightbox="media/miro-admin-setup/app-installation.png":::

## Next step

> [!div class="nextstepaction"]
> [Deploy the Miro connector](miro-deployment.md)