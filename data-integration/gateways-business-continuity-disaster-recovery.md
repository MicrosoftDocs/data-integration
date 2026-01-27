---
title: Business Continuity and Disaster Recovery (BCDR) for On-premises Data Gateway and Virtual Network Data Gateway 
description: This article describes best practices and recommendations for the on-premises data gateway and virtual network data gateway business Continuity and Disaster Recovery (BCDR).
ms.topic: best-practice
ms.date: 7/25/2025
author: lrtoyou1223
ms.author: lle
---

# Business continuity and disaster recovery (BCDR) for gateways

Microsoft Fabric and Power Platform support two gateway types to enable secure data movement and access across hybrid networks: the On-premises Data Gateway and the Virtual Network Data Gateway. This document outlines their Business Continuity and Disaster Recovery (BCDR) behavior across different levels of Azure service availability disruptions.

## Availability zone-level resiliency

At the **Availability Zone** level, gateway services are designed to be fully resilient. Microsoft automatically distributes and manages infrastructure across multiple availability zones within the same Azure region.

- **Impact:** No customer action is required.
- **User experience**: Transparent to users. There's no downtime or impact to gateway-related operations.

## Region-level disruption

At the **Azure region** level, the behavior depends on the specific service and gateway configuration.

### Power BI service region failure

If the **Power BI service** in a region experiences a major outage:

- Power BI will **automatically fail over** to its **paired region**.
- The failover experience is limited to **read-only mode**:
      - Users can view reports and dashboards.
      - Data refresh, dataset modification, and other authoring features may be temporarily unavailable.

> [!NOTE]
> This applies only to the Power BI service. Gateway availability depends on other services as detailed below.

### Virtual network data gateway

The **Virtual Network Data Gateway**, hosted in a customer-managed Azure Virtual Network (VNet), is deployed regionally.

If the gateway region is unavailable:

- There is no **automatic failover**.
- Users must **manually provision** a backup gateway in the **paired Azure region** to ensure continuity.
- Workspaces and pipelines must be configured to target the backup gateway if failover is needed.

### On-premises data gateway

The **On-premises Data Gateway** depends on several Azure services to connect securely to cloud services, including **Azure Relay**.

If the **Azure Relay service** is down in a region:

- The On-premises Data Gateway will **stop working**, even if your local infrastructure is unaffected. 
- There is **no automatic failover** for the Azure Relay service. 
- Customers are encouraged to **install a second gateway** in a **paired region** and configure **redundant gateway clusters** for high availability. 

## Recommendations for customers

To enhance your business continuity and disaster recovery posture, Microsoft recommends the following actions:

For Virtual Network Data Gateway:

- Deploy a **secondary gateway** in a paired region.
- Use infrastructure-as-code (e.g., ARM, Bicep, Terraform) to automate deployment and configuration.

For On-premises Data Gateway:

- Configure **high availability clusters**.
- Install gateways in **multiple Azure regions** if your scenarios are sensitive to regional failures.
- Monitor gateway connectivity and set up alerts for failure detection.

## Summary table

|Failure scope |Gateway type |Automatic failover |User action required |Impact |
|-----------|-----------|----------|-----------------|---------------|
|Availability Zone Failure |Both |Yes |No |No impact. Fully transparent. |
|Region Failure (Power BI) |Power BI Service |Partial |No |Read-only mode; some functionality unavailable.|
|Region Failure |Virtual Network Gateway |No |Yes (manual failover setup) |Must manually provision gateway in paired region. |
|Region Failure |On-premises Gateway |No |Yes (manual failover setup) |Gateway fails if Azure Relay is down. Cluster or regional redundancy recommended. |
