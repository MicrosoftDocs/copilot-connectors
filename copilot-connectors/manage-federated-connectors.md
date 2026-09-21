---
title: Manage federated connector availability
description: Learn how to use PowerShell to control the availability of federated connectors for Microsoft 365 Copilot in your organization.
#customer intent: As an admin, I want to learn how to manage federated connectors for Microsoft 365 Copilot using PowerShell.
author: danipocket
ms.author: danielabo
manager: calvind
ms.reviewer: mansipakhale
ms.service: microsoft-365-copilot-connectors

ms.date: 04/28/2026
ms.topic: how-to
ms.localizationpriority: medium
ms.audience: Admin
---

# Manage federated connector availability

[!INCLUDE [wiqd-beta-disclaimer](includes/wiqd-beta-disclaimer.md)]

Federated connectors for Microsoft 365 Copilot enable users to access information from external data sources directly within their Copilot experience. Microsoft provides default federated connectors that use the Model Context Protocol (MCP) to integrate with popular services and tools. While these connectors enhance Copilot's capabilities by extending its knowledge base, organizations might need to control their availability for security, compliance, or governance reasons.

As an administrator, you can use PowerShell to manage the availability of all default federated connectors across your tenant. This centralized management approach allows you to quickly disable or enable connectors organization-wide while maintaining visibility and control over individual connector settings.

> [!IMPORTANT]
> Microsoft is retiring the command-line (CLI) toggle for setFederatedConnectors by **August 25, 2026**. The CLI is being deprecated so that connector and agent settings are honored from the same global tenant settings, giving you one consistent place to govern both. Going forward, you can manage the same intent through the **Allowed agent types** setting in Agent 365. For more information, see [Allowed agent types](/microsoft-365/admin/manage/agent-settings#allowed-agent-types).

## Manage federated connector availability for your organization

The federated connector management capability provides a tenant-wide toggle that allows you to:

- **Disable all default federated connectors** in a single operation.
- **Automatically apply the setting to future default connectors** that Microsoft releases.
- **Selectively enable specific connectors** while keeping the global disable setting active.
- **Reenable all connectors** to restore default behavior when needed.

## Prerequisites

The federated connector management capability requires the following prerequisites:

- **Administrator role**: Global Administrator or Search Administrator permissions
- **PowerShell access**: Ability to run PowerShell as an administrator (CLI will be deprecated by August 25, 2026)
- **Connector.Cmd module**: Version 2.1 or later (installed in the following steps) (CLI will be deprecated by August 25, 2026)

## Disable the agent type used by Copilot connectors

The [Allowed agent types](/microsoft-365/admin/manage/agent-settings#allowed-agent-types) setting provides a tenant-wide control for governing Microsoft 365 Copilot agents and connectors from a single location in the Microsoft 365 admin center. When an administrator disables the agent type used by Copilot connectors, Microsoft 365 Copilot connectors are no longer available to end users. Existing connectors remain visible to administrators for management and governance purposes, but their allowed-user scope is automatically set to **No users**, preventing end-user access.

To disable the agent type used by Copilot connectors:

1. In the Microsoft 365 admin center, go to [Allowed agent types](/microsoft-365/admin/manage/agent-settings#allowed-agent-types).
1. Disable the agent type used by Microsoft 365 Copilot connectors.
1. Save your changes.

To make a specific connector available, an administrator can open that connector's settings and update its allowed-user scope to the desired users or groups. This change enables selective connector access while maintaining centralized tenant-wide governance.

## Install the PowerShell module (CLI will be deprecated by August 25, 2026)

1. Open PowerShell as an administrator.

1. Install the Connector.Cmd module from the PowerShell Gallery:

    ```powershell
    Install-Module Connector.Cmd
    ```

    > [!NOTE]
    > These steps require Connector.Cmd version 2.1 or later.

1. If prompted, confirm that you want to install from the PowerShell Gallery by entering **Y**.

## Configure the federated connector toggle (CLI will be deprecated by August 25, 2026)

Use the `Set-FederatedConnectorToggle` cmdlet to enable or disable federated connectors across your tenant.

1. In PowerShell, run the following command:

    ```powershell
    Set-FederatedConnectorToggle
    ```

1. When prompted, authenticate with your Global Administrator or Search Administrator credentials.

1. Approve the requested permissions.

1. The cmdlet displays the current state of the federated connector toggle and prompts you to choose an action:
   - Select **Disable** to turn off all federated connectors.
   - Select **Enable** to turn on all federated connectors.

> [!NOTE]
> The tenant toggle automatically applies to future federated connectors. If you disable the toggle, new connectors appear in a disabled state. If you enable the toggle, new connectors follow the default rollout behavior.

## Verify the changes

After you configure the toggle, changes propagate across your organization:

- Changes can take **up to 10 minutes** to take effect across all Microsoft 365 experiences.
- You might need to refresh the Microsoft 365 admin center to see updated connector states.
- Users might experience a brief delay before connector availability changes are reflected in their Copilot experience.

To verify the current state, run `Set-FederatedConnectorToggle` again to display the current configuration before prompting for changes.

## Next steps

After you manage the federated connector toggle, you can:

- Monitor connector usage in the Microsoft 365 admin center.
- Selectively enable or disable individual connectors even when the global toggle is set to disable.
- Review user feedback to determine which connectors provide the most value to your organization.

## Frequently asked questions

### If an admin previously disabled federated Copilot connectors by using the Set-FederatedConnectorToggle CLI, will they remain disabled after this rollout?

Yes. If an admin previously disabled federated Copilot connectors by using the `Set-FederatedConnectorToggle` CLI, the setting is honored until October 20, 2026. Admins must update the **Allowed agent types** settings by then to continue this behavior after October 20, 2026.

### Will the Allowed agent types setting follow the same behavior as Set-FederatedConnectorToggle?

Yes. It applies to future connectors while allowing admins to selectively enable or disable individual connectors.

### Between August 25 and October 20, if admins need to disable all federated connectors, should they manually disable each connector under Microsoft 365 admin center > Copilot > Connectors?

If the admin didn't use `Set-FederatedConnectorToggle` before August 25, they can disable all federated connectors directly by using **Allowed agent types**.

## Related content

- [Federated Microsoft 365 Copilot connectors](federated-connectors-overview.md)
- [Connector.Cmd in the PowerShell Gallery](https://www.powershellgallery.com/packages/Connector.Cmd/2.1)
 
