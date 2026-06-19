---
title: "Deploy the Salesforce CRM connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 6/18/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the Salesforce CRM Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Salesforce CRM connector

The Salesforce CRM Microsoft 365 Copilot connector enables your organization to index Salesforce records, such as accounts, contacts, leads, opportunities, and cases, so users can discover that content in Copilot and Microsoft Search.

This article describes the steps to deploy and customize the Salesforce CRM connector.

For advanced Salesforce configuration information, see [Set up the Salesforce service for connector ingestion](salesforce-crm-admin-setup.md).

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be a Microsoft 365 admin.
- You have the Salesforce instance URL in the format `https://<domain>.my.salesforce.com`.
- You created a Salesforce connected app for OAuth 2.0 and have the consumer key and consumer secret.
- The Salesforce account used during connector authorization has required API and object permissions.
- The Salesforce CRM connector supports OAuth 2.0 authentication. Before you begin, create an External Client App in Salesforce and note the consumer key and consumer secret. For setup steps, see [Create an External Client App](salesforce-crm-admin-setup.md#create-an-external-client-app).

## Deploy the connector

To add the Salesforce CRM connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, select **Copilot** > **Connectors**.
1. Select the **Gallery** tab.
1. From the list of available connectors, select **Salesforce CRM**.

### Set display name

The display name identifies references in Copilot responses so users can recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **Salesforce CRM** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

### Set instance URL

For the instance URL, enter your Salesforce domain URL in the format `https://<domain>.my.salesforce.com`.

### Choose authentication type

To authenticate:

1. Select **OAuth 2.0**.
1. Enter the client ID (consumer key) and client secret from Salesforce.
1. Select **Authorize** and complete the Salesforce sign-in prompt.

If the sign-in prompt doesn't appear, allow browser pop-ups and redirects.

### Roll out

To roll out to a limited audience, select the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](staged-rollout.md).

Select **Create** to deploy the connection. The Salesforce CRM connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|---------------|
| Users | Access permissions are set to only people with access to this data source. Identities are mapped by using Microsoft Entra ID. |
| Content | Accounts, contacts, leads, opportunities, and cases are indexed. No modified-time filter or SOQL filter is applied by default. |
| Sync | Incremental crawl runs every 15 minutes. Full crawl runs every day. |

> [!NOTE]
> If your Salesforce users don't have Microsoft Entra ID identities mapped, configure identity mapping before creating the connection. For details, see [Map identities](#map-identities).

To customize these values, select **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Salesforce CRM connector settings. To customize settings, on the connector page in the admin center, select **Custom setup**.

### Customize user settings

#### Access permissions

The Salesforce CRM connector supports search permissions visible to **Everyone** or **Only people with access to this data source**. If you choose **Everyone**, all users see the indexed data in the search results. If you choose **Only people with access to this data source**, only users who have access in Salesforce see the indexed data in search results.

#### Map identities

You can map both Microsoft Entra identities and non-Microsoft Entra identities from Salesforce ACLs.

To map non-Microsoft Entra identities, see [Map your non-Microsoft Entra identities](map-non-entra-id.md). To map Microsoft Entra identities, see [Map your Microsoft Entra identities](map-entra-id.md).

### Customize content settings

#### Query string

Use a Salesforce Object Query Language (SOQL) `WHERE` clause to limit indexed data to specific records or criteria. You can also set a modified-time window to index only records created or changed in a rolling period.

#### Manage properties

You can add or remove source properties and assign schema attributes to each property. The following table lists the default properties indexed by the connector. The **Attributes** column indicates whether a property is searchable (S), queryable (Q), retrievable (R), or refinable (Ref).

