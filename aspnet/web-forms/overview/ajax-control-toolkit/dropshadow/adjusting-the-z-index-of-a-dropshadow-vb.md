---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
title: (VB) DropShadow의 Z-인덱스 조정 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit에서 DropShadow 컨트롤 그림자를 사용 하 여 패널을 확장합니다. 그러나이 섀도 경우에 따라 설치에 대 한 다른 컨트롤을 사용 하 여 충돌 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ecb004b5-82c0-44fb-bcaf-233fffac6195
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
msc.type: authoredcontent
ms.openlocfilehash: b01913b3ad3291d90bdf9455c3d35bb7b36b3f28
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59415247"
---
# <a name="adjusting-the-z-index-of-a-dropshadow-vb"></a><span data-ttu-id="5faa9-104">DropShadow의 Z-인덱스 조정(VB)</span><span class="sxs-lookup"><span data-stu-id="5faa9-104">Adjusting the Z-Index of a DropShadow (VB)</span></span>

<span data-ttu-id="5faa9-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="5faa9-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5faa9-106">[코드를 다운로드](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="5faa9-106">[Download Code](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1VB.pdf)</span></span>

> <span data-ttu-id="5faa9-107">AJAX Control Toolkit에서 DropShadow 컨트롤 그림자를 사용 하 여 패널을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="5faa9-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="5faa9-108">그러나이 섀도 ASP.NET Menu 컨트롤 예를 들어 다른 컨트롤과 경우에 따라 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="5faa9-108">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="5faa9-109">때 메뉴 항목 팝업 뒤에 그림자 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5faa9-109">When a menu entry pops up, it appears behind the drop shadow.</span></span>


## <a name="overview"></a><span data-ttu-id="5faa9-110">개요</span><span class="sxs-lookup"><span data-stu-id="5faa9-110">Overview</span></span>

<span data-ttu-id="5faa9-111">AJAX Control Toolkit에서 DropShadow 컨트롤 그림자를 사용 하 여 패널을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="5faa9-111">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="5faa9-112">그러나이 섀도 ASP.NET Menu 컨트롤 예를 들어 다른 컨트롤과 경우에 따라 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="5faa9-112">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="5faa9-113">때 메뉴 항목 팝업 뒤에 그림자 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5faa9-113">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="steps"></a><span data-ttu-id="5faa9-114">단계</span><span class="sxs-lookup"><span data-stu-id="5faa9-114">Steps</span></span>

<span data-ttu-id="5faa9-115">코드 표시 되도록 효과 대 한 충분 한 텍스트를 포함 하는 패널 수 있도록 충분 한 텍스트가 포함 된 패널 자체를 사용 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5faa9-115">The code commences with the Panel itself, containing enough text so that the panel contains enough text for the effect to be visible:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample1.aspx)]

<span data-ttu-id="5faa9-116">다른 패널 바로 앞에 삽입 된 `panelShadow` 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="5faa9-116">Another panel is placed directly before the `panelShadow` panel.</span></span> <span data-ttu-id="5faa9-117">메뉴 항목 위에 나타나도록 가로 방향으로 메뉴가 포함 (또는 대신: 아래)를 `dropShadow` 패널):</span><span class="sxs-lookup"><span data-stu-id="5faa9-117">It contains a menu with horizontal orientation so that menu entries appear over (or rather: under) the `dropShadow` panel):</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample2.aspx)]

<span data-ttu-id="5faa9-118">그런 다음, `DropShadowExtender` 확장에 추가 되는 `panelShadow` 그림자 효과 사용 하 여 패널:</span><span class="sxs-lookup"><span data-stu-id="5faa9-118">Then, the `DropShadowExtender` is added to extend the `panelShadow` panel with a drop shadow effect:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample3.aspx)]

<span data-ttu-id="5faa9-119">마지막으로 ASP.NET AJAX `ScriptManager` 제어 하려면 컨트롤 도구 키트를 사용 하면:</span><span class="sxs-lookup"><span data-stu-id="5faa9-119">Finally, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample4.aspx)]

<span data-ttu-id="5faa9-120">이 스크립트를 실행 하면 메뉴 항목 패널 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5faa9-120">When you run this script, the menu entries appear underneath the panel.</span></span> <span data-ttu-id="5faa9-121">하지만 메뉴는 CSS 클래스를 사용 `panel` 만 있는 두 가지 다른 패널 앞에 표시 되는 요소를 정의 하려면:</span><span class="sxs-lookup"><span data-stu-id="5faa9-121">However the menu uses the CSS class `panel` where you just have to define two things to make elements appear in front of the other panel:</span></span>

- <span data-ttu-id="5faa9-122">상대 위치</span><span class="sxs-lookup"><span data-stu-id="5faa9-122">Relative positioning</span></span>
- <span data-ttu-id="5faa9-123">양의 z-인덱스</span><span class="sxs-lookup"><span data-stu-id="5faa9-123">A positive z-index</span></span>

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample5.css)]

<span data-ttu-id="5faa9-124">그런 다음, `DropShadowExtender` 컨트롤 메뉴 컨트롤을 사용 하 여 더 이상 충돌 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5faa9-124">Then, the `DropShadowExtender` control does not conflict any longer with the Menu control.</span></span>


[![B<span data-ttu-id="5faa9-125">전: 메뉴 항목이 표시 되지 않으면]</span><span class="sxs-lookup"><span data-stu-id="5faa9-125">efore: The menu entry is not visible]</span></span>(adjusting-the-z-index-of-a-dropshadow-vb/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image1.png)

<span data-ttu-id="5faa9-126">이전: 메뉴 항목이 표시 되지 않습니다 ([클릭 하 여 큰 이미지 보기](adjusting-the-z-index-of-a-dropshadow-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="5faa9-126">Before: The menu entry is not visible ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-vb/_static/image3.png))</span></span>


[![A<span data-ttu-id="5faa9-127">뒤: 메뉴 항목 표시]</span><span class="sxs-lookup"><span data-stu-id="5faa9-127">fter: The menu entry appears]</span></span>(adjusting-the-z-index-of-a-dropshadow-vb/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image4.png)

<span data-ttu-id="5faa9-128">이후: 메뉴 항목이 표시 됩니다 ([클릭 하 여 큰 이미지 보기](adjusting-the-z-index-of-a-dropshadow-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="5faa9-128">After: The menu entry appears ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5faa9-129">[이전](manipulating-dropshadow-properties-from-client-code-cs.md)
> [다음](manipulating-dropshadow-properties-from-client-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="5faa9-129">[Previous](manipulating-dropshadow-properties-from-client-code-cs.md)
[Next](manipulating-dropshadow-properties-from-client-code-vb.md)</span></span>
