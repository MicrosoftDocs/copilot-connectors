---
ms.date: 02/10/2026
title: "View connection details"
ms.author: danielabo
author: danielabom
manager: calvind
ms.topic: article
ms.service: microsoft-365-copilot-connectors
ms.localizationpriority: medium
description: "Access and manage your Microsoft 365 Copilot connectors as an AI administrator for your tenant."
---
<!-- markdownlint-disable no-inline-html -->

# View connection details

To access and manage your Microsoft 365 Copilot connectors, you must be an AI administrator for your tenant. 

To see your connections in the [Microsoft 365 admin center](https://admin.microsoft.com), go to the [Your Connections tab](https://admin.microsoft.com/#/copilot/connectors).

Select a connection to view the connection details and errors.  

:::image type="content" source="media/view-details/data-sources-tab-1.png" alt-text="Screenshot that shows the connectors list with a connector selected and details pane showing information about this connector." lightbox="media/view-details/data-sources-tab-1.png":::

## View connection statistics 

Connection statistics help you get overall information about what is happening to the data after the first full crawl is completed successfully.

This section includes the data about the total number of items discovered, successfully indexed, or failed across all crawls. The data updates after every crawl and provides a cumulative perspective on the sync between the data source and the Microsoft 365 Copilot connector index. With this information, you can identify discrepancies and ensure that the connection is up to date. 

The sync between the data source and the index is cumulative and not just the last crawl. 

An item is indexed with the following information - content, properties (default + custom), and access.
- An item as fully indexed when all three parts of the item - content, properties (default + custom), and access - are indexed successfully. 
- An item is partially indexed when some of the data is indexed, but a part is missing. The item is still searchable with the remaining properties, but all properties might not be indexed. 

The following table explains the data in the connection statistics.

| Sr. No |Section | Meaning |
|:---|:--- |:---|
|1. |**Total number of discovered items** |Total items discovered in the data source during crawling. This number is the number of items that the admin credentials have access to against the data source.|
|2. |**Items currently in index**|All the items that were indexed, partially or completely.|
|2.a	|**Completely indexed items**|Total items successfully indexed with complete information attached to it, including content, access, and properties.|
|2.b	|**Partially indexed items**|Items that are partially indexed<br> a) Partially indexed with incomplete ACL<br> b) Partially indexed with incomplete data<br> c) Partially indexed with incomplete properties <br>.|
|2.c	|**Items in the index but out of sync**|All items that weren't updated with the latest information from the data source. The update is attempted again in the next crawl.|
|3. |**Items failed to index**|Items that were discovered but weren't processed due to any error. You can find more details for each error on the **Errors** tab.|

## View index status

During the initial setup, the index status displays real-time progress, including the number of items, users, groups, and group memberships at any moment. You can use the **Refresh** action to retrieve the latest counts. After setup, it continues to reflect the current number of searchable items, ensuring visibility into indexing completeness and availability at any time.

The following values are available in the index for each connection.

|Value|Description| 
|:--- |:---|
| Updated at| Date and time when the data was last updated.|
| Items| Number of items that have been successfully ingested.| 
| Users| Number of users successfully mapped.|
| Groups| Number of groups interpreted from the datasource.|  
| Group memberships| Number of users to group mapping instances.|  
| Item Errors| Number of items that produced an error and failed to ingest.| 
| User & group Errors| Number of user and group mapping failures.| 

## Related content

- [Deploy Microsoft 365 Copilot connectors](deployment-overview.md)