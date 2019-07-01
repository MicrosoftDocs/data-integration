---
title: Monitor and optimize gateway performance
description: This article provides ways for you to monitor and optimize the performance of the on-premises data gateway activities.
author: mgblythe
ms.author: mblythe
manager: kfile
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-gateways
ms.topic: conceptual
ms.date: 04/19/2019
LocalizationGroup: Gateways 
---

# Monitor and optimize gateway performance

## Monitor Performance

<iframe width="560" height="315" src="https://www.youtube.com/embed/IJ_DJ30VNk4?showinfo=0" frameborder="0" allowfullscreen></iframe>

### Performance Counters

There are a number of performance counters that can be used to gauge the activities for the gateway. These can be helpful to understand if you have a large load of activity and might need to make a new gateway. These counters do not reflect how long something takes.

These counters can be accessed through the Windows Performance Monitor tool.

![Access counters through the Windows Performance Monitor tool](media/service-gateway-performance/gateway-perfmon.png)

There are general groupings of these counters.

| Counter Type | Description |
| --- | --- |
| ADO.NET |This is used for any DirectQuery connection. |
| ADOMD |This is used for Analysis Services 2014 and earlier. |
| OLEDB |Certain data sources use this. This includes SAP HANA and Analysis Service 2016 or later. |
| Mashup |This includes any imported data source. If you are scheduling refresh or doing an on-demand refresh, it goes through the mashup engine. |

Here is a listing of the available performance counters.

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
| # of items in the Service Bus pool |Number of items in the Service Bus pool. |
| # of Mashup open connection executed / sec |Number of Mashup open connection actions executed per second (succeeded or failed). |
| # of Mashup open connection failed / sec |Number of Mashup open connection actions failed per second. |
| # of Mashup queries executed / sec |Number of Mashup queries executed per second (succeeded or failed). |
| # of Mashup queries failed / sec |Number of Mashup failed queries executed per second |
| # of OLEDB multiple result set queries failed / sec |Number of multiple result sets of OLEDB failed queries executed per second. |
| # of OLEDB multiple result sets of queries executed / sec |Number of OLEDB multiple result sets of queries executed per second (succeeded or failed). |
| # of OLEDB open connection executed / sec |Number of OLEDB open connection actions executed per second (succeeded or failed). |
| # of OLEDB open connection failed / sec |Number of OLEDB open connection actions failed per second. |
| # of OLEDB queries executed / sec |Number of OLEDB multiple result sets of queries executed per second (succeeded or failed). |
| # of OLEDB queries failed / sec |Number of OLEDB multiple result sets of failed queries executed per second. |
| # of OLEDB single result set queries executed / sec |Number of OLEDB single result set queries executed per second (succeeded or failed). |
| # of queries failed / sec |Number of failed queries executed per second. |
| # of single result set OLEDB queries failed / sec |Number of single result set OLEDB failed queries executed per second. |

## Slow performing queries

Long-running queries might require additional modification on your data source or further optimization of the query itself. This could be either for direct database queries (like Power BI DirectQuery/PowerApps/Logic Apps) or Power BI refreshes.

By default the gateway performs basic logging. If you're investigating slow performing queries and need more information about query connection details, you can temporarily enable Additional logging to gather additional log information. To do this, in the [on-premises data gateway app](service-gateway-app.md) select **Diagnostics** > **Additional logging**.

![Turn additional logging on](media/service-gateway-performance/additional-logging.png)

Enabling this setting likely will increase the log size significantly, based on gateway usage. We recommend that once you're done reviewing the logs, you disable additional logging. We don't recommend leaving this setting enabled during normal gateway usage.

## Gateway performance monitoring (public preview)

