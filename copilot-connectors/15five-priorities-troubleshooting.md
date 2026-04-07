---
title: "Troubleshoot issues with the 15Five Priorities connector"
ms.author: lauragra
author: wangchen
manager: zezhangzhao
ms.reviewer: wangchen
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 04/07/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the 15Five Priorities Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the 15Five Priorities connector

The 15Five Priorities Microsoft 365 Copilot connector enables your organization to index 15Five priority data so the data surfaces in Microsoft 365 Copilot and Microsoft Search experiences. This article provides troubleshooting information for common errors that you might encounter when you deploy the connector.

## 15Five Priorities connector troubleshooting

The following table lists common errors and troubleshooting steps.

| Error | Resolution |
|-------|------------|
| Your security credentials expired for this session. Please go back and sign in again with your app key and app secret. | Credential information expired. Create a new key in the 15Five integrations settings and copy the latest access token from the settings tab in 15Five to authenticate. |
| Invalid credentials detected. Please check the credential info and check the permission scopes of the 15Five App. | This error indicates invalid credentials. Go to the 15Five integrations settings and verify that the access token is correct. |

## Related content

- [15Five Priorities connector overview](15five-priorities-overview.md)
- [Deploy the 15Five Priorities connector](15five-priorities-deployment.md)