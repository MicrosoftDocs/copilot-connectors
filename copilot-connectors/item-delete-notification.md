---
title: "Connectors item delete notifications"
ms.author: rmalhotra
author: rmalhotra
ms.date: 02/24/2025
manager: james.lau
audience: Admin
ms.audience: Admin
ms.topic: article
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Find information about item delete notifications for Microsoft 365 Copilot connectors."
---

# Item delete notifications

The following information pertains to customers who are part of a preview offering wherein their ingested data from Microsoft 365 Copilot connectors appears in the Topics card. This information applies when an item (for example, a file or other content) is deleted from the source system and should be processed and deleted from the Microsoft system within 30 days.

## Connector types

For partner-built Microsoft 365 Copilot connectors, we don't have any direct visibility into when an item is created, updated, or deleted in the data source. The first point of visibility is when the connector invokes public Microsoft Graph APIs via a create, read, update, or delete operation.

For Microsoft 365 Copilot connectors built by Microsoft, the crawl setting that is set by the AI administrator determines when an item deletion is detected. The reliability of the data depends on the availability and reliability of the data source to process the request.  

## Ensure timely item deletion

Given that there can be delays between when an item is deleted or changed in the data source and when Microsoft first detects this operation, we recommend that you schedule an incremental crawl or full crawl in less than 14 days to improve detection.

For more information, see [Crawl scheduling](/microsoft-365/copilot/connectors/deployment-overview?branch=pr-en-us-11#crawl-scheduling).
