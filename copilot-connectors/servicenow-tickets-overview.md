---
title: "ServiceNow Tickets Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvindrover
ms.reviewer: mayanksethi
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 01/07/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the ServiceNow Tickets Microsoft 365 Copilot connector."
---

# ServiceNow Tickets Microsoft 365 Copilot connector overview

The ServiceNow Tickets Microsoft 365 Copilot connector allows organizations to index ticket records from ServiceNow and makes them searchable across Microsoft 365 experiences, including Microsoft 365 Copilot and Microsoft Search. After you deploy the connector, users can retrieve ticket information by using natural language queries in Copilot. This capability enhances visibility into IT service management workflows and improves operational efficiency.

## Why use the ServiceNow Tickets connector to index your data?

The ServiceNow Tickets connector helps organizations streamline support operations and improve service delivery by surfacing ticket data directly in Microsoft 365. Common use cases include:

- Empowering support teams to quickly locate and review incident, problem, or change request tickets.
- Allowing managers to track ticket resolution timelines and identify bottlenecks.
- Allowing employees to check the status of their submitted requests without leaving Microsoft 365.
- Enhancing decision-making with access to historical ticket data and trends.

## Build agents with the ServiceNow Tickets connector

Developers can use this connector as a knowledge source in declarative agents they build with the [Copilot Studio full experience](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), the [Copilot Studio lite experience](/microsoft-365-copilot/extensibility/copilot-studio-agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Agent prompts

The following examples show prompts that agent builders can use to help their users retrieve information from ServiceNow Tickets.

| Department | Example Prompts |
|------------|------------------|
| IT Support | - Find the ticket for the network outage reported yesterday.<br>- What is the status of the high-priority ticket?<br>- Show all open tickets assigned to me. |
| Operations | - List all change requests submitted this month.<br>- Who closed the ticket related to the VPN issue?<br>- How many tickets were resolved in the last week? |
| HR/Facilities | - Show tickets related to office equipment requests.<br>- What is the due date for the onboarding ticket for new hires?<br>- Find the ticket for the broken badge reader. |

## ServiceNow Tickets connector capabilities and limitations

The ServiceNow Tickets connector enables users to:

- Perform natural language queries to retrieve ticket details.
- Search across incident, problem, and change request records.
- Filter results by ticket status, priority, assignment group, and other indexed properties.
- View ticket metadata such as creation date, assigned user, and resolution notes.
- Customize URL formats for ticket links to match organizational portal configurations.

The ServiceNow Tickets connector has the following limitations:

- The **Everyone** option on the **Users** tab doesn't process any permissions. Don't select this option unless you want to test the connection between selected team members in an isolated environment. 
- The connector doesn't support reading ACL rules for any ticket items or any table. 
- Incremental crawls don't update permissions or ACLs—only full crawls do.
- Attachments and comments aren't indexed. 

## Data types indexed from ServiceNow Tickets

The connector indexes ticket records from the `task` table and its child tables, such as `incident`, `problem`, and `change_request`. It also indexes user-related data from tables including `sys_user`, `sys_user_group`, and `core_company`. Indexed properties include ticket number, status, priority, assignment group, opened by, closed by, and more.

These indexed properties power search and Copilot experiences, enabling users to retrieve relevant ticket information with contextual prompts.

## Permissions model and access control

The connector supports the **Only people with access to this data source** permission model. Admins can configure access control rules for each indexed table by selecting user fields such as `AssignedTo`, `OpenedBy`, and `ClosedBy`, or based on roles like `itil`. Microsoft Entra ID supports identity mapping, with options for default or custom mapping based on organizational needs.

## Next step

> [!div class="nextstepaction"]
> [Deploy the ServiceNow Tickets connector](servicenow-tickets-deployment.md)
