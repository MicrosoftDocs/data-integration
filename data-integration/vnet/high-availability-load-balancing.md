---
title: Manage virtual network (VNet) data gateway high availability and load balancing
description: Describes how to create and manage virtual network (VNet) data gateway clusters for high availability and load balancing.
ms.reviewer: dougklo
ms.topic: conceptual
ms.date: 6/27/2025
---

# Manage virtual network data gateway high availability and load balancing

You can use a cluster of virtual network data gateways to load balance the queries executing on the cluster and to avoid a single point of failure.

## High-availability and load balancing a cluster for a virtual network data gateway

You can create high-availability clusters when creating a new virtual network data gateway. Having multiple gateways in the cluster ensures that your organization can access your data behind the virtual network. It also avoids a single point of failure when accessing on-premises data resources. A cluster with multiple gateways not only provides high-availability, but also provides load balancing functionality. The selection of a gateway during load balancing is random.

## How to create a cluster of multiple virtual network data gateways

There are two ways to create a cluster of virtual network data gateways. The first one is to directly create a cluster with multiple gateways during the first-time creation of the data gateway. The second option is to edit the settings for existing virtual network data gateways.

If you're creating a new virtual network data gateway, you first need to fill out the required information for creating the virtual network from the Power Platform admin center. Afterwards, you're presented with an advanced options menu.

:::image type="content" source="media/high-availability-load-balancing/create-virtual-network.png" alt-text="Screenshot of the VNet data gateway form, with the Subscription, Resource group, Virtual network, Subnet, and Name entries filled in.":::

By default, the number of gateways is set to 1. This setting means that only one gateway is created. You can increase the number of gateways by using the slider. The maximum number of gateways per cluster is 7 now.

## How to ensure your gateway is available for query execution

The virtual network data gateway cluster autopauses after a certain time of inactivity. After the gateway is auto paused, it takes about 2 to 3 minutes for the cluster to become available again. By default, the time interval of inactivity before autopause is set to 30 minutes. You can increase this time interval to a maximum of 24 hours. There's no support for leaving the virtual network data gateway cluster always on.

:::image type="content" source="media/high-availability-load-balancing/setting-time-interval.png" alt-text="Screenshot of the VNet gateway advanced options, with the Time interval set to 1 hour 30 minutes and the number of gateways set to 4.":::

## How to change the high availability options

At any point in time, you can change the number of gateways you have in the cluster. You can also change the time interval of inactivity before auto pause. To edit these settings, select a virtual network data gateway, and then select **Settings** on the top. You can now change the advanced options on the **Settings** panel.

:::image type="content" source="media/high-availability-load-balancing/change-vnet-settings.png" alt-text="Screenshot with a VNet data gateway selected, the setting selection emphasized, and the Settings panel open." lightbox="media/high-availability-load-balancing/change-vnet-settings.png":::

## Virtual network data gateway performance and workload capacity

Gateways support multiple workloads, allowing for efficient parallel execution. Each virtual network data gateway instance is designed to handle concurrent jobs across different workloads:

- Up to 6 refresh queries can run simultaneously, enabling efficient data updates for scheduled refresh operations.
- Up to 15 direct queries can execute concurrently, supporting interactive reporting and real-time data retrieval.
- 1 Fabric Pipeline Copy activity job. Generally, a Copy activity only generates one Copy activity job. However, in some cases, multiple jobs can be generated.
- 1 Fabric Copy job. If the data source has multiple tables, the copy job is divided into multiple subjobs. A gateway instance can only run one subjob at a time.
- Up to 6 Lookup, Get metadata, Delete and Script  activity can run concurrently.
- Up to 200 other pipeline activities such as Stored Procedure and HDInsight can run concurrently.