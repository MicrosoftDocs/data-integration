---
title: Update an on-premises data gateway
description: Describes how to update to the latest version of the on-premises data gateway.
author: arthiriyer
manager: kfile
ms.reviewer: ''
ms.technology: on-premises-data-gateway
ms.topic: conceptual
ms.date: 07/15/2019
ms.author: arthii
LocalizationGroup: Gateways

---

# Update an on-premises data gateway

We aim to release an update every month for on-premises data gateways. Each of these updates includes new features along with the latest Mashup Engine.

> [!NOTE]
> If you're running a gateway cluster, we recommend that you update all nodes in the cluster at the same time.

## Update a gateway

To update a gateway:

1. Download the latest [standard mode gateway](https://go.microsoft.com/fwlink/?LinkId=2116849&clcid=0x409) or [personal mode gateway](https://go.microsoft.com/fwlink/?LinkId=2116848&clcid=0x409) and run the installation program. If the version you're trying to install isn't newer than the version already installed, you'll receive one of the following error messages.

   ![The update version is the same as the installed version](media/service-gateway-update/gateway-same-version.png)

   ![The update version is older than the installed version](media/service-gateway-update/gateway-old-version.png)

1. If you install a newer version, you'll be prompted to update. Select **Update** to begin updating.

   ![Getting ready to update](media/service-gateway-update/update-getting-ready.png)

1. After the installation finishes, select **Sign in**.

   ![Gateway update sign-in](media/service-gateway-update/gateway-update-signin.png)

The gateway update is now complete.

![The gateway update is complete](media/service-gateway-update/gateway-update-complete.png)

## Next steps

* [Monitor and optimize gateway performance](service-gateway-performance.md)
