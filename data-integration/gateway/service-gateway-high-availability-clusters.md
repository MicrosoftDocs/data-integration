---
title: Manage on-premises data gateway high availability clusters and load balancing
description: You can create clusters of on-premises data gateways to provide high availability for your enterprise. In addition, you can configure your cluster to provide load balancing over multiple computers.
author: mgblythe
ms.author: mblythe
manager: kfile
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-gateways
ms.topic: conceptual
ms.date: 07/15/19
LocalizationGroup: Gateways 
---

# Manage on-premises data gateway high availability clusters and load balancing

You can use a gateway cluster to avoid single points of failure, and to load balance traffic across gateways in a cluster.

## High availability clusters for on-premises data gateway

You can create high availability clusters of on-premises data gateway installations to ensure your organization can access on-premises data resources using any cloud services like Power BI, PowerApps, and others. Such clusters allow gateway administrators to group gateways to avoid single points of failure in accessing on-premises data resources. The gateway cloud service always uses the primary gateway in the cluster, unless it’s not available. In that case, the service switches to the next gateway in the cluster, and so on.

### Manage a gateway cluster

Once you create a cluster of two or more gateways, all gateway management operations, such as granting administrative permissions to a gateway or adding data sources/connections, apply to all gateways that are part of the cluster.

For example, in **Manage gateways** in Power BI, administrators see the list of registered clusters or individual gateways, but do not see the individual gateway instances that are members of the cluster.

All requests are routed to the primary instance of a given gateway cluster. If the primary gateway instance is not online, the request is routed to another gateway instance in the cluster.

## Load balance across gateways in a cluster

You can choose to allow traffic to be distributed evenly across gateways in a cluster. Currently, the selection of a gateway during load balancing is random.

For example, to provide load balancing from the Power BI service, first select the gear icon ![Settings gear icon](media/service-gateway-manage/icon-gear.png) in the upper-right corner, then select **Manage gateways**. Then enable the option to "Distribute requests across all active gateways in this cluster."

![Load balance](media/service-gateway-high-availability-clusters/gateway-onprem-loadbalance.png)

## Next steps

* [PowerShell support for gateway clusters](service-gateway-powershell-support.md)


