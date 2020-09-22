---
title: Configure proxy settings for the on-premises data gateway
description: Provides information about configuration of proxy settings for the on-premises data gateway.
author: arthiriyer
manager: kfile
ms.reviewer: ''
ms.prod: on-premises-data-gateway
ms.technology:
ms.topic: conceptual
ms.date: 07/15/2019
ms.author: arthii
LocalizationGroup: Gateways

---
# Configure proxy settings for the on-premises data gateway

Your work environment might require that you go through a proxy to access the internet. This could prevent the Microsoft on-premises data gateway from connecting to the service.

The following post on superuser.com discusses how you can try to determine if you have a proxy on your network:
[How do I know what proxy server I'm using? (SuperUser.com)](https://superuser.com/questions/346372/how-do-i-know-what-proxy-server-im-using).

Although most gateway configuration settings can be changed by using the on-premises data gateway app, proxy information is configured within a .NET configuration file. The location and file names are different, depending on the gateway you're using.

Two main configuration files are involved with the gateway in which proxy settings can be edited:

* The first file is for the configuration screens that actually configure the gateway. If you're having issues configuring the gateway, look at the following file: _C:\Program Files\On-premises data gateway\enterprisegatewayconfigurator.exe.config_.
* The second file is for the actual Windows service that interacts with the cloud service using the gateway. This file handles the requests: _C:\Program Files\On-premises data gateway\Microsoft.PowerBI.EnterpriseGateway.exe.config_.

If you're going to make changes to the proxy configuration, these files must be edited so that proxy configurations are exactly the same in both files.

## Configure proxy settings

The following sample shows the default proxy configuration found in both of the two main configuration files.

```xml
<system.net>
    <defaultProxy useDefaultCredentials="true" />
</system.net>
```

The default configuration works with Windows authentication. If your proxy uses another form of authentication, you must change the settings. If you aren't sure, contact your network administrator.

We don't recommend basic proxy authentication. Using basic proxy authentication might cause proxy authentication errors that result in the gateway not being properly configured. Use a stronger proxy authentication mechanism to resolve.

In addition to using default credentials, you can add a `<proxy>` element to define proxy server settings in more detail. For example, you can specify that your on-premises data gateway should always use the proxy, even for local resources, by setting the *bypassonlocal* parameter to false. This can help in troubleshooting situations, if you want to track all HTTPS requests that originate from a gateway in the proxy log files. The following sample configuration specifies that all requests must go through a specific proxy with the IP address 192.168.1.10.

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

Additionally, for the gateway to connect to cloud data sources through a proxy, update one of the following files:
* On-premises data gateway up to and including March 2020 release&mdash;_C:\Program Files\On-premises data gateway\Microsoft.Mashup.Container.NetFX45.exe.config_.
* On-premises data gateway April 2020 and newer&mdash;_C:\Program Files\On-premises data gateway\m\Microsoft.Mashup.Container.NetFX45.exe.config_.

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

To learn more about the configuration of the proxy elements for .NET configuration files, see [defaultProxy Element (Network settings)](https://msdn.microsoft.com/library/kd3cf2ex.aspx).

## Change the gateway service account to a domain user

As explained earlier, when you configure the proxy settings to use default credentials, you might encounter authentication issues with your proxy. This situation is because the default service account is the Service SID, and not an authenticated domain user. You can change the service account of the gateway to allow proper authentication with your proxy. For more information about how to change the gateway service account, see [Change the on-premises data gateway service account](service-gateway-service-account.md).

> [!NOTE]
> We recommend that you use a managed service account to avoid having to reset passwords. Learn how to create a [managed service account](https://technet.microsoft.com/library/dd548356.aspx) within Active Directory.
>

## Next steps

* [Firewall information](service-gateway-tshoot.md#firewall-or-proxy)  