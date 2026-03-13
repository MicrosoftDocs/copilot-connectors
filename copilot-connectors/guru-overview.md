---
title: "Guru Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: rantang
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 11/24/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the Guru Microsoft 365 Copilot connector."
---

# Guru Microsoft 365 Copilot connector overview

The Guru Microsoft 365 Copilot connector integrates Guru content into Microsoft 365, allowing Microsoft 365 Copilot, and Microsoft Search experiences to surface relevant Guru Cards directly within apps like Teams, Outlook, and SharePoint. When you configure the Guru connector for your organization and index data from the Guru instance, users can search for Guru content in Microsoft Search, Microsoft 365 Copilot, and Copilot Search.

## Why use the Guru connector to index your data?

Organizations that use Guru for internal Cards often face knowledge silos and inefficient search workflows. The Guru Copilot connector addresses these problems by integrating Guru content into Microsoft 365. This integration allows employees to surface Guru Cards through Copilot, Copilot Search, and Microsoft Search—in everyday apps like Teams, Outlook, or SharePoint—without leaving their flow of work. The result is a more connected knowledge ecosystem that drives productivity and collaboration.

The Guru Copilot connector provides the following benefits:

- **Boosts productivity**: Employees access Guru content directly within Microsoft 365 apps, reducing time spent searching and switching platforms.
- **Improves decision-making**: Unified search across Guru and Microsoft tools ensures faster access to institutional knowledge, enabling more informed and timely decisions.
- **Enhances collaboration**: Cross-functional teams discover and utilize each other's Guru content, reducing duplication and improving alignment.
- **Frictionless knowledge discovery**: Empower employees to search, summarize, and generate content from internal knowledge—such as policies, SOPs, and best practices—to support faster execution across various workflows.
- **Secure, contextual knowledge delivery**: Surface relevant information with full respect to access controls, ensuring the right people get the right knowledge at the right time.

## Use cases

The following table lists common use cases for the Guru connector.

| **Department/role**       | **Use case**                                                | **Business benefit**                                |
|---------------------------|------------------------------------------------------------|-----------------------------------------------------|
| People                   | Summarize onboarding guides, policies, FAQs               | Faster onboarding; reduced dependency on HR staff. |
| IT support/help desk     | Retrieve troubleshooting steps or runbooks from Guru via Copilot | Faster ticket resolution; improved consistency.    |
| Engineering/DevOps       | Access design docs, retrospectives, deployment guides     | Reduced context switching; faster execution.       |
| Product management       | Query release plans, feature specs, team Cards           | Better alignment; faster planning cycles.          |
| Sales/marketing          | Discover case studies, messaging docs, campaign plans    | Improved collaboration; reduced duplicated work.   |
| Executives/managers      | Ask Copilot for summaries of policy or project updates   | Faster decision-making; better visibility.         |
| Customer Support         | Easily access accurate knowledge—product details, policies, and troubleshooting guides | Resolve issues efficiently.                        |
| All Employees            | Self-serve to discover and apply internal knowledge—such as benefits info, SOPs, IT instructions, and best practices | Empowering faster and more informed decision-making.|

## Build agents with the Guru connector

Developers can use this connector as a knowledge source in declarative agents they build with [Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/copilot-studio-lite), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Eaxmple prompts

The following examples show prompts that users can use to retrieve information from Guru:

- **People/HR**: Summarize the onboarding process for new hires in the engineering team, including links to relevant Guru Cards.  
- **IT Support/Help desk**: Find the runbook for resolving VPN connectivity issues and summarize the steps.  
- **Engineering/DevOps**: Summarize the architecture of the new microservices deployment from the last retrospective.  
- **Product management**: List all feature specs in the collection of 'vNext' and summarize their status.  
- **Sales/marketing**: Summarize the messaging framework for the Contoso campaign and link to the case studies.  
- **Executives/managers**: Summarize the latest project updates across all teams from Guru.  

## Connector capabilities and limitations

The Guru connector has the following key capabilities:

- **Indexes core Guru content**: Crawls Guru Cards from all collections by default.
- **Integrates with Copilot**: Enables Copilot and Microsoft Search to find and use Guru content. Users can ask questions in natural language and get answers that include information from Guru Cards, with reference links back to the source.
- **Respects Guru permissions**: The connector only shows content to users who have access in Guru. It honors Guru's access control, so responses and search results don't expose Cards to unauthorized users.
- **Configurable content scope**: Admins can control what Guru data is indexed. Use the Guru Query Language (GQL) to filter your data before it's indexed.

The Guru connector has the following limitations:

- **Permission updates latency**: Changes to user or group access in Guru aren't reflected immediately in the Copilot index. Permission changes are picked up only during a full crawl (once every 24 hours by default), not during the 15-minute incremental syncs.
- **Identity mapping requirement**: The connector relies on matching Guru user identities to Microsoft Entra ID accounts to enforce permissions. If your Guru users' email IDs don't exactly match their Entra ID user principal names (UPNs), an admin must configure a manual identity mapping.

## Data types indexed from Guru

The Guru connector indexes Guru Cards so they can be used in Copilot, Copilot Search, and Microsoft Search.

## Permissions model and access control

You can configure the Guru connector to enforce that only users who have access to a Guru item can see it in Copilot responses and search results. The system uses the Guru access control list (ACL) for collections, folders, and cards. You can control permissions in the following ways:

- **Align with Guru access control mechanism**: Visibility depends on the union of permissions set at the collection, folder, and card levels.
- **User identity mapping**: The connector maps Guru user accounts to Microsoft 365 (Microsoft Entra ID) identities. If Guru users' emails match their Entra ID user principal names (UPNs), this mapping is automatic. If they differ, you can provide a mapping rule.
- **Visible to everyone option**: You can choose not to enforce per-user permissions (setting the connector to index content as **Visible to everyone**). In that case, all indexed Guru data is searchable by any user in the tenant.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Guru connector](guru-deployment.md)