---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-cs
title: 다른 컨트롤 (C#)에서 애니메이션 트리거 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 일반적으로 시작을...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5d99c2b-d8ee-413c-80d5-c120cffb0a4c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 6216f24e497936245280f337477b287ff2afb080
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58421390"
---
<a name="triggering-an-animation-in-another-control-c"></a><span data-ttu-id="32d1b-104">다른 컨트롤에서 애니메이션 트리거(C#)</span><span class="sxs-lookup"><span data-stu-id="32d1b-104">Triggering an Animation in another Control (C#)</span></span>
====================
<span data-ttu-id="32d1b-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="32d1b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="32d1b-106">[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="32d1b-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8CS.pdf)</span></span>

> <span data-ttu-id="32d1b-107">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="32d1b-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="32d1b-108">일반적으로 동일한 컨트롤을 사용 하 여 사용자 상호 작용에 의해 트리거됩니다는 애니메이션을 시작.</span><span class="sxs-lookup"><span data-stu-id="32d1b-108">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="32d1b-109">하지만 이기도 다른 컨트롤이 컨트롤 및 애니메이션을 사용 하 여 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32d1b-109">It is however also possible to interact with one control and then animation another control.</span></span>


## <a name="overview"></a><span data-ttu-id="32d1b-110">개요</span><span class="sxs-lookup"><span data-stu-id="32d1b-110">Overview</span></span>

<span data-ttu-id="32d1b-111">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="32d1b-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="32d1b-112">일반적으로 동일한 컨트롤을 사용 하 여 사용자 상호 작용에 의해 트리거됩니다는 애니메이션을 시작.</span><span class="sxs-lookup"><span data-stu-id="32d1b-112">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="32d1b-113">하지만 이기도 다른 컨트롤이 컨트롤 및 애니메이션을 사용 하 여 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32d1b-113">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="steps"></a><span data-ttu-id="32d1b-114">단계</span><span class="sxs-lookup"><span data-stu-id="32d1b-114">Steps</span></span>

<span data-ttu-id="32d1b-115">첫째, 포함 된 `ScriptManager` 페이지 그런 다음 ASP.NET AJAX 라이브러리 로드 되 면 컨트롤 도구 키트를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="32d1b-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample1.aspx)]

<span data-ttu-id="32d1b-116">그러면 다음과 같은 텍스트 패널에 애니메이션 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32d1b-116">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample2.aspx)]

<span data-ttu-id="32d1b-117">패널에 대 한 연결 된 CSS 클래스에 유용한 배경 색을 정의 하 고 패널 고정된 너비를 설정할 수도:</span><span class="sxs-lookup"><span data-stu-id="32d1b-117">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](triggering-an-animation-in-another-control-cs/samples/sample3.css)]

<span data-ttu-id="32d1b-118">패널에 애니메이션 적용을 시작 하기 위해 HTML 단추가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32d1b-118">In order to start animating the panel, an HTML button is used.</span></span> <span data-ttu-id="32d1b-119">사실은 `<input type="button" />` 들이 통해 좋아하는 `<asp:Button />` 사용자가 해당 단추를 클릭 하면 포스트백 않을 것 이므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="32d1b-119">Note that `<input type="button" />` is favoured over `<asp:Button />` since we do not want a postback when the user clicks on that button.</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample4.aspx)]

<span data-ttu-id="32d1b-120">그런 다음 추가 `AnimationExtender` 페이지에서 제공 하는 `ID`, `TargetControlID` 특성과 필수 항목 이지만 `runat="server"`.</span><span class="sxs-lookup"><span data-stu-id="32d1b-120">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`.</span></span> <span data-ttu-id="32d1b-121">설정 하는 것이 반드시 `TargetControlID` 단추 (애니메이션 트리거 요소)의 ID로 패널 (애니메이션 효과가 적용 되는 요소)의 ID에 없습니다</span><span class="sxs-lookup"><span data-stu-id="32d1b-121">It is important to set `TargetControlID` to the ID of the button (the element triggering the animation), not to the ID of the panel (the element being animated)</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample5.aspx)]

<span data-ttu-id="32d1b-122">내는 `<Animations>` 노드를 일반적인 방법으로 위치 애니메이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="32d1b-122">Within the `<Animations>` node, place animations as usual.</span></span> <span data-ttu-id="32d1b-123">단추가 아닌는 패널을 변경할 수 있도록, 하려면 설정 합니다 `AnimationTarget` 내에서 모든 애니메이션 요소에 대 한 특성 `AnimationExtender`합니다.</span><span class="sxs-lookup"><span data-stu-id="32d1b-123">In order to make them change the panel, not the button, set the `AnimationTarget` attribute for every animation element within `AnimationExtender`.</span></span> <span data-ttu-id="32d1b-124">에 대 한 값 `AnimationTarget` 물론은 패널의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="32d1b-124">The value for `AnimationTarget` is the ID of the panel, of course.</span></span> <span data-ttu-id="32d1b-125">이런 방식으로 애니메이션 트리거 단추와 패널을 사용 하 여 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="32d1b-125">That way, the animations happen with the panel, not with the triggering button.</span></span> <span data-ttu-id="32d1b-126">다음은 `AnimationExtender` 이 시나리오에 대 한 태그:</span><span class="sxs-lookup"><span data-stu-id="32d1b-126">Here is the `AnimationExtender` markup for this scenario:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample6.aspx)]

<span data-ttu-id="32d1b-127">특별 한 순서는 개별 애니메이션 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="32d1b-127">Note the special order in which the individual animations appear.</span></span> <span data-ttu-id="32d1b-128">첫째, 단추 애니메이션 실행 되 면 비활성화를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="32d1b-128">First of all, the button gets deactivated once the animation runs.</span></span> <span data-ttu-id="32d1b-129">있기 때문 없습니다 `AnimationTarget` 특성을 `<EnableAction>` 원래 컨트롤 요소를이 애니메이션을 적용할: 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="32d1b-129">Since there is no `AnimationTarget` attribute in the `<EnableAction>` element, this animation is applied to the originating control: the button.</span></span> <span data-ttu-id="32d1b-130">다음 두 애니메이션 단계를 병렬로 수행 됩니다 (`<Parallel>` 요소).</span><span class="sxs-lookup"><span data-stu-id="32d1b-130">The next two animation steps shall be carried out in parallel (`<Parallel>` element).</span></span> <span data-ttu-id="32d1b-131">둘 다 해당 `AnimationTarget` 특성으로 설정 `"Panel1"`, 따라서 패널에 단추가 아닌 애니메이션을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="32d1b-131">Both have their `AnimationTarget` attributes set to `"Panel1"`, thus animating the panel, not the button.</span></span>


<span data-ttu-id="32d1b-132">[![창 애니메이션을 시작 하는 단추 마우스 클릭](triggering-an-animation-in-another-control-cs/_static/image2.png)](triggering-an-animation-in-another-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="32d1b-132">[![A mouse click on the button starts the panel animation](triggering-an-animation-in-another-control-cs/_static/image2.png)](triggering-an-animation-in-another-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="32d1b-133">창 애니메이션을 시작 하는 단추 마우스 클릭 ([클릭 하 여 큰 이미지 보기](triggering-an-animation-in-another-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="32d1b-133">A mouse click on the button starts the panel animation ([Click to view full-size image](triggering-an-animation-in-another-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="32d1b-134">[이전](disabling-actions-during-animation-cs.md)
> [다음](modifying-animations-from-the-server-side-cs.md)</span><span class="sxs-lookup"><span data-stu-id="32d1b-134">[Previous](disabling-actions-during-animation-cs.md)
[Next](modifying-animations-from-the-server-side-cs.md)</span></span>
