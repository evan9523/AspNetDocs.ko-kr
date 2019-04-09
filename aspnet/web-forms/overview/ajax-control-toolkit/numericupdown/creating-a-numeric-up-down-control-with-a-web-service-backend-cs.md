---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
title: 웹 서비스 백 엔드 (C#)를 사용 하 여 숫자 위로/아래로 컨트롤 만들기 | Microsoft Docs
author: wenz
description: 확인 상자에 값을 입력 하는 사용자를 대신 숫자 위로/아래로 컨트롤 (Windows 및 기타 운영 체제에 있는) 점점 더 많은 c 증명 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c99bbc72-d4de-41ed-92a4-9a4632368363
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
msc.type: authoredcontent
ms.openlocfilehash: b8160c6f5ac090e120e86f4273749b756857967e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59385711"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-c"></a><span data-ttu-id="084ee-103">웹 서비스 백 엔드를 사용하여 숫자 위로/아래로 컨트롤 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="084ee-103">Creating a Numeric Up/Down Control with a Web Service Backend (C#)</span></span>

<span data-ttu-id="084ee-104">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="084ee-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="084ee-105">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="084ee-105">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)</span></span>

> <span data-ttu-id="084ee-106">확인 상자에 값을 입력 하는 사용자를 대신 숫자 위로/아래로 컨트롤 (존재 하는 Windows 및 기타 운영 체제에서) 증명 하는 점점 더 많은 편리 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="084ee-106">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="084ee-107">기본적으로 NumericUpDown 컨트롤 항상 만큼 늘어나거나 줄어들 값 1, 하지만 더 많은 유연성을 증명 하는 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="084ee-107">By default, the NumericUpDown control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>


## <a name="overview"></a><span data-ttu-id="084ee-108">개요</span><span class="sxs-lookup"><span data-stu-id="084ee-108">Overview</span></span>

<span data-ttu-id="084ee-109">확인 상자에 값을 입력 하는 사용자를 대신 숫자 위로/아래로 컨트롤 (존재 하는 Windows 및 기타 운영 체제에서) 증명 하는 점점 더 많은 편리 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="084ee-109">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="084ee-110">기본적으로 `NumericUpDown` 컨트롤 항상 만큼 늘어나거나 줄어들 값 1, 하지만 더 많은 유연성을 증명 하는 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="084ee-110">By default, the `NumericUpDown` control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="084ee-111">단계</span><span class="sxs-lookup"><span data-stu-id="084ee-111">Steps</span></span>

<span data-ttu-id="084ee-112">ASP.NET AJAX Control Toolkit에 포함 된 `NumericUpDown` 텍스트 상자에 두 개의 단추를 자동으로 추가 하는 extender: 감소에 대 한 해당 값을 높이기 위한 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="084ee-112">The ASP.NET AJAX Control Toolkit contains the `NumericUpDown` extender which automatically adds two buttons to a text box: One for increasing its value, one for decreasing it.</span></span> <span data-ttu-id="084ee-113">그러나 컨트롤을 웹 서비스 호출 (또는 페이지 메서드 호출)도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="084ee-113">However the control also supports a web service call (or page method call).</span></span> <span data-ttu-id="084ee-114">때마다를 위로 또는 아래로 단추를 클릭 하면 JavaScript 코드 웹 서버에 연결 하 고 있는 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="084ee-114">Whenever the up or down button is clicked, the JavaScript code connects to the web server and executes a method there.</span></span> <span data-ttu-id="084ee-115">메서드 서명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="084ee-115">The method signature is the following one:</span></span>

[!code-csharp[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample1.cs)]

<span data-ttu-id="084ee-116">`current` 인수는 텍스트 상자; 현재 값을 `tag` 특성은 속성으로 설정할 수 있는 추가 컨텍스트 데이터를 `NumericUpDown` extender (하지만 필요 하지 않습니다).</span><span class="sxs-lookup"><span data-stu-id="084ee-116">The `current` argument is the current value in the text box; the `tag` attribute is additional context data that can be set as a property of the `NumericUpDown` extender (but is not required).</span></span>

<span data-ttu-id="084ee-117">이 샘플에서는 숫자 위로/아래로 컨트롤은 2의 거듭제곱 값 허용: 1, 2, 4, 8, 16, 32, 64 및 등입니다.</span><span class="sxs-lookup"><span data-stu-id="084ee-117">For this sample, the numeric up/down control shall only allow values that are powers of two: 1, 2, 4, 8, 16, 32, 64, and so on.</span></span> <span data-ttu-id="084ee-118">따라서 사용자가 값을 늘려야 하는 경우 실행 해야 이전 값을 double; 또 다른 방법은 두 값을 나누려고 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="084ee-118">Therefore, the method executed when the user wants to increase the value must double the old value; the other method must divide value by two.</span></span> <span data-ttu-id="084ee-119">이것이 완전 한 웹 서비스:</span><span class="sxs-lookup"><span data-stu-id="084ee-119">So here is the complete web service:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample2.aspx)]

