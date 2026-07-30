---
title: Federated connectors overview
description: Get an overview of MCP-based Microsoft 365 Copilot federated connectors.
#customer intent: As an admin, I want to learn about federated connectors and whether and how to enable them in the Microsoft 365 admin center.
author: Lauragra
ms.author: lauragra
manager: calvind
ms.reviewer: mansipakhale
ms.service: microsoft-365-copilot-connectors
ms.date: 06/22/2026
ms.topic: overview
ms.localizationpriority: medium
ms.audience: Admin
---
 
# Federated connectors overview
 
Microsoft 365 Copilot supports federated Copilot connectors to enable organizations to connect their data to Copilot by using Model Context Protocol (MCP). Federated connectors use MCP to access data in real time, so Copilot can retrieve up-to-date information directly from external systems. This approach makes it easy to integrate live, dynamic data sources while keeping the data in its original location.

Federated connectors can be Microsoft-published or submitted by partners to Microsoft for approval and publication in the Connectors Gallery.

By using federated connectors, organizations can extend Copilot to work seamlessly with their existing tools and data to unlock more relevant and timely insights across their workflows.
 
## What are federated connectors?
 
Federated Copilot connectors:
 
- Use Model Context Protocol (MCP) to fetch data in real time.
- Access data using the user's identity and permissions.
- Don't index external data into Microsoft 365.
- Are managed and governed by admins in the Microsoft 365 admin center.
- Can be Microsoft-published or partner-submitted and Microsoft-approved.
- Are read-only and can be audited in Microsoft Purview.
 
## Supported Copilot experiences
 
Microsoft 365 Copilot currently supports federated Copilot connectors in the following experiences:

- Microsoft 365 Copilot Chat
- Copilot in Excel
- Researcher agent
 
## Federated connectors in the Connectors Gallery
 
Microsoft provides a set of federated connectors in the Connectors Gallery. These connectors can be Microsoft-published or submitted by partners and approved by Microsoft.

Currently, federated connectors are available for the following data sources, organized by category:

| Category | Data sources |
|---|---|
| Productivity | Autodesk, Excalidraw, Fellow.ai, Google Calendar, Google Contacts, Grain, Granola, Mem, Notion, Taskrabbit Booking Assistance |
| Sales and marketing | Clarify, Customer.io, HG Insights, HubSpot, Intercom, MailerLite, Polar Analytics, Sprouts Data Intelligence |
| Design | Canva, Cloudinary |
| Development tools | Context7, Enosix, GoDaddy, GraphOS MCP Tools, Hugging Face, Jam, Linear, pg-aiguide |
| Financial Services | Aiwyn Tax, Blockscout, CB Insights, Clarity AI, Daloopa, FactSet, Fitch Solutions, LSEG, Moody's, Morningstar, PitchBook, S&P Global |
| Data & Analytics | Forrester, Infor Nexus Digital Assistant, Pulse by Passby, Sight Machine, Wolfram |
| Human Resources & Recruiting | Dice, ZipRecruiter |
| Legal | BoardWise, Harvey, Legal Data Hunter |
| Nonprofit | Kindora Funder Discovery |
| Security & IT | Malwarebytes |
| Education | Article Galaxy, Microsoft Learn |
| Health & Life Sciences | NyquistAI, OpenTargets |
 
Partners who want to make a federated connector available in the gallery can submit their remote MCP server to Microsoft for review. For more information, see [Submit a federated connector](submit-federated-connector.md). For any questions related to submitting your remote MCP server, [send us an email](mailto:submit-fcc@microsoft.com).

The following image shows federated connectors in the **Your connections** list in the Microsoft 365 admin center.
 
:::image type="content" source="media/federated-connectors/your-connections-tab.png" alt-text="Screenshot of the Your connections tab in the admin center with federated connectors appearing in the list." lightbox="media/federated-connectors/your-connections-tab.png":::

> [!IMPORTANT]
> Admins can enable and disable all default federated connectors in their organization by using a tenant-wide toggle. When admins set the toggle to **disable**, federated connectors aren't enabled by default in the tenant. The admin must enable each connector individually. For more information, see [Manage federated connectors](manage-federated-connectors.md).

## Admin experience and controls
 
Microsoft-published federated connectors are enabled by default for a tenant unless admins disable them. Admins must approve partner federated connectors before enabling them for the organization. Admins can manage federated Copilot connectors in the Microsoft 365 admin center by choosing **Copilot connectors** > **Your connections**.
 
Admins can:
 
