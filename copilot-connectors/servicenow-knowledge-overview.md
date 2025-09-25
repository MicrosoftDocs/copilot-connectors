---
title: "ServiceNow Knowledge Microsoft 365 Copilot connector overview"
ms.author: lauragra
author: lauragra
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 09/25/2025
ms.localizationpriority: Medium
description: "Learn about the capabilities, limitations, and use cases for the ServiceNow Knowledge Copilot connector."
---

# ServiceNow Knowledge Copilot connector overview

The ServiceNow Knowledge Microsoft 365 Copilot connector enables organizations to index ServiceNow knowledge base (KB) articles into Microsoft 365 Copilot and search experiences. When you index ServiceNow knowledge base content, users can retrieve relevant information using natural language queries across Microsoft 365 apps. This connector enhances productivity by surfacing IT service management data directly in Copilot, streamlining workflows and improving decision-making.

## Why use the ServiceNow Knowledge connector to index your data?

The ServiceNow Knowledge connector is ideal for organizations that rely on ServiceNow for IT operations, HR services, and customer support. Common use cases include:

- Enabling employees to query ticket status, incident history, and service requests directly from Copilot.
- Allowing HR teams to access onboarding workflows and policy documents.
- Empowering support agents to retrieve troubleshooting steps and resolution logs.

This connector helps reduce context switching and improves access to operational data across departments.

## Use cases

Enable your users to ask questions related to your IT/HR workflows in Copilot, such as:

   - How can I request a new device?
   - How do I create a new VPN connection?
   - How do I apply for leaves?

## Build agents with the ServiceNow Knowledge connector

Developers can use the ServiceNow Knowledge connector as a knowledge source in declarative agents built with the [Microsoft Copilot Studio full experience](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), the [Microsoft Copilot Studio lite experience](/microsoft-365-copilot/extensibility/copilot-studio-lite), or the [Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Agent prompts

The following examples show prompts that agent builders can use to help users retrieve information from ServiceNow.

| Department | Role | Example Prompt |
|------------|------|----------------|
| IT         | Support Analyst | "Show me all open incidents assigned to me this week." |
| HR         | Manager | "What is the onboarding status for new hires in September?" |
| Operations | Admin | "List all service requests pending approval." |

## ServiceNow Knowledge connector capabilities and limitations

The ServiceNow Knowledge connector has the following capabilities:

- Indexes all types of knowledge articles.
- Enables Copilot and search experiences in Microsoft 365 to respond to user questions related to your IT/HR workflows in Copilot.
- Uses [semantic search in Copilot](semantic-index-for-copilot.md) to enable users to find relevant content based on keywords, personal preferences, and social connections.
- Supports  [advanced user criteria permissions](https://docs.servicenow.com/bundle/xanadu-servicenow-platform/page/product/knowledge-management/task/create-user-criteria-record-in-knowledge-management.html).
- Enables customization of the ServiceNow URL in Copilot responses as needed for your organization.

The ServiceNow Knowledge connector has the following limitations:

- If both knowledge base and knowledge article-level permissions are defined, only the article-level permissions are honored. Knowledge base-level permissions are disregarded and therefore don't apply to the articles.
- The connector doesn't index attachments on KB articles.
- The connector doesn't support reading content from default or custom knowledge article templates, such as FAQs, How-to, What Is, or KCS article templates.

## Data types indexed from ServiceNow Knowledge

The connector indexes structured data from ServiceNow, including:

- Incident records
- Service requests
- HR workflows
- Knowledge base articles

Indexed content is surfaced in Copilot responses and Microsoft Search results, enabling contextual access to enterprise data.

## Permissions model and access control

Access to indexed ServiceNow data is governed by access control lists (ACLs) configured in ServiceNow. Admins can manage permissions to ensure that only authorized users can view specific data types in Copilot and search experiences.

## Next step

> [!div class="nextstepaction"]
> [Deploy the ServiceNow Knowledge connector](servicenow-knowledge-deployment.md)
