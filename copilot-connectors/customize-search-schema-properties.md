Microsoft 365 Copilot connectors allow organizations to integrate
external data sources into Microsoft 365 experiences, including Copilot
and Microsoft Search. Customizing the search schema is essential for
optimizing how data is indexed, queried, and displayed in search
results. This article explains the key schema properties, attributes,
and customization options available to admins.

------------------------------------------------------------------------

## What is a Search Schema?

A **search schema** defines how properties from your data source are
indexed and made available for search, query, retrieval, and refinement.
It determines what information users can find and how it appears in
Microsoft 365 experiences.

------------------------------------------------------------------------

## Key Search Schema Attributes

Each property in your connector’s schema can be configured with the
following attributes:

| **Attribute** | **Function** | **Example** |
|----|----|----|
| **SEARCH** | Makes the text content of a property searchable (full-text index). | If the property is title, a query for "Enterprise" returns items with "Enterprise" in the title or text. |
| **QUERY** | Allows programmatic or verbatim queries for a specific property. | If the Title property is queryable, you can use Title:Enterprise in a search. |
| **RETRIEVE** | Enables the property to be displayed in search results. | Only retrievable properties can be shown in result types. |
| **REFINE** | Allows filtering by the property on the search results page. | Users can filter by URL if the property is marked as refinable. |

**Note:** The "int" datatype properties cannot be refined, even if
marked as refinable. Only string properties can be marked searchable.
The content property is searchable only and cannot be used with retrieve
or query options.

## Customizing Schema Properties

**Manage Properties**

Admins can configure source properties to be:

- **Searchable**: Included in full-text index.

- **Queryable**: Used in direct queries.

- **Retrievable**: Displayed in search results.

- **Refinable**: Used for filtering results.

You can assign **semantic labels** and **aliases** to properties to
enhance search relevance and unify filters across multiple connections.

**Semantic Labels**

Semantic labels are well-known tags provided by Microsoft that add
meaning to properties and enable integration with Microsoft 365
experiences. Common labels include:

- **title**: Title shown in search and other experiences.

- **url**: Target URL of the item.

- **Created By**: Creator’s name.

- **Last modified by**: Last editor’s name.

- **Authors**: Collaborators’ names.

- **Created date time**: Creation timestamp.

- **Last modified date time**: Last edit timestamp.

- **File name**: Name of the file.

- **File extension**: File type (e.g., PDF, DOC).

The title label is especially important for participating in result
cluster experiences. Not all labels need to be assigned, but incorrect
mapping can degrade search quality.

**Aliases**

Aliases are friendly names for properties, used in queries and filters.
They help normalize property names across multiple connections, enabling
unified filtering.

## Custom Setup Options

When configuring a connector, admins can choose **Custom Setup** for
advanced schema control. This provides access to three tabs:

- **Users**: Configure access permissions and identity mapping.

- **Content**: Manage properties, assign labels and aliases, and set
  schema attributes.

- **Sync**: Adjust data refresh intervals and crawl schedules.

------------------------------------------------------------------------

## Guidelines and Recommendations

- Only properties marked as **retrievable** can be shown in search
  results and used to create modern result types (MRTs).

- The **content** property is for search only; it cannot be retrieved or
  queried.

- For optimal performance, avoid rendering search results with the
  content property (e.g., large text fields).

- To update the schema after connection creation, refer to the "manage
  search schema" documentation.
