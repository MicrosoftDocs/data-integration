---
title: Change the on-premises data gateway service account
description: Provides information on how to change the Windows account for the on-premises data gateway service.
ms.topic: conceptual
ms.date: 6/26/2025
---

# Change the on-premises data gateway service account

The on-premises data gateway is configured to use *NT SERVICE\PBIEgwService* for the Windows service sign-in credential. In the context of the machine on which you install the gateway, the account by default has the right of Log on as a service.

This service account isn't the account used to connect to on-premises data sources. It also isn't the work or school account that you sign in to cloud services with.

## Change the service account

It isn't necessary to change the service account, but you can, if necessary. To change the Windows service account for the on-premises data gateway:

1. Open the [on-premises data gateway app](service-gateway-app.md), select **Service settings**, and then select **Change account**.

   > [!NOTE]
   > We recommend using the on-premises data gateway app to change the service account instead of the Windows Service app. Using the gateway app ensures that the new account has all the required privileges. Not using the on-premises data gateway app for this purpose could lead to inconsistent logging and other issues.

   :::image type="content" source="media/service-gateway-service-account/service-settings.png" alt-text="Screenshot of the on-premises data gateway app with the Change account option emphasized.":::

    The default account for this service is *NT SERVICE\PBIEgwService*. Change this account to a domain user account within your Windows Server Active Directory domain, or use a managed service account to avoid having to change the password.

1. In the pop-up, select **Apply & Restart**. You need the recovery key to change the service account.

   :::image type="content" source="media/service-gateway-service-account/change-account.png" alt-text="Screenshot of the restart warning dialog for the change account option.":::

1. Provide the service account and password, and select **Configure**.

   :::image type="content" source="media/service-gateway-service-account/configure-account.png" alt-text="Screenshot of the configure option service account and password entries.":::

1. Provide your sign-in account, and select **Sign in**.

   :::image type="content" source="media/service-gateway-service-account/account-sign-in.png" alt-text="Screenshot of the account sign in screen where you enter your email address.":::

1. In the next window, select **Migrate, restore or takeover an existing gateway**, and follow the process for [restoring](service-gateway-migrate.md) your gateway.

1. After the restoration is complete, the new gateway uses the domain account.

   :::image type="content" source="media/service-gateway-service-account/domain-account.png" alt-text="Screenshot of the on-premises data gateway app showing the new domain account.":::

> [!NOTE]
> To reset the gateway to the default service account, you need to uninstall and reinstall the gateway. You need the recovery key for this operation.

## Switch to a group managed service account (gMSA)

Group managed service accounts (gMSAs) can be used for the data gateway in place of normal accounts. To use a gMSA, you can follow these steps.

1. On a computer with the Remote Server Administration Tools installed, run the following command to configure a KDS Root key (if it hasn't already been done in your organization):

   ```powershell
   Add-KdsRootKey -EffectiveImmediately
   ```

1. Run the following command to create the group managed service account. Use the **Name** parameter to specify the service account name and the **PrincipalsAllowedToRetrieveManagedPassword** parameter to specify the NetBIOS name of the computers allowed to use the group managed service account.

   ```powershell
   New-ADServiceAccount -Name "PowerBiDGgMSA" -PrincipalsAllowedToRetrieveManagedPassword server1$ -DnsHostName server1.contoso.com -Enabled $True
   ```

   > [!NOTE]
   > The `$` at the end of the NetBIOS server name is necessary to indicate the computer account.

1. Add the service account to the computer hosting the data gateway.

   ```powershell
   Install-ADServiceAccount -Identity PowerBiDGgMSA
   ```

   > [!NOTE]
   > This step must be performed on the computer hosting the data gateway.

1. On the computer hosting the data gateway, launch the Services applet from Administrative Tools or by pressing Windows-R to launch a **Run** window, and running *services.msc*.

1. Locate the service **On-premises data gateway service** and double-click it to open its properties.

1. Update the log on in the service properties to the gMSA you want to use and select **OK**.

   :::image type="content" source="media/service-gateway-service-account/update-service-account.png" alt-text="Screenshot showing where to update the service log on account in the service properties.":::

   > [!NOTE]
   > Be sure to include the `$` at the end of the account name. Don't specify a password when using a group managed service account.

1. Select **OK** to acknowledge that the *Logon as a service* right has been granted to the group managed service account.

1. Select **OK** to acknowledge that the service has to be stopped and restarted manually.

1. Restart the service from the Services applet.

1. Launch the on-premises data gateway app. When prompted, sign in as an administrator of the gateway.

1. Select **Migrate, restore, or takeover an existing gateway** and then select **Next**.

1. Enter the recovery key that you created when you set up the gateway and then select **Configure**.

   :::image type="content" source="media/service-gateway-service-account/enter-recovery-key.png" alt-text="Screenshot showing where to enter the recovery key for the gateway.":::

1. Select **Close** to exit the data gateway app configuration.

## Related content

* [Set the datacenter region](service-gateway-data-region.md)  
