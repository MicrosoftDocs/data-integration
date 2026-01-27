---
title: Manage virtual network (VNet) data gateways
description: Provides information about how to manage virtual network (VNet) data gateways and remove them if necessary.
ms.topic: concept-article
ms.date: 6/23/2025
ms.custom: sfi-image-nochange
---

# Manage virtual network data gateways

After you [create](create-data-gateways.md) a virtual network (VNet) data gateway, it's available in the **Data (preview)** > **Virtual network data gateways** tab in the [Power Platform admin center](https://admin.powerplatform.microsoft.com) for you to manage. Also make sure you select your tenant's default home region in the region dropdown to display and manage all your VNet data gateways. You select your tenant's default region because the metadata (name, details, data sources, encrypted credentials, and so on) for all your VNet data gateways are stored in your tenant's default region.

> [!NOTE]
> Tenant Admin mode provides a broader view of gateway resources within a tenant. When enabled, it displays all gateways in the tenant that the user has permission to manage as a Tenant Administrator. By contrast, the regular view only lists gateways where the user explicitly assigns as a gateway administrator. 

:::image type="content" source="media/manage-data-gateways/manage-vnet-data-gateways.png" alt-text="Screenshot of the Virtual Network data gateways page whey you manage VNet data gateways." lightbox="media/manage-data-gateways/manage-vnet-data-gateways.png":::

## Manage access to creating VNet data gateways (gateway installer setting)

Access to creating a VNet data gateway can be limited to selected people only. To do this limitation, you must be a Microsoft Entra ID Global administrator (which includes Global admins) or a Power BI service administrator. Use of Global Admins is discouraged for most cases, where the Power BI service administrator role is sufficient to grant the necessary access. Use the **Manage gateway installers** option to manage who can create a VNet data gateway in your enterprise. This operation isn’t available for gateway admins. To learn more, go to the [manage gateway installers](/power-platform/admin/onpremises-data-gateway-management#manage-gateway-installers) documentation.

## Manage admins and users

You can manage admins for this VNet data gateway like you do for on-premises data gateways in the **Manage Connections and Gateway** setting in Fabric and Power BI/  Power Platform admin center. To add or remove admins, select a gateway, and then select **Manage Users**.

You can also share the gateway with other users in the organization, allowing them to see and use this VNet Data Gateway without needing to create a new one. You can choose either the **Connection Creator** or **Connection Creator with resharing** role.

:::image type="content" source="media/manage-data-gateways/manage-admins.png" alt-text="Screenshot of the Virtual Network data gateways page with the Manage admins pane opened." lightbox="media/manage-data-gateways/manage-admins.png":::

## Manage capacity for billing

The capacity linked to your VNet data gateway incurs the consumption. You can view and edit this capacity in the [settings](manage-data-gateways.md#manage-settings) for the gateway. Fabric and Power BI capacities are valid. We support F, P SKUs and A SKUs above A4.

> [!NOTE]
> Existing preview users are required to assign a capacity to each of their existing gateways in order to make edits to their configuration, or to create new gateways after February 1, 2024.

## Firewall Configuration for Certificate Connectivity
The following domains related to certificate (HTTP/Port 80) may need to be included in your firewall allowlists to optimize connectivity. These endpoints are used during certificate validation and renewal processes. You can get full list from:

- [Azure Certificate Authority details | Microsoft Learn](https://learn.microsoft.com/azure/security/fundamentals/azure-ca-details?tabs=root-and-subordinate-cas-list#certificate-downloads-and-revocation-lists)
- [DigiCert Certificate Status IP Addresses](https://knowledge.digicert.com/alerts/digicert-certificate-status-ip-address#certificate-status-ipv4)

## Manage settings

You can view properties for a selected VNet data gateway in the Power Platform admin center by selecting **Settings**.

:::image type="content" source="media/manage-data-gateways/manage-settings.png" alt-text="Screenshot of the Power Platform admin center with the Manage settings pane displayed." lightbox="media/manage-data-gateways/manage-settings.png":::

### Time to auto-shutdown

This setting allows you to shut down a VNet data gateway that has been idling for the designated amount of time. Idling starts after the last query is finished executing. The interval to wait options include: 30 minutes, 1 hour, 1 hour and 30 minutes, 2 hours, 2 hours and 30 minutes, 4 hours, 6 hours, 8 hours, 12 hours, and 24 hours.

### Certificate & proxy support (preview)

Certificate and Proxy Support enable secure and compliant connectivity for enterprise environments. With certificate-based authentication, organizations can use trusted, enterprise-issued certificates to validate gateway communication. Proxy configuration support allows the VNET Data Gateway to connect through corporate-controlled network routes when direct internet access is restricted. Together, these enhancements strengthen security, improve deployment flexibility, and allow the VNET Data Gateway to operate seamlessly in highly controlled and regulated network infrastructures.

:::image type="content" source="media/manage-data-gateways/certificate-proxy-setting.png" alt-text="Screenshot of the Virtual Network data gateway certificate and proxy setting page" lightbox="media/manage-data-gateways/certificate-proxy-setting.png":::

## Remove VNet data gateways

You can remove or delete VNet data gateways by selecting the gateway and selecting **Remove**.

> [!NOTE]
> When you remove the last gateway associated to a gateway/subnet, it might take up to 48-72 hours before you can delete the subnet or VNet.

> [!IMPORTANT]
> To be able to remove or delete a VNet data gateway, you need to:
>
> * Be a gateway admin of the VNet data gateway you want to remove
> * Have Microsoft.Network/virtualNetworks/subnets/join/action permission on the VNet
> * Register the Microsoft.PowerPlatform provider as a resource provider

:::image type="content" source="media/manage-data-gateways/remove-gateway.png" alt-text="Screenshot of the Virtual network data gateways page with the Remove VNet data gateway pane displayed." lightbox="media/manage-data-gateways/remove-gateway.png":::

## Related content

For detailed instructions on managing capacity in Fabric and Power BI, refer to [Manage your Fabric capacity](/fabric/admin/capacity-settings?tabs=power-bi-premium).
