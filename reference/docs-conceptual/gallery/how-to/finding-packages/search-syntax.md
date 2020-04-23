---
ms.date: 06/12/2017
contributor: JKeithB
keywords: 库,powershell,cmdlet,psgallery
title: 库搜索语法
ms.openlocfilehash: aabcaa1f1b5b641ab5033c9ba2e358477c84a23b
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "71328448"
---
# <a name="gallery-search-syntax"></a><span data-ttu-id="edb85-103">库搜索语法</span><span class="sxs-lookup"><span data-stu-id="edb85-103">Gallery Search Syntax</span></span>

<span data-ttu-id="edb85-104">可以使用 [PowerShell 库的网站](https://www.powershellgallery.com/)搜索 PowerShell 库。</span><span class="sxs-lookup"><span data-stu-id="edb85-104">You can search the PowerShell Gallery using the [PowerShell Gallery's web site](https://www.powershellgallery.com/).</span></span>
<span data-ttu-id="edb85-105">PowerShell 库网站提供文本搜索框，可以在其中使用单词、短语和关键字表达式来缩小搜索结果的范围。</span><span class="sxs-lookup"><span data-stu-id="edb85-105">PowerShell Gallery web site offers a text searchbox where you can use words, phrases and keyword expressions to narrow down search results.</span></span>

## <a name="search-by-keywords"></a><span data-ttu-id="edb85-106">按关键字搜索</span><span class="sxs-lookup"><span data-stu-id="edb85-106">Search by Keywords</span></span>

    dsc azure sql

<span data-ttu-id="edb85-107">“搜索”尝试查找包含所有 3 个关键字的相关文档，并返回匹配的文档。</span><span class="sxs-lookup"><span data-stu-id="edb85-107">Search attempts to find relevant documents containing all 3 keywords, and return matching documents.</span></span>

## <a name="search-using-phrases-and-keywords"></a><span data-ttu-id="edb85-108">使用短语和关键字进行搜索</span><span class="sxs-lookup"><span data-stu-id="edb85-108">Search using Phrases and keywords</span></span>

    "azure sql" deployment

<span data-ttu-id="edb85-109">在引号（“”）之间输入短语将搜索更改为查找特定的短语而不是单独的关键字。</span><span class="sxs-lookup"><span data-stu-id="edb85-109">Entering a phrase between quotation marks ("") change the search to look for the particular phrase instead of separate keywords.</span></span>
<span data-ttu-id="edb85-110">匹配的文档通常应包含确切的短语“azure sql”，包括大写的变体。“Azure SQL”，并通常还包含“deployment”一词。</span><span class="sxs-lookup"><span data-stu-id="edb85-110">Matching documents should usually contain the exact phrase "azure sql", including variations on capitalization e.g. "Azure SQL", and also usually contain the word 'deployment'.</span></span>

## <a name="filtering-on-fields"></a><span data-ttu-id="edb85-111">按字段进行筛选</span><span class="sxs-lookup"><span data-stu-id="edb85-111">Filtering on fields</span></span>

<span data-ttu-id="edb85-112">通过将字段名称作为搜索词前缀，可以搜索特定包 ID（或“Id”或“id”），或一些其他字段。</span><span class="sxs-lookup"><span data-stu-id="edb85-112">You can search for a specific package ID (or 'Id' or 'id'), or certain other fields by prefixing search terms with the field name.</span></span>

<span data-ttu-id="edb85-113">目前可搜索的字段有“Id”、“Version”、“Tags”、“Author”、“Owner”、“Functions”、“Cmdlet”、“DscResources”和“PowerShellVersion”。</span><span class="sxs-lookup"><span data-stu-id="edb85-113">Currently the searchable fields are 'Id', 'Version', 'Tags', 'Author', 'Owner', 'Functions', 'Cmdlets', 'DscResources' and 'PowerShellVersion'.</span></span>

<span data-ttu-id="edb85-114">[ID 和标题之间的区别是什么？</span><span class="sxs-lookup"><span data-stu-id="edb85-114">[What's the difference between ID and Title?</span></span> <span data-ttu-id="edb85-115">ID 是在控制台中使用的名称。</span><span class="sxs-lookup"><span data-stu-id="edb85-115">ID is the name you use in the console.</span></span> <span data-ttu-id="edb85-116">标题是在搜索结果中的包页顶部所显示的内容。]</span><span class="sxs-lookup"><span data-stu-id="edb85-116">Title is what is shown at the top of the package page in search results.]</span></span>

## <a name="examples"></a><span data-ttu-id="edb85-117">示例</span><span class="sxs-lookup"><span data-stu-id="edb85-117">Examples</span></span>

    ID:PSReadline
    
<span data-ttu-id="edb85-118">查找 ID 包含“PSReadline”的包。</span><span class="sxs-lookup"><span data-stu-id="edb85-118">finds packages with an ID containing "PSReadline".</span></span>

    Id:"AzureRM.Profile"

<span data-ttu-id="edb85-119">是另一种在其 ID 字段中查找具有“AzureRM.Profile”的包的方法。</span><span class="sxs-lookup"><span data-stu-id="edb85-119">is another way to find packages with "AzureRM.Profile" in their ID field.</span></span>

<span data-ttu-id="edb85-120">“Id”筛选器是一个子字符串匹配，因此，如果搜索以下内容：</span><span class="sxs-lookup"><span data-stu-id="edb85-120">The 'Id' filter is a substring match, so if you search for the following:</span></span>

    Id:"azure"

<span data-ttu-id="edb85-121">它将提供结果，其中包括“AzureRM.Profile”和“Azure.Storage”。</span><span class="sxs-lookup"><span data-stu-id="edb85-121">This provides results that include AzureRM.Profile' and 'Azure.Storage'.</span></span>

<span data-ttu-id="edb85-122">你也可以搜索单个字段中的多个关键字。</span><span class="sxs-lookup"><span data-stu-id="edb85-122">You can also search for multiple keywords in a single field.</span></span> 

    id:azure tags:intellisense

<span data-ttu-id="edb85-123">还可以使用双引号执行短语搜索：</span><span class="sxs-lookup"><span data-stu-id="edb85-123">And you can perform phrase searches using double quotes:</span></span>

    id:"azure.storage"

<span data-ttu-id="edb85-124">搜索具有 DSC 标记的所有包。</span><span class="sxs-lookup"><span data-stu-id="edb85-124">To search all packages with DSC tag.</span></span>

    Tags:DSC

<span data-ttu-id="edb85-125">搜索具有指定函数的所有包。</span><span class="sxs-lookup"><span data-stu-id="edb85-125">To search all packages with the specified function.</span></span>

    Functions:Get-TreeSize

<span data-ttu-id="edb85-126">搜索具有指定 cmdlet 的所有包。</span><span class="sxs-lookup"><span data-stu-id="edb85-126">To search all packages with the specified cmdlet.</span></span>

    Cmdlets:Get-AzureRmEnvironment

<span data-ttu-id="edb85-127">搜索具有指定 DSC 资源名称的所有包。</span><span class="sxs-lookup"><span data-stu-id="edb85-127">To search all packages with the specified DSC Resource name.</span></span>

    DscResources:xArchive

<span data-ttu-id="edb85-128">搜索具有指定 PowerShellVersion 的所有包</span><span class="sxs-lookup"><span data-stu-id="edb85-128">To search all packages with the specified PowerShellVersion</span></span>

    PowerShellVersion:2.0

<span data-ttu-id="edb85-129">最后，如果你使用不支持的字段（如“commands”），我们将忽略该字段并搜索所有字段。</span><span class="sxs-lookup"><span data-stu-id="edb85-129">Finally, if you use a field we don't support, such as 'commands', we'll just ignore it and search all the fields.</span></span> <span data-ttu-id="edb85-130">因此以下查询</span><span class="sxs-lookup"><span data-stu-id="edb85-130">So the following query</span></span>

    commands:blobs storage

<span data-ttu-id="edb85-131">的解释与此查询完全相同：</span><span class="sxs-lookup"><span data-stu-id="edb85-131">Is interpreted exactly the same as this query:</span></span>

    blobs storage
