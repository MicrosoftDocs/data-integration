---
title: What is an on-premises data gateway?
description: Learn the basics about on-premises data gateways, which enable quick and secure data transfer between on-premises data and several Microsoft cloud services.
author: arthiriyer
manager: kfile
ms.reviewer: ''

ms.technology: on-premises-data-gateway
ms.topic: overview
ms.date: 07/15/2019
ms.author: arthii

LocalizationGroup: Gateways
---

# What is an on-premises data gateway?

>[!Note]
Currently, Microsoft actively supports only the last six releases of the on-premises data gateway.

The on-premises data gateway acts as a bridge. It provides quick and secure data transfer between on-premises data, which is data that isn't in the cloud, and several Microsoft cloud services. These services include Power BI, Power Apps, Power Automate, Azure Analysis Services, and Azure Logic Apps.

By using a gateway, organizations can keep databases and other data sources on their on-premises networks while securely using that on-premises data in cloud services.

## How the gateway works

![Gateway overview](media/service-gateway-getting-started/on-premises-data-gateway.png)

For detailed information on how the gateway works, see [On-premises data gateway architecture](service-gateway-onprem-indepth.md).

## Types of gateways

There are two different types of gateways, each for a different scenario.

* **On-premises data gateway**: Allows multiple users to connect to multiple on-premises data sources. With a single gateway installation, you can use an on-premises data gateway with all supported services. This gateway is well-suited to complex scenarios where multiple people access multiple data sources.

* **On-premises data gateway (personal mode)**: Allows one user to connect to data sources and can’t be shared with others. An on-premises data gateway (personal mode) can be used only with Power BI. This gateway is well-suited to scenarios where you’re the only one who creates reports and you don't need to share any data sources with others.

## Using a gateway

There are four main steps for using a gateway.

1. [Download and install the gateway](service-gateway-install.md) on a local computer.
1. [Configure](service-gateway-app.md) the gateway based on your firewall and other network requirements.
1. [Add gateway admins](service-gateway-manage.md) who can also manage and administer other network requirements.
1. [Troubleshoot](service-gateway-tshoot.md) the gateway in case of errors.

## Considerations

- Logic Apps, Power Apps, and Power Automate support both read and write operations through the gateway:
  - Write operations have a 2-MB payload limit.
  - Read operations have a 2-MB request limit and an 8-MB compressed data response limit.
- While using the gateway with Power BI in Direct Query Mode, there is a 16-MB uncompressed data response limit.
- For information about installation considerations, see [Related considerations](service-gateway-install.md#related-considerations).

## Gateway documentation

This document contains general information about the on-premises data gateway that applies to all services that the gateway supports. You can obtain more on-premises data gateway information for specific products by visiting the following product-specific sites.

* [On-premises data gateway in-depth - Power BI](https://docs.microsoft.com/en-us/power-bi/service-gateway-onprem-indepth/)

* [Using an on-premises data gateway in Power Platform Dataflows](https://docs.microsoft.com/en-us/powerapps/maker/common-data-service/using-dataflows-with-on-premises-data)

* [Manage connections in Power Automate](https://docs.microsoft.com/en-us/power-automate/add-manage-connections)

* [Connect to on-premises data sources from Azure Logic Apps](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-gateway-connection)

* [Connecting to on-premises data sources with On-premises data gateway - Azure Analysis Services](https://docs.microsoft.com/en-us/azure/analysis-services/analysis-services-gateway)

## Next steps

* [Install the on-premises data gateway](service-gateway-install.md)
