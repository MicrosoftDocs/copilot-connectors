---
title: Set up the Salesforce service for Salesforce CRM connector ingestion
description: Get the steps that the Salesforce CRM admin needs to complete for your organization to configure the Salesforce CRM Microsoft 365 Copilot connector.
author: lauragra
ms.author: lauragra
manager: calvind
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 11/13/2025
---

# Set up the Salesforce service for Salesforce CRM connector ingestion

The Salesforce CRM Microsoft 365 Copilot connector allows your organization to index contacts, opportunities, leads, cases, and accounts objects in your Salesforce instance. After you configure the connector and index content from Salesforce, users can search for those items from any Microsoft Search and Microsoft 365 Copilot client.

This article provides information about the configuration steps that Salesforce admins need to complete in order for your organization to deploy the Salesforce CRM connector.

For information about how to deploy the connector, see [Deploy the Salesforce CRM connector](salesforce-connector.md).

## Prerequisites

Before you configure the service, make sure you have:

- A Salesforce account with **System Administrator** privileges.
- API access enabled for the account.
- Permissions to create and manage connected apps in Salesforce.
- Access to the Microsoft 365 admin center.

## Setup checklist

The following checklist lists the steps involved in configuring the environment and setting up the connector prerequisites.

| Task | Role |
|------|------|
| Identify Salesforce instance URL | Salesforce CRM admin |
| Enable API access | Salesforce CRM admin |
| Create connected app | Salesforce CRM admin |
| Configure refresh token policy | Salesforce CRM admin |
| Define identity mapping | Salesforce CRM admin |
| Determine data ingestion filters | Salesforce CRM admin |
| Verify field-level security (FLS) settings | Salesforce CRM admin |

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

## Create a connected app

Set up a connected app for OAuth 2.0 authentication:

1. Sign in to Salesforce and go to **Setup > Apps > App Manager**.
1. Select **New Connected App**.
1. In the API section:
    - Enable **OAuth settings**.
    - Set the **Callback URL**:
       - For Microsoft 365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`
       - For Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
    - Select required OAuth scopes:
       - Access and manage your data (API)
       - Perform requests on your behalf at any time (refresh_token, offline_access)
    - Uncheck **Require PKCE Extension**.
    - Check **Require secret for web server flow**.
1. Save the app.

### Get client ID and secret

1. Go to **Setup > Apps > App Manager**.
1. Select the connected app and select **Manage Consumer Details**.
1. Copy the **Consumer Key** (client ID) and **Consumer Secret** (client secret).

## Configure refresh token policy

To prevent token expiration:

1. Go to **Apps > App Manager**.
1. Select your app, and select **Manage** > **Edit Policies**.
1. Set **Refresh token policy** to **Refresh token is valid until revoked**.

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

- Confirm the connected app's profile has permission to read FLS metadata. The **System Administrator** profile already includes this access. For custom profiles, ensure **View Setup and Configuration** and **View All Profiles** are enabled (see [Enable API access](#enable-api-access)).
- Verify the FLS settings for the indexed objects and decide which FLS-restricted fields are safe to index in Microsoft 365 and which must stay excluded.

For how to opt in to FLS-restricted fields in the Microsoft 365 admin center, see [Include FLS-restricted fields](salesforce-connector.md#include-fls-restricted-fields).

## Next step

> [!div class="nextstepaction"]
> [Deploy the Salesforce CRM connector](salesforce-connector.md)
