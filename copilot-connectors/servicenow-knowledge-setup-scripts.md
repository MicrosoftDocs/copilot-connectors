---
title: Set up ServiceNow Knowledge connector prerequisites by using background scripts
description: Use background scripts to automate service account creation, ACL setup, and Scripted REST API configuration for the ServiceNow Knowledge Microsoft 365 Copilot connector.
ms.author: mayanksethi
author: mayanksethi
manager: calvind
ms.reviewer: jasonjoh
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 10/09/2026
---

<!-- cSpell:ignore mayanksethi useraccount grmember -->

# Set up ServiceNow Knowledge connector prerequisites by using background scripts

You can run background scripts that automate some configuration steps for the [ServiceNow Knowledge Microsoft 365 Copilot connector](servicenow-knowledge-overview.md). These scripts perform the same configuration as the corresponding manual steps described in [Set up the ServiceNow service](servicenow-knowledge-admin-setup.md), [Grant table access](granting-table-access-servicenow-knowledge.md), and [Federated Auth](servicenow-knowledge-deployment.md#federated-auth-federated-identity-credentials). They don't introduce any extra permissions, plugins, or external connections.

The scripts are hosted in the [ServiceNow Knowledge connector setup scripts GitHub repo](https://github.com/microsoft/copilot-servicenow-connector-setup-scripts).

## Prerequisites

The scripts require the following prerequisites:

- ServiceNow admin account with the `security_admin` role elevated.
- Access to **System Definition** > **Scripts - Background** in your ServiceNow instance.

## Scripts overview

The following table lists and describes the scripts.

| Script | What it does | Equivalent manual steps |
|--------|-------------|------------------------|
| [federated_auth_setup.js](https://github.com/microsoft/copilot-servicenow-connector-setup-scripts/blob/main/federated_auth_setup.js) | Configures Federated Auth (OIDC): the provider configuration, Application Registry entity, `useraccount` auth scope, and machine integration user. For Federated Auth deployments only. | [Federated Auth](servicenow-knowledge-deployment.md#federated-auth-federated-identity-credentials) |
| [row_level_acl_setup.js](https://github.com/microsoft/copilot-servicenow-connector-setup-scripts/blob/main/row_level_acl_setup.js) | Creates service account, custom role, and row-level READ ACLs for all required tables | [Create service account and set up permissions](servicenow-knowledge-admin-setup.md#create-service-account-and-set-up-permissions-to-index-items) and [Grant table access](granting-table-access-servicenow-knowledge.md) |
| [field_level_acl_setup.js](https://github.com/microsoft/copilot-servicenow-connector-setup-scripts/blob/main/field_level_acl_setup.js) | Creates field-level READ ACLs (`table.*`) for tables where field values are restricted | [Grant field-level access](granting-table-access-servicenow-knowledge.md#grant-field-level-access) |
| [scripted_rest_api_setup.js](https://github.com/microsoft/copilot-servicenow-connector-setup-scripts/blob/main/scripted_rest_api_setup.js) | Creates the Scripted REST API endpoint for the Advanced connector flow | [Set up REST API](servicenow-knowledge-admin-setup.md#set-up-rest-api) |
| [incremental_identity_sync_setup.js](https://github.com/microsoft/copilot-servicenow-connector-setup-scripts/blob/main/incremental_identity_sync_setup.js) | Adds the `user_changes` resource for incremental identity sync, grants read access to the audit tables, and enables table auditing. For Advanced flow only. | [Set up REST API for incremental identity sync](servicenow-knowledge-admin-setup.md#set-up-rest-api-for-incremental-identity-sync) |

All scripts are:

- **Idempotent** — Safe to run multiple times. The scripts reuse existing records and don't create duplicates.
- **Non-destructive** — The scripts don't modify, delete, or overwrite any existing records.
- **Self-contained** — No external dependencies or network calls outside your ServiceNow instance.

## Set up federated authentication

If you deploy the connector by using the **Federated Auth (Federated Identity Credentials)** authentication option, run the `federated_auth_setup.js` script first. It configures the OpenID Connect (OIDC) provider, the Application Registry entity, the `useraccount` auth scope, and the machine integration user that the connector authenticates as. For other authentication methods, such as Basic auth or OAuth 2.0, skip this section.

1. Elevate your role to `security_admin` in ServiceNow.
1. Go to **All** > **System Definition** > **Scripts - Background**.
1. Copy the script from [federated_auth_setup.js](https://github.com/microsoft/copilot-servicenow-connector-setup-scripts/blob/main/federated_auth_setup.js) and paste it into the script editor.

    > [!TIP]
    > Set the `SP_OBJECT_ID` (service principal object ID) and `TENANT_ID` (Microsoft Entra tenant ID) variables in the **CONFIGURATION** section before you run the script. To find these values, see [Federated Auth](servicenow-knowledge-deployment.md#federated-auth-federated-identity-credentials).

1. Select **Run script**.
1. Review the output summary to confirm all steps completed successfully.

When you run the `row_level_acl_setup.js` script in the next step, set its `USER_ID` to the same service principal object ID so that the read role and ACLs are assigned to the integration user that the connector maps to.

## Step 1: Create service account and grant row-level access

The `row_level_acl_setup.js` script creates a service account user, a custom role, assigns the role to the user, and creates row-level READ ACLs for all tables required by the connector.

1. Elevate your role to `security_admin` in ServiceNow.
1. Go to **All** > **System Definition** > **Scripts - Background**.
1. Copy the script from [row_level_acl_setup.js](https://github.com/microsoft/copilot-servicenow-connector-setup-scripts/blob/main/row_level_acl_setup.js) and paste it into the script editor.

    > [!TIP]
    > Review the **CONFIGURATION** section at the top of the script before running. You can change the role name, user ID, and user name to match your organization's naming conventions.

1. Select **Run script**.
1. Review the output summary to confirm all steps completed successfully.

**What the script doesn't do:**

- It doesn't grant field-level access. If the service account can view rows but field values aren't visible, you need to grant field-level access separately. See [Step 3](#step-3-grant-field-level-access-if-needed).
- It doesn't set the service account password. You must set the password manually after running the script.

## Step 2: Verify row-level access

After running the row-level script, verify that the service account can access the required tables.

1. Set a strong, unique password for the service account that complies with your organization's password policy.
1. Use a REST client (for example, curl or Postman) to query a table as the service account:

    ```http
    GET https://<instance>.service-now.com/api/now/table/kb_knowledge?sysparm_limit=1
    ```

    Authenticate with the service account credentials (Basic Auth).

1. Confirm that rows are returned in the response.

> [!NOTE]
> On Zurich and later releases, the script marks the service account as a machine identity (`identity_type = machine`), which automatically enables "Web service access only". Machine identity accounts can't be impersonated through the ServiceNow UI. Use the REST API to verify access instead.

If rows are returned with field values populated, skip to [Step 4](#step-4-set-up-rest-api-for-advanced-flow). If rows are returned but field values are empty, continue to Step 3.

## Step 3: Grant field-level access (if needed)

Run this step **only** if the service account can view rows but field values appear empty. The `field_level_acl_setup.js` script creates a field-level READ ACL (`table.*`) for each table you list and links it to the custom role created in Step 1.

> [!WARNING]
> On a table that has no existing field-level read ACL, creating a `table.*` read ACL **removes field read access for every user that doesn't have the connector role**. ServiceNow has no default `*.*` read ACL to fall through to, so the new `table.*` ACL becomes the only match. To limit the impact, the script ships with an **empty `TABLES` list** and with `DRY_RUN` set to `true`, so the first run makes **no changes** and only reports what it would do. Review that output, add only the tables you verified actually restrict field values, and prefer per-field ACLs for shared, platform-wide tables (such as `sys_user`, `sys_user_group`, `sys_dictionary`, `sys_properties`, and `core_company`). For details, see [Grant field-level access](granting-table-access-servicenow-knowledge.md#grant-field-level-access).

1. Confirm which tables need field-level access. Query each candidate table as the service account (same REST approach as Step 2) and note only the tables where rows return but field values are empty.
1. Elevate your role to `security_admin` in ServiceNow.
1. Go to **All** > **System Definition** > **Scripts - Background**.
1. Copy the script from [field_level_acl_setup.js](https://github.com/microsoft/copilot-servicenow-connector-setup-scripts/blob/main/field_level_acl_setup.js) and paste it into the script editor.
1. Add the tables you confirmed in step 1 to the `TABLES` list at the top of the script. If your role name differs from the default (`copilot_connector`), also update the `TARGET_ROLE_NAME` variable.
1. Leave `DRY_RUN` set to `true` and select **Run script**. The script makes no changes. It lists the ACLs it would create and flags each table where it would add the first field-level read ACL (which would remove field read access for users without the connector role).
1. Review the dry-run output and remove any table you don't intend to restrict.
1. Set `DRY_RUN` to `false` and select **Run script** again to create the ACLs.

**How to verify:**

1. Use a REST client to query the table as the service account (same approach as Step 2), and confirm that both rows **and** field values are now returned. This confirms the connector can read the fields.
1. Check the side effect on other users. Sign in as (or impersonate) an affected non-admin user who doesn't have the connector role, and confirm they still have the field access they need. Don't use the service account for this check. It holds the connector role, so it keeps access and would report success even if other users are locked out. Admins also bypass the restriction when **Admin overrides** is set.

## Step 4: Set up REST API for advanced flow

If your ServiceNow instance uses advanced scripts in user criteria (rather than simple user or group-based criteria), select the **Advanced** flow when you configure the connector in the Microsoft 365 admin center. Run the `scripted_rest_api_setup.js` script to create the `GetAllUserCriteriaV2` resource that the connector calls to resolve user criteria at query time.

To determine whether your instance uses advanced user criteria, see [Check for advanced scripts and hierarchical permissions](servicenow-knowledge-admin-setup.md#check-for-advanced-scripts-and-hierarchical-permissions-in-servicenow).

1. Elevate your role to `security_admin` in ServiceNow.
1. Go to **All** > **System Definition** > **Scripts - Background**.
1. Copy the script from [scripted_rest_api_setup.js](https://github.com/microsoft/copilot-servicenow-connector-setup-scripts/blob/main/scripted_rest_api_setup.js) and paste it into the script editor.

    > [!TIP]
    > By default, the scripts use the `copilot_connector` role for the crawling service account. If your service account uses a different custom role, update the `ROLE_NAME` variable at the top of the script before you run it. For example: `var ROLE_NAME = 'copilot_connector';`.

1. Choose **Run script** and review the output summary.

**How to verify:**

1. Go to **Scripted REST APIs** > **Microsoft Copilot**. Under **Security**, confirm **Default ACLs** shows **Microsoft Copilot, Scripted REST External Default**.
1. Open the **GetAllUserCriteriaV2** resource. Under **Security**, confirm **Requires authentication** and **Requires ACL authorization** are checked, and **ACLs** shows **Microsoft Copilot, Scripted REST External Default**.
1. Confirm the resource uses the `POST` method and `/user_criteria_v2` relative path. The Microsoft 365 admin enters the API namespace when they [deploy the ServiceNow Knowledge connector](servicenow-knowledge-deployment.md).

For the complete resource configuration and script, see [Set up REST API](servicenow-knowledge-admin-setup.md#set-up-rest-api).

## Step 5: Set up incremental identity sync

Incremental identity sync keeps identity changes—new or removed users, role and group memberships, and user criteria definitions—up to date between full crawls. It applies only to the **Advanced** flow. Run the `incremental_identity_sync_setup.js` script after `scripted_rest_api_setup.js`.

1. Elevate your role to `security_admin` in ServiceNow.
1. Go to **All** > **System Definition** > **Scripts - Background**.
1. Copy the script from [incremental_identity_sync_setup.js](https://github.com/microsoft/copilot-servicenow-connector-setup-scripts/blob/main/incremental_identity_sync_setup.js) and paste it into the script editor.

    > [!TIP]
    > By default, the script uses the `copilot_connector` role for the crawling service account. If your service account uses a different custom role, update the `ROLE_NAME` variable at the top of the script before you run it.

1. Choose **Run script** and review the output summary.

**What the script does:**

- Adds the `user_changes` resource (`GET` `/user_changes`) to the **Microsoft Copilot** scripted REST API.
- Creates row-level READ ACLs for `sys_audit` and `sys_audit_delete`, linked to the crawling role.
- Enables **table-level** auditing on `sys_user`, `sys_user_has_role`, `sys_user_grmember`, and `user_criteria`, and sets the field-level audit flags on the monitored fields. Table-level auditing is what lets ServiceNow record field changes in `sys_audit` (and deletions in `sys_audit_delete`).

**How to verify:**

1. Go to **Scripted REST APIs** > **Microsoft Copilot** and open the **user_changes** resource. Confirm it uses the `GET` method and `/user_changes` relative path, with **Requires authentication** and **Requires ACL authorization** checked.
1. Make a test change and a test deletion to an audited record, then confirm entries appear in `sys_audit` and `sys_audit_delete`.

For the complete resource configuration, script, and auditing requirements, see [Set up REST API for incremental identity sync](servicenow-knowledge-admin-setup.md#set-up-rest-api-for-incremental-identity-sync).

## Configuration options

Each script includes a clearly marked **CONFIGURATION** section at the top where you can customize:

- **Role name** — Default: `copilot_connector`
- **Service account user ID** — Default: `microsoft.copilot`
- **Table lists** — Add or remove tables based on your instance requirements

## Verify service account permissions

After you run the scripts, use the **Copilot Connector Checker Tool** to confirm that all required permissions are configured correctly:

1. Open the [Copilot Connector Checker Tool](https://testconnectivity.microsoft.com/tests/CopilotServiceNowGraphConnectors/input).
1. Choose the authentication type in the **Authentication Type** field: Basic or OAuth (recommended).
1. Complete the fields and choose **Perform Test**.
1. The tool automatically validates connectivity, verifies credentials, checks table-level permissions, provides a summary of results, and recommends next steps as needed.

## Related content

- [Set up the ServiceNow service for connector ingestion](servicenow-knowledge-admin-setup.md)
- [Grant table access to a service account in ServiceNow](granting-table-access-servicenow-knowledge.md)
- [Deploy the ServiceNow Knowledge connector](servicenow-knowledge-deployment.md)
- [Setup scripts GitHub repo](https://github.com/microsoft/copilot-servicenow-connector-setup-scripts)
