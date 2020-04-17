---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
title: 콤보박스 컨트롤은 어떻게 사용하나요? (VB) | 마이크로 소프트 문서
author: rick-anderson
description: 콤보박스는 사용자가 선택할 수 있는 옵션 목록과 텍스트 상자의 유연성을 결합한 ASP.NET AJAX 컨트롤입니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: e887e7b2-a6e7-4a28-a134-ba334494badb
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 237e3ef864238c11fc1fb49239c3f6fa3f75537d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543069"
---
# <a name="how-do-i-use-the-combobox-control-vb"></a><span data-ttu-id="aeb26-104">콤보박스 컨트롤은 어떻게 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="aeb26-104">How do I use the ComboBox Control?</span></span> <span data-ttu-id="aeb26-105">(VB)</span><span class="sxs-lookup"><span data-stu-id="aeb26-105">(VB)</span></span>

<span data-ttu-id="aeb26-106">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="aeb26-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="aeb26-107">콤보박스는 사용자가 선택할 수 있는 옵션 목록과 텍스트 상자의 유연성을 결합한 ASP.NET AJAX 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-107">ComboBox is an ASP.NET AJAX control that combines the flexibility of a TextBox with a list of options from which users can choose.</span></span>

<span data-ttu-id="aeb26-108">이 자습서의 목표는 AJAX 제어 툴킷 콤보박스 컨트롤을 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-108">The goal of this tutorial is to explain the AJAX Control Toolkit ComboBox control.</span></span> <span data-ttu-id="aeb26-109">콤보박스는 표준 ASP.NET 드롭다운리스트 컨트롤과 텍스트 박스 컨트롤 사이의 조합처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-109">The ComboBox works like a combination between a standard ASP.NET DropDownList control and a TextBox control.</span></span> <span data-ttu-id="aeb26-110">기존 항목 목록에서 선택하거나 새 항목을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-110">You can either select from a pre-existing list of items or enter a new item.</span></span>

<span data-ttu-id="aeb26-111">ComboBox는 자동 완성 컨트롤 익스텐더와 유사하지만 컨트롤은 다른 시나리오에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-111">The ComboBox is similar to the AutoComplete control extender, but the controls are used in different scenarios.</span></span> <span data-ttu-id="aeb26-112">자동 완성 익스텐더는 웹 서비스를 쿼리하여 일치하는 항목을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-112">The AutoComplete extender queries a web service to get matching entries.</span></span> <span data-ttu-id="aeb26-113">반면 콤보박스 컨트롤은 항목 집합으로 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-113">The ComboBox control, in contrast, is initialized with a set of items.</span></span> <span data-ttu-id="aeb26-114">ComboBox 컨트롤을 사용하는 동안 대량의 데이터 세트(수백만 대의 자동차 부품)로 작업하는 동안 AutoComplete 익스텐더를 사용하면 작은 데이터 집합(수십 개의 자동차 부품)으로 작업하는 것이 합리적입니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-114">Using the AutoComplete extender makes sense when you are working with a large set of data (millions of car parts) while using the ComboBox control makes sense when working with a small set of data (dozens of car parts).</span></span>

## <a name="selecting-from-a-static-list-of-items"></a><span data-ttu-id="aeb26-115">항목의 정적 목록에서 선택</span><span class="sxs-lookup"><span data-stu-id="aeb26-115">Selecting from a Static List of Items</span></span>

<span data-ttu-id="aeb26-116">의 콤보 박스 컨트롤을 사용하는 간단한 샘플로 시작하자.</span><span class="sxs-lookup"><span data-stu-id="aeb26-116">Let�s start with a simple sample of using the ComboBox control.</span></span> <span data-ttu-id="aeb26-117">드롭다운 목록에 항목의 정적 목록을 표시하려고 한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-117">Imagine that you want to display a static list of items in a dropdown list.</span></span> <span data-ttu-id="aeb26-118">그러나 목록이 완료되지 않았을 가능성을 열어 두려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-118">However, you want to leave open the possibility that the list is not complete.</span></span> <span data-ttu-id="aeb26-119">사용자가 목록에 사용자 지정 값을 입력하도록 허용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-119">You want to allow a user to enter a custom value into the list.</span></span>

