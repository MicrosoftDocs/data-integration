---
title: Install an on-premises data gateway
description: Learn how to install a gateway so you can connect to on-premises data.
ms.topic: conceptual
ms.date: 10/15/2025
ms.custom: sfi-image-nochange
---

# Install an on-premises data gateway

An on-premises data gateway is software that you install in an on-premises network. The gateway facilitates access to data in that network.

As we explain in the [overview](service-gateway-onprem.md#types-of-gateways), you can install a gateway either in personal mode, which applies to Power BI only, or in standard mode. We recommend standard mode. In that mode, you can install a standalone gateway or add a gateway to a cluster, which we recommend for high availability.

In this article, we show you how to install a standard gateway, how to add another gateway to create a cluster, and how to install a personal mode gateway.

> [!NOTE]
> To update an existing gateway to a later version, refer to [Update an on-premises data gateway](service-gateway-update.md).

## Requirements

### Minimum requirements

* .NET Framework 4.8
* A 64-bit version of Windows 10 or a 64-bit version of Windows Server 2019
* 4-GB disk space for [performance monitoring](service-gateway-performance.md#gateway-performance-monitoring-public-preview) logs (in default configuration)

> [!NOTE]
> The minimum screen resolution supported for the on-premises data gateway is 1280 x 800.

### Recommended

* An 8-core CPU
* 8 GB of memory
* A 64-bit version of Windows Server 2019 or later
* Solid-state drive (SSD) storage for spooling

### Related considerations

* Workloads might have specific requirements around compatible gateway versions. For dataflows, go to [using dataflows with on-premises data](/power-query/dataflows/using-dataflows-with-on-premises-data).
* Gateways aren't supported on Server Core installations.
* Gateways aren't supported on Windows containers.
* The user installing the gateway must be the admin of the machine where the gateway is being installed.
* The gateway can't be installed on a domain controller.
* If you're planning to use Windows authentication, make sure you install the gateway on a computer that's a member of the same Microsoft Entra environment as the data sources.
* Don't install a gateway on a computer, like a laptop, that might be turned off, asleep, or disconnected from the internet. The gateway can't run under any of those circumstances.
* If a gateway uses a wireless network, its performance might suffer. We recommend that you set the gateway on a wired device for best network performance.
* If you use a virtualization layer for your virtual machine, performance might suffer or perform inconsistently.
* You could install other applications on the gateway machine, but these applications might degrade gateway performance. If you do install other applications on the gateway machine, be sure to monitor the gateway closely to check if there's any resource contention.
* You can install up to two gateways on a single computer: one running in personal mode and the other running in standard mode. An on-premises data gateway (personal mode) can be used only with Power BI. You can't have more than one gateway running in the same mode on the same computer.
* When using an on-premises data gateway (standard mode) to access a data source on a remote domain, the gateway has to be installed on a domain joined machine having a trust relationship with the target domain.

* <a name="private-link-consideration"></a>Using an on-premises data gateway with private link enabled isn't supported. We recommend using the [VNet data gateway](../vnet/overview.md), which does support private link scenarios. If private link is enabled, you get the following error when trying to register a new gateway or migrate/restore/takeover an existing gateway:

   `System.NullReferenceException: Object reference not set to an instance of an object`

   at Microsoft.PowerBI.DataMovement.GatewayCommon.DmtsGatewayCreation.UpdateGatewayConfiguration.

   To disable private link, go to the powerbi.com page, and select **Settings** > **Admin portal**. Look for the **Advanced networking** section at the bottom of the page, and disable the **Azure Private Link** property. After the gateway is configured, you can enable the **Azure Private Link** property.  

> [!NOTE]
> If your home tenant is located in a region that Microsoft Fabric doesn’t currently support&mdash;such as West India&mdash;and you need to use Fabric workloads like Pipeline or Copy Job, the on-premises data gateway isn't supported in this scenario. We recommend using the VNet data gateway as an alternative.

## Download and install a standard gateway

Because the gateway runs on the computer that you install it on, be sure to install it on a computer that's always turned on. For better performance and reliability, we recommend that the computer is on a wired network rather than a wireless one.

1. [Download the standard gateway](https://go.microsoft.com/fwlink/?LinkId=2116849&clcid=0x409).

   > [!NOTE]
   > If the on-premises data gateway (standard mode) requires access to a remote data source in a different domain, it must be installed on a domain joined machine having a trust relationship with the target domain.

1. In the gateway installer, keep the default installation path, accept the terms of use, and then select **Install**.

    :::image type="content" source="media/service-gateway-install/install-path.png" alt-text="Screenshot of the installation dialog demonstrating installation to the default installation path.":::

1. Enter the email address for your Office 365 organization account, and then select **Sign in**.

    :::image type="content" source="media/service-gateway-install/email-address.png" alt-text="Screenshot of the installation dialog where you enter your email address.":::

    > [!NOTE]
    > You need to sign in with either a work account or a school account. This account is an *organization account*. If you signed up for an Office 365 offering and didn't supply your work email address, your address might look like nancy\@contoso.onmicrosoft.com. Your account is stored within a tenant in Microsoft Entra ID. In most cases, your Microsoft Entra ID account's User Principal Name (UPN) matches the email address.  

    The gateway is associated with your Office 365 organization account. You manage gateways from within the associated service.

    You're now signed in to your account.

1. Select **Register a new gateway on this computer** > **Next**.

    :::image type="content" source="media/service-gateway-install/register-gateway.png" alt-text="Screenshot of the gateway dialog where you register the gateway.":::

1. Enter a name for the gateway. The name must be unique across the tenant. Also enter a recovery key. You need this key if you ever want to recover or move your gateway. Select **Configure**.

    :::image type="content" source="media/service-gateway-install/configure-gateway.png" alt-text="Screenshot of the gateway configuration dialog.":::

    > [!IMPORTANT]
    > You're responsible for keeping the gateway recovery key in a safe place where it can be retrieved later. Microsoft doesn't have access to this key and it can't be retrieved by us.

    Note the **Add to an existing gateway cluster** checkbox. We use this checkbox in the next section of this article.

    Also note that you can change the region that connects the gateway to cloud services. For more information, go to [Set the data center region](service-gateway-data-region.md).

    > [!NOTE]
    > For sovereign clouds, we currently only support installing gateways in the default Power BI region of your tenant. The region picker on the installer is only supported for Public cloud.

    Finally, you can also provide your own Azure Relay details. For more information about how to change the Azure Relay details, go to [Set the Azure Relay for on-premises data gateway](service-gateway-azure-relay.md).

1. Review the information in the final window. Because this example uses the same account for Power BI, Power Apps, and Power Automate, the gateway is available for all three services. Select **Close**.

    :::image type="content" source="media/service-gateway-install/summary-screen.png" alt-text="Screenshot of the gateway summary window.":::

Now that you've installed a gateway, you can add another gateway to create a cluster.

## Add another gateway to create a cluster

A cluster lets gateway admins avoid having a single point of failure for on-premises data access. If the primary gateway is unavailable, data requests are routed to the second gateway that you add, and so on.

Because you can install only one standard gateway on a computer, you must install each extra gateway in the cluster on a different computer. This requirement makes sense because you want redundancy in the cluster.

   > [!NOTE]
   > Offline gateway members within a cluster negatively impact performance. These members should either be removed or disabled.
   >
   > Make sure the gateway members in a cluster are running the same gateway version, as different versions could cause unexpected failures based on supported functionality.

To create high-availability gateway clusters, you need the November 2017 update or a later update to the gateway software.

1. Download the gateway to a different computer and install it.

1. After you sign in to your Office 365 organization account, register the gateway. Select **Add to an existing cluster**. In the **Available gateway clusters** list, select the *primary gateway*, which is the first gateway you installed. Enter the recovery key for that gateway. Select **Configure**.

    :::image type="content" source="media/service-gateway-install/add-cluster.png" alt-text="Screenshot of the gateway dialog where you add a gateway to a cluster.":::

## Download and install a personal mode gateway

1. [Download the personal mode gateway](https://go.microsoft.com/fwlink/?LinkId=2116848&clcid=0x409).

1. In the gateway installer, enter the default installation path, accept the terms of use, and then select **Install**.

    :::image type="content" source="media/service-gateway-install/install-path-personal.png" alt-text="Screenshot of the installation dialog demonstrating the installation path to the personal mode gateway.":::

1. Enter the email address for your Office 365 organization account, and then select **Sign in**.

    :::image type="content" source="media/service-gateway-install/email-address-personal.png" alt-text="Screenshot of the personal mode gateway dialog with your personal mode email address.":::

    > [!NOTE]
    > You need to sign in with either a work account or a school account. This account is an *organization account*. If you signed up for an Office 365 offering and didn't supply your work email address, your address might look like nancy\@contoso.onmicrosoft.com. Your account is stored within a tenant in Microsoft Entra ID. In most cases, your Microsoft Entra ID account's User Principal Name (UPN) matches the email address.  

    The gateway is associated with your Office 365 organization account. You manage gateways from within the associated service.

1. You're now signed in to your account. Select **Close**.

    :::image type="content" source="media/service-gateway-install/summary-screen-personal.png" alt-text="Screenshot of the personal mode gateway summary.":::

## Next steps

* [Configure on-premises data gateways](service-gateway-app.md)

* [Manage an on-premises data gateway](service-gateway-manage.md)

* [Monitor and optimize gateway performance](service-gateway-performance.md)
