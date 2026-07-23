---
title: "Deploy the Azure Data Lake Storage Gen2 connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: microsoft-365-copilot-connectors
ms.date: 07/22/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the Azure Data Lake Storage Gen2 Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Azure Data Lake Storage Gen2 connector

The Azure Data Lake Storage Gen2 Microsoft 365 Copilot connector indexes files stored in [Azure Blob Storage](/azure/storage/blobs/storage-blobs-introduction) and [Azure Data Lake Gen 2 Storage](/azure/storage/blobs/data-lake-storage-introduction) accounts. This article describes the steps to deploy and customize the Azure Data Lake Storage Gen2 connector in the Microsoft 365 admin center.

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be a Microsoft 365 AI administrator.
- An Azure Storage account (Azure Blob Storage or Azure Data Lake Gen 2 Storage) with at least one container and one file.
- Access to the primary storage connection string, OR the ability to assign roles (Storage Blob Data Reader, Storage Queue Data Contributor, Storage Blob Delegator) to the Copilot connector service app in the Azure portal.
- If using queue notifications: a queue created in the same storage account.

## Deploy the connector

To add the Azure Data Lake Storage Gen2 connector for your organization:

1. In the Microsoft 365 admin center, go to **Copilot** > **Connectors**.
1. Select the **Gallery** tab.
1. From the list of available connectors, select **Azure Data Lake Storage Gen2**.

[Add Azure Data Lake Storage Gen2 Copilot connector](https://admin.microsoft.com/adminportal/home#/microsoft-365/copilot/connectors/Connectors/add?ms_search_referrer=microsoft-365/copilot/connectorsDocs_ADLSGen2&type=ADLSGen2)

### Set display name

The display name identifies references in Copilot responses so users can recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **Azure Data Lake Storage Gen2** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

### Set connection settings

Enter the primary storage connection string for your Azure Storage account. This string is required to allow access to your storage account. To find your connection string, go to the [Azure portal](https://ms.portal.azure.com/#home) and navigate to the **Access keys** section (under **Security + networking**) of your relevant Azure Storage account.

### Choose authentication type

The Azure Data Lake Storage Gen2 connector supports the following authentication methods:

#### Connection string with AccountKey (recommended)

Provide the full primary storage connection string, which includes the **AccountKey** parameter. This method is the simplest authentication method.

#### Service principal (role-based)

If you prefer not to provide the AccountKey in the connection string, grant access to the Copilot connector service for the following roles on your Azure Storage account:

1. Go to the **Access control (IAM)** tab of your Azure Storage account.
1. Select **Add role assignment** and assign the following roles to the Copilot connector service:
   - **Storage Blob Data Reader**
   - **Storage Queue Data Contributor**
   - **Storage Blob Delegator**
1. Use the following app identity:
   - **App ID:** `56c1da01-2129-48f7-9355-af6d59d42766`
   - **App Name:** Copilot connector service

### Configure queue notifications (optional)

Support for processing changes in real-time in the Copilot connectors service might be added in the future. In that case, the service monitors Azure Storage change notifications stored in a queue. To configure queue notifications:

1. Create a queue in the same account as your Azure Storage account.
1. On the queue page, go to **Events** and configure an **Event Subscription**.
1. Choose all the blob events that the queue receives and connect the queue to the Azure Storage account.

### Test the connection

Select **Test Connection** to validate your configuration.

> [!NOTE]
> The **Test Connection** must succeed before you can move to the next configuration section. The ADLS Gen2–enabled storage account must have at least one container with at least one file for the test to succeed. If no content exists, the test fails and raises a connection error.

### Rollout

To roll out to a limited audience, select the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](staged-rollout.md).

Select **Create** to deploy the connection. The Azure Data Lake Storage Gen2 connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|---------------|
| **Users** | Everyone (Azure Blob Storage) or ACL-trimmed (Azure Data Lake Gen 2) |
| **Content** | All supported file types in all containers |
| **Sync** | Incremental crawl every 15 minutes; full crawl every week |

To customize these values, select **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Azure Data Lake Storage Gen2 connector settings. To customize settings, on the connector page in the admin center, select **Custom setup**.

### Customize user settings

#### Access permissions

The Azure Data Lake Storage Gen2 connector supports the following access permission options:

- **Everyone** — All indexed content is visible to all users in the organization.
- **Only people with access to this data source** — The connector ingests and enforces access control lists (ACLs) from Azure Data Lake Gen 2 Storage. Search content is trimmed based on the permissions of the signed-in user's Microsoft Entra ID. This option isn't available for Azure Blob Storage connections.

#### Map identities

For Azure Data Lake Gen 2 Storage connections, the connector maps user identities from ACLs to Microsoft Entra ID so that search results are properly trimmed based on user permissions. The connector automatically resolves Azure Data Lake Storage ACL entries to their corresponding Microsoft Entra ID accounts by using user principal names (UPNs).

### Customize content settings

#### Assign property labels

Assign a source property to each label by choosing from a menu of options. While this step isn't mandatory, having some property labels improves the search relevance and ensures better search results for end users.

#### Manage properties

On **Manage Schema**, you can add or remove properties, assign schema attributes to each property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias. The following properties are available for customization:

- **Content** — The full text content of the indexed file.
- **Title** — The file name.
- **LastModifiedDateTime** — The date and time the file was last modified.
- **CreatedBy** — The identity that created the file.
- **LastModifiedBy** — The identity that last modified the file.

Assign source properties to semantic labels to improve search relevance for end users.

### Customize sync intervals

Customize the following sync intervals for the Azure Data Lake Storage Gen2 connector:

- **Incremental crawl:** Default every 15 minutes.
- **Full crawl:** Default every week.

For more information, see [Guidelines for crawl settings](deployment-overview.md#guidelines-for-crawl-settings).

## Related content

- [Azure Data Lake Storage Gen2 connector overview](azure-data-lake-storage-gen2-overview.md)
- [Troubleshoot issues with the Azure Data Lake Storage Gen2 connector](azure-data-lake-storage-gen2-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](deployment-overview.md)
