---
title: Manage virtual network (VNet) data gateways
description: Provides information about how to manage virtual network (VNet) data gateways and remove them if necessary.
ms.topic: conceptual
ms.date: 05/06/2024
---

# Manage virtual network data gateways

After you've [created](create-data-gateways.md) a virtual network (VNet) data gateway, it will be available in the **Data (preview)** > **Virtual network data gateways** tab in the [Power Platform admin center](https://admin.powerplatform.microsoft.com) for you to manage. Also make sure you select your tenant's default home region in the region dropdown to display and manage all your VNet data gateways. You select your tenant's default region because the metadata (name, details, data sources, encrypted credentials, and so on) for all your VNet data gateways are stored in your tenant's default region.

> [!NOTE]
> The **Virtual network data gateways** tab won't be visible when the **Tenant Administration** toggle is turned on.

:::image type="content" source="media/manage-vnet-data-gateways.png" alt-text="Manage VNet data gateways.":::

## Manage access to creating VNet data gateways (gateway installer setting)

Access to creating a VNet data gateway can be limited to selected people only. To do this limitation, you must be a Microsoft Entra ID Global administrator (which includes Global admins) or a Power BI service administrator. Use the **Manage gateway installers** option to manage who can create a VNet data gateway in your enterprise. This operation isn’t available for gateway admins. Go to the [manage gateway installers](/power-platform/admin/onpremises-data-gateway-management#manage-gateway-installers) documentation to learn more.

## Manage admins

You can manage admins for this VNet data gateway like you do for standard data gateways in the Power Platform admin center. To add or remove admins, select a gateway, and then select **Manage Users**.

:::image type="content" source="media/manage-admins.png" alt-text="Manage admins.":::

## Manage capacity for billing

The capacity linked to your VNet data gateway incurs the bill. You can view and edit this capacity in the [settings](manage-data-gateways.md#manage-settings) for the gateway. Fabric and Power BI capacities are valid. We support F and P SKUs today.

> [!NOTE]
> Existing preview users are required to assign a capacity to each of their existing gateways in order to make edits to their configuration, or to create new gateways after February 1st, 2024.

## Manage settings

You can view properties for a selected VNet data gateway in the Power Platform admin center by selecting **Settings**.

:::image type="content" source="media/manage-settings.png" alt-text="Manage settings.":::

### Time to auto-shutdown

This setting allows you to shutdown a VNet data gateway that has been idling for the designated amount of time. Idling starts after the last query has finished executing. The interval to wait options include: 30 minutes, 1 hour, 1 hour and 30 minutes, 2 hours, 2 hours and 30 minutes, 4 hours, 6 hours, 8 hours, 12 hours, and 24 hours.

## Remove VNet data gateways

You can remove or delete VNet data gateways by selecting the gateway and selecting **Remove**.

> [!NOTE]
> When you remove the last gateway associated to a gateway/subnet, it might take up to 48-72 hours before you can delete the subnet or VNet. When bringing a previously deprovisioned VNet online, it typically takes about 2 minutes to become available, but can take up to 15 minutes in some cases before it's available.

>[!Important]
> To be able to remove or delete a VNet data gateway, you need to:
>
> * Be a gateway admin of the VNet data gateway you want to remove
> * Have the Azure Network Contributor role in the Azure portal
> * Register the Microsoft.PowerPlatform provider as a resource provider

:::image type="content" source="media/remove-gateway.png" alt-text="Remove VNet data gateway.":::

## Related content

For detailed instructions on managing capacity in Fabric and Power BI, refer to [Manage your Fabric capacity](/fabric/admin/capacity-settings?tabs=power-bi-premium).
