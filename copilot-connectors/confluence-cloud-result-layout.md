--- 

title: "Result Layout for Confluence Cloud Microsoft 365 Copilot connector" 
ms.author: vivg 
author: vivg 
manager: harshkum 
audience: Admin
ms.audience: Admin 
ms.topic: how-to
ms.service: copilot-connectors 
ms.localizationpriority: medium 
description: "Get a JSON example of a Microsoft Search result layout for the Confluence Cloud Microsoft 365 Copilot connector." 
ms.date: 03/08/2023
---

# Result layout for Confluence Cloud Microsoft 365 Copilot connector

The [Confluence Cloud Microsoft 365 Copilot connector](confluence-cloud-overview.md) allows your organization to index Confluence content. After you configure the connector and index data from the Confluence site, users can search for that content in Microsoft Search.

To set up the search result page, you need to:
1. Set up [search vertical](/microsoftsearch/manage-verticals).
2. Set up [search result type](/microsoftsearch/manage-result-types).

This article provides sample result layout JSON required for setting up your result layout for the Confluence Cloud Copilot connector.

## Prerequisites

Configure the Confluence Cloud Copilot connector. To consume the sample result layout JSON as-is, select the following properties for indexing with the mentioned [search schema](deployment-overview.md).

> [!NOTE]
> * **Retrieve** search attribute is required for displaying a property in the search result template. A property can have other search attributes also.  

| Property | Search schema attribute required |
| -------- | -------- |
| Title | Retrieve |
| URL | Retrieve |
| UpdatedByName | Retrieve |
| UpdatedOn | Retrieve |
| Content | Content property |

## Result layout

With this sample, your search results look like the following.

:::image type="content" alt-text="Example of a layout for the Confluence Cloud Copilot connector." source="media/confluence-cloud/confluence-cloud-example-layout.png" lightbox="media/confluence-cloud/confluence-cloud-example-layout.png":::

The following example shows the JSON file associated with the layout.


```json
{
    "type": "AdaptiveCard",
    "version": "1.3",
    "body": [
        {
            "type": "ColumnSet",
            "columns": [
                {
                    "type": "Column",
                    "width": "auto",
                    "items": [
                        {
                            "type": "Image",
                            "url": "https://searchuxcdn.blob.core.windows.net/designerapp/images/DefaultMRTIcon.png",
                            "horizontalAlignment": "center",
                            "size": "small"
                        }
                    ],
                    "horizontalAlignment": "center"
                },
                {
                    "type": "Column",
                    "width": "stretch",
                    "items": [
                        {
                            "type": "ColumnSet",
                            "columns": [
                                {
                                    "type": "Column",
                                    "width": "auto",
                                    "items": [
                                        {
                                            "type": "TextBlock",
                                            "text": "[${Title}](${Url})",
                                            "weight": "bolder",
                                            "size": "medium",
                                            "maxLines": 3,
                                            "color": "accent"
                                        }
                                    ],
                                    "spacing": "none"
                                }
                            ],
                            "spacing": "small"
                        },
                        {
                            "type": "TextBlock",
                            "text": "[${Url}](${Url})",
                            "spacing": "small",
                            "weight": "bolder",
                            "color": "dark"
                        },
                        {
                            "type": "Container",
                            "items": [
                                {
                                    "type": "TextBlock",
                                    "text": "**${UpdatedByName}** modified {{DATE(${UpdatedOn})}}",
                                    "spacing": "small",
                                    "$when": "${UpdatedByName!='' && UpdatedOn!=''}"
                                },
                                {
                                    "type": "TextBlock",
                                    "text": "Modified on {{DATE(${UpdatedOn})}}",
                                    "spacing": "small",
                                    "$when": "${UpdatedByName=='' && UpdatedOn!=''}"
                                },
                                {
                                    "type": "TextBlock",
                                    "text": "Modified by __${UpdatedByName}__",
                                    "spacing": "small",
                                    "$when": "${UpdatedByName!='' && UpdatedOn==''}"
                                }
                            ],
                            "spacing": "small"
                        },
                        {
                            "type": "TextBlock",
                            "text": "${ResultSnippet}",
                            "maxLines": 2,
                            "wrap": true,
                            "spacing": "small"
                        }
                    ],
                    "spacing": "medium"
                }
            ]
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "$data": {
        "UpdatedOn": "2019-09-25T06:08:39Z,SHORT",
        "ResultSnippet": "Marketing team at Contoso.., and looking at the Contoso Marketing documents on the team site. This contains the data from FY20 and will taken over to FY21...Marketing Planning is ongoing for FY20..",
        "UpdatedByName": "Amanda Brady",
        "Url": "https://modernacdesigner.azurewebsites.net",
        "Title": "Contoso Marketing Analysis - Q3 FY18"
    }
}
```

## Related content

- [Customize search result page](/microsoftsearch/customize-search-page)
- [Manage search result layouts](/microsoftsearch/customize-results-layout)
