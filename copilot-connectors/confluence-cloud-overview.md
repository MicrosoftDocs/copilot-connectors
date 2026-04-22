---
ms.date: 12/19/2025
title: "Confluence Cloud Connector Overview"
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Confluence Cloud Copilot connector."
---

# Confluence Cloud Copilot connector overview

The Confluence Cloud Microsoft 365 Copilot connector integrates Confluence content into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface relevant wiki pages and blogs directly within apps like Teams, Outlook, and SharePoint.

When you configure the Confluence Cloud connector for your organization and index data from the Confluence site, users can search for Confluence content in Microsoft Search, Microsoft 365 Copilot, and Copilot Search. The Confluence Cloud connector content can bring improved operational efficiency, faster response times for user requests, and enhanced request management.

## Why use the Confluence Cloud connector to index your data?

Organizations that use Atlassian Confluence for internal wikis and documentation often face knowledge silos and inefficient search workflows. The Confluence Cloud Copilot connector addresses these problems by integrating Confluence content into Microsoft 365. This allows employees to surface Confluence pages and blogs through Copilot, Copilot Search, and Microsoft Search – in everyday apps like Teams, Outlook, or SharePoint – without leaving their flow of work. The result is a more connected knowledge ecosystem that drives productivity and collaboration.

The Confluence Cloud Copilot connector provides the following benefits:

- **Boosts productivity** - Employees access Confluence content directly within Microsoft 365 apps, reducing time spent searching and switching platforms.
- **Improves decision-making** - Unified search across Confluence and Microsoft tools ensures faster access to institutional knowledge, enabling more informed and timely decisions.
- **Accelerates request fulfillment** - Support teams and operations resolve issues faster by retrieving troubleshooting guides and documentation instantly via Copilot.
- **Enhances collaboration** - Cross-functional teams discover and utilize each other’s Confluence content, reducing duplication and improving alignment.
- **Strengthens onboarding and training** - New hires and managers can use Copilot to summarize onboarding materials and policies stored in Confluence, streamlining ramp-up.
- **Preserves security and compliance** - The connector respects Confluence permissions to ensure that sensitive content is only visible to authorized users.

### Use cases

The following table lists common use cases for the Confluence Cloud connector.

| Department/role | Use case | Business benefit |
| --------------- | -------- | ---------------- |
| All | How do I submit an expense claim?  | Consolidate policy guidance from multiple knowledge bases into a single answer, reducing confusion and support tickets. |
| All | Find documents related to the most recent project I'm working on. | Surface relevant project documents instantly, reducing time spent searching across multiple systems. |
| All | Who should I reach out to as the subject matter expert for Data & Analytics? What is his email address? | Identify key contacts and their details from organizational wikis, reducing time spent finding the right person. |
| Engineering | Create discussion points for the Sprint Review meeting to ensure all user stories are addressed, focusing on progress and blockers. Include questions to assess the team's comfort with the sprint's workload, task manageability, and unforeseen challenges. | Streamline sprint planning by automatically generating structured discussion points grounded in Confluence documentation. |
| Engineering | Conduct an in-depth product analysis. Showcase our strengths and pinpoint areas where enhancements are possible. | Leverage internal competitive research docs in Confluence to produce actionable competitive insights. |
| Product | Create a Product Requirements Document based on the meeting notes in Confluence. | Accelerate PRD creation by synthesizing meeting notes from Confluence into structured product specs. |
| Product | Write a project report summary . For each item, include a short section with a clear explanation, emphasizing only the most important details. | Generate concise executive summaries from project wiki pages, saving time on manual status reporting. |
| Marketing | Rewrite this release note as social media post and ensure it complies with our social media standards. | Repurpose Confluence release content into social-ready formats while maintaining brand compliance. |
| Marketing | Create a detailed go-to-market plan, covering the intended audience, unique value, marketing approach, schedule, and key performance indicators. | Transform product documentation into comprehensive GTM strategies, accelerating time-to-market. |
| Sales | Examine the account plan from the attachments to spot upsell possibilities using data, product shortcomings, and recent support cases.  | Combine account plans with Confluence knowledge to identify data-driven upsell opportunities. |
| Helpdesk | Find all HR policies relevant for onboarding new employees, and present them in a table format. | Aggregate onboarding guides and policies from Confluence into structured, easy-to-follow formats for faster onboarding. |
| Customer support | Compose a brief, assertive, and positive reply to a customer's concern. Address the objection constructively and highlight how it can be leveraged as an opportunity. | Draft customer responses grounded in Confluence knowledge base articles, improving response quality and consistency. |
| Security | Develop a thorough incident response strategy. Include detection, communication, containment, and recovery steps, customized to the situation's unique risks. | Build comprehensive incident response plans leveraging institutional knowledge from Confluence runbooks and past incident records. |

## Build agents with the Confluence Cloud connector

