---
title: Adjust gateway performance based on server CPU
description: This article provides ways for you to monitor and optimize the performance of the on-premises data gateway activities.
author: mgblythe
ms.author: mblythe
manager: kfile
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-gateways
ms.topic: conceptual
ms.date: 09/19/2019
LocalizationGroup: Gateways 
---

# Adjust gateway performance based on server CPU

The on-premises data gateway has settings that control resource usage on the machine where the gateway is installed. By default, gateway releases starting in June 2019 (3000.6.204) automatically scale these settings, using more or less resources depending on CPU capacity:

| Setting | Description
| -------- | ------|
| `MashupDefaultPoolContainerMaxCount` | Maximum container count for Power BI refresh, Azure Analysis Services, and others. |
| `MashupDQPoolContainerMaxCount` | Maximum container count for Power BI Direct Query. |
| `MashupDQPoolContainerMaxWorkingSetInMB` | Maximum working set size for Power BI Direct Query. |
| `MashupTestConnectionPoolContainerMaxInstanceCount` | Maximum container count for test connections. |
| `MashupTestConnectionPoolContainerMaxWorkingSetInMB` | Maximum working set size for test connections. |
| `MashupAzureConnectorsCachingPoolContainerMaxCount` | Maximum container count for LogicApps, PowerApps, and Microsoft Flow. |
| `MashupAzureConnectorsCachingPoolContainerMaxWorkingSetInMB` | Maximum working set size for LogicApps, PowerApps, and Microsoft Flow. |
| | |

Most queries use _mashup containers_ to execute. So the number of mashup containers determines the number of queries that can be executed in parallel. A _working set_ defines the memory allocated to each container. These settings are available in _\Program Files\On-premises data gateway\Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config_.

If you've changed any of these settings manually, automatic scaling is not enabled by default. To enable it, in _\Program Files\On-premises data gateway\Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config_ set `MashupDisableContainerAutoConfig` to _False_.
