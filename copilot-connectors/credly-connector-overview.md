---
title: "Credly connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 04/09/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Credly Microsoft 365 Copilot connector."
---

# Credly Copilot connector overview

The Credly Microsoft 365 Copilot connector integrates digital credential data from your organization's Credly account into Microsoft 365, enabling Copilot and profile cards to surface verified badges, awards, and certifications directly within apps like Teams, Outlook, and SharePoint.

When you configure the Credly connector for your organization and index data from Credly, employees' verified credentials are enriched in their Microsoft 365 user profiles. The Credly connector content can bring improved visibility into employee qualifications, faster identification of subject-matter experts, and enhanced collaboration across your organization.

> [!NOTE]
> The Credly connector is currently released as a Preview feature. Its functionality and requirements might change in future updates.

## Why use the Credly connector to index your data?

Organizations that use Credly for digital credentials and badges often lack a centralized way to surface employees' qualifications within their daily workflow tools. The Credly Copilot connector addresses this problem by integrating Credly credential data into Microsoft 365. This allows employees to discover colleagues' badges, awards, and certifications through Copilot and profile cards--without leaving their flow of work. The result is a more transparent view of your workforce's skills and achievements that drive collaboration and informed decision-making.

The Credly Copilot connector provides the following benefits:

- **Boosts profile visibility** - Employees' verified digital badges, awards, and certifications appear on their Microsoft 365 profile cards automatically, without manual data entry.
- **Enhances Copilot responses** - Copilot can answer natural-language questions about colleagues' qualifications and achievements based on their Credly credentials.
- **Keeps data current** - The connector performs incremental crawls daily and full crawls weekly by default, so newly earned badges are reflected in Microsoft 365 automatically.
- **Simplifies identity matching** - The connector maps each Credly badge to the correct Microsoft 365 user by matching email addresses with Microsoft Entra ID accounts.
- **Preserves security and compliance** - Badge data follows existing information barriers and privacy settings in your tenant.

### Use cases

The following table lists common use cases for the Credly connector.

| Department/role | Use case | Business benefit |
|:---|:---|:---|
| HR/People operations | View employee certifications and awards across the organization. | Identify qualified team members without manual tracking. |
| Project managers | Ask Copilot "Who on my team has a project management badge?" | Quickly find the right people for project assignments. |
| Hiring managers | Review a colleague's verified credentials on their profile card. | Validate qualifications at a glance during collaboration. |
| IT administrators | Monitor which employees hold security or compliance certifications. | Ensure teams meet compliance requirements. |

### Example prompts

The following examples show prompts that users can use to retrieve credential information from Credly.

**Discover credentials**

- "What certifications does Jane Doe have?"
- "Show me badges earned by my team members."

**Find experts**

- "Who in my department has an Azure certification?"
- "Which colleagues have a project management badge?"

## Connector capabilities and limitations

The Credly connector has the following key capabilities:

- **Indexes credential data** – Ingests badge names, descriptions, issuing organization, issue dates, and other relevant metadata into each user's Microsoft 365 profile.
- **Integrates with profile cards** – Displays badges in a dedicated **Awards and Certifications** section on users' profile cards, with links to view details on Credly's site.
- **Integrates with Copilot** – Enables Copilot to find and use Credly credential data. Users can ask questions in natural language and get answers that include information from Credly badges, with reference links back to the source.
- **Automated identity resolution** – Maps Credly badge owners to Microsoft Entra ID accounts by matching email addresses (UPN or primary SMTP address).
- **Periodic synchronization** – Runs incremental crawls daily and full crawls weekly to keep credential data up to date.

The Credly connector has the following limitations:

- **Awards and certifications only** – The connector indexes only badge data that users publicly accept or share on their Credly profiles. Private badges, badge evidence, related skills, user social profiles, and other noncredential data aren't indexed.
- **Broad access permissions** – All imported badge data is visible to everyone in your organization by default. Granular per-user or group filtering isn't available in this release.
- **Identity mapping requirement** – The connector relies on matching Credly user email addresses to Microsoft Entra ID accounts. If a Credly user's email doesn't exactly match their Entra ID UPN or primary SMTP address, those badges can't be mapped to a Microsoft 365 user profile and are skipped during indexing.
- **Fixed schema** – The connector uses a predefined set of profile attributes (**Awards** and **Certifications** properties in Microsoft Graph). You can't add or remove properties in this release.
- **Active users only** – The connector only indexes credentials for active, licensed users. Badges for inactive users are filtered out.
- **One organization per connection** – Each connector instance supports a single Credly Organization ID. Set up separate instances for multiple Credly organizations.

> [!NOTE]
> When Copilot cites Credly provided profile data, the source appears as office.com. Microsoft 365 aggregates profile data from multiple sources and attributes responses to the unified profile endpoint.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Credly Copilot connector](credly-connector-deployment-guide.md)

## Related content

- [Troubleshoot the Credly connector](credly-connector-troubleshoot.md)
- [Microsoft 365 Copilot connectors for people data](https://learn.microsoft.com/en-us/graph/peopleconnectors)
- [Microsoft 365 Copilot connectors overview](https://learn.microsoft.com/en-us/microsoftsearch/connectors-overview)