To monitor performance, gateway admins have traditionally depended on manually monitoring performance counters through the Windows Performance Monitor tool. We now offer additional query logging and a [Gateway Performance PBI template file](http://download.microsoft.com/download/D/A/1/DA1FDDB8-6DA8-4F50-B4D0-18019591E182/GatewayPerformanceMonitoring.pbit) to visualize the results. This feature provides new insights into gateway usage and allows you to troubleshoot slow performing queries.

> [!NOTE]
> This feature is currently available only for the on-premises data gateway in the standard mode and not for the personal mode.

### Enable performance logging

To enable this feature, make the following changes to the *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* file in the "\Program Files\On-premises data gateway" folder:

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

1. There are other values in the config file that you can update as needed.

    - **ReportFilePath**: Determines the path where the three log files are stored. By default, this path is either "\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\Report" or "Windows\ServiceProfiles\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\Report", depending on the OS version. If you use a service account for the gateway other than _PBIEgwService_, replace this part of the path with the service account name.
    - **ReportFileCount**: Determines the number of log files of each kind to retain. The default value is 10.
    - **ReportFileSizeInBytes**: Determines the size of the file to maintain. The default value is 104857600.
    - **QuerExecutionAggregationTimeInMinutes**: Determines the number of minutes for which the query execution information is aggregated. The default value is 5.
    - **SystemCounterAggregationTimeInMinutes**: Determines the number of minutes for which the system counters is aggregated. The default value is 5.

1. After you've made the changes to the config file, restart the gateway for these config values to take effect. You'll now start seeing the report files being generated in the location you specified for **ReportFilePath**.

    > [!NOTE]
    > It can take up to 10 minutes plus the amount of time set for **QuerExecutionAggregationTimeInMinutes** in the config file until files start showing up in the folder.

### Understand performance logs

When you turn this feature on, we create three new log files:

- The Query Execution Report
- The Query Execution Aggregation Report
- The System Counter Aggregation Report

The Query Execution Report contains detailed query execution information. We capture the following attributes:

|Attribute |Description |
| ---- | ---- |
|**GatewayObjectId** |Unique identifier for the gateway. |
|**RequestId** |Unique identifier for a gateway request. It could be the same for multiple queries. |
|**DataSource** |Contains both the data source type and data source. |
|**QueryTrackingId** |Unique identifier for a query. |  
|**QueryExecutionEndTimeUTC** |Time when the query execution completed. |
|**QueryExecutionDuration**(ms) |Duration for a query execution. |
|**QueryType** |Type of query - for instance, the query passed could be a Power BI refresh/DirectQuery or queries from PowerApps and Microsoft Flow. |
|**DataProcessingEndTimeUTC** |Time when data processing activities like spooling, data retrieval, compression, data processing, and so on completed. |
|**DataProcessingDuration**(ms) |Duration for data processing activities like spooling, data retrieval, compression, data processing, and so on. |
|**Success** |Indicates if the query succeeded or failed. |
|**ErrorMessage** |If the query failed, indicates the error message. |
| | |

The Query Execution Aggregation Report contains query information aggregated to a time interval by **GatewayObjectId**, **DataSource**, **Success**, and **QueryType**. The default value is 5 minutes, but you can adjust it as described below. We capture the following attributes:

|Attribute |Description |
| ---- | ---- |
|**GatewayObjectId** |Unique identifier for the gateway. |
|**AggregationStartTimeUTC** |Start of the time window for which query attributes were aggregated. |
|**AggregationEndTimeUTC** |End of the time window for which query attributes were aggregated. |
|**DataSource** |Contains both the data source type and data source. |
|**Success** |Indicates if the query succeeded or failed. |
|**AverageQueryExecutionDuration**(ms) |Average query execution time for the aggregation time window. |
|**MaxQueryExecutionDuration**(ms) |Maximum query execution time for the aggregation time window. |
|**MinQueryExecutionDuration**(ms) |Minimum query execution time for the aggregation time window. |
|**QueryType** |Type of query - for instance, the query passed could be a Power BI refresh/DirectQuery or queries from PowerApps and Microsoft Flow. |
|**AverageDataProcessingDuration**(ms) |Average time for data processing activities like spooling, data retrieval, compression, data processing, and so on for the aggregation time window. |
|**MaxDataProcessingDuration**(ms) |Maximum time for data processing activities like spooling, data retrieval, compression, data processing, and so on for the aggregation time window. |
|**MinDataProcessingDuration**(ms) |Minimum time for data processing activities like spooling, data retrieval, compression, data processing, and so on for the aggregation time window. |
|**Count** |Number of queries. |
| | |

The System Counter Aggregation Report contains system counter values aggregated to a time interval. The default value is 5 minutes, but you can adjust it as described below. We capture the following attributes:

|Attribute |Description |
| ---- | ---- |
|**GatewayObjectId** |Unique Identifier for the gateway. |
|**AggregationStartTimeUTC** |Start of the time window for which system counters have been aggregated. |
|**AggregationEndTimeUTC** |End of the time window for which system counters have been aggregated. |
|**CounterName** |System counters, including memory and CPU usage by the gateway, mashup, and overall by the machine hosting the gateway. |
|**Max** |Maximum value for the system counter for the aggregation time window. |
|**Min** |Minimum value for the system counter for the aggregation time window. |
|**Average** |Average value for the system counter for the aggregation time window. |
| | |

### Visualize gateway performance

Now, you can visualize the data that's in the log files.

1. Download the [Gateway Performance PBI template](http://download.microsoft.com/download/D/A/1/DA1FDDB8-6DA8-4F50-B4D0-18019591E182/GatewayPerformanceMonitoring.pbit) and open it using Power BI desktop.

1. In the dialog box that opens, check that the folder path matches the value in **ReportFilePath**.

    ![Pop-up for the Folder path](media/service-gateway-performance/gateway-folder-path-pop-up.png)

1. Select **Load**, and the template file starts loading the data from your log files. All visuals should then be populated using the data in the reports.

1. Optionally save this file as a PBIX and publish it to your service for automatic refreshes.

Additionally, you can customize this template file to suit your needs. For more information on Power BI templates, see this [Microsoft Power BI Blog post](https://powerbi.microsoft.com/en-us/blog/deep-dive-into-query-parameters-and-power-bi-templates/).

## Next steps

* [Troubleshooting tools](service-gateway-tshoot.md#troubleshooting-tools)
