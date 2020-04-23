---
ms.date: 06/12/2017
contributor: manikb
keywords: 库,powershell,cmdlet,psget
title: cmdlet 故障排除
ms.openlocfilehash: d87c680472c2588efbfe8b3c4d6f2dbee6883a0c
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "72352107"
---
# <a name="troubleshooting-cmdlets"></a><span data-ttu-id="387d2-103">cmdlet 故障排除</span><span class="sxs-lookup"><span data-stu-id="387d2-103">Troubleshooting cmdlets</span></span>

## <a name="how-to-resolve-warning-package-your-package-name-failed-to-download-issue"></a><span data-ttu-id="387d2-104">如何解决“警告：无法下载包‘你的包名称’”问题</span><span class="sxs-lookup"><span data-stu-id="387d2-104">How to resolve "WARNING: Package 'your package name' failed to download" issue</span></span>

<span data-ttu-id="387d2-105">收到 `Install-Module` 或 `Update-Module` 有时在某些计算机上失败的报告。</span><span class="sxs-lookup"><span data-stu-id="387d2-105">It is reported that `Install-Module` or `Update-Module` sometimes fails on some machines.</span></span> <span data-ttu-id="387d2-106">根据我们的调查，此问题与网络连接有关。</span><span class="sxs-lookup"><span data-stu-id="387d2-106">Based on our investigation, it is something to do with the networking connection.</span></span> <span data-ttu-id="387d2-107">最近，我们更新了 NuGet 提供程序，使其可以可靠地下载包。</span><span class="sxs-lookup"><span data-stu-id="387d2-107">Recently we updated NuGet provider so that it can reliably download packages.</span></span> <span data-ttu-id="387d2-108">你可以按照以下说明安装 NuGet 提供程序的最新版本，然后安装或更新你的模块。</span><span class="sxs-lookup"><span data-stu-id="387d2-108">You can follow the instructions below to install the latest build of NuGet provider and then install or update your module.</span></span> <span data-ttu-id="387d2-109">下面，我们使用“Azure”模块作为示例。</span><span class="sxs-lookup"><span data-stu-id="387d2-109">Let's use 'Azure' module as an example below.</span></span>

```powershell
Install-PackageProvider NuGet -MinimumVersion 2.8.5.206 -Force
Launch new PowerShell Console
Update-Module Azure -Verbose
```

### <a name="required-network-endpoints"></a><span data-ttu-id="387d2-110">所需的网络终结点</span><span class="sxs-lookup"><span data-stu-id="387d2-110">Required network endpoints</span></span>

<span data-ttu-id="387d2-111">安装和更新 cmdlet 需要通过 Internet 访问连接 PowerShell 库使用的网络终结点。</span><span class="sxs-lookup"><span data-stu-id="387d2-111">The Install and Update cmdlets require internet access to connect to the network endpoints used by by the PowerShell Gallery.</span></span> <span data-ttu-id="387d2-112">请确保网络访问策略允许连接以下终结点。</span><span class="sxs-lookup"><span data-stu-id="387d2-112">Ensure that your network access policies allow you to connect to the following endpoints.</span></span>

- <span data-ttu-id="387d2-113">oneget.org</span><span class="sxs-lookup"><span data-stu-id="387d2-113">oneget.org</span></span>
- <span data-ttu-id="387d2-114">go.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="387d2-114">go.microsoft.com</span></span>
- <span data-ttu-id="387d2-115">az818661.vo.msecnd.net</span><span class="sxs-lookup"><span data-stu-id="387d2-115">az818661.vo.msecnd.net</span></span>
- <span data-ttu-id="387d2-116">www.powershellgallery.com</span><span class="sxs-lookup"><span data-stu-id="387d2-116">www.powershellgallery.com</span></span>
- <span data-ttu-id="387d2-117">devopsgallerystorage.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="387d2-117">devopsgallerystorage.blob.core.windows.net</span></span>
