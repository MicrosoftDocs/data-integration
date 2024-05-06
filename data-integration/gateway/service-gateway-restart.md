---
title: Restart an on-premises data gateway
description: Learn how to restart the gateway Windows service.
ms.topic: conceptual
ms.date: 05/06/2024
---

# Restart an on-premises data gateway

Restart the on-premises data gateway service with any of the following methods.

* In the [gateway app](service-gateway-app.md), select **Service Settings**, then select **Restart now**.

    :::image type="content" source="media/service-gateway-restart/restart-gateway.png" alt-text="Restarting from the gateway app.":::

* In the services app, select the gateway service and then restart.

    :::image type="content" source="media/service-gateway-restart/service-restart.png" alt-text="Restarting from the services app.":::

* In an admin Command Prompt window, use the following commands.

    `net stop PBIEgwService`

    `net start PBIEgwService`

## Next steps

* [Tenant level administration](/power-platform/admin/onpremises-data-gateway-management)
