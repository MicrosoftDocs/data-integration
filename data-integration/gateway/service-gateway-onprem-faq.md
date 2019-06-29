---
title: On-premises data gateway FAQ
description: This is the on-premises data gateway FAQ. This collects frequently asked questions into one spot for the gateway.
author: mgblythe
manager: kfile
ms.reviewer: ''

ms.service: powerbi
ms.subservice: powerbi-gateways
ms.topic: conceptual
ms.date: 04/25/2019
ms.author: mblythe

LocalizationGroup: Gateways
---
# On-premises data gateway FAQ

## General

**Question:** What is the actual Windows service called?  
**Answer:** The gateway is called On-premises data gateway service in Services.

**Question:** What are the requirements for the gateway?  
**Answer:** Take a look at the requirements section of the [installation article](service-gateway-install.md#requirements).

**Question:** Do I need a gateway for cloud data sources like Azure SQL Database?  
**Answer:** No. In general, the service will be able to connect to that data source without a gateway. However, for on-premises data sources, or if the data sources reside behind a firewall, or requires a VPN, or are on virtual networks, a data gateway may be needed.

**Question:** Are there any inbound connections to the gateway from the cloud?  
**Answer:** No. The gateway uses outbound connections to Azure Service Bus.

**Question:** What if I block outbound connections? What do I need to open?  
**Answer:** See [Enable outbound Azure connections](service-gateway-communication.md#enable-outbound-azure-connections).

**Question:** Does the gateway have to be installed on the same machine as the data source?  
**Answer:** No. The gateway will connect to the data source using the connection information that was provided. Think of the gateway as a client application in this sense. It will just need to be able to connect to the server name that was provided.

**Question:** Are there any permissions prerequisites to install gateways?  
**Answer:** There are no restrictions for installing and registering a gateway, but every cloud service could have restrictions on how gateways are used within their service based on licensing.

**Question:** What is the latency for running queries to a data source from the gateway? What is the best architecture?  
**Answer:** We recommend that you have the gateway as close to the data source as possible to avoid network latency. If you can install the gateway on the actual data source, it will minimize the latency introduced. Consider the data centers as well. For example, if your service is making use of the West US data center, and you have SQL Server hosted in an Azure VM, you will want to have the Azure VM in West US as well. This will minimize latency and avoid egress charges on the Azure VM.

**Question:** Are there any requirements for network bandwidth?  
**Answer:** We recommend that you have good throughput for your network connection. Every environment is different and this is also dependent on the amount of data being sent. Using ExpressRoute could help to guarantee a level of throughput between on-premises and the Azure data centers.

You can use the 3rd party [Azure Speed Test app](http://azurespeedtest.azurewebsites.net/) to help gauge what your throughput is.

**Question:** Can the gateway Windows service run with an Azure Active Directory account?  
**Answer:** No. The Windows service needs to have a valid Windows account. By default it will run with the Service SID *NT SERVICE\PBIEgwService*.

**Question:** How are results sent back to the cloud?  
**Answer:** This is done by way of the Azure Service Bus. For more information, see [on-premises data gateway architecture](service-gateway-onprem-indepth.md).

**Question:** Where are my credentials stored?  
**Answer:** The credentials you enter for a data source are stored encrypted in the gateway cloud service. The credentials are decrypted at the gateway on-premises.

**Question:** Can I place the gateway in a perimeter network (also known as DMZ, demilitarized zone, and screened subnet)?  
**Answer:** The gateway requires connectivity to the data source. If the data source is not accessible in your perimeter network, the gateway may not be able to connect to it. For example, your SQL Server may not be in your perimeter network. And, you cannot connect to your SQL Server from the perimeter network. If you placed the gateway in your perimeter network, it would not be able to reach the SQL Server.

**Question:** Is it possible to force the gateway to use HTTPS traffic with Azure Service Bus instead of TCP?  
**Answer:** Yes. For more information, see [Force HTTPS communication with Azure Service Bus](service-gateway-communication.md#force-https-communication-with-azure-service-bus). Turning on this feature has very little impact on performance.

**Question:** Do I need to whitelist the Azure Datacenter IP list? Where do I get the list?  
**Answer:** If you are blocking outbound IP traffic, you may need to whitelist the Azure Datacenter IP list. Currently, the gateway will communicate with Azure Service Bus using the IP address in addition to the fully qualified domain name. The Azure Datacenter IP list is updated weekly. For more information, see [Enable outbound Azure connections](service-gateway-communication.md#enable-outbound-azure-connections).

**Question:** Are the on-premises data gateway and the Data Management Gateway (used by Azure Machine Learning Studio and Azure Data Factory) the same thing?  
**Answer:** No, they are two different products. To get more information about the Data Management Gateway (now called Self-hosted Integration Runtime), see [Create and configure a self-hosted integration runtime](https://docs.microsoft.com/azure/data-factory/create-self-hosted-integration-runtime).

**Question:** Can the person who sets up that gateway in the Azure Portal be different from the one who installs the gateway?  
**Answer:** Yes. You'll have to use PowerShell to add other owners to the same gateway and these users could create the gateway on the portal. However, the tenant under which they connect to Azure Portal and the gateway should be the same.

## High Availability/Disaster Recovery

**Question:** Are there any plans for enabling high availability scenarios with the gateway?  
**Answer:** [High availability clusters of on-premises data gateways](service-gateway-high-availability-clusters.md) help with avoiding a single point of failure. Cloud services like PowerApps or Power BI use the primary node by default, but falls back to the secondary in case the primary is unavailable.

**Question:** What options are available for disaster recovery?  
**Answer:** You can use the recovery key to [restore](service-gateway-migrate.md) or move a gateway. When you install the gateway, supply the recovery key.

**Question:** What is the benefit of the recovery key?  
**Answer:** It provides a way to migrate, recover, take over, or add a new gateway to the cluster.

## Troubleshooting

**Question:** Where are the gateway logs located?  
**Answer:** See [Troubleshooting tools](service-gateway-tshoot.md#troubleshooting-tools).

**Question:** How can I see what queries are being sent to the on-premises data source?  
**Answer:** You can enable query tracing by turning on [Additional logging](service-gateway-performance.md#slow-performing-queries).  This will include the queries being sent. Remember to turn query tracing back off when done troubleshooting. Having query tracing enabled will cause the logs to be larger.

You can also look at tools your data source has for tracing queries. For example, for SQL Server and Analysis Services you can use Extended Events or SQL Profiler.

## Administration

**Question:** Can I have more than one admin for a gateway?  
**Answer:** Yes. When you manage a gateway, you can go to the administrator’s tab to add additional admins. You can also have security groups as admins.

**Question:** Does the gateway admin need to be an admin on the machine where the gateway is installed?  
**Answer:** No. The gateway admin is used to manage the gateway from within the service.

## Next steps

* [Troubleshoot the on-premises data gateway](service-gateway-tshoot.md)
