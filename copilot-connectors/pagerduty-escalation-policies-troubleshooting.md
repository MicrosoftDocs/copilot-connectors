---
title: "Troubleshoot issues with the PagerDuty Escalation Policies connector"
ms.author: wangchen
author: wangchen
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 05/26/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the PagerDuty Escalation Policies Copilot connector."
---

# Troubleshoot issues with the PagerDuty Escalation Policies connector

The PagerDuty Escalation Policies Microsoft 365 Copilot connector enables users to surface PagerDuty escalation policy data in Microsoft 365 experiences such as Copilot, Copilot Search, and Microsoft Search. This article provides troubleshooting information for common errors that you might encounter when you deploy the PagerDuty Escalation Policies connector.

## PagerDuty Escalation Policies connector troubleshooting

The following table lists common errors and recommended troubleshooting steps.

| Error or issue | Possible cause | Recommended action |
| --- | --- | --- |
| **Your security credentials have expired for this session. Please go back and sign in again with your Client ID and Client secret.** | OAuth credentials expired. | Create a new app ID in the PagerDuty app registration setting and copy the latest Client ID and Client Secret from **settings** to reauthenticate the connector. |
| **Invalid credentials detected. Please check the credential info and check the permission scopes of the PagerDuty App.** | Incorrect Client ID or Client Secret, or missing required permission scopes. | Go back to the PagerDuty app registration setting and verify that the Client ID and Client Secret are correct and that all required permission scopes are selected: Audit records (Read), Escalation Policies (Read), Teams (Read), and Users (Read). |
| **Escalation policies not appearing in Copilot or search** | Permissions mismatch or Advanced Permissions enabled in PagerDuty. | When Advanced Permissions is enabled in PagerDuty, only members of teams linked to a specific escalation policy can access it. Verify that users requesting access are members of the appropriate teams in PagerDuty. |
| **Connector fails to authenticate** | Invalid or expired OAuth token, or incorrect redirect URL. | Verify that the redirect URL is correctly configured in the PagerDuty app registration. For M365 Enterprise, use `https://gcs.office.com/v1.0/admin/oauth/callback`. For M365 Government, use `https://gcsgcc.office.com/v1.0/admin/oauth/callback`. |
| **Missing audit properties (createdBy, lastModifiedBy, etc.)** | PagerDuty plan doesn't support audit properties. | A PagerDuty Business or Enterprise plan license is required to index audit-related properties. Upgrade your PagerDuty plan or contact your PagerDuty administrator. |
| **Connector setup fails in admin center** | Incorrect REST API URL or missing API access. | Confirm that the REST API URL is correct based on your PagerDuty service region. For US, use `https://api.pagerduty.com`. For EU, use `https://api.eu.pagerduty.com`. Ensure API access is enabled for your PagerDuty account. |
| **Permission changes not reflected immediately** | Connector sync delay. | Wait for the next scheduled crawl. The PagerDuty Escalation Policies connector performs a full crawl every 24 hours by default. You can manually trigger a crawl or adjust the sync schedule in the connector settings. |
| **Incomplete escalation policy data indexed** | Missing required scopes in PagerDuty app registration. | Verify that all required scopes are selected in the PagerDuty app registration: Audit records (Read), Escalation Policies (Read), Teams (Read), and Users (Read). Update the scopes and reauthenticate if necessary. |

## Related content

- [PagerDuty Escalation Policies connector overview](pagerduty-escalation-policies-overview.md)
- [Deploy the PagerDuty Escalation Policies connector](pagerduty-escalation-policies-deployment.md)
