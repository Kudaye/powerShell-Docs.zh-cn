---
ms.date: 06/12/2017
contributor: JKeithB
keywords: 库,powershell,cmdlet,psgallery
title: 通过社交媒体或发表评论提供反馈
ms.openlocfilehash: 95e5db22b94151c3974189c30f1d4e580b47eeb5
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "71327878"
---
# <a name="providing-feedback-via-social-media-or-comments"></a><span data-ttu-id="36cb9-103">通过社交媒体或发表评论提供反馈</span><span class="sxs-lookup"><span data-stu-id="36cb9-103">Providing Feedback via social media or comments</span></span>

<span data-ttu-id="36cb9-104">PowerShell 库支持以下两种反馈方法，以便用户能够提供有关包的公共反馈：</span><span class="sxs-lookup"><span data-stu-id="36cb9-104">The PowerShell Gallery supports two approaches for users to provide public feedback on a package:</span></span>

- <span data-ttu-id="36cb9-105">使用左侧边缘的链接，在 Facebook、LinkedIn 或 Twitter 社交媒体网站中“分享”包；</span><span class="sxs-lookup"><span data-stu-id="36cb9-105">Use the links on the left edge to "share" a package in Facebook, LinkedIn, or Twitter social media sites;</span></span>
- <span data-ttu-id="36cb9-106">使用评论功能对包发表评论，并允许作者查看已对包发表的评论。</span><span class="sxs-lookup"><span data-stu-id="36cb9-106">Use the Comment feature to post comments on a package, and to allow Authors to watch for comments on packages they publish.</span></span>

## <a name="social-media-feedback"></a><span data-ttu-id="36cb9-107">社交媒体反馈</span><span class="sxs-lookup"><span data-stu-id="36cb9-107">Social Media Feedback</span></span>

<span data-ttu-id="36cb9-108">对于 PowerShell 库中的每一个包，网页左侧都有 Facebook、LinkedIn 和 Twitter 链接。</span><span class="sxs-lookup"><span data-stu-id="36cb9-108">On the left side of the page for each package in the PowerShell Gallery there are links for Facebook, LinkedIn, and Twitter.</span></span>
<span data-ttu-id="36cb9-109">单击这些链接可以打开社交媒体网站，并能快速分享包链接。</span><span class="sxs-lookup"><span data-stu-id="36cb9-109">Clicking on these links will open the social media site, and allow quickly sharing a link to the package.</span></span>

<span data-ttu-id="36cb9-110">用户必须登录已选择的网站，才能分享 PowerShell 库包。</span><span class="sxs-lookup"><span data-stu-id="36cb9-110">Users must log in to the site they have chosen in order to share the PowerShell Gallery package.</span></span>

<span data-ttu-id="36cb9-111">如果用户认为需要向他人推荐包，建议执行上述操作。</span><span class="sxs-lookup"><span data-stu-id="36cb9-111">Users are encouraged to do this if they find that a package is something they would recommend to others.</span></span>
<span data-ttu-id="36cb9-112">PowerShell 库将检查每个用于“分享”包的社交媒体网站，并显示相应包在每个社交媒体网站中的分享次数。</span><span class="sxs-lookup"><span data-stu-id="36cb9-112">The PowerShell Gallery will check each social media site for "shares" of the package, and display how many times that package has been shared in each of the social media sites.</span></span>
<span data-ttu-id="36cb9-113">由于只显示分享次数，因此其他用户可以看作是“赞”相应包的次数。</span><span class="sxs-lookup"><span data-stu-id="36cb9-113">Since this shows only the count of times something has been shared, it will be interpreted other users as "liking" the package.</span></span>

## <a name="comments"></a><span data-ttu-id="36cb9-114">注释</span><span class="sxs-lookup"><span data-stu-id="36cb9-114">Comments</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36cb9-115">Livefyre 评论由第三方供应商提供，不再受支持。</span><span class="sxs-lookup"><span data-stu-id="36cb9-115">Livefyre commenting is provided by a third-party vendor and is no longer supported.</span></span>
> <span data-ttu-id="36cb9-116">自 2019 年 5 月 1 日起，PowerShell 库将不再支持 Livefyre 评论。</span><span class="sxs-lookup"><span data-stu-id="36cb9-116">Livefyre commenting will no longer be available on the PowerShell Gallery starting 05/01/2019.</span></span> 

