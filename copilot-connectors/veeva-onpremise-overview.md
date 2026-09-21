---
title: "Veeva On-Premises Microsoft 365 Copilot connector overview"
ms.author: danielabo
author: danipocket
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: microsoft-365-copilot-connectors
ms.date: 09/08/2026
ms.localizationpriority: Medium
description: "Learn about the capabilities and limitations of the Veeva On-Premises Microsoft 365 Copilot connector."
---

# Veeva On-Premises Microsoft 365 Copilot connector overview

The Veeva On-Premises Microsoft 365 Copilot connector enables organizations to index documents and metadata from
Veeva Vault PromoMats, QualityDocs, and RIM into Microsoft Graph. The indexed content can then be discovered through
Microsoft Search and used by Microsoft 365 Copilot, subject to the permissions configured in Veeva Vault.

## Connector architecture

> [!IMPORTANT]
> The Veeva On-Premises connector uses a hybrid architecture that combines Microsoft 365 services with the
> Microsoft Graph connector agent (GCA) running in your environment. The GCA must be installed and registered on
> a Windows computer managed by your organization. It downloads and processes content from Veeva Vault through
> the Veeva Direct Data API before securely transferring the content to Microsoft Graph. For deployment
> requirements and configuration steps, see
> [Deploy the Veeva On-Premises connector](veeva-onpremise-deployment.md).

The Veeva On-Premises connector uses the following components:

1. **Veeva Vault** stores the documents, metadata, users, and access control information.
2. **The Veeva Direct Data API** provides bulk access to document content and metadata.
3. **The Microsoft Graph connector agent (GCA)** runs on a Windows computer in your network. It connects to Veeva
   Vault, downloads and processes content locally, applies configured filters, and transfers the content to
   Microsoft Graph.
4. **The Veeva On-Premises connector** receives the processed content and makes it available in Microsoft Graph.
5. **Microsoft Search and Microsoft 365 Copilot** use the indexed content while enforcing the configured security model.

The GCA is a required component for the Veeva On-Premises connector. Deployment planning includes installing and
registering the GCA and configuring Microsoft Entra ID OAuth 2.0/OpenID Connect authentication.

## Why use the Veeva On-Premises connector to index your data?

### Business scenarios and benefits

Organizations in life sciences and other regulated industries rely on Veeva Vault as the central repository for
promotional materials, quality documents, and regulatory submissions. Users can search and summarize this content
alongside information in Microsoft 365.

The Veeva On-Premises connector brings Veeva Vault content into Microsoft Graph through an agent that runs within
your environment. This approach gives organizations control over the infrastructure used to download and process
document content while allowing authorized users to discover the content in Microsoft 365.

The Veeva on-premises connector brings Veeva Vault content into Microsoft Graph through an agent that runs within your environment. This approach gives organizations control over the infrastructure used to download and process document content while allowing authorized users to discover the content in Microsoft 365.

- **Keeps data transfer within your control** – The GCA handles downloads from Veeva Vault on infrastructure
  managed by your organization. Documents are processed locally before they are submitted for indexing.
- **Reduces load on Veeva with incremental crawls** – The connector uses the Direct Data API to download content
  in batches and detect changes since the last sync, so only new or modified documents need to be processed during
  an incremental crawl.
- **Supports multiple Vault apps** – The connector supports PromoMats, QualityDocs, and RIM. Each connector
  connection targets one Vault app. To index multiple Vault apps, create a separate connection for each app.
- **Boosts productivity across teams** – Quality, regulatory, marketing, and medical affairs teams can find and
  summarize Vault documents in Microsoft 365 apps such as Teams, SharePoint, and Outlook.

## Choose between the Veeva On-Premises connector and Graph Connector Service connectors

Microsoft 365 provides two ways to connect Veeva Vault content to Microsoft Graph:

- **Veeva On-Premises connector** – Uses the Microsoft Graph connector agent (GCA) to download and process Veeva
  Vault content through the Veeva Direct Data API. The GCA runs on a Windows computer managed by your organization.
- **Graph Connector Service (GCS) connectors** – Existing connector connections for specific Veeva Vault
  applications, including the [Veeva RIM](veeva-rim-overview.md),
  [Veeva PromoMats](veeva-promomats-overview.md), and
  [Veeva QualityDocs](veeva-qualitydocs-overview.md) connectors.

The following table summarizes the main differences:

| Consideration | Veeva On-Premises connector | GCS connectors |
| --- | --- | --- |
| Deployment model | Uses the Microsoft Graph connector agent (GCA) in your environment. | Uses the existing GCS connector experience in the Microsoft 365 admin center. |
| Veeva Vault applications | Supports PromoMats, QualityDocs, and RIM; each connection targets one app. | Uses a separate Veeva RIM, PromoMats, or QualityDocs connector. |
| Data access method | Uses the Veeva Direct Data API for bulk document and metadata retrieval. | Uses the configuration and data access model of the corresponding GCS connector. |

Choose the connector that best matches your organization's deployment, infrastructure, data access, and migration
requirements. The following section provides information about transitioning from a GCS connector to the Veeva
On-Premises connector.

## Considerations when moving from Graph Connector Service to the Veeva On-Premises connector

The Veeva On-Premises connector differs from the Graph Connector Service (GCS) in its deployment architecture and
default indexed properties. The following considerations apply when deploying the Veeva On-Premises connector:

- You need a customer-managed Windows computer with the GCA.
- The GCA requires the software and network configuration described in the
  [Microsoft Graph connector agent documentation](/microsoft-365/copilot/connectors/connector-agent). This includes
  the required .NET 8.0.x runtime version when specified by the GCA requirements.
