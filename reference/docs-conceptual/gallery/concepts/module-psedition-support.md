---
ms.date: 03/28/2019
contributor: manikb
keywords: 库,powershell,cmdlet,psget
title: 具有兼容的 PowerShell 版本的模块
ms.openlocfilehash: 425588c168a4f864fdc0c52aa53cfd748b80dc98
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "71328498"
---
# <a name="modules-with-compatible-powershell-editions"></a><span data-ttu-id="b39c1-103">具有兼容的 PowerShell 版本的模块</span><span class="sxs-lookup"><span data-stu-id="b39c1-103">Modules with compatible PowerShell Editions</span></span>

<span data-ttu-id="b39c1-104">从版本 5.1 开始，PowerShell 以表现出不同功能集和平台兼容性的不同版本提供。</span><span class="sxs-lookup"><span data-stu-id="b39c1-104">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="b39c1-105">**桌面版：** 在 .NET Framework 上生成，适用于 Windows 桌面、Windows Server、Windows Server Core 和大多数其他 Windows 版本上的 Windows PowerShell v4.0 和更低版本以及 Windows PowerShell 5.1。</span><span class="sxs-lookup"><span data-stu-id="b39c1-105">**Desktop Edition:** Built on .NET Framework, applies to Windows PowerShell v4.0 and below as well as Windows PowerShell 5.1 on Windows Desktop, Windows Server, Windows Server Core and most other Windows editions.</span></span>
- <span data-ttu-id="b39c1-106">**核心版：** 在 .NET Core 上生成，适用于减少了占用情况的 Windows 版本（如 Windows IoT 和 Windows Nanoserver）上的 PowerShell Core 6.0 和更高版本以及 Windows PowerShell 5.1。</span><span class="sxs-lookup"><span data-stu-id="b39c1-106">**Core Edition:** Built on .NET Core, applies to PowerShell Core 6.0 and above as well as Windows PowerShell 5.1 on reduced footprint Windows Editions such as Windows IoT and Windows Nanoserver.</span></span>

<span data-ttu-id="b39c1-107">有关 PowerShell 版本的详细信息，请参阅 [about_PowerShell_Editions][]。</span><span class="sxs-lookup"><span data-stu-id="b39c1-107">For more information on PowerShell editions, see [about_PowerShell_Editions][].</span></span>

## <a name="declaring-compatible-editions"></a><span data-ttu-id="b39c1-108">声明兼容的版本</span><span class="sxs-lookup"><span data-stu-id="b39c1-108">Declaring compatible editions</span></span>

<span data-ttu-id="b39c1-109">模块作者可使用 CompatiblePSEditions 模块清单键声明其模块，使其与一个或多个 PowerShell 版本兼容。</span><span class="sxs-lookup"><span data-stu-id="b39c1-109">Module authors can declare their modules to be compatible with one or more PowerShell editions using the CompatiblePSEditions module manifest key.</span></span> <span data-ttu-id="b39c1-110">仅 PowerShell 5.1 或更高版本支持该键。</span><span class="sxs-lookup"><span data-stu-id="b39c1-110">This key is only supported on PowerShell 5.1 or later.</span></span>

> [!NOTE]
> <span data-ttu-id="b39c1-111">使用 CompatiblePSEditions 键指定模块清单后，该清单无法导入到 PowerShell 版本 4 及更低版本。</span><span class="sxs-lookup"><span data-stu-id="b39c1-111">Once a module manifest is specified with the CompatiblePSEditions key, it can not be imported on PowerShell versions 4 and below.</span></span>

```powershell
New-ModuleManifest -Path .\TestModuleWithEdition.psd1 -CompatiblePSEditions Desktop,Core -PowerShellVersion 5.1
$ModuleInfo = Test-ModuleManifest -Path .\TestModuleWithEdition.psd1
$ModuleInfo.CompatiblePSEditions
```

```Output
Desktop
Core
```

```powershell
$ModuleInfo | Get-Member CompatiblePSEditions
```

```Output
   TypeName: System.Management.Automation.PSModuleInfo

Name                 MemberType Definition
----                 ---------- ----------
CompatiblePSEditions Property   System.Collections.Generic.IEnumerable[string] CompatiblePSEditions {get;}
```

<span data-ttu-id="b39c1-112">可通过 PowerShell 版本筛选列表来获取一列可用模块。</span><span class="sxs-lookup"><span data-stu-id="b39c1-112">When getting a list of available modules, you can filter the list by PowerShell edition.</span></span>

```powershell
Get-Module -ListAvailable -PSEdition Desktop
```

