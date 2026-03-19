---
title: "Deploy the Azure File Share Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 12/15/2025
ms.localizationpriority: Medium
description: "Find information about how to deploy the Azure File Share Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Azure File Share Microsoft 365 Copilot connector

The Azure File Share Microsoft 365 Copilot connector enables organizations to integrate Azure File Share content into Microsoft 365. This article describes the steps to deploy and customize the Azure File Share connector in the Microsoft 365 admin center.

## Prerequisites

Before you deploy the Azure File Share connector, make sure that your environment meets the following requirements:

- You must be a Microsoft 365 AI administrator.
- Your Azure File Share must be mounted on a device.
- The Microsoft Graph connector agent must be installed and registered on the same device. Use version 3.1.8.0 or later.
- Use the same credentials to:
  - Mount the Azure File Share.
  - Run the Microsoft Graph Connector Agent.
  - Configure the connector in the Microsoft 365 admin center.
- The user running the agent must have read access to all files and directories under the source folder paths.

## Deploy the connector

To add the Azure File Share connector for your organization:

1. In the Microsoft 365 admin center, go to **Copilot** > **Connectors**.
2. Select the **Gallery** tab.
3. From the list of available connectors, choose **Azure File Share**.

### Set display name

The display name identifies the connector in Copilot responses and helps users recognize trusted content sources. You can accept the default **Azure File Share** display name or customize it to match departmental or organizational naming conventions.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

### Set instance URL

Specify the Universal Naming Convention (UNC) path for the Azure File Share. For example: `\\testpath.file.core.windows.net\projectshare\team1`.

Make sure that the path matches the location you mounted locally for the Microsoft Graph Connector Agent.

### Choose authentication type

Use **Windows authentication** with valid admin credentials. Select the registered Microsoft Graph Connector Agent that has access to your Azure File Share. This authentication ensures that New Technology File System (NTFS) permissions are mapped and enforced.

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The Azure File Share connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|----------------|
| **Users** | Respects NTFS permissions; only authorized files are accessible. |
| **Content** | Indexes metadata such as file name, owner, last modified date, and file path. |
| **Sync** | Full crawl occurs once daily. |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Azure File Share connector settings. To customize settings, choose **Custom setup** on the connector page in the admin center.

### Customize user settings

#### Access permissions

The connector adheres to New Technology File System (NTFS) access control lists (ACLs) to control file access. You can set the access permissions to **Visible to everyone**; however, we recommend that you retain NTFS-trimmed access.

#### Mapping identities

Identity mapping uses Windows authentication and the Microsoft Graph Connector Agent’s credentials. Make sure that your Microsoft Entra ID and NTFS access models align.

### Customize content settings

#### Query string

Specify a query string to filter indexed content. Use filters to include or exclude certain file types or folder paths.

#### Manage properties

You can create custom properties that enhance metadata available for search. Use static values or regex-based mappings to extract structured information. For example:

1. Name the property as it appears in search results.
2. Choose a mapping type:
   - **Static value**
   - **String/regex mapping**
3. Configure extraction expressions and preview sample values.

### Customize sync intervals

You can adjust the frequency of full or incremental crawls. The default full crawl runs daily. Customize these intervals based on content update patterns and performance expectations.

For more information, see [Guidelines for sync settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [Azure File Share connector overview](azure-file-share-overview.md)
- [Troubleshoot issues with the Azure File Share connector](azure-file-share-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)
