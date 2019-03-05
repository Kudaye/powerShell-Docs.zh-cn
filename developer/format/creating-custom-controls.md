---
title: 创建自定义控件 |Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c3baa406-cd33-4420-be5a-07ef09d93480
caps.latest.revision: 8
ms.openlocfilehash: 3504ab1d974c55e9279172d0e851961474ccb926
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2019
ms.locfileid: "56853193"
---
# <a name="creating-custom-controls"></a><span data-ttu-id="45907-102">创建自定义控件</span><span class="sxs-lookup"><span data-stu-id="45907-102">Creating Custom Controls</span></span>

<span data-ttu-id="45907-103">自定义控件是格式设置文件的最灵活组件。</span><span class="sxs-lookup"><span data-stu-id="45907-103">Custom controls are the most flexible components of a formatting file.</span></span> <span data-ttu-id="45907-104">与表、 列表和宽视图定义的数据，表的数据，例如正式结构的不同自定义控件，可以定义单独的数据片的显示方式。</span><span class="sxs-lookup"><span data-stu-id="45907-104">Unlike table, list, and wide views that define a formal structure of data, such as a table of data, custom controls allow you to define how an individual piece of data is displayed.</span></span> <span data-ttu-id="45907-105">可以定义一组通用的可供的格式设置文件的所有视图的自定义控件，可以定义自定义控件，可用于特定视图，或可以定义一组可供一组对象的控件。</span><span class="sxs-lookup"><span data-stu-id="45907-105">You can define a common set of custom controls that are available to all the views of the formatting file, you can define custom controls that are available to a specific view, or you can define a set of controls that are available to a group of objects.</span></span>

## <a name="custom-control-example"></a><span data-ttu-id="45907-106">自定义控件示例</span><span class="sxs-lookup"><span data-stu-id="45907-106">Custom Control Example</span></span>

<span data-ttu-id="45907-107">下面的示例显示 Certificates.Format.ps1xml 文件中定义的自定义控件。</span><span class="sxs-lookup"><span data-stu-id="45907-107">The following example shows a custom control that is defined in the Certificates.Format.ps1xml file.</span></span> <span data-ttu-id="45907-108">此自定义控件用于分隔[System.Management.Automation.Signature](/dotnet/api/System.Management.Automation.Signature)表视图中显示的对象。</span><span class="sxs-lookup"><span data-stu-id="45907-108">This custom control is used to separate the [System.Management.Automation.Signature](/dotnet/api/System.Management.Automation.Signature) objects displayed in a table view.</span></span>

```xml
<Controls>
  <Control>
    <Name>SignatureTypes-GroupingFormat</Name>
    <CustomControl>
      <CustomEntries>
        <CustomEntry>
          <CustomItem>
            <Frame>
              <LeftIndent>4</LeftIndent>
              <CustomItem>
                <Text AssemblyName="System.Management.Automation" BaseName="FileSystemProviderStrings"
                  ResourceId="DirectoryDisplayGrouping"/>
                <ExpressionBinding>
                  <ScriptBlock>split-path $_.Path</ScriptBlock>
                </ExpressionBinding>
                <NewLine/>
              </CustomItem>
            </Frame>
          </CustomItem>
        </CustomEntry>
      </CustomEntries>
    </CustomControl>
  </Control>
</Controls>

```

## <a name="see-also"></a><span data-ttu-id="45907-109">另请参阅</span><span class="sxs-lookup"><span data-stu-id="45907-109">See Also</span></span>

[<span data-ttu-id="45907-110">编写 PowerShell 格式设置文件</span><span class="sxs-lookup"><span data-stu-id="45907-110">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)