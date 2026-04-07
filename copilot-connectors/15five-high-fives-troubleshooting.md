---
title: "Troubleshoot issues with the 15Five High Fives connector"
ms.author: lauragra
author: wangchen
manager: zezhangzhao
ms.reviewer: wangchen
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 04/06/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the 15Five High Fives Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the 15Five High Fives connector

The 15Five High Fives Microsoft 365 Copilot connector enables your organization to index 15Five high-five data to make it available to Microsoft 365 Copilot and Microsoft Search. This article provides troubleshooting information for common errors that you might encounter when you deploy the connector.

## 15Five High Fives connector troubleshooting

The following table lists common errors and troubleshooting steps.

| Error | Resolution |
|-------|------------|
| Your security credentials expired for this session. Please go back and sign in again with your App key and App secret. | Credential information expired. Create a new key in the 15Five integrations setting and copy the latest access token from **settings** in 15Five to authenticate. |
| Invalid Credentials detected. Please check the credential info and the permission scopes of the 15Five App. | This error occurs when there's a problem with the credentials. Go to the 15Five integrations setting and verify that the access token is correct. | 

## Related content

- [15Five High Fives connector overview](15five-high-fives-overview.md)
- [Deploy the 15Five High Fives connector](15five-high-fives-deployment.md)