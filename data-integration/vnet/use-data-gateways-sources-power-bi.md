---
title: Use virtual network (VNet) data gateway and data sources in Power BI
description: Provides information about how to use virtual network (VNet) data gateway and data sources in Power BI.
author: arthiriyer
ms.reviewer: kvivek
ms.prod: on-premises-data-gateway
ms.technology:
ms.topic: conceptual
ms.date: 03/01/2021
ms.author: arthii
---

# Use virtual network data gateway and data sources in Power BI

You can manage admins for a virtual network (VNet) data gateway like you do for standard data gateways either in the Power Platform admin center or on the **Manage gateways** page in Power BI.

![Manage VNet data gateways](media/vnet-in-pbi.png)

## Manage data sources

You can also create data sources and share these data sources to users like you do today for data sources created on the standard data gateway.

![Manage data source](media/manage-data-source.png)

## Supported Azure Data services 

In teh current release, VNet data gateways will support connectivity to the following Azure data services: 
- Azure SQL
- Azure Synapse Analytics
- Azure Data Explorer (Kusto)
- Azure Table Storage
- Azure Blob Storage
- Azure HDInsight (Spark) 
- Azure Data Lake (Gen2)
- Cosmos DB

## Azure Active Directory Single Sign-On for Direct Query

When a user interacts with a DirectQuery report in the Power BI Service, each cross-filter, slice, sort, and report editing operation can result in queries that execute live against the underlying Azure VNet data source. When you configure Single Sign-On (SSO) for an applicable data source, queries execute under the Azure Active Directory (Azure AD) identity of the user that interacts with Power BI.

To enable Azure AD SSO, on the **Manage Gateways** page in Power BI, go to the **Data source setting** page, and select the **Use SSO via Azure AD for Direct Queries** check box.

![Azure AD SSO for Direct Query](media/azure-ad-sso.png)

## Use virtual network (VNet) data gateways in Power BI datasets

A Power BI report maker or creator can now publish a report and associate the dataset to the VNet data gateway data source if the person has been added as a data source user.

![Use in Power BI datasets](media/use-in-pbi-datasets.png)

