---
title: RunSpace08 代码示例 |Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0f286201-8a02-4b00-9a2c-1b833ccdbdbf
caps.latest.revision: 7
ms.openlocfilehash: 21d7c4fe69e5026089676c43ad69a4263732cc34
ms.sourcegitcommit: 7f2479edd329dfdc55726afff7019d45e45f9156
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80978247"
---
# <a name="runspace08-code-sample"></a><span data-ttu-id="065b0-102">RunSpace08 代码示例</span><span class="sxs-lookup"><span data-stu-id="065b0-102">RunSpace08 Code Sample</span></span>

<span data-ttu-id="065b0-103">下面是[创建将参数添加到命令的控制台应用程序](https://msdn.microsoft.com/848b2b46-60f1-4a86-b448-cfc7c0cccfba)中所述的 Runspace08 示例的源代码。</span><span class="sxs-lookup"><span data-stu-id="065b0-103">Here is the source code for the Runspace08 sample described in [Creating a Console Application That Adds Parameters to a Command](https://msdn.microsoft.com/848b2b46-60f1-4a86-b448-cfc7c0cccfba).</span></span>
<span data-ttu-id="065b0-104">此示例应用程序创建一个运行空间，创建一个管道，将两个命令添加到管道，将两个参数添加到第二个命令，然后执行管道。</span><span class="sxs-lookup"><span data-stu-id="065b0-104">This sample application creates a runspace, creates a pipeline, adds two commands to the pipeline, adds two parameters to the second command, and then executes the pipeline.</span></span> <span data-ttu-id="065b0-105">添加到管道中的命令是 `Get-Process` 和 `Sort-Object` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="065b0-105">The commands that are added to the pipeline are the `Get-Process` and `Sort-Object` cmdlets.</span></span>

## <a name="code-sample"></a><span data-ttu-id="065b0-106">代码示例</span><span class="sxs-lookup"><span data-stu-id="065b0-106">Code Sample</span></span>

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/Runspace08/Runspace08.cs" range="11-86":::

## <a name="see-also"></a><span data-ttu-id="065b0-107">另请参阅</span><span class="sxs-lookup"><span data-stu-id="065b0-107">See Also</span></span>

[<span data-ttu-id="065b0-108">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="065b0-108">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
