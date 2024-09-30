---
title: Configure gateway disk space
description: Describes how to troubleshoot out of disk space errors caused by gateway spooling and persistent cache filling up all disk space.
ms.reviewer: mideboer
ms.topic: conceptual
ms.date: 05/06/2024
---

# Configure gateway disk space

This article focuses on the configuration settings governing disk space for gateway users who run out of disk space.

## Gateway spooling data

Power BI and the on-premises data gateway create temporary cache files when communicating between the on-premises environment and the cloud in a process called *spooling*. Depending on how much disk space you have available for spooling, it's possible for an "out of disk space" error to occur when disk space is full because of the spooler.

>[!NOTE]
> We recommend you use a solid-state drive (SSD) as the spooling storage drive for optimal performance.

When spooling causes an "out of disk space" error, use the following steps to change the location of the spooler to a disk with more capacity.

1. Navigate to C:\Program Files\On-premises data gateway\.
2. Make a backup copy of the Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config configuration file.
3. Edit the Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config configuration file.
4. Search for **SpoolerDirectory**.

   ```xml
   <setting name="SpoolerDirectory" serializeAs="String">
       <value>%LOCALAPPDATA%\Microsoft\On-premises data gateway\Spooler</value>
   </setting>
   ```

   The \<value> tag specifies the location of the SpoolerDirectory.

5. Modify this path to a location that contains enough disk space for your business needs.  
6. Once modified, save the file and restart the on-premises data gateway.

> [!NOTE]
> If you modify the path, you'll also need to restart the on-premises data gateway service.

:::image type="content" source="media/service-gateway-configure-disk-space/restart-service.png" alt-text="Screenshot of the Windows Services dialog with the on-premises data gateway service emphasized." lightbox="media/service-gateway-configure-disk-space/restart-service.png":::

## Mashup engine persistent cache

If spooling has been mapped to a different drive, but you continue to get "out of disk space" errors, it could be due to the persistent cache. This error could be due to queries that don't fold (for more information about query folding, go to [Query folding overview](/power-query/query-folding-basics#query-folding-overview)). Or the error could be due to poorly performing queries (for more information on optimizing gateway performance, go to [Monitor and optimize on-premises data gateway performance](service-gateway-performance.md)).

If the query can't be optimized, the persistent cache can be moved to a larger capacity drive. The persistent cache (as opposed to the spooler) uses the root drive, and the operating system \temp path. In order to avoid the "out of disk space" error, you'll need to either free up space on the root drive, expand the size of the root drive, or potentially remap the temp folder to a drive with more space.

You can change (or set) the value of the Windows TMP environment variable *for the user account being used to run the gateway* to move the persistent cache to a larger capacity drive. The path used for cache and temp directories is determined through the Win32 [GetTempPath](/windows/win32/api/fileapi/nf-fileapi-gettemppatha) function. According to the Win32 documentation, this function uses the first value it finds from the following list:

* The path specified by the TMP environment variable.
* The path specified by the TEMP environment variable.
* The path specified by the USERPROFILE environment variable.
* The Windows directory.

So, change TMP for the gateway user to move the persistent cache onto another drive.

>[!NOTE]
>To change the environment variables in Windows, from the **Start** menu, select **Search**, enter **Environment Variables**, select **Edit the system environment variables**, and from **System Properties** select **Environment Variables**.
