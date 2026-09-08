---
title: "Troubleshoot issues with the Veeva On-Premises Microsoft 365 Copilot connector"
ms.author: danielabo
author: danipocket
manager: calvind
ms.reviewer: dannyyao
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: microsoft-365-copilot-connectors
ms.date: 09/08/2026
ms.localizationpriority: Medium
description: "Find troubleshooting information for the Veeva On-Premises Microsoft 365 Copilot connector."
---

# Troubleshoot issues with the Veeva On-Premises Microsoft 365 Copilot connector

The Veeva On-Premises Microsoft 365 Copilot connector allows organizations to index documents and metadata from
Veeva Vault PromoMats, QualityDocs, and RIM into Microsoft Graph using the Veeva Direct Data API and a locally
hosted Microsoft Graph connector agent (GCA).

This article provides troubleshooting information for common errors that you might encounter when you deploy the
Veeva On-Premises connector.

To verify Direct Data API, OAuth 2.0/OpenID Connect, security policy, and identity configuration, see
[Set up the Veeva Vault service for Veeva On-Premises connector ingestion](veeva-onpremise-admin-setup.md).

## Veeva On-Premises connector troubleshooting

Errors are grouped by category. For each error, the **Behavior** column indicates whether the connector retries
automatically or requires manual intervention.

To view error details for a specific crawl, select the connection in the Microsoft 365 admin center and choose
**Error details** > **Error code**. For more information, see [Monitor your connections](./manage-connector.md).

### Connector errors

The following table lists errors that occur during connector operation or validation.

| Error | Description | Behavior | Resolution |
| --- | --- | --- | --- |
| `BadDataSourceAPIResponse` | Veeva API returned a malformed or unexpected JSON response. | Retryable | The connector retries automatically. If the error persists, check the Veeva API status and verify that the connector configuration is correct. |
| `DataSourceUnreachable` | HTTP connection failure or API endpoint unreachable. | Retryable | The connector retries automatically. Verify network connectivity between the GCA host machine and the Veeva Vault instance. Check firewall rules and proxy settings. For required endpoints, see [Microsoft Graph connector agent](/microsoft-365/copilot/connectors/connector-agent). |
| `InvalidCredentials` | Missing or invalid credential details (session ID). | Fatal — crawl aborted | Reauthenticate the connector. Verify that the client ID, client secret, and Vault session ID URL are correct. |
| `AuthenticationError` | Session authentication failure or no vault access. | Token refresh, then retry | The connector automatically attempts to refresh the session token. If the error persists, reauthenticate the connector. |
| `AuthorizationError` | Permission check failure; remapped to `InvalidCredentials`. | Fatal — crawl aborted | Verify that the connector service account has the required permissions in Veeva Vault, then reauthenticate. |
| `NetworkUnreachable` | Network connectivity issue during validation. | Fatal — crawl aborted | Check network connectivity on the GCA host machine. Verify that the GCA host can reach the Veeva Vault instance and all required Microsoft 365 endpoints. |
| `EmptyRefreshToken` | OAuth refresh token is null or empty. | Retryable | Reauthenticate the connector to generate a new OAuth refresh token. |
| `SourceThrottlingCrawl` | API rate limiting (HTTP 429 or `API_LIMIT_EXCEEDED`). | Exponential backoff retry | The connector retries automatically with exponential backoff. To reduce throttling, lower the crawl frequency under **Customize settings** > **Sync**. |
| `InternalError` (9005) | General processing error in enumerators. | Retryable | The connector retries automatically. If the error persists, contact Microsoft support. |
| `InternalError` (9007) | Failed to fetch source properties during validation. | Retryable | Verify that the connector service account has permission to read document properties in Vault. The connector retries automatically. |
| `InternalError` (9010) | Invalid content filter in the connection configuration. | Permanent — item skipped | Review the content filter rules under **Customize settings** > **Content filters**. Verify that each field name is a valid, queryable Vault field and that the operator is appropriate for that field type. |

### Veeva API errors

The following table lists errors returned directly by the Veeva API.

| Error | Description | Behavior | Resolution |
| --- | --- | --- | --- |
| `INVALID_SESSION_ID` | Veeva session expired or invalid. | Token refresh, then retry | The connector automatically attempts to refresh the session token. If the error persists, reauthenticate the connector. |
| `TOO_MANY_REQUESTS` | Veeva API rate limit hit. | Exponential backoff retry | The connector retries automatically with exponential backoff. To reduce the frequency of this error, lower the crawl frequency under **Customize settings** > **Sync**. |
| `API_LIMIT_EXCEEDED` | Veeva API daily or burst limit exceeded. | Exponential backoff retry | The connector retries automatically. If this error occurs regularly, consider reducing the crawl frequency or contacting Veeva support to review your API quota. |
| `Operation Not Allowed` | Direct Data API is not enabled. | Fatal — crawl aborted | Enable the Direct Data API in Veeva Vault by navigating to **Admin** > **Settings** > **General Settings** and selecting **Enable Direct Data API**. Then rerun validation or the crawl. If the option isn't available, contact your Veeva Vault administrator or Veeva support because the feature may not be enabled for the Vault instance. |
| Other | Any other Veeva API error type. | Retryable | Check the error details for additional context. The connector retries automatically. If the error persists, consult the Veeva Vault API documentation or contact Veeva support. |


## Related content

- [Veeva On-Premises connector overview](veeva-onpremise-overview.md)
- [Deploy the Veeva On-Premises connector](veeva-onpremise-deployment.md)
- [Set up the Veeva Vault service for Veeva On-Premises connector ingestion](veeva-onpremise-admin-setup.md)
- [Microsoft Graph connector agent](/microsoft-365/copilot/connectors/connector-agent)
