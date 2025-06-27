---
title: Use virtual network (VNet) data gateway in Power Platform dataflows
description: Learn about how to connect to data using the virtual network (VNet) data gateway, along with details of supported data sources.
ms.reviewer: dougklo
ms.topic: conceptual
ms.date: 6/27/2025
---

# Use virtual network (VNet) data gateway in Power Platform dataflows

Virtual network data gateways let Power Platform dataflows connect to data services secured in an Azure VNet without the need of an on-premises data gateway. For more information about virtual network data gateways and their limitations, go to [What is a virtual network (VNet) data gateway](what-is.md).

> [!NOTE]
>For Power Platform dataflows, this feature currently doesn't support the ability to write to a privatized data lake or Dataverse.

## Connect to data using a VNet data gateway

To connect to data using a VNet data gateway:

1. Create a new dataflow on the Power Apps maker portal. For more information, go to [Create and use dataflows in Power Apps - Power Apps](/powerapps/maker/data-platform/create-and-use-dataflows).

   :::image type="content" source="media/create-a-new-dataflow.png" alt-text="Screenshot showing the New Dataflow dialog in Power Apps, with the name of the new dataflow entered in the Name text box.":::

2. Once you provide the connection details and then connect to data, the VNet data gateways are now included in the **On-premises data gateway** selections.

   :::image type="content" source="media/vnet-gateway-selections.png" alt-text="Screenshot showing the Power Query connect to data source dialog box with VNet data gateway names included in the on-premises data gateway selection box." lightbox="media/vnet-gateway-selections.png":::

3. Select a VNet data gateway, choose an authentication kind, and then select **Next** to connect and continue with transforming data.

   :::image type="content" source="media/finishing-vnet-connection.png" alt-text="Screenshot showing the Power Query connect to data source dialog box with the VNet data gateway name selected, the user signed in, and ready to select the Next button." lightbox="media/finishing-vnet-connection.png":::

You can also update VNet data gateway details just like you do for an on-premises data gateway. In the Power Query editor, select **Home** > **Options** > **Project options** while editing your dataflow.

   :::image type="content" source="media/project-options-gateway.png" alt-text="Screenshot showing the Power Query Project options dialog box that contains the VNet data gateway options you can change while editing your dataflow." lightbox="media/project-options-gateway.png":::

## Supported data sources

Power Platform dataflows support the same data sources that Power BI does. For a list of supported data sources, go to [Power BI supported data sources](use-data-gateways-sources-power-bi.md#supported-azure-data-services).
