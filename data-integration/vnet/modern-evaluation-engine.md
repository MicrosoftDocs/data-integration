---
title: Use the modern evaluation engine with virtual network data gateways (preview)
description: Learn how to enable the modern evaluation engine for Fabric workloads that use virtual network data gateways.
ms.service: fabric
ms.subservice: data-factory
ms.topic: concept-article
author: goupadhy
ms.author: goupadhy
ms.reviewer: goupadhy
ms.date: 07/24/2026
---

# Modern evaluation engine for virtual network (VNet) data gateway (preview) 

The modern evaluation engine is an opt-in feature that supported Fabric workloads can use for query evaluation and refresh execution when they connect through a virtual network (VNet) data gateway. You can enable it as a public preview setting from the **Manage connections and gateways** page.

The modern evaluation engine can reduce refresh duration for some workloads and improve DirectQuery startup latency for supported scenarios. Actual performance depends on the connector, data source, query shape, gateway configuration, and workload concurrency. During public preview, the setting is off by default, and existing gateways continue to use the legacy engine until you enable the option.

## Prerequisites

- [A configured VNet data gateway.](create-data-gateways.md)
- [Permission to manage the gateway or connection settings.](manage-data-gateways.md)
- One or more supported Fabric workloads that use the gateway.
- A validation plan for refresh duration, query latency, and capacity consumption.

## Supported scenarios

The modern evaluation engine applies to supported workloads that use a VNet data gateway, including:

- Semantic model refreshes.
- Dataflow Gen2 refreshes.
- DirectQuery workloads that connect through a VNet data gateway.

Support can vary by connector and workload. Test representative workloads before enabling the setting for production gateways.

> [!TIP]
> The modern evaluation engine is an opt-in setting. Existing gateways continue to use the legacy engine until you enable the option.

## Enable the modern evaluation engine

Gateway administrators can enable the modern evaluation engine as an opt-in setting for a specific gateway.
    
1. In Fabric, open **Manage connections and gateways**.
1. Select the VNet data gateway that you want to update.
1. In the gateway settings, under the advanced options, turn on **Use modern evaluation engine**.
1. Save the change.
1. Run representative refresh and DirectQuery workloads.
1. Compare refresh duration, query latency, and capacity metrics before and after enabling the setting.

:::image type="content" source="media/modern-evaluation-engine/evaluation.png" alt-text="Screenshot of the Settings panel with the Use modern evaluation engine toggle enabled and highlighted.":::

## Disable the modern evaluation engine

Turn off the modern evaluation engine if you need to return a gateway to the legacy engine.

1. Open **Manage connections and gateways**.
1. Select the VNet data gateway.
1. Turn off **Use modern evaluation engine**.
1. Save the change.
1. Rerun the affected workload to confirm behavior.

## Performance considerations

The modern evaluation engine can improve elapsed time for some refresh and query scenarios. The following examples show observed results from benchmark runs. These results are examples only and shouldn't be used as a guarantee for a specific environment.

### Refresh scenarios

| Scenario | Connector | Cloud | VNet data gateway - legacy | VNet data gateway - modern |
| --- | --- | ---: | ---: | ---: |
| Semantic model refresh | Azure Blob Storage (10 GB) | 35:10 | 42:26 | 26:59 |
| Semantic model refresh | SQL (100 million rows) | 7:50 | 13:18 | 7:40 |
| Dataflow Gen2 refresh | Azure Blob Storage (10 GB) | 19:30 (modern) | 46:09 | 25:31 |

### DirectQuery scenarios

| Metric | Legacy | Modern |
| --- | ---: | ---: |
| Semantic model DirectQuery cold startup, end-to-end | 10 seconds | 200 ms |
| Semantic model DirectQuery steady state, end-to-end | 200 ms | 200 ms |

> [!NOTE]
> These results are examples from benchmark scenarios. Actual performance depends on connector behavior, source system latency, query shape, gateway configuration, model design, and workload concurrency.

## Capacity and billing considerations

The modern evaluation engine can reduce wall-clock refresh time for some workloads. Capacity impact depends on which workload is running and how that workload is metered.

Shorter refresh duration or reduced CPU time can influence capacity usage in some scenarios, but the actual impact varies. Admins should compare before-and-after behavior by using the Fabric Capacity Metrics app and representative workloads from their own environment.


## Workload validation

After you enable the modern evaluation engine, validate the workloads that use the gateway:

1. Run a representative semantic model refresh.
1. Run a representative Dataflow Gen2 refresh.
1. Test DirectQuery reports that connect through the gateway.
1. Review refresh history for failures or regressions.
1. Compare wall-clock duration and capacity metrics against your baseline.
1. If a workload doesn't behave as expected, turn off **Use modern evaluation engine** and contact Microsoft support with gateway diagnostics.

## Troubleshooting

### Refresh performance doesn't improve

Performance improvements vary by connector, query shape, source system, and available gateway resources. Compare multiple runs before and after enabling the setting, and confirm that the workload is using a supported connector and gateway path.

### Capacity consumption doesn't decrease

Shorter wall-clock duration doesn't always result in a proportional capacity reduction. Gateway uptime, cooldown behavior, workload CPU time, and concurrency can affect observed capacity usage.

### DirectQuery cold startup is still slow

Confirm that the report uses the VNet data gateway path and that the connector is supported. Also check whether startup time is affected by source system latency, authentication, or model initialization outside the gateway path.

## Related content
- [Modern Evaluator for Dataflow Gen2](/fabric/data-factory/dataflow-gen2-modern-evaluator)
- [Virtual network data gateways](overview.md)
- [Virtual network data gateway business model](data-gateway-business-model.md)
- [Download logs on the VNet data gateway](data-gateway-download-diagnostics.md)
- [Fabric Capacity Metrics app](/fabric/enterprise/metrics-app)
