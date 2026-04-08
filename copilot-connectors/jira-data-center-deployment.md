---
title: "Deploy the Jira Data Center connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: neocheng
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 12/17/2025
ms.localizationpriority: Medium
description: "Find information about how to deploy the Jira Data Center Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Jira Data Center connector

The Jira Data Center Microsoft 365 Copilot connector allows your organization to index Jira Data Center issues and related project data so they become discoverable and actionable in Microsoft 365 and Microsoft Search experiences. This article describes the steps to deploy and customize the Jira Data Center connector.

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be a Microsoft 365 admin.
- Install the [Microsoft Graph connector agent](/microsoft-365/copilot/connectors/connector-agent) on a Windows computer within the same network as your Jira Data Center instance. If the agent is already installed, verify that you're running version **3.1.15.0 or later**.
- Install the Jira Data Center plugin from the Microsoft 365 Copilot connector listing in the [Atlassian Marketplace](https://marketplace.atlassian.com/).  
  > [!NOTE]
  > The plugin supports Jira Data Center versions **8.10.0 – 10.5.1**.
- Configure a service account with the permissions listed in the following table.

    | Permission name | Permission type | Required for |
    |-----------------|------------------|--------------|
    | **Browse projects** | Project permission | Crawling Jira issues (mandatory). |
    | **Issue level security** | Issue-level security | Crawling issue types with security levels (optional). |
    | **Browse users and groups** | Global permission | Security trimming when **Only people with access to this data source** is selected (optional). |
    | **Administer Jira** | Global permission | Required when enforcing strict access-control mapping (optional). |

- Allow unlimited requests to prevent throttling. In **System** > **Rate limiting** > **Exemptions** > **Add exemptions**, add the service account to the **exemptions** list.

   :::image type="content" alt-text="Screenshot that shows allowing unlimited requests for the Service Account" source="media/jira-data-center/jira-data-center-graph-connector-allow-unlimited-requests-for-service-account.png" lightbox="media/jira-data-center/jira-data-center-graph-connector-allow-unlimited-requests-for-service-account.png":::

## Deploy the connector

To add the Jira Data Center connector for your organization:

1. In the **Microsoft 365 admin center**, in the left pane, choose **Copilot** > **Connectors**.
2. Choose the **Gallery** tab.
3. From the list of available connectors, choose **Jira Data Center**.

### Set display name

The display name identifies the content source in Copilot responses. You can accept the default **Jira Data Center** name or customize it to help users recognize the data source.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

### Set instance URL

Enter the URL of your Jira Data Center instance. The typical format is: `https://jira.<your-domain>.com`.

### Choose authentication type

Configure OAuth 2.0 authentication by using Jira Application Links.

To configure OAuth in Jira:

1. Sign in to Jira Data Center.
2. Go to **Settings** > **Applications** > **Application links**.

    :::image type="content" alt-text="Screenshot of Click Application in Settings menu." source="media/jira-data-center/jira-step2-1-click-application.png" lightbox="media/jira-data-center/jira-step2-1-click-application.png":::

    :::image type="content" alt-text="Screenshot of Application links page." source="media/jira-data-center/jira-step2-2-app-links-page.png" lightbox="media/jira-data-center/jira-step2-2-app-links-page.png":::

1. Select **Create link**.

    :::image type="content" alt-text="Screenshot of Select Create link." source="media/jira-data-center/jira-step3-create-link.png" lightbox="media/jira-data-center/jira-step3-create-link.png":::

1. Choose **External application**, then choose **Incoming** as the direction.

    :::image type="content" alt-text="Screenshot of Select External application and Incoming direction." source="media/jira-data-center/jira-step4-external-incoming.png" lightbox="media/jira-data-center/jira-step4-external-incoming.png":::

1. Complete the **Configure an incoming link** form:
   - **Redirect URL:**  
     - Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`  
     - Government Community Cloud High (GCC High): `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
   - **Scope:** Admin

    :::image type="content" alt-text="Screenshot of Configure an incoming link form." source="media/jira-data-center/jira-step5-config-form.png" lightbox="media/jira-data-center/jira-step5-config-form.png":::

1. Copy the **client ID** and **secret**, and paste them into the Microsoft 365 admin center connection setup page.

    :::image type="content" alt-text="Screenshot of Client ID and Secret." source="media/jira-data-center/jira-step6-credentials.png" lightbox="media/jira-data-center/jira-step6-credentials.png":::

### Roll out

To validate the connection before a full rollout, select **Rollout to limited audience** and specify the users or groups for the staged deployment. For more information, see [Staged rollout for Copilot connectors](/microsoft-365/copilot/connectors/staged-rollout).

Choose **Create** to deploy the connector. The Jira Data Center connector starts indexing content right away.

The following table lists the default values that the connector applies.

| Category | Default value |
|----------|----------------|
| **Users** | Access permissions: Only people with access to this data source; identities mapped using Microsoft Entra ID. |
| **Content** | All projects indexed by default; default property schema applied. |
| **Sync** | Incremental crawl every 15 minutes; full crawl daily. |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize settings for the Jira Data Center connector.

### Customize user settings

#### Access permissions

The connector supports two access options:

- **Everyone**
- **Only people with access to this data source** (recommended)

When you select **Only people with access to this data source**, the connector enforces the Jira permission model, including issue-level security and project permissions. Identity mapping is required if Jira email IDs differ from Microsoft Entra ID user principal name (UPN) values.

The connector uses the following hierarchy:
1. **Issue security level (Highest priority):** If set, access is restricted to users in that level.
2. **Fallback to project-level permissions:** If no security level is set, access is determined by the **Browse Projects** permission.

#### Map identities

If you use restrictive permissions, map Jira identities to Microsoft 365 identities in one of the following ways:

- **Microsoft Entra ID:** Choose this option if the email ID of Jira users is the same as the UPN in Microsoft Entra ID.
- **Non-Entra ID:** Choose this option if the IDs differ (requires a Regex rule).

### Customize content settings

#### Filter data

You can filter issues by creation or update timestamp, or by using **JQL**. For example: `project = "PROJ" AND updated >= -30d`.

#### Manage properties

Select the Jira fields (schema properties) you want to index. Include built-in Jira fields or add custom fields. For more information, see [Manage search schema](/microsoftsearch/manage-search-schema). The following properties are indexed by default.

|Source property       | Semantic Label          | Schema  |               
|:---------------------|:---------------------- |:---------------------- |
| AssigneeEmailId       |                         | Query, Retrieve, Search |
| AssigneeName          |                         | Query, Retrieve, Search |
| Authors               | Authors               | Query, Retrieve       |
| Created               | Created date time       | Retrieve              |
| DueDate               |                         | Retrieve              |
| IssueDescription      |                         | Search                |
| IssueIconUrl          | IconUrl                  | Retrieve                |
| IssueId               |                         | Retrieve              |
| IssueKey              |                         | Query, Retrieve, Search|
| IssueLink             | Url                     | Query, Retrieve, Search|
| IssuePriority         |                         | Query, Retrieve, Search |
| IssueStatus           |                         | Query, Retrieve  |
| IssueSummary          |                         | Search |
| IssueType             |                         | Query, Retrieve | 
| Labels                |                         | Query, Retrieve | 
| ProjectName           |                         | Query, Retrieve  |
| ReporterEmailId       | Created by              | Query, Retrieve, Search  |
| ReporterName          |                         | Query, Retrieve, Search | 
| Title                 | Title                   | Query, Retrieve, Search  |
| Updated               | Last modified date time | Query, Retrieve | 


### Customize sync intervals

You can adjust the crawl frequency to fit your data refresh needs. The following are the default values:

- **Full crawl:** Every day  
- **Incremental crawl:** Every 15 minutes

For more information, see [Guidelines for crawl settings](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [Jira Data Center connector overview](jira-data-center-overview.md)
- [Troubleshoot issues with the Jira Data Center connector](jira-data-center-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365/copilot/connectors/deployment-overview)
