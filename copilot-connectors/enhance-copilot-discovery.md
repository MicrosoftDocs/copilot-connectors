---
ms.date: 06/17/2024
title: "Enhance Copilot Discovery with Microsoft 365 Copilot connectors content"
ms.author: souravpoddar
author: souravpoddar001
manager: harshkum
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: "Enhance the discoverability of Microsoft 365 Copilot connectors' content within Microsoft Copilot."
---

# Enhance Copilot discovery with Microsoft 365 Copilot connectors content

This article describes how to optimize Microsoft 365 Copilot connector connection names and descriptions to enhance Copilot discovery of the connector content. Choose a meaningful connection name and description to help Copilot better match the connector content to the user's request. 

## Connection name

Assign a **representative and concise name** to each connection. The connection name should reflect the nature and intended use of the content to help users identify and access the relevant information.

## Connector description

You can **modify the connection name and description** for Microsoft-built connectors in the admin portal at any time to reflect updates or changes to the content. Updates are usually reflected within minutes. 

> [!Note]
> To update descriptions for on-premises connectors, use the Copilot connectors API. For more information, see [Update externalConnection](/graph/api/externalconnectors-externalconnection-update)

To update the connector description:

1. In the Microsoft 365 admin center, go to **Settings** > **Copilot** > **Connectors**.
2. Select [Data sources](https://admin.microsoft.com/#/copilot/connectors).
3. Select the connector that you want to update the description for and choose **Edit** on the bottom right.

      [![Screenshot that shows Connection details pane.](/MicrosoftSearch/media/connection-details-pane.png)](/MicrosoftSearch/media/connection-details-pane.png#lightbox)

4. The **Name the connection** page includes fields for the **Connection name** and **Description**. Update the name or description to best fit your organization's scenarios.

      [![Screenshot that shows Update the connection description](/MicrosoftSearch/media/update-the-connection-description.png)](/MicrosoftSearch/media/update-the-connection-description.png#lightbox)

> [!Note]
> Copilot connectors for Jira, ServiceNow Tickets, ADO Work Items, and Salesforce have default generic descriptions. We recommend that you review and modify the descriptions to use the specific terms and language that apply to your organization.
  
### Best practices for connector descriptions

The connector description helps users to locate the content they're looking for. Include the following elements in your description:

* A brief overview of the content type. 
* The scope of the content available within the connection. 
* Keywords that users might use to find the content (for example, tickets, wiki, knowledge base, How to).
* Alternative names for the connection that users might be familiar with. 

The following table shows some examples of effective connector descriptions.

| Connector | Description |
| --------- | ----------- |
| Jira | This connection to Jira contains tickets to track issues related to software development and business project management. Jira may also be used for service desk tickets, product management, and other daily work item management. It is used to run scrums and track progress on initiatives, especially within engineering and product teams.<br /><br />Keywords: Issues, Bugs, Tasks, Sub-tasks, Epic, User Story, Tickets, Backlog, Atlassian Jira |
| ServiceNow Tickets | This connection is used to manage and track customer requests and IT incidents. Businesses use this tool to enhance their service delivery and ensure issues are resolved on time. |
| ADO Work Items | This connection to Azure DevOps Work items contains tickets to track software development and business projects. It is used by engineering and product teams to track daily work, run scrums and track progress on initiatives.<br /><br />Keywords: Work items, Bugs, Tasks, Epic, User Story, Tickets, Backlog, Issue, ADO, Azure DevOps |
| Salesforce | Salesforce CRM stores a wide range of data to support various business functions. Types of data stored in Salesforce CRM include common record categories such as Leads, Accounts, Contacts, Opportunities, and Cases. Salesforce CRM's data model is designed to make data understandable and accessible, representing database tables as objects, columns as fields, and rows as records.<br /><br />The content in this connection can also be referred to as SFDC, Salesforce data or Salesforce Sales cloud. |
| BambooHR | This connection to BambooHR people data populates profiles of people in Microsoft 365 Copilot experiences like Teams or CoPilot. It's used to see or query about e.g., titles, emails, managers, and other people-related data. |

## Related content

- [Deploy Copilot connectors](deployment-overview.md)