---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
title: UpdatePanel 컨트롤 (VB) 애니메이션 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 내용에 대 한 프로그램...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4c306a2c-92b6-4904-b70b-365b847334fe
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
msc.type: authoredcontent
ms.openlocfilehash: a7c40ebe359e21602d9f1de8205e1a7c808acc85
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59384255"
---
# <a name="animating-an-updatepanel-control-vb"></a><span data-ttu-id="651ae-104">UpdatePanel 컨트롤 애니메이션(VB)</span><span class="sxs-lookup"><span data-stu-id="651ae-104">Animating an UpdatePanel Control (VB)</span></span>

<span data-ttu-id="651ae-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="651ae-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="651ae-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="651ae-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)</span></span>

> <span data-ttu-id="651ae-107">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="651ae-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="651ae-108">UpdatePanel의 내용에 대 한 특별 한 extender를 있는 애니메이션 프레임 워크에 크게 의존 합니다. UpdatePanelAnimation.</span><span class="sxs-lookup"><span data-stu-id="651ae-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="651ae-109">이 자습서는 UpdatePanel에 대 한 이러한 애니메이션을 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="651ae-109">This tutorial shows how to set up such an animation for an UpdatePanel.</span></span>


## <a name="overview"></a><span data-ttu-id="651ae-110">개요</span><span class="sxs-lookup"><span data-stu-id="651ae-110">Overview</span></span>

<span data-ttu-id="651ae-111">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="651ae-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="651ae-112">내용에 대 한는 `UpdatePanel`, 애니메이션 프레임 워크에 크게 의존 하는 특별 한 extender 존재: `UpdatePanelAnimation`합니다.</span><span class="sxs-lookup"><span data-stu-id="651ae-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="651ae-113">이 자습서에 대 한 이러한 애니메이션을 설정 하는 방법을 보여 줍니다는 `UpdatePanel`합니다.</span><span class="sxs-lookup"><span data-stu-id="651ae-113">This tutorial shows how to set up such an animation for an `UpdatePanel`.</span></span>

## <a name="steps"></a><span data-ttu-id="651ae-114">단계</span><span class="sxs-lookup"><span data-stu-id="651ae-114">Steps</span></span>

<span data-ttu-id="651ae-115">첫 번째 단계는 일반적으로 포함 합니다 `ScriptManager` 페이지에서 ASP.NET AJAX library가 로드 하 고 컨트롤 도구 키트를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="651ae-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample1.aspx)]

<span data-ttu-id="651ae-116">ASP.NET에이 시나리오에서는 애니메이션을 적용할 `Wizard` 에 있는 웹 컨트롤을 `UpdatePanel`입니다.</span><span class="sxs-lookup"><span data-stu-id="651ae-116">The animation in this scenario will be applied to an ASP.NET `Wizard` web control residing in an `UpdatePanel`.</span></span> <span data-ttu-id="651ae-117">세 가지 (임의) 단계는 포스트백을 트리거하려면 충분 한 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="651ae-117">Three (arbitrary) steps provide enough options to trigger postbacks:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample2.aspx)]

<span data-ttu-id="651ae-118">에 필요한 태그를 `UpdatePanelAnimationExtender` 컨트롤에 사용 되는 태그에 상당히 비슷합니다는 `AnimationExtender`합니다.</span><span class="sxs-lookup"><span data-stu-id="651ae-118">The markup necessary for the `UpdatePanelAnimationExtender` control is quite similar to the markup used for the `AnimationExtender`.</span></span> <span data-ttu-id="651ae-119">`TargetControlID` 제공 하는 특성을 `ID` 의 `UpdatePanel` ;에 애니메이션 효과를 내는 `UpdatePanelAnimationExtender` 컨트롤을 `<Animations>` 요소 있는 애니메이션의 XML 태그를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="651ae-119">In the `TargetControlID` attribute we provide the `ID` of the `UpdatePanel` to animate; within the `UpdatePanelAnimationExtender` control, the `<Animations>` element holds XML markup for the animation(s).</span></span> <span data-ttu-id="651ae-120">그러나 한 가지 차이가 있습니다. 이벤트 및 이벤트 처리기의 용량은 제한 비교 `AnimationExtender`합니다.</span><span class="sxs-lookup"><span data-stu-id="651ae-120">However there is one difference: The amount of events and event handlers is limited in comparison to `AnimationExtender`.</span></span> <span data-ttu-id="651ae-121">에 대 한 `UpdatePanels`, 두 개의 정도의 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="651ae-121">For `UpdatePanels`, only two of them exist:</span></span>

- <span data-ttu-id="651ae-122">`<OnUpdated>` UpdatePanel 업데이트 된 경우</span><span class="sxs-lookup"><span data-stu-id="651ae-122">`<OnUpdated>` when the UpdatePanel has been updated</span></span>
- <span data-ttu-id="651ae-123">`<OnUpdating>` UpdatePanel 업데이트를 시작할 때</span><span class="sxs-lookup"><span data-stu-id="651ae-123">`<OnUpdating>` when the UpdatePanel starts updating</span></span>

<span data-ttu-id="651ae-124">이 시나리오에서는 새 내용의 `UpdatePanel` 포스트백) (이후에 페이드 인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="651ae-124">In this scenario, the new content of the `UpdatePanel` (after the postback) shall fade in.</span></span> <span data-ttu-id="651ae-125">필요한 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="651ae-125">This is the necessary markup for that:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample3.aspx)]

<span data-ttu-id="651ae-126">이제 UpdatePanel 내 포스트백이 발생할 때마다 패널의 새 내용이 페이드 원활 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="651ae-126">Now whenever a postback occurs within the UpdatePanel, the new contents of the panel fade in smoothly.</span></span>


<span data-ttu-id="651ae-127">[![다음 마법사 단계 옅은 색은](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="651ae-127">[![The next wizard step is fading in](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="651ae-128">다음 마법사 단계 옅은 색은 ([클릭 하 여 큰 이미지 보기](animating-an-updatepanel-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="651ae-128">The next wizard step is fading in ([Click to view full-size image](animating-an-updatepanel-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="651ae-129">[이전](changing-an-animation-using-client-side-code-vb.md)
> [다음](dynamically-controlling-updatepanel-animations-vb.md)</span><span class="sxs-lookup"><span data-stu-id="651ae-129">[Previous](changing-an-animation-using-client-side-code-vb.md)
[Next](dynamically-controlling-updatepanel-animations-vb.md)</span></span>
