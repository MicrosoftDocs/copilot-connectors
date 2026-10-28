---
title: Static IP addresses for MCP and federated connectors
description: Configure firewall allow lists for static outbound IP addresses used by MCP-based federated connectors and declarative agents in Microsoft 365 Copilot.
author: avni333malhotra-dev
ms.author: avnimalhotra
ms.reviewer: mansipakhale
ms.date: 10/23/2026
ms.topic: how-to
ms.localizationpriority: medium
ms.audience: Admin
---

<!-- cSpell:ignore avni333malhotra-dev avnimalhotra mansipakhale -->

# Static IP addresses for MCP and federated connectors

Microsoft 365 Copilot Chat uses a fixed, known set of outbound (egress) IP addresses for Model Context Protocol (MCP) tool and API calls from declarative agents and federated connectors. If the firewall protecting your MCP server restricts incoming traffic by source IP address, add these addresses to its allow list instead of allowing a large, dynamic Azure address space.

Static egress is enabled by default for all MCP-based interactions in declarative agents and federated connectors. No manifest flag or configuration change is required to enable it. Static egress doesn't apply to Agent-to-Agent (A2A) interactions.

These static egress IP addresses apply only to MCP protocol requests between Microsoft 365 Copilot and the MCP server. They don't apply to sign-in, authentication, or other Microsoft 365 Copilot traffic. Configure those network requirements separately.

## How static egress works

For an MCP request, traffic follows this path:

```text
Declarative agent or federated connector (MCP)
  -> Copilot runtime
  -> Static egress layer
  -> Customer or partner MCP server
```

The MCP server receives requests from the static egress IP addresses in the downloadable list. IP allow listing doesn't replace authentication or authorization. Continue to enforce the authentication and permissions required by your MCP server.

## EU regional isolation

Static egress preserves EU regional isolation for GDPR. Requests to MCP servers in EU regions use an EU subnet source IP address. When configuring the firewall allow list for an EU-region MCP server, use the [EU static egress IP address list (JSON)](media/federated-connectors/static-egress-ip-addresses-eu.json).

## Configure your firewall allow list

Download the [static egress IP address list (JSON)](media/federated-connectors/static-egress-ip-addresses.json) and add the applicable source IP addresses to the firewall protecting your MCP server.

> [!IMPORTANT]
> This IP address list can change with seven days' notice. Review this page regularly and update your firewall allow list before changes take effect.

## IP addresses for Cowork

For Cowork IP ranges, see [Cowork network endpoints](/microsoft-365/copilot/cowork/cowork-network-endpoints#ip-address-ranges-for-firewall-configuration).

## Related content

- [Federated connectors overview](federated-connectors-overview.md)
- [Set up custom federated connectors](set-up-custom-federated-connectors.md)
