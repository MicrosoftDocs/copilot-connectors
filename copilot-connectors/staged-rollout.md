--- 
ms.date: 10/26/2023
title: "Staged rollout for Microsoft 365 Copilot connectors" 
ms.author: souravpoddar 
author: souravpoddar 
manager: srramam
audience: Admin
ms.audience: Admin 
ms.topic: how-to
ms.service: copilot-connectors 
ms.localizationpriority: medium 
description: "Use Stage Rollout to gradually roll out a Microsoft 365 Copilot connector to your users." 
---

# Staged rollout for Microsoft 365 Copilot connectors

Staged rollout is a feature that allows you to gradually introduce Microsoft 365 Copilot connectors to a select group of users in your production environment. You can use it to deploy an existing or new connection to a limited set of users, monitor the performance, and adjust settings as needed. You can expand or shrink the scope of the rollout at any time. When you're ready, you can end the staged rollout and deploy the connection to the entire organization (or to all applicable users).

> [!NOTE]
> **Microsoft 365 Copilot connectors** enable you to connect and index data from various external sources, such as ServiceNow, Salesforce, Azure Data Lake Storage, Jira Cloud, Confluence Cloud, and more. With Copilot connectors, you can enrich your Microsoft Search experience with relevant and diverse content from your organization. For details about how to set up Copilot connectors, see [Deploy Microsoft 365 Copilot connectors](deployment-overview.md).

This document guides you through the steps to apply staged rollout to a Microsoft Graph connection, and also how to edit staging settings when needed.

>[!IMPORTANT]
>* Staged rollout settings are applicable to all Search and Copilot experiences.
>* You must be a Search Admin or a Global Admin to access this feature.


<!---## Steps to apply staged rollout to a connection-->
## Apply staged rollout to a connection

Go to the [Microsoft 365 admin center](https://admin.microsoft.com) and complete the following steps to apply a staged rollout to a Copilot connector.


1. **Go to the Search & Intelligence portal**. Choose **Show all** on the left panel and under **Settings**, select **Search & Intelligence**.

<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup 
instructions.-->

1. Go to the **Connectors** tab and select the connection that you want to apply staged rollout to. 

1. After you configure all the connection settings, on the **Review & Publish** step, click on the button **Publish to limited users**. This allows you to deploy the connector to a limited audience.

   ![Publish to limited users.](media/Staged_Rollout_Publish_limited_users.png)

2. Add the users or security groups to whom you want to give access to the connector. Currently, you can add up to **100 users and 15 Microsoft 365 groups**. For details, see [Overview of Microsoft 365 Groups for administrators](/microsoft-365/admin/create-groups/office-365-groups).

   ![Add user or M365 groups.](media/Staged_Rollout_add_users.png)


5. After you add the list of users or groups for a given connection, choose **Save** to apply your changes. The portal shows you a confirmation screen with the list of users and groups included in the deployment.

   ![Review changes.](media/Staged_Rollout_review_changes.png)

6. Choose **Publish to limited users** to complete the connection set-up.

   The portal starts the staged rollout process. Depending on the size of your organization and the number of users selected, the rollout process might take some time. You can check the status on the **Display all connections** section on the **Connectors** tab. After the connection is published, only the users who are included in the rollout will be able to see the connector results (if they have access permissions) in Microsoft Search.

<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup 
instructions.-->

## Modify or stop staged rollout

To modify the staged rollout settings for a connector:

1. On the **Connectors** page of the admin center, on the **Your connections** tab, check the status in the **Staged rollout** column. Connections that are currently staged show the status **Staged**.
2. Choose **Edit** to add or remove users from the staged rollout.

### Stop the staged rollout
If you want to stop the staged rollout and you're ready to deploy the connection to the organization, in the **Staged rollout** column, choose **Edit**. On the **Staged rollout** settings panel, choose **End staging**.

In the confirmation modal, choose **End** to confirm the action. Note that when you end staging, the connection results start appearing to everyone in the organization or those who have access to the items. This depends on the option you chose when you [deploy the connection](deployment-overview.md).

![End staging option.](media/Staged_Rollout_end_staging.png)

## Limitations

The staged rollout feature has the following limitations:

- You can only add up to 100 users and 15 Microsoft 365 groups to the staged rollout list.
- The staged rollout settings are currently only applicable to Search and Copilot experiences.

