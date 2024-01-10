---
title: Use VNet data gateways with Dataflows Gen2 in Fabric
description: Discusses how to create a Dataflow Gen 2 in Fabric with a connection through the VNet data gateway.
ms.topic: conceptual
ms.date: 1/10/2024
---

# Run a Fabric Dataflows Gen 2 through the VNet Data Gateway

To use a Dataflow Gen2 with VNETs:
1.	In Fabric, navigate to your workspace by clicking on Workspaces and selecting your workspace.
![Open your workspace](media/select-fabric-workspace.png)

2.	Make sure you have selected Data Factory in the bottom left. Then select New+ and then select Dataflow Gen2 (Preview) from the drop-down menu.
![Select new artifact](media/select-new.png)
![Select new Dataflow Gen2](select-new-dataflowgen2.png)

3.	Select Get Data. If you open the drop-down menu, select More….
![Select Get Data](select-get-data.png)

4.	Search for and select your datasource.
5.	Input all the necessary connection details for your data source. Under the Data gateway header, select the arrow to open the drop-down menu. Select your VNet data gateway from the list. Note that it will be prefixed with the [Virtual network] tag. If you don’t see VNet data gateway here, you need to [create one](https://learn.microsoft.com/en-us/data-integration/vnet/create-data-gateways).
![Select Gateway in Get Data](get-data-select-gateway.png)

6.	Click Next.
7.	Select the data you want to load from your source.
8.	You are now back in the Power Query editor. Apply any transformations to your data here.
9.	Select Publish.
10.	You will be taken back to your workspace where you can view your new Dataflow Gen2 loading. You can also navigate to the manage connections and gateways page and look under virtual network data gateways to see the new connection to your data source, if you made a new one in step 5.

