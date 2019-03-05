---
title: 创建 Windows PowerShell 容器提供程序 |Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- providers [PowerShell Programmer's Guide], container provider
- container providers [PowerShell Programmer's Guide]
ms.assetid: a7926647-0d18-45b2-967e-b31f92004bc4
caps.latest.revision: 5
ms.openlocfilehash: 8c111f8f2943043e4ad2a6a8677db4afe1b3cdab
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2019
ms.locfileid: "56863163"
---
# <a name="creating-a-windows-powershell-container-provider"></a><span data-ttu-id="a2b8a-102">创建 Windows PowerShell 容器提供程序</span><span class="sxs-lookup"><span data-stu-id="a2b8a-102">Creating a Windows PowerShell Container Provider</span></span>

<span data-ttu-id="a2b8a-103">本主题介绍如何创建可在多层数据存储的 Windows PowerShell 提供程序。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-103">This topic describes how to create a Windows PowerShell provider that can work on multi-layer data stores.</span></span> <span data-ttu-id="a2b8a-104">对于此类型的数据存储区中，存储的最高级别包含根项和每个后续级别被称为子项目的节点。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-104">For this type of data store, the top level of the store contains the root items and each subsequent level is referred to as a node of child items.</span></span> <span data-ttu-id="a2b8a-105">通过允许用户若要在这些子节点上运行，用户可以通过在数据存储区按层次结构交互。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-105">By allowing the user to work on these child nodes, a user can interact hierarchically through the data store.</span></span>

<span data-ttu-id="a2b8a-106">适用于多级别数据存储区的提供程序称为 Windows PowerShell 容器提供程序。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-106">Providers that can work on multi-level data stores are referred to as Windows PowerShell container providers.</span></span> <span data-ttu-id="a2b8a-107">但是，请注意只有在没有一个容器 （没有嵌套的容器） 中它的项时，可以使用 Windows PowerShell 容器提供程序。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-107">However, be aware that a Windows PowerShell container provider can be used only when there is one container (no nested containers) with items in it.</span></span> <span data-ttu-id="a2b8a-108">如果有嵌套的容器，则必须实现一个 Windows PowerShell 导航提供程序。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-108">If there are nested containers, then you must implement a Windows PowerShell navigation provider.</span></span> <span data-ttu-id="a2b8a-109">有关实现 Windows PowerShell 导航提供程序的详细信息，请参阅[创建一个 Windows PowerShell 导航提供程序](./creating-a-windows-powershell-navigation-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-109">For more information about implementing Windows PowerShell navigation provider, see [Creating a Windows PowerShell Navigation Provider](./creating-a-windows-powershell-navigation-provider.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a2b8a-110">您可以下载C#Microsoft Windows 软件开发工具包适用于 Windows Vista 和.NET Framework 3.0 运行时组件使用此提供程序的源文件 (AccessDBSampleProvider04.cs)。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-110">You can download the C# source file (AccessDBSampleProvider04.cs) for this provider using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="a2b8a-111">有关下载说明，请参阅[如何安装 Windows PowerShell 和下载 Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk)。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-111">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
> <span data-ttu-id="a2b8a-112">您可以下载C#Microsoft Windows 软件开发工具包适用于 Windows Vista 和.NET Framework 3.0 运行时组件使用此提供程序的源文件 (AccessDBSampleProvider04.cs)。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-112">You can download the C# source file (AccessDBSampleProvider04.cs) for this provider using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="a2b8a-113">有关下载说明，请参阅[如何安装 Windows PowerShell 和下载 Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk)。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-113">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="a2b8a-114">已下载的源文件中有 **\<PowerShell 示例 >** 目录。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-114">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>
>
> <span data-ttu-id="a2b8a-115">有关其他 Windows PowerShell 提供程序实现的详细信息，请参阅[设计你 Windows PowerShell 提供程序](./designing-your-windows-powershell-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-115">For more information about other Windows PowerShell provider implementations, see [Designing Your Windows PowerShell Provider](./designing-your-windows-powershell-provider.md).</span></span>

<span data-ttu-id="a2b8a-116">此处所述的 Windows PowerShell 容器提供程序定义为其单个容器，使用表和行作为容器的项定义的数据库的数据库。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-116">The Windows PowerShell container provider described here defines the database as its single container, with the tables and rows of the database defined as items of the container.</span></span>

> [!CAUTION]
> <span data-ttu-id="a2b8a-117">请注意，此设计假定具有名为 id，字段的数据库字段的类型是 LongInteger。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-117">Be aware that this design assumes a database that has a field with the name ID, and that the type of the field is LongInteger.</span></span>

<span data-ttu-id="a2b8a-118">下面是此主题中的部分列表。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-118">Here is a list of the sections in this topic.</span></span> <span data-ttu-id="a2b8a-119">如果您不熟悉编写 Windows PowerShell 容器提供程序，请阅读此信息中出现的顺序。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-119">If you are unfamiliar with writing a Windows PowerShell container provider, please read this information in the order that it appears.</span></span> <span data-ttu-id="a2b8a-120">但是，如果你熟悉编写 Windows PowerShell 容器提供程序，请直接转到所需的信息。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-120">However, if you are familiar with writing a Windows PowerShell container provider, please go directly to the information that you need.</span></span>

- [<span data-ttu-id="a2b8a-121">定义 Windows PowerShell 容器提供程序类</span><span class="sxs-lookup"><span data-stu-id="a2b8a-121">Defining a Windows PowerShell Container Provider Class</span></span>](#Defining-a-Windows-PowerShell-Container-Provider-Class)

- [<span data-ttu-id="a2b8a-122">定义基本功能</span><span class="sxs-lookup"><span data-stu-id="a2b8a-122">Defining Base Functionality</span></span>]()

- [<span data-ttu-id="a2b8a-123">正在检索子项目</span><span class="sxs-lookup"><span data-stu-id="a2b8a-123">Retrieving Child Items</span></span>](#Retrieving-Child-Items)

- [<span data-ttu-id="a2b8a-124">附加到的动态参数`Get-ChildItem`Cmdlet</span><span class="sxs-lookup"><span data-stu-id="a2b8a-124">Attaching Dynamic Parameters to the `Get-ChildItem` Cmdlet</span></span>](#Attaching-Dynamic-Parameters-to-the-Get-ChildItem-Cmdlet)

- [<span data-ttu-id="a2b8a-125">检索子项名称</span><span class="sxs-lookup"><span data-stu-id="a2b8a-125">Retrieving Child Item Names</span></span>](#Retrieving-Child-Item-Names)

- <span data-ttu-id="a2b8a-126">[附加到的动态参数`Get-ChildItem`Cmdlet （名称）](#Attaching-Dynamic-Parameters-to-the-Get-ChildItem-Cmdlet-(Name))</span><span class="sxs-lookup"><span data-stu-id="a2b8a-126">[Attaching Dynamic Parameters to the `Get-ChildItem` Cmdlet (Name)](#Attaching-Dynamic-Parameters-to-the-Get-ChildItem-Cmdlet-(Name))</span></span>

- [<span data-ttu-id="a2b8a-127">重命名项</span><span class="sxs-lookup"><span data-stu-id="a2b8a-127">Renaming Items</span></span>](#Renaming-Items)

- [<span data-ttu-id="a2b8a-128">附加到的动态参数`Rename-Item`Cmdlet</span><span class="sxs-lookup"><span data-stu-id="a2b8a-128">Attaching Dynamic Parameters to the  `Rename-Item` Cmdlet</span></span>](#Attaching-Dynamic-Parameters-to-the-Rename-Item-Cmdlet)

- [<span data-ttu-id="a2b8a-129">创建新项</span><span class="sxs-lookup"><span data-stu-id="a2b8a-129">Creating New Items</span></span>](#Creating-New-Items)

- [<span data-ttu-id="a2b8a-130">附加到的动态参数`New-Item`Cmdlet</span><span class="sxs-lookup"><span data-stu-id="a2b8a-130">Attaching Dynamic Parameters to the `New-Item` Cmdlet</span></span>](#Attaching-Dynamic-Parameters-to-the-New-Item-Cmdlet)

- [<span data-ttu-id="a2b8a-131">删除项</span><span class="sxs-lookup"><span data-stu-id="a2b8a-131">Removing a Items</span></span>](#Removing-Items)

- [<span data-ttu-id="a2b8a-132">附加到的动态参数`Remove-Item`Cmdlet</span><span class="sxs-lookup"><span data-stu-id="a2b8a-132">Attaching Dynamic Parameters to the `Remove-Item` Cmdlet</span></span>](#Attaching-Dynamic-Parameters-to-the-Remove-Item-Cmdlet)

- [<span data-ttu-id="a2b8a-133">查询子项目</span><span class="sxs-lookup"><span data-stu-id="a2b8a-133">Querying for Child Items</span></span>](#Querying-for-Child-Items)

- [<span data-ttu-id="a2b8a-134">如何运用给出的项</span><span class="sxs-lookup"><span data-stu-id="a2b8a-134">Coping Items</span></span>](#Copying-Items)

- [<span data-ttu-id="a2b8a-135">附加到的动态参数`Copy-Item`Cmdlet</span><span class="sxs-lookup"><span data-stu-id="a2b8a-135">Attaching Dynamic Parameters to the  `Copy-Item` Cmdlet</span></span>](#Attaching-Dynamic-Parameters-to-the-Copy-Item-Cmdlet)

- [<span data-ttu-id="a2b8a-136">代码示例</span><span class="sxs-lookup"><span data-stu-id="a2b8a-136">Code Sample</span></span>](#Code-Sample)

- [<span data-ttu-id="a2b8a-137">定义对象类型和格式设置</span><span class="sxs-lookup"><span data-stu-id="a2b8a-137">Defining Object Types and Formatting</span></span>]()

- [<span data-ttu-id="a2b8a-138">生成 Windows PowerShell 提供程序</span><span class="sxs-lookup"><span data-stu-id="a2b8a-138">Building the Windows PowerShell Provider</span></span>](#Building-the-Windows-PowerShell-Provider)

- [<span data-ttu-id="a2b8a-139">测试 Windows PowerShell 提供程序</span><span class="sxs-lookup"><span data-stu-id="a2b8a-139">Testing the Windows PowerShell Provider</span></span>](#Testing-the-Windows-PowerShell-Provider)

## <a name="defining-a-windows-powershell-container-provider-class"></a><span data-ttu-id="a2b8a-140">定义 Windows PowerShell 容器提供程序类</span><span class="sxs-lookup"><span data-stu-id="a2b8a-140">Defining a Windows PowerShell Container Provider Class</span></span>

<span data-ttu-id="a2b8a-141">Windows PowerShell 容器提供程序必须定义一个.NET 类，派生自[System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider)基类。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-141">A Windows PowerShell container provider must define a .NET class that derives from the [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) base class.</span></span> <span data-ttu-id="a2b8a-142">下面是在本部分中所述的 Windows PowerShell 容器提供程序的类定义。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-142">Here is the class definition for the Windows PowerShell container provider described in this section.</span></span>

```csharp
   [CmdletProvider("AccessDB", ProviderCapabilities.None)]
   public class AccessDBProvider : ContainerCmdletProvider
```

[!code-csharp[AccessDBProviderSample04.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample04/AccessDBProviderSample04.cs#L34-L35 "AccessDBProviderSample04.cs")]

<span data-ttu-id="a2b8a-143">请注意，在这类定义后， [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute)属性包含两个参数。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-143">Notice that in this class definition, the [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) attribute includes two parameters.</span></span> <span data-ttu-id="a2b8a-144">第一个参数指定由 Windows PowerShell 提供程序的用户友好名称。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-144">The first parameter specifies a user-friendly name for the provider that is used by Windows PowerShell.</span></span> <span data-ttu-id="a2b8a-145">第二个参数指定的 Windows PowerShell 的特定功能的提供程序公开到 Windows PowerShell 运行时在命令处理过程。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-145">The second parameter specifies the Windows PowerShell specific capabilities that the provider exposes to the Windows PowerShell runtime during command processing.</span></span> <span data-ttu-id="a2b8a-146">为此提供程序，没有 Windows PowerShell 特定功能添加的。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-146">For this provider, there are no Windows PowerShell specific capabilities that are added.</span></span>

## <a name="defining-base-functionality"></a><span data-ttu-id="a2b8a-147">定义基本功能</span><span class="sxs-lookup"><span data-stu-id="a2b8a-147">Defining Base Functionality</span></span>

<span data-ttu-id="a2b8a-148">如中所述[设计你 Windows PowerShell 提供程序](./designing-your-windows-powershell-provider.md)，则[System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider)类派生自多个提供其他类不同的提供程序功能。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-148">As described in [Designing Your Windows PowerShell Provider](./designing-your-windows-powershell-provider.md), the [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) class derives from several other classes that provided different provider functionality.</span></span> <span data-ttu-id="a2b8a-149">Windows PowerShell 容器提供程序，因此，需要定义的所有这些类提供的功能。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-149">A Windows PowerShell container provider, therefore, needs to define all of the functionality provided by those classes.</span></span>

<span data-ttu-id="a2b8a-150">若要实现用于添加特定于会话的初始化信息和用于释放资源提供程序使用的功能，请参阅[创建一个基本的 Windows PowerShell 提供程序](./creating-a-basic-windows-powershell-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-150">To implement functionality for adding session-specific initialization information and for releasing resources that are used by the provider, see [Creating a Basic Windows PowerShell Provider](./creating-a-basic-windows-powershell-provider.md).</span></span> <span data-ttu-id="a2b8a-151">但是，大多数提供程序 （包括此处所述的提供程序） 可以使用 Windows PowerShell 提供此功能的默认实现。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-151">However, most providers (including the provider described here) can use the default implementation of this functionality that is provided by Windows PowerShell.</span></span>

<span data-ttu-id="a2b8a-152">若要获取对数据存储的访问，提供程序必须实现的方法[System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider)基类。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-152">To get access to the data store, the provider must implement the methods of the [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) base class.</span></span> <span data-ttu-id="a2b8a-153">有关实现这些方法的详细信息，请参阅[创建 Windows PowerShell 驱动器提供程序](./creating-a-windows-powershell-drive-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-153">For more information about implementing these methods, see [Creating an Windows PowerShell Drive Provider](./creating-a-windows-powershell-drive-provider.md).</span></span>

<span data-ttu-id="a2b8a-154">若要操作的数据存储，如获取、 设置和清除项的项提供程序必须实现提供的方法[System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider)基类。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-154">To manipulate the items of a data store, such as getting, setting, and clearing items, the provider must implement the methods provided by the [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) base class.</span></span> <span data-ttu-id="a2b8a-155">有关实现这些方法的详细信息，请参阅[创建 Windows PowerShell 项提供程序](./creating-a-windows-powershell-item-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-155">For more information about implementing these methods, see [Creating an Windows PowerShell Item Provider](./creating-a-windows-powershell-item-provider.md).</span></span>

## <a name="retrieving-child-items"></a><span data-ttu-id="a2b8a-156">正在检索子项目</span><span class="sxs-lookup"><span data-stu-id="a2b8a-156">Retrieving Child Items</span></span>

<span data-ttu-id="a2b8a-157">若要检索的子项，Windows PowerShell 容器提供程序必须重写[System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems)方法，以支持来自调用`Get-ChildItem`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-157">To retrieve a child item, the Windows PowerShell container provider must override the [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) method to support calls from the `Get-ChildItem` cmdlet.</span></span> <span data-ttu-id="a2b8a-158">此方法从数据存储中检索子项目，并将其写入到管道作为对象。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-158">This method retrieves child items from the data store and writes them to the pipeline as objects.</span></span> <span data-ttu-id="a2b8a-159">如果`recurse`指定 cmdlet 参数，方法检索而不考虑这些服务都处于何种级别的所有子级。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-159">If the `recurse` parameter of the cmdlet is specified, the method retrieves all children regardless of what level they are at.</span></span> <span data-ttu-id="a2b8a-160">如果`recurse`未指定参数，该方法检索单个级别的子级。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-160">If the `recurse` parameter is not specified, the method retrieves only a single level of children.</span></span>

<span data-ttu-id="a2b8a-161">下面是实现[System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems)此提供程序的方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-161">Here is the implementation of the [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) method for this provider.</span></span> <span data-ttu-id="a2b8a-162">请注意，路径指示访问数据库，并从表中的行检索子项目，如果该路径表示数据表时，此方法，检索所有数据库表中的子项。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-162">Notice that this method retrieves the child items in all database tables when the path indicates the Access database, and retrieves the child items from the rows of that table if the path indicates a data table.</span></span>

```csharp
protected override void GetChildItems(string path, bool recurse)
{
    // If path represented is a drive then the children in the path are
    // tables. Hence all tables in the drive represented will have to be
    // returned
    if (PathIsDrive(path))
    {
        foreach (DatabaseTableInfo table in GetTables())
        {
            WriteItemObject(table, path, true);

            // if the specified item exists and recurse has been set then
            // all child items within it have to be obtained as well
            if (ItemExists(path) && recurse)
            {
                GetChildItems(path + pathSeparator + table.Name, recurse);
            }
        } // foreach (DatabaseTableInfo...
    } // if (PathIsDrive...
    else
    {
        // Get the table name, row number and type of path from the
        // path specified
        string tableName;
        int rowNumber;

        PathType type = GetNamesFromPath(path, out tableName, out rowNumber);

        if (type == PathType.Table)
        {
            // Obtain all the rows within the table
            foreach (DatabaseRowInfo row in GetRows(tableName))
            {
                WriteItemObject(row, path + pathSeparator + row.RowNumber,
                        false);
            } // foreach (DatabaseRowInfo...
        }
        else if (type == PathType.Row)
        {
            // In this case the user has directly specified a row, hence
            // just give that particular row
            DatabaseRowInfo row = GetRow(tableName, rowNumber);
            WriteItemObject(row, path + pathSeparator + row.RowNumber,
                        false);
        }
        else
        {
            // In this case, the path specified is not valid
            ThrowTerminatingInvalidPathException(path);
        }
    } // else
} // GetChildItems
```

[!code-csharp[AccessDBProviderSample04.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample04/AccessDBProviderSample04.cs#L311-L362 "AccessDBProviderSample04.cs")]

#### <a name="things-to-remember-about-implementing-getchilditems"></a><span data-ttu-id="a2b8a-163">要实现 GetChildItems 记住的事项</span><span class="sxs-lookup"><span data-stu-id="a2b8a-163">Things to Remember About Implementing GetChildItems</span></span>

<span data-ttu-id="a2b8a-164">以下条件可能适用于特定的实现[System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems):</span><span class="sxs-lookup"><span data-stu-id="a2b8a-164">The following conditions may apply to your implementation of [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems):</span></span>

- <span data-ttu-id="a2b8a-165">在定义的提供程序类时，Windows PowerShell 容器提供程序可能会从声明提供程序功能 ExpandWildcards、 筛选器、 包括或排除， [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities)枚举。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-165">When defining the provider class, a Windows PowerShell container provider might declare provider capabilities of ExpandWildcards, Filter, Include, or Exclude, from the [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumeration.</span></span> <span data-ttu-id="a2b8a-166">在这些情况下，实现[System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems)方法需要确保传递给方法的路径满足指定的要求功能。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-166">In these cases, the implementation of the [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) method needs to ensure that the path passed to the method meets the requirements of the specified capabilities.</span></span> <span data-ttu-id="a2b8a-167">若要执行此操作，该方法应访问相应的属性，例如，则[System.Management.Automation.Provider.Cmdletprovider.Exclude\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude)和[System.Management.Automation.Provider.Cmdletprovider.Include\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include)属性。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-167">To do this, the method should access the appropriate property, for example, the [System.Management.Automation.Provider.Cmdletprovider.Exclude\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) and [System.Management.Automation.Provider.Cmdletprovider.Include\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) properties.</span></span>

- <span data-ttu-id="a2b8a-168">此方法的实现应考虑到帐户的访问权限的任何窗体可能会使该项对用户可见的项。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-168">The implementation of this method should take into account any form of access to the item that might make the item visible to the user.</span></span> <span data-ttu-id="a2b8a-169">例如，如果用户具有到通过 FileSystem 提供程序 （由 Windows PowerShell 提供），但不能读取访问的文件的写访问权限，该文件仍存在和[System.Management.Automation.Provider.Itemcmdletprovider.Itemexists\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists)返回`true`。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-169">For example, if a user has write access to a file through the FileSystem provider (supplied by Windows PowerShell), but not read access, the file still exists and [System.Management.Automation.Provider.Itemcmdletprovider.Itemexists\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) returns `true`.</span></span> <span data-ttu-id="a2b8a-170">您的实现可能需要检查父项以查看子可进行枚举。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-170">Your implementation might require the checking of a parent item to see if the child can be enumerated.</span></span>

- <span data-ttu-id="a2b8a-171">编写多个项时[System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems)方法可能需要一些时间。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-171">When writing multiple items, the [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) method can take some time.</span></span> <span data-ttu-id="a2b8a-172">您可以设计你的提供商将使用项写入[System.Management.Automation.Provider.Cmdletprovider.Writeitemobject\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteItemObject)方法一次。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-172">You can design your provider to write the items using the [System.Management.Automation.Provider.Cmdletprovider.Writeitemobject\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteItemObject) method one at a time.</span></span> <span data-ttu-id="a2b8a-173">使用此方法将会向流中的用户的项。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-173">Using this technique will present the items to the user in a stream.</span></span>

- <span data-ttu-id="a2b8a-174">实现[System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems)负责有循环的链接，以及类似时防止无限递归。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-174">Your implementation of [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) is responsible for preventing infinite recursion when there are circular links, and the like.</span></span> <span data-ttu-id="a2b8a-175">应引发相应的终止异常，以反映此类情况。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-175">An appropriate terminating exception should be thrown to reflect such a condition.</span></span>

## <a name="attaching-dynamic-parameters-to-the-get-childitem-cmdlet"></a><span data-ttu-id="a2b8a-176">附加到的 Get-childitem Cmdlet 的动态参数</span><span class="sxs-lookup"><span data-stu-id="a2b8a-176">Attaching Dynamic Parameters to the Get-ChildItem Cmdlet</span></span>

<span data-ttu-id="a2b8a-177">有时`Get-ChildItem`调用的 cmdlet [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems)需要在运行时动态指定的其他参数。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-177">Sometimes the `Get-ChildItem` cmdlet that calls [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) requires additional parameters that are specified dynamically at runtime.</span></span> <span data-ttu-id="a2b8a-178">若要提供这些动态参数，Windows PowerShell 容器提供程序必须实现[System.Management.Automation.Provider.Containercmdletprovider.Getchilditemsdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItemsDynamicParameters)方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-178">To provide these dynamic parameters, the Windows PowerShell container provider must implement the [System.Management.Automation.Provider.Containercmdletprovider.Getchilditemsdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItemsDynamicParameters) method.</span></span> <span data-ttu-id="a2b8a-179">此方法检索动态参数指定的路径处的项并返回具有属性和字段与分析属性类似于 cmdlet 类的对象或[System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary)对象。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-179">This method retrieves dynamic parameters for the item at the indicated path and returns an object that has properties and fields with parsing attributes similar to a cmdlet class or a [System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) object.</span></span> <span data-ttu-id="a2b8a-180">Windows PowerShell 运行时使用返回的对象添加到参数`Get-ChildItem`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-180">The Windows PowerShell runtime uses the returned object to add the parameters to the `Get-ChildItem` cmdlet.</span></span>

<span data-ttu-id="a2b8a-181">此 Windows PowerShell 容器提供程序未实现此方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-181">This Windows PowerShell container provider does not implement this method.</span></span> <span data-ttu-id="a2b8a-182">但是，以下代码是此方法的默认实现。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-182">However, the following code is the default implementation of this method.</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidergetchilditemsdynamicparameters](Msh_samplestestcmdlets#testprovidergetchilditemsdynamicparameters)]  -->

## <a name="retrieving-child-item-names"></a><span data-ttu-id="a2b8a-183">检索子项名称</span><span class="sxs-lookup"><span data-stu-id="a2b8a-183">Retrieving Child Item Names</span></span>

<span data-ttu-id="a2b8a-184">若要检索的子项目的名称，Windows PowerShell 容器提供程序必须重写[System.Management.Automation.Provider.Containercmdletprovider.Getchildnames\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNames)方法，以支持来自调用`Get-ChildItem`cmdlet 时其`Name`指定参数。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-184">To retrieve the names of child items, the Windows PowerShell container provider must override the [System.Management.Automation.Provider.Containercmdletprovider.Getchildnames\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNames) method to support calls from the `Get-ChildItem` cmdlet when its `Name` parameter is specified.</span></span> <span data-ttu-id="a2b8a-185">此方法检索的所有容器指定的路径或子项名称的子项目的名称，如果`returnAllContainers`指定 cmdlet 参数。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-185">This method retrieves the names of the child items for the specified path or child item names for all containers if the `returnAllContainers` parameter of the cmdlet is specified.</span></span> <span data-ttu-id="a2b8a-186">子名称是路径的叶部分。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-186">A child name is the leaf portion of a path.</span></span> <span data-ttu-id="a2b8a-187">例如，路径 c:\windows\system32\abc.dll 子名称是"abc.dll"。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-187">For example, the child name for the path c:\windows\system32\abc.dll is "abc.dll".</span></span> <span data-ttu-id="a2b8a-188">目录 c:\windows\system32 的子名称是"system32"。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-188">The child name for the directory c:\windows\system32 is "system32".</span></span>

<span data-ttu-id="a2b8a-189">下面是实现[System.Management.Automation.Provider.Containercmdletprovider.Getchildnames\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNames)此提供程序的方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-189">Here is the implementation of the [System.Management.Automation.Provider.Containercmdletprovider.Getchildnames\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNames) method for this provider.</span></span> <span data-ttu-id="a2b8a-190">请注意，该方法，是否指定的路径指示的 Access 数据库 （驱动器） 和行号，如果该路径表示表中检索表名。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-190">Notice that the method retrieves table names if the specified path indicates the Access database (drive) and row numbers if the path indicates a table.</span></span>

```csharp
protected override void GetChildNames(string path,
                            ReturnContainers returnContainers)
{
    // If the path represented is a drive, then the child items are
    // tables. get the names of all the tables in the drive.
    if (PathIsDrive(path))
    {
        foreach (DatabaseTableInfo table in GetTables())
        {
            WriteItemObject(table.Name, path, true);
        } // foreach (DatabaseTableInfo...
    } // if (PathIsDrive...
    else
    {
        // Get type, table name and row number from path specified
        string tableName;
        int rowNumber;

        PathType type = GetNamesFromPath(path, out tableName, out rowNumber);

        if (type == PathType.Table)
        {
            // Get all the rows in the table and then write out the
            // row numbers.
            foreach (DatabaseRowInfo row in GetRows(tableName))
            {
                WriteItemObject(row.RowNumber, path, false);
            } // foreach (DatabaseRowInfo...
        }
        else if (type == PathType.Row)
        {
            // In this case the user has directly specified a row, hence
            // just give that particular row
            DatabaseRowInfo row = GetRow(tableName, rowNumber);

            WriteItemObject(row.RowNumber, path, false);
        }
        else
        {
            ThrowTerminatingInvalidPathException(path);
        }
    } // else
} // GetChildNames
```

[!code-csharp[AccessDBProviderSample04.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample04/AccessDBProviderSample04.cs#L369-L411 "AccessDBProviderSample04.cs")]

#### <a name="things-to-remember-about-implementing-getchildnames"></a><span data-ttu-id="a2b8a-191">要实现 GetChildNames 记住的事项</span><span class="sxs-lookup"><span data-stu-id="a2b8a-191">Things to Remember About Implementing GetChildNames</span></span>

<span data-ttu-id="a2b8a-192">以下条件可能适用于特定的实现[System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems):</span><span class="sxs-lookup"><span data-stu-id="a2b8a-192">The following conditions may apply to your implementation of [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems):</span></span>

- <span data-ttu-id="a2b8a-193">在定义的提供程序类时，Windows PowerShell 容器提供程序可能会从声明提供程序功能 ExpandWildcards、 筛选器、 包括或排除， [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities)枚举。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-193">When defining the provider class, a Windows PowerShell container provider might declare provider capabilities of ExpandWildcards, Filter, Include, or Exclude, from the [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumeration.</span></span> <span data-ttu-id="a2b8a-194">在这些情况下，实现[System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems)方法需要确保传递给方法的路径满足指定的要求功能。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-194">In these cases, the implementation of the [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) method needs to ensure that the path passed to the method meets the requirements of the specified capabilities.</span></span> <span data-ttu-id="a2b8a-195">若要执行此操作，该方法应访问相应的属性，例如，则[System.Management.Automation.Provider.Cmdletprovider.Exclude\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude)和[System.Management.Automation.Provider.Cmdletprovider.Include\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include)属性。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-195">To do this, the method should access the appropriate property, for example, the [System.Management.Automation.Provider.Cmdletprovider.Exclude\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) and [System.Management.Automation.Provider.Cmdletprovider.Include\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) properties.</span></span>

  > [!NOTE]
  > <span data-ttu-id="a2b8a-196">此规则的例外发生时`returnAllContainers`指定 cmdlet 参数。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-196">An exception to this rule occurs when the `returnAllContainers` parameter of the cmdlet is specified.</span></span> <span data-ttu-id="a2b8a-197">在这种情况下，该方法应检索任何子容器名称，即使与的值不匹配[System.Management.Automation.Provider.Cmdletprovider.Filter\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Filter)， [System.Management.Automation.Provider.Cmdletprovider.Include\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include)，或[System.Management.Automation.Provider.Cmdletprovider.Exclude\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude)属性。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-197">In this case, the method should retrieve any child name for a container, even if it does not match the values of the [System.Management.Automation.Provider.Cmdletprovider.Filter\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Filter), [System.Management.Automation.Provider.Cmdletprovider.Include\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include), or [System.Management.Automation.Provider.Cmdletprovider.Exclude\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) properties.</span></span>

- <span data-ttu-id="a2b8a-198">默认情况下，重写此方法应检索的对象，除非通常隐藏的用户名称[System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force)指定属性。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-198">By default, overrides of this method should not retrieve names of objects that are generally hidden from the user unless the [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) property is specified.</span></span> <span data-ttu-id="a2b8a-199">如果指定的路径指示容器[System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force)属性不是必需。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-199">If the specified path indicates a container, the [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) property is not required.</span></span>

- <span data-ttu-id="a2b8a-200">实现[System.Management.Automation.Provider.Containercmdletprovider.Getchildnames\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNames)负责有循环的链接，以及类似时防止无限递归。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-200">Your implementation of [System.Management.Automation.Provider.Containercmdletprovider.Getchildnames\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNames) is responsible for preventing infinite recursion when there are circular links, and the like.</span></span> <span data-ttu-id="a2b8a-201">应引发相应的终止异常，以反映此类情况。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-201">An appropriate terminating exception should be thrown to reflect such a condition.</span></span>

## <a name="attaching-dynamic-parameters-to-the-get-childitem-cmdlet-name"></a><span data-ttu-id="a2b8a-202">将动态参数附加到的 Get-childitem Cmdlet （名称）</span><span class="sxs-lookup"><span data-stu-id="a2b8a-202">Attaching Dynamic Parameters to the Get-ChildItem Cmdlet (Name)</span></span>

<span data-ttu-id="a2b8a-203">有时`Get-ChildItem`cmdlet (使用`Name`参数) 需要在运行时动态指定的其他参数。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-203">Sometimes the `Get-ChildItem` cmdlet (with the `Name` parameter) requires additional parameters that are specified dynamically at runtime.</span></span> <span data-ttu-id="a2b8a-204">若要提供这些动态参数，Windows PowerShell 容器提供程序必须实现[System.Management.Automation.Provider.Containercmdletprovider.Getchildnamesdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNamesDynamicParameters)方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-204">To provide these dynamic parameters, the Windows PowerShell container provider must implement the [System.Management.Automation.Provider.Containercmdletprovider.Getchildnamesdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNamesDynamicParameters) method.</span></span> <span data-ttu-id="a2b8a-205">此方法检索指定的路径处的项的动态参数并返回具有属性和字段与分析属性类似于 cmdlet 类的对象或[System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary)对象。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-205">This method retrieves the dynamic parameters for the item at the indicated path and returns an object that has properties and fields with parsing attributes similar to a cmdlet class or a [System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) object.</span></span> <span data-ttu-id="a2b8a-206">Windows PowerShell 运行时使用返回的对象添加到参数`Get-ChildItem`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-206">The Windows PowerShell runtime uses the returned object to add the parameters to the `Get-ChildItem` cmdlet.</span></span>

<span data-ttu-id="a2b8a-207">此提供程序未实现此方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-207">This provider does not implement this method.</span></span> <span data-ttu-id="a2b8a-208">但是，以下代码是此方法的默认实现。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-208">However, the following code is the default implementation of this method.</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidergetchildnamesdynamicparameters](Msh_samplestestcmdlets#testprovidergetchildnamesdynamicparameters)]  -->

## <a name="renaming-items"></a><span data-ttu-id="a2b8a-209">重命名项</span><span class="sxs-lookup"><span data-stu-id="a2b8a-209">Renaming Items</span></span>

<span data-ttu-id="a2b8a-210">若要重命名某个项，Windows PowerShell 容器提供程序必须重写[System.Management.Automation.Provider.Containercmdletprovider.Renameitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem)方法，以支持来自调用`Rename-Item`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-210">To rename an item, a Windows PowerShell container provider must override the [System.Management.Automation.Provider.Containercmdletprovider.Renameitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem) method to support calls from the `Rename-Item` cmdlet.</span></span> <span data-ttu-id="a2b8a-211">此方法的指定路径处的项的名称更改为提供的新名称。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-211">This method changes the name of the item at the specified path to the new name provided.</span></span> <span data-ttu-id="a2b8a-212">新名称必须始终为相对于父项 （容器）。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-212">The new name must always be relative to the parent item (container).</span></span>

<span data-ttu-id="a2b8a-213">此提供程序不会覆盖[System.Management.Automation.Provider.Containercmdletprovider.Renameitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem)方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-213">This provider does not override the [System.Management.Automation.Provider.Containercmdletprovider.Renameitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem) method.</span></span> <span data-ttu-id="a2b8a-214">但是，以下是默认实现。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-214">However, the following is the default implementation.</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testproviderrenameitem](Msh_samplestestcmdlets#testproviderrenameitem)]  -->

#### <a name="things-to-remember-about-implementing-renameitem"></a><span data-ttu-id="a2b8a-215">要实现 RenameItem 记住的事项</span><span class="sxs-lookup"><span data-stu-id="a2b8a-215">Things to Remember About Implementing RenameItem</span></span>

<span data-ttu-id="a2b8a-216">以下条件可能适用于特定的实现[System.Management.Automation.Provider.Containercmdletprovider.Renameitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem):</span><span class="sxs-lookup"><span data-stu-id="a2b8a-216">The following conditions may apply to your implementation of [System.Management.Automation.Provider.Containercmdletprovider.Renameitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem):</span></span>

- <span data-ttu-id="a2b8a-217">在定义的提供程序类时，Windows PowerShell 容器提供程序可能会从声明提供程序功能 ExpandWildcards、 筛选器、 包括或排除， [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities)枚举。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-217">When defining the provider class, a Windows PowerShell container provider might declare provider capabilities of ExpandWildcards, Filter, Include, or Exclude, from the [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumeration.</span></span> <span data-ttu-id="a2b8a-218">在这些情况下，实现[System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems)方法需要确保传递给方法的路径满足指定的要求功能。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-218">In these cases, the implementation of the [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) method needs to ensure that the path passed to the method meets the requirements of the specified capabilities.</span></span> <span data-ttu-id="a2b8a-219">若要执行此操作，该方法应访问相应的属性，例如，则[System.Management.Automation.Provider.Cmdletprovider.Exclude\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude)和[System.Management.Automation.Provider.Cmdletprovider.Include\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include)属性。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-219">To do this, the method should access the appropriate property, for example, the [System.Management.Automation.Provider.Cmdletprovider.Exclude\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) and [System.Management.Automation.Provider.Cmdletprovider.Include\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) properties.</span></span>

- <span data-ttu-id="a2b8a-220">[System.Management.Automation.Provider.Containercmdletprovider.Renameitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem)方法旨在针对仅限，项名称的修改而不是针对移动操作。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-220">The [System.Management.Automation.Provider.Containercmdletprovider.Renameitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem) method is intended for the modification of the name of an item only, and not for move operations.</span></span> <span data-ttu-id="a2b8a-221">如果该方法的实现应编写错误`newName`参数包含路径分隔符，或可能会导致要更改其父位置的项。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-221">Your implementation of the method should write an error if the `newName` parameter contains path separators, or might otherwise cause the item to change its parent location.</span></span>

- <span data-ttu-id="a2b8a-222">默认情况下，重写此方法不应重命名对象除非[System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force)指定属性。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-222">By default, overrides of this method should not rename objects unless the [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) property is specified.</span></span> <span data-ttu-id="a2b8a-223">如果指定的路径指示容器[System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force)属性不是必需。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-223">If the specified path indicates a container, the [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) property is not required.</span></span>

- <span data-ttu-id="a2b8a-224">实现[System.Management.Automation.Provider.Containercmdletprovider.Renameitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem)方法应调用[System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) ，并向数据存储区进行任何更改之前检查它的返回值。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-224">Your implementation of the [System.Management.Automation.Provider.Containercmdletprovider.Renameitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem) method should call [System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) and check its return value before making any changes to the data store.</span></span> <span data-ttu-id="a2b8a-225">此方法用于确认操作的执行时更改为系统状态，例如，重命名文件。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-225">This method is used to confirm execution of an operation when a change is made to system state, for example, renaming files.</span></span> <span data-ttu-id="a2b8a-226">[System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess)发送要更改对用户来说，与 Windows PowerShell 运行时将考虑在内的任何命令行设置或首选项变量中的资源的名称确定应显示的内容。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-226">[System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) sends the name of the resource to be changed to the user, with the Windows PowerShell runtime taking into account any command line settings or preference variables in determining what should be displayed.</span></span>

  <span data-ttu-id="a2b8a-227">在调用[System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess)返回`true`，则[System.Management.Automation.Provider.Containercmdletprovider.Renameitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem)方法应调用[System.Management.Automation.Provider.Cmdletprovider.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue)方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-227">After the call to [System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) returns `true`, the [System.Management.Automation.Provider.Containercmdletprovider.Renameitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem) method should call the [System.Management.Automation.Provider.Cmdletprovider.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) method.</span></span> <span data-ttu-id="a2b8a-228">此方法发送一条消息的确认消息给用户以允许其他反馈以说是否应继续执行该操作。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-228">This method sends a message a confirmation message to the user to allow additional feedback to say if the operation should be continued.</span></span> <span data-ttu-id="a2b8a-229">一个提供程序应调用[System.Management.Automation.Provider.Cmdletprovider.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue)作为具有潜在危险的系统修改为额外检查。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-229">A provider should call [System.Management.Automation.Provider.Cmdletprovider.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) as an additional check for potentially dangerous system modifications.</span></span>

## <a name="attaching-dynamic-parameters-to-the-rename-item-cmdlet"></a><span data-ttu-id="a2b8a-230">附加到重命名项 Cmdlet 的动态参数</span><span class="sxs-lookup"><span data-stu-id="a2b8a-230">Attaching Dynamic Parameters to the Rename-Item Cmdlet</span></span>

<span data-ttu-id="a2b8a-231">有时`Rename-Item`cmdlet 需要在运行时动态指定的其他参数。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-231">Sometimes the `Rename-Item` cmdlet requires additional parameters that are specified dynamically at runtime.</span></span> <span data-ttu-id="a2b8a-232">若要提供这些动态参数，Windows PowerShell 容器提供程序必须实现[System.Management.Automation.Provider.Containercmdletprovider.Renameitemdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItemDynamicParameters)方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-232">To provide these dynamic parameters, Windows PowerShell container provider must implement the [System.Management.Automation.Provider.Containercmdletprovider.Renameitemdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItemDynamicParameters) method.</span></span> <span data-ttu-id="a2b8a-233">此方法检索指定的路径处的项的参数并返回具有属性和字段与分析属性类似于 cmdlet 类的对象或[System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary)对象。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-233">This method retrieves the parameters for the item at the indicated path and returns an object that has properties and fields with parsing attributes similar to a cmdlet class or a [System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) object.</span></span> <span data-ttu-id="a2b8a-234">Windows PowerShell 运行时使用返回的对象添加到参数`Rename-Item`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-234">The Windows PowerShell runtime uses the returned object to add the parameters to the `Rename-Item` cmdlet.</span></span>

<span data-ttu-id="a2b8a-235">此容器提供程序未实现此方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-235">This container provider does not implement this method.</span></span> <span data-ttu-id="a2b8a-236">但是，以下代码是此方法的默认实现。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-236">However, the following code is the default implementation of this method.</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testproviderrenameitemdynamicparameters](Msh_samplestestcmdlets#testproviderrenameitemdynamicparameters)]  -->

## <a name="creating-new-items"></a><span data-ttu-id="a2b8a-237">创建新项</span><span class="sxs-lookup"><span data-stu-id="a2b8a-237">Creating New Items</span></span>

<span data-ttu-id="a2b8a-238">若要创建新项目，容器提供程序必须实现[System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem)方法，以支持来自调用`New-Item`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-238">To create new items, a container provider must implement the [System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) method to support calls from the `New-Item` cmdlet.</span></span> <span data-ttu-id="a2b8a-239">此方法创建在位于指定路径的数据项。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-239">This method creates a data item located at the specified path.</span></span> <span data-ttu-id="a2b8a-240">`type` Cmdlet 参数包含新项的定义提供程序的类型。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-240">The `type` parameter of the cmdlet contains the provider-defined type for the new item.</span></span> <span data-ttu-id="a2b8a-241">例如，FileSystem 提供程序使用`type`参数，其值为"文件"或"directory"。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-241">For example, the FileSystem provider uses a `type` parameter with a value of "file" or "directory".</span></span> <span data-ttu-id="a2b8a-242">`newItemValue` Cmdlet 参数指定新项的特定于提供程序的值。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-242">The `newItemValue` parameter of the cmdlet specifies a provider-specific value for the new item.</span></span>

<span data-ttu-id="a2b8a-243">下面是实现[System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem)此提供程序的方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-243">Here is the implementation of the [System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) method for this provider.</span></span>

```csharp
protected override void NewItem( string path, string type,
                                 object newItemValue )
{
    // Create the new item here after
    // performing necessary validations
    //
    // WriteItemObject(newItemValue, path, false);

    // Example
    //
    // if (ShouldProcess(path, "new item"))
    // {
    //      // Create a new item and then call WriteObject
    //      WriteObject(newItemValue, path, false);
    // }

} // NewItem
```

[!code-csharp[AccessDBProviderSample04.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample04/AccessDBProviderSample04.cs#L939-L955 "AccessDBProviderSample04.cs")]

#### <a name="things-to-remember-about-implementing-newitem"></a><span data-ttu-id="a2b8a-244">要实现 NewItem 记住的事项</span><span class="sxs-lookup"><span data-stu-id="a2b8a-244">Things to Remember About Implementing NewItem</span></span>

<span data-ttu-id="a2b8a-245">以下条件可能适用于特定的实现[System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem):</span><span class="sxs-lookup"><span data-stu-id="a2b8a-245">The following conditions may apply to your implementation of [System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem):</span></span>

- <span data-ttu-id="a2b8a-246">[System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem)方法应执行不区分大小写比较的字符串中传入`type`参数。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-246">The [System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) method should perform a case-insensitive comparison of the string passed in the `type` parameter.</span></span> <span data-ttu-id="a2b8a-247">它还应允许至少不明确的匹配项。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-247">It should also allow for least ambiguous matches.</span></span> <span data-ttu-id="a2b8a-248">例如，对于类型"文件"和"directory"中，只将第一个字母被需要消除歧义。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-248">For example, for the types "file" and "directory", only the first letter is required to disambiguate.</span></span> <span data-ttu-id="a2b8a-249">如果`type`参数指示的类型不能创建您的提供程序，请[System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem)方法应编写一条消息与 ArgumentException指示类型可以创建提供程序。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-249">If the `type` parameter indicates a type your provider cannot create, the [System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) method should write an ArgumentException with a message indicating the types the provider can create.</span></span>

- <span data-ttu-id="a2b8a-250">有关`newItemValue`参数，请实现[System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem)方法，建议接受最小值的字符串。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-250">For the `newItemValue` parameter, the implementation of the [System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) method is recommended to accept strings at a minimum.</span></span> <span data-ttu-id="a2b8a-251">它还应接受将检索的对象的类型[System.Management.Automation.Provider.Itemcmdletprovider.Getitem\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem)相同路径的方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-251">It should also accept the type of object that is retrieved by the [System.Management.Automation.Provider.Itemcmdletprovider.Getitem\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) method for the same path.</span></span> <span data-ttu-id="a2b8a-252">[System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem)方法可以使用[System.Management.Automation.Languageprimitives.Convertto\*](/dotnet/api/System.Management.Automation.LanguagePrimitives.ConvertTo)方法来转换到类型所需的类型。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-252">The [System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) method can use the [System.Management.Automation.Languageprimitives.Convertto\*](/dotnet/api/System.Management.Automation.LanguagePrimitives.ConvertTo) method to convert types to the desired type.</span></span>

- <span data-ttu-id="a2b8a-253">实现[System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem)方法应调用[System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) ，并向数据存储区进行任何更改之前检查它的返回值。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-253">Your implementation of the [System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) method should call [System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) and check its return value before making any changes to the data store.</span></span> <span data-ttu-id="a2b8a-254">在调用[System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) ，则返回 true， [System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem)方法应调用[System.Management.Automation.Provider.Cmdletprovider.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue)具有潜在危险的系统修改作为额外检查方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-254">After the call to [System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) returns true, the [System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) method should call the [System.Management.Automation.Provider.Cmdletprovider.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) method as an additional check for potentially dangerous system modifications.</span></span>

## <a name="attaching-dynamic-parameters-to-the-new-item-cmdlet"></a><span data-ttu-id="a2b8a-255">附加到新项 Cmdlet 的动态参数</span><span class="sxs-lookup"><span data-stu-id="a2b8a-255">Attaching Dynamic Parameters to the New-Item Cmdlet</span></span>

<span data-ttu-id="a2b8a-256">有时`New-Item`cmdlet 需要在运行时动态指定的其他参数。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-256">Sometimes the `New-Item` cmdlet requires additional parameters that are specified dynamically at runtime.</span></span> <span data-ttu-id="a2b8a-257">若要提供这些动态参数，容器提供程序必须实现[System.Management.Automation.Provider.Containercmdletprovider.Newitemdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItemDynamicParameters)方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-257">To provide these dynamic parameters, the container provider must implement the [System.Management.Automation.Provider.Containercmdletprovider.Newitemdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItemDynamicParameters) method.</span></span> <span data-ttu-id="a2b8a-258">此方法检索指定的路径处的项的参数并返回具有属性和字段与分析属性类似于 cmdlet 类的对象或[System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary)对象。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-258">This method retrieves the parameters for the item at the indicated path and returns an object that has properties and fields with parsing attributes similar to a cmdlet class or a [System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) object.</span></span> <span data-ttu-id="a2b8a-259">Windows PowerShell 运行时使用返回的对象添加到参数`New-Item`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-259">The Windows PowerShell runtime uses the returned object to add the parameters to the `New-Item` cmdlet.</span></span>

<span data-ttu-id="a2b8a-260">此提供程序未实现此方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-260">This provider does not implement this method.</span></span> <span data-ttu-id="a2b8a-261">但是，以下代码是此方法的默认实现。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-261">However, the following code is the default implementation of this method.</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidernewitemdynamicparameters](Msh_samplestestcmdlets#testprovidernewitemdynamicparameters)]  -->

## <a name="removing-items"></a><span data-ttu-id="a2b8a-262">删除项</span><span class="sxs-lookup"><span data-stu-id="a2b8a-262">Removing Items</span></span>

<span data-ttu-id="a2b8a-263">若要删除的项，Windows PowerShell 提供程序必须重写[System.Management.Automation.Provider.Containercmdletprovider.Removeitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem)方法，以支持来自调用`Remove-Item`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-263">To remove items, the Windows PowerShell provider must override the [System.Management.Automation.Provider.Containercmdletprovider.Removeitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem) method to support calls from the `Remove-Item` cmdlet.</span></span> <span data-ttu-id="a2b8a-264">此方法从指定的路径的数据存储区中删除的项。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-264">This method deletes an item from the data store at the specified path.</span></span> <span data-ttu-id="a2b8a-265">如果`recurse`的参数`Remove-Item`cmdlet 设置为`true`，方法将移除所有子项目，而不考虑其级别。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-265">If the `recurse` parameter of the `Remove-Item` cmdlet is set to `true`, the method removes all child items regardless of their level.</span></span> <span data-ttu-id="a2b8a-266">如果该参数设置为`false`，方法将移除单个项在指定的路径。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-266">If the parameter is set to `false`, the method removes only a single item at the specified path.</span></span>

<span data-ttu-id="a2b8a-267">此提供程序不支持删除项。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-267">This provider does not support item removal.</span></span> <span data-ttu-id="a2b8a-268">但是，下面的代码是的默认实现[System.Management.Automation.Provider.Containercmdletprovider.Removeitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem)。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-268">However, the following code is the default implementation of [System.Management.Automation.Provider.Containercmdletprovider.Removeitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem).</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testproviderremoveitem](Msh_samplestestcmdlets#testproviderremoveitem)]  -->

#### <a name="things-to-remember-about-implementing-removeitem"></a><span data-ttu-id="a2b8a-269">要实现 RemoveItem 记住的事项</span><span class="sxs-lookup"><span data-stu-id="a2b8a-269">Things to Remember About Implementing RemoveItem</span></span>

<span data-ttu-id="a2b8a-270">以下条件可能适用于特定的实现[System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem):</span><span class="sxs-lookup"><span data-stu-id="a2b8a-270">The following conditions may apply to your implementation of [System.Management.Automation.Provider.Containercmdletprovider.Newitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem):</span></span>

- <span data-ttu-id="a2b8a-271">在定义的提供程序类时，Windows PowerShell 容器提供程序可能会从声明提供程序功能 ExpandWildcards、 筛选器、 包括或排除， [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities)枚举。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-271">When defining the provider class, a Windows PowerShell container provider might declare provider capabilities of ExpandWildcards, Filter, Include, or Exclude, from the [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumeration.</span></span> <span data-ttu-id="a2b8a-272">在这些情况下，实现[System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems)方法需要确保传递给方法的路径满足指定的要求功能。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-272">In these cases, the implementation of the [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) method needs to ensure that the path passed to the method meets the requirements of the specified capabilities.</span></span> <span data-ttu-id="a2b8a-273">若要执行此操作，该方法应访问相应的属性，例如，则[System.Management.Automation.Provider.Cmdletprovider.Exclude\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude)和[System.Management.Automation.Provider.Cmdletprovider.Include\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include)属性。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-273">To do this, the method should access the appropriate property, for example, the [System.Management.Automation.Provider.Cmdletprovider.Exclude\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) and [System.Management.Automation.Provider.Cmdletprovider.Include\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) properties.</span></span>

- <span data-ttu-id="a2b8a-274">默认情况下，重写此方法不应删除对象除非[System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force)属性设置为 true。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-274">By default, overrides of this method should not remove objects unless the [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) property is set to true.</span></span> <span data-ttu-id="a2b8a-275">如果指定的路径指示容器[System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force)属性不是必需。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-275">If the specified path indicates a container, the [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) property is not required.</span></span>

- <span data-ttu-id="a2b8a-276">实现[System.Management.Automation.Provider.Containercmdletprovider.Removeitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem)负责有循环的链接，以及类似时防止无限递归。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-276">Your implementation of [System.Management.Automation.Provider.Containercmdletprovider.Removeitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem) is responsible for preventing infinite recursion when there are circular links, and the like.</span></span> <span data-ttu-id="a2b8a-277">应引发相应的终止异常，以反映此类情况。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-277">An appropriate terminating exception should be thrown to reflect such a condition.</span></span>

- <span data-ttu-id="a2b8a-278">实现[System.Management.Automation.Provider.Containercmdletprovider.Removeitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem)方法应调用[System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) ，并向数据存储区进行任何更改之前检查它的返回值。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-278">Your implementation of the [System.Management.Automation.Provider.Containercmdletprovider.Removeitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem) method should call [System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) and check its return value before making any changes to the data store.</span></span> <span data-ttu-id="a2b8a-279">在调用[System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess)返回`true`，则[System.Management.Automation.Provider.Containercmdletprovider.Removeitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem)方法应调用[System.Management.Automation.Provider.Cmdletprovider.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue)具有潜在危险的系统修改作为额外检查方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-279">After the call to [System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) returns `true`, the [System.Management.Automation.Provider.Containercmdletprovider.Removeitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem) method should call the [System.Management.Automation.Provider.Cmdletprovider.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) method as an additional check for potentially dangerous system modifications.</span></span>

## <a name="attaching-dynamic-parameters-to-the-remove-item-cmdlet"></a><span data-ttu-id="a2b8a-280">附加到 Remove-item Cmdlet 的动态参数</span><span class="sxs-lookup"><span data-stu-id="a2b8a-280">Attaching Dynamic Parameters to the Remove-Item Cmdlet</span></span>

<span data-ttu-id="a2b8a-281">有时`Remove-Item`cmdlet 需要在运行时动态指定的其他参数。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-281">Sometimes the `Remove-Item` cmdlet requires additional parameters that are specified dynamically at runtime.</span></span> <span data-ttu-id="a2b8a-282">若要提供这些动态参数，容器提供程序必须实现[System.Management.Automation.Provider.Containercmdletprovider.Removeitemdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItemDynamicParameters)方法来处理这些参数。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-282">To provide these dynamic parameters, the container provider must implement the [System.Management.Automation.Provider.Containercmdletprovider.Removeitemdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItemDynamicParameters) method to handle these parameters.</span></span> <span data-ttu-id="a2b8a-283">此方法检索指定的路径处的项的动态参数并返回具有属性和字段与分析属性类似于 cmdlet 类的对象或[System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary)对象。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-283">This method retrieves the dynamic parameters for the item at the indicated path and returns an object that has properties and fields with parsing attributes similar to a cmdlet class or a [System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) object.</span></span> <span data-ttu-id="a2b8a-284">Windows PowerShell 运行时使用返回的对象添加到参数`Remove-Item`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-284">The Windows PowerShell runtime uses the returned object to add the parameters to the `Remove-Item` cmdlet.</span></span>

<span data-ttu-id="a2b8a-285">此容器提供程序未实现此方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-285">This container provider does not implement this method.</span></span> <span data-ttu-id="a2b8a-286">但是，下面的代码是的默认实现[System.Management.Automation.Provider.Containercmdletprovider.Removeitemdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItemDynamicParameters)。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-286">However, the following code is the default implementation of [System.Management.Automation.Provider.Containercmdletprovider.Removeitemdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItemDynamicParameters).</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testproviderremoveitemdynamicparameters](Msh_samplestestcmdlets#testproviderremoveitemdynamicparameters)]  -->

## <a name="querying-for-child-items"></a><span data-ttu-id="a2b8a-287">查询子项目</span><span class="sxs-lookup"><span data-stu-id="a2b8a-287">Querying for Child Items</span></span>

<span data-ttu-id="a2b8a-288">若要检查的指定路径处是否存在子项目，Windows PowerShell 容器提供程序必须重写[System.Management.Automation.Provider.Containercmdletprovider.Haschilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.HasChildItems)方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-288">To check to see if child items exist at the specified path, the Windows PowerShell container provider must override the [System.Management.Automation.Provider.Containercmdletprovider.Haschilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.HasChildItems) method.</span></span> <span data-ttu-id="a2b8a-289">此方法返回`true`的项具有子项，如果和`false`否则为。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-289">This method returns `true` if the item has children, and `false` otherwise.</span></span> <span data-ttu-id="a2b8a-290">为 null 或为空路径，该方法会考虑要为子级的数据存储区中的任何项，并返回`true`。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-290">For a null or empty path, the method considers any items in the data store to be children and returns `true`.</span></span>

<span data-ttu-id="a2b8a-291">下面是用于重写[System.Management.Automation.Provider.Containercmdletprovider.Haschilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.HasChildItems)方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-291">Here is the override for the [System.Management.Automation.Provider.Containercmdletprovider.Haschilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.HasChildItems) method.</span></span> <span data-ttu-id="a2b8a-292">如果有两个路径部分 ChunkPath 帮助器方法创建的该方法返回`false`，因为定义数据库容器和表容器。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-292">If there are more than two path parts created by the ChunkPath helper method, the method returns `false`, since only a database container and a table container are defined.</span></span> <span data-ttu-id="a2b8a-293">有关此帮助器方法的详细信息，请参阅 ChunkPath 方法详见[创建 Windows PowerShell 项提供程序](./creating-a-windows-powershell-item-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-293">For more information about this helper method, see the ChunkPath method is discussed in [Creating a Windows PowerShell Item Provider](./creating-a-windows-powershell-item-provider.md).</span></span>

```csharp
protected override bool HasChildItems( string path )
{
    return false;
} // HasChildItems
```

[!code-csharp[AccessDBProviderSample04.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample04/AccessDBProviderSample04.cs#L1094-L1097 "AccessDBProviderSample04.cs")]

#### <a name="things-to-remember-about-implementing-haschilditems"></a><span data-ttu-id="a2b8a-294">要实现 HasChildItems 记住的事项</span><span class="sxs-lookup"><span data-stu-id="a2b8a-294">Things to Remember About Implementing HasChildItems</span></span>

<span data-ttu-id="a2b8a-295">以下条件可能适用于特定的实现[System.Management.Automation.Provider.Containercmdletprovider.Haschilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.HasChildItems):</span><span class="sxs-lookup"><span data-stu-id="a2b8a-295">The following conditions may apply to your implementation of [System.Management.Automation.Provider.Containercmdletprovider.Haschilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.HasChildItems):</span></span>

- <span data-ttu-id="a2b8a-296">如果容器提供程序公开的根包含有趣装入点的实现[System.Management.Automation.Provider.Containercmdletprovider.Haschilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.HasChildItems)方法应返回`true`为 null 或空字符串传递时中的路径。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-296">If the container provider exposes a root that contains interesting mount points, the implementation of the [System.Management.Automation.Provider.Containercmdletprovider.Haschilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.HasChildItems) method should return `true` when a null or an empty string is passed in for the path.</span></span>

## <a name="copying-items"></a><span data-ttu-id="a2b8a-297">复制项</span><span class="sxs-lookup"><span data-stu-id="a2b8a-297">Copying Items</span></span>

<span data-ttu-id="a2b8a-298">若要复制的项，容器提供程序必须实现[System.Management.Automation.Provider.Containercmdletprovider.Copyitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem)方法，以支持来自调用`Copy-Item`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-298">To copy items, the container provider must implement the [System.Management.Automation.Provider.Containercmdletprovider.Copyitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) method to support calls from the `Copy-Item` cmdlet.</span></span> <span data-ttu-id="a2b8a-299">此方法将从所指示的位置中复制的数据项`path`到所指示的位置 cmdlet 参数`copyPath`参数。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-299">This method copies a data item from the location indicated by the `path` parameter of the cmdlet to the location indicated by the `copyPath` parameter.</span></span> <span data-ttu-id="a2b8a-300">如果`recurse`指定参数，该方法将复制所有子容器。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-300">If the `recurse` parameter is specified, the method copies all sub-containers.</span></span> <span data-ttu-id="a2b8a-301">如果未指定参数，该方法将复制单个级别的项。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-301">If the parameter is not specified, the method copies only a single level of items.</span></span>

<span data-ttu-id="a2b8a-302">此提供程序未实现此方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-302">This provider does not implement this method.</span></span> <span data-ttu-id="a2b8a-303">但是，下面的代码是的默认实现[System.Management.Automation.Provider.Containercmdletprovider.Copyitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem)。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-303">However, the following code is the default implementation of [System.Management.Automation.Provider.Containercmdletprovider.Copyitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem).</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidercopyitem](Msh_samplestestcmdlets#testprovidercopyitem)]  -->

#### <a name="things-to-remember-about-implementing-copyitem"></a><span data-ttu-id="a2b8a-304">要实现 CopyItem 记住的事项</span><span class="sxs-lookup"><span data-stu-id="a2b8a-304">Things to Remember About Implementing CopyItem</span></span>

<span data-ttu-id="a2b8a-305">以下条件可能适用于特定的实现[System.Management.Automation.Provider.Containercmdletprovider.Copyitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem):</span><span class="sxs-lookup"><span data-stu-id="a2b8a-305">The following conditions may apply to your implementation of [System.Management.Automation.Provider.Containercmdletprovider.Copyitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem):</span></span>

- <span data-ttu-id="a2b8a-306">在定义的提供程序类时，Windows PowerShell 容器提供程序可能会从声明提供程序功能 ExpandWildcards、 筛选器、 包括或排除， [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities)枚举。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-306">When defining the provider class, a Windows PowerShell container provider might declare provider capabilities of ExpandWildcards, Filter, Include, or Exclude, from the [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumeration.</span></span> <span data-ttu-id="a2b8a-307">在这些情况下，实现[System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems)方法需要确保传递给方法的路径满足指定的要求功能。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-307">In these cases, the implementation of the [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) method needs to ensure that the path passed to the method meets the requirements of the specified capabilities.</span></span> <span data-ttu-id="a2b8a-308">若要执行此操作，该方法应访问相应的属性，例如，则[System.Management.Automation.Provider.Cmdletprovider.Exclude\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude)和[System.Management.Automation.Provider.Cmdletprovider.Include\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include)属性。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-308">To do this, the method should access the appropriate property, for example, the [System.Management.Automation.Provider.Cmdletprovider.Exclude\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) and [System.Management.Automation.Provider.Cmdletprovider.Include\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) properties.</span></span>

- <span data-ttu-id="a2b8a-309">默认情况下，重写此方法不应将复制对象对现有对象除非[System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force)属性设置为`true`。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-309">By default, overrides of this method should not copy objects over existing objects unless the [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) property is set to `true`.</span></span> <span data-ttu-id="a2b8a-310">例如，FileSystem 提供程序不会将复制 c:\temp\abc.txt 通过现有 c:\abc.txt 文件除非[System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force)属性设置为`true`。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-310">For example, the FileSystem provider will not copy c:\temp\abc.txt over an existing c:\abc.txt file unless the [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) property is set to `true`.</span></span> <span data-ttu-id="a2b8a-311">如果在指定的路径`copyPath`参数存在，并指示容器[System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force)属性不是必需。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-311">If the path specified in the `copyPath` parameter exists and indicates a container, the [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) property is not required.</span></span> <span data-ttu-id="a2b8a-312">在这种情况下， [System.Management.Automation.Provider.Containercmdletprovider.Copyitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem)应将复制所指示的项`path`到容器参数为由`copyPath`作为子参数。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-312">In this case, [System.Management.Automation.Provider.Containercmdletprovider.Copyitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) should copy the item indicated by the `path` parameter to the container indicated by the `copyPath` parameter as a child.</span></span>

- <span data-ttu-id="a2b8a-313">实现[System.Management.Automation.Provider.Containercmdletprovider.Copyitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem)负责有循环的链接，以及类似时防止无限递归。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-313">Your implementation of [System.Management.Automation.Provider.Containercmdletprovider.Copyitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) is responsible for preventing infinite recursion when there are circular links, and the like.</span></span> <span data-ttu-id="a2b8a-314">应引发相应的终止异常，以反映此类情况。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-314">An appropriate terminating exception should be thrown to reflect such a condition.</span></span>

- <span data-ttu-id="a2b8a-315">实现[System.Management.Automation.Provider.Containercmdletprovider.Copyitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem)方法应调用[System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) ，并向数据存储区进行任何更改之前检查它的返回值。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-315">Your implementation of the [System.Management.Automation.Provider.Containercmdletprovider.Copyitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) method should call [System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) and check its return value before making any changes to the data store.</span></span> <span data-ttu-id="a2b8a-316">在调用[System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) ，则返回 true， [System.Management.Automation.Provider.Containercmdletprovider.Copyitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem)方法应调用[System.Management.Automation.Provider.Cmdletprovider.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue)具有潜在危险的系统修改作为额外检查方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-316">After the call to [System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) returns true, the [System.Management.Automation.Provider.Containercmdletprovider.Copyitem\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) method should call the [System.Management.Automation.Provider.Cmdletprovider.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) method as an additional check for potentially dangerous system modifications.</span></span> <span data-ttu-id="a2b8a-317">有关调用这些方法的详细信息，请参阅[重命名项](#Renaming-Items)。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-317">For more information about calling these methods, see [Rename Items](#Renaming-Items).</span></span>

## <a name="attaching-dynamic-parameters-to-the-copy-item-cmdlet"></a><span data-ttu-id="a2b8a-318">附加到 Copy-item Cmdlet 的动态参数</span><span class="sxs-lookup"><span data-stu-id="a2b8a-318">Attaching Dynamic Parameters to the Copy-Item Cmdlet</span></span>

<span data-ttu-id="a2b8a-319">有时`Copy-Item`cmdlet 需要在运行时动态指定的其他参数。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-319">Sometimes the `Copy-Item` cmdlet requires additional parameters that are specified dynamically at runtime.</span></span> <span data-ttu-id="a2b8a-320">若要提供这些动态参数，Windows PowerShell 容器提供程序必须实现[System.Management.Automation.Provider.Containercmdletprovider.Copyitemdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItemDynamicParameters)方法来处理这些参数。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-320">To provide these dynamic parameters, the Windows PowerShell container provider must implement the [System.Management.Automation.Provider.Containercmdletprovider.Copyitemdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItemDynamicParameters) method to handle these parameters.</span></span> <span data-ttu-id="a2b8a-321">此方法检索指定的路径处的项的参数并返回具有属性和字段与分析属性类似于 cmdlet 类的对象或[System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary)对象。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-321">This method retrieves the parameters for the item at the indicated path and returns an object that has properties and fields with parsing attributes similar to a cmdlet class or a [System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) object.</span></span> <span data-ttu-id="a2b8a-322">Windows PowerShell 运行时使用返回的对象添加到参数`Copy-Item`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-322">The Windows PowerShell runtime uses the returned object to add the parameters to the `Copy-Item` cmdlet.</span></span>

<span data-ttu-id="a2b8a-323">此提供程序未实现此方法。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-323">This provider does not implement this method.</span></span> <span data-ttu-id="a2b8a-324">但是，下面的代码是的默认实现[System.Management.Automation.Provider.Containercmdletprovider.Copyitemdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItemDynamicParameters)。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-324">However, the following code is the default implementation of [System.Management.Automation.Provider.Containercmdletprovider.Copyitemdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItemDynamicParameters).</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidercopyitemdynamicparameters](Msh_samplestestcmdlets#testprovidercopyitemdynamicparameters)]  -->

## <a name="code-sample"></a><span data-ttu-id="a2b8a-325">代码示例</span><span class="sxs-lookup"><span data-stu-id="a2b8a-325">Code Sample</span></span>

<span data-ttu-id="a2b8a-326">有关完整的示例代码，请参阅[AccessDbProviderSample04 代码示例](./accessdbprovidersample04-code-sample.md)。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-326">For complete sample code, see [AccessDbProviderSample04 Code Sample](./accessdbprovidersample04-code-sample.md).</span></span>

## <a name="building-the-windows-powershell-provider"></a><span data-ttu-id="a2b8a-327">生成 Windows PowerShell 提供程序</span><span class="sxs-lookup"><span data-stu-id="a2b8a-327">Building the Windows PowerShell Provider</span></span>

<span data-ttu-id="a2b8a-328">请参阅[如何注册 Cmdlet、 提供程序，和托管应用程序](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-328">See [How to Register Cmdlets, Providers, and Host Applications](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).</span></span>
<span data-ttu-id="a2b8a-329">请参阅[如何注册 Cmdlet、 提供程序，和托管应用程序](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-329">See [How to Register Cmdlets, Providers, and Host Applications](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).</span></span>

## <a name="testing-the-windows-powershell-provider"></a><span data-ttu-id="a2b8a-330">测试 Windows PowerShell 提供程序</span><span class="sxs-lookup"><span data-stu-id="a2b8a-330">Testing the Windows PowerShell Provider</span></span>

<span data-ttu-id="a2b8a-331">Windows PowerShell 提供程序具有已注册到 Windows PowerShell，可以通过在命令行上运行的受支持的 cmdlet 来测试它。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-331">When your Windows PowerShell provider has been registered with Windows PowerShell, you can test it by running the supported cmdlets on the command line.</span></span> <span data-ttu-id="a2b8a-332">请注意下面的示例输出使用虚构的 Access 数据库。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-332">Be aware that the following example output uses a fictitious Access database.</span></span>

1. <span data-ttu-id="a2b8a-333">运行`Get-ChildItem`cmdlet 从 Access 数据库中的客户表中检索子项目的列表。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-333">Run the `Get-ChildItem` cmdlet to retrieve the list of child items from a Customers table in the Access database.</span></span>

   ```powershell
   Get-ChildItem mydb:customers
   ```

   <span data-ttu-id="a2b8a-334">将显示以下输出。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-334">The following output appears.</span></span>

   ```output
   PSPath        : AccessDB::customers
   PSDrive       : mydb
   PSProvider    : System.Management.Automation.ProviderInfo
   PSIsContainer : True
   Data          : System.Data.DataRow
   Name          : Customers
   RowCount      : 91
   Columns       :
   ```

2. <span data-ttu-id="a2b8a-335">运行`Get-ChildItem`cmdlet 再次检索表中的数据。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-335">Run the `Get-ChildItem` cmdlet again to retrieve the data of a table.</span></span>

   ```powershell
   (Get-ChildItem mydb:customers).data
   ```

   <span data-ttu-id="a2b8a-336">将显示以下输出。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-336">The following output appears.</span></span>

   ```output
   TABLE_CAT   : c:\PS\northwind
   TABLE_SCHEM :
   TABLE_NAME  : Customers
   TABLE_TYPE  : TABLE
   REMARKS     :
   ```

3. <span data-ttu-id="a2b8a-337">现在，使用`Get-Item`cmdlet 来检索数据的表中的第 0 行处的项。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-337">Now use the `Get-Item` cmdlet to retrieve the items at row 0 in the data table.</span></span>

   ```powershell
   Get-Item mydb:\customers\0
   ```

   <span data-ttu-id="a2b8a-338">将显示以下输出。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-338">The following output appears.</span></span>

   ```output
   PSPath        : AccessDB::customers\0
   PSDrive       : mydb
   PSProvider    : System.Management.Automation.ProviderInfo
   PSIsContainer : False
   Data          : System.Data.DataRow
   RowNumber     : 0
   ```

4. <span data-ttu-id="a2b8a-339">重复使用`Get-Item`若要检索的数据的第 0 行中的项。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-339">Reuse `Get-Item` to retrieve the data for the items in row 0.</span></span>

   ```powershell
   (Get-Item mydb:\customers\0).data
   ```

   <span data-ttu-id="a2b8a-340">将显示以下输出。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-340">The following output appears.</span></span>

   ```output
   CustomerID   : 1234
   CompanyName  : Fabrikam
   ContactName  : Eric Gruber
   ContactTitle : President
   Address      : 4567 Main Street
   City         : Buffalo
   Region       : NY
   PostalCode   : 98052
   Country      : USA
   Phone        : (425) 555-0100
   Fax          : (425) 555-0101
   ```

5. <span data-ttu-id="a2b8a-341">现在，使用`New-Item`cmdlet 将行添加到现有表。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-341">Now use the `New-Item` cmdlet to add a row to an existing table.</span></span> <span data-ttu-id="a2b8a-342">`Path`参数指定行的完整路径，并且必须指明行数大于现有表中的行数。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-342">The `Path` parameter specifies the full path to the row, and must indicate a row number that is greater than the existing number of rows in the table.</span></span> <span data-ttu-id="a2b8a-343">`Type`参数指示"行"指定要添加的项的类型。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-343">The `Type` parameter indicates "row" to specify that type of item to add.</span></span> <span data-ttu-id="a2b8a-344">最后，`Value`参数指定的列的行的值以逗号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-344">Finally, the `Value` parameter specifies a comma-delimited list of column values for the row.</span></span>

   ```powershell
   New-Item -Path mydb:\Customers\3 -ItemType "row" -Value "3,CustomerFirstName,CustomerLastName,CustomerEmailAdress,CustomerTitle,CustomerCompany,CustomerPhone, CustomerAddress,CustomerCity,CustomerState,CustomerZip,CustomerCountry"
   ```

6. <span data-ttu-id="a2b8a-345">验证新项操作的正确性，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-345">Verify the correctness of the new item operation as follows.</span></span>

   ```none
   PS mydb:\> cd Customers
   PS mydb:\Customers> (Get-Item 3).data
   ```

   <span data-ttu-id="a2b8a-346">将显示以下输出。</span><span class="sxs-lookup"><span data-stu-id="a2b8a-346">The following output appears.</span></span>

   ```output
   ID        : 3
   FirstName : Eric
   LastName  : Gruber
   Email     : ericgruber@fabrikam.com
   Title     : President
   Company   : Fabrikam
   WorkPhone : (425) 555-0100
   Address   : 4567 Main Street
   City      : Buffalo
   State     : NY
   Zip       : 98052
   Country   : USA
   ```

## <a name="see-also"></a><span data-ttu-id="a2b8a-347">另请参阅</span><span class="sxs-lookup"><span data-stu-id="a2b8a-347">See Also</span></span>

[<span data-ttu-id="a2b8a-348">创建 Windows PowerShell 提供程序</span><span class="sxs-lookup"><span data-stu-id="a2b8a-348">Creating Windows PowerShell Providers</span></span>](./how-to-create-a-windows-powershell-provider.md)

[<span data-ttu-id="a2b8a-349">设计 Windows PowerShell 提供程序</span><span class="sxs-lookup"><span data-stu-id="a2b8a-349">Designing Your Windows PowerShell Provider</span></span>](./designing-your-windows-powershell-provider.md)

[<span data-ttu-id="a2b8a-350">实现项 Windows PowerShell 提供程序</span><span class="sxs-lookup"><span data-stu-id="a2b8a-350">Implementing an Item Windows PowerShell Provider</span></span>](./creating-a-windows-powershell-item-provider.md)

[<span data-ttu-id="a2b8a-351">实现导航 Windows PowerShell 提供程序</span><span class="sxs-lookup"><span data-stu-id="a2b8a-351">Implementing a Navigation Windows PowerShell Provider</span></span>](./creating-a-windows-powershell-navigation-provider.md)

[<span data-ttu-id="a2b8a-352">如何注册 Cmdlet、 提供程序，和托管应用程序</span><span class="sxs-lookup"><span data-stu-id="a2b8a-352">How to Register Cmdlets, Providers, and Host Applications</span></span>](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[<span data-ttu-id="a2b8a-353">如何注册 Cmdlet、 提供程序，和托管应用程序</span><span class="sxs-lookup"><span data-stu-id="a2b8a-353">How to Register Cmdlets, Providers, and Host Applications</span></span>](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[<span data-ttu-id="a2b8a-354">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="a2b8a-354">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)

[<span data-ttu-id="a2b8a-355">Windows PowerShell 程序员指南</span><span class="sxs-lookup"><span data-stu-id="a2b8a-355">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)