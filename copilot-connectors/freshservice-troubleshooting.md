---
title: "Troubleshoot issues with the Freshservice connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: wangchen
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 11/25/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Freshservice Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Freshservice connector

The Freshservice Microsoft 365 Copilot connector enables your organization to index Freshservice solution article data and make it available to Microsoft 365 Copilot and Microsoft Search. This article provides troubleshooting information for common errors that you might encounter when you deploy the Freshservice connector.

## Freshservice connector troubleshooting

The following table lists common errors and troubleshooting steps for the Freshservice connector.

| Error message or symptom | Possible cause | Troubleshooting steps |
|-------------------------|---------------|----------------------|
| Your security credentials expired for this session. Go back and sign in again with your API key. | Credential information expired. | Create a new API key in the Freshservice API key setting and copy the latest key from the user profile setting page to authenticate. |
| Invalid credentials detected. Check the credentials information. | Common credential error. | Go back to the Freshservice API key setting and verify that the API key is correct. If needed, generate a new API key from your Freshservice user profile settings and update the connector configuration. |

## Related content

- [Freshservice connector overview](freshservice-overview.md)
- [Deploy the Freshservice connector](freshservice-deployment.md)
