---
title: Use virtual network (VNet) data gateway and data sources in Power BI
description: Provides information about how to use virtual network (VNet) data gateway and data sources in Power BI.
ms.topic: conceptual
ms.date: 1/17/2024
---

# Use virtual network data gateway and data sources in Power BI

Virtual network data gateways allow import or direct query semantic models to connect to data services within an Azure VNet without the need of an on-premises data gateway.

> [!NOTE]
> Virtual network data gateways is a Premium and Embedded feature, and will be available only in Power BI Premium workspaces, Premium Per User (PPU), and Power BI Embedded for public preview.

## Manage Virtual network data gateways

You can manage admins for a virtual network (VNet) data gateway like you do for standard data gateways either in the Power Platform admin center or on the **Manage gateways** page in Power BI.

:::image type="content" source="media/vnet-in-pbi.png" alt-text="Screenshot of the Gateway Cluster Settings page with a VNet gateway selected and the gateway's data displayed.":::

## Manage data sources

You can also create data sources and share these data sources to users like you do today for data sources created on the standard data gateway.

:::image type="content" source="media/manage-data-source.png" alt-text="Screenshot of the Data Source Settings page with the data source settings filled out.":::

## Supported Azure data services

In the current release, VNet data gateways support connectivity to all of the following data sources.

Supported sources with secure connectivity:
- Azure Batch
- Azure Blob Storage
- Azure Cosmos DB v1
- Azure Cosmos DB v2
- Azure Cost Management
- Azure Data Explorer (Kusto)
- Azure Data Factory Workspace
- Azure Data Lake Analytics
- Azure Data Lake Storage Gen1
- Azure Data Lake Storage Gen2
- Azure Databricks
- Azure Databricks workspace
- Azure DevOps (Boards only)
- Azure Function
- Azure HDInsight on AKS Trino
- Azure HDInsight Spark
- Azure Keyvault Service
- Azure Machine Learning
- Azure Resource Graph
- Azure Synapse Analytics workspace
- Azure Synapse Workspace
- Azure SQL
- Azure Table Storage

Sources supported with public endpoints:
- AdMaD
- Admin Insights
- Amazon Redshift
- Amazon S3
- Analysis Services
- Anaplan Connection Configuration
- appFigures
- AriaConnector
- Asana
- Assemble Views
- AtScale cubes
- Autodesk Construction Cloud
- Automation Anywhere
- AutomyDataAnalytics
- AutoPremium
- BitSightSecurityRatings
- Bloomberg Data and Analytics  v1.1.3
- BQECore
- Capacity Metrics
- CData Connect Cloud
- Celonis EMS
- Cherwell Data Connector v1.0
- CloudScope
- CloudScopeInstagram
- Cognite Data Fusion (CDF)
- Common Data Service (Legacy)
- Connect to comScore Digital Analytix
- Connect to Viva Insights Data
- CSV
- Databricks
- Dataflows
- Datamarts
- Dataverse
- DataWorld.semantic model
- DCW - Integrations Platform Insights
- Delta Sharing
- Dremio Cloud
- Dremio Software
- Dynamics 365 Business Central
- Dynamics 365 Business Central (on-premises)
- Dynamics 365 Customer Insights
- Dynamics NAV
- Eduframe
- ElasticSearch
- Emigo.Contents
- EmplifiMetrics
- EntersoftBusinessSuite
- EQuIS
- EventHub
- eWayCRM
- FactSetAnalytics
- FactSetRMS
- Fhir
- From Paxata
- FTP
- GitHub
- Goals
- Google BigQuery
- Google BigQuery (Azure AD)
- Google Cloud Storage
- Google Sheets
- HDInsight Interactive Query
- Hexagon PPM Smart API
- Hive LLAP
- IBM Netezza
- Impala
- Azure Enterprise
- IndustrialAppStore
- InfinityConnector
- Information Grid BI Services
- Intune Data Warehouse
- IoTHub
- JamfPro
- JDIConnector
- KaizalaAttendanceReports
- KaizalaReports
- KaizalaSurveyReports
- Kognitwin v1.1
- Lakehouse
- LinkedIn Sales Navigator
- MetricsCES
- MetricsDataConnector
- Microsoft Teams Personal Analytics
- Microsoft365
- MicrosoftCallQuality
- MicroStrategy for Power BI ver. 2.4.5
- mixpanel
- MongoDBAtlasForPipeline
- MongoDBForPipeline
- myob_ar
- Navigational data
- OData
- Office365Mon2
- Plantronics
- Planview Enterprise Architecture
- Planview IdeaPlace
- Planview OKR
- Planview Portfolios
- Planview ProjectPlace
- PostgreSQL
- Power BI dataflows (Legacy)
- PowerBI Semantic Model
- ProductInsights
- Productioneer Connector
- Profisee
- QuestionPro Connector
- Quick Base Connector
- QuickBooks Online
- Roamler
- Salesforce Objects
- ScopevisioPowerBICon
- SentryOne
- SFTP
- ShareAdvance ProjectIntelligence Data Source Information
- SharePoint
- ShortcutsBI
- SIS-CC SDMX Connector for SDMX-CSV web services
- Siteimprove
- Smartsheet.Tables
- Snowflake
- SocialbakersMetrics
- SoftOne BI
- SolarWindsServiceDesk
- Solver
- Spark
- SparkPost
- SpotlightCloudReports
- Azure SQL
- SumTotal BI Connector
- SurveyMonkey
- SweetIQ
- TeamDesk.Database
- Tenforce (Smart)List
- Timelog
- UsageMetricsCES
- UsageMetricsDataConnector
- Usercube
- UserVoice
- Vena 1.0.4
- Vertica
- VesselInsight
- VoiceAnalytics
- Warehouse
- Web
- Web V2
- Webtrends Analytics
- Witivio 365 - Configuration
- Wrike
- WtsParadigm
- Xero - Contents
- Zendesk
- Zoho Creator
- Zucchetti HR Infinity

## Microsoft Entra ID single sign-on for Direct Query

When a user interacts with a DirectQuery report in the Power BI Service, each cross-filter, slice, sort, and report editing operation can result in queries that execute live against the underlying Azure VNet data source. When you configure single sign-on (SSO) for an applicable data source, queries execute under the Microsoft Entra ID identity of the user that interacts with Power BI.

To enable Microsoft Entra ID SSO, on the **Manage Gateways** page in Power BI, go to the **Data source settings** page, and select the **Use SSO via Azure AD for Direct Queries** check box.

:::image type="content" source="media/azure-ad-sso.png" alt-text="Screenshot of the data source settings page with Use SSO via Microsoft Entra ID for Direct queries emphasized.":::

## Use virtual network (VNet) data gateways in Power BI semantic models

A Power BI report maker or creator can now publish a report and associate the semantic model to the VNet data gateway data source.

:::image type="content" source="media/use-in-pbi-datasets.png" alt-text="Screenshot of the Gateway connection showing the data sources included in the semantic model.":::
