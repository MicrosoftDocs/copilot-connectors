---
title: "Set up the Dropbox service for Dropbox connector ingestion"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: ang.gao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 11/21/2025
ms.localizationpriority: Medium
description: "Get the steps that the Dropbox admin needs to complete for your organization to configure the Dropbox Microsoft 365 Copilot connector."
---

# Set up the Dropbox service for Dropbox connector ingestion

The Dropbox connector for Microsoft 365 Copilot enables your organization to index Dropbox content - including team folders, shared folders, private folders, and Dropbox Paper documents - and surface the content in Microsoft 365 Copilot and Microsoft Search experiences. This article provides information about the configuration steps that Dropbox admins need to complete to deploy the [Dropbox connector](dropbox-overview.md).

For information about how to deploy the connector, see [Deploy the Dropbox connector](dropbox-deployment.md).

## Setup checklist

The following checklist lists the steps involved in configuring the environment and setting up the connector prerequisites.

| Task | Role |
|------|------|
| [Set up a team admin user](#set-up-a-team-admin-user) | Dropbox admin |
| [Configure a Dropbox app](#configure-a-dropbox-app) | Dropbox admin |
| [Add redirect URIs](#add-redirect-uris) | Dropbox admin |
| [Add API scopes](#add-api-scopes) | Dropbox admin |
| [Get app key and app secret](#get-app-key-and-app-secret) | Dropbox admin |

## Set up a team admin user

Create a Dropbox Business account and assign a team admin user. This account is used to authorize the connector.

## Configure a Dropbox app

To configure a Dropbox app:

- Go to the [Dropbox developer portal](https://www.dropbox.com/developers/apps/) and select **Create app**.

  :::image type="content" source="media/dropbox/dropbpx-create-app.png" alt-text="Screenshot of the Create app button in the Dropbox developer portal." lightbox="media/dropbox/dropbpx-create-app.png":::

- Configure the app with:

    - A unique app name
    - Scoped access
    - Full Dropbox access permissions
    
 :::image type="content" source="media/dropbox/dropbox-prerequisites-2.png" alt-text="Screenshot of the app configuration fields." lightbox="media/dropbox/dropbox-prerequisites-2.png":::

For more information, see [Getting started with Dropbox](https://www.dropbox.com/developers/reference/getting-started).

## Add redirect URIs

In the **OAuth 2.0** section of the Dropbox App Console, add the following URLs:

- For Microsoft 365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`
- For Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`

 :::image type="content" source="media/dropbox/dropbox-add-directurl.png" alt-text="Screenshot of the Redirect URIs field." lightbox="media/dropbox/dropbox-add-directurl.png":::

## Add API scopes

Go to the **Permissions** tab and add the following API scopes:

**Individual scopes**

- files.metadata.read
- files.content.read
- sharing.read
- file_requests.read

**Team scopes**

- team_info.read
- team_data.member
- team_data.governance.write
- team_data.governance.read
- team_data.content.read
- files.team_metadata.read
- members.read
- groups.read
- events.read

:::image type="content" source="media/dropbox/dropbox-api-scopes.png" alt-text="Screenshot of the permissions tab." lightbox="media/dropbox/dropbox-api-scopes.png"::: 

## Get app key and app secret

From the **Settings** tab in the Dropbox App Console, copy the app key and app secret. These credentials are required for connector authentication.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Dropbox connector](dropbox-deployment.md)
