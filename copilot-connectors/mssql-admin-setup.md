---
title: "Set up the Azure SQL and Microsoft SQL Server services"
description: "Learn about the configuration steps that database admins complete before you deploy the Azure SQL and Microsoft SQL Server Microsoft 365 Copilot connectors."
author: danipocket
ms.author: danielabo
manager: calvind
ms.reviewer:
audience: Admin
ms.audience: Admin
ms.topic: concept-article
ms.service: microsoft-365-copilot-connectors
ms.date: 08/17/2026
ms.localizationpriority: Medium
---

# Set up the Azure SQL and Microsoft SQL Server services

Before the Azure SQL or Microsoft SQL Server Microsoft 365 Copilot connectors can index your database, you need to prepare the database and its surrounding environment to accept the connection. This article provides information about the configuration steps that Azure SQL and Microsoft SQL Server admins need to complete for your organization to deploy the [Azure SQL and Microsoft SQL Server connectors](mssql-overview.md).

After you complete these steps, see the [deployment guide](mssql-deployment.md) to create the connection in the Microsoft 365 admin center.

## Setup checklist

| Task | Role | Applies to |
|---|---|---|
| Install and configure the Microsoft Graph connector agent | Server or infrastructure admin | Microsoft SQL Server only |
| Create a service account with read permissions | Database admin | Both connectors |
| Register an app in Microsoft Entra ID and generate a client secret | Microsoft Entra admin | Azure SQL only |
| Add the registered app to the database and grant db_datareader | Database admin | Azure SQL only |
| Add Microsoft 365 client IP ranges to the firewall | Database or network admin | Azure SQL only |

## Install the Microsoft Graph connector agent

This task applies to the Microsoft SQL Server connector only. To access your Microsoft SQL Server, you must install and configure the connector agent. To learn more, see [Install the Microsoft Graph connector agent](connector-agent.md).

> [!NOTE]
> If you use Windows authentication while configuring the Microsoft SQL Server connector, the user that you use to sign in needs to have interactive sign-in rights to the machine where you install the connector agent. For more information, see [login policy management](/windows/security/threat-protection/security-policy-settings/allow-log-on-locally#policy-management).

## Create a service account

To connect to your SQL database and allow the Copilot connector to update records regularly, you need a service account with read permissions granted to the service account.

## Register an app in Microsoft Entra ID

This task applies to the Azure SQL connector only. Register an app in Microsoft Entra ID to allow the Microsoft Search app and Microsoft 365 Copilot to access data for indexing. To learn more about registering an app, see the Microsoft Graph documentation on how to [register an app](/graph/auth-register-app-v2).

After you complete the app registration, note the app name, application (client) ID, and tenant ID, and then [generate a new client secret](/azure/healthcare-apis/register-confidential-azure-ad-client-app#application-secret). The client secret is only displayed once, so note and store it securely. You use the client ID and client secret while configuring a new connection in Microsoft Search and Microsoft 365 Copilot.

To learn more about revoking access to an app registered in Microsoft Entra ID, see [removing a registered app](/azure/active-directory/develop/quickstart-remove-app).

## Add the registered app to your Azure SQL database

This task applies to the Azure SQL connector only. To add the registered app to your Azure SQL database:

1. Sign in to your Azure SQL DB.
1. Open a new query window.
1. Create a new user by running the command `CREATE USER [app name] FROM EXTERNAL PROVIDER`.
1. Add the user to the role by running the command `exec sp_addrolemember 'db_datareader', [app name]` or `ALTER ROLE db_datareader ADD MEMBER [app name]`.

## Configure firewall settings

This task applies to the Azure SQL connector only. For added security, you can configure IP firewall rules for your Azure SQL Server or database. To learn more about setting up IP firewall rules, see the documentation on [IP firewall rules](/azure/azure-sql/database/firewall-configure). Add the following client IP ranges in the firewall settings.

| Region | Microsoft 365 Enterprise | Microsoft 365 Government |
|---|---|---|
| NAM | 52.250.92.252/30, 52.224.250.216/30 | 52.245.230.216/30, 20.141.117.64/30 |
| EUR | 20.54.41.208/30, 51.105.159.88/30 | NA |
| APC | 52.139.188.212/30, 20.43.146.44/30 | NA |

## Next step

> [!div class="nextstepaction"]
> [Deploy the Azure SQL and Microsoft SQL Server connectors](mssql-deployment.md)
