---
title: "Google Drive Microsoft 365 Copilot connector troubleshooting"
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 12/16/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Google Drive Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Google Drive Microsoft 365 Copilot connector

The Google Drive Microsoft 365 Copilot connector allows your organization in Microsoft 365 to index files from Google Drive, making them available to Microsoft 365 Copilot and Microsoft 365 Search. This article provides troubleshooting information for common errors you might encounter when deploying or managing this connector.

To verify Google Drive service configuration and help troubleshoot errors, see [Set up the Google Workspace service for connector ingestion](google-drive-admin-setup.md).

## Google Drive connector troubleshooting

### Invalid credentials detected

**Error:**  
Invalid credentials detected. Check the credential info and check the permissions of the service account.

**Resolution:**  
This error occurs when the service account lacks the necessary permissions for Google Drive access.
- Check the credentials info of the account.
- Ensure that credentials are correctly filled in on the setup page.

### Missing required permissions for users or files

**Error:**  
Authentication error: one or more required OAuth scopes for your service account are missing.

**Resolution:**  
Your service account must include all of the following API scopes:
- `https://www.googleapis.com/auth/admin.directory.user.readonly`
- `https://www.googleapis.com/auth/drive.readonly`
- `https://www.googleapis.com/auth/admin.directory.group.readonly`
- `https://www.googleapis.com/auth/admin.reports.audit.readonly`


### Failed to capture file information

**Error:**  
Failed to capture file information. Ensure the workspace isn't empty and has files accessible to the admin.

**Resolution:**  
During the connector setup, you must have at least one file in your organization's workspace to test the connection successfully.


### Encrypted files might fail to be ingested

**Error:**  
Encrypted files aren't decrypted on the Google Drive side, and the Google Drive API doesn't indicate whether a file is encrypted. As a result, encrypted files might not ingest properly, or ingestion might fail due to size limits.

**Cause:**  
The document parser can't extract encrypted content. The connector tries to ingest the full encrypted content, which can exceed size limits and fail ingestion.

**Workaround:**  
Currently, there's no direct mitigation because encryption status isn't detectable via the API. To manage this issue:
- Monitor ingestion logs for encrypted-file-related ingestion failures.
- Consider excluding encrypted files from the sync scope if they consistently cause failures.

## Related content

- [Google Drive connector overview](google-drive-overview.md)
- [Deploy the Google Drive connector](google-drive-deployment.md)
