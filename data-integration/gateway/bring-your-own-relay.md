---
title: Bring your own relay for on-premises data gateway
description: Learn how to use a bring your own relay to keep data in the region where it's stored.
ms.topic: conceptual
ms.date: 11/4/2022
---

# Bring your own relay for on-premises data gateway

If you want to keep your data within the region where it’s stored, all you need to do is:

* [Bring your own relay](service-gateway-azure-relay.md) that lives in the same region as the data.
* Make sure your capacity is in the same region.

When you install an on-premises data gateway, it must be in the home tenant region to work with Power BI. The Azure Relay used to transfer your data automatically gets installed in the same region. However, if you set up your own relay, then the data will transfer through that relay instead in its location. Data will go from there to the capacity. Only metadata will go to the gateway application in the home region and this can't be changed. This means you can keep your data within the region it’s stored in if your relay, the capacity, and the data are all in the same region.

## Next steps

* [What is Azure Relay?](/azure/azure-relay/relay-what-is-it)

[!INCLUDE[footer-include](../includes/footer-banner.md)]
