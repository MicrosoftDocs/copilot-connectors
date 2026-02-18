---
title: Microsoft 365 Copilot extension for Microsoft 365 Copilot connectors
ms.author: danielabo
author: danipocket
manager: calvind
ms.topic: article
ms.service: mssearch
ms.audience: Admin
ms.localizationpriority: medium
ms.date: 02/13/2026
description: Learn how the Microsoft 365 Copilot extension works with Microsoft 365 Copilot connectors to capture user activity signals, improve personalization, and enhance Copilot and Search experiences.
---

# Microsoft 365 Copilot extension for Copilot connectors

The Microsoft 365 Copilot extension is a browser-based extension that works with Microsoft 365 Copilot connectors to capture user activity signals from external applications. These signals help improve personalization and relevance in Microsoft 365 Copilot and Microsoft Search by prioritizing content that users actively engage with in connected systems.

The Copilot extension is a key part of enabling high-quality Copilot experiences for external data sources. It operates only with connectors that are approved and configured by an administrator and respects existing permissions and access controls in the source systems.

## How the extension works with Copilot connectors

When deployed, the Microsoft 365 Copilot extension runs in supported browsers and detects user interactions with content from connected applications. For example, it tracks interactions such as viewing, editing, or engaging with items such as tickets, documents, or knowledge articles.

The extension sends activity signals only when the following conditions are met:

- The connector is enabled in the tenant.
- The connector is configured to support activity signal ingestion.
- The visited URL can be mapped to an indexed item in the connector.
- The user has access to the content in the source system.

These signals are then associated with indexed connector items and used by Copilot and Microsoft Search to improve ranking, relevance, and response quality.

## Admin prerequisites

Before you deploy the extension and enable activity signals, make sure that the following prerequisites are met:

- A Microsoft 365 Copilot connector is configured, authorized, and in a **Ready** state.
- Connector content is successfully crawled and searchable in Copilot and Microsoft Search.
- User-facing content is accessible through stable browser URLs.
- You have permissions to manage connectors and deploy browser extensions.
- You can configure connector activity settings by using the Microsoft Graph API.

## Configure activity signal ingestion

To enable activity signals, you must configure activity settings on the connector so the system can map visited URLs to indexed item IDs.

Before you configure activity settings:

- Confirm that the connector state is **Ready** in the Microsoft 365 admin center.
- Validate that items from the data source appear in search results.
- Identify the URL patterns used to display individual items in the source system.
- Retrieve the connector ID by using the Microsoft Graph API.

If activity settings are already present, verify that they match the URLs users visit.

### Define activity settings

Activity signals are generated only when the system can resolve a URL to a specific item ID. This mapping is defined in the connector’s activity settings.

Use the Microsoft Graph API to:

- Specify base URLs that represent supported user-facing domains.
- Define URL-to-item resolvers that extract item IDs from URLs.
- Map extracted IDs to the connector’s item schema.

If activity settings are missing or misconfigured, no activity signals are captured.

### Deploy the Microsoft 365 Copilot extension

The extension must be installed and active in users' browsers to collect activity signals.

As an admin, you can deploy the extension by using centralized browser management tools such as Microsoft Intune or Group Policy. Silent deployment ensures that the extension is installed without requiring user action.

After deployment, verify that:

- The extension appears in the browser's extension list.
- The extension is enabled.
- The extension name is shown as **Microsoft 365 Copilot extension**.

### Validate signal ingestion

After you deploy the extension, validate the signals:

- Go to known item pages in supported browsers.
- Perform related searches in Copilot or Microsoft Search.
- Confirm that recently viewed items are prioritized in results.

Allow time for signals to propagate before you perform validation.

## Guidance for common issues

When you configure activity signal ingestion, keep the following guidance in mind:

- Include all relevant domain variants in base URLs.
- Use precise URL patterns to avoid matching dashboards or non-item pages.
- Ensure that extracted IDs match the IDs used during indexing.
- Test configurations with real user-facing URLs.

If no signals appear to be captured:

- Confirm that the extension is installed and enabled.
- Verify that the user is signed in and has access to the content.
- Recheck activity settings on the connector.
- Make sure that the visited URLs match the configured base URLs and patterns.

## Browser extension user experience

From a user perspective, the Microsoft 365 Copilot extension works automatically in the background and doesn't require manual interaction.

Users continue to browse and work in applications as usual. When they view or interact with supported content, Copilot uses those signals to tailor future results. For example:

- Two users searching for the same term might see different results based on what they recently worked on.
- Frequently viewed tickets, documents, or pages might appear higher in Copilot responses.
- Content from external systems is more tightly integrated into Microsoft 365 experiences.

The extension collects signals only from administrator-approved applications and doesn't track general web browsing. Existing permissions in the source systems are always respected.

## Supported connectors

The Microsoft 365 Copilot extension works with Microsoft 365 Copilot connectors that support activity signal ingestion. Supported sources include common enterprise tools such as issue tracking systems, document repositories, and CRM platforms, depending on which connectors are enabled in the tenant.

## Related content

- [Deploy Microsoft 365 Copilot connectors](deployment-overview.md)