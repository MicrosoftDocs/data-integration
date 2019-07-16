---
title: What is an on-premises data gateway?
description: Learn the basics about on-premises data gateways, which enable quick and secure data transfer between on-premises data and several Microsoft cloud services.
author: mgblythe
manager: kfile
ms.reviewer: ''

ms.service: powerbi
ms.subservice: powerbi-gateways
ms.topic: overview
ms.date: 07/15/2019
ms.author: mblythe

LocalizationGroup: Gateways
---

# What is an on-premises data gateway?

The on-premises data gateway acts as a bridge, providing quick and secure data transfer between on-premises data (data that is not in the cloud) and several Microsoft cloud services, including Power BI, PowerApps, Microsoft Flow, Azure Analysis Services, and Logic Apps. By using a gateway, organizations can keep databases and other data sources on their on-premises networks, yet securely use that on-premises data in cloud services.

## How the gateway works

![Gateway overview](media/service-gateway-getting-started/on-premises-data-gateway.png)

For detailed information on how the gateway works, see [On-premises data gateway architecture](service-gateway-onprem-indepth.md).

## Types of gateways

There are two different types of gateways, each for a different scenario:

* **On-premises data gateway** – allows multiple users to connect to multiple on-premises data sources. You can use an on-premises data gateway with all supported services, with a single gateway installation. This gateway is well-suited to complex scenarios with multiple people accessing multiple data sources.

* **On-premises data gateway (personal mode)** – allows one user to connect to sources, and can’t be shared with others. An on-premises data gateway (personal mode) can be used only with Power BI. This gateway is well-suited to scenarios where you’re the only person who creates reports, and you don't need to share any data sources with others.

## Using a gateway

There are four main steps for using a gateway:

1. [Download and install the gateway](service-gateway-install.md) on a local computer.
2. [Configure](service-gateway-app.md) the gateway based on your firewall and other network requirements.
3. [Add gateway admins](service-gateway-manage.md) who can also manage and administer other network requirements.
4. [Troubleshoot](service-gateway-tshoot.md) the gateway in case of errors.

## Next steps

* [Install the on-premises data gateway](service-gateway-install.md)
