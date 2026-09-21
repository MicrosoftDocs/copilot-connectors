---
title: Federated connectors overview
description: Learn how MCP-based Microsoft 365 Copilot federated connectors retrieve data and use write, update, and delete actions.
#customer intent: As an admin, I want to learn about federated connectors, including read and write capabilities, and how to manage them in the Microsoft 365 admin center.
author: Lauragra
ms.author: lauragra
manager: calvind
ms.reviewer: mansipakhale
ms.service: copilot-connectors
ms.date: 09/21/2026
ms.topic: overview
ms.localizationpriority: medium
ms.audience: Admin
---
 
# Federated connectors overview
 
Microsoft 365 Copilot supports federated Copilot connectors to enable organizations to connect their data to Copilot by using Model Context Protocol (MCP). Federated connectors use MCP to access data in real time, so Copilot can retrieve up-to-date information directly from external systems. This approach makes it easy to integrate live, dynamic data sources while keeping the data in its original location.

Where a connector provides the tools, Copilot can also create, update, or delete data in the connected system on the user's behalf.

Federated connectors can be Microsoft-published or submitted by partners to Microsoft for approval and publication in the Connectors Gallery.

By using federated connectors, organizations can extend Copilot to work seamlessly with their existing tools and data to unlock more relevant and timely insights across their workflows.

