---
title: "Submit a federated Microsoft 365 Copilot connector"
description: "Learn how to submit a remote Model Context Protocol (MCP) server as a federated Microsoft 365 Copilot connector, including publishing paths, required metadata, and review expectations."
ms.author: danielabo
author: danipocket
manager: calvind
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: microsoft-365-copilot-connectors
ms.date: 06/03/2026
ms.localizationpriority: Medium
---

# Submit a federated Microsoft 365 Copilot connector

[!INCLUDE [wiqd-beta-disclaimer](includes/wiqd-beta-disclaimer.md)]

The federated Microsoft 365 Copilot connector program allows partners to submit a remote Model Context Protocol (MCP) server to Microsoft for inclusion in the Connectors Gallery for Microsoft 365 Copilot tenants. After Microsoft approves your MCP server and adds it to the gallery, tenant admins review and approve the connector for their organization. After an admin approves it, Microsoft 365 Copilot connects to your remote MCP server through a public HTTPS endpoint and surfaces your content in Copilot experiences. This article explains what a connector delivers, which publishing route applies to you, how to test before you publish, and what to expect during review.

## What a connector gives your customers

A connector is built and certified once, and it answers everywhere the user works. Approved connectors surface content in Microsoft 365 Copilot Chat, Copilot in Excel, Cowork, and the Researcher agent, with Word and PowerPoint coming soon. You don't integrate per surface and you don't maintain a separate path for each experience; your content follows the user into whichever surface they open.

## Example scenarios by domain

The scenarios below show what a connector looks like in daily use.

| Domain | Connected content | What Copilot does with it | Surfaces |
|---|---|---|---|
| Engineering and IT | Incident tickets, runbooks, service catalogs | Pulls the incident history behind a question and cites the tickets it used | Chat, Researcher agent |
| Sales | CRM accounts, opportunities, call notes | Assembles an account brief ahead of a customer meeting | Chat, Cowork |
| Finance | Billing systems, spend and vendor records | Answers a spend question and returns the underlying rows for analysis | Excel, Chat |
| HR and people | Policy libraries, benefits and case systems | Answers a policy question with the governing policy cited | Chat |
| Legal and compliance | Contract repositories, matter management | Finds the clauses and matters behind a review question | Researcher, Cowork |
| Field and operations | Asset, work order and inventory systems | Surfaces asset history and open work orders in context | Chat, Excel |

## Choose your publishing path

How you publish depends on who your connector serves. Independent software vendors build for many tenants and publish commercially. Line-of-business teams build for their own organization and publish internally. Find your row in the following table, then follow the matching section.

| You are | Publish through | Test with | What to expect |
|---|---|---|---|
| An ISV building for many tenants | A plugin package submitted in Partner Center | A test tenant and the reviewer test account, before certification | Store listing, certification review, store-managed updates |
| A line-of-business team building for one tenant | The Microsoft 365 admin center | Sideloading on pilot devices | Admin approval and scoping inside your tenant; Microsoft Store submission available as an additional route |

## For ISVs: package your connector as a plugin

Your connector reaches customers as a packaged plugin submitted through Partner Center. The connector itself doesn't change: a remote MCP server behind a public HTTPS endpoint, with search and fetch tools annotated `readOnlyHint`, and OAuth 2.0 for authenticated scenarios. What changes is the package around it and the storefront it arrives through.

### Before you start

- A Partner Center account with the developer or manager role, so you can create the product and receive submission notifications.
- A reachable public HTTPS endpoint for your MCP server, with every tool carrying a human-readable title and the `readOnlyHint` annotation.
- OAuth 2.0 credentials registered with Microsoft for any authenticated scenario, plus a test account that reviewers can use.
- Listing assets: display name, an 80-character description, up to 10 synonyms, a 192 x 192 color logo, a 32 x 32 outline logo, and links to your documentation, privacy policy, and support channel.

## Submit through Partner Center

Reserve your product name first, then open the submission. Names are unique across the store, and a reservation holds yours for three months, which is usually long enough to finish development without losing the branding you build.

1. Reserve the product name in the **Apps and games** section of Partner Center: choose the product type, enter the title, check availability, and reserve it.
1. Set pricing and availability, including markets and any trial.
1. Set properties, including category and declared capabilities.
1. Complete the age ratings questionnaire.
1. Upload your packages.
1. Complete the store listing: description, feature list, screenshots, and logos.
1. Review submission options, including certification notes, any scheduled publish date, and who receives submission notifications.
1. Select **Submit for certification**.

Partner Center validates your inputs and flags missing items before the submission goes through. Your product shows as in certification while it is under review. The account owner is always notified of publishing status. Add teammates as developers or managers if they need the same notifications.

## Test before you submit

Test the connector end to end before certification rather than after. Exercise every tool you declared against the same test account you hand to reviewers, confirm each one returns results for the sample prompts you plan to ship, and check the behavior in more than one surface, since the same connector answers in Chat, Excel, Cowork, and the Researcher agent. Supply at least three prompts with their expected responses: reviewers use them, and they double as your own regression set.

