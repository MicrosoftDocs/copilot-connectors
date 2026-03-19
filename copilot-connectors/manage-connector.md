---
title: "Manage Microsoft 365 Copilot connectors"
ms.author: danielabo
author: danielabom
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Manage your Microsoft 365 Copilot connector connection state and index quota utilization."
ms.date: 03/19/2026
---

# Manage Microsoft 365 Copilot connector connections

Microsoft 365 Copilot connectors extend the reach of Microsoft 365 Copilot and Microsoft Search experiences by connecting to data beyond Microsoft 365. This article describes how to manage your connections after you [deploy them in the admin center](deployment-overview.md).

To access and manage your Microsoft 365 Copilot connectors, you must be an AI administrator for your organization. 

## Supported connection operations

For each connector type, the Microsoft 365 admin center supports the following operations.

|Operation | Connectors by Microsoft | Connectors by partners
|:--- |:-------- |:---|
|Add a connection | :heavy_check_mark: | :x: (Refer to partner or custom-built connector admin documentation)|
|Delete a connection | :heavy_check_mark: | :heavy_check_mark:|
|Edit a published connection | :heavy_check_mark: Name and description<br></br> :heavy_check_mark: Connection settings<br></br> :heavy_check_mark: Property labels<br></br> :heavy_check_mark: Schema<br></br> :heavy_check_mark: Refresh schedule<br></br> :heavy_check_mark: Query string (as applicable)<br></br> :heavy_check_mark: Advanced criteria (as applicable)<br></br> | :heavy_check_mark: Name<br></br> :heavy_check_mark: Description |
|Edit a draft connection | :heavy_check_mark: | :x:|

## Monitor your connection state

You can view the connection state for your deployed connectors on the **Your Connections** tab in the admin center. The state shows in the **Connection state** column. One of the following states is displayed for each connection:

- Syncing - The connector crawls the data from the source to index the existing items and make any updates.
- Ready - The connection is ready, and there's no active crawl running against it. **Last sync time** indicates when the last successful crawl happened. The connection is as fresh as the last sync time.
- Paused - The crawls are paused by the admin via the **Pause** button on the connector page. The next crawl runs  when it's manually resumed. However, the data from this connection continues to be searchable.
- Failed - The connection had a critical failure. This error requires manual intervention. The admin needs to take appropriate action based on the error message shown. Data that was indexed until the error occurred is searchable. 
- Delete failed - The deletion of the connection failed. Based on the failure reason, the data might still be indexed, item quota might still be consumed, and crawls might still run for the connection. We recommend that you try deleting the connection again when this state occurs.
  
## Manage visibility of partner data sources in Copilot

Admins can control the visibility of partner connectors in Copilot and Copilot Search via a simple toggle. This feature enhances data governance and the user experience by allowing selective exposure of indexed content. If the connection is off, it can still crawl the data source, but the data isn't used for search results.

To manage visibility of data sources in Copilot:

- Go to **Copilot** > **Connectors** > **Your Connections**.
- Select the connection that you want to modify.
- Under **Copilot Visibility**, select the toggle to turn the connector on or off, and choose **Save**.

:::image type="content" alt-text="Screenshot that shows the Copilot Visibility toggle on the connection pane" source="media/manage-connector/copilot-visibility.png" lightbox="media/manage-connector/copilot-visibility.png":::

When the visibility is off, the connector is excluded from all Copilot Search and Copilot Chat results and responses.

The default behavior is visible by default, with changes syncing automatically with search, without affecting declarative agents and their data.

> [!Note]
> After you update the visibility settings at the connection level, allow up to 30 minutes for the changes to propagate across all Copilot experiences.

## Manage schema recommendations for custom Copilot connectors

When you build a custom Copilot connector, the schema you define determines how your content is indexed and surfaced in Microsoft 365 Copilot. To help you get started, the Microsoft 365 admin center provides schema recommendations for published custom connectors.

Schema recommendations analyze your connector schema and highlight missing semantic labels for key properties that Copilot relies on to understand, rank, and cite content.

### Supported recommendations

Schema recommendations currently check for four missing semantic labels:

- **Title** – Semantically indexes the primary display name of an item. Required for meaningful result rendering and relevant Copilot results.
- **URL** – Identifies the canonical link to the source item. Required for Copilot citations to link back to the source system.
- **LastModifiedBy** – Identifies who last updated an item. Improves attribution in Copilot responses.
- **LastModifiedDateTime** – Indicates when an item was last updated. Enables Copilot to reason over recency and answer time-based questions.

