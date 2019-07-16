---
title: Change the on-premises data gateway service account
description: Provides information on how to change the Windows account for the on-premises data gateway service.
author: mgblythe
manager: kfile
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-gateways
ms.topic: conceptual
ms.date: 07/15/2019
ms.author: mblythe
LocalizationGroup: Gateways

---
# Change the on-premises data gateway service account

The on-premises data gateway is configured to use *NT SERVICE\PBIEgwService* for the Windows service sign in credential. By default, it has the right of Log on as a service, in the context of the machine that you're installing the gateway on. The account isn't the same account used to connect to on-premises data sources. The account is also not the work or school account that you sign in to cloud services with.

## Change the service account

To change the Windows service account for the on-premises data gateway:

1. Open the [on-premises data gateway app](service-gateway-app.md), select **Service settings**, and then select **Change account**.

   ![Service settings](media/service-gateway-service-account/service-settings.png)

    The default account for this service is *NT SERVICE\PBIEgwService*. You'll want to change this to a domain user account within your Active Directory domain. Or, you'll want to use a managed service account to avoid having to change the password.

2. You'll need the recovery key to change the service account. Select the **Change Account** button.

   ![Change account](media/service-gateway-service-account/change-account.png)

3. Provide the service account and password and select the **Configure** button.

   ![Configure account](media/service-gateway-service-account/configure-account.png)

4. Provide your sign in account and select **Sign in**.

   ![Account sign-in](media/service-gateway-service-account/account-sign-in.png)

5. On the next screens select "Migrate, restore or takeover an existing gateway" and follow the process for [restoring](service-gateway-migrate.md) your gateway.

6. Once the restore process is complete, the new gateway will use the domain account.

   ![Domain account](media/service-gateway-service-account/domain-account.png)

## Next steps

* [Set the data center region](service-gateway-data-region.md)  
