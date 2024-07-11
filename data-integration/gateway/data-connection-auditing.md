---
title: Data connection auditing for exfiltration protection
description: Learn how to use data connection auditing for data exfiltration protection in Microsoft Fabric and Power BI across your tenant.
ms.topic: concept-article
ms.date: 06/13/2024
#customer intent: As a tenant administrator, I want to secure and protect my organizations data from eunwanted xfiltration.
---

# Use data connection auditing to protect your tenant from data exfiltration

Learn how to use data connection auditing to protect your tenant from data exfiltration in Microsoft Fabric data pipelines and Dataflows Gen2, and Power BI semantic models and datamarts.

## What is data exfiltration

Data exfiltration occurs when sensitive business data is accidentally or intentionally moved outside of a trusted boundary. Fabric data pipelines and Dataflows Gen2, and Power BI semantic models and datamarts, are all Microsoft 365 services that enable users to easily connect to, extract, move, and transform data across hundreds of supported data sources. Dataflows and semantic models both build upon an underlying service called Power Query Online, which hosts the data movement engine (Mashup Engine) as a cloud service. By default, connectivity originates from this cloud location and has unrestricted access to the internet. Therefore, when using Dataflows Gen 2 or Power BI semantic models to access and move sensitive data, organizations should consider strategies to deter insiders from accidental or malicious data exfiltration.

## How to use data connection auditing

This article outlines the capability to view audit logs on all actions taken on connections in your tenant. You can view all attempted create, read, update or delete actions(CRUDs), and all retrieval of data from all your data sources across your tenant.

We're excited to announce auditing for all activity on data source connections within Fabric for the following artifacts: data pipelines, Dataflows Gen2, semantic models, and datamarts. Tenant admins can now use the Purview auditing portal to find any call made to a connection, including both failed and successful calls to create, delete, update, or use connections. For each connection, users can find all connections by querying:

- Time period
- Data source name
- Data source path
- Data source kind
- Gateway ID

For each attempted connection, we include the following information:

- Status: Success or failed
- Creation time and date
- User object ID
- Data source kind
- Data source path
- Gateway Object ID
- Credential Type
- Request ID
- Activity ID

## Get started with data policies

To get started with data polices, just log in to your Power BI or Fabric environment and run one of the supported artifacts:

- Microsoft Fabric data pipelines
- Microsoft Fabric Dataflows Gen2
- Power BI semantic models
- Power BI datamarts

Then go to Microsoft Purview while logged in to the same tenant as the same user and use an [Audit New Search](/purview/audit-search) to query the logs.

## Related content

[Troubleshoot the on-premises data gateway](service-gateway-tshoot.md)
