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
8. Choose **Create** to deploy the connection. The connector begins indexing content using default settings.

[IMAGE PLACEHOLDER]

> [!NOTE]
> Most connectors use optimized default settings for access permissions, schema, and sync frequency. To customize the default settings, see [Customize connector settings](#customize-connector-settings-optional).

On the success screen, add a description that answers the following:

- What kind of content does this connection include?
- How do users refer to this content source?
- When do users access this content in their workflow?
- What are key characteristics of the content?

For guidance, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

## Customize connector settings (optional)

You can customize the default values for connector settings. On the connector page in the admin center, choose **Custom setup**. This option includes three tabs:

- **Users**
- **Content**
- **Sync**

### User settings

[IMAGE PLACEHOLDER]

On the **Users** tab, under **Access Permissions**, choose whether indexed data is visible to:

- Only users with access to the content
- Everyone in the organization

By default, users are mapped by matching their email to `UserPrincipalName` or `Mail` in Microsoft Entra ID. In the **Map Identities** section, you can provide a custom mapping formula.


### Content settings

[IMAGE PLACEHOLDER]

On the **Content** tab, under **Manage properties**, you can:

- Configure properties to be searchable, queryable, or refinable.
- Assign semantic labels and aliases to improve search relevance.
- Customize values for properties for certain connectors, like **URL**.

For details, see #guidelines-for-manage-properties-settings.

#### Content property

Select a **Content property** from the dropdown or use the default. This property supports full-text indexing, snippet generation, language detection, and relevance ranking.

You can use the system-generated **ResultSnippet** property in your result type to display dynamic snippets.

#### Aliases

In the **Alias** column, add aliases to normalize property names across multiple connections. This enables unified filters and queries.

#### Semantic labels

Assign semantic labels to source properties to integrate connector data into Microsoft 365 experiences. The following table lists the supported labels.

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

We recommend that you assign a property to the **title** label.

Incorrect mapping labels can affect search experiences. Not all labels need to have a property assigned.

#### Search schema attributes

You can set the search schema attributes to control the search functionality of each source property. A search schema helps determine what results are displayed on the search results page and what information end users can view and access.

Search schema attributes include options to **Query**, **Search**, **Retrieve**, and **Refine**. The following table lists the supported attributes.

> [!NOTE]
> Properties with the `int` datatype can't be refined, even if marked as refinable.

| Attribute | Function |
|----------|----------|
| **SEARCH** | Makes property content searchable |
| **QUERY** | Enables property-specific queries |
| **RETRIEVE** | Allows property to appear in search results |
| **REFINE** | Enables filtering on the search results page |

Only string properties can be marked as searchable.

### Sync settings

[IMAGE PLACEHOLDER]

On the **Sync** tab, you can configure how often data syncs between the source and the connector index.

- **Full crawl**: Syncs all data at scheduled intervals.
- **Incremental crawl**: Syncs only new or changed data.

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

### IP firewall rules

To secure access, configure your firewall to allow Copilot connector service IP ranges.

| Region | Microsoft 365 Enterprise | Microsoft 365 Government |
| ------ | ------------------------ | ------------------------ |
| NAM | 52.250.92.252/30, 52.224.250.216/30 | 52.245.230.216/30, 20.141.117.64/30 |
| EUR | 20.54.41.208/30, 51.105.159.88/30 | NA|
| APC | 52.139.188.212/30, 20.43.146.44/30 | NA |