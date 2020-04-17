---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
title: 컬러피커 컨트롤 익스텐더 사용 (C#) | 마이크로 소프트 문서
author: rick-anderson
description: ColorPicker는 팝업 컨트롤에서 UI와 클라이언트 측 색상 선택 기능을 제공하는 ASP.NET AJAX 익스텐더입니다. 그것은 어떤 ASP.NET 부착 할 수 있습니다 ...
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0d86a1e7-a910-4ab2-b85c-7a9ea6906c39
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 63b6bc58d36fdfcb5ee0a1c97988091e8d35505b
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543134"
---
# <a name="using-the-colorpicker-control-extender-c"></a><span data-ttu-id="40b87-104">컬러피커 컨트롤 익스텐더 사용(C#)</span><span class="sxs-lookup"><span data-stu-id="40b87-104">Using the ColorPicker Control Extender (C#)</span></span>

<span data-ttu-id="40b87-105">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="40b87-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="40b87-106">ColorPicker는 팝업 컨트롤에서 UI와 클라이언트 측 색상 선택 기능을 제공하는 ASP.NET AJAX 익스텐더입니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-106">ColorPicker is an ASP.NET AJAX extender that provides client-side color-picking functionality with UI in a popup control.</span></span> <span data-ttu-id="40b87-107">모든 ASP.NET TextBox 컨트롤에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-107">It can be attached to any ASP.NET TextBox control.</span></span> <span data-ttu-id="40b87-108">그것은.</span><span class="sxs-lookup"><span data-stu-id="40b87-108">It.</span></span>

<span data-ttu-id="40b87-109">이 자습서의 목표는 AJAX 제어 도구 키트 ColorPicker 컨트롤 익스텐더를 사용하는 방법을 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-109">The goal of this tutorial is to explain how you can use the AJAX Control Toolkit ColorPicker control extender.</span></span> <span data-ttu-id="40b87-110">ColorPicker 컨트롤 익스텐더에는 색상을 선택할 수 있는 팝업 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-110">The ColorPicker control extender displays a popup dialog that enables you to select a color.</span></span> <span data-ttu-id="40b87-111">ColorPicker는 사용자가 색상을 선택할 수 있도록 직관적인 사용자 인터페이스를 제공하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-111">The ColorPicker is useful whenever you want to provide an intuitive user interface for a user to pick a color.</span></span>

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a><span data-ttu-id="40b87-112">색상 선택기 컨트롤 확장기를 사용하여 텍스트 상자 컨트롤 확장</span><span class="sxs-lookup"><span data-stu-id="40b87-112">Extending a TextBox Control with the ColorPicker Control Extender</span></span>

<span data-ttu-id="40b87-113">예를 들어 방문자가 사용자 지정된 명함을 만들 수 있는 웹 사이트를 만들려고 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-113">Imagine, for example, that you want to create a website that enables visitors to create customized business cards.</span></span> <span data-ttu-id="40b87-114">방문자는 명함의 텍스트를 입력하고 색상을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-114">Visitors can enter the text for a business card and pick the color.</span></span> <span data-ttu-id="40b87-115">목록 1의 ASP.NET 페이지에는 txtCardText 및 txtCardColor라는 두 개의 텍스트 상자 컨트롤이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-115">The ASP.NET page in Listing 1 contains two TextBox controls named txtCardText and txtCardColor.</span></span> <span data-ttu-id="40b87-116">양식을 제출하면 선택한 값이 표시됩니다(그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="40b87-116">When you submit the form, the selected values are displayed (see Figure 1).</span></span>

<span data-ttu-id="40b87-117">[![명함을 만들기 위한 간단한 양식](using-the-colorpicker-control-extender-cs/_static/image1.jpg)](using-the-colorpicker-control-extender-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="40b87-117">[![Simple form for creating a business card](using-the-colorpicker-control-extender-cs/_static/image1.jpg)](using-the-colorpicker-control-extender-cs/_static/image1.png)</span></span>

<span data-ttu-id="40b87-118">**그림 01**: 명함을 만들기위한 간단한 양식[(전체 크기 이미지를 보려면 클릭)](using-the-colorpicker-control-extender-cs/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="40b87-118">**Figure 01**: Simple form for creating a business card ([Click to view full-size image](using-the-colorpicker-control-extender-cs/_static/image2.png))</span></span>

<span data-ttu-id="40b87-119">**목록 1 - CreateCard.aspx**</span><span class="sxs-lookup"><span data-stu-id="40b87-119">**Listing 1 - CreateCard.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample1.aspx)]

<span data-ttu-id="40b87-120">목록 1의 양식은 작동하지만 훌륭한 사용자 환경을 제공하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-120">The form in Listing 1 works, but it does not provide a great user experience.</span></span> <span data-ttu-id="40b87-121">사용자는 텍스트 상자에 색상을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-121">The user has to type a color into the textbox.</span></span> <span data-ttu-id="40b87-122">사용자가 완두콩 녹색의 올바른 음영과 같은 특수 한 색상을 원한다면 사용자는 도움없이 HTML 색상 코드를 파악해야합니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-122">If the user wants a specialized color - for example, just the right shade of pea green - then the user must figure out the HTML color code without any help.</span></span>

<span data-ttu-id="40b87-123">ColorPicker 컨트롤 익스텐더를 사용하여 더 나은 사용자 환경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-123">You can use the ColorPicker control extender to create a better user experience.</span></span> <span data-ttu-id="40b87-124">TextBox 컨트롤로 포커스를 이동할 때 ColorPicker에 색상 대화 상자가 표시됩니다(그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="40b87-124">The ColorPicker displays a color dialog when you move focus to a TextBox control (see Figure 2).</span></span>

<span data-ttu-id="40b87-125">[![컬러피커 컨트롤 익스텐더](using-the-colorpicker-control-extender-cs/_static/image2.jpg)](using-the-colorpicker-control-extender-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="40b87-125">[![The ColorPicker Control Extender](using-the-colorpicker-control-extender-cs/_static/image2.jpg)](using-the-colorpicker-control-extender-cs/_static/image3.png)</span></span>

<span data-ttu-id="40b87-126">**그림 02**: 컬러 피커 컨트롤 익스텐더[(전체 크기 이미지를 보려면 클릭)](using-the-colorpicker-control-extender-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="40b87-126">**Figure 02**: The ColorPicker Control Extender ([Click to view full-size image](using-the-colorpicker-control-extender-cs/_static/image4.png))</span></span>

<span data-ttu-id="40b87-127">목록 1의 양식과 함께 ColorPicker 컨트롤 익스텐더를 사용하려면 두 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-127">You need to complete two steps to use the ColorPicker control extender with the form in Listing 1:</span></span>

1. <span data-ttu-id="40b87-128">페이지에 스크립트 관리자 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="40b87-128">Add a ScriptManager control to the page</span></span>
2. <span data-ttu-id="40b87-129">페이지에 ColorPicker 컨트롤 익스텐더 추가</span><span class="sxs-lookup"><span data-stu-id="40b87-129">Add the ColorPicker control extender to the page</span></span>

<span data-ttu-id="40b87-130">ColorPicker를 사용하려면 먼저 페이지에 ScriptManager를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-130">Before you can use the ColorPicker, you must add a ScriptManager to your page.</span></span> <span data-ttu-id="40b87-131">ScriptManager를 추가하는 좋은 장소는 열기 서버 측 &lt;&gt; 양식 태그 바로 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-131">A good place to add the ScriptManager is right below the opening server-side &lt;form&gt; tag.</span></span> <span data-ttu-id="40b87-132">도구 상자에서 페이지로 ScriptManager를 드래그할 수 있습니다(스크립트 관리자는 AJAX 확장 탭 아래에 있음).</span><span class="sxs-lookup"><span data-stu-id="40b87-132">You can drag the ScriptManager onto the page from the toolbox (the ScriptManager is located under the AJAX Extensions tab).</span></span> <span data-ttu-id="40b87-133">또는 열기 서버 측 양식 태그 아래에 다음 태그를 소스 보기에 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-133">Alternatively, you can type the following tag into Source View beneath the opening server-side form tag:</span></span>

<span data-ttu-id="40b87-134">&lt;asp:스크립트관리자 ID="스크립트관리자1" 런나트="서버" /&gt;</span><span class="sxs-lookup"><span data-stu-id="40b87-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span></span>

<span data-ttu-id="40b87-135">페이지에 ColorPicker 컨트롤 익스텐더를 추가하는 가장 쉬운 방법은 디자인 뷰에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-135">The easiest way to add the ColorPicker control extender to the page is in Design View.</span></span> <span data-ttu-id="40b87-136">txtCardColor 텍스트 상자 위에 마우스를 가져가면 확장기를 추가할 수 있는 스마트 작업 옵션이 나타납니다(그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="40b87-136">If you hover your mouse over the txtCardColor TextBox, a smart task option appears the enables you to add an extender (see Figure 3).</span></span> <span data-ttu-id="40b87-137">이 옵션을 선택하면 확장자 마법사가 나타납니다(그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="40b87-137">If you pick this option, the Extender Wizard appears (see Figure 4).</span></span>

<span data-ttu-id="40b87-138">[![익스텐더 추가](using-the-colorpicker-control-extender-cs/_static/image3.jpg)](using-the-colorpicker-control-extender-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="40b87-138">[![Adding an extender](using-the-colorpicker-control-extender-cs/_static/image3.jpg)](using-the-colorpicker-control-extender-cs/_static/image5.png)</span></span>

<span data-ttu-id="40b87-139">**그림 03**: 익스텐더 추가[(전체 크기 이미지를 보려면 클릭)](using-the-colorpicker-control-extender-cs/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="40b87-139">**Figure 03**: Adding an extender ([Click to view full-size image](using-the-colorpicker-control-extender-cs/_static/image6.png))</span></span>

<span data-ttu-id="40b87-140">[![익스텐더 마법사를 사용하여 컨트롤 익스텐더 선택](using-the-colorpicker-control-extender-cs/_static/image4.jpg)](using-the-colorpicker-control-extender-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="40b87-140">[![Selecting a control extender with the Extender Wizard](using-the-colorpicker-control-extender-cs/_static/image4.jpg)](using-the-colorpicker-control-extender-cs/_static/image7.png)</span></span>

<span data-ttu-id="40b87-141">**그림 04**: 익스텐더 마법사를 사용하여 컨트롤 익스텐더 선택[(전체 크기 이미지를 보려면 클릭)](using-the-colorpicker-control-extender-cs/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="40b87-141">**Figure 04**: Selecting a control extender with the Extender Wizard ([Click to view full-size image](using-the-colorpicker-control-extender-cs/_static/image8.png))</span></span>

<span data-ttu-id="40b87-142">ColorPicker 익스텐더를 선택하여 colorPicker 익스텐더를 사용하여 txtCardColor 텍스트 상자를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-142">You can pick the ColorPicker extender to extend the txtCardColor TextBox with the ColorPicker extender.</span></span> <span data-ttu-id="40b87-143">확인을 클릭하여 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-143">Click OK to close the dialog.</span></span>

<span data-ttu-id="40b87-144">이러한 변경을 하면 페이지의 소스가 목록 2처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-144">After you make these changes, the source for the page looks like Listing 2.</span></span>

<span data-ttu-id="40b87-145">목록 2 - CreateCard.aspx(컬러선택기)</span><span class="sxs-lookup"><span data-stu-id="40b87-145">Listing 2 - CreateCard.aspx (with ColorPicker)</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample2.aspx)]

<span data-ttu-id="40b87-146">이제 페이지에 txtCardColor 텍스트 상자 컨트롤 바로 아래에 나타나는 ColorPickerExtender 컨트롤이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-146">Notice that the page now contains a ColorPickerExtender control that appears directly below the txtCardColor TextBox control.</span></span> <span data-ttu-id="40b87-147">ColorPickerExtender 컨트롤은 txtCardColor 컨트롤을 확장하여 색상 선택기 대화 상자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-147">The ColorPickerExtender control extends the txtCardColor control so that it displays a color picker dialog.</span></span>

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a><span data-ttu-id="40b87-148">단추를 사용하여 색상 선택기 대화 상자 시작</span><span class="sxs-lookup"><span data-stu-id="40b87-148">Using a Button to Launch the Color Picker Dialog</span></span>

<span data-ttu-id="40b87-149">ColorPicker 익스텐더는 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-149">The ColorPicker extender supports the following properties:</span></span>

- <span data-ttu-id="40b87-150">팝업ButtonId - 색상 선택기 대화 상자가 나타나는 페이지의 단추 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-150">PopupButtonId - The ID of a button on the page that causes the color picker dialog to appear.</span></span>
- <span data-ttu-id="40b87-151">팝업 위치 - 색상 선택 기 대화 상자의 대상 컨트롤을 기준으로 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-151">PopupPosition - The position, relative to the target control, of the color picker dialog.</span></span> <span data-ttu-id="40b87-152">가능한 값은 절대, 가운데, 아래쪽 왼쪽, 아래쪽 오른쪽, 맨 위 왼쪽, 오른쪽, 왼쪽(기본값은 아래쪽 왼쪽)입니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-152">Possible values are Absolute, Center, BottomLeft, BottomRight, TopLeft, TopRight, Right, and Left (the default is BottomLeft).</span></span>
- <span data-ttu-id="40b87-153">SampleControlId - 선택한 색상을 표시하는 컨트롤의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-153">SampleControlId - The ID of a control that displays the selected color.</span></span>
- <span data-ttu-id="40b87-154">선택색상 - ColorPicker가 선택한 초기 색상입니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-154">SelectedColor - The initial color selected by the ColorPicker.</span></span>

<span data-ttu-id="40b87-155">이러한 속성을 사용하여 색상 선택 대화 상자가 표시되는 방법과 선택한 색상이 표시되는 방법을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-155">You can use these properties to customize how the color picker dialog is displayed and how the selected color is displayed.</span></span> <span data-ttu-id="40b87-156">목록 3의 페이지에서는 이러한 속성 중 몇 가지를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-156">The page in Listing 3 illustrates how you can use several of these properties.</span></span>

<span data-ttu-id="40b87-157">**목록 3 - 만들기CardButton.aspx**</span><span class="sxs-lookup"><span data-stu-id="40b87-157">**Listing 3 - CreateCardButton.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample3.aspx)]

<span data-ttu-id="40b87-158">목록 3의 페이지에는 색상 선택 버튼이 포함되어 있습니다(그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="40b87-158">The page in Listing 3 includes a Pick Color button (see Figure 5).</span></span> <span data-ttu-id="40b87-159">이 단추를 클릭하면 텍스트 상자 위에 색상 선택기 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-159">When you click this button, the color picker dialog appears above the TextBox.</span></span> <span data-ttu-id="40b87-160">대화 상자에서 색상을 선택하면 선택한 색상이 lblSample 레이블 컨트롤의 배경색으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-160">If you select a color from the dialog then the selected color appears as the background color of the lblSample Label control.</span></span>

<span data-ttu-id="40b87-161">ColorPicker PopupButtonID 속성은 색상 선택 단추를 ColorPicker 익스텐더와 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-161">The ColorPicker PopupButtonID property is used to associate the Pick Color button with the ColorPicker extender.</span></span> <span data-ttu-id="40b87-162">PopupButtonID 속성에 대 한 값을 제공 하는 경우 대상 컨트롤에 포커스가 있을 때 색상 선택 대화 상자가 더 이상 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-162">When you supply a value for the PopupButtonID property, the color picker dialog no longer appears when the target control has focus.</span></span> <span data-ttu-id="40b87-163">대화 상자를 표시하려면 단추를 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-163">You must click the button to display the dialog.</span></span>

<span data-ttu-id="40b87-164">SampleControlID 속성은 선택한 색상을 ColorPicker와 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-164">The SampleControlID property is used to associate a control that displays the selected color with the ColorPicker.</span></span> <span data-ttu-id="40b87-165">ColorPicker는 이 컨트롤의 배경색을 현재 선택한 색상으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-165">The ColorPicker changes the background color of this control to the currently selected color.</span></span>

<span data-ttu-id="40b87-166">[![단추로 색상 선택 대화 상자 표시](using-the-colorpicker-control-extender-cs/_static/image5.jpg)](using-the-colorpicker-control-extender-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="40b87-166">[![Displaying the color picker dialog with a button](using-the-colorpicker-control-extender-cs/_static/image5.jpg)](using-the-colorpicker-control-extender-cs/_static/image9.png)</span></span>

<span data-ttu-id="40b87-167">**그림 05**: 버튼으로 색상 선택기 대화 상자 표시[(전체 크기 이미지를 보려면 클릭)](using-the-colorpicker-control-extender-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="40b87-167">**Figure 05**: Displaying the color picker dialog with a button ([Click to view full-size image](using-the-colorpicker-control-extender-cs/_static/image10.png))</span></span>

## <a name="summary"></a><span data-ttu-id="40b87-168">요약</span><span class="sxs-lookup"><span data-stu-id="40b87-168">Summary</span></span>

<span data-ttu-id="40b87-169">이 자습서에서는 ColorPicker 컨트롤 익스텐더를 사용하여 팝업 색상 선택기 대화 상자를 표시하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-169">In this tutorial, you learned how to use the ColorPicker control extender to display a popup color picker dialog.</span></span> <span data-ttu-id="40b87-170">먼저 포커스가 TextBox 컨트롤로 이동될 때 대화 상자를 표시하는 방법을 살펴보습니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-170">First, we examined how you can display the dialog when focus is moved to a TextBox control.</span></span> <span data-ttu-id="40b87-171">다음으로 단추를 클릭할 때 색상 선택 대화 상자를 표시하는 단추를 만드는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="40b87-171">Next, you learned how to create a button that displays the color picker dialog when the button is clicked.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="40b87-172">다음</span><span class="sxs-lookup"><span data-stu-id="40b87-172">Next</span></span>](using-the-colorpicker-control-extender-vb.md)
