---
ms.date: 10/08/2019
title: "Azure Data Lake Storage Gen2 connector"
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Set up the Azure Data Lake Storage Gen2 Microsoft 365 Copilot connector"
---
# Azure Data Lake Storage Gen2 connector

The Azure Data Lake Storage Gen2 Microsoft 365 Copilot connector indexes and enables users in your organization to search for files stored in [Azure Blob Storage](/azure/storage/blobs/storage-blobs-introduction) and [Azure Data Lake Gen 2 Storage](/azure/storage/blobs/data-lake-storage-introduction) accounts.

This article is for anyone who configures, runs, and monitors an Azure Data Lake Storage Gen2 Copilot connector. It supplements the general setup process and shows instructions that apply only to the Azure Data Lake Storage Gen2 Copilot connector. It  also includes information about [Limitations](#limitations).

In the article, we use *Azure Storage* as a generic term for [Azure Blob Storage](/azure/storage/blobs/storage-blobs-introduction) and [Azure Data Lake Gen 2 Storage](/azure/storage/blobs/data-lake-storage-introduction).

## Limitations
A published connection for Azure Blob Storage can't be reconfigured for Azure Data Lake Storage Gen2 source, and the other way around. In such scenarios, it's recommended to configure a new connection.

Also, the size of the files needs to be 4 MB or less for it to be crawled. File types currently supported are:

* Word (docx, .docm, .dotx, .dotm)
* PowerPoint (.pptm, .pptx, .potm, .potx, .ppam, .ppsm, .ppsx)
* Excel (.xlsx, .xlsm)
* Legacy Office formats (.doc, .dot, etc.)
* Text (.txt)
* HTML
* PDF

Binary files like images (.jpg, .bmp, etc.) aren't supported. For example, if a .docx file contains only images, it might be skipped because it doesn't return any content.

## Get started
### Add a connector in the Microsoft 365 admin center

[Add Azure Data Lake Storage Gen2 Copilot connector](https://admin.microsoft.com/adminportal/home#/microsoft-365/copilot/connectors/Connectors/add?ms_search_referrer=microsoft-365/copilot/connectorsDocs_ADLSGen2&type=ADLSGen2)

(See general [setup instructions](./deployment-overview.md) for more details)

### Name the connection

Follow the general [setup instructions](./deployment-overview.md).

### Configure the connection settings

Enter your primary storage connection string. This string is required to allow access to your storage account. To find your connection string, go to the [Azure portal](https://ms.portal.azure.com/#home) and navigate to the **Keys** section of your relevant Azure Storage account.

If you prefer not to provide the **Accountkey** (a parameter in the primary storage connection string), grant access to the Copilot connectors service for the following roles:

* Storage Blob Data Reader
* Storage queue data contributor
* Storage blob delegator

Navigate to the **Access control** tab of your Azure Storage account, and follow the instructions there to grant access to the following app:

* **First Party App ID:** 56c1da01-2129-48f7-9355-af6d59d42766
* **First Party App Name:** Copilot connector service

#### Storage account and queue notifications (optional)

Support for processing changes in real-time in the Copilot connectors service might be added in the future. In that case, we'll monitor Azure Storage change notifications stored in a queue. You'll need to create a queue in the same account as your Azure Storage account.

After you create a queue, go to the **Events** tab on the queue page to configure **Event Subscription**. Choose all the blob events that the queue receives, and connect the queue to the Azure Storage account.

#### Test the connection

Test the connection by clicking the **Test Connection** button.

> [!NOTE]
> The **Test Connection** must succeed before you can move to the next configuration section. The ADLS gen 2 enabled storage account **MUST** have a container **AND** at least one file within it as a minimum for the **Test Connection** to succeed. A connection error is raised if the content does not exist.

### Assign property labels

You can assign a source property to each label by choosing from a menu of options. While this step isn't mandatory, having some property labels improves the search relevance and ensures better search results for end users.

### Manage schema

On the **Manage Schema** screen, you can change the schema attributes associated with the properties, the options are **Query**, **Search**, **Retrieve**, and **Refine**. You also can add optional aliases, and choose the **Content** property.

#### Manage search permissions

#### Azure Data Lake Gen 2

You can choose to ingest the Access Control Lists (ACLs) from your [Azure Data Lake Gen 2 Storage](/azure/storage/blobs/data-lake-storage-introduction) account. When these search permissions are set, search content is trimmed based on the permissions of the user signed in [Microsoft Entra ID](/azure/active-directory/). Alternatively, you can choose to make all the content indexed from your storage account visible to everyone in your organization. In this case, everyone in your organization has access to all the data in your storage account.

The Azure Data Lake Storage Gen2 Copilot connector supports search permissions visible to **Everyone**, or **Only people with access to this data source**. Indexed data that appears in the search results could be visible to users in the organization who have access to each item.

#### Azure Blob Storage

For a connection to [Azure Blob Storage](/azure/storage/blobs/storage-blobs-introduction), all the content indexed from the configured source is visible to everyone in your organization. Access control lists aren't supported at the blob level in Azure Blob Storage.

#### Set the refresh schedule

On the **Refresh settings** screen, you can set the incremental crawl interval and the full crawl interval. The default intervals for the Azure Data Lake Storage Gen2 Copilot connector are 15 minutes for an incremental crawl and one week for a full crawl.

#### Review connection

Follow the general [setup instructions](./deployment-overview.md).

## Troubleshooting
After publishing your connection, you can review the status in the **Connectors** section of the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).
