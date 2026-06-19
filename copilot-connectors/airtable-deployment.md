---
title: "Deploy the Airtable connector (preview)"
ms.author: kailiang
author: Kai-Cloud
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 05/27/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the Airtable Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Airtable connector (preview)

The Airtable Microsoft 365 Copilot connector integrates Airtable records into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface relevant record information directly within apps like Microsoft Teams, Outlook, and SharePoint. This article describes the steps to deploy and customize the Airtable connector.

For advanced Airtable configuration information, see [Set up the Airtable service for connector ingestion](airtable-admin-setup.md).

> [!NOTE]
> The Airtable connector is currently in preview. Connector functionality and requirements are subject to change.

## Prerequisites

Before you deploy the Airtable connector, make sure that the Airtable environment is configured in your organization. The following table summarizes the steps to configure the Airtable environment and deploy the connector.

| Task | Role |
| ---- | ---- |
| [Configure the Airtable environment](airtable-admin-setup.md#configure-the-airtable-environment) | Airtable admin |
| [Set up connector prerequisites](airtable-admin-setup.md#set-up-connector-prerequisites) | Airtable admin |
| [Deploy the connector](#deploy-the-connector) | Microsoft 365 admin |
| [Customize connector settings](#customize-settings-optional) (optional) | Microsoft 365 admin |

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be a Microsoft 365 admin.
- Your Airtable account must be on an Airtable Enterprise plan.
- An Airtable admin must complete the setup steps in [Set up the Airtable service for connector ingestion](airtable-admin-setup.md).
- You must have the Airtable Enterprise ID, OAuth Client ID, and OAuth Client Secret from the Airtable admin.

## Deploy the connector

To add the Airtable connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, select **Copilot** > **Connectors**.
1. Select the **Gallery** tab.
1. From the list of available connectors, select **Airtable**.

### Set display name

The display name identifies references in Copilot responses, so users can recognize the associated record. The display name also signifies trusted content and acts as a content source filter.

You can accept the default **Airtable** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](/microsoft-365/copilot/connectors/enhance-copilot-discovery).

### Set Airtable URL

In the **Airtable URL** field, enter the base URL for the Airtable API. The typical value is:

`https://api.airtable.com`

### Set Enterprise ID

In the **Enterprise ID** field, enter your Airtable Enterprise ID. The connector uses this ID to scope crawling and identity mapping to your enterprise account.

The Enterprise ID has the format `entXXXXXXXXXXXXXX` (for example, `entABC123def456GH`). For information about how to find your Enterprise ID, see [Identify the Airtable Enterprise ID](airtable-admin-setup.md#identify-the-airtable-enterprise-id).

### Choose authentication type

The Airtable connector supports the following authentication type:

- **OAuth 2.0**: Secure authentication by using Airtable's OAuth flow.

Before you configure authentication, an Airtable admin must register an OAuth integration in the Airtable Builder Hub and add it to the allow list for the enterprise. For detailed steps, see [Register an OAuth integration](airtable-admin-setup.md#register-an-oauth-integration) and [Allowlist the OAuth integration](airtable-admin-setup.md#allowlist-the-oauth-integration).

To configure OAuth authentication:

1. Paste the **Client ID** and **Client Secret** (provided by the Airtable admin) into the corresponding fields on the connector setup page.
1. Choose **Authorize** and complete the OAuth flow with an Airtable account that has access to the bases you want to index.

During the OAuth authorization flow, Airtable prompts you to select which bases and workspaces to grant access to. You can select **Add all resources**, **Add a base**, or **Add the organization** to define the scope of data that the connector can index.

> [!NOTE]
> You authorize access to the Airtable integration in a popup window. Make sure that your browser permits popup windows, or grants access if the popup is blocked.

### Roll out

To roll out to a limited audience, select the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](staged-rollout.md).

Select the **Notice** checkbox to acknowledge the data indexing terms, and then select **Create** to deploy the connection. The Airtable connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Setting | Default value |
|---|---|---|
| Users | Access permissions | Only people with access to the content in the data source. |
| Users | Map identities | Data source identities mapped using Microsoft Entra IDs. |
| Content | Manage properties | For information about the default properties and their schema, see [Customize content settings](#customize-content-settings). |
| Sync | Incremental crawl | Runs every 15 minutes. |
| Sync | Full crawl | Runs every day. |

To customize these values, select **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

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

The connector doesn't crawl records in any excluded workspace, base, or table.

#### Manage properties

You can add or remove available properties from your Airtable records, assign a schema to a property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property.

The following table lists the properties that the connector indexes by default.

| Default property | Label | Description | Searchable | Queryable | Retrievable | Refinable |
|---|---|---|---|---|---|---|
| baseId | `NA` | ID of the base that contains the record. | No | Yes | Yes | Yes |
| baseName | `NA` | Name of the base that contains the record. | Yes | Yes | Yes | Yes |
| content | `Content` | Concatenated content of the record's fields, used for full-text search. | Yes | No | No | No |
| createdDateTime | `createdDateTime` | Date and time that the record was created. | No | Yes | Yes | No |
| iconUrl | `IconUrl` | URL of the icon shown for the record in Copilot and search results. | No | No | Yes | No |
| recordId | `NA` | ID of the record. | Yes | Yes | Yes | No |
| recordUrl | `url` | Deep link to the record in Airtable. | No | No | Yes | No |
| tableId | `NA` | ID of the table that contains the record. | No | Yes | Yes | Yes |
| tableName | `NA` | Name of the table that contains the record. | Yes | Yes | Yes | Yes |
| title | `Title` | Primary field of the record, used as the result title. | Yes | Yes | Yes | No |

### Customize sync intervals

You can configure the frequency of full and incremental crawls:

- **Full crawl**: Schedule every 24 hours to ensure complete data refresh.
- **Incremental crawl**: Schedule every 15 minutes to capture recent changes.

For more information, see [Guidelines for crawl settings](deployment-overview.md#guidelines-for-crawl-settings).

## Related content

- [Airtable connector overview](airtable-overview.md)
- [Set up the Airtable service for connector ingestion](airtable-admin-setup.md)
- [Troubleshoot issues with the Airtable connector](airtable-troubleshooting.md)
