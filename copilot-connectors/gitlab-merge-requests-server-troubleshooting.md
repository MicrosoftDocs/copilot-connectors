---
title: "GitLab Merge Requests Server connector troubleshooting"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 01/22/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the GitLab Merge Requests Server Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the GitLab Merge Requests Server connector

The GitLab Merge Requests Server Microsoft 365 Copilot connector indexes merge request metadata from GitLab Self‑Managed (Server) so users can discover, summarize, and retrieve MR insights in Microsoft 365. This article provides troubleshooting steps for common issues you might encounter during deployment and operation of the connector.

## GitLab Merge Requests Server connector troubleshooting

The table lists common errors and troubleshooting steps.

| Issue | Cause | Resolution |
|-------|--------|------------|
| **Merge requests not appearing in Microsoft Search or Copilot** | GitLab version is below the required minimum or API access is restricted. | Ensure GitLab Server is version **17.7 or later** and confirm the instance is reachable through the GitLab REST API. Verify that the authentication account has the required access to repositories, issues, merge requests, and wiki pages. |
| **Connector fails during authorization** | OAuth app not configured with correct scopes or redirect URLs. | Confirm that your GitLab OAuth app includes the scopes `read_api`, `read_repository`, and `read_user`. Verify the correct redirect URL based on Microsoft 365 cloud environment. |
| **ACL mapping inconsistencies** | GitLab identity attributes don't map cleanly to Microsoft Entra ID. | Update identity mapping to use email, login, or name. If matching fails, apply regex transformations to normalize input values. |
| **Missing or incomplete merge request details** | Some merge request metadata types aren't indexed by design. | The connector doesn't index code diffs, file‑level changes, inline comments, commit messages, or commit‑level metadata. This issue is expected behavior. |
| **Permission errors when accessing MRs from public projects** | Security restrictions for GitLab Server connectors. | Access to merge requests in **public projects with member‑restricted visibility** is limited to users with the **Reporter** role or higher. |
| **Planner role assignment issues** | Planner role is deprecated for GitLab Server connectors. | Assign **Reporter** or higher. Planner role support was removed due to stability concerns. |
| **Slow or incomplete ingestion** | Rate limits or insufficient API throughput. | Disable or raise rate limits in GitLab: uncheck authenticated API limits, set Users API rate limit high (for example, 100000), and set Groups, Projects, and Members API limits to **0**. Confirm that the Microsoft Graph connector agent version is **3.1.8.0 or later**. |
| **Connector cannot reach GitLab Server** | Network or firewall restrictions. | Confirm that the machine running the Microsoft Graph connector agent can reach your GitLab Server instance over the network. Validate outbound connectivity and any required proxy configurations. |

## Related content

- [GitLab Merge Requests Server connector overview](gitlab-merge-requests-server-overview.md)  
- [Deploy the GitLab Merge Requests Server connector](gitlab-merge-requests-server-deployment.md)
