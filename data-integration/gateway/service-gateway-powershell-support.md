---
title: PowerShell support for on-premises data gateway clusters
description: You can retrieve gateway and cluster information, modify the status within a gateway, or delete a gateway by using PowerShell commands.
ms.reviewer: dougklo
ms.topic: conceptual
ms.date: 1/17/2024
---

# PowerShell support for on-premises data gateway clusters

PowerShell scripts are available in the [PowerShell gallery](https://www.powershellgallery.com/packages/OnPremisesDataGatewayHAMgmt/3000.15.18/). The scripts described in this article are for PowerShell version 5. When you use PowerShell version 7, refer to [PowerShell Cmdlets for on-premises data gateway management](/powershell/gateway/overview). You can use the PowerShell scripts to perform the following operations:

- Retrieve the list of gateway clusters available for a user.
- Retrieve the list of gateway instances registered in a cluster and their online or offline status.
- Modify the enable or disable status for a gateway instance within a cluster and other gateway properties.
- Delete a gateway.

## Run the PowerShell commands

To install these cmdlets, run the following command in an elevated PowerShell session:

```powershell
Install-Module -Name OnPremisesDataGatewayHAMgmt
```

The entire list of cmdlets can be found using the following command:

```powershell
Get-Command -Module OnPremisesDataGateway*
```

Examples and descriptions are included in the cmdlets and you can access them using the following command:

```powershell
get-help <cmdlet-name>
```

Now you can use the commands in the following table to manage your gateway clusters.

| **Command** | **Description** | **Parameters** |
| --- | --- | --- |
| *Login-OnPremisesDataGateway* |Use this command to sign in to manage your on-premises data gateway clusters. You must run this command and sign in *before* other high-availability commands can work properly. Note: The Microsoft Entra ID auth token acquired as part of a `login` call is valid for only 1 hour, after which it expires. You can rerun the `login` command to acquire a new token.| Microsoft Entra ID username and password (provided as part of the command execution, not initial invocation).|
| *Get-OnPremisesDataGatewayClusters* | Retrieves the list of gateway clusters for the signed-in user. | Optionally, you can pass formatting parameters to this command for better readability, such as *Format-Table -AutoSize -Wrap*. |
| *Get-OnPremisesDataClusterGateways* | Retrieves the list of gateways within the specified cluster and additional information for each gateway like online or offline status and machine name. | *-ClusterObjectID xyz* (where *xyz* is replaced with an actual cluster object ID value, which can be retrieved by using the *Get-OnPremisesDataGatewayClusters* command).|
| *Set-OnPremisesDataGateway* | Use this command to set property values for a given gateway within a cluster, which includes the ability to enable or disable a specific gateway instance.  | *-ClusterObjectID xyz* (where *xyz* is replaced with an actual cluster object ID value, which can be retrieved by using the *Get-OnPremisesDataGatewayClusters* command). *-GatewayObjectID abc* (where *abc* is replaced with an actual gateway object ID value, which can be retrieved by using the *Get-OnPremisesDataClusterGateways* command, given a cluster object ID). |
| *Get-OnPremisesDataGatewayStatus* | Use this command to retrieve the status for a given gateway instance within a cluster.  | *-ClusterObjectID xyz* (where *xyz* is replaced with an actual cluster object ID value, which can be retrieved by using the *Get-OnPremisesDataGatewayClusters* command).  *-GatewayObjectID abc*  (where *abc* is replaced with an actual gateway object ID value, which can be retrieved by using the *Get-OnPremisesDataClusterGateways* command, given a cluster object ID). |
| *Remove-OnPremisesDataGateway*  | Use this command to remove a gateway instance from a cluster. Note: The primary gateway in the cluster can't be removed until all other gateways in the cluster are removed.| *-ClusterObjectID xyz* (where *xyz* is replaced with an actual cluster object ID value, which can be retrieved by using the *Get-OnPremisesDataGatewayClusters* command).  *-GatewayObjectID abc* (where *abc* is replaced with an actual gateway object ID value, which can be retrieved by using the *Get-OnPremisesDataClusterGateways* command, given a cluster object ID). |

## Next steps

- [On-premises data gateway app](service-gateway-app.md)
- [Manage high-availability clusters and load balancing](service-gateway-high-availability-clusters.md)
- [Remove or delete an on-premises data gateway](service-gateway-manage.md)
