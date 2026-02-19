---
title: Set up the Jira Cloud service for Jira Cloud Microsoft 365 Copilot connector ingestion
description: Get the steps that the Jira Cloud admin needs to complete for your organization to configure the Jira Cloud Microsoft 365 Copilot connector.
author: lauragra
ms.author: lauragra
manager: calvind
ms.reviewer: jecui
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 11/11/2025
---

# Set up the Jira Cloud service for Jira Cloud Copilot connector ingestion

The Jira Cloud connector for Microsoft 365 Copilot and Microsoft Search allows your organization to index and search Jira Cloud content directly within Microsoft 365 experiences. By integrating Jira Cloud with Microsoft 365, users can discover issues, projects, and other Jira data through Copilot and Microsoft Search, improving productivity and collaboration. 

This article provides information about the configuration steps that Jira Cloud admins need to complete in order for your organization to deploy the Jira Cloud Copilot connector for your organization.

For information about how to deploy the connector, see [Jira Cloud Copilot connector](jira-cloud-overview.md).

## Prerequisites

Before you begin, make sure that you meet the following prerequisites:

- You must be a **Jira Cloud site admin** and a **Microsoft 365 global admin**.
- Confirm that Jira REST APIs are enabled and accessible.
- Make sure that your organization allows outbound connections to Microsoft Graph connector IPs if network restrictions apply.
- Make sure that you have access to the [Atlassian Developer Console](https://developer.atlassian.com/console/myapps/).

## Setup checklist

| Task | Role |
|------|------|
| [Identify the Jira Cloud instance URL](#identify-the-jira-cloud-instance-url) | Jira admin |
| [Enable API access](#enable-api-access) | Jira admin |
| [Create an OAuth 2.0 app](#create-an-oauth-20-app) | Jira admin |
| [Define attribute mapping](#define-attribute-mapping) | Jira admin |
| [Create a service account](#create-a-service-account) | Jira admin |
| [Estimate content scope](#estimate-content-scope) | Jira admin |

## Identify the Jira Cloud instance URL

The Jira Cloud instance URL is required when you deploy the connector in the Microsoft 365 admin center. To identify the Jira Cloud instance URL:

- Sign in to your Jira Cloud account at `https://<yourcompany>.atlassian.net`.
- From the dashboard, note the **base URL** in the browser address bar. For example: `https://<yourcompany>.atlassian.net`.

> [!NOTE]
> - Don't use a project-specific URL (such as `/browse/PROJ-123`).
> - Test the URL in a browser to confirm that it resolves to your Jira dashboard.  

## Enable API access

Verify that Jira Cloud REST APIs are enabled by default and that no API restrictions or app allowlists prevent access.

If your organization uses network-level restrictions, add the Microsoft Graph connector IPs to the allowlist.

## Create an OAuth 2.0 app

When you deploy the connector, you need the **client ID** and **client secret** for [OAuth 2.0 authentication](jira-cloud-deployment.md#3-provide-authentication-type). To create an OAuth 2.0 app:

- Go to https://developer.atlassian.com/console/myapps/ and sign in with your Jira admin account.
- Select **Create** and choose **OAuth 2.0 integration**.
- Enter a name for the app and create it.
- Under **Authorization**, add the callback URL: `https://gcs.office.com/v1.0/admin/oauth/callback`
- Copy the **Client ID** and **Client Secret** from **Settings**.  

## Define attribute mapping

Configure attribute mappings in the Microsoft 365 Copilot connector to determine how Jira data appears in Microsoft 365 Copilot and Microsoft Search experiences.

## Create a service account

To create a service account:

- Sign in to the [Atlassian Admin Console](https://admin.atlassian.com/) as an org or site admin.
- Go to **Directory > Users**.
- Choose **Invite users** and enter a dedicated email address, such as: `jira-connector@yourdomain.com`. Don't use a personal account.
- Under **Products**, select **Jira Software**.
- Don't assign admin or project admin roles unless required.
- Make sure that the account has **Browse Projects** and **View Issues** permissions.

## Estimate content scope

Determine the number of projects and issues to index. For instances with more than 10,000 issues:

- Enable incremental sync.
- Plan for throttling.
- Full indexing can take several hours. Schedule the initial sync during off-business hours.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Jira Cloud connector](jira-cloud-deployment.md)