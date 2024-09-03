---
title: Download logs on the VNet data gateway
description: This document provides information about how to download and interpret virtual network (VNet) data gateways logs.
ms.topic: conceptual
ms.date: 05/06/2024
---

# Download logs on the virtual network (VNET) data gateway (preview)

Logs for your VNET data gateway are available for download on the **Manage connections and gateways** page. Three folders are downloaded:

- System Counters
- Mashup Logs
- Query Execution Report

## Notes:

- You must be an admin on the VNet data gateway to download logs. Check the [manage users](manage-data-gateways.md) option to see if you're an admin.
- Retention of logs: MashupLogs are kept for the past 48 hours. The SystemCounters and QueryExecutionReport logs are kept for the past 29 days. Currently, customers don't have the ability to change how long the logs are retained.
- The gateway must be online to provide logs. Check the status of the VNet by selecting the icon in the "Status" column. 
- If you don’t see the download, check to make sure pop-ups aren't disabled on your browser.
- This feature isn't available in certain regions, including Mexico central, Spain central, Qatar central, China regions, and US Gov Virginia regions.
- Mashup logs are in JSONL format, while SystemCounters and QueryExecutionReport are in Parquet format.

## How to download logs

1. From the page header in the [Power BI service](https://app.powerbi.com), select the **Settings** icon and then select **Manage connections and gateways**.
2. Select the **Virtual network data gateways** tab.
3. Find your VNet data gateway and, in the same row, select the download icon in the **Download diagnostics** column.
4. To view the logs, open the downloaded folder.

## SystemCounters

| Attribute | Description |
| --- | --- |
| Timestamp | The time the counter was emitted. |
| ID | Unique identifier for the container on which your gateway is currently running. |
| CommittedMemoryinMB | Memory used out of the total 8-GB RAM reserved per VNET. |
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
| ID | Gateway object identifier. |
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
