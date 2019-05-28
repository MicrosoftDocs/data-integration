---
title: Set the data center region
description: This article describes how to determine the data center region and how its value can be set.
author: mgblythe
ms.author: mblythe
manager: kfile
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-gateways
ms.topic: conceptual
ms.date: 05/16/2019
LocalizationGroup: Gateways 
---

# Set the data center region

During gateway installation, you can set the data center region used by the gateway. By default, the data center region is the region of your Power BI tenant or your Office 356 tenant if you have registered for either of these services. If not, it may be the closest Azure region to you.

![On-premises data gateway data center region](media/service-gateway-data-region/data-center-region.png)

If you want to change the data center region after your gateway is installed, you can:

- Restore the on-premises data gateway on the current gateway machine.
- Migrate or take over the on-premises data gateway on a different machine.

![Setting the gateway data center region after installation](media/service-gateway-data-region/restore-change-region.png)

To find the current data center region you're in after the gateway is installed:

1. Open the [on-premises data gateway app](service-gateway-app.md) and sign in to your account.
2. In the **Status** tab, your data region is listed under **Logic Apps, Azure Analysis Services**.

   ![Your data is stored in](media/service-gateway-data-region/gateway-data-center-region.png)

