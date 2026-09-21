---
title: "Troubleshoot issues with the Credly connector (preview)"
ms.author: vivekdatir
author: vivekdatir
manager: rampo
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: microsoft-365-copilot-connectors
ms.date: 04/09/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Credly Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Credly connector (preview)

The Credly Microsoft 365 Copilot connector integrates digital credential data from your organization's Credly account into Microsoft 365. This integration enables Copilot and profile cards to surface verified badges, awards, and certifications directly within apps like Teams, Outlook, and SharePoint.

This article provides troubleshooting information for common issues that you might encounter when you deploy the Credly connector.

> [!NOTE]
> The Credly connector is currently in preview. Connector functionality and requirements are subject to change.

## Badges don't appear on user profiles

In some cases, badges don't appear on user profiles. The following table lists possible causes and resolutions for this issue.

| Possible cause | Resolution |
|---|---|
| The user's email in Credly doesn't match their UPN or primary SMTP address in Microsoft Entra ID. | Verify that the employee's Credly account uses their organization email address. The connector matches identities by email only. |
| The user didn't accept or share the badge publicly on Credly. | Ask the user to accept the badge on their Credly profile. The connector doesn't index private or unaccepted badges. |
| The user account is inactive in your directory. | The connector only indexes credentials for active users. Confirm the user is active and licensed in your Microsoft 365 tenant. |
| The initial sync didn't complete. | Go to **Settings** > **Copilot** > **Connectors** in the Microsoft 365 admin center and check the connector status. Incremental crawls run daily and full crawls run weekly by default. |

## Copilot doesn't return Credly data

In some cases, Copilot doesn't return Credly data. The following table lists possible causes and resolutions for this issue.

| Possible cause | Resolution |
|---|---|
| Badge data isn't synced yet. | Newly earned badges require at least one completed crawl cycle before Copilot can surface them. Verify a successful sync on the **Connectors** page in the Microsoft 365 admin center. |
| Copilot cites office.com instead of Credly. | This behavior is expected. Microsoft 365 aggregates profile data from multiple sources and attributes responses to the unified profile endpoint (office.com). |

## Connection setup fails

The following table lists possible causes and resolutions for connection setup failures.

| Possible cause | Resolution |
|---|---|
| Invalid Organization ID format. | The Credly Organization ID must be a valid GUID. Copy the value directly from the Credly Developers portal. |
| Incorrect or expired Client ID or Client Secret. | Verify your credentials in the Credly Developers portal. If the Client Secret isn't saved at creation time, create a new OAuth application to generate new credentials. |
| Wrong API endpoint URL. | For production accounts, use `https://www.credly.com`. Sandbox environments require a different URL. |

## Multiple Credly organizations

Each connector instance supports a single Credly Organization ID. If your company manages multiple Credly organizations (for example, separate subsidiaries), create a separate connector instance for each Organization ID in the Microsoft 365 admin center.

## Schema can't be customized

The connector uses a fixed set of profile attributes in Microsoft Graph (the **Awards** and **Certifications** properties). You can't add, remove, or modify properties in the content schema in this release.

## Related content

- [Credly connector overview](credly-overview.md)
- [Deploy the Credly connector](credly-deployment.md)
- [Manage connections](/microsoft-365/copilot/connectors/manage-connector)
