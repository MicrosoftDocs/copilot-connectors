---
title: "Deploy the Airtable connector (preview)"
ms.author: kailiang
author: Kai-Cloud
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 05/21/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the Airtable Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Airtable connector (preview)

The Airtable Microsoft 365 Copilot connector integrates Airtable records into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface relevant record information directly within apps like Microsoft Teams, Outlook, and SharePoint. This article describes the steps to deploy and customize the Airtable connector.

> [!NOTE]
> The Airtable connector is currently in preview. Connector functionality and requirements are subject to change.

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be a Microsoft 365 admin.
- Your Airtable account must be on an [Airtable Enterprise](https://airtable.com/pricing) plan. The Enterprise plan is required to register and allowlist OAuth integrations.
- You must have your Airtable Enterprise ID. The Enterprise ID has the format `entXXXXXXXXXXXXXX` and is visible in the URL of the Airtable Admin Hub (`https://airtable.com/admin/{enterpriseId}/...`).
- An Airtable admin must register an OAuth integration for the connector and allowlist it for the enterprise (see [Choose authentication type](#choose-authentication-type)).
- Identity mapping must be configured if Airtable user emails differ from Microsoft Entra ID user principal names (UPNs).

## Deploy the connector

To add the Airtable connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
2. Choose the **Gallery** tab.
3. From the list of available connectors, choose **Airtable**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated record. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **Airtable** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Set Airtable URL

In **Airtable URL**, enter the base URL for the Airtable API. The typical value is:

`https://api.airtable.com`

### Set Enterprise ID

In **Enterprise ID**, enter your Airtable Enterprise ID. The connector uses this ID to scope crawling and identity mapping to your enterprise account.

### Choose authentication type

The Airtable connector supports the following authentication type:

- **OAuth 2.0** (default): Secure authentication using Airtable's OAuth flow.

To use **Airtable OAuth** for authentication, an Airtable admin must register an OAuth integration in the [Airtable Builder Hub](https://airtable.com/create/oauth). We recommend that the admin creates a dedicated service account in Airtable to register and authorize the integration, so that the connection isn't tied to an individual user. You can also use a regular Airtable admin account.

Use the information in the following table to complete the OAuth integration registration form.

| Field | Description | Recommended value |
|---|---|---|
| Name | Display name for the OAuth integration. | `Microsoft 365 Copilot Connector` |
| OAuth redirect URLs | Required callback URLs that the authorization server redirects to. | For **Microsoft 365 Enterprise**: `https://gcs.office.com/v1.0/admin/oauth/callback`</br></br>For **Microsoft 365 Government**: `https://gcsgcc.office.com/v1.0/admin/oauth/callback` |
| Scopes | Read scopes that define what the connector can access. | Enable the following scopes: `data.records:read`, `data.recordComments:read`, `schema.bases:read`, `user.email:read`, `workspacesAndBases:read`, `enterprise.groups:read`, `enterprise.user:read`, `enterprise.account:read`, `enterprise.auditLogs:read`, `enterprise.changeEvents:read`. |

After you save the integration, generate a client secret and copy both the **Client ID** and **Client Secret**. Store them securely; Airtable doesn't display the secret again.

> [!IMPORTANT]
> Airtable Enterprise accounts block third-party OAuth integrations by default. In the Airtable Admin Hub, under **Settings** > **Integrations & development** > **Third party integration allowlist**, choose **Allow integration** and enter the **Client ID** of the integration you registered. Without allowlisting, users can't authorize the connector during the OAuth flow.

Paste the **Client ID** and **Client Secret** into the corresponding fields on the connector setup page. Choose **Authorize** and complete the OAuth flow with an Airtable account that has access to the bases you want to index.

> [!NOTE]
> You authorize access to the Airtable integration in a popup window. Make sure that your browser permits popup windows, or grants access if the popup is blocked.

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to.

Select the **Notice** checkbox to acknowledge the data indexing terms, then choose **Create** to deploy the connection. The Airtable Copilot connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Setting | Default value |
|---|---|---|
| Users | Access permissions | Only people with access to the content in the data source. |
| Users | Map identities | Data source identities mapped using Microsoft Entra IDs. |
| Content | Manage properties | For information about the default properties and their schema, see [Customize content settings](#customize-content-settings). |
| Sync | Incremental crawl | Runs every 15 minutes. |
| Sync | Full crawl | Runs every day. |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Airtable connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

The Airtable connector supports the following user access permissions:

- Everyone
- Only people with access to this data source (default)

If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results only for users who have access to the corresponding record in Airtable.

In Airtable, access is defined by workspace, base, and table permissions assigned to users and groups in your enterprise account.

#### Map identities

The default method to map your data source identities with Microsoft Entra ID is to verify that the email ID of Airtable users is the same as the user principal name (UPN) of the users in Microsoft Entra ID. If the default mapping doesn't work for your organization, you can provide a custom mapping formula. For more information, see [Map your non-Azure AD identities](map-non-entra-id.md).

To identify which option is best for your organization:

- Choose the **Microsoft Entra ID** option if the email ID of Airtable users is the *same* as the UPN in Microsoft Entra ID.
- Choose the **Non-Microsoft Entra ID** option if the email ID of Airtable users is *different* than the users' UPN and email in Microsoft Entra ID.

### Customize content settings

#### Content filter

By default, the connector indexes records from all bases that the authorizing Airtable account can access. To exclude specific content from indexing, use the **Content filter** section to enter:

- Workspace IDs to exclude (prefix `wsp`).
- Base IDs to exclude (prefix `app`).
- Table IDs to exclude (prefix `tbl`).

Records in any excluded workspace, base, or table aren't crawled.

#### Manage properties

You can add or remove available properties from your Airtable records, assign a schema to a property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property.

The following table lists the properties that are indexed by default.

| Default property | Label | Description |
|---|---|---|
| BaseId | `NA` | ID of the base that contains the record. |
| BaseName | `NA` | Name of the base that contains the record. |
| Content | `Content` | Concatenated content of the record's fields, used for full-text search. |
| CreatedDateTime | `createdDateTime` | Date and time that the record was created. |
| IconUrl | `IconUrl` | URL of the icon shown for the record in Copilot and search results. |
| RecordId | `NA` | ID of the record. |
| RecordUrl | `url` | Deep link to the record in Airtable. |
| TableId | `NA` | ID of the table that contains the record. |
| TableName | `NA` | Name of the table that contains the record. |
| Title | `Title` | Primary field of the record, used as the result title. |

### Customize sync intervals

You can configure the frequency of full and incremental crawls:

- **Full crawl**: Schedule every 24 hours to ensure complete data refresh.
- **Incremental crawl**: Schedule every 15 minutes to capture recent changes.

For more information, see [Guidelines for crawl settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [Airtable connector overview](airtable-overview.md)
- [Troubleshoot issues with the Airtable connector](airtable-troubleshooting.md)
- [Set up Copilot connectors in the admin center](/microsoft-365/copilot/connectors/deployment-overview)
