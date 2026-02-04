---
title: "Troubleshoot issues with the Zendesk Ticket Microsoft 365 Copilot connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: anggao
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 01/14/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Zendesk Ticket Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Zendesk Ticket Microsoft 365 Copilot connector

The Zendesk Ticket Microsoft 365 Copilot connector allows your organization to index tickets from Zendesk. After you configure the connector, end users can search for these tickets from Zendesk in Microsoft Copilot and from any Microsoft Search client.

This article provides troubleshooting information for common errors that you might encounter when deploying or managing the Zendesk Ticket connector.

## Can't authenticate with the data source

To troubleshoot authentication errors:

- Verify that your Zendesk instance URL is correct.
- Verify that the OAuth client ID and secret are entered correctly.
- Confirm that the Zendesk admin created the OAuth client in the [Zendesk Admin Center](https://support.zendesk.com/hc/en-us/articles/4581766374554-Using-Zendesk-Admin-Center#topic_hfg_dyz_1hb).
- Make sure that the redirect URL matches the Microsoft 365 environment (Enterprise or Government).

## You don't have permission to access this data source error

This error might occur if the service account lacks access to required data. Confirm that the service account has the **Admin** role in Zendesk. The Agent or Light agent roles might not provide sufficient permissions for identity data (users, groups, organizations).

For more information, see [Using OAuth authentication with your application](https://support.zendesk.com/hc/en-us/articles/4408845965210-Using-OAuth-authentication-with-your-application).

## Common errors and known issues

To avoid common errors:

- Use an **Admin role** for the service account to avoid insufficient permissions for crawling user data such as organizations, groups, and memberships.
- Configure identity mapping correctly if you want to restrict visibility. Incorrect mapping can make data visible to everyone.

The following are known issues with the Zendesk Ticket connector:

- You might need to authenticate twice if no error appears and no green checkmark is shown in the credential box.
- If incremental crawls fail, verify that the OAuth token isn't expired and refresh it if necessary.

## Related content

- [Zendesk Ticket connector overview](zendesk-ticket-overview.md)
- [Deploy the Zendesk Ticket connector](zendesk-ticket-deployment.md)