---
title: 创建 Windows PowerShell 内容提供程序
ms.date: 09/13/2016
ms.topic: article
ms.assetid: 3da88ff9-c4c7-4ace-aa24-0a29c8cfa060
ms.openlocfilehash: 149ddb5becf2e0237973e535323ddf8b03b86f24
ms.sourcegitcommit: 30ccbbb32915b551c4cd4c91ef1df96b5b7514c4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2020
ms.locfileid: "80500837"
---
# <a name="creating-a-windows-powershell-content-provider"></a><span data-ttu-id="5e2c5-102">创建 Windows PowerShell 内容提供程序</span><span class="sxs-lookup"><span data-stu-id="5e2c5-102">Creating a Windows PowerShell Content Provider</span></span>

<span data-ttu-id="5e2c5-103">本主题介绍如何创建 Windows PowerShell 提供程序，该提供程序使用户能够操作数据存储区中的项的内容。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-103">This topic describes how to create a Windows PowerShell provider that enables the user to manipulate the contents of the items in a data store.</span></span> <span data-ttu-id="5e2c5-104">因此，可操作项内容的提供程序称为 Windows PowerShell 内容提供程序。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-104">As a consequence, a provider that can manipulate the contents of items is referred to as a Windows PowerShell content provider.</span></span>

> [!NOTE]
> <span data-ttu-id="5e2c5-105">你可以使用适用C#于 windows Vista 的 Microsoft Windows 软件开发工具包和 .NET Framework 3.0 运行时组件下载此提供程序的源文件（AccessDBSampleProvider06.cs）。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-105">You can download the C# source file (AccessDBSampleProvider06.cs) for this provider using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="5e2c5-106">有关下载说明，请参阅[如何安装 Windows powershell 和下载 Windows POWERSHELL SDK](/powershell/scripting/developer/installing-the-windows-powershell-sdk)。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-106">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/scripting/developer/installing-the-windows-powershell-sdk).</span></span>
> <span data-ttu-id="5e2c5-107">下载的源文件在 **\<PowerShell 示例 >** 目录中提供。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-107">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span> <span data-ttu-id="5e2c5-108">有关其他 Windows PowerShell 提供程序实现的详细信息，请参阅[设计 Windows Powershell 提供程序](./designing-your-windows-powershell-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-108">For more information about other Windows PowerShell provider implementations, see [Designing Your Windows PowerShell Provider](./designing-your-windows-powershell-provider.md).</span></span>

## <a name="define-the-windows-powershell-content-provider-class"></a><span data-ttu-id="5e2c5-109">定义 Windows PowerShell 内容提供程序类</span><span class="sxs-lookup"><span data-stu-id="5e2c5-109">Define the Windows PowerShell Content Provider Class</span></span>

<span data-ttu-id="5e2c5-110">Windows PowerShell 内容提供程序必须创建一个支持[Icontentcmdletprovider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider)接口的 .net 类。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-110">A Windows PowerShell content provider must create a .NET class that supports the [System.Management.Automation.Provider.Icontentcmdletprovider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider) interface.</span></span> <span data-ttu-id="5e2c5-111">下面是本部分中所述的项提供程序的类定义。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-111">Here is the class definition for the item provider described in this section.</span></span>

[!code-csharp[AccessDBProviderSample06.cs](~/powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L32-L33 "AccessDBProviderSample06.cs")]

<span data-ttu-id="5e2c5-112">请注意，在此类定义中， [Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute)属性包括两个参数。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-112">Note that in this class definition, the [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) attribute includes two parameters.</span></span> <span data-ttu-id="5e2c5-113">第一个参数指定 Windows PowerShell 使用的提供程序的用户友好名称。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-113">The first parameter specifies a user-friendly name for the provider that is used by Windows PowerShell.</span></span> <span data-ttu-id="5e2c5-114">第二个参数指定 Windows PowerShell 特定功能，该功能是在命令处理过程中提供给 Windows PowerShell 运行时的。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-114">The second parameter specifies the Windows PowerShell specific capabilities that the provider exposes to the Windows PowerShell runtime during command processing.</span></span> <span data-ttu-id="5e2c5-115">对于此提供程序，没有添加 Windows PowerShell 特定功能。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-115">For this provider, there are no added Windows PowerShell specific capabilities.</span></span>

## <a name="define-functionality-of-base-class"></a><span data-ttu-id="5e2c5-116">定义基类的功能</span><span class="sxs-lookup"><span data-stu-id="5e2c5-116">Define Functionality of Base Class</span></span>

