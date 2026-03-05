---
title: "Deploy the Veeva Vault RIM Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: anggao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 03/05/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the Veeva Vault RIM Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Veeva Vault RIM Microsoft 365 Copilot connector

The Veeva Vault RIM Microsoft 365 Copilot connector allows organizations to index regulatory submissions and compliance documents from Veeva Vault into Microsoft Graph, making them accessible across Microsoft 365 experiences, including Microsoft 365 Copilot and Microsoft Search. The connector integrates Vault RIM's built-in permission model to ensure that users can only access authorized content. It enhances content generation and review speed through intelligent content analysis and preparation. By streamlining the entire regulatory submission lifecycle, the connector helps submitters track submission status more effectively and significantly reduces turnaround times.

This article describes the steps to deploy and customize the Veeva Vault RIM connector. For general information about Copilot connector deployment, see [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365-copilot/connectors/deployment-overview).

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be a Microsoft 365 admin.
- The Veeva Vault RIM instance must be accessible and properly configured.
- Microsoft Entra ID must be set up for authentication.
- Required permissions and roles must be assigned in Veeva Vault and Microsoft 365.

### Register an application and configure OAuth

Use the following steps to configure Microsoft Entra ID OAuth 2.0/OpenID Connect for the Veeva RIM connector.

1. Register an application in Microsoft Entra ID.
   - Go to **Microsoft Entra admin center** > **App registrations** > **New registration**.
   - Name the application and select **Accounts in this organizational directory only**.
   - Add the redirect URI:
     - For Microsoft 365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`
     - For Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
   - Generate a client secret under **Certificates & Secrets** and store it securely.

2. Configure OAuth in Veeva RIM.
   - Go to **Admin > Settings > OAuth 2.0/OpenID Connect Profiles**.
   - Create a new profile, set the **Status** to active, and select **Azure AD** as the provider.
   - Choose **Upload AS metadata** > **Provide Authorization Server Metadata URL**, and paste the following link. Replace {tenant-id} with your tenant ID.
     `https://login.microsoftonline.com/{tenant-id}/v2.0/.well-known/openid-configuration`
   - Set **Identity is in another claim** to `upn`, and in **User ID Type**, select **Federated ID**. The UPN should be the same as the federated ID.
   - Choose **Client Applications** > **Add**, and use the client ID from your Microsoft Entra ID application for both **Application Client ID** and **Authorization Server Client ID**. Add an **Application Label**.

    > [!NOTE]
    > To enable **Perform strict Audience Restriction validation**, add the client ID to the **Audience** field.
3. Create security policies and link users.
   - Go to **Admin > Settings > Security Policies** > **Create** > **Single sign-on**. Provide a name and description, and set the status to **active**.
   - For the authentication type, choose **Single Sign-on**, and choose a profile. For more information, see [Configuring Single Sign-on](https://platform.veevavault.help/en/gr/13977/).
   - In **eSignature Profile**, select **None**, and in **OAuth 2.0 / OpenID Connect Profile**, select the OAuth 2.0 profile that you created. Keep the default values for the remaining settings.
   - Go to **Admin** > **Users & Groups**, select the vault owner, and choose **Edit**.
   - In **Details** > **Security Policy**, change the values to the new policy, and in **Federated ID**, change the value to the UPN of the connector admin account.

## Deploy the connector

To add the Veeva Vault RIM connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
2. Choose the **Gallery** tab.
3. From the list of available connectors, choose **Veeva Vault RIM**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.  

You can accept the default **Veeva Vault RIM** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](/microsoft-365-copilot/connectors/enhance-copilot-discovery).

### Set instance URL

Enter the URL of your Veeva Vault RIM instance. For example:  
`https://<your-vault-domain>.veevavault.com`

### Choose authentication type

To authenticate the Veeva RIM connector, for the **Authentication type**, choose **Microsoft Entra ID OIDC**, and provide the following information:

