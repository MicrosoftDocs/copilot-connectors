---
title: "PagerDuty Escalation Policies connector overview"
ms.author: wangchen
author: wangchen
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 05/26/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the PagerDuty Escalation Policies Microsoft 365 Copilot connector."
---

# PagerDuty Escalation Policies connector overview

The PagerDuty Escalation Policies Microsoft 365 Copilot connector enables your organization to index PagerDuty escalation policy data to make it available to Microsoft 365 Copilot and Microsoft Search. When you deploy the connector, Copilot, Copilot Search, and Microsoft Search can surface relevant escalation policy information directly within apps like Microsoft Teams, Outlook, and SharePoint.

## Why use the PagerDuty Escalation Policies connector to index your data?

Organizations that use PagerDuty for incident management often face challenges in quickly accessing critical escalation policy information across multiple tools. The PagerDuty Escalation Policies connector addresses these challenges by integrating escalation policy data into Microsoft 365. This integration allows employees to surface PagerDuty escalation policies within everyday apps like Teams, Outlook, or SharePoint without leaving their flow of work.

The PagerDuty Escalation Policies connector provides the following benefits:

- **Boosts productivity** – Access PagerDuty escalation policies directly within Microsoft 365 apps, reducing time spent switching platforms.
- **Improves incident response** – Quick access to escalation policies ensures faster incident resolution and better accountability.
- **Enhances collaboration** – Teams can easily understand escalation paths and responsibilities without leaving Microsoft 365.
- **Preserves security and compliance** – The connector respects PagerDuty permissions to ensure that sensitive escalation policy information is only visible to authorized users.

### Common use cases

| Department or role | Use case | Business benefit |
| --- | --- | --- |
| Incident management | Quickly identify escalation paths for critical incidents. | Faster incident resolution and reduced downtime |
| IT operations | Review escalation policy assignments and team coverage. | Better resource allocation and coverage planning |
| Site Reliability Engineering (SRE) | Understand escalation rules and notification timings. | Improved incident response coordination |
| DevOps teams | Track which services are linked to escalation policies. | Enhanced service ownership and accountability |

## Build agents with the PagerDuty Escalation Policies connector

Developers can use this connector as a knowledge source in declarative agents they build with the [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that agent builders can use to help their users retrieve information from PagerDuty escalation policies.

#### Incident management

- Show me the escalation policy for the production database service.
- What are the escalation rules for critical infrastructure incidents?
- List all escalation policies that include the SRE team.

#### Policy review

- Which escalation policies were recently modified?
- Show me all escalation policies created by [user name].
- What services use the 24/7 on-call escalation policy?

#### Team coordination

- What is the escalation path for incidents assigned to my team?
- List all teams linked to escalation policies for the payment service.
- How long does it take for an incident to escalate in the critical services policy?

## PagerDuty Escalation Policies connector capabilities and limitations

The PagerDuty Escalation Policies connector enables the following scenarios:

- **Semantic search** – Access PagerDuty escalation policies in Copilot by using the power of semantic search.
- **ACL retention** – Retain access control lists (ACLs) defined by your organization.
- **Customized crawl frequency** – Customize your crawl frequency to fit your data refresh needs.
- **Copilot Studio integration** – Create workflows by using this connection and plugins from Microsoft Copilot Studio.

The PagerDuty Escalation Policies connector has the following limitations:

- **Advanced Permissions** – When Advanced Permissions is enabled in PagerDuty, only members of the teams linked to a specific escalation policy can access and search for that escalation policy in Microsoft Search and Microsoft 365 Copilot.
- **License requirements** – A PagerDuty Business or Enterprise plan license is required to index the following data properties: `createdBy`, `createdDateTime`, `lastModifiedBy`, and `lastModifiedDateTime`.

## Data types indexed from PagerDuty Escalation Policies

The PagerDuty Escalation Policies connector indexes the following data types from your PagerDuty environment:

- **Escalation policy metadata**: Policy ID, name, summary, description, and URLs.
- **Audit information**: Created by, created date/time, last modified by, last modified date/time (requires PagerDuty Business or Enterprise plan).
- **Escalation rules**: Rule details including escalation timeframes and notification targets.
- **Service associations**: Services that use each escalation policy.
- **Team relationships**: Teams linked to escalation policies (for Advanced Permissions).

The connector indexes escalation policy content and associated metadata to make it searchable and accessible through Copilot, Copilot Search, and Microsoft Search within Microsoft 365 apps.

## Permissions model and access control

The PagerDuty Escalation Policies connector supports two permission models:

- **Everyone in the organization**: All indexed escalation policies are visible to everyone in your Microsoft 365 organization. This is the default setting.
- **Advanced Permissions (PagerDuty ACLs)**: When you enable Advanced Permissions in PagerDuty, the connector respects PagerDuty's access control lists. Only members of the teams linked to a specific escalation policy can access and search for that policy in Microsoft Search and Microsoft 365 Copilot.

Admins can configure the access permissions during connector deployment or customize them later through the connector settings in the Microsoft 365 admin center.

## Next step

> [!div class="nextstepaction"]
> [Deploy the PagerDuty Escalation Policies connector](pagerduty-escalation-policies-deployment.md)

