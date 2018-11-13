---
ms.date: 06/12/2017
contributor: JKeithB
keywords: 库,powershell,cmdlet,psgallery
title: 删除包
ms.openlocfilehash: ca5e68fcad52e4c7561d2c2b3858228652f22e0b
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2018
ms.locfileid: "50003686"
---
# <a name="deleting-packages"></a><span data-ttu-id="08385-103">删除包</span><span class="sxs-lookup"><span data-stu-id="08385-103">Deleting Packages</span></span>

<span data-ttu-id="08385-104">PowerShell 库不支持永久删除包，因为这会对依赖其仍可用的用户造成中断。</span><span class="sxs-lookup"><span data-stu-id="08385-104">The PowerShell Gallery does not support permanent deletion of packages, because that would break anyone who is depending on it remaining available.</span></span>

<span data-ttu-id="08385-105">但是，PowerShell 库支持“取消列出”包的方式，可以在网站包管理页面完成此操作。</span><span class="sxs-lookup"><span data-stu-id="08385-105">Instead, the PowerShell Gallery supports a way to 'unlist' a package, which can be done in the package management page on the web site.</span></span>
<span data-ttu-id="08385-106">如果取消列出某个包，它将不会在搜索和任何包列表中显示（无论是在 PowerShell 库上，还是使用 PowerShellGet 命令）。</span><span class="sxs-lookup"><span data-stu-id="08385-106">When a package is unlisted, it no longer shows up in search and in any package listing, both on the PowerShell Gallery and using PowerShellGet commands.</span></span>
<span data-ttu-id="08385-107">但是，仍可通过指定精确版本下载它（精确版本可允许自动脚本继续运行）。</span><span class="sxs-lookup"><span data-stu-id="08385-107">However, it remains downloadable by specifying its exact version, which is what allows the automated scripts to continue working.</span></span>

<span data-ttu-id="08385-108">如果遇到认为必须删除一个包的特殊情况，PowerShell 库团队可手动解决此问题。</span><span class="sxs-lookup"><span data-stu-id="08385-108">If you run into an exceptional situation where you think one of your packages must be deleted, this can be handled manually by the PowerShell Gallery team.</span></span>
<span data-ttu-id="08385-109">例如，如果存在侵犯版权问题或潜在有害内容，这是删除项的正当理由。</span><span class="sxs-lookup"><span data-stu-id="08385-109">For example, if there is a copyright infringement issue, or potentially harmful content, that could be a valid reason to delete it.</span></span>
<span data-ttu-id="08385-110">在这种情况下，应通过 [PowerShell 库](http://www.PowerShellGallery.com)提交支持请求。</span><span class="sxs-lookup"><span data-stu-id="08385-110">You should submit a support request through [PowerShell Gallery](http://www.PowerShellGallery.com) in that case.</span></span>