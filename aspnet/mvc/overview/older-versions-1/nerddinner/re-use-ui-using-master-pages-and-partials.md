---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: 마스터 페이지 및 부분 페이지를 사용하여 UI 재사용 | 마이크로 소프트 문서
author: rick-anderson
description: 7단계에서는 부분 보기 템플릿과 마스터 페이지를 사용하여 코드 중복을 제거하기 위해 뷰 템플릿 내에서 'DRY 원칙'을 적용할 수 있는 방법을 살펴봅니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: f381c4424a9fa0718cd234beeb01ce41bc4ca61e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542601"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a><span data-ttu-id="329d1-103">마스터 페이지 및 부분을 사용하여 UI 재사용</span><span class="sxs-lookup"><span data-stu-id="329d1-103">Re-use UI Using Master Pages and Partials</span></span>

<span data-ttu-id="329d1-104">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="329d1-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="329d1-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="329d1-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="329d1-106">이것은 MVC 1을 ASP.NET 사용하여 작지만 완전한 웹 응용 프로그램을 빌드하는 방법을 안내하는 무료 ["NerdDinner" 응용 프로그램 자습서의](introducing-the-nerddinner-tutorial.md) 7단계입니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-106">This is step 7 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="329d1-107">7단계는 부분 보기 템플릿 및 마스터 페이지를 사용하여 코드 중복을 제거하기 위해 뷰 템플릿 내에서 "DRY 원칙"을 적용할 수 있는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-107">Step 7 looks at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication, using partial view templates and master pages.</span></span>
> 
> <span data-ttu-id="329d1-108">MVC 3을 ASP.NET 사용하는 경우 [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC 뮤직 스토어](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-7-partials-and-master-pages"></a><span data-ttu-id="329d1-109">얼간이 저녁 식사 단계 7: 부분 및 마스터 페이지</span><span class="sxs-lookup"><span data-stu-id="329d1-109">NerdDinner Step 7: Partials and Master Pages</span></span>

<span data-ttu-id="329d1-110">MVC가 ASP.NET 디자인 철학 중 하나는 "자신을 반복하지 마십시오" 원칙(일반적으로 "DRY"라고 함)입니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-110">One of the design philosophies ASP.NET MVC embraces is the "Do Not Repeat Yourself" principle (commonly referred to as "DRY").</span></span> <span data-ttu-id="329d1-111">DRY 디자인은 코드와 논리의 중복을 제거하는 데 도움이 되며, 궁극적으로 응용 프로그램을 더 빠르게 빌드하고 유지 관리가 쉬워집니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-111">A DRY design helps eliminate the duplication of code and logic, which ultimately makes applications faster to build and easier to maintain.</span></span>

<span data-ttu-id="329d1-112">우리는 이미 우리의 NerdDinner 시나리오의 몇 가지에 적용 된 DRY 원리를 보았다.</span><span class="sxs-lookup"><span data-stu-id="329d1-112">We've already seen the DRY principle applied in several of our NerdDinner scenarios.</span></span> <span data-ttu-id="329d1-113">몇 가지 예: 유효성 검사 논리는 모델 계층 내에서 구현되므로 컨트롤러에서 편집 및 생성 시나리오 모두에서 적용할 수 있습니다. 편집, 세부 정보 및 삭제 작업 메서드에서 "NotFound" 보기 템플릿을 다시 사용하고 있습니다. 뷰 템플릿을 사용하여 규칙-명명 패턴을 사용하고 있으므로 View() 도우미 메서드를 호출할 때 이름을 명시적으로 지정할 필요가 없습니다. 편집 및 만들기 작업 시나리오모두에 DinnerFormViewModel 클래스를 다시 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-113">A few examples: our validation logic is implemented within our model layer, which enables it to be enforced across both edit and create scenarios in our controller; we are re-using the "NotFound" view template across the Edit, Details and Delete action methods; we are using a convention- naming pattern with our view templates, which eliminates the need to explicitly specify the name when we call the View() helper method; and we are re-using the DinnerFormViewModel class for both Edit and Create action scenarios.</span></span>

<span data-ttu-id="329d1-114">이제 뷰 템플릿 내에서 "DRY 원칙"을 적용하여 코드 중복을 제거할 수 있는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-114">Let's now look at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication there as well.</span></span>

### <a name="re-visiting-our-edit-and-create-view-templates"></a><span data-ttu-id="329d1-115">편집 및 뷰 템플릿 만들기 다시 방문</span><span class="sxs-lookup"><span data-stu-id="329d1-115">Re-visiting our Edit and Create View Templates</span></span>

<span data-ttu-id="329d1-116">현재 우리는 두 개의 서로 다른 보기 템플릿을 사용 하 여- "Edit.aspx" 그리고 "Create.aspx" - 우리의 저녁 식사 양식 UI를 표시 하려면.</span><span class="sxs-lookup"><span data-stu-id="329d1-116">Currently we are using two different view templates – "Edit.aspx" and "Create.aspx" – to display our Dinner form UI.</span></span> <span data-ttu-id="329d1-117">빠른 시각적 비교는 그들이 얼마나 비슷한지 강조합니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-117">A quick visual comparison of them highlights how similar they are.</span></span> <span data-ttu-id="329d1-118">다음은 만들기 양식의 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-118">Below is what the create form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

<span data-ttu-id="329d1-119">그리고 여기에 우리의 "편집"양식의 모습은 다음과 같습니다 :</span><span class="sxs-lookup"><span data-stu-id="329d1-119">And here is what our "Edit" form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

<span data-ttu-id="329d1-120">큰 차이는 없는가요?</span><span class="sxs-lookup"><span data-stu-id="329d1-120">Not much of a difference is there?</span></span> <span data-ttu-id="329d1-121">제목 및 헤더 텍스트 이외에 양식 레이아웃과 입력 컨트롤은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-121">Other than the title and header text, the form layout and input controls are identical.</span></span>

<span data-ttu-id="329d1-122">"Edit.aspx" 및 "Create.aspx" 보기 템플릿을 열면 동일한 양식 레이아웃 및 입력 제어 코드가 포함되어 있음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-122">If we open up the "Edit.aspx" and "Create.aspx" view templates we'll find that they contain identical form layout and input control code.</span></span> <span data-ttu-id="329d1-123">이 중복은 우리가 소개하거나 새로운 Dinner 속성을 변경할 때마다 두 번 변경해야 한다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-123">This duplication means we end up having to make changes twice anytime we introduce or change a new Dinner property - which is not good.</span></span>

### <a name="using-partial-view-templates"></a><span data-ttu-id="329d1-124">부분 뷰 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="329d1-124">Using Partial View Templates</span></span>

<span data-ttu-id="329d1-125">ASP.NET MVC는 페이지의 하위 부분에 대한 뷰 렌더링 논리를 캡슐화하는 데 사용할 수 있는 "부분 보기" 템플릿을 정의하는 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-125">ASP.NET MVC supports the ability to define "partial view" templates that can be used to encapsulate view rendering logic for a sub-portion of a page.</span></span> <span data-ttu-id="329d1-126">"Partials"는 뷰 렌더링 논리를 한 번 정의한 다음 응용 프로그램 전체의 여러 위치에서 다시 사용할 수 있는 유용한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-126">"Partials" provide a useful way to define view rendering logic once, and then re-use it in multiple places across an application.</span></span>

<span data-ttu-id="329d1-127">Edit.aspx 및 Create.aspx 뷰 템플릿 중복을 "DRY-up"하는 데 도움이 되도록 폼 레이아웃 과 두 가지 모두에 공통적인 입력 요소를 캡슐화하는 "DinnerForm.ascx"라는 부분 뷰 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-127">To help "DRY-up" our Edit.aspx and Create.aspx view template duplication, we can create a partial view template named "DinnerForm.ascx" that encapsulates the form layout and input elements common to both.</span></span> <span data-ttu-id="329d1-128">우리는 우리의 / 보기 / 저녁 식사 디렉토리를 마우스 오른쪽 버튼으로 클릭하고 "추가 보기"메뉴&gt;명령을 선택하여이 작업을 수행 할 수 있습니다 :</span><span class="sxs-lookup"><span data-stu-id="329d1-128">We'll do this by right-clicking on our /Views/Dinners directory and choosing the "Add-&gt;View" menu command:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

<span data-ttu-id="329d1-129">그러면 "보기 추가" 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-129">This will display the "Add View" dialog.</span></span> <span data-ttu-id="329d1-130">"DinnerForm"을 만들 새 뷰의 이름을 지정하고 대화 상자 내에서 "부분 보기 만들기" 확인란을 선택하고 DinnerFormViewModel 클래스를 전달할 것임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-130">We'll name the new view we want to create "DinnerForm", select the "Create a partial view" checkbox within the dialog, and indicate that we will pass it a DinnerFormViewModel class:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

<span data-ttu-id="329d1-131">"추가" 단추를 클릭하면 Visual Studio에서 "\View\Dinners" 디렉토리 내에서 새 "DinnerForm.ascx" 보기 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-131">When we click the "Add" button, Visual Studio will create a new "DinnerForm.ascx" view template for us within the "\Views\Dinners" directory.</span></span>

<span data-ttu-id="329d1-132">그런 다음 Edit.aspx/ Create.aspx 보기 템플릿에서 중복 양식 레이아웃/입력 제어 코드를 새 "DinnerForm.ascx" 부분 보기 템플릿에 복사/붙여넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-132">We can then copy/paste the duplicate form layout / input control code from our Edit.aspx/ Create.aspx view templates into our new "DinnerForm.ascx" partial view template:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

<span data-ttu-id="329d1-133">그런 다음 편집 및 뷰 만들기 템플릿을 업데이트하여 DinnerForm 부분 템플릿을 호출하고 양식 중복을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-133">We can then update our Edit and Create view templates to call the DinnerForm partial template and eliminate the form duplication.</span></span> <span data-ttu-id="329d1-134">뷰 템플릿 내에서 Html.RenderPartial("DinnerForm")를 호출하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-134">We can do this by calling Html.RenderPartial("DinnerForm") within our view templates:</span></span>

##### <a name="createaspx"></a><span data-ttu-id="329d1-135">만들기.aspx</span><span class="sxs-lookup"><span data-stu-id="329d1-135">Create.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a><span data-ttu-id="329d1-136">편집.aspx</span><span class="sxs-lookup"><span data-stu-id="329d1-136">Edit.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

<span data-ttu-id="329d1-137">Html.RenderPartial(예: ~보기/Dinners/DinnerForm.ascx)를 호출할 때 원하는 부분 템플릿의 경로를 명시적으로 한정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-137">You can explicitly qualify the path of the partial template you want when calling Html.RenderPartial (for example: ~Views/Dinners/DinnerForm.ascx").</span></span> <span data-ttu-id="329d1-138">그러나 위의 코드에서는 ASP.NET MVC 내에서 규칙 기반 명명 패턴을 활용하고 렌더링할 부분의 이름으로 "DinnerForm"을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-138">In our code above, though, we are taking advantage of the convention-based naming pattern within ASP.NET MVC, and just specifying "DinnerForm" as the name of the partial to render.</span></span> <span data-ttu-id="329d1-139">이 작업을 수행할 때 MVC는 컨벤션 기반 뷰 디렉토리에서 먼저 살펴볼 ASP.NET.이 컨트롤러의 경우 /View/Dinners가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-139">When we do this ASP.NET MVC will look first in the convention-based views directory (for DinnersController this would be /Views/Dinners).</span></span> <span data-ttu-id="329d1-140">부분 템플릿을 찾지 못하면 /View /Shared 디렉터리에서 해당 템플릿을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-140">If it doesn't find the partial template there it will then look for it in the /Views/Shared directory.</span></span>

