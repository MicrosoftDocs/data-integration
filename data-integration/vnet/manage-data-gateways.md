---
title: Manage virtual network (VNet) data gateways
description: Provides information about how to manage virtual network (VNet) data gateways and remove them if required.
author: arthiriyer
ms.reviewer: kvivek
ms.prod: on-premises-data-gateway
ms.technology:
ms.topic: conceptual
ms.date: 03/01/2021
ms.author: arthii
---

# Manage virtual network data gateways

After you have [created](create-data-gateways.md) a virtual network (VNet) data gateway, it will be available in the **Data (preview)** > **Virtual network data gateways** tab in the [Power Platform admin center](https://admin.powerplatform.microsoft.com) for you to manage.

> [!NOTE]
> The Virtual network data gateways tab will not be visible when the Tenant Administration toggle is turned on 

![Manage VNet data gateways](media/manage-vnet-data-gateways.png)

## Manage admins

You can manage admins for this VNet data gateway like you do for standard data gateways in the Power Platform admin center. To add or remove admins, select a gateway and then select **Manage Users**.

![Manage admins](media/manage-admins.png)

## Manage settings

You can view properties for a selected VNet data gateway in the Power Platform admin center by selecting **Settings**.

![Manage settings](media/manage-settings.png)

## Remove VNet data gateways

You can remove or delete VNet data gateways by selecting the gateway and selecting **Remove**.

> [!NOTE]
> When you remove the last gateway associated to a gateway/subnet, it might take up to 48-72 hours before you can delete the subnet or VNet.

![Remove VNet data gateway](media/remove-gateway.png)
