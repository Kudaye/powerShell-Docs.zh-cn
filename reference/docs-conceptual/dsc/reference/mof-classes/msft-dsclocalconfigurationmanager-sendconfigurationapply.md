---
ms.date: 06/12/2017
keywords: dsc,powershell,配置,安装程序
title: SendConfigurationApply 方法
ms.openlocfilehash: 11b9d435bbaac1600d25ff074b6c55b236a8378b
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "71954884"
---
# <a name="sendconfigurationapply-method"></a><span data-ttu-id="d6359-103">SendConfigurationApply 方法</span><span class="sxs-lookup"><span data-stu-id="d6359-103">SendConfigurationApply method</span></span>

<span data-ttu-id="d6359-104">将配置文档发送到托管节点，并使用配置代理应用配置。</span><span class="sxs-lookup"><span data-stu-id="d6359-104">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="d6359-105">语法</span><span class="sxs-lookup"><span data-stu-id="d6359-105">Syntax</span></span>

```mof
uint32 SendConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="d6359-106">参数</span><span class="sxs-lookup"><span data-stu-id="d6359-106">Parameters</span></span>

<span data-ttu-id="d6359-107">ConfigurationData  \[in\]：配置的环境数据。</span><span class="sxs-lookup"><span data-stu-id="d6359-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="d6359-108">force  \[in\]：若为 true  ，则强制停止配置。</span><span class="sxs-lookup"><span data-stu-id="d6359-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="d6359-109">返回值</span><span class="sxs-lookup"><span data-stu-id="d6359-109">Return value</span></span>

<span data-ttu-id="d6359-110">如果成功，则返回零；否则返回错误代码。</span><span class="sxs-lookup"><span data-stu-id="d6359-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="d6359-111">备注</span><span class="sxs-lookup"><span data-stu-id="d6359-111">Remarks</span></span>

<span data-ttu-id="d6359-112">这是一种静态方法。</span><span class="sxs-lookup"><span data-stu-id="d6359-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="d6359-113">要求</span><span class="sxs-lookup"><span data-stu-id="d6359-113">Requirements</span></span>

<span data-ttu-id="d6359-114">**MOF：** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="d6359-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="d6359-115">**命名空间**：Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="d6359-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="d6359-116">另请参阅</span><span class="sxs-lookup"><span data-stu-id="d6359-116">See also</span></span>

[<span data-ttu-id="d6359-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="d6359-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
