---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
title: AJAX 컨트롤 도구 키트 컨트롤 및 컨트롤 Extender 사용 (VB) | Microsoft Docs
author: microsoft
description: ASP.NET 페이지에 AJAX 컨트롤 도구 키트 컨트롤과 extender를 추가 하는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 763650a9-ffde-46a9-b779-7a9145dd5d88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
msc.type: authoredcontent
ms.openlocfilehash: 90a6003ff50ba6e85196c25cf175e057810f0f84
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497051"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-vb"></a><span data-ttu-id="cd787-103">Using AJAX 컨트롤 도구 키트 컨트롤 및 컨트롤 Extender 사용(VB)</span><span class="sxs-lookup"><span data-stu-id="cd787-103">Using AJAX Control Toolkit Controls and Control Extenders (VB)</span></span>

<span data-ttu-id="cd787-104">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="cd787-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="cd787-105">ASP.NET 페이지에 AJAX 컨트롤 도구 키트 컨트롤과 extender를 추가 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-105">Learn how to add AJAX Control Toolkit controls and extenders to your ASP.NET pages.</span></span>

<span data-ttu-id="cd787-106">AJAX 컨트롤 도구 키트에는 컨트롤 및 컨트롤 extender 집합이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-106">The AJAX Control Toolkit contains a set of controls and control extenders.</span></span> <span data-ttu-id="cd787-107">이 간략 한 자습서에서는 ASP.NET 페이지에 컨트롤과 컨트롤 extender를 추가 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-107">In this brief tutorial, you learn how to add both controls and control extenders to an ASP.NET page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="cd787-108">Ajax 컨트롤 도구 키트를 설치 하 고 Visual Studio/Visual Web Developer 도구 상자에 AJAX 컨트롤 도구 키트를 추가 하는 방법에 대 한 지침은 [Ajax 컨트롤 도구 키트 시작](get-started-with-the-ajax-control-toolkit-vb.md)자습서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="cd787-108">For instructions on installing the AJAX Control Toolkit and adding the AJAX Control Toolkit to the Visual Studio/Visual Web Developer toolbox, see the tutorial [Get Started with the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb.md).</span></span>

## <a name="using-ajax-control-toolkit-controls"></a><span data-ttu-id="cd787-109">AJAX 컨트롤 도구 키트 컨트롤 사용</span><span class="sxs-lookup"><span data-stu-id="cd787-109">Using AJAX Control Toolkit Controls</span></span>

<span data-ttu-id="cd787-110">AJAX 컨트롤 도구 키트 컨트롤은 일반적인 ASP.NET 컨트롤과 마찬가지로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-110">An AJAX Control Toolkit control works just like a normal ASP.NET control.</span></span> <span data-ttu-id="cd787-111">도구 상자에서 컨트롤을 ASP.NET 페이지로 끌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-111">You can drag the control from the toolbox onto an ASP.NET page.</span></span> <span data-ttu-id="cd787-112">디자인 뷰 또는 소스 뷰에서 페이지에 컨트롤을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-112">You can add the control to the page in either Design view or Source view.</span></span>

<span data-ttu-id="cd787-113">AJAX 컨트롤 도구 키트의 컨트롤을 사용 하는 경우 특별 한 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-113">There is one special requirement when using the controls from the AJAX Control Toolkit.</span></span> <span data-ttu-id="cd787-114">페이지는 ScriptManager 컨트롤을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-114">The page must contain a ScriptManager control.</span></span> <span data-ttu-id="cd787-115">ScriptManager 컨트롤은 AJAX 컨트롤 도구 키트 컨트롤에 필요한 모든 JavaScript를 포함 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-115">The ScriptManager control is responsible for including all of the necessary JavaScript required by the AJAX Control Toolkit controls.</span></span>

<span data-ttu-id="cd787-116">예를 들어 AJAX 컨트롤 도구 키트 탭은 편집기 컨트롤 이라는 컨트롤을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-116">For example, the AJAX Control Toolkit tab includes a control named the Editor control.</span></span> <span data-ttu-id="cd787-117">이 컨트롤은 리치 HTML 편집기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-117">This control displays a rich HTML editor.</span></span> <span data-ttu-id="cd787-118">페이지에 편집기 컨트롤을 추가 하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="cd787-118">Follow these steps to add the Editor control to a page:</span></span>

