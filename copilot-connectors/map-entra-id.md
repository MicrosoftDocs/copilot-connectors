---
title: "Map your Microsoft Entra identities" 
ms.author: misvenso 
author: monaray97 
manager: jameslau 
ms.audience: Admin 
ms.topic: how-to
ms.service: copilot-connectors 
ms.localizationpriority: medium 
description: "Find information about how to map users to Microsoft Entra IDs when you customize Microsoft 365 Copilot connectors in the admin center." 
ms.date: 11/05/2020
---

# Map your Microsoft Entra identities  

This article describes how to map your Microsoft Entra identities to a unique identifier for your data source (non-Microsoft Entra identity) so that people in your access control list (ACL) with non-Entra ID identities can see connector results scoped to them.

These steps are relevant for administrators who [Customize connector settings](/microsoft-365-copilot/connectors/deployment-overview#customize-connector-settings-optional) when they deploy Microsoft-built connectors by choosing **Only people with access to this data source** and map identities to user principal names in Entra ID.

## elect Microsoft Entra user properties to map

You can select the Microsoft Entra properties you need to map to the Federation ID.

You can select a Microsoft Entra user property from the dropdown. You can also add as many Microsoft Entra user properties as you would like if these properties are necessary to create the Federation ID mapping for your organization.

## Create formula to complete mapping

You can combine the values of the Microsoft Entra user properties to form the unique Federation ID.

In the formula box, "{0}" corresponds to the *first* Microsoft Entra property you selected. "{1}" corresponds to the *second* Microsoft Entra property you selected. "{2}" corresponds to the *third* Microsoft Entra property, and so on.  

Below are some examples of formulas with sample regular expression outputs and formula outputs:

| Sample formula                  | Value of property {0} for a sample user                 | Value of property {1} for a sample user           | Output of formula                  |
| :------------------- | :------------------- |:---------------|:---------------|
| {0}.{1}@contoso.com  | firstname | lastname |firstname.lastname@contoso.com
| {0}@domain.com                 | userid                 |             |userid@domain.com

After you provide your formula, you can optionally click **Preview** to see a preview of 5 random users from your data source with their respective user mappings applied. The output of the preview includes the value of the Microsoft Entra user properties selected in step 1 for those users and the output of the final formula provided in step 2 for that user. It also indicates whether the output of the formula could be resolved to a Microsoft Entra user in your tenant via a **Success** or **Failed** icon.  

>[!NOTE]
>You can still proceed with creating your connection if one or more user mappings have a "Failed" status after you click **Preview**. The preview shows 5 random users and their mappings from your data source. If the mapping you provide does not map all users, you may experience this case.

## Limitations  

The following limitations apply when you map Microsoft Entra IDs:

- Only one mapping is supported for all users. Conditional mappings aren't supported.  
- You can't change your mapping after the connection is published.  
- Regex-based expressions against the Microsoft Entra user properties aren't supported for the Microsoft Entra ID to Federation ID transformation.

## Related content

- [Map non-Entra identities](map-non-entra-id.md)
- [Deployment overview](deployment-overview.md)
