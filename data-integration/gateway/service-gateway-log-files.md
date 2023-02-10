---
title: Configure log files for the on-premises data gateway
description: Describes how to configure Gateway Log Retention for various versions of the On-Premise Data Gateway.
ms.topic: conceptual
ms.date: 02/09/2023
---
# Configure log files for the on-premises data gateway
There are three categories of service logs for an on-premises data gateway: information, error, and network. This categorization provides a troubleshooting experience that lets you focus on the specific area for an error or issue.

In order to check your logging configurations, please do:
1. Open the Gateway configuration file "Microsoft.PowerBI.EnterpriseGateway.exe.config", which by default should be located under "\Program Files\On-premises data gateway"
1. Before proceeding further, please make sure you do a copy of this file (just in case if you need to restore it back)
1. Locate the listener "ApplicationFileTraceListener" which will be under system.diagnostics

Please see the details below per retention type depending on your gateway version.

## Age based retention
With the introduction of the new age based retention concept within Gateway, starting with February 2023, this is the new default retention type for **new** gateway installations.

For this retention type, there are two main aspects to consider (in order of precedence):
 1. Maximum disk space to be consumed by Gateway logs (GatewayInfo*.log,GatewayError*.log,GatewayNetwork*.log), default value of 5Gb.
 1. Retention period in days, default value of 30 days.
 
In this new logic, we ensure that for every new day a new log file is provisioned to ensure the information of a given day is present in log files where the filename matches the log entry dates.
Also the file partition within the day is performed if the maximum individual file size (default of 100MB) is reached.

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

If you would like to change the retention default parameters values, you should adjust them within the **initializeData** value. Please find below the description of each parameter:
1. Retention period in days ( a value between 1 and 365 days)
2. Maximum total size in MB which can be consumed by the 3 log file types
3. Maximum size in MB which each log file can have individually (each time the limit is reached a new file will be created with an sequential number appended)

> [!NOTE] 
> Gateway logs are using UTC based timestamps, and the daily log file rotation will take place at 00:00 UTC.

## File count based retention
This was the default log retention logic within Gateway for versions December 2022 and earlier. This logic has two main concepts:

 1. Number of files to be retained per log type (GatewayInfo*.log, GatewayError*.log, GatewayNetwork*.log)
 1. Maximum disk space to be consumed per log type (GatewayInfo*.log, GatewayError*.log, GatewayNetwork*.log)

The files are partitioned accordingly with the criteria above, and therefore, whenever we reach the maximum number of files we will typically also be at or close to maximum disk space.

The following excerpt from the gateway configuration file *Microsoft.PowerBI.EnterpriseGateway.exe.config* contains the three categories: `GatewayInfo.log`, `GatewayErrors.log`, and `GatewayNetwork.log`.

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

## Will the new age based retention logic apply by default to my existing on-premises data gateway installation?
No. This retention logic for now is applied to completely new Gateway installations. Existing gateways while upgrading to February 2023 or later versions should keep their current log retention logic (File count based retention).

## Next steps

For information on how to export gateway logs for troubleshooting, go to [Troubleshooting tools](service-gateway-tshoot.md#troubleshooting-tools).
