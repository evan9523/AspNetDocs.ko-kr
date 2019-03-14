---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: (VB) ReorderList에 포스트백 사용 | Microsoft Docs
author: wenz
description: ReorderList 컨트롤이 AJAX Control Toolkit에서 끌어서 놓기를 통해 사용자에 의해 다시 정렬할 수 있는 목록을 제공 합니다. 목록 순서를 바꿀 때마다 po...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 1e2124327a36c94db8bafbdf91f767068ac7e834
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57025430"
---
<a name="using-postbacks-with-reorderlist-vb"></a><span data-ttu-id="c4b0e-104">ReorderList에 포스트백 사용(VB)</span><span class="sxs-lookup"><span data-stu-id="c4b0e-104">Using Postbacks with ReorderList (VB)</span></span>
====================
<span data-ttu-id="c4b0e-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="c4b0e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c4b0e-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="c4b0e-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span></span>

> <span data-ttu-id="c4b0e-107">ReorderList 컨트롤이 AJAX Control Toolkit에서 끌어서 놓기를 통해 사용자에 의해 다시 정렬할 수 있는 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b0e-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="c4b0e-108">목록 순서를 바꿀 때마다 포스트백 됩니다 변경의 서버를 게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="c4b0e-108">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>


## <a name="overview"></a><span data-ttu-id="c4b0e-109">개요</span><span class="sxs-lookup"><span data-stu-id="c4b0e-109">Overview</span></span>

<span data-ttu-id="c4b0e-110">`ReorderList` AJAX Control Toolkit 컨트롤 끌어서 놓기를 통해 사용자에 의해 다시 정렬할 수 있는 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b0e-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="c4b0e-111">목록 순서를 바꿀 때마다 포스트백 됩니다 변경의 서버를 게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="c4b0e-111">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="steps"></a><span data-ttu-id="c4b0e-112">단계</span><span class="sxs-lookup"><span data-stu-id="c4b0e-112">Steps</span></span>

<span data-ttu-id="c4b0e-113">에 대 한 몇 가지 가능한 데이터 원본이 `ReorderList` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b0e-113">There are several possible data sources for the `ReorderList` control.</span></span> <span data-ttu-id="c4b0e-114">하나를 사용 하는 것을 `XmlDataSource` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b0e-114">One is to use an `XmlDataSource` control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="c4b0e-115">이 XML을 바인딩하려면는 `ReorderList` 컨트롤과 사용 포스트백, 다음과 같은 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b0e-115">In order to bind this XML to a `ReorderList` control and enable postbacks, the following attributes must be set:</span></span>

- <span data-ttu-id="c4b0e-116">`DataSourceID`: 데이터 원본 ID</span><span class="sxs-lookup"><span data-stu-id="c4b0e-116">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="c4b0e-117">`SortOrderField`: 정렬할 속성</span><span class="sxs-lookup"><span data-stu-id="c4b0e-117">`SortOrderField`: The property to sort by</span></span>
- <span data-ttu-id="c4b0e-118">`AllowReorder`: 목록 요소 순서를 변경 하려면 사용자 수 있도록 할지 여부</span><span class="sxs-lookup"><span data-stu-id="c4b0e-118">`AllowReorder`: Whether to allow the user to reorder the list elements</span></span>
- <span data-ttu-id="c4b0e-119">`PostBackOnReorder`: 목록 다시 정렬 됩니다 될 때마다 다시 게시를 만들지 여부를</span><span class="sxs-lookup"><span data-stu-id="c4b0e-119">`PostBackOnReorder`: Whether to create a postback whenever the list is rearranged</span></span>

<span data-ttu-id="c4b0e-120">컨트롤에 대 한 적절 한 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b0e-120">Here is the appropriate markup for the control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="c4b0e-121">내 합니다 `ReorderList` 를 사용 하 여 컨트롤, 데이터 원본에서 특정 데이터를 바인딩할 수 있습니다는 `Eval()` 메서드:</span><span class="sxs-lookup"><span data-stu-id="c4b0e-121">Within the `ReorderList` control, specific data from the data source may be bound using the `Eval()` method:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

<span data-ttu-id="c4b0e-122">페이지에는 임의의 위치에서 마지막 재정렬 발생 했을 때 레이블을 정보가 보관 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4b0e-122">At an arbitrary position on the page, a label will hold the information when the last reordering occurred:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="c4b0e-123">이 레이블은 포스트백 처리 서버 쪽 코드에서 텍스트를 사용 하 여 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="c4b0e-123">This label is filled with text in the server-side code, handling the postback:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

<span data-ttu-id="c4b0e-124">마지막으로, ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해는 `ScriptManager` 페이지에서 설정 해야 하는 컨트롤:</span><span class="sxs-lookup"><span data-stu-id="c4b0e-124">Finally, in order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put on the page:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]


<span data-ttu-id="c4b0e-125">[![포스트백 트리거 각 순서 변경](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c4b0e-125">[![Each reordering triggers a postback](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="c4b0e-126">각 다시 정렬 포스트백을 트리거합니다 ([클릭 하 여 큰 이미지 보기](using-postbacks-with-reorderlist-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="c4b0e-126">Each reordering triggers a postback ([Click to view full-size image](using-postbacks-with-reorderlist-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c4b0e-127">[이전](drag-and-drop-via-reorderlist-cs.md)
> [다음](drag-and-drop-via-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="c4b0e-127">[Previous](drag-and-drop-via-reorderlist-cs.md)
[Next](drag-and-drop-via-reorderlist-vb.md)</span></span>
