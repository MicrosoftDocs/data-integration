---
title: Monitor and optimize on-premises data gateway performance
description: This article provides ways for you to monitor and optimize the performance of the on-premises data gateway activities.
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

# Monitor and optimize on-premises data gateway performance

[!INCLUDE [gateway-rewrite](../includes/gateway-rewrite.md)]

## Monitor performance

<iframe width="560" height="315" src="https://www.youtube.com/embed/IJ_DJ30VNk4?showinfo=0" frameborder="0" allowfullscreen></iframe>

### Performance counters

There are a number of performance counters that you can use to gauge the activities for the gateway. It can be helpful to understand these counters, especially if you have a large load of activity and need to make a new gateway. These counters don't reflect how long something takes.

You can access these counters through the Windows Performance Monitor tool.

![Access counters through the Windows Performance Monitor tool](media/service-gateway-performance/gateway-perfmon.png)

There are general groupings of these counters.

| Counter type | Description |
| --- | --- |
| ADO.NET |This counter type is used for any DirectQuery connection. |
| ADOMD |This counter type is used for SQL Server 2014 Analysis Services and earlier. |
| OLEDB |Certain data sources use this counter type. Examples include SAP HANA and SQL Server 2016 Analysis Services or later. |
| Mashup |This counter type includes any imported data source. If you're scheduling refresh or doing an on-demand refresh, it goes through the Mashup Engine. |

Here's a list of the available performance counters.

| Counter | Description |
| --- | --- |
| # of ADO.NET open connection executed / sec |Number of ADO.NET open connection actions executed per second (succeeded or failed). |
| # of ADO.NET open connection failed / sec |Number of ADO.NET open connections actions failed per second. |
| # of ADO.NET queries executed / sec |Number of ADO.NET queries executed per second (succeeded or failed). |
| # of ADO.NET queries failed / sec |Number of ADO.NET failed queries executed per second. |
| # of ADOMD open connection executed / sec |Number of ADOMD open connection actions executed per second (succeeded or failed). |
| # of ADOMD open connection failed / sec |Number of ADOMD open connection actions failed per second. |
| # of ADOMD queries executed / sec |Number of ADOMD queries executed per second (succeeded or failed). |
| # of ADOMD queries failed / sec |Number of ADOMD failed queries executed per second. |
| # of all open connection executed / sec |Number of open connection actions executed per second (succeeded or failed). |
| # of all open connection failed / sec |Number of failed open connection actions executed per second. |
| # of all queries executed / sec |Number of queries executed per second (succeeded or failed). |
| # of items in the ADO.NET connection pool |Number of items in the ADO.NET connection pool. |
| # of items in the OLEDB connection pool |Number of items in the OLEDB connection pool. |
| # of items in the Service Bus pool |Number of items in the Azure Service Bus pool. |
| # of Mashup open connections executed / sec |Number of Mashup open connection actions executed per second (succeeded or failed). |
| # of Mashup open connections failed / sec |Number of Mashup open connection actions failed per second. |
| # of Mashup queries executed / sec |Number of Mashup queries executed per second (succeeded or failed). |
| # of Mashup queries failed / sec |Number of Mashup failed queries executed per second. |
| # of OLEDB multiple result set queries failed / sec |Number of multiple result sets of OLEDB failed queries executed per second. |
| # of OLEDB multiple result sets of queries executed / sec |Number of OLEDB multiple result sets of queries executed per second (succeeded or failed). |
| # of OLEDB open connection executed / sec |Number of OLEDB open connection actions executed per second (succeeded or failed). |
| # of OLEDB open connection failed / sec |Number of OLEDB open connection actions failed per second. |
| # of OLEDB queries executed / sec |Number of OLEDB multiple result sets of queries executed per second (succeeded or failed). |
| # of OLEDB queries failed / sec |Number of OLEDB multiple result sets of failed queries executed per second. |
| # of OLEDB single result set queries executed / sec |Number of OLEDB single result set queries executed per second (succeeded or failed). |
| # of queries failed / sec |Number of failed queries executed per second. |
| # of single result set OLEDB queries failed / sec |Number of single result set OLEDB failed queries executed per second. |

