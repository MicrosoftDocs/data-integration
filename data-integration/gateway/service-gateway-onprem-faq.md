---
title: On-premises data gateway FAQ
description: This article is the on-premises data gateway FAQ. It collects frequently asked questions about the gateway into one spot.
author: mgblythe
manager: kfile
ms.reviewer: ''

ms.service: powerbi
ms.subservice: powerbi-gateways
ms.topic: conceptual
ms.date: 07/15/2019
ms.author: mblythe

LocalizationGroup: Gateways
---

# On-premises data gateway FAQ

[!INCLUDE [gateway-rewrite](../includes/gateway-rewrite.md)]

## General

**Question:** What is the actual Windows service called?  
**Answer:** In the Services app, the service is called On-premises data gateway service.

**Question:** What are the requirements for the gateway?  
**Answer:** Take a look at the requirements section of the [installation article](service-gateway-install.md#requirements).

**Question:** Do I need a gateway for cloud data sources like Azure SQL Database?  
**Answer:** No. In general, services can connect to cloud data sources without a gateway. But a data gateway might be needed for on-premises data sources or if the data sources are behind a firewall, require a VPN, or are on virtual networks.

**Question:** Are there any inbound connections to the gateway from the cloud?  
**Answer:** No. The gateway uses outbound connections to Azure Service Bus.

**Question:** What if I block outbound connections? What do I need to open?  
**Answer:** See [Enable outbound Azure connections](service-gateway-communication.md#enable-outbound-azure-connections).

**Question:** Does the gateway have to be installed on the same machine as its data source?  
**Answer:** No. The gateway connects to its data source by using the provided connection information. In this sense, think of the gateway as a client application. It just needs to connect to the server that has the provided name.

**Question:** Are there any permissions prerequisites required to install gateways?  
**Answer:** There are no restrictions for installing and registering a gateway. But any cloud service might have licensing restrictions on how gateways are used within that service.

**Question:** What is the latency for running queries from the gateway to a data source? What is the best architecture?  
**Answer:** We recommend that you have the gateway as close to the data source as possible to avoid network latency. If you install the gateway on the actual data source, the introduced latency is minimized.

Consider the Azure data centers as well. For example, if your service uses the West US data center and you have SQL Server hosted in an Azure virtual machine, you want the Azure VM to also be in West US. This configuration minimizes latency and avoids egress charges on the Azure VM.

**Question:** Are there any requirements for network bandwidth?  
**Answer:** We recommend that your network connection has good throughput. But because each environment is different, throughput also depends on the amount of data being sent. Using Azure ExpressRoute can help guarantee a minimum level of throughput between on-premises and the Azure data centers.

You can use a partner's [Azure Speed Test app](https://azurespeedtest.azurewebsites.net/) to help gauge your throughput.

**Question:** Can the gateway Windows service run with an Azure Active Directory (Azure AD) account?  
**Answer:** No. The Windows service needs a valid Windows account. By default, the service runs with the Service security identifier (SID) *NT SERVICE\PBIEgwService*.

**Question:** How are results sent back to the cloud?  
**Answer:** They are sent by way of Azure Service Bus. For more information, see [on-premises data gateway architecture](service-gateway-onprem-indepth.md).

**Question:** Where are my credentials stored?  
**Answer:** The credentials you enter for a data source are encrypted and stored in the gateway cloud service. The credentials are decrypted at the gateway on-premises.

**Question:** Can I place the gateway in a perimeter network (also known as DMZ, demilitarized zone, and screened subnet)?  
**Answer:** The gateway requires connectivity to its data source. If the data source isn't reachable in your perimeter network, the gateway might not be able to connect to it.

For example, assume your SQL Server computer isn't in your perimeter network. Also assume you can't connect to that computer from the perimeter network. If you place the gateway in your perimeter network, it can't reach the SQL Server computer.

**Question:** Is it possible to force the gateway to use HTTPS traffic with Azure Service Bus instead of TCP?  
**Answer:** Yes. For more information, see [Force HTTPS communication with Azure Service Bus](service-gateway-communication.md#force-https-communication-with-azure-service-bus). Turning on this feature has little effect on performance.

**Question:** Do I need to whitelist the Azure Datacenter IP list? Where do I get the list?  
**Answer:** If you block outbound IP traffic, you might need to whitelist the Azure Datacenter IP list. The gateway communicates with Azure Service Bus by using an IP address and a fully qualified domain name. The Azure Datacenter IP list is updated weekly. For more information, see [Enable outbound Azure connections](service-gateway-communication.md#enable-outbound-azure-connections).

**Question:** Are the on-premises data gateway and Data Management Gateway, as used by Azure Machine Learning Studio and Azure Data Factory, the same thing?  
**Answer:** No, they are two different products. To get more information about Data Management Gateway, which is now called Self-hosted Integration Runtime, see [Create and configure a self-hosted integration runtime](/azure/data-factory/create-self-hosted-integration-runtime).

**Question:** Can the person who sets up the gateway in the Azure portal be different from the one who installs that gateway?  
**Answer:** Yes. You must use PowerShell to add other owners to the same gateway. These users can create the gateway on the portal. But they should connect to the portal and the gateway under the same tenant.

## High availability and disaster recovery

**Question:** Are there any plans for enabling high-availability scenarios with the gateway?  
**Answer:** [High-availability clusters of on-premises data gateways](service-gateway-high-availability-clusters.md) help avoid a single point of failure. Cloud services like PowerApps and Power BI use the primary node by default. They fall back to the secondary node if the primary node is unavailable.

**Question:** What options are available for disaster recovery?  
**Answer:** When you install the gateway, you supply a recovery key. You can use the key to [restore](service-gateway-migrate.md) or move a gateway.

**Question:** What is the benefit of a recovery key?  
**Answer:** It provides a way to add a new gateway to a cluster or to migrate, recover, or take over a gateway.

## Troubleshooting

**Question:** Where are the gateway logs located?  
**Answer:** See [Troubleshooting tools](service-gateway-tshoot.md#troubleshooting-tools).

**Question:** How can I see what queries are sent to the on-premises data source?  
**Answer:** You can enable query tracing by turning on [Additional logging](service-gateway-performance.md#slow-performing-queries). The logs then include the queries being sent. Remember to turn off query tracing when you're done troubleshooting. Having query tracing enabled causes the logs to be larger.

You can also look at your data source's tools for tracing queries. For example, if SQL Server and SQL Server Analysis Services are data sources, you can use SQL Server Extended Events or SQL Server Profiler to trace queries.

## Administration

**Question:** Can I have more than one admin for a gateway?  
**Answer:** Yes. When you manage a gateway, you can go to the administrator's tab to add additional admins. You can also have security groups as admins.

**Question:** Does the gateway admin need to be an admin on the machine where the gateway is installed?  
**Answer:** No. The gateway admin manages the gateway from within the service.

## Next steps

* [Troubleshoot the on-premises data gateway](service-gateway-tshoot.md)
