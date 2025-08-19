---
title: Troubleshoot the on-premises data gateway
description: This article provides ways for you to troubleshoot issues you might have with the on-premises data gateway. It provides potential workarounds to known issues and tools to assist you.
ms.topic: troubleshooting
ms.date: 6/11/2025
ms.custom: sfi-image-nochange
---

# Troubleshoot the on-premises data gateway

This article discusses some common issues when you use the on-premises data gateway.

> [!NOTE]
>If you encounter an issue that isn't listed here, create a support ticket for the particular cloud service that's running the gateway.

## Update to the latest version

It's a good general practice to make sure you're using a supported version. We release a new update of the on-premises data gateway every month. Currently, Microsoft actively supports only the last six releases of the on-premises data gateway. If you're experiencing issues with the version you're using, try upgrading to the latest one as your issue might be resolved in the latest version.

### Inconsistent versions between gateway members in a cluster

Keep the versions of the gateway members in a cluster in sync. Having all the same version in a cluster helps to avoid unexpected refresh failures. These refresh failures might occur because the gateway member that a specific query is routed to might not be capable of executing it due to a lower version.

## Troubleshoot Gateway management

Here are a few common management issues and the resolutions that helped other customers.

### Error while removing the primary node of a gateway cluster

The primary node of a gateway can't be removed if there are other members in the cluster. Removing the primary node also means removing the gateway cluster.

## Troubleshoot common installation issues

Here are a few common installation issues and the resolutions that helped other customers.

### Error: Failed to add user to group. (-2147463168 PBIEgwService Performance Log Users)

You might receive this error if you're trying to install the gateway on a domain controller. Deploying on a domain controller isn't supported. You need to deploy the gateway on a machine that isn't a domain controller.

### Out-of-date antivirus software

You might encounter installation failures if the antivirus software on the installation machine is out of date. You can either update the antivirus installation or disable the antivirus software only during the gateway installation. After the installation is finished, reenable the antivirus software.

### McAfee Endpoint Defender software enabled

You might encounter installation failure when antivirus software, like McAfee Endpoint Defender, is enabled. Configure your antivirus software to ignore the gateway process.

### Same or older gateway version

You might come across the following error if you try to install the same version or a previous version of the gateway compared to the one that you already have.

:::image type="content" source="media/service-gateway-tshoot/gateway-install-error.png" alt-text="Screenshot of a gateway installation error.":::

### Error: The user profile is a temporary profile

There's an issue with the machine. Contact your internal IT team to remove the temporary profile.

### Error generating an asymmetric key

An antivirus such as McCafee can cause the corruption or deletion of files needed for the gateway to be able to complete the setup. Disable your antivirus temporarily or configure it to ignore the gateway process. Then delete the RSA folder from the path c:\Users\<GW Service Account User>\AppData\Roaming\Microsoft\Crypto\RSA. In some cases, depending on whether you're signing in as a user or service profile, the root path might be different. Finally, restart the machine and complete the gateway setup and sign-in.

## Troubleshoot configuration

### Firewall or proxy

