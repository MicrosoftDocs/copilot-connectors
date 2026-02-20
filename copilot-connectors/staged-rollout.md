--- 
ms.date: 02/12/2026
title: "Staged rollout for Microsoft 365 Copilot connectors" 
ms.author: souravpoddar 
author: souravpoddar 
manager: srramam
audience: Admin
ms.audience: Admin 
ms.topic: how-to
ms.service: copilot-connectors 
ms.localizationpriority: medium 
description: "Use staged rollout to gradually introduce a Microsoft 365 Copilot connector to users in your organization. Staged rollout allows you to test, monitor, and adjust settings before deploying a connector to your organization." 
---

# Staged rollout for Microsoft 365 Copilot connectors

Staged rollout of Microsoft 365 Copilot connectors allows you to gradually introduce a connector to a select group of users in your production environment. You can use it to deploy an existing or new connection to a limited set of users, monitor the performance, and adjust settings as needed. You can expand or reduce the scope of the rollout at any time. When you're ready, you can end the staged rollout and deploy the connection to the entire organization (or to all applicable users).

For information about how to set up Copilot connectors, see [Deploy Microsoft 365 Copilot connectors](deployment-overview.md).

This article describes how to apply staged rollout to a Copilot connector and how to edit staged rollout settings.

>[!IMPORTANT]
>* Staged rollout settings are applicable to all Search and Copilot experiences.
>* You must be an AI administrator to access this feature.

## Apply staged rollout to a new connection

Complete the following steps to apply a staged rollout to a new connection:

1. In the [Microsoft 365 admin center](https://admin.microsoft.com), go to **Copilot** > **Connectors**. 
1. On the **Gallery** tab, choose the connector that you want to deploy.
1. Configure the connection settings as described in the [Deployment overview](deployment-overview.md) article.
1. Select the toggle next to **Rollout to limited audience**.
1. Add the users or security groups that you want to have access to the connector. You can add up to 100 users and 15 Microsoft 365 groups.
5. Choose **Create** to create the connection. When the rollout finishes, only the users and groups you specified see connector data in results, depending on their permissions. 

:::image type="content" alt-text="Screenshot of the Rollout to a limited audience toggle on the connector setup page." source="media/staged-rollout/staged-rollout.png" lightbox="media/staged-rollout/staged-rollout.png":::

## Modify staged rollout

To modify the staged rollout settings for a connector:

1. In the [Microsoft 365 admin center](https://admin.microsoft.com), go to **Copilot** > **Connectors** > **Your Connections**.
1. Find the connector that you want to modify.
1. In the **Staged Rollout** column, next to **Staged**, choose **Edit**.
1. Add or remove users and groups from the staged rollout, and choose **Save**.

:::image type="content" alt-text="Screenshot of the Staged Rollout pane for a configured connector." source="media/staged-rollout/modify-staged-rollout.png" lightbox="media/staged-rollout/modify-staged-rollout.png":::

### Stop staged rollout

To stop a staged rollout for a connector:

1. In the [Microsoft 365 admin center](https://admin.microsoft.com), go to **Copilot** > **Connectors** > **Your Connections**.
1. Find the connector that you want to modify.
1. In the **Staged Rollout** column, next to **Staged**, choose **Edit**.
1. Choose **End Staging**, and when prompted, choose **Remove**.

:::image type="content" alt-text="Screenshot of the Staged Rollout pane with End Staging highlighted." source="media/staged-rollout/end-staged-rollout.png" lightbox="media/staged-rollout/end-staged-rollout.png":::

> [!NOTE]
> When you remove staged rollout, the connection results start appearing to all users in the organization who have access.

## Staged rollout limitations

The staged rollout feature has the following limitations:

- You can only add up to 100 users and 15 Microsoft 365 groups to the staged rollout list.
- The staged rollout settings are currently only applicable to Search and Copilot experiences.

## Related content

- [Deployment overview](deployment-overview.md)

