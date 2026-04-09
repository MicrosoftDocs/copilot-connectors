---
title: "Deploy the Credly connector in the Microsoft 365 admin center"
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 04/09/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the Credly Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Credly Copilot connector in the Microsoft 365 admin center

The Credly Microsoft 365 Copilot connector integrates digital credential data from your organization's Credly platform into Microsoft 365, enabling Copilot and profile cards to surface verified badges, awards, and certifications directly within apps like Teams, Outlook, and SharePoint.

This article describes the steps to deploy and customize the Credly Copilot connector. For general information about Copilot connector deployment, see [Set up Copilot connectors in the Microsoft 365 admin center](https://learn.microsoft.com/en-us/microsoft-365/copilot/connectors/deployment-overview).

## Prerequisites

Before you deploy the Credly connector, make sure that the Credly environment is configured for your organization. The following table summarizes the steps to configure the Credly environment and deploy the connector.

| Task | Role |
|:---|:---|
| Configure the Credly environment | Credly admin |
| Set up API credentials | Credly admin |
| Deploy the connector in the Microsoft 365 admin center | Microsoft 365 admin |
| Customize connector settings (optional) | Microsoft 365 admin |

To deploy the connector, you must meet the following prerequisites:

- You must be a Global Administrator or Copilot Administrator for your organization's Microsoft 365 tenant.
- Your organization must have an active Microsoft 365 tenant with [Microsoft 365 Copilot](https://learn.microsoft.com/en-us/microsoft-365/copilot/overview) enabled (for the preview).
- You must have a Credly account with administrative rights for your organization. In the Credly portal, navigate to **Developers** and locate your **Organization ID** (a GUID that uniquely identifies your organization on Credly).
- You must have authentication credentials for the connector. Under **OAuth Applications** in the Credly Developers portal, create a new application (for example, named "Microsoft 365 Copilot Connector") to generate a **Client ID** and **Client Secret**.

> [!IMPORTANT]
> Copy and save the Client Secret when it's shown. Credly doesn't display the secret again after creation.

## Deploy the connector

To add the Credly connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Connectors** tab, and in the left pane, choose **Gallery**.
1. From the list of available connectors, choose **Credly**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated content. The display name also signifies trusted content and is used as a content source filter.

You can accept the default Credly display name, or customize the value to use a display name that users in your organization recognize (for example, "Credly Profiles" or "Credly Badges").

### Set Credly Organization ID

Enter your **Credly Organization ID** (the GUID obtained from the Credly Developers portal). The connector uses this ID to target the correct Credly organization account. The Organization ID must be in the proper GUID format.

### Choose authentication type

To authenticate and synchronize data from Credly, choose **OAuth 2.0 Client Credentials** as the authentication method. No interactive user sign-in is required; the connector uses the client credentials to access Credly programmatically.

1. Provide the base URL for the Credly OAuth 2.0 token service. For a production Credly account, use `https://www.credly.com` as the authorization endpoint (the default value).
1. Enter the **Client ID** and **Client Secret** that you obtained from the Credly Developers portal.

### Roll out

To deploy the connector, choose **Create** in the Microsoft 365 admin center. The Credly Copilot connector starts indexing badges from your Credly account right away.

The following table lists the default values that are set. These values work best with Credly data.

| Category | Setting | Default value |
|:---|:---|:---|
| Users | Access permissions | Everyone in the organization. |
| Users | Map identities | Data source identities mapped using Microsoft Entra IDs. |
| Content | Manage properties | All Credly badge fields mapped to Awards and Certifications profile properties (fixed). |
| Sync | Incremental crawl | Frequency: Every day |
| Sync | Full crawl | Frequency: Every week |

To customize these values, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Credly connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

The Credly connector sets access permissions to **Everyone** by default, which means all indexed badge data is visible to all users in your organization. Granular per-user or group filtering isn't available in this preview release.

Identity mapping is based on user email addresses mapped to Microsoft Entra ID. The connector matches the badge owner's email address in Credly with their UPN or primary SMTP address in Microsoft Entra ID.

> [!NOTE]
> If a Credly user's email doesn't match their Microsoft Entra ID UPN or primary SMTP address, those badges can't be mapped to a Microsoft 365 user profile and are skipped during indexing.

### Customize content settings

The Credly connector uses a fixed schema in this release. It automatically selects a set of badge fields to ingest and maps them to the corresponding **Awards** and **Certifications** profile properties in Microsoft Graph. You can't add or remove properties from the schema.

### Customize sync intervals

The refresh interval determines how often your data is synchronized between the data source and the Credly connector index. Copilot connectors use two types of refresh intervals:

- **Full crawl** - Performs a complete synchronization of all content. By default, full crawls run every week.
- **Incremental crawl** - Syncs new and modified content. By default, incremental crawls run every day.

You can change the default values of the refresh intervals. For more information, see [Guidelines for sync settings](https://learn.microsoft.com/en-us/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [Credly connector overview](credly-connector-overview.md)
- [Troubleshoot the Credly connector](credly-connector-troubleshoot.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](https://learn.microsoft.com/en-us/microsoft-365/copilot/connectors/deployment-overview)
- [Monitor Microsoft 365 Copilot connectors](https://learn.microsoft.com/en-us/microsoftsearch/manage-connector)
