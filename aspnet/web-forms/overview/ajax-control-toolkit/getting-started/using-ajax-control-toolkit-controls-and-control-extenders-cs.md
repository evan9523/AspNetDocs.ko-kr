---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: AJAX 컨트롤 도구 키트 컨트롤 및 컨트롤 Extenders 사용 (C#)를 사용 하 여 | Microsoft Docs
author: microsoft
description: ASP.NET 페이지에 AJAX Control Toolkit 컨트롤 및 extender를 추가 하는 방법에 알아봅니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 82fae91e40ec2f1508fe5c82992eeef4abc4e19a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59419225"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a><span data-ttu-id="b42e5-103">Using AJAX 컨트롤 도구 키트 컨트롤 및 컨트롤 Extender 사용(C#)</span><span class="sxs-lookup"><span data-stu-id="b42e5-103">Using AJAX Control Toolkit Controls and Control Extenders (C#)</span></span>

<span data-ttu-id="b42e5-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b42e5-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="b42e5-105">ASP.NET 페이지에 AJAX Control Toolkit 컨트롤 및 extender를 추가 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-105">Learn how to add AJAX Control Toolkit controls and extenders to your ASP.NET pages.</span></span>


<span data-ttu-id="b42e5-106">AJAX Control Toolkit 컨트롤 및 컨트롤 extenders 집합이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-106">The AJAX Control Toolkit contains a set of controls and control extenders.</span></span> <span data-ttu-id="b42e5-107">이 간략 한 자습서는 ASP.NET 페이지에 컨트롤 및 컨트롤 extenders 사용을 추가 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-107">In this brief tutorial, you learn how to add both controls and control extenders to an ASP.NET page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="b42e5-108">AJAX Control Toolkit을 설치 하 고 Visual Studio/Visual Web Developer 도구 상자에 AJAX Control Toolkit을 추가 하는 방법은 자습서를 참조 하세요 [AJAX Control Toolkit 시작](get-started-with-the-ajax-control-toolkit-cs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-108">For instructions on installing the AJAX Control Toolkit and adding the AJAX Control Toolkit to the Visual Studio/Visual Web Developer toolbox, see the tutorial [Get Started with the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs.md).</span></span>


## <a name="using-ajax-control-toolkit-controls"></a><span data-ttu-id="b42e5-109">AJAX 컨트롤 도구 키트 컨트롤을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b42e5-109">Using AJAX Control Toolkit Controls</span></span>

<span data-ttu-id="b42e5-110">AJAX Control Toolkit 컨트롤을 일반적인 ASP.NET 컨트롤 처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-110">An AJAX Control Toolkit control works just like a normal ASP.NET control.</span></span> <span data-ttu-id="b42e5-111">ASP.NET 페이지를 도구 상자에서 컨트롤을 끌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-111">You can drag the control from the toolbox onto an ASP.NET page.</span></span> <span data-ttu-id="b42e5-112">디자인 뷰 또는 원본 보기 페이지로 컨트롤을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-112">You can add the control to the page in either Design view or Source view.</span></span>

<span data-ttu-id="b42e5-113">AJAX Control Toolkit에서 컨트롤을 사용 하는 경우 특별 한 요구 사항 중 하나가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-113">There is one special requirement when using the controls from the AJAX Control Toolkit.</span></span> <span data-ttu-id="b42e5-114">페이지에 ScriptManager 컨트롤을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-114">The page must contain a ScriptManager control.</span></span> <span data-ttu-id="b42e5-115">ScriptManager 컨트롤은 모두 AJAX Control Toolkit 컨트롤에 필요한 필요한 JavaScript를 비롯 한 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-115">The ScriptManager control is responsible for including all of the necessary JavaScript required by the AJAX Control Toolkit controls.</span></span>

<span data-ttu-id="b42e5-116">예를 들어, AJAX Control Toolkit 탭에는 편집기 컨트롤 이라는 컨트롤을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-116">For example, the AJAX Control Toolkit tab includes a control named the Editor control.</span></span> <span data-ttu-id="b42e5-117">이 컨트롤에 풍부한 HTML 편집기를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-117">This control displays a rich HTML editor.</span></span> <span data-ttu-id="b42e5-118">페이지에는 편집기 컨트롤을 추가 하려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-118">Follow these steps to add the Editor control to a page:</span></span>

1. <span data-ttu-id="b42e5-119">ShowEditor.aspx 라는 새로운 ASP.NET 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="b42e5-119">Create a new ASP.NET page named ShowEditor.aspx</span></span>
2. <span data-ttu-id="b42e5-120">도구 상자에서 AJAX 확장명 탭 아래 ScriptManager 컨트롤을 선택 하 고 컨트롤을 페이지로 끌어다 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-120">Select the ScriptManager control from beneath the AJAX Extensions tab in the toolbox and drag the control onto the page.</span></span>
3. <span data-ttu-id="b42e5-121">도구 상자에서 AJAX Control Toolkit 탭 아래 편집기 컨트롤을 선택 하 고 컨트롤을 페이지로 끌어 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="b42e5-121">Select the Editor control from beneath the AJAX Control Toolkit tab in the toolbox and drag the control onto the page (see Figure 1).</span></span> <span data-ttu-id="b42e5-122">디자이너는 그림 2와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-122">The Designer should look like Figure 2.</span></span>
4. <span data-ttu-id="b42e5-123">메뉴 옵션을 선택 하 여 웹 사이트를 실행할 **디버그, 디버깅 시작** F5 키를 눌러 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-123">Run the web site by selecting the menu option **Debug, Start Debugging** or hitting the F5 key.</span></span>
5. <span data-ttu-id="b42e5-124">그림 3에는 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-124">You should see the page in Figure 3.</span></span>


<span data-ttu-id="b42e5-125">[![HTML 편집기 컨트롤 선택](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b42e5-125">[![Selecting the HTML Editor control](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)</span></span>

<span data-ttu-id="b42e5-126">**그림 01**: HTML 편집기 컨트롤 선택 ([클릭 하 여 큰 이미지 보기](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="b42e5-126">**Figure 01**: Selecting the HTML Editor control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))</span></span>


<span data-ttu-id="b42e5-127">[![ScriptManager 및 편집 컨트롤을 사용 하 여 visual Studio 디자이너](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="b42e5-127">[![Visual Studio Designer with ScriptManager and Edit control](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)</span></span>

<span data-ttu-id="b42e5-128">**그림 02**: ScriptManager 및 편집 컨트롤을 사용 하 여 visual Studio Designer ([클릭 하 여 큰 이미지 보기](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="b42e5-128">**Figure 02**: Visual Studio Designer with ScriptManager and Edit control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))</span></span>


<span data-ttu-id="b42e5-129">[![DisplayEditor.aspx 페이지](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="b42e5-129">[![The DisplayEditor.aspx page](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)</span></span>

<span data-ttu-id="b42e5-130">**그림 03**: DisplayEditor.aspx 페이지 ([클릭 하 여 큰 이미지 보기](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="b42e5-130">**Figure 03**: The DisplayEditor.aspx page([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))</span></span>


## <a name="using-ajax-control-toolkit-control-extenders"></a><span data-ttu-id="b42e5-131">AJAX 컨트롤 도구 키트 컨트롤 Extender를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b42e5-131">Using AJAX Control Toolkit Control Extenders</span></span>

<span data-ttu-id="b42e5-132">AJAX Control Toolkit 컨트롤 extenders를 사용에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-132">The AJAX Control Toolkit also contains control extenders.</span></span> <span data-ttu-id="b42e5-133">해당 이름에서 알 수 있듯이 컨트롤 extender를 기존 컨트롤의 기능을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-133">As its name suggests, a control extender extends the functionality of an existing control.</span></span> <span data-ttu-id="b42e5-134">예를 들어 ConfirmButton 컨트롤 extender는 표준 ASP.NET Button 컨트롤을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-134">For example, the ConfirmButton control extender extends the standard ASP.NET Button control.</span></span> <span data-ttu-id="b42e5-135">Extender는 단추를 클릭 하면 확인 대화 상자가 표시 되도록 단추 컨트롤의의 동작을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-135">The extender changes the Button control�s behavior so that the Button displays a confirmation dialog when you click it.</span></span>

<span data-ttu-id="b42e5-136">컨트롤 extender는 AJAX Control Toolkit 컨트롤 처럼 ScriptManager 컨트롤에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-136">A control extender, just like an AJAX Control Toolkit control, requires a ScriptManager control.</span></span> <span data-ttu-id="b42e5-137">페이지에서 컨트롤 extender를 사용 하려면 먼저 페이지에 ScriptManager 컨트롤을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-137">You must add a ScriptManager control to a page before you start using control extenders in the page.</span></span>

<span data-ttu-id="b42e5-138">컨트롤 같이 ConfirmButton extender를 사용 하려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-138">Follow these steps to use the ConfirmButton control extender:</span></span>

1. <span data-ttu-id="b42e5-139">ShowConfirmButton.aspx 라는 새로운 ASP.NET 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="b42e5-139">Create a new ASP.NET page named ShowConfirmButton.aspx</span></span>
2. <span data-ttu-id="b42e5-140">AJAX 확장명 탭 아래 페이지 컨트롤을 끌어 페이지에 ScriptManager 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-140">Add a ScriptManager control to the page by dragging the control onto the page from beneath the AJAX Extensions tab.</span></span>
3. <span data-ttu-id="b42e5-141">표준 탭 아래 단추를 도구 상자에서 디자이너 화면에 끌어 페이지에 표준 단추 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-141">Add a standard Button control to the page by dragging the Button from beneath the Standard tab in the toolbox onto the Designer surface.</span></span>
4. <span data-ttu-id="b42e5-142">클릭 합니다 **Extender 추가** 작업 옵션 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="b42e5-142">Click the **Add Extender** task option (see Figure 4).</span></span>
5. <span data-ttu-id="b42e5-143">Extender 선택 대화 상자에서 ConfirmButtonExtender 선택 (그림 5 참조) 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-143">In the Choose Extender dialog, select ConfirmButtonExtender (see Figure 5) and click the OK button.</span></span>
6. <span data-ttu-id="b42e5-144">디자이너에서 단추 컨트롤을 선택 하 고 Extender가 Button1 확장\_속성 창에서 ConfirmButtonExtender 노드 (그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="b42e5-144">Select the Button control in the Designer and expand the Extenders, Button1\_ConfirmButtonExtender node in the Properties window (see Figure 6).</span></span> <span data-ttu-id="b42e5-145">값을 할당 *실제로?* ConfirmText 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-145">Assign the value *�Really?�* to the ConfirmText property.</span></span>
7. <span data-ttu-id="b42e5-146">메뉴 옵션을 선택 하 여 페이지를 실행할 **디버그, 디버깅 시작** 또는 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-146">Run the page by selecting the menu option **Debug, Start Debugging** or hit the F5 key.</span></span>


<span data-ttu-id="b42e5-147">[![Extender 추가 작업 옵션](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="b42e5-147">[![The Add Extender task option](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)</span></span>

<span data-ttu-id="b42e5-148">**그림 04**: Extender 추가 작업 옵션 ([클릭 하 여 큰 이미지 보기](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="b42e5-148">**Figure 04**: The Add Extender task option([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))</span></span>


<span data-ttu-id="b42e5-149">[![컨트롤 같이 ConfirmButton extender를 선택합니다.](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="b42e5-149">[![Selecting the ConfirmButton control extender](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)</span></span>

<span data-ttu-id="b42e5-150">**그림 05**: 컨트롤 같이 ConfirmButton extender를 선택 하면 ([클릭 하 여 큰 이미지 보기](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="b42e5-150">**Figure 05**: Selecting the ConfirmButton control extender([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))</span></span>


<span data-ttu-id="b42e5-151">[![ConfirmButton 속성 설정](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="b42e5-151">[![Setting a ConfirmButton property](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)</span></span>

<span data-ttu-id="b42e5-152">**그림 06**: ConfirmButton 속성을 설정 ([클릭 하 여 큰 이미지 보기](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="b42e5-152">**Figure 06**: Setting a ConfirmButton property([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))</span></span>


<span data-ttu-id="b42e5-153">페이지가 열릴 때 단추가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-153">When the page opens, you should see a button.</span></span> <span data-ttu-id="b42e5-154">단추를 클릭 하면 그림 7에서 확인 대화 상자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-154">When you click the button, you get the confirmation dialog in Figure 7.</span></span>


<span data-ttu-id="b42e5-155">[![확인 대화 상자를 표시합니다.](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="b42e5-155">[![Displaying the confirmation dialog](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)</span></span>

<span data-ttu-id="b42e5-156">**그림 07**: 확인 대화 상자를 표시 합니다. ([클릭 하 여 큰 이미지 보기](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="b42e5-156">**Figure 07**: Displaying the confirmation dialog([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))</span></span>


<span data-ttu-id="b42e5-157">일반적으로 끌어 오지 않은 컨트롤 extender를 페이지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-157">Notice that you normally do not drag a control extender onto a page.</span></span> <span data-ttu-id="b42e5-158">대신 사용 합니다 **Extender 추가** extender를 페이지에 이미 추가한 컨트롤에 추가 하는 옵션을 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-158">Instead, you use the **Add Extender** task option to add an extender to a control that you have already added to a page.</span></span> <span data-ttu-id="b42e5-159">확인, 또한 컨트롤 extender 속성 설정 되는 확장 된 컨트롤의 속성 시트를 열어 합니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-159">Notice, furthermore, that you set control extender properties by opening the property sheet for the control being extended.</span></span>

<span data-ttu-id="b42e5-160">여러 컨트롤 extenders 사용 하 여 단일 ASP.NET 컨트롤을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-160">A single ASP.NET control can be extended by multiple control extenders.</span></span> <span data-ttu-id="b42e5-161">확장 된 컨트롤에 대 한 속성 시트 컨트롤과 연결 된 컨트롤 extender의 모든를 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b42e5-161">The property sheet for the control being extended will list all of the control extenders associated with the control.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b42e5-162">[이전](get-started-with-the-ajax-control-toolkit-cs.md)
> [다음](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)</span><span class="sxs-lookup"><span data-stu-id="b42e5-162">[Previous](get-started-with-the-ajax-control-toolkit-cs.md)
[Next](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)</span></span>
