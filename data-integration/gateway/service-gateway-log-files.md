---
title: Configure log files for the on-premises data gateway
description: Describes how to configure gateway log retention for various versions of the on-premises data gateway.
ms.topic: concept-article
ms.date: 07/16/2026
---
# Configure log files for the on-premises data gateway

The on-premises data gateway has three categories of service logs: information, error, and network. This categorization provides a troubleshooting experience that you can focus on the specific area for an error or issue.

To check your logging configurations, follow these steps:

1. Open the gateway configuration file `Microsoft.PowerBI.EnterpriseGateway.exe.config`. By default, you can find this file under `\Program Files\On-premises data gateway`.
1. Make a copy of this file in case you need to restore it later.
1. Find the listener `ApplicationFileTraceListener`, which is under `system.diagnostics`.

The following sections provide the configuration details per retention type, which depends on your gateway version.

## Age based retention

Starting in February 2023, the gateway introduces a new age based retention concept. This concept is the default retention type for **new** gateway installations.

For this retention type, consider two main aspects (in order of precedence):

* Maximum disk space for gateway logs (GatewayInfo*.log, GatewayError*.log, GatewayNetwork*.log), with a default value of 5 GB.
* Retention period in days, with a default value of 30 days.

In this new logic, the gateway ensures that for every new day it creates a new log file. This provisioning ensures the information for a given day is present in log files where the filename matches the log entry dates.
Also, the gateway performs file partitioning within the day if the maximum individual file size (default of 100 MB) is reached.

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

To change the retention default parameter values, adjust the `initializeData` value. The following list describes each parameter:

* Retention period in days (a value between 1 and 365 days).
* Maximum total size in MB that the three log file types can consume.
* Maximum size in MB that each log file can have individually. Each time the limit is reached, the gateway creates a new file with a sequential number appended.

> [!NOTE]
> Gateway logs use UTC based timestamps, and the daily log file rotation takes place at 00:00 UTC.

## File count based retention

This style was the default log retention logic within a gateway for versions December 2022 and earlier. This logic has two main concepts:

* Number of files to retain per log type (GatewayInfo*.log, GatewayError*.log, GatewayNetwork*.log).
* Maximum disk space to consume per log type (GatewayInfo*.log, GatewayError*.log, GatewayNetwork*.log).

The files are partitioned according to these criteria. Therefore, whenever you reach the maximum number of files, you typically reach the maximum disk space.

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

The following example specifies that 20 log files are retained, and the sum total of all files in each category is no more than 50 MB in size:
 `GatewayInfo.log,GatewayErrors.log,GatewayNetwork.log,20,50`

## Does the new age based retention logic apply by default to my existing on-premises data gateway installation?

No. This retention logic currently applies to only new gateway installations. Existing gateways that upgrade to February 2023 or later versions keep their current log retention logic (file count based retention).

## Admin consent for gateway diagnostics (Preview)

Admin consent for gateway diagnostics is a feature that administrators use to explicitly control whether diagnostic data from on-premises data gateways is collected and sent to the cloud.

This feature introduces a consent-driven model to ensure that potentially sensitive data, such as Mashup logs, is only transmitted after administrative approval. It also enables future monitoring and diagnostics capabilities. For now, this feature is applicable to Dataflows Gen2 artifact only. For more information, see [Download detailed refresh logs](/fabric/data-factory/dataflows-gen2-monitor).

### How it works

Gateway administrators can enable diagnostics in the gateway settings. When you enable this setting, the gateway starts collecting and sending diagnostic data.

   :::image type="content" source="media/service-gateway-log-files/gateway-admin-consent.png" alt-text="Screenshot of gateway admin diagnostics consent." lightbox="media/service-gateway-log-files/gateway-admin-consent.png":::

Tenant administrators provide an extra layer of governance by controlling organization-wide consent for diagnostics. By default, gateway administrators can enable diagnostics without needing tenant-level approval. However, tenant administrators can revoke consent at any time to stop diagnostic data collection across all gateways in the organization.

If tenant-level consent is revoked, all gateways immediately stop sending diagnostic data, and any ongoing data transfer is terminated.

   :::image type="content" source="media/service-gateway-log-files/tenant-admin-consent-option.png" alt-text="Screenshot of tenant admin diagnostics consent option." lightbox="media/service-gateway-log-files/tenant-admin-consent-option.png":::

   :::image type="content" source="media/service-gateway-log-files/tenant-admin-consent-switch.png" alt-text="Screenshot of tenant admin diagnostics consent switch." lightbox="media/service-gateway-log-files/tenant-admin-consent-switch.png":::

For immediate enforcement, restarting the on-premises data gateway terminates any ongoing diagnostics uploads.

The service stores the gateway diagnostic data for 24 hours in an Azure Data Lake Storage managed by the service. After 24 hours, the data is no longer available for download.


## FAQs about Gateway diagnostics for on-premises data gateways in Fabric

The on-premises data gateways Diagnostics Settings helps collect detailed diagnostic logs for troubleshooting Fabric Dataflow Gen2 refresh operations. This section answers common questions about where uploaded logs are stored, what information is collected, who can access the logs, and whether storage has additional cost.

### What is the relationship between on-premises data gateways Diagnostics Settings and Dataflows?

The on-premises data gateways Diagnostics Settings currently only applies to Fabric Dataflow Gen2. When a Dataflow Gen2 refresh runs:

- The gateway collects diagnostic information required for troubleshooting.
- The system uploads relevant mashup logs to Microsoft-managed storage.
- The logs associate with the refresh execution.
- Users can download the detailed diagnostics from the Dataflow Gen2 refresh history experience.

**This capability might also support future diagnostic scenarios.**

### What logs are collected and uploaded?

Currently, on-premises data gateways Diagnostics Settings primarily uploads Mashup Engine logs associated with Fabric Dataflow Gen2 refresh operations.

Examples of collected information include:

- Dataflow Gen2 refresh execution details.
- Mashup engine diagnostics.
- Query processing and execution traces.


### Where are uploaded logs stored?

The tenant's Power BI or Fabric signup region determines the storage location. Microsoft-managed storage in the applicable tenant region stores the uploaded logs.

### Which Azure regions support this feature?

All Fabric-supported regions that offer the managed storage infrastructure support on-premises data gateways Diagnostics Settings. This feature isn't available in the Qatar region.


### Does the uploaded data contain sensitive information?

Yes. Uploaded diagnostics might contain information that customers consider sensitive. The feature is disabled by default. Review your organization's data handling and support policies before opting for on-premises data gateways Diagnostics settings.

### How long are logs stored?

The system retains diagnostic data for 24 hours. You can download data from Fabric Dataflow Gen2 runs during this 24-hour period.


### Who can access uploaded logs?

Access is tightly controlled. Microsoft personnel don't routinely access uploaded logs. Access is restricted by default and granted only when necessary under approved operational procedures.

### Is there any additional cost for storing these logs?

No. As of today, on-premises data gateways Diagnostics Settings is provided at no extra cost.

## Related content

For information on how to export gateway logs for troubleshooting, see [Troubleshooting tools](service-gateway-tshoot.md#troubleshooting-tools).
