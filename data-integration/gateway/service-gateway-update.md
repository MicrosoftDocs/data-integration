---
title: Update an on-premises data gateway
description: Describes how to update to the latest version of the on-premises data gateway.
ms.topic: conceptual
ms.date: 05/06/2024
---

# Update an on-premises data gateway

We release an update every month for on-premises data gateways. Each of these updates includes new features along with the latest Mashup Engine.

> [!NOTE]
>Currently, Microsoft actively supports only the last six releases of the on-premises data gateway. We release a new update for data gateways every month.

We recommend that you update gateway members one after the other in a timely manner. This process reduces sporadic failures as a query may succeed on one gateway member, but not on the other, based on disparity in capabilities across different versions.

Use the following steps when updating a gateway cluster with two or more members:

1. Disable one gateway member.
2. Wait for ongoing work to be completed. A waiting period of 30 minutes is sufficient for most workloads, however clusters frequently running critical long running jobs may require more time for requests to drain.
3. Update the gateway member.
4. Enable the updated gateway member.
5. Repeat step 1-4 until all gateway members are updated.

Disabling a gateway makes sure the load balancer doesn't try to execute queries on the member you're updating, hence reducing delays and failures.

## Update a gateway

To update a gateway:

1. Download the latest [standard mode gateway](https://go.microsoft.com/fwlink/?LinkId=2116849&clcid=0x409) or [personal mode gateway](https://go.microsoft.com/fwlink/?LinkId=2116848&clcid=0x409) and run the installation program. If the version you're trying to install isn't newer than the version already installed, you'll receive one of the following error messages.

   ![The update version is the same as the installed version.](media/service-gateway-update/gateway-same-version.png)

   ![The update version is older than the installed version.](media/service-gateway-update/gateway-old-version.png)

1. If you install a newer version, you'll be prompted to update. Select **Update** to begin updating.

   ![Getting ready to update.](media/service-gateway-update/update-getting-ready.png)

1. After the installation finishes, select **Sign in**.

   ![Gateway update sign-in.](media/service-gateway-update/gateway-update-signin.png)

The gateway update is now complete.

![The gateway update is complete.](media/service-gateway-update/gateway-update-complete.png)

## Next steps

* [Monitor and optimize gateway performance](service-gateway-performance.md)