| Property | Label | Description | Attributes |
|---|---|---|---|
| Id | `-` | Unique Salesforce record identifier (18-char). Maps to the external item ID in the Graph connection. | S, Q, R |
| Url | `url` | Direct URL to open the record in Salesforce. | R |
| IconUrl | `iconUrl` | URL to the object-type icon asset displayed on search result cards. | R |
| ObjectName | `itemType` | CRM object type name (Account, Contact, Lead, Opportunity, Case). | S, Q, R |
| Type | `-` | Record sub-classification within an object (for example, Customer or Partner for Account; Problem or Question for Case). Null for Lead and Contact. | S, Q, R |
| Source | `-` | Marketing or lead attribution source indicating how the record entered the pipeline (for example, Web, Phone Inquiry, Partner Referral). | S, Q, R |
| Number | `secondaryId` | Account number or Case number. Null for Contact, Lead, and Opportunity. | S, Q, R |
| Name | `title` | Primary display name of the record (for example, account company name, contact full name, opportunity deal name, case subject). | S, Q, R |
| Description | `-` | Free-text description field. Mapped to the content property for semantic search and Copilot summarization. | S |
| Owner | `assignedToPeople` | The user who owns this record. | S, Q, R |
| CreatedBy | `createdBy` | The user who created this record. | R |
| CreatedDate | `createdDateTime` | Timestamp when the record was created. | Q, R, Ref |
| LastModifiedBy | `lastModifiedBy` | The user who last modified this record. | R |
| LastModifiedDate | `lastModifiedDateTime` | Timestamp of the most recent modification to the record. | Q, R, Ref |
| AccountName | `-` | Name of the related Account record. For Lead, only populated after conversion. | S, Q, R |
| AccountId | `-` | Salesforce ID of the related Account record. For Lead, only populated after conversion. | S, Q, R |
| ContactName | `-` | Full contact name. For Contact and Lead, computed from Salutation, FirstName, and LastName. For Opportunity and Case, the related Contact's name. Null for Account. | S, R |
| ContactId | `-` | Salesforce ID of the related Contact record. | R |
| ContactDetails | `-` | Consolidated contact details combining phone, email, and fax fields into a searchable JSON string. | S, R |
| Email | `-` | Primary email address. Null for Account and Opportunity. | S, Q, R |
| Address | `-` | Consolidated address field combining all address sources per object into a searchable JSON string. | S, R |
| Status | `-` | Lifecycle status of the record (for example, Open, Closed Won, Qualified). Null for Account and Contact. | S, Q, R |
| IsClosed | `-` | Boolean indicating the record has reached a terminal state. For Lead, maps from IsConverted. Null for Account and Contact. | Q, R |
| LastActivityDate | `-` | Date of the most recent logged activity on the record. Null for Case. | Q, R |
| Industry | `-` | Industry classification (for example, Technology, Healthcare, Finance). Only populated for Account and Lead. | S, Q, R |
| Rating | `-` | Engagement rating (Hot, Warm, Cold). Only populated for Account and Lead. | S, Q, R |
| Website | `-` | Company website URL. Only populated for Account and Lead. | S, R |
| AnnualRevenue | `-` | Annual revenue of the company, normalized to the organization's base currency. Only populated for Account and Lead. | Q, R |
| NumberOfEmployees | `-` | Number of employees at the company. Only populated for Account and Lead. | Q, R |
| ParentId | `parentId` | Foreign key to the parent record. Account links to parent Account; Case links to parent Case. | Q |
| ParentName | `-` | Display name of the parent record. | S, R |
| ParentUrl | `parentUrl` | URL deep link to the parent record in Salesforce. | S |
| ClosedDate | `-` | Date the record was closed or converted. Null for Account and Contact. | Q, R, Ref |
| Ownership | `-` | Account only. Ownership structure (Public, Private, Subsidiary, Other). | S, R |
| TickerSymbol | `-` | Account only. Stock market ticker symbol. Only relevant for publicly traded companies. | S, R |
| SicCode | `-` | Account only. Standard Industrial Classification (SIC) code for industry categorization. | S, R |
| Site | `-` | Account only. Location descriptor label for the account (for example, HQ, Branch, Regional Office). | S, R |
| JobTitle | `-` | Contact only. Job title of the contact (for example, VP of Engineering, CTO). | S, R |
| Department | `-` | Contact only. Department the contact belongs to (for example, Engineering, Sales, Marketing). | S, R |
| Birthdate | `-` | Contact only. Contact's date of birth. | Q, R, Ref |
| AssistantName | `-` | Contact only. Name of the contact's administrative assistant. | S, R |
| ReportsTo | `-` | Contact only. Name of the contact's manager or supervisor. | S, R |
| ReportsToId | `-` | Contact only. Salesforce ID of the contact's manager or supervisor. | R |
| ConvertedDate | `-` | Lead only. Date when the lead was converted to a Contact, Account, and Opportunity. Null for unconverted leads. | S, Q |
| ConvertedOpportunityName | `-` | Lead only. Name of the Opportunity record created during lead conversion. | S, Q |
| ConvertedOpportunityId | `-` | Lead only. Salesforce ID of the Opportunity record created during lead conversion. | R |
| Company | `-` | Lead only. Company or organization name for the lead. | S, Q |
| Stage | `-` | Opportunity only. Pipeline stage (for example, Prospecting, Negotiation, Closed Won). | S, Q, R |
| Amount | `-` | Opportunity only. Deal monetary value, normalized to the organization's base currency. | Q, R |
| Probability | `-` | Opportunity only. Estimated probability of winning the deal as a percentage (0-100). | Q, R |
| ExpectedRevenue | `-` | Opportunity only. Weighted expected revenue calculated as Amount multiplied by Probability. | Q, R |
| NextStep | `-` | Opportunity only. Free-text field describing the next planned action for this deal. | S, R |
| IsWon | `-` | Opportunity only. Boolean flag indicating whether the opportunity was won. | Q, R |
| ForecastCategory | `-` | Opportunity only. Sales forecast category bucket (Pipeline, Best Case, Commit, Closed). | S, Q, R |
| FiscalQuarter | `-` | Opportunity only. Fiscal quarter number (1-4). | Q, R |
| FiscalYear | `-` | Opportunity only. Fiscal year number. | Q, R |
| Fiscal | `-` | Opportunity only. Human-readable fiscal period label (for example, 2026 Q2). | S, R |
| Subject | `-` | Case only. Case subject line or headline summarizing the issue. | S, R |
| Priority | `priority` | Case only. Case priority (High, Medium, Low, Critical). | R |
| Reason | `-` | Case only. Root cause category (for example, Installation, Performance, User Error). | S, Q, R |
| IsEscalated | `-` | Case only. Boolean flag indicating the case has been escalated. | Q, R |
| SuppliedEmail | `-` | Case only. Email address submitted through Web-to-Case or Email-to-Case. | S, Q |

