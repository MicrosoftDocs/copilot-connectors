--- 
title: "Gong Copilot connector" 
ms.author: rerabo
author: vivg
manager: harshkum
audience: Admin
ms.audience: Admin 
ms.topic: article 
ms.service: copilot-connectors 
ms.localizationpriority: medium 
description: "Set up the Gong Copilot connector for Microsoft 365 Copilot and Microsoft Search" 
ms.date: 12/25/2025
---

# Gong Copilot connector

With the Microsoft 365 Copilot connector for Gong, your organization can index calls and meeting-related content like summaries, action items, and call metadata. The connector enables Gong users to retrieve this information through Microsoft 365 Copilot and any Microsoft Search client.

## Capabilities
- Index calls and meetings content such as brief, key points, and action items.
- Index calls and meetings metadata, including the title, duration, and basic context from the CRM, such as the Account name and Deal name.
- Enable your end users to ask questions related to Gong directly within Copilot, for example.
    - What are the action items from the Q2 planning meeting with Acme Corp on May 12?
    - What were the key insights from the Demo discussion meeting with Contoso Ltd?
    - What topics come up repeatedly in calls with Fabrikam Inc?
    - Who was the decision maker in the contract review meeting with Northwind Traders?

## Limitations
- Updates to existing calls - such as deletions, workspace changes, trimming, or removal of CRM context or trackers - are reflected only after a full sync.
- Moving calls between workspaces is captured only during a full crawl, not during incremental sync.
- Access to calls may be impacted when users become inactive or lack workspace permissions. If a user becomes inactive, others may lose access to calls they participated in. Similarly, if a call is linked to a workspace a user cannot access, others might not be able to view it.

## Prerequisites
- You must be the AI administrator for your organization's Microsoft 365 tenant.
- To connect to Gong, the Copilot connector uses OAuth authentication. A **Gong administrator** must sign in with their Gong credentials to authorize the connector.
- The base URL of your Gong instance is required to complete the setup. Follow the steps below to get the Gong base URL:
    1. In Gong, navigate to **Admin Center → Ecosystem → API** or simply browse to https://app.gong.io/company/api-authentication
    2. Copy the base URL shown here and enter it when setting up the connector.
[![Screenshot that shows how to get the Gong base URL.](media/gong-connector/gong-base-url.png)](media/gong-connector/gong-base-url.png#lightbox)

## Get Started

### 1. Display name
A display name is used to identify each reference in Copilot, making it easier for users to recognize the associated file or item. It also indicates that the content is trusted and serves as a [content source filter](/microsoft-365/copilot/connectors/custom-filters#content-source-filters). While a default value is provided, you can customize the display name to something more familiar and meaningful for users in your organization.

### 2. Gong URL
Enter the Gong base URL that you copied during the [Prerequisites step](#prerequisites).

### 3. Authentication
- Select **'OAuth 2.0'**.
- Select **Authorize** and authenticate to your Gong instance by signing in with a Gong administrator account.
- Complete the OAuth consent flow to grant the connector access to the required Gong APIs.
[![Screenshot that shows completion of OAuth flow.](media/gong-connector/gong-oauth.png)](media/gong-connector/gong-oauth.png#lightbox)

### 4. Rollout to limited audience
Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before expanding the rollout to a broader audience. To know more about limited rollout, click [here](staged-rollout.md).

At this stage, you're ready to create the connection to Gong. To proceed, review and agree to the terms by selecting the checkbox next to the **Notice** section.
Then, click the **Create** button. The Copilot connector begins indexing calls and meeting-related content from your Gong instance.

## Custom Setup
Custom setup is intended for admins who want greater control over user access, the content being crawled, and the frequency of data refresh by modifying the default settings. Once you click on the **Custom setup** option, you see three more tabs - Users, Content, and Sync.

>[!NOTE]
> Ensure you authenticate to be able to edit the properties under Users, Content, and Sync.

[![Screenshot that shows custom setup options.](media/gong-connector/gong-custom2.png)](media/gong-connector/gong-custom2.png#lightbox)

### Users

#### Access Permissions
The Gong Copilot connector supports search permissions visible to **Only people with access to this data source** (default) or **Everyone**.

If you choose **Only people with access to this data source**, indexed data appears in search results only for users who have access to it in Gong. This means that if a user can access a call in Gong, they see it in Copilot, and if they can’t access a call in Gong, it won’t appear for them in Copilot either.

If you choose **Everyone**, indexed data appears in the search results for all users.

#### Map Identities

[![Screenshot that shows Users setup.](media/gong-connector/gong-users.png)](media/gong-connector/gong-users.png#lightbox)

To enforce correct permissions, you need to map user identities from Gong to Microsoft Entra ID (ME-ID). There are two options:
1. **Microsoft Entra ID (ME-ID) mapping (default):**<br>
By default, the system attempts to match users by comparing the **user's email in Gong** with either the **UserPrincipalName** (UPN) or **Mail** attribute in Microsoft Entra ID. This method works when the email addresses align between systems.
2. **Non-Microsoft Entra ID (non ME-ID) mapping (custom):** <br>
If the default mapping doesn't work for your organization (for example, if email formats differ) you can define a custom mapping formula to link users across systems.

[Click here](map-non-entra-id.md) to learn more about mapping non-Entra ID identities.

>[!Important]
>- Access is based on Gong user profiles: <br>
>In Copilot, access to calls is determined by the user's profile in Gong. If a call is manually shared with someone who wouldn’t normally have access based on their user profile, they'll not see it in Copilot.
>- Folder-based access is not supported:<br>
>If a user has access to a call in Gong solely because it resides in a folder with unique permissions (but they lack access through their Gong profile) they'll not have access to that call in Copilot.

### Filter data

#### Filter by workspace
By default, data is crawled from all Gong workspaces. To limit crawling to a specific workspace, click **Specific workspace**. A dropdown menu will appear, allowing you to select a single workspace for data indexing.
[![Screenshot that shows Gong workspace selection.](media/gong-connector/gong-workspace.png)](media/gong-connector/gong-workspace.png#lightbox)

#### Filter by date
By default, data is crawled from all available dates. To limit the crawl to more recent content, you can select a specific start date by clicking the **Select start date** option.
[![Screenshot that shows Gong date selection.](media/gong-connector/gong-date.png)](media/gong-connector/gong-date.png#lightbox)

### Sync
The refresh interval determines how often your data is synced between the data source and the Copilot connector index. There are two types of refresh intervals: full crawl and incremental crawl. For more details, click [here](deployment-overview.md#guidelines-for-crawl-settings).
You can change the default refresh interval values from here if needed.
[![Screenshot that shows sync and refresh frequency settings.](media/gong-connector/gong-sync.png)](media/gong-connector/gong-sync.png#lightbox)
