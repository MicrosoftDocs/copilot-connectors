---
title: "Troubleshoot issues with the GitLab Knowledge Cloud connector"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: raynezou
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.date: 01/23/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the GitLab Knowledge Cloud Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the GitLab Knowledge Cloud connector

The GitLab Knowledge Cloud Microsoft 365 Copilot connector indexes documentation and knowledge artifacts stored in GitLab projects on GitLab.com. This article provides troubleshooting information for common errors that you might encounter when you deploy and use the GitLab Knowledge Cloud connector. These issues are typically related to authentication, permissions, missing content, or GitLab API access.

## Can't find GitLab knowledge content in Copilot or Microsoft Search

If users can’t find GitLab documentation, wikis, or knowledge artifacts in Copilot or search results, review the following:

- Confirm that the GitLab instance URL is correct.
- Verify that the GitLab OAuth app has the required scopes:  
  - `read_api`  
  - `read_repository`  
  - `read_user`
- Check that the authenticated GitLab account has access to all indexed projects, wikis, and files.
- Ensure that users have Microsoft Entra ID identities that correctly map to GitLab users.
- Confirm that content is within the default indexing range (the last 365 days unless customized).

## Missing access to certain GitLab projects, wikis, or runbooks

If some content is missing from search results or Copilot responses:

- Verify the permissions of the GitLab account used during connector setup.
- Check whether the missing projects, wiki pages, or runbooks require project‑level permissions.
- Confirm that identity mapping rules correctly match GitLab users to Microsoft Entra ID accounts.
- If regex transformations are in use, ensure that patterns match the expected user identifiers.

## GitLab OAuth authorization issues

If you encounter issues completing the OAuth flow:

- Confirm that the **client ID** and **client secret** are valid and belong to the GitLab OAuth app configured for your tenant.
- Verify that the correct redirect URL is configured:
  - **Microsoft 365 Enterprise:** `https://gcs.office.com/v1.0/admin/oauth/callback`
  - **Microsoft 365 Government:** `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
- Check whether single sign-on (SSO) is enabled in your GitLab instance. Some SSO flows require the account to be signed in separately before authorization.

### GitLab API rate limiting or incomplete ingestion

If indexing pauses or content appears incomplete:

- Check whether your GitLab tenant is hitting rate limits.  
- Review ingestion volume guidelines:
  - Up to 100,000 items: Typically completes within several hours.
  - 100,000 to 1,000,000 items: Ingestion might take multiple days.
  - Over 1,000,000 items: Ingestion might take from several days to weeks depending on load.
- Reduce indexing scope temporarily (for example, by narrowing date range) to determine whether performance improves.
- Review sync interval customizations to ensure they meet organizational needs:
  - Incremental crawl: 15 minutes (default)
  - Full crawl: daily (default)

### Incorrect or unexpected search results in Copilot

If Copilot responses show unexpected content or omit expected GitLab documentation:

- Verify property mappings on the **Data** tab.
- Confirm that important fields—such as title, content, description, labels, and timestamps—are mapped and set correctly.
- Verify that properties marked **searchable**, **retrievable**, or **refinable** match your content needs.
- Review the query string configuration to confirm that filtering isn't excluding required content.

### Identity mapping issues

If users are unable to see expected content:

- Confirm that identity mappings align with your GitLab tenant:
  - Email
  - Login
  - Name
  - Regex transformation
- Make sure that GitLab and Microsoft Entra ID users align across all required attributes.
- If mapping rules are complex, test with a small set of accounts to verify correct mapping behavior.

### Permissions issues

If users receive **no access** errors:

- Validate that GitLab REST API permissions allow the connector's service account to read the full scope of documents, wikis, and knowledge assets.
- Check Microsoft 365 access settings:
  - **Only people with access to this data source**  
  - **Everyone**
- Confirm that GitLab group or project‑level permissions aren't preventing the connector from retrieving content.

### GitLab instance URL errors

If the connector reports instance URL issues:

- Make sure that the instance URL matches the GitLab deployment used to host knowledge content.
    - For GitLab.com, use `https://gitlab.com`.
    - For GitLab self‑managed instances, verify that the URL is accessible and reachable from the Microsoft 365 environment.

## Related content

- [GitLab Knowledge Cloud connector overview](gitlab-knowledge-cloud-overview.md)  
- [Deploy the GitLab Knowledge Cloud connector](gitlab-knowledge-cloud-deployment.md)