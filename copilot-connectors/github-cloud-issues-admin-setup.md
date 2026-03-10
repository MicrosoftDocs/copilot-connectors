---
title: Set up the GitHub service for GitHub Cloud Issues Microsoft 365 Copilot connector ingestion
description: "Get the steps that the GitHub admin needs to complete to configure the service for your organization so you can deploy the GitHub Cloud Issues Microsoft 365 Copilot connector."
author: Lauragra
ms.author: lauragra
ms.reviewer: lauragra
manager: calvind
ms.date: 03/09/2026
ms.service: copilot-connectors
ms.topic: concept-article
---

# Set up the GitHub service for GitHub Cloud Issues connector ingestion

The GitHub Cloud Issues Microsoft 365 Copilot connector allows your organization to index issues stored in GitHub to make them available in Microsoft 365 Copilot and search experiences. This article provides information about the configuration steps that GitHub admins must complete before your organization deploys the GitHub Cloud Issues connector.

For information about how to deploy the connector, see [Deploy the GitHub Issues connector](/microsoftsearch/github-cloud-issues-deployment).

## Setup checklist

The following checklist lists the steps involved in configuring the environment and setting up the connector prerequisites.

| **Task**                                              | **Role**     |
|-------------------------------------------------------|--------------|
| [Identify the GitHub organization name](#identify-the-github-organization-name)                        | GitHub admin |
| [Ensure API access to the target GitHub instance](#ensure-api-access-to-the-target-github-instance)   | GitHub admin |
| [Identify Microsoft Entra ID mapping rules](#identify-entra-id-mapping-rules)  | GitHub admin |
| [Sign in to the GitHub account](#sign-in-to-the-github-account)                         | GitHub admin |
| [Use a custom GitHub app for authentication](#use-a-custom-github-app-for-authentication-optional)(optional) | GitHub admin |
| [Configure firewall settings](#configure-firewall-settings) | Network admin |

## Identify the GitHub organization name

Determine which GitHub organization you want to index when you set up the connector.

## Ensure API access to the target GitHub instance

Confirm that your GitHub instance is accessible via API.

## Identify Entra ID mapping rules

Define the Entra ID mapping rules. Make sure that users who access the indexed GitHub data have corresponding Entra ID identities to enable accurate permission mapping.

## Sign in to the GitHub account

For enterprise-managed users who authenticate through single sign-on (SSO), make sure the account is signed in before you perform any setup actions. Currently, the GitHub authentication flow doesn't support SSO-based sign-in during configuration.

## Use a custom GitHub app for authentication (optional)

For the most streamlined setup experience, use the GitHub app managed by Microsoft.

You can also choose to use your own GitHub app for authentication. If you choose this option, follow the steps in the following checklist to complete the setup.

| **Task**                             | **Role**     |
|--------------------------------------|--------------|
| [Create and configure the GitHub app](#create-and-configure-the-github-app)  | GitHub admin |
| [Create credentials for the GitHub app](#create-credentials-for-the-github-app) | GitHub admin |
| [Install the GitHub app](#install-the-github-app)               | GitHub admin |

### Create and configure the GitHub app

To create a GitHub app for use with the GitHub Cloud Issues connector:

1. In GitHub, select your profile photo on the top right, select **Your organizations**, and choose the organization the connector should pull data from.

:::image type="content" source="./media/github-cloud-issues-admin-setup/github-your-organizations.png" alt-text="Screenshot of GitHub with Your organizations highlighted":::

2. On the organization overview page, select **Settings**.

:::image type="content" source="./media/github-cloud-issues-admin-setup/github-settings.png" alt-text="Screenshot of GitHub with Settings highlighted":::

3. In the left sidebar, scroll down to **Developer settings** and select **GitHub Apps**.

:::image type="content" source="./media/github-cloud-issues-admin-setup/github-apps.png" alt-text="Screenshot of GitHub with GitHub Apps highlighted":::

4.  Select **New GitHub App**.

:::image type="content" source="./media/github-cloud-issues-admin-setup/new-github-app.png" alt-text="Screenshot of GitHub with New GitHub App highlighted":::

5.  Configure the app:

    - **GitHub app name**: Enter the name of your choice.
    - **Homepage URL**: Copy the URL from your browser's address bar.
    - **Callback URL**:
      - For Microsoft 365 for enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`
      - For Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`

    :::image type="content" source="./media/github-cloud-issues-admin-setup/callback-url.png" alt-text="Screenshot of GitHub with Callback URL highlighted":::

6.  Uncheck the **Webhook** option.

7.  Set the following permissions:

    **Repository permissions**
      - Administration - **Read-only**
      - Metadata - **Read-only**
      - Issues - **Read-only**
      - Webhooks - **Read and Write**

    **Organization permissions**
      - Administration - **Read-only**
      - Members - **Read-only**
      - Webhooks - **Read and Write**

    **Account permissions**
      - Email addresses - **Read-only**

    > [!NOTE]
    > Webhook support is currently available in preview. Be sure to set the Webhooks (Read and Write) permissions at both the Repository and Organization levels. Webhooks allow you to take advantage of enhanced automation and real-time updates to ensure a more seamless and responsive integration experience.

8.  Under **Where can this GitHub App be installed**, select **Any account**, and then select **Create GitHub App**.

:::image type="content" source="./media/github-cloud-issues-admin-setup/create-github-app.png" alt-text="Screenshot of GitHub with Permissions, Any account, and Create GitHub App highlighted":::

### Create credentials for the GitHub App

Depending on the authentication method you plan to use, generate either a client secret or a private key. You don't need both.

- **For custom GitHub app (on behalf of user) authentication:** On the **General** page of the GitHub app, select **Generate a new client secret** to generate and copy the **client secret**.

    :::image type="content" source="./media/github-cloud-issues-admin-setup/new-client-secret.png" alt-text="Screenshot of GitHub with Generate a new client secret highlighted" lightbox="./media/github-cloud-issues-admin-setup/new-client-secret.png":::

- **For custom GitHub app (installation) authentication:** On the **General** page of the GitHub app, scroll down to the **Private keys** section and select **Generate a private key**. Save the downloaded `.pem` file securely.

    :::image type="content" source="./media/github-cloud-issues-admin-setup/generate-private-key.png" alt-text="Screenshot of the GitHub App Private keys section with Generate a private key button." lightbox="./media/github-cloud-issues-admin-setup/generate-private-key.png":::

### Install the GitHub App

1.  On the **General** page of the GitHub app, select **Install App**.  
    
    :::image type="content" source="./media/github-cloud-issues-admin-setup/install-app.png" alt-text="Screenshot of GitHub with Install App highlighted":::

2.  Select the organization where you want to install the app.

    :::image type="content" source="./media/github-cloud-issues-admin-setup/install-authorize.png" alt-text="Screenshot of GitHub with Install & Authorize highlighted":::

## Configure firewall settings

For added security, you can configure IP firewall rules for your Azure SQL Server or database. For more information, see [IP firewall rules](/azure/azure-sql/database/firewall-configure).

Add the following client IP ranges in the firewall settings.

| Region | Microsoft 365 Enterprise                  | Microsoft 365 Government                 |
|--------|-------------------------------------------|------------------------------------------|
| NAM    | 52.250.92.252/30, 52.224.250.216/30       | 52.245.230.216/30, 20.141.117.64/30      |
| EUR    | 20.54.41.208/30, 51.105.159.88/30         | NA                                       |
| APC    | 52.139.188.212/30, 20.43.146.44/30        | NA           |

IP restrictions can cause the connector to stop working and lead to crawl failures. To resolve this issue, add the connector's IP address to the allowlist.

## Next step

> [!div class="nextstepaction"]
> [Deploy the GitHub Issues connector](/microsoftsearch/github-cloud-issues-deployment)