---
title: "Microsoft Graph connector agent overview" 
ms.author: kam1 
author: kam1 
manager: jameslau 
audience: Admin
ms.audience: Admin 
ms.topic: install-set-up-deploy
ms.service: copilot-connectors 
ms.localizationpriority: medium 
description: "Find the steps to install the Microsoft Graph connector agent to allow you to index on-premises content via Microsoft 365 Copilot connectors." 
ms.date: 05/11/2026
---

# Microsoft Graph connector agent

To use on-premises Microsoft 365 Copilot connectors, you must install the Microsoft Graph connector agent. The agent allows for secure data transfer between on-premises data and the Copilot connector APIs. This article describes how to install and configure the Microsoft Graph connector agent.

## Install the agent

[Download](https://aka.ms/gca) the latest version of the Microsoft Graph connector agent and install use the installation configuration assistant to install it. For information about the latest connector agent release, see the [Connector agent release notes](connector-agent-releases.md).

>[!NOTE]
>We recommend that you always use the latest version of the connector agent to ensure feature completeness.

### Check execution policy

The execution policy has to be set to allow remote signed scripts to run. If any computer or group-level policy restricts remote signed scripts, the installation fails. Run the following command to get the execution policy:

```powershell
Get-ExecutionPolicy -List
```

For more information, see [Execution policy](/powershell/module/microsoft.powershell.core/about/about_execution_policies).

### Prerequisites

Before you install the agent, make sure that you have the required role-based access control (RBAC) roles for each step.

|Step|RBAC role|
|:---|:---|
|Install agent on-premises| AI administrator, Copilot admin.|
|Register the app in Entra ID| Azure App admin, Azure admin.|
|Create the service account on the target servers|See the deployment guide for the connector.|

> [!NOTE]
> If you're installing the connector agent on a server in a Government Community Cloud (GCCH) and DoD environment, after you install the agent, make the following change:
> - In the `C:\Program Files\Graph connector agent\ConfigApp\appsettings.json` file, in the `CloudInstanceUrl` attribute, update the URL value to be `https://login.microsoftonline.us`.

### Recommended configuration

When you use the recommended configuration, the connector agent instance can handle up to three connections. Any connections beyond that might degrade the performance of all connections on the agent. The following configuration is recommended:

* Windows 10, Windows Server 2016 R2, and higher versions
* [.NET Framework 4.7.2](https://dotnet.microsoft.com/en-us/download/dotnet-framework/net472)
* [.NET Core Desktop Runtime 8.0 (x64)](https://dotnet.microsoft.com/download/dotnet/8.0)
* 8 cores, 3 GHz
* 16-GB RAM
* 40-GB Disk space for 5M items and 9GB/Million items after 5M items
* Network access to the data source and internet through 443

If your organization's proxy servers or firewalls block communication to unknown domains, add the following rules to the allow list.

| **Microsoft 365 Enterprise** | **Microsoft 365 GCC** | **Microsoft365 GCCH** |
| ------------- | -------------| -------------|
| 1. `*.servicebus.windows.net` | 1. `*.servicebus.usgovcloudapi.net` | 1. `*.servicebus.usgovcloudapi.net`
| 2. `*.events.data.microsoft.com` | 2. `*.events.data.microsoft.com` | 2. `*.events.data.microsoft.com`
| 3. `*.office.com` | 3. `*.office.com` | 3. `*.office.com`, `*.office365.us`
| 4. `https://login.microsoftonline.com` | 4. `https://login.microsoftonline.com` | 4. `https://login.microsoftonline.com`, `https://login.microsoftonline.us`
| 5. `https://gcs.office.com/` | 5. `https://gcsgcc.office.com` | 5. `https://gcs.office365.us/`
| 6. `https://graph.microsoft.com/` | 6. `https://graph.microsoft.com` | 6. `https://graph.microsoft.com/`, `https://graph.microsoft.us/`

>[!NOTE]
>Proxy authentication isn't supported. If your environment has a proxy that requires authentication, we recommend that you allow the connector agent to bypass the proxy.

>[!NOTE]
>In case of interactive Entra ID sign-in dependencies, go over [link](https://learn.microsoft.com/en-us/microsoft-365/enterprise/urls-and-ip-address-ranges?view=o365-worldwide) to whitelist sign in urls

If your organization uses an outbound proxy, the agent's crawl requests to your data source also route through that proxy by default, which can cause crawl failures. Configure proxy bypass for your data source hostnames by using whichever method matches your proxy setup:

- `NO_PROXY` system environment variable
- Windows system proxy bypass settings
- Your PAC file

For example, if you use `HTTP_PROXY`/`HTTPS_PROXY` environment variables, set `NO_PROXY=sharepoint.contoso.com`. If `NO_PROXY` already exists, add your hostnames to it. After you change system environment variables, restart the **GcaHostService** Windows service.

## Upgrade the agent

To upgrade the agent to the latest version:

1. [Download](https://aka.ms/gca) and install the Microsoft Graph connector agent.

1. On the connection pane, choose **Upgrade**.

   :::image type="content" source="media/connector-agent/one-click-upgrade.png" alt-text="Upgrade button on the agent connection pane." lightbox="media/connector-agent/one-click-upgrade.png":::

If you're upgrading the agent from version 1.x to version 2.x: 

1. [Download](https://aka.ms/gca) the installer.

1. The installer prompts you to install .NET 8 Desktop runtime, if it isn't already installed.

1. Allow communication to the endpoint *.office.com.

1. The configuration app restarts. If the agent isn't registered, sign in and proceed with the registration.

1. If the agent is already registered, the configuration app shows the following success message.

   :::image type="content" source="media/connector-agent/health-check-sign-in.jpg" alt-text="Health check success on connector agent sign-in page." lightbox="media/connector-agent/health-check-sign-in.jpg":::

1. If any errors occur, follow the suggested mitigation steps in the error message and close and reopen the configuration app.

1. If the error message says, "Can't determine the health of the agent. If the error persists, contact support, restart GcaHostService, and open the configuration app again.

1. You can run the checks anytime by closing and opening the GCA Config app or by using the "Health Check" button next to the "Edit" button in the registration details screen.

   :::image type="content" source="media/connector-agent/health-check-registration.jpg" alt-text="Health check success on the connector registration page." lightbox="media/connector-agent/health-check-registration.jpg":::

>[!NOTE]
>If you uninstall and reinstall the Microsoft Graph connector agent, you must restart all existing connections. After you reinstall the agent, delete your connections and create new ones.

## Create and configure an app for the agent  

First, sign in and note that the minimum required privilege on the account is AI administrator. The agent asks you to provide authentication details.

To create an app and generate the required authentication details:

1. Go to the [Azure portal](https://portal.azure.com) and sign in with admin credentials for the tenant.

2. Go to **Microsoft Entra ID** > **App registrations** and select **New registration**.

3. Provide a name for the app and select **Register**.

4. Make a note of the application (client) ID.

5. Open **API permissions** and select **Add a permission**.

6. Select **Microsoft Graph** and then **Application permissions**.

7. Search for the following permissions and select **Add permissions**.

   | **Permission** | **When is the permission required** |
   | ------------- | -------------|
   | [ExternalItem.ReadWrite.OwnedBy](/graph/permissions-reference#application-permissions-52) or [ExternalItem.ReadWrite.All](/graph/permissions-reference#application-permissions-52) | Always |
   | [ExternalConnection.ReadWrite.OwnedBy](/graph/permissions-reference#application-permissions-58) | Always |
   | [Directory.Read.All](/graph/permissions-reference#application-permissions-23) | Required for Confluence DC, GitHub server, File share, MS SQL, and Oracle SQL connectors |

8. Select **Grant admin consent for [TenantName]** and select **Yes**.

9. Verify that the permissions status is **Granted**.

    :::image type="content" alt-text="Configured permissions with a status of Granted." source="media/connector-agent/granted-state.png" lightbox="media/connector-agent/granted-state.png":::

### Configure authentication

You can provide authentication details using a client secret or a certificate. 

#### Configure the client secret for authentication

1. Go to the [Azure portal](https://portal.azure.com) and sign in with admin credentials for the tenant.

2. Open **App registration** and go to the appropriate app. Under **Manage**, select **Certificates and secrets**.

3. Select **New Client secret** and select an expiry period for the secret. Copy and save the generated secret.

4. Use the client secret and the application ID to configure the agent. Alphanumeric characters are accepted. You can't use blank spaces in the **Name** field of the agent.

#### Use a certificate for authentication

To use certificate-based authentication:

1. Create or obtain a certificate.
2. Upload the certificate to the Azure portal.
3. Assign the certificate to the agent.

##### Get a certificate

You can use the following script to generate a self-signed certificate. If your organization doesn't allow self-signed certificates, acquire a certificate according to your organization's policies.

```powershell
$dnsName = "<TenantDomain like agent.onmicrosoft.com>" # Your DNS name
$password = "<password>" # Certificate password
$folderPath = "D:\New folder\" # Where do you want the files to get saved to? The folder needs to exist.
$fileName = "agentcert" # What do you want to call the cert files? without the file extension
$yearsValid = 10 # Number of years until you need to renew the certificate
$certStoreLocation = "cert:\LocalMachine\My"
$expirationDate = (Get-Date).AddYears($yearsValid)
$certificate = New-SelfSignedCertificate -DnsName $dnsName -CertStoreLocation $certStoreLocation -NotAfter $expirationDate -KeyExportPolicy Exportable -KeySpec Signature -KeyLength 2048 -KeyAlgorithm RSA -HashAlgorithm SHA256
$certificatePath = $certStoreLocation + '\' + $certificate.Thumbprint
$filePath = $folderPath + '\' + $fileName
$securePassword = ConvertTo-SecureString -String $password -Force -AsPlainText
Export-Certificate -Cert $certificatePath -FilePath ($filePath + '.cer')
Export-PfxCertificate -Cert $certificatePath -FilePath ($filePath + '.pfx') -Password $securePassword
```

##### Upload the certificate to the Azure portal

1. Open the application and go to **Certificates and secrets**.
2. Select **Upload certificate** and upload the .cer file.
3. Open **App registration** and select **Certificates and secrets**. Copy the certificate thumbprint.

    :::image type="content" alt-text="List of thumbprint certificates when Certificates and secrets are selected in the left pane." source="media/connector-agent/certificates.png" lightbox="media/connector-agent/certificates.png":::

##### Assign the certificate to the agent

If you use the script to generate a certificate, the .pfx file is saved in the location identified in the script.

1. Download the certificate .pfx file to the agent computer.

2. Select the .pfx file to launch the certificate installation dialog box.

3. Select **Local machine** for the store location.

4. After the certificate is installed, open **Manage computer certificates** from the **Start** menu.

5. Select the installed certificate from **Personal** > **Certificates**.

6. Select and hold (or right-click) on the certificate and select **All tasks** > **Manage private keys**.

7. In the permissions dialog box, select **Add**. It pops up a new window. Select **Locations**. Select the computer on which the agent is installed and select **Ok**.

8. In the user selection dialog box, input **NT Service\GcaHostService** and select **OK**. Don't select **Check Names**.

9. Select **OK** on the permissions dialog box. The agent computer is now configured for the agent to generate tokens using the certificate.

## Troubleshooting the connector agent

### Installation failure

If an installation failure occurs, check the installation logs by running: `msiexec /i "< path to msi >\GcaInstaller.msi" /L*V "< destination path >\install.log"`. Make sure you don't get any security exceptions. Generally, these exceptions occur due to wrong policy settings. The execution policy needs to be remotely signed. 

If the errors aren't resolvable, contact Microsoft Support with the error logs.

### Registration failure

If signing in to configure the application fails and shows the error **Sign-in failed, please select the sign-in button to try again** after browser authentication succeeds, open services.msc, and verify that GcaHostService is running. If it doesn't start, start it manually. In the Task Manager, go to **Services**, select and hold (right-click) GcaHostService and start the service.

When the service fails to start with the error **The service didn't start due to a logon failure**, check whether the virtual account `NT Service\GcaHostService` has permission to sign in as a service on the machine. For more information, see [Log on as a service](/windows/security/threat-protection/security-policy-settings/log-on-as-a-service). If the option to add a user or group is grayed out in the Local Policies\User Rights Assignment, the user adding this account doesn't have admin privileges, or a group policy overrides it. The group policy must be updated to allow the host service to sign in as a service.

### Agent is offline

The agent is considered offline if it isn't able to contact the Copilot connector services. To troubleshoot:

1. Check whether the agent is running. In the Task Manager, go to **Services**, and verify that the **GcaHostService** is in a running state. If not, select and hold (right-click) the service and start it. 

    :::image type="content" alt-text="Screenshot of the connector service in Task Manager." source="media/connector-agent/gcahostservice-gcaupdateservice.png" lightbox="media/connector-agent/gcahostservice-gcaupdateservice.png":::
   
2. Verify that the domain gcs.office.com is reachable. (For a GCC tenant, substitute gcsgcc.office.com, and for a GCCHigh tenant, substitute gcs.office365.us.)

* From PowerShell, run the following command:

    ```powershell
    tnc gcs.office.com -Port 443
    ```

    The response should contain the output `TcpTestSucceeded: True`.

    :::image type="content" alt-text="Screenshot showing that Tcp test succeeded." source="media/connector-agent/tnc-gcs-1.png" lightbox="media/connector-agent/tnc-gcs-1.png":::
   
    If it's false, verify that the domain is allowed in your proxy/firewall and that requests are going through the proxy.

   * For a more specific test, or if you can't run tnc because ICMP ping is blocked in your network, run the following command:

    ```powershell
    wget https://gcs.office.com/v1.0/admin/AdminDataSetCrawl/healthcheck
    ```

       The output should contain  `StatusCode: 200`.
 
       If it isn't 200, verify that the domain is allowed in your proxy/firewall and that requests are going through the proxy.

3. If the steps passed successfully and the agent is still offline, check the agent logs for any network proxy issues.
    * GcaHostService logs are found in the following locations:
        1. For Windows Server 2016: `C:\Users\GcaHostService\AppData\Local\Microsoft\GraphConnectorAgent\HostService\logs`
        2. For all other supported Windows versions: `C:\Windows\ServiceProfiles\GcaHostService\AppData\Local\Microsoft\GraphConnectorAgent\HostService\logs`
    * Sort the log files in the folder in reverse order of **Modified Time** and open the latest two files.
    * Check for any error messages with the following text: **No connection could be made because the target machine actively refused it.**
        1. Indicates that there's an issue with the network settings that prevent the GcaHostService virtual account from contacting the `https://gcs.office.com` endpoint.
        2. Check with your network/proxy team to allow the virtual account (NT Service\GcaHostService) to send traffic to this domain.
        3. The issue is resolved when the log file no longer contains these errors.

4. If none of the steps fix your issue, contact Microsoft Support and provide the two latest log files.

### Agent is unreachable

If the agent is unreachable when you set up a connection, the following error screen appears.

:::image type="content" alt-text="Screenshot of the agent unreachable screen." source="media/connector-agent/agentunreachableerror-adminux.png" lightbox="media/connector-agent/agentunreachableerror-adminux.png":::

Use the service bus namespace provided in the error details to troubleshoot:

1. From PowerShell, run the following command:

    ```powershell
    tnc `<yournamespacename>.servicebus.windows.net` -port 443
    ```

      The response should contain the output `TcpTestSucceeded: True:`

    :::image type="content" alt-text="Screenshot of tnc 2." source="media/connector-agent/tnc-gcs-namespace.png" lightbox="media/connector-agent/tnc-gcs-namespace.png":::   
   
      If it's false, verify that the domain is allowed in your proxy/firewall and that requests are going through the proxy.

1. If you can't run tnc because ICMP Ping is blocked in your network, run the following command in PowerShell:

    ```powershell
    wget https://`<yournamespacename>`.servicebus.windows.net/
    ```

      The output should contain `StatusCode: 200`:

    :::image type="content" alt-text="Screenshot of wget 2." source="media/connector-agent/wget-gcs-namespace.png" lightbox="media/connector-agent/wget-gcs-namespace.png"::: 
   
      If it's false, verify that the domain is allowed in your proxy/firewall and that requests are going through the proxy.

1. If none of the steps fix your issue, contact Microsoft Support and provide the two latest log files.

#### Update in progress

This error occurs when an update is already in progress and should resolve after a maximum of 30 minutes.

:::image type="content" alt-text="Screenshot of connector agent update in progress." source="media/connector-agent/agentupgradingerror-adminux.png" lightbox="media/connector-agent/agentupgradingerror-adminux.png"::: 

If the error persists after 30 minutes, follow these steps:

1. Sign in to the computer where the agent is installed and verify that it's running. In Task Manager, go to **Services**, and check whether GcaHostService is in a running state. If not, select and hold (right-click) and start the service.

    :::image type="content" alt-text="Screenshot of the connector service in Task Manager." source="media/connector-agent/gcahostservice-gcaupdateservice.png" lightbox="media/connector-agent/gcahostservice-gcaupdateservice.png":::

1. If the issue persists, contact Microsoft Support and provide the two latest log files. You can find the log files in `C:\Windows\System32\config\systemprofile\AppData\Local\Microsoft\GraphConnectorAgent\AgentUpdateApp\logs+`.

### Connection failure

If the `Test connection` action fails when you create a connection with the error **Please check username/password and the data source path** and the username and password you provided are correct, make sure that the user account has interactive sign-in rights to the computer where the connector agent is installed. For details, see [logon policy management](/windows/security/threat-protection/security-policy-settings/allow-log-on-locally#policy-management). Also, make sure that the data source and the agent computer are on the same network.

## Related content

- [Connector agent release notes](connector-agent-releases.md)