:::image type="content" alt-text="Schema recommendations can be accessed via the connection detail panel." source="media/manage-connector/schema-recommendations-2.png" lightbox="media/manage-connector/schema-recommendations-2.png":::

> [!NOTE]
> Schema recommendations aren't exhaustive and don't replace the full schema design guidance for Copilot connectors. For comprehensive schema best practices, property attributes, and semantic label guidance, see [Semantic labels](/graph/connecting-external-content-manage-schema#semantic-labels).

## Notifications for permanent crawl failures in your connections

Connection crawls are scheduled to run at specific intervals. Failures can occur due to various issues with the connections. Some failures are temporary, and crawl resume automatically, while others are permanent and require administrative intervention to restart. If a permanent failure occurs, the connection is marked as **Failed**, and notifications are sent to the service health dashboard under the **Issues** section for your organization to act on.

:::image type="content" alt-text="Screenshot that shows issues in your environment section of service health." source="media/manage-connector/shd-notification-home.png" lightbox="media/manage-connector/shd-notification-home.png":::

This information is also available as an advisory in the service status section of the service health page, under the Microsoft 365 suite category.

:::image type="content" alt-text="Screenshot that shows service status section" source="media/manage-connector/notification-service-status.png" lightbox="media/manage-connector/notification-bar-mac.png":::

If there are active notifications, admins receive alerts in the form of notification bars on the Microsoft 365 admin center home page. These bars display the connection ID associated with the failed crawls. Admins can select the notification bars to view more details or remove them from the page.

:::image type="content" alt-text="Screenshot that shows sample notification bar" source="media/manage-connector/notification-bar-mac.png" lightbox="media/manage-connector/notification-bar-mac.png":::

Admins can select the notification to view the notification details.

:::image type="content" alt-text="Screenshot that shows sample notification" source="media/manage-connector/sample-notification.png" lightbox="media/manage-connector/sample-notification.png":::

The notification remains active in the service health dashboard for six days. After this period, it's automatically moved to **Issue history** where it's retained for up to 30 days. If the connection resumes crawling, the notification is also moved to the **Issue history**. 
No new notification is issued for the same connection until crawling restarts. If the crawls restart and fail again, a new notification is generated. For multiple connections with crawl failures, each connection has a separate notification bar on both the admin center home page and the service health dashboard landing page.

### Email notifications subscription

To receive failure notifications and updates via email, admins can add up to two email addresses:

1. Go to the customize section on service health and open the email tab.
2. Check the box for **Issues in your environment that require action**.
3. In **Include these services**, select Microsoft 365 suite. This selection ensures that admins receive all notifications for the Microsoft 365 suite, including Copilot connector notifications, when they subscribe to service health notifications.
4. Save your changes.

:::image type="content" alt-text="Screenshot that shows e-mail subscription for notifications" source="media/manage-connector/notification-mail.png" lightbox="media/manage-connector/on-demand-crawl.png":::

## Manage crawls in your connections

During connection creation or configuration editing, you can configure the crawl schedule. In addition to the scheduled crawls, you can run on-demand crawls for your connection through the connection pane.

:::image type="content" alt-text="Screenshot that shows on-demand crawl connection pane." source="media/manage-connector/on-demand-crawl.png" lightbox="media/manage-connector/on-demand-crawl.png":::

On-demand crawl helps you start a crawl outside of the crawl schedule. You can choose to run a full or incremental crawl, as shown in the image.

:::image type="content" alt-text="Screenshot that shows on-demand crawl drop-down." source="media/manage-connector/on-demand-dropdown.png" lightbox="media/manage-connector/on-demand-dropdown.png":::

> [!NOTE]
> The Microsoft Graph connector agent versions 2.1.0.0 and later support on-demand crawl.

Only one category of crawl—scheduled or on-can run on a connection at any time. If a connection is in a **Syncing** state, on-demand crawls are disabled. Scheduled crawls are triggered automatically.

If a scheduled or on-demand crawl continues beyond the time of the next scheduled full or incremental crawl, the ongoing crawl is stopped, and the next scheduled crawl is skipped and queued. After the ongoing crawl completes, the opposite type of crawl (full or incremental) is picked from the skipped queue and triggered. For example, if the previous crawl was a full crawl, only the incremental crawl, if present in the skipped queue, is triggered—and vice versa.

Identify connections that contain items you no longer want to index. To update this connection, first delete the existing connection and create a new one with a data source exclusion filter that excludes the items you no longer want to index.

You can permanently delete one or more connections as needed.

## Related content

- [Deploy Microsoft 365 Copilot connectors](deployment-overview.md)
