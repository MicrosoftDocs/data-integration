---
title: On-premises data gateway architecture
description: This article looks at the on-premises gateway in-depth. It looks at how the service works with Microsoft Entra ID and your on-premises Active Directory.
ms.topic: concept-article
ms.date: 6/10/2025
ms.custom: intro-internal
---

# On-premises data gateway architecture

Users in your organization can access on-premises data to which they already have access authorization from services in the cloud like Power BI, Power Platform, and Microsoft Fabric. But before those users can connect the cloud service to your on-premises data source, an on-premises data gateway needs to be installed and configured.

The gateway facilitates quick and secure behind-the-scenes communication. This communication flows from a user in the cloud to your on-premises data source and then back to the cloud.

An admin is usually the one who installs and configures a gateway. These actions might require special knowledge of your on-premises servers or Server Administrator permissions.

This article doesn't provide step-by-step guidance on how to install and configure the gateway. For that guidance, go to [Install an on-premises data gateway](service-gateway-install.md). This article does provide in-depth understanding of how the gateway works.

## How the gateway works

:::image type="content" source="./media/service-gateway-onprem-indepth/on-prem-data-gateway-how-it-works.png" alt-text="Diagram illustrating the relationship among cloud services, gateway, and data sources.":::

Let's first look at what happens when you interact with an element that is connected to an on-premises data source.

> [!NOTE]
> Depending on the cloud service, you might need to configure a data source for the gateway.

1. The cloud service creates a query and the encrypted credentials for the on-premises data source. The query and credentials are sent to the gateway queue for processing when the gateway polls the service periodically. For more information about credential encryption in Power BI, go to [Power BI security whitepaper](/power-bi/guidance/whitepaper-powerbi-security).
1. The gateway cloud service analyzes the query and pushes the request to [Azure Relay](/azure/azure-relay/relay-what-is-it).
1. Azure Relay sends the pending requests to the gateway when it polls periodically. Both the gateway and Power BI service are implemented to only accept Transport Layer Security (TLS) 1.2 traffic.
1. The gateway gets the query, decrypts the credentials, and connects to one or more data sources with those credentials.
1. The gateway sends the query to the data source to be run.
1. The results are sent from the data source back to the gateway and then to the cloud service. The service then uses the results.

In step 6, queries like Power BI and Azure Analysis Services refreshes can return large amounts of data. For such queries, data is temporarily stored on the gateway machine. This data storage continues until all data is received from the data source. The data is then sent back to the cloud service. This process is called spooling. We recommend you use a solid-state drive (SSD) as the spooling storage.

## Authentication to on-premises data sources

A stored credential is used to connect from the gateway to on-premises data sources. Regardless of the user, the gateway uses the stored credential to connect. But there might be authentication exceptions like DirectQuery and LiveConnect for Analysis Services in Power BI. For more information about credential encryption in Power BI, go to [Power BI security whitepaper](/power-bi/guidance/whitepaper-powerbi-security).

## Sign-in account

You sign in with either a work account or a school account. This account is your organization account. If you signed up for an Office 365 offering and didn't supply your actual work email address, your account name might look like `nancy@contoso.onmicrosoft.com`. A cloud service stores your account within a tenant in Microsoft Entra ID. In most cases, the User Principal Name (UPN) of your Microsoft Entra ID account matches your email address.

## Network traffic security

Traffic goes from the gateway to Azure Relay to the Power BI backend cluster. By using Azure ExpressRoute, you can make sure this traffic doesn't traverse the public internet. All Azure internal traffic goes over the Azure backbone.

## Microsoft Entra ID

Microsoft cloud services use [Microsoft Entra ID](/entra/fundamentals/whatis) to authenticate users. Microsoft Entra ID is the tenant that contains usernames and security groups. Typically, the email address that you use for sign-in is the same as the UPN of your account. For more information about authentication in Power BI, go to [Power BI security whitepaper](/power-bi/guidance/whitepaper-powerbi-security).

### How do I tell what my UPN is?

You might not know your UPN, and you might not be a domain admin. To find out the UPN for your account, run the following command from your workstation: `whoami /upn`.

Although the result looks like an email address, it's the UPN on your local domain account.

### Synchronize an on-premises Active Directory with Microsoft Entra ID

You want each of your on-premises Active Directory accounts to match a Microsoft Entra ID account, because the UPN for both accounts must be the same.

The cloud services know only about accounts within Microsoft Entra ID. It doesn't matter if you add an account in your on-premises Active Directory. If the account doesn't exist in Microsoft Entra ID, it can't be used.

There are different ways to match your on-premises Active Directory accounts with Microsoft Entra ID.

* Add accounts manually to Microsoft Entra ID.

    Create an account on the Azure portal or within the Microsoft 365 admin center. Make sure the account name matches the UPN of the on-premises Active Directory account.

* Use the [Microsoft Entra ID Connect](/entra/identity/hybrid/connect/how-to-connect-sync-whatis) tool to synchronize local accounts to your Microsoft Entra ID tenant.

    The Microsoft Entra ID Connect tool provides options for directory synchronization and authentication setup. These options include password hash sync, pass-through authentication, and federation. If you're not a tenant admin or a local domain admin, contact your IT admin to get Microsoft Entra ID Connect configured.

 Microsoft Entra ID Connect ensures that your Microsoft Entra ID UPN matches your local Active Directory UPN. This matching helps if you're using Analysis Services live connections with Power BI or single sign-on (SSO) capabilities.

> [!NOTE]
> Synchronizing accounts with the Microsoft Entra ID Connect tool creates new accounts within your Microsoft Entra ID tenant.

## Related content

* [On-premises data gateway FAQ](service-gateway-onprem-faq.yml)  
* [Azure Relay](/azure/azure-relay/relay-what-is-it)  
* [Microsoft Entra ID Connect](/entra/identity/hybrid/connect/how-to-connect-sync-whatis)  
