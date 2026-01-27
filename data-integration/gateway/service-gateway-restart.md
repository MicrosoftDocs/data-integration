---
title: Restart an on-premises data gateway
description: Learn how to restart the gateway Windows service.
ms.topic: how-to
ms.date: 6/26/2025
---

# Restart an on-premises data gateway

Restart the on-premises data gateway service with any of the following methods.

* In the [gateway app](service-gateway-app.md), select **Service Settings**, then select **Restart now**.

    :::image type="content" source="media/service-gateway-restart/restart-gateway.png" alt-text="Screenshot of the gateway app with the Restart now option emphasized.":::

* In the services app, select the gateway service and then restart.

    :::image type="content" source="media/service-gateway-restart/service-restart.png" alt-text="Screenshot of the Windows Services app where you restart the gateway.":::

* In an admin Command Prompt window, use the following commands.

    `net stop PBIEgwService`

    `net start PBIEgwService`

## Related content

* [Tenant level administration](/power-platform/admin/onpremises-data-gateway-management)
