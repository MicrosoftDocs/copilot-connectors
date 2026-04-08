---
title: "Troubleshoot issues with the Dropbox connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: ang.gao
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 11/21/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Dropbox Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Dropbox connector

The Dropbox connector integrates Dropbox content into Microsoft 365, so Copilot and Microsoft Search can surface files and insights directly within apps such as Teams, Outlook, and SharePoint. This article provides troubleshooting guidance for common issues you might encounter when deploying the Dropbox connector.

To verify Dropbox configuration and assist with troubleshooting, see [Set up the Dropbox service for Dropbox Microsoft 365 Copilot connector ingestion](dropbox-admin-setup.md).

## Dropbox connector troubleshooting

The following table lists common errors and troubleshooting steps.

| Error | Troubleshooting steps |
|-------|------------------------|
| Required permission scopes are missing | Make sure that all required scopes are selected in the Dropbox App Console:<br>**Individual scopes:** files.metadata.read, files.content.read, sharing.read, file_requests.read<br>**Team scopes:** team_info.read, team_data.member, team_data.governance.write, team_data.governance.read, team_data.content.read, files.team_metadata.read, members.read, groups.read, events.read |
| OAuth 2.0 flow failed | Verify credential information and confirm that the Dropbox App is configured correctly in the **OAuth 2.0** settings tab. |
| OAuth 2.0 flow failed due to user role | Confirm that the Dropbox user associated with the team access token holds the team admin role and is active. |
| Security credentials expired | Sign in again and refresh credentials. Copy the latest app key and app secret from the Dropbox App Console. |
| Invalid credentials detected | Check credential information and confirm that permission scopes in the Dropbox App Console are correctly configured. |

## Related content

- [Dropbox connector overview](dropbox-overview.md)
- [Deploy the Dropbox connector](dropbox-deployment.md)
