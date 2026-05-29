---
title: "Deploy the {connector name} connector"
ms.author: 
author: 
manager:
ms.reviewer: 
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 
ms.localizationpriority: Medium
description: "Find information about how to deploy the {connector name} Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the {connector name} connector

{Introduce the connector with a brief description.}

This article describes the steps to deploy and customize the {connector name} connector. 

{If the connector requires advanced service configuration, include a link to the set up topic:

For advanced {service name} configuration information, see [Set up the {service name} service for connector ingestion](connectorname-admin-setup.md).}

## Prerequisites

{Optional section for complex connectors (connectors that require admin setup content):  

Before you deploy the {connector name} connector, make sure that the {service name} environment is configured in your organization. The following table summarizes the steps to configure the {service name} environment and deploy the connector.

| Task | Role |
| ---- | ---- |
| [Configure the environment](connectorname-admin-setup.md#configure-the-confluence-environment) | {Service name} admin |
| [Set up prerequisites](connectorname-admin-setup.md#set-up-connector-prerequisites) | {Service name} admin/Network admin |
| [Deploy the connector in the Microsoft 365 admin center](#deploy-the-connector) | Microsoft 365 admin |
| [Customize connector settings](#customize-settings-optional) (optional) | Microsoft 365 admin |

}

Before you deploy the connector, make sure that you meet the following prerequisites:

{Add a bulleted list of prerequisites, including that the user must be a Microsoft 365 admin.}

## Deploy the connector

To add the {connector name} connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, select **Copilot** > **Connectors**.
1. Select the **Gallery** tab.
1. From the list of available connectors, select **{connector name}**.

### Set display name

The display name identifies references in Copilot responses so users can recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **{connector name}** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

### Set instance URL

{Provide details about the instance URL for the connector, including the typical structure of the URL.}

### Choose authentication type

{Provide details about the authentication types that are available for the connector. Include a bulleted list with the authentication options, and call out which option is recommended.}

### Roll out

{Optional introduction to provide information about a staged rollout to a limited set of users before the full rollout.}

To roll out to a limited audience, select the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](staged-rollout.md).

Select **Create** to deploy the connection. The {connector name} connector starts indexing content right away.

{Provide information about default values for the connector as applicable. The categories for the values are Users, Content, and Sync. Include the default values in a table as shown, or if necessary add subsections for each category to provide details.

The following table lists the default values that are set.

| Category | Default value |
|----------|---------------|
| Users    |               |
| Content  |               |
| Sync     |               |
}

To customize these values, select **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the {connector name} connector settings. To customize settings, on the connector page in the admin center, select **Custom setup**.

### Customize user settings

#### Access permissions

{Describe the access permission settings that can be customized.}

#### Map identities

{Describe the identity mapping settings that can be customized.}

### Customize content settings

#### Query string

{Describe the default query string and how it can be customized.}

#### Manage properties

{Describe how to manage properties. Include a table that lists the properties that the connector indexes by default.}

|Property |Semantic Label |Description |Schema Attributes|
|---|---|---|---|

### Customize sync intervals

{Describe the sync intervals that can be customized. These intervals typically include Full crawl and Incremental crawl. Provide the default values that are set.}

For more information, see [Guidelines for crawl settings](deployment-overview.md#guidelines-for-crawl-settings).

## Related content

- [{Connector name} connector overview](connectorname-overview.md)
- [Troubleshoot issues with the {connector name} connector](connectorname-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](deployment-overview.md)
