---
ms.date: 06/12/2017
keywords: dsc,powershell,配置,安装程序
title: 从拉取服务器更新节点
ms.openlocfilehash: fa59a2f6574db2dbc96621be4326f1d5a55e5de9
ms.sourcegitcommit: 30ccbbb32915b551c4cd4c91ef1df96b5b7514c4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2020
ms.locfileid: "80500660"
---
# <a name="update-nodes-from-a-pull-server"></a><span data-ttu-id="1cd0b-103">从拉取服务器更新节点</span><span class="sxs-lookup"><span data-stu-id="1cd0b-103">Update Nodes from a Pull Server</span></span>

<span data-ttu-id="1cd0b-104">以下部分假定你已设置拉取服务器。</span><span class="sxs-lookup"><span data-stu-id="1cd0b-104">The sections below assume that you have already set up a Pull Server.</span></span> <span data-ttu-id="1cd0b-105">如果尚未设置拉取服务器，则可以使用以下指南：</span><span class="sxs-lookup"><span data-stu-id="1cd0b-105">If you have not set up your Pull Server, you can use the following guides:</span></span>

- [<span data-ttu-id="1cd0b-106">设置 DSC SMB 拉取服务器</span><span class="sxs-lookup"><span data-stu-id="1cd0b-106">Set up a DSC SMB Pull Server</span></span>](pullServerSmb.md)
- [<span data-ttu-id="1cd0b-107">设置 DSC HTTP 拉取服务器</span><span class="sxs-lookup"><span data-stu-id="1cd0b-107">Set up a DSC HTTP Pull Server</span></span>](pullServer.md)

<span data-ttu-id="1cd0b-108">每个目标节点都可以配置为下载配置、资源，甚至是报告其状态。</span><span class="sxs-lookup"><span data-stu-id="1cd0b-108">Each target node can be configured to download configurations, resources, and even report its status.</span></span> <span data-ttu-id="1cd0b-109">本文将演示如何上传资源以便下载，以及如何将客户端配置为自动下载资源。</span><span class="sxs-lookup"><span data-stu-id="1cd0b-109">This article will show you how to upload resources so they are available to be downloaded, and configure clients to download resources automatically.</span></span> <span data-ttu-id="1cd0b-110">当节点通过“拉取”  或“推送”  (v5) 接收已分配的配置时，将从 LCM 中指定的位置自动下载配置所需的任何资源。</span><span class="sxs-lookup"><span data-stu-id="1cd0b-110">When the Node's receives an assigned Configuration, through **Pull** or **Push** (v5), it automatically downloads any resources required by the Configuration from the location specified in the LCM.</span></span>

## <a name="using-the-update-dscconfiguration-cmdlet"></a><span data-ttu-id="1cd0b-111">使用 Update-DSCConfiguration cmdlet</span><span class="sxs-lookup"><span data-stu-id="1cd0b-111">Using the Update-DSCConfiguration cmdlet</span></span>

<span data-ttu-id="1cd0b-112">从 PowerShell 5.0 开始，[Update-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/update-dscconfiguration) cmdlet 强制节点从 LCM 中配置的拉服务器更新其配置。</span><span class="sxs-lookup"><span data-stu-id="1cd0b-112">Beginning in PowerShell 5.0, the [Update-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/update-dscconfiguration) cmdlet, forces a Node to update its configuration from the Pull Server configured in the LCM.</span></span>

```powershell
Update-DSCConfiguration -ComputerName "Server01"
```

## <a name="using-invoke-cimmethod"></a><span data-ttu-id="1cd0b-113">使用 Invoke-CIMMethod</span><span class="sxs-lookup"><span data-stu-id="1cd0b-113">Using Invoke-CIMMethod</span></span>

<span data-ttu-id="1cd0b-114">在 PowerShell 4.0 中，仍可以手动强制拉取客户端以使用 [Invoke-CIMMethod](/powershell/module/cimcmdlets/invoke-cimmethod) 更新其配置。</span><span class="sxs-lookup"><span data-stu-id="1cd0b-114">In PowerShell 4.0, you can still manually force a Pull Client to update its Configuration using [Invoke-CIMMethod](/powershell/module/cimcmdlets/invoke-cimmethod).</span></span> <span data-ttu-id="1cd0b-115">以下示例使用指定的凭据创建 CIM 会话、调用相应的 CIM 方法以及删除该会话。</span><span class="sxs-lookup"><span data-stu-id="1cd0b-115">The following example creates a CIM session with specified credentials, invokes the appropriate CIM method, and removes the session.</span></span>

```powershell
$cimSession = New-CimSession -ComputerName "Server01" -Credential $(Get-Credential)
Invoke-CimMethod -CimSession $cimSession -Namespace 'root/microsoft/windows/desiredstateconfiguration' -Class 'MSFT_DscLocalConfigurationManager' -MethodName 'PerformRequiredConfigurationChecks' -Arguments @{ 'Flags' = [uint32]1 } -Verbose
$cimSession | Remove-CimSession
```

## <a name="see-also"></a><span data-ttu-id="1cd0b-116">另请参阅</span><span class="sxs-lookup"><span data-stu-id="1cd0b-116">See Also</span></span>

[<span data-ttu-id="1cd0b-117">PerformRequiredConfigurationChecks</span><span class="sxs-lookup"><span data-stu-id="1cd0b-117">PerformRequiredConfigurationChecks</span></span>](../reference/mof-classes/msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks.md)
