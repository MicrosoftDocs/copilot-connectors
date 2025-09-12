---
title: "Licensing requirements for Microsoft 365 Copilot connectors"
ms.author: lauragra
author: lauragra
manager: calvind
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Learn about the licensing requirements for deploying Copilot connectors in your organization."
ms.date: 09/09/2025
---

# Licensing requirements for Microsoft 365 Copilot connectors

Microsoft 365 Copilot connectors enable your organization to bring external data into the intelligent experiences within Microsoft 365. Before you deploy Copilot connectors, it's important to understand the licensing requirements and other prerequisites.

## Licenses and quotas

All eligible Microsoft 365 and Office 365 enterprise customers receive a default index quota of 50 million items at no additional cost. This applies to the following license tiers:

- Microsoft 365: E3, E5, F1, F3, Business Basic, Standard, Premium
- Office 365: E1, E3, E5, F3
- Education: A3, A5
- Government: G1, G3, G5

> [!NOTE]
> Connectors in preview status don't count against the quota until they reach general availability.

Organizations that require additional quota beyond the standard 50 million items can purchase it through the Microsoft 365 admin center. Admins can monitor and adjust quota allocations as needed.

Pricing for additional quota is $1,000 USD per 1 million items per month.

### What represents items in an index quota?

An item represents one unit of index quota. Each entity (or record) from the source system that is added to Microsoft Graph is considered an item. In Microsoft Graph, each item appears as a unique citation in Microsoft 365 Copilot responses and as a distinct search result in Microsoft Search.

Depending on the type of data source, an item is defined as:

- One document (Word, Excel, PPT, PDF) in a file share
- One wiki page in Confluence
- One webpage on a website
- One ticket or issue in Jira

The total quota utilized is based on the number of items stored in the index. The frequency of updates or changes to an item doesn't affect the quota calculation.

## Copilot Studio and agent licensing

If you're using Copilot Studio to build agents that use connectors, you need either:

- A Copilot Studio license
- Usage billing (pay-as-you-go) set up in the tenant

Advanced features like semantic search require the maker to have a Microsoft 365 Copilot license in the tenant.

For more information, see [Agent capabilities and licensing models](microsoft-365-copilot/extensibility/prerequisites).

For information about usage billing rates, see [Billing rates and management](/microsoft-copilot-studio/requirements-messages-management).

## Related content

- [Microsoft 365 Copilot connectors overview](overview.md)
- [Deploy Microsoft 365 Copilot connectors](deployment-overview.md)