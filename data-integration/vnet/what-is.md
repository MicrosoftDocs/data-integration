---
title: Overview of virtual network (VNet), private links, and Power BI
description: Learn about the virtual network (VNet), private links, and Power BI.
ms.topic: conceptual
ms.date: 10/11/2022
ms.custom: intro-internal
---

# What is a virtual network (VNet)?

[Azure virtual network (VNet)](/azure/virtual-network/virtual-networks-overview) enables many types of Azure resources, such as Azure Virtual Machines (VM), to securely communicate with each other, the internet, and on-premises networks. This VNet offers direct connectivity to Azure resources over an optimized route over the Azure backbone network. Azure resources can either be deployed within a VNet or they can be associated to the VNet using service or private endpoints.  

## Virtual networks, Private Links, and Power BI

Your communication with Power BI with respect to Azure VNets can be categorized as follows:

- Secure Inbound connections to Power BI from your network using Private links.
- Secure Outbound connectivity from Power BI to data sources within a VNet.

The scope of this document is restricted to only *Secure Outbound connectivity from Power BI to data sources within a VNet*. For the *Secure Inbound connections to Power BI from your network using Private links*, go to the [Power BI Private Links documentation](/power-bi/admin/service-security-private-links).

The Azure resources associated with a VNet could include Azure data services like Azure SQL, Synapse Analytics, Azure Data Explorer, and others. A list of supported data services is available at [Supported Azure data services](use-data-gateways-sources-power-bi.md#supported-azure-data-services).

Before the advent of the Vnet gateway, to be able to connect from Power BI to Azure data services within your VNet, you had to install the on-premises data gateway on a vm inside the Vnet. This is still an option.  The on-premises data gateway enables secure connectivity to these data sources associated with the VNet and manages query execution from one or more of such data sources.

However, an on-premises data gateway brings its own overhead, like monthly updates and monitoring. The VNet gateway will eliminate this overhead and enable secure connectivity to data sources associated with your VNet.