> [!NOTE]
> Support for write, update, and delete actions will begin rolling out in early October 2026. For availability by Copilot experience, see [Write, update, and delete actions](#write-update-and-delete-actions).
 
## What are federated connectors?
 
Federated Copilot connectors:
 
- Use Model Context Protocol (MCP) to fetch data in real time.
- Access data using the user's identity and permissions.
- Don't index external data into Microsoft 365.
- Are managed and governed by admins in the Microsoft 365 admin center.
- Can be Microsoft-published or partner-submitted and Microsoft-approved.
- Can read data and, where a connector provides the tools, create, update, or delete data with the user's approval. Activity can be audited in Microsoft Purview.
 
## Supported Copilot experiences
 
Microsoft 365 Copilot supports federated Copilot connectors in the following experiences:

- Microsoft 365 Copilot Chat
- Agents
- Cowork
- Copilot in Word, Excel, PowerPoint, and Outlook
- Researcher agent

Support for write, update, and delete actions varies by experience. The Researcher agent remains read-only. For details, see [Supported experiences for write, update, and delete actions](#supported-experiences).
 
## Federated connectors in the Connectors Gallery
 
Microsoft provides a set of federated connectors in the Connectors Gallery. These connectors can be Microsoft-published or submitted by partners and approved by Microsoft.

Currently, federated connectors are available for the following data sources, organized by category:

| Category | Data sources |
|---|---|
| Productivity | Autodesk, Excalidraw, Fellow.ai, Google Calendar, Google Contacts, Grain, Granola, Mem, Notion |
| Sales and marketing | Clarify, Customer.io, HG Insights, HubSpot, Intercom, MailerLite, Polar Analytics, Sprouts Data Intelligence |
| Design | Canva, Cloudinary |
| Development tools | Context7, GoDaddy, GraphOS MCP Tools, Hugging Face, Jam, Linear, pg-aiguide |
| Financial Services | Aiwyn Tax, Blockscout, CB Insights, Clarity AI, Daloopa, FactSet, Fitch Solutions, LSEG, Moody's, Morningstar, PitchBook, S&P Global |
| Data & Analytics | Forrester, Sight Machine, Wolfram |
| Human Resources & Recruiting | Dice, ZipRecruiter |
| Supply Chain & Logistics | Enosix, Infor Nexus Digital Assistant |
| Legal | BoardWise, Harvey, Legal Data Hunter |
| Nonprofit | Kindora Funder Discovery |
| Security & IT | Malwarebytes |
| Commerce & Shopping | Pulse by Passby, Taskrabbit Booking Assistance |
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

Tools that create, update, or delete data require user approval. For confirmation options and tool permissions, see [Write, update, and delete actions](#write-update-and-delete-actions).

Examples of read operations through dynamic tooling include:

- Searching knowledge repositories
- Looking up records in line-of-business applications
- Retrieving project or operational status information
- Querying customer, product, or support information
- Accessing specialized search capabilities exposed by a source system

Dynamic tooling doesn't index external data into Microsoft 365.

## Write, update, and delete actions

Federated connectors aren't limited to retrieving information. When the MCP server behind a connector provides tools that create, update, or delete data, Microsoft 365 Copilot can use those tools to make changes in the connected third-party system on the user's behalf. Users can complete work without leaving Copilot. For example, a user can turn an escalation email into an issue in a project-tracking tool, update a record in a customer relationship management (CRM) system, or add a comment to a ticket directly from Copilot Chat.

Write, update, and delete actions follow the same federated connector model as read tools:

- Actions run in the third-party service on behalf of the signed-in user and are limited by that user's permissions. Copilot can change only what the user is already permitted to change in the source system.
- No data is indexed into Microsoft 365. Copilot sends the connector the information it needs to complete the action and returns the outcome to the user.
- Tools that create, update, or delete data initially require the user's explicit approval. Users can choose whether Copilot asks again for that tool, as described in [Confirm an action](#confirm-an-action). Actions that the user declines aren't performed.
- The actions available through a connector depend on the tools exposed by the connector publisher. Publishers can add or change tools over time.

### Supported experiences

The following table summarizes support for read tools and for tools that create, update, or delete data.

| Copilot experience | Read tools | Write, update, and delete tools |
|---|---|---|
| Microsoft 365 Copilot Chat | Yes | Yes |
| Agents | Yes | Yes |
| Cowork | Yes | Yes |
| Copilot in Word, Excel, PowerPoint, and Outlook | Yes | Coming shortly after the Copilot Chat release |
| Researcher agent | Yes | No (read-only) |

Federated connectors in the Researcher agent remain read-only. Researcher uses a connector's read tools and doesn't offer its write or delete tools.

### Confirm an action

Users must authenticate to the third-party service before Copilot can use any authenticated capabilities that the connector provides, including tools that create, update, or delete data. Federated connectors support user-scoped access and authentication to external systems.

Each tool that creates, updates, or deletes content initially requires user approval. Copilot shows a confirmation card that names the connector and the tool it wants to use. Users can expand the card to review the parameters that will be sent to the third-party service.

These actions export Customer Data to the connected system to create, update, delete, or otherwise modify data. While an action is awaiting confirmation, nothing is sent to the connected system until the user responds. Read tools don't require confirmation and continue to run as they do today.

The following image shows a collapsed confirmation card for a write action.

:::image type="content" source="media/federated-connectors/write-action-confirmation-collapsed.png" alt-text="Screenshot of a collapsed confirmation card in Copilot Chat showing a request to create an issue in Zava." lightbox="media/federated-connectors/write-action-confirmation-collapsed.png":::

Users can expand the card to review the action parameters before approving it.

:::image type="content" source="media/federated-connectors/write-action-confirmation-expanded.png" alt-text="Screenshot of an expanded confirmation card in Copilot Chat showing the parameters to be sent to Zava." lightbox="media/federated-connectors/write-action-confirmation-expanded.png":::

Open the approval menu to choose how long to allow the tool.

:::image type="content" source="media/federated-connectors/write-action-approval-options.png" alt-text="Screenshot of the confirmation card with Allow once, Allow for conversation, Always allow, and Cancel options." lightbox="media/federated-connectors/write-action-approval-options.png":::

The user chooses one of the following options:

| Option | What happens |
|---|---|
| **Allow once** | Runs the action now. Copilot asks again the next time it wants to use the tool. |
| **Allow for conversation** | Runs the action and doesn't ask again for this tool for the rest of the current conversation. |
| **Always allow** | Runs the action and doesn't ask again for this tool until the user changes the setting or the publisher changes the tool. |
| **Cancel** | Declines the action. Nothing is changed in the connected system. |

**Always allow** and **Allow for conversation** apply to the individual tool, not to the whole connector. Users can decide which tools to allow.

### Manage tool permissions

Users can review or reset tool permissions in Copilot by going to **Settings** > **Sources** and selecting the connector. The **Tools** section groups the connector's **Write/Delete tools** separately from its **Read tools**.

:::image type="content" source="media/federated-connectors/tool-permissions-groups.png" alt-text="Screenshot of connector settings showing separate Write/Delete tools and Read tools groups." lightbox="media/federated-connectors/tool-permissions-groups.png":::

Read tools are always allowed and don't require approval.

:::image type="content" source="media/federated-connectors/read-tools-always-allowed.png" alt-text="Screenshot of the Read tools group with a tooltip explaining that read tools can run without asking for approval." lightbox="media/federated-connectors/read-tools-always-allowed.png":::

Write, update, and delete tools default to **Needs approval**, which means Copilot asks for confirmation each time. A user who selected **Always allow** can switch back to **Needs approval** for the entire **Write/Delete tools** group.

:::image type="content" source="media/federated-connectors/write-delete-group-permissions.png" alt-text="Screenshot of the approval settings menu for the entire Write/Delete tools group." lightbox="media/federated-connectors/write-delete-group-permissions.png":::

Expand **Write/Delete tools** to review individual tools and their approval settings.

:::image type="content" source="media/federated-connectors/write-delete-tools-expanded.png" alt-text="Screenshot of the expanded Write/Delete tools group showing individual tools set to Needs approval." lightbox="media/federated-connectors/write-delete-tools-expanded.png":::

The following image shows a tool description in the expanded list.

:::image type="content" source="media/federated-connectors/write-tool-description.png" alt-text="Screenshot of the Add comment tool description in the expanded Write/Delete tools list." lightbox="media/federated-connectors/write-tool-description.png":::

Users can also change approval settings for an individual tool.

:::image type="content" source="media/federated-connectors/write-tool-permission-options.png" alt-text="Screenshot of an individual tool's approval menu with Needs approval and Always allow options." lightbox="media/federated-connectors/write-tool-permission-options.png":::

If a connector publisher adds a new write-capable tool or changes an existing one, the tool is set to **Needs approval**. Copilot asks for confirmation the next time it wants to use that tool.

### View a connector's tools in the admin center

Write, update, and delete tools are part of the connector and aren't enabled separately. The availability controls in [Admin experience and controls](#admin-experience-and-controls) continue to apply. Admins can enable or disable a connector for the tenant and limit it to specific groups. Disabling a connector removes all of its tools. If an already-enabled connector includes tools that create, update, or delete data, those tools are available to Copilot.

Each federated connector's details page in the Microsoft 365 admin center includes a **Tools** section that lists the tools available to users in the organization, including tools that can modify or delete data. To view the tools:

1. In the Microsoft 365 admin center, go to **Copilot connectors** > **Your connections** and select the federated connector.
1. On the connector's details page, go to the **Tools** section and sign in to the third-party service.
1. Review the list of tools and note which tools can create, update, or delete data.

> [!NOTE]
> The tool list reflects the permissions of the account used to sign in. We recommend signing in with an account that has a high level of access to the connector so you can see the complete list of tools.

Before enabling or continuing to use a connector that exposes write, update, or delete tools, review the connector's capabilities, privacy terms, and third-party agreements against your organization's security, compliance, and acceptable-use requirements. Update user and help-desk guidance so users understand that actions are performed using their own permissions in the third-party service.
 
## Security and compliance
 
The following security and compliance features apply to federated connectors:
 
- Federated connectors don't copy or store data in Microsoft 365.
- All permissions are enforced by the source system. Users can only access content they're authorized to view and make changes they're authorized to make in the original data source.
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
