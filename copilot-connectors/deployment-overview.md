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

## Prerequisites

Before you begin, make sure you have the following prerequisites:

- **Admin access**: You must be an AI administrator in the Microsoft 365 admin center.
- **Data source credentials**: Gather the required credentials and permissions for the data source.
- **Service account (if applicable)**: Make sure that the service account has the necessary roles or permissions.

## Deploy a connector

:::image type="content" alt-text="Screenshot of the connector gallery in the Microsoft 365 admin center." source="media/deployment-overview/add-connector.png" lightbox="media/deployment-overview/add-connector.png":::

Use the following steps to deploy a connector:

1. Sign in to the [Microsoft 365 admin center](https://admin.microsoft.com/).
2. In the left pane, choose **Copilot** > **Connectors**.
3. On the **Connectors** tab, in the left pane, choose **Gallery**, and select the data source you want to connect (for example, ServiceNow Knowledge or Salesforce).
4. Enter a name to help users recognize the source in Copilot and search results. You can customize the default name.
5. Provide the URL of your data source. For example: `https://your-organization-name.service-now.com`.
6. Choose an authentication method to access the data source.
7. Deploy the connector to a subset of users for validation before a broader rollout.
8. Choose **Create** to deploy the connection. The connector begins indexing content using default settings.

:::image type="content" alt-text="Screenshot that shows Connection creation screen for ServiceNow Knowledge Copilot connector." source="media/deployment-overview/aha-setup.png" lightbox="media/deployment-overview/aha-setup.png":::

> [!NOTE]
> Most connectors use optimized default settings for access permissions, schema, and sync frequency. To customize the default settings, see [Customize connector settings](#customize-connector-settings-optional).

On the success screen, add a description that answers the following questions:

- What kind of content does this connection include?
- How do users refer to this content source?
- When do users access this content in their workflow?
- What are key characteristics of the content?

For guidance, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

## Customize connector settings (optional)

You can customize the default values for connector settings. On the connector page in the admin center, choose **Custom setup**. This option includes three tabs:

- **User**
- **Data**
- **Crawl**

### User settings

:::image type="content" alt-text="Screenshot that shows the User configuration screen for ServiceNow Knowledge Copilot connector." source="media/deployment-overview/customize-user.png" lightbox="media/deployment-overview/customize-user.png":::

On the **User** tab, under **Access Permissions**, choose whether indexed data is visible to:

- Only users with access to the content
- Everyone in the organization

By default, users are mapped by matching their email to `UserPrincipalName` or `Mail` in Microsoft Entra ID. In the **Map Identities** section, you can provide a custom mapping formula.


### Data settings

:::image type="content" alt-text="Screenshot that shows the Content configuration screen for ServiceNow Knowledge Copilot connector." source="media/deployment-overview/customize-data.png" lightbox="media/deployment-overview/customize-data.png":::

On the **Data** tab, under **Manage properties**, you can:

- Configure properties to be searchable, queryable, or refinable.
- Assign semantic labels and aliases to improve search relevance.
- Customize values for properties for certain connectors, like **URL**.

#### Content property

Select a **Content property** from the dropdown or use the default. This property supports full-text indexing, snippet generation, language detection, and relevance ranking.

You can use the system-generated **ResultSnippet** property in your result type to display dynamic snippets.

#### Aliases

In the **Alias** column, add aliases to normalize property names across multiple connections. This alias enables unified filters and queries.

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

### Crawl settings

:::image type="content" alt-text="Screenshot of the connector gallery in the Microsoft 365 admin center." source="media/deployment-overview/customize-crawl.png" lightbox="media/deployment-overview/customize-crawl.png":::

On the **Crawl** tab, you can configure how often data syncs between the source and the connector index.

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

## Connector setting guidelines

### Content property

We recommend that you select a **Content property** from the drop-down list, or keep the default selection if one is provided. The content property is used for full-text indexing and supports scenarios such as search result snippet generation, [result cluster](/microsoftsearch/result-cluster) participation, language detection, HTML and text processing, ranking and relevance, and query formulation.

When you select a content property, you can use the system-generated **ResultSnippet** property when you [create your result type](customize-results-layout.md). **ResultSnippet** acts as a placeholder for dynamic snippets that are generated at query time from the content property. When this property is included in a result type, snippets appear in search results automatically.

### Aliases for source properties

You can add aliases to properties by using the **Alias** column. Aliases are friendly names that you can use in queries and when creating filters. They also help normalize properties from multiple connections by mapping different source properties to a single, common name. This approach allows you to create a single filter for a vertical that spans multiple connections. For more information, see [Customize the search results page](customize-search-page.md).

### Semantic labels for source properties

You can assign semantic labels to source properties. Semantic labels are well-known tags provided by Microsoft that add meaning to your data and enable integration across Microsoft 365 experiences, including Copilot, enhanced search, people cards, intelligent discovery, and more.

The following table lists the supported semantic labels and their descriptions.

| Label | Description |
| --- | --- |
| **title** | The title of the item shown in search and other Microsoft 365 experiences |
| **url** | The target URL of the item in the source system |
| **Created By** | The name of the person who created the item |
| **Last modified by** | The name of the person who most recently edited the item |
| **Authors** | The names of people who contributed to or collaborated on the item |
| **Created date time** | The date and time when the item was created |
| **Last modified date time** | The date and time when the item was most recently edited |
| **File name** | The name of the file |
| **File extension** | The file type, such as PDF or DOC |

The properties on this page are preselected based on your data source, but you can change the selection if a different property is better suited for a specific label.

The **title** label is the most important semantic label. We *strongly recommend* that you map a property to this label so that your connection can participate in the [result cluster experience](result-cluster.md).

Incorrect label mappings can degrade the search experience. Not all labels are required to have a property assigned.

### Search schema attributes

> [!NOTE]
> Properties with the **int** data type can’t be refined, even if they’re marked as refinable.

Search schema attributes control how each source property behaves in search. The search schema determines which results appear on the search results page and what information users can view and access.

Copilot connectors support the following search schema attributes.

| Search schema attribute | Function | Example |
| --- | --- | --- |
| **SEARCH** | Makes the text content of a property searchable and includes it in the full-text index. | If the **title** property is searchable, a query for **Enterprise** returns items that contain **Enterprise** in the title or body text. |
| **QUERY** | Allows querying against a specific property by name, either programmatically or by using query syntax. | If the **Title** property is queryable, the query `Title:Enterprise` is supported. |
| **RETRIEVE** | Allows a property to be displayed in search results and used in result types. | Only retrievable properties can appear in search results. |
| **REFINE** | Enables a property to be used as a filter on the Microsoft Search results page. | Users can [filter](custom-filters.md) by **URL** if the property is marked as refinable. |

For all connectors except the File share Copilot connector, custom types must be configured manually. To enable search capabilities, the search schema must be mapped to a set of properties. The connection configuration assistant selects a default schema based on the source properties you choose, but you can modify it by selecting the appropriate attributes for each property on the search schema page.

:::image type="content" alt-text="Screenshot that shows how the schema for a connector can be customized." source="media/deployment-overview/manageschema.png" lightbox="media/deployment-overview/manageschema.png":::

### Restrictions and recommendations for search schema settings

- The **content** property supports **search** only. It can’t be marked as **retrieve** or **query**.
- Rendering search results with the **content** property can cause performance issues. For example, using the **Text** field for a [ServiceNow](https://www.servicenow.com) knowledge base article can significantly affect performance.
- Only properties marked as **retrievable** can appear in search results and be used to create modern result types (MRTs).
- Only string properties can be marked as **searchable**.
- All properties mapped to semantic labels must be **retrievable**.
- Properties with the **int** data type can’t be refined.
- A refinable property should also be **queryable** and **retrievable**.
- You can’t remove the **retrievable** attribute from a property.
- You can’t add or remove the **refinable** attribute from a property after setup.

> [!NOTE]
> To update the schema after creating a connection, see [Manage search schema](manage-search-schema.md).

### Customize values for certain schema properties

Some connectors, such as ServiceNow, allow you to customize the values of specific schema properties, such as **AccessURL**, to meet organizational requirements. For example, if your organization uses a custom URL for ServiceNow knowledge articles instead of the default ServiceNow URL, you can configure the **AccessURL** property to point to the correct location. This customized URL is then used in Microsoft Search and Copilot responses.

> [!NOTE]
> To customize schema property values, you must create a new Copilot connector connection. Editing an existing connection to change schema property values isn’t currently supported.

To customize the value of a schema property:

1. During connection setup, select **Custom setup** and authenticate your credentials.
2. Before publishing the connection, open the **Content** tab and go to **Manage properties**.
3. In the **Properties** table, select the property you want to customize (for example, **URL**).
4. In the side panel, locate the **Default expression** section.
5. Enter the expression in the **New default expression** box.
   - Reference variable components by using the exact property name enclosed in `${}`.
6. Select **Save changes** at the bottom of the side panel.
7. Select **Preview data** at the top of the **Content** tab and scroll to the customized property to validate the expression.

**Example**

Assume that a ServiceNow knowledge article URL in your organization looks like this:

`https://instancedomain.service-now.com/sp?id=kb_article&sys_id=1A2bcd3e45f6ghij17890kl1mn2345678o`

Replace the variable component (`sys_id`) with the indexed property name (for example, **SysId**):

`https://instancedomain.service-now.com/sp?id=kb_article&sys_id=${SysId}`

The following table shows more examples.

| Connector | URL in your organization | Default expression |
| --- | --- | --- |
| ServiceNow Knowledge | `https://contosos.service-now.com/serviceportal?id=kb_article_view&sysparm_article=KB0102362` | `https://contosos.service-now.com/serviceportal?id=kb_article_view&sysparm_article=${Number}` |
| ServiceNow Knowledge | `https://custom.contoso.com/knowp?id=kb_article&table=kb_knowledge&sys_id=a3f66636838e9a90` | `https://custom.contoso.com/knowp?id=kb_article&table=kb_knowledge&sys_id=${SysId}` |
| ServiceNow Catalog | `https://custom.contoso.com/sp?id=sc_cat_item&sys_id=bf21d3a54731465c34` | `https://custom.contoso.com/sp?id=sc_cat_item&sys_id=${SysId}` |
| ServiceNow Catalog | `https://contoso.service-now.com/1M_PorTAL?id=sc_cat_item&table=sc_cat_item&sys_id=4df777541b37ab4000` | `https://contoso.service-now.com/1M_PorTAL?id=sc_cat_item&table=sc_cat_item&sys_id=${SysId}` |
| ServiceNow Ticket | `https://contoso.service-now.com/esc?id=ticket&table=sc_req_item&sys_id=113851de1b7894&view=sp` | `https://contoso.service-now.com/esc?id=ticket&table=${EntityType}&sys_id=${SysId}&view=sp` |
| ServiceNow Ticket | `https://contoso.service-now.com/esc?id=ticket&sys_id=a3f66636838e9a9a&table=incident` | `https://contoso.service-now.com/esc?id=ticket&sys_id=${SysId}&table=${EntityType}` |

### Add rules to customization for schema properties

For some connectors, you can override the default expression for specific items by adding rules based on property filters. Examples include:

- **Knowledge Base** for ServiceNow Knowledge
- **Category** for ServiceNow Catalog
- **Entity type** (such as `incident` or `change_request`) for ServiceNow Tickets

To add rules:

1. Complete steps 1–4 in [Customize values for certain schema properties](#customize-values-for-certain-schema-properties).
2. In the **Set additional rules to configure expressions** section, select **Add new rule**.
3. In the side panel:
   - Select the **Filter property** (for example, **KbKnowledgeBase** or **Category**).
   - Enter the **Value** using the exact case from your schema. Separate multiple values with commas.
   - Define the **Expression** to apply.
4. Select **Save changes**.
5. Save changes again at the bottom of the side panel.
6. Use **Preview data** on the **Content** tab to validate the customized expression.

> [!NOTE]
> - If an item matches multiple rules, the first rule in the list is applied.
> - URL changes take effect in Copilot results after the next scheduled full crawl.

**Example**

To apply a different URL expression for ServiceNow knowledge articles in the **IT** and **HR Policy** knowledge bases, set **KbKnowledgeBase** as the filter, specify `IT, HR Policy` as the value, and use an expression such as:

`https://instancedomain.service-now.com/esc?id=kb_article_view&sysparm_article=${Number}`

### Guidelines for crawl settings

The refresh interval controls how often data is synchronized between the source system and Microsoft Search. Optimal schedules vary by data source and depend on how frequently content and metadata change.

Two refresh types are supported: **Full refresh** and **Incremental refresh**. Incremental refresh isn’t available for all data sources.

A full refresh processes and indexes all changed items, regardless of previous crawls. Use a full refresh in scenarios such as:

- Detecting deleted items.
- Recovering from incremental crawl failures.
- Updating ACLs.
- Modifying crawl rules.
- Updating the connection schema.

An incremental refresh processes only items that were created or modified since the last successful crawl. This approach is faster and is best suited for frequent content or metadata updates.

> [!NOTE]
> Incremental crawls don’t currently process updates to **permissions**.

Even when using incremental refreshes, you should run full refreshes periodically to ensure data consistency between the source system and the search index.

### Crawl scheduling

You can configure full and incremental crawls by using the advanced scheduling options on the **Refresh settings** page. Some connectors don’t support incremental crawls. For others, incremental crawling is optional and enabled by default.

A default crawl schedule is selected based on the connector type, but you can change it during connection creation or by editing the connection after publishing.

Available options include:

- **Recurrence**: Daily, weekly, biweekly, or every four weeks.
- **Day**: Run crawls on specific days of the week.
- **Run once a day**: Run a single crawl at a specified start time.
- **Frequency**: Repeat crawls within a day. Intervals range from 15 minutes to 12 hours.
- **Starting time**: The time when the crawl begins.
- **Reset**: Restore the default schedule for the connector.

:::image type="content" alt-text="Screenshot that shows a refresh settings configuration." source="media/deployment-overview/incremental-week-view.png" lightbox="media/deployment-overview/incremental-week-view.png":::

Also consider the following:

- If fields are left blank, Copilot connectors automatically select an optimal start time.
- System load can delay crawl start times by up to an hour.
- If a crawl overlaps with the next scheduled crawl, the next crawl runs only if it’s a different type (full or incremental).

### IP firewall rules

If your data source uses IP firewall rules, allow access to the Copilot connectors service by permitting the following IP ranges.

| Region | Microsoft 365 Enterprise | Microsoft 365 Government |
| --- | --- | --- |
| NAM | 52.250.92.252/30, 52.224.250.216/30 | 52.245.230.216/30, 20.141.117.64/30 |
| EUR | 20.54.41.208/30, 51.105.159.88/30 | N/A |
| APC | 52.139.188.212/30, 20.43.146.44/30 | N/A |

## Related content

- [Prerequisites](prerequisites.md)
- [Connectors gallery](connectors-gallery.md)