<span data-ttu-id="329d1-141">Html.RenderPartial()가 부분 뷰의 이름만으로 호출되면 ASP.NET mVC가 호출 뷰 템플릿에서 사용하는 것과 동일한 모델 및 ViewData 사전 개체를 부분 뷰로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-141">When Html.RenderPartial() is called with just the name of the partial view, ASP.NET MVC will pass to the partial view the same Model and ViewData dictionary objects used by the calling view template.</span></span> <span data-ttu-id="329d1-142">또는 부분 뷰를 사용할 대체 모델 개체 및/또는 ViewData 사전을 전달할 수 있는 Html.RenderPartial()의 오버로드된 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-142">Alternatively, there are overloaded versions of Html.RenderPartial() that enable you to pass an alternate Model object and/or ViewData dictionary for the partial view to use.</span></span> <span data-ttu-id="329d1-143">이 기능은 전체 모델/뷰모델의 하위 집합만 전달하려는 시나리오에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-143">This is useful for scenarios where you only want to pass a subset of the full Model/ViewModel.</span></span>

| <span data-ttu-id="329d1-144">**측면 주제: &lt;&gt; &lt;왜 % 대신&gt;%= % ?**</span><span class="sxs-lookup"><span data-stu-id="329d1-144">**Side Topic: Why &lt;% %&gt; instead of &lt;%= %&gt;?**</span></span> |
| --- |
| <span data-ttu-id="329d1-145">위의 코드에서 발견 할 수있는 미묘한 것 중 하나는 &lt;Html.RenderPartial ()를 호출 할 때&gt; &lt;%= % 블록 대신 % %&gt; 블록을 사용하고 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-145">One of the subtle things you might have noticed with the code above is that we are using a &lt;% %&gt; block instead of a &lt;%= %&gt; block when calling Html.RenderPartial().</span></span> <span data-ttu-id="329d1-146">&lt;ASP.NET %= %&gt; 블록은 개발자가 지정된 값을 렌더링하려고 &lt;함을 나타냅니다(예:&gt; %= "Hello" %는 "Hello"를 렌더링합니다).</span><span class="sxs-lookup"><span data-stu-id="329d1-146">&lt;%= %&gt; blocks in ASP.NET indicate that a developer wants to render a specified value (for example: &lt;%= "Hello" %&gt; would render "Hello").</span></span> <span data-ttu-id="329d1-147">&lt;%&gt; 블록대신 개발자가 코드를 실행하려고 함을 나타내며, 그 안에 렌더링된 출력은 &lt;명시적으로 수행되어야 함을 나타냅니다(예: % Response.Write("Hello") %&gt;</span><span class="sxs-lookup"><span data-stu-id="329d1-147">&lt;% %&gt; blocks instead indicate that the developer wants to execute code, and that any rendered output within them must be done explicitly (for example: &lt;% Response.Write("Hello") %&gt;.</span></span> <span data-ttu-id="329d1-148">위의 Html.RenderPartial &lt;코드에서 % 블록을&gt; 사용하는 이유는 Html.RenderPartial() 메서드가 문자열을 반환하지 않고 대신 콘텐츠를 호출 뷰 템플릿의 출력 스트림으로 직접 출력하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-148">The reason we are using a &lt;% %&gt; block with our Html.RenderPartial code above is because the Html.RenderPartial() method doesn't return a string, and instead outputs the content directly to the calling view template's output stream.</span></span> <span data-ttu-id="329d1-149">성능 효율성을 위해 이 작업을 수행하므로 (잠재적으로 매우 큰) 임시 문자열 개체를 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-149">It does this for performance efficiency reasons, and by doing so it avoids the need to create a (potentially very large) temporary string object.</span></span> <span data-ttu-id="329d1-150">이렇게 하면 메모리 사용량이 줄어들고 전체 응용 프로그램 처리량이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-150">This reduces memory usage and improves overall application throughput.</span></span> <span data-ttu-id="329d1-151">Html.RenderPartial()를 사용할 때 의 한 가지 일반적인 실수는 % &lt;&gt; 블록 내에 있을 때 호출이 끝날 때 세미 콜론을 추가하는 것을 잊어버리는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-151">One common mistake when using Html.RenderPartial() is to forget to add a semi-colon at the end of the call when it is within a &lt;% %&gt; block.</span></span> <span data-ttu-id="329d1-152">예를 들어, 이 코드는 컴파일러 &lt;오류를 발생 합니다: % Html.RenderPartial ("DinnerForm") 대신&gt; 작성 해야: &lt;% Html.RenderPartial ("DinnerForm"); %&gt; &gt; 블록은 &lt;자체 포함된 코드 문이며 C# 코드 문을 사용하는 경우 세미 콜론으로 종료해야 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-152">For example, this code will cause a compiler error: &lt;% Html.RenderPartial("DinnerForm") %&gt; You instead need to write: &lt;% Html.RenderPartial("DinnerForm"); %&gt; This is because &lt;% %&gt; blocks are self-contained code statements, and when using C# code statements need to be terminated with a semi-colon.</span></span> |

