---
title: "Jira Data Center connector troubleshooting"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: neocheng
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 12/17/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Jira Data Center Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Jira Data Center connector

The Jira Data Center Microsoft 365 Copilot connector indexes Jira Data Center issues and project data so users can retrieve and analyze content in Microsoft 365. This article provides troubleshooting information for common errors that you might encounter when you deploy the Jira Data Center connector or run the connection.

## Jira Data Center connector troubleshooting

The following table lists common issues you might encounter during connector deployment or indexing and provides possible causes.

| Deployment step | Error or error message | Possible cause |
|-----------------|------------------------|------------------|
| **Connection settings** | Unable to reach the Jira Data Center service. | The Microsoft Graph Connector Agent might be offline or disconnected. Firewall or proxy rules might be blocking outbound access to the Jira Data Center URL. Verify agent connectivity and network allowlists. |
| **Connection settings** | The request is malformed or incorrect. | The Jira site URL might be incorrect. Make sure that the URL begins with `https://` and doesn’t contain trailing slashes. |
| **Authentication** | The client doesn't have permission to perform the action. | The client ID or client secret from Jira Application Links might be invalid or incorrect. Confirm that the Application Link is configured as an *Incoming* connection with **Admin** scope selected. |
| **Select properties** | No preview results appear. | The JQL string might be invalid, the selected projects might not contain matching items, or the service account might not have **Browse Projects** permission for the target projects. |
| **Sync** | Permissions aren't syncing correctly. | Identity mapping might be misconfigured. Jira email addresses might not match Microsoft Entra ID user principal names (UPNs), or the Regex rule for non-Entra ID environments might be incorrect. |
| **Sync** | Some issues are missing after a crawl completes. | Jira Data Center rate limiting might be rejecting API requests during the crawl. Verify that the service account is exempt from rate limiting, or that limits are set to per-minute or per-hour — not per-second. Per-second throttling causes partial crawl failures where some issues are silently skipped. |

## Related content

- [Jira Data Center connector overview](jira-data-center-overview.md)
- [Deploy the Jira Data Center connector](jira-data-center-deployment.md)