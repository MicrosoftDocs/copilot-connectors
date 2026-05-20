---
title: "Troubleshoot issues with the PagerDuty Incidents connector"
ms.author: wangchen
author: wangchen
manager: zezhangzhao
ms.reviewer: lauragra
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 05/20/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the PagerDuty Incidents Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the PagerDuty Incidents connector

The PagerDuty Incidents Microsoft 365 Copilot connector integrates PagerDuty incident data into Microsoft 365, enabling Copilot and Microsoft Search to surface incident details directly within apps like Teams, Outlook, and SharePoint.

This article provides troubleshooting information for common errors that you might encounter when you deploy the PagerDuty Incidents connector.

To verify PagerDuty configuration information to help troubleshoot errors, see [Deploy the PagerDuty Incidents connector](pagerduty-incidents-deployment.md).

## PagerDuty Incidents connector troubleshooting

You might encounter the following errors when you deploy the PagerDuty Incidents connector or when the connector indexes data.

| Deployment step | Error or error message | Possible reason | Resolution |
| --- | --- | --- | --- |
| Connection settings | Your security credentials have expired for this session. Please go back and sign in again with your Client ID and Client Secret. | The OAuth credentials expired. | Create a new app in the PagerDuty app registration settings. Copy the latest Client ID and Client Secret from the settings tab to authenticate. For more information, see [Register an App](https://developer.pagerduty.com/docs/register-an-app). |
| Connection settings | Invalid credentials detected. Please check the credential info and check the permission scopes of the PagerDuty App. | The Client ID or Client Secret is incorrect, or the app doesn't have the required permission scopes. | Go to the PagerDuty app registration settings and verify that the Client ID and Client Secret are correct. Ensure the app has the following scopes enabled: Audit Records (Read), Schedules (Read), Teams (Read), Users (Read), Incidents (Read), and Incident Types (Read). |
| Crawl | Items aren't indexed or the item count is lower than expected. | The **Since (Month)** content filter might be set to a short time range, or the PagerDuty account has restricted access to certain incidents. | Adjust the **Since (Month)** parameter in the content filter settings to include a wider date range. Verify that the authenticated PagerDuty account has access to the incidents you expect to be indexed. |

### Redirect URL mismatch

If authentication fails during setup, verify that the Redirect URL configured in your PagerDuty app registration matches your Microsoft 365 environment:

- For Microsoft 365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`
- For Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`

### OAuth scope configuration

If any scopes are missing, the connector might fail to authenticate or might not index all expected data. Configure the PagerDuty app with **Scoped OAuth** and enable the following scopes.

| Scope | Access level |
| --- | --- |
| Audit Records | Read Access |
| Schedules | Read Access |
| Teams | Read Access |
| Users | Read Access |
| Incidents | Read Access |
| Incident Types | Read Access |

### Service region API URL

PagerDuty supports multiple service regions. If you use the wrong API URL, you might experience connection failures.

| Service region | REST API URL |
| --- | --- |
| US | `https://api.pagerduty.com` |
| EU | `https://api.eu.pagerduty.com` |

For more information, see [PagerDuty Service Regions](https://support.pagerduty.com/main/docs/service-regions).

## Related content

- [PagerDuty Incidents connector overview](pagerduty-incidents-overview.md)
- [Deploy the PagerDuty Incidents connector](pagerduty-incidents-deployment.md)