Developers can use this connector as a knowledge source in declarative agents they build with [Microsoft Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that agent builders can use to help their users retrieve information from Confluence Cloud.

**People/HR**

- Summarize the onboarding process for new hires in the engineering team, including links to relevant Confluence pages.
- What are the latest updates to the remote work policy documented in Confluence?

**IT Support/Help desk**

- Find the runbook for resolving VPN connectivity issues and summarize the steps.
- What troubleshooting guides are available for Outlook sync errors?

**Engineering/DevOps**

- Summarize the architecture of the new microservices deployment from the last retrospective.
- What are the key decisions documented in the Q3 design review wiki?

**Product management**

- List all feature specs tagged with 'vNext' and summarize their status.
- What are the dependencies mentioned in the release plan for Project Orion?

**Sales/marketing**

- Summarize the messaging framework for the Contoso campaign and link to the case studies.
- What are the key takeaways from the last marketing retrospective?

**Executives/managers**

- Summarize the latest project updates across all teams from Confluence.
- What are the documented risks and mitigation plans for the upcoming launch?

## Connector capabilities and limitations

The Confluence Cloud connector has the following key capabilities:

- **Indexes core Confluence content** – Crawls Confluence Cloud wiki pages and blog posts (from all spaces by default).
- **Integrates with Copilot** – Enables Copilot and Microsoft Search to find and use Confluence content. Users can ask questions in natural language and get answers that include information from Confluence pages or files, with reference links back to the source. 
- **Respects Confluence permissions** – The connector only shows content to users who have access in Confluence. It honors Confluence’s space permissions and page restrictions, so responses and search results don't expose pages to unauthorized users. 
- **Configurable content scope** – Admins can control what Confluence data is indexed. For example, you can include or exclude specific spaces or filter by metadata using Confluence Query Language (CQL) queries.

The Confluence Cloud connector has the following limitations:

- **Supports Confluence Cloud only** – This connector works with Atlassian Confluence Cloud. It doesn't support Confluence Server or Data Center deployments – those require a separate on-premises connector.
- **Permission updates latency** – Changes to user or group access in Confluence are not reflected immediately in the Copilot index. Permission changes are picked up only during a full crawl (once every 24 hours by default), not during the 15-minute incremental syncs. This means there can be a delay (up to the next full reindex) before Copilot results fully reflect newly changed permissions.
- **Identity mapping requirement** – The connector relies on matching Confluence user identities to Microsoft Entra ID accounts to enforce permissions. If your Confluence users’ email IDs do not exactly match their Entra ID user principal names (UPNs), an admin must configure a manual identity mapping so the system knows which Microsoft 365 user corresponds to each Confluence account. Without this mapping, some content might not appear for intended users because the service can't verify that they have access.
- **Focused on wiki content** – The connector indexes Confluence pages and blog posts. It doesn't index certain Confluence metadata or app-specific content outside of pages. For example, it doesn’t pull in Confluence user profile information, page history versions, or content from third-party Confluence apps (like Questions, calendars, or other add-ons). It also only indexes published content – content that is archived, unpublished drafts, or in the recycle bin is not ingested. This ensures Copilot draws from the official current knowledge base, but it means historical or deleted content won’t surface in answers. 

## Data types indexed from Confluence Cloud

The Confluence Cloud connector indexes key Confluence content types so they can be used in Copilot, Copilot Search, and Microsoft Search. By default, the connector crawls all Confluence pages and blog posts in your Confluence Cloud site. 

| Confluence content type | Indexed and surfaced in Copilot and search |
| ----------------------- | ------------------------------------------ |
| **Pages** | Main content pages in Confluence spaces. The connector indexes page titles and body text. These appear as search results or referenced content in Copilot responses.| 
| **Blog posts** | Confluence blog entries (news or updates). Copilot can retrieve the content and show it in results by title. Users can query Copilot for information contained in blog posts. |
| **Attachments** | Files attached to pages or blog posts. Attachments are indexed together with Confluence page contents into the content property of the data schema.|

## Custom data filters

The Confluence Cloud connector includes the following custom data filter for Copilot Search:

- Space

## Permissions model and access control

You can configure the Confluence Cloud connector to enforce that only users who have access to a Confluence item can see it in Copilot responses and search results. The system uses the Confluence access control list (ACL) for spaces and pages.

The Confluence Cloud connector (and the Confluence on-premises connector) honor the same permission setup as the data source. This means that if a user can see content in Confluence, they can see it in Copilot and Microsoft Search results. If they don't have access in Confluence, the content won't appear in their results.

You can control permissions in the following ways:

- **Space permissions and page restrictions** – If a page has specific view restrictions, the page is only visible to authorized users in responses and search results. If no page-level restriction exists, the connector applies the Confluence space permissions settings. If a space is open to all Confluence users (or has anonymous access enabled), content from that space is available to all users in the organization. If the space is restricted to certain groups, only those groups members get results from that space. Content with no applicable permission information is not shown to any users to prevent accidental exposure.

- **User identity mapping** - The connector maps Confluence user accounts to Microsoft 365 (Entra ID) identities. If Confluence users' emails match their Entra ID UPNs, this mapping is automatic. If they differ, you can provide a mapping rule to map identities in Confluence to identities in Microsoft 365. For more information, see [Map your non-Entra ID identities](map-non-entra-id.md). This ensures that the system provides appropriate access to Confluence content in responses.

- **Visible to everyone option** - You can choose not to enforce per-user permissions (setting the connector to index content as **Visible to everyone**). In that case, all indexed Confluence data is searchable by any user in the tenant. This works for non-confidential knowledge bases. However, for most scenarios, we recommend using the restricted mode so that results mirror the Confluence permission boundaries.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Confluence Cloud connector](confluence-cloud-deployment.md)
