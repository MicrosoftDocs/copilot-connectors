---
title: "Map Microsoft Entra identities" 
ms.author: misvenso 
author: monaray97 
manager: jameslau 
ms.audience: Admin 
ms.topic: how-to
ms.service: microsoft-365-copilot-connectors
ms.localizationpriority: medium 
description: "Find information about how to map users to Microsoft Entra IDs when you customize Microsoft 365 Copilot connectors in the admin center." 
ms.date: 02/13/2026
---

# Map Microsoft Entra identities  

This article describes how to map your Microsoft Entra identities to a unique identifier for your data source (non-Microsoft Entra identity). This mapping allows people in your access control list (ACL) with non-Microsoft Entra identities to view connector results scoped to them.

These steps are relevant for AI administrators who choose **Only people with access to this data source** when they [Customize connector settings](/microsoft-365/copilot/connectors/deployment-overview#customize-connector-settings-optional) and map identities to user principal names (UPNs) in Entra ID.

## Select Microsoft Entra user properties to map

You can select the Microsoft Entra properties you need to map to the external accounts.

You can select a Microsoft Entra user property from the dropdown. You can also add as many Microsoft Entra user properties as you want if these properties are necessary to create the mapping for your organization.

## Create formula to complete mapping

You can combine the values of the Microsoft Entra user properties to form the unique ID.

In the formula box, `{0}` corresponds to the *first* Microsoft Entra property you selected. `{1}` corresponds to the *second* Microsoft Entra property you selected. `{2}` corresponds to the *third* Microsoft Entra property, and so on.  

The following table shows some examples of formulas with regular expression outputs and formula outputs.

| Sample formula                  | Value of property {0} for a sample user                 | Value of property {1} for a sample user           | Output of formula                  |
| :------------------- | :------------------- |:---------------|:---------------|
| {0}.{1}@contoso.com  | firstname | lastname |firstname.lastname@contoso.com
| {0}@domain.com                 | userid                 |             |userid@domain.com

After you provide your formula, you can choose **Preview** to see a preview of five users from your data source with their respective user mappings applied. The output of the preview includes the value of the Microsoft Entra user properties you selected for those users and the output of the final formula provided for that user. It also indicates whether the output of the formula can be resolved to a Microsoft Entra user in your tenant via a **Success** or **Failed** icon.  

>[!NOTE]
>You can still create your connection if one or more user mappings have a **Failed** status after you choose **Preview**. The preview shows five random users and their mappings from your data source. If the mapping you provide doesn't map all users, a failure can occur.

## Limitations  

The following limitations apply when you map Microsoft Entra IDs:

- Only one mapping is supported for all users. Conditional mappings aren't supported.  
- You can't change your mapping after the connection is published.  
- Regex-based expressions against the Microsoft Entra user properties aren't supported for the Microsoft Entra ID to Federation ID transformation.

## Related content

- [Map non-Entra identities](map-non-entra-id.md)
- [Deployment overview](deployment-overview.md)
