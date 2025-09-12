---
title: "Licensing requirements for Microsoft 365 Copilot connectors"
ms.author: lauragra
author: lauragra
manager: calvind
ms.audience: Admin
ms.topic: overview
ms.service: copilot-connectors
ms.localizationpriority: medium
description: ""
ms.date: 09/09/2025
---

# Licensing requirements for Microsoft 365 Copilot connectors

Copilot connectors allow Microsoft 365 Copilot to index and reason over external data sources—such as SaaS apps, file shares, and on-prem systems—via Microsoft Graph. Understanding the licensing requirements is essential for deploying connectors effectively and managing costs.

Included Licensing
All eligible Microsoft 365 and Office 365 enterprise customers receive a default index quota of 50 million items at no additional cost. This applies to the following license tiers:

Microsoft 365: E3, E5, F1, F3, Business Basic, Standard, Premium
Office 365: E1, E3, E5, F3
Education: A3, A5
Government: G1, G3, G5


Note: Connectors in preview status do not count against the quota until they reach general availability.


Add-On Licensing
Organizations requiring additional quota can purchase it through the Microsoft 365 admin center:

Pricing: $1,000 USD per 1 million items per month
Management: Admins can monitor and adjust quota allocations as needed


Copilot Studio & Agent Licensing
When using Copilot Studio to build agents that leverage connectors:

A Copilot Studio license or Pay-As-You-Go (PAYGO) billing setup is required.
PAYGO users can access agents grounded in tenant data (e.g., SharePoint, Graph).
Advanced features like semantic search require the maker to have a Microsoft 365 Copilot license in the same tenant.


Connector Deployment & Access Control
Connectors are configured in the Microsoft 365 admin center and can be scoped using Rollout to limited audience to control access.
Once deployed, connectors can be added as knowledge sources in Copilot Studio.

Indexing Delay: Connectors may take up to 48 hours to appear in Studio after deployment.


Developer & ISV Considerations
Independent Software Vendors (ISVs) can build custom connectors using the Copilot connectors REST API, which consumes item quota.
Publishing a connector requires:

Schema registration
Packaging and validation
Compliance with Microsoft marketplace policies


Cost & Metering for Copilot Chat
For agents using Copilot Chat:

PAYGO pricing: $0.01 per message or $200 for 25,000 messages/month
Typical usage: Queries involving Graph connectors consume ~12 messages
(10 for grounding, 2 for generation)