---
title: On-premises data gateway FAQ
description: This article is the on-premises data gateway FAQ. It collects frequently asked questions about the gateway into one spot.
author: arthiriyer
manager: kfile
ms.reviewer: ''

ms.prod: on-premises-data-gateway
ms.technology:
ms.topic: conceptual
ms.date: 07/15/2019
ms.author: arthii

LocalizationGroup: Gateways
---

# On-premises data gateway FAQ

## General

**Question:** Do I need a gateway for cloud data sources, such as Azure SQL Database?  
**Answer:** No, services can generally connect to cloud data sources without a gateway. However, you might need a data gateway if your data sources are behind a firewall, require a VPN, or are on virtual networks.

**Question:** What are the requirements for the gateway?  
**Answer:** Review the requirements section in the [installation article](service-gateway-install.md#requirements).

**Question:** Does the gateway have to be installed on the same machine as the data source?  
**Answer:** No, the gateway connects to the data source by using the provided connection information. In this sense, consider the gateway as a client application. The gateway just needs to connect to the specified server.

**Question:** How many releases of the on-premises data gateway does Microsoft actively support?  
**Answer:** Currently, Microsoft actively supports only the last six releases of the on-premises data gateway. We release a new update for data gateways every month.

**Question:** Are there any permissions prerequisites required to install gateways?  
**Answer:** There are no restrictions for installing and registering a gateway. But any cloud service might have licensing restrictions on how gateways are used within that service.

**Question:** Are there any requirements for network bandwidth?  
**Answer:** Check that your network connection has good throughput. Each environment is different, and throughput depends on the amount of data that is sent. To ensure a minimum level of throughput between your on-premises data source and Azure datacenters, use [Azure ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction). To help measure your throughput, you can use the [Azure Speed Test app](https://azurespeedtest.azurewebsites.net/).

**Question:** Where are my credentials stored?  
**Answer:** The credentials that you enter for a data source are encrypted and stored in the gateway cloud service. The credentials are decrypted at the gateway on premises.

**Question:** What is the actual Windows service called?  
**Answer:** On your local computer, in the Services app, the service is called "On-premises data gateway service". In Task Manager, on the Services tab, the service name is "PBIEgwService". By default, the Windows service uses "NT SERVICE\PBIEgwService" as the Service SID (SSID).

**Question:** Can the gateway Windows service run with an Azure Active Directory (Azure AD) account?  
**Answer:** No, the Windows service needs a valid Windows account.

**Question:** Are there any inbound connections to the gateway from the cloud?  
**Answer:** No, the gateway uses outbound connections to Azure Service Bus.

**Question:** What if I block outbound connections? What do I need to open?  
**Answer:** See [Enable outbound Azure connections](service-gateway-communication.md#enable-outbound-azure-connections).

**Question:** Do I need to unblock the Azure Datacenter IP list? Where do I get the list?  
**Answer:** If you block outbound IP traffic, you might need to unblock the Azure Datacenter IP list. The gateway communicates with Azure Service Bus by using an IP address and a fully qualified domain name. The Azure Datacenter IP list is updated weekly. For more information, see [Enable outbound Azure connections](service-gateway-communication.md#enable-outbound-azure-connections).

**Question:** What is the latency for running queries from the gateway to a data source? What is the best architecture?  
**Answer:** To avoid network latency, install the gateway as close as possible to the data source. If you can install the gateway on the actual data source, this closer location minimizes latency.

Also, consider the proximity to the Azure datacenters. For example, if your service uses the West US datacenter, and you have SQL Server hosted in an Azure virtual machine, you might also want your Azure VM in the West US region. This configuration minimizes latency and avoids egress charges on the Azure VM.

**Question:** How are results sent back to the cloud?  
**Answer:** The results are sent through Azure Service Bus. For more information, see [On-premises data gateway architecture](service-gateway-onprem-indepth.md).

**Question:** Can I place the gateway in a perimeter network (also known as DMZ, demilitarized zone, and screened subnet)?  
**Answer:** The gateway requires connectivity to the data source. So, if the data source isn't reachable in your perimeter network, the gateway might not have access.

For example, assume your SQL Server computer isn't in your perimeter network. Also, assume you can't connect to that computer from the perimeter network. If you place the gateway in your perimeter network, the gateway can't reach the SQL Server computer.

**Question:** Can I force the gateway to use HTTPS traffic with Azure Service Bus instead of TCP?  
**Answer:** Yes, for more information, see [Force HTTPS communication with Azure Service Bus](service-gateway-communication.md#force-https-communication-with-azure-service-bus). Turning on this feature has little effect on performance.

**Question:** Are the on-premises data gateway and Data Management Gateway, which is used by Azure Machine Learning Studio and Azure Data Factory, the same thing?  
**Answer:** No, they are different products. To get more information about Data Management Gateway, which is now called Self-hosted Integration Runtime, see [Create and configure a self-hosted integration runtime](/azure/data-factory/create-self-hosted-integration-runtime).

**Question:** Can the person who sets up the gateway in the Azure portal be different from the one who installs that gateway?  
**Answer:** Yes, you must use PowerShell to add other owners to the same gateway. These users can create the gateway in the Azure portal. However, they should connect to the portal and the gateway by using the same tenant.

## High availability and disaster recovery

**Question:** Are there any plans for enabling high-availability scenarios with the gateway?  
**Answer:** To help avoid a single point of failure, you can [set up on-premises data gateways as clusters](service-gateway-high-availability-clusters.md) for high availability. By default, cloud services such as Power Apps and Power BI use the primary gateway and fall back to the secondary gateway if the primary is unavailable.

**Question:** What options are available for disaster recovery?  
**Answer:** When you install the gateway, you supply a recovery key. You can use the key to [restore or migrate](service-gateway-migrate.md) a gateway.

**Question:** What is the benefit of the recovery key?  
**Answer:** The key provides a way to add a new gateway to a cluster or to migrate, recover, or take over a gateway.

## Troubleshooting

For more information, see [Troubleshoot the on-premises data gateway](service-gateway-tshoot.md).

**Question:** Where are the gateway logs located?  
**Answer:** See [Troubleshooting tools](service-gateway-tshoot.md#troubleshooting-tools).

**Question:** How can I see what queries are sent to the on-premises data source?  
**Answer:** You can enable query tracing by turning on [additional logging](service-gateway-performance.md#slow-performing-queries). The logs include the queries that are sent. Remember to turn off query tracing when you're done troubleshooting. Having query tracing enabled causes the logs to be larger.

You can also look at your data source's tools for tracing queries. For example, if SQL Server and SQL Server Analysis Services are data sources, you can use SQL Server Extended Events or SQL Server Profiler to trace queries.

## Administration

**Question:** Can I have more than one admin for a gateway?  
**Answer:** Yes, when you manage a gateway, you can go to the administrator's tab to add additional admins. You can also have security groups as admins.

**Question:** Does the gateway admin need to be an admin on the machine where the gateway is installed?  
**Answer:** No, the gateway admin manages the gateway from within the service.

## Next steps

* [Troubleshoot the on-premises data gateway](service-gateway-tshoot.md)