### <a name="using-partial-view-templates-to-clarify-code"></a><span data-ttu-id="329d1-153">부분 보기 템플릿을 사용하여 코드 명확성</span><span class="sxs-lookup"><span data-stu-id="329d1-153">Using Partial View Templates to Clarify Code</span></span>

<span data-ttu-id="329d1-154">여러 위치에서 뷰 렌더링 논리가 중복되지 않도록 "DinnerForm" 부분 뷰 템플릿을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-154">We created the "DinnerForm" partial view template to avoid duplicating view rendering logic in multiple places.</span></span> <span data-ttu-id="329d1-155">이것이 부분 보기 템플릿을 만드는 가장 일반적인 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-155">This is the most common reason to create partial view templates.</span></span>

<span data-ttu-id="329d1-156">때로는 한 곳에서만 호출되는 경우에도 부분 뷰를 만드는 것이 합리적입니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-156">Sometimes it still makes sense to create partial views even when they are only being called in a single place.</span></span> <span data-ttu-id="329d1-157">뷰 렌더링 논리를 추출하고 하나 이상의 잘 명명된 부분 템플릿으로 분할할 때 매우 복잡한 뷰 템플릿을 읽기가 훨씬 쉬워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-157">Very complicated view templates can often become much easier to read when their view rendering logic is extracted and partitioned into one or more well named partial templates.</span></span>

