---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: AJAX 제어 툴킷 제어 및 제어 익스텐더 사용 (C#) | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET 페이지에 AJAX 제어 툴킷 컨트롤 및 익스텐더를 추가하는 방법을 알아봅니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 5729db63f831b74ca37c573791c53c39265c1f39
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543719"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a><span data-ttu-id="56c94-103">Using AJAX 컨트롤 도구 키트 컨트롤 및 컨트롤 Extender 사용(C#)</span><span class="sxs-lookup"><span data-stu-id="56c94-103">Using AJAX Control Toolkit Controls and Control Extenders (C#)</span></span>

<span data-ttu-id="56c94-104">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="56c94-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="56c94-105">ASP.NET 페이지에 AJAX 제어 툴킷 컨트롤 및 익스텐더를 추가하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-105">Learn how to add AJAX Control Toolkit controls and extenders to your ASP.NET pages.</span></span>

<span data-ttu-id="56c94-106">AJAX 제어 툴킷에는 일련의 컨트롤 및 컨트롤 익스텐더가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-106">The AJAX Control Toolkit contains a set of controls and control extenders.</span></span> <span data-ttu-id="56c94-107">이 간단한 자습서에서는 컨트롤 및 컨트롤 extenders를 ASP.NET 페이지에 추가하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-107">In this brief tutorial, you learn how to add both controls and control extenders to an ASP.NET page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="56c94-108">AJAX 제어 도구 키트를 설치하고 AJAX 제어 도구 키트를 시각적 스튜디오/비주얼 웹 개발자 도구 상자에 추가하는 방법에 대한 지침은 [AJAX 제어 도구 키트로 시작하기 자습서를](get-started-with-the-ajax-control-toolkit-cs.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="56c94-108">For instructions on installing the AJAX Control Toolkit and adding the AJAX Control Toolkit to the Visual Studio/Visual Web Developer toolbox, see the tutorial [Get Started with the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs.md).</span></span>

## <a name="using-ajax-control-toolkit-controls"></a><span data-ttu-id="56c94-109">AJAX 제어 툴킷 컨트롤 사용</span><span class="sxs-lookup"><span data-stu-id="56c94-109">Using AJAX Control Toolkit Controls</span></span>

<span data-ttu-id="56c94-110">AJAX 제어 툴킷 컨트롤은 일반 ASP.NET 컨트롤처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-110">An AJAX Control Toolkit control works just like a normal ASP.NET control.</span></span> <span data-ttu-id="56c94-111">도구 상자에서 ASP.NET 페이지로 컨트롤을 드래그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-111">You can drag the control from the toolbox onto an ASP.NET page.</span></span> <span data-ttu-id="56c94-112">디자인 뷰 또는 소스 보기에서 페이지에 컨트롤을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-112">You can add the control to the page in either Design view or Source view.</span></span>

<span data-ttu-id="56c94-113">AJAX 제어 도구 키트의 컨트롤을 사용할 때 는 한 가지 특별한 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-113">There is one special requirement when using the controls from the AJAX Control Toolkit.</span></span> <span data-ttu-id="56c94-114">페이지에ScriptManager 컨트롤이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-114">The page must contain a ScriptManager control.</span></span> <span data-ttu-id="56c94-115">ScriptManager 컨트롤은 AJAX 제어 도구 키트 컨트롤에 필요한 모든 자바스크립트를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-115">The ScriptManager control is responsible for including all of the necessary JavaScript required by the AJAX Control Toolkit controls.</span></span>

<span data-ttu-id="56c94-116">예를 들어 AJAX 제어 도구 키트 탭에는 편집기 컨트롤이라는 컨트롤이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-116">For example, the AJAX Control Toolkit tab includes a control named the Editor control.</span></span> <span data-ttu-id="56c94-117">이 컨트롤에는 풍부한 HTML 편집기가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-117">This control displays a rich HTML editor.</span></span> <span data-ttu-id="56c94-118">다음 단계에 따라 페이지에 편집기 컨트롤을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-118">Follow these steps to add the Editor control to a page:</span></span>

1. <span data-ttu-id="56c94-119">ShowEditor.aspx라는 이름의 새 ASP.NET 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="56c94-119">Create a new ASP.NET page named ShowEditor.aspx</span></span>
2. <span data-ttu-id="56c94-120">도구 상자의 AJAX 확장 탭 아래에서 ScriptManager 컨트롤을 선택하고 컨트롤을 페이지로 드래그합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-120">Select the ScriptManager control from beneath the AJAX Extensions tab in the toolbox and drag the control onto the page.</span></span>
3. <span data-ttu-id="56c94-121">도구 상자의 AJAX 제어 도구 키트 탭 아래에서 편집기 컨트롤을 선택하고 컨트롤을 페이지로 드래그합니다(그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="56c94-121">Select the Editor control from beneath the AJAX Control Toolkit tab in the toolbox and drag the control onto the page (see Figure 1).</span></span> <span data-ttu-id="56c94-122">디자이너는 그림 2와 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-122">The Designer should look like Figure 2.</span></span>
4. <span data-ttu-id="56c94-123">메뉴 옵션 **디버그, 디버깅 시작** 또는 F5 키를 누르면 웹 사이트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-123">Run the web site by selecting the menu option **Debug, Start Debugging** or hitting the F5 key.</span></span>
5. <span data-ttu-id="56c94-124">그림 3의 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-124">You should see the page in Figure 3.</span></span>

<span data-ttu-id="56c94-125">[![HTML 편집기 컨트롤 선택](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="56c94-125">[![Selecting the HTML Editor control](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)</span></span>

<span data-ttu-id="56c94-126">**그림 01**: HTML 편집기 컨트롤 선택[(클릭하여 전체 크기 이미지 보기)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="56c94-126">**Figure 01**: Selecting the HTML Editor control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))</span></span>

<span data-ttu-id="56c94-127">[![스크립트 관리자 및 편집 컨트롤이 있는 비주얼 스튜디오 디자이너](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="56c94-127">[![Visual Studio Designer with ScriptManager and Edit control](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)</span></span>

<span data-ttu-id="56c94-128">**그림 02**: 스크립트 관리자 및 편집 컨트롤이 있는 비주얼 스튜디오[디자이너(클릭하여 전체 크기 이미지 보기)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="56c94-128">**Figure 02**: Visual Studio Designer with ScriptManager and Edit control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))</span></span>

<span data-ttu-id="56c94-129">[![디스플레이 에디터.aspx 페이지](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="56c94-129">[![The DisplayEditor.aspx page](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)</span></span>

<span data-ttu-id="56c94-130">**그림 03**: DisplayEditor.aspx 페이지[(전체 크기 이미지를 보려면 클릭)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="56c94-130">**Figure 03**: The DisplayEditor.aspx page([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))</span></span>

## <a name="using-ajax-control-toolkit-control-extenders"></a><span data-ttu-id="56c94-131">AJAX 제어 툴킷 제어 익스텐더 사용</span><span class="sxs-lookup"><span data-stu-id="56c94-131">Using AJAX Control Toolkit Control Extenders</span></span>

<span data-ttu-id="56c94-132">AJAX 제어 툴킷에는 컨트롤 익스텐더도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-132">The AJAX Control Toolkit also contains control extenders.</span></span> <span data-ttu-id="56c94-133">이름에서 알 수 있듯이 컨트롤 익스텐더는 기존 컨트롤의 기능을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-133">As its name suggests, a control extender extends the functionality of an existing control.</span></span> <span data-ttu-id="56c94-134">예를 들어 ConfirmButton 컨트롤 익스텐더는 표준 ASP.NET 버튼 컨트롤을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-134">For example, the ConfirmButton control extender extends the standard ASP.NET Button control.</span></span> <span data-ttu-id="56c94-135">Extender는 단추를 클릭할 때 확인 대화 상자를 표시되도록 단추 컨트롤의 동작을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-135">The extender changes the Button control�s behavior so that the Button displays a confirmation dialog when you click it.</span></span>

<span data-ttu-id="56c94-136">AJAX 컨트롤 툴킷 컨트롤과 마찬가지로 컨트롤 익스텐더에는 ScriptManager 컨트롤이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-136">A control extender, just like an AJAX Control Toolkit control, requires a ScriptManager control.</span></span> <span data-ttu-id="56c94-137">페이지에서 컨트롤 익스텐더를 사용하기 전에 페이지에 ScriptManager 컨트롤을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-137">You must add a ScriptManager control to a page before you start using control extenders in the page.</span></span>

<span data-ttu-id="56c94-138">확인 단추 컨트롤 익스텐더를 사용 하려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-138">Follow these steps to use the ConfirmButton control extender:</span></span>

1. <span data-ttu-id="56c94-139">ShowConfirmButton.aspx라는 이름의 새 ASP.NET 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="56c94-139">Create a new ASP.NET page named ShowConfirmButton.aspx</span></span>
2. <span data-ttu-id="56c94-140">AJAX 확장 탭 아래에서 페이지로 컨트롤을 드래그하여 페이지에 ScriptManager 컨트롤을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-140">Add a ScriptManager control to the page by dragging the control onto the page from beneath the AJAX Extensions tab.</span></span>
3. <span data-ttu-id="56c94-141">도구 상자의 표준 탭 아래에서 디자이너 표면으로 단추를 드래그하여 페이지에 표준 단추 컨트롤을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-141">Add a standard Button control to the page by dragging the Button from beneath the Standard tab in the toolbox onto the Designer surface.</span></span>
4. <span data-ttu-id="56c94-142">확장 **작업 추가** 옵션을 클릭합니다(그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="56c94-142">Click the **Add Extender** task option (see Figure 4).</span></span>
5. <span data-ttu-id="56c94-143">확장자 선택 대화 상자에서 확인단추 익스텐더(그림 5 참조)를 선택하고 확인 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-143">In the Choose Extender dialog, select ConfirmButtonExtender (see Figure 5) and click the OK button.</span></span>
6. <span data-ttu-id="56c94-144">디자이너에서 단추 컨트롤을 선택하고 속성 창에서\_Extender, Button1 ConfirmButtonExtender 노드를 확장합니다(그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="56c94-144">Select the Button control in the Designer and expand the Extenders, Button1\_ConfirmButtonExtender node in the Properties window (see Figure 6).</span></span> <span data-ttu-id="56c94-145">값을 *정말?* ConfirmText 속성에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-145">Assign the value *�Really?�* to the ConfirmText property.</span></span>
7. <span data-ttu-id="56c94-146">메뉴 옵션 **디버그, 디버깅 시작 또는** F5 키를 선택하여 페이지를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-146">Run the page by selecting the menu option **Debug, Start Debugging** or hit the F5 key.</span></span>

<span data-ttu-id="56c94-147">[![확장기 추가 작업 옵션](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="56c94-147">[![The Add Extender task option](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)</span></span>

<span data-ttu-id="56c94-148">**그림 04**: 확장 작업 추가 옵션[(클릭하여 전체 크기 이미지 보기)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="56c94-148">**Figure 04**: The Add Extender task option([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))</span></span>

<span data-ttu-id="56c94-149">[![확인 단추 제어 익스텐더 선택](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="56c94-149">[![Selecting the ConfirmButton control extender](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)</span></span>

<span data-ttu-id="56c94-150">**그림 05**: 확인 버튼 컨트롤 익스텐더 선택[(전체 크기 이미지를 보려면 클릭)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="56c94-150">**Figure 05**: Selecting the ConfirmButton control extender([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))</span></span>

<span data-ttu-id="56c94-151">[![ConfirmButton 속성 설정](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="56c94-151">[![Setting a ConfirmButton property](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)</span></span>

<span data-ttu-id="56c94-152">**그림 06**: ConfirmButton 속성 설정[(전체 크기 이미지를 보려면 클릭)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="56c94-152">**Figure 06**: Setting a ConfirmButton property([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))</span></span>

<span data-ttu-id="56c94-153">페이지가 열리면 단추가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-153">When the page opens, you should see a button.</span></span> <span data-ttu-id="56c94-154">단추를 클릭하면 그림 7의 확인 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-154">When you click the button, you get the confirmation dialog in Figure 7.</span></span>

<span data-ttu-id="56c94-155">[![확인 대화 상자 표시](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="56c94-155">[![Displaying the confirmation dialog](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)</span></span>

<span data-ttu-id="56c94-156">**그림 07**: 확인 대화 상자 표시[(전체 크기 이미지를 보려면 클릭)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="56c94-156">**Figure 07**: Displaying the confirmation dialog([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))</span></span>

<span data-ttu-id="56c94-157">일반적으로 컨트롤 익스텐더를 페이지로 드래그하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-157">Notice that you normally do not drag a control extender onto a page.</span></span> <span data-ttu-id="56c94-158">대신 **Extender 추가** 작업 옵션을 사용하여 페이지에 이미 추가한 컨트롤에 extender를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-158">Instead, you use the **Add Extender** task option to add an extender to a control that you have already added to a page.</span></span> <span data-ttu-id="56c94-159">또한 확장되는 컨트롤에 대한 속성 시트를 열어 컨트롤 익스텐더 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-159">Notice, furthermore, that you set control extender properties by opening the property sheet for the control being extended.</span></span>

<span data-ttu-id="56c94-160">단일 ASP.NET 컨트롤은 여러 컨트롤 익스텐더로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-160">A single ASP.NET control can be extended by multiple control extenders.</span></span> <span data-ttu-id="56c94-161">확장되는 컨트롤에 대한 속성 시트에는 컨트롤과 연결된 모든 컨트롤 익스텐더가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="56c94-161">The property sheet for the control being extended will list all of the control extenders associated with the control.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="56c94-162">[이전](get-started-with-the-ajax-control-toolkit-cs.md)
> [다음](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)</span><span class="sxs-lookup"><span data-stu-id="56c94-162">[Previous](get-started-with-the-ajax-control-toolkit-cs.md)
[Next](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)</span></span>
