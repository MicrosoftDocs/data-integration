---
title: Manage on-premises data gateway high-availability clusters and load balancing
description: You can create clusters of on-premises data gateways to provide high availability for your enterprise. In addition, you can configure your clusters to provide load balancing over multiple computers.
author: mgblythe
ms.author: mblythe
manager: kfile
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-gateways
ms.topic: conceptual
ms.date: 07/15/2019
LocalizationGroup: Gateways 
---

# Manage on-premises data gateway high-availability clusters and load balancing

[!INCLUDE [gateway-rewrite](../includes/gateway-rewrite.md)]

You can use an on-premises data gateway cluster to avoid single points of failure and to load balance traffic across gateways in a cluster.

## High-availability clusters for an on-premises data gateway

You can create high-availability clusters of gateway installations. The clusters help ensure that your organization can access on-premises data resources. These resources can use any cloud service, including Power BI and PowerApps. Gateway admins use such clusters to avoid single points of failure when accessing on-premises data resources.

The gateway cloud service always uses the primary gateway in a cluster unless that gateway is not available. In that case, the service switches to the next available gateway in the cluster.

### Manage a gateway cluster

After you create a cluster of two or more gateways, all gateway management operations apply to every gateway in the cluster. These operations include granting administrative permissions to a gateway and adding data sources or connections.

For example, when admins select **Manage gateways** in Power BI, they see the list of registered clusters or individual gateways. But, they don't see the individual gateway instances that are members of the cluster.

All requests are routed to the primary instance of a gateway cluster. If the primary gateway instance isn't online, the request is routed to another gateway instance in the cluster.

## Load balance across gateways in a cluster

You can choose to let traffic be distributed evenly across gateways in a cluster. By default, the selection of a gateway during load balancing is random.

For example, to provide load balancing from the Power BI service, select the gear icon ![A gear icon](media/service-gateway-manage/icon-gear.png) in the upper-right corner, then select **Manage gateways**. Next, select **Distribute requests across all active gateways in this cluster**.

![Gateway cluster settings](media/service-gateway-high-availability-clusters/gateway-onprem-loadbalance.png)

## Next steps

* [PowerShell support for gateway clusters](service-gateway-powershell-support.md)
