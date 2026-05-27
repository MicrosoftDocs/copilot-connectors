---
title: "Airtable connector troubleshooting (preview)"
ms.author: kailiang
author: Kai-Cloud
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 05/27/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Airtable Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Airtable connector (preview)

The Airtable Microsoft 365 Copilot connector enables users to surface Airtable records in Microsoft 365 apps such as Teams, Outlook, and SharePoint using Copilot, Copilot Search, and Microsoft Search. This article provides troubleshooting information for common errors that you might encounter when you deploy the Airtable connector.

To verify Airtable configuration information to help troubleshoot errors, see [Set up the Airtable service for connector ingestion](airtable-admin-setup.md).

> [!NOTE]
> The Airtable connector is currently in preview. Connector functionality and requirements are subject to change.

## Airtable connector troubleshooting

The following table lists common errors and recommended troubleshooting steps.

| Error or issue | Possible cause | Recommended action |
|---|---|---|
| **OAuth authorization fails with "Invalid Credentials detected"** | The OAuth integration isn't allowlisted for the enterprise. | In the Airtable Admin Hub, go to **Settings** > **Integrations & development** > **Third party integration allowlist**, choose **Allow integration**, and enter the **Client ID** of the integration. Retry the authorization. |
| **OAuth authorization fails with redirect URI mismatch** | The redirect URL registered in the Airtable OAuth integration doesn't match the expected callback URL. | Verify that the OAuth integration includes the callback URL: `https://gcs.office.com/v1.0/admin/oauth/callback`. |
| **"Invalid scope" error during authorization** | A required read scope isn't enabled, or an unsupported scope is enabled on the OAuth integration. | In the Airtable Builder Hub, enable only the read scopes listed in the deployment guide. Don't enable write or manage scopes. |
| **Enterprise ID not accepted during setup** | The Enterprise ID is missing the `ent` prefix or was copied from the wrong location. | Confirm that the value starts with `ent` and was copied from the Airtable Admin Hub URL (`https://airtable.com/admin/{enterpriseId}/...`). |
| **Connection stuck in Draft** | The OAuth authorization step wasn't completed. | Reopen the connector setup, choose **Authorize**, and complete the OAuth flow. The connection remains in Draft until authorization succeeds. |

## Related content

- [Airtable connector overview](airtable-overview.md)
- [Set up the Airtable service for connector ingestion](airtable-admin-setup.md)
- [Deploy the Airtable connector](airtable-deployment.md)
