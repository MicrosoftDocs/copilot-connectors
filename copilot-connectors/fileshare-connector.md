---
ms.date: 02/23/2026
title: "File Share connector"
ms.author: danielabo
author: danielabom
manager: SteveWilkins1123
audience: Admin
ms.audience: Admin
ms.topic: how-to
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Set up the File Share Microsoft 365 Copilot connector"
---
# File Share connector

The File Share Microsoft 365 Copilot connector allows users in your organization to search on premises Windows file shares. After you configure the connector and index data from the file path, end users can search for that content in Microsoft Search and Microsoft 365 Copilot. 
 
## Capabilities

- Ask natural language questions about on-prem files content in Copilot, such as summarizing the document, with enhanced search capabilities. 
- Perform natural language queries for accurate responses using Semantic Search support. 
- Content of the following formats can be indexed and searched: DOC, DOCM, DOCX, DOT, DOTX, EML, GIF, HTML, JPEG, JPG, MHT, MHTML, MSG, NWS, OBD, OBT, ODP, ODS, ODT, ONE, PDF, PNG, POT, PPS, PPT, PPTM, PPTX, TXT, XLB, XLC, XLSB, XLS, XLSX, XLT, XLXM, XML, XPS, and ZIP. Only the textual content of these formats is indexed, and all multimedia content is ignored. For multimedia and other file types, only metadata is indexed. 

## Limitations

- The maximum supported file size is 100 MB. Files that exceed 100 MB aren't indexed. The maximum post-processed size limit is 4 MB. Processing stops when a file's size reaches 4 MB. Therefore, some phrases present in the file might not work for search. 
- You can index up to twenty different file shares in a single connection. Enter one file share per line in the file shares text box area. 

## Prerequisites

### Install the Microsoft Graph connector agent

