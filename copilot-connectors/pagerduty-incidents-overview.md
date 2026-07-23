---
title: "PagerDuty Incidents connector overview"
ms.author: wangchen
author: wangchen
manager: zezhangzhao
ms.reviewer: lauragra
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: microsoft-365-copilot-connectors
ms.date: 06/18/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the PagerDuty Incidents Microsoft 365 Copilot connector."
---

# PagerDuty Incidents connector overview

The PagerDuty Incidents Microsoft 365 Copilot connector integrates PagerDuty incident data into Microsoft 365. This integration enables Copilot, Copilot Search, and Microsoft Search to surface incident details directly within apps like Teams, Outlook, and SharePoint.

When you configure the PagerDuty Incidents connector for your organization and index data from your PagerDuty account, users can search for incident information in Microsoft Search, Microsoft 365 Copilot, and Copilot Search. The PagerDuty Incidents connector content can bring improved operational efficiency, faster incident response times, and enhanced incident management.

## Why use the PagerDuty Incidents connector to index your data?

Organizations that use [PagerDuty](https://www.pagerduty.com/) for incident management often face challenges in surfacing incident context across their workflow tools. The PagerDuty Incidents connector addresses these problems by integrating incident data into Microsoft 365. This integration allows employees to find incident details through Copilot, Copilot Search, and Microsoft Search without leaving their flow of work. The result is a more connected operations ecosystem that drives faster incident resolution and better collaboration.

The PagerDuty Incidents connector provides the following benefits:

- **Accelerates incident response** — On-call engineers and responders can quickly find incident history and context directly within Microsoft 365 apps, reducing time spent switching between platforms.
- **Improves situational awareness** — Unified search across PagerDuty incidents and Microsoft tools ensures faster access to incident timelines, priorities, and resolution details, enabling more informed decisions during outages.
- **Enhances cross-team collaboration** — Support, engineering, and management teams can discover incident details, escalation policies, and assigned responders, reducing communication gaps during incidents.
- **Streamlines post-incident reviews** — Teams can use Copilot to summarize incident history, resolution steps, and patterns, accelerating post-mortem analysis and learning.
- **Preserves security and compliance** — The connector respects PagerDuty permissions to ensure that sensitive incident data is only visible to authorized users.

The following table lists common use cases for the PagerDuty Incidents connector.

| Department or role | Use case | Business benefit |
| --- | --- | --- |
| Engineering/DevOps | What incidents triggered on the payments service last week? | Quickly surface recent incident history for a specific service to assess stability and recurring issues. |
| Engineering/DevOps | Summarize the most recent P1 incident and its resolution steps. | Reduce time spent searching PagerDuty by retrieving incident summaries directly in Copilot. |
| On-call/SRE | Who was assigned to the last database outage incident? | Identify responders and escalation paths without leaving Microsoft Teams. |
| On-call/SRE | Are there any open incidents on the authentication service right now? | Get real-time visibility into active incidents to assess operational risk. |
| IT management | How many high-urgency incidents occurred this month? | Generate operational reports from incident data to track trends and improve reliability. |
| IT management | What is the average resolution time for incidents on the checkout service? | Analyze incident metrics to identify areas for process improvement. |
| Customer support | Find recent incidents related to API latency issues. | Equip support teams with incident context so they can proactively communicate with affected customers. |
| Executives/managers | Summarize incident trends across all teams for the past quarter. | Provide leadership with operational health insights grounded in real incident data. |

## Build agents with the PagerDuty Incidents connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that users can use to retrieve information from PagerDuty Incidents.

**Incident response**

- What P1 incidents triggered in the last 24 hours? List the services affected and current status.
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

## PagerDuty Incidents connector capabilities and limitations

The PagerDuty Incidents connector enables users to:

- **Index PagerDuty incidents** — Crawl incident records from your PagerDuty account, including titles, descriptions, priorities, statuses, assignments, and related metadata.
- **Integrate with Copilot** — Allow Copilot and Microsoft Search to find and use PagerDuty incident data. Users can ask questions in natural language and get answers that include information from incidents, with reference links back to the source in PagerDuty.
- **Respect access permissions** — Ensure that only users who have access to PagerDuty data can see it in Copilot responses and search results, based on your organization's access control configuration.
- **Configure content scope** — Control the date range of incidents indexed by using the **Since (Month)** parameter to define how far back the crawl should go.
- **Support full and incremental crawl** — Use both full crawl and incremental crawl to keep incident data up to date.

The PagerDuty Incidents connector has the following limitations:

- **Incident crawl cap** — The connector crawls only the 10,000 most recent incidents, sorted in descending order by their creation date and time.
- **Focused on incidents** — The connector indexes PagerDuty incident data only. It doesn't index other PagerDuty objects such as services, on-call schedules, maintenance windows, or analytics reports.
- **Regional API support** — The connector supports PagerDuty US and EU service regions. Ensure you use the correct REST API URL for your account's region.
- **Permission updates latency** — Changes to user access in PagerDuty aren't reflected immediately in the Copilot index. Permission changes are picked up during the next full crawl cycle.

## Data types indexed from PagerDuty Incidents

The PagerDuty Incidents connector indexes incident records from your PagerDuty account. Indexed incident content includes the incident title, summary, status, priority, urgency, incident type, associated service, escalation policy, assigned and acknowledging users, conference details, timestamps for creation and resolution, and links back to the source incident in PagerDuty. Indexed incidents appear as results in Microsoft Search and as grounding content in Microsoft 365 Copilot and Copilot Search responses, with reference links back to the incident in PagerDuty.

## Permissions model and access control

You can configure the PagerDuty Incidents connector to control who can see indexed incident data in Copilot responses and search results.

You can control permissions in the following ways:

- **Visible to everyone** — All indexed incident data is searchable by any user in the tenant. This option works for organizations where incident visibility is shared broadly.
- **Restricted to users with access** — Only users who have access to PagerDuty data can see incident results. The connector uses PagerDuty's team-based access to determine which users can view specific incidents.

## Next step

> [!div class="nextstepaction"]
> [Deploy the PagerDuty Incidents connector](pagerduty-incidents-deployment.md)