<span data-ttu-id="aeb26-120">새 ASP.NET 웹 폼 페이지를 만들고 페이지에서 ComboBox 컨트롤을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-120">We�ll create a new ASP.NET Web Forms page and use the ComboBox control in the page.</span></span> <span data-ttu-id="aeb26-121">새 ASP.NET 페이지를 프로젝트에 추가하고 디자인 보기로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-121">Add the new ASP.NET page to your project and switch to Design view.</span></span>

<span data-ttu-id="aeb26-122">페이지에서 ComboBox 컨트롤을 사용하려면 페이지에 ScriptManager 컨트롤을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-122">If you want to use the ComboBox control in the page then you must add a ScriptManager control to the page.</span></span> <span data-ttu-id="aeb26-123">AJAX 확장 탭 아래에서 디자이너 표면으로 ScriptManager 컨트롤을 끕니까.</span><span class="sxs-lookup"><span data-stu-id="aeb26-123">Drag the ScriptManager control from beneath the AJAX Extensions tab onto the Designer surface.</span></span> <span data-ttu-id="aeb26-124">페이지 맨 위에 ScriptManager 컨트롤을 추가해야 합니다. 서버 측 &lt;양식&gt; 태그 열기 바로 아래에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-124">You should add the ScriptManager control at the top of the page; you can add it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="aeb26-125">다음으로, ComboBox 컨트롤을 페이지로 드래그합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-125">Next, drag the ComboBox control onto the page.</span></span> <span data-ttu-id="aeb26-126">다른 AJAX 제어 툴킷 컨트롤 및 컨트롤 익스텐더와 함께 도구 상자에서 콤보박스 컨트롤을 찾을 수 있습니다(그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="aeb26-126">You can find the ComboBox control in the Toolbox with the other AJAX Control Toolkit controls and control extenders (see figure1).</span></span>

