---
title: Troubleshoot the on-premises data gateway
description: This article provides ways for you to troubleshoot issues you may be having with the on-premises data gateway. It provides potential workarounds to known issues, as well as tools to assist you.
author: mgblythe
ms.author: mblythe
manager: kfile
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-gateways
ms.topic: conceptual
ms.date: 07/15/2019
LocalizationGroup: Gateways 
---

# Troubleshoot the on-premises data gateway

This article discusses some common issues when using the on-premises data gateway.

>[!NOTE]
>If you encounter an issue that is not listed below, you can create a support ticket for the particular cloud service that's running the gateway.

## Update to the latest version

Issues can occur when the gateway version is out of date. It's a good general practice to make sure you're using the latest version. If you haven't updated the gateway for a month, or longer, you might want to consider [installing the latest version of the gateway](service-gateway-update.md). Then see if you can reproduce the issue.

### Inconsistent versions between gateway members in a cluster

Keep the versions of the gateway members in a cluster in sync. Having all the same version in a cluster will help avoid unexpected refresh failures. These refresh failures might occur because the gateway member that a specific query is routed to may not be capable of executing it due to a lower version.

## Troubleshoot common installation issues

Here are a few common installation issues and the resolutions that have helped a number of customers.

### Error: Failed to add user to group.  (-2147463168   PBIEgwService   Performance Log Users   )

You might receive this error if you're trying to install the gateway on a domain controller. Deploying on a domain controller isn't supported. You'll need to deploy the gateway on a machine that isn't a domain controller.

### Out of date anti-virus

You might encounter installation failures if the anti-virus software on the installation machine is out of date. You can either update the anti-virus installation, or disable the anti-virus only for the duration of the gateway installation. Once the installation is complete, then re-enable the anti-virus.

### Same or older gateway version

You might come across the following error if you try to install the same version or a previous version of the gateway compared to the one that you already have.

![Gateway installation error](media/service-gateway-tshoot/gateway-install-error.png)

## Troubleshoot configuration

### Firewall or proxy

To test if the gateway has access to all the required ports, run the [network ports test](service-gateway-communication.md#network-ports-test). The results of the test are either Completed (Succeeded) or Completed (Failed, see last test results). If the test succeeded, then your gateway successfully connected to all the required ports. If the test failed, then your network environment might be blocking these required ports and servers.

For information on providing proxy information for your gateway, see [Configure proxy settings for the on-premises data gateway](service-gateway-proxy.md).

A firewall might also be blocking the connections that the Azure Service Bus makes to the Azure data centers. If that's the case, you'll want to whitelist (unblock) the IP addresses for your region for those data centers. You can get a list of Azure IP addresses [here](https://www.microsoft.com/en-us/download/details.aspx?id=56519). To find the current data center region you're in, see [Set the data center region](service-gateway-data-region.md).

### Authentication to proxy server

Your proxy may require authentication from a domain user account. By default, the gateway uses a Service SID for the windows service sign in user. Changing the sign in user to a domain user can help with this. For more information, see [Change the gateway service account to a domain user](service-gateway-proxy.md#change-the-gateway-service-account-to-a-domain-user).

### Your proxy only allows ports 80 and 443 traffic

Some proxies restrict traffic to only ports 80 and 443. By default, communication to Azure Service Bus occurs on ports other than 443.

You can force the gateway to [communicate with Azure Service Bus using HTTPS](service-gateway-communication.md#force-https-communication-with-azure-service-bus) instead of direct TCP.

### Common errors

#### Error: Failed to create a gateway. Try again

This error could be due to proxy configuration issues. The gateway log provides additional details for troubleshooting. For more information, see [Configure proxy settings for the on-premises data gateway](service-gateway-proxy.md).

#### Error: Power BI service reported local gateway as unreachable. Restart the gateway and try again

At the end of configuration, the Power BI service is called again to validate the gateway. The Power BI service doesn't report the gateway as *live*. Restarting the windows service may allow the communication to be successful. You can collect and review the logs, as described in the following section, to get more details.

## Troubleshooting tools

### Collect logs from the on-premises data gateway app

There are several logs you can collect for the gateway, and you should always start with the logs. The simplest way to collect logs after installing the gateway is through the [on-premises data gateway app](service-gateway-app.md). In the on-premises data gateway app, select **Diagnostics** and then select the **Export logs** link, as shown in the following image.

![On-premises data gateway app logs](media/service-gateway-tshoot/gateway-onprem-UI-logs.png)

This file is saved to the ODGLogs folder on your Windows desktop in .zip format.

### Event Logs

The **on-premises data gateway service** event logs are present under **Application and Services Logs**.

![On-premises data gateway event logs](media/service-gateway-tshoot/on-prem-data-gateway-event-logs.png)

## Next steps

* [On-premises data gateway FAQ](service-gateway-onprem-faq.md)
