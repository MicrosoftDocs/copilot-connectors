---
title: "Troubleshoot issues with the ServiceNow Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 09/25/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the ServiceNow Knowledge Copilot connector."
---

# Troubleshoot issues with the ServiceNow Copilot connector

The ServiceNow Knowledge Microsoft 365 Copilot connector enables organizations to index ServiceNow knowledge base (KB) articles into Microsoft 365 Copilot and search experiences. This article provides troubleshooting information for common errors that you might encounter when you deploy the ServiceNow Knowledge connector.

To verify ServiceNow configuration information to help troubleshoot errors, see [Set up the ServiceNow service for connector ingestion](servicenow-knowledge-admin-setup.md).

## ServiceNow Knowledge connector troubleshooting

The following table lists common errors with the ServiceNow Knowledge connector and how to resolve them.

| Error | Cause | Resolution |
|------|-------|------------|
| Connector fails to register in Microsoft 365 admin center | Missing permissions or incorrect configuration | Make sure that the admin account has appropriate permissions and that the ServiceNow instance URL is correct. |
| No data indexed from ServiceNow | API access not enabled or ACLs misconfigured | Enable REST API access for required tables and verify that ACLs allow read access for the connector. |
| Users unable to access indexed content | Permissions not properly assigned | Confirm role-based access control settings in Microsoft 365 and ACLs in ServiceNow. |
| Data appears outdated or incomplete | Indexing schedule not configured or sync failed | Check indexing frequency settings and validate sync status in the connector dashboard. |
| Connector returns unexpected results in Copilot | Incorrect table or field mapping | Review data source configuration and ensure relevant fields are selected for indexing. |

## Related content

- [ServiceNow Knowledge connector overview](servicenow-knowledge-overview.md)
- [Deploy the ServiceNow Knowledge connector](servicenow-knowledge-deployment.md)
