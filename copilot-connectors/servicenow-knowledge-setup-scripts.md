---
title: Set up ServiceNow Knowledge connector prerequisites by using background scripts
description: Use background scripts to automate the ServiceNow configuration steps required for the ServiceNow Knowledge Microsoft 365 Copilot connector, including service account creation, ACL setup, and Scripted REST API configuration.
ms.author: mayanksethi
author: mayanksethi
manager: calvind
ms.reviewer: lauragra
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.localizationpriority: medium
ms.date: 04/02/2026
---

# Set up ServiceNow Knowledge connector prerequisites by using background scripts

You can run background scripts that automate the configuration steps for the [ServiceNow Knowledge Microsoft 365 Copilot connector](servicenow-knowledge-overview.md) instead of completing the steps manually. The scripts are hosted on GitHub at [microsoft/copilot-servicenow-connector-setup-scripts](https://github.com/microsoft/copilot-servicenow-connector-setup-scripts).

These scripts perform the same configuration as the manual steps described in [Set up the ServiceNow service](servicenow-knowledge-admin-setup.md) and [Grant table access](granting-table-access-servicenow-knowledge.md). They don't introduce any extra permissions, plugins, or external connections.

## Prerequisites

The scripts require the following prerequisites:

- ServiceNow admin account with the `security_admin` role elevated.
- Access to **System Definition > Scripts - Background** in your ServiceNow instance.

## Scripts overview

| Script | What it does | Equivalent manual steps |
|--------|-------------|------------------------|
| [row_level_acl_setup.js](https://github.com/microsoft/copilot-servicenow-connector-setup-scripts/blob/main/row_level_acl_setup.js) | Creates service account, custom role, and row-level READ ACLs for all required tables | [Create service account and set up permissions](servicenow-knowledge-admin-setup.md#create-service-account-and-set-up-permissions-to-index-items) and [Grant table access](granting-table-access-servicenow-knowledge.md) |
| [field_level_acl_setup.js](https://github.com/microsoft/copilot-servicenow-connector-setup-scripts/blob/main/field_level_acl_setup.js) | Creates field-level READ ACLs (`table.*`) for tables where field values are restricted | [Grant field-level access](granting-table-access-servicenow-knowledge.md#grant-field-level-access) |
| [scripted_rest_api_setup.js](https://github.com/microsoft/copilot-servicenow-connector-setup-scripts/blob/main/scripted_rest_api_setup.js) | Creates the Scripted REST API endpoint for the Advanced connector flow | [Set up REST API](servicenow-knowledge-admin-setup.md#set-up-rest-api) |

All scripts are:

- **Idempotent** — Safe to run multiple times. Existing records are reused, not duplicated.
- **Non-destructive** — Sripts don't modify, delete, or overwrite any existing records.
- **Self-contained** — No external dependencies or network calls outside your ServiceNow instance.

## Step 1: Create service account and grant row-level access

The `row_level_acl_setup.js` script creates a service account user, a custom role, assigns the role to the user, and creates row-level READ ACLs for all tables required by the connector.

1. Elevate your role to `security_admin` in ServiceNow.
1. Go to **All > System Definition > Scripts - Background**.
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

1. Set a password for the service account (for example, `microsoft.copilot`).
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

If the service account can view rows but field values appear empty, run the `field_level_acl_setup.js` script. This script creates a field-level READ ACL (`table.*`) for each configured table and links it to the custom role created in Step 1.

1. Elevate your role to `security_admin` in ServiceNow.
1. Go to **All > System Definition > Scripts - Background**.
1. Copy the script from [field_level_acl_setup.js](https://github.com/microsoft/copilot-servicenow-connector-setup-scripts/blob/main/field_level_acl_setup.js) and paste it into the script editor.

    > [!TIP]
    > If your role name differs from the default (`copilot_connector`), update the `TARGET_ROLE_NAME` variable at the top of the script before running it. You can also add or remove tables from the `TABLES` list based on which tables have restricted field values on your instance.

1. Select **Run script**.
1. Review the output summary to confirm all steps completed successfully.

**How to verify:**

1. Use a REST client to query a table as the service account (same approach as Step 2).
1. Confirm that both rows **and** field values are now returned in the response.

## Step 4: Set up REST API for advanced flow

If your ServiceNow instance uses advanced scripts in user criteria (rather than simple user or group-based criteria), select the **Advanced** flow when you configure the connector in the Microsoft 365 admin center. Run the `scripted_rest_api_setup.js` script to create the Scripted REST API endpoint that the connector calls to resolve user criteria at query time.

To determine whether your instance uses advanced user criteria, see [Check for advanced scripts and hierarchical permissions](servicenow-knowledge-admin-setup.md#check-for-advanced-scripts-and-hierarchical-permissions-in-servicenow).

1. Elevate your role to `security_admin` in ServiceNow.
1. Go to **All > System Definition > Scripts - Background**.
1. Copy the script from [scripted_rest_api_setup.js](https://github.com/microsoft/copilot-servicenow-connector-setup-scripts/blob/main/scripted_rest_api_setup.js) and paste it into the script editor.

    > [!TIP]
    > If your crawling service account uses a custom role instead of `admin`, update the `ROLE_NAME` variable at the top of the script before you run it. For example: `var ROLE_NAME = 'copilot_connector';`

1. Choose **Run script** and review the output summary. A successful run ends with:

    ```
    All steps completed successfully. No manual actions needed.
    ```

    If any step can't be completed automatically (for example, on older ServiceNow versions), the output lists specific manual follow-ups.

**How to verify:**

1. Go to **Scripted REST APIs** > **Microsoft Copilot**. Under **Security**, confirm **Default ACLs** shows **Microsoft Copilot, Scripted REST External Default**.
1. Open the **GetAllUserCriteria** resource. Under **Security**, confirm **Requires authentication** and **Requires ACL authorization** are checked, and **ACLs** shows **Microsoft Copilot, Scripted REST External Default**.
1. Note the **Resource path** (for example, `/api/<namespace>/microsoft_copilot/user_criteria`). The Microsoft 365 admin enters the `<namespace>` value when they [deploy the ServiceNow Knowledge connector](servicenow-knowledge-deployment.md).

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
- [Setup scripts on GitHub](https://github.com/microsoft/copilot-servicenow-connector-setup-scripts)