## Slow-performing queries

Long-running queries might require additional modification on your data source or further optimization of the query itself. This could be either for direct database queries, like Power BI DirectQuery, PowerApps, or Azure Logic Apps, or for Power BI refreshes.

By default, the gateway performs basic logging. If you're investigating slow-performing queries and need more information about query connection details, you can temporarily enable **Additional logging** to gather additional log information. To do this, in the [on-premises data gateway app](service-gateway-app.md) select **Diagnostics** > **Additional logging**.

![Turn on additional logging](media/service-gateway-performance/additional-logging.png)

Enabling this setting likely will increase the log size significantly, based on gateway usage. We recommend that after you finish reviewing the logs that you disable additional logging. We don't recommend leaving this setting enabled during normal gateway usage.

## Gateway performance monitoring (public preview)

To monitor performance, gateway admins have traditionally depended on manually monitoring performance counters through the Windows Performance Monitor tool. We now offer additional query logging and a [Gateway Performance PBI template file](https://download.microsoft.com/download/D/A/1/DA1FDDB8-6DA8-4F50-B4D0-18019591E182/GatewayPerformanceMonitoring.pbit) to visualize the results. This feature provides new insights into gateway usage. You can use it to troubleshoot slow-performing queries.

> [!NOTE]
> This feature is currently available only for the on-premises data gateway in the standard mode. It's not available for the personal mode.

### Enable performance logging

To enable this feature, make the following changes to the *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* file in the *\Program Files\On-premises data gateway* folder.

1. Update **QueryExecutionReportOn** to _True_ to enable additional logging for queries executed using the gateway. Enabling this option creates both the Query Execution Report and the Query Execution Aggregation Report files.

   ``` xml
   <setting name="QueryExecutionReportOn" serializeAs="String">
     <value>True</value>
   </setting>
   ```

1. Update **SystemCounterReportOn** to _True_ to enable additional logging for memory and CPU system counters. Enabling this option creates the System Counter Aggregation Report file.

   ```xml
   <setting name="SystemCounterReportOn" serializeAs="String">
     <value>True</value>
   </setting>
   ```

1. There are other values in the config file that you can update as needed:

    - **ReportFilePath**: Determines the path where the three log files are stored. By default, this path is either *\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\Report* or *Windows\ServiceProfiles\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\Report*. The path depends on the OS version. If you use a service account for the gateway other than _PBIEgwService_, replace this part of the path with the service account name.
    - **ReportFileCount**: Determines the number of log files of each kind to retain. The default value is 10.
    - **ReportFileSizeInBytes**: Determines the size of the file to maintain. The default value is 104,857,600.
    - **QuerExecutionAggregationTimeInMinutes**: Determines the number of minutes for which the query execution information is aggregated. The default value is 5.
    - **SystemCounterAggregationTimeInMinutes**: Determines the number of minutes for which the system counter is aggregated. The default value is 5.

1. After you make the changes to the config file, restart the gateway for these config values to take effect. You now see the report files being generated in the location that you specified for **ReportFilePath**.

    > [!NOTE]
    > It can take up to 10 minutes plus the amount of time set for **QuerExecutionAggregationTimeInMinutes** in the config file until files start to show up in the folder.

### Understand performance logs

When you turn this feature on, three new log files are created:

- The Query Execution Report
- The Query Execution Aggregation Report
- The System Counter Aggregation Report

The Query Execution Report contains detailed query execution information. The following attributes are captured.

|Attribute |Description |
| ---- | ---- |
|**GatewayObjectId** |Unique identifier for the gateway. |
|**RequestId** |Unique identifier for a gateway request. It could be the same for multiple queries. |
|**DataSource** |Contains both the data source type and data source. |
|**QueryTrackingId** |Unique identifier for a query. | 
|**QueryExecutionEndTimeUTC** |Time when the query execution completed. |
|**QueryExecutionDuration** (ms) |Duration for a query execution. |
|**QueryType** |Type of query. For instance, the query passed could be a Power BI refresh or DirectQuery. Or, it could be queries from PowerApps and Microsoft Flow. |
|**DataProcessingEndTimeUTC** |Time when data processing activities like spooling, data retrieval, compression, and data processing completed. |
|**DataProcessingDuration** (ms) |Duration for data processing activities like spooling, data retrieval, compression, and data processing. |
|**Success** |Indicates if the query succeeded or failed. |
|**ErrorMessage** |If the query failed, indicates the error message. |
| | |

The Query Execution Aggregation Report contains query information aggregated to a time interval by **GatewayObjectId**, **DataSource**, **Success**, and **QueryType**. The default value is 5 minutes, but you can adjust it. The following attributes are captured.

|Attribute |Description |
| ---- | ---- |
|**GatewayObjectId** |Unique identifier for the gateway. |
|**AggregationStartTimeUTC** |Start of the time window for which query attributes were aggregated. |
|**AggregationEndTimeUTC** |End of the time window for which query attributes were aggregated. |
|**DataSource** |Contains both the data source type and data source. |
|**Success** |Indicates if the query succeeded or failed. |
|**AverageQueryExecutionDuration** (ms) |Average query execution time for the aggregation time window. |
|**MaxQueryExecutionDuration** (ms) |Maximum query execution time for the aggregation time window. |
|**MinQueryExecutionDuration** (ms) |Minimum query execution time for the aggregation time window. |
|**QueryType** |Type of query. For instance, the query passed could be a Power BI refresh or DirectQuery. Or, it could be queries from PowerApps and Microsoft Flow. |
|**AverageDataProcessingDuration** (ms) |Average time for data processing activities like spooling, data retrieval, compression, and data processing for the aggregation time window. |
|**MaxDataProcessingDuration** (ms) |Maximum time for data processing activities like spooling, data retrieval, compression, and data processing for the aggregation time window. |
|**MinDataProcessingDuration** (ms) |Minimum time for data processing activities like spooling, data retrieval, compression, and data processing for the aggregation time window. |
|**Count** |Number of queries. |
| | |

The System Counter Aggregation Report contains system counter values aggregated to a time interval. The default value is 5 minutes, but you can adjust it. The following attributes are captured.

|Attribute |Description |
| ---- | ---- |
|**GatewayObjectId** |Unique identifier for the gateway. |
|**AggregationStartTimeUTC** |Start of the time window for the system counters that were aggregated. |
|**AggregationEndTimeUTC** |End of the time window for the system counters that were aggregated. |
|**CounterName** |System counters, which includes memory and CPU usage by the gateway, Mashup Engine, and overall by the machine hosting the gateway. |
|**Max** |Maximum value for the system counter for the aggregation time window. |
|**Min** |Minimum value for the system counter for the aggregation time window. |
|**Average** |Average value for the system counter for the aggregation time window. |
| | |

### Visualize gateway performance

Now, you can visualize the data that's in the log files.

1. Download the [Gateway Performance PBI template](https://download.microsoft.com/download/D/A/1/DA1FDDB8-6DA8-4F50-B4D0-18019591E182/GatewayPerformanceMonitoring.pbit), and open it by using Power BI Desktop.

1. In the dialog box that opens, check that the folder path matches the value in **ReportFilePath**.

    ![Pop-up for the folder path](media/service-gateway-performance/gateway-folder-path-pop-up.png)

1. Select **Load**, and the template file starts loading the data from your log files. All visuals are populated by using the data in the reports.

1. Optionally, save this file as a PBIX, and publish it to your service for automatic refreshes.

You also can customize this template file to suit your needs. For more information on Power BI templates, see this [Microsoft Power BI blog post](https://powerbi.microsoft.com/en-us/blog/deep-dive-into-query-parameters-and-power-bi-templates/).

## Next steps

* [Troubleshooting tools](service-gateway-tshoot.md#troubleshooting-tools)
