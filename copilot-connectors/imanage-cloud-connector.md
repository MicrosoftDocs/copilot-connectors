---
ms.date: 11/19/2025
title: "iManage Cloud connector (preview)"
ms.author: danielabo
author: danielabo
manager: laugra
audience: Admin
ms.audience: Admin
ms.topic: install-set-up-deploy
ms.service: copilot-connectors
ms.localizationpriority: Medium
description: "Set up the iManage Cloud Microsoft 365 Copilot connector."
---

# iManage Cloud connector (preview)

The iManage Cloud Microsoft 365 Copilot connector enables your organization to index content from iManage Cloud so users can discover it in Microsoft 365 Copilot experiences and Microsoft Search clients. This connector is part of the Microsoft 365 Copilot connectors platform and supports Copilot extensibility scenarios.

> [!IMPORTANT]
> **Preview scope & gating**  
> - **Supported (preview):** **multi-tenant iManage Cloud (`https://cloudimanage.com`)** only.  
> - **Not supported:** on-premises iManage or **single-tenant/private cloud** environments (for example, `imanage.work`).  
> - Although this Learn page is public, **the connector is not discoverable or deployable** unless your tenant is **allow-listed/pilot-flag enabled** **and** iManage has created the **per-tenant application with OAuth credentials**. The gallery tile won’t appear otherwise.

## Capabilities

- Indexes content from iManage Cloud workspaces, documents, and metadata.
- Enables semantic search and retrieval in Microsoft 365 Copilot experiences.
- Supports incremental crawls for updated content.
- Supports **matter filters** to **include or exclude** specific matters from the crawl.
- Integrates with Microsoft Search, Microsoft 365 apps, and Copilot extensibility APIs.

## Limitations

- Supports **iManage Cloud (multi-tenant)** only during preview; on-prem and single-tenant/private cloud aren’t supported.
- Limited to English-language content during preview.
- Permissions mapping is based on iManage identities and groups; custom ACLs may not be fully supported.
- Real-time indexing isn’t available; indexing occurs on a scheduled basis.
- Advanced filtering or custom schema extensions may be limited in preview.
- **Identity mapping during preview supports only `userPrincipalName` (UPN) and `mail`. Alias (`mailNickname`) is not supported.**
- **Email transformations (different email formats for dev/prod) aren't supported; mapped identities must remain consistent across environments.**

## Prerequisites

Before setting up the connector, ensure the following:

- You have **Microsoft 365 admin permissions**.
- You can access the **Microsoft 365 admin center**.
- Your tenant has been **allow-listed** for the private preview (pilot flag enabled).
- iManage has created your **per-tenant iManage application** and provided **OAuth credentials** (Client ID/Secret, redirect URIs).
- You have an **iManage Cloud administrator** account (for example, **NRTADMIN** or equivalent) with API access.

## Custom setup

### Step 1: Register the connector

