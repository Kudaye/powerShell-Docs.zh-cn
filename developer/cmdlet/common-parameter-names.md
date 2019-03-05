---
title: 常见的参数名称 |Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0db9f54c-4014-4450-9e81-c9f5fe562a0e
caps.latest.revision: 12
ms.openlocfilehash: a421d151ac3fdbb763668dd6fbf775f5b91a833f
ms.sourcegitcommit: 6ae5b50a4b3ffcd649de1525c3ce6f15d3669082
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56863643"
---
# <a name="common-parameter-names"></a><span data-ttu-id="677af-102">常见参数名称</span><span class="sxs-lookup"><span data-stu-id="677af-102">Common Parameter Names</span></span>

<span data-ttu-id="677af-103">本主题中所述的参数嘿*通用参数*。</span><span class="sxs-lookup"><span data-stu-id="677af-103">The parameters described in this topic are referred to as *common parameters*.</span></span> <span data-ttu-id="677af-104">它们由 Windows PowerShell 运行时添加到 cmdlet，并不能声明为 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="677af-104">They are added to cmdlets by the Windows PowerShell runtime and cannot be declared by the cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="677af-105">这些参数也会添加到提供程序 cmdlet 和函数使用修饰`CmdletBinding`属性。</span><span class="sxs-lookup"><span data-stu-id="677af-105">These parameters are also added to provider cmdlets and to functions that are decorated with the `CmdletBinding` attribute.</span></span>

## <a name="general-common-parameters"></a><span data-ttu-id="677af-106">常规常见参数</span><span class="sxs-lookup"><span data-stu-id="677af-106">General Common Parameters</span></span>

<span data-ttu-id="677af-107">以下参数添加到所有 cmdlet 和可访问，无论何时运行该 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="677af-107">The following parameters are added to all cmdlets and can be accessed whenever the cmdlet is run.</span></span> <span data-ttu-id="677af-108">这些参数定义由[System.Management.Automation.Internal.Commonparameters](/dotnet/api/System.Management.Automation.Internal.CommonParameters)类。</span><span class="sxs-lookup"><span data-stu-id="677af-108">These parameters are defined by the [System.Management.Automation.Internal.Commonparameters](/dotnet/api/System.Management.Automation.Internal.CommonParameters) class.</span></span>

### <a name="debug-alias-db"></a><span data-ttu-id="677af-109">调试 (别名： db)</span><span class="sxs-lookup"><span data-stu-id="677af-109">Debug (alias: db)</span></span>

<span data-ttu-id="677af-110">数据类型：SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="677af-110">Data type: SwitchParameter</span></span>

<span data-ttu-id="677af-111">此参数指定是否程序员级别调试消息，可以显示在命令行。</span><span class="sxs-lookup"><span data-stu-id="677af-111">This parameter specifies whether programmer-level debugging messages that can be displayed at the command line.</span></span> <span data-ttu-id="677af-112">这些消息用于故障排除的 cmdlet，该操作，并通过调用生成[System.Management.Automation.Cmdlet.Writedebug\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug)方法。</span><span class="sxs-lookup"><span data-stu-id="677af-112">These messages are intended for troubleshooting the operation of the cmdlet, and are generated by calls to the [System.Management.Automation.Cmdlet.Writedebug\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) method.</span></span> <span data-ttu-id="677af-113">调试消息不需要本地化。</span><span class="sxs-lookup"><span data-stu-id="677af-113">Debug messages do not need to be localized.</span></span>

### <a name="erroraction-alias-ea"></a><span data-ttu-id="677af-114">ErrorAction (别名： ea)</span><span class="sxs-lookup"><span data-stu-id="677af-114">ErrorAction (alias: ea)</span></span>

<span data-ttu-id="677af-115">数据类型：枚举</span><span class="sxs-lookup"><span data-stu-id="677af-115">Data type: Enumeration</span></span>

<span data-ttu-id="677af-116">此参数指定发生错误时采取的操作应发生。</span><span class="sxs-lookup"><span data-stu-id="677af-116">This parameter specifies what action should take place when an error occurs.</span></span> <span data-ttu-id="677af-117">此参数的可能值定义由[System.Management.Automation.Actionpreference](/dotnet/api/System.Management.Automation.ActionPreference)枚举。</span><span class="sxs-lookup"><span data-stu-id="677af-117">The possible values for this parameter are defined by the [System.Management.Automation.Actionpreference](/dotnet/api/System.Management.Automation.ActionPreference) enumeration.</span></span>

### <a name="errorvariable-alias-ev"></a><span data-ttu-id="677af-118">ErrorVariable (别名： ev)</span><span class="sxs-lookup"><span data-stu-id="677af-118">ErrorVariable (alias: ev)</span></span>

<span data-ttu-id="677af-119">数据类型：字符串</span><span class="sxs-lookup"><span data-stu-id="677af-119">Data type: String</span></span>