```Output
    Directory: C:\Program Files\WindowsPowerShell\Modules


ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Manifest   1.0        ModuleWithPSEditions
```

```powershell
Get-Module -ListAvailable -PSEdition Core | % CompatiblePSEditions
```

```Output
Desktop
Core
```

## <a name="targeting-multiple-editions"></a><span data-ttu-id="b39c1-113">面向多个版本</span><span class="sxs-lookup"><span data-stu-id="b39c1-113">Targeting multiple editions</span></span>

<span data-ttu-id="b39c1-114">模块作者可发布面向 PowerShell 的两个版本（Desktop 和 Core）或其中之一的单一模块。</span><span class="sxs-lookup"><span data-stu-id="b39c1-114">Module authors can publish a single module targeting to either or both PowerShell editions (Desktop and Core).</span></span>

<span data-ttu-id="b39c1-115">由于模块作者必须使用 $PSEdition 变量在 RootModule 或模块清单中添加所需的逻辑，因此单一模块可同时在 Desktop 和 Core 版本上运行。</span><span class="sxs-lookup"><span data-stu-id="b39c1-115">A single module can work on both Desktop and Core editions, in that module author has to add required logic in either RootModule or in the module manifest using $PSEdition variable.</span></span> <span data-ttu-id="b39c1-116">模块可以有两套以 CoreCLR 和 FullCLR 为目标的已编译 DLL。</span><span class="sxs-lookup"><span data-stu-id="b39c1-116">Modules can have two sets of compiled DLLs targeting both CoreCLR and FullCLR.</span></span> <span data-ttu-id="b39c1-117">以下是两种使用逻辑打包模块来加载合适的 dll 的选项。</span><span class="sxs-lookup"><span data-stu-id="b39c1-117">Here are the couple of options to package your module with logic for loading proper dlls.</span></span>

### <a name="option-1-packaging-a-module-for-targeting-multiple-versions-and-multiple-editions-of-powershell"></a><span data-ttu-id="b39c1-118">选项 1：打包面向多个版本和多个 PowerShell 版本的模块</span><span class="sxs-lookup"><span data-stu-id="b39c1-118">Option 1: Packaging a module for targeting multiple versions and multiple editions of PowerShell</span></span>

<span data-ttu-id="b39c1-119">模块文件夹内容</span><span class="sxs-lookup"><span data-stu-id="b39c1-119">Module folder contents</span></span>

- <span data-ttu-id="b39c1-120">Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="b39c1-120">Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span>
- <span data-ttu-id="b39c1-121">Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="b39c1-121">Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span>
- <span data-ttu-id="b39c1-122">PSScriptAnalyzer.psd1</span><span class="sxs-lookup"><span data-stu-id="b39c1-122">PSScriptAnalyzer.psd1</span></span>
- <span data-ttu-id="b39c1-123">PSScriptAnalyzer.psm1</span><span class="sxs-lookup"><span data-stu-id="b39c1-123">PSScriptAnalyzer.psm1</span></span>
- <span data-ttu-id="b39c1-124">ScriptAnalyzer.format.ps1xml</span><span class="sxs-lookup"><span data-stu-id="b39c1-124">ScriptAnalyzer.format.ps1xml</span></span>
- <span data-ttu-id="b39c1-125">ScriptAnalyzer.types.ps1xml</span><span class="sxs-lookup"><span data-stu-id="b39c1-125">ScriptAnalyzer.types.ps1xml</span></span>
- <span data-ttu-id="b39c1-126">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="b39c1-126">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span>
- <span data-ttu-id="b39c1-127">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="b39c1-127">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span>
- <span data-ttu-id="b39c1-128">en-US\about_PSScriptAnalyzer.help.txt</span><span class="sxs-lookup"><span data-stu-id="b39c1-128">en-US\about_PSScriptAnalyzer.help.txt</span></span>
- <span data-ttu-id="b39c1-129">en-US\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll-Help.xml</span><span class="sxs-lookup"><span data-stu-id="b39c1-129">en-US\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll-Help.xml</span></span>
- <span data-ttu-id="b39c1-130">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="b39c1-130">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span>
- <span data-ttu-id="b39c1-131">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="b39c1-131">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span>
- <span data-ttu-id="b39c1-132">Settings\CmdletDesign.psd1</span><span class="sxs-lookup"><span data-stu-id="b39c1-132">Settings\CmdletDesign.psd1</span></span>
- <span data-ttu-id="b39c1-133">Settings\DSC.psd1</span><span class="sxs-lookup"><span data-stu-id="b39c1-133">Settings\DSC.psd1</span></span>
- <span data-ttu-id="b39c1-134">Settings\ScriptFunctions.psd1</span><span class="sxs-lookup"><span data-stu-id="b39c1-134">Settings\ScriptFunctions.psd1</span></span>
- <span data-ttu-id="b39c1-135">Settings\ScriptingStyle.psd1</span><span class="sxs-lookup"><span data-stu-id="b39c1-135">Settings\ScriptingStyle.psd1</span></span>
- <span data-ttu-id="b39c1-136">Settings\ScriptSecurity.psd1</span><span class="sxs-lookup"><span data-stu-id="b39c1-136">Settings\ScriptSecurity.psd1</span></span>

