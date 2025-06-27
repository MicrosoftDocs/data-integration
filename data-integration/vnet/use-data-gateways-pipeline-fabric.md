---
title: Use virtual network data gateway with pipeline in Fabric
description: This article describes how to run a Fabric pipeline Copy Activity through the virtual network data gateway.
ms.topic: conceptual
ms.date: 6/27/2025
---

# Run a Fabric pipeline Copy Activity through the virtual network data gateway

To use a Microsoft Fabric pipeline Copy Activity with a virtual network (VNet) data gateway:

1. In Fabric, navigate to your workspace by selecting **Workspaces**, and then selecting your workspace.

   :::image type="content" source="media/select-fabric-workspace-pipeline.png" alt-text="Screenshot of the workspaces with the example workspace name emphasized." lightbox="media/select-fabric-workspace-pipeline.png":::

2. Make sure you select **Fabric** in the bottom left. Then select **New item**.

   :::image type="content" source="media/select-new-pipeline.png" alt-text="Screenshot of the Data Factory page with Data Factory and New emphasized." lightbox="media/select-new-pipeline.png":::

3. Select **Data pipeline** from the pop-up window.

   :::image type="content" source="media/create-new-pipeline.png" alt-text="Screenshot of the Data Factory page with Pipeline emphasized." lightbox="media/create-new-pipeline.png":::

4. Create a new pipeline. In the pipeline page, select **Copy data assistant**.

   :::image type="content" source="media/select-copy-assistant.png" alt-text="Screenshot of the Data Factory page with Copy data assistant." lightbox="media/select-copy-assistant.png":::

5. Search for and select your data source.
6. Input all the necessary connection details for your data source. Under the **Data gateway** header, select the arrow to open the drop-down menu. Select your VNet data gateway from the list, which is prefixed with the **[Virtual network]** tag. If there's no VNet data gateway here, you need to [create one](create-data-gateways.md).

   :::image type="content" source="media/get-data-select-gateway-pipeline.png" alt-text="Screenshot of the Get data window with Data gateway emphasized." lightbox="media/get-data-select-gateway-pipeline.png":::

7. Select **Next**.
8. Select the data you want to load from your source.
9. Do the same for the destination.
10. A copy activity is created in the canvas. Select **Run**. The data is transferred from the source to the destination using the VNet data gateway.

:::image type="content" source="media/run-pipeline.png" alt-text="Screenshot of pipeline run with Data gateway." lightbox="media/run-pipeline.png":::
