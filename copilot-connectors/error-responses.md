---
ms.date: 10/02/2019
title: "Monitor connector errors "
ms.author: danielabo
author: danielabom
manager: SteveWilkins1123
ms.topic: article
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Learn how to identify and handle error responses in Microsoft 365 Copilot connectors."
---
# Monitor connector errors

You can view a limited set of Microsoft 365 Copilot connector errors in the Microsoft 365 admin center UI. To view a comprehensive list of connection errors, use the following steps to run a PowerShell script.

1. Open Windows PowerShell with administrator rights.
2. Install the script from the PowerShell gallery by using the following cmdlet.
    ```powershell
        Install-Script -Name DownloadErrorScript
    ```
    With this script, you can download the item errors from a Microsoft 365 Copilot connector connection. It generates an MSAL token using the tenant credentials associated with the connection. The installation of the script automatically includes the MSAL.PS module. If the module isn't installed, install the module manually by using the following cmdlet.

    ```powershell
        Install-Module -Name MSAL.PS
    ```
    For more information, see [Download error script](https://www.powershellgallery.com/packages/DownloadErrorScript/2.1).

3. Run the script.

    ```powershell
        DownloadErrorScript.ps1
    ```
4. Provide the connection ID of the connection for which you want to download the error report.
5. Specify the name for the output file without extension (the default extension is .csv).
6. Define the batch size for downloading errors. Larger batches are best for thousands of errors to minimize data retrieval time, but might increase the likelihood of failures. The maximum batch size is 5,000 errors. After you sign in with your tenant account, the download process begins.
7. Depending on batch size and error count, the download duration varies. The generated file is saved in the script's path with the specified name.

    :::image type="content" alt-text="Screenshot that shows a PowerShell script run to download the error report." source="media/errors/errorreport.png" lightbox="media/errors/errorreport.png":::

## Monitor errors

To monitor errors, go to **Connectors** > **Your connections** in the Microsoft 365 admin center, select the connection, and choose **Error** in the connection details pane. The **Error** tab displays:

- Error codes - Lists the error codes for errors that occurred.
- Counts -  Displays the number of occurrences for each error code.
- Download log - An option to download a file that lists the errors.

To view detailed information about a specific error, select the error code.

The following table lists the errors that can occur on any connection.

Error code | Error message | Solution
|:--- |:--- |:---|
|1000 | The data source isn't available. Check your internet connection or make sure the data source is still accessible by the connector. | This error occurs when the data source isn't reachable due to a network issue or when the data source itself is deleted, moved, or renamed. Check if the data source details provided are still valid.|
|1001 | Can't update the data because the data source is throttling the connector. | To unthrottle the data source, check if its scale limits can be increased or wait until a less traffic-heavy time of the day.|
|1002 | Can't authenticate with the data source. Verify that the credentials associated with this data source are correct.| Select **Edit** to update the authentication credentials.|
|1003 | The account associated with the connector doesn't have permission to access the item. |Ensure the proper account has access to the item you want indexed.|
|1005 | Credentials associated with this data source expired. Renew the credentials and update the connection.| Select **Edit** to update the authentication credentials.|
|1008 | The total quota utilization of your tenant reached its limit. | Try deleting a connection to free up some of your quota or adjusting your ingestion filters to bring in less data. If these steps don't solve the issue, contact Microsoft support.|
|1009 | The total quota utilization for your connection reached its limit. | Try adjusting your ingestion filters to bring in less data. If this step doesn't solve the issue, contact Microsoft support.|
|1010 | The total quota utilization for indexing non-Microsoft Entra ID groups reached its limit of 100 K. | Try deleting a connection to free up some of your quota or adjusting your ingestion filters to bring in less data. If these steps don't solve the issue, contact Microsoft support.
|1011 | The [Microsoft Graph connector agent](connector-agent.md) isn't reachable or offline. |
|1012 | Authentication to your connection failed due to an unsupported authentication mode. | Edit the connection to update the authentication settings for your connection.|
|1015 | Connections created on this agent will fail due to insufficient permissions. Grant the ExternalItem.ReadWrite.OwnedBy permission to the Microsoft Entra ID app used for registration to allow the app to read and write all external items without a signed-in user and resume the crawl. | Ensure that the Entra ID app used for Agent registration has ExternalItem.ReadWrite.OwnedBy  permission.|
|1016 | Connections created on this agent will fail due to insufficient permissions. Grant the Directory.Read.All  permission to the Microsoft Entra ID app used for registration to read data in your organization's directory and resume the crawl. | Ensure that the Entra ID app used for agent registration has a Directory.Read.All permission.|
|1017 | Item can't be indexed because the network is unavailable. | Restore the network and wait for the next crawl for the item to get indexed.|
|1018 | Ensure that the user account has interactive sign-in rights to the computer where the Microsoft Graph connector agent is installed. | Ensure that the user account has interactive sign-in rights to the computer where the Microsoft 365 Copilot connector agent is installed. For more information, see [Connector agent troubleshooting](connector-agent.md#troubleshooting-the-connector-agent).|
|1019 | Connection failed because the app credentials given to the Microsoft 365 Copilot connector instance are invalid or expired. Please update the credentials. | Check your app credentials for the Microsoft 365 Copilot connector instance associated with the connection.|
|1020 | The Graph Connector Agent associated with the connection isn't able to connect to GRPC connector server. | The Microsoft Graph connector agent instance couldn't crawl the data source because there was an issue connecting to the custom connector over GRPC.|
|1025 | The Graph Connector Agent associated with this connection is deprecated due to critical issues. Upgrade to the latest version. Learn more: https://aka.ms/gca | Upgrade your Microsoft Graph connector agent by [downloading the latest version](https://aka.ms/GCAdownload).|
|1026 | The connection has failed due to a critical issue with the associated Graph Connector Agent. Upgrade to the latest version or contact support to resolve the issue. Learn more: https://aka.ms/gca | Upgrade your Microsoft Graph connector agent version by [downloading the latest version](https://aka.ms/GCAdownload).|
|2001 | Indexing is throttled because of a large number of updates in the queue. Depending on the queue, it can take some time for the updates to complete. | Wait until the queue gets cleared.|
|2002 | Indexing failed due to unsupported item formatting. | For more information, see the connector-specific documentation.|
|2003 | Indexing failed due to unsupported item content. | For more information, see the connector-specific documentation.|
|2004 | Indexing failed due to unsupported item or file size. | For more information, see the connector-specific documentation.|
|2005 | Indexing failed because the URI is too long. | For more information, see the connector-specific documentation.|
|2006 | User mapping failed due to an invalid mapping formula or no Microsoft Entra user with this property. | Try deleting and recreating the connection with a different mapping formula.
|2007 | This item won't be displayed in Microsoft Search because some users or groups without permission to view this item couldn't be indexed.|
|2008 | Connections can't have non-Entra ID groups with more than 50,000 members. | Try removing users from a group or try removing items ACLed with that group from ingestion and recreate the connection.|
|2009 | Non-Entra ID group indexing is temporarily paused due to a large number of requests. Indexing resumes when the system finishes processing these requests. Check back later.|
|2010 | This connection is no longer valid because of an update made by Microsoft. | Delete the connection and create a new one.|
|5000 | Something went wrong. If this issue continues, contact support.|

## Related content

- [Monitor Microsoft 365 Copilot connector connections](manage-connector.md)