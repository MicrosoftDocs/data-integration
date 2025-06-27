---
title: Update an on-premises data gateway
description: Describes how to update to the latest version of the on-premises data gateway.
ms.topic: conceptual
ms.date: 6/26/2025
---

# Update an on-premises data gateway

We release an update every month for on-premises data gateways. Each of these updates includes new features along with the latest Mashup Engine.

> [!NOTE]
>Currently, Microsoft actively supports only the last six releases of the on-premises data gateway. We release a new update for data gateways every month.

We recommend that you update gateway members one after the other in a timely manner. This process reduces sporadic failures as a query might succeed on one gateway member, but not on the other, based on disparity in capabilities across different versions.

Use the following steps when updating a gateway cluster with two or more members:

1. Disable one gateway member.
2. Wait for ongoing work to be completed. A waiting period of 30 minutes is sufficient for most workloads. However, clusters frequently running critical long-running jobs might require more time for requests to drain.
3. Update the gateway member.
4. Enable the updated gateway member.
5. Repeat step 1-4 until all gateway members are updated.

Disabling a gateway makes sure the load balancer doesn't try to execute queries on the member you're updating, hence reducing delays and failures.

## Update a gateway

To update a gateway:

1. Download the latest [standard mode gateway](https://go.microsoft.com/fwlink/?LinkId=2116849&clcid=0x409) or [personal mode gateway](https://go.microsoft.com/fwlink/?LinkId=2116848&clcid=0x409) and run the installation program. If the version you're trying to install isn't newer than the version already installed, you receive one of the following error messages. To review recent updates, refer to the [Currently supported monthly updates](service-gateway-monthly-updates.md).

   :::image type="content" source="media/service-gateway-update/gateway-same-version.png" alt-text="Screenshot of the update version is the same as the installed version message.":::

   :::image type="content" source="media/service-gateway-update/gateway-old-version.png" alt-text="Screenshot of the update version is older than the installed version message.":::

1. If you install a newer version, you're prompted to update. Select **Update** to begin updating.

   :::image type="content" source="media/service-gateway-update/update-getting-ready.png" alt-text="Screenshot of the Getting ready to update window.":::

1. After the installation finishes, select **Sign in**.

   :::image type="content" source="media/service-gateway-update/gateway-update-signin.png" alt-text="Screenshot of the gateway setup window where you sign in.":::

The gateway update is now complete.

:::image type="content" source="media/service-gateway-update/gateway-update-complete.png" alt-text="Screenshot of the gateway app after the gateway update is complete.":::

## Related content

* [Monitor and optimize gateway performance](service-gateway-performance.md)
