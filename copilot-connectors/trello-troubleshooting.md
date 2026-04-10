---
title: "Troubleshoot issues with the Trello connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: anggao
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 04/09/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Trello Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Trello connector

The Trello Microsoft 365 Copilot connector enables your organization to index Trello cards so users can discover, access, and use Trello content directly within Microsoft 365 experiences. This article provides troubleshooting information for common errors that you might encounter when you deploy the Trello connector.

## Trello connector troubleshooting

The following table lists common errors and troubleshooting steps.

| Error | Troubleshooting steps |
|--------|-------------------------|
| Required permission scopes are missing | Make sure that all required scopes are selected in the Trello app configuration. |
| OAuth 2.0 flow failed | Verify credential information and confirm that the Trello app is configured correctly in the OAuth settings tab. |
| OAuth 2.0 flow failed due to user role | Confirm that the Trello user associated with the access token holds the required administrative role and is active. |
| Security credentials expired | Sign in again and refresh credentials. Copy the latest app key and app secret from the Trello app console. |
| Invalid credentials detected | Check credential information and confirm that permission scopes in the Trello app configuration are correctly set. |

## Related content

- [Trello connector overview](trello-overview.md)
- [Deploy the Trello connector](trello-deployment.md)