<span data-ttu-id="329d1-158">예를 들어 프로젝트의 Site.master 파일에서 아래 코드 조각을 살펴보겠습니다(곧 살펴보겠습니다).</span><span class="sxs-lookup"><span data-stu-id="329d1-158">For example, consider the below code-snippet from the Site.master file in our project (which we will be looking at shortly).</span></span> <span data-ttu-id="329d1-159">코드는 비교적 간단하게 읽을 수 있습니다 - 부분적으로 화면 오른쪽 상단에 로그인 /로그 아웃 링크를 표시하는 논리가 "LogOnUserControl"부분 내에 캡슐화되어 있기 때문에:</span><span class="sxs-lookup"><span data-stu-id="329d1-159">The code is relatively straight-forward to read – partly because the logic to display a login/logout link at the top right of the screen is encapsulated within the "LogOnUserControl" partial:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

<span data-ttu-id="329d1-160">뷰 템플릿 내에서 html/코드 태그를 이해하려고 애쓰는 것이 혼란스러울 때마다 일부 가 추출되어 잘 명명된 부분 뷰로 리팩터링된 경우 더 명확하지 않은지 고려하십시오.</span><span class="sxs-lookup"><span data-stu-id="329d1-160">Whenever you find yourself getting confused trying to understand the html/code markup within a view-template, consider whether it wouldn't be clearer if some of it was extracted and refactored into well-named partial views.</span></span>

