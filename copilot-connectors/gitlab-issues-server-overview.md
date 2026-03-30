---
title: "GitLab Issues Server Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 01/21/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the GitLab Issues Server Microsoft 365 Copilot connector."
---

# GitLab Issues Server Microsoft 365 Copilot connector overview

The GitLab Issues Server Microsoft 365 Copilot connector integrates GitLab issue data into Microsoft 365. When you deploy this connector, Microsoft 365 Copilot and Microsoft Search can surface relevant GitLab issues directly in apps such as Teams, Outlook, and SharePoint. By indexing issues from GitLab Server projects and groups, users can search, summarize, and reason over issue data using Copilot and Microsoft Search. This capability helps development and delivery teams track work, triage bugs, and understand project status without leaving their Microsoft 365 flow of work.  

## Why use the GitLab Issues Server connector to index your data?

For many engineering and DevOps teams, GitLab Issues serve as the system of record for feature requests, defects, incidents, and operational tasks. However, this information is often siloed within GitLab, making it harder for stakeholders outside engineering to stay informed without switching tools. The GitLab Issues Server connector indexes issue data from GitLab projects and groups so that developers, product managers, support teams, and engineering leaders can discover and summarize relevant issues directly within Microsoft 365.  

Users can ask natural language questions such as:

- What are the open P1 issues for the payments service?
- Which GitLab issues are assigned to me this sprint?

### Use cases

The following table lists common use cases for the GitLab Issues Server connector.


| Department / role       | Use case                                                                                     | Business benefit                                                             |
|-------------------------|-----------------------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| Engineering             | Ask Copilot for open bugs, assigned issues, or blockers.                                      | Faster understanding of current work; less time spent filtering issues.      |
| DevOps / SRE            | Summarize incidents, reliability issues, or operational tasks across projects.                | Improved incident reviews and better identification of reliability trends.   |
| IT support / Help desk  | Surface user‑reported issues and summarize their current status.                              | Faster responses to stakeholders; fewer duplicate issues.                    |
| Product management      | Review feature requests and backlog items grouped by labels, milestones, or epics.            | Better prioritization and roadmap planning.                                  |
| Engineering leadership  | Get summaries of critical issues, overdue items, and release blockers across teams.           | Faster decision‑making and improved delivery confidence.                     |

## Build agents with the GitLab Issues Server connector

Developers can use this connector as a knowledge source in declarative agents they build with Copilot Studio, Agent Builder in Microsoft 365 Copilot, or the Microsoft 365 Agents Toolkit.  

By connecting GitLab Issues to these agents, teams can build experiences that:

- Answer questions about current issue load, ownership, and priorities  
- Summarize related issues for a feature, epic, or incident  
- Help teams plan sprints, milestones, and releases using live GitLab data  

### Example prompts

The following examples show prompts that agent builders can use to help their users retrieve information from GitLab Issues Server.  

**Engineering:**

- What are the open bugs for the checkout service, and who are they assigned to?  
- Summarize issues labeled *performance* created in the last seven days.  
- Which GitLab issues are blocking the next release for Project Alpha?  

**DevOps / SRE:**

- List open incidents labeled *production* or *sev1* and summarize their current status.  
- What recurring error patterns appear in issues labeled *database* over the last month?  
- Summarize follow-up tasks created after the most recent production incident.  

**IT support / Help desk:**

- Find GitLab issues related to VPN or single sign‑on (SSO) problems and summarize their status.  
- Which issues track user‑reported authentication failures, and what is the expected resolution timeline?  

**Product management:**

- Summarize all open feature requests labeled *vNext* for Project Alpha.  
- What are the top customer-requested features based on issues labeled *customer-request*?  
- Which issues are currently scoped into the next milestone for the mobile app?  

**Engineering leadership:**

- Give me a summary of all critical open issues across our top three GitLab projects.  
- Which high‑priority issues are at risk of missing the current milestone?  

## GitLab Issues Server connector capabilities and limitations

### Capabilities

The GitLab Issues Server connector enables users to:

- Index GitLab repositories and access issues.  
- Retrieve GitLab data efficiently from Microsoft Search and Microsoft 365 Copilot.  
- Maintain GitLab access control lists (ACLs) and user permissions.  
- Allow administrators to customize crawl frequency and indexing preferences.  

### Limitations

The GitLab Issues Server connector has the following limitations:

- Doesn't support indexing GitLab CI/CD pipelines beyond status indexing.  
- Only repositories and issues are indexed.  
- Banning users isn't supported as a permission rule; remove users from groups instead.  
- Restricting group access by IP address isn't supported.  
- The Planner role is deprecated; assign Reporter roles or higher.  
- Access to merge requests for public projects with restricted visibility is limited to Reporter roles and higher.  

## Data types indexed from GitLab Issues Server

The connector indexes GitLab issues and associated metadata, including titles, descriptions, labels, timestamps, users, and project or group hierarchy. This information is available to Microsoft 365 Copilot and Microsoft Search, allowing users to discover, filter, summarize, and reference GitLab issues directly from Microsoft 365 apps.

## Permissions model and access control

The GitLab Issues Server connector respects GitLab project visibility, group membership, and access control lists. Users only see issue data they're authorized to view based on GitLab's permissions model, ensuring security and compliance.  

## Next step

> [!div class="nextstepaction"]  
> [Deploy the GitLab Issues Server connector](gitlab-issues-server-deployment.md)
