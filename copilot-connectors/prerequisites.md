---
title: "Prerequisites for deploying connectors"
ms.author: lauragra
author: lauragra
manager: calvind
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Learn about the licensing requirements for deploying Copilot connectors in your organization."
ms.date: 04/09/2026
---

# Prerequisites for deploying connectors

Microsoft 365 Copilot connectors enable your organization to bring external data into the intelligent experiences within Microsoft 365. This article describes the prerequisites required to deploy Copilot connectors in your organization.

Copilot connectors are available to all organizations with Microsoft 365 licenses. The experiences that connector content surfaces in—such as Microsoft Search or Microsoft 365 Copilot—depend on your organization's licensing.

Some prebuilt connectors also have unique prerequisites and setup steps. For more information, see the deployment guide for that connector.

## Admin roles and access

To configure and deploy Copilot connectors, you must be an AI administrator in the Microsoft 365 admin center.

In addition, for prebuilt connectors (such as Google Drive, Confluence, ServiceNow), you must have admin access to the external service (Google Workspace Super Admin, Confluence Admin).

## Data source credentials and configuration

To deploy connectors, you need access to the data source, including:

- Data source authentication credentials (API keys, service account tokens).
- Configuration of the external environment (Google Cloud Project for Google Drive, Confluence site URL). For information about the configuration details for specific connectors, see the deployment guide for that connector.
- Permissions to access the content you want indexed (wiki pages, catalog items, meeting transcripts, and so on).

## Licensing and eligibility

Copilot connectors work across multiple Microsoft 365 surfaces. The surfaces available to your users depend on your organization's licensing:

| License | Microsoft Search | Microsoft 365 Copilot grounding | Copilot Chat agents (grounded on connector data) |
|---|---|---|---|
| Microsoft 365 (any plan) | ✅ | ❌ | ❌ |
| Microsoft 365 + Microsoft 365 Copilot add-on | ✅ | ✅ | ✅ |
| Copilot Studio license | ✅ | ❌ | ✅ |
| Usage billing (pay-as-you-go) enabled in tenant | ✅ | ❌ | ✅ |

> [!NOTE]
> Microsoft 365 Copilot is an add-on to Microsoft 365. If your organization has Microsoft 365 Copilot licenses, connector grounding in Copilot is included—no separate connector entitlement is required. Advanced features such as semantic search require at least one Microsoft 365 Copilot license in the tenant.


For more information, see [Agent capabilities and licensing models](/microsoft-365/copilot/extensibility/prerequisites).

For information about usage billing rates, see [Billing rates and management](/microsoft-copilot-studio/requirements-messages-management).

## Related content

- [Microsoft 365 Copilot connectors overview](overview.md)
- [Deploy Microsoft 365 Copilot connectors](deployment-overview.md)