- **Vault session ID URL**: In Veeva RIM, go to **Admin panel** > **Settings** > **OAuth 2.0/ OpenID Connect Profiles**, and choose the profile you created for this connection. Copy the Vault Session ID URL.
- **Client ID**: The application ID for the Entra application you registered for Veeva RIM.
- **Client secret**: The client secret associated with the Entra application.

Select **Authorize** to sign in with your Entra ID account, and select **Consent on behalf of your organization**, and then on the permission request screen, choose **Accept**.

> [!IMPORTANT]
> Configure both Microsoft Entra ID and Veeva RIM admin settings to enable Microsoft Entra ID authentication.

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](/microsoft-365-copilot/connectors/staged-rollout).  
Choose **Create** to deploy the connection. The Veeva Vault RIM Copilot connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|--------------|
| Users    | Respects Veeva Vault permissions; only viewable documents are accessible. |
| Content  | Indexes key metadata, such as document name, owner, and lifecycle stage. Enables metadata like title, created by, and last modified by. |
| Sync     | Full crawl—daily. |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).  
After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Veeva Vault RIM connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

The connector adheres to the access control lists (ACLs) defined in Veeva Vault. Only users with view permissions in Veeva Vault can see the indexed content in Microsoft 365. Admins can optionally allow all users access to all indexed content, although this approach isn't recommended.

#### Mapping identities

If you want to enforce the security settings of your Veeva RIM instance, choose **Non-ME-ID** as the identity type for your content source.

Enter the required information for identity mapping. For example, if you want to map identities based on email addresses:

1. For the **Microsoft Entra user property**, select **Mail**.
2. Under **non-Microsoft Entra user property**, select **Add identity property**, and choose **Email**. Use an expression such as `([^@]+)` to capture a sequence of one or more characters that are not the `@` symbol.
Create a formula to complete the mapping, such as `{0}@<your-domain>`.

### Customize content settings

#### Query string

You can use query string conditions to precisely control the synchronization of articles, ensuring efficient indexing.

#### Manage properties

The following table lists the properties that the Veeva Vault RIM connector indexes by default.

