---
title: Tenant level administration for the on-premises data gateway
description: Describes how an admin can manage all on-premises data gateways within their tenant.
author: mgblythe
ms.author: mblythe
manager: kfile
ms.reviewer: ''
ms.technology: on-premises-data-gateway
ms.topic: conceptual
LocalizationGroup: Gateways
ms.date: 07/15/2019
---

# Tenant-level administration for the on-premises data gateway

[!INCLUDE [gateway-rewrite](../includes/gateway-rewrite.md)]

You can use the Power Platform Admin center to get visibility into all on-premises data gateways in a tenant. To do so, sign in as a tenant admin and select the **Data Gateways** option.

> [!NOTE]
> Only users who are part of the Azure Active Directory (Azure AD) tenant's global admin role will see the **Data Gateways** option. This role includes Office 365 global admins.

![On-premises data gateway page](media/service-gateway-tenant-level-admin/tenant-data-gateway.png)

The Gateways page lists all gateway clusters installed on the tenant. On this page, you can also review the following information about these clusters.

* **Gateway Cluster Name**: The name of the gateway cluster.
* **Contact info**: Admin contact information for the gateway cluster.
* **Administrators**: The list of gateway admins.
* **Gateways**: The number of gateway members in the gateway cluster.

## Display gateway members

To see the gateway members, device name, and version in a gateway cluster, select the **Open in new window** icon (![Icon for opening in new window](media/service-gateway-tenant-level-admin/open-icon.png)) next to the gateway cluster name.

![Selecting the icon for opening in a new window](media/service-gateway-tenant-level-admin/open-in-new-window.png)

## Manage gateway admins

To see the list of gateway admins, select the **People** icon (![People icon](media/service-gateway-tenant-level-admin/people-icon.png)) next to the gateway cluster name. Add or remove gateway admins in the **Manage Administrators** page.

For each on-premises data gateway (personal mode), this page shows the gateway owner. The owner can't be changed because of the security scope of such gateways.

![Page for managing admins](media/service-gateway-tenant-level-admin/manage-admins.png)

## Search

Select the **Search** icon to find gateway clusters and see their details. You can search for gateway cluster names and contact info but not admins.

![The Search icon highlighted](media/service-gateway-tenant-level-admin/gateway-search.png)

## Next steps

* [Manage an on-premises data gateway](service-gateway-manage.md)
* [Manage high availability clusters and load balancing](service-gateway-high-availability-clusters.md)
