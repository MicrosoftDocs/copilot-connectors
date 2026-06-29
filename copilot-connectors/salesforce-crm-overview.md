---
ms.date: 06/24/2026
title: "Salesforce CRM connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Learn about the capabilities, limitations, and use cases for the Salesforce CRM Copilot connector."
---

# Salesforce CRM connector overview

The Salesforce CRM Microsoft 365 Copilot connector integrates Salesforce data into Microsoft 365. This integration enables Copilot, Copilot Search, and Microsoft Search to surface CRM records directly within apps like Teams, Outlook, and SharePoint.

When you configure the Salesforce CRM connector for your organization and index data from Salesforce, users can search for contacts, opportunities, leads, cases, and accounts in Microsoft Search, Microsoft 365 Copilot, and Copilot Search. The connector bridges the gap between CRM data and daily productivity tools, delivering faster pipeline reviews, improved customer context, and streamlined cross-team collaboration.

## Why use the Salesforce CRM connector to index your data?

Organizations that rely on Salesforce CRM for customer relationship management often face knowledge silos: sales reps search in Salesforce while the rest of the company works in Microsoft 365. The Salesforce CRM Copilot connector addresses this gap by surfacing CRM records in the tools employees already use. Copilot can then answer questions about accounts, deals, and cases without users switching context.

The Salesforce CRM Copilot connector provides the following benefits:

- **Accelerates deal velocity** - Sales teams pull opportunity details, contact history, and account context into Teams conversations and Outlook emails without leaving their flow of work.
- **Improves customer service** - Support agents retrieve open cases, account relationships, and historical resolutions through Copilot, reducing time-to-resolution.
- **Enables data-driven decisions** - Managers and executives get immediate answers about pipeline, case backlog, and lead status grounded in live Salesforce data.
- **Strengthens cross-team collaboration** - Marketing, finance, and operations teams discover relevant CRM records when building campaigns, forecasts, or account plans.
- **Reduces context switching** - Employees access Salesforce data directly within Microsoft 365 apps, eliminating the need to open and search Salesforce separately.
- **Preserves security and compliance** - The connector respects Salesforce record-level access controls, ensuring that users only see CRM data they have permission to access in Copilot and Search results.

## Build agents with the Salesforce CRM connector

Developers can use this connector as a knowledge source in declarative agents they build with [Microsoft Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that agent builders can use to help their users retrieve information from Salesforce CRM.

**Account and contact lookups**

- Pull up the account for Pinnacle Health Systems.
- Find the contact Sarah Mitchell.
- What industry is Grand Hotels & Resorts Ltd in?
- Give me the name, title, and email for all contacts at United Oil.

**Opportunity tracking**

- What stage is the Dickenson Mobile Generators opportunity in?
- Show me opportunities for Express Logistics and Transport with their stage and amount.
- Which opportunities are in the Negotiation/Review stage?

**Case management**

- Tell me about case 00001005 for Pinnacle Health Systems.
- Show me cases with status Escalated for Pinnacle Health Systems.
- Show me Mechanical type cases for Pinnacle Health Systems.

**Lead tracking**

- Find the lead Karen Foster.
- Which leads have a status of Working - Contacted?
- Show me leads from the Agriculture industry with a Hot rating.

**Custom fields (requires custom field configuration)**

- What is the product on case 00001001?
- Show me all cases on the GC1060 product.
- Which cases have both SLA violation and potential liability flagged?

## Connector capabilities and limitations

The Salesforce CRM connector has the following key capabilities:

- **Indexes core CRM objects** - Crawls standard Salesforce objects including Account, Contact, Opportunity, Lead, and Case. For the full list, see [Data types indexed from Salesforce CRM](#data-types-indexed-from-salesforce-crm).
- **Supports custom fields** - Admins can select custom fields (fields ending in `__c`) and standard fields not included in the default schema. For configuration steps, see [Add properties](salesforce-crm-deployment.md#add-properties).
- **Respects Salesforce permissions** - The connector honors Salesforce record-level sharing rules and object permissions. Users only see records they have access to in Salesforce.

The Salesforce CRM connector has the following limitations:

- **Field-level security (FLS) not honored when opted in** - FLS-restricted fields are excluded from indexing by default. If you opt in to index FLS-restricted fields, the connector doesn't enforce Salesforce FLS when showing results, so review carefully before enabling. For configuration steps, see [Include FLS-restricted fields](salesforce-crm-deployment.md#include-fls-restricted-fields).
- **Limited object coverage** - The connector currently indexes Account, Contact, Opportunity, Lead, and Case objects. Support for additional standard objects is on the roadmap. If you need a specific object included, contact Microsoft support. This documentation will be updated when new object support is released.
- **Comments and attachments not indexed by default** - Comments and attachments on records are in private preview. Because this content can introduce noise that affects core use cases, it is not included by default. Admins can selectively enable comments and attachments in the **Manage properties** section.
- **API usage during crawls** - Full crawls consume Salesforce API quota. Consider scheduling full crawls during off-peak hours or weekends, especially for orgs with large record volumes, to avoid impacting daily operations or exhausting API limits.

If your scenario needs objects or fields not covered by the connector's default behavior, you can build a custom synced connector using the [Copilot connectors API](/graph/connecting-external-content-connectors-api-overview). A reference implementation for Salesforce CRM is available at the [Salesforce custom Copilot connector](https://github.com/microsoft/Salesforce-Custom-Copilot-Connector) repo on GitHub. For an overview of the sample and customization guidance, see [Build a custom Salesforce CRM connector](salesforce-custom-connector-sample.md).

## Data types indexed from Salesforce CRM

The Salesforce CRM connector indexes the following Salesforce objects so they can be used in Copilot, Copilot Search, and Microsoft Search.

| Salesforce object | Description |
| ----------------- | ----------- |
| **Account** | Company or organization records, including industry, revenue, address, and ownership details. |
| **Contact** | People associated with accounts, including name, title, email, phone, and mailing address. |
| **Opportunity** | Sales deals, including stage, amount, close date, probability, and associated account. |
| **Lead** | Prospective customers not yet converted to contacts or opportunities, including source, status, and company. |
| **Case** | Support tickets, including subject, description, priority, status, and associated account or contact. |

## Permissions model and access control

You can configure the Salesforce CRM connector to enforce that only users who have access to a Salesforce record can see it in Copilot responses and search results. The system uses the Salesforce access control list (ACL) based on record-level sharing rules.

The connector supports the following access configurations:

- **Only people with access to this data source** (default) - The connector enforces Salesforce record ownership, sharing rules, and role hierarchy. Users only see records they can access in Salesforce. Identity mapping (Microsoft Entra ID or non-Entra ID) determines which Microsoft 365 user corresponds to each Salesforce user.

- **Everyone** - All indexed Salesforce data is searchable by any user in the tenant. Use this option for non-confidential CRM data that should be broadly accessible.

For identity mapping configuration, see [Set up the Salesforce service for connector ingestion](salesforce-crm-admin-setup.md#define-identity-mapping).

> [!NOTE]
> Updates to groups governing access permissions sync in full crawls only. Incremental crawls don't support processing of updates to permissions.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Salesforce CRM connector](salesforce-crm-deployment.md)
