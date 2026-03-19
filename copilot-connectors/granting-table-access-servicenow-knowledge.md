---
ms.date: 02/23/2026
title: "Grant table access to a service account in ServiceNow Knowledge"
ms.author: lauragra
author: lauragra
manager: calvind
ms.reviewer: mayanksethi
audience: Admin 
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Grant table access to a service account in ServiceNow that can be used to set up ServiceNow Knowledge Microsoft 365 Copilot connectors."
---

# Grant table access to an account in ServiceNow Knowledge

This article explains how to grant table access to a service account in ServiceNow Knowledge. The process involves creating a role, assigning it to a user, and configuring row-level and field-level access controls.

## Prerequisites

- Admin access in ServiceNow.
- Elevate to the `security_admin` role to make changes to access control lists (ACLs).
  
## Create a user

To create a user:

1. Go to **User Administration > Users**.
1. Select **New** to create a new user.
1. Fill in the user details:
   - For the **User ID**: `microsoft.copilot`. The **User ID** is required for successful crawls.
   - For the **First Name** and **Last Name**: `Microsoft` and `Copilot`.
   - Set **Identity Type** to `Machine`. For earlier versions of ServiceNow, check **Web service access only**. 
1. Select **Submit** to save the user.

##  Create a role

To create a role:

1. Go to **User Administration > Roles**.
1. Select **New**.
1. Enter a unique name for the role (for example, `Copilot Connector Account`).
1. Select **Submit** to save the role.

## Assign the role to a user

To assign the role to a user:

1. Go to **User Administration > Users**.
1. Open the user record for the intended user (for example, `Microsoft Copilot`).
1. In the **Roles** related list, select **Edit**.
1. Add the newly created role (`Copilot Connector Account`).

    > [!NOTE]
    > You might also assign the following roles to the service account so knowledge articles are indexed without any blocking ACL issues: `knowledge_admin`, `user_criteria_admin`, `user_admin`. Assigning these roles is optional.

1. Select **Save** to finalize the assignment.
1. Select **Update** to update the user record.

## Grant row-level access

To grant access to rows within a specific table, follow these steps:

1. Elevate to the `security_admin` role.
1. Go to **System Security > Access Control (ACL)**.
1. Select **New** to create a new ACL record.
1. Fill in the following fields:
   - **Type**: Select **record**.
   - **Operation**: Choose the `read` operation.
   - **Name**: Enter the table name (for example, `sys_dictionary`).
1. In the **Roles** section, add the previously created role (`Copilot Connector Account`).
1. Select **Submit** to save the ACL.

## Verification

1. Impersonate the user (for example, `Microsoft Copilot`).
1. Access the target table (for example, `sys_dictionary`) and confirm that rows are visible. 

If the user can view the rows, but the field values aren't visible, you need to [grant field-level access](#grant-field-level-access).

## Grant field-level access

If the user can view rows but not field values, configure field-level access:

1. Go to **System Security > Access Control (ACL)**.
1. Select **New** to create a new ACL record.
1. Fill in these fields:
   - **Type**: Select **record**.
   - **Operation**: Choose the `read` operation.
   - **Name**: Enter the table name (for example, `sys_dictionary`) and use `*` in the field name to apply to all fields.
1. In the **Roles** section, add the previously created role (`Copilot Connector Account`).
1. Select **Submit** to save the ACL.

## Final verification

To verify access to the table:

1. Impersonate the user (for example, `Microsoft Copilot`).
1. Confirm that both rows and field values within the target table are now visible.

You successfully granted table access to a service account in ServiceNow.

## Verify service account permissions

You can use the **Copilot Connector Checker Tool** to confirm that all required permissions for ServiceNow Knowledge Base (KB) tables are configured correctly:

1. Open the [Copilot Connector Checker Tool](https://testconnectivity.microsoft.com/tests/CopilotServiceNowGraphConnectors/input).
1. Choose the authentication type in the **Authentication Type** field: Basic or OAuth (recommended).
1. Complete the fields and choose **Perform Test**.
1. The tool automatically validates connectivity, verifies credentials, checks table-level permissions, provides a summary of results, and recommends next steps as needed.

If you have feedback about the tool, choose the **Feedback** link at the bottom of the page.