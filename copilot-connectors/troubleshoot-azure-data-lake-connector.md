--- 
ms.date: 09/11/2024 
title: "Troubleshooting the Azure Data Lake Storage Gen2 connector" 
ms.author: gladysa
author: gladysa
manager: brian.jackett
audience: Admin 
ms.audience: Admin 
ms.topic: troubleshooting-general
ms.service: copilot-connectors 
ms.localizationpriority: medium 
description: "Troubleshooting the Azure Data Lake Storage Gen2 Microsoft 365 Copilot connector"
--- 

# Troubleshooting the Azure Data Lake Storage Gen2 connector 

### Common errors observed while configuring the connector.

| Configuration step | Error message | Possible reason(s) |
|:----|:----|:----|
| Connection settings | The connection fails even after allowing the public IP address in the ADLS firewall settings. |  Allow access to the VNet and the IP (for disaster recovery purposes) using a PowerShell command, as there is no option to do that in the Azure portal. |
| Connection settings | InvalidConfigurationException |  Check if you have set up a valid storage for crawls, but have later deleted the storage account, which could result this situation. |
| Connection settings / Crawl | EndpointUnsupportedAccountFeatures (Error code 7010) | Your Azure Data Lake Storage Gen2 account has **BlobStorageEvents** or **SoftDelete** enabled. This endpoint does not support these features. Disable BlobStorageEvents and SoftDelete on your storage account, then retry the connection. For steps, see [How to fix EndpointUnsupportedAccountFeatures](https://learn.microsoft.com/en-us/answers/questions/1853681/how-to-fix-the-problem-endpointunsupportedaccount). |


To view more error types, select the connection and click **error details** > **error code**. For more information, see [Monitor your connections](./manage-connector.md). 
