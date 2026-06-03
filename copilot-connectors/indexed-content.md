---
ms.date: 02/09/2026
title: "Search and validate indexed connector content"
ms.author: danielabo
author: danielabom
manager: calvind
audience: Admin
ms.topic: article
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Learn how to search and validate whether Microsoft 365 Copilot connector content is indexed in Microsoft Search and Microsoft 365 Copilot."
---

# Search and validate indexed content

When you test a Microsoft 365 Copilot connection, use the index browser to verify connector content indexing. To verify properties and user access, review the metadata and access control lists (ACLs) of indexed items. This review also helps troubleshoot search problems. If users report problems accessing items, you can check whether the item was indexed correctly and includes the correct data.

:::image type="content" source="media/manage-connector/index-search.png" alt-text="Screenshot that shows what users can see when they enter an item ID of an indexed item.":::

## Index browser

When you enter an item ID to check its index status, you can view the following details if the item is indexed:

- Name of the Content - The name of the indexed item.
- Status - The current status of the item and its last refresh time.
- Properties - Indicates the status of all properties defined during configuration for the item.
- Permissions - Lists all groups and individual users associated with the item. If the status is **allow**, all users in those groups can view the item. If the status is **deny**, users in those groups can't access the item. If access permissions are configured as **Allow everyone** instead of **Only people with access** for the connection, all items in the index are visible to everyone, and no specific permissions are enforced.
- Check user access - Allows searching for a specific user to verify their access to the item. Enter the user name or email address to display a list of groups to which the user belongs. If the user is denied access to any of these groups, their overall permission to view the item is revoked.

>[!NOTE]
>- In permissions, you can see users shown individually (outside of a group) in the data source and groups within the data source. To check for a user present in a group, use **Check user access**. 
>- If a user doesn't appear in **Check user access**, it might be due to a failed user mapping or the user not being discovered (for example, the Microsoft Entra ID user ID wasn't found). To resolve this, verify that the user has access in the data source and review the user mapping formula and the error reports.

To search for indexed content, enter the unique identifier of the item in the index browser. 