### <a name="master-pages"></a><span data-ttu-id="329d1-161">마스터 페이지</span><span class="sxs-lookup"><span data-stu-id="329d1-161">Master Pages</span></span>

<span data-ttu-id="329d1-162">ASP.NET MVC는 부분 보기를 지원하는 것 외에도 사이트의 공통 레이아웃 및 최상위 HTML을 정의하는 데 사용할 수 있는 "마스터 페이지" 템플릿을 만드는 기능도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-162">In addition to supporting partial views, ASP.NET MVC also supports the ability to create "master page" templates that can be used to define the common layout and top-level html of a site.</span></span> <span data-ttu-id="329d1-163">그런 다음 콘텐츠 자리 표시자 컨트롤을 마스터 페이지에 추가하여 뷰별로 재정의하거나 "채우기"할 수 있는 대체 가능한 영역을 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-163">Content placeholder controls can then be added to the master page to identify replaceable regions that can be overridden or "filled in" by views.</span></span> <span data-ttu-id="329d1-164">이렇게 하면 응용 프로그램 전체에 공통 레이아웃을 적용하는 매우 효과적인(및 DRY) 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-164">This provides a very effective (and DRY) way to apply a common layout across an application.</span></span>

<span data-ttu-id="329d1-165">기본적으로 새 ASP.NET MVC 프로젝트에는 마스터 페이지 템플릿이 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-165">By default, new ASP.NET MVC projects have a master page template automatically added to them.</span></span> <span data-ttu-id="329d1-166">이 마스터 페이지의 이름은 "Site.master"이며 \View\Shared\ 폴더 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-166">This master page is named "Site.master" and lives within the \Views\Shared\ folder:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