To test if the gateway has access to all the required ports, run the [network ports test](service-gateway-communication.md#network-ports-test). The results of the test are either Completed (Succeeded) or Completed (Failed, see last test results). If the test succeeded, your gateway successfully connected to all the required ports. If the test failed, your network environment might be blocking these required ports and servers.

For information on how to provide proxy information for your gateway, go to [Configure proxy settings for the on-premises data gateway](service-gateway-proxy.md).

A firewall also might be blocking the connections that the Azure Relay makes to the Azure data centers. If that's the case, unblock the IP addresses for your region for those data centers. You can get a list of Azure IP addresses from [this website](https://www.microsoft.com/en-us/download/details.aspx?id=56519). To find the current data center region you're in, go to [Set the data center region](service-gateway-data-region.md).

### Authentication to proxy server

Your proxy might require authentication from a domain user account. By default, the gateway uses a Service SID for the Windows service sign-in user. Changing the sign-in user to a domain user can help with this situation. For more information, go to [Change the gateway service account to a domain user](service-gateway-proxy.md#change-the-gateway-service-account-to-a-domain-user).

### Your proxy only allows ports 80 and 443 traffic

Some proxies restrict traffic to only ports 80 and 443. By default, communication to Azure Relay occurs on ports other than 443.

You can force the gateway to [communicate with Azure Relay by using HTTPS](service-gateway-communication.md#force-https-communication-with-azure-relay) instead of direct TCP.

### Gateway proxy unable to connect to managed data lake

If you're using a proxy to access on-premises data using an on-premises data gateway, you might not be able to connect to a managed data lake (MDL) using the default proxy settings. To connect to MDL, be sure to add addresses `*.dfs.core.windows.net` and `*.blob.core.windows.net` to the allowlist on your proxy server.

### System performance counter data is unavailable

If the current service account being used by the on-premises data gateway application isn't a member of the local security group **Performance Log Users**,  you might observe in the [System Counter Aggregation Report](service-gateway-performance.md) that only system memory usage value is available.

To address this behavior, add the on-premises data gateway service account to the local security group [Performance Log Users](/windows-server/identity/ad-ds/manage/understand-security-groups#performance-log-users), and restart the on-premises data gateway service.

### Bring your own Azure Relay

Gateways experiencing connectivity issues while using Bring Your Own Relay should ensure that Private Link isn't enabled on the Relay, as this configuration isn't supported.

### Connectivity errors

When a gateway is facing connectivity issues, you might observe different symptoms. Here are a few of the common symptoms.

#### Error: Gateway shows offline status in Manage Gateways page

You might come across one of the following indications in the manage gateways page if there's a connectivity issue.

:::image type="content" source="media/service-gateway-tshoot/manage-gateway-offline.png" alt-text="Gateway offline in manage gateways page." lightbox="media/service-gateway-tshoot/manage-gateway-offline.png":::

#### Error: Your data gateway is offline or couldn't be reached

You might come across one of the following data refresh errors if there's a connectivity issue.

:::image type="content" source="media/service-gateway-tshoot/gateway-offline.png" alt-text="Gateway offline or couldn't be reached error." lightbox="media/service-gateway-tshoot/gateway-offline.png":::

#### Error: Network request returned unexpected error

You might come across one of the following errors when trying to sign in to the gateway configurator if there's a connectivity issue.

:::image type="content" source="media/service-gateway-tshoot/network-unexpected-error.png" alt-text="Gateway configurator network unexpected error." lightbox="media/service-gateway-tshoot/network-unexpected-error.png":::

Connectivity issues can have several different causes. Therefore, if you run into any of the previously mentioned symptoms, perform the following verifications:

1. Are the FQDNs and ports mentioned in our [documentation](/data-integration/gateway/service-gateway-communication#ports) opened/allowed in your firewall and/or proxy?
1. If you're using a proxy server in your environment:

   1. Make sure the proxy server is properly [configured in the gateway config files](/data-integration/gateway/service-gateway-proxy).
   1. Verify if the [proxy configuration is consistent](/data-integration/gateway/service-gateway-proxy-setup-guide#verify-consistent-proxy-configuration).
   1. Check your proxy logs to check if there are any requests being blocked at the proxy level.
1. Is your Firewall just allowing the communication on ports 80 and 443?
   1. If yes, ensure the [HTTPS mode in gateway](/data-integration/gateway/service-gateway-communication#force-https-communication-with-azure-relay) is enabled.

### Fabric Pipeline Task Memory Requirements on On-Premises Data Gateway

When running a pipeline on an on-premises data gateway, each activity is broken down into one or more tasks. The gateway machine must have sufficient memory to execute these tasks; otherwise, they will be queued.

1. **System management**: 5% of the machine’s memory is reserved for system processes.

1. **Task execution**: Each process running a task is allocated a fixed amount of memory. By default, this is 1,000 MB, but it can be modified the value of **OnPremRuntimeDefaultWorkerMaxWorkingSetInMB** in the configuration file **Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config**, with a minimum setting of 100 MB.

### Common errors

#### Error: Failed to create a gateway. Try again.

This error could be due to proxy configuration issues. The gateway log provides more details for troubleshooting. For more information, go to [Configure proxy settings for the on-premises data gateway](service-gateway-proxy.md).

#### Error: Power BI service reported local gateway as unreachable. Restart the gateway and try again.

At the end of configuration, the Power BI service is called again to validate the gateway. The Power BI service doesn't report the gateway as *live*. Restarting the Windows service might allow the communication to be successful. To get more details, collect and review the logs, as described in the following section.

#### Error: Information is needed in order to combine data

You might experience a refresh failure in Power BI service with an error "Information is needed in order to combine data," even though refresh on Power BI Desktop works. This problem occurs when the refresh in Power BI Desktop works with the **File** > **Options and settings** > **Options** > **Privacy** > **Always ignore privacy level settings** option set, but throws a firewall error when other options are selected. If you attempt to preform this refresh in Power BI service, the refresh doesn't work because **Always ignore privacy level settings** isn't available in Power BI service. To resolve this error, try changing the privacy level in the Power BI desktop **Options** > **Global** > **Privacy** and **Options** > **Current File** > **Privacy** settings so that it doesn't ignore the privacy of data. Republish the file to Power BI service and update the credentials to "Organizational" in Power BI service.

#### Error: There are too many refreshes occurring concurrently

The gateway has a concurrency limit of 30. If you're getting this error, it means you reached the concurrency limit. You can monitor the concurrency count with the [gateway diagnostics template](service-gateway-performance.md). To avoid running into this issue, upgrade the number of gateways in a cluster or start a new cluster to load balance the request.

## Troubleshooting tools

### Collect logs from the on-premises data gateway app

There are several logs you can collect for the gateway, and you should always start with the logs. The simplest way to collect logs after you install the gateway is through the [on-premises data gateway app](service-gateway-app.md). In the on-premises data gateway app, select **Diagnostics** and then select the **Export logs** link.

:::image type="content" source="media/service-gateway-tshoot/gateway-onprem-UI-logs.png" alt-text="On-premises data gateway app logs.":::

This file is saved to the ODGLogs folder on your Windows desktop in .zip format.

### Event logs

To find the event logs for the *on-premises data gateway service*, follow these steps:

1. On the computer with the gateway installation, open the **Event Viewer**.

1. Expand **Event Viewer** > **Applications and Services Logs**.

1. Select **On-premises data gateway service**.

:::image type="content" source="media/service-gateway-tshoot/on-prem-data-gateway-event-logs.png" alt-text="On-premises data gateway event logs.":::

## Troubleshoot refresh failures for a specific source

Refreshes utilizing the gateway require that the source is accessible from the computer with the gateway installation.
To troubleshoot a data source issue, use Power BI Desktop locally on the gateway computer to test the connection.
This test is especially helpful if the data source requires other components to be installed on the computer, such as a third-party database driver. Also, a local test helps to test data source connections that require extra environment settings, such as access to a shared network drive file or folder.
This technique allows you to test iteratively, testing the connection on the gateway computer after each configuration change.

Although it isn't a guarantee of a successful refresh through the gateway, a successful Power BI Desktop refresh from the gateway computer is a strong indicator that everything is configured correctly on the gateway computer.
In other words, if you can't refresh in Power BI Desktop from the gateway computer, it's highly unlikely that a refresh through the gateway succeeds.
After a successful refresh in Desktop, you can narrow your troubleshooting steps to the configuration of the datasource and the semantic model in the Power BI service.

## Limitations and considerations

When you use OAuth2 credentials, the gateway currently doesn't support refreshing tokens automatically when access tokens expire (one hour after the refresh started). If you get the errors "InvalidConnectionCredentials" or "AccessUnauthorized" when accessing cloud data sources using OAuth2 credentials even though the credentials were updated recently, you might be hitting this error. This limitation for long running refreshes exists for both VNet gateways and on-premises data gateways.

The Power BI [gateways REST APIs](/rest/api/power-bi/gateways) don't support [gateway clusters](service-gateway-high-availability-clusters.md).

## Related content

* [On-premises data gateway FAQ](service-gateway-onprem-faq.yml)
