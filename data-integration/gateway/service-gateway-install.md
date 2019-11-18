---

title: "Install an on-premises data gateway"
description: Learn how to install a gateway so you can connect to on-premises data.
author: mgblythe
manager: kfile
ms.reviewer: ''

ms.technology: on-premises-data-gateway
ms.topic: conceptual
ms.date: 09/19/2019
ms.author: mblythe

LocalizationGroup: Gateways
---

# Install an on-premises data gateway

[!INCLUDE [gateway-rewrite](../includes/gateway-rewrite.md)]

An on-premises data gateway is software that you install in an on-premises network. The gateway facilitates access to data in that network.

As we explain in the [overview](service-gateway-onprem.md), you can install a gateway either in personal mode, which applies to Power BI only, or in standard mode. We recommend standard mode. In that mode, you can install a standalone gateway or add a gateway to a cluster, which we recommend for high availability.

In this article, we show you how to install a standard gateway and then add another gateway to create a cluster.

## Requirements

### Minimum requirements

* .NET Framework 4.6 (Gateway release August 2019 and earlier)
* .NET Framework 4.7.2 (Gateway release September 2019 and later)
* A 64-bit version of Windows 7 or a 64-bit version of Windows Server 2008 R2

### Recommended

* An 8-core CPU
* 8 GB of memory
* A 64-bit version of Windows Server 2012 R2 or later
* Solid state drive (SSD) storage for spooling.

### Related considerations

* Gateways aren't supported on Server Core installations.
* The user installing the gateway must be the admin of the gateway.
* The gateway can't be installed on a domain controller.
* If you're planning to use Windows authentication, make sure you install the gateway on a computer that's a member of the same Active Directory environment as the data sources.
* You shouldn't install a gateway on a computer, like a laptop, that might be turned off, asleep, or disconnected from the internet. The gateway can't run under any of those circumstances.
* If a gateway uses a wireless network, its performance might suffer.
* You can install up to two gateways on a single computer: one running in personal mode and the other running in standard mode. You can't have more than one gateway running in the same mode on the same computer.

## Download and install a gateway

Because the gateway runs on the computer that you install it on, be sure to install it on a computer that's always turned on. For better performance and reliability, we recommend that the computer is on a wired network rather than a wireless one.

1. [Download the gateway](https://go.microsoft.com/fwlink/?LinkId=820925&clcid=0x409).

1. In the gateway installer, select **Next**.

    ![Starting gateway installation](media/service-gateway-install/gateway-installer.png)

1. Select **On-premises data gateway (recommended)** > **Next**.

    ![Choosing the gateway type](media/service-gateway-install/gateway-type.png)

    > [!NOTE]
    > The **On-premises data gateway (personal mode)** option can be used only with Power BI. For more information on installation, management, and use of personal gateways, see [Use personal gateways in Power BI](/power-bi/service-gateway-personal-mode).

1. Select **Next**.

    ![Reminder before you install](media/service-gateway-install/laptop-reminder.png)

1. Keep the default installation path, accept the terms of use, and then select **Install**.

    ![Installing to the default installation path](media/service-gateway-install/install-path.png)

1. Enter the email address for your Office 365 organization account, and then select **Sign in**.

    ![Entering your email address](media/service-gateway-install/email-address.png)

    > [!NOTE]
    > You need to sign in with either a work account or a school account. This account is an *organization account*. If you signed up for an Office 365 offering and didn't supply your work email address, your address might look like nancy\@contoso.onmicrosoft.com. Your account is stored within a tenant in Azure AD. In most cases, your Azure AD account’s User Principal Name (UPN) will match the email address.  

    The gateway is associated with your Office 365 organization account. You manage gateways from within the associated service.

    You're now signed in to your account.

1. Select **Register a new gateway on this computer** > **Next**.

    ![Registering the gateway](media/service-gateway-install/register-gateway.png)

1. Enter a name for the gateway. The name must be unique across the tenant. Also enter a recovery key. You'll need this key if you ever want to recover or move your gateway. Select **Configure**.

    ![Configuring the gateway](media/service-gateway-install/configure-gateway.png)

    Note the **Add to an existing gateway cluster** checkbox. We'll use this checkbox in the next section of this article.

    Also note that you can change the region that connects the gateway to cloud services. You should change the region to the region of your Power BI tenant or Office 365 tenant or to the Azure region closest to you. For more information, see [Set the data center region](service-gateway-data-region.md).

1. Review the information in the final window. Because this example uses the same account for Power BI, PowerApps, and Power Automate, the gateway is available for all three services. Select **Close**.

    ![Gateway summary](media/service-gateway-install/summary-screen.png)

Now that you've installed a gateway, you can add another gateway to create a cluster.

## Add another gateway to create a cluster

A cluster lets gateway admins avoid having a single point of failure for on-premises data access. If the primary gateway is unavailable, data requests are routed to the second gateway that you add, and so on.

Because you can install only one standard gateway on a computer, you must install each additional gateway in the cluster on a different computer. This requirement makes sense because you want redundancy in the cluster.

   > [!NOTE]
   > Offline gateway members within a cluster will negatively impact performance. These members should either be removed or disabled.

To create high-availability gateway clusters, you need the November 2017 update or a later update to the gateway software.

1. Download the gateway to a different computer and install it.

1. After you sign in to your Office 365 organization account, register the gateway. Select **Add to an existing cluster**. In the **Available gateway clusters** list, select the *primary gateway*, which is the first gateway you installed. Enter the recovery key for that gateway. Select **Configure**.

    ![Adding a gateway to a cluster](media/service-gateway-install/add-cluster.png)

## Next steps

* [Configure on-premises data gateways](service-gateway-app.md)

* [Manage an on-premises data gateway](service-gateway-manage.md)

* [Monitor and optimize gateway performance](service-gateway-performance.md)