<span data-ttu-id="329d1-167">기본 Site.master 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-167">The default Site.master file looks like below.</span></span> <span data-ttu-id="329d1-168">사이트의 외부 html과 상단탐색 메뉴를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-168">It defines the outer html of the site, along with a menu for navigation at the top.</span></span> <span data-ttu-id="329d1-169">여기에는 두 개의 대체 가능한 콘텐츠 자리 표시자 컨트롤(하나는 제목용이고 다른 하나는 페이지의 기본 콘텐츠를 대체해야 하는 컨트롤)이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-169">It contains two replaceable content placeholder controls – one for the title, and the other for where the primary content of a page should be replaced:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

<span data-ttu-id="329d1-170">NerdDinner 응용 프로그램("목록", "세부 정보", "편집", "만들기", "NotFound" 등)을 위해 만든 모든 보기 템플릿은 이 Site.master 템플릿을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-170">All of the view templates we've created for our NerdDinner application ("List", "Details", "Edit", "Create", "NotFound", etc) have been based on this Site.master template.</span></span> <span data-ttu-id="329d1-171">이것은 "추가보기" 대화 상자를 사용하여 뷰를 만들 때 &lt;기본적으로 상위&gt; % @ 페이지 % 지시문에 추가 된 "MasterPageFile"특성을 통해 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-171">This is indicated via the "MasterPageFile" attribute that was added by default to the top &lt;% @ Page %&gt; directive when we created our views using the "Add View" dialog:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

<span data-ttu-id="329d1-172">즉, Site.master 콘텐츠를 변경하고 뷰 템플릿을 렌더링할 때 변경 내용을 자동으로 적용하고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-172">What this means is that we can change the Site.master content, and have the changes automatically be applied and used when we render any of our view templates.</span></span>

<span data-ttu-id="329d1-173">우리의 응용 프로그램의 헤더가 "내 MVC 응용 프로그램"대신 "NerdDinner"되도록 Site.master의 헤더 섹션을 업데이트 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-173">Let's update our Site.master's header section so that the header of our application is "NerdDinner" instead of "My MVC Application".</span></span> <span data-ttu-id="329d1-174">또한 첫 번째 탭이 "Dinner찾기"(HomeController의 Index() 작업 메서드에서 처리되도록 탐색 메뉴를 업데이트하고 "DinnersController의 Create() 작업 메서드에서 처리됨"이라는 새 탭을 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-174">Let's also update our navigation menu so that the first tab is "Find a Dinner" (handled by the HomeController's Index() action method), and let's add a new tab called "Host a Dinner" (handled by the DinnersController's Create() action method):</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

<span data-ttu-id="329d1-175">Site.master 파일을 저장하고 브라우저를 새로 고치면 응용 프로그램 내의 모든 보기에서 헤더 변경 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-175">When we save the Site.master file and refresh our browser we'll see our header changes show up across all views within our application.</span></span> <span data-ttu-id="329d1-176">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="329d1-176">For example:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

<span data-ttu-id="329d1-177">그리고 */Dinners/편집/[id]* URL:</span><span class="sxs-lookup"><span data-stu-id="329d1-177">And with the */Dinners/Edit/[id]* URL:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a><span data-ttu-id="329d1-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="329d1-178">Next Step</span></span>

<span data-ttu-id="329d1-179">부분 및 마스터 페이지는 뷰를 깔끔하게 구성할 수 있는 매우 유연한 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-179">Partials and master pages provide very flexible options that enable you to cleanly organize views.</span></span> <span data-ttu-id="329d1-180">뷰 콘텐츠/코드가 중복되는 것을 방지하고 보기 템플릿을 더 쉽게 읽고 유지 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-180">You'll find that they help you avoid duplicating view content/ code, and make your view templates easier to read and maintain.</span></span>

<span data-ttu-id="329d1-181">이제 이전에 빌드한 목록 시나리오를 다시 방문하여 확장 가능한 페이징 지원을 사용하도록 설정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="329d1-181">Let's now revisit the listing scenario we built earlier and enable scalable paging support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="329d1-182">[이전](use-viewdata-and-implement-viewmodel-classes.md)
> [다음](implement-efficient-data-paging.md)</span><span class="sxs-lookup"><span data-stu-id="329d1-182">[Previous](use-viewdata-and-implement-viewmodel-classes.md)
[Next](implement-efficient-data-paging.md)</span></span>
