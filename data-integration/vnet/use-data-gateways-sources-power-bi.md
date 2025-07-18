---
title: Use virtual network data gateway and data sources in Power BI
description: Provides information about how to use virtual network data gateway and data sources in Power BI.
ms.topic: conceptual
ms.date: 6/13/2025
---

# Use virtual network data gateway and data sources in Power BI

Virtual network data gateways allow import or direct query semantic models to connect to data services within an Azure virtual network.

In Power BI, virtual network data gateways require a Power BI Premium capacity license (A4 or higher or any F or P).

## Manage virtual network data gateways

You can manage admins for a virtual network data gateway like you do for standard data gateways either in the Power Platform admin center or on the **Manage connections and gateways** page in Power BI.

:::image type="content" source="media/vnet-in-pbi.png" alt-text="Screenshot of the Gateway Cluster Settings page with a virtual network gateway selected and the gateway's data displayed.":::

## Manage data sources

You can also create data sources and share these data sources to users like you do today for data sources created on the standard data gateway.

:::image type="content" source="media/manage-data-source.png" alt-text="Screenshot of the Data Source Settings page with the data source settings filled out.":::

## Supported Azure data services

The virtual network data gateway can be used to connect securely to your data sources. There are a few different ways you can use the virtual network to connect:

1. Connecting to your private resources in Azure. For this scenario, you need to create a private endpoint and private Domain Name System (DNS) zone or service endpoints on your data source.
2. Connecting to your private resources outside of Azure. For this scenario, you need to use Express Route and/or VPNs.
3. Connecting to public resources.

In scenarios 1 and 2, all traffic remains on the Azure backbone and is never exposed to the public internet.

Azure sources that support secure private endpoint connectivity (as in scenario 1):

- Azure AI Search
- Azure Batch
- Azure Blob Storage
- Azure Cosmos DB v1
- Azure Cosmos DB v2
- Azure Database for PostgreSQL
- Azure Data Explorer (Kusto)
- Azure Data Factory Workspace
- Azure Data Lake Analytics
- Azure Data Lake Storage Gen1
- Azure Data Lake Storage Gen2
- Azure Databricks
- Azure Databricks workspace
- Azure DevOps Services(Boards only)
- Azure Function
- Azure HDInsight Cluster
- Azure HDInsight on Azure Kubernetes Services (AKS) Trino
- Azure HDInsight on Demand Cluster
- Azure HDInsight Spark
- Azure Keyvault Service
- Azure Machine Learning
- Azure Resource Graph
- Azure Synapse Analytics workspace
- Azure Synapse Workspace
- Azure SQL
- Azure SQL Managed Instance
- Azure Table Storage
- Azure Snowflake

Sources supported through either public endpoints or secure private endpoint connectivity with Express Route or VPNs (scenarios 2 and 3):

- Acterys
- Access Database
- Adobe Analytics
- AdMaD
- Admin Insights
- Amazon Relational Database Service for SQL Server
- Amazon Redshift
- Amazon S3
- Analysis Services
- Anaplan Connection Configuration
- appFigures
- Aptix - Integrations Platform Insights
- AriaConnector
- Asana
- AssembleViews
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
- CloudBluePSA
- CloudScope
- CloudScopeInstagram
- Cognite Data Fusion (CDF)
- Common Data Service (Legacy)
- Confluent Cloud
- comScore Digital Analytix
- VivaInsights Data
- Databricks
- Dataflows
- Datamarts
- Dataverse
- DataWorld.semantic model
- Digital Construction Works Insights
- Delta Sharing
- Digital Analytix
- Dremio Cloud
- Dremio Software
- Dynamics 365
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
- Event Hubs
- eWayCRM
- Excel
- Fabric Data Pipelines
- FactSetAnalytics
- FactSetRMS
- Fhir
- Paxata
- FTP
- GitHub
- GitHub - Source Control (preview)
- Goals
- Google Pub Sub
- Google BigQuery
- Google BigQuery (Microsoft Entra ID)
- Google Cloud Storage
- Google Sheets
- HDInsight Interactive Query
- Hexagon PPM Smart API
- Hive Live Long and Process (LLAP)
- Http
- HTML
- IBM Netezza
- Impala
- Azure Enterprise
- IndustrialAppStore
- InfinityConnector
- Information Grid BI Services
- Intune Data Warehouse
- inwink source
- IoTHub
- JamfPro
- JDIConnector
- JSON
- KaizalaAttendanceReports
- KaizalaReports
- KaizalaSurveyReports
- Kinesis
- Kognitwin v1.1
- Lakehouse
- LEAP.Contents
- LinkedIn Sales Navigator
- LinkedIn Learning
- Microsoft Outlook
- Microsoft Teams
- MetricsCES
- MetricsDataConnector
- Microsoft Cost Management
- Microsoft Teams Personal Analytics
- Microsoft 365
- MicrosoftCallQuality
- MicroStrategy for Power BI ver. 2.4.5
- mixpanel
- MongoDBAtlasForPipeline
- MongoDBForPipeline
- myob_ar
- MySQL
- Navigational data
- OData
- Office365Mon2
- Oracle Cloud Storage
- Plantronics
- Planview Enterprise Architecture
- Planview IdeaPlace
- Planview Objectives and Key Results (OKR)
- Planview Portfolios
- Planview ProjectPlace
- PostgreSQL
- Power BI dataflows (Legacy)
- Power BI Semantic Model
- ProductInsights
- Productioneer Connector
- Profisee
- QuestionPro Connector
- Quick Base Connector
- QuickBooks Online
- REST
- Roamler
- Samsara API Get Records (Beta)
- Salesforce Objects
- ScopevisioPowerBICon
- Secure File Transfer Protocol (SFTP)
- SentryOne
- ShareAdvance ProjectIntelligence Data Source Information
- SharePoint
- ShortcutsBI
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
- Statistical Information System Collaboration Community (SIS-CC) Statistical Data and Metadata Exchange (SDMX) Connector for SDMX-CSV web services
- SQL Server
- SumTotal BI Connector
- SurveyMonkey
- Supermetrics
- SweetIQ
- TeamDesk.Database
- Tenforce (Smart) List
- Timelog
- UsageMetricsCES
- UsageMetricsDataConnector
- Usercube
- UserVoice
- VivaInsights Data
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
- XML
- Zendesk
- Zoho Creator
- Zucchetti HR Infinity

## Microsoft Entra ID single sign-on for DirectQuery

When a user interacts with a DirectQuery report in the Power BI service, each cross-filter, slice, sort, and report editing operation can result in queries. The queries execute live against the underlying Azure virtual network data source. When you configure single sign-on (SSO) for an applicable data source, queries execute under the Microsoft Entra ID identity of the user that interacts with Power BI.

To enable Microsoft Entra ID SSO, on the **Manage Gateways** page in Power BI, go to the **Data source settings** page, and select the **Use SSO via Azure AD for Direct Queries** check box.

:::image type="content" source="media/azure-ad-sso.png" alt-text="Screenshot of the data source settings page with Use SSO via Microsoft Entra ID for DirectQuery queries emphasized.":::

## Use virtual network data gateways in Power BI semantic models

A Power BI report maker or creator can now publish a report and associate the semantic model to the virtual network data gateway data source.

:::image type="content" source="media/use-in-pbi-datasets.png" alt-text="Screenshot of the Gateway connection showing the data sources included in the semantic model.":::
