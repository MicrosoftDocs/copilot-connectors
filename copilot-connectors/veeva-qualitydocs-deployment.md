---
title: "Deploy the Veeva QualityDocs Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 12/01/2025
ms.localizationpriority: Medium
description: "Find information about how to deploy the Veeva QualityDocs Microsoft 365 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Veeva QualityDocs Microsoft 365 Copilot connector

The Veeva QualityDocs Microsoft 365 Copilot connector enables organizations to index controlled quality documents—such as Standard Operating Procedures (SOPs), work instructions, policies, CAPAs, and batch records—from Veeva Vault QualityDocs into Microsoft Graph. This integration makes them accessible across Microsoft 365 experiences, including Microsoft 365 Copilot   and Microsoft Search. The connector respects Vault QualityDocs' granular permission model, ensuring that only authorized users can see or interact with relevant documents. By pairing Microsoft's AI capabilities with QualityDocs' single source of truth, quality, regulatory, manufacturing, and supply-chain teams can collaborate more efficiently while maintaining compliance.

This article describes the steps to deploy and customize the Veeva QualityDocs connector. For general information about Copilot connector deployment, see [Set up Copilot connectors in the Microsoft 365 admin center](/microsoftsearch/configure-connector).

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be a Microsoft 365 admin.
- Your organization must have a configured Veeva Vault QualityDocs environment.
- Microsoft Entra ID must be set up for OAuth 2.0/OpenID Connect authentication.
- You must have the client ID and client secret from your Microsoft Entra application.
- You must have the Veeva Vault QualityDocs instance URL.
- User identity mapping between Veeva Vault QualityDocs and Microsoft Entra ID must be configured.

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

To add the Veeva QualityDocs connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot** > **Connectors**.
1. Go to the **Connectors** tab, and in the left pane, choose **Gallery**.
1. From the list of available connectors, choose **Veeva QualityDocs**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **Veeva QualityDocs** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](/microsoftsearch/enhancing-microsoft-copilot-discovery-with-graph-connector-content).

### Set instance URL

Enter the URL of your Veeva QualityDocs instance. For example: `https://<your-vault-domain>.veevavault.com`.

### Choose authentication type

To authenticate the Veeva QualityDocs connector, for the **Authentication type**, choose **Microsoft Entra ID OIDC**, and provide the following information:

- **Vault session ID URL**: In Veeva QualityDocs, go to **Admin panel** > **Settings** > **OAuth 2.0/ OpenID Connect Profiles**, and choose the profile you created for this connection. Copy the Vault Session ID URL.
- **Client ID**: The application ID for the Entra application you registered for Veeva QualityDocs.
- **Client secret**: The client secret associated with the Entra application.

Select **Authorize** to sign in with your Entra ID account, and select **Consent on behalf of your organization**, and the on the permission request screen, choose **Accept**.

> [!IMPORTANT]
> Configure both Microsoft Entra ID and Veeva QualityDocs admin settings to enable Microsoft Entra ID authentication.

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Copilot connectors](/microsoftsearch/staged-rollout-for-graph-connectors).

Choose **Create** to deploy the connection. The Veeva QualityDocs Copilot connector starts indexing content right away.

The following table lists the default values that are set.

| Category | Default value |
|----------|--------------|
| Users    | Respects Veeva QualityDocs permissions; only viewable documents are accessible. |
| Content  | Indexes key metadata, such as document name, owner, and lifecycle stage. |
| Sync     | Full crawls every day. |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

## Customize settings (optional)

You can customize the default values for the Veeva QualityDocs connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

#### Access permissions

The connector adheres to the access control lists (ACLs) defined in Veeva QualityDocs. Only users with view permissions in Veeva QualityDocs can see the indexed content in Microsoft 365. Admins can optionally allow all users access to all indexed content, although this approach isn't recommended for regulated repositories.

#### Mapping identities

The connector relies on mapping Veeva QualityDocs user identities (for example, Federated ID) to Microsoft Entra ID user accounts. Make sure that the Microsoft Entra UPN matches the Federated ID used in QualityDocs, or configure custom identity mapping so security permissions can be enforced correctly.

If you want to enforce the security settings of your Veeva QualityDocs instance, choose **Non-ME-ID** as the identity type for your content source.

