---

title: "PagerDuty Incidents connector overview"
ms.author: wangchen
author: wangchen
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the PagerDuty Incidents Copilot connector."
ms.date: 05/15/2026
---

# PagerDuty Incidents connector overview

The PagerDuty Incidents Microsoft 365 Copilot connector integrates PagerDuty incident data into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface incident details directly within apps like Teams, Outlook, and SharePoint.

When you configure the PagerDuty Incidents connector for your organization and index data from your PagerDuty account, users can search for incident information in Microsoft Search, Microsoft 365 Copilot, and Copilot Search. The PagerDuty Incidents connector content can bring improved operational efficiency, faster incident response times, and enhanced incident management.

## Why use the PagerDuty Incidents connector to index your data?

Organizations that use [PagerDuty](https://www.pagerduty.com/) for incident management often face challenges in surfacing incident context across their workflow tools. The PagerDuty Incidents Copilot connector addresses these problems by integrating incident data into Microsoft 365. This allows employees to find incident details through Copilot, Copilot Search, and Microsoft Search — in everyday apps like Teams, Outlook, or SharePoint — without leaving their flow of work. The result is a more connected operations ecosystem that drives faster incident resolution and better collaboration.

The PagerDuty Incidents Copilot connector provides the following benefits:

- **Accelerates incident response** — On-call engineers and responders can quickly find incident history and context directly within Microsoft 365 apps, reducing time spent switching between platforms.
- **Improves situational awareness** — Unified search across PagerDuty incidents and Microsoft tools ensures faster access to incident timelines, priorities, and resolution details, enabling more informed decisions during outages.
- **Enhances cross-team collaboration** — Support, engineering, and management teams can discover incident details, escalation policies, and assigned responders, reducing communication gaps during incidents.
- **Streamlines post-incident reviews** — Teams can use Copilot to summarize incident history, resolution steps, and patterns, accelerating post-mortem analysis and learning.
- **Preserves security and compliance** — The connector respects PagerDuty permissions to ensure that sensitive incident data is only visible to authorized users.

### Use cases

The following table lists common use cases for the PagerDuty Incidents connector.

| Department/role | Use case | Business benefit |
| --- | --- | --- |
| Engineering/DevOps | What incidents were triggered on the payments service last week? | Quickly surface recent incident history for a specific service to assess stability and recurring issues. |
| Engineering/DevOps | Summarize the most recent P1 incident and its resolution steps. | Reduce time spent searching PagerDuty by retrieving incident summaries directly in Copilot. |
| On-call/SRE | Who was assigned to the last database outage incident? | Identify responders and escalation paths without leaving Microsoft Teams. |
| On-call/SRE | Are there any open incidents on the authentication service right now? | Get real-time visibility into active incidents to assess operational risk. |
| IT management | How many high-urgency incidents occurred this month? | Generate operational reports from incident data to track trends and improve reliability. |
| IT management | What is the average resolution time for incidents on the checkout service? | Analyze incident metrics to identify areas for process improvement. |
| Customer support | Find recent incidents related to API latency issues. | Equip support teams with incident context so they can proactively communicate with affected customers. |
| Executives/managers | Summarize incident trends across all teams for the past quarter. | Provide leadership with operational health insights grounded in real incident data. |

## Build agents with the PagerDuty Incidents connector

Developers can use this connector as a knowledge source in declarative agents they build with [Microsoft Copilot Studio](/en-us/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/en-us/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/en-us/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that agent builders can use to help their users retrieve information from PagerDuty incidents.

**Incident response**

- What P1 incidents were triggered in the last 24 hours? List the services affected and current status.
- Summarize the timeline and resolution steps for incident #12345.

**On-call/SRE**

- Who is currently assigned to open incidents on the platform infrastructure service?
- What incidents were escalated beyond the first responder this week?

**Engineering/DevOps**

- Show all incidents related to the deployment pipeline in the past month and their root causes.
- What services have the highest incident frequency this quarter?

**IT management/executives**

- Generate a summary of incident trends across all teams for the past 30 days, grouped by priority.
- What are the top 5 services by incident volume, and what is their average time to resolution?

## Connector capabilities and limitations

The PagerDuty Incidents connector has the following key capabilities:

- **Indexes PagerDuty incidents** — Crawls incident records from your PagerDuty account, including titles, descriptions, priorities, statuses, assignments, and related metadata.
- **Integrates with Copilot** — Enables Copilot and Microsoft Search to find and use PagerDuty incident data. Users can ask questions in natural language and get answers that include information from incidents, with reference links back to the source in PagerDuty.
- **Respects access permissions** — The connector can enforce that only users who have access to PagerDuty data can see it in Copilot responses and search results, based on your organization's access control configuration.
- **Configurable content scope** — Admins can control the date range of incidents indexed using the **Since (Month)** parameter to define how far back the crawl should go.
- **Supports full and incremental crawl** — The connector supports both full crawl and incremental crawl to keep incident data up to date.

The PagerDuty Incidents connector has the following limitations:

- **Focused on incidents** — The connector indexes PagerDuty incident data only. It doesn't index other PagerDuty objects such as services, on-call schedules, maintenance windows, or analytics reports.
- **Regional API support** — The connector supports PagerDuty US and EU service regions. Ensure you use the correct REST API URL for your account's region.
- **Permission updates latency** — Changes to user access in PagerDuty are not reflected immediately in the Copilot index. Permission changes are picked up during the next full crawl cycle.

## Data types indexed from PagerDuty

The PagerDuty Incidents connector indexes incident records so they can be used in Copilot, Copilot Search, and Microsoft Search. The following table describes the properties that are indexed.

| Source property | Label | Description |
| --- | --- | --- |
| AcknowledgedBy | Not applicable | The users who acknowledged the incident. |
| AssignedTo | Not applicable | The users assigned to the incident. |
| ConferenceNumber | Not applicable | The conference number for the incident. |
| ConferenceUrl | Not applicable | The conference URL for the incident. |
| Content | `CONTENT` | The content of the incident. |
| CreatedDateTime | `createdDateTime` | The time at which the incident was created. |
| EscalationPolicyName | Not applicable | The name of the escalation policy associated with the incident. |
| HtmlUrl | `url` | URL of the incident in PagerDuty. |
| IconUrl | `IconUrl` | |
| Id | Not applicable | Unique ID of the incident. |
| IncidentKey | Not applicable | The incident key. |
| IncidentNumber | Not applicable | The incident number. |
| IncidentType | Not applicable | The type of the incident. |
| LastModifiedDateTime | `lastModifiedDateTime` | The time at which the incident was last modified. |
| LastStatusChangeAt | Not applicable | The time at which the incident status was last changed. |
| LastStatusChangeBy | Not applicable | The user who last changed the incident status. |
| Priority | Not applicable | The priority of the incident. |
| ResolveReason | Not applicable | The reason the incident was resolved. |
| ResolvedAt | Not applicable | The time at which the incident was resolved. |
| ServiceName | Not applicable | The name of the service associated with the incident. |
| Status | Not applicable | The status of the incident. |
| Summary | Not applicable | A short-form, server-generated string by PagerDuty that provides succinct, important information about the incident. |
| Teams | Not applicable | The teams associated with the incident. |
| Title | `title` | The title of the incident. |
| Urgency | Not applicable | The urgency of the incident. |

## Permissions model and access control

You can configure the PagerDuty Incidents connector to control who can see indexed incident data in Copilot responses and search results.

You can control permissions in the following ways:

- **Visible to everyone** — All indexed incident data is searchable by any user in the tenant. This works for organizations where incident visibility is shared broadly.
- **Restricted to users with access** — Only users who have access to PagerDuty data can see incident results. The connector uses PagerDuty's team-based access to determine which users can view specific incidents.

## Related articles

- [Set up the PagerDuty Incidents connector](pagerduty-incidents-connector.md)
