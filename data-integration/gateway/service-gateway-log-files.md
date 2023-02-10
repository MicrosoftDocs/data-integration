---
title: Configure log files for the on-premises data gateway
description: Describes how to configure gateway log retention for various versions of the on-premise data gateway.
ms.topic: conceptual
ms.date: 02/09/2023
---
# Configure log files for the on-premises data gateway

There are three categories of service logs for an on-premises data gateway: information, error, and network. This categorization provides a troubleshooting experience that lets you focus on the specific area for an error or issue.

In order to check your logging configurations, take the following steps:

1. Open the gateway configuration file Microsoft.PowerBI.EnterpriseGateway.exe.config, which by default should be located under \Program Files\On-premises data gateway.
1. Before proceeding further, make a copy of this file just in case you need to restore it later.
1. Locate the listener `ApplicationFileTraceListener` which is under `system.diagnostics`.

The following sections provide the configuration details per retention type, which depends on your gateway version.

## Age based retention

With the introduction of the new age based retention concept within a gateway, starting in February 2023, this is the new default retention type for **new** gateway installations.

For this retention type, there are two main aspects to consider (in order of precedence):

 * Maximum disk space to be consumed by gateway logs (GatewayInfo*.log, GatewayError*.log, GatewayNetwork*.log), with a default value of 5 GB.
 * Retention period in days, with a default value of 30 days.
 
In this new logic, we ensure that for every new day a new log file is provisioned to ensure the information of a given day is present in log files where the filename matches the log entry dates.
Also the file partition within the day is performed if the maximum individual file size (default of 100 MB) is reached.

```xml
  <system.diagnostics>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <remove name="Default" />
        <add name="ApplicationFileTraceListener" type="Microsoft.PowerBI.DataMovement.Pipeline.Common.Diagnostics.AgeBasedRetentionRotatableFilesManagerTraceListener, Microsoft.PowerBI.DataMovement.Pipeline.Common" initializeData="%LOCALAPPDATA%\Microsoft\On-premises data gateway\,30,5120,100" />
      </listeners>
    </trace>
  </system.diagnostics>
```

If you would like to change the retention default parameters values, you should adjust them in the `initializeData` value. The following list describes each parameter:

* Retention period in days (a value between 1 and 365 days).
* Maximum total size in MB which can be consumed by the three log file types.
* Maximum size in MB which each log file can have individually. Each time the limit is reached, a new file is created with an sequential number appended.

> [!NOTE] 
> Gateway logs use UTC based timestamps, and the daily log file rotation will take place at 00:00 UTC.

## File count based retention

This was the default log retention logic within a gateway for versions December 2022 and earlier. This logic has two main concepts:

 * Number of files to be retained per log type (GatewayInfo*.log, GatewayError*.log, GatewayNetwork*.log).
 * Maximum disk space to be consumed per log type (GatewayInfo*.log, GatewayError*.log, GatewayNetwork*.log).

The files are partitioned accordingly with the previously listed criteria, and therefore, whenever we reach the maximum number of files we will typically also be at or close to maximum disk space.

The following excerpt from the gateway configuration file Microsoft.PowerBI.EnterpriseGateway.exe.config contains the three categories: `GatewayInfo.log`, `GatewayErrors.log`, and `GatewayNetwork.log`.

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

By default, the gateway configuration file is located in the directory \Program Files\On-premises data gateway. To set the number of log files to retain, change the first number in the file's `initializeData` value. To configure the size of each log file, change the second number.

The following example specifies that 20 log files, the sum total of all files in each category being no more than 50 MB in size, will be retained:
 `GatewayInfo.log,GatewayErrors.log,GatewayNetwork.log,20,50`

## Will the new age based retention logic apply by default to my existing on-premises data gateway installation?

No. This retention logic for now is applied to completely new gateway installations. Existing gateways while upgrading to February 2023 or later versions should keep their current log retention logic (file count based retention).

## Next steps

For information on how to export gateway logs for troubleshooting, go to [Troubleshooting tools](service-gateway-tshoot.md#troubleshooting-tools).
