---
title: On-premises data gateway architecture
description: This article looks at the on-premises gateway in-depth. This looks at how the service works with Azure Active Directory and your local Active Directory.
author: mgblythe
manager: kfile
ms.reviewer: ''

ms.service: powerbi
ms.subservice: powerbi-gateways
ms.topic: conceptual
ms.date: 07/15/2019
ms.author: mblythe

LocalizationGroup: Gateways
---
# On-premises data gateway architecture

It's possible for users in your organization to access on-premises data (to which they already have access authorization), but before those users can connect to your on-premises data source, an on-premises data gateway needs to be installed and configured. The gateway facilitates quick and secure behind-the-scenes communication between a user in the cloud, to your on-premises data source, and then back to the cloud.

Installing and configuring a gateway is usually done by an administrator. It may require special knowledge of your on-premises servers and in some cases may require Server Administrator permissions.

This article doesn’t provide step-by-step guidance on how to install and configure the gateway. For that, be sure to see [Install an-premises data gateway](service-gateway-install.md). This article is meant to provide you with an in-depth understanding of how the gateway works.

## How the gateway works

![How the on-premises data gateway works](./media/service-gateway-onprem-indepth/on-prem-data-gateway-how-it-works.png)

Let’s first look at what happens when a user interacts with an element connected to an on-premises data source.

> [!NOTE]
> Depending on the cloud service, you will need to configure a data source for the gateway.

1. A query will be created by the cloud service, along with the encrypted credentials for the on-premises data source, and sent to the queue for the gateway to process.
2. The gateway cloud service will analyze the query and will push the request to the [Azure Service Bus](/azure/service-bus-messaging/service-bus-messaging-overview/).
3. Azure Service Bus sends the pending requests to the on-premises data gateway.
4. The gateway gets the query, decrypts the credentials, and connects to the data source(s) with those credentials.
5. The gateway sends the query to the data source for execution.
6. The results are sent from the data source, back to the gateway, and then onto the cloud service. The service then uses the results.

For queries returning large amounts of data in step 6 (like Power BI refreshes and AAS refreshes), data is temporarily stored on disk (SSD recommended) on the gateway machine, until all data is received from the data source. It is then sent back to the cloud service. This process is called spooling.

## Authentication to on-premises data sources

A stored credential will be used to connect to on-premises data sources from the gateway. Regardless of the individual user, the gateway uses the stored credential to connect. There may be exceptions, for example DirectQuery and LiveConnect (for Analysis Services) in Power BI.

## Sign in account

Users sign in with either a work or school account. This is your organization account. If you signed up for an Office 365 offering and didn’t supply your actual work email, it may look like nancy@contoso.onmicrosoft.com. Your account, within a cloud service, is stored within a tenant in Azure Active Directory (AAD). In most cases, your AAD account’s UPN will match the email address.

## Azure Active Directory

Microsoft cloud services use [Azure Active Directory](/azure/active-directory/fundamentals/active-directory-whatis) to take care of authenticating users. Azure Active Directory is the tenant that contains usernames and security groups. Typically, the email address a user signs in with is the same as the UPN of the account.

### How do I tell what my UPN is?

You may not know what your UPN is, and you may not be a domain administrator. You can use the following command from your workstation to find out the UPN for your account: `whoami /upn`.

The result will look similar to an email address, but this is the UPN that is on your local domain account.

### Synchronize an on-premises Active Directory with Azure Active Directory

You want your local Active Directory accounts to match Azure Active Directory, because the UPN has to match between the accounts.

The cloud services only know about accounts within Azure Active Directory. It doesn’t matter if you added an account in your local Active Directory, if it doesn’t exist in AAD, it cannot be used. There are different ways that you can match your local Active Directory accounts with Azure Active Directory.

* You can add accounts manually to Azure Active Directory.

    You can create an account on the Azure portal, or within the Microsoft 365 admin center, and the account name matches the UPN of the local Active Directory account.

* You can use the [Azure AD Connect](/azure/active-directory/hybrid/how-to-connect-sync-whatis) tool to synchronize local accounts to your Azure Active Directory tenant.

    The Azure AD Connect tool provides options for directory synchronization and setting up authentication, including password hash sync, pass-through authentication, and federation. If you are not a tenant admin or a local domain administrator, you will need to contact your IT admin to get this configured.

Using Azure AD Connect ensures that the UPN will match between AAD and your local Active Directory. This will help if you're using Analysis Services live connections with Power BI or single sign-on (SSO) capabilities.

> [!NOTE]
> Synchronizing accounts with the Azure AD Connect tool will create new accounts within your AAD tenant.

## Next steps

* [On-premises data gateway FAQ](service-gateway-onprem-faq.md)  
* [Azure Service Bus](/azure/service-bus-messaging/service-bus-messaging-overview/)  
* [Azure AD Connect](/azure/active-directory/hybrid/how-to-connect-sync-whatis/)  

