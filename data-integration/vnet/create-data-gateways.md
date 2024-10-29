---
title: Create virtual network (VNet) data gateways
description: Provides information about how to create virtual network (VNet) data gateways.
ms.topic: conceptual
ms.date: 05/06/2024
ms.custom: references_regions
---

# Create virtual network data gateways

Details to consider when creating a VNet data gateway:
- VNET data gateways require a Power BI Premium capacity license (
A4 SKU or higher or any P SKU) or a Fabric license (any SKU).
- Before creating a VNet data gateway, check that the feature is [supported in your region](#regions-supported-for-vnet-data-gateways).
- The creation of VNET data gateways across tenant boundaries isn't supported.
- The metadata (name, details, data sources, encrypted credentials, and so on) for all your VNet data gateways are stored in your Power BI home’s default region. However, the VNet data gateway runs in the same region as your Azure VNet. Sometimes, there's a difference between the default environment of Power Platform and the default region of Power BI. This might impact the regions you pick.


Creating a virtual network (VNet) data gateway is a three-step process:

> [Step 1: Register Microsoft.PowerPlatform as a resource provider](#step-1-register-microsoftpowerplatform-as-a-resource-provider)

> [Step 2: Associate the subnet to Microsoft Power Platform](#step-2-associate-the-subnet-to-microsoft-power-platform)

> [Step 3: Create a VNet data gateway](#step-3-create-a-vnet-data-gateway)


## Step 1: Register Microsoft.PowerPlatform as a resource provider

On the Azure portal, sign in as a subscription owner and register `Microsoft.PowerPlatform` as a resource provider for the subscription that contains the VNet. This change enables your subscription to work with this resource provider.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. Navigate to the specific subscription.

1. Select **Resource providers**.

1. Search for and select **Microsoft.PowerPlatform**, and then select **Register**.

   :::image type="content" source="media/register-resource-provider.png" lightbox="media/register-resource-provider.png" alt-text="Screenshot showing the Resource providers tab of a subscription on the Azure portal.":::

## Step 2: Associate the subnet to Microsoft Power Platform

A user in a role with the Microsoft.Network/virtualNetworks/subnets/join/action permission on the VNet, like the Azure [Network Contributor](/azure/role-based-access-control/built-in-roles#network-contributor) role, can delegate the subnet within the same VNet to Microsoft Power Platform. Subnet delegation enables you to designate a specific subnet for an Azure PaaS service of your choice that needs to be injected into your virtual network. 

> [!NOTE]
> The assignment of a user to the Network Contributor role or granting of the Microsoft.Network/virtualNetworks/subnets/join/action permission on the VNet is configured in Azure, so users unfamiliar with how to do this should contact the person in their organization who manages Azure virtual networks to assist them with the change.

This subnet should have connectivity to the data service.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. [Add a new subnet](/azure/virtual-network/virtual-network-manage-subnet#add-a-subnet) in the VNet. This new subnet can't be shared with other services, but will be used entirely by the Power Platform VNet service. Five IPs on this subnet will be reserved for basic functionality. In addition to those five, reserve one IP for every gateway member you plan to create. For example, if you plan to have 2 clusters of 3 gateway members each, you would want a total of 2 x 3 + 5 or 11 IPs in the subnet CIDR range. It's a good idea to add more IPs for future gateways.

    The gateways within each cluster need to be able to communicate. For this reason, if you are restricting the allowed IPs the delegated subnet can communicate with, don't block the subnet IP range itself. 

    > [!NOTE]
    >
    > * Don't use the subnet names "gatewaysubnet" or "AzureBastionSubnet" as these are reserved words for other features. You won't be able to use it to create a VNet data gateway in Step 3.
    > * Make sure this subnet doesn't have an IPV6 address space added.
    > * Make sure the subnet's IP range doesn't overlap with 10.0.1.x.

1. Select **Microsoft.PowerPlatform/vnetaccesslinks** from the subnet delegation drop-down list.

1. Select **Save**.

   :::image type="content" source="media/associate-subnet.png" lightbox="media/associate-subnet.png" alt-text="Screenshot showing the Add subnet dialog with the Delegate subnet to a service setting showing Microsoft.PowerPlatform/vnetaccesslinks selected.":::

## Step 3: Create a VNet data gateway

A Microsoft Power Platform user enables the subnet for use in Microsoft Power Platform and creates a VNet data gateway. By doing this process, the user authorizes the Microsoft Power Platform VNet service to inject containers into the subnet. The user also needs Microsoft.Network/virtualNetworks/subnets/join/action permission on the VNet to be able to perform this action.

1. Sign in to the [Power BI homepage](https://app.powerbi.com).

1. In the top navigation bar, select the settings gear icon on the right.

1. From the drop down, select the Manage connections and gateways page.
   
1. Select **Virtual network (VNet) data gateway** > **New**.

1. Select the license capacity, subscription, resource group, VNet and the Subnet. Only subnets that are delegated to Microsoft Power Platform are displayed in the drop-down list. VNET data gateways require a [Power BI Premium capacity](/power-bi/enterprise/service-premium-what-is) license (A4 SKU or higher or any P SKU) or [Fabric license](/fabric/enterprise/buy-subscription) to be used (any SKU).

1. By default, we provide a unique name for this data gateway, but you could optionally update it.

1. Select **Save**. This VNet data gateway is now displayed in your **Virtual network data gateways** tab. A VNet data gateway is a managed gateway that could be used for controlling access to this resource for Power platform users.  

   :::image type="content" source="media/vnet-data-gateway.png" lightbox="media/vnet-data-gateway.png" alt-text="Screenshot showing the New virtual network data gateway dialog.":::

   > [!NOTE]
   > Depending on the permissions of your account, you may first be prompted to choose a capacity before selecting a subscription as shown on the previous screenshot of the New virtual network data gateway dialog.

## Regions supported for VNet data gateways

Your Azure VNet region needs to be in one of the following regions for you to be able to create a virtual network (VNet) data gateway:

* Australia East
* Australia Southeast
* Brazil South
* Canada Central
* Central India
* Central US
* East Asia
* East US
* East US 2
* France Central
* Germany West Central
* Japan East
* Korea Central
* North Central US
* North Europe
* Norway East
* South Africa North
* South Central US
* Southeast Asia
* Switzerland North
* UAE North
* UK South
* West Central US
* West Europe
* West US
* West US 2

### See also

[Manage virtual network data gateways](manage-data-gateways.md)
