---
title: Data connection auditing for exfiltration protection
description: Learn how to use data connection auditing for data exfiltration protection in Microsoft Fabric and Power BI across your tenant.
ms.topic: concept-article
ms.date: 06/13/2024
#customer intent: As a tenant administrator, I want to secure and protect my organizations data from eunwanted xfiltration.
---

# Use data connection auditing to protect your tenant from data exfiltration

Learn how to use data connection auditing to protect your tenant from data exfiltration in Microsoft Fabric Dataflows Gen2 and Power BI semantic models.

## What is data exfiltration

Data exfiltration occurs when sensitive business data is accidentally or intentionally moved outside of a trusted boundary. Fabric Dataflows Gen2 and Power BI semantic models are Microsoft 365 services that enable users to easily connect to, extract, move, and transform data across hundreds of supported data sources. Dataflows and semantic models both build upon an underlying service called Power Query Online, which hosts the data movement engine (Mashup Engine) as a cloud service. By default, connectivity originates from this cloud location and has unrestricted access to the internet. Therefore, when using Dataflows Gen 2 or Power BI semantic models to access and move sensitive data, organizations should consider strategies to deter insiders from accidental or malicious data exfiltration.

## How to use data connection auditing

This article outlines the capability to view audit logs on all actions taken on connections in your tenant. You will be able to view all attempted CRUDs and GETs on your data sources across your tenant.  

We are excited to announce auditing for all activity on data source connections within Fabric for the following artifacts: data pipelines, Dataflows Gen2, semantic models, and datamarts. Tenant admins can now use the Purview auditing portal to find any call made to a connection. This includes failed and successful calls to create, delete, update, or use connections. For each connection, users will be able to find all connections by querying:

- Time period
- User (by user object id; they can get the id from user name through AAD Graph)
- Data source name
- Data source path
- Data source kind
- Gateway Id

For each attempted connection we will include the following information: 

- Status: Success or failed
- Creation time and date
- User object id
- Data source kind
- Data source path
- Gateway Object Id
- Credential Type
- Request Id
- Activity Id

## Get started with data policies

Follow these steps to get started with data policies for your tenant.

1. Log in to your Power BI or Fabric environment.
1. Run one of the supported artifacts:
    - Microsoft Fabric data pipelines
    - Microsoft Fabric Dataflows Gen2
    - Power BI semantic models
    - Power BI datamarts
1. Go to Microsoft Purview, logged in with the same user/tenant, and follow these instructions to query the logs [Audit New Search](/purview/audit-search).