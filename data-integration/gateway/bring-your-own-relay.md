---
title: Bring your own relay for on-premises data gateway
description: Learn how to use a "bring your own relay" to keep data in the region where it's stored.
ms.topic: conceptual
ms.date: 11/4/2022
---

# Bring your own relay for on-premises data gateway

If you want to keep your data within the region where it’s stored, all you need to do is:

* [Bring your own relay](service-gateway-azure-relay.md) that lives in the same region as the data.
* Make sure your capacity is in the same region.

When you install an on-premises data gateway, it must be in the home tenant region to work with Power BI. Data from your gateway must travel to the relay then to the location of your [Power BI capacity](/power-bi/enterprise/service-admin-premium-manage). An Azure Relay automatically gets installed in the same region as the on-premises data gateway.

However, you have the option to choose your own relay in a different location. Then, the data will transfer through the location of your assigned relay instead. Only metadata will go to the gateway application in the home region and this condition can't be changed. This means you can keep your data within the region it's stored in if your relay, the capacity, and the data are all in the same region.

## Additional information

* [Set the Azure Relay for on-premises data gateway](service-gateway-azure-relay.md)
* [What is Azure Relay?](/azure/azure-relay/relay-what-is-it)

[!INCLUDE[footer-include](../includes/footer-banner.md)]