|Connector name|Input per item ID|Where to find the item ID|
|:---|:---|:---|
|ADO WI|ID|Use the work item ID.|	
|ADO Wiki|Organization name, page ID|Found in the URL. For example, in this URL: `https://dev.azure.com/IdentityDivision/DevEx/_wiki/wikis/DevEx.wiki/74398/Passkey-FAQ`, the organization name is `IdentityDivision`, and the page ID is 74398.|
|ServiceNow KB|Sys_Id of the knowledge article<br><br>Article number<br><br>Sys ID of the knowledge base| For the Sys_id of the article, go to the record, right-click the header bar, and select **Copy sys_id**. You can also select the **menu (three-line)** button > **Copy sys_id**.<br><br>For article number, copy the KB number of the article; for example, `KB0123456`.<br><br>For the sys_id of the knowledge base, go to the knowledge base that contains the article, right-click the header bar, and select **Copy sys_id**. You can also select the **menu (three-line)** button > **Copy sys_id**.<br><br>For more information, see [ServiceNow documentation](https://docs.servicenow.com/csh?topicname=c_UniqueRecordIdentifier.html&version=latest).|
|ServiceNow Catalog|Sys_Id.value|Go to the record, right-click the header bar, and select Copy sys_id. You can also select the **menu (three-line)** button > **Copy sys_id**. For more information, see [ServiceNow documentation](https://docs.servicenow.com/csh?topicname=c_UniqueRecordIdentifier.html&version=latest).|
|ServiceNow Tickets|Sys_Id.value|Go to the record, right-click the header bar, and select **Copy sys_id**. You can also select the **menu (three-line)** button > **Copy sys_id**. For more information, see [ServiceNow documentation](https://docs.servicenow.com/csh?topicname=c_UniqueRecordIdentifier.html&version=latest).|
|Salesforce|ID|Found in the URL.|
|Intranet (Cloud/OnPrem)|URL|Final URL, all lowercase.| 
|Jira| Issue ID| For information, see [How to get issue id from the Jira User Interface](https://confluence.atlassian.com/jirakb/how-to-get-issue-id-from-the-jira-user-interface-1115156394.html#:~:text=User%20needs%20to%20get%20the%20issue%20id%20in%20an%20easier).|
|Confluence (Cloud/OnPrem)|Page blog post ID|Found in the item ID of the URL. Examples can be found in the Confluence Cloud URL from the data source.|
|PagerDuty Incidents|Incident ID|Found in the incident URL. For example, in this URL: `https://contoso.pagerduty.com/incidents/Q2E4AJBLCXV8CS`, the incident ID is `Q2E4AJBLCXV8CS`.|
|PagerDuty Escalation Policies|Policy ID|Found in the escalation policy URL. For example, in this URL: `https://contoso.pagerduty.com/escalation_policies/P1H1CV3`, the policy ID is `P1H1CV3`.|
|PagerDuty Schedules|Schedule ID|Found in the schedule URL. For example, in this URL: `https://contoso.pagerduty.com/schedules/P25H5CH`, the schedule ID is `P25H5CH`.|
|CSV|Unique identifier list, item key|Admin configured details.|
|Azure SQL, Oracle DB, MS SQL|Values to all the columns in unique key columns|Admin configured details.|
|Mediawiki|Page ID, namespace, sourceUrl|Admin configured details.|
|ADLS gen 2|File URI|Admin configured details.|
|Sharepoint|GUID|Admin configured details.|
|FileShare|Filepath|Admin configured details.|
|Custom connector|Item ID|Admin configured details.|
|SAP|user ID|Admin configured details.|
|BambooHR|Employee ID (EeId) |Go to the user profile in BambooHR. The Employee ID (EeId) is found in the URL. For example, in this URL: `https://contoso.bamboohr.com/employees/employee.php?id=4&page=2078`), the Employee ID (EeId) is `4`.|

## Examples
### Item status is partially indexed

An item status of **Partially indexed** indicates that the item is missing some information, such as properties, user details, or content, but remains searchable in Microsoft Search and Microsoft 365 Copilot. To ensure the item is complete, review the **Errors** tab for any errors.

### Item status is deny all

An item status of **Deny all** indicates that the item is indexed but remains inaccessible to all users, as shown by an empty response in the permissions tab. Although the item is present in the index, users can't view it.

For ServiceNow Knowledge connectors, the **Deny all** status might occur for the following reasons:

- **Advanced user criteria applied on knowledge article and simple flow used during connection setup instead of advanced flow** - If the connection is configured with simple flow and advanced user criteria is applied to knowledge articles in the **Cannot read** section, the item status might be **Deny all**. Try removing the advanced criteria and triggering a full crawl, or complete the connection setup using the [advanced flow method](servicenow-knowledge-admin-setup.md#set-up-rest-api). 

- **Advanced user criteria applied on knowledge base and simple flow used during connection setup instead of advanced flow** - If the connection  is configured with simple flow and advanced user criteria is applied on a knowledge base in the **Cannot read** or **Cannot contribute** section, the item status might be **Deny all** for the articles within that knowledge base. Identify the knowledge base the article belongs to and remove the advanced criteria, or complete the connection setup using the [advanced flow method](servicenow-knowledge-admin-setup.md#set-up-rest-api). 

Temporary issues might also cause a **Deny all** status that is resolved during the next full crawl.

### Item status is allowed for everyone

When an item is configured to be visible to everyone, it's accessible to all users within the organization, regardless of the permissions set in the data source.

If an item is discovered but not indexed, check the **Errors** tab for any issues that prevented the indexing process.

>[!NOTE]
>- Changes to user or group permissions (ACLs) might take up to 24 hours to reflect in Microsoft Search and Microsoft 365 Copilot.
>- Permissions updates occur during a full crawl, not an incremental crawl.
>- If your data source permissions change after the last full crawl, you must trigger a new full crawl on-demand or schedule it to update the index.
>- When testing in Microsoft Search or Microsoft 365 Copilot, make sure that you're searching with a searchable or queryable property. For more information, see [Manage schema](/microsoftsearch/manage-search-schema). 

## Related content

- [Deploy Microsoft 365 Copilot connectors](deployment-overview.md)