1. <span data-ttu-id="cd787-119">ShowEditor 라는 새 ASP.NET 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-119">Create a new ASP.NET page named ShowEditor.aspx</span></span>
2. <span data-ttu-id="cd787-120">도구 상자의 AJAX 확장 탭 아래에서 ScriptManager 컨트롤을 선택 하 고 컨트롤을 페이지로 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-120">Select the ScriptManager control from beneath the AJAX Extensions tab in the toolbox and drag the control onto the page.</span></span>
3. <span data-ttu-id="cd787-121">도구 상자의 AJAX 컨트롤 도구 키트 탭 아래에서 편집기 컨트롤을 선택 하 고 컨트롤을 페이지로 끌어옵니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="cd787-121">Select the Editor control from beneath the AJAX Control Toolkit tab in the toolbox and drag the control onto the page (see Figure 1).</span></span> <span data-ttu-id="cd787-122">디자이너는 그림 2와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-122">The Designer should look like Figure 2.</span></span>
4. <span data-ttu-id="cd787-123">**디버그, 디버깅 시작** 또는 F5 키로 메뉴 옵션을 선택 하 여 웹 사이트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-123">Run the web site by selecting the menu option **Debug, Start Debugging** or hitting the F5 key.</span></span>
5. <span data-ttu-id="cd787-124">그림 3에 페이지가 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-124">You should see the page in Figure 3.</span></span>

