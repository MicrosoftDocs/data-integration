---
title: "Migrate, restore, or take over an on-premises data gateway"
description: Learn how to move a gateway to a new computer, recover a damaged gateway, or take over ownership of a gateway.
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

# Migrate, restore, or take over an on-premises data gateway

[!INCLUDE [gateway-rewrite](../includes/gateway-rewrite.md)]

Run the gateway installer on a computer where you want to migrate, restore, or take over the gateway.

If you're restoring the gateway on the same computer as the original gateway was installed on, you must first uninstall the gateway on that computer before restoring the gateway.

> [!NOTE]
> If you [remove or delete a gateway cluster](service-gateway-manage.md#remove-or-delete-an-on-premises-data-gateway) in any of the cloud services, you will not be able to restore it.

1. Download the gateway and install it. For more information, see [Install an on-premises data gateway](service-gateway-install.md).

2. After you've signed in to your Office 356 account, register the gateway. Select **Migrate, restore, or take over an existing gateway** > **Next**.

    ![Register gateway](media/service-gateway-migrate/register-gateway.png)

3. Select from the available clusters and gateways, and enter the recover key for the selected gateway. The recovery key is the one you created and safely stored when you originally installed the gateway (see step 8 in [Install an on-premises data gateway](service-gateway-install.md)).

4. Select **Configure**.

    ![Migrate, restore, or take over](media/service-gateway-migrate/migrate-restore-takeover.png)

Once the configuration finishes, the migrate, restore, or takeover process is complete.

## Next steps

* [Troubleshoot the on-premises data gateway](service-gateway-tshoot.md)
