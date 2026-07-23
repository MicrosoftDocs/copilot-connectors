---
title: "Troubleshoot issues with the Azure Data Lake Storage Gen2 connector"
ms.author: gladysa
author: gladysa
manager: brian.jackett
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: microsoft-365-copilot-connectors
ms.date: 07/22/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Azure Data Lake Storage Gen2 Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Azure Data Lake Storage Gen2 connector

The Azure Data Lake Storage Gen2 Microsoft 365 Copilot connector indexes files stored in [Azure Blob Storage](/azure/storage/blobs/storage-blobs-introduction) and [Azure Data Lake Gen 2 Storage](/azure/storage/blobs/data-lake-storage-introduction) accounts. This article provides troubleshooting information for common errors that you might encounter when you deploy the Azure Data Lake Storage Gen2 connector.

## Azure Data Lake Storage Gen2 connector troubleshooting

The following table lists common errors and possible resolution steps.

| Configuration step | Error message | Possible resolution |
|:----|:----|:----|
| Connection settings | The connection fails even after allowing the public IP address in the ADLS firewall settings. | Allow access to both the virtual network and the IP address (for disaster recovery purposes) by using the Azure PowerShell `Add-AzStorageAccountNetworkRule` cmdlet. The Azure portal doesn't provide an option to do that. For syntax and examples, see [Add-AzStorageAccountNetworkRule](/powershell/module/az.storage/add-azstorageaccountnetworkrule). |
| Connection settings | InvalidConfigurationException | Check whether you set up a valid storage for crawls, but later deleted the storage account. |
| Connection settings/crawl | EndpointUnsupportedAccountFeatures (Error code 7010) | Your Azure Data Lake Storage Gen2 account has **BlobStorageEvents** or **SoftDelete** enabled. This endpoint doesn't support these features. Disable **BlobStorageEvents** and **SoftDelete** on your storage account, and then retry the connection. Disabling **SoftDelete** can affect data retention and recovery, so only do this action if it's appropriate for your organization's protection requirements. Re-enable **SoftDelete** after troubleshooting if possible. For details, see [How to fix EndpointUnsupportedAccountFeatures](/answers/questions/1853681/how-to-fix-the-problem-endpointunsupportedaccount). |
| Test Connection | Test Connection fails | Ensure the ADLS Gen2–enabled storage account has at least one container with at least one file. A connection error is raised if the content doesn't exist. |

To view more error types, in the Microsoft 365 admin center, select **Connectors**. On the **Your Connections** tab, select the connector and then select the **Error** tab. For more information, see [Monitor errors](/microsoft-365/copilot/connectors/error-responses#monitor-errors).

## Related content

- [Azure Data Lake Storage Gen2 connector overview](azure-data-lake-storage-gen2-overview.md)
- [Deploy the Azure Data Lake Storage Gen2 connector](azure-data-lake-storage-gen2-deployment.md)
