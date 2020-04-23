---
ms.date: 03/15/2018
keywords: dsc,powershell,配置,安装程序
title: 在 Microsoft Azure 上使用 DSC
ms.openlocfilehash: 6d71b69eea78e775a3e5aaac64bccfa10092b8e6
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "75870823"
---
# <a name="using-dsc-on-microsoft-azure"></a><span data-ttu-id="14444-103">在 Microsoft Azure 上使用 DSC</span><span class="sxs-lookup"><span data-stu-id="14444-103">Using DSC on Microsoft Azure</span></span>

<span data-ttu-id="14444-104">通过 [Azure 所需状态配置扩展处理程序](/azure/virtual-machines/extensions/dsc-overview)和 [Azure 自动化 DSC](/azure/automation/automation-dsc-overview)，Microsoft Azure 中支持所需状态配置 (DSC)。</span><span class="sxs-lookup"><span data-stu-id="14444-104">Desired State Configuration (DSC) is supported in Microsoft Azure through the [Azure Desired State Configuration extension handler](/azure/virtual-machines/extensions/dsc-overview) and through [Azure Automation DSC](/azure/automation/automation-dsc-overview).</span></span>

## <a name="azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="14444-105">Azure 所需状态配置扩展处理程序</span><span class="sxs-lookup"><span data-stu-id="14444-105">Azure Desired State Configuration extension handler</span></span>

<span data-ttu-id="14444-106">Azure DSC 扩展允许通过 DSC 管理位于 Microsoft Azure 中的 VM。</span><span class="sxs-lookup"><span data-stu-id="14444-106">The Azure DSC extension allows VMs hosted in Microsoft Azure to be managed with DSC.</span></span> <span data-ttu-id="14444-107">有关详情，请参阅以下主题：</span><span class="sxs-lookup"><span data-stu-id="14444-107">For more information, see the following topics:</span></span>

- [<span data-ttu-id="14444-108">Azure 所需状态配置扩展处理程序</span><span class="sxs-lookup"><span data-stu-id="14444-108">Azure Desired State Configuration extension handler</span></span>](/azure/virtual-machines/extensions/dsc-overview)
- [<span data-ttu-id="14444-109">通过 Azure Resource Manager 模板实现 Windows VMSS 和所需状态配置</span><span class="sxs-lookup"><span data-stu-id="14444-109">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>](/azure/virtual-machines/extensions/dsc-template)
- [<span data-ttu-id="14444-110">将凭据传递到 Azure DSC 扩展处理程序</span><span class="sxs-lookup"><span data-stu-id="14444-110">Passing credentials to the Azure DSC extension handler</span></span>](/azure/virtual-machines/extensions/dsc-credentials)
- [<span data-ttu-id="14444-111">Azure 所需状态配置扩展历史记录</span><span class="sxs-lookup"><span data-stu-id="14444-111">Azure Desired State Configuration extension history</span></span>](azureDscexthistory.md)

## <a name="azure-automation-dsc"></a><span data-ttu-id="14444-112">Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="14444-112">Azure Automation DSC</span></span>

<span data-ttu-id="14444-113">通过 [Azure 自动化服务](https://azure.microsoft.com/services/automation/)，可从 Azure 内部管理 DSC 配置、资源和托管节点。</span><span class="sxs-lookup"><span data-stu-id="14444-113">The [Azure Automation service](https://azure.microsoft.com/services/automation/) allows you to manage DSC configurations, resources, and managed nodes from within Azure.</span></span> <span data-ttu-id="14444-114">有关详情，请参阅以下主题：</span><span class="sxs-lookup"><span data-stu-id="14444-114">For more information, see the following topics:</span></span>

- [<span data-ttu-id="14444-115">Azure 自动化 DSC</span><span class="sxs-lookup"><span data-stu-id="14444-115">Azure Automation DSC</span></span>](/azure/automation/automation-dsc-overview)
- [<span data-ttu-id="14444-116">Azure 自动化 DSC 入门</span><span class="sxs-lookup"><span data-stu-id="14444-116">Getting started with Azure Automation DSC</span></span>](/azure/automation/automation-dsc-getting-started)
- [<span data-ttu-id="14444-117">载入计算机以便通过 Azure 自动化 DSC 进行管理</span><span class="sxs-lookup"><span data-stu-id="14444-117">Onboarding machines for management by Azure Automation DSC</span></span>](/azure/automation/automation-dsc-onboarding)