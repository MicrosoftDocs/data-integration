---
title: "Restart an on-premises gateway"
description: Learn how to restart the gateway Windows service.
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

# Restart an on-premises gateway

[!INCLUDE [gateway-rewrite](../includes/gateway-rewrite.md)]

The on-premises data gateway service can be restarted using multiple methods.

1. In the [on-premises data gateway app](service-gateway-app.md), select the **Service Settings** tab, then select **Restart now**.

    ![Select Restart now](media/service-gateway-restart/restart-gateway.png)

2. You can also restart the service from the services application. Find the on-premises data gateway service and restart.

    ![Select Restart now](media/service-gateway-restart/service-restart.png)

3. To restart the gateway from an admin command prompt, use the following commands:

    `net stop PBIEgwService`

    `net start PBIEgwService`

## Next steps

* [Tenant level administration](service-gateway-tenant-level-admin.md)
