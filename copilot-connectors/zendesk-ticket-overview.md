---
title: "Zendesk Ticket Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: anggao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 01/14/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Zendesk Ticket Microsoft 365 Copilot connector."
---

# Zendesk Ticket Microsoft 365 Copilot connector overview

The Zendesk Ticket Microsoft 365 Copilot connector allows your organization to index tickets from Zendesk. After you configure the connector, users can search for these tickets from Zendesk in Microsoft 365 Copilot and from any Microsoft Search client. The Zendesk ticket system is a centralized customer support platform that turns customer inquiries from multiple channels into tickets. Teams can track, prioritize, assign, and resolve tickets efficiently with automation, workflow tools, and contextual customer data—helping support teams streamline communication, improve response times, and deliver consistent service at scale.

## Why use the Zendesk Ticket connector to index your data?

The Zendesk Ticket connector enables organizations to:
- Search Zendesk tickets directly in Microsoft 365 Copilot and Microsoft Search.
- Sync users, organizations, and groups for access control.
- Respect Zendesk access permissions in search results.
- Support both incremental (every 15 minutes) and full crawls (daily).

Common use cases for the connector include:
- Quickly locate Zendesk tickets without leaving Microsoft 365.
- Summarize ticket details in Copilot for reporting or decision-making.
- Ask Copilot questions related to project tracking, support queries, or task execution.

## Build agents with the Zendesk Ticket connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that agent builders can use to help their users retrieve information from Zendesk Ticket:
- Find the issue with the mobile app not loading.
- Check the status of ticket CP-2234.
- Summarize CP-1234.

## Zendesk Ticket connector capabilities and limitations

The Zendesk Ticket connector has the following capabilities:

- Performs natural language queries to find tickets.
- Retrieves ticket details for reporting and analysis.
- Respects Zendesk access permissions in search results.
- Syncs users, organizations, and groups for access control.
- Supports incremental and full crawls for up-to-date indexing.

The connector has the following limitations:

- Doesn't index attachments.

## Data types indexed from Zendesk Ticket

The connector indexes Zendesk ticket data, including ticket metadata, status, assignee, requester, priority, and other properties. Indexed content is surfaced in Copilot and Microsoft Search results, allowing users to find and interact with ticket information directly within Microsoft 365.

## Permissions model and access control

Admins can configure access permissions so that only users with appropriate Zendesk permissions can view indexed ticket data in Copilot and Microsoft Search. The connector supports mapping Zendesk identities to Microsoft Entra ID, ensuring secure and accurate access control.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Zendesk Ticket connector](zendesk-ticket-deployment.md)
