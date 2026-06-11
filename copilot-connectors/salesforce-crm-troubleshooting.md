---
title: "Troubleshoot issues with the Salesforce CRM connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 06/05/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Salesforce CRM Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Salesforce CRM connector

The Salesforce CRM Microsoft 365 Copilot connector enables your organization to index accounts, contacts, leads, opportunities, and cases from Salesforce so users can find that data in Microsoft 365 Copilot and Microsoft Search.

This article provides troubleshooting information for common errors that you might encounter when you deploy the Salesforce CRM connector.

To verify Salesforce configuration information to help troubleshoot errors, see [Set up the Salesforce service for connector ingestion](salesforce-crm-admin-setup.md).

## Salesforce CRM connector troubleshooting

| Error | Cause | Resolution |
|---|---|---|
| Bad state error while signing in | The Salesforce connected app has **Require PKCE Extension** enabled. | In Salesforce **App Manager**, edit the connected app and clear **Require PKCE Extension**. Save the app and retry authorization. |
| OAuth scope names don't match older documentation | Salesforce renamed some OAuth scopes in the UI. | Use the current scope names: **Manage user data via APIs (api)** and **Perform requests at any time**. |
| Insufficient permissions during setup or crawl | The connector account is missing required administrative or object permissions. | Ensure **View Setup and Configuration** and API access are enabled. Under administrative permissions, enable **View Roles and Role Hierarchy**, **View All Profiles**, and **View All Users**. Grant **Read** and **View All** on Accounts, Cases, Contacts, Leads, and Opportunities. |
| Field values don't appear in search | The field isn't indexed or is blocked by field-level security (FLS). | Verify the field is selected in **Manage properties**, confirm the item and field are indexed in [Search and validate indexed content](indexed-content.md), and review FLS settings in Salesforce under **Object Manager** > **Fields & Relationships** > **View Field Accessibility**. |

## Related content

- [Salesforce CRM connector overview](salesforce-crm-overview.md)
- [Deploy the Salesforce CRM connector](salesforce-crm-deployment.md)
