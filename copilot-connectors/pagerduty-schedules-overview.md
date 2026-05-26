---
ms.date: 05/20/2026
title: "PagerDuty Schedules connector overview"
ms.author: wangchen
author: wangchen
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the PagerDuty Schedules Copilot connector."
---

# PagerDuty Schedules connector overview (preview)

The PagerDuty Schedules Microsoft 365 Copilot connector integrates PagerDuty schedule data into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface schedule information directly within apps like Teams, Outlook, and SharePoint.

When you configure the PagerDuty Schedules connector for your organization and index data from PagerDuty, users can search for schedule information in Microsoft Search, Microsoft 365 Copilot, and Copilot Search. The PagerDuty Schedules connector content can bring improved operational efficiency, faster response times for incident management, and enhanced team coordination.

[!INCLUDE [conector-preview-access](includes/connector-preview-access.md)]

## Why use the PagerDuty Schedules connector to index your data?

Organizations that use PagerDuty for incident management and on-call scheduling often struggle with fragmented information and inefficient schedule lookups. The PagerDuty Schedules Copilot connector addresses these problems by integrating schedule data into Microsoft 365. This allows employees to access PagerDuty schedules through Copilot, Copilot Search, and Microsoft Search – in everyday apps like Teams, Outlook, or SharePoint – without leaving their flow of work. The result is more efficient incident response and improved team coordination.

The PagerDuty Schedules Copilot connector provides the following benefits:

- **Accelerates incident response** - Teams can quickly identify who is on-call without switching to PagerDuty, enabling faster escalation and resolution.
- **Improves coordination** - Managers and team leads can view schedule coverage directly within Microsoft 365 apps, improving resource planning and shift management.
- **Reduces context switching** - Users access schedule information directly within their workflow, reducing time spent searching across platforms.
- **Enhances transparency** - Cross-functional teams can discover on-call schedules for dependent services, improving communication and collaboration.
- **Streamlines planning** - Operations teams can query schedule information via Copilot to plan maintenance windows and change deployments around on-call coverage.
- **Preserves security and compliance** - The connector respects PagerDuty permissions to ensure that schedule information is only visible to authorized users.

### Use cases

The following table lists common use cases for the PagerDuty Schedules connector.

| Department/role | Use case | Business benefit |
| --------------- | -------- | ---------------- |
| IT Operations | Who is on-call for the database team this week? | Quickly identify on-call engineers for immediate escalation during incidents. |
| Engineering | Show me the schedule for the DevOps team for the next 7 days. | Plan deployments and maintenance windows around on-call coverage. |
| Site Reliability Engineering (SRE) | Find all schedules that include [team member name]. | Understand coverage patterns and identify potential schedule conflicts. |
| Engineering managers | Summarize the on-call rotation for Q2 and identify coverage gaps. | Improve schedule planning and ensure adequate coverage for critical services. |
| DevOps | Who is on-call for the infrastructure team during the upcoming holiday weekend? | Plan for holiday coverage and ensure adequate staffing for critical systems. |
| Support teams | What is the escalation schedule for priority 1 incidents? | Streamline incident escalation by identifying the correct on-call responders. |
| Operations | Create a summary of all on-call schedules with coverage percentage. | Analyze schedule effectiveness and identify optimization opportunities. |
| IT Leadership | What teams have overlapping on-call schedules this month? | Optimize resource allocation and prevent schedule conflicts across teams. |

## Build agents with the PagerDuty Schedules connector

