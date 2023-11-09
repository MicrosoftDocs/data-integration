---
title: Create virtual network (VNet) data gateways
description: Provides information about how to create virtual network (VNet) data gateways.
ms.topic: conceptual
ms.date: 07/14/2023
---

# Download logs on the VNet data gateway
Logs for your VNET data gateway are available for download on the manage connections and gateways page. Three folders are downloaded:

- the Mashup Logs
- the Query Execution Report
- the System Counters

## Notes:
1. You must be an admin on the VNet data gateway to download logs. Check the [manage users](https://learn.microsoft.com/en-us/data-integration/vnet/manage-data-gateways) option to see if you are an admin.
2. The gateway must be online to provide logs. Check the status of the VNet by clicking the icon in the “Status” column. 
3. If you don’t see the download, check to make sure pop-ups are not disabled on your browser.
4. This feature is not available in certain regions, including Sweden central, Poland central, China regions, us gov virginia reigons, nateast

## How to download logs
1. From the page header in the [Power BI service](https://app.powerbi.com), select the **Settings** icon and then select the manage connections and gateways page.
2. Click on the “virtual network data gateways” tab.
3. Find your VNet data gateway and, in the same row, click on the download icon in the column “Download diagnostics”.
4. Open the downloaded folder to view the logs.

SystemCounters
| Attribute | Description |
| Timestamp | The time the counter was emitted. |
| Id | Unique identifier for the container on which your gateway is currently running. |
| CommittedMemoryinMB | Memory used out of the total 2GB RAM reserved per VNET. |
| CPUUsagePercentage | CPU used. |
| MemoryAvailableinMB | Memory available. |

MashupLogs
| Attribute | Description |
| Start | Start of action. |
| Action | Action name. |
| ProductVersion | Version of Mashup. |
| ActivityId | Activity identifier. |
| CorrelationId | Correlation identifies. |
| Process | Process name. |
| Pid | Process id. |
| Tid | Thread id. |
| Duration | Duration of action. |

QueryExecutionReport
| Attribute | Description |
| Id | Gateway object identifier. |
| Timestamp | Start of the query execution. |
| QueryId | Query identifier. |
| InstanceId | Identifier for the container on which your gateway is currently running. |
| RequestId | Request identifier. |
| QueryType | Query type, ie. DirectQuery, PollingModeQuery. |
| ConnectionPath | Data source kinds and paths. |
| Status | Wether the query failed or succeeded. |
| StartTime | Start of the query execution. |
| DurationMS | Duration of the query in milliseconds. |
| ExecutionStartTime | Start of the query execution. |
| ExecutionDurationMS | Duration of the query in milliseconds. |
| DataReadingAndSerializationStartTime | Start of data serialization. |
| DataReadingAndSerializationDurationMS | Duration of the data serialization. |
| StreamingDurationMS | Duration of the data streaming. |