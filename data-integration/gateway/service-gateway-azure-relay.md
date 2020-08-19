---
title: "Set the Azure Relay for on-premises data gateway"
description: Learn how to change the details of the Azure Relay for an on-premises data gateway.
author: arthiriyer
manager: kfile
ms.reviewer: ''

ms.technology: on-premises-data-gateway
ms.topic: conceptual
ms.date: 08/19/2020
ms.author: arthii


LocalizationGroup: Gateways
---

# Set the Azure Relay for on-premises data gateway

During installation of the on-premises data gateway, the Azure Relays are automatically provisioned. However, you have the option to provide your own relay details.

**To provide your own relay details**

1.	Select **Provide Relay details**. 

    ![Select Provide Relay details](media/service-gateway-azure-relay/configure-gateway-2.png)

2.	You can now provide additional details about your relay.

    ![Provide additional relay details](media/service-gateway-azure-relay/provide-relay-details.png)
 
    1. **WCF Relay endpoint URI**&mdash;Provide the URI (highlighted below) for your WCF relay from the Azure portal.

       ![Provide the WCF relay URI](media/service-gateway-azure-relay/wfc-relay-uri.png)
  
    2. **Send key value and the Listen Key Value**&mdash;Create two shared access policies, one called SendAccessKey and the other ListenAccessKey. Provide either the primary or the secondary keys in the on-premises data gateway app. To learn more, see [Azure Relay authentication and authorization](https://docs.microsoft.com/azure/azure-relay/relay-authentication-and-authorization).

       ![Send and listen access keys](media/service-gateway-azure-relay/send-access-key-policy.png)

>[!Note]
>If you recover an existing gateway with customized relay details to a new machine, you'll have to explicitly uninstall the gateway from the old machine or rotate the sender and listener keys. If this operation isn’t done, then queries through this gateway may fail.

## Next steps

- [What is Azure Relay?](https://docs.microsoft.com/azure/azure-relay/relay-what-is-it)
  
. 
