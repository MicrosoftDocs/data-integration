---
title: Use virtual network (VNet) data gateway in Power Platform dataflows
description: Learn about how to connect to data using the virtual network (VNet) data gateway, along with details of supported data sources.
author: arthiriyer
ms.reviewer: dougklo
ms.prod: on-premises-data-gateway
ms.technology:
ms.topic: conceptual
ms.date: 06/22/2021
ms.author: arthii
---

# Use virtual network (VNet) data gateway in Power Platform dataflows

Virtual network data gateways let Power Platform dataflows connect to data services secured in an Azure VNet without the need of an on-premises data gateway. For more information about virtual network data gateways and their limitations, go to [What is a virtual network (VNet) data gateway (Preview)](what-is.md).

>[!Note]
>
>* During public preview, Power platform dataflows users will have access to this feature for *free*.
>* For Power Platform dataflows, this feature currently does not support the ability to write to a privatized data lake or Dataverse.

## Connect to data using a VNet data gateway

To connect to data using a VNet data gateway:

1. Create a new dataflow on the Power Apps maker portal. More information: [Create and use dataflows in Power Apps - Power Apps](/powerapps/maker/data-platform/create-and-use-dataflows)

   ![Screenshot showing the New Dataflow dialog box in Power Apps, with the name of the new dataflow entered in the Name text box](media/create-a-new-dataflow.png)

2. Once you provide the connection details and then connect to data, you'll now see VNet data gateways included in the **On-premises data gateway** selections.

   ![Screenshot showing the Power Query connect to data source dialog box with VNet data gateway names included in the on-premises data gateway selection box](media/vnet-gateway-selections.png)

3. Select a VNet data gateway, choose an authentication kind, and then select **Next** to connect and continue with transforming data.

   ![Screenshot showing the Power Query connect to data source dialog box with the VNet data gateway name selected, the user signed in, and ready to select the Next button](media/finishing-vnet-connection.png)

You can also update VNet data gateway details just like you do for an on-premises data gateway. In the Power Query editor, select **Home > Options > Project options** while editing your dataflow.

   ![Screenshot showing the Power Query Project options dialog box that contains the VNet data gateway options you can change while editing your dataflow](media/project-options-gateway.png)

## Supported data sources

VNet data gateways aren’t supported for:

* data sources requiring 3rd party drivers like SAP, Oracle, and so on
* the [Web](/power-query/connectors/web/web) connector
* the [ODBC](/power-query/connectors/odbc) connector

On-premises data sources can be connected using ExpressRoute. But this configuration hasn’t been tested and won't be supported by Microsoft during public preview.
