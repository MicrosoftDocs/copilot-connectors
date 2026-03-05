---
title: "Deploy the Veeva PromoMats Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 03/05/2026
ms.localizationpriority: Medium
description: "Find information about how to deploy the Veeva PromoMats Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Veeva PromoMats Microsoft 365 Copilot connector

The Veeva PromoMats Microsoft 365 Copilot connector allows organizations to index promotional marketing materials from Veeva PromoMats into Microsoft Graph, making them accessible across Microsoft 365 experiences, including Microsoft 365 Copilot and Microsoft Search. The connector integrates the Vault PromoMats built-in permission model to ensure that users only access authorized content, and supports faster content generation and review through content analysis and preparation. It helps maintain brand consistency by improving efficiency throughout the content lifecycle. This functionality is beneficial for marketing, medical affairs, and regulatory teams, enabling informed decision-making and reducing the time-to-market for promotional materials.

This article describes the steps to deploy and customize the Veeva PromoMats connector. For general information about Copilot connector deployment, see [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365-copilot/connectors/deployment-overview).

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be a Microsoft 365 admin.
- You must have access to a configured Veeva PromoMats environment.
- You must have the necessary permissions in both Microsoft Entra ID and Veeva PromoMats to register applications and configure OAuth/OpenID Connect.
- You must have the PromoMats instance URL and admin credentials.

### Register an application and configure OAuth

Use the following steps to configure Microsoft Entra ID OAuth 2.0/OpenID Connect for the Veeva QualityDocs connector.

1. Register an application in Microsoft Entra ID.
   - Go to **Microsoft Entra admin center** > **App registrations** > **New registration**.
   - Name the application and select **Accounts in this organizational directory only**.
   - Add the redirect URI:
     - For Microsoft 365 Enterprise: `https://gcs.office.com/v1.0/admin/oauth/callback`
     - For Microsoft 365 Government: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
   - Generate a client secret under **Certificates & Secrets** and store it securely.

2. Configure OAuth in Veeva QualityDocs.
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

To add the Veeva PromoMats connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Choose the **Gallery** tab.
1. From the list of available connectors, choose **Veeva PromoMats**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **Veeva PromoMats** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](/microsoft-365-copilot/connectors/enhance-copilot-discovery).

### Set instance URL

Enter the URL of your Veeva PromoMats instance. For example: `https://<your-vault-domain>.veevavault.com`

### Choose authentication type

To authenticate the Veeva QualityDocs connector, for the **Authentication type**, choose **Microsoft Entra ID OIDC**, and provide the following information:

- **Vault session ID URL**: In Veeva QualityDocs, go to **Admin panel** > **Settings** > **OAuth 2.0/ OpenID Connect Profiles**, and choose the profile you created for this connection. Copy the Vault Session ID URL.
- **Client ID**: The application ID for the Entra application you registered for Veeva QualityDocs.
- **Client secret**: The client secret associated with the Entra application.

Select **Authorize** to sign in with your Entra ID account, and select **Consent on behalf of your organization**, and the on the permission request screen, choose **Accept**.

