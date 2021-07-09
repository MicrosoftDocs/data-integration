---
title: Overview of virtual network (VNet), private links, and Power BI
description: Learn about the virtual network (VNet), private links, and Power BI.
author: arthiriyer
ms.reviewer: kvivek
ms.prod: on-premises-data-gateway
ms.technology:
ms.topic: conceptual
ms.date: 03/01/2021
ms.author: arthii
ms.custom: intro-internal
---

# What is a virtual network (VNet)? 

[Azure virtual network (VNet)](/azure/virtual-network/virtual-networks-overview) enable many types of Azure resources, such as Azure Virtual Machines (VM), to securely communicate with each other, the internet, and on-premises networks. This offers direct connectivity to Azure resources over an optimized route over the Azure backbone network. Azure resources can either be deployed within a VNet or they can be associated to the VNet using service or private endpoints.  

## Virtual networks, Private Links, and Power BI

We could categorize your communication with Power BI with respect to Azure VNets into the following:
-	Secure Inbound connections to Power BI from your network using Private links 
-	Secure Outbound connectivity from Power BI to data sources within a VNet

The scope of this document is restricted to only *Secure Outbound connectivity from Power BI to data sources within a VNet*. For the *Secure Inbound connections to Power BI from your network using Private links*, see the [Power BI Private Links documentation](/power-bi/admin/service-security-private-links). 

The Azure resources associated to a VNet could include Azure data services like Azure SQL, Synapse Analytics, Azure Data Explorer, and others. List of supported data services is available here: [Supported Azure data services](use-data-gateways-sources-power-bi.md#supported-azure-data-services).

Currently, to be able to connect from Power BI to Azure data services within your VNet, you must install the on-premises data gateway. Data gateway enables secure connectivity to these data sources associated to the VNet and manages query execution from one or more of such data sources. 

A data gateway however brings its own overhead like monthly updates and monitoring. The VNet Gateway will eliminate this overhead and enable secure connectivity to data sources associated to your VNet. 

