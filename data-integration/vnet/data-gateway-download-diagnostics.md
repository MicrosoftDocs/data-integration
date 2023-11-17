---
title: Download logs on the VNet data gateway
description: Provides information about how to download and interpret virtual network (VNet) data gateways logs.
ms.topic: conceptual
ms.date: 11/17/2023
---

# Download logs on the VNet data gateway

Logs for your VNET data gateway are available for download on the manage connections and gateways page. Three folders are downloaded:

- System Counters
- Mashup Logs
- Query Execution Report

## Notes:

- You must be an admin on the VNet data gateway to download logs. Check the [manage users](manage-data-gateways.md) option to see if you are an admin.
- The gateway must be online to provide logs. Check the status of the VNet by selecting the icon in the "Status" column. 
- If you don’t see the download, check to make sure pop-ups aren't disabled on your browser.
- This feature isn't available in certain regions, including Sweden central, Poland central, China regions, US Gov Virginia regions, and nateast.

## How to download logs

1. From the page header in the [Power BI service](https://app.powerbi.com), select the **Settings** icon and then select **Manage connections and gateways**.
2. Select the **Virtual network data gateways** tab.
3. Find your VNet data gateway and, in the same row, select the download icon in the **Download diagnostics** column.
4. Open the downloaded folder to view the logs.

## SystemCounters

| Attribute | Description |
| --- | --- |
| Timestamp | The time the counter was emitted. |
| Id | Unique identifier for the container on which your gateway is currently running. |
| CommittedMemoryinMB | Memory used out of the total 2GB RAM reserved per VNET. |
| CPUUsagePercentage | CPU used. |
| MemoryAvailableinMB | Memory available. |

## MashupLogs

| Attribute | Description |
| --- | --- |
| Start | Start of action. |
| Action | Action name. |
| ProductVersion | Version of Mashup. |
| ActivityId | Activity identifier. |
| CorrelationId | Correlation identifier. |
| Process | Process name. |
| Pid | Process identifier. |
| Tid | Thread identifier. |
| Duration | Duration of action. |

## QueryExecutionReport

| Attribute | Description |
| --- | --- |
| Id | Gateway object identifier. |
| Timestamp | Start of the query execution. |
| QueryId | Query identifier. |
| InstanceId | Identifier for the container on which your gateway is currently running. |
| RequestId | Request identifier. |
| QueryType | Query type, that is, DirectQuery, PollingModeQuery. |
| ConnectionPath | Data source kinds and paths. |
| Status | Indicates whether the query failed or succeeded. |
| StartTime | Start of the query execution. |
| DurationMS | Duration of the query in milliseconds. |
| ExecutionStartTime | Start of the query execution. |
| ExecutionDurationMS | Duration of the query in milliseconds. |
| DataReadingAndSerializationStartTime | Start of data serialization. |
| DataReadingAndSerializationDurationMS | Duration of the data serialization. |
| StreamingDurationMS | Duration of the data streaming. |
