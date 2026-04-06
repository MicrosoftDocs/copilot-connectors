# Deploy the Credly Microsoft 365 Copilot connector

This article walks Microsoft 365 administrators through the prerequisites and step-by-step setup of the Credly Microsoft 365 Copilot connector in the Microsoft 365 admin center.

## Prerequisites

- An active Microsoft 365 tenant with [Microsoft 365 Copilot](https://learn.microsoft.com/en-us/microsoft-365/copilot/overview) enabled (for the preview). You must be a Global Administrator or Copilot Administrator in the tenant to create and manage people data connectors.
- A Credly account with administrative rights for your organization. You need to use the Credly Developers portal to create API credentials for the connector. In the Credly portal, navigate to **Developers** and locate your **Organization ID** (a GUID that uniquely identifies your organization on Credly). Then, under **OAuth Applications**, create a new application (for example, named "Microsoft 365 Copilot Connector") to generate a **Client ID** and **Client Secret** for Microsoft 365 to use. Copy and save the Client Secret when it's shown, because Credly won't display that secret again after creation.
- The appropriate base URL for the Credly API in your environment. For most organizations, this is the production API endpoint (for example, `https://www.credly.com` for API calls to `api.credly.com`), unless you have a sandbox environment.

## Add the connector

To add the Credly Microsoft 365 Copilot connector, complete the following steps in the Microsoft 365 admin center:

1. In the Microsoft 365 admin center, go to **Setup** > **Connectors**, select **Add connector**, and choose **Credly** from the **Human Resources & Recruiting** category. Enter a descriptive display name (for example, "Credly Profiles" or "Credly Badges") so users can recognize this source in Copilot citations and search results.
1. Enter your **Credly Organization ID** (the GUID obtained from the Credly Developers portal) when prompted. The connector uses this ID to target the correct Credly organization account. The Organization ID must be in the proper GUID format.
1. Select **OAuth 2.0 Client Credentials** as the authentication method. No interactive user sign-in is required; the connector uses the client credentials to access Credly programmatically.
1. Provide the base URL for the Credly OAuth 2.0 token service. For a production Credly account, use `https://www.credly.com` as the authorization endpoint (the default value).
1. Input the **Client ID** and **Client Secret** that you obtained from the Credly Developers portal. After entering these credentials, finish the connection setup. The admin center establishes the connection and initiates the first data sync.

## Default settings

Once the connector is added through Quick setup, it uses preconfigured defaults optimal for Credly data:

- **Access permissions** &mdash; All profiles and badges ingested are visible to everyone in the organization.
- **Identity mappings** &mdash; Automatically managed by matching Credly user emails to Microsoft Entra ID accounts.
- **Content schema** &mdash; Fixed. All Credly badge fields are mapped to the built-in Awards or Certifications profile properties.
- **Sync schedule** &mdash; Incremental crawl every day and a full crawl once weekly to retrieve new or updated data from Credly. These values can be adjusted if needed, but the default timing is appropriate for most organizations.

## Custom setup

After adding the connector, you can switch to **Custom setup** to modify configuration details. In this preview release, the custom settings are largely fixed, but you can review the following tabs:

- **Users** &mdash; Access permissions are set to *Everyone* (all indexed badge data is broadly accessible in the tenant) and identity mapping is based on user email addresses mapped to Microsoft Entra ID. No additional user scoping options are available in this preview.
- **Content** &mdash; The connector doesn't support adding or removing properties from the schema. It automatically selects a set of badge fields to ingest and maps them to the corresponding Awards/Certifications profile properties in Microsoft 365.
- **Sync** &mdash; The default crawl frequencies are an incremental sync every 15 minutes and a full sync once per day. You can adjust the interval of either crawl type to meet your organization's needs. In most cases, the default schedule is recommended to keep data fresh without unnecessary load.

## Next steps

After publishing the Credly connection, monitor its status and ingestion results on the **Connectors** page in the Microsoft 365 admin center. From there, you can edit the connection or delete it if needed.

## Related content

- [Credly connector overview](credly-connector-overview.md)
- [Troubleshoot the Credly connector](credly-connector-troubleshoot.md)
- [Set up prebuilt Microsoft 365 Copilot connectors in the Microsoft 365 admin center](https://learn.microsoft.com/en-us/microsoftsearch/configure-connector?source=recommendations)
- [Monitor Microsoft 365 Copilot connectors](https://learn.microsoft.com/en-us/microsoftsearch/manage-connector?source=recommendations)
