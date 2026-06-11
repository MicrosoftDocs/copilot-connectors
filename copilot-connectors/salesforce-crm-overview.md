---
title: "Salesforce CRM connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 06/05/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Salesforce CRM Microsoft 365 Copilot connector."
---

# Salesforce CRM connector overview

The Salesforce CRM Microsoft 365 Copilot connector enables your organization to index Salesforce records, such as accounts, contacts, leads, opportunities, and cases, so users can discover that content in Microsoft 365 Copilot and Microsoft Search experiences.

## Why use the Salesforce CRM connector to index your data?

Organizations use the Salesforce CRM connector to bring customer and pipeline data into daily Microsoft 365 workflows.

Common use cases include:

- Help sellers and account teams quickly find customer records and deal context in Copilot.
- Surface case and account details to support and operations teams without switching apps.
- Improve cross-team visibility by making CRM records searchable in Microsoft 365.
- Support scenario-based prompting and agent experiences that rely on Salesforce business data.

## Build agents with the Salesforce CRM connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that users can use to retrieve information from Salesforce CRM.

- Summarize open opportunities for Contoso and list next steps.
- Show active support cases for Fabrikam and include owners and priorities.
- Find leads created in the last 30 days that are assigned to my team.
- List accounts with opportunities closing this quarter and show deal stage.
- Retrieve the latest activity for the top five opportunities by amount.

## Salesforce CRM connector capabilities and limitations

The Salesforce CRM connector enables users to:

- Search Salesforce accounts, contacts, leads, opportunities, and cases from Copilot and Microsoft Search.
- Apply data inclusion filters to control which Salesforce records are indexed.
- Preserve source permissions through access-control and identity mapping options.
- Configure crawl intervals for incremental and full refreshes.
- Use connector content in Copilot-based agents and workflow experiences.

The Salesforce CRM connector has the following limitations:

- It doesn't honor visibility permissions applied through managed permission sets or permission set groups.
- It doesn't support Apex-based sharing, territory-based sharing, or personal-group sharing.
- A known Salesforce API issue can affect private org-wide defaults for leads.
- Field-level security (FLS) restricted fields aren't indexed by default unless an admin explicitly opts in.

## Custom data filters

The Salesforce CRM connector includes the following custom data filters for Copilot Search:

- Modified time period to index records created or changed within a rolling time window.
- A Salesforce Object Query Language (SOQL) `WHERE` clause to include only matching records.

## Data types indexed from Salesforce CRM

By default, the connector indexes these Salesforce object types:

- Accounts
- Contacts
- Leads
- Opportunities
- Cases

Indexed content appears in Microsoft 365 Copilot and Microsoft Search for users who have access to the source records.

## Permissions model and access control

The Salesforce CRM connector supports permission-aware results through configurable access settings:

- **Visible to everyone** shows indexed content to all users in the tenant.
- **Only people with access to this data source** uses Salesforce ACLs and identity mapping.

Admins can map Microsoft Entra identities and non-Microsoft Entra identities to align Salesforce permissions with Microsoft 365 access control.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Salesforce CRM connector](salesforce-crm-deployment.md)
