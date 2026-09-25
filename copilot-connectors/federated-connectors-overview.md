---
title: Federated connectors overview
description: Learn how MCP-based Microsoft 365 Copilot federated connectors retrieve data and use write, update, and delete actions.
#customer intent: As an admin, I want to learn about federated connectors, including read and write capabilities, and how to manage them in the Microsoft 365 admin center.
author: danipocket
ms.author: danielabo
manager: calvind
ms.reviewer: mansipakhale
ms.date: 09/25/2026
ms.topic: overview
ms.localizationpriority: medium
ms.audience: Admin
---

# Federated connectors overview

[!INCLUDE [wiqd-beta-disclaimer](includes/wiqd-beta-disclaimer.md)]

Microsoft 365 Copilot supports federated Copilot connectors to enable organizations to connect their data to Copilot by using Model Context Protocol (MCP). Federated connectors use MCP to access data in real time, so Copilot can retrieve up-to-date information directly from external systems. This approach makes it easy to integrate live, dynamic data sources while keeping the data in its original location.

Where a connector provides the tools, Copilot can also create, update, or delete data in the connected system on the user's behalf.

Federated connectors can be Microsoft-published or submitted by partners to Microsoft for approval and publication in the Connectors Gallery.

By using federated connectors, organizations can extend Copilot to work seamlessly with their existing tools and data to unlock more relevant and timely insights across their workflows.

