---
title: Step by step guide on configuring your proxy settings
description: Provides step by step instructions on how to configure the proxy settings for the on-premises data gateway.
ms.topic: conceptual
ms.date: 11/17/2022
---
# Step by step guide on configuring your proxy settings

If your work environment requires Microsoft on-premises data gateway to go through a Proxy Server for connecting to the service, follow the steps below in order to configure the proxy settings.

## Configure proxy settings

1. Create your proxy definition element. To learn more about the configuration of the proxy elements for .NET configuration files, go to [defaultProxy Element (Network settings)](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings).

   The following example routes all requests through a specific proxy with the IP address 192.168.0.1 on port 8888:

    ```xml
    <defaultProxy useDefaultCredentials="true">
        <proxy  
            autoDetect="false"  
            proxyaddress="http://192.168.0.1:8888"
            bypassonlocal="false"
            usesystemdefault="false"
        />
    </defaultProxy>
    ```

2. Browse the installation folder for the on-premises data gateway, for example, *C:\Program Files\On-premises data gateway\*.
3. Open the first file that's used for the configuration screens that configure the gateway, that is, *EnterpriseGatewayConfigurator.exe.config*.
4. Locate the `defaultProxy` element and replace it with your proxy configuration created in the step 1 above, and then save your changes to the file.
5. Open the second file that's used for the actual Windows service that interacts with the cloud service using the gateway and handles the requests, that is, *Microsoft.PowerBI.EnterpriseGateway.exe.config* and repeat step 4.
6. For the third configuration file that's used for the gateway to connect to the data sources&mdash;typically cloud data sources&mdash;open the subfolder *m* in the installation folder and then the file *Microsoft.Mashup.Container.NetFX45.exe.config*. Repeat step 4 to insert the proxy configuration into this file.

   If the file is in the default state, you'll need to add the `system.net` tag, together with the proxy definition, as in the following example:

    ```xml
    <system.net>
        <defaultProxy useDefaultCredentials="true">
            <proxy  
                autoDetect="false"  
                proxyaddress="http://192.168.0.1:8888"
                bypassonlocal="false"
                usesystemdefault="false"
            />
        </defaultProxy>
    </system.net>
    ```

7. Open the on-premises data gateway application, navigate to **Service Settings** tab and select **Restart now** to restart the Gateway service and apply the new proxy settings.

## Verify consistent proxy configuration

1. Ensure you’re running September 2022 version or higher.
2. Open the on-premises data gateway application.
3. Navigate to **Diagnostics** tab.
4. Under **Network ports test**, select **Start new test**.
5. Once the network ports test is complete, select **Open last completed test results**.
6. If your proxy configuration is consistent across the three required configuration files, a `Proxy configuration : Proxy settings match for all Gateway process configurations.` message is displayed.
7. Otherwise, if the proxy configuration isn't consistent, the following information is displayed:

   ```
   Proxy configuration : Proxy settings are not consistent. Please ensure that the proxy configuration matches across the files listed below:
   C:\Program Files\On-premises data gateway\EnterpriseGatewayConfigurator.exe.config
   C:\Program Files\On-premises data gateway\Microsoft.PowerBI.EnterpriseGateway.exe.config
   C:\Program Files\On-premises data gateway\m\Microsoft.Mashup.Container.NetFX45.exe.config
   Review <https://docs.microsoft.com/data-integration/gateway/service-gateway-proxy>  for additional information about configuring proxies for the Gateway.
   ```

## Inconsistent or missing proxy configuration behaviors

If the proxy definition is either missing or inconsistent, you can experience different behaviors with your on-premises data gateway. A few examples are:

* A dataset or dataflow refresh failure, error message example: `Error: Unable to connect to the remote server`.
* While launching on premises data gateway, you fail to sign in, the sign-in prompt appears but its content can't be displayed, or an error message page is displayed.
* The Network Port test results report failures connecting to the servers.

## Next steps

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE5cv1m]

* [Firewall information](service-gateway-tshoot.md#firewall-or-proxy)
