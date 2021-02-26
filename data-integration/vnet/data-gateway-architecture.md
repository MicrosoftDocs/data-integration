---
title: Virtual network (VNet) data gateway architecture
description: Overview of virtual network (VNet) data gateway Architecture.
author: arthiriyer
ms.reviewer: kvivek
ms.prod: on-premises-data-gateway
ms.technology:
ms.topic: conceptual
ms.date: 03/01/2021
ms.author: arthii
---

# Virtual network data gateway architecture 

The virtual network (VNet) data gateway facilitates secure connectivity to data sources associated to your VNet. 

Users in your organization can access data secured by a VNet to which they already have access. But before these users can connect to these data sources from Microsoft Cloud services, a VNet gateway needs to be [registered and configured](). 

Let’s first look at what happens when you interact with a Power BI report that is connected to a data source within a VNet.
1.	Power BI cloud service (or one of the other supported cloud services) kicks off a query and sends the query, data source details and credentials to the Microsoft Power Platform VNet service.

2.	The Microsoft Power Platform VNet service then securely injects a container running the VNet data gateway into the subnet. This VNet data Gateway can now connect to data services accessible from within this subnet.

3.	The Microsoft Power Platform VNet service service then sends the query, data source details and credentials to the VNet data gateway. 

4.	The VNet data gateway gets the query and connects to the data sources with those credentials.

5.	The query is then sent to the data source for execution.

6.	After execution, the results are sent to the VNet data gateway and the Microsoft Power Platform VNet service securely pushes the data from the container to the cloud service.
 

