---
title: Federated connectors overview
description: Get an overview of MCP-based Microsoft 365 Copilot federated connectors.
#customer intent: As an admin, I want to learn about federated connectors and whether and how to enable them in the Microsoft 365 admin center.
author: danipocket
ms.author: danielabo
manager: calvind
ms.reviewer: mansipakhale
ms.service: microsoft-365-copilot-connectors
ms.date: 08/27/2026
ms.topic: overview
ms.localizationpriority: medium
ms.audience: Admin
---
 
# Federated connectors overview

[!INCLUDE [wiqd-beta-disclaimer](includes/wiqd-beta-disclaimer.md)]
 
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
- Cowork
 
## Federated connectors in the Connectors Gallery
 
Microsoft provides a set of federated connectors in the Connectors Gallery. These connectors can be Microsoft-published or submitted by partners and approved by Microsoft.

Currently, federated connectors are available for the following data sources, organized by category:

| Category | Data sources |
| --- | --- |
| Accounting and finance | Aiwyn Tax, Blockscout, CB Insights, Clarity AI, Daloopa, FactSet, Fitch Solutions, Klardaten DATEV-Connector, LSEG, Mercury, Money Forward, Moody's, Morningstar, PitchBook, S&P Global, Xero, Zacks |
| Collaboration and communication | TeamsMaestro |
| Content management systems | Templafy |
| Customer relationship management | Clarify, HubSpot, Intercom |
| Data visualization | Forrester, IDC, Infor Nexus Digital Assistant, Polar Analytics, Pulse by PassBy, S&P Global Energy, Sight Machine, Statista, Wolfram |
| Design | Canva, Cloudinary, Excalidraw |
| Developer tools | Context7, Enosix, GoDaddy, GraphOS MCP Tools, Hugging Face, Jam, pg-aiguide |
| Education | Article Galaxy, Autodesk Product Help, Microsoft Learn |
| Files and documents | Box |
| Health and life sciences | bioRxiv, ClinicalTrials.gov Explorer (by BLEN), CMS Coverage, Consensus, MedlinePlus, NPI Registry, NyquistAI, OpenTargets, PopHIVE, PubMed, RxNorm |
| Human resources and recruiting | Dice, Gusto, ZipRecruiter |
| IT service management tools | Azure DevOps, Cloudflare, Malwarebytes |
| Legal | BoardWise, Descrybe Legal Engine, Everlaw, Harvey, Harvey AU, Harvey EU, iManage Work, Legal Data Hunter |
| Nonprofit | Kindora Funder Discovery |
| Others | Granted, Tavily |
| Productivity | Autodesk, DeepL MCP, Fellow.ai, Google Calendar, Google Contacts, Granola, Mem, Notion, Taskrabbit Booking Assistance |
| Project management | Dotted, Flow Studio Cowork, Linear, Quire |
| Sales | Adobe Journey Optimizer, Ahrefs, Crossbeam, Customer.io, Grain, HG Insights, MailerLite, Sprouts Data Intelligence |

ISVs use a single connector manifest and single publishing pipeline for all connector types. For more information, see [ISV success guidance](/partner-center/membership/isv-success).

The following image shows federated connectors in the **Your connections** list in the Microsoft 365 admin center.
 
:::image type="content" source="media/federated-connectors/your-connections-tab.png" alt-text="Screenshot of the Your connections tab in the admin center with federated connectors appearing in the list." lightbox="media/federated-connectors/your-connections-tab.png":::

> [!IMPORTANT]
> Admins control whether default federated connectors are available to their organization from the **Settings** tab in Agent 365, by using the [Allowed agent types](/microsoft-365/admin/manage/agent-settings#allowed-agent-types). When the Microsoft-published and third-party-published options are deselected, federated connectors aren't enabled by default in the tenant, including connectors released in the future, and the admin enables each connector individually. This setting replaces the tenant-wide PowerShell toggle. Tenants that previously used the cmdlet receive a Message Center post asking them to reapply the choice in the UX within a limited window, after which the cmdlet state is no longer honored. For more information, see [Manage federated connectors](manage-federated-connectors.md).

## Admin experience and controls
 
Microsoft-published federated connectors are enabled by default for a tenant unless admins disable them. Admins must approve partner federated connectors before enabling them for the organization. Admins can manage federated Copilot connectors in the Microsoft 365 admin center by choosing **Copilot connectors** > **Your connections**.

Administrators can manage Microsoft 365 Copilot connectors, synchronized connectors, federated connectors, and supported Cowork plugins from a single location: Copilot connectors > Your connections.
 
Admins can:
 
- View federated connectors that are available in the tenant on the **Your connections** tab, including Microsoft-published connectors and partner connectors that Microsoft approved and the admin enabled.
- Enable or disable connectors at the tenant level.
- Limit availability to specific Microsoft Entra ID groups by choosing **Add staging** in the **Staged Rollout** column.
- Bulk disable all federated connectors by using [Allowed Agent Type](/microsoft-365/admin/manage/agent-settings#allowed-agent-types), and selectively enable specific federated connectors in the Microsoft 365 admin center based on organizational policies and readiness. For more information, see [Manage federated connectors](manage-federated-connectors.md).
- Manage federated connectors from the Agent tab in the Microsoft 365 admin center portal apart from the **Copilot connectors** > **Your connections** section.
 
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


### Does the **Allowed plugins type** setting apply to federated connectors released in the future?
Yes. The setting applies to connectors released after you configure it. If you deselect the **Microsoft-published** and **third-party-published** options, users can't access new connectors until an admin enables them. If you select those options, new connectors follow the default rollout behavior.


### How do ISVs publish connectors?

ISVs use a single connector manifest and single publishing pipeline for all connector types.

 
## Related content
 
- [Manage federated connectors](manage-federated-connectors.md)
- [Microsoft 365 Copilot connectors overview](overview.md)