<span data-ttu-id="677af-120">此参数指定要在其中发生错误时放置对象的变量。</span><span class="sxs-lookup"><span data-stu-id="677af-120">This parameter specifies the variable in which to place objects when an error occurs.</span></span> <span data-ttu-id="677af-121">若要将追加到此变量，使用 +*varname*而不是清除并设置变量。</span><span class="sxs-lookup"><span data-stu-id="677af-121">To append to this variable, use +*varname* rather than clearing and setting the variable.</span></span>

### <a name="outvariable-alias-ov"></a><span data-ttu-id="677af-122">OutVariable (别名： 时，可以选择)</span><span class="sxs-lookup"><span data-stu-id="677af-122">OutVariable (alias: ov)</span></span>

<span data-ttu-id="677af-123">数据类型：字符串</span><span class="sxs-lookup"><span data-stu-id="677af-123">Data type: String</span></span>

<span data-ttu-id="677af-124">此参数指定要在其中放置所有输出由 cmdlet 生成的对象的变量。</span><span class="sxs-lookup"><span data-stu-id="677af-124">This parameter specifies the variable in which to place all output objects generated by the cmdlet.</span></span> <span data-ttu-id="677af-125">若要将追加到此变量，使用 +*varname*而不是清除并设置变量。</span><span class="sxs-lookup"><span data-stu-id="677af-125">To append to this variable, use +*varname* rather than clearing and setting the variable.</span></span>

### <a name="outbuffer-alias-ob"></a><span data-ttu-id="677af-126">OutBuffer (别名： ob)</span><span class="sxs-lookup"><span data-stu-id="677af-126">OutBuffer (alias: ob)</span></span>

<span data-ttu-id="677af-127">数据类型：Int32</span><span class="sxs-lookup"><span data-stu-id="677af-127">Data type: Int32</span></span>

<span data-ttu-id="677af-128">此参数定义要在管道向下传递的任何对象之前，在输出缓冲区中存储对象的数。</span><span class="sxs-lookup"><span data-stu-id="677af-128">This parameter defines the number of objects to store in the output buffer before any objects are passed down the pipeline.</span></span> <span data-ttu-id="677af-129">默认情况下，通过管道向下立即传递的对象中。</span><span class="sxs-lookup"><span data-stu-id="677af-129">By default, objects are passed immediately down the pipeline.</span></span>

### <a name="verbose-alias-vb"></a><span data-ttu-id="677af-130">详细 (别名： vb)</span><span class="sxs-lookup"><span data-stu-id="677af-130">Verbose (alias: vb)</span></span>

<span data-ttu-id="677af-131">数据类型：SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="677af-131">Data type: SwitchParameter</span></span>

<span data-ttu-id="677af-132">此参数指定是否该 cmdlet 将写入可以显示在命令行的解释性消息。</span><span class="sxs-lookup"><span data-stu-id="677af-132">This parameter specifies whether the cmdlet writes explanatory messages that can be displayed at the command line.</span></span> <span data-ttu-id="677af-133">这些消息用于提供给用户，更多帮助，并通过调用生成[System.Management.Automation.Cmdlet.Writeverbose\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose)方法。</span><span class="sxs-lookup"><span data-stu-id="677af-133">These messages are intended to provide additional help to the user, and are generated by calls to the [System.Management.Automation.Cmdlet.Writeverbose\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose) method.</span></span>

### <a name="warningaction-alias-wa"></a><span data-ttu-id="677af-134">WarningAction (别名： 华盛顿州)</span><span class="sxs-lookup"><span data-stu-id="677af-134">WarningAction (alias: wa)</span></span>

<span data-ttu-id="677af-135">数据类型：枚举</span><span class="sxs-lookup"><span data-stu-id="677af-135">Data type: Enumeration</span></span>

<span data-ttu-id="677af-136">此参数指定该 cmdlet 将写入一条警告消息时采取的操作应该发生。</span><span class="sxs-lookup"><span data-stu-id="677af-136">This parameter specifies what action should take place when the cmdlet writes a warning message.</span></span> <span data-ttu-id="677af-137">此参数的可能值定义由[System.Management.Automation.Actionpreference](/dotnet/api/System.Management.Automation.ActionPreference)枚举。</span><span class="sxs-lookup"><span data-stu-id="677af-137">The possible values for this parameter are defined by the [System.Management.Automation.Actionpreference](/dotnet/api/System.Management.Automation.ActionPreference) enumeration.</span></span>

### <a name="warningvariable-alias-wv"></a><span data-ttu-id="677af-138">WarningVariable (别名： 西弗吉尼亚州)</span><span class="sxs-lookup"><span data-stu-id="677af-138">WarningVariable (alias: wv)</span></span>

<span data-ttu-id="677af-139">数据类型：字符串</span><span class="sxs-lookup"><span data-stu-id="677af-139">Data type: String</span></span>

<span data-ttu-id="677af-140">此参数指定要在其中保存警告消息的变量。</span><span class="sxs-lookup"><span data-stu-id="677af-140">This parameter specifies the variable in which warning messages can be saved.</span></span> <span data-ttu-id="677af-141">若要将追加到此变量，使用 +*varname*而不是清除并设置变量。</span><span class="sxs-lookup"><span data-stu-id="677af-141">To append to this variable, use +*varname* rather than clearing and setting the variable.</span></span>