| Property               | Veeva field                                                                              | Semantic label       | Description                                                           | Schema attributes              |
|------------------------|------------------------------------------------------------------------------------------|----------------------|-----------------------------------------------------------------------|--------------------------------|
| Id                     | document_number_version                                                                  |                      | Unique identifier of the document composed of document number and version | Query, Retrieve            |
| DocumentNumber         | document_number__v                                                                       |                      | System-assigned document number in the Veeva system                  | Query, Retrieve                |
| GlobalId               | global_id__sys                                                                           |                      | System-generated globally unique identifier across Vaults            | Query, Retrieve, Search        |
| Name                   | name__v                                                                                  | title                | Document name or title (up to 100 characters)                        | Query, Retrieve, Search        |
| FileName               | filename__v                                                                              | fileName             | Name of the uploaded source file                                     | Query, Retrieve, Search        |
| Extension              | file extension of filename__v                                                            | fileExtension        | File type extension (for example, PDF, DOCX, PPTX)                  | Query, Retrieve, Search        |
| Url                    | https://{vaultDns}/ui/#doc_info/{id}/{major_version_number__v}/{minor_version_number__v} | url                  | Direct URL to access or preview the document in Veeva Vault          | Query, Retrieve                |
| Status                 | status__v                                                                                | state                | Current lifecycle state of the document (for example, Draft, Approved, Effective) | Query, Retrieve, Refine |
| DocumentId             | id                                                                                       |                      | Unique document identifier (primary key) in the Veeva system         | Query, Retrieve                |
| Version                | {major_version_number__v}_{minor_version_number__v}                                      |                      | Combined version string of the document                              | Query, Retrieve                |
| UrlRoutingId           | concat(id, '/', major_version_number__v, '/', minor_version_number__v)                   |                      | Composite routing identifier used for URL resolution                 | Query, Retrieve                |
| MajorVersion           | major_version_number__v                                                                  |                      | Major version number of the document (for example, the "2" in v2.1) | Query, Retrieve                |
| MinorVersion           | minor_version_number__v                                                                  |                      | Minor version number of the document (for example, the "1" in v2.1) | Query, Retrieve                |
| Type                   | type__v                                                                                  | containerName        | Top-level document type classification                               | Query, Retrieve                |
| Subtype                | subtype__v                                                                               |                      | Second-level document classification under type                      | Query, Retrieve                |
| Product                | product__v.name__v                                                                       |                      | Product associated with the document                                 | Query, Retrieve                |
| Country                | country__v.name__v                                                                       |                      | Country or region associated with the document                       | Query, Retrieve                |
| Format                 | format__v                                                                                |                      | File format of the source document                                   | Query, Retrieve                |
| ItemType               | format__v                                                                                | itemType             | Item type derived from the document format                           | Query, Retrieve, Refine        |
| ItemPath               | {type__v}/{subtype__v}                                                                   | itemPath             | Hierarchical path combining the document type and subtype            | Query, Retrieve                |
| DocumentCreationDate   | document_creation_date__v                                                                | createdDateTime      | Date and time the document was created in Vault                      | Query, Retrieve                |
| VersionModifiedDate    | version_modified_date__v                                                                 | lastModifiedDateTime | Date and time when this version was last modified                    | Query, Retrieve                |
| CreatedBy              | created_by__v (name, email)                                                              | createdBy            | User who originally created the document                             | Query, Retrieve, Search        |
| CreatedByUserId        | created_by__v                                                                            |                      | Internal user identifier for the document creator                    | Query, Retrieve                |
| LastModifiedBy         | last_modified_by__v (name, email)                                                        | lastModifiedBy       | User who last modified the document                                  | Query, Retrieve, Search        |
| LastModifiedByUserId   | last_modified_by__v                                                                      |                      | Internal user identifier of the last modifier                        | Query, Retrieve                |
| Lifecycle              | lifecycle__v                                                                             |                      | Lifecycle assigned to the document                                   | Query, Retrieve                |
| Size                   | size__v                                                                                  |                      | File size of the document                                            |                                |
| Content                | document content                                                                         |                      | Main text or body content extracted from the document                | Search                         |
| ApprovedDate           | approved_date__c                                                                         |                      | Date when the document was approved                                  | Query, Retrieve                |
| AnnotationsAll         | annotations_all__v                                                                       |                      | Total count of all annotations on the document                       | Query, Retrieve                |
| AnnotationsAnchors     | annotations_anchors__v                                                                   |                      | Count of anchor annotations on the document                          | Query, Retrieve                |
| AnnotationsApproved    | annotations_approved__v                                                                  |                      | Count of approved annotations on the document                        | Query, Retrieve                |
| AnnotationsAuto        | annotations_auto__v                                                                      |                      | Count of auto-generated annotations on the document                  | Query, Retrieve                |
| AnnotationsClaim       | annotations_claim__v                                                                     |                      | Count of claim annotations on the document                           | Query, Retrieve                |
| AnnotationsLines       | annotations_lines__v                                                                     |                      | Count of line annotations on the document                            | Query, Retrieve                |
| AnnotationsLinks       | annotations_links__v                                                                     |                      | Count of link annotations on the document                            | Query, Retrieve                |
| AnnotationsNotes       | annotations_notes__v                                                                     |                      | Count of note annotations on the document                            | Query, Retrieve                |
| AnnotationsPermalink   | annotations_permalink__v                                                                 |                      | Count of permalink annotations on the document                       | Query, Retrieve                |
| AnnotationsResolved    | annotations_resolved__v                                                                  |                      | Count of resolved annotations on the document                        | Query, Retrieve                |
| AnnotationsUnresolved  | annotations_unresolved__v                                                                |                      | Count of unresolved annotations on the document                      | Query, Retrieve                |
| FileCreatedBy          | file_created_by__v                                                                       |                      | User who created the uploaded source file                            | Query, Retrieve                |
| FileCreatedDate        | file_created_date__v                                                                     |                      | Date when the uploaded source file was created                       | Query, Retrieve                |
| FileMetaAuthor         | file_meta_author__v                                                                      |                      | Author metadata extracted from the source file                       | Query, Retrieve                |
| FileMetaKeywords       | file_meta_keywords__v                                                                    |                      | Keywords metadata extracted from the source file                     | Query, Retrieve                |
| FileModifiedBy         | file_modified_by__v                                                                      |                      | User who last modified the uploaded source file                      | Query, Retrieve                |
| FileModifiedDate       | file_modified_date__v                                                                    |                      | Date when the uploaded source file was last modified                 | Query, Retrieve                |
| SourceDocumentId       | source_document_id__v                                                                    |                      | Identifier of the source document this version was derived from      | Query, Retrieve                |
| SourceDocumentName     | source_document_name__v                                                                  |                      | Name of the source document this version was derived from            | Query, Retrieve                |
| VersionCreatedBy       | version_created_by__v (name, email)                                                      |                      | User who created this specific document version                      | Query, Retrieve, Search        |
| VersionLink            | version_link__sys                                                                        |                      | System link to the document version                                  | Query, Retrieve                |
| HealthAuthorityVersion | health_authority_version__c                                                              |                      | Health authority version identifier for regulatory submissions       | Query, Retrieve                |
| IdmpSubmissionDate     | idmp_submission_date__v                                                                  |                      | Identification of Medicinal Products (IDMP) submission date          | Query, Retrieve                |
| IncludeForAllLanguages | include_for_all_languages__v                                                             |                      | Indicates whether the document is included for all language versions  | Query, Retrieve                |
| MasterFileCode         | master_file_code__v                                                                      |                      | Master file code for the regulatory document                         | Query, Retrieve                |
| MasterFileIdentifier   | master_file_identifier__v                                                                |                      | Master file identifier for the regulatory document                   | Query, Retrieve                |
| RIMAutoClassification  | rim_autoclassification__v                                                                |                      | RIM auto-classification value assigned to the document               | Query, Retrieve                |
| TemplateDocument       | template_document__v                                                                     |                      | Indicates whether the document is a template                         | Query, Retrieve                |
| XevmpdSubmissionStatus | xevmpd_attachment_only_submission_status__v                                              |                      | Extended EudraVigilance Medicinal Product Dictionary (XEVMPD) attachment-only submission status | Query, Retrieve |