<span data-ttu-id="b39c1-137">PSScriptAnalyzer.psd1 文件内容</span><span class="sxs-lookup"><span data-stu-id="b39c1-137">Contents of PSScriptAnalyzer.psd1 file</span></span>

```powershell
@{

# Author of this module
Author = 'Microsoft Corporation'

# Script module or binary module file associated with this manifest.
RootModule = 'PSScriptAnalyzer.psm1'

# Version number of this module.
ModuleVersion = '1.6.1'

# ---
}
```

<span data-ttu-id="b39c1-138">以下逻辑基于当前版本加载所需程序集。</span><span class="sxs-lookup"><span data-stu-id="b39c1-138">Below logic loads the required assemblies depending on the current edition or version.</span></span>

<span data-ttu-id="b39c1-139">PSScriptAnalyzer.psm1 文件内容：</span><span class="sxs-lookup"><span data-stu-id="b39c1-139">Contents of PSScriptAnalyzer.psm1 file:</span></span>

```powershell
#
# Script module for module 'PSScriptAnalyzer'
#
Set-StrictMode -Version Latest

# Set up some helper variables to make it easier to work with the module
$PSModule = $ExecutionContext.SessionState.Module
$PSModuleRoot = $PSModule.ModuleBase

# Import the appropriate nested binary module based on the current PowerShell version
$binaryModuleRoot = $PSModuleRoot


if (($PSVersionTable.Keys -contains "PSEdition") -and ($PSVersionTable.PSEdition -ne 'Desktop')) {
    $binaryModuleRoot = Join-Path -Path $PSModuleRoot -ChildPath 'coreclr'
}
else
{
    if ($PSVersionTable.PSVersion -lt [Version]'5.0')
    {
        $binaryModuleRoot = Join-Path -Path $PSModuleRoot -ChildPath 'PSv3'
    }
}

$binaryModulePath = Join-Path -Path $binaryModuleRoot -ChildPath 'Microsoft.Windows.PowerShell.ScriptAnalyzer.dll'
$binaryModule = Import-Module -Name $binaryModulePath -PassThru

# When the module is unloaded, remove the nested binary module that was loaded with it
$PSModule.OnRemove = {
    Remove-Module -ModuleInfo $binaryModule
}
```

### <a name="option-2-use-psedition-variable-in-the-psd1-file-to-load-the-proper-dlls-and-nestedrequired-modules"></a><span data-ttu-id="b39c1-140">选项 2：使用 PSD1 文件中的 $PSEdition 变量加载适当的 Dll 和嵌套/必需模块</span><span class="sxs-lookup"><span data-stu-id="b39c1-140">Option 2: Use $PSEdition variable in the PSD1 file to load the proper DLLs and Nested/Required modules</span></span>

<span data-ttu-id="b39c1-141">在 PS 5.1 或更高版本中，模块清单文件中允许使用 $PSEdition 全局变量。</span><span class="sxs-lookup"><span data-stu-id="b39c1-141">In PS 5.1 or newer, $PSEdition global variable is allowed in the module manifest file.</span></span> <span data-ttu-id="b39c1-142">使用此变量，模块作者可在模块清单文件中指定条件值。</span><span class="sxs-lookup"><span data-stu-id="b39c1-142">Using this variable, module author can specify the conditional values in the module manifest file.</span></span> <span data-ttu-id="b39c1-143">可在受限语言模式或数据部分引用 $PSEdition 变量。</span><span class="sxs-lookup"><span data-stu-id="b39c1-143">$PSEdition variable can be referenced in restricted language mode or a Data section.</span></span>

> [!NOTE]
> <span data-ttu-id="b39c1-144">通过 CompatiblePSEditions 键或使用 `$PSEdition` 变量指定模块清单后，该清单无法导入到较低版本的 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b39c1-144">Once a module manifest is specified with the CompatiblePSEditions key or uses `$PSEdition` variable, it can not be imported on lower versions of PowerShell.</span></span>

