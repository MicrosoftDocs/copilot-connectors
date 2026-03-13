--- 
title: "Result layout for the Azure DevOps Wiki Microsoft 365 Copilot connector" 

ms.author: vivg 
author: vivg 
manager: harshkum 
audience: Admin
ms.audience: Admin 
ms.topic: how-to
ms.service: copilot-connectors 
ms.localizationpriority: medium 
description: "Result layout JSON for Azure DevOps Wiki Microsoft 365 Copilot connector" 
ms.date: 06/03/2022
---

# Result layout for Azure DevOps Wiki Microsoft 365 Copilot connector

The [Azure DevOps Wiki Microsoft 365 Copilot connector](azure-devops-wiki-connector.md) allows your organization to index wikis from the Azure DevOps service. After you configure the connector and index content, you need to set up a search result page.

To set up the search result page, you need to:
1. Set up [search vertical](/microsoft-365-copilot/connectors/manage-verticals).
2. Set up [search result type](/microsoft-365-copilot/connectors/manage-result-types).

This article provides a result layout JSON example to set up your result layout for the Azure DevOps Wiki Copilot connector.

## Before you get started

You must have configured the Azure DevOps Wiki Copilot connector. To consume the sample result layout JSON, you must select the following properties for indexing.

> [!NOTE]
> The **Retrieve** search attribute is required for displaying a property in the search result template. A property can have other search attributes also.  

| Property | Search schema attribute required |
| -------- | -------- |
| Title | Retrieve |
| RemoteURL | Retrieve |
| LastPublishedAuthorName | Retrieve |
| LastPublishedDate | Retrieve |
| Content | Content property |
| Organization | Retrieve |
| Project | Retrieve |
| WikiIdentifier | Retrieve |

## Result layout

The following example shows what search results look like.

:::image type="content" source="media/ado-wiki/azure-devops-wiki-connector-example-layout.png" alt-text="Example of a layout for Azure DevOps Wiki Copilot connector." lightbox="media/ado-wiki/azure-devops-wiki-connector-example-layout.png"::: 

The following is the associated JSON file.


```json
{
    "type": "AdaptiveCard",
    "version": "1.0",
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
                            "url": "https://searchuxcdn.blob.core.windows.net/designerapp/images/AzureDevOpsLogo.png",
                            "horizontalAlignment": "Center",
                            "altText": "Not available",
                            "width": "-1px",
                            "size": "Small"
                        }
                    ]
                },
                {
                    "type": "Column",
                    "width": 8,
                    "items": [
                        {
                            "type": "TextBlock",
                            "text": "[${Title}](${RemoteURL})",
                            "color": "Accent",
                            "size": "Medium",
                            "weight": "Bolder"
                        },
                        {
                            "type": "TextBlock",
                            "text": "__${LastPublishedAuthorName}__ modified on {{DATE(${LastPublishedDate})}}",
                            "spacing": "Small"
                        },
                        {
                            "type": "ColumnSet",
                            "columns": [
                                {
                                    "type": "Column",
                                    "width": "stretch",
                                    "items": [
                                        {
                                            "type": "TextBlock",
                                            "text": "__Organization:__ ${Organization}"
                                        }
                                    ]
                                },
                                {
                                    "type": "Column",
                                    "width": "stretch",
                                    "items": [
                                        {
                                            "type": "TextBlock",
                                            "text": "__Project:__ ${Project}"
                                        }
                                    ]
                                },
                                {
                                    "type": "Column",
                                    "width": "stretch",
                                    "items": [
                                        {
                                            "type": "TextBlock",
                                            "text": "__Wiki:__ ${WikiIdentifier}"
                                        }
                                    ]
                                }
                            ]
                        },
                        {
                            "type": "TextBlock",
                            "text": "${ResultSnippet}",
                            "wrap": true,
                            "maxLines": 3,
                            "spacing": "Medium"
                        }
                    ],
                    "horizontalAlignment": "Center",
                    "spacing": "Medium"
                }
            ]
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "$data": {
    }
}

```
## Related content

- [Customize search verticles](/microsoft-365-copilot/connectors/manage-verticals)
- [Manage search result layouts](/microsoft-365-copilot/connectors/customize-results-layout)
