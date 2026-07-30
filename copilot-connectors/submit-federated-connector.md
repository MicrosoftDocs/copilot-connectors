---
title: "Submit a federated connector"
description: "Learn how to submit a remote MCP server as a federated Microsoft 365 Copilot connector, including requirements, metadata, and review expectations."
ms.author: danielabo
author: danipocket
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: microsoft-365-copilot-connectors
ms.date: 06/03/2026
ms.localizationpriority: Medium
---

# Submit a federated connector

The federated Microsoft 365 Copilot Connector program allows partners to submit a remote Model Context Protocol (MCP) server to Microsoft for inclusion in the connectors gallery for Microsoft 365 Copilot tenants.

After Microsoft approves your MCP server and adds it to the gallery as a federated connector, tenant admins can review and approve the connector for their organization. After an admin approves it, Microsoft 365 Copilot connects to your remote MCP server through a public HTTPS endpoint and surfaces your content in Copilot experiences, such as the Copilot app and the Researcher agent.

This article explains submission prerequisites, requirements, required artifacts, and what to expect during review and onboarding of a federated connector. For legal terms, see [Microsoft Product Terms](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/MCA).

> [!NOTE]
> Microsoft enables only tools that perform search and fetch operations. Each tool must include the `readOnlyHint` annotation to be enabled in the connectors gallery in the Microsoft 365 admin center.

## Gallery requirements

All submitted federated connectors must meet the following requirements:

- **Security and privacy:** Meets Microsoft security and privacy standards.
- **Tool metadata:** Each tool has a clear title and includes the required `readOnlyHint` annotation.
- **Authentication:** Authenticated scenarios use OAuth 2.0.
- **Documentation quality:** Setup, usage, and support guidance are clear and complete.

Microsoft reviews all submissions for quality, usefulness, and safety before listing. Building an MCP server doesn't guarantee that it will be included in the gallery.

## Submitter responsibilities

When you submit a federated connector, you agree to:

- Maintain connector functionality and security over time.
- Respond promptly to security issues.
- Provide accurate metadata, assets, and documentation.
- Support Microsoft validation and ring-based rollout activities.

## Required metadata and assets

Provide the following artifacts with your submission.

| Field | Requirement |
|------|------------|
| **MCP server URL** | Public HTTPS endpoint for your MCP server. For example: `https://mcp.contoso.com/mcp`. |
| **Connector display name** | User-facing connector name. |
| **Short description** | Public description, 80 characters or fewer. |
| **Synonyms** | Up to 10 comma-separated keywords users might search for. Avoid generic or competitor names. |
| **Logo (color.png)** | 192 x 192 pixel full-color PNG. |
| **Logo (outline.png)** | 32 x 32 pixel white-on-transparent PNG. |
| **OAuth credentials** | OAuth reference ID for your Microsoft registration. For setup information, see [OAuth 2.0](set-up-custom-federated-connectors.md#oauth-20). |
| **Tool list** | Complete list of tools with human-readable names and confirmation that each tool includes the `readOnlyHint` annotation. |
| **Documentation and support** | Links to product documentation, privacy policy, and support channel. |
| **Test credentials** | Test account details and step-by-step setup instructions for reviewers. |
| **Sample prompts** | At least three prompts with expected responses that demonstrate connector capabilities. |

## Review and onboarding process

Microsoft accepts submissions on a rolling basis. Review time varies based on submission volume and completeness of provided artifacts.

After you submit a federated connector:

- Microsoft validates the submitted metadata, assets, and technical requirements.
- Microsoft integrates the connector and coordinates validation via email.
- Microsoft proceeds with release discussions and ring-based rollout planning.
- After Microsoft approves the connector and publishes it in the gallery, each customer organization's admin must approve the partner federated connector before it's enabled for that organization.

Microsoft doesn't provide notifications for every intermediate status change. For status questions, contact your Microsoft representative.

## Submit your connector

To submit your connector, complete the [Federated Copilot connector submission form](https://aka.ms/FccSubmissionForm).

For any questions related to submitting your remote MCP server, [send us an email](mailto:submit-fcc@microsoft.com).

## Related content

- [Microsoft Product Terms](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/MCA)
- [Federated connectors overview](federated-connectors-overview.md)
- [Set up custom federated connectors](set-up-custom-federated-connectors.md)
- [Create OAuth credentials](set-up-custom-federated-connectors.md#oauth-20)
