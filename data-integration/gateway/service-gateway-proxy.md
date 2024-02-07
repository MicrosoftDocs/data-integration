---
title: Configure proxy settings for the on-premises data gateway
description: Provides information about configuration of proxy settings for the on-premises data gateway.
ms.topic: conceptual
ms.date: 9/5/2023
---
# Configure proxy settings for the on-premises data gateway

Your work environment might require that you go through a proxy to access the internet. This requirement could prevent the Microsoft on-premises data gateway from connecting to the service.

The following post on superuser.com discusses how you can try to determine if you have a proxy on your network:
[How do I know what proxy server I'm using? (SuperUser.com)](https://superuser.com/questions/346372/how-do-i-know-what-proxy-server-im-using).

Although most gateway configuration settings can be changed by using the on-premises data gateway app, proxy information is configured within a .NET configuration file. The location and file names are different, depending on the gateway you're using.

There are three configuration files associated with using a proxy with the on-premises data gateway. The following two main configuration files apply to the gateway and its configuration process.

* The first file is for the configuration screens that actually configure the gateway. If you're having issues configuring the gateway, look at the following file: _C:\Program Files\On-premises data gateway\enterprisegatewayconfigurator.exe.config_. On the on-premises data gateway (personal mode), the corresponding file is _%LocalAppData%\Microsoft\On-premises data gateway (personal mode)\PersonalGatewayConfigurator.exe.config_.
* The second file is for the actual Windows service that interacts with the cloud service using the gateway. This file handles the requests: _C:\Program Files\On-premises data gateway\Microsoft.PowerBI.EnterpriseGateway.exe.config_. On the on-premises data gateway (personal mode), the corresponding file is _%LocalAppData%\Microsoft\On-premises data gateway (personal mode)\Microsoft.PowerBI.DataMovement.PersonalGateway.exe.config_.

If you're going to make changes to the proxy configuration, these files must be edited so that proxy configurations are exactly the same in both files.

The third configuration file needs to be edited for the gateway to connect to cloud data sources through a proxy.

* _C:\Program Files\On-premises data gateway\m\Microsoft.Mashup.Container.NetFX45.exe.config_

On the on-premises data gateway (personal mode), the corresponding file is _%LocalAppData%\Microsoft\On-premises data gateway (personal mode)\m\Microsoft.Mashup.Container.NetFX45.exe.config_.

The following section describes how to edit these files.

## Configure proxy settings

The following sample shows the default proxy configuration found in both of the two main configuration files.

```xml
<system.net>
    <defaultProxy useDefaultCredentials="true" />
</system.net>
```

The default configuration works with Windows authentication. If your proxy uses another form of authentication, you must change the settings. If you aren't sure, contact your network administrator.

We don't recommend basic proxy authentication. Using basic proxy authentication might cause proxy authentication errors that result in the gateway not being properly configured. Use a stronger proxy authentication mechanism to resolve.

In addition to using default credentials, you can add a `<proxy>` element to define proxy server settings in more detail. For example, you can specify that your on-premises data gateway should always use the proxy, even for local resources, by setting the *bypassonlocal* parameter to false. This setting can help in troubleshooting situations in order to track all HTTPS requests that originate from a gateway in the proxy log files. The following sample configuration specifies that all requests must go through a specific proxy with the IP address 192.168.1.10.

```xml
<system.net>
    <defaultProxy useDefaultCredentials="true">
        <proxy  
            autoDetect="false"  
            proxyaddress="http://192.168.1.10:3128"  
            bypassonlocal="false"  
            usesystemdefault="true"
        />  
    </defaultProxy>
</system.net>
```

You also need to edit the _Microsoft.Mashup.Container.NetFX45.exe.config_ file if you want the gateway to connect to cloud data sources through a gateway.

In the file, expand the `<configurations>` section to include the following contents, and update the `proxyaddress` attribute with your proxy information. The following example routes all cloud requests through a specific proxy with the IP address 192.168.1.10.

```xml
<configuration>
    <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
        <proxy proxyaddress="http://192.168.1.10:3128" bypassonlocal="true" />
        </defaultProxy>
    </system.net>
</configuration>
```

Configuring this third file might be necessary if your proxy is a requirement for all internet communication, especially for corporate usage where networks are secure and locked-down. If a proxy is required for gateway communication, it's likely also needed for any internet traffic from containers. In this case, the gateway might appear to be operating successfully until any container makes any external (internet) query. This issue is especially applicable to dataflows, which attempt to push the resulting query of on-premises data to Azure Data Lake Storage. But it also applies when a gateway query merges an on-premises semantic model with an internet-bound semantic model.

To learn more about the configuration of the proxy elements for .NET configuration files, go to [defaultProxy Element (Network settings)](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings).

### Configure gateway for output destinations

In addition, to use the gateway with output destinations, the gateway might need to be configured to be able to pass through a firewall or proxy to reach the destination data source. If you're using a proxy server, this passthrough might require enable-listing URLs to appropriate destinations, for example \*.datawarehouse.pbidedicated.windows.net for LakeHouse, \*.dfs.core.windows.net for Data Lake, and so on.

> [!NOTE]
> If you are using LakeHouse destinations, you must be running at least the May 2023 release of the gateway. The Lakehouse connector isn't available in gateway versions prior to this release.

## Change the gateway service account to a domain user

As explained earlier, when you configure the proxy settings to use default credentials, you might come across authentication issues with your proxy. This situation occurs when the default service account is the Service SID, and not an authenticated domain user.
If the proxy on your organization requires a domain account in order to authenticate the request, you can change the service account of the gateway to a domain service account. This change allows the proper authentication with your proxy.
For more information about how to change the gateway service account, go to [Change the on-premises data gateway service account](service-gateway-service-account.md).

> [!NOTE]
> We recommend that you use a managed service account to avoid having to reset passwords. Learn how to create a [managed service account](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd548356(v=ws.10)) within Active Directory.
>

## Next steps

* [Step by step guide on configuring your proxy settings](service-gateway-proxy-setup-guide.md)
* [Firewall information](service-gateway-tshoot.md#firewall-or-proxy)  
