---
ms.date: 06/24/2026
title: "Build a custom Salesforce CRM connector"
ms.author: anparanjape
author: anshuman2702
manager: calvind
ms.reviewer:
ms.topic: how-to
audience: Admin
ms.audience: Admin
ms.service: copilot-connectors
ms.localizationpriority: Medium
description: "Reference implementation of a custom Microsoft 365 Copilot connector for Salesforce CRM."
---

# Build a custom Salesforce CRM connector

The Microsoft 365 Copilot Salesforce CRM custom synced connector sample is a Python reference implementation that shows how to use the [Copilot connectors API](/graph/connecting-external-content-connectors-api-overview) to ingest Salesforce CRM data into Microsoft Graph. Use the sample as a starting point when the [default Salesforce CRM connector](salesforce-crm-overview.md) doesn't cover your scenario. For example, you might need to index custom objects or standard objects beyond the default connector's default set.

The sample is published as open source at [microsoft/Salesforce-Custom-Copilot-Connector](https://github.com/microsoft/Salesforce-Custom-Copilot-Connector). Fork the repository and customize it for your organization's Salesforce schema. The repository's `README.md` covers prerequisites, architecture, deployment commands, and configuration in detail.

## When to use the sample

Consider the sample when your scenario requires:

- **Custom objects** - Salesforce objects ending in `__c` that the default connector doesn't index.
- **Standard objects beyond the default set** - For example, Campaign, FeedItem, Order, Quote, or OpportunityLineItem. The sample supports these objects in addition to Account, Contact, Lead, Opportunity, and Case.
- **Broader custom-field coverage** - Surfacing more custom fields than the default connector exposes through its **Add Properties** experience.

## Customize the sample for your Salesforce org

Edit the following files:

- **`config/schema.json`** - defines which Salesforce objects and fields are fetched per object type. Add entries for your custom objects (`__c`) and custom fields.
- **`config/graph-schema.json`** - defines the Microsoft Graph property schema your items use: property names, types, flags (`isSearchable`, `isQueryable`, `isRetrievable`, `isRefinable`), and semantic labels.
- **`config/template.json`** - the Adaptive Card template used to render the sample's items as Microsoft Search results.
- **`env/.env.local`** - connector ID, connection name, connection description, Salesforce instance URL, and tuning parameters. Put secrets in `env/.env.local.user`.

For step-by-step configuration and deployment instructions, see the repository's `README.md`.

## Related content

- [Salesforce CRM connector overview](salesforce-crm-overview.md)
- [Copilot connectors API overview](/graph/connecting-external-content-connectors-api-overview)
- [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md)