Enter the required information for identity mapping. For example, if you want to map identities based on email addresses:

1. For the **Microsoft Entra user property**, select **Mail**.
2. Under **non-Microsoft Entra user property**, select **Add identity property**, and choose **Email**. Use an expression such as `([^@]+)` to capture a sequence of one or more characters that are not the `@` symbol.
Create a formula to complete the mapping, such as `{0}@<your-domain>`.

### Customize content settings

#### Query string

You can use query-string conditions to include only relevant documents to enable more targeted and efficient indexing.

#### Manage properties

The following table lists the properties that the Veeva QualityDocs connector indexes by default.

| Property                  | Semantic Label      | Description                                         | Schema Attributes         |
|---------------------------|--------------------|-----------------------------------------------------|--------------------------|
| content                   |                    | Main text or body content extracted from the document | Search                   |
| country                   |                    | Country or region associated with the document      | Query, Retrieve          |
| createdBy                 | CreatedBy          | User who initially created the document             | Query, Retrieve          |
| createdByUserId           |                    | Internal user identifier for the document creator   | Query, Retrieve          |
| daysBeforeToStartPeriodicReview |              | Number of days before the document's periodic review begins | Query, Retrieve  |
| documentCreationDate      | CreatedDateTime    | Date and time when the document was originally created | Query, Retrieve      |
| documentId                |                    | Unique identifier for the document within Veeva system | Query, Retrieve      |
| extension                 | FileExtension      | File type extension such as PDF, DOCX, XLSX         | Query, Retrieve, Search  |
| fileName                  | Title              | File name or title of the document                  | Query, Retrieve, Search  |
| format                    |                    | Document format or type information                 | Query, Retrieve          |
| id                        |                    | Unique identifier for the document record           | Query, Retrieve          |
| implementationPeriodDays  |                    | Number of days designated for implementation of the document | Query, Retrieve  |
| importedDocument          |                    | Indicates if the document was imported              | Query, Retrieve          |
| lastModifiedBy            | LastModifiedBy     | User who last modified the document                 | Query, Retrieve          |
| lastModifiedByUserId      |                    | Internal user identifier of the last modifier       | Query, Retrieve          |
| lifecycle                 |                    | Document lifecycle state (for example, Draft, Approved)    | Query, Retrieve          |
| majorVersion              |                    | Major version number of the document                | Query, Retrieve          |
| minorVersion              |                    | Minor version number of the document                | Query, Retrieve          |
| obsolescenceApproved      |                    | Indicates whether obsolescence is approved    | Query, Retrieve          |
| owningDepartment          |                    | Department responsible for owning the document      | Query, Retrieve          |
| owningFacility            |                    | Facility associated with the document ownership     | Query, Retrieve          |
| periodicReviewFrequency   |                    | Frequency at which the document undergoes periodic review | Query, Retrieve    |
| product                   |                    | Product related to or covered by the document       | Query, Retrieve          |
| referenceModelCategory    |                    | High-level reference model category of the document | Query, Retrieve          |
| referenceModelSubcategory |                    | Subcategory within the reference model classification | Query, Retrieve      |
| requiresDcc               |                    | Indicates if Document Change Control is required    | Query, Retrieve          |
| scope                     |                    | Scope or applicability of the document              | Query, Retrieve          |
| size                      |                    | File size of the document     |                     |
| status                    |                    | Document status (for example, Active, Archived)            | Query, Retrieve          |
| subtype                   |                    | Specific subtype or classification of the document  | Query, Retrieve          |
| type                      |                    | Type or main category of the document               | Query, Retrieve          |
| url                       | url                | Direct URL to access or preview the document        | Query, Retrieve          |
| versionModifiedDate       | LastModifiedDateTime | Date and time when this version was last modified  | Query, Retrieve          |

### Customize sync intervals

You can modify the frequency of full crawls to fit your organization's requirements. The default is a full crawl every day. For more information, see [Guidelines for sync settings](/microsoftsearch/configure-connector#guidelines-for-sync-settings).

## Related content

- [Veeva QualityDocs connector overview](veeva-qualitydocs-overview.md)
- [Troubleshoot issues with the Veeva QualityDocs connector](veeva-qualitydocs-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoftsearch/configure-connector)
