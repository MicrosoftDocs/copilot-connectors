---
title: "Map non-Microsoft Entra ID Identities" 
ms.author: misvenso 
author: monaray97 
manager: jameslau 
ms.audience: Admin 
ms.topic: how-to
ms.service: copilot-connectors 
ms.localizationpriority: medium 
description: "Find information about how to map non-Entra ID identities when you set up Microsoft 365 Copilot connectors in the Microsoft 365 admin center." 
ms.date: 02/13/2026
---

# Map non-Microsoft Entra ID identities  

This article describes how to map non-Microsoft Entra ID identities to your Microsoft Entra identities. Mapping identities allows people in your access control list (ACL) with non-Microsoft Entra ID identities to view connector responses scoped to them.

These steps are relevant for AI administrators who choose **Only people with access to this data source** when you [Customize connector settings](/microsoft-365/copilot/connectors/deployment-overview#customize-connector-settings-optional) and choose **Non-Entra ID**.

## Select a Microsoft Entra user property  

Select the Microsoft Entra user property you're creating the mapping for. This property is the target property to map your non-Entra ID identities to.  

You can select one of the following Microsoft Entra properties.

| Microsoft Entra property    | Definition           | Example         |
| :------------------- | :------------------- |:--------------- |
| User Principal Name (UPN)  | A UPN consists of a UPN prefix (the user account name) and a UPN suffix (a DNS domain name). The prefix is joined with the suffix using the "@" symbol. | us1@contoso.onmicrosoft.com |
| Microsoft Entra ID                 | A Microsoft Entra ID for a given user is the unique GUID of the user.                 | 58006c96-9e6e-45ea-8c88-4a56851eefad            |
| Microsoft Entra object ID                 | A unique identifier that Microsoft Entra uses to identify objects as security principal.                  | S-1-5-21-453406510-812318184-4183662089             |

## Select non-Entra ID user properties to map

You can select non-Entra ID properties pulled from your data source to apply regular expressions on.

Select a non-Entra ID user property from the dropdown and provide a regular expression to be applied on those user property values.

The following table shows examples of regular expressions and their outputs applied to a sample string. 

| Sample String        | Regular expression   | Output of regular expression on sample string |
| :------------------- | :------------------- |:---------------|
| Alexis Vasquez       | `.*`                 | Alexis Vasquez |
| Alexis Vasquez       | `..$`                | ez             |
| Alexis Vasquez       | `(\w+)$`             | Vasquez        |

You can add as many non-Entra ID user properties as you want expressions for. You can apply different regular expressions to the same user property if your final formula warrants that.  

## Create formula to complete mapping

You can combine the outputs of the regular expressions applied to each of your non-Entra ID user properties to form the Microsoft Entra property.

In the formula box, `{0}` corresponds to the output of the regular expression applied to the *first* non-Entra ID property you selected. `{1}` corresponds to the output of the regular expression applied to the *second* non-Entra ID property you selected. `{2}` corresponds to the output of the regular expression applied to the *third* non-Entra ID property, and so on.  

The following table shows some examples of formulas with regular expression outputs and formula outputs.

| Sample formula                  | Value of {0} on sample user                 | Value of {1} on sample user           | Output of formula                  |
| :------------------- | :------------------- |:---------------|:---------------|
| {0}.{1}@contoso.com  | firstname | lastname |firstname.lastname@contoso.com
| {0}@domain.com                 | userid                 |             |userid@domain.com

After you provide your formula, you can optionally select **Preview** to see a preview of five users from your data source with their respective user mappings applied. The output of the preview includes the value of the non-Entra ID user properties for those users and the output of the final formula for that user. It also indicates whether the output of the formula resolves to a Microsoft Entra user in your tenant via a **Success** or **Failed** icon.  

>[!NOTE]
>You can proceed to create your connection if one or more user mappings have a **Failed** status after you select **Preview**. The preview shows five random users and their mappings from your data source. If the mapping you provide doesn't map all users, a failure can occur.

## Limitations  

The following limitations apply when you map non-Microsoft Entra IDs:

- Only one mapping is supported for all users. Conditional mappings aren't supported.  
- You can't change your mapping after the connection is published.  
- Only regex-based expressions against the non-Entra ID user properties are supported for the transformation.
- You can choose to map only three Microsoft Entra identities: UPN, Microsoft Entra ID, and object ID.

## Related content

- [Map Microsoft Entra IDs](map-entra-id.md)
- [Deployment overview](deployment-overview.md)
