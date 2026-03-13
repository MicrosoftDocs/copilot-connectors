---
title: "Troubleshoot issues with the Atlassian Jira Cloud Microsoft 365 Copilot connector"
description: "Learn how to troubleshoot common issues with the Atlassian Jira Cloud Microsoft 365 Copilot connector, including error messages, possible causes, and resolution steps."
ms.author: lauragra
author: lauragra
manager: calvind
ms.topic: troubleshooting
ms.service: copilot-connectors
ms.date: 11/19/2025
ms.localizationpriority: medium
---

# Troubleshoot issues with the Atlassian Jira Cloud Microsoft 365 Copilot connector

This article provides troubleshooting guidance for the Atlassian Jira Cloud Microsoft 365 Copilot connector*, including common error messages, possible causes, and next steps.
This article provides troubleshooting guidance for the Atlassian Jira Cloud Microsoft 365 Copilot connector, including common error messages, possible causes, and next steps.
To verify Jira Cloud configuration information to help troubleshoot errors, see [Set up the Jira Cloud service for connector ingestion](jira-cloud-admin-setup.md).

## Jira Cloud connector troubleshooting

The following table lists common errors that can occur during connector configuration or crawling and possible reasons for the issue.

| Step  | Error message| Possible reason |
|-------|--------------|-----------------|
| **Connection settings**      | The request is malformed or incorrect. | Incorrect Jira site URL.   |
| **Connection settings**      | Unable to reach the Jira cloud service for your Jira site. | Incorrect Jira site URL.  |
| **Connection settings**      | The client doesn't have permission to perform the action. | Invalid API token provided for Basic authentication.   |
| **Connection settings**      | "Something went wrong" error in OAuth pop-up window.  | The scopes granted to the OAuth app don't match. The mismatched scopes are listed in the pop-up window. |
| **Crawl time (post-configuration)** | Can't authenticate with the data source. Verify the credentials associated with this data source are correct. | The user doesn't have one or more permissions required to crawl Jira.            |
| **Crawl time (post-configuration)** | You don't have permission to access this data source. You can contact the owner of this data source to request permission. | If using OAuth, the app scopes might have changed, or the app might have expired or been deleted.<br>If using Basic authentication, the API token might have expired or been deleted. |
| **Crawl time (post-configuration)** | Error code: 1003 - You don't have permission to access this data source.<br>Detailed error code: 7612 | The crawl account doesn't have **Browse projects** permission for the listed project (under the 'item ID' column). |

## Issue resolution steps

Use the following steps to help resolve issues:
- Verify that the Jira Cloud instance URL is correct and resolves to your Jira dashboard.
- Confirm that the service account has the required permissions:
  - **Browse projects** (required)
  - Issue-level security and user/group browsing permissions for security trimming (optional)
- For OAuth issues:
  - Check that all required scopes are granted.
  - Verify that the callback URL is correct: `https://gcs.office.com/v1.0/admin/oauth/callback`
- For Basic authentication:
  - Regenerate the API token if it expired or was deleted.
  - Confirm that the username and token match the Jira account used for crawling.

## Related content

- [Jira Cloud connector overview](jira-cloud-overview.md)
- [Set up the Jira Cloud service for connector ingestion](jira-cloud-admin-setup.md)
- [Deploy the Jira Cloud connector](jira-cloud-deployment.md)
