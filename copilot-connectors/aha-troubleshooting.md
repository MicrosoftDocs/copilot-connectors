---
title: "Troubleshoot issues with the Aha! Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 01/08/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Aha! Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Aha! Microsoft 365 Copilot connector

The Aha! Features and Ideas Microsoft 365 Copilot connectors empower your organization to index and search Aha! features and ideas across your enterprise.  This article provides troubleshooting information for common errors that you might encounter when you deploy the Aha! connector.

To verify Aha! configuration information to help troubleshoot errors, see [Set up the Aha! service for connector ingestion](aha-admin-setup.md).

## Aha! connector troubleshooting

The following table lists common issues and steps to resolve them.

| Issue | Possible cause | Resolution |
|-------|----------------|------------|
| Authentication fails during setup | Incorrect client ID or client secret | Verify that the client ID and client secret match the values generated in the Aha! OAuth application. Make sure that the redirect URI is correct for your environment (Enterprise or Government). |
| Connector can't access Aha! data | Network restrictions or IP allow list not configured | Confirm that Microsoft 365 Copilot Connector IP addresses are added to the allow list in Aha! under **Account** > **Security and single sign-on** > **IP address–based access control**. |
| Data not indexing after deployment | Crawl frequency settings or authorization incomplete | Check that the connector is authorized in the Microsoft 365 admin center. Review sync settings for incremental and full crawl intervals. |
| Limited or missing properties in search results | Schema not configured or properties removed | Verify property mappings in **Custom setup**. Make sure that required properties (such as `name`, `description`, and `status`) are included and correctly labeled. |
| OAuth authorization errors | Redirect URI mismatch | Confirm that the redirect URI entered in Aha! matches the Microsoft 365 environment: `https://gcs.office.com/v1.0/admin/oauth/callback` (Enterprise) or `https://gcsgcc.office.com/v1.0/admin/oauth/callback` (Government). |

## Related content

- [Aha! connector overview](aha-overview.md)
- [Deploy the Aha! connector](aha-deployment.md)