<span data-ttu-id="aeb26-127">[![명함을 만들기 위한 간단한 양식](how-do-i-use-the-combobox-control-vb/_static/image1.jpg)](how-do-i-use-the-combobox-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-127">[![Simple form for creating a business card](how-do-i-use-the-combobox-control-vb/_static/image1.jpg)](how-do-i-use-the-combobox-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="aeb26-128">**그림 01**: 도구 상자에서 콤보박스 컨트롤 선택[(전체 크기 이미지를 보려면 클릭)](how-do-i-use-the-combobox-control-vb/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-128">**Figure 01**: Selecting the ComboBox control from the toolbox ([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image2.png))</span></span>

<span data-ttu-id="aeb26-129">콤보박스 컨트롤을 사용하여 정적 선택 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-129">We�ll use the ComboBox control to display a static list of choices.</span></span> <span data-ttu-id="aeb26-130">사용자는 순, 중간 및 핫의 세 가지 선택 목록에서 음식에 대한 특정 수준의 매운 맛을 선택할 수 있습니다(그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="aeb26-130">The user can select a particular level of spiciness for their food from a list of three choices: Mild, Medium, and Hot (see Figure 2).</span></span>

<span data-ttu-id="aeb26-131">[![항목의 정적 목록에서 선택](how-do-i-use-the-combobox-control-vb/_static/image2.jpg)](how-do-i-use-the-combobox-control-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-131">[![Selecting from a static list of items](how-do-i-use-the-combobox-control-vb/_static/image2.jpg)](how-do-i-use-the-combobox-control-vb/_static/image3.png)</span></span>

<span data-ttu-id="aeb26-132">**그림 02**: 항목의 정적 목록에서 선택[(전체 크기 이미지를 보려면 클릭)](how-do-i-use-the-combobox-control-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-132">**Figure 02**: Selecting from a static list of items([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image4.png))</span></span>

<span data-ttu-id="aeb26-133">ComboBox 컨트롤에 이러한 옵션을 추가할 수 있는 방법에는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-133">There are two ways that you can add these choices to the ComboBox control.</span></span> <span data-ttu-id="aeb26-134">먼저 디자인 보기에서 컨트롤 위에 마우스를 가져가면 옵션 편집 작업 옵션을 선택하고 항목 편집기(그림 3 참조)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-134">First, you select the Edit Options task option when hovering your mouse over the control in Design view and open the Item Editor (see Figure 3).</span></span>

<span data-ttu-id="aeb26-135">[![콤보박스 항목 편집](how-do-i-use-the-combobox-control-vb/_static/image3.jpg)](how-do-i-use-the-combobox-control-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-135">[![Editing ComboBox items](how-do-i-use-the-combobox-control-vb/_static/image3.jpg)](how-do-i-use-the-combobox-control-vb/_static/image5.png)</span></span>

<span data-ttu-id="aeb26-136">**그림 03**: 콤보박스 항목 편집[(클릭하여 전체 크기 이미지 보기)](how-do-i-use-the-combobox-control-vb/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-136">**Figure 03**: Editing ComboBox items([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image6.png))</span></span>

<span data-ttu-id="aeb26-137">두 번째 옵션은 소스 보기에서 열기와 닫기 &lt;asp:ComboBox&gt; 태그 사이에 항목 목록을 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-137">The second option is to add the list of items in between the opening and closing &lt;asp:ComboBox&gt; tags in Source view.</span></span> <span data-ttu-id="aeb26-138">목록 1의 페이지에는 항목 목록이 있는 업데이트된 ComboBox가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-138">The page in Listing 1 contains the updated ComboBox that has the list of items.</span></span>

<span data-ttu-id="aeb26-139">**목록 1 - 정적.aspx**</span><span class="sxs-lookup"><span data-stu-id="aeb26-139">**Listing 1 - Static.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample1.aspx)]

<span data-ttu-id="aeb26-140">리스팅 1에서 페이지를 열면 ComboBox에서 기존 옵션 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-140">When you open the page in Listing 1, you can select one of the pre-existing options from the ComboBox.</span></span> <span data-ttu-id="aeb26-141">즉, 콤보박스는 드롭다운리스트 컨트롤처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-141">In other words, the ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="aeb26-142">그러나 기존 목록에 없는 새 선택(예: Super Spicy)을 입력할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-142">However, you also have the option of entering a new choice (for example, Super Spicy) that is not in the existing list.</span></span> <span data-ttu-id="aeb26-143">그래서, 콤보 박스는 텍스트 상자 컨트롤처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-143">So, the ComboBox also works like a TextBox control.</span></span>

<span data-ttu-id="aeb26-144">기존 항목을 선택하든 사용자 지정 항목을 입력하든 양식을 제출할 때 선택 항목이 레이블 컨트롤에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-144">Regardless of whether you pick a pre-existing item or you enter a custom item, when you submit the form, your choice appears in the label control.</span></span> <span data-ttu-id="aeb26-145">양식을 제출하면 btnSubmit\_Click 처리기가 레이블을 실행하고 업데이트합니다(그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="aeb26-145">When you submit the form, the btnSubmit\_Click handler executes and updates the label (see Figure 4).</span></span>

<span data-ttu-id="aeb26-146">[![선택한 항목 표시](how-do-i-use-the-combobox-control-vb/_static/image4.jpg)](how-do-i-use-the-combobox-control-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-146">[![Displaying the selected item](how-do-i-use-the-combobox-control-vb/_static/image4.jpg)](how-do-i-use-the-combobox-control-vb/_static/image7.png)</span></span>

<span data-ttu-id="aeb26-147">**그림 04**: 선택한 항목 표시[(전체 크기 이미지를 보려면 클릭)](how-do-i-use-the-combobox-control-vb/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-147">**Figure 04**: Displaying the selected item([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image8.png))</span></span>

<span data-ttu-id="aeb26-148">ComboBox는 양식을 제출한 후 선택한 항목을 검색하기 위한 DropDownList 컨트롤과 동일한 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-148">The ComboBox supports the same properties as the DropDownList control for retrieving the selected item after a form is submitted:</span></span>

- <span data-ttu-id="aeb26-149">SelectedItem.Text - 선택한 항목의 텍스트 속성 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-149">SelectedItem.Text - Displays the value of the Text property of the selected item.</span></span>
- <span data-ttu-id="aeb26-150">SelectedItem.Value - 선택한 항목의 Value 속성 값을 표시하거나 콤보박스에 입력된 텍스트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-150">SelectedItem.Value - Displays the value of the Value property of the selected item or displays the text typed into the ComboBox.</span></span>
- <span data-ttu-id="aeb26-151">Selected값 - 선택된 Item.Value와 동일합니다.이 속성을 사용하면 선택한 기본(초기) 항목을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-151">SelectedValue - Same as SelectedItem.Value except that this property enables you to specify the default (initial) selected item.</span></span>

<span data-ttu-id="aeb26-152">ComboBox에 사용자 지정 선택을 입력하면 사용자 지정 선택이 SelectedItem.Text 및 SelectedItem.Value 속성 모두에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-152">If you type a custom choice into the ComboBox then the custom choice is assigned to both the SelectedItem.Text and SelectedItem.Value properties.</span></span>

## <a name="selecting-the-list-of-items-from-the-database"></a><span data-ttu-id="aeb26-153">데이터베이스에서 항목 목록 선택</span><span class="sxs-lookup"><span data-stu-id="aeb26-153">Selecting the List of Items from the Database</span></span>

<span data-ttu-id="aeb26-154">데이터베이스에서 ComboBox가 표시하는 항목 목록을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-154">You can retrieve the list of items that the ComboBox displays from a database.</span></span> <span data-ttu-id="aeb26-155">예를 들어 ComboBox를 SqlDataSource 컨트롤, 개체 데이터 소스 컨트롤, LinqDataSource 또는 EntityDataSource에 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-155">For example, you can bind the ComboBox to a SqlDataSource control, an ObjectDataSource control, a LinqDataSource, or an EntityDataSource.</span></span>

<span data-ttu-id="aeb26-156">콤보박스에 영화 목록을 표시한다고 가정해 보십니까?</span><span class="sxs-lookup"><span data-stu-id="aeb26-156">Imagine that you want to display a list of movies in a ComboBox.</span></span> <span data-ttu-id="aeb26-157">Movies 데이터베이스 테이블에서 동영상 목록을 검색하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-157">You want to retrieve the list of movies from the Movies database table.</span></span> <span data-ttu-id="aeb26-158">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="aeb26-158">Follow these steps:</span></span>

1. <span data-ttu-id="aeb26-159">Movies.aspx라는 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="aeb26-159">Create a page named Movies.aspx</span></span>
2. <span data-ttu-id="aeb26-160">도구 상자의 AJAX 확장 탭 아래에서 스크립트 관리자를 페이지로 드래그하여 페이지에 ScriptManager 컨트롤을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-160">Add a ScriptManager control to the page by dragging the ScriptManager from under the AJAX Extensions tab in the Toolbox onto the page.</span></span>
3. <span data-ttu-id="aeb26-161">ComboBox를 페이지에 드래그하여 페이지에 콤보박스 컨트롤을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-161">Add a ComboBox control to the page by dragging the ComboBox onto the page.</span></span>
4. <span data-ttu-id="aeb26-162">디자인 보기에서 ComboBox 컨트롤 위로 마우스를 마우스로 가리키고 **데이터 원본** 작업 선택 옵션을 선택합니다(그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="aeb26-162">In Design view, hover your mouse over the ComboBox control and select the **Choose Data Source** task option (see Figure 5).</span></span> <span data-ttu-id="aeb26-163">데이터 원본 구성 마법사가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-163">The Data Source Configuration Wizard is launched.</span></span>
5. <span data-ttu-id="aeb26-164">데이터 **원본 선택** 단계에서 &lt;새 데이터 원본&gt; 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-164">In the **Choose a Data Source** step, select the &lt;New data source�&gt; option.</span></span>
6. <span data-ttu-id="aeb26-165">데이터 **원본 유형 선택** 단계에서 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-165">In the **Choose a Data Source Type** step, select Database.</span></span>
7. <span data-ttu-id="aeb26-166">데이터 연결 선택 단계에서 데이터베이스(예: MoviesDB.mdf)를 **선택합니다.**</span><span class="sxs-lookup"><span data-stu-id="aeb26-166">In the **Choose Your Data Connection** step, select your database (for example, MoviesDB.mdf).</span></span>
8. <span data-ttu-id="aeb26-167">응용 **프로그램 구성 파일** 파일에 연결 문자열 저장 단계에서 연결 문자열을 저장하는 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-167">In the **Save the Connection String to the Application Configuration File** step, select the option to save your connection string.</span></span>
9. <span data-ttu-id="aeb26-168">**명령문 선택** 구성 단계에서 Movies 데이터베이스 테이블을 선택하고 모든 열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-168">In the **Configure the Select Statement** step, select the Movies database table and select all of the columns.</span></span>
10. <span data-ttu-id="aeb26-169">테스트 **쿼리** 단계에서 완료 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-169">In the **Test Query** step, click the Finish button.</span></span>
11. <span data-ttu-id="aeb26-170">**데이터 원본 선택** 단계에서 표시할 필드의 제목 열과 데이터 필드의 ID 열을 선택합니다(그림 참조).</span><span class="sxs-lookup"><span data-stu-id="aeb26-170">Back in the **Choose Data Source** step, select the Title column for the field to display and the Id column for the data field (see Figure).</span></span>
12. <span data-ttu-id="aeb26-171">확인 버튼을 클릭하여 마법사를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-171">Click the OK button to close the wizard.</span></span>

<span data-ttu-id="aeb26-172">[![데이터 원본 선택](how-do-i-use-the-combobox-control-vb/_static/image5.jpg)](how-do-i-use-the-combobox-control-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-172">[![Choosing a data source](how-do-i-use-the-combobox-control-vb/_static/image5.jpg)](how-do-i-use-the-combobox-control-vb/_static/image9.png)</span></span>

<span data-ttu-id="aeb26-173">**그림 05**: 데이터 원본 선택[(전체 크기 이미지를 보려면 클릭)](how-do-i-use-the-combobox-control-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-173">**Figure 05**: Choosing a data source([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image10.png))</span></span>

<span data-ttu-id="aeb26-174">[![데이터 텍스트 및 값 필드 선택](how-do-i-use-the-combobox-control-vb/_static/image6.jpg)](how-do-i-use-the-combobox-control-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-174">[![Choosing the data text and value fields](how-do-i-use-the-combobox-control-vb/_static/image6.jpg)](how-do-i-use-the-combobox-control-vb/_static/image11.png)</span></span>

<span data-ttu-id="aeb26-175">**그림 06**: 데이터 텍스트 및 값 필드 선택[(전체 크기 이미지를 보려면 클릭)](how-do-i-use-the-combobox-control-vb/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-175">**Figure 06**: Choosing the data text and value fields([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image12.png))</span></span>

<span data-ttu-id="aeb26-176">위의 단계를 완료하면 ComboBox는 Movies 데이터베이스 테이블의 동영상을 나타내는 SqlDataSource 컨트롤에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-176">After you complete the steps above, the ComboBox is bound to a SqlDataSource control that represents the movies from the Movies database table.</span></span> <span data-ttu-id="aeb26-177">페이지의 소스는 목록 2처럼 보입니다 (서식을 약간 정리했습니다).</span><span class="sxs-lookup"><span data-stu-id="aeb26-177">The source for the page looks like Listing 2 (I cleaned up the formatting a little bit).</span></span>

<span data-ttu-id="aeb26-178">**리스팅 2 - 영화.aspx**</span><span class="sxs-lookup"><span data-stu-id="aeb26-178">**Listing 2 - Movies.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample2.aspx)]

<span data-ttu-id="aeb26-179">콤보박스 컨트롤에는 SqlDataSource 컨트롤을 가리키는 DataSourceID 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-179">Notice that the ComboBox control has a DataSourceID property that points to the SqlDataSource control.</span></span> <span data-ttu-id="aeb26-180">브라우저에서 페이지를 열면 데이터베이스의 동영상 목록이 표시됩니다(그림 7 참조).</span><span class="sxs-lookup"><span data-stu-id="aeb26-180">When you open the page in a browser, the list of movies from the database is displayed (see Figure 7).</span></span> <span data-ttu-id="aeb26-181">목록에서 영화를 선택하거나 ComboBox에 영화를 입력하여 새 영화를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-181">You can either a pick a movie from the list or enter a new movie by typing the movie into the ComboBox.</span></span>

<span data-ttu-id="aeb26-182">[![영화 목록 표시](how-do-i-use-the-combobox-control-vb/_static/image7.jpg)](how-do-i-use-the-combobox-control-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-182">[![Displaying a list of movies](how-do-i-use-the-combobox-control-vb/_static/image7.jpg)](how-do-i-use-the-combobox-control-vb/_static/image13.png)</span></span>

<span data-ttu-id="aeb26-183">**그림 07**: 동영상 목록[표시(전체 크기 이미지를 보려면 클릭)](how-do-i-use-the-combobox-control-vb/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-183">**Figure 07**: Displaying a list of movies([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image14.png))</span></span>

## <a name="setting-the-dropdownstyle"></a><span data-ttu-id="aeb26-184">드롭다운 스타일 설정</span><span class="sxs-lookup"><span data-stu-id="aeb26-184">Setting the DropDownStyle</span></span>

<span data-ttu-id="aeb26-185">콤보박스 드롭다운스타일 속성을 사용하여 콤보박스의 동작을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-185">You can use the ComboBox DropDownStyle property to change the behavior of the ComboBox.</span></span> <span data-ttu-id="aeb26-186">이 속성은 가능한 값을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-186">This property accepts there possible values:</span></span>

- <span data-ttu-id="aeb26-187">드롭다운 - (기본값) 화살표를 클릭하면 ComboBox에 드롭다운 목록이 표시되고 사용자 지정 값을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-187">DropDown - (default value) The ComboBox displays a dropdown list when you click the arrow and you can enter a custom value.</span></span>
- <span data-ttu-id="aeb26-188">단순 - 콤보박스는 드롭다운 목록을 자동으로 표시하며 사용자 지정 값을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-188">Simple - The ComboBox displays a dropdown list automatically and you can enter a custom value.</span></span>
- <span data-ttu-id="aeb26-189">드롭다운목록 - 콤보박스는 드롭다운리스트 컨트롤처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-189">DropDownList - The ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="aeb26-190">드롭다운과 단순의 차이점은 항목 목록이 표시되는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-190">The different between DropDown and Simple is when the list of items is displayed.</span></span> <span data-ttu-id="aeb26-191">단순의 경우 포커스를 콤보박스로 이동할 때 목록이 즉시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-191">In the case of Simple, the list is displayed immediately when you move focus to the ComboBox.</span></span> <span data-ttu-id="aeb26-192">드롭다운의 경우 화살표를 클릭하여 항목 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-192">In the case of DropDown, you must click the arrow to see the list of items.</span></span>

<span data-ttu-id="aeb26-193">드롭다운목록 값을 사용하면 ComboBox 컨트롤이 표준 드롭다운리스트 컨트롤처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-193">The DropDownList value causes the ComboBox control to work just like a standard DropDownList control.</span></span> <span data-ttu-id="aeb26-194">그러나 여기에는 중요한 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-194">However, there is an important difference here.</span></span> <span data-ttu-id="aeb26-195">이전 버전의 Internet Explorer에는 무한 z 인덱스가 있는 DropDownList 컨트롤이 표시되므로 컨트롤이 앞에 배치된 컨트롤 앞에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-195">Older versions of Internet Explorer display a DropDownList control with an infinite z-index so the control will appear in front of any control placed in front of it.</span></span> <span data-ttu-id="aeb26-196">&lt;콤보박스는 HTML 선택&gt; &lt;&gt; 태그 대신 HTML div 태그를 렌더링하므로 ComboBox는 z 순서를 올바르게 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-196">Because the ComboBox renders an HTML &lt;div&gt; tag instead of an HTML &lt;select&gt; tag, the ComboBox correctly respects z-ordering.</span></span>

## <a name="setting-the-autocompletemode"></a><span data-ttu-id="aeb26-197">자동 컴컴 모드 설정</span><span class="sxs-lookup"><span data-stu-id="aeb26-197">Setting the AutoCompleteMode</span></span>

<span data-ttu-id="aeb26-198">ComboBox 자동 완료 모드 속성을 사용 하 여 다른 사용자가 ComboBox에 텍스트를 입력 할 때 발생 하는 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-198">You use the ComboBox AutoCompleteMode property to specify what happens when someone types text into the ComboBox.</span></span> <span data-ttu-id="aeb26-199">이 속성은 다음과 같은 가능한 값을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-199">This property accepts the following possible values:</span></span>

- <span data-ttu-id="aeb26-200">없음 - (기본값) ComboBox는 자동 완성 동작을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-200">None - (default value) The ComboBox does not provide any auto-complete behavior.</span></span>
- <span data-ttu-id="aeb26-201">제안 - ComboBox는 목록을 표시하고 목록에서 일치하는 항목을 강조 표시합니다(그림 8 참조).</span><span class="sxs-lookup"><span data-stu-id="aeb26-201">Suggest - The ComboBox displays the list and it highlights the matching item in the list (see Figure 8).</span></span>
- <span data-ttu-id="aeb26-202">추가 - ComboBox는 목록을 표시하지 않으며 목록에서 입력한 항목에 일치하는 항목을 추가합니다(그림 9 참조).</span><span class="sxs-lookup"><span data-stu-id="aeb26-202">Append - The ComboBox does not display the list and it appends the matching item from the list onto what you have typed (see Figure 9).</span></span>
- <span data-ttu-id="aeb26-203">제안 앱- ComboBox는 모두 목록을 표시하고 목록에서 일치하는 항목을 입력한 항목으로 추가합니다(그림 10 참조).</span><span class="sxs-lookup"><span data-stu-id="aeb26-203">SuggestAppend - The ComboBox both displays the list and appends the matching item from the list onto what you have typed (see Figure 10).</span></span>

<span data-ttu-id="aeb26-204">[![콤보 박스는 제안을합니다](how-do-i-use-the-combobox-control-vb/_static/image8.jpg)](how-do-i-use-the-combobox-control-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-204">[![The ComboBox makes a suggestion](how-do-i-use-the-combobox-control-vb/_static/image8.jpg)](how-do-i-use-the-combobox-control-vb/_static/image15.png)</span></span>

<span data-ttu-id="aeb26-205">**그림 08**: 콤보박스가 제안을[합니다(전체 크기 이미지를 보려면 클릭하세요)](how-do-i-use-the-combobox-control-vb/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-205">**Figure 08**: The ComboBox makes a suggestion([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image16.png))</span></span>

<span data-ttu-id="aeb26-206">[![콤보 박스는 일치하는 텍스트를 부속](how-do-i-use-the-combobox-control-vb/_static/image9.jpg)](how-do-i-use-the-combobox-control-vb/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-206">[![ComboBox appends matching text](how-do-i-use-the-combobox-control-vb/_static/image9.jpg)](how-do-i-use-the-combobox-control-vb/_static/image17.png)</span></span>

<span data-ttu-id="aeb26-207">**그림 09**: ComboBox는 일치하는 텍스트를 추가했다[(클릭을 클릭하여 전체 크기 이미지 보기)](how-do-i-use-the-combobox-control-vb/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-207">**Figure 09**: ComboBox appends matching text([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image18.png))</span></span>

<span data-ttu-id="aeb26-208">[![콤보 박스 제안 하 고 부속](how-do-i-use-the-combobox-control-vb/_static/image10.jpg)](how-do-i-use-the-combobox-control-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-208">[![The ComboBox suggests and appends](how-do-i-use-the-combobox-control-vb/_static/image10.jpg)](how-do-i-use-the-combobox-control-vb/_static/image19.png)</span></span>

<span data-ttu-id="aeb26-209">**그림 10**: 콤보박스가 제안하고 부속[(클릭하여 전체 크기 이미지를 보려면 클릭)](how-do-i-use-the-combobox-control-vb/_static/image20.png)</span><span class="sxs-lookup"><span data-stu-id="aeb26-209">**Figure 10**: The ComboBox suggests and appends([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image20.png))</span></span>

## <a name="summary"></a><span data-ttu-id="aeb26-210">요약</span><span class="sxs-lookup"><span data-stu-id="aeb26-210">Summary</span></span>

<span data-ttu-id="aeb26-211">이 자습서에서는 ComboBox 컨트롤을 사용하여 고정된 항목 집합을 표시하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-211">In this tutorial, you learned how to use the ComboBox control to display a fixed set of items.</span></span> <span data-ttu-id="aeb26-212">ComboBox 컨트롤을 정적 항목 집합과 데이터베이스 테이블에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-212">We bound the ComboBox control both to a static set of items and to a database table.</span></span> <span data-ttu-id="aeb26-213">마지막으로 드롭다운 스타일 및 자동 컴컴 모드 속성을 설정하여 콤보박스의 동작을 수정하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb26-213">Finally, you learned how to modify the behavior of the ComboBox by setting its DropDownStyle and AutoCompleteMode properties.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="aeb26-214">이전</span><span class="sxs-lookup"><span data-stu-id="aeb26-214">Previous</span></span>](how-do-i-use-the-combobox-control-cs.md)
