---
title: "BambooHR connector overview"
ms.author: danielabo
author: danipocket
manager: calvind
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: microsoft-365-copilot-connectors
ms.date: 08/17/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the BambooHR Microsoft 365 Copilot connector."
---

# BambooHR connector overview

The BambooHR Microsoft 365 Copilot connector enables organizations to index employee profiles from BambooHR into Microsoft Graph, making them accessible across Microsoft 365 experiences including Microsoft 365 Copilot and Microsoft Search. The connector is a [Microsoft 365 Copilot connector for people data](/graph/peopleconnectors) that syncs core employee profile information — names, contact details, job titles, departments, hire dates, and organizational hierarchy.

> [!VIDEO https://www.youtube-nocookie.com/embed/kpzXm_eKKkg]

## Why use the BambooHR connector to index your data?

The BambooHR connector is designed for organizations that use BambooHR as their HR system of record. Common scenarios and use cases include:

- Enable natural language queries about colleagues via Copilot (for example, "Who manages the Finance team?").
- Keep employee directory information current with near-real-time incremental syncing.
- Enhance organizational awareness by surfacing BambooHR profile data across Microsoft 365 apps.
- Reduce tool switching — users discover colleague information without leaving Teams, Outlook, or SharePoint.
- Support semantic people search based on departments, locations, and organizational relationships.

## Build agents with the BambooHR connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that users can use to retrieve information from BambooHR:

- Who is the head of the Marketing department?
- Show me all employees in the Engineering division.
- Who was recently hired in the North America division?
- What is John Smith's job title and department?
- Find colleagues in the Seattle office.
- Who reports to Sarah Johnson?

## BambooHR connector capabilities and limitations

The BambooHR connector enables you to:

- Index comprehensive employee profiles including names, contact details, job titles, departments, hire dates, and organizational hierarchy from BambooHR.
- Use natural language queries about colleagues through Microsoft 365 Copilot.
- Perform semantic search to find relevant colleagues based on keywords, skills, departments, locations, and organizational relationships.
- Synchronize employee data in near real time with incremental syncs every 15 minutes and full syncs daily.
- Map BambooHR identities to Microsoft Entra ID users automatically by matching email addresses.

The BambooHR connector has the following limitations:

- Data indexing is limited to core employee profile information. It doesn't index time off, documents, benefits, trainings, assets, notes, emergency contacts, onboarding, offboarding, and custom properties.
- Everyone in the Microsoft tenant can access all indexed profile data. Granular user-level permission controls aren't currently available.
- Identity mapping requires work email addresses in BambooHR to match UserPrincipalName (UPN) or email addresses in Microsoft Entra.
- Schema configuration uses a predefined set of properties; you can't add custom properties.
- It only indexes active employees. BambooHR treats employees without a populated hire (or original hire) date as inactive.

> [!NOTE]
> When you ask Copilot about a person, the citation appears as **office.com** instead of **BambooHR**, because profile information in Microsoft 365 can come from multiple sources. For example, job titles might come from BambooHR, while names and other details might come from Microsoft Entra or other connected systems.

## Data types indexed from BambooHR

The BambooHR connector indexes employee profile data. The following table lists the schema properties that the connector indexes.

| Schema property | Description |
|---|---|
| First name | Employee's first name |
| Last name | Employee's last name |
| Name | Employee's full name (display name) |
| Email | Employee's work email address |
| Birth date | Employee's date of birth |
| Job information department | Employee's department |
| Job information division | Employee's division |
| Employee number | Employee's number |
| Employee Eeid | Employee's ID in BambooHR |
| Employment status | Employment status (full-time, contractor, etc.) |
| Original hire date time | Employee's original date of hire |
| Hire date time | Employee's hire date (used when original hire date is null) |
| Job information job title | Employee's job title |
| Supervisor ID | Employee's manager identifier |
| Mobile phone | Employee's work mobile phone |
| Work phone | Employee's work phone |
| Job information location | Employee's office location |
| Status | Active/inactive (internal filtering only) |

## Permissions model and access control

Manage permissions to BambooHR data in Copilot and search results as follows:

- Everyone in the Microsoft tenant can access all profiles that the BambooHR connector indexes.
- The connector uses Microsoft Entra ID for identity mapping and matches BambooHR work email addresses to UPN or email in Microsoft Entra.
- If you block a user from viewing another user's profile in Microsoft 365, the blocked user can't see BambooHR data.
- Future updates will include granular user-level permission controls.


## Next step

> [!div class="nextstepaction"]
> [Deploy the BambooHR connector](bamboohr-deployment.md)
