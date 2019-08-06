---
title: On-premises data gateway architecture
description: This article looks at the on-premises gateway in-depth. It looks at how the service works with Azure Active Directory and your on-premises Active Directory.
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

[!INCLUDE [gateway-rewrite](../includes/gateway-rewrite.md)]

Users in your organization can access on-premises data for which they already have access authorization. But, before those users can connect to your on-premises data source, an on-premises data gateway needs to be installed and configured. The gateway facilitates quick and secure behind-the-scenes communication. Data flows from a user in the cloud to your on-premises data source and then back to the cloud.

Installing and configuring a gateway is usually done by an admin. These actions might require special knowledge of your on-premises servers. In some cases they might require Server Administrator permissions.

This article doesn’t provide step-by-step guidance on how to install and configure a gateway. For that, be sure to see [Install an-premises data gateway](service-gateway-install.md). This article provides you with in-depth understanding of how the gateway works.

## How the gateway works

![Relationship among cloud services, gateway, and data sources](./media/service-gateway-onprem-indepth/on-prem-data-gateway-how-it-works.png)

Let’s first look at what happens when you interact with an element that is connected to an on-premises data source.

> [!NOTE]
> Depending on the cloud service, you might need to configure a data source for the gateway.

1. The cloud service creates a query. It also creates the encrypted credentials for the on-premises data source. The query and credentials are sent to the gateway queue for processing.
1. The gateway cloud service analyzes the query and pushes the request to [Azure Service Bus](/azure/service-bus-messaging/service-bus-messaging-overview/).
1. Azure Service Bus sends the pending requests to the gateway.
1. The gateway gets the query, decrypts the credentials, and connects to the data sources with those credentials.
1. The gateway sends the query to the data source to be run.
1. The results are sent from the data source back to the gateway. From there the results are sent to the cloud service, which uses them.

In step 6, queries like Power BI refreshes and Azure Analysis Services refreshes can return large amounts of data. For such queries, data is temporarily stored on the gateway machine. This data storage continues until all data is received from the data source. The data is then sent back to the cloud service. This process is called spooling. We recommend that you use an SSD as the spooling storage.

## Authentication to on-premises data sources

Regardless of the user, the gateway typically uses a stored credential to connect to on-premises data sources. But, there might be exceptions like DirectQuery and LiveConnect for Analysis Services in Power BI.

## Sign-in account

You sign in with either a work account or a school account. This account is your organization account. If you signed up for an Office 365 offering and didn’t supply your actual work email address, the account name might look like nancy@contoso.onmicrosoft.com. A cloud service stores your account within a tenant in Azure Active Directory (Azure AD). In most cases, the user principal name (UPN) of your Azure AD account matches your email address.

## Azure Active Directory

Microsoft cloud services use [Azure AD](/azure/active-directory/fundamentals/active-directory-whatis) to  authenticate users. Azure AD is the tenant that contains usernames and security groups. Typically, the email address that you sign in with is the same as the UPN of your account.

### How do I tell what my UPN is?

You might not know what your UPN is, and you might not be a domain admin. To find out the UPN for your account, use the following command from your workstation: `whoami /upn`.

The result will look similar to an email address, but it is the UPN on your local domain account.

### Synchronize an on-premises Active Directory with Azure Active Directory

You want each on-premises Active Directory account to match its corresponding Azure AD account, because the UPN for each pair of accounts has to be the same.

The cloud services know only about accounts within Azure AD. It doesn’t matter if you added an account in your on-premises Active Directory. If the account doesn’t exist in Azure AD, it can't be used. There are different ways to match your on-premises Active Directory accounts with Azure AD.

* Add accounts manually to Azure Active Directory.

    Create an account on the Azure portal or within the Microsoft 365 admin center. The account name then matches the UPN of the on-premises Active Directory account.

* Use the [Azure Active Directory Connect](/azure/active-directory/hybrid/how-to-connect-sync-whatis) tool to synchronize on-premises accounts to your Azure AD tenant.

    Azure AD Connect provides options for directory synchronization and setting up authentication. These options include password hash sync, pass-through authentication, and federation. If you're not a tenant admin or a local domain admin, contact your IT admin to get Azure AD Connect configured.

By using Azure AD Connect, you ensure that your Azure AD UPN will match your on-premises Active Directory UPN. This matching helps if you're using Analysis Services live connections with Power BI or single sign-on (SSO) capabilities.

> [!NOTE]
> Synchronizing accounts with Azure AD Connect creates new accounts within your Azure AD tenant.

## Next steps

* [On-premises data gateway FAQ](service-gateway-onprem-faq.md)  
* [Azure Service Bus](/azure/service-bus-messaging/service-bus-messaging-overview/)  
* [Azure AD Connect](/azure/active-directory/hybrid/how-to-connect-sync-whatis/)  
