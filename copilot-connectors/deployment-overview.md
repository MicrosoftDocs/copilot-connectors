---

title: "Deploy Microsoft 365 Copilot connectors in the Microsoft 365 admin center"
description: Learn how to deploy and customize Copilot connectors in the Microsoft 365 admin center.
ms.author: souravpoddar
author: souravpoddar001
manager: harshkum
audience: Admin
ms.audience: Admin
ms.topic: install-set-up-deploy
ms.service: copilot-connectors
ms.localizationpriority: medium
ms.date: 07/24/2025
---

# Deploy Microsoft 365 Copilot connectors in the Microsoft 365 admin center

This article describes how to set up Microsoft 365 Copilot connectors in the Microsoft 365 admin center. The setup process is streamlined and requires minimal input, making it easy to create connections. You can also choose a custom setup to fine-tune specific settings.

> [!NOTE]
> The setup process is similar for all Copilot connectors, with some differences. We recommend that you reference the deployment guide specific to your data source.

> [!TIP]
> **Product survey**  
> Help us prioritize new data sources for connectors by completing this [survey](https://forms.office.com/r/0Hh4GJNsJe).

## Prerequisites

Before you begin, make sure you have the following:

- **Admin access**: You must have one of the following roles in the Microsoft 365 admin center:
  - Global admin
  - Search admin
  - Copilot admin
- **Data source credentials**: Gather the required credentials and permissions for the data source.
- **Service account (if applicable)**: Make sure that the service account has the necessary roles or permissions.

## Deploy a connector

<img src="media/add-connector.png" alt="Data sources available include: ADLS Gen2, Enterprise websites, Microsoft SQL server, Azure SQL, Oracle SQL database, ServiceNow Knowledge, ServiceNow Catalog, File share, Azure DevOps, and MediaWiki." data-linktype="relative-path">

Use the following steps to deploy a connector:

1. Sign in to the [Microsoft 365 admin center](https://admin.microsoft.com/).
2. In the left pane, choose **Copilot** > **Connectors**.
3. On the **Connectors** tab, in the left pane, choose **Gallery**, and select the data source you want to connect (for example, ServiceNow Knowledge or Salesforce).
4. Enter a name to help users recognize the source in Copilot and search results. You can customize the default name.
5. Provide the URL of your data source. For example: `https://your-organization-name.service-now.com`.
6. Choose an authentication method to access the data source.
7. Deploy the connector to a subset of users for validation before a broader rollout.

[IMAGE PLACEHOLDER]

> [!NOTE]
> Most connectors use optimized default settings for access permissions, schema, and sync frequency. To edit these settings, choose #step-4-customize-connector-configuration-optional.

---

## Step 3: Create the connection

Click **Create** to set up the connection. The connector begins indexing content using default settings.

On the success screen, add a description that briefly answers:

- What kind of content does this connection include?
- How do users refer to this content source?
- When do users access this content in their workflow?
- What are key characteristics of the content?

For more guidance, see enhancing-microsoft-copilot-discovery-with-graph-connector-content.md.

## Customize connector configuration (optional)

Choose **Custom setup** for more control. This option includes three tabs:

- **Users**
- **Content**
- **Sync**

### Users

media/servicenow-knowledge-connector/servicenow-knowledge-users-page.png

1. **Access permissions**  
   Choose whether indexed data is visible to:
   - Everyone in the organization
   - Only users with access to the content

2. **Map identities**  
   By default, users are mapped by matching their email to `UserPrincipalName` or `Mail` in Microsoft Entra ID. You can provide a custom mapping formula if needed.

---

### Content

media/servicenow-knowledge-connector/servicenow-knowledge-content-page.png

1. **Manage properties**  
   Configure properties to be searchable, queryable, or refinable. Assign semantic labels and aliases to improve search relevance.

For details, see #guidelines-for-manage-properties-settings.

---

### Sync

media/servicenow-knowledge-connector/servicenow-knowledge-sync-page.png

**Refresh intervals**  
Configure how often data syncs between the source and the connector index.

- **Full crawl**: Syncs all data at scheduled intervals.
- **Incremental crawl**: Syncs only new or changed data.

Adjust sync settings as needed. For more information, see #guidelines-for-sync-settings.

---

## Guidelines for Manage Properties settings

### Content property

Select a **Content property** from the dropdown or use the default. This property supports full-text indexing, snippet generation, language detection, and relevance ranking.

If selected, you can use the system-generated **ResultSnippet** property in your result type to display dynamic snippets.

### Aliases

Add aliases under the "Alias" column to normalize property names across multiple connections. This enables unified filters and queries.

See customize-search-page.md for more info.

### Semantic labels

Assign semantic labels to source properties to integrate connector data into Microsoft 365 experiences. Supported labels include:

| Label | Description |
|-------|-------------|
| **title** | Title shown in search and other experiences |
| **url** | Target URL of the item |
| **Created By** | Creator of the item |
| **Last modified by** | Most recent editor |
| **Authors** | Collaborators |
| **Created date time** | Creation timestamp |
| **Last modified date time** | Last edit timestamp |
| **File name** | Name of the file |
| **File extension** | File type (PDF, DOC, etc.) |

The **title** label is essential for participating in the result-cluster.md.

---

## Search schema attributes

> [!NOTE]
> Properties with the `int` datatype can't be refined, even if marked as refinable.

Search schema attributes control search functionality. Supported attributes include:

| Attribute | Function |
|----------|----------|
| **SEARCH** | Makes property content searchable |
| **QUERY** | Enables property-specific queries |
| **RETRIEVE** | Allows property to appear in search results |
| **REFINE** | Enables filtering on the search results page |

Only string properties can be marked as searchable.

To update the schema after connection creation, see manage-search-schema.md.

---

## Guidelines for Sync settings

Refresh intervals determine how often data syncs. Choose between:

- **Full refresh**: Indexes all changed items.
- **Incremental refresh**: Indexes only new or modified items.

> [!NOTE]
> Incremental crawls don't support permission updates. Run full crawls periodically to maintain sync accuracy.

### Crawl scheduling

Configure crawl frequency and timing:

- **Recurrence**: Daily, weekly, biweekly, or monthly
- **Days**: Specific days of the week
- **Frequency**: Repeat interval (15 minutes to 12 hours)
- **Start time**: When the crawl begins
- **Reset**: Revert to default schedule

If fields are left blank, Copilot connectors choose optimal crawl times.

---

## IP firewall rules

To secure access, configure your firewall to allow Copilot connector service IP ranges.

RegionMicrosoft 365 EnterpriseMicrosoft 365 GovernmentNAM52.250.92.252/30, 52.224.250.216/3052.245.230.216/30, 20.141.117.64/30EUR20.54.41.208/30, 51.105.159.88/30NA| APC | 52.139.188.212/30, 20.43.146.44/30 | NA |