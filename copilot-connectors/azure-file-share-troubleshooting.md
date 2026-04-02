---
title: "Azure File Share connector troubleshooting"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 12/15/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Azure File Share Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Azure File Share connector

The Azure File Share Microsoft 365 Copilot connector integrates Azure File Share content into Microsoft 365, allowing Microsoft 365 Copilot and Microsoft Search experiences to surface relevant files and folders directly in apps like Teams, Outlook, and SharePoint. This article provides troubleshooting information for common errors that you might encounter when you deploy the Azure File Share connector.

## Azure File Share connector troubleshooting

The following table lists common issues and troubleshooting steps.

| Issue | Cause | Resolution |
|-------|--------|------------|
| **Files or folders not appearing in Copilot or Microsoft Search** | The Microsoft Graph Connector Agent account lacks New Technology File System (NTFS) read permissions on some directories. | Make sure that the user account used to mount the Azure File Share and run the Microsoft Graph Connector Agent has read access to all directories and files under the source folder paths. |
| **Connector does not index content beyond a certain size** | The connector indexes files up to 100 MB with up to 4 MB of extracted text. Larger files or oversized text extracts are skipped. | Reduce file size or divide content into smaller documents to ensure indexing. |
| **Some file types are not searchable** | Only Office documents, PDFs, text files, and JSON files are supported. Nontext formats (such as images or videos) are excluded by default. | Convert nontext content to supported formats if necessary. |
| **Users see fewer results than expected** | The connector enforces NTFS access control lists (ACLs), so items not accessible to a specific user don’t appear. | Review NTFS permissions, ensure access alignment with Microsoft Entra ID identities, or adjust access trimming (if appropriate). |
| **Slow crawl performance or long delays between updates** | Crawl performance depends on file size, content type, and network conditions of the environment where Microsoft Graph Connector Agent is deployed. | Review network throughput, examine Microsoft Graph Connector Agent host performance, or reduce volume of low-value content. |
| **Agent authentication issues** | The wrong credentials were used for mounting the file share or configuring the agent. | Verify that the same credentials are used for all three operations: mounting the share, running the Microsoft Graph Connector Agent, and configuring the connector in the admin center. |

## Related content

- [Azure File Share connector overview](azure-file-share-overview.md)
- [Deploy the Azure File Share connector](azure-file-share-deployment.md)