- View federated connectors that are available in the tenant on the **Your Connections** tab, including Microsoft-published connectors and partner connectors that Microsoft approved and the admin enabled.
- Enable or disable connectors at the tenant level.
- Limit availability to specific Microsoft Entra ID groups by choosing **Add staging** in the **Staged Rollout** column.
- Bulk disable all federated connectors by using PowerShell cmdlets, and selectively enable specific federated connectors in the Microsoft 365 admin center based on organizational policies and readiness. For more information, see [Manage federated connectors](manage-federated-connectors.md).
 
> [!NOTE]
> **Admin review window**
>
> When a Microsoft-published federated connector first appears in the admin center, it's available **only to admins for seven calendar days** before it's available to users. During this window, admins can:
>
> 1. Review the connector.
> 1. Disable it if it doesn't meet organizational requirements.
> 1. Configure staged rollout.
>
> If a connector is disabled during this window, it isn't made available to users.
 
The following image shows the connector pane for the HubSpot federated connector.
 
:::image type="content" source="media/federated-connectors/hubspot-connector.png" alt-text="Screenshot of the HubSpot connector in the admin center with Staged rollout and Enable/disable data source highlighted." lightbox="media/federated-connectors/hubspot-connector.png":::
 
## How to connect and use federated Copilot connectors
 
When an admin enables a federated connector:
 
- Users can discover the data source in the **Sources** menu in the Researcher agent, in deep research mode in Microsoft 365 Copilot chat, and in Copilot Chat where available.
- Users authenticate by using their own credentials when prompted to connect to the data sources.
- Copilot only accesses data the user already has permission to see.
- Users can disable the data source at any time by turning off the source in Researcher or by managing the source in Copilot Chat settings.

### Connect to federated connectors in Copilot Chat

Where Copilot Chat is available for users, they can connect federated data sources directly from chat settings:

1. Open Microsoft 365 Copilot Chat.
1. Select the ellipsis (**...**) menu, and then select **Settings**.
    :::image type="content" source="media/federated-connectors/copilot-chat-settings.png" alt-text="Screenshot of the settings option in Copilot Chat." lightbox="media/federated-connectors/copilot-chat-settings.png":::
1. In the settings dialog, select **Sources** in the left pane.
1. Find the external data source you want to use, select **Connect**, and complete authentication.
1. Enter your prompt directly in Copilot Chat.
 
> [!NOTE]
> No data is indexed into Microsoft 365. Responses are fetched dynamically from the data source via MCP.
 
The following image shows how the user accesses federated connector data sources in Researcher.
 
:::image type="content" source="media/federated-connectors/researcher-data-source.png" alt-text="Screenshot of federated connector data sources in Researcher." lightbox="media/federated-connectors/researcher-data-source.png":::

## Dynamic tooling through MCP

Dynamic tooling enables Microsoft 365 Copilot to retrieve information from connected systems at runtime based on a user's request.

The MCP server associated with the federated connector determines tool availability. When appropriate, Microsoft 365 Copilot dynamically selects relevant tools to gather the information needed to answer a request.

The authenticated user's identity and permissions in the source system govern tool access. Users can only access information they're authorized to view.

Examples of dynamic tooling include:

- Searching knowledge repositories
- Looking up records in line-of-business applications
- Retrieving project or operational status information
- Querying customer, product, or support information
- Accessing specialized search capabilities exposed by a source system

Like all federated connector interactions, Microsoft 365 Copilot fetches information through dynamic tooling in real time and doesn't index it into Microsoft 365.
 
## Security and compliance
 
The following security and compliance features apply to federated connectors:
 
- Federated connectors don't copy or store data in Microsoft 365.
- All permissions are enforced by the source system. Users only see content they have access to in the original data source.
- OAuth 2.0 and encrypted communication ensure secure access and authentication.
 
## FAQs
 
### How are federated Copilot connectors different from synced Copilot connectors?

Synced Copilot connectors index data into Microsoft Graph. Federated Copilot connectors fetch content live; no indexing takes place.
 
Synced connectors are supported at an organization level; federated connectors are federated at the user level. User credentials, rather than admin credentials, are required to connect to any data source.
 
### Can I use both federated and synced connectors in my tenant?
 
Both federated and synced connectors can coexist in your tenant and appear together in your connector list.

### Do I need to rerun the CLI cmdlet when Microsoft releases new federated connectors?

The CLI setting automatically applies to future federated connectors. If you disable the toggle, new connectors appear in a disabled state. If you enable the toggle, new connectors follow the default rollout behavior.
 
## Related content
 
- [Manage federated connectors](manage-federated-connectors.md)
- [Microsoft 365 Copilot connectors overview](overview.md)