To index your Windows file shares, you must install and register the connector agent. For more information, see [Install the Microsoft Graph connector agent](connector-agent.md#install-the-agent). Make sure that the data source and agent computers are on the same network to get the best latency and throughput for indexing files.

If you have some old file formats in your data source, such as .msg and .doc, you must install the Microsoft Visual C++ 2012 Redistributable Update 4 (x86 and x64) on the connector agent host to enable ingestion of such files. [Download Visual C++ Redistributable for Visual Studio 2012 Update 4 from Official Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=30679).

## Get Started

### Choose display name

The display name helps users easily recognize the associated file or item in Copilot, signifying trusted content. Display name is also used as a [content source filter](/microsoft-365/copilot/connectors/custom-filters#content-source-filters). A default value is present for this field, but you can customize it to a name that users in your organization recognize. 

### File Share on-premises URL

Enter the path to the file share and select your previously installed Microsoft Graph connector agent. Enter the credentials for a [Microsoft Windows](https://microsoft.com/windows) user account with read access to all the files in the file share.

### Limits for file indexing

You have the ability to limit files and folders from indexing based on file type, modified date, and location.

#### Based on file types

For these file formats, only the text is indexed: DOC, DOCM, DOCX, DOT, DOTX, EML, HTML, MHT, MHTML, MSG, NWS, OBD, OBT, ODP, ODS, ODT, ONE, PDF, POT, PPS, PPT, PPTM, PPTX, TXT, XLB, XLC, XLSB, XLS, XLSX, XLT, XLXM, XML, XPS. For multimedia and other file types, only metadata is indexed.

#### Based on the last modified date or the number of days since the last modification

Use these selections to only index files modified within a specified number of days or since a specific date.

## Full network path or regular expression

In the network path, use the escape character (\\) before special characters like \\. Example: For the path \\\\CONTOSO\\FILE\\SHAREDFOLDER, correct way to input is  \\\\\\\\CONTOSO\\\\FILE\\\\SHAREDFOLDER

For information about writing regular expressions, see [Regular Expression Language Quick Reference](/dotnet/standard/base-types/regular-expression-language-quick-reference).

You also have the ability to create an exception to the limit rule. The priority of the exception rule will supersede limit rules. Exception rules can be defined by entering folder or file paths for the items you want to include in indexing.

:::image type="content" source="media/file-connector/exclusionrule.png" alt-text="Graphic showing a subset of files excluded from indexing with exceptions.":::

## Preserve last access time 

When the connector attempts to crawl a file, the "last access time" field in its metadata is updated. If you depend on that field for archiving and backup solutions and you don't want to update it when the connector accesses it, select this option. 

## Custom setup

You can enrich your indexed data by creating custom properties based on the connector's default properties.

:::image type="content" source="media/file-connector/connectors-custom-property-setup.png" alt-text="Custom property set up with a rule for URL.":::

To add a custom property:

  1. Enter a property name. This name appears in the search results from this connector.
  1. For the value, select **Static or String/Regex Mapping**. A static value is included in all search results from this connector. The string/regex value varies based on the rules you add.
  1. Select **Edit value**.
  1. If you selected a static value, enter the string you want to appear.
  1. If you selected a string/regex value:
      * In the **Add expressions** section, in the **Property** list, select a default property from the list.
      * For **Sample value**, enter a string to represent the type of values that could appear. This sample is used when you preview your rule.
      * For **Expression**, enter a regex expression to define the portion of the property value that should appear in search results. You can add up to three expressions. To learn more about regex expressions, see [Regular expression language quick reference](/dotnet/standard/base-types/regular-expression-language-quick-reference) or search the web for a regex expression reference guide.
      * In the **Create formula** section, enter a formula to combine the values extracted from the expressions. 

## Property labels

Follow the general [setup instructions](./deployment-overview.md).
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## Manage schema

Follow the general [setup instructions](./deployment-overview.md).
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## Manage search permissions

You can restrict the permission to search for any file based on Share Access Control Lists or New Technology File System (NTFS) Access Control Lists, by selecting the desired option on the **Manage search permissions** page. The user accounts and groups provided in the Access Control Lists must be managed by Active Directory (AD). If you're using any other system for user accounts management, you can select the 'everyone' option, which lets users search for all the files without any access restrictions. However, when users try to open the file, access controls set at the source apply.

Windows by default provides 'Read' permission to 'Everyone' in Share ACLs when a folder is shared on the network. By extension, if you're choosing Share ACLs in **Manage search permissions**, users can search for all the files. If you want to restrict access, remove 'Read' access for 'Everyone' in file shares and provide access only to the desired users and groups. The connector then reads these access restrictions and applies them to the search.

You can choose to share ACLs only if the share path you provided follows UNC path format. You can create a path in UNC format by going to 'Advanced Sharing' under the 'Sharing' option.

:::image type="content" source="media/file-connector/file-advanced-sharing.png" alt-text="Screenshot of the Advanced settings dialog box.":::

## Synchronization

The refresh interval determines how often your data is synchronized between the data source and the Copilot connector index. There are two types of refresh intervals – full crawl and incremental crawl. For more details, click [here](/microsoft-365/copilot/connectors/deployment-overview#guidelines-for-crawl-settings). You can change the default values of the refresh interval from here if you want to. 

## Review and test your connection

- Follow the general [setup instructions](./deployment-overview.md).
- Search and validate your indexed content and permissions using [Index browser](indexed-content.md).
- Find answers to common questions in the [FAQ](/microsoft-365/copilot/connectors/frequently-asked-questions).

For Microsoft Search, if you need to customize the search results page. To learn about customizing search results, see [Customize the search results page](/microsoft-365/copilot/connectors/deployment-overview#step-11-customize-the-search-results-page).

## Troubleshooting
After publishing your connection, you can review the status in the **Connectors** section of the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

You can find troubleshooting steps for commonly seen issues [here](troubleshoot-file-share-connector.md).

If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).