#### Include FLS-restricted fields

Salesforce field-level security (FLS) hides specific fields from selected profiles or permission sets. The connector detects these fields in your selected entities and excludes them from the crawl by default. On the **Content** tab, you can opt in to index specific fields. Coordinate with your Salesforce admin first; for the Salesforce-side preparation, see [Verify field-level security (FLS) settings](salesforce-crm-admin-setup.md#verify-field-level-security-fls-settings).

When the connector finds FLS-restricted fields, a banner appears at the top of the **Content** tab with the affected counts and a summary pill (for example, **0 of 6 FLS fields included**). Select **Show FLS Fields** to expand the **Field-Level Security Review** panel.

The panel groups fields by entity. Expand an entity, then for each field:

- **Field Name**: The API name of the field in Salesforce.
- **Restricted Permission Sets**: The Salesforce profiles or permission sets restricted from the field.
- **Include in Crawl**: Switch the toggle to **Yes** to index the field. Use **Select All** to include every FLS field in an entity at once.

Opted-in fields appear in the **Manage properties** table with an **FLS** badge. Excluded FLS fields don't appear there.

> [!WARNING]
> When you set **Include in Crawl** to **Yes**, the field is indexed for all Microsoft 365 users who have access to the records of the entity, regardless of the Salesforce FLS restrictions. Only opt in after your Salesforce admin confirms the field is safe to share broadly in Microsoft Search and Microsoft 365 Copilot.

#### Add properties

Select **Add Properties** to open the side panel where you can choose fields to index. Two categories of fields are available:

- **Custom fields** - Fields with API names ending in `__c` that your organization creates.
- **Standard fields** - Fields that exist on the object but aren't included in the connector's default schema.

You can ingest selected fields in two ways:

- **Content key-value** - The field value is included in the item's content for full-text search. This method is the default when you select a field.
- **Schema property** - The field is promoted to a queryable, searchable, retrievable, or refinable property. This method enables structured search, filtering, and ranking in Copilot and Search.

If you need advanced capabilities such as filtering, sorting, or structured queries on a field, select schema annotations (Searchable, Queryable, Retrievable, Refinable) for that field. For definitions of each annotation, see [Define the schema](/graph/connecting-external-content-manage-schema).

> [!NOTE]
> When you select an annotation for a field, the field is promoted to a schema property and counts against the property limit per connection. If you select **Queryable**, it also counts against the queryable property limit. The side panel displays counters so you can monitor usage against these limits.

### Customize sync intervals

You can customize both full crawl and incremental crawl intervals. The default values are a daily full crawl and a 15-minute incremental crawl.

> [!NOTE]
> Full crawls consume Salesforce API quota. For organizations with large record volumes, consider scheduling full crawls during off-peak hours or weekends.

For more information, see [Guidelines for crawl settings](deployment-overview.md#guidelines-for-crawl-settings).

## Related content

- [Salesforce CRM connector overview](salesforce-crm-overview.md)
- [Troubleshoot issues with the Salesforce CRM connector](salesforce-crm-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](deployment-overview.md)

