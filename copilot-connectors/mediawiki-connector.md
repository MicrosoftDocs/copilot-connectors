---
ms.date: 10/08/2019
title: "MediaWiki Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: install-set-up-deploy
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Set up the MediaWiki Copilot connector for Microsoft Search and Microsoft 365 Copilot"
---
<!---Previous ms.author: monaray --->

# MediaWiki Copilot connector

The MediaWiki Copilot connector allows your organization to discover and index data from a wiki created by using MediaWiki software. This connector indexes specified content into Microsoft Search and Microsoft 365 Copilot and supports periodic crawls to keep the index up to date.

This article is for anyone who configures, runs, and monitors a MediaWiki Copilot connector. It supplements the general setup process and shows instructions that apply only to the MediaWiki Copilot connector. This article also includes information about [Limitations](#limitations).

<!---## Before you get started-->

<!---Insert "Before you get started" recommendations for this data source-->

> [!NOTE]
> The wiki should be hosted under subdirectory/wiki.

## Step 1: Add a connector in the Microsoft 365 admin center

[Add the MediaWiki Copilot connector](https://admin.microsoft.com/adminportal/home#/microsoft-365/copilot/connectors/Connectors/add?ms_search_referrer=microsoft-365/copilot/connectorsDocs_MediaWiki&type=MediaWiki)

Follow the general [setup instructions](./deployment-overview.md).
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## Step 2: Name the connection

Follow the general [setup instructions](./deployment-overview.md).
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## Step 3: Configure the connection settings

Enter your **Wiki URL** and choose the **Authentication type** from the drop-down menu of options. The options are **None**, **Basic**, and **OAuth
2.0 Microsoft Entra ID**.

If you choose **Basic** as the Authentication type, you need to provide the **Username** and **Password** for the wiki.

If you choose **OAuth 2.0 Microsoft Entra ID** as the authentication type, you need to provide the **Resource ID** of the wiki installation. You also need to provide the **client ID** and **client secret** generated on the Microsoft Entra Application registration page.

## Step 4: Manage search permissions

The MediaWiki Copilot connector only supports search permissions visible to **Everyone**. Indexed data appears in the search results and is visible to all users in the organization.

## Step 5: Assign property labels

Follow the general [setup instructions](./deployment-overview.md).
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## Step 6: Manage schema

Follow the general [setup instructions](./deployment-overview.md).
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## Step 7: Choose refresh settings

Follow the general [setup instructions](./deployment-overview.md).
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## Step 8: Review connection

Follow the general [setup instructions](./deployment-overview.md).
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

<!---## Troubleshooting-->
<!---To be added-->

## Limitations

The MediaWiki Copilot connector has these limitations in the preview release:

* Supports only cloud-based wikis.
* Supports only Basic or OAuth 2.0 with Microsoft Entra ID or Azure authentication.
* Doesn't support namespace selection for indexing. Indexes only main, category, and file namespaces.
* Doesn't support Access Control Lists (ACLs). Thus, indexed pages are visible to all users in the organization.

## Troubleshooting
After publishing your connection, you can review the status in the **Connectors** section of the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

You can find troubleshooting steps for commonly seen issues [here](troubleshoot-media-wiki-connector.md).

If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).
