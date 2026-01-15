---
title: What is an on-premises data gateway?
description: Learn the basics about on-premises data gateways, which enable quick and secure data transfer between on-premises data and several Microsoft cloud services.
ms.topic: overview
ms.date: 6/10/2025
---

# What is an on-premises data gateway?

> [!NOTE]
>Currently, Microsoft actively supports only the last six releases of the on-premises data gateway. We release a new update for data gateways every month.

> [!NOTE]
>Beginning on March 15, 2023, any Power BI dataflow using an on-premises data gateway version older than April 2021 might fail. To ensure your refreshes continue to work correctly, be sure to update your gateway to the latest version and sign in to it.

The on-premises data gateway is a locally installed Windows client application that acts as a bridge between your local on-premises data sources and services in the Microsoft cloud. It provides quick and secure data transfer and requires no inbound ports to your network&mdash;only outbound ports to reach the Azure web service to which the gateway connects. The gateway functions with multiple services including Azure Analysis Services, Azure Data Factory, Azure Logic Apps, Microsoft Fabric, Power Apps, Power Automate, and Power BI.

Using a gateway allows organizations to keep databases and other data sources on their on-premises networks while securely using that on-premises data in cloud services.

## How the gateway works

:::image type="content" source="media/service-gateway-getting-started/on-premises-data-gateway.png" alt-text="Diagram showing a conceptual drawing of how the gateway works.":::

The on-premises data gateway initiates outbound connections to the cloud, but requires no inbound connections. All communication from the cloud is received in responses to polling over the outbound connections. For detailed information on how the gateway works, go to [On-premises data gateway architecture](service-gateway-onprem-indepth.md) and [Adjust communication settings for the on-premises data gateway](service-gateway-communication.md).

## Types of gateways

There are two different types of on-premises data gateways, each for a different scenario.

* **On-premises data gateway**: Allows multiple users to connect to multiple on-premises data sources. With a single gateway installation, you can use an on-premises data gateway with all supported services. This gateway is well suited to complex scenarios where multiple people access multiple data sources.

* **On-premises data gateway (personal mode)**: Allows one user to connect to data sources and can't be shared with others. An on-premises data gateway (personal mode) can be used only with Power BI. This gateway is well suited to scenarios where you're the only one who creates reports and you don't need to share any data sources with others.

In addition, there's a virtual network (VNet) data gateway that lets multiple users connect to multiple data sources secured by virtual networks. No installation is required because it's a Microsoft managed service. This gateway is well suited to complex scenarios in which multiple people access multiple data sources. Virtual network data gateways are discussed in depth in [What is a virtual network (VNet) data gateway](../vnet/overview.md).

## Using a gateway

There are four main steps for using a gateway.

1. [Download and install the gateway](service-gateway-install.md) on a local computer.
1. [Configure](service-gateway-app.md) the gateway based on your firewall and other network requirements.
1. Add gateway admins who can also manage and administer other network requirements:
   - [Add gateway admins in the Power BI service](/power-bi/connect-data/service-gateway-data-sources#manage-users)
   - [Add gateway admins in the Power Platform admin center](/power-platform/admin/onpremises-data-gateway-management#manage-users).
1. [Troubleshoot](service-gateway-tshoot.md) the gateway if there are errors.

## Considerations and Limitations

* Logic Apps, Power Apps, and Power Automate support both read and write operations through the gateway:
  * The gateway has a 2-MB payload limit for write operations.
  * The gateway has a 2-MB request limit and an 8-MB compressed data response limit for read operations.
  * URL for the GET request has a 2048 character limit.
* When you use the gateway with Power BI in DirectQuery mode, there's a 16-MB uncompressed data response limit.
* For information about installation considerations, go to [Related considerations](service-gateway-install.md#related-considerations).
* We cache credentials on the gateway client side, which improves the performance of the queries executed on the gateway. The cache expires in a matter of hours. However, this caching behavior means that changed credentials might not be immediately reflected and can cause refreshes to fail. For example, if a user uploads a DirectQuery report with a connection and then edits that connection's credentials, the new credentials aren't used for approximately 5 hours and the user can expect the connection in the report to fail.
* There's a limitation of 1,000 data sources maximum on each enterprise or personal gateway cluster. [How to avoid reaching this limit](/data-integration/gateway/service-gateway-onprem-faq#what-do-i-need-to-do-if-i-reach-the-maximum-limit-of-1-000-data-sources-per-user--and-how-do-i-avoid-reaching-this-limit-).

## Gateway documentation

This document contains general information about the on-premises data gateway that applies to all services that the gateway supports. You can obtain more on-premises data gateway information for specific products by visiting the following product-specific sites.

* [On-premises data gateway in-depth - Power BI](/power-bi/service-gateway-onprem-indepth/)

* [How to access on-premises data sources in Data Factory for Microsoft Fabric](/fabric/data-factory/how-to-access-on-premises-data)

* [Using an on-premises data gateway in Power Platform Dataflows](/powerapps/maker/common-data-service/using-dataflows-with-on-premises-data)

* [Manage connections in Power Automate](/power-automate/add-manage-connections)

* [Connect to on-premises data sources from Azure Logic Apps](/azure/logic-apps/logic-apps-gateway-connection)

* [Connecting to on-premises data sources with On-premises data gateway - Azure Analysis Services](/azure/analysis-services/analysis-services-gateway)

## Related content

* [Install the on-premises data gateway](service-gateway-install.md)
