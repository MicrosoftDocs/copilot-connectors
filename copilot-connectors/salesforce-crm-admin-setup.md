---
title: Set up the Salesforce service for Salesforce CRM connector ingestion
description: Get the steps that the Salesforce CRM admin needs to complete for your organization to configure the Salesforce CRM Microsoft 365 Copilot connector.
author: lauragra
ms.author: lauragra
manager: calvind
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 6/18/2026
---

# Set up the Salesforce service for Salesforce CRM connector ingestion

The Salesforce CRM Microsoft 365 Copilot connector allows your organization to index contacts, opportunities, leads, cases, and accounts objects in your Salesforce instance. After you configure the connector and index content from Salesforce, users can search for those items from any Microsoft Search and Microsoft 365 Copilot client.

This article provides information about the configuration steps that Salesforce admins need to complete in order for your organization to deploy the Salesforce CRM connector.

For information about how to deploy the connector, see [Deploy the Salesforce CRM connector](salesforce-crm-deployment.md).

## Prerequisites

Before you configure the service, make sure you have:

- A Salesforce account with **System Administrator** privileges.
- API access enabled for the account.
- Permissions to create and manage External Client Apps in Salesforce.
- Access to the Microsoft 365 admin center.

## Setup checklist

The following checklist lists the steps involved in configuring the environment and setting up the connector prerequisites.

| Task | Role |
|------|------|
| [Identify Salesforce instance URL](#identify-the-salesforce-instance-url) | Salesforce CRM admin |
| [Enable API access](#enable-api-access) | Salesforce CRM admin |
| [Create an External Client App](#create-an-external-client-app) | Salesforce CRM admin |
| [Configure refresh token policy](#configure-refresh-token-policy) | Salesforce CRM admin |
| [Define identity mapping](#define-identity-mapping) | Salesforce CRM admin |
| [Determine data ingestion filters](#determine-data-to-ingest) | Salesforce CRM admin |
| [Verify field-level security (FLS) settings](#verify-field-level-security-fls-settings) | Salesforce CRM admin |

## Identify the Salesforce instance URL

To connect to your Salesforce instance, you need your organization's Salesforce instance URL.

- In Salesforce, go to **Settings** > **Company Settings** > **My Domain** > **My Domain URL**.
- The URL format is: `https://<your-organization>.my.salesforce.com`. For example: `https://contoso.my.salesforce.com`

## Enable API access

Make sure that the connector account has API access:

- Assign the **System Administrator** profile, or verify the following permissions for custom profiles:
    - **Administrative permissions**:
       - API Enabled
       - View Setup and Configuration
       - View Roles and Role Hierarchy
       - View All Profiles
       - View All Users
    - **Standard object permissions**:
       - Read and View All for Accounts, Cases, Contacts, Leads, and Opportunities.

## Create an External Client App

Set up an External Client App for OAuth 2.0 authentication. External Client Apps are Salesforce's current framework for registering OAuth integrations (replacing the deprecated Connected App model).

1. Sign in to Salesforce and go to **Setup**.
1. Go to **Apps** > **External Client Apps** > **External Client App Manager**.
1. Select **New External Client App** (top-right).
1. Fill in the required fields:
    - **External Client App Name**: Enter a descriptive name (for example, `M365CopilotConnector`).
    - **Contact Email**: Enter the email address of the Salesforce admin managing this integration.
1. Select **Create**.

### Configure OAuth settings

1. On the External Client App detail page, select the **Settings** tab.
1. Select **Edit** (top-right of the Settings panel).
1. Expand the **OAuth Settings** section.
1. Check **Enable OAuth Settings**. Additional fields appear.
1. Set the **Callback URL**:
    - For Microsoft 365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`
    - For Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
1. Move the following scopes from **Available OAuth Scopes** to **Selected OAuth Scopes**:
    - Manage user data via APIs (api)
    - Perform requests at any time (refresh_token, offline_access)
1. Under **OAuth flows**, check **Enable Authorization Code and Credentials Flow**.
1. Under the security section:
    - Leave **Require Secret for Web Server Flow** checked (default).
    - Clear **Require Proof Key for Code Exchange (PKCE)**.
1. Select **Save**.

### Get client ID and secret

1. On the External Client App detail page, in the OAuth Settings section, select **Consumer Key and Secret**.
1. Complete the email verification if prompted (one-time per session).
1. Copy the **Consumer Key** (client ID) and **Consumer Secret** (client secret).

> [!NOTE]
> The **Consumer Key and Secret** page requires email verification the first time you access it in a session. Salesforce sends a verification code to the contact email address configured for the app.

## Configure refresh token policy

To prevent token expiration:

1. On the External Client App detail page, select the **Policies** tab.
1. In the **OAuth Policies** section, locate **Refresh Token Policy**.
1. Set the value to **Refresh token is valid until revoked**.
1. Select **Save**.

> [!IMPORTANT]
> Without this setting, the refresh token expires (default 24 hours), which causes the connection to go stale and require manual re-authorization.

## Define identity mapping

Your data source can include:

- **Microsoft Entra identities** (federated users). For more information, see [Map Microsoft Entra identities](/microsoft-365/copilot/connectors/map-entra-id) and [Configure Salesforce for Single sign-on in Microsoft Entra ID](/entra/identity/saas-apps/salesforce-tutorial).
- **Non-Microsoft Entra identities** (native Salesforce users). For more information, see [Map non-Microsoft Entra identities](/microsoft-365/copilot/connectors/map-non-entra-id).

## Determine data to ingest

You can filter indexed Salesforce content by:
- **Modified time period**: Index items created or modified within a selected rolling time frame.
- **SOQL query**: Use a WHERE clause to specify entities and conditions. Leave empty to index all content. For more information, see [SOQL and SOSL Reference](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql_select_conditionexpression.htm).

## Verify field-level security (FLS) settings

If your Salesforce org uses field-level security to hide fields from specific profiles or permission sets, the connector detects these restrictions and excludes the affected fields from the crawl by default. You can opt in to indexing specific FLS-restricted fields on the **Content** tab in the Microsoft 365 admin center. Before deploying the connector:

- Confirm the Salesforce user account that signs in to the connector has permission to read FLS metadata. The **System Administrator** profile already includes this access. For custom profiles, ensure **View Setup and Configuration** and **View All Profiles** are enabled (see [Enable API access](#enable-api-access)).
- Verify the FLS settings for the indexed objects and decide which FLS-restricted fields are safe to index in Microsoft 365 and which must stay excluded.

For information about how to opt in to FLS-restricted fields in the Microsoft 365 admin center, see [Include FLS-restricted fields](salesforce-crm-deployment.md#include-fls-restricted-fields).

## Next step

> [!div class="nextstepaction"]
> [Deploy the Salesforce CRM connector](salesforce-crm-deployment.md)
