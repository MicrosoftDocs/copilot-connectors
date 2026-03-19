---
title: "Zendesk Help Center Microsoft 365 Copilot connector troubleshooting"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: ang.gao
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 11/24/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Zendesk Help Center Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Zendesk Help Center Microsoft 365 Copilot connector

The Zendesk Help Center Microsoft 365 Copilot connector enables your organization to index articles from Zendesk Help Center (also known as Zendesk Guide). This article provides troubleshooting information for common errors that you might encounter when deploying or managing the Zendesk Help Center connector.

To verify Zendesk Help Center connector configuration information to help troubleshoot errors, see [Deploy the Zendesk Help Center connector](zendesk-help-center-deployment.md).

## Zendesk Help Center connector troubleshooting

The following table lists common errors and troubleshooting steps.

| Error    | Troubleshooting |
|----------|-----------------|
| Can't authenticate with the data source.        | Verify that your instance URL is correct and check your credentials. |
| You don't have permission to access this data source. | This issue can occur when the service account lacks access to required data. Check the error message for the specific article. For more information, see [Using OAuth authentication with your application](https://support.zendesk.com/hc/articles/4408845965210-Using-OAuth-authentication-with-your-application). |

## Related content

- [Zendesk Help Center connector overview](zendesk-help-center-overview.md)
- [Deploy the Zendesk Help Center connector](zendesk-help-center-deployment.md)
