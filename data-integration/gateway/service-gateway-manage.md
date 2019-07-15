---
title: "Manage an on-premises data gateway"
description: Learn how to manage a gateway so you can connect to on-premises data.
author: mgblythe
manager: kfile
ms.reviewer: ''

ms.service: powerbi
ms.subservice: powerbi-gateways
ms.topic: conceptual
ms.date: 07/15/19
ms.author: mblythe


LocalizationGroup: Gateways
---

# Manage an on-premises data gateway

After you install an on-premises data gateway, you manage it based on your requirements. Every service might integrate gateways differently, so the management options differ depending on the service. While you can manage gateways from any of these services, the articles in this section refer to the "Manage gateways" page in Power BI.

![Manage gateways](media/service-gateway-manage/manage-gateways.png)

> [!NOTE]
> **Manage gateways** will not show up until you're the admin of at least one gateway. This can happen either by being added as an admin or you installing and configuring a gateway.

## Manage gateway admins

When you install a gateway, you are by default an admin of that gateway. You can then add additional users or security groups as admins using the **Administrators** tab for the gateway. You can also remove administrators using this option.

![Gateway administrators tab](media/service-gateway-manage/gateway-admin-tab.png)

>[!NOTE]
>Groups without an email can't be added.

## Remove or delete an on-premises data gateway

You can remove (Power BI) or delete (PowerApps, Microsoft Flow) an on-premises data gateway if you're no longer using it.

However, be aware that removing a gateway in Power BI deletes all the data sources under it. Deleting the Power BI data sources in turn breaks any Power BI dashboards and reports that rely on those data sources.

> [!NOTE]
> If you remove or delete a gateway cluster in any of the cloud services, you won't be able to [restore](service-gateway-migrate.md) it. Also, when you remove or delete a gateway cluster, the gateway is not uninstalled from the gateway machine. You'll have to manually uninstall it from each gateway machine in the cluster.

For example, to remove a gateway in the Power BI service:

1. In the upper-right corner of the Power BI service, select the gear icon ![Settings gear icon](media/service-gateway-manage/icon-gear.png) > **Manage gateways**.

2. Select the gateway > **Remove**

   ![Remove gateway](media/service-gateway-manage/remove-gateway.png)

## Next steps

* [Manage high availability clusters and load balancing](service-gateway-high-availability-clusters.md)

* [Tenant level administration](service-gateway-tenant-level-admin.md)