- The Veeva Direct Data API must be enabled and available to the Vault account used by the connector.
- The best user experience is supported when Veeva Vault users who need to access indexed content have
  corresponding Microsoft Entra ID identities.
- When the Graph Connector Service (GCS) and the Veeva On-Premises connector index the same Vault content, search
  and Copilot responses can reflect content from both connections. Distinct connector labels and an appropriately
  scoped rollout help administrators identify and manage each connection during testing or migration. For migration
  guidance, see [Deploy the Veeva On-Premises connector](veeva-onpremise-deployment.md).

## Build agents with the Veeva On-Premises connector

Developers can use this connector as a knowledge source in declarative agents they build with
[Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio),
[Agent Builder in Microsoft 365 Copilot](/microsoft-365-copilot/extensibility/agent-builder), or the
[Microsoft 365 Agents Toolkit](/microsoft-365/developer/overview-m365-agents-toolkit).

### Example prompts


The following examples show prompts that users can use to retrieve information from Veeva Vault. Replace the bracketed values with values relevant to your organization.

| Scenario | Example prompt | Properties that might be required |
| --- | --- | --- |
| Promotional content retrieval | Find approved promotional materials for [product] that are ready for field deployment. | Product, status, lifecycle, approval state |
| Key message summary | Summarize the key messages in the latest MLR-approved campaign assets for [brand]. | Brand, campaign, approval status, modified date |
| SOP lookup | Retrieve the current SOP for [process] and summarize the key steps. | Document type, process, lifecycle, version |
| CAPA review | List all CAPAs opened in the last quarter related to [product line] and their current status. | CAPA type, product line, creation date, status |
| Regulatory submission summary | Summarize recent regulatory submissions for [product] by region. | Product, region, submission date, submission type |
| Audit preparation | Summarize changes made to quality documents related to [process] for use during a regulatory inspection. | Process, modified date, version, lifecycle, document role |

Results depend on indexed fields, crawl status, source-file support, and the user's permissions. Prompts that
require nondefault fields work only after an administrator adds those fields to the connector schema.

## Veeva on-premises connector capabilities and limitations

The Veeva on-premises connector enables you to:

- Index documents and metadata from PromoMats, QualityDocs, and RIM.
- Search and summarize supported Vault content with links to source documents.
- Enforce Vault-derived access control lists (ACLs) through mapped Microsoft Entra identities.
- Filter indexed documents by configurable Veeva fields on the GCA.
- Synchronize changed content with incremental crawls.
- Process downloaded content on customer-managed infrastructure before indexing.

The Veeva on-premises connector has the following limitations and configuration considerations:

- The connector primarily supports text-based files. Images and video aren't supported.
- Documents larger than 20 MB aren't included in indexing. For accepted files, the connector indexes at most 4 MB
  of extracted text.
- The GCA is installed, registered, and running on Windows infrastructure managed by your organization.
- The Veeva Direct Data API must be enabled. If the API isn't enabled or the connector account doesn't have the
  required access, validation or crawl operations might report an `Operation Not Allowed` error. API enablement and
  account permissions are part of the connection prerequisites.
- Document fields configured as hidden on the Veeva platform aren't indexed.
- Custom properties become available for queries after an administrator selects them for the connector schema and
  configures the appropriate schema attributes and semantic labels or aliases.
- Updates to user or group permissions in Vault are synchronized according to the configured crawl schedule.
- Document Roles and some permission changes might not be fully captured during every incremental crawl. A full
  crawl might be required before access changes are completely reflected in Microsoft Graph.
- When the Graph Connector Service (GCS) and the Veeva On-Premises connector index the same content, search and
  Copilot responses can reflect content from both connections. Distinct labels and an appropriately scoped rollout
  help administrators identify and manage each connection when testing or transitioning between connections.

## Data types indexed from Veeva Vault

The connector ingests documents and associated metadata from the selected Vault app so that they become available
in Copilot and Microsoft Search. At a high level, it indexes:

- Supported file content for documents in the selected PromoMats, QualityDocs, or RIM app.
- Shared document metadata, including document ID and number, file name and extension, source URL, type, lifecycle,
  status, major and minor version, creation and modified dates, and size.
- Administrator-selected custom document fields that are queryable, enabled, and visible.
- Nested fields from supported referenced Veeva objects when an ObjectReference child field is selected.

Indexed items are available to Microsoft Search, Microsoft 365 Copilot, and supported agents, subject to the
configured schema and permissions.

## Permissions model and access control

The On-Premises connector can be configured so that only users with view access to a given document in Vault can
see it in Copilot responses or search results. The model works as follows:

- **Vault permissions and access control lists (ACLs)**: If a document in the Vault app is restricted, for example
  to certain groups, regions, roles, or Document Roles, the connector uses the configured Vault permissions when
  indexing the document.
- **User identity mapping**: Vault user identities are mapped to your organization's Microsoft Entra ID identities.
  When the identities don't automatically match, administrators can configure custom identity mappings. A matching
  Microsoft Entra ID identity supports access to the corresponding content in Microsoft 365.
- **Visible to everyone option**: For content that isn't confidential and is intended for broad access, the
  connector administrator can configure the content to be visible to everyone. This option is intended for content
  that meets your organization's security requirements.
- **Access-change latency**: Changes to permissions in Vault might not instantly reflect in the index; if a
  permission is revoked, there can be a delay until the next full crawl.

Post-deployment validation includes test accounts that represent the relevant Vault roles and groups. An authorized
user can be expected to find the relevant document, and access changes can be validated after the applicable crawl
has completed.

## Next step

> [!div class="nextstepaction"]
> [Deploy the Veeva On-Premises connector](veeva-onpremise-deployment.md)