<span data-ttu-id="36cb9-117">PowerShell 库使用 LiveFyre 服务来允许用户对包发表评论。</span><span class="sxs-lookup"><span data-stu-id="36cb9-117">The PowerShell Gallery uses the LiveFyre service to allow users to comment on packages.</span></span>
<span data-ttu-id="36cb9-118">如果需要提供建议或反馈，用户可以使用此功能提供对包网页的所有访问者都可见的反馈。</span><span class="sxs-lookup"><span data-stu-id="36cb9-118">Users who have recommendations or feedback can use this feature to provide feedback that is visible to anyone who visits the package page.</span></span>
<span data-ttu-id="36cb9-119">包所有者可以关注此反馈，并在有人发表评论时收到通知。</span><span class="sxs-lookup"><span data-stu-id="36cb9-119">Package owners can Follow this feedback, and be notified when someone posts a comment.</span></span>

<span data-ttu-id="36cb9-120">评论系统基于 LiveFyre，这是不受 Microsoft 管理的独立服务，要求使用唯一登录名。</span><span class="sxs-lookup"><span data-stu-id="36cb9-120">The Comment system is based on LiveFyre, which is a separate service that is not managed by Microsoft, and requires unique login to use.</span></span>
<span data-ttu-id="36cb9-121">首次选择对一个包发表评论或关注评论时，系统会提示创建 LiveFyre 帐户。</span><span class="sxs-lookup"><span data-stu-id="36cb9-121">The first time you choose to leave a comment or follow comments on one of your packages, you will be prompted to create a LiveFyre account.</span></span>

<span data-ttu-id="36cb9-122">如果已经创建 LiveFyre 帐户并登录，可以编写评论以提供包反馈，再单击“发表评论...”。评论不会立即可见。</span><span class="sxs-lookup"><span data-stu-id="36cb9-122">If you have created a LiveFyre account and logged in, you can craft a comment that provides feedback on the package, then click on "Post comment..." The comment will not be visible immediately.</span></span>
<span data-ttu-id="36cb9-123">PowerShell 库管理员会审核库包的评论，要发表的所有评论都会先经由审查方审核，然后才会发表并对其他人可见。</span><span class="sxs-lookup"><span data-stu-id="36cb9-123">Comments for gallery packages are moderated by the PowerShell Gallery administrators, and all posts are reviewed by the moderators before being published and visible to others.</span></span>
<span data-ttu-id="36cb9-124">之所以要审核评论是为了确保它们符合 PowerShell 库[使用条款](https://www.powershellgallery.com/policies/Terms)规定的公共行为。</span><span class="sxs-lookup"><span data-stu-id="36cb9-124">Our purpose in moderating the comments is to ensure that they align with public behavior consistent with the PowerShell Gallery [Terms of Use](https://www.powershellgallery.com/policies/Terms).</span></span>

<span data-ttu-id="36cb9-125">建议包所有者关注在 LiveFyre 中发表的评论。</span><span class="sxs-lookup"><span data-stu-id="36cb9-125">Package owners are encouraged to Follow comments that are posted to LiveFyre.</span></span>
<span data-ttu-id="36cb9-126">必须创建 LiveFyre 帐户，建议使用在 LiveFyre 中发布包时所用的同一电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="36cb9-126">A LiveFyre account is required, and it is recommended to use the same email address you use for publishing your package in LiveFyre.</span></span>
<span data-ttu-id="36cb9-127">若要关注评论，请先登录 LiveFyre，再导航到你被列为所有者的任意包。</span><span class="sxs-lookup"><span data-stu-id="36cb9-127">To Follow comments, log into LiveFyre, and navigate to any package where you are listed as an Owner.</span></span>
<span data-ttu-id="36cb9-128">在每个包底部的“评论”框下方，都会看到“+关注”。</span><span class="sxs-lookup"><span data-stu-id="36cb9-128">Below the Comment box at the bottom of each package you will see "+Follow".</span></span>
<span data-ttu-id="36cb9-129">单击此按钮后，LiveFyre 便会在有人对此包发表新评论时向注册的电子邮件地址发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="36cb9-129">Once you click on this, LiveFyre will send an email to the registered email address any time new comments made on the package.</span></span>
