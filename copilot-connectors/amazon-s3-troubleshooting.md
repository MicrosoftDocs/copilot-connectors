---
title: "Amazon S3 connector troubleshooting"
author: lauragra
ms.author: kailiang
manager: zezhangzhao
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: microsoft-365-copilot-connectors
ms.date: 10/22/2025
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Amazon S3 Copilot connector."
---

# Troubleshoot issues with the Amazon S3 Copilot connector

This article provides troubleshooting guidance for common errors you might encounter when deploying or managing the Amazon S3 Microsoft 365 Copilot connector. The connector indexes content from Amazon S3 buckets into Microsoft 365, enabling Copilot, Copilot Search, and Microsoft Search to surface relevant files directly within apps like Microsoft Teams, Outlook, and SharePoint.

## Amazon S3 connector troubleshooting

The following table lists common errors and recommended troubleshooting steps.

| Error message or issue | Description | Recommended action |
|------------------------|-------------|--------------------|
| **Authorization failed** | The connector can't validate the AWS credentials. | Verify that the Access Key ID and Secret Access Key are correct. Ensure the IAM user has the **AmazonS3ReadOnlyAccess** policy attached. |
| **Bucket not found** | The specified bucket name doesn't exist or is inaccessible. | Confirm the bucket name is spelled correctly and that the IAM user has permission to access it. |
| **No content indexed** | The connector completes setup but no content appears in Microsoft 365. | Check that the bucket contains supported file types. Use the **Preview results** feature to verify content visibility. |
| **Owner field missing** | The **Owner** field is no longer returned in the schema. | Amazon S3 no longer returns the **DisplayName** of the **Owner** field. Remove or ignore this field in schema mappings. |
| **Sync failures** | The connector fails during scheduled sync. | The Amazon S3 connector supports only full crawl. Ensure the sync interval is configured correctly and that the bucket is accessible during sync. |
| **Access denied to objects** | Some objects in the bucket aren't indexed. | Ensure all objects are publicly accessible or have permissions that allow the IAM user to read them. |
| **Preview results empty** | No data appears during preview. | Confirm that the bucket contains files and that the IAM user has read access. Try a different bucket or file path. |

## Related content

- [Amazon S3 connector overview](amazon-s3-overview.md)
- [Deploy the Amazon S3 connector](amazon-s3-deployment.md)
