---
title: Configure log files for the on-premises data gateway
description: Describes ways to configure how gateway logging data is stored.
ms.topic: conceptual
ms.date: 11/17/2022
---

# Configure log files for the on-premises data gateway

There are three categories of service logs for an on-premises data gateway: information, error, and network. This categorization provides a troubleshooting experience that lets you focus on the specific area for an error or issue. The following excerpt from the gateway configuration file *Microsoft.PowerBI.EnterpriseGateway.exe.config* contains the three categories: `GatewayInfo.log`, `GatewayErrors.log`, and `GatewayNetwork.log`.

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

By default, the gateway configuration file is located in the directory *\Program Files\On-premises data gateway*. To set the number of log files to retain, change the first number in the file's **initializeData** value. To configure the size of each log file, change the second number.

The following example specifies that 20 log files, the sum total of all files in each category being no more than 50 MB in size, will be retained:

 `GatewayInfo.log,GatewayErrors.log,GatewayNetwork.log,20,50`

## Next steps

For information on how to export gateway logs for troubleshooting, go to [Troubleshooting tools](service-gateway-tshoot.md#troubleshooting-tools).
