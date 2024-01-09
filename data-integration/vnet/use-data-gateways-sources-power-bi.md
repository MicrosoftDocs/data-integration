---
title: Use virtual network (VNet) data gateway and data sources in Power BI
description: Provides information about how to use virtual network (VNet) data gateway and data sources in Power BI.
ms.topic: conceptual
ms.date: 12/10/2023
---

# Use virtual network data gateway and data sources in Power BI

Virtual network data gateways allow import or direct query datasets to connect to data services within an Azure VNet without the need of an on-premises data gateway.

> [!NOTE]
> Virtual network data gateways is a Premium and Embedded feature, and will be available only in Power BI Premium workspaces, Premium Per User (PPU), and Power BI Embedded for public preview. However, licensing requirements might change when VNet data gateways become generally available.

## Manage Virtual network data gateways

You can manage admins for a virtual network (VNet) data gateway like you do for standard data gateways either in the Power Platform admin center or on the **Manage gateways** page in Power BI.

:::image type="content" source="media/vnet-in-pbi.png" alt-text="Screenshot of the Gateway Cluster Settings page with a VNet gateway selected and the gateway's data displayed.":::

## Manage data sources

You can also create data sources and share these data sources to users like you do today for data sources created on the standard data gateway.

:::image type="content" source="media/manage-data-source.png" alt-text="Screenshot of the Data Source Settings page with the data source settings filled out.":::

## Supported Azure data services

In the current release, VNet data gateways support connectivity to the following data sources:

- Azure SQL
- Azure Synapse Analytics
- Azure Databricks
- Azure Data Explorer (Kusto)
- Azure Table Storage
- Azure Blob Storage
- Azure HDInsight (Spark)
- Azure Data Lake (Gen2)
- Cosmos DB
- Azure SQL Managed Instance (MI)
- Snowflake on Azure
- PostgreSQL
- SQL Server
- And more&mdash;all data sources shown when creating a connection are supported

> [!NOTE]
>SQL Server on a virtual machine (VM) isn't supported.

## Azure Active Directory single sign-on for Direct Query

When a user interacts with a DirectQuery report in the Power BI Service, each cross-filter, slice, sort, and report editing operation can result in queries that execute live against the underlying Azure VNet data source. When you configure single sign-on (SSO) for an applicable data source, queries execute under the Azure Active Directory (Azure AD) identity of the user that interacts with Power BI.

To enable Azure AD SSO, on the **Manage Gateways** page in Power BI, go to the **Data source settings** page, and select the **Use SSO via Azure AD for Direct Queries** check box.

:::image type="content" source="media/azure-ad-sso.png" alt-text="Screenshot of the data source settings page with Use SSO via Azure AD for Direct queries emphasized.":::

## Use virtual network (VNet) data gateways in Power BI datasets

A Power BI report maker or creator can now publish a report and associate the dataset to the VNet data gateway data source.

:::image type="content" source="media/use-in-pbi-datasets.png" alt-text="Screenshot of the Gateway connection showing the data sources included in the dataset.":::