<span data-ttu-id="b39c1-145">具有 CompatiblePSEditions 键的示例模块清单</span><span class="sxs-lookup"><span data-stu-id="b39c1-145">Sample module manifest file with CompatiblePSEditions key</span></span>

```powershell
@{
    # Script module or binary module file associated with this manifest.
    RootModule = if($PSEdition -eq 'Core')
    {
        'coreclr\MyCoreClrRM.dll'
    }
    else # Desktop
    {
        'clr\MyFullClrRM.dll'
    }

    # Supported PSEditions
    CompatiblePSEditions = 'Desktop', 'Core'

    # Modules to import as nested modules of the module specified in RootModule/ModuleToProcess
    NestedModules = if($PSEdition -eq 'Core')
    {
        'coreclr\MyCoreClrNM1.dll',
        'coreclr\MyCoreClrNM2.dll'
    }
    else # Desktop
    {
        'clr\MyFullClrNM1.dll',
        'clr\MyFullClrNM2.dll'
    }
}
```

### <a name="module-contents"></a><span data-ttu-id="b39c1-146">模块内容</span><span class="sxs-lookup"><span data-stu-id="b39c1-146">Module contents</span></span>

```powershell
dir -Recurse
```

```Output
    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions

Mode           LastWriteTime   Length Name
----           -------------   ------ ----
d-----    7/5/2016   1:37 PM          clr
d-----    7/5/2016   1:36 PM          coreclr
-a----    7/5/2016   1:34 PM     4906 ModuleWithEditions.psd1

    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions\clr

Mode           LastWriteTime    Length Name
----           -------------    ------ ----
-a----    7/5/2016   1:35 PM         0 MyFullClrNM1.dll
-a----    7/5/2016   1:35 PM         0 MyFullClrNM2.dll
-a----    7/5/2016   1:35 PM         0 MyFullClrRM.dl

    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions\coreclr

Mode           LastWriteTime   Length Name
----           -------------   ------ ----
-a----    7/5/2016   1:35 PM        0 MyCoreClrNM1.dll
-a----    7/5/2016   1:35 PM        0 MyCoreClrNM2.dll
-a----    7/5/2016   1:35 PM        0 MyCoreClrRM.dl
```

<span data-ttu-id="b39c1-147">PowerShell 库用户可使用 PSEdition_Desktop 和 PSEdition_Core 标记查找某特定 PowerShell 版本支持的模块列表。</span><span class="sxs-lookup"><span data-stu-id="b39c1-147">PowerShell Gallery users can find the list of modules supported on a specific PowerShell Edition using tags PSEdition_Desktop and PSEdition_Core.</span></span>

<span data-ttu-id="b39c1-148">不带 PSEdition_Desktop 和 PSEdition_Core 标记的模块可以在 PowerShell Desktop 版本上运行。</span><span class="sxs-lookup"><span data-stu-id="b39c1-148">Modules without PSEdition_Desktop and PSEdition_Core tags are considered to work fine on PowerShell Desktop editions.</span></span>

```powershell
# Find modules supported on PowerShell Desktop edition
Find-Module -Tag PSEdition_Desktop

# Find modules supported on PowerShell Core editions
Find-Module -Tag PSEdition_Core
```

## <a name="more-details"></a><span data-ttu-id="b39c1-149">更多详细信息</span><span class="sxs-lookup"><span data-stu-id="b39c1-149">More details</span></span>

[<span data-ttu-id="b39c1-150">PSEditions 脚本</span><span class="sxs-lookup"><span data-stu-id="b39c1-150">Scripts with PSEditions</span></span>](script-psedition-support.md)

[<span data-ttu-id="b39c1-151">PowerShell 库的 PSEditions 支持</span><span class="sxs-lookup"><span data-stu-id="b39c1-151">PSEditions support on PowerShellGallery</span></span>](../how-to/finding-packages/searching-by-compatibility.md)

[<span data-ttu-id="b39c1-152">更新模块清单</span><span class="sxs-lookup"><span data-stu-id="b39c1-152">Update module manifest</span></span>](/powershell/module/powershellget/update-modulemanifest)

<span data-ttu-id="b39c1-153">[about_PowerShell_Editions][]</span><span class="sxs-lookup"><span data-stu-id="b39c1-153">[about_PowerShell_Editions][]</span></span>

[about_PowerShell_Editions]: /powershell/module/Microsoft.PowerShell.Core/About/about_PowerShell_Editions