<span data-ttu-id="cd787-125">[HTML 편집기 컨트롤을 선택 ![](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="cd787-125">[![Selecting the HTML Editor control](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)</span></span>

<span data-ttu-id="cd787-126">**그림 01**: HTML 편집기 컨트롤 선택 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="cd787-126">**Figure 01**: Selecting the HTML Editor control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png))</span></span>

<span data-ttu-id="cd787-127">[ScriptManager 및 Edit 컨트롤을 사용 하 여 Visual Studio Designer ![](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="cd787-127">[![Visual Studio Designer with ScriptManager and Edit control](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)</span></span>

<span data-ttu-id="cd787-128">**그림 02**: ScriptManager 및 Edit 컨트롤이 있는 Visual Studio 디자이너 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="cd787-128">**Figure 02**: Visual Studio Designer with ScriptManager and Edit control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png))</span></span>

<span data-ttu-id="cd787-129">[DisplayEditor .aspx 페이지 ![](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="cd787-129">[![The DisplayEditor.aspx page](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)</span></span>

<span data-ttu-id="cd787-130">**그림 03**: displayeditor .aspx 페이지 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="cd787-130">**Figure 03**: The DisplayEditor.aspx page([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png))</span></span>

## <a name="using-ajax-control-toolkit-control-extenders"></a><span data-ttu-id="cd787-131">AJAX 컨트롤 도구 키트 컨트롤 Extender 사용</span><span class="sxs-lookup"><span data-stu-id="cd787-131">Using AJAX Control Toolkit Control Extenders</span></span>

<span data-ttu-id="cd787-132">AJAX 컨트롤 도구 키트에는 컨트롤 extender도 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-132">The AJAX Control Toolkit also contains control extenders.</span></span> <span data-ttu-id="cd787-133">이름에서 알 때 컨트롤 extender는 기존 컨트롤의 기능을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-133">As its name suggests, a control extender extends the functionality of an existing control.</span></span> <span data-ttu-id="cd787-134">예를 들어, ASP.NET button 컨트롤 extender는 표준 Button 컨트롤을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-134">For example, the ConfirmButton control extender extends the standard ASP.NET Button control.</span></span> <span data-ttu-id="cd787-135">Extender는 단추 컨트롤의 동작을 변경 하 여 단추를 클릭 하면 확인 대화 상자가 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-135">The extender changes the Button control�s behavior so that the Button displays a confirmation dialog when you click it.</span></span>

<span data-ttu-id="cd787-136">AJAX 컨트롤 도구 키트 컨트롤과 마찬가지로 컨트롤 extender에는 ScriptManager 컨트롤이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-136">A control extender, just like an AJAX Control Toolkit control, requires a ScriptManager control.</span></span> <span data-ttu-id="cd787-137">페이지에서 컨트롤 extender 사용을 시작 하기 전에 페이지에 ScriptManager 컨트롤을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-137">You must add a ScriptManager control to a page before you start using control extenders in the page.</span></span>

<span data-ttu-id="cd787-138">다음 단계를 수행 하 여 추가 단추 컨트롤 extender를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-138">Follow these steps to use the ConfirmButton control extender:</span></span>

1. <span data-ttu-id="cd787-139">ShowASP.NET 라는 새 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-139">Create a new ASP.NET page named ShowConfirmButton.aspx</span></span>
2. <span data-ttu-id="cd787-140">AJAX 확장 탭 아래에서 페이지로 컨트롤을 끌어서 ScriptManager 컨트롤을 페이지에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-140">Add a ScriptManager control to the page by dragging the control onto the page from beneath the AJAX Extensions tab.</span></span>
3. <span data-ttu-id="cd787-141">도구 상자의 표준 탭 아래에서 단추를 디자이너 화면으로 끌어서 표준 단추 컨트롤을 페이지에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-141">Add a standard Button control to the page by dragging the Button from beneath the Standard tab in the toolbox onto the Designer surface.</span></span>
4. <span data-ttu-id="cd787-142">확장 작업 **추가** 옵션을 클릭 합니다 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="cd787-142">Click the **Add Extender** task option (see Figure 4).</span></span>
5. <span data-ttu-id="cd787-143">Extender 선택 대화 상자에서를 선택 하 고 (그림 5 참조) 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-143">In the Choose Extender dialog, select ConfirmButtonExtender (see Figure 5) and click the OK button.</span></span>
6. <span data-ttu-id="cd787-144">디자이너에서 Button 컨트롤을 선택 하 고 속성 창에서 Extender, Button1\_로 Buttonextender 노드를 확장 합니다 (그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="cd787-144">Select the Button control in the Designer and expand the Extenders, Button1\_ConfirmButtonExtender node in the Properties window (see Figure 6).</span></span> <span data-ttu-id="cd787-145">값을 *실제* 값으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-145">Assign the value *�Really?�* to the ConfirmText property.</span></span>
7. <span data-ttu-id="cd787-146">**디버그, 디버깅 시작** 메뉴 옵션을 선택 하거나 F5 키를 눌러 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-146">Run the page by selecting the menu option **Debug, Start Debugging** or hit the F5 key.</span></span>

<span data-ttu-id="cd787-147">[Extender 추가 작업 옵션 ![](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="cd787-147">[![The Add Extender task option](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)</span></span>

<span data-ttu-id="cd787-148">**그림 04**: Extender 추가 작업 옵션 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="cd787-148">**Figure 04**: The Add Extender task option([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png))</span></span>

<span data-ttu-id="cd787-149">[![하 여 컨트롤 extender를 선택 합니다.](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="cd787-149">[![Selecting the ConfirmButton control extender](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)</span></span>

<span data-ttu-id="cd787-150">**그림 05**: 확장[이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png)합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-150">**Figure 05**: Selecting the ConfirmButton control extender([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png))</span></span>

<span data-ttu-id="cd787-151">[![를 설정 하는 단추 속성](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="cd787-151">[![Setting a ConfirmButton property](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)</span></span>

<span data-ttu-id="cd787-152">**그림 06**: 단일 기능 단추 속성 설정 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="cd787-152">**Figure 06**: Setting a ConfirmButton property([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png))</span></span>

<span data-ttu-id="cd787-153">페이지가 열리면 단추가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-153">When the page opens, you should see a button.</span></span> <span data-ttu-id="cd787-154">단추를 클릭 하면 그림 7에 확인 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-154">When you click the button, you get the confirmation dialog in Figure 7.</span></span>

<span data-ttu-id="cd787-155">[확인 대화 상자를 표시 하 ![](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="cd787-155">[![Displaying the confirmation dialog](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)</span></span>

<span data-ttu-id="cd787-156">**그림 07**: 확인 대화 상자 표시 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="cd787-156">**Figure 07**: Displaying the confirmation dialog([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png))</span></span>

<span data-ttu-id="cd787-157">일반적으로 컨트롤 extender를 페이지로 끌어 오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-157">Notice that you normally do not drag a control extender onto a page.</span></span> <span data-ttu-id="cd787-158">대신, 페이지에 이미 추가 된 컨트롤에 extender를 추가 하려면 **extender 작업 추가** 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-158">Instead, you use the **Add Extender** task option to add an extender to a control that you have already added to a page.</span></span> <span data-ttu-id="cd787-159">또한 확장 중인 컨트롤의 속성 시트를 열어 컨트롤 extender 속성을 설정 하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-159">Notice, furthermore, that you set control extender properties by opening the property sheet for the control being extended.</span></span>

<span data-ttu-id="cd787-160">단일 ASP.NET 컨트롤은 여러 컨트롤 extender로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-160">A single ASP.NET control can be extended by multiple control extenders.</span></span> <span data-ttu-id="cd787-161">확장 되는 컨트롤의 속성 시트에는 컨트롤과 연결 된 모든 컨트롤 extender가 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd787-161">The property sheet for the control being extended will list all of the control extenders associated with the control.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cd787-162">[이전](get-started-with-the-ajax-control-toolkit-vb.md)
> [다음](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)</span><span class="sxs-lookup"><span data-stu-id="cd787-162">[Previous](get-started-with-the-ajax-control-toolkit-vb.md)
[Next](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)</span></span>
