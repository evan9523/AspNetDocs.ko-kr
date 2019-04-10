---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
title: 컨트롤 (VB)에 애니메이션 추가 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 이 자습서에서는 방법...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c120187e-963e-4439-bb85-32771bc7f1f4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: c55bbeb383b15f4dc9cb95d25905cade1e8c5c29
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418900"
---
# <a name="adding-animation-to-a-control-vb"></a><span data-ttu-id="83fa3-104">컨트롤에 애니메이션 추가(VB)</span><span class="sxs-lookup"><span data-stu-id="83fa3-104">Adding Animation to a Control (VB)</span></span>

<span data-ttu-id="83fa3-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="83fa3-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="83fa3-106">[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="83fa3-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)</span></span>

> <span data-ttu-id="83fa3-107">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="83fa3-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="83fa3-108">이 자습서에서는 이러한 애니메이션을 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="83fa3-108">This tutorial shows how to set up such an animation.</span></span>


## <a name="overview"></a><span data-ttu-id="83fa3-109">개요</span><span class="sxs-lookup"><span data-stu-id="83fa3-109">Overview</span></span>

<span data-ttu-id="83fa3-110">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="83fa3-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="83fa3-111">이 자습서에서는 이러한 애니메이션을 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="83fa3-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="83fa3-112">단계</span><span class="sxs-lookup"><span data-stu-id="83fa3-112">Steps</span></span>

<span data-ttu-id="83fa3-113">첫 번째 단계는 일반적으로 포함 합니다 `ScriptManager` 페이지에서 ASP.NET AJAX library가 로드 하 고 컨트롤 도구 키트를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="83fa3-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample1.aspx)]

<span data-ttu-id="83fa3-114">이 시나리오에서는 애니메이션 패널 다음과 같이 표시 됩니다는 텍스트에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="83fa3-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample2.aspx)]

<span data-ttu-id="83fa3-115">패널에 대 한 연결 된 CSS 클래스에는 배경 색과 너비를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="83fa3-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-vb/samples/sample3.css)]

<span data-ttu-id="83fa3-116">필요한 up, 다음은 `AnimationExtender`합니다.</span><span class="sxs-lookup"><span data-stu-id="83fa3-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="83fa3-117">입력 한 후는 `ID` 및 일반적인 `runat="server"`, `TargetControlID` 특성 컨트롤에 여기서는 패널에서 애니메이션 효과를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83fa3-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample4.aspx)]

<span data-ttu-id="83fa3-118">하지만 완전히 현재 Visual Studio의 IntelliSense에서 지원 하는 XML 구문을 사용 하 여 전체 애니메이션을 선언적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="83fa3-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="83fa3-119">루트 노드는 `<Animations>;` 이 노드 내에서 여러 이벤트는 사용할 수 있는 애니메이션의 현재 위치를 take(s) 하는 경우를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="83fa3-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- `OnClick` <span data-ttu-id="83fa3-120">(마우스 클릭)</span><span class="sxs-lookup"><span data-stu-id="83fa3-120">(mouse click)</span></span>
- `OnHoverOut` <span data-ttu-id="83fa3-121">(경우 마우스가 컨트롤)</span><span class="sxs-lookup"><span data-stu-id="83fa3-121">(when the mouse leaves a control)</span></span>
- `OnHoverOver` <span data-ttu-id="83fa3-122">(컨트롤 위로 마우스를 가져가면 중지는 `OnHoverOut` 애니메이션)</span><span class="sxs-lookup"><span data-stu-id="83fa3-122">(when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- `OnLoad` <span data-ttu-id="83fa3-123">(때 페이지 로드 된)</span><span class="sxs-lookup"><span data-stu-id="83fa3-123">(when the page has been loaded)</span></span>
- `OnMouseOut` <span data-ttu-id="83fa3-124">(경우 마우스가 컨트롤)</span><span class="sxs-lookup"><span data-stu-id="83fa3-124">(when the mouse leaves a control)</span></span>
- `OnMouseOver` <span data-ttu-id="83fa3-125">(컨트롤 위로 마우스를 가져가면 중지 하지 않습니다는 `OnMouseOut` 애니메이션)</span><span class="sxs-lookup"><span data-stu-id="83fa3-125">(when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="83fa3-126">프레임 워크를 각각 자체 XML 요소로 표시 애니메이션 집합이 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="83fa3-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="83fa3-127">선택 영역은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="83fa3-127">Here is a selection:</span></span>

- `<Color>` <span data-ttu-id="83fa3-128">(색을 변경합니다.)</span><span class="sxs-lookup"><span data-stu-id="83fa3-128">(changing a color)</span></span>
- `<FadeIn>` <span data-ttu-id="83fa3-129">(페이드)</span><span class="sxs-lookup"><span data-stu-id="83fa3-129">(fading in)</span></span>
- `<FadeOut>` <span data-ttu-id="83fa3-130">(페이드)</span><span class="sxs-lookup"><span data-stu-id="83fa3-130">(fading out)</span></span>
- `<Property>` <span data-ttu-id="83fa3-131">(컨트롤의 속성을 변경합니다.)</span><span class="sxs-lookup"><span data-stu-id="83fa3-131">(changing a control's property)</span></span>
- `<Pulse>` <span data-ttu-id="83fa3-132">(pulsating)</span><span class="sxs-lookup"><span data-stu-id="83fa3-132">(pulsating)</span></span>
- `<Resize>` <span data-ttu-id="83fa3-133">(크기 변경)</span><span class="sxs-lookup"><span data-stu-id="83fa3-133">(changing the size)</span></span>
- `<Scale>` <span data-ttu-id="83fa3-134">(비례적으로 크기 변경)</span><span class="sxs-lookup"><span data-stu-id="83fa3-134">(proportionally changing the size)</span></span>

<span data-ttu-id="83fa3-135">이 예제에서는 패널은 페이드 아웃을 적용 합니다. 애니메이션 1.5 시간 (초)을 사용 해야 (`Duration` 특성), 초 당 24 프레임 (애니메이션 단계)을 표시 (`Fps` 특성).</span><span class="sxs-lookup"><span data-stu-id="83fa3-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attribute).</span></span> <span data-ttu-id="83fa3-136">전체 태그를 다음과 같습니다는 `AnimationExtender` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="83fa3-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample5.aspx)]

<span data-ttu-id="83fa3-137">이 스크립트를 실행 하면 패널이 표시 되 고 1.5 명의 초에 페이드 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="83fa3-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>


[![T<span data-ttu-id="83fa3-138">그 패널 페이드아웃은]</span><span class="sxs-lookup"><span data-stu-id="83fa3-138">he panel is fading out]</span></span>(adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)

<span data-ttu-id="83fa3-139">패널은 페이드아웃 ([클릭 하 여 큰 이미지 보기](adding-animation-to-a-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="83fa3-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="83fa3-140">[이전](dynamically-controlling-updatepanel-animations-cs.md)
> [다음](executing-several-animations-at-the-same-time-vb.md)</span><span class="sxs-lookup"><span data-stu-id="83fa3-140">[Previous](dynamically-controlling-updatepanel-animations-cs.md)
[Next](executing-several-animations-at-the-same-time-vb.md)</span></span>
