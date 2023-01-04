---
title: What is an on-premises data gateway?
description: Learn the basics about on-premises data gateways, which enable quick and secure data transfer between on-premises data and several Microsoft cloud services.
ms.topic: overview
ms.date: 1/4/2023
---

# What is an on-premises data gateway?

>[!Note]
>Currently, Microsoft actively supports only the last six releases of the on-premises data gateway. We release a new update for data gateways every month.

>[!NOTE]
>Beginning on February 15, 2023, any on-premises data gateway version older than April 2021 will no longer be supported. To ensure your refreshes continue to work correctly, be sure to update your gateway to the latest version.

The on-premises data gateway acts as a bridge. It provides quick and secure data transfer between on-premises data, which is data that isn't in the cloud, and several Microsoft cloud services. These services include Power BI, Power Apps, Power Automate, Azure Analysis Services, and Azure Logic Apps.

By using a gateway, organizations can keep databases and other data sources on their on-premises networks while securely using that on-premises data in cloud services.

## How the gateway works

![Gateway overview.](media/service-gateway-getting-started/on-premises-data-gateway.png)

For detailed information on how the gateway works, go to [On-premises data gateway architecture](service-gateway-onprem-indepth.md).

## Types of gateways

There are two different types of on-premises data gateways, each for a different scenario.

* **On-premises data gateway**: Allows multiple users to connect to multiple on-premises data sources. With a single gateway installation, you can use an on-premises data gateway with all supported services. This gateway is well suited to complex scenarios where multiple people access multiple data sources.

* **On-premises data gateway (personal mode)**: Allows one user to connect to data sources and can't be shared with others. An on-premises data gateway (personal mode) can be used only with Power BI. This gateway is well suited to scenarios where you're the only one who creates reports and you don't need to share any data sources with others.

In addition, there's a virtual network (VNet) data gateway that lets multiple users connect to multiple data sources that are secured by virtual networks. No installation is required because it's a Microsoft managed service. This gateway is well suited to complex scenarios in which multiple people access multiple data sources. Virtual network data gateways are discussed in depth in [What is a virtual network (VNet) data gateway](../vnet/overview.md).

## Using a gateway

There are four main steps for using a gateway.

1. [Download and install the gateway](service-gateway-install.md) on a local computer.
1. [Configure](service-gateway-app.md) the gateway based on your firewall and other network requirements.
1. [Add gateway admins](service-gateway-manage.md) who can also manage and administer other network requirements.
1. [Troubleshoot](service-gateway-tshoot.md) the gateway if there are errors.

## Considerations

* Logic Apps, Power Apps, and Power Automate support both read and write operations through the gateway:
  * The gateway has a 2-MB payload limit for write operations.
  * The gateway has a 2-MB request limit and an 8-MB compressed data response limit for read operations.
  * URL for the GET request has a 2048 character limit.
* While using the gateway with Power BI in Direct Query Mode, there's a 16-MB uncompressed data response limit.
* For information about installation considerations, go to [Related considerations](service-gateway-install.md#related-considerations).

## Gateway documentation

This document contains general information about the on-premises data gateway that applies to all services that the gateway supports. You can obtain more on-premises data gateway information for specific products by visiting the following product-specific sites.

* [On-premises data gateway in-depth - Power BI](/power-bi/service-gateway-onprem-indepth/)

* [Using an on-premises data gateway in Power Platform Dataflows](/powerapps/maker/common-data-service/using-dataflows-with-on-premises-data)

* [Manage connections in Power Automate](/power-automate/add-manage-connections)

* [Connect to on-premises data sources from Azure Logic Apps](/azure/logic-apps/logic-apps-gateway-connection)

* [Connecting to on-premises data sources with On-premises data gateway - Azure Analysis Services](/azure/analysis-services/analysis-services-gateway)

## Next steps

* [Install the on-premises data gateway](service-gateway-install.md)