#### Add custom properties

In addition to the default properties, the connector automatically discovers custom and other document properties from your Veeva PromoMats instance. During setup, the connector retrieves all available document fields that are queryable, not disabled, and not hidden, and presents them as additional properties under **Manage properties**.

You can select and add these custom properties one by one to the connector schema. Each added custom property has the following default schema attributes:

- **Query** and **Retrieve** are enabled by default.
- **Search** and **Refine** aren't enabled by default but can be turned on on the **Manage properties** custom setup.

For properties that reference Veeva Vault objects (ObjectReference type), the connector also fetches the referenced object's metadata and exposes its fields as nested properties. For example, if a custom property references a VObject of type `campaign__v`, the connector generates properties like `campaign__v.name__v`, `campaign__v.status__v`, and so on.

After adding custom properties, you can customize the schema attributes for any property—both default and custom—under **Manage properties**. You can enable or disable **Query**, **Retrieve**, **Search**, and **Refine** for each property based on your organization's requirements.

### Customize sync intervals

You can modify the frequency of full crawls to fit your organization's requirements. The following are the default crawls:
- Full crawl—daily.

For more information, see [Guidelines for sync settings](/microsoft-365-copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [Veeva Vault RIM connector overview](veeva-rim-overview.md)
- [Troubleshoot issues with the Veeva Vault RIM connector](veeva-rim-troubleshooting.md)
