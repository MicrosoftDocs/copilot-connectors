--- 
ms.date: 09/11/2024 
title: "Troubleshooting the Azure Data Lake Storage Gen2 Microsoft 365 Copilot connector" 
ms.author: gladysa
author: gladysa
manager: brian.jackett
audience: Admin 
ms.audience: Admin 
ms.topic: troubleshooting-general
ms.service: mssearch 
ms.localizationpriority: medium 
description: "Troubleshooting the Azure Data Lake Storage Gen2 Microsoft 365 Copilot connector"
--- 

# Troubleshooting the Azure Data Lake Storage Gen2 Microsoft 365 Copilot connector 

### Common errors observed while configuring the connector.

| Configuration step | Error message | Possible reason(s) |
|:----|:----|:----|
| Connection settings | The connection fails even after allowing the public IP address in the ADLS firewall settings. |  Allow access to the VNet and the IP (for disaster recovery purposes) using a PowerShell command, as there is no option to do that in the Azure portal. |
| Connection settings | InvalidConfigurationException |  Check if you have set up a valid storage for crawls, but have later deleted the storage account, which could result this situation. |

To view more error types, select the connection and click **error details** > **error code**. For more information, see [Monitor your connections](./manage-connector.md). 
