---
title: Virtual network data gateway best practices
description: This article describes best practices and recommendations to improve performance and functioning for the virtual network data gateway.
ms.topic: troubleshooting
ms.date: 05/09/2024
---

# Virtual network data gateway best practices and recommendations

This article describes best practices and recommendations for the virtual network data gateway.

## Enable storage service endpoint in virtual network's delegated subnet

If you're using a storage account, for example Databricks, Snowflake, or Azure Data Lake Services (ADLS) Gen2, we suggest you enable a service endpoint for it inside the delegated subnet. This service endpoint ensures the service uses IPv6 and not IPv4.

1. Navigate to the subnet delegated to your virtual network data gateway.

   :::image type="content" source="media/vnet-best-practices/navigate-to-vnet-gateway-subnet.png" alt-text="Screenshot showing how to navigate to the virtual network for your gateway.":::

1. Scroll down to **Service Endpoints** and expand the dropdown menu.
   :::image type="content" source="media/vnet-best-practices/service-endpoints.png" alt-text="Screenshot showing where to select subnet Service Endpoints in your virtual network data gateway configuration in Azure.":::

1. Select **Microsoft.Storage**.

   :::image type="content" source="media/vnet-best-practices/save-endpoint.png" alt-text="Screenshot showing where to save the newly defined service endpoint.":::

## Related content

- [Overview of the virtual network data gateway](overview.md)
- [Troubleshoot the virtual network data gateway](troubleshoot-data-gateway.md)
- [Virtual network data gateway FAQs](data-gateway-faqs.yml)