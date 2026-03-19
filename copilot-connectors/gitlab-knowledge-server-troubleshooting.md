---
title: "GitLab Knowledge Server Microsoft 365 Copilot connector troubleshooting"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 01/26/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the GitLab Knowledge Server Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the GitLab Knowledge Server Microsoft 365 Copilot connector

The GitLab Knowledge Server connector allows Microsoft 365 Copilot and Microsoft Search to index knowledge content stored in your GitLab self‑managed instance. This article provides troubleshooting guidance for common errors you might encounter during connector deployment, configuration, or ingestion.

## Authentication failures

If authentication fails during connector authorization:

- Confirm that the client ID and client secret were generated from the correct GitLab OAuth application.
- Verify that the required scopes are granted: `read_api`, `read_repository`, and `read_user`.
- Make sure the redirect URL matches the environment:
  - Microsoft 365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`
  - Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
- Make sure that the authentication account has access to repositories, wikis, and documentation files.

## Content not indexing

If ingestion begins but no items appear:

- Verify that the GitLab instance is reachable from the server running the Microsoft Graph connector agent.
- Make sure that API rate limits in GitLab aren't blocking ingestion. Disable or raise the User, IP, or API request limits.
- Confirm that the GitLab version is 17.7 or later.
- Check that the agent version is 3.1.8.0 or later.
- Confirm that the connector account has repository and wiki access for all relevant projects.

## Slow ingestion or crawl delays

If ingestion completes slowly:

- Increase GitLab rate-limiting thresholds for User, IP, Files API, Deprecated API, Users API, Groups API, Projects API, and Members API.
- For large environments, use the following guidance:
  - Up to 100,000 items: 9,000 requests/hour
  - 100,000–1,000,000 items: 15,000 requests/hour
  - More than 1,000,000 items: 15,000 requests/hour; ingestion might take 1–2 weeks depending on system load

## Permission mismatches

If users see search results they shouldn't have access to, or don't see results they should have access to:

- Confirm that identity mapping is configured correctly. Supported mapping attributes include email, login, and name.
- If user attributes don't match between GitLab and Microsoft Entra ID, configure regular expressions (regex) to transform values.
- Check whether email visibility settings or mixed domains in GitLab are preventing accurate mapping.
- Ensure that the selected access model (**Only people with access to this data source** or **Everyone**) matches your organization’s requirements.

## Merge request or role‑based access issues

If users experience permission problems with merge requests or certain GitLab roles:

- Access to merge requests for public projects restricted to project members is enforced at the Reporter role or higher.
- The Planner role is deprecated for stability reasons. Assign the Reporter role or a higher role to users who require access.

## Microsoft Graph connector agent issues

If the agent fails to connect or reports errors:

- Verify that the agent host computer can reach the GitLab Server instance over the required ports.
- Verify that the agent has sufficient memory and CPU capacity.
- Restart the agent service and attempt ingestion again.

## Related content

- [GitLab Knowledge Server connector overview](gitlab-knowledge-server-overview.md)
- [Deploy the GitLab Knowledge Server connector](gitlab-knowledge-server-deployment.md)