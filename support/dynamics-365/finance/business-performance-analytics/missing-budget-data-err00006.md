---
title: Missing budget data error
description: Provides information about the Missing budget data error (error code ERR00006) in Business performance analytics in Microsoft Dynamics 365 Finance.
author: jinniew
ms.author: jiwo
ms.reviewer: twheeloc 
ms.date: 04/30/2024
ms.custom: sap:Business intelligence, reporting, analytics
ms.search.form: business-performance-analytics
audience: Application User
---
# Missing budget data: Error code: ERR00006 [Type: Warning]

> [!NOTE]
> The functionality that's described in this article is available as part of a preview release. The functionality and the content of this article are subject to change. For more information about how to participate in the public preview for [Business performance analytics](/dynamics365/finance/business-performance-analytics/business-performance-analytics-home-page), contact <bpaquestions@service.microsoft.com>.

## Symptoms

Error code *ERR00006* is logged in the **Bpa self help logs** table in Microsoft Dataverse when no budget is created in Dynamics 365 Finance, and no budget data is available for reports.

Here's an example of a record:

> BudgetFact is empty due to one or more missing inputs ['mserp_budgettransactionlinebientity', 'mserp_budgettransactionheaderbientity']

## Resolution

This warning is for information only. No action is required.

The warning indicates that there's no budget in Dynamics 365 Finance, and no budget data is available for reports. This issue doesn't require immediate attention. Instead, consider this information as part of your overall financial data assessment.

## See also

[Business performance analytics self-help](business-performance-analytics-self-help-overview.md)
