---
title: "ServiceNow Knowledge connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: mayanksethi
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 08/23/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the ServiceNow Knowledge Copilot connector."
---

# ServiceNow Knowledge Copilot connector overview

The ServiceNow Knowledge Microsoft 365 Copilot connector enables organizations to index ServiceNow knowledge base (KB) articles into Microsoft 365 Copilot and search experiences. When you index ServiceNow knowledge base content, users can retrieve relevant information using natural language queries across Microsoft 365 apps. This connector enhances productivity by surfacing IT service management data directly in Copilot, streamlining workflows and improving decision-making.

## Why use the ServiceNow Knowledge connector to index your data?

The ServiceNow Knowledge connector is ideal for organizations that rely on ServiceNow for IT operations, HR services, and customer support. Organizations can use the connector to:

- Enable employees to query ticket status, incident history, and service requests directly from Copilot.
- Allow HR teams to access onboarding workflows and policy documents.
- Empower support agents to retrieve troubleshooting steps and resolution logs.

This connector helps reduce context switching and improves access to operational data across departments.

### Use cases

Enable your users to ask questions related to your IT/HR workflows in Copilot, such as:

- How can I request a new device?
- How do I create a new VPN connection?
- How do I apply for leaves?

## Build agents with the ServiceNow Knowledge connector

Developers can use the ServiceNow Knowledge connector as a knowledge source in declarative agents built with [Microsoft Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [Agent Builder in Microsoft 365 Copilot](/microsoft-365/copilot/extensibility/agent-builder), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts

The following examples show prompts that agent builders can use to help users retrieve information from ServiceNow.

| Department | Role | Example Prompt |
|------------|------|----------------|
| IT         | Support Analyst | "Show me all open incidents assigned to me this week." |
| HR         | Manager | "What is the onboarding status for new hires in September?" |
| Operations | Admin | "List all service requests pending approval." |

## Connector capabilities and limitations

The ServiceNow Knowledge connector has the following capabilities:

- Indexes all types of knowledge articles.
- Enables Copilot and search experiences in Microsoft 365 to respond to user questions related to your IT/HR workflows in Copilot.
- Uses [semantic search in Copilot](/microsoftsearch/semantic-index-for-copilot) to enable users to find relevant content based on keywords, personal preferences, and social connections.
- Supports evaluation of [advanced script-based user criteria permissions](https://docs.servicenow.com/bundle/xanadu-servicenow-platform/page/product/knowledge-management/task/create-user-criteria-record-in-knowledge-management.html).
- Indexes comments on knowledge articles.
- Indexes attachments on knowledge articles, including documents that are hyperlinked or embedded within the article body.
  - Supported attachment formats include:
    - Microsoft Office files (Word, Excel, PowerPoint, OneNote)
    - OpenDocument files
    - PDFs
    - Text and markup files (TXT, Markdown, HTML, XML, XPS)
    - Web page archives (MHT, MHTML)
    - Email messages (EML, MSG)
    - ZIP archives
- Indexes only attachments that are visible to users in your ServiceNow instance.
- Supports indexing content from custom or default knowledge article templates, such as FAQs, How-to, What Is, or KCS article templates.
- Supports customization of the ServiceNow URL in Copilot responses as needed for your organization.
- Considers both knowledge base-level and article-level permissions (user criteria) when evaluating article permissions.
- Supports evaluating permissions based on user criteria or role-based permissions. 
- For Advanced flow connections, supports incremental identity sync to keep identity changes - such as users, role assignments, group memberships, and user criteria attributes - up to date between full crawls.
- Indexes knowledge blocks—the reusable, modular content components embedded within knowledge articles—and evaluates their user criteria. Indexing knowledge blocks requires additional table permissions. For more information, see [Create service account and set up permissions to index items](servicenow-knowledge-admin-setup.md#create-service-account-and-set-up-permissions-to-index-items).
- Indexes content contained in accordions within knowledge articles.

The ServiceNow Knowledge connector has the following limitations:

- Image files aren't indexed as attachments. Formats such as .png, .jpg, .jpeg, .gif, .bmp, and .svg are skipped; only text-based document formats are indexed.
- Each knowledge article indexes a maximum of 100 attachments, up to a combined size of 64 MB. Attachments beyond these limits aren't indexed.

## Data types indexed from ServiceNow Knowledge

The connector indexes structured data from ServiceNow knowledge base articles.

Indexed content is surfaced in Copilot responses and Microsoft Search results, enabling contextual access to enterprise data.

## Permissions model and access control

Access to indexed ServiceNow data is governed by access control lists (ACLs) and user criteria configured in ServiceNow. Admins can manage permissions to ensure that only authorized users can view specific data types in Copilot and search experiences.

## Next step

> [!div class="nextstepaction"]
> [Deploy the ServiceNow Knowledge connector](servicenow-knowledge-deployment.md)