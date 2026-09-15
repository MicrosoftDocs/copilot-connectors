---
title: "Troubleshoot issues with the Galileo by The Josh Bersin Company connector"
ms.author: xupzhou
author: xupzhou
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 09/11/2026
ms.localizationpriority: Medium
description: "Troubleshoot common setup, authentication, indexing, citation, and agent issues with the Galileo by The Josh Bersin Company Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Galileo by The Josh Bersin Company connector

This article provides troubleshooting guidance for common issues with the Galileo by The Josh Bersin Company Microsoft 365 Copilot connector and its declarative agents.

Before troubleshooting, confirm that you completed [Set up Galileo by The Josh Bersin Company for connector ingestion](galileo-admin-setup.md) and [deployed the Galileo connector](galileo-deployment.md).

## Common issues

| Symptom | Likely cause | Resolution |
| --- | --- | --- |
| Setup asks for credentials you don't have. | The onboarding package hasn't been delivered, or the secure secret link expired before retrieval. | Contact your Josh Bersin Company contact to issue or reissue the credentials. Credentials are never sent in plain email. |
| Authentication fails when saving the connection. | The client ID was mistyped, or the client secret expired or was revoked. | Reenter both values from the onboarding package. If validation still fails, request a reissued secret. Don't reuse credentials from another integration. |
| The Galileo connection isn't listed when adding knowledge to the agent. | The connector isn't activated for your tenant, or admin center changes are still propagating. | Verify the **Ready** state under **Your connections**, and allow up to 10 minutes after changes. |
| Copilot answers don't cite Galileo. | The user doesn't have a Microsoft 365 Copilot license, is outside the rollout audience, or the initial index is still running. | Confirm the user's license and access-group membership, and then allow approximately two to three hours for the initial index to complete. |
| Users see the agent but get no Galileo results. | The agent is shared more broadly than the connector's rollout audience. | Align both to the same Galileo access group. The connector audience is the superset. |
| Citation links don't open. | Outbound access to the content domain is blocked. | Allow the Josh Bersin Company content domain from your onboarding package through your egress controls. |
| Content appears stale. | The daily refresh is delayed. | Compare item last-modified dates. If content is more than 48 hours older than the expected publication, contact your JBC contact. |

## Related content

- [Galileo by The Josh Bersin Company connector overview](galileo-overview.md)
- [Set up Galileo by The Josh Bersin Company for connector ingestion](galileo-admin-setup.md)
- [Deploy the Galileo by The Josh Bersin Company connector](galileo-deployment.md)
- [Build declarative agents for Galileo by The Josh Bersin Company](galileo-declarative-agents.md)
