---
title: Set the datacenter region for the on-premises data gateway
description: This article describes how to determine the datacenter region and how its value can be set.
ms.topic: conceptual
ms.date: 05/06/2024
---

# Set the datacenter region for the on-premises data gateway

During installation of the on-premises data gateway, you can set the datacenter region used by the gateway.

If you're registered for either Power BI or Office 365, the datacenter region by default is the region of the registered service's tenant. Otherwise, the datacenter region might be the Azure region closest to you.

:::image type="content" source="media/service-gateway-data-region/data-center-region.png" alt-text="Screenshot of the new on-premises data gateway registration page with the Change Region area emphasized.":::

> [!NOTE]
> For sovereign clouds and in Power BI's default region, we currently only support installing gateways in the default PowerBI region of your tenant. The region picker on the installer is only supported for Public cloud.

## Restore, migrate, or take over a gateway in a nondefault region

During installation, after you sign in, you can choose **Migrate, restore, or takeover an existing gateway.** If you want to migrate, restore, or take over a gateway in a nondefault Power BI region, select **Change Region**, and then select the region you want to use.

:::image type="content" source="media/service-gateway-data-region/restore-change-region.png" alt-text="Screenshot of the Migrate, restore, or takeover an existing gateway page with the change region menu displayed with West Central US selected.":::

## Current datacenter region

To find the current datacenter region after you install the gateway:

1. Open the [on-premises data gateway app](service-gateway-app.md) and sign in to your account.
1. In the **Status** tab, your datacenter region appears under **Logic Apps, Azure Analysis Services**.

   :::image type="content" source="media/service-gateway-data-region/gateway-data-center-region.png" alt-text="Screenshot of the on-premises data gateway Status tab open, with West Central US emphasized.":::

For more information about setting the datacenter region for your resources, [watch this video](https://guyinacube.com/2018/01/power-bi-azure-analysis-services-gateway-data-region/).

## Related content

* [Adjust communications settings](service-gateway-communication.md)
