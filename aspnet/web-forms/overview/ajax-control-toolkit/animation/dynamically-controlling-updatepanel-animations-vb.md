---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
title: UpdatePanel 애니메이션 (VB)을 동적으로 제어 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 내용에 대 한 프로그램...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: bea66072-59b6-42b4-98fa-211812f5925f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
msc.type: authoredcontent
ms.openlocfilehash: 223fad7013a53212c0c822a87bd3e2fcc0a5f17f
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59408955"
---
# <a name="dynamically-controlling-updatepanel-animations-vb"></a><span data-ttu-id="305d3-104">UpdatePanel 애니메이션을 동적으로 제어(VB)</span><span class="sxs-lookup"><span data-stu-id="305d3-104">Dynamically Controlling UpdatePanel Animations (VB)</span></span>

<span data-ttu-id="305d3-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="305d3-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="305d3-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="305d3-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)</span></span>

> <span data-ttu-id="305d3-107">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="305d3-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="305d3-108">UpdatePanel의 내용에 대 한 특별 한 extender를 있는 애니메이션 프레임 워크에 크게 의존 합니다. UpdatePanelAnimation.</span><span class="sxs-lookup"><span data-stu-id="305d3-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="305d3-109">UpdatePanel 트리거와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305d3-109">It can also work together with UpdatePanel triggers.</span></span>


## <a name="overview"></a><span data-ttu-id="305d3-110">개요</span><span class="sxs-lookup"><span data-stu-id="305d3-110">Overview</span></span>

<span data-ttu-id="305d3-111">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="305d3-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="305d3-112">내용에 대 한는 `UpdatePanel`, 애니메이션 프레임 워크에 크게 의존 하는 특별 한 extender 존재: `UpdatePanelAnimation`합니다.</span><span class="sxs-lookup"><span data-stu-id="305d3-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="305d3-113">함께 사용할 수도 있습니다 `UpdatePanel` 트리거.</span><span class="sxs-lookup"><span data-stu-id="305d3-113">It can also work together with `UpdatePanel` triggers.</span></span>

## <a name="steps"></a><span data-ttu-id="305d3-114">단계</span><span class="sxs-lookup"><span data-stu-id="305d3-114">Steps</span></span>

<span data-ttu-id="305d3-115">첫 번째 단계는 일반적으로 포함 합니다 `ScriptManager` 페이지에서 ASP.NET AJAX library가 로드 하 고 컨트롤 도구 키트를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="305d3-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample1.aspx)]

<span data-ttu-id="305d3-116">이 시나리오에서는 애니메이션의 현재 디스플레이에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="305d3-116">The animation in this scenario will be applied to a display of the current time.</span></span> <span data-ttu-id="305d3-117">이 정보를 사용 하 여 레이블에 쓸 수는 `Page_Load()` 메서드 또는 다음 인라인 코드를 사용 (간단히):</span><span class="sxs-lookup"><span data-stu-id="305d3-117">This information can be written into a label using the `Page_Load()` method, or (for the sake of simplicity) the following inline code is used:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample2.aspx)]

<span data-ttu-id="305d3-118">또한에 업데이트를 트리거하는 단추를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="305d3-118">Also, a button to trigger updating the time is created:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample3.aspx)]

<span data-ttu-id="305d3-119">이 코드는 다음을 배치 합니다 `<ContentTemplate>` 부분을 `UpdatePanel` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="305d3-119">This code is then put into the `<ContentTemplate>` section of an `UpdatePanel` element.</span></span> <span data-ttu-id="305d3-120">패널의 `UpdateMode` 특성으로 설정 되어 있어야 `"Conditional"`가 트리거만 패널의 콘텐츠를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305d3-120">The panel's `UpdateMode` attribute must be set to `"Conditional"`, since only triggers may update the panel's contents.</span></span> <span data-ttu-id="305d3-121">에 `<Triggers>` 의 섹션을 `UpdatePanel`, 비동기 포스트백 트리거를 만들고 연결를 `Click` 단추의 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="305d3-121">In the `<Triggers>` section of the `UpdatePanel`, an asynchronous postback trigger is created and tied to the `Click` event of the button.</span></span> <span data-ttu-id="305d3-122">따라서 사용자가 단추를 클릭할 경우의 `UpdatePanel` 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="305d3-122">Thus, if the user clicks on the button, the `UpdatePanel` is refreshed.</span></span> <span data-ttu-id="305d3-123">여기에 대 한 태그는 `UpdatePanel` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="305d3-123">Here is the markup for the `UpdatePanel` control:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample4.aspx)]

<span data-ttu-id="305d3-124">마지막으로 `UpdatePanelAnimationExtender` 구성 해야 합니다. 설정 된 `TargetControlID` 패널의 id 특성 및 extender에서 애니메이션을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="305d3-124">Finally, the `UpdatePanelAnimationExtender` must be configured: Set the `TargetControlID` attribute to the ID of the panel, and define an animation within the extender.</span></span> <span data-ttu-id="305d3-125">페이딩 만드는 업데이트 된 시간에 유용한 시각적 강조를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="305d3-125">Fading in makes sense, which creates a nice visual emphasis on the updated time.</span></span> <span data-ttu-id="305d3-126">Extender 태그는 다음과 같은 다음 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="305d3-126">Your extender markup may then look like this:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample5.aspx)]

<span data-ttu-id="305d3-127">브라우저에서 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="305d3-127">Run the file in the browser.</span></span> <span data-ttu-id="305d3-128">단추를 클릭할 때마다 현재 항상 1 초 동안 페이드 인 패널에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="305d3-128">Whenever you click on the button, the current time is shown in the panel, always fading in for the duration of one second.</span></span>


<span data-ttu-id="305d3-129">[![현재는 페이드 인](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="305d3-129">[![The current time is fading in](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)</span></span>

<span data-ttu-id="305d3-130">현재 시간 페이딩 됩니다 ([클릭 하 여 큰 이미지 보기](dynamically-controlling-updatepanel-animations-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="305d3-130">The current time is fading in ([Click to view full-size image](dynamically-controlling-updatepanel-animations-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="305d3-131">이전</span><span class="sxs-lookup"><span data-stu-id="305d3-131">Previous</span></span>](animating-an-updatepanel-control-vb.md)
