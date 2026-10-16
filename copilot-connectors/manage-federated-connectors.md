---
title: Manage federated connector availability
description: Learn how to control the availability of federated connectors for Microsoft 365 Copilot by using Agent and plugin access, User access, and connector-level settings in the Microsoft 365 admin center.
#customer intent: As an admin, I want to manage federated connector availability in the Microsoft 365 admin center.
author: jasonjoh
ms.author: jasonjoh
manager: calvind
ms.reviewer: mansipakhale
ms.date: 10/15/2026
ms.topic: how-to
ms.localizationpriority: medium
ms.audience: Admin
---

<!-- cSpell:ignore mansipakhale -->

# Manage federated connector availability

Federated connectors for Microsoft 365 Copilot enable users to access information from external data sources directly within their Copilot experience. Microsoft provides default federated connectors that use the Model Context Protocol (MCP) to integrate with popular services and tools. While these connectors enhance Copilot's capabilities by extending its knowledge base, organizations might need to control their availability for security, compliance, or governance reasons.

As an administrator, you manage federated connector availability in the Microsoft 365 admin center. Use Agent and plugin access to allow or block connectors in bulk by publisher type, User access to set which users can use connectors, and connector-level settings to enable, disable, or stage individual connectors.

## Manage federated connector availability for your organization

Agent and plugin access lets you:

- Turn off all connectors of a publisher type (Microsoft, your organization, or external publishers) in a single step.
- Apply that choice automatically to future connectors of that type.
- Selectively turn on specific connectors while the bulk setting stays off.
- Re-select the option to restore default behavior.

## Prerequisites

To manage federated connectors, you need one of the following administrator roles:

- **Global Administrator**
- **Search Administrator**

## Control connector availability with Agent and plugin access

Agent and plugin access controls which types of agents and plugins, including connectors and MCP servers, are available in your organization.

1. In the Microsoft 365 admin center, go to **Agents** > **Settings** > **Agent and plugin access**.
1. Clear the publisher types you want to block:
   - **Allow agents and plugins built by Microsoft**
   - **Allow agents and plugins built by your organization** (custom connectors)
   - **Allow agents and plugins built by external publishers** (partner connectors)
1. Select **Save**.

When you clear an option, existing connectors of that type remain visible to admins in **Copilot connectors** > **Your connections**, but their staged rollout is set to **No users**. Connectors of that type released later aren't available to users. To make a specific connector available, open it in **Your connections** and set its staged rollout to the users or groups you want.

## Limit who can use connectors with User access

**User access** in **Agents** > **Settings** applies to all agents and plugins, including federated connectors delivered as Microsoft 365 app packages.

| Option | Effect on connectors |
|---|---|
| **All users** (default) | Connector-level staging decides who gets each connector. New connectors are available to all users. |
| **Specific users or groups** | Only these users can use any connector. Connector staging can narrow but not widen this population. |
| **No users** | No user can use connectors, regardless of connector-level settings. |

**User access** doesn't turn connectors on or off; it sets the maximum population. A connector whose details pane shows **Everyone** is still unavailable to users excluded by **User access**.

## How settings combine

| Control | Location | What it does for connectors |
|---|---|---|
| **Agent and plugin access** | **Agents** > **Settings** > **Agent and plugin access** | Allows or blocks connectors in bulk by publisher type, including future connectors. Clearing a type sets that type's connectors' staged rollout to **No users**. |
| **User access** | **Agents** > **Settings** > **User access** | Tenant-wide ceiling on who can use any agent or plugin, including MOS connector packages. Options: **All users** (default), **Specific users or groups**, **No users**. |
| **Enable / Disable** | **Copilot** > **Connectors** > **Your connections** | Turns an individual connector on or pauses it without removing configuration. |
| **Staged rollout** | **Copilot** > **Connectors** > **Your connections** > **Staged rollout** | Which users or groups get an individual connector, within the **User access** population. |
| **Tools block / unblock** | **Agents** > **Tools** | Tool-level and connector-level blocking. |
| **Delete** | **Copilot** > **Connectors** > **Your connections** | Permanently removes a custom connector and its configuration. |

A setting you make on an individual connector takes precedence over the bulk **Agent and plugin access** setting. **User access** always applies.

## Verify the changes

Changes can take up to 10 minutes to take effect across Microsoft 365 experiences. Refresh the Microsoft 365 admin center to see updated connector states, including staged rollout. To confirm what users get, check **Agents** > **Settings** > **Agent and plugin access**, **Agents** > **Settings** > **User access**, and the connector's **Staged rollout** in **Your connections**, then sign in as a test user and check **Settings** > **Sources** in Copilot Chat.

## Next steps

After you manage federated connector availability, you can:

- Monitor connector usage in the Microsoft 365 admin center.
- Turn on, turn off, or stage individual connectors to specific users or groups, even when a publisher type is cleared in Agent and plugin access.
- Review user feedback to determine which connectors provide the most value to your organization.

## Frequently asked questions

### Does Agent and plugin access apply to federated connectors released in the future?

Yes. If you clear an option, new connectors of that type aren't available until an admin turns them on individually.

### Can I turn on a specific connector when its publisher type is cleared?

Yes. Open the connector in **Copilot connectors** > **Your connections** and stage it to the users or groups you want. Availability is still limited by **User access**.

### Is there a PowerShell or API option for Agent and plugin access?

Not currently. Use the Microsoft 365 admin center.

For more questions about availability, visibility, and troubleshooting, see [Set up custom federated connectors – Frequently asked questions](/microsoft-365/copilot/connectors/frequently-asked-questions).

## Related content

- [Federated Microsoft 365 Copilot connectors](federated-connectors-overview.md)