## <a name="risk-mitigation-parameters"></a><span data-ttu-id="677af-142">风险缓解参数</span><span class="sxs-lookup"><span data-stu-id="677af-142">Risk-Mitigation Parameters</span></span>

<span data-ttu-id="677af-143">以下参数添加到请求确认，才执行其操作的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="677af-143">The following parameters are added to cmdlets that requests confirmation before they perform their action.</span></span> <span data-ttu-id="677af-144">确认请求的详细信息，请参阅[请求确认](./requesting-confirmation-from-cmdlets.md)。</span><span class="sxs-lookup"><span data-stu-id="677af-144">For more information about confirmation requests, see [Requesting Confirmation](./requesting-confirmation-from-cmdlets.md).</span></span> <span data-ttu-id="677af-145">这些参数定义由[System.Management.Automation.Internal.Shouldprocessparameters](/dotnet/api/System.Management.Automation.Internal.ShouldProcessParameters)类。</span><span class="sxs-lookup"><span data-stu-id="677af-145">These parameters are defined by the [System.Management.Automation.Internal.Shouldprocessparameters](/dotnet/api/System.Management.Automation.Internal.ShouldProcessParameters) class.</span></span>

### <a name="confirm-alias-cf"></a><span data-ttu-id="677af-146">确认 (别名： cf)</span><span class="sxs-lookup"><span data-stu-id="677af-146">Confirm (alias: cf)</span></span>

<span data-ttu-id="677af-147">数据类型：SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="677af-147">Data type: SwitchParameter</span></span>

<span data-ttu-id="677af-148">此参数指定该 cmdlet 是否显示提示，询问用户是否确定要继续。</span><span class="sxs-lookup"><span data-stu-id="677af-148">This parameter specifies whether the cmdlet displays a prompt that asks if the user is sure that they want to continue.</span></span>

### <a name="whatif-alias-wi"></a><span data-ttu-id="677af-149">WhatIf (别名： wi)</span><span class="sxs-lookup"><span data-stu-id="677af-149">WhatIf (alias: wi)</span></span>

<span data-ttu-id="677af-150">数据类型：SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="677af-150">Data type: SwitchParameter</span></span>

<span data-ttu-id="677af-151">此参数指定该 cmdlet 是否写入一条消息，说明不实际在执行任何操作的情况下运行该 cmdlet 的效果。</span><span class="sxs-lookup"><span data-stu-id="677af-151">This parameter specifies whether the cmdlet writes a message that describes the effects of running the cmdlet without actually performing any action.</span></span>

## <a name="transaction-parameters"></a><span data-ttu-id="677af-152">事务参数</span><span class="sxs-lookup"><span data-stu-id="677af-152">Transaction Parameters</span></span>

<span data-ttu-id="677af-153">以下参数添加到支持事务的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="677af-153">The following parameter is added to cmdlets that support transactions.</span></span> <span data-ttu-id="677af-154">这些参数定义由[System.Management.Automation.Internal.Transactionparameters](/dotnet/api/System.Management.Automation.Internal.TransactionParameters)类。</span><span class="sxs-lookup"><span data-stu-id="677af-154">These parameters are defined by the [System.Management.Automation.Internal.Transactionparameters](/dotnet/api/System.Management.Automation.Internal.TransactionParameters) class.</span></span>

### <a name="usetransaction-alias-usetx"></a><span data-ttu-id="677af-155">UseTransaction (别名： usetx)</span><span class="sxs-lookup"><span data-stu-id="677af-155">UseTransaction (alias: usetx)</span></span>

<span data-ttu-id="677af-156">数据类型：SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="677af-156">Data type: SwitchParameter</span></span>

<span data-ttu-id="677af-157">此参数指定该 cmdlet 是否将使用当前事务执行其操作。</span><span class="sxs-lookup"><span data-stu-id="677af-157">This parameter specifies whether the cmdlet will use the current transaction to perform its action.</span></span>

## <a name="see-also"></a><span data-ttu-id="677af-158">另请参阅</span><span class="sxs-lookup"><span data-stu-id="677af-158">See Also</span></span>

[<span data-ttu-id="677af-159">System.Management.Automation.Internal.Commonparameters</span><span class="sxs-lookup"><span data-stu-id="677af-159">System.Management.Automation.Internal.Commonparameters</span></span>](/dotnet/api/System.Management.Automation.Internal.CommonParameters)

[<span data-ttu-id="677af-160">System.Management.Automation.Internal.Shouldprocessparameters</span><span class="sxs-lookup"><span data-stu-id="677af-160">System.Management.Automation.Internal.Shouldprocessparameters</span></span>](/dotnet/api/System.Management.Automation.Internal.ShouldProcessParameters)

[<span data-ttu-id="677af-161">System.Management.Automation.Internal.Transactionparameters</span><span class="sxs-lookup"><span data-stu-id="677af-161">System.Management.Automation.Internal.Transactionparameters</span></span>](/dotnet/api/System.Management.Automation.Internal.TransactionParameters)

[<span data-ttu-id="677af-162">编写 Windows PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="677af-162">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)

[<span data-ttu-id="677af-163">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="677af-163">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)