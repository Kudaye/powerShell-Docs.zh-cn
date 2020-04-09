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
# <a name="runspace06-code-sample"></a>RunSpace06 代码示例

下面是[使用 Windows PowerShell 管理单元配置运行空间](https://msdn.microsoft.com/a7289ee8-9732-49ee-91c7-d533e9538b83)中所述的 Runspace06 示例的源代码。
此示例应用程序基于 Windows PowerShell 管理单元创建一个运行空间，然后使用该管理单元通过一个命令来运行管道。 为此，应用程序将创建运行空间配置信息，创建运行空间，使用单个命令创建管道，然后执行管道。

> [!NOTE]
> 您可以使用适用C#于 windows Vista 的 Windows 软件开发工具包和 Microsoft .NET Framework 3.0 运行时组件下载源文件（runspace06.cs）。 有关下载说明，请参阅[如何安装 Windows powershell 和下载 Windows POWERSHELL SDK](/powershell/scripting/developer/installing-the-windows-powershell-sdk)。
> 下载的源文件在 **\<PowerShell 示例 >** 目录中提供。

## <a name="code-sample"></a>代码示例

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/Runspace06/Runspace06.cs" range="11-85":::

## <a name="see-also"></a>另请参阅

[Windows PowerShell 程序员指南](./windows-powershell-programmer-s-guide.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)