<span data-ttu-id="084ee-120">마지막으로 새로운 ASP.NET 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="084ee-120">Finally, create a new ASP.NET page.</span></span> <span data-ttu-id="084ee-121">해야 일반적으로 `ScriptManager` 컨트롤을 `TextBox` 컨트롤 및 `NumericUpDownExtender` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="084ee-121">As usual, you need a `ScriptManager` control, a `TextBox` control and a `NumericUpDownExtender` control.</span></span> <span data-ttu-id="084ee-122">후자의 경우 웹 서비스 정보를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="084ee-122">For the latter, you have to provide the web service information:</span></span>

- `ServiceDownMethod` <span data-ttu-id="084ee-123">아래쪽의 이름을 웹 메서드 또는 메서드를 페이지</span><span class="sxs-lookup"><span data-stu-id="084ee-123">name of the down web method or page method</span></span>
- `ServiceDownPath` <span data-ttu-id="084ee-124">아래쪽 서비스 메서드를 사용 하 여 웹 서비스에 대 한 경로 페이지 메서드를 사용 하는 경우를 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="084ee-124">path to the web service with the down service method; omit if you are using a page method</span></span>
- `ServiceUpMethod` <span data-ttu-id="084ee-125">위쪽의 이름을 웹 메서드 또는 메서드를 페이지</span><span class="sxs-lookup"><span data-stu-id="084ee-125">name of the up web method or page method</span></span>
- `ServiceUpPath` <span data-ttu-id="084ee-126">최신 서비스 메서드를 사용 하 여 웹 서비스에 대 한 경로 페이지 메서드를 사용 하는 경우를 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="084ee-126">path to the web service with the up service method; omit if you are using a page method</span></span>

<span data-ttu-id="084ee-127">페이지의 전체 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="084ee-127">Here is the complete markup for the page:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample3.aspx)]

<span data-ttu-id="084ee-128">페이지를 실행 하는 방법을 텍스트 상자에 값을 항상 두 배로 위쪽 단추를 클릭 하 고 아래쪽 단추를 클릭할 때 절반이 됩니다 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="084ee-128">If you run the page, notice how the value in the text box always doubles when you click on the upper button, and is halved when you click on the lower button.</span></span>


[![O<span data-ttu-id="084ee-129">2의 제곱 된 있는 숫자 표시]</span><span class="sxs-lookup"><span data-stu-id="084ee-129">nly numbers that are a power of 2 appear]</span></span>(creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)

<span data-ttu-id="084ee-130">2의 제곱 된 번호만 표시 ([클릭 하 여 큰 이미지 보기](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="084ee-130">Only numbers that are a power of 2 appear ([Click to view full-size image](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="084ee-131">다음</span><span class="sxs-lookup"><span data-stu-id="084ee-131">Next</span></span>](creating-a-numeric-up-down-control-with-a-web-service-backend-vb.md)
