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
# <a name="getproc01-c-sample-code"></a>GetProc01 (C#) 示例代码

下面的代码演示 GetProc01 示例 cmdlet 的实现。 请注意，通过将进程检索的实际工作保留给[Getprocesses *](/dotnet/api/System.Diagnostics.Process.GetProcesses)方法，可简化 cmdlet。

> [!NOTE]
> 你可以使用适用C#于 windows Vista 的 Microsoft Windows 软件开发工具包和 .NET Framework 3.0 运行时组件下载此 getproc01.cs cmdlet 的源文件（）。 有关下载说明，请参阅[如何安装 Windows powershell 和下载 Windows POWERSHELL SDK](/powershell/scripting/developer/installing-the-windows-powershell-sdk)。
> 下载的源文件在 **\<PowerShell 示例 >** 目录中提供。

## <a name="code-sample"></a>代码示例

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/GetProcessSample01/GetProcessSample01.cs" range="11-126":::

## <a name="see-also"></a>另请参阅

[Windows PowerShell 程序员指南](./windows-powershell-programmer-s-guide.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)
