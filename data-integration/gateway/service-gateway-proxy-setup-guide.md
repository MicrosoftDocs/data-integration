---
title: Step by step guide on how to configure your proxy settings for the on-premises data gateway
description: Provides step by step instructions on how to configure the proxy settings for the on-premises data gateway.
ms.topic: conceptual
ms.date: 10/25/2022
---
# Step by step guide on how to configure your proxy settings for the on-premises data gateway

If your work environment requires Microsoft on-premises data gateway to go through a Proxy Server for connecting to the service, follow the steps below in order to configure the proxy settings.

## Configure proxy settings

1. Create your proxy definition element. To learn more about the configuration of the proxy elements for .NET configuration files, go to [defaultProxy Element (Network settings)](https://learn.microsoft.com/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings).
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

2. Browse the installation folder for the on-premises data gateway, e.g: “C:\Program Files\On-premises data gateway\”
3. Open the first file that is used for the configuration screens that configure the gateway “EnterpriseGatewayConfigurator.exe.config”
4. Locate the "defaultProxy" element and replace it with your proxy configuration created in the step 1 above and save your changes to the file.
5. Now, open the second file that is used for the actual Windows service that interacts with the cloud service using the gateway and handles the requests: “Microsoft.PowerBI.EnterpriseGateway.exe.config” and repeat step 4.
6. For the third configuration file that is used for the gateway to connect to the data sources, typically cloud data sources, open the subfolder “m” in the installation folder and then the file “Microsoft.Mashup.Container.NetFX45.exe.config”. Repeat step 4 to insert the proxy configuration into this file.
   If the file is in default state, you'll need to add the "system.net" tag together with the proxy definition, as the example below:

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

7. Open the on-premises data gateway application, navigate to “Service Settings” tab and press “Restart now” to restart the Gateway service and apply the new proxy settings.

### How to verify if my proxy configuration is consistent for my on-premises data gateway

1. Ensure you’re running September 2022 version or higher
2. Open the on-premises data gateway application
3. Navigate to “Diagnostics” tab
4. Under “Network ports test”, click into “Start new test”
5. Once the network ports test is complete, click into “Open last completed test results”
6. If your proxy configuration is consistent across the three required configuration files, you should see:
    1. “Proxy configuration : Proxy settings match for all Gateway process configurations.”
7. Otherwise, if proxy configuration isn't consistent you should find the information:
    1. “Proxy configuration : Proxy settings are not consistent. Please ensure that the proxy configuration matches across the files listed below:
    C:\Program Files\On-premises data gateway\EnterpriseGatewayConfigurator.exe.config
    C:\Program Files\On-premises data gateway\Microsoft.PowerBI.EnterpriseGateway.exe.config
    C:\Program Files\On-premises data gateway\m\Microsoft.Mashup.Container.NetFX45.exe.config
    Review <https://docs.microsoft.com/data-integration/gateway/service-gateway-proxy>  for additional information about configuring proxies for the Gateway.
    ”

### Examples of possible behaviors that may be related to inconsistent or missing proxy configuration

If the proxy definition is either missing or inconsistent, you may experience different behaviors with your on-premises data gateway, few examples are:

1. A dataset or dataflow refresh failure, error message example: “Error: Unable to connect to the remote server”
2. While launching on premises data gateway, you fail to sign-in, the sign-in prompt appears but its content can't be displayed or you do see an error message page.
3. The Network Port test results report failures connecting to the servers

[!INCLUDE[footer-include](../includes/footer-banner.md)]
