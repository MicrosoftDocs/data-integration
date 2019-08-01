---
title: Configure log files for the on-premises data gateway
description: Describes ways to configure how gateway logging data is stored.
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

# Configure log files for the on-premises data gateway

[!INCLUDE [gateway-rewrite](../includes/gateway-rewrite.md)]

There are three categories of services logs for an on-premises data gateway: information, error, and network. This categorization provides a troubleshooting experience that, depending on the error or issue, lets you focus on a specific area. You can see the three categories `GatewayInfo.log`, `GatewayErrors.log`, and `GatewayNetwork.log` in the following snippet from the gateway configuration file *Microsoft.PowerBI.EnterpriseGateway.exe.config*.

```xml
  <system.diagnostics>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <remove name="Default" />
        <add name="ApplicationFileTraceListener"
             type="Microsoft.PowerBI.DataMovement.Pipeline.Common.Diagnostics.RotatableFilesManagerTraceListener, Microsoft.PowerBI.DataMovement.Pipeline.Common"
             initializeData="%LOCALAPPDATA%\Microsoft\On-premises data gateway\,GatewayInfo.log,GatewayErrors.log,GatewayNetwork.log,20,50" />
      </listeners>
    </trace>
  </system.diagnostics>
```

By default, the gateway configuration file is located at *\Program Files\On-premises data gateway*. To set the number of log files to retain, change the first number in the file's **initializeData** value. To configure the size of each log file, change the second number.

The following example specifies that 20 log files, each 50 MB in size, will be retained:

 `GatewayInfo.log,GatewayErrors.log,GatewayNetwork.log,20,50`

## Next steps

For information on how to export gateway logs for troubleshooting, see [Troubleshooting tools](service-gateway-tshoot.md#troubleshooting-tools).
