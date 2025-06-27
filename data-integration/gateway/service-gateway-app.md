---
title: Use the on-premises data gateway app
description: Learn how to use the on-premises data gateway app to configure various services of your on-premises data gateway.
ms.topic: conceptual
ms.date: 6/10/2025
---

# Use the on-premises data gateway app

To open the on-premises data gateway app:

1. On the machine where the gateway is running, enter **gateway** in Windows search.

1. Select the **On-premises data gateway** app.

   :::image type="content" source="media/service-gateway-app/gateway-app-search.png" alt-text="Screenshot of the search match for the on-premises data gateway app.":::

   :::image type="content" source="media/service-gateway-app/opening-dialog.png" alt-text="Screenshot of the opening dialog of the on-premises data gateway app.":::

Some of the on-premises data gateway app features can be used only after you sign in to your Office 365 account. For example, under the **Service Settings** tab, you can restart the gateway without signing in, but you can't change the service account of your gateway without signing in.

:::image type="content" source="media/service-gateway-app/sign-on-actions.png" alt-text="Screenshot of example of actions that can and can't be taken without signing in.":::

> [!NOTE]
> Each cloud service that supports the gateway has its own administrative management page where you can configure the gateway and connections for use by that service. For more details, go to [Manage an on-premises data gateway](service-gateway-manage.md).

## On-premises data gateway app features

After you sign in to your Office 365 account, you have access to the following features in the on-premises data gateway app.

|Tab |Service |Description |
| ---- | ---- | ---- |
|Status |Status of the gateway cluster |Indicates whether your gateway is online, the version number of the gateway, and a list of any apps currently associated with the gateway. |
|Service Settings |Restart the gateway |Provides a way of [restarting the gateway](service-gateway-restart.md) whenever a restart is needed. |
|Service Settings |Gateway service account |By default, the gateway is configured to use *NT SERVICE\PBIEgwService* for the Windows service sign-in credential. You can change the [service account](service-gateway-service-account.md) to a domain user account within your Active Directory domain. Or, you can use a managed service account to avoid having to change the password. |
|Diagnostics |Additional logging |Turning on this feature provides [more verbose information in the log file](service-gateway-performance.md#slow-performing-queries), which includes duration information. This information can be useful in figuring out why some responses through the gateway are slow. Enabling this feature could increase the log size significantly depending on gateway usage. So, we recommend that you don't leave this setting enabled long term. |
|Diagnostics |Gateway logs |Provides a [copy of all of the gateway logs](service-gateway-tshoot.md#troubleshooting-tools) in a single file in .zip format. |
|Diagnostics |Network ports test |Checks if the gateway has [access to all required ports](service-gateway-communication.md#network-ports-test). |
|Network |Network status |Indicates whether the gateway can reach outside your network. The network status is displayed as either Connected or Disconnected. |
|Network |HTTPS mode |Forces the gateway to communicate with Azure Relay by using [HTTPS instead of TCP](service-gateway-communication.md#force-https-communication-with-azure-relay) when turned on. |
|Connectors |Custom data connectors | You can connect to and access data from Power BI by using custom data connectors that you develop. |
|Recovery Keys |Recovery Keys |Changes the [recovery key](service-gateway-recovery-key.md) you specified when installing the on-premises data gateway. This feature doesn't appear until you sign in. Not available in the on-premises data gateway (personal mode).|

## Related content

* [Troubleshoot the on-premises data gateway](service-gateway-tshoot.md)
