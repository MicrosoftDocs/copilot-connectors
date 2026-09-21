---
ms.date: 05/26/2026
title: "Troubleshoot issues with the PagerDuty Schedules connector"
ms.author: wangchen
author: wangchen
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: microsoft-365-copilot-connectors
ms.localizationpriority: Medium
description: "Find troubleshooting information for the PagerDuty Schedules Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the PagerDuty Schedules connector

The PagerDuty Schedules Microsoft 365 Copilot connector integrates PagerDuty schedule data into Microsoft 365, enabling Copilot and Microsoft Search to surface schedule information directly within apps like Teams, Outlook, and SharePoint.

This article provides troubleshooting information for common errors that you might encounter when you deploy the PagerDuty Schedules connector.

To verify PagerDuty configuration information to help troubleshoot errors, see [Set up the PagerDuty service for connector ingestion](pagerduty-schedules-admin-setup.md).

## PagerDuty Schedules connector troubleshooting

You might encounter the following errors when you deploy the PagerDuty Schedules connector or when the connector indexes data.

| Deployment step | Error or error message | Possible reason | Resolution |
|:------------ |:------------ |:------------ |:------------ |
| Connection settings | The request is malformed or incorrect. | Incorrect PagerDuty REST API URL. | Verify that you're using the correct REST API URL for your service region: `https://api.pagerduty.com` for US or `https://api.eu.pagerduty.com` for EU. For more information, see [Service regions](https://support.pagerduty.com/main/docs/service-regions) in the PagerDuty documentation. |
| Connection settings | Unable to reach the PagerDuty service. | Incorrect PagerDuty REST API URL or network connectivity issue. | Verify that you're using the correct REST API URL for your service region. Check that your network allows outbound connections to PagerDuty API endpoints. |
| Authentication | Invalid credentials detected. | Incorrect Client ID or Client Secret entered during authentication setup. | Verify that the Client ID and Client Secret are copied correctly from your PagerDuty OAuth app registration. Make sure that there are no extra spaces or characters. For more information, see [Set up the PagerDuty service for connector ingestion](pagerduty-schedules-admin-setup.md). |
| Authentication | The client doesn't have permission to perform the action. | Required OAuth scopes are not configured in the PagerDuty app. | Verify that all required OAuth scopes are enabled in your PagerDuty app registration: Audit records (Read), Schedules (Read), Teams (Read), and Users (Read). For more information, see [Configure OAuth scopes](pagerduty-schedules-admin-setup.md#configure-oauth-scopes). |
| Authentication | Your security credentials have expired for this session. | OAuth credentials have expired. | Create a new OAuth app in PagerDuty or regenerate the Client Secret for your existing app. Update the connector configuration with the new credentials. For more information, see [Register an OAuth 2.0 app in PagerDuty](pagerduty-schedules-admin-setup.md#register-an-oauth-20-app-in-pagerduty). |
| Authentication | Authorization failed with redirect URL mismatch. | Incorrect redirect URL configured in PagerDuty OAuth app. | Verify that the redirect URL in your PagerDuty app matches your Microsoft 365 environment: `https://gcs.office.com/v1.0/admin/oauth/callback` for Enterprise or `https://gcsgcc.office.com/v1.0/admin/oauth/callback` for Government. For more information, see [Configure redirect URLs](pagerduty-schedules-admin-setup.md#configure-redirect-urls). |
| Authentication | OAuth type mismatch. | Incorrect OAuth type selected in PagerDuty app registration. | Verify that **Scoped OAuth** is selected in your PagerDuty app registration settings. Standard OAuth is not supported by the connector. |
| Crawl | No items indexed. | PagerDuty account has no schedules, or schedules are outside the configured date range. | Verify that schedules exist in your PagerDuty account. Check the **Days Before** and **Days After** settings in the connector configuration to ensure the date range covers your schedules. For more information, see [Content filter](pagerduty-schedules-deployment.md#content-filter). |
| Crawl | Partial schedule data indexed. | The connector service account doesn't have access to all schedules. | Verify that the PagerDuty admin account used for authentication has access to all schedules you want to index. If Advanced Permissions is enabled, verify that team assignments are configured correctly. For more information, see [Advanced Permissions](https://support.pagerduty.com/main/docs/advanced-permissions) in the PagerDuty documentation. |
| Crawl | Crawl failed with API rate limit error. | PagerDuty API rate limits exceeded. | Reduce the crawl frequency or adjust the date range to index fewer schedule entries per crawl. Wait for the rate limit window to reset before retrying the crawl. For more information about PagerDuty rate limits, see the PagerDuty API documentation. |
| Permissions | Users see schedules they shouldn't have access to. | Access permissions set to **Everyone** in connector configuration. | Change the access permissions setting to **Only people with access to this data source** in the connector configuration. For more information, see [Customize user settings](pagerduty-schedules-deployment.md#customize-user-settings). |
| Permissions | Users don't see schedules they should have access to. | Identity mapping between PagerDuty and Microsoft Entra ID is incorrect. | Verify that PagerDuty user email addresses match Microsoft Entra ID user principal names (UPNs). If they don't match, configure a custom identity mapping. For more information, see [Map your non-Entra ID identities](map-non-entra-id.md). |
| Permissions | Advanced Permissions not enforced. | Team assignments in PagerDuty are not configured or Advanced Permissions is not enabled. | Verify that Advanced Permissions is enabled in PagerDuty and that schedules are assigned to the appropriate teams. For more information, see [Advanced Permissions](https://support.pagerduty.com/main/docs/advanced-permissions) in the PagerDuty documentation. |

## Related content

- [PagerDuty Schedules connector overview](pagerduty-schedules-overview.md)
- [Set up the PagerDuty service for connector ingestion](pagerduty-schedules-admin-setup.md)
- [Deploy the PagerDuty Schedules connector](pagerduty-schedules-deployment.md)