Developers can use this connector as a knowledge source in declarative agents they build with [Microsoft Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that agent builders can use to help their users retrieve information from PagerDuty Schedules.

**IT Operations/DevOps**

- Who is currently on-call for the production infrastructure team?
- Show me the on-call schedule for the database team for the next two weeks.
- Find all schedules where [team member name] is on-call this month.

**Engineering/SRE**

- What is the coverage percentage for the API services schedule?
- List all teams that have on-call coverage during the upcoming holiday weekend.
- Summarize the on-call rotation for the platform engineering team in Q2.

**Support/Helpdesk**

- Who should I escalate this priority 1 incident to based on the current on-call schedule?
- Show me the escalation path for network-related incidents.

**Engineering managers**

- Identify coverage gaps in the DevOps team schedule for next month.
- Compare on-call schedules across all engineering teams to identify overlapping coverage.
- Summarize on-call distribution across the team to ensure balanced rotations.

## Connector capabilities and limitations

The PagerDuty Schedules connector has the following key capabilities:

- **Indexes PagerDuty schedules** – Crawls PagerDuty schedule data including schedule names, on-call rotations, and coverage information.
- **Integrates with Copilot** – Enables Copilot and Microsoft Search to find and use PagerDuty schedule information. Users can ask questions in natural language and get answers that include schedule details, with reference links back to the source in PagerDuty.
- **Respects PagerDuty permissions** – The connector only shows schedule information to users who have access in PagerDuty. It honors PagerDuty's Advanced Permissions settings, so responses and search results don't expose schedules to unauthorized users.
- **Configurable content scope** – Admins can control the date range for schedule data that is indexed using the Days Before and Days After parameters.
- **Semantic search** – Leverages semantic search capabilities to help users find schedule information using natural language queries.
- **Customizable crawl frequency** – Admins can adjust the full crawl schedule to fit their data refresh needs.

The PagerDuty Schedules connector has the following limitations:

- **Supports PagerDuty Cloud only** – This connector works with PagerDuty's cloud service. On-premises or self-hosted PagerDuty instances are not supported.
- **Preview status** – This connector is currently in preview and may have limited availability. Preview features are subject to change.
- **Full crawl only** – The connector only supports full crawl operations. Incremental crawl is not available, so all schedule data is re-indexed during each crawl cycle.
- **Advanced Permissions enforcement** – When Advanced Permissions is enabled in PagerDuty, only members of the teams linked to a specific schedule can access and search for that schedule in Microsoft Search and Microsoft 365 Copilot.
- **Date range limitation** – The connector only indexes schedule entries within the configured date range (defined by Days Before and Days After parameters). Historical schedules outside this range are not indexed.
- **Schedule focus** – The connector indexes schedule data only. It doesn't index incidents, alerts, or other PagerDuty objects.

## Data types indexed from PagerDuty Schedules

The PagerDuty Schedules connector indexes schedule data so it can be used in Copilot, Copilot Search, and Microsoft Search. The connector crawls schedule information based on the configured date range.

| PagerDuty content type | Indexed and surfaced in Copilot and search |
| ----------------------- | ------------------------------------------ |
| **Schedules** | Schedule information including name, description, time zone, and final schedule entries. The connector indexes schedule titles and descriptions, making them searchable in Copilot responses and search results. |
| **Schedule entries** | On-call rotation entries within the configured date range, including user assignments, start times, and end times. |
| **Coverage information** | Coverage percentage data for each schedule, indicating the proportion of the configured time range that has on-call coverage. |
| **Usage data** | Information about escalation policies associated with each schedule. |

## Permissions model and access control

You can configure the PagerDuty Schedules connector to enforce that only users who have access to a schedule in PagerDuty can see it in Copilot responses and search results. The system uses the PagerDuty access control list (ACL) for schedules.

The PagerDuty Schedules connector honors the same permission setup as the data source. This means that if a user can see a schedule in PagerDuty, they can see it in Copilot and Microsoft Search results. If they don't have access in PagerDuty, the schedule information won't appear in their results.

You can control permissions in the following ways:

- **Advanced Permissions enforcement** – When Advanced Permissions is enabled in PagerDuty, the connector respects team-based access controls. Only members of the teams linked to a specific schedule can access and search for that schedule in Microsoft Search and Microsoft 365 Copilot.

- **User identity mapping** - The connector maps PagerDuty user accounts to Microsoft 365 (Entra ID) identities. If PagerDuty users' emails match their Entra ID UPNs, this mapping is automatic. If they differ, you can provide a mapping rule to map identities in PagerDuty to identities in Microsoft 365. For more information, see [Map your non-Entra ID identities](map-non-entra-id.md). This ensures that the system provides appropriate access to PagerDuty schedule information in responses.

- **Visible to everyone option** - You can choose not to enforce per-user permissions (setting the connector to index content as **Visible to everyone**). In that case, all indexed PagerDuty schedule data is searchable by any user in the tenant. This works for organizations where schedule information is considered non-confidential. However, for most scenarios, we recommend using the restricted mode so that results mirror the PagerDuty permission boundaries.

## Next step

> [!div class="nextstepaction"]
> [Set up the PagerDuty service for connector ingestion](pagerduty-schedules-admin-setup.md)
