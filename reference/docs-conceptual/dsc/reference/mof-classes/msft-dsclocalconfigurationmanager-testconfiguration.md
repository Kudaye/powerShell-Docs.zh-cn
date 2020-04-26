---
ms.date: 06/12/2017
keywords: dsc,powershell,配置,安装程序
title: TestConfiguration 方法
ms.openlocfilehash: 384134212e3b29b63dc045aee4b708c87c970302
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "71954864"
---
# <a name="testconfiguration-method"></a><span data-ttu-id="74f40-103">TestConfiguration 方法</span><span class="sxs-lookup"><span data-stu-id="74f40-103">TestConfiguration method</span></span>

<span data-ttu-id="74f40-104">将配置文档发送到托管节点并针对该文档验证当前配置。</span><span class="sxs-lookup"><span data-stu-id="74f40-104">Sends the configuration document to the managed node and verifies the current configuration against the document.</span></span>

## <a name="syntax"></a><span data-ttu-id="74f40-105">语法</span><span class="sxs-lookup"><span data-stu-id="74f40-105">Syntax</span></span>

```mof
uint32 TestConfiguration(
  [in]  uint8                          configurationData[],
  [out] boolean                        InDesiredState,
  [out] MSFT_ResourceInDesiredState    ResourcesInDesiredState[],
  [out] MSFT_ResourceNotInDesiredState ResourcesNotInDesiredState[]
);
```

## <a name="parameters"></a><span data-ttu-id="74f40-106">参数</span><span class="sxs-lookup"><span data-stu-id="74f40-106">Parameters</span></span>

<span data-ttu-id="74f40-107">configurationData  \[in\]：配置的环境数据。</span><span class="sxs-lookup"><span data-stu-id="74f40-107">*configurationData* \[in\] Environment data for the confuguration.</span></span>

<span data-ttu-id="74f40-108">InDesiredState  \[out\]：返回响应时，指定托管节点是否处于配置文档指定的状态。</span><span class="sxs-lookup"><span data-stu-id="74f40-108">*InDesiredState* \[out\] On return, specifies whether the managed node is in the state specified by the configuration document.</span></span>

<span data-ttu-id="74f40-109">ResourcesInDesiredState  \[out\]：返回响应时，包含 MSFT_ResourceInDesiredState  类的嵌入实例，此类指定处于所需状态的资源。</span><span class="sxs-lookup"><span data-stu-id="74f40-109">*ResourcesInDesiredState* \[out\] On return, contains an embedded instance of the **MSFT_ResourceInDesiredState** class that specifies resources that are in the desired state.</span></span>

<span data-ttu-id="74f40-110">ResourcesNotInDesiredState  \[out\]：返回响应时，包含 MSFT_ResourceNotInDesiredState  类的嵌入实例，此类指定不处于所需状态的资源。</span><span class="sxs-lookup"><span data-stu-id="74f40-110">*ResourcesNotInDesiredState* \[out\] On return, contains an embedded instance of the **MSFT_ResourceNotInDesiredState** class that specifies resources that are not in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="74f40-111">返回值</span><span class="sxs-lookup"><span data-stu-id="74f40-111">Return value</span></span>

<span data-ttu-id="74f40-112">如果成功，则返回零；否则返回错误代码。</span><span class="sxs-lookup"><span data-stu-id="74f40-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="74f40-113">备注</span><span class="sxs-lookup"><span data-stu-id="74f40-113">Remarks</span></span>

<span data-ttu-id="74f40-114">这是一种静态方法。</span><span class="sxs-lookup"><span data-stu-id="74f40-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="74f40-115">要求</span><span class="sxs-lookup"><span data-stu-id="74f40-115">Requirements</span></span>

<span data-ttu-id="74f40-116">**MOF：** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="74f40-116">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="74f40-117">**命名空间**：Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="74f40-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="74f40-118">另请参阅</span><span class="sxs-lookup"><span data-stu-id="74f40-118">See also</span></span>

[<span data-ttu-id="74f40-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="74f40-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