<span data-ttu-id="5e2c5-117">如[设计你的 Windows PowerShell 提供程序](./designing-your-windows-powershell-provider.md)中所述， [Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)类从提供不同提供程序功能的其他一些类派生。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-117">As described in [Design Your Windows PowerShell Provider](./designing-your-windows-powershell-provider.md), the [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) class derives from several other classes that provided different provider functionality.</span></span> <span data-ttu-id="5e2c5-118">因此，Windows PowerShell 内容提供程序通常定义这些类提供的所有功能。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-118">A Windows PowerShell content provider, therefore, typically defines all of the functionality provided by those classes.</span></span>

<span data-ttu-id="5e2c5-119">若要详细了解如何实现添加特定于会话的初始化信息以及释放提供程序所用资源的功能，请参阅[创建基本 Windows PowerShell 提供程序](./creating-a-basic-windows-powershell-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-119">For more information about how to implement functionality for adding session-specific initialization information and for releasing resources that are used by the provider, see [Creating a Basic Windows PowerShell Provider](./creating-a-basic-windows-powershell-provider.md).</span></span>
<span data-ttu-id="5e2c5-120">但是，大多数提供程序（包括此处所述的提供程序）都可以使用 Windows PowerShell 提供的此功能的默认实现。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-120">However, most providers, including the provider described here, can use the default implementation of this functionality that is provided by Windows PowerShell.</span></span>

<span data-ttu-id="5e2c5-121">若要访问数据存储区，该提供程序必须实现[Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider)基类的方法。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-121">To access the data store, the provider must implement the methods of the [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) base class.</span></span> <span data-ttu-id="5e2c5-122">有关实现这些方法的详细信息，请参阅[创建 Windows PowerShell 驱动器提供程序](./creating-a-windows-powershell-drive-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-122">For more information about implementing these methods, see [Creating a Windows PowerShell Drive Provider](./creating-a-windows-powershell-drive-provider.md).</span></span>

<span data-ttu-id="5e2c5-123">若要操作数据存储区的项（如获取、设置和清除项），提供程序必须实现[Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider)基类提供的方法。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-123">To manipulate the items of a data store, such as getting, setting, and clearing items, the provider must implement the methods provided by the [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) base class.</span></span> <span data-ttu-id="5e2c5-124">有关实现这些方法的详细信息，请参阅[创建 Windows PowerShell 项提供程序](./creating-a-windows-powershell-item-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-124">For more information about implementing these methods, see [Creating a Windows PowerShell Item Provider](./creating-a-windows-powershell-item-provider.md).</span></span>

<span data-ttu-id="5e2c5-125">若要处理多层数据存储区，提供程序必须实现[Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider)基类所提供的方法。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-125">To work on multi-layer data stores, the provider must implement the methods provided by the [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) base class.</span></span> <span data-ttu-id="5e2c5-126">有关实现这些方法的详细信息，请参阅[创建 Windows PowerShell 容器提供程序](./creating-a-windows-powershell-container-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-126">For more information about implementing these methods, see [Creating a Windows PowerShell Container Provider](./creating-a-windows-powershell-container-provider.md).</span></span>

<span data-ttu-id="5e2c5-127">若要支持递归命令、嵌套容器和相对路径，提供程序必须实现[Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)基类。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-127">To support recursive commands, nested containers, and relative paths, the provider must implement the [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) base class.</span></span> <span data-ttu-id="5e2c5-128">此外，此 Windows PowerShell 内容提供程序还可以将[Icontentcmdletprovider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider)接口附加到[Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)基类，因此必须实现该类提供的方法，这也是必需的。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-128">In addition, this Windows PowerShell content provider can attaches [System.Management.Automation.Provider.Icontentcmdletprovider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider) interface to the [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) base class, and must therefore implement the methods provided by that class.</span></span> <span data-ttu-id="5e2c5-129">有关详细信息，请参阅实现这些方法。请参阅[实现导航 Windows PowerShell 提供程序](./creating-a-windows-powershell-navigation-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-129">For more information, see implementing those methods, see [Implement a Navigation Windows PowerShell Provider](./creating-a-windows-powershell-navigation-provider.md).</span></span>

## <a name="implementing-a-content-reader"></a><span data-ttu-id="5e2c5-130">实现内容读取器</span><span class="sxs-lookup"><span data-stu-id="5e2c5-130">Implementing a Content Reader</span></span>

<span data-ttu-id="5e2c5-131">若要从项读取内容，提供程序必须实现从[Icontentreader](/dotnet/api/System.Management.Automation.Provider.IContentReader)派生的内容读取器类。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-131">To read content from an item, a provider must implements a content reader class that derives from [System.Management.Automation.Provider.Icontentreader](/dotnet/api/System.Management.Automation.Provider.IContentReader).</span></span>
<span data-ttu-id="5e2c5-132">此提供程序的内容读取器允许访问数据表中某行的内容。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-132">The content reader for this provider allows access to the contents of a row in a data table.</span></span> <span data-ttu-id="5e2c5-133">内容读取器类定义一个**读取**方法，该方法从指示的行中检索数据并返回一个表示该数据的列表、一个移动内容读取器的**查找**方法、一个关闭内容读取器的**关闭**方法以及一个**Dispose**方法。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-133">The content reader class defines a **Read** method that retrieves the data from the indicated row and returns a list representing that data, a **Seek** method that moves the content reader, a **Close** method that closes the content reader, and a **Dispose** method.</span></span>

[!code-csharp[AccessDBProviderSample06.cs](~/powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L2115-L2241
"AccessDBProviderSample06.cs")]

## <a name="implementing-a-content-writer"></a><span data-ttu-id="5e2c5-134">实现内容编写器</span><span class="sxs-lookup"><span data-stu-id="5e2c5-134">Implementing a Content Writer</span></span>

<span data-ttu-id="5e2c5-135">若要向项写入内容，提供程序必须实现从[Icontentwriter](/dotnet/api/System.Management.Automation.Provider.IContentWriter)派生的内容编写器类。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-135">To write content to an item, a provider must implement a content writer class derives from [System.Management.Automation.Provider.Icontentwriter](/dotnet/api/System.Management.Automation.Provider.IContentWriter).</span></span>
<span data-ttu-id="5e2c5-136">内容编写器类定义**写入**方法，该方法写入指定的行内容、移动内容编写器的**Seek**方法、关闭内容编写器的**关闭**方法以及**Dispose**方法。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-136">The content writer class defines a **Write** method that writes the specified row content, a **Seek** method that moves the content writer, a **Close** method that closes the content writer, and a **Dispose** method.</span></span>

[!code-csharp[AccessDBProviderSample06.cs](~/powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L2250-L2394 "AccessDBProviderSample06.cs")]

## <a name="retrieving-the-content-reader"></a><span data-ttu-id="5e2c5-137">检索内容读取器</span><span class="sxs-lookup"><span data-stu-id="5e2c5-137">Retrieving the Content Reader</span></span>

<span data-ttu-id="5e2c5-138">若要从项获取内容，提供程序必须实现[Icontentcmdletprovider. Getcontentreader \*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader)以支持 `Get-Content` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-138">To get content from an item, the provider must implement the [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreader\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader) to support the `Get-Content` cmdlet.</span></span> <span data-ttu-id="5e2c5-139">此方法返回位于指定路径处的项的内容读取器。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-139">This method returns the content reader for the item located at the specified path.</span></span> <span data-ttu-id="5e2c5-140">然后，可以打开读取器对象来读取内容。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-140">The reader object can then be opened to read the content.</span></span>

<span data-ttu-id="5e2c5-141">下面是此提供程序的此方法的[Icontentcmdletprovider. Getcontentreader \*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader)实现。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-141">Here is the implementation of [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreader\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader) for this method for this provider.</span></span>

```csharp
public IContentReader GetContentReader(string path)
{
    string tableName;
    int rowNumber;

    PathType type = GetNamesFromPath(path, out tableName, out rowNumber);

    if (type == PathType.Invalid)
    {
        ThrowTerminatingInvalidPathException(path);
    }
    else if (type == PathType.Row)
    {
        throw new InvalidOperationException("contents can be obtained only for tables");
    }

    return new AccessDBContentReader(path, this);
} // GetContentReader
```

[!code-csharp[AccessDBProviderSample06.cs](~/powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L1829-L1846 "AccessDBProviderSample06.cs")]

#### <a name="things-to-remember-about-implementing-getcontentreader"></a><span data-ttu-id="5e2c5-142">有关实现 GetContentReader 的注意事项</span><span class="sxs-lookup"><span data-stu-id="5e2c5-142">Things to Remember About Implementing GetContentReader</span></span>

<span data-ttu-id="5e2c5-143">以下条件可能适用于[Icontentcmdletprovider. Getcontentreader \*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader)的实现：。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-143">The following conditions may apply to an implementation of [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreader\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader):</span></span>

- <span data-ttu-id="5e2c5-144">定义提供程序类时，Windows PowerShell 内容提供程序可以声明 ExpandWildcards、Filter、Include 或 Exclude 的提供程序功能， [Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities)枚举。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-144">When defining the provider class, a Windows PowerShell content provider might declare provider capabilities of ExpandWildcards, Filter, Include, or Exclude, from the [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumeration.</span></span> <span data-ttu-id="5e2c5-145">在这些情况下， [Icontentcmdletprovider. Getcontentreader \*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader)方法的实现必须确保传递给该方法的路径满足指定功能的要求。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-145">In these cases, the implementation of the [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreader\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader) method must ensure that the path passed to the method meets the requirements of the specified capabilities.</span></span> <span data-ttu-id="5e2c5-146">若要执行此操作，方法应访问相应的属性，例如， [Cmdletprovider \*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude)和[Cmdletprovider \*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include)属性中的相应属性，例如 ""。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-146">To do this, the method should access the appropriate property, for example, the [System.Management.Automation.Provider.Cmdletprovider.Exclude\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) and [System.Management.Automation.Provider.Cmdletprovider.Include\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) properties.</span></span>

- <span data-ttu-id="5e2c5-147">默认情况下，此方法的重写不应检索用户隐藏的对象的读取器，除非[Cmdletprovider \*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force)属性设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-147">By default, overrides of this method should not retrieve a reader for objects that are hidden from the user unless the [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) property is set to `true`.</span></span> <span data-ttu-id="5e2c5-148">如果路径表示从用户和[Cmdletprovider \*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force)中隐藏的项被设置为 `false`，则应写入错误，则为。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-148">An error should be written if the path represents an item that is hidden from the user and [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) is set to `false`.</span></span>

## <a name="attaching-dynamic-parameters-to-the-get-content-cmdlet"></a><span data-ttu-id="5e2c5-149">将动态参数附加到获取内容 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="5e2c5-149">Attaching Dynamic Parameters to the Get-Content Cmdlet</span></span>

<span data-ttu-id="5e2c5-150">`Get-Content` cmdlet 可能需要在运行时动态指定的其他参数。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-150">The `Get-Content` cmdlet might require additional parameters that are specified dynamically at runtime.</span></span> <span data-ttu-id="5e2c5-151">为了提供这些动态参数，Windows PowerShell 内容提供程序必须实现[Icontentcmdletprovider. Getcontentreaderdynamicparameters \*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReaderDynamicParameters)方法。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-151">To provide these dynamic parameters, the Windows PowerShell content provider must implement the [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreaderdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReaderDynamicParameters) method.</span></span> <span data-ttu-id="5e2c5-152">此方法检索指定路径处的项的动态参数，并返回一个对象，该对象具有与 cmdlet 类或[Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary)对象类似的分析特性的属性和字段。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-152">This method retrieves dynamic parameters for the item at the indicated path and returns an object that has properties and fields with parsing attributes similar to a cmdlet class or a [System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) object.</span></span> <span data-ttu-id="5e2c5-153">Windows PowerShell 运行时使用返回的对象将参数添加到 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-153">The Windows PowerShell runtime uses the returned object to add the parameters to the cmdlet.</span></span>

<span data-ttu-id="5e2c5-154">此 Windows PowerShell 容器提供程序未实现此方法。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-154">This Windows PowerShell container provider does not implement this method.</span></span> <span data-ttu-id="5e2c5-155">但是，下面的代码是此方法的默认实现。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-155">However, the following code is the default implementation of this method.</span></span>

```csharp
public object GetContentReaderDynamicParameters(string path)
{
    return null;
}
```

[!code-csharp[AccessDBProviderSample06.cs](~/powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L1853-L1856 "AccessDBProviderSample06.cs")]

## <a name="retrieving-the-content-writer"></a><span data-ttu-id="5e2c5-156">检索内容编写器</span><span class="sxs-lookup"><span data-stu-id="5e2c5-156">Retrieving the Content Writer</span></span>

<span data-ttu-id="5e2c5-157">若要向项写入内容，提供程序必须实现[Icontentcmdletprovider. Getcontentwriter \*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriter)以支持 `Set-Content` 和 `Add-Content` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-157">To write content to an item, the provider must implement the [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentwriter\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriter) to support the `Set-Content` and `Add-Content` cmdlets.</span></span> <span data-ttu-id="5e2c5-158">此方法返回位于指定路径处的项的内容编写器。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-158">This method returns the content writer for the item located at the specified path.</span></span>

<span data-ttu-id="5e2c5-159">下面是此方法的[Icontentcmdletprovider. Getcontentwriter \*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriter)的实现方法。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-159">Here is the implementation of [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentwriter\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriter) for this method.</span></span>

```csharp
public IContentWriter GetContentWriter(string path)
{
    string tableName;
    int rowNumber;

    PathType type = GetNamesFromPath(path, out tableName, out rowNumber);

    if (type == PathType.Invalid)
    {
        ThrowTerminatingInvalidPathException(path);
    }
    else if (type == PathType.Row)
    {
        throw new InvalidOperationException("contents can be added only to tables");
    }

    return new AccessDBContentWriter(path, this);
}
```

[!code-csharp[AccessDBProviderSample06.cs](~/powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L1863-L1880 "AccessDBProviderSample06.cs")]

#### <a name="things-to-remember-about-implementing-getcontentwriter"></a><span data-ttu-id="5e2c5-160">有关实现 GetContentWriter 的注意事项</span><span class="sxs-lookup"><span data-stu-id="5e2c5-160">Things to Remember About Implementing GetContentWriter</span></span>

<span data-ttu-id="5e2c5-161">以下情况可能适用于你的[Icontentcmdletprovider. Getcontentwriter \*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriter)实现：</span><span class="sxs-lookup"><span data-stu-id="5e2c5-161">The following conditions may apply to your implementation of [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentwriter\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriter):</span></span>

- <span data-ttu-id="5e2c5-162">定义提供程序类时，Windows PowerShell 内容提供程序可以声明 ExpandWildcards、Filter、Include 或 Exclude 的提供程序功能， [Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities)枚举。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-162">When defining the provider class, a Windows PowerShell content provider might declare provider capabilities of ExpandWildcards, Filter, Include, or Exclude, from the [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumeration.</span></span> <span data-ttu-id="5e2c5-163">在这些情况下， [Icontentcmdletprovider. Getcontentwriter \*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriter)方法的实现必须确保传递给该方法的路径满足指定功能的要求。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-163">In these cases, the implementation of the [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentwriter\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriter) method must ensure that the path passed to the method meets the requirements of the specified capabilities.</span></span> <span data-ttu-id="5e2c5-164">若要执行此操作，方法应访问相应的属性，例如， [Cmdletprovider \*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude)和[Cmdletprovider \*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include)属性中的相应属性，例如 ""。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-164">To do this, the method should access the appropriate property, for example, the [System.Management.Automation.Provider.Cmdletprovider.Exclude\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) and [System.Management.Automation.Provider.Cmdletprovider.Include\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) properties.</span></span>

- <span data-ttu-id="5e2c5-165">默认情况下，此方法的重写不应检索用户隐藏的对象的编写器，除非[Cmdletprovider \*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force)属性设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-165">By default, overrides of this method should not retrieve a writer for objects that are hidden from the user unless the [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) property is set to `true`.</span></span> <span data-ttu-id="5e2c5-166">如果路径表示从用户和[Cmdletprovider \*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force)中隐藏的项被设置为 `false`，则应写入错误，则为。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-166">An error should be written if the path represents an item that is hidden from the user and [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) is set to `false`.</span></span>

## <a name="attaching-dynamic-parameters-to-the-add-content-and-set-content-cmdlets"></a><span data-ttu-id="5e2c5-167">将动态参数附加到添加内容和集内容 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="5e2c5-167">Attaching Dynamic Parameters to the Add-Content and Set-Content Cmdlets</span></span>

<span data-ttu-id="5e2c5-168">`Add-Content` 和 `Set-Content` cmdlet 可能需要添加了运行时的其他动态参数。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-168">The `Add-Content` and `Set-Content` cmdlets might require additional dynamic parameters that are added a runtime.</span></span> <span data-ttu-id="5e2c5-169">为了提供这些动态参数，Windows PowerShell 内容提供程序必须实现[Icontentcmdletprovider. Getcontentwriterdynamicparameters \*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriterDynamicParameters)方法来处理这些参数。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-169">To provide these dynamic parameters, the Windows PowerShell content provider must implement the [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentwriterdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriterDynamicParameters) method to handle these parameters.</span></span> <span data-ttu-id="5e2c5-170">此方法检索指定路径处的项的动态参数，并返回一个对象，该对象具有与 cmdlet 类或[Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary)对象类似的分析特性的属性和字段。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-170">This method retrieves dynamic parameters for the item at the indicated path and returns an object that has properties and fields with parsing attributes similar to a cmdlet class or a [System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) object.</span></span> <span data-ttu-id="5e2c5-171">Windows PowerShell 运行时使用返回的对象将参数添加到 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-171">The Windows PowerShell runtime uses the returned object to add the parameters to the cmdlets.</span></span>

<span data-ttu-id="5e2c5-172">此 Windows PowerShell 容器提供程序未实现此方法。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-172">This Windows PowerShell container provider does not implement this method.</span></span> <span data-ttu-id="5e2c5-173">但是，下面的代码是此方法的默认实现。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-173">However, the following code is the default implementation of this method.</span></span>

[!code-csharp[AccessDBProviderSample06.cs](~/powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L1887-L1890 "AccessDBProviderSample06.cs")]

## <a name="clearing-content"></a><span data-ttu-id="5e2c5-174">清除内容</span><span class="sxs-lookup"><span data-stu-id="5e2c5-174">Clearing Content</span></span>

<span data-ttu-id="5e2c5-175">你的内容提供商实现了[Icontentcmdletprovider. Clearcontent \*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent)方法，以支持 `Clear-Content` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-175">Your content provider implements the [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontent\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent) method in support of the `Clear-Content` cmdlet.</span></span> <span data-ttu-id="5e2c5-176">此方法删除指定路径处的项的内容，但保留该项不变。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-176">This method removes the contents of the item at the specified path, but leaves the item intact.</span></span>

<span data-ttu-id="5e2c5-177">下面是此提供程序的[Icontentcmdletprovider. Clearcontent \*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent)方法的实现。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-177">Here is the implementation of the [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontent\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent) method for this provider.</span></span>

[!code-csharp[AccessDBProviderSample06.cs](~/powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L1775-L1812 "AccessDBProviderSample06.cs")]

#### <a name="things-to-remember-about-implementing-clearcontent"></a><span data-ttu-id="5e2c5-178">有关实现 ClearContent 的注意事项</span><span class="sxs-lookup"><span data-stu-id="5e2c5-178">Things to Remember About Implementing ClearContent</span></span>

<span data-ttu-id="5e2c5-179">以下条件可能适用于[Icontentcmdletprovider. Clearcontent \*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent)的实现：。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-179">The following conditions may apply to an implementation of [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontent\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent):</span></span>

- <span data-ttu-id="5e2c5-180">定义提供程序类时，Windows PowerShell 内容提供程序可以声明 ExpandWildcards、Filter、Include 或 Exclude 的提供程序功能， [Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities)枚举。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-180">When defining the provider class, a Windows PowerShell content provider might declare provider capabilities of ExpandWildcards, Filter, Include, or Exclude, from the [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumeration.</span></span> <span data-ttu-id="5e2c5-181">在这些情况下， [Icontentcmdletprovider. Clearcontent \*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent)方法的实现必须确保传递给该方法的路径满足指定功能的要求。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-181">In these cases, the implementation of the [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontent\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent) method must ensure that the path passed to the method meets the requirements of the specified capabilities.</span></span> <span data-ttu-id="5e2c5-182">若要执行此操作，方法应访问相应的属性，例如， [Cmdletprovider \*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude)和[Cmdletprovider \*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include)属性中的相应属性，例如 ""。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-182">To do this, the method should access the appropriate property, for example, the [System.Management.Automation.Provider.Cmdletprovider.Exclude\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) and [System.Management.Automation.Provider.Cmdletprovider.Include\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) properties.</span></span>

- <span data-ttu-id="5e2c5-183">默认情况下，除非[Cmdletprovider \*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force)属性设置为 `true`，否则此方法的重写不应清除用户隐藏的对象的内容。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-183">By default, overrides of this method should not clear the contents of objects that are hidden from the user unless the [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) property is set to `true`.</span></span> <span data-ttu-id="5e2c5-184">如果路径表示从用户和[Cmdletprovider \*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force)中隐藏的项被设置为 `false`，则应写入错误，则为。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-184">An error should be written if the path represents an item that is hidden from the user and [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) is set to `false`.</span></span>

- <span data-ttu-id="5e2c5-185">在对数据存储进行任何更改之前，你的[Icontentcmdletprovider 和 Clearcontent \*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent)方法的实现应调用[Cmdletprovider](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) ，并验证其返回值的返回值。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-185">Your implementation of the [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontent\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent) method should call [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) and verify its return value before making any changes to the data store.</span></span> <span data-ttu-id="5e2c5-186">此方法用于确认对数据存储进行更改时（如清除内容）执行操作。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-186">This method is used to confirm execution of an operation when a change is made to the data store, such as clearing content.</span></span> <span data-ttu-id="5e2c5-187">[Cmdletprovider. ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess)方法发送要更改为用户的资源的名称，并在 Windows PowerShell 运行时处理任何命令行设置或首选项变量来确定应显示的内容。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-187">The [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) method sends the name of the resource to be changed to the user, with the Windows PowerShell runtime handling any command-line settings or preference variables in determining what should be displayed.</span></span>

  <span data-ttu-id="5e2c5-188">在对 Cmdletprovider 的调用返回 `true`后，\* 方法应调用[ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess)方法，则为，否则返回[Icontentcmdletprovider. Clearcontent \*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent)方法的调用方，则为。 [System.Management.Automation.Provider.Cmdletprovider.ShouldContinue](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue)</span><span class="sxs-lookup"><span data-stu-id="5e2c5-188">After the call to [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) returns `true`, the [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontent\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent) method should call the [System.Management.Automation.Provider.Cmdletprovider.ShouldContinue](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) method.</span></span> <span data-ttu-id="5e2c5-189">此方法向用户发送一条消息，以允许反馈验证是否应继续进行操作。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-189">This method sends a message to the user to allow feedback to verify if the operation should be continued.</span></span> <span data-ttu-id="5e2c5-190">对[Cmdletprovider. ShouldContinue](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue)的调用允许对潜在的危险系统修改进行额外检查。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-190">The call to [System.Management.Automation.Provider.Cmdletprovider.ShouldContinue](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) allows an additional check for potentially dangerous system modifications.</span></span>

## <a name="attaching-dynamic-parameters-to-the-clear-content-cmdlet"></a><span data-ttu-id="5e2c5-191">将动态参数附加到清除内容 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="5e2c5-191">Attaching Dynamic Parameters to the Clear-Content Cmdlet</span></span>

<span data-ttu-id="5e2c5-192">`Clear-Content` cmdlet 可能需要在运行时添加的其他动态参数。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-192">The `Clear-Content` cmdlet might require additional dynamic parameters that are added at runtime.</span></span> <span data-ttu-id="5e2c5-193">为了提供这些动态参数，Windows PowerShell 内容提供程序必须实现[Icontentcmdletprovider. Clearcontentdynamicparameters \*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContentDynamicParameters)方法来处理这些参数。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-193">To provide these dynamic parameters, the Windows PowerShell content provider must implement the [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontentdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContentDynamicParameters) method to handle these parameters.</span></span> <span data-ttu-id="5e2c5-194">此方法检索指定路径处的项的参数。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-194">This method retrieves the parameters for the item at the indicated path.</span></span> <span data-ttu-id="5e2c5-195">此方法检索指定路径处的项的动态参数，并返回一个对象，该对象具有与 cmdlet 类或[Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary)对象类似的分析特性的属性和字段。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-195">This method retrieves dynamic parameters for the item at the indicated path and returns an object that has properties and fields with parsing attributes similar to a cmdlet class or a [System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) object.</span></span> <span data-ttu-id="5e2c5-196">Windows PowerShell 运行时使用返回的对象将参数添加到 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-196">The Windows PowerShell runtime uses the returned object to add the parameters to the cmdlet.</span></span>

<span data-ttu-id="5e2c5-197">此 Windows PowerShell 容器提供程序未实现此方法。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-197">This Windows PowerShell container provider does not implement this method.</span></span> <span data-ttu-id="5e2c5-198">但是，下面的代码是此方法的默认实现。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-198">However, the following code is the default implementation of this method.</span></span>

```csharp
public object ClearContentDynamicParameters(string path)
{
    return null;
}
```

[!code-csharp[AccessDBProviderSample06.cs](~/powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L1819-L1822 "AccessDBProviderSample06.cs")]

## <a name="code-sample"></a><span data-ttu-id="5e2c5-199">代码示例</span><span class="sxs-lookup"><span data-stu-id="5e2c5-199">Code Sample</span></span>

<span data-ttu-id="5e2c5-200">有关完整的示例代码，请参阅[AccessDbProviderSample06 代码示例](./accessdbprovidersample06-code-sample.md)。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-200">For complete sample code, see [AccessDbProviderSample06 Code Sample](./accessdbprovidersample06-code-sample.md).</span></span>

## <a name="defining-object-types-and-formatting"></a><span data-ttu-id="5e2c5-201">定义对象类型和格式设置</span><span class="sxs-lookup"><span data-stu-id="5e2c5-201">Defining Object Types and Formatting</span></span>

<span data-ttu-id="5e2c5-202">编写提供程序时，可能需要将成员添加到现有对象或定义新的对象。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-202">When writing a provider, it may be necessary to add members to existing objects or define new objects.</span></span> <span data-ttu-id="5e2c5-203">完成此操作后，你必须创建一个类型文件，Windows PowerShell 可以使用该文件来标识该对象的成员和定义如何显示该对象的格式化文件。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-203">When this is done, you must create a Types file that Windows PowerShell can use to identify the members of the object and a Format file that defines how the object is displayed.</span></span> <span data-ttu-id="5e2c5-204">有关详细信息，请参阅[扩展对象类型和格式](/previous-versions/ms714665(v=vs.85))。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-204">For more information, see [Extending Object Types and Formatting](/previous-versions/ms714665(v=vs.85)).</span></span>

## <a name="building-the-windows-powershell-provider"></a><span data-ttu-id="5e2c5-205">生成 Windows PowerShell 提供程序</span><span class="sxs-lookup"><span data-stu-id="5e2c5-205">Building the Windows PowerShell Provider</span></span>

<span data-ttu-id="5e2c5-206">请参阅[如何注册 cmdlet、提供程序和主机应用程序](/previous-versions/ms714644(v=vs.85))。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-206">See [How to Register Cmdlets, Providers, and Host Applications](/previous-versions/ms714644(v=vs.85)).</span></span>

## <a name="testing-the-windows-powershell-provider"></a><span data-ttu-id="5e2c5-207">测试 Windows PowerShell 提供程序</span><span class="sxs-lookup"><span data-stu-id="5e2c5-207">Testing the Windows PowerShell Provider</span></span>

<span data-ttu-id="5e2c5-208">向 Windows powershell 注册 Windows PowerShell 提供程序后，可以通过在命令行上运行支持的 cmdlet 来对其进行测试。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-208">When your Windows PowerShell provider has been registered with Windows PowerShell, you can test it by running the supported cmdlets on the command line.</span></span> <span data-ttu-id="5e2c5-209">例如，测试示例内容提供程序。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-209">For example, test the sample content provider.</span></span>

<span data-ttu-id="5e2c5-210">使用 `Get-Content` cmdlet 可检索数据库表中由 `Path` 参数指定的路径处的指定项的内容。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-210">Use the `Get-Content` cmdlet to retrieve the contents of specified item in the database table at the path specified by the `Path` parameter.</span></span> <span data-ttu-id="5e2c5-211">`ReadCount` 参数指定已定义内容读取器读取的项数（默认值为1）。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-211">The `ReadCount` parameter specifies the number of items for the defined content reader to read (default 1).</span></span> <span data-ttu-id="5e2c5-212">对于以下命令项，该 cmdlet 将从表中检索两行（items）并显示其内容。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-212">With the following command entry, the cmdlet retrieves two rows (items) from the table and displays their contents.</span></span> <span data-ttu-id="5e2c5-213">请注意，下面的示例输出使用虚构的 Access 数据库。</span><span class="sxs-lookup"><span data-stu-id="5e2c5-213">Note that the following example output uses a fictitious Access database.</span></span>

```powershell
Get-Content -Path mydb:\Customers -ReadCount 2
```

```Output
ID        : 1
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
ID        : 2
FirstName : Eva
LastName  : Corets
Email     : evacorets@cohowinery.com
Title     : Sales Representative
Company   : Coho Winery
WorkPhone : (360) 555-0100
Address   : 8910 Main Street
City      : Cabmerlot
State     : WA
Zip       : 98089
Country   : USA
```

## <a name="see-also"></a><span data-ttu-id="5e2c5-214">另请参阅</span><span class="sxs-lookup"><span data-stu-id="5e2c5-214">See Also</span></span>

[<span data-ttu-id="5e2c5-215">创建 Windows PowerShell 提供程序</span><span class="sxs-lookup"><span data-stu-id="5e2c5-215">Creating Windows PowerShell providers</span></span>](./how-to-create-a-windows-powershell-provider.md)

[<span data-ttu-id="5e2c5-216">设计你的 Windows PowerShell 提供程序</span><span class="sxs-lookup"><span data-stu-id="5e2c5-216">Design Your Windows PowerShell provider</span></span>](./designing-your-windows-powershell-provider.md)

<span data-ttu-id="5e2c5-217">[扩展对象类型和格式](/previous-versions//ms714665(v=vs.85))</span><span class="sxs-lookup"><span data-stu-id="5e2c5-217">[Extending Object Types and Formatting](/previous-versions//ms714665(v=vs.85))</span></span>

[<span data-ttu-id="5e2c5-218">实现导航 Windows PowerShell 提供程序</span><span class="sxs-lookup"><span data-stu-id="5e2c5-218">Implement a Navigation Windows PowerShell provider</span></span>](./creating-a-windows-powershell-navigation-provider.md)

<span data-ttu-id="5e2c5-219">[如何注册 Cmdlet、提供程序和主机应用程序](/previous-versions/ms714644(v=vs.85))</span><span class="sxs-lookup"><span data-stu-id="5e2c5-219">[How to Register Cmdlets, Providers, and Host Applications](/previous-versions/ms714644(v=vs.85))</span></span>

[<span data-ttu-id="5e2c5-220">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="5e2c5-220">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)

[<span data-ttu-id="5e2c5-221">Windows PowerShell 程序员指南</span><span class="sxs-lookup"><span data-stu-id="5e2c5-221">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)
