---
title: "Set up Galileo by The Josh Bersin Company for connector ingestion"
ms.author: xupzhou
author: xupzhou
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: copilot-connectors
ms.date: 09/11/2026
ms.localizationpriority: Medium
description: "Prepare your Microsoft 365 environment, access group, and credentials before deploying the Galileo by The Josh Bersin Company Copilot connector."
---

# Set up Galileo by The Josh Bersin Company for connector ingestion

This article describes the administrative and onboarding tasks to complete before you deploy the Galileo by The Josh Bersin Company Microsoft 365 Copilot connector.

For information about deploying the connector after setup is complete, see [Deploy the Galileo by The Josh Bersin Company connector](galileo-deployment.md).

## Prerequisites

Before you begin, make sure that you meet the following prerequisites:

- **Josh Bersin account**: You need a valid Josh Bersin license to access content. Contact The Josh Bersin Company to request the credentials required for access.
- **Service account**: You must be an admin for your organization's Microsoft 365 tenant.
- Each user who accesses Galileo content through Copilot needs a Microsoft 365 Copilot license.

## Identify the Galileo instance URL

The Galileo data API endpoint is prefilled when you configure the connector in the Microsoft 365 admin center. Confirm the endpoint with your Josh Bersin Company contact. Don't change the prefilled value unless your contact directs you to do so.

## Enable API access

Make sure that the connector account has API access and that no API restrictions or app allowlists prevent access.

## Create OAuth application and rollout audience

1. Under **Authentication**, select **OAuth 2.0 Client Credentials**.
1. Enter the client ID and client secret from your onboarding package. A green check appears next to each value when the credentials are accepted.
1. Turn on **Rollout to limited audience**.
1. Select your Galileo access group.

> [!IMPORTANT]
> The **Rollout to limited audience** setting is the master audience control for Galileo in your tenant. The audience you select is the maximum audience for every downstream experience, including agents.

1. Review Microsoft's data notice.
1. Select the acknowledgment.
1. Create the connection.
