---

title: "Troubleshoot issues with the PagerDuty Incidents connector"
ms.author: wangchen
author: wangchen
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.localizationpriority: Medium
description: "Find troubleshooting information for the PagerDuty Incidents Microsoft 365 Copilot connector."
ms.date: 05/15/2026
---

# Troubleshoot issues with the PagerDuty Incidents connector (preview)

The PagerDuty Incidents Microsoft 365 Copilot connector integrates PagerDuty incident data into Microsoft 365, enabling Copilot and Microsoft Search to surface incident details directly within apps like Teams, Outlook, and SharePoint.

This article provides troubleshooting information for common errors that you might encounter when you deploy the PagerDuty Incidents connector.

To verify PagerDuty configuration information to help troubleshoot errors, see [Set up the PagerDuty Incidents connector](PagerDuty-Incident-Connector-Deployment.md).

## PagerDuty Incidents connector troubleshooting

You might encounter the following errors when you deploy the PagerDuty Incidents connector or when the connector indexes data.

| Deployment step | Error or error message | Possible reason | Resolution |
| --- | --- | --- | --- |
| Connection settings | Your security credentials have expired for this session. Please go back and sign in again with your Client ID and Client Secret. | The OAuth credentials have expired. | Create a new app in the PagerDuty app registration settings and copy the latest Client ID and Client Secret from the settings tab to authenticate. For more information, see [Register an App](https://developer.pagerduty.com/docs/register-an-app). |
| Connection settings | Invalid credentials detected. Please check the credential info and check the permission scopes of the PagerDuty App. | The Client ID or Client Secret is incorrect, or the app doesn't have the required permission scopes. | Go to the PagerDuty app registration settings and verify that the Client ID and Client Secret are correct. Ensure the app has the following scopes enabled: Audit Records (Read), Schedules (Read), Teams (Read), Users (Read), Incidents (Read), and Incident Types (Read). |
| Crawl | Items are not being indexed or item count is lower than expected. | The **Since (Month)** content filter might be set to a short time range, or the PagerDuty account has restricted access to certain incidents. | Adjust the **Since (Month)** parameter in the content filter settings to include a wider date range. Verify that the authenticated PagerDuty account has access to the incidents you expect to be indexed. |


## Common configuration issues

### Redirect URL mismatch

If authentication fails during setup, verify that the Redirect URL configured in your PagerDuty app registration matches your Microsoft 365 environment:

- For M365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`
- For M365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`

### OAuth scope configuration

The PagerDuty app must be configured with **Scoped OAuth** and must have the following scopes enabled:

| Scope | Access level |
| --- | --- |
| Audit Records | Read Access |
| Schedules | Read Access |
| Teams | Read Access |
| Users | Read Access |
| Incidents | Read Access |
| Incident Types | Read Access |

If any of these scopes are missing, the connector might fail to authenticate or might not index all expected data.

### Service region API URL

PagerDuty supports multiple service regions. Using the wrong API URL causes connection failures.

| Service region | REST API URL |
| --- | --- |
| US | `https://api.pagerduty.com` |
| EU | `https://api.eu.pagerduty.com` |

For more information, see [PagerDuty Service Regions](https://support.pagerduty.com/main/docs/service-regions).

## Get help

If you continue to experience issues or want to provide feedback, contact [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).
