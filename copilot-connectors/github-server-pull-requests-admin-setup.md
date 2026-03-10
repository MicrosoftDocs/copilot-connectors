---
title: "Set up the GitHub service for GitHub Server Pull Requests connector ingestion"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 03/09/2026
ms.localizationpriority: Medium
description: "Get the steps that GitHub admins need to complete to configure the GitHub Server Pull Requests Microsoft 365 Copilot connector."
---

# Set up the GitHub service for GitHub Server Pull Requests connector ingestion

This article provides information about the configuration steps that GitHub admins must complete for your organization to deploy the GitHub Server Pull Requests connector. When configured, the connector indexes pull request data from GitHub Enterprise Server so users can search, summarize, and retrieve PR information in Microsoft Search, Microsoft 365 Copilot, and Copilot Search.

This article applies to the GitHub Server Pull Requests connector. For information about how to deploy the connector, see [Deploy the GitHub Server Pull Requests connector](github-server-pull-requests-deployment.md).

## Setup checklist

The following checklist lists the steps involved in configuring the GitHub Server environment and setting up the connector prerequisites.

| **Task** | **Role** |
|----------|----------|
| [Identify the organization name](#identify-the-organization-name) | GitHub admin |
| [Ensure API access to the target GitHub instance](#ensure-api-access-to-the-target-github-instance) | GitHub admin |
| [Identify Microsoft Entra ID identity mapping rules](#identify-microsoft-entra-id-mapping-rules) | GitHub admin |
| [Sign in to the GitHub account](#sign-in-to-the-github-account) | GitHub admin |
| [Configure a custom GitHub app for authentication](#use-a-custom-github-app-for-authentication) | GitHub admin |
| [Adjust GitHub Server API rate limit](#adjust-github-server-api-rate-limit) | GitHub admin |
| [Configure firewall settings](#configure-firewall-settings) | Network admin |

## Identify the organization name

Determine which GitHub Enterprise Server organization the connector will use for PR ingestion. The connector indexes only the content accessible to the GitHub App installed in the selected organization.

## Ensure API access to the target GitHub instance

Confirm that your GitHub Enterprise Server instance is reachable via API. The connector requires API access to retrieve pull request metadata. Make sure that:

- The GitHub instance is accessible over HTTPS.
- Firewall or network restrictions allow inbound/outbound API requests.
- The Graph Connector Agent host device can reach the GitHub Enterprise Server domain.

## Identify Microsoft Entra ID mapping rules

Define the Microsoft Entra ID mapping rules. Identity mapping ensures correct permissions enforcement when users access PR data in Copilot and search experiences.

Supported mapping strategies include:

- **Email:** Matches GitHub email addresses to Microsoft Entra ID properties.
- **Login:** Maps GitHub usernames to Microsoft Entra ID attributes.
- **Name:** Uses the GitHub profile name for mapping.

If identities don't match directly, you can use regular expressions (regex) to normalize data. For example: `[a-zA-Z0-9]+`

Users must share the required GitHub identity attributes, especially in Bring Your Own User (BYOU) environments.

## Sign in to the GitHub account

If your organization uses single sign‑on (SSO), sign in to GitHub before configuring the connector. Currently, the GitHub Server Pull Requests connector doesn't support completing authentication flows that rely on SSO during connector configuration.

## Use a custom GitHub app for authentication

For the most streamlined setup experience, use the GitHub app managed by Microsoft.

You can also choose to use your own GitHub app for authentication. If you choose this option, follow the steps in the following checklist to complete the setup.

| **Task**                             | **Role**     |
|--------------------------------------|--------------|
| [Create and configure the GitHub app](#create-and-configure-the-github-app)  | GitHub admin |
| [Create credentials for the GitHub app](#create-credentials-for-the-github-app) | GitHub admin |
| [Install the GitHub app](#install-the-github-app)  | GitHub admin |

### Create and configure the GitHub app

Verify that you have the right permissions assigned to configure the GitHub service. For more information, see [Roles in an organization](https://docs.github.com/en/organizations/managing-peoples-access-to-your-organization-with-roles/roles-in-an-organization#permissions-for-organization-roles).

To create a GitHub app for use with the GitHub Server Pull Requests connector:

1. In GitHub, select your profile photo on the top right, select **Organizations**, and choose the organization the connector should pull data from.

    :::image type="content" alt-text="Screenshot that shows how to access 'Your organizations'." source="media/github-server-admin-setup/organizations-nav.png" lightbox="media/github-server-admin-setup/organizations-nav.png":::

2. On the organization overview page, select **Settings**.

   :::image type="content" alt-text="Screenshot that shows how to access 'Settings' within the organization page." source="media/github-server-admin-setup/organization-overview.png" lightbox="media/github-server-admin-setup/organization-overview.png":::

3. In the left sidebar, scroll down to **Developer settings** and select **GitHub Apps**.

    :::image type="content" alt-text="Screenshot that shows how to access GitHub Apps." source="media/github-server-admin-setup/github-apps.png" lightbox="media/github-server-admin-setup/github-apps.png":::

4. Select **New GitHub App**.

    :::image type="content" alt-text="Screenshot that shows entry point to creation of new app." source="media/github-server-admin-setup/new-github-app.png" lightbox="media/github-server-admin-setup/new-github-app.png":::

5. Configure the app:

    - **GitHub App name**: Enter the name of your choice.
    - **Homepage URL**: Copy the URL from your browser's address bar.
    - **Callback URL**:
      - For Microsoft 365 for enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`
      - For Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`

    :::image type="content" alt-text="Screenshot that shows the initial part of the app configuration including name and URLs." source="media/github-server-admin-setup/github-app1.png" lightbox="media/github-server-admin-setup/github-app1.png":::

6. Uncheck the **Webhook** option.

7. Set the following permissions:

    **Repository permissions**
    - Contents - **Read-only**
    - Metadata - **Read-only**
    - Administration - **Read-only**
    
    **Organization permissions**
    - Members - **Read-only**
    - Administration - **Read-only**
    
    **Account permissions**
    - Email addresses - **Read-only**

8. Under **Where can this GitHub App be installed**, select **Any account**, and then select **Create GitHub App**.

### Create credentials for the GitHub app

Depending on the authentication method you plan to use, generate either a client secret or a private key. You don't need both.

- **For custom GitHub app (on behalf of user) authentication:** On the **General** page of the GitHub app, select **Generate a new client secret** to generate and copy the **client secret**.

    :::image type="content" alt-text="Screenshot that shows the credentials of the app, including Client Id and Client secret." source="media/github-server-admin-setup/github-app-credentials.png" lightbox="media/github-server-admin-setup/github-app-credentials.png":::

- **For custom GitHub app (installation) authentication:** On the **General** page of the GitHub app, scroll down to the **Private keys** section and select **Generate a private key**. Save the downloaded `.pem` file securely.

    :::image type="content" source="media/github-server-admin-setup/generate-private-key.png" alt-text="Screenshot of the GitHub App Private keys section with Generate a private key button." lightbox="media/github-server-admin-setup/generate-private-key.png":::

### Install the GitHub app

1. On the **General** page of the GitHub app, select **Install App**. 

    :::image type="content" alt-text="Screenshot that shows the app installation dialog." source="media/github-server-admin-setup/github-install.png" lightbox="media/github-server-admin-setup/github-install.png":::

2. Select the organization where you want the app to be installed.

## Adjust GitHub Server API rate limit

When you ingest large volumes of GitHub data—such as pull requests, issues, or knowledge files—the API rate‑limit configuration in your GitHub Server environment directly affects how quickly the ingestion process is completed. GitHub Server applies a default API limit of 15,000 authenticated requests per hour per user or token. This limit supports smaller datasets, but can slow ingestion when hundreds of thousands or millions of items are processed.

If your organization needs to increase throughput, you can raise the API rate limit. Higher limits allow the connector to retrieve items more quickly, but they also increase load on your GitHub Server infrastructure. Before you update rate‑limit settings, verify that your environment has adequate CPU capacity, storage I/O, and network bandwidth to support the increased request volume. After you update the limit, monitor system performance to ensure stable ingestion at higher throughput.

### Rate-limit setting recommendations

Use the guidance in the following table to help you choose an appropriate rate‑limit setting based on the approximate number of pull requests in your GitHub environment.

| Approximate number of items | Recommended rate-limit setting | Approximate time to complete ingestion |
|-----------------------------|--------------------------------|----------------------------------------|
| Up to 100,000 | Use default rate‑limit settings (normal ingestion speed) | NA |
| 100,000 to 1,000,000 | Increase rate limit to 30,000 requests/hour | 2 days to 1 week |
| 1,000,000 or more | Use 30,000 requests/hour or higher (depending on server capacity) | 1–2 weeks (varies by environment load) |

### Update the API rate-limit setting

To increase the API request limit:

1. Sign in to your GitHub Server instance with an admin account.
1. In the upper‑right corner, select **Site admin** to enter administration mode. For more information, see [Configuring rate limits](https://docs.github.com/en/enterprise-server@3.16/admin/configuring-settings/configuring-user-applications-for-your-enterprise/configuring-rate-limits?utm_source=chatgpt.com).
1. In the left pane, select **Management Console** (or **Admin Console**, depending on your version).
1. Open the **Rate limiting** tab.
1. Confirm that **Enable HTTP API** rate limiting is selected.
1. Under **API requests (per hour) – Authenticated**, enter the rate‑limit value (for example, **30000**).
1. Select **Save settings**.

:::image type="content" source="./media/github-server-rate-limit.png" alt-text="Screenshot of the Rate limiting tab in GitHub Server with API Requests and Save settings highlighted.":::

> [!NOTE]
> When you save your changes, certain GitHub Server services might restart and cause a brief service interruption. After you save, allow time for the configuration to propagate across the instance.

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
> [Deploy the GitHub Server Pull Requests connector](github-server-pull-requests-deployment.md)