> [!IMPORTANT]
> Configure both Microsoft Entra ID and Veeva QualityDocs admin settings to enable Microsoft Entra ID authentication.

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](/microsoft-365-copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The Veeva PromoMats Copilot connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|--------------|
| Users    | Respects Veeva Vault permissions; only viewable documents are accessible. |
| Content  | Indexes key metadata, such as document name, owner, and lifecycle stage. Enables metadata like title, created by, and last modified by. |
| Sync     | Full crawl – daily. |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Veeva PromoMats connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

The connector adheres to the access control lists (ACLs) defined in Veeva PromoMats. Only users with view permissions in Veeva PromoMats can see the indexed content in Microsoft 365. Admins can optionally allow all users access to all indexed content, although this isn't recommended.

#### Mapping identities

The connector requires that PromoMats user identities map to the organization's Microsoft Entra ID identities. If the identities don't automatically match, admins can configure custom user mappings so that access rights are enforced. For example, you can map identities based on email addresses or other unique identifiers.

If you want to enforce the security settings of your Veeva QualityDocs instance, choose **Non-ME-ID** as the identity type for your content source.

Enter the required information for identity mapping. For example, if you want to map identities based on email addresses:

1. For the **Microsoft Entra user property**, select **Mail**.
2. Under **non-Microsoft Entra user property**, select **Add identity property**, and choose **Email**. Use an expression such as `([^@]+)` to capture a sequence of one or more characters that are not the `@` symbol.
Create a formula to complete the mapping, such as `{0}@<your-domain>`.

### Customize content settings

#### Query string

Admins can use query string conditions to precisely control the synchronization of articles to ensure efficient indexing. For example, you can filter by metadata, document state, or time to include only relevant content.

#### Manage properties

You can view and manage properties crawled from your Veeva PromoMats instance. The following table lists the properties that the connector indexes by default.

| Property             | Veeva field                            | Semantic label       | Description                                                          | Schema attributes                    |
|----------------------|----------------------------------------|----------------------|----------------------------------------------------------------------|--------------------------------------|
| Id                   | document_number__v                     |                      | Unique identifier of the document                                    | Query, Retrieve                      |
| DocId                | id                                     |                      | Internal document identifier (primary key) in the Veeva system       | Query, Retrieve                      |
| GlobalId             | global_id__sys                         |                      | System-generated globally unique identifier across Vaults            | Query, Retrieve                      |
| DocumentNumber       | document_number__v                     |                      | System-assigned document number in the Veeva system                  | Query, Retrieve                      |
| FileName             | filename__v                            | fileName             | Name of the uploaded source file                                     | Query, Retrieve                      |
| Title                | title__v                               | title                | Document title                                                       | Retrieve, Search                     |
| Description          | description__v                         |                      | Free-text description of the document                                | Retrieve, Search                     |
| Extension            | file extension of filename__v          | fileExtension        | File type extension (for example, PDF, DOCX, PPTX)                  | Query, Retrieve, Search              |
| Url                  | https://{vaultDns}/ui/#doc_info/{id}   | url                  | Direct URL to access or preview the document in Veeva Vault          | Query, Retrieve                      |
| Status               | status__v                              |                      | Document status (for example, Active, Archived)                      | Query, Retrieve                      |
| VersionId            | version_id                             |                      | Unique identifier for a specific document version                    | Query, Retrieve                      |
| MajorVersion         | major_version_number__v                |                      | Major version number of the document                                 | Query, Retrieve                      |
| MinorVersion         | minor_version_number__v                |                      | Minor version or revision number                                     | Query, Retrieve                      |
| Type                 | type__v                                | containerName        | Top-level document type classification                               | Query, Retrieve                      |
| Subtype              | subtype__v                             |                      | Second-level document classification under type                      | Query, Retrieve                      |
| Product              | product__v.name__v                     |                      | Product associated with the document content                         | Query, Retrieve                      |
| Brand                | branding__v                            |                      | Brand associated with the promotional material                       | Query, Retrieve, Search, Refine      |
| SecondaryBrand       | secondary_brands__v                    |                      | Secondary brands associated with the promotional material            | Query, Retrieve, Search, Refine      |
| KeyMessages          | key_message__v                         |                      | Key messages associated with the promotional material                | Retrieve, Search                     |
| Tags                 | tags__v                                | tags                 | Tags or keywords associated with the document                        | Query, Retrieve, Refine              |
| Country              | country__v.name__v                     |                      | Country or region related to the document                            | Query, Retrieve                      |
| Format               | format__v                              |                      | File format of the source document                                   | Query, Retrieve                      |
| ItemType             | format__v                              | itemType             | Item type derived from the document format                           | Query, Retrieve, Refine              |
| ItemPath             | {type__v}/{subtype__v}                 | itemPath             | Hierarchical path combining the document type and subtype            | Query, Retrieve                      |
| Authors              | file_meta_author__v                    | authors              | Author metadata from the source file                                 | Query, Retrieve, Refine              |
| DocumentCreationDate | document_creation_date__v              | createdDateTime      | Date and time the document was created in Vault                      | Query, Retrieve                      |
| VersionModifiedDate  | version_modified_date__v               | lastModifiedDateTime | Date and time when this version was last modified                    | Query, Retrieve                      |
| CreatedBy            | created_by__v (name, email)            | createdBy            | User who initially created the document                              | Query, Retrieve, Search              |
| CreatedByUserId      | created_by__v                          |                      | Internal user identifier for document creator                        | Query, Retrieve                      |
| LastModifiedByUserId | last_modified_by__v                    |                      | Internal user identifier for last modifier                           | Query, Retrieve                      |
| LastModifiedBy       | last_modified_by__v (name, email)      | lastModifiedBy       | User who last modified the document                                  | Query, Retrieve, Search              |
| Lifecycle            | lifecycle__v                           |                      | Lifecycle assigned to the document                                   | Query, Retrieve                      |
| Size                 | size__v                                |                      | File size of the document                                            |                                      |
| Content              | document content                       |                      | Main text or body content extracted from the document                | Search                               |

#### Add custom properties

In addition to the default properties, the connector automatically discovers custom and other document properties from your Veeva PromoMats instance. During setup, the connector retrieves all available document fields that are queryable, not disabled, and not hidden, and presents them as additional properties under **Manage properties**.

You can select and add these custom properties one by one to the connector schema. Each added custom property has the following default schema attributes:

- **Query** and **Retrieve** are enabled by default.
- **Search** and **Refine** aren't enabled by default but can be turned on under **Manage properties**.

For properties that reference Veeva Vault objects (ObjectReference type), the connector also fetches the referenced object's metadata and exposes its fields as nested properties. For example, if a custom property references a VObject of type `campaign__v`, the connector generates properties like `campaign__v.name__v`, `campaign__v.status__v`, and so on.

After adding custom properties, you can customize the schema attributes for any property—both default and custom—under **Manage properties**. You can enable or disable **Query**, **Retrieve**, **Search**, and **Refine** for each property based on your organization's requirements.

### Customize sync intervals

You can modify the frequency of full crawls according to your organization's requirements. The default is a full crawl every day.

For more information, see [Guidelines for sync settings](/microsoft-365-copilot/connectors/deployment-overview#guidelines-for-crawl-settings).

## Related content

- [Veeva PromoMats connector overview](veeva-promomats-overview.md)
- [Troubleshoot issues with the Veeva PromoMats connector](veeva-promomats-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365-copilot/connectors/deployment-overview)
