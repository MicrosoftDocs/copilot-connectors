---
title: "Troubleshoot issues with the BambooHR connector"
ms.author: danielabo
author: danipocket
manager: calvind
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: microsoft-365-copilot-connectors
ms.date: 08/17/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the BambooHR Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the BambooHR connector

The BambooHR Microsoft 365 Copilot connector allows organizations to index employee profiles from BambooHR into Microsoft Graph to make them accessible across Microsoft 365 experiences, including Microsoft 365 Copilot and Microsoft Search. This article provides troubleshooting information for common errors that you might encounter when you deploy the BambooHR connector.

For more support or to provide feedback, contact [People connectors support](mailto:peopleconnectorsfeedback@microsoft.com).

To verify BambooHR configuration information to help troubleshoot errors, see [Set up the BambooHR service for connector ingestion](bamboohr-admin-setup.md).

## BambooHR connector troubleshooting

The following table lists common errors that you might encounter and possible resolutions.

| Configuration step | Error message | Resolution |
|:---|:---|:---|
| Authentication | `Invalid Credentials` | <ul><li>Verify the credential information from the BambooHR developer portal.</li><li>Ensure that you select the required read-only scopes in the BambooHR developer portal. For more information, see [Select application scopes](bamboohr-admin-setup.md#select-application-scopes).</li><li>Verify that the app client ID and client secret match the values in your BambooHR developer portal credentials.</li><li>Verify that the redirect URLs are configured as described in [Configure redirect URLs](bamboohr-admin-setup.md#configure-redirect-urls); for Microsoft 365 Enterprise, add `https://gcs.office.com/v1.0/admin/oauth/callback`, and select **Authorize** again.</li></ul> |
| User mapping | `User mapping failed due to an invalid mapping formula or no Azure AD user with this property.` | Ensure that user work email addresses in BambooHR have a 1:1 mapping with user email addresses in Microsoft Entra. Because transformations aren't supported, email addresses must match between BambooHR and Microsoft Entra for successful indexing. |

## Related content

- [BambooHR connector overview](bamboohr-overview.md)
- [Deploy the BambooHR connector](bamboohr-deployment.md)
- [Set up the BambooHR service for connector ingestion](bamboohr-admin-setup.md)
- [Microsoft 365 Copilot connectors for people data](/graph/peopleconnectors)
