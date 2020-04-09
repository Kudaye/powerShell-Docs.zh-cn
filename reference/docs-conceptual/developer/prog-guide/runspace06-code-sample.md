---
title: RunSpace06 代码示例 |Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d71f86d5-eb62-4b16-aa95-5fd3f314ffd3
caps.latest.revision: 6
ms.openlocfilehash: d1d5e7f4096288ed09dada8eb8a61773921dc1ce
ms.sourcegitcommit: 7f2479edd329dfdc55726afff7019d45e45f9156
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80978217"
---
# <a name="runspace06-code-sample"></a><span data-ttu-id="f02b9-102">RunSpace06 代码示例</span><span class="sxs-lookup"><span data-stu-id="f02b9-102">RunSpace06 Code Sample</span></span>

<span data-ttu-id="f02b9-103">下面是[使用 Windows PowerShell 管理单元配置运行空间](https://msdn.microsoft.com/a7289ee8-9732-49ee-91c7-d533e9538b83)中所述的 Runspace06 示例的源代码。</span><span class="sxs-lookup"><span data-stu-id="f02b9-103">Here is the source code for the Runspace06 sample described in [Configuring a Runspace Using a Windows PowerShell Snap-in](https://msdn.microsoft.com/a7289ee8-9732-49ee-91c7-d533e9538b83).</span></span>
<span data-ttu-id="f02b9-104">此示例应用程序基于 Windows PowerShell 管理单元创建一个运行空间，然后使用该管理单元通过一个命令来运行管道。</span><span class="sxs-lookup"><span data-stu-id="f02b9-104">This sample application creates a runspace based on a Windows PowerShell snap-in, which is then used to run a pipeline with a single command.</span></span> <span data-ttu-id="f02b9-105">为此，应用程序将创建运行空间配置信息，创建运行空间，使用单个命令创建管道，然后执行管道。</span><span class="sxs-lookup"><span data-stu-id="f02b9-105">To do this, the application creates the runspace configuration information, creates a runspace, creates a pipeline with a single command, and then executes the pipeline.</span></span>

> [!NOTE]
> <span data-ttu-id="f02b9-106">您可以使用适用C#于 windows Vista 的 Windows 软件开发工具包和 Microsoft .NET Framework 3.0 运行时组件下载源文件（runspace06.cs）。</span><span class="sxs-lookup"><span data-stu-id="f02b9-106">You can download the C# source file (runspace06.cs) by using the Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="f02b9-107">有关下载说明，请参阅[如何安装 Windows powershell 和下载 Windows POWERSHELL SDK](/powershell/scripting/developer/installing-the-windows-powershell-sdk)。</span><span class="sxs-lookup"><span data-stu-id="f02b9-107">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/scripting/developer/installing-the-windows-powershell-sdk).</span></span>
> <span data-ttu-id="f02b9-108">下载的源文件在 **\<PowerShell 示例 >** 目录中提供。</span><span class="sxs-lookup"><span data-stu-id="f02b9-108">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="f02b9-109">代码示例</span><span class="sxs-lookup"><span data-stu-id="f02b9-109">Code Sample</span></span>

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/Runspace06/Runspace06.cs" range="11-85":::

## <a name="see-also"></a><span data-ttu-id="f02b9-110">另请参阅</span><span class="sxs-lookup"><span data-stu-id="f02b9-110">See Also</span></span>

[<span data-ttu-id="f02b9-111">Windows PowerShell 程序员指南</span><span class="sxs-lookup"><span data-stu-id="f02b9-111">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="f02b9-112">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="f02b9-112">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
