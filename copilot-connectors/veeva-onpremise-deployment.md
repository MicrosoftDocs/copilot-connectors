---
title: "Deploy the Veeva On-Premises Microsoft 365 Copilot connector"
ms.author: danielabo
author: danipocket
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.date: 09/08/2026
ms.localizationpriority: Medium
description: "Deploy the Veeva On-Premises Microsoft 365 Copilot connector in the Microsoft 365 admin center."
---

# Deploy the Veeva On-Premises Microsoft 365 Copilot connector

The Veeva On-Premises Microsoft 365 Copilot connector indexes documents and metadata from one Veeva Vault app:
PromoMats, QualityDocs, or RIM. This article describes the steps to deploy and customize the Veeva On-Premises
connector.

For advanced Veeva Vault configuration information, see
[Set up the Veeva Vault service for connector ingestion](veeva-onpremise-admin-setup.md).

## Prerequisites

The Veeva On-Premises connector isn't a direct cloud-to-Veeva connection. It requires the Microsoft Graph
connector agent (GCA), which runs on a Windows computer managed by your organization.

The deployment flow is:

1. Veeva Vault stores documents, metadata, users, and permissions.
2. The Veeva Direct Data API provides bulk access to document content and metadata.
3. The GCA runs in your network, downloads and processes content locally, and applies configured content filters.
4. Microsoft Search and Microsoft 365 Copilot make the indexed content available to authorized users.

The GCA must be installed and registered before you create the connector connection. The GCA host must be able to
reach both Veeva Vault and the required Microsoft 365 endpoints.

Before you deploy the Veeva On-Premises connector, make sure that the Veeva Vault environment is configured in
your organization. The following table summarizes the responsibilities for configuring the environment and
deploying the connector.

| Task | Role |
| --- | --- |
| [Configure Veeva Vault and Microsoft Entra prerequisites](veeva-onpremise-admin-setup.md) | Veeva Vault admin and Microsoft Entra application admin |
| [Install and register the Microsoft Graph connector agent](#install-and-register-the-microsoft-graph-connector-agent) | Windows admin and Microsoft 365 admin |
| [Deploy the connector in the Microsoft 365 admin center](#deploy-the-connector) | Microsoft 365 admin |
| [Customize connector settings](#customize-settings-optional) (optional) | Microsoft 365 admin |

Before you deploy the connector, make sure that you meet the following additional prerequisites:

- You have access to a configured Veeva Vault instance for at least one of the following apps: PromoMats,
   QualityDocs, or RIM.
- The Veeva Direct Data API is enabled for the Vault instance, and the connector account has permission to use it
   and read the documents and metadata that you want to index.
- Microsoft Entra ID is configured for OAuth 2.0/OpenID Connect authentication.
- You have the instance URL and administrator credentials for the selected Veeva Vault app.
- Vault user identities are mapped to Microsoft Entra ID identities. The Federated ID, UPN, email address, or other
   mapped property must match the identity property configured for the connection.
- A Windows computer is available in your network for the GCA. The person installing the GCA must have the required
   Windows permissions, and the person opening or registering the GCA must have the Microsoft role required by your
   organization. In many environments, Search Administrator is required to open the GCA configuration app.
- The required GCA software and runtime prerequisites are installed. Use the
   [Microsoft Graph connector agent documentation](/microsoft-365/copilot/connectors/connector-agent) to confirm the
   supported .NET 8.0.x runtime, Windows version, hardware, proxy, firewall, and network requirements before
   installation.


## Install and register the Microsoft Graph connector agent

> [!IMPORTANT]
> The GCA is required for the Veeva On-Premises connector. The connector uses the Veeva Direct Data API to download
> documents in bulk. Document content is downloaded and processed through the GCA before it is submitted for
> indexing.

To install and register the GCA:

1. Download the latest version of the Microsoft Graph connector agent from
   [https://aka.ms/gca](https://aka.ms/gca) and run the installer on a Windows computer that can reach your Veeva
   Vault instance and the required Microsoft 365 endpoints.
2. Confirm that the GCA host meets the current Windows, .NET 8.0.x, hardware, firewall, proxy, and network
   requirements in the
   [Microsoft Graph connector agent documentation](/microsoft-365/copilot/connectors/connector-agent).
3. Open the GCA configuration app. Sign in with an account that has the required Microsoft 365 role, such as Search
   Administrator where applicable.
4. On the **Registration** tab, enter a name for the agent and provide the application client ID and client secret
   from the Microsoft Entra application.
5. Choose **Register** and wait for registration to complete.
6. Choose **Health Check** and resolve any reported issue before creating the Veeva connection.

## Deploy the connector

To add the Veeva On-Premises connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **Veeva On-Premises**.

### Set display name

The display name identifies references in Copilot responses to help users recognize the associated file or item.
The display name also signifies trusted content and is used as a content source filter.

You can accept the default **Veeva On-Premises** display name, or customize the value to use a display name that
users in your organization recognize.

For more information about connector display names and descriptions, see
[Enhance Copilot discovery of connector content](enhance-copilot-discovery.md).

### Set instance URL

Enter the **Veeva Vault instance URL** for your Vault instance. For example: `https://<your-domain>.veevavault.com`

### Select a connector agent

Select the **Graph connector agent** that you registered earlier from the dropdown. The connector routes all
document downloads through this agent.

### Choose authentication type


#### Microsoft Entra ID OAuth 2.0/OpenID Connect

For Microsoft Entra ID OAuth 2.0/OpenID Connect authentication, provide the following information:

- **Vault session ID URL**: In Veeva Vault, go to **Admin panel** > **Settings** > **OAuth 2.0/OpenID Connect
   Profiles**, and select the profile you created for this connection. Copy the **Vault Session ID URL**.
- **Client ID**: The application ID for the Microsoft Entra application you registered.
- **Client secret**: The client secret associated with the Microsoft Entra application.

Select **Authorize** to sign in with your Microsoft Entra ID account, select **Consent on behalf of your
organization**, and then select **Accept**.

> [!IMPORTANT]
> Configure both Microsoft Entra ID and Veeva Vault admin settings to enable Microsoft Entra ID authentication.

### Roll out

To roll out to a limited audience, select the toggle next to **Rollout to limited audience** and specify the users
and groups to roll the connector out to. For more information, see
[Staged rollout for Copilot connectors](staged-rollout.md).

Choose **Create** to deploy the connection. The Veeva On-Premises connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
| --- | --- |
| Users | Respects Veeva Vault permissions; only viewable documents are accessible. |
| Content | Indexes a minimal set of properties shared across PromoMats, QualityDocs, and RIM. |
| Content filters | No filters; all documents from the selected Vault app are indexed. |
| Sync | Full crawl – daily. Incremental crawl – every 15 minutes. |

To customize these values, select **Custom setup**. For more information, see
[Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the
[Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Veeva On-Premises connector settings. To customize settings, on the
connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

The connector follows the access control lists (ACLs) that you define in Veeva Vault. Only users with view
permissions in Veeva Vault can see the indexed content in Microsoft 365. Admins can optionally grant all users
access to all indexed content. Don't use broad access for confidential content.

#### Map identities

The connector requires that Vault user identities map to the organization's Microsoft Entra ID identities. If the
identities don't automatically match, admins can configure custom user mappings so that access rights are enforced.
For example, you can map identities based on email addresses or other unique identifiers.

The source draft identifies the identity type as `Non-ME-ID`. Select the source and Microsoft Entra properties
prepared during admin setup.

### Customize content settings

#### Configure content filters

You can configure content filters to control which documents are indexed based on Veeva document fields.

Under **Content filter**, configure the following settings:

1. Under **Filter match conditions**, select how multiple filter conditions are combined:

   - **Match all conditions (AND)** – A document must match all conditions to be indexed.
   - **Match any condition (OR)** – A document is indexed if it matches any one condition.

2. Under **Select content by Veeva document fields**, add one or more conditions:

   - In the **doc field** box, enter the Veeva document field name (for example, `status__v`).
   - Select an operator from the dropdown (for example, **In**).
   - In the values box, enter one or more values to match (for example, `["approved_for_use__c","in_review__c"]`).
   - Choose **Add** to add the condition.

3. Repeat to add more conditions as needed.

For example, to index only documents with specific status values, add a condition with the field `status__v`, the
operator **In**, and the values `["approved_for_use__c","in_review__c"]`.

If no conditions are configured, all documents from the selected Vault app are indexed.

#### Manage properties

You can view and manage properties crawled from your Veeva Vault instance. Because this connector supports multiple
Vault apps (PromoMats, QualityDocs, and RIM), the default indexed properties are limited to the fields shared across
all three apps. App-specific and custom fields aren't included by default and must be added manually.

> [!NOTE]
> Most production deployments require custom properties because the default schema includes only fields shared across PromoMats, QualityDocs, and RIM. App-specific and customer-defined fields must be added manually.

The following table lists the properties that the Veeva On-Premises connector indexes by default.

| Property | Semantic label | Description | Schema attributes |
| --- | --- | --- | --- |
| Id | None | Unique document/version identifier from `{document_number__v}_{major_version_number__v}_{minor_version_number__v}`, such as `REF-00001_1_0` | Query, Retrieve |
| DocId | None | Internal Veeva document primary key from `id` | Query, Retrieve |
| DocumentNumber | None | System-assigned Veeva document number from `document_number__v` | Query, Retrieve |
| FileName | `fileName` | Uploaded source-file name from `filename__v` | Query, Retrieve, Search |
| Extension | `fileExtension` | File extension of `filename__v`, such as PDF, DOCX, or PPTX | Query, Retrieve, Search |
| Url | `url` | Direct Veeva document URL built from `{vaultDns}/ui/#doc_info/{id}/{major_version_number__v}/{minor_version_number__v}` | Query, Retrieve |
| MajorVersion | None | Major version number from `major_version_number__v` | Query, Retrieve |
| MinorVersion | None | Minor version number from `minor_version_number__v` | Query, Retrieve |
| Status | `state` | Current lifecycle state from `status__v` | Query, Retrieve, Refine |
| Lifecycle | None | Assigned document lifecycle from `lifecycle__v` | Query, Retrieve |
| Type | `containerName` | Top-level document type from `type__v` | Query, Retrieve |
| DocumentCreationDate | `createdDateTime` | Vault creation date and time from `document_creation_date__v` | Query, Retrieve |
| VersionModifiedDate | `lastModifiedDateTime` | Version modification date and time from `version_modified_date__v` | Query, Retrieve |
| Size | None | File size in bytes from `size__v` | None |
| Content | None| Search |

#### Add custom properties

In addition to the default properties, the connector automatically discovers custom and other document properties
from your Veeva Vault instance. During setup, the connector retrieves all available document fields that are
queryable, not disabled, and not hidden, and presents them as additional properties under **Manage properties**.

You can select and add these custom properties one by one to the connector schema.

For properties that reference Veeva Vault objects (ObjectReference type), the connector also fetches the referenced
object's metadata and exposes its fields as nested properties. For example, if a custom property references a
VObject of type `product__v`, the connector generates properties like `product__v.name__v`,
`product__v.status__v`, and so on. When adding a custom property for an ObjectReference type, you must specify the
exact nested field (for example, `product__v.name__v`), not the parent object (`product__v`).

After adding custom properties, you can customize the schema attributes for any default or custom property under
**Manage properties**. You can enable or disable **Query**, **Retrieve**, **Search**, and **Refine** for each
property based on your organization's requirements.

> [!IMPORTANT]
> Custom properties should be selected during connector creation whenever possible. Modifying the schema after deployment can result in validation failures for certain Veeva fields that use the property__v naming convention.

### Customize sync intervals

Change how often the connector crawls to fit your organization's needs.

- **Full crawl**: By default, runs daily. A full crawl reindexes all documents from the selected Vault app.
- **Incremental crawl**: By default, runs every 15 minutes. An incremental crawl uses the Direct Data API to detect
   and index only documents that changed since the last sync.

For more information, see [Guidelines for crawl settings](deployment-overview.md#guidelines-for-crawl-settings).

## Validate the deployment

After the first full crawl, validate the deployment:

1. Confirm that the connector status is healthy and that the GCA health check passes.
1. Verify that expected documents and properties are indexed.
1. Test queries that use the default properties and any configured aliases.
1. Test source links with a user who has Vault access.
1. Test security trimming with users who have different Vault permissions.
1. Revoke access for a test user, run or wait for the required crawl, and confirm that the user can no longer
   retrieve the document.
1. Confirm that only the intended connector connection is indexing the production content.
1. Confirm that configured content filters include and exclude the expected documents.

## Related content

- [Veeva On-Premises connector overview](veeva-onpremise-overview.md)
- [Troubleshoot issues with the Veeva On-Premises connector](veeva-onpremise-troubleshooting.md)
- [Set up the Veeva Vault service for Veeva On-Premises connector ingestion](veeva-onpremise-admin-setup.md)
- [Microsoft Graph connector agent](/microsoft-365/copilot/connectors/connector-agent)
- [Set up Copilot connectors in the Microsoft 365 admin center](deployment-overview.md)