## Common points of confusion

If you come from declarative agent development, these distinctions are worth reading before you package anything.

| What you might have heard | How it actually works |
|---|---|
| The declarative agent plugin manifest and the agent connector manifest are the same file. | They aren't interchangeable. A declarative agent plugin and an agent connector are different artifacts, and each has its own manifest and its own submission path. |
| Plugins only work in Cowork. | A published connector answers across Chat, Excel, Cowork, and Researcher, with Word and PowerPoint coming soon. You don't publish separately for each surface. |
| Publishing to the Microsoft Store replaces the admin center path. | It doesn't. The Microsoft 365 admin center experience is generally available and isn't being withdrawn. Store submission is an additional route. |
| There's no way to try an app before publishing it. | Sideload a signed package onto pilot devices first. See [Test by sideloading](/windows/application-management/sideload-apps-in-windows). |

## For line-of-business apps: publish through the Microsoft 365 admin center

If you're building for your own organization, publish through the Microsoft 365 admin center. It's the guided path from a working connector to an approved app inside one tenant: an admin uploads the app, reviews what it can reach, and approves it for the organization or for a pilot group, without leaving the console they already use to administer Copilot. This experience is generally available.

Microsoft Store submission is now available to line-of-business teams as well. It's an addition, not a replacement: the admin center path stays as it is. Choose store submission when you want store-managed distribution, signing, and updates instead of maintaining your own hosting and certificate rotation. Choose the admin center when the app serves one tenant and you want approval and scoping to stay with your Copilot admins.

## Test by sideloading

Before you publish to the whole tenant, sideload the app onto a few pilot devices. Sideloading deploys a signed app package directly to a device, and you keep the signing, hosting, and deployment. You need devices with sideloading enabled, a trusted certificate assigned to your app, and a package signed with that same certificate. License keys aren't required, and devices don't have to be joined to a domain.

1. Turn on sideloading. On managed devices, use group policy or a mobile device management provider such as Microsoft Intune to apply the policy to your target devices. On an unmanaged device, turn on Developer mode in Settings.
1. Import the security certificate to the local device. Open the app package properties, use the certificate import wizard, and install into the Trusted Root Certification Authorities store. This step creates the trust between the device and the app.
1. Install the app. Open the package in File Explorer, distribute it over the network with a web-based app installer, or use the `Add-AppxPackage` PowerShell cmdlet.

> [!IMPORTANT]
> When you enable sideloading, you allow apps from outside the Microsoft Store to install and run, which can increase security risks to the device and your data. Keep it scoped to your test devices and turn it off when the pilot ends. If an organizational policy blocks sideloading, users can't turn it on themselves.

## Submit through the Microsoft Store

Store submission for line-of-business apps follows the same Partner Center flow described earlier in this article. Reserve the product name, complete the submission pages, upload your package, and submit for certification. See [Submit your app to Microsoft Store](/windows/apps/publish/).

For best practices, see the [Teams Store validation guidelines](/microsoftteams/platform/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines).

## Required metadata and assets

Provide the following artifacts with your submission. Incomplete artifacts can slow down the review process.

| Field | Requirement |
|---|---|
| **MCP server URL** | Public HTTPS endpoint for your MCP server. For example: `https://mcp.contoso.com/mcp`. |
| **Connector display name** | User-facing connector name. |
| **Short description** | Public description, 80 characters or fewer. |
| **Synonyms** | Up to 10 comma-separated keywords users might search for. Avoid generic or competitor names. |
| **Logo (color.png)** | 192 x 192 pixel full-color PNG. |
| **Logo (outline.png)** | 32 x 32 pixel white-on-transparent PNG. |
| **OAuth credentials** | OAuth reference ID for your Microsoft registration. |
| **Tool list** | Complete list of tools with human-readable names and confirmation that each tool includes the `readOnlyHint` annotation. |
| **Documentation and support** | Links to product documentation, privacy policy, and support channel. |
| **Test credentials** | Test account details and step-by-step setup instructions for reviewers. |
| **Sample prompts** | At least three prompts with expected responses that demonstrate connector capabilities. |

## Review and onboarding

Microsoft accepts submissions on a rolling basis. Review time varies with submission volume and how complete your artifacts are. After you submit, Microsoft validates the metadata, assets, and technical requirements, integrates the connector, coordinates validation by mail, then moves to release discussions and ring-based rollout planning.

After Microsoft approves the connector and publishes it in the gallery, each customer organization's admin must approve it before it is enabled for that organization. Microsoft doesn't provide notifications for every intermediate status change. For status questions, contact your Microsoft representative.

When you submit, you agree to maintain connector functionality and security over time, respond promptly to security issues, provide accurate metadata, assets, and documentation, and support Microsoft validation and ring-based rollout activities.

## Related content

- [Microsoft Product Terms](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/MCA)
- [Federated connectors overview](federated-connectors-overview.md)
- [Set up custom federated connectors](set-up-custom-federated-connectors.md)
- [Create OAuth credentials](set-up-custom-federated-connectors.md#oauth-20)
