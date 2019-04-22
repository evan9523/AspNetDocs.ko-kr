---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
title: (VB) ModalPopup에서 포스트백 처리 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 ModalPopup 컨트롤 클라이언트 쪽 의미를 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. Pos 때 특별히 주의 해야 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f70ac2b3-900f-40fa-858f-ab057904506b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: add305855d876b5033bbd7921ad24b5e840b9acc
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59386400"
---
# <a name="handling-postbacks-from-a-modalpopup-vb"></a><span data-ttu-id="2a702-104">ModalPopup에서 포스트백 처리(VB)</span><span class="sxs-lookup"><span data-stu-id="2a702-104">Handling Postbacks from a ModalPopup (VB)</span></span>

<span data-ttu-id="2a702-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="2a702-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="2a702-106">[코드를 다운로드](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="2a702-106">[Download Code](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)</span></span>

> <span data-ttu-id="2a702-107">AJAX Control Toolkit의 ModalPopup 컨트롤 클라이언트 쪽 의미를 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a702-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="2a702-108">팝업 내에서 다시 게시를 만들 때 특별히 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a702-108">Special care must be taken when a postback is created from within the popup.</span></span>


## <a name="overview"></a><span data-ttu-id="2a702-109">개요</span><span class="sxs-lookup"><span data-stu-id="2a702-109">Overview</span></span>

<span data-ttu-id="2a702-110">AJAX Control Toolkit의 ModalPopup 컨트롤 클라이언트 쪽 의미를 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a702-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="2a702-111">팝업 내에서 다시 게시를 만들 때 특별히 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a702-111">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="2a702-112">단계</span><span class="sxs-lookup"><span data-stu-id="2a702-112">Steps</span></span>

<span data-ttu-id="2a702-113">ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):</span><span class="sxs-lookup"><span data-stu-id="2a702-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample1.aspx)]

<span data-ttu-id="2a702-114">다음으로 모달 팝업으로 사용 되는 패널을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a702-114">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="2a702-115">사용자 이름 및 전자 메일 주소를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a702-115">There, the user can enter a name and an email address.</span></span> <span data-ttu-id="2a702-116">단추 정보를 저장 하 고 팝업을 닫습니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a702-116">A button is used to close the popup and save the information.</span></span> <span data-ttu-id="2a702-117">`OnClick` 특성을 설정 하 여 포스트백이이 단추를 클릭할 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a702-117">Note that the `OnClick` attribute is set so that a postback occurs when this button is clicked:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample2.aspx)]

<span data-ttu-id="2a702-118">정확히 동일한 정보에 대 한 두 레이블의 페이지 자체 구성 됩니다: 이름 및 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="2a702-118">The page itself consists of two labels for exactly the same information: name and email address.</span></span> <span data-ttu-id="2a702-119">모달 팝업을 트리거할 단추 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a702-119">A button is used to trigger the modal popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample3.aspx)]

<span data-ttu-id="2a702-120">팝업 표시를 하려면 추가 `ModalPopupExtender` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a702-120">In order to make the popup appear, add the `ModalPopupExtender` control.</span></span> <span data-ttu-id="2a702-121">설정 된 `PopupControlID` 패널의 id 특성 및 `TargetControlID` 단추의 id:</span><span class="sxs-lookup"><span data-stu-id="2a702-121">Set the `PopupControlID` attribute to the panel's ID and `TargetControlID` to the button's ID:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample4.aspx)]

<span data-ttu-id="2a702-122">이제 때마다 합니다 `Save` 모달 팝업 내의 단추 서버 쪽 `SaveData()` 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a702-122">Now whenever the `Save` button within the modal popup is clicked, the server-side `SaveData()` method is executed.</span></span> <span data-ttu-id="2a702-123">여기에서 데이터 저장소에 입력 된 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a702-123">There, you could save the entered data in a data store.</span></span> <span data-ttu-id="2a702-124">간단히 하기 위해 새 데이터 레이블에 출력만:</span><span class="sxs-lookup"><span data-stu-id="2a702-124">For the sake of simplicity, the new data is just output in the label:</span></span>

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample5.vb)]

<span data-ttu-id="2a702-125">또한 현재 이름 및 전자 메일을 사용 하 여 모달 팝업에 textbox 컨트롤이 채워야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a702-125">Also, the textbox controls within the modal popup should be filled with the current name and email.</span></span> <span data-ttu-id="2a702-126">그러나는 필요한 경우에 포스트백이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a702-126">However this is only necessary when no postback occurs.</span></span> <span data-ttu-id="2a702-127">다시 게시 인 경우 ASP.NET viewstate 기능을 자동으로 적절 한 값을 사용 하 여 텍스트 상자를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="2a702-127">If there is a postback, the ASP.NET viewstate feature will automatically fill the textboxes with the appropriate values.</span></span>

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample6.vb)]


<span data-ttu-id="2a702-128">[![모달 팝업은 포스트백을 발생 시키는](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2a702-128">[![The modal popup causes a postback](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)</span></span>

<span data-ttu-id="2a702-129">모달 팝업은 포스트백을 발생 시키는 ([클릭 하 여 큰 이미지 보기](handling-postbacks-from-a-modalpopup-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="2a702-129">The modal popup causes a postback ([Click to view full-size image](handling-postbacks-from-a-modalpopup-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2a702-130">[이전](using-modalpopup-with-a-repeater-control-vb.md)
> [다음](positioning-a-modalpopup-vb.md)</span><span class="sxs-lookup"><span data-stu-id="2a702-130">[Previous](using-modalpopup-with-a-repeater-control-vb.md)
[Next](positioning-a-modalpopup-vb.md)</span></span>
