---
title: "Prerequisites for deploying connectors"
ms.author: lauragra
author: lauragra
manager: calvind
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Learn about the licensing requirements for deploying Microsoft 365 Copilot connectors in your organization."
ms.date: 06/01/2026
---

# Prerequisites for deploying connectors

Microsoft 365 Copilot connectors bring external data into Microsoft 365 experiences such as Microsoft 365 Copilot and Microsoft Search. The following types of connectors are available:

- **Synced connectors** index content from an external data source into the Microsoft 365 substrate on a recurring schedule. 
- **Federated connectors** query the external data source at runtime without indexing.

This article covers the prerequisites that apply to synced and federated connectors.

For setup steps for individual data sources, see deployment guide for the [Microsoft-built synced connector](prebuilt-connectors-overview.md) or [Set up custom federated connectors](set-up-custom-federated-connectors.md).

## Admin roles and access

To configure and deploy Copilot connectors, you must be an AI administrator in the Microsoft 365 admin center.

In addition, for prebuilt synced connectors (such as Google Drive, Confluence, ServiceNow), you must have admin access to the external service (Google Workspace Super Admin, Confluence Admin).

## Microsoft 365 tenant

Your tenant must have Microsoft 365 licenses. The surfaces available to your users (Microsoft Search, Microsoft 365 Copilot grounding, Copilot Chat agents) and the connector types you can deploy depend on your organization's licensing. For details, see [Licensing](#licensing).

## Synced connector prerequisites

Synced connectors require:

- **Admin access to the external service.** For prebuilt synced connectors (such as Google Drive, Confluence, ServiceNow), you must have admin access to the data source - for example, Google Workspace Super Admin or Confluence Admin.
- **Data source authentication credentials**, such as API keys or service account tokens.
- **Configuration of the external environment**, such as a Google Cloud Project for Google Drive or a Confluence site URL. For configuration details, see the deployment guide for the specific connector.
- **Permissions to access the content you want indexed**, such as wiki pages, catalog items, or meeting transcripts.

Indexing of synced connector data incurs no extra cost for tenants with Microsoft 365 licenses.

## Federated connector prerequisites

Federated connectors require:

- **A Microsoft 365 Copilot add-on license for every user** who queries the federated source. For an eligibility matrix, see [Licensing](#licensing).
- **An OAuth-based identity configuration** between the external service and Microsoft Entra ID, so Copilot can query the source on behalf of the signed-in user. For custom federated connectors, see [Set up custom federated connectors](custom-federated-connectors.md).
- **A compatible external data source** that supports the required authentication and query patterns. For details, see [Federated connectors overview](federated-connectors-overview.md).

Unlike synced connectors, federated connectors don't require admin access to the data source for ingestion, and they don't index content. Content stays in the source system and is queried at runtime.

## Licensing

The following table shows which connector types and Copilot experiences each licensing model supports.

| License | Synced connectors - Microsoft Search | Synced connectors - Copilot grounding and agents | Federated connectors |
|---|---|---|---|
| Microsoft 365 (any plan) | ✅ | ❌ | ❌ |
| Microsoft 365 + Microsoft 365 Copilot add-on | ✅ | ✅ | ✅ |
| Microsoft 365 E7 | ✅ | ✅ | ✅ |
| Microsoft 365 + Copilot Studio license | ✅ | Agents only (no Copilot grounding) | ❌ |
| Microsoft 365 Copilot pay-as-you-go | ✅ | Agents only (no Copilot grounding) | ❌ |

> [!IMPORTANT]
> Federated Copilot connectors are available only to tenants and users with a Microsoft 365 Copilot add-on license (or Microsoft 365 E7). They aren't supported with Copilot Studio licenses or Microsoft 365 Copilot pay-as-you-go.

> [!NOTE]
> Microsoft 365 Copilot is an add-on to Microsoft 365. If your organization has Microsoft 365 Copilot licenses, connector grounding in Copilot is included, and no extra charges apply. Advanced features such as semantic search require at least one Microsoft 365 Copilot license in the tenant.

For more information, see [Agent capabilities and licensing models](/microsoft-365/copilot/extensibility/prerequisites#agent-capabilities-and-licensing-models).

For information about usage billing rates, see [Billing rates and management](/microsoft-copilot-studio/requirements-messages-management).

## Related content

- [Microsoft 365 Copilot connectors overview](overview.md)
- [Deploy Microsoft 365 Copilot connectors](deployment-overview.md)
