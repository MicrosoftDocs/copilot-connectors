---
title: "Deploy the Amazon S3 Microsoft 365 Copilot connector"
author: lauragra
ms.author: kailiang
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.date: 12/05/2025
ms.localizationpriority: Medium
description: "Find information about how to deploy the Amazon S3 Copilot connector in the Microsoft 365 admin center, including prerequisites, configuration steps, and customization options."
---

# Deploy the Amazon S3 Copilot connector

The Amazon S3 Microsoft 365 Copilot connector indexes content from Amazon S3 buckets into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface relevant files directly within apps like Microsoft Teams, Outlook, and SharePoint.

This article describes the steps to deploy and customize the Amazon S3 connector. For general information about Copilot connector deployment, see [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365-copilot/connectors/deployment-overview).

## Prerequisites

Before you deploy the connector, make sure that you meet the following prerequisites:

- You must be a Microsoft 365 tenant admin.
- You need an AWS Access Key ID and Secret Access Key with read permissions to the S3 bucket.
- The IAM user must have the **AmazonS3ReadOnlyAccess** policy attached.

## Deploy the connector

To add the Amazon S3 connector for your organization:

1. In the Microsoft 365 admin center, in the left pane, choose **Copilot > Connectors**.
2. Go to the **Connectors** tab, and in the left pane, choose **Gallery**.
3. From the list of available connectors, choose **Amazon S3**.

### Set display name

The display name is used to identify references in Copilot responses to help users recognize the associated file or item. The display name also signifies trusted content and is used as a content source filter.

You can accept the default **Amazon S3** display name, or customize the value to use a display name that users in your organization recognize.

For more information about connector display names and descriptions, see [Enhance Copilot discovery of connector content](/microsoft-365-copilot/connectors/enhancing-microsoft-copilot-discovery-with-graph-connector-content).

### Choose authentication type
                                                
The Amazon S3 connector supports the following authentication type:

- **Amazon Signature V4**

Provide the following AWS credentials:

- **Access Key ID**
- **Secret Access Key**

As a best practice, create a dedicated IAM user with the **AmazonS3ReadOnlyAccess** permission to the S3 bucket.

> [!IMPORTANT]
> The Amazon S3 connector only supports **Visible to Everyone** permission. All indexed content is visible to Microsoft 365 users.
> To support this scenario:
> - Verify ACL compliance before you set up the connector.
> - Use a dedicated IAM user with tailored permissions for the required AWS credentials.
> - Evaluate the **limited audience** feature to restrict visibility to selected users or groups.

### Roll out

To roll out to a limited audience, choose the toggle next to **Rollout to limited audience** and specify the users and groups to roll the connector out to. For more information, see [Staged rollout for Microsoft 365 Copilot connectors](/microsoft-365-copilot/connectors/staged-rollout).

Choose **Create** to deploy the connection. The Amazon S3 Copilot connector starts indexing content right away. After you create your connection, you can review the status in the **Connectors** section of the [Microsoft 365 admin center](https://admin.microsoft.com/).

### Default values

The following table lists the default values that are set.

| Category | Setting | Default value |
|----------|---------|---------------|
| Users | Access permissions | All indexed content is visible to Microsoft 365 users. |
| Content | Include/exclude buckets | All |
| Content | Manage properties | For default properties and schemas, see [Manage properties](#manage-properties). |
| Sync | Incremental crawl | Frequency: Every 15 minutes |
| Sync | Full crawl | Frequency: Every day |

To customize these values, choose **Custom setup**. For more information, see [Customize settings](#customize-settings-optional).

## Customize settings (optional)

You can customize the default values for the Amazon S3 connector settings. To customize settings, on the connector page in the admin center, choose **Custom setup**.

### Customize user settings

The Amazon S3 connector only supports the **Everyone** user access permission. All indexed content is accessible to Microsoft 365 users.

### Customize content settings

#### Preview data
Choose **Preview data** to verify the data retrieved by the connection. 

#### Content filter
The connector provides a content filter to scope what content gets indexed. In the **Bucket name** field, select the specific buckets to include.

#### Manage properties
To view available properties from your S3 objects, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias in the property. The following table lists the default properties and labels.

| Default property        | Label | Description                                |
|------------------------|----------------|--------------------------------------------|
| BucketName      | `N/A`            | Name of the S3 bucket that contains the object |
| Content         | `N/A`        | Full text content of the object             |
| ETag            | `N/A`            | Entity tag for object version identification|
| FileExtension   | `fileExtension` | File type extension                         |
| IconUrl         | `iconUrl`        | URL to the icon representing the file type  |
| Id              | `N/A`            | Unique identifier for the object            |
| LastModified    | `lastModifiedDateTime`  | Timestamp when the object was last modified     |
| Name            | `fileName`      | Name of the object in S3                    |
| Size            | `N/A`            | Size of the object in bytes                 |
| StorageClass    | `N/A`            | S3 storage class for the object             |
| Url             | `url`            | Direct URL to access the object             |
| Type           | `itemType`            | Entity type of the object             |
| Path           | `itemPath`            | S3 URI to the object             |
| Tags           | `Tags`            | Tags of the object             |

### Customize sync intervals

The refresh interval determines how often your data is synced between Amazon S3 and the Microsoft 365 Copilot connector index. The S3 Copilot connector supports both full crawl and incremental crawls. The following are the default values:

- **Incremental crawl:** Every 15 minutes.
- **Full crawl:** Every day.

You can customize these values. For more information, see [Guidelines for sync settings](/microsoft-365-copilot/connectors/deployment-overview#guidelines-for-sync-settings).

## Related content

- [Amazon S3 connector overview](amazon-s3-overview.md)
- [Troubleshoot issues with the Amazon S3 connector](amazon-s3-troubleshooting.md)
- [Set up Copilot connectors in the Microsoft 365 admin center](/microsoft-365-copilot/connectors/deployment-overview)