> [!NOTE]
> Support for write, update, and delete actions begins rolling out in early October 2026. For availability by Copilot experience, see [Write, update, and delete actions](#write-update-and-delete-actions-coming-soon).

## What are federated connectors?

Federated Copilot connectors:

- Use Model Context Protocol (MCP) to fetch data in real time.
- Access data using the user's identity and permissions.
- Don't index external data into Microsoft 365.
- Are managed and governed by admins in the Microsoft 365 admin center.
- Can be Microsoft-published or partner-submitted and Microsoft-approved.
- Can read data and, where a connector provides the tools, create, update, or delete data with the user's approval. Admins can audit activity in Microsoft Purview.

## Supported Copilot experiences

Microsoft 365 Copilot supports federated Copilot connectors in the following experiences:

- Microsoft 365 Copilot Chat
- Agents
- Cowork
- Copilot in Word, Excel, PowerPoint, and Outlook
- Researcher agent

The Researcher agent doesn't support write, update, or delete actions. Federated Copilot connectors remain read-only in this experience.

## Federated connectors in the Connectors Gallery

Microsoft provides a set of federated connectors in the Connectors Gallery. These connectors can be Microsoft-published or submitted by partners and approved by Microsoft.

Currently, federated connectors are available for the following data sources, organized by category:

| Category | Data sources |
| --- | --- |
| Accounting and finance | Aiwyn Tax, CB Insights, Clarity AI, DiligenceSquared, FactSet, FinancialReports, Fiscal.ai, Klardaten DATEV-Connector, LSEG, Mercury, Money Forward, Moody's, Morningstar, MT Newswires, PrivCo, Quartr, Syrto, Xero, Zacks, Zoho Books |
| Collaboration | Gmail, Linear, Miro, TeamsMaestro, Trello |
| Content management | PandaDoc, Templafy, TextMine |
| CRM | Clarify, HubSpot |
| Data analytics | ARC Advisory AI, Ask Rystad, AskPolly, Contentsquare, DecisionPoint, EIU, IDC, Mixpanel, MoSPI, Polar Analytics, Pulse by PassBy, Resilinc, S&P Global Energy, Statista, Wolfram |
| Site design | Canva, Cloudinary, Excalidraw, Mobbin, Webflow |
| IT management tools | Apify, Clerk, Context7, Enosix, GoDaddy, GraphOS MCP Tools, Hugging Face, Jam, pg-aiguide |
| Training and tutorial | Article Galaxy, Articulate, Articulate EU, Autodesk Product Help, Microsoft Learn, Padlet, Scite, Siemens |
| Files and documents | Box |
| Health and life sciences | BioRender, Consensus, Cortellis Regulatory Intelligence, NyquistAI, PopHIVE, SciLeads, Smarts.bio |
| Legal + HR and recruiting | BoardWise, Courtroom5, Descrybe Legal Engine, Dice, DirectCase Legal Search, Everlaw, Gusto, Harvey, Harvey AU, Harvey EU, iManage Work, Lawstronaut, Legal Data Hunter, Relativity, ZipRecruiter |
| IT service management tools | Cloudflare, Malwarebytes |
| Reference | AllTrails, Fibre2Fashion, Granted, Kindora Funder Discovery, Melon, SiteTrax.io, Tavily |
| Productivity | DeepL MCP, Fellow.ai, Fireflies, Goodnotes, Google Calendar, Google Contacts, Granola, Mem, Memoket, Notion, Taskrabbit Booking Assistance |
| Project management | Asana, awork, Dotted, Flow Studio Cowork, Make, monday.com, Quire |
| Sales and marketing | Adobe Journey Optimizer, Ahrefs, Crossbeam, Customer.io, Grain, HG Insights, Local Falcon, MailerLite |

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

Write, update, and delete tools are part of the connector and aren't enabled separately.

The following image shows the connector pane for the HubSpot federated connector.

:::image type="content" source="media/federated-connectors/hubspot-connector.png" alt-text="Screenshot of the HubSpot connector in the admin center with Staged rollout and Enable/disable data source highlighted." lightbox="media/federated-connectors/hubspot-connector.png":::

### View a connector's tools in the admin center (Coming soon)

> [!NOTE]
> Viewing tools in the admin center isn't available for all connectors. If you encounter issues, sign in to Microsoft 365 Copilot with your user account, go to **Settings** > **Sources**, and select the connector. Then [expand **Write/Delete tools** to review individual tools and their approval settings](#review-individual-tool-permissions).

For connectors that support this feature, the details page in the Microsoft 365 admin center includes a **Tools** section that lists the tools available to users in the organization, including tools that can modify or delete data. To view the tools:

1. In the Microsoft 365 admin center, go to **Copilot connectors** > **Your connections** and select the federated connector.

    :::image type="content" source="media/federated-connectors/admin-center-connector-details.png" alt-text="Screenshot of the Zava HR connector details pane in the Microsoft 365 admin center, showing the Tools section and Sign in button." lightbox="media/federated-connectors/admin-center-connector-details.png":::

1. On the connector's details page, go to the **Tools** section and sign in to the third-party service.

    :::image type="content" source="media/federated-connectors/admin-center-tools-signed-in.png" alt-text="Screenshot of a successful sign-in to Zava HR, with Read/Search and Write/Delete tool counts and the All tools button." lightbox="media/federated-connectors/admin-center-tools-signed-in.png":::

1. Select **All tools**, and then review the list to identify tools that can create, update, or delete data.

    :::image type="content" source="media/federated-connectors/admin-center-available-tools.png" alt-text="Screenshot of the Zava HR Available tools list in the Microsoft 365 admin center, showing tools labeled Read, Write, or Delete." lightbox="media/federated-connectors/admin-center-available-tools.png":::

> [!NOTE]
> The tool list reflects the permissions of the account used to sign in. Sign in by using an account that has a high level of access to the connector so you see the comprehensive list of tools.

Before enabling or continuing to use a connector that exposes write, update, or delete tools, review the connector's capabilities, privacy terms, and third-party agreements against your organization's security, compliance, and acceptable-use requirements. Update user and help-desk guidance so users understand that actions are performed using their own permissions in the third-party service.

## How to connect and use federated Copilot connectors

When an admin enables a federated connector:

- Users can discover the data source in the **Sources** menu in the Researcher agent, in deep research mode in Microsoft 365 Copilot chat, and in Copilot Chat where available.
- Users authenticate by using their own credentials when prompted to connect to the data sources.
- Copilot only accesses data the user already has permission to see and makes changes the user is already permitted to make.
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

Dynamic tooling enables Microsoft 365 Copilot to retrieve information from connected systems and take actions in them at runtime based on a user's request.

The MCP server associated with the federated connector determines tool availability. When appropriate, Microsoft 365 Copilot dynamically selects relevant tools to retrieve information or perform an action.

The authenticated user's identity and permissions in the source system govern tool access. Users can only access information they're authorized to view and change data they're authorized to modify.

Tools that create, update, or delete data require user approval. For confirmation options and tool permissions, see [Write, update, and delete actions](#write-update-and-delete-actions-coming-soon).

Examples of read operations through dynamic tooling include:

- Searching knowledge repositories
- Looking up records in line-of-business applications
- Retrieving project or operational status
- Querying customer, product, or support information
- Accessing specialized search capabilities exposed by a source system

Dynamic tooling doesn't index external data into Microsoft 365.

## Write, update, and delete actions (Coming soon)

With federated connectors, users can do more than retrieve information. When a connector provides the appropriate tools, users can ask Microsoft 365 Copilot to create, update, or delete information in a connected third-party system on their behalf. Users can complete work without leaving Copilot. For example, a user can turn an escalation email into an issue in a project-tracking tool, update a record in a customer relationship management (CRM) system, or add a comment to a ticket directly from Copilot Chat.

Write, update, and delete actions follow the same federated connector model as read tools:

- Actions run in the third-party service on behalf of the user and are limited by that user's permissions. Copilot can change only what the user is already permitted to change in the source system.
- No data is indexed into Microsoft 365. Copilot sends the connector the information it needs to complete the action and returns the outcome to the user.
- Tools that create, update, or delete data initially require the user's explicit approval. Users can choose whether Copilot asks again for that tool, as described in [Confirm an action](#confirm-an-action). Actions that the user declines aren't performed.
- The actions available through a connector depend on the tools exposed by the connector publisher. Publishers can add or change tools over time.

### Confirm an action

Users must be connected to the third-party service before Copilot can use any authenticated capabilities that the connector provides, including tools that create, update, or delete data.

These actions export Customer Data to the connected system to create, update, delete, or otherwise modify data. While an action is awaiting confirmation, nothing is sent to the connected system until the user responds. Read tools don't require confirmation and continue to run as they do today.

The following image shows a collapsed confirmation card for a write action.

:::image type="content" source="media/federated-connectors/write-action-confirmation-collapsed.jpg" alt-text="Screenshot of a collapsed confirmation card in Copilot Chat showing a request to create an issue in Zava." lightbox="media/federated-connectors/write-action-confirmation-collapsed.jpg":::

Users can expand the card to review the action parameters before approving it.

:::image type="content" source="media/federated-connectors/write-action-confirmation-expanded.jpg" alt-text="Screenshot of an expanded confirmation card in Copilot Chat showing the parameters to be sent to Zava." lightbox="media/federated-connectors/write-action-confirmation-expanded.jpg":::

Open the menu next to **Allow once** to choose **Allow for conversation** or **Always allow**.

:::image type="content" source="media/federated-connectors/write-action-approval-options.jpg" alt-text="Screenshot of the Zava confirmation card with Allow once and Cancel buttons and an open menu offering Allow for conversation and Always allow." lightbox="media/federated-connectors/write-action-approval-options.jpg":::

The user chooses one of the following options:

| Option | What happens |
|---|---|
| **Allow once** | Runs the action now. Copilot asks again the next time it wants to use the tool. |
| **Allow for conversation** | Runs the action and doesn't ask again for this tool for the rest of the current conversation. |
| **Always allow** | Runs the action and doesn't ask again for this tool until the user changes the setting or the publisher changes the tool. |
| **Cancel** | Declines the action. Nothing is changed in the connected system. |

**Always allow** and **Allow for conversation** apply to the individual tool, not to the whole connector. Users can decide which tools to allow.

### Manage tool permissions for write, update, and delete

Users can review or reset tool permissions in Copilot by going to **Settings** > **Sources** and selecting the connector. The **Tools** section groups the connector's **Write/Delete tools** separately from its **Read tools**.

:::image type="content" source="media/federated-connectors/tool-permissions-groups.png" alt-text="Screenshot of connector settings showing separate Write/Delete tools and Read tools groups." lightbox="media/federated-connectors/tool-permissions-groups.png":::

Read tools are always allowed and don't require approval.

:::image type="content" source="media/federated-connectors/read-tools-always-allowed.png" alt-text="Screenshot of the Read tools group with a tooltip explaining that read tools can run without asking for approval." lightbox="media/federated-connectors/read-tools-always-allowed.png":::

Write, update, and delete tools default to **Needs approval**, which means Copilot asks for confirmation each time. A user who selected **Always allow** can switch back to **Needs approval** for the entire **Write/Delete tools** group.

:::image type="content" source="media/federated-connectors/write-delete-group-permissions.png" alt-text="Screenshot of the approval settings menu for the entire Write/Delete tools group." lightbox="media/federated-connectors/write-delete-group-permissions.png":::

#### Review individual tool permissions

Expand **Write/Delete tools** to review individual tools and their approval settings.

:::image type="content" source="media/federated-connectors/write-delete-tools-expanded.png" alt-text="Screenshot of the expanded Write/Delete tools group showing individual tools set to Needs approval." lightbox="media/federated-connectors/write-delete-tools-expanded.png":::

The following image shows a tool description in the expanded list.

:::image type="content" source="media/federated-connectors/write-tool-description.png" alt-text="Screenshot of the Add comment tool description in the expanded Write/Delete tools list." lightbox="media/federated-connectors/write-tool-description.png":::

Users can also change approval settings for an individual tool.

:::image type="content" source="media/federated-connectors/write-tool-permission-options.png" alt-text="Screenshot of an individual tool's approval menu with Needs approval and Always allow options." lightbox="media/federated-connectors/write-tool-permission-options.png":::

If a connector publisher adds a new write-capable tool or changes an existing one, the tool is set to **Needs approval** by default. Thus, Copilot will ask for confirmation the next time it wants to use that tool.

## Security and compliance

The following security and compliance features apply to federated connectors:

- Federated connectors don't copy or store data in Microsoft 365.
- The source system enforces all permissions. Users can only access content they're authorized to view and make changes they're authorized to make in the original data source.
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
