---
title: Use VNet data gateways with Dataflow Gen2 in Fabric
description: Discusses how to create a Dataflow Gen2 in Fabric with a connection through the VNet data gateway.
ms.topic: how-to
ms.date: 6/30/2025
---

# Run a Fabric Dataflow Gen2 through the VNet data gateway

To use a Dataflow Gen2 with VNets:

1. In Fabric, navigate to your workspace by selecting **Workspaces**, and then selecting your workspace.

   :::image type="content" source="media/use-data-gateways-dfgen2-fabric/select-fabric-workspace.png" alt-text="Screenshot of the workspaces with the example workspace name emphasized." lightbox="media/use-data-gateways-dfgen2-fabric/select-fabric-workspace.png":::

2. Make sure you selected **Data Factory** in the bottom left. Then select **New item**.

   :::image type="content" source="media/use-data-gateways-dfgen2-fabric/select-new.png" alt-text="Screenshot of the Data Factory page with Data Factory and New emphasized." lightbox="media/use-data-gateways-dfgen2-fabric/select-new.png":::

3. Select **Dataflow Gen2** from the drop-down menu.

   :::image type="content" source="media/use-data-gateways-dfgen2-fabric/select-new-dataflow-gen2.png" alt-text="Screenshot of the Data Factory page with Dataflow Gen2 emphasized." lightbox="media/use-data-gateways-dfgen2-fabric/select-new-dataflow-gen2.png":::

4. Select **Get data**. If you open the drop-down menu, select **More**.

   :::image type="content" source="media/use-data-gateways-dfgen2-fabric/select-get-data.png" alt-text="Screenshot of the Data Factory page with Get data emphasized." lightbox="media/use-data-gateways-dfgen2-fabric/select-get-data.png":::

5. Search for and select your datasource.

6. Input all the necessary connection details for your data source. Under the **Data gateway** header, select the arrow to open the drop-down menu. Select your VNet data gateway from the list, which is prefixed with the **[Virtual network]** tag. If there's no VNet data gateway here, you need to [create one](create-data-gateways.md).

   :::image type="content" source="media/use-data-gateways-dfgen2-fabric/get-data-select-gateway.png" alt-text="Screenshot of the Get data window with Data gateway emphasized." lightbox="media/use-data-gateways-dfgen2-fabric/get-data-select-gateway.png":::

7. Select **Next**.
8. Select the data you want to load from your source.
9. You're now back in the Power Query editor. Apply any transformations to your data here.
10. Select **Publish**.

You're taken back to your workspace where you can view your new Dataflow Gen2 loading. You can also navigate to the **Manage connections and gateways** page and look under virtual network data gateways. Here you can see the new connection to your data source if you made a new one in step 5.
