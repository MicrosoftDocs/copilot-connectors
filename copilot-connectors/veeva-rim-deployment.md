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
ms.date: 02/09/2026
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

You can view properties crawled from your Veeva RIM instance. The connector indexes metadata such as document name, owner, lifecycle stage, title, created by, and last modified by. The following table lists the properties that the Veeva QualityDocs connector indexes by default.

| Properties             | Semantic label         | Description                                                    | Schema                 |
|------------------------|------------------------|----------------------------------------------------------------|------------------------|
| Id |  | Unique identifier of the document version in Veeva RIM. | Query, Retrieve |
| Name | title | Display name of the regulatory document. | Query, Retrieve |
| FileName | filename | Original file name of the uploaded document. | Query, Search, Retrieve |
| Extension | fileExtension | File type extension (e.g., .pdf, .docx). | Query, Search, Retrieve |
| Url | url | Direct link to open the document in Veeva RIM. | Query, Retrieve |
| Status | state | Current lifecycle state of the document (e.g., Draft, Approved). | Query, Retrieve |
| DocumentId |  | Unique identifier of the document (without version). | Query, Retrieve |
| MajorVersion |  | Major version number assigned to the document. | Query, Retrieve |
| MinorVersion |  | Minor version number of the document. | Query, Retrieve |
| Type |  | Regulatory document type (e.g., Submission, Report). | Query, Retrieve |
| Subtype |  | Sub-classification of the document type. | Query, Retrieve |
| Product |  | Associated product(s) linked to the document. | Query, Retrieve |
| Country |  | Country or region relevant to the document. | Query, Retrieve |
| Format |  | Defined format of the regulatory document. | Query, Retrieve |
| DocumentCreationDate | createdDateTime | Original creation date of the document. | Query, Retrieve |
| VersionModifiedDate | lastModifiedDateTime | Date when the document version was last modified. | Query, Retrieve |
| CreatedBy | createdBy | Name of the user who created the document. | Query, Retrieve |
| CreatedByUserId |  | System ID of the user who created the document. | Query, Retrieve |
| LastModifiedByUserId |  | System ID of the user who last modified the document. | Query, Retrieve |
| LastModifiedBy | lastModifiedBy | Name of the user who last modified the document. | Query, Retrieve |
| Lifecycle |  | Document lifecycle phase within RIM. | Query, Retrieve |
| Size |  | File size of the document in bytes. |  |
| Content |  | Extracted text/content of the document. | Retrieve |
| ApprovedDate |  | Date when the document was approved. | Query, Retrieve |
| AnnotationsAll |  | Total count of annotations in the document. | Query, Retrieve |
| AnnotationsAnchors |  | Count of anchor annotations. | Query, Retrieve |
| AnnotationsApproved |  | Count of approved annotations. | Query, Retrieve |
| AnnotationsAuto |  | Count of automatically generated annotations. | Query, Retrieve |
| AnnotationsClaim |  | Count of claim annotations. | Query, Retrieve |
| AnnotationsLines |  | Count of line-level annotations. | Query, Retrieve |
| AnnotationsLinks |  | Count of link annotations. | Query, Retrieve |
| AnnotationsNotes |  | Count of note annotations. | Query, Retrieve |
| AnnotationsPermalink |  | Count of permalink annotations. | Query, Retrieve |
| AnnotationsResolved |  | Count of resolved annotations. | Query, Retrieve |
| AnnotationsUnresolved |  | Count of unresolved annotations. | Query, Retrieve |
| FileCreatedBy |  | System name of the file’s original author. | Query, Retrieve |
| FileCreatedDate |  | Date when the file was originally created. | Query, Retrieve |
| FileMetaAuthor |  | Metadata field capturing the file’s author. | Query, Retrieve |
| FileMetaKeywords |  | Metadata keywords associated with the file. | Query, Retrieve |
| FileModifiedBy |  | System name of the user who last modified the file. | Query, Retrieve |
| FileModifiedDate |  | Date when the file was last modified. | Query, Retrieve |
| SourceDocumentId |  | ID of the source or parent document (if derived). | Query, Retrieve |
| SourceDocumentName |  | Name of the source or parent document. | Query, Retrieve |
| VersionCreatedBy |  | User who created the current version. | Query, Retrieve |
| VersionLink |  | Link to the specific document version in RIM. | Query, Retrieve |
| HealthAuthorityVersion |  | Version identifier used for health authority submissions. | Query, Retrieve |
| IdmpSubmissionDate |  | Date of IDMP (Identification of Medicinal Products) submission. | Query, Retrieve |
| IncludeForAllLanguages |  | Indicates whether the document is applicable across all languages. | Query, Retrieve |
| MasterFileCode |  | Code used to classify the master file. | Query, Retrieve |
| MasterFileIdentifier |  | Identifier for the master file record. | Query, Retrieve |
| RIMAutoClassification |  | Auto-classification category assigned by RIM. | Query, Retrieve |
| TemplateDocument |  | Flag indicating if the document is a template. | Query, Retrieve |
| XevmpdSubmissionStatus |  | Status of XEVMPD (Extended EudraVigilance Medicinal Product Dictionary) submission. | Query, Retrieve |
| Version |  | the version number of a file | Query, Retrieve |
| ItemPath |  |  | Search, Retrieve |
| ItemType |  |  | Search, Retrieve |

### Customize sync intervals

You can modify the frequency of full crawls to fit your organization's requirements. The following are the default crawls:
- Full crawl—daily.

For more information, see [Guidelines for sync settings](/microsoft-365-copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [Veeva Vault RIM connector overview](veeva-rim-overview.md)
- [Troubleshoot issues with the Veeva Vault RIM connector](veeva-rim-troubleshooting.md)