1. Go to the [Microsoft 365 admin center](https://admin.microsoft.com).
2. Navigate to **Copilot > Data connections > Gallery** (the **iManage Cloud** tile is shown only for allow-listed tenants).
3. Search for **iManage** and select **Add**.

> [!NOTE]
> In some preview rings, you may also see a legacy path under **Search & intelligence**; follow the **Copilot > Data connections** path when available.

### Step 2: Configure connection settings

- **Connector name**: `iManage Cloud`  
- **Endpoint URL Example**: `https://cloudimanage.com`  
  > [!NOTE]  
  > **Supported in preview: multi-tenant iManage Cloud (cloudimanage.com). Not supported: on-prem or single-tenant/private cloud (e.g., imanage.work).**
- **Authentication type**: `OAuth 2.0`
- **Client ID / Secret**: Use the **per-tenant iManage app** (“**Microsoft – iManage Cloud Graph Connector**”) created by iManage; enter the **OAuth credentials provided by iManage**.
- **Authorize**: Sign in with an **iManage admin** account (**NRTADMIN** or equivalent).

### Step 3: Map permissions

- Choose who can see the data source in search/Copilot.
- If your identity systems differ, configure **Non-Microsoft Entra ID** mapping (replaces the older “Non-ME-ID” terminology).

#### **Identity mapping behavior**
The connector supports the following Microsoft Entra ID (Azure AD) identity properties:

- **userPrincipalName (UPN)** — recommended  
- **mail** — supported when consistent with UPN  
- **mailNickname (alias)** — **not supported**  

> [!NOTE]
> Some previous documentation referenced “Alias” as a selectable user identity property.  
> **The iManage Cloud connector preview does not support alias-based identity mapping.**  
> Only **UPN** and **mail** may be used.

#### **Regex Requirements**
Regex patterns for identity mapping must **fully match the entire value** of the UPN or mail attribute.

Examples:  
✔ `.*@contoso\.com`  
✘ `.*` (rejected; not a valid full identity pattern)  
✘ partial fragments of an email address  

#### **Email transformations**
If your organization uses different email formats across environments (prod/dev), note:

- Identity transformation or rewriting is **not supported**.
- The connector requires **consistent identity attributes** across environments.

#### **Identity data source**
Identity properties used for mapping (UPN/mail) come from **Microsoft Entra ID**, not from iManage.  
The connector maps Entra ID identities to the corresponding iManage user accounts.

---

### Step 4: Content data

- Select one or more **content libraries** for indexing (default: all libraries).
- Select a **time range** for the content to be indexed.
- **Matter(s) filter:** You can **include** or **exclude** specific matters from the crawl. Provide a JSON array; each matter is identified by `{ "library": "<lib>", "matter": "<workspaceName>" }`. Wildcards/regex are supported for both `library` and `matter`.  
  Examples:  
  - **Exclude**  
    `[{ "library": "lib1", "matter": "projectA" }]`  
    Excludes all documents where `workspaceName = projectA` under `lib1`.  
  - **Include**  
    `[{ "library": "lib1", "matter": "projectA" }]`  
    Ingests only documents where `workspaceName = projectA` under `lib1`.
- **Properties filter:** Define document queries using parameter expressions, for example:  
  `custom1=ACME&custom17=10330-10400&custom25=true&name=contract*`.
- **Manage Properties** to define the connection schema used by Copilot and Search experiences.

### Step 5: Schedule crawls

- Set crawl frequency (for example, daily/weekly).
- Enable **incremental crawls** to reduce load and improve performance.

## Troubleshooting

| Issue | Resolution |
|---|---|
| **Connector fails to authenticate** | Verify the **per-tenant iManage app** is enabled in **iManage Control Center**; confirm **OAuth Client ID/Secret**, **redirect URIs**, and **admin consent**. |
| **No content indexed** | Check content scope and filters; ensure iManage APIs are returning data. |
| **Search results missing** | Confirm identity mapping and crawl status; use Microsoft Search diagnostics. |
| **Copilot not surfacing iManage content** | Ensure your tenant is **allow-listed** and the connection is enabled for Copilot extensibility. |
| **Incremental crawl errors** | Review crawl logs for API rate limits or schema mismatches. |

### Review and test your connection

> [!NOTE]
> **Rollout vs Access Permissions**  
> - **Publish to limited audience** controls who can see the Copilot experience.  
> - **Access Permissions** control which users can retrieve indexed iManage content.  
> These settings operate at different layers and must be configured separately.

- For testing, you can choose [publish to limited audience](./staged-rollout.md#modify-staged-rollout)
- Search and validate your indexed content and permissions using [index browser](indexed-content.md).
- You might find answers to common questions in the [FAQ](./frequently-asked-questions.yml).

For Microsoft Search, if you need to customize the search results page, see [Customize the search results page](/microsoftsearch/customize-search-page).

If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/graph/support).
