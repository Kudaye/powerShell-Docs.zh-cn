---
title: GetProc01 （C#）示例代码 |Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 65094bb7-1972-44b3-b8b0-5f639860b58c
caps.latest.revision: 5
ms.openlocfilehash: 71ba68521ed8d26d0c85169d2b0d547cc6d2d5e3
ms.sourcegitcommit: 7f2479edd329dfdc55726afff7019d45e45f9156
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80978417"
---
# <a name="getproc01-c-sample-code"></a><span data-ttu-id="74dc0-102">GetProc01 (C#) 示例代码</span><span class="sxs-lookup"><span data-stu-id="74dc0-102">GetProc01 (C#) Sample Code</span></span>

<span data-ttu-id="74dc0-103">下面的代码演示 GetProc01 示例 cmdlet 的实现。</span><span class="sxs-lookup"><span data-stu-id="74dc0-103">The following code shows the implementation of the GetProc01 sample cmdlet.</span></span> <span data-ttu-id="74dc0-104">请注意，通过将进程检索的实际工作保留给[Getprocesses \*](/dotnet/api/System.Diagnostics.Process.GetProcesses)方法，可简化 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="74dc0-104">Notice that the cmdlet is simplified by leaving the actual work of process retrieval to the [System.Diagnostics.Process.Getprocesses\*](/dotnet/api/System.Diagnostics.Process.GetProcesses) method.</span></span>

> [!NOTE]
> <span data-ttu-id="74dc0-105">你可以使用适用C#于 windows Vista 的 Microsoft Windows 软件开发工具包和 .NET Framework 3.0 运行时组件下载此 getproc01.cs cmdlet 的源文件（）。</span><span class="sxs-lookup"><span data-stu-id="74dc0-105">You can download the C# source file (getproc01.cs) for this Get-Proc cmdlet using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="74dc0-106">有关下载说明，请参阅[如何安装 Windows powershell 和下载 Windows POWERSHELL SDK](/powershell/scripting/developer/installing-the-windows-powershell-sdk)。</span><span class="sxs-lookup"><span data-stu-id="74dc0-106">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/scripting/developer/installing-the-windows-powershell-sdk).</span></span>
> <span data-ttu-id="74dc0-107">下载的源文件在 **\<PowerShell 示例 >** 目录中提供。</span><span class="sxs-lookup"><span data-stu-id="74dc0-107">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="74dc0-108">代码示例</span><span class="sxs-lookup"><span data-stu-id="74dc0-108">Code Sample</span></span>

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/GetProcessSample01/GetProcessSample01.cs" range="11-126":::

## <a name="see-also"></a><span data-ttu-id="74dc0-109">另请参阅</span><span class="sxs-lookup"><span data-stu-id="74dc0-109">See Also</span></span>

[<span data-ttu-id="74dc0-110">Windows PowerShell 程序员指南</span><span class="sxs-lookup"><span data-stu-id="74dc0-110">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="74dc0-111">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="74dc0-111">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
