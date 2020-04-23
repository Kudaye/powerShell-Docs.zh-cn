---
ms.date: 12/31/2019
keywords: powershell,cmdlet
title: ISEMenuItem 对象
ms.openlocfilehash: c3ffe6e8f0b28987543fe0a873c552292dc5158a
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "75736975"
---
# <a name="the-isemenuitem-object"></a><span data-ttu-id="b02ef-103">ISEMenuItem 对象</span><span class="sxs-lookup"><span data-stu-id="b02ef-103">The ISEMenuItem Object</span></span>

<span data-ttu-id="b02ef-104">ISEMenuItem 对象是 Microsoft.PowerShell.Host.ISE.ISEMenuItem 类的实例。  </span><span class="sxs-lookup"><span data-stu-id="b02ef-104">An **ISEMenuItem** object is an instance of the **Microsoft.PowerShell.Host.ISE.ISEMenuItem** class.</span></span>
<span data-ttu-id="b02ef-105">“**加载项**”菜单上的所有对象都是 **Microsoft.PowerShell.Host.ISE.ISEMenuItem** 类的实例。</span><span class="sxs-lookup"><span data-stu-id="b02ef-105">All menu objects on the **Add-ons** menu are instances of the **Microsoft.PowerShell.Host.ISE.ISEMenuItem** class.</span></span>

## <a name="properties"></a><span data-ttu-id="b02ef-106">属性</span><span class="sxs-lookup"><span data-stu-id="b02ef-106">Properties</span></span>

### <a name="displayname"></a><span data-ttu-id="b02ef-107">DisplayName</span><span class="sxs-lookup"><span data-stu-id="b02ef-107">DisplayName</span></span>

<span data-ttu-id="b02ef-108">在 Windows PowerShell ISE 2.0 和更高版本中受支持。</span><span class="sxs-lookup"><span data-stu-id="b02ef-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="b02ef-109">只读属性，可获取菜单项的显示名称。</span><span class="sxs-lookup"><span data-stu-id="b02ef-109">The read-only property that gets the display name of the menu item.</span></span>

```powershell
# Get the display name of the Add-ons menu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayName
```

### <a name="action"></a><span data-ttu-id="b02ef-110">操作</span><span class="sxs-lookup"><span data-stu-id="b02ef-110">Action</span></span>

<span data-ttu-id="b02ef-111">在 Windows PowerShell ISE 2.0 和更高版本中受支持。</span><span class="sxs-lookup"><span data-stu-id="b02ef-111">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="b02ef-112">只读属性，可获取脚本块。</span><span class="sxs-lookup"><span data-stu-id="b02ef-112">The read-only property that gets the block of script.</span></span> <span data-ttu-id="b02ef-113">单击菜单项时，它将调用该操作。</span><span class="sxs-lookup"><span data-stu-id="b02ef-113">It invokes the action when you click the menu item.</span></span>

```powershell
# Get the action associated with the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action

# Invoke the script associated with the first submenu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action.Invoke()
```

### <a name="shortcut"></a><span data-ttu-id="b02ef-114">快捷方式</span><span class="sxs-lookup"><span data-stu-id="b02ef-114">Shortcut</span></span>

<span data-ttu-id="b02ef-115">在 Windows PowerShell ISE 2.0 和更高版本中受支持。</span><span class="sxs-lookup"><span data-stu-id="b02ef-115">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="b02ef-116">只读属性，可获取菜单项的 Windows 输入键盘快捷方式。</span><span class="sxs-lookup"><span data-stu-id="b02ef-116">The read-only property that gets the Windows input keyboard shortcut for the menu item.</span></span>

```powershell
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

### <a name="submenus"></a><span data-ttu-id="b02ef-117">子菜单</span><span class="sxs-lookup"><span data-stu-id="b02ef-117">Submenus</span></span>

<span data-ttu-id="b02ef-118">在 Windows PowerShell ISE 2.0 和更高版本中受支持。</span><span class="sxs-lookup"><span data-stu-id="b02ef-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="b02ef-119">只读属性，可获取菜单项的[子菜单列表](The-ISEMenuItemCollection-Object.md)。</span><span class="sxs-lookup"><span data-stu-id="b02ef-119">The read-only property that gets the [list of submenus](The-ISEMenuItemCollection-Object.md) of the menu item.</span></span>

```powershell
# List the submenus of the Add-ons menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus
```

## <a name="scripting-example"></a><span data-ttu-id="b02ef-120">脚本示例</span><span class="sxs-lookup"><span data-stu-id="b02ef-120">Scripting example</span></span>

<span data-ttu-id="b02ef-121">若要更好地了解加载项菜单及其可编写脚本属性的使用，请通读下面的脚本示例。</span><span class="sxs-lookup"><span data-stu-id="b02ef-121">To better understand the use of the Add-ons menu and its scriptable properties, read through the following scripting example.</span></span>

```powershell
# This is a scripting example that shows the use of the Add-ons menu.
# Clear the Add-ons menu if any entries currently exist
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()

# Add an Add-ons menu item with an shortcut and fast access key.
# Note the use of “_”  as opposed to the “&” for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add('_Process', {Get-Process}, 'Alt+P')
# Add a nested menu - a parent and a child submenu item.
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('Parent', $null, $null)
$parentAdded.SubMenus.Add('_Dir', {dir}, 'Alt+D')
```

## <a name="see-also"></a><span data-ttu-id="b02ef-122">另请参阅</span><span class="sxs-lookup"><span data-stu-id="b02ef-122">See Also</span></span>

- [<span data-ttu-id="b02ef-123">ISEMenuItemCollection 对象</span><span class="sxs-lookup"><span data-stu-id="b02ef-123">The ISEMenuItemCollection Object</span></span>](The-ISEMenuItemCollection-Object.md)
- [<span data-ttu-id="b02ef-124">Windows PowerShell ISE 脚本对象模型的用途</span><span class="sxs-lookup"><span data-stu-id="b02ef-124">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="b02ef-125">ISE 对象模型层次结构</span><span class="sxs-lookup"><span data-stu-id="b02ef-125">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
