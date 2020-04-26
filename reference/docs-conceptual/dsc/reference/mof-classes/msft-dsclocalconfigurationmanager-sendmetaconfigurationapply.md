---
ms.date: 06/12/2017
keywords: dsc,powershell,配置,安装程序
title: SendMetaConfigurationApply 方法
ms.openlocfilehash: b2e420bafb8ea22aea43800f6e429d3ed785d1e8
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "71954874"
---
# <a name="sendmetaconfigurationapply-method"></a><span data-ttu-id="4c485-103">SendMetaConfigurationApply 方法</span><span class="sxs-lookup"><span data-stu-id="4c485-103">SendMetaConfigurationApply method</span></span>

<span data-ttu-id="4c485-104">设置用于控制配置代理的本地配置管理器设置。</span><span class="sxs-lookup"><span data-stu-id="4c485-104">Sets the Local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

## <a name="syntax"></a><span data-ttu-id="4c485-105">语法</span><span class="sxs-lookup"><span data-stu-id="4c485-105">Syntax</span></span>

```mof
uint32 SendMetaConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="4c485-106">参数</span><span class="sxs-lookup"><span data-stu-id="4c485-106">Parameters</span></span>

<span data-ttu-id="4c485-107">ConfigurationData  \[in\]：配置的环境数据。</span><span class="sxs-lookup"><span data-stu-id="4c485-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="4c485-108">force  \[in\]：若为 true  ，则强制停止配置。</span><span class="sxs-lookup"><span data-stu-id="4c485-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="4c485-109">返回值</span><span class="sxs-lookup"><span data-stu-id="4c485-109">Return value</span></span>

<span data-ttu-id="4c485-110">如果成功，则返回零；否则返回错误代码。</span><span class="sxs-lookup"><span data-stu-id="4c485-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="4c485-111">备注</span><span class="sxs-lookup"><span data-stu-id="4c485-111">Remarks</span></span>

<span data-ttu-id="4c485-112">这是一种静态方法。</span><span class="sxs-lookup"><span data-stu-id="4c485-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="4c485-113">要求</span><span class="sxs-lookup"><span data-stu-id="4c485-113">Requirements</span></span>

<span data-ttu-id="4c485-114">**MOF：** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="4c485-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="4c485-115">**命名空间**：Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="4c485-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="4c485-116">另请参阅</span><span class="sxs-lookup"><span data-stu-id="4c485-116">See also</span></span>

[<span data-ttu-id="4c485-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="4c485-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
