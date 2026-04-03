---
title: "Troubleshoot issues with the Monday.com connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: huichunli
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 01/13/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for common issues with the Monday.com Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Monday.com connector

The Monday.com Microsoft 365 Copilot connector allows organizations to index Monday.com boards, groups, tasks, and related metadata into Microsoft Graph so that the content can be discovered and used across Microsoft 365 experiences, including Microsoft 365 Copilot and Microsoft Search.

This article provides troubleshooting information for common errors that you might encounter when you deploy the Monday.com connector or when the connector is indexing content.

## Monday.com connector troubleshooting

You might encounter the following issues during connector setup, deployment, or content indexing.

| Deployment step | Error or issue | Possible cause | Resolution |
|---|---|---|---|
| Connection settings | Can't authenticate with the data source. | The Monday.com instance URL is incorrect, or the OAuth credentials are invalid. | Verify that the Monday.com instance URL is correct and reachable. Confirm that the OAuth client ID and client secret are correct and that the app is promoted to **Live** status in the Monday.com Developer Center. |
| Connection settings | Don't have permission to access this data source. | OAuth permissions in Monday.com aren't configured correctly or required read scopes are missing. | In the Monday.com Developer Center, ensure that all required read permissions are enabled for the OAuth app. Reauthorize the connection after updating permissions. |
| Authentication | Authorization fails during OAuth sign-in. | Redirect URLs are missing or incorrect for the OAuth app. | Verify that the redirect URL is configured correctly in Monday.com. Use the Microsoft 365 Enterprise or Microsoft 365 Government redirect URL based on your tenant type. Save changes and reauthorize the app. |
| Indexing | Content is missing or incomplete in search results. | The authorized Monday.com user doesn't have access to the missing boards or items. | Confirm that the user who authorized the connector has permission to access the boards and items that should be indexed. The connector crawls data on behalf of the OAuth-authorized user. |
| Indexing | Connector status shows crawl failures. | Daily API call limits in Monday.com are exceeded. | Review your Monday.com plan API limits and verify crawl schedules. Reduce incremental crawl frequency if necessary and use the default crawl settings when possible to stay within API limits. |
| Permissions | Users see content they shouldn't have access to, or don't see expected content. | Identity mapping between Monday.com and Microsoft Entra ID is misconfigured. | Review identity mapping settings and ensure that Monday.com user email addresses correctly map to Microsoft Entra ID user principal names. Update mapping rules and run a full crawl to apply permission changes. |
| Sync | Permission updates aren't reflected immediately. | Permission changes are processed only during full crawls. | Wait for the next full crawl or manually trigger a full crawl to ensure that permission updates are applied. |

## Related content

- [Monday.com Microsoft 365 Copilot connector overview](monday-overview.md)
- [Deploy the Monday.com Microsoft 365 Copilot connector](monday-deployment.md)
