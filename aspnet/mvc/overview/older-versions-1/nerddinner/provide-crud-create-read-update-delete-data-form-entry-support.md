---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: CRUD 제공(데이터 양식 입력 지원 생성, 읽기, 업데이트, 삭제 | 마이크로 소프트 문서
author: rick-anderson
description: 5단계는 DinnersController 클래스를 편집, 생성 및 삭제에 대한 지원을 활성화하여 더 나아가는 방법을 보여 주며, Dinners를 사용하여 저녁 식사도 생성하고 삭제할 수 있도록 합니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: 2b75a7eda8bce4baa25d92626639f4d904eb363a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542627"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a><span data-ttu-id="ccffb-103">CRUD(만들기, 읽기, 업데이트, 삭제) 데이터 양식 항목 지원 제공</span><span class="sxs-lookup"><span data-stu-id="ccffb-103">Provide CRUD (Create, Read, Update, Delete) Data Form Entry Support</span></span>

<span data-ttu-id="ccffb-104">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ccffb-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="ccffb-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="ccffb-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="ccffb-106">이것은 MVC 1을 ASP.NET 사용하여 작지만 완전한 웹 응용 프로그램을 빌드하는 방법을 안내하는 무료 ["NerdDinner" 응용 프로그램 자습서의](introducing-the-nerddinner-tutorial.md) 5단계입니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-106">This is step 5 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="ccffb-107">5단계는 DinnersController 클래스를 편집, 생성 및 삭제에 대한 지원을 활성화하여 더 나아가는 방법을 보여 주며, Dinners를 사용하여 저녁 식사도 생성하고 삭제할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-107">Step 5 shows how to take our DinnersController class further by enable support for editing, creating and deleting Dinners with it as well.</span></span>
> 
> <span data-ttu-id="ccffb-108">MVC 3을 ASP.NET 사용하는 경우 [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC 뮤직 스토어](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a><span data-ttu-id="ccffb-109">NerdDinner 단계 5: 양식 시나리오 만들기, 업데이트, 삭제</span><span class="sxs-lookup"><span data-stu-id="ccffb-109">NerdDinner Step 5: Create, Update, Delete Form Scenarios</span></span>

<span data-ttu-id="ccffb-110">컨트롤러와 뷰를 도입했으며 이를 사용하여 현장에서 Dinners에 대한 목록/세부 정보 환경을 구현하는 방법을 다루었습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-110">We've introduced controllers and views, and covered how to use them to implement a listing/details experience for Dinners on site.</span></span> <span data-ttu-id="ccffb-111">우리의 다음 단계는 우리의 DinnersController 클래스를 더 가지고 편집, 생성 및 그것으로 저녁 식사를 삭제에 대한 지원을 가능하게하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-111">Our next step will be to take our DinnersController class further and enable support for editing, creating and deleting Dinners with it as well.</span></span>

### <a name="urls-handled-by-dinnerscontroller"></a><span data-ttu-id="ccffb-112">저녁 식사 컨트롤러에 의해 처리 되는 URL</span><span class="sxs-lookup"><span data-stu-id="ccffb-112">URLs handled by DinnersController</span></span>

<span data-ttu-id="ccffb-113">이전에는 DinnersController에 두 개의 URL에 대한 지원을 구현한 */Dinners/Details/[id]* 작업 *메서드를 추가했습니다.*</span><span class="sxs-lookup"><span data-stu-id="ccffb-113">We previously added action methods to DinnersController that implemented support for two URLs: */Dinners* and */Dinners/Details/[id]*.</span></span>

| <span data-ttu-id="ccffb-114">**URL**</span><span class="sxs-lookup"><span data-stu-id="ccffb-114">**URL**</span></span> | <span data-ttu-id="ccffb-115">**VERB**</span><span class="sxs-lookup"><span data-stu-id="ccffb-115">**VERB**</span></span> | <span data-ttu-id="ccffb-116">**용도**</span><span class="sxs-lookup"><span data-stu-id="ccffb-116">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ccffb-117">*/저녁 식사/*</span><span class="sxs-lookup"><span data-stu-id="ccffb-117">*/Dinners/*</span></span> | <span data-ttu-id="ccffb-118">GET</span><span class="sxs-lookup"><span data-stu-id="ccffb-118">GET</span></span> | <span data-ttu-id="ccffb-119">다가오는 저녁 식사의 HTML 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-119">Display an HTML list of upcoming dinners.</span></span> |
| <span data-ttu-id="ccffb-120">*/저녁 식사/세부 정보/[ID]*</span><span class="sxs-lookup"><span data-stu-id="ccffb-120">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="ccffb-121">GET</span><span class="sxs-lookup"><span data-stu-id="ccffb-121">GET</span></span> | <span data-ttu-id="ccffb-122">특정 저녁 식사에 대한 세부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-122">Display details about a specific dinner.</span></span> |

<span data-ttu-id="ccffb-123">이제 세 개의 추가 URL을 구현하기 위한 작업 *메서드를 추가합니다: /Dinners/편집/[id]*, */Dinners/Create*및 */Dinners/Delete/id.*</span><span class="sxs-lookup"><span data-stu-id="ccffb-123">We will now add action methods to implement three additional URLs: */Dinners/Edit/[id]*, */Dinners/Create*, and */Dinners/Delete/[id]*.</span></span> <span data-ttu-id="ccffb-124">이러한 URL을 사용하면 기존 저녁 식사 편집, 새 저녁 식사 만들기 및 저녁 식사 삭제를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-124">These URLs will enable support for editing existing Dinners, creating new Dinners, and deleting Dinners.</span></span>

<span data-ttu-id="ccffb-125">이러한 새 URL과의 HTTP GET 및 HTTP POST 동사 상호 작용을 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-125">We will support both HTTP GET and HTTP POST verb interactions with these new URLs.</span></span> <span data-ttu-id="ccffb-126">이러한 URL에 대한 HTTP GET 요청은 데이터의 초기 HTML 보기를 표시합니다("편집"의 경우 Dinner 데이터로 채워진 양식, "만들기"의 경우 빈 양식, "삭제"의 경우 삭제 확인 화면).</span><span class="sxs-lookup"><span data-stu-id="ccffb-126">HTTP GET requests to these URLs will display the initial HTML view of the data (a form populated with the Dinner data in the case of "edit", a blank form in the case of "create", and a delete confirmation screen in the case of "delete").</span></span> <span data-ttu-id="ccffb-127">이러한 URL에 대한 HTTP POST 요청은 DinnerRepository(그리고 거기에서 데이터베이스까지)에서 Dinner 데이터를 저장/업데이트/삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-127">HTTP POST requests to these URLs will save/update/delete the Dinner data in our DinnerRepository (and from there to the database).</span></span>

| <span data-ttu-id="ccffb-128">**URL**</span><span class="sxs-lookup"><span data-stu-id="ccffb-128">**URL**</span></span> | <span data-ttu-id="ccffb-129">**VERB**</span><span class="sxs-lookup"><span data-stu-id="ccffb-129">**VERB**</span></span> | <span data-ttu-id="ccffb-130">**용도**</span><span class="sxs-lookup"><span data-stu-id="ccffb-130">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ccffb-131">*/저녁 식사/편집/[id]*</span><span class="sxs-lookup"><span data-stu-id="ccffb-131">*/Dinners/Edit/[id]*</span></span> | <span data-ttu-id="ccffb-132">GET</span><span class="sxs-lookup"><span data-stu-id="ccffb-132">GET</span></span> | <span data-ttu-id="ccffb-133">Dinner 데이터로 채워진 편집 가능한 HTML 양식을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-133">Display an editable HTML form populated with Dinner data.</span></span> |
| <span data-ttu-id="ccffb-134">POST</span><span class="sxs-lookup"><span data-stu-id="ccffb-134">POST</span></span> | <span data-ttu-id="ccffb-135">특정 Dinner에 대한 양식 변경 내용을 데이터베이스에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-135">Save the form changes for a particular Dinner to the database.</span></span> |
| <span data-ttu-id="ccffb-136">*/저녁 식사/만들기*</span><span class="sxs-lookup"><span data-stu-id="ccffb-136">*/Dinners/Create*</span></span> | <span data-ttu-id="ccffb-137">GET</span><span class="sxs-lookup"><span data-stu-id="ccffb-137">GET</span></span> | <span data-ttu-id="ccffb-138">사용자가 새 Dinners를 정의할 수 있는 빈 HTML 양식을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-138">Display an empty HTML form that allows users to define new Dinners.</span></span> |
| <span data-ttu-id="ccffb-139">POST</span><span class="sxs-lookup"><span data-stu-id="ccffb-139">POST</span></span> | <span data-ttu-id="ccffb-140">새 Dinner를 만들고 데이터베이스에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-140">Create a new Dinner and save it in the database.</span></span> |
| <span data-ttu-id="ccffb-141">*/저녁 식사/삭제/[id]*</span><span class="sxs-lookup"><span data-stu-id="ccffb-141">*/Dinners/Delete/[id]*</span></span> | <span data-ttu-id="ccffb-142">GET</span><span class="sxs-lookup"><span data-stu-id="ccffb-142">GET</span></span> | <span data-ttu-id="ccffb-143">삭제 확인 화면을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-143">Display delete confirmation screen.</span></span> |
| <span data-ttu-id="ccffb-144">POST</span><span class="sxs-lookup"><span data-stu-id="ccffb-144">POST</span></span> | <span data-ttu-id="ccffb-145">데이터베이스에서 지정된 저녁 식사를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-145">Deletes the specified dinner from the database.</span></span> |

### <a name="edit-support"></a><span data-ttu-id="ccffb-146">지원 편집</span><span class="sxs-lookup"><span data-stu-id="ccffb-146">Edit Support</span></span>

<span data-ttu-id="ccffb-147">먼저 "편집" 시나리오를 구현해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-147">Let's begin by implementing the "edit" scenario.</span></span>

#### <a name="the-http-get-edit-action-method"></a><span data-ttu-id="ccffb-148">HTTP-GET 편집 작업 방법</span><span class="sxs-lookup"><span data-stu-id="ccffb-148">The HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="ccffb-149">먼저 편집 작업 메서드의 HTTP "GET" 동작을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-149">We'll start by implementing the HTTP "GET" behavior of our edit action method.</span></span> <span data-ttu-id="ccffb-150">이 메서드는 */Dinners/편집/[id]* URL이 요청될 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-150">This method will be invoked when the */Dinners/Edit/[id]* URL is requested.</span></span> <span data-ttu-id="ccffb-151">구현은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-151">Our implementation will look like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

<span data-ttu-id="ccffb-152">위의 코드는 DinnerRepository를 사용하여 Dinner 개체를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-152">The code above uses the DinnerRepository to retrieve a Dinner object.</span></span> <span data-ttu-id="ccffb-153">그런 다음 Dinner 개체를 사용하여 뷰 템플릿을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-153">It then renders a View template using the Dinner object.</span></span> <span data-ttu-id="ccffb-154">*View()* 도우미 메서드에 템플릿 이름을 명시적으로 전달하지 않았으므로 규칙 기반 기본 경로를 사용하여 보기 템플릿을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-154">Because we haven't explicitly passed a template name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Edit.aspx.</span></span>

<span data-ttu-id="ccffb-155">이제 이 보기 템플릿을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-155">Let's now create this view template.</span></span> <span data-ttu-id="ccffb-156">편집 방법 내에서 마우스 오른쪽 단추를 클릭하고 "보기 추가" 컨텍스트 메뉴 명령을 선택하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-156">We will do this by right-clicking within the Edit method and selecting the "Add View" context menu command:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

<span data-ttu-id="ccffb-157">"보기 추가" 대화 상자 내에서 Dinner 개체를 뷰 템플릿에 해당 모델로 전달하고 "편집" 템플릿을 자동으로 스캐폴드하도록 선택했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-157">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to auto-scaffold an "Edit" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

<span data-ttu-id="ccffb-158">"추가" 단추를 클릭하면 Visual Studio에서 "\View\Dinners" 디렉토리 내에 새 "Edit.aspx" 보기 템플릿 파일이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-158">When we click the "Add" button, Visual Studio will add a new "Edit.aspx" view template file for us within the "\Views\Dinners" directory.</span></span> <span data-ttu-id="ccffb-159">또한 코드 편집기 내에서 새로운 "Edit.aspx" 보기 템플릿을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-159">It will also open up the new "Edit.aspx" view template within the code-editor – populated with an initial "Edit" scaffold implementation like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

<span data-ttu-id="ccffb-160">생성된 기본 "편집" 스캐폴드를 몇 가지 변경하고 편집 보기 템플릿을 업데이트하여 아래 콘텐츠(노출하지 않으려는 속성 중 일부를 제거)를 갖도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-160">Let's make a few changes to the default "edit" scaffold generated, and update the edit view template to have the content below (which removes a few of the properties we don't want to expose):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

<span data-ttu-id="ccffb-161">응용 프로그램을 실행하고 *"저녁 식사 / 편집 / 1"URL을* 요청하면 다음 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-161">When we run the application and request the *"/Dinners/Edit/1"* URL we will see the following page:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

<span data-ttu-id="ccffb-162">뷰에서 생성된 HTML 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-162">The HTML markup generated by our view looks like below.</span></span> <span data-ttu-id="ccffb-163">"저장" &lt;&gt; 입력 유형="제출"/버튼을 눌려있을 때 */Dinners/편집/1* URL에 HTTP POST를 수행하는 &lt;양식&gt; 요소가 있는 표준 HTML입니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-163">It is standard HTML – with a &lt;form&gt; element that performs an HTTP POST to the */Dinners/Edit/1* URL when the "Save" &lt;input type="submit"/&gt; button is pushed.</span></span> <span data-ttu-id="ccffb-164">HTML &lt;입력 유형="텍스트"/요소가&gt; 각 편집 가능한 속성에 대해 출력되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-164">A HTML &lt;input type="text"/&gt; element has been output for each editable property:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a><span data-ttu-id="ccffb-165">Html.BeginForm() 및 Html.TextBox() HTML 도우미 방법</span><span class="sxs-lookup"><span data-stu-id="ccffb-165">Html.BeginForm() and Html.TextBox() Html Helper Methods</span></span>

<span data-ttu-id="ccffb-166">우리의 "편집.aspx" 보기 템플릿은 몇 가지 "Html 도우미" 메서드를 사용 하 여: Html.ValidationSummary (), Html.BeginForm (), Html.TextBox(), 그리고 Html.ValidationMessage().</span><span class="sxs-lookup"><span data-stu-id="ccffb-166">Our "Edit.aspx" view template is using several "Html Helper" methods: Html.ValidationSummary(), Html.BeginForm(), Html.TextBox(), and Html.ValidationMessage().</span></span> <span data-ttu-id="ccffb-167">이러한 도우미 메서드는 HTML 태그를 생성하는 것 외에도 기본 제공 오류 처리 및 유효성 검사 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-167">In addition to generating HTML markup for us, these helper methods provide built-in error handling and validation support.</span></span>

##### <a name="htmlbeginform-helper-method"></a><span data-ttu-id="ccffb-168">Html.BeginForm() 도우미 방법</span><span class="sxs-lookup"><span data-stu-id="ccffb-168">Html.BeginForm() helper method</span></span>

<span data-ttu-id="ccffb-169">Html.BeginForm() 도우미 메서드는 태그에서 &lt;HTML&gt; 양식 요소를 출력하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-169">The Html.BeginForm() helper method is what output the HTML &lt;form&gt; element in our markup.</span></span> <span data-ttu-id="ccffb-170">Edit.aspx 보기 템플릿에서는 이 메서드를 사용할 때 C# "using" 문을 적용하고 있음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-170">In our Edit.aspx view template you'll notice that we are applying a C# "using" statement when using this method.</span></span> <span data-ttu-id="ccffb-171">열린 곱슬 대괄호는 &lt;양식&gt; 내용의 시작을 나타내고 닫는 곱슬 대괄호는 &lt;/form&gt; 요소의 끝을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-171">The open curly brace indicates the beginning of the &lt;form&gt; content, and the closing curly brace is what indicates the end of the &lt;/form&gt; element:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

<span data-ttu-id="ccffb-172">또는 이와 같은 시나리오에서 "using" 문 접근 방식이 부자연스럽다면 Html.BeginForm() 및 Html.EndForm(동일한 작업을 수행하는) 조합을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-172">Alternatively, if you find the "using" statement approach unnatural for a scenario like this, you can use a Html.BeginForm() and Html.EndForm() combination (which does the same thing):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

<span data-ttu-id="ccffb-173">매개 변수없이 Html.BeginForm()을 호출하면 현재 요청의 URL에 HTTP-POST를 수행하는 양식 요소가 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-173">Calling Html.BeginForm() without any parameters will cause it to output a form element that does an HTTP-POST to the current request's URL.</span></span> <span data-ttu-id="ccffb-174">그래서 편집 보기는 \* &lt;양식 동작="/Dinners/편집/1" 메서드="post"&gt; 요소를 생성합니다.\*</span><span class="sxs-lookup"><span data-stu-id="ccffb-174">That is why our Edit view generates a *&lt;form action="/Dinners/Edit/1" method="post"&gt;* element.</span></span> <span data-ttu-id="ccffb-175">다른 URL에 게시하려는 경우 명시적 매개 변수를 Html.BeginForm()에 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-175">We could have alternatively passed explicit parameters to Html.BeginForm() if we wanted to post to a different URL.</span></span>

##### <a name="htmltextbox-helper-method"></a><span data-ttu-id="ccffb-176">Html.TextBox() 도우미 방법</span><span class="sxs-lookup"><span data-stu-id="ccffb-176">Html.TextBox() helper method</span></span>

<span data-ttu-id="ccffb-177">Edit.aspx 보기는 Html.TextBox() 도우미 메서드를 &lt;사용하여 입력 입력&gt; ="텍스트"/요소를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-177">Our Edit.aspx view uses the Html.TextBox() helper method to output &lt;input type="text"/&gt; elements:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

<span data-ttu-id="ccffb-178">위의 Html.TextBox() 메서드는 &lt;입력 type="text"/요소의&gt; id/name 속성을 모두 출력할 뿐만 아니라 텍스트 상자 값을 채우는 모델 속성을 지정하는 데 사용되는 단일 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-178">The Html.TextBox() method above takes a single parameter – which is being used to specify both the id/name attributes of the &lt;input type="text"/&gt; element to output, as well as the model property to populate the textbox value from.</span></span> <span data-ttu-id="ccffb-179">예를 들어 편집 뷰에 전달한 Dinner 개체에는 ".NET Futures"의 "Title" 속성 값이 있으므로 Html.TextBox("제목") 메서드 호출 출력: \* &lt;입력 id="Title" name="Title" type="text" 값="net"net&gt;\*</span><span class="sxs-lookup"><span data-stu-id="ccffb-179">For example, the Dinner object we passed to the Edit view had a "Title" property value of ".NET Futures", and so our Html.TextBox("Title") method call output: *&lt;input id="Title" name="Title" type="text" value=".NET Futures" /&gt;*.</span></span>

<span data-ttu-id="ccffb-180">또는 첫 번째 Html.TextBox() 매개 변수를 사용하여 요소의 ID/이름을 지정한 다음 값을 명시적으로 전달하여 두 번째 매개 변수로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-180">Alternatively, we can use the first Html.TextBox() parameter to specify the id/name of the element, and then explicitly pass in the value to use as a second parameter:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

<span data-ttu-id="ccffb-181">종종 출력되는 값에 대한 사용자 지정 서식을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-181">Often we'll want to perform custom formatting on the value that is output.</span></span> <span data-ttu-id="ccffb-182">.NET에 내장된 String.Format() 정적 메서드는 이러한 시나리오에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-182">The String.Format() static method built-into .NET is useful for these scenarios.</span></span> <span data-ttu-id="ccffb-183">Edit.aspx 보기 템플릿은 이 것을 사용하여 EventDate 값(DateTime 형식)을 포맷하여 시간 동안 초를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-183">Our Edit.aspx view template is using this to format the EventDate value (which is of type DateTime) so that it doesn't show seconds for the time:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

<span data-ttu-id="ccffb-184">Html.TextBox()에 대한 세 번째 매개 변수는 선택적으로 추가 HTML 특성을 출력하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-184">A third parameter to Html.TextBox() can optionally be used to output additional HTML attributes.</span></span> <span data-ttu-id="ccffb-185">아래 코드 조각은 입력 type="text"/요소에 &lt;&gt; 추가 크기="30" 특성 및 클래스="mycssclass" 특성을 렌더링하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-185">The code-snippet below demonstrates how to render an additional size="30" attribute and a class="mycssclass" attribute on the &lt;input type="text"/&gt; element.</span></span> <span data-ttu-id="ccffb-186">"클래스"를@" character because "사용하여 클래스 특성의 이름을 이스케이프하는 방법은 C#의 예약된 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-186">Note how we are escaping the name of the class attribute using a "@" character because "class" is a reserved keyword in C#:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a><span data-ttu-id="ccffb-187">HTTP-POST 편집 작업 방법 구현</span><span class="sxs-lookup"><span data-stu-id="ccffb-187">Implementing the HTTP-POST Edit Action Method</span></span>

<span data-ttu-id="ccffb-188">이제 편집 작업 메서드의 HTTP-GET 버전이 구현되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-188">We now have the HTTP-GET version of our Edit action method implemented.</span></span> <span data-ttu-id="ccffb-189">사용자가 */Dinners/편집/1 URL을* 요청하면 다음과 같은 HTML 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-189">When a user requests the */Dinners/Edit/1* URL they receive an HTML page like the following:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

<span data-ttu-id="ccffb-190">"저장" 버튼을 누르면 */Dinners/편집/1* URL에 양식 게시물이 발생 하 &lt;&gt; 고 HTTP POST 동사를 사용 하 여 HTML 입력 양식 값을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-190">Pressing the "Save" button causes a form post to the */Dinners/Edit/1* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span> <span data-ttu-id="ccffb-191">이제 Dinner 저장을 처리하는 편집 작업 메서드의 HTTP POST 동작을 구현해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-191">Let's now implement the HTTP POST behavior of our edit action method – which will handle saving the Dinner.</span></span>

<span data-ttu-id="ccffb-192">HTTP POST 시나리오를 처리한다는 것을 나타내는 "AcceptVerbs" 특성이 있는 DinnersController에 오버로드된 "편집" 작업 메서드를 추가하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-192">We'll begin by adding an overloaded "Edit" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

<span data-ttu-id="ccffb-193">[AcceptVerbs] 특성이 오버로드된 작업 메서드에 적용되면 ASP.NET MVC는 들어오는 HTTP 동사에 따라 적절한 작업 메서드로 요청을 디스패치하는 요청을 자동으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-193">When the [AcceptVerbs] attribute is applied to overloaded action methods, ASP.NET MVC automatically handles dispatching requests to the appropriate action method depending on the incoming HTTP verb.</span></span> <span data-ttu-id="ccffb-194">HTTP POST */Dinners/편집/[id]* URL에 대한 HTTP POST 요청은 위의 편집 방법으로 이동하지만 다른 모든 HTTP 동사 요청은 */Dinners/편집/[id]* URL로 이동하며, URL은 `[AcceptVerbs]` 특성이 없는 첫 번째 편집 메서드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-194">HTTP POST requests to */Dinners/Edit/[id]* URLs will go to the above Edit method, while all other HTTP verb requests to */Dinners/Edit/[id]* URLs will go to the first Edit method we implemented (which did not have an `[AcceptVerbs]` attribute).</span></span>

| <span data-ttu-id="ccffb-195">**측면 주제: HTTP 동사를 통해 차별화하는 이유는 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="ccffb-195">**Side Topic: Why differentiate via HTTP verbs?**</span></span> |
| --- |
| <span data-ttu-id="ccffb-196">단일 URL을 사용하고 HTTP 동사를 통해 동작을 차별화하는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ccffb-196">You might ask – why are we using a single URL and differentiating its behavior via the HTTP verb?</span></span> <span data-ttu-id="ccffb-197">편집 변경 내용을 로드하고 저장하는 데 두 개의 별도 URL만 있는 것은 어떨까요?</span><span class="sxs-lookup"><span data-stu-id="ccffb-197">Why not just have two separate URLs to handle loading and saving edit changes?</span></span> <span data-ttu-id="ccffb-198">예: /Dinners/편집/[id]를 표시하여 초기 양식을 표시하고/Dinners/Save/[id]를 표시하여 양식 게시물을 처리하여 저장합니까?</span><span class="sxs-lookup"><span data-stu-id="ccffb-198">For example: /Dinners/Edit/[id] to display the initial form and /Dinners/Save/[id] to handle the form post to save it?</span></span> <span data-ttu-id="ccffb-199">두 개의 별도 URL을 게시하는 단점은 입력 오류로 인해 HTML 양식을 다시 표시해야하는 경우 최종 사용자가 브라우저의 주소 표시 줄에 /Dinners / Save /2 URL을 표시해야한다는 것입니다 (해당 양식이 게시 된 URL이었기 때문에).</span><span class="sxs-lookup"><span data-stu-id="ccffb-199">The downside with publishing two separate URLs is that in cases where we post to /Dinners/Save/2, and then need to redisplay the HTML form because of an input error, the end-user will end up having the /Dinners/Save/2 URL in their browser's address bar (since that was the URL the form posted to).</span></span> <span data-ttu-id="ccffb-200">최종 사용자가 이 페이지를 브라우저 즐겨찾기 목록에 다시 표시하거나 URL을 복사/붙여넣은 후 친구에게 이메일을 지정하면 나중에 작동하지 않는 URL이 저장됩니다(해당 URL은 게시물 값에 따라 달라지기 때문에).</span><span class="sxs-lookup"><span data-stu-id="ccffb-200">If the end-user bookmarks this redisplayed page to their browser favorites list, or copy/pastes the URL and emails it to a friend, they will end up saving a URL that won't work in the future (since that URL depends on post values).</span></span> <span data-ttu-id="ccffb-201">단일 URL(예: /Dinners/Edit/[id])을 노출하고 HTTP 동사로 처리를 차별화하면 최종 사용자가 편집 페이지를 즐겨찾기에 표시하거나 URL을 다른 사용자에게 보내는 것이 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-201">By exposing a single URL (like: /Dinners/Edit/[id]) and differentiating the processing of it by HTTP verb, it is safe for end-users to bookmark the edit page and/or send the URL to others.</span></span> |

#### <a name="retrieving-form-post-values"></a><span data-ttu-id="ccffb-202">양식 게시물 값 검색</span><span class="sxs-lookup"><span data-stu-id="ccffb-202">Retrieving Form Post Values</span></span>

<span data-ttu-id="ccffb-203">HTTP POST "편집" 방법 내에서 게시된 양식 매개 변수에 액세스할 수 있는 다양한 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-203">There are a variety of ways we can access posted form parameters within our HTTP POST "Edit" method.</span></span> <span data-ttu-id="ccffb-204">한 가지 간단한 방법은 Controller 기본 클래스의 Request 속성을 사용하여 양식 컬렉션에 액세스하고 게시된 값을 직접 검색하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-204">One simple approach is to just use the Request property on the Controller base class to access the form collection and retrieve the posted values directly:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

<span data-ttu-id="ccffb-205">위의 방법은 약간 상세하지만, 특히 오류 처리 논리를 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-205">The above approach is a little verbose, though, especially once we add error handling logic.</span></span>

<span data-ttu-id="ccffb-206">이 시나리오에 대 한 더 나은 방법은 컨트롤러 기본 클래스에 기본 *제공 UpdateModel()* 도우미 메서드를 활용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-206">A better approach for this scenario is to leverage the built-in *UpdateModel()* helper method on the Controller base class.</span></span> <span data-ttu-id="ccffb-207">들어오는 양식 매개 변수를 사용하여 전달하는 개체의 속성 업데이트를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-207">It supports updating the properties of an object we pass it using the incoming form parameters.</span></span> <span data-ttu-id="ccffb-208">리플렉션을 사용하여 개체의 속성 이름을 결정한 다음 클라이언트가 제출한 입력 값에 따라 자동으로 변환하고 값을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-208">It uses reflection to determine the property names on the object, and then automatically converts and assigns values to them based on the input values submitted by the client.</span></span>

<span data-ttu-id="ccffb-209">UpdateModel() 메서드를 사용하여 이 코드를 사용하여 HTTP-POST 편집 작업을 단순화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-209">We could use the UpdateModel() method to simplify our HTTP-POST Edit Action using this code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

<span data-ttu-id="ccffb-210">이제 */Dinners/편집/1 URL을* 방문하여 저녁 식사 의 제목을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-210">We can now visit the */Dinners/Edit/1* URL, and change the title of our Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

<span data-ttu-id="ccffb-211">"저장" 단추를 클릭하면 편집 작업에 양식 게시를 수행하고 업데이트된 값이 데이터베이스에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-211">When we click the "Save" button, we'll perform a form post to our Edit action, and the updated values will be persisted in the database.</span></span> <span data-ttu-id="ccffb-212">그런 다음 Dinner의 세부 정보 URL로 리디렉션됩니다(새로 저장된 값이 표시됩니다).</span><span class="sxs-lookup"><span data-stu-id="ccffb-212">We will then be redirected to the Details URL for the Dinner (which will display the newly saved values):</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a><span data-ttu-id="ccffb-213">편집 오류 처리</span><span class="sxs-lookup"><span data-stu-id="ccffb-213">Handling Edit Errors</span></span>

<span data-ttu-id="ccffb-214">현재 HTTP-POST 구현은 오류가 있는 경우를 제외하고 는 정상적으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-214">Our current HTTP-POST implementation works fine – except when there are errors.</span></span>

<span data-ttu-id="ccffb-215">사용자가 양식을 편집하는 실수를 할 때 양식을 수정하도록 안내하는 유익한 오류 메시지와 함께 양식이 다시 표시되는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-215">When a user makes a mistake editing a form, we need to make sure that the form is redisplayed with an informative error message that guides them to fix it.</span></span> <span data-ttu-id="ccffb-216">여기에는 최종 사용자가 잘못된 입력(예: 잘못된 날짜 문자열)을 게시하는 경우와 입력 형식이 유효하지만 비즈니스 규칙 위반이 있는 경우가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-216">This includes cases where an end-user posts incorrect input (for example: a malformed date string), as well as cases where the input format is valid but there is a business rule violation.</span></span> <span data-ttu-id="ccffb-217">오류가 발생하면 양식은 사용자가 원래 입력한 입력 데이터를 보존하여 변경 내용을 수동으로 다시 채울 필요가 없도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-217">When errors occur the form should preserve the input data the user originally entered so that they don't have to refill their changes manually.</span></span> <span data-ttu-id="ccffb-218">이 프로세스는 양식이 성공적으로 완료될 때까지 필요한 만큼 반복되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-218">This process should repeat as many times as necessary until the form successfully completes.</span></span>

<span data-ttu-id="ccffb-219">ASP.NET MVC에는 오류 처리 및 양식 재표시를 쉽게 만드는 몇 가지 멋진 기본 제공 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-219">ASP.NET MVC includes some nice built-in features that make error handling and form redisplay easy.</span></span> <span data-ttu-id="ccffb-220">이러한 기능을 확인하려면 다음 코드로 편집 작업 메서드를 업데이트해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-220">To see these features in action let's update our Edit action method with the following code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

<span data-ttu-id="ccffb-221">위의 코드는 이전 구현과 유사합니다 .</span><span class="sxs-lookup"><span data-stu-id="ccffb-221">The above code is similar to our previous implementation – except that we are now wrapping a try/catch error handling block around our work.</span></span> <span data-ttu-id="ccffb-222">UpdateModel()를 호출할 때 예외가 발생하거나 DinnerRepository를 시도하고 저장할 때(저장하려는 Dinner 개체가 모델 내의 규칙 위반으로 인해 유효하지 않은 경우 예외를 발생시) catch 오류 처리 블록이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-222">If an exception occurs either when calling UpdateModel(), or when we try and save the DinnerRepository (which will raise an exception if the Dinner object we are trying to save is invalid because of a rule violation within our model), our catch error handling block will execute.</span></span> <span data-ttu-id="ccffb-223">그 안에서 Dinner 개체에 있는 규칙 위반을 반복하고 ModelState 개체에 추가합니다(곧 설명하겠습니다).</span><span class="sxs-lookup"><span data-stu-id="ccffb-223">Within it we loop over any rule violations that exist in the Dinner object and add them to a ModelState object (which we'll discuss shortly).</span></span> <span data-ttu-id="ccffb-224">그런 다음 뷰를 다시 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-224">We then redisplay the view.</span></span>

<span data-ttu-id="ccffb-225">이 작업을 보려면 응용 프로그램을 다시 실행하고 Dinner를 편집하고 빈 제목인 "BOGUS"의 EventDate를 가지고 미국 국가 값이 있는 영국 전화 번호를 사용하도록 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-225">To see this working let's re-run the application, edit a Dinner, and change it to have an empty Title, an EventDate of "BOGUS", and use a UK phone number with a country value of USA.</span></span> <span data-ttu-id="ccffb-226">"저장" 버튼을 누르면 HTTP POST 편집 방법이 Dinner를 저장할 수 없으며(오류가 있기 때문에) 양식을 다시 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-226">When we press the "Save" button our HTTP POST Edit method will not be able to save the Dinner (because there are errors) and will redisplay the form:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

<span data-ttu-id="ccffb-227">우리의 응용 프로그램은 괜찮은 오류 경험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-227">Our application has a decent error experience.</span></span> <span data-ttu-id="ccffb-228">잘못된 입력이 있는 텍스트 요소가 빨간색으로 강조 표시되고 유효성 검사 오류 메시지가 최종 사용자에게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-228">The text elements with the invalid input are highlighted in red, and validation error messages are displayed to the end user about them.</span></span> <span data-ttu-id="ccffb-229">또한 양식은 사용자가 원래 입력한 입력 데이터를 보존하므로 아무 것도 다시 채울 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-229">The form is also preserving the input data the user originally entered – so that they don't have to refill anything.</span></span>

<span data-ttu-id="ccffb-230">어떻게 이런 일이 발생했습니까?</span><span class="sxs-lookup"><span data-stu-id="ccffb-230">How, you might ask, did this occur?</span></span> <span data-ttu-id="ccffb-231">제목, EventDate 및 ContactPhone 텍스트 상자는 빨간색으로 자신을 강조 표시하고 원래 입력한 사용자 값을 출력하는 방법을 알고 있었습니까?</span><span class="sxs-lookup"><span data-stu-id="ccffb-231">How did the Title, EventDate, and ContactPhone textboxes highlight themselves in red and know to output the originally entered user values?</span></span> <span data-ttu-id="ccffb-232">그리고 오류 메시지가 상단의 목록에 어떻게 표시되었습니까?</span><span class="sxs-lookup"><span data-stu-id="ccffb-232">And how did error messages get displayed in the list at the top?</span></span> <span data-ttu-id="ccffb-233">좋은 소식은 이것이 마술에 의해 발생하지 않았다는 것입니다 - 오히려 입력 유효성 검사 및 오류 처리 시나리오를 쉽게 만드는 기본 제공 ASP.NET MVC 기능 중 일부를 사용했기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-233">The good news is that this didn't occur by magic - rather it was because we used some of the built-in ASP.NET MVC features that make input validation and error handling scenarios easy.</span></span>

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a><span data-ttu-id="ccffb-234">모델상태 및 유효성 검사 HTML 도우미 방법 이해</span><span class="sxs-lookup"><span data-stu-id="ccffb-234">Understanding ModelState and the Validation HTML Helper Methods</span></span>

<span data-ttu-id="ccffb-235">컨트롤러 클래스에는 모델 개체가 뷰에 전달되는 경우 오류가 있음을 나타내는 방법을 제공하는 "ModelState" 속성 컬렉션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-235">Controller classes have a "ModelState" property collection which provides a way to indicate that errors exist with a model object being passed to a View.</span></span> <span data-ttu-id="ccffb-236">ModelState 컬렉션 내의 오류 항목은 문제가 있는 모델 속성의 이름을 식별하고(예: "제목", "EventDate" 또는 "ContactPhone") 인간 친화적인 오류 메시지를 지정할 수 있습니다(예: "제목이 필요합니다.").</span><span class="sxs-lookup"><span data-stu-id="ccffb-236">Error entries within the ModelState collection identify the name of the model property with the issue (for example: "Title", "EventDate", or "ContactPhone"), and allow a human-friendly error message to be specified (for example: "Title is required").</span></span>

<span data-ttu-id="ccffb-237">*UpdateModel()* 도우미 메서드는 모델 개체의 속성에 양식 값을 할당하는 동안 오류가 발생하면 ModelState 컬렉션을 자동으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-237">The *UpdateModel()* helper method automatically populates the ModelState collection when it encounters errors while trying to assign form values to properties on the model object.</span></span> <span data-ttu-id="ccffb-238">예를 들어 Dinner 개체의 EventDate 속성은 DateTime 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-238">For example, our Dinner object's EventDate property is of type DateTime.</span></span> <span data-ttu-id="ccffb-239">UpdateModel() 메서드가 위의 시나리오에서 문자열 값 "BOGUS"를 할당할 수 없는 경우 UpdateModel() 메서드는 해당 속성에서 할당 오류가 발생했음을 나타내는 ModelState 컬렉션에 항목을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-239">When the UpdateModel() method was unable to assign the string value "BOGUS" to it in the scenario above, the UpdateModel() method added an entry to the ModelState collection indicating an assignment error had occurred with that property.</span></span>

<span data-ttu-id="ccffb-240">개발자는 Dinner 개체의 활성 규칙 위반을 기반으로 하는 항목으로 ModelState 컬렉션을 채우는 "catch" 오류 처리 블록 내에서 아래에서 수행하는 것처럼 ModelState 컬렉션에 오류 항목을 명시적으로 추가하는 코드를 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-240">Developers can also write code to explicitly add error entries into the ModelState collection like we are doing below within our "catch" error handling block, which is populating the ModelState collection with entries based on the active Rule Violations in the Dinner object:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a><span data-ttu-id="ccffb-241">모델스테이트와 Html 도우미 통합</span><span class="sxs-lookup"><span data-stu-id="ccffb-241">Html Helper Integration with ModelState</span></span>

<span data-ttu-id="ccffb-242">HTML 도우미 메서드(예: Html.TextBox() - 출력을 렌더링할 때 ModelState 컬렉션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-242">HTML helper methods - like Html.TextBox() - check the ModelState collection when rendering output.</span></span> <span data-ttu-id="ccffb-243">항목에 대한 오류가 있으면 사용자 입력 값과 CSS 오류 클래스를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-243">If an error for the item exists, they render the user-entered value and a CSS error class.</span></span>

<span data-ttu-id="ccffb-244">예를 들어 "편집" 보기에서 Html.TextBox() 도우미 메서드를 사용하여 Dinner 개체의 EventDate를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-244">For example, in our "Edit" view we are using the Html.TextBox() helper method to render the EventDate of our Dinner object:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

<span data-ttu-id="ccffb-245">오류 시나리오에서 뷰가 렌더링되었을 때 Html.TextBox() 메서드는 ModelState 컬렉션을 선택하여 Dinner 개체의 "EventDate" 속성과 관련된 오류가 있는지 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-245">When the view was rendered in the error scenario, the Html.TextBox() method checked the ModelState collection to see if there were any errors associated with the "EventDate" property of our Dinner object.</span></span> <span data-ttu-id="ccffb-246">오류가 있다고 판단되면 제출된 사용자 입력("BOGUS")을 값으로 렌더링하고 &lt;생성된 입력 유형="textbox"/&gt; 태그에 css 오류 클래스를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-246">When it determined that there was an error it rendered the submitted user input ("BOGUS") as the value, and added a css error class to the &lt;input type="textbox"/&gt; markup it generated:</span></span>

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

<span data-ttu-id="ccffb-247">원하는 모양으로 css 오류 클래스의 모양을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-247">You can customize the appearance of the css error class to look however you want.</span></span> <span data-ttu-id="ccffb-248">기본 CSS 오류 클래스인 "입력 유효성 검사 오류"는 *\content\site.css* 스타일시트에 정의되어 있으며 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-248">The default CSS error class – "input-validation-error" – is defined in the *\content\site.css* stylesheet and looks like below:</span></span>

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

<span data-ttu-id="ccffb-249">이 CSS 규칙은 잘못된 입력 요소를 다음과 같이 강조 표시하게 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-249">This CSS rule is what caused our invalid input elements to be highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a><span data-ttu-id="ccffb-250">Html.유효성 검사메시지() 도우미 방법</span><span class="sxs-lookup"><span data-stu-id="ccffb-250">Html.ValidationMessage() Helper Method</span></span>

<span data-ttu-id="ccffb-251">Html.ValidationMessage() 도우미 메서드를 사용하여 특정 모델 속성과 연결된 ModelState 오류 메시지를 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-251">The Html.ValidationMessage() helper method can be used to output the ModelState error message associated with a particular model property:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

<span data-ttu-id="ccffb-252">위의 코드 출력: \* &lt;span class="필드 유효성&gt; 검사-오류" 값 'BOGUS' 값이 잘못되었습니다/범위&lt;&gt;\*</span><span class="sxs-lookup"><span data-stu-id="ccffb-252">The above code outputs: *&lt;span class="field-validation-error"&gt; The value ‘BOGUS' is invalid&lt;/span&gt;*</span></span>

<span data-ttu-id="ccffb-253">Html.ValidationMessage() 도우미 메서드는 개발자가 표시되는 오류 텍스트 메시지를 재정의할 수 있는 두 번째 매개 변수도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-253">The Html.ValidationMessage() helper method also supports a second parameter that allows developers to override the error text message that is displayed:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

<span data-ttu-id="ccffb-254">위의 코드 출력: \* &lt;&gt;\*&lt;EventDate&gt; \* 속성에 대 한 오류가 있을 때 기본 오류 텍스트 대신 "필드 유효성 검사 오류" /span 클래스=</span><span class="sxs-lookup"><span data-stu-id="ccffb-254">The above code outputs: *&lt;span class="field-validation-error"&gt;\*&lt;/span&gt;* instead of the default error text when an error is present for the EventDate property.</span></span>

##### <a name="htmlvalidationsummary-helper-method"></a><span data-ttu-id="ccffb-255">Html.유효성 검사요약() 도우미 방법</span><span class="sxs-lookup"><span data-stu-id="ccffb-255">Html.ValidationSummary() Helper Method</span></span>

<span data-ttu-id="ccffb-256">Html.ValidationSummary() 도우미 메서드는 ModelState 컬렉션의 모든 자세한 오류 &lt;메시지의 ul&gt;&lt;li/ul&gt;&lt;&gt; 목록과 함께 요약 오류 메시지를 렌더링하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-256">The Html.ValidationSummary() helper method can be used to render a summary error message, accompanied by a &lt;ul&gt;&lt;li/&gt;&lt;/ul&gt; list of all detailed error messages in the ModelState collection:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

<span data-ttu-id="ccffb-257">Html.ValidationSummary() 도우미 메서드는 선택적 문자열 매개 변수를 사용 하며, 자세한 오류 목록 위에 표시 하는 요약 오류 메시지를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-257">The Html.ValidationSummary() helper method takes an optional string parameter – which defines a summary error message to display above the list of detailed errors:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

<span data-ttu-id="ccffb-258">선택적으로 CSS를 사용하여 오류 목록의 모양을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-258">You can optionally use CSS to override what the error list looks like.</span></span>

#### <a name="using-a-addruleviolations-helper-method"></a><span data-ttu-id="ccffb-259">추가 규칙 위반 도우미 방법 사용</span><span class="sxs-lookup"><span data-stu-id="ccffb-259">Using a AddRuleViolations Helper Method</span></span>

<span data-ttu-id="ccffb-260">우리의 초기 HTTP-POST 편집 구현 은 Dinner 개체의 규칙 위반을 반복하고 컨트롤러의 ModelState 컬렉션에 추가하기 위해 catch 블록 내의 foreach 문을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-260">Our initial HTTP-POST Edit implementation used a foreach statement within its catch block to loop over the Dinner object's Rule Violations and add them to the controller's ModelState collection:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

<span data-ttu-id="ccffb-261">NerdDinner 프로젝트에 "ControllerHelpers" 클래스를 추가하여 이 코드를 좀 더 깨끗하게 만들고 mVC ModelStateDictionary 클래스에 도우미 메서드를 추가하는 "AddRule위반" 확장 메서드를 구현할 수 ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ccffb-261">We can make this code a little cleaner by adding a "ControllerHelpers" class to the NerdDinner project, and implement an "AddRuleViolations" extension method within it that adds a helper method to the ASP.NET MVC ModelStateDictionary class.</span></span> <span data-ttu-id="ccffb-262">이 확장 메서드는 ModelStateDictionary를 규칙 위반 오류 목록으로 채우는 데 필요한 논리를 캡슐화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-262">This extension method can encapsulate the logic necessary to populate the ModelStateDictionary with a list of RuleViolation errors:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

<span data-ttu-id="ccffb-263">그런 다음 HTTP-POST 편집 작업 메서드를 업데이트하여 이 확장 메서드를 사용하여 Dinner 규칙 위반으로 ModelState 컬렉션을 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-263">We can then update our HTTP-POST Edit action method to use this extension method to populate the ModelState collection with our Dinner Rule Violations.</span></span>

#### <a name="complete-edit-action-method-implementations"></a><span data-ttu-id="ccffb-264">작업 방법 구현 완료</span><span class="sxs-lookup"><span data-stu-id="ccffb-264">Complete Edit Action Method Implementations</span></span>

<span data-ttu-id="ccffb-265">아래 코드는 편집 시나리오에 필요한 모든 컨트롤러 논리를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-265">The code below implements all of the controller logic necessary for our Edit scenario:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

<span data-ttu-id="ccffb-266">편집 구현의 좋은 점은 컨트롤러 클래스나 View 템플릿이 Dinner 모델에서 적용되는 특정 유효성 검사 또는 비즈니스 규칙에 대해 아무 것도 알 필요가 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-266">The nice thing about our Edit implementation is that neither our Controller class nor our View template has to know anything about the specific validation or business rules being enforced by our Dinner model.</span></span> <span data-ttu-id="ccffb-267">나중에 모델에 규칙을 추가할 수 있으며 지원하기 위해 컨트롤러 나 뷰를 코드를 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-267">We can add additional rules to our model in the future and do not have to make any code changes to our controller or view in order for them to be supported.</span></span> <span data-ttu-id="ccffb-268">이를 통해 최소한의 코드 변경으로 향후 응용 프로그램 요구 사항을 쉽게 발전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-268">This provides us with the flexibility to easily evolve our application requirements in the future with a minimum of code changes.</span></span>

### <a name="create-support"></a><span data-ttu-id="ccffb-269">지원 만들기</span><span class="sxs-lookup"><span data-stu-id="ccffb-269">Create Support</span></span>

<span data-ttu-id="ccffb-270">DinnersController 클래스의 "편집" 동작 구현을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-270">We've finished implementing the "Edit" behavior of our DinnersController class.</span></span> <span data-ttu-id="ccffb-271">이제 사용자가 새 Dinners를 추가할 수 있는 "만들기" 지원을 구현해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-271">Let's now move on to implement the "Create" support on it – which will enable users to add new Dinners.</span></span>

#### <a name="the-http-get-create-action-method"></a><span data-ttu-id="ccffb-272">HTTP-GET 만들기 작업 방법</span><span class="sxs-lookup"><span data-stu-id="ccffb-272">The HTTP-GET Create Action Method</span></span>

<span data-ttu-id="ccffb-273">먼저 만들기 작업 메서드의 HTTP "GET" 동작을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-273">We'll begin by implementing the HTTP "GET" behavior of our create action method.</span></span> <span data-ttu-id="ccffb-274">이 메서드는 *사용자가 /Dinners/CREATE URL을* 방문할 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-274">This method will be called when someone visits the */Dinners/Create* URL.</span></span> <span data-ttu-id="ccffb-275">구현은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-275">Our implementation looks like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

<span data-ttu-id="ccffb-276">위의 코드는 새 Dinner 개체를 만들고 해당 EventDate 속성을 나중에 1주일로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-276">The code above creates a new Dinner object, and assigns its EventDate property to be one week in the future.</span></span> <span data-ttu-id="ccffb-277">그런 다음 새 Dinner 개체를 기반으로 하는 뷰를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-277">It then renders a View that is based on the new Dinner object.</span></span> <span data-ttu-id="ccffb-278">*View()* 도우미 메서드에 이름을 명시적으로 전달하지 않았으므로 규칙 기반 기본 경로를 사용하여 보기 템플릿을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-278">Because we haven't explicitly passed a name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Create.aspx.</span></span>

<span data-ttu-id="ccffb-279">이제 이 보기 템플릿을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-279">Let's now create this view template.</span></span> <span data-ttu-id="ccffb-280">작업 만들기 메서드 내에서 마우스 오른쪽 단추를 클릭하고 "보기 추가" 컨텍스트 메뉴 명령을 선택하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-280">We can do this by right-clicking within the Create action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="ccffb-281">"보기 추가" 대화 상자 내에서 Dinner 개체를 뷰 템플릿에 전달하고 "만들기" 템플릿을 자동으로 스캐폴드하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-281">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to the view template, and choose to auto-scaffold a "Create" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

<span data-ttu-id="ccffb-282">"추가" 단추를 클릭하면 Visual Studio에서 새 스캐폴드 기반 "Create.aspx" 보기를 "\View\Dinners" 디렉토리에 저장하고 IDE 내에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-282">When we click the "Add" button, Visual Studio will save a new scaffold-based "Create.aspx" view to the "\Views\Dinners" directory, and open it up within the IDE:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

<span data-ttu-id="ccffb-283">우리를 위해 생성 된 기본 "만들기"스캐폴드 파일을 몇 가지 변경하고 아래와 같이 수정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-283">Let's make a few changes to the default "create" scaffold file that was generated for us, and modify it up to look like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

<span data-ttu-id="ccffb-284">이제 응용 프로그램을 실행하고 브라우저 내에서 *"/Dinners/Create"* URL에 액세스하면 작업 구현 만들기에서 아래와 같은 UI를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-284">And now when we run our application and access the *"/Dinners/Create"* URL within the browser it will render UI like below from our Create action implementation:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a><span data-ttu-id="ccffb-285">HTTP-POST 만들기 작업 메서드 구현</span><span class="sxs-lookup"><span data-stu-id="ccffb-285">Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="ccffb-286">우리는 우리의 만들기 작업 메서드의 HTTP-GET 버전을 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-286">We have the HTTP-GET version of our Create action method implemented.</span></span> <span data-ttu-id="ccffb-287">사용자가 "저장" 단추를 클릭하면 */Dinners/Create* URL에 양식 게시물을 수행하고 HTTP &lt;POST&gt; 동사를 사용하여 HTML 입력 양식 값을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-287">When a user clicks the "Save" button it performs a form post to the */Dinners/Create* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span>

<span data-ttu-id="ccffb-288">이제 만들기 작업 메서드의 HTTP POST 동작을 구현해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-288">Let's now implement the HTTP POST behavior of our create action method.</span></span> <span data-ttu-id="ccffb-289">HTTP POST 시나리오를 처리한다는 것을 나타내는 "AcceptVerbs" 특성이 있는 DinnersController에 오버로드된 "만들기" 작업 메서드를 추가하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-289">We'll begin by adding an overloaded "Create" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

<span data-ttu-id="ccffb-290">HTTP-POST 지원 "만들기" 메서드 내에서 게시된 양식 매개 변수에 액세스할 수 있는 방법에는 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-290">There are a variety of ways we can access the posted form parameters within our HTTP-POST enabled "Create" method.</span></span>

<span data-ttu-id="ccffb-291">한 가지 방법은 새 Dinner 개체를 만든 다음 *UpdateModel()* 도우미 메서드(편집 작업에서 와 같이)를 사용하여 게시된 양식 값으로 채우는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-291">One approach is to create a new Dinner object and then use the *UpdateModel()* helper method (like we did with the Edit action) to populate it with the posted form values.</span></span> <span data-ttu-id="ccffb-292">그런 다음 DinnerRepository에 추가하고 데이터베이스에 유지한 다음 사용자를 세부 정보 작업으로 리디렉션하여 아래 코드를 사용하여 새로 만든 Dinner를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-292">We can then add it to our DinnerRepository, persist it to the database, and redirect the user to our Details action to show the newly created Dinner using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

<span data-ttu-id="ccffb-293">또는 Create() 작업 메서드가 Dinner 개체를 메서드 매개 변수로 사용하는 접근 방식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-293">Alternatively, we can use an approach where we have our Create() action method take a Dinner object as a method parameter.</span></span> <span data-ttu-id="ccffb-294">ASP.NET MVC는 자동으로 우리를 위해 새 Dinner 개체를 인스턴스화하고 양식 입력을 사용하여 속성을 채우고 작업 메서드에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-294">ASP.NET MVC will then automatically instantiate a new Dinner object for us, populate its properties using the form inputs, and pass it to our action method:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

<span data-ttu-id="ccffb-295">위의 작업 메서드는 ModelState.IsValid 속성을 확인 하여 Dinner 개체가 양식 게시물 값으로 성공적으로 채워졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-295">Our action method above verifies that the Dinner object has been successfully populated with the form post values by checking the ModelState.IsValid property.</span></span> <span data-ttu-id="ccffb-296">입력 변환 문제(예: EventDate 속성에 대한 "BOGUS" 문자열)가 있고 문제가 있는 경우 작업 메서드가 양식을 다시 표시하는 경우 false가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-296">This will return false if there are input conversion issues (for example: a string of "BOGUS" for the EventDate property), and if there are any issues our action method redisplays the form.</span></span>

<span data-ttu-id="ccffb-297">입력 값이 유효한 경우 작업 메서드는 DinnerRepository에 새 Dinner를 추가하고 저장하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-297">If the input values are valid, then the action method attempts to add and save the new Dinner to the DinnerRepository.</span></span> <span data-ttu-id="ccffb-298">이 작업을 try/catch 블록 내에서 래핑하고 비즈니스 규칙 위반이 있는 경우 양식을 다시 표시합니다(dinnerRepository.Save() 메서드가 예외를 발생시게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-298">It wraps this work within a try/catch block and redisplays the form if there are any business rule violations (which would cause the dinnerRepository.Save() method to raise an exception).</span></span>

<span data-ttu-id="ccffb-299">이 오류 처리 동작이 작동하는 것을 보려면 */Dinners/Create URL을* 요청하고 새 Dinner에 대한 세부 정보를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-299">To see this error handling behavior in action, we can request the */Dinners/Create* URL and fill out details about a new Dinner.</span></span> <span data-ttu-id="ccffb-300">잘못된 입력 이나 값 아래와 같이 강조 된 오류와 함께 만들기 양식다시 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-300">Incorrect input or values will cause the create form to be redisplayed with the errors highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

<span data-ttu-id="ccffb-301">만들기 양식이 편집 양식과 동일한 유효성 검사 및 비즈니스 규칙을 어떻게 준수하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-301">Notice how our Create form is honoring the exact same validation and business rules as our Edit form.</span></span> <span data-ttu-id="ccffb-302">이는 유효성 검사 및 비즈니스 규칙이 모델에 정의되어 있고 응용 프로그램의 UI 또는 컨트롤러 내에 포함되지 않았기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-302">This is because our validation and business rules were defined in the model, and were not embedded within the UI or controller of the application.</span></span> <span data-ttu-id="ccffb-303">즉, 나중에 유효성 검사 또는 비즈니스 규칙을 한 곳에서 변경/발전시키고 응용 프로그램 전체에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-303">This means we can later change/evolve our validation or business rules in a single place and have them apply throughout our application.</span></span> <span data-ttu-id="ccffb-304">기존 규칙이나 수정 사항을 자동으로 준수하기 위해 편집 또는 작업 메서드 만들기 내에서 코드를 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-304">We will not have to change any code within either our Edit or Create action methods to automatically honor any new rules or modifications to existing ones.</span></span>

<span data-ttu-id="ccffb-305">입력 값을 수정하고 "저장" 버튼을 다시 클릭하면 DinnerRepository에 추가가 성공하고 새 Dinner가 데이터베이스에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-305">When we fix the input values and click the "Save" button again, our addition to the DinnerRepository will succeed, and a new Dinner will be added to the database.</span></span> <span data-ttu-id="ccffb-306">그런 다음 */Dinners/Details/[id]* URL로 리디렉션되며 새로 생성된 저녁 식사에 대한 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-306">We will then be redirected to the */Dinners/Details/[id]* URL – where we will be presented with details about the newly created Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a><span data-ttu-id="ccffb-307">지원 삭제</span><span class="sxs-lookup"><span data-stu-id="ccffb-307">Delete Support</span></span>

<span data-ttu-id="ccffb-308">이제 DinnersController에 "삭제" 지원을 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-308">Let's now add "Delete" support to our DinnersController.</span></span>

#### <a name="the-http-get-delete-action-method"></a><span data-ttu-id="ccffb-309">HTTP-GET 삭제 작업 방법</span><span class="sxs-lookup"><span data-stu-id="ccffb-309">The HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="ccffb-310">먼저 삭제 작업 메서드의 HTTP GET 동작을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-310">We'll begin by implementing the HTTP GET behavior of our delete action method.</span></span> <span data-ttu-id="ccffb-311">이 메서드는 누군가가 */Dinners/Delete/id] URL을* 방문할 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-311">This method will get called when someone visits the */Dinners/Delete/[id]* URL.</span></span> <span data-ttu-id="ccffb-312">다음은 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-312">Below is the implementation:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

<span data-ttu-id="ccffb-313">작업 메서드는 삭제할 Dinner를 검색하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-313">The action method attempts to retrieve the Dinner to be deleted.</span></span> <span data-ttu-id="ccffb-314">Dinner가 있는 경우 Dinner 개체를 기반으로 보기를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-314">If the Dinner exists it renders a View based on the Dinner object.</span></span> <span data-ttu-id="ccffb-315">개체가 존재하지 않거나 이미 삭제된 경우 "세부 정보" 작업 메서드를 위해 이전에 만든 "NotFound" 뷰 템플릿을 렌더링하는 뷰를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-315">If the object doesn't exist (or has already been deleted) it returns a View that renders the "NotFound" view template we created earlier for our "Details" action method.</span></span>

<span data-ttu-id="ccffb-316">삭제 작업 메서드 내에서 마우스 오른쪽 단추를 클릭하고 "보기 추가" 컨텍스트 메뉴 명령을 선택하여 "삭제" 보기 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-316">We can create the "Delete" view template by right-clicking within the Delete action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="ccffb-317">"보기 추가" 대화 상자 내에서 Dinner 개체를 뷰 템플릿에 해당 모델로 전달하고 빈 템플릿을 만들도록 선택했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-317">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to create an empty template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

<span data-ttu-id="ccffb-318">"추가" 단추를 클릭하면 Visual Studio에서 "\View\Dinners" 디렉토리 내에 새 "Delete.aspx" 보기 템플릿 파일이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-318">When we click the "Add" button, Visual Studio will add a new "Delete.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="ccffb-319">템플릿에 HTML 및 코드를 추가하여 다음과 같은 삭제 확인 화면을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-319">We'll add some HTML and code to the template to implement a delete confirmation screen like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

<span data-ttu-id="ccffb-320">위의 코드는 삭제할 Dinner의 제목을 표시하고 &lt;최종&gt; 사용자가 해당 내의 "삭제" 단추를 클릭하면 POST를 수행하는 양식 요소를 /Dinners/Delete/[id] URL로 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-320">The code above displays the title of the Dinner to be deleted, and outputs a &lt;form&gt; element that does a POST to the /Dinners/Delete/[id] URL if the end-user clicks the "Delete" button within it.</span></span>

<span data-ttu-id="ccffb-321">응용 프로그램을 실행하고 유효한 Dinner 개체에 대한 *"/Dinners/Delete/id"URL에* 액세스하면 다음과 같이 UI가 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-321">When we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it renders UI like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| <span data-ttu-id="ccffb-322">**측면 주제: POST를 수행하는 이유는 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="ccffb-322">**Side Topic: Why are we doing a POST?**</span></span> |
| --- |
| <span data-ttu-id="ccffb-323">삭제 확인 화면에서 &lt;양식을&gt; 만드는 작업을 거치게 된 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ccffb-323">You might ask – why did we go through the effort of creating a &lt;form&gt; within our Delete confirmation screen?</span></span> <span data-ttu-id="ccffb-324">실제 삭제 작업을 수행하는 작업 메서드에 연결하기 위해 표준 하이퍼링크를 사용하는 것은 어떨까요?</span><span class="sxs-lookup"><span data-stu-id="ccffb-324">Why not just use a standard hyperlink to link to an action method that does the actual delete operation?</span></span> <span data-ttu-id="ccffb-325">그 이유는 웹 크롤러와 검색 엔진이 URL을 발견하고 링크를 따를 때 실수로 데이터가 삭제되는 것을 막기 위해 주의를 기울여야 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-325">The reason is because we want to be careful to guard against web-crawlers and search engines discovering our URLs and inadvertently causing data to be deleted when they follow the links.</span></span> <span data-ttu-id="ccffb-326">HTTP-GET 기반 URL은 액세스/크롤링에 대해 "안전"으로 간주되며 HTTP-POST URL을 따르지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-326">HTTP-GET based URLs are considered "safe" for them to access/crawl, and they are supposed to not follow HTTP-POST ones.</span></span> <span data-ttu-id="ccffb-327">좋은 규칙은 항상 HTTP-POST 요청 뒤에 파괴적 이거나 데이터 수정 작업을 배치 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-327">A good rule is to make sure you always put destructive or data modifying operations behind HTTP-POST requests.</span></span> |

#### <a name="implementing-the-http-post-delete-action-method"></a><span data-ttu-id="ccffb-328">HTTP-POST 삭제 작업 방법 구현</span><span class="sxs-lookup"><span data-stu-id="ccffb-328">Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="ccffb-329">이제 삭제 확인 화면을 표시하는 삭제 작업 메서드의 HTTP-GET 버전이 구현되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-329">We now have the HTTP-GET version of our Delete action method implemented which displays a delete confirmation screen.</span></span> <span data-ttu-id="ccffb-330">최종 사용자가 "삭제" 버튼을 클릭하면 */Dinners/Dinner/[id]* URL에 양식 게시물을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-330">When an end user clicks the "Delete" button it will perform a form post to the */Dinners/Dinner/[id]* URL.</span></span>

<span data-ttu-id="ccffb-331">이제 아래 코드를 사용하여 삭제 작업 메서드의 HTTP "POST" 동작을 구현해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-331">Let's now implement the HTTP "POST" behavior of the delete action method using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

<span data-ttu-id="ccffb-332">삭제 작업 메서드의 HTTP-POST 버전은 삭제할 dinner 개체를 검색하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-332">The HTTP-POST version of our Delete action method attempts to retrieve the dinner object to delete.</span></span> <span data-ttu-id="ccffb-333">찾을 수 없는 경우(이미 삭제되었기 때문에) "NotFound" 템플릿을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-333">If it can't find it (because it has already been deleted) it renders our "NotFound" template.</span></span> <span data-ttu-id="ccffb-334">저녁 식사가 발견되면 DinnerRepository에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-334">If it finds the Dinner, it deletes it from the DinnerRepository.</span></span> <span data-ttu-id="ccffb-335">그런 다음 "삭제됨" 템플릿을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-335">It then renders a "Deleted" template.</span></span>

<span data-ttu-id="ccffb-336">"삭제됨" 템플릿을 구현하려면 작업 메서드에서 마우스 오른쪽 단추로 클릭하고 "보기 추가" 컨텍스트 메뉴를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-336">To implement the "Deleted" template we'll right-click in the action method and choose the "Add View" context menu.</span></span> <span data-ttu-id="ccffb-337">뷰의 이름을 "삭제됨"으로 지정하고 빈 템플릿으로 지정하고 강력한 형식의 모델 개체를 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-337">We'll name our view "Deleted" and have it be an empty template (and not take a strongly-typed model object).</span></span> <span data-ttu-id="ccffb-338">그런 다음 HTML 콘텐츠를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-338">We'll then add some HTML content to it:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

<span data-ttu-id="ccffb-339">그리고 지금 우리가 우리의 응용 프로그램을 실행 하 고 액세스 할 때 *"/Dinners/Delete/id]"* URL 유효한 Dinner 개체에 대 한 그것은 렌더링 됩니다 우리의 Dinner 삭제 확인 화면 아래 와 같이:</span><span class="sxs-lookup"><span data-stu-id="ccffb-339">And now when we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it will render our Dinner delete confirmation screen like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

<span data-ttu-id="ccffb-340">"삭제" 버튼을 클릭하면 데이터베이스에서 Dinner를 삭제하고 "삭제됨" 보기 템플릿을 표시하는 */Dinners/Delete/[id]* URL에 HTTP-POST를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-340">When we click the "Delete" button it will perform an HTTP-POST to the */Dinners/Delete/[id]* URL, which will delete the Dinner from our database, and display our "Deleted" view template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a><span data-ttu-id="ccffb-341">모델 바인딩 보안</span><span class="sxs-lookup"><span data-stu-id="ccffb-341">Model Binding Security</span></span>

<span data-ttu-id="ccffb-342">ASP.NET MVC의 기본 제공 모델 바인딩 기능을 사용하는 두 가지 방법에 대해 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-342">We've discussed two different ways to use the built-in model-binding features of ASP.NET MVC.</span></span> <span data-ttu-id="ccffb-343">첫 번째는 UpdateModel() 메서드를 사용하여 기존 모델 개체의 속성을 업데이트하고 두 번째는 ASP.NET MVC의 지원으로 모델 개체를 작업 메서드 매개 변수로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-343">The first using the UpdateModel() method to update properties on an existing model object, and the second using ASP.NET MVC's support for passing model objects in as action method parameters.</span></span> <span data-ttu-id="ccffb-344">이 두 가지 기술은 모두 매우 강력하고 매우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-344">Both of these techniques are very powerful and extremely useful.</span></span>

<span data-ttu-id="ccffb-345">이 힘은 또한 그 힘으로 책임을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-345">This power also brings with it responsibility.</span></span> <span data-ttu-id="ccffb-346">사용자 입력을 수락할 때 항상 보안에 대해 편집증적으로 하는 것이 중요하며, 개체를 바인딩하여 입력을 형성할 때도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-346">It is important to always be paranoid about security when accepting any user input, and this is also true when binding objects to form input.</span></span> <span data-ttu-id="ccffb-347">HTML 및 JavaScript 주입 공격을 피하기 위해 항상 사용자 입력 된 값을 인코딩하고 SQL 주입 공격에주의해야합니다 (참고 : 이러한 유형의 공격을 방지하기 위해 매개 변수를 자동으로 인코딩하는 응용 프로그램에 LINQto to SQL을 사용하고 있습니다).</span><span class="sxs-lookup"><span data-stu-id="ccffb-347">You should be careful to always HTML encode any user-entered values to avoid HTML and JavaScript injection attacks, and be careful of SQL injection attacks (note: we are using LINQ to SQL for our application, which automatically encodes parameters to prevent these types of attacks).</span></span> <span data-ttu-id="ccffb-348">클라이언트 측 유효성 검사만으로는 절대로 사용하지 말아야 하며 항상 서버 측 유효성 검사를 사용하여 가짜 값을 보내려는 해커를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-348">You should never rely on client-side validation alone, and always employ server-side validation to guard against hackers attempting to send you bogus values.</span></span>

<span data-ttu-id="ccffb-349">ASP.NET MVC의 바인딩 기능을 사용할 때 생각할 수 있는 추가 보안 항목 중 하나는 바인딩할 개체의 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-349">One additional security item to make sure you think about when using the binding features of ASP.NET MVC is the scope of the objects you are binding.</span></span> <span data-ttu-id="ccffb-350">특히 바인딩할 수 있는 속성의 보안 의미를 이해하고 최종 사용자가 실제로 업데이트해야 하는 속성만 업데이트하도록 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-350">Specifically, you want to make sure you understand the security implications of the properties you are allowing to be bound, and make sure you only allow those properties that really should be updatable by an end-user to be updated.</span></span>

<span data-ttu-id="ccffb-351">기본적으로 UpdateModel() 메서드는 들어오는 양식 매개 변수 값과 일치하는 모델 개체의 모든 속성을 업데이트하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-351">By default, the UpdateModel() method will attempt to update all properties on the model object that match incoming form parameter values.</span></span> <span data-ttu-id="ccffb-352">마찬가지로 작업 메서드 매개 변수로 전달된 개체는 기본적으로 양식 매개 변수를 통해 설정된 모든 속성을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-352">Likewise, objects passed as action method parameters also by default can have all of their properties set via form parameters.</span></span>

#### <a name="locking-down-binding-on-a-per-usage-basis"></a><span data-ttu-id="ccffb-353">사용단위로 바인딩 잠금</span><span class="sxs-lookup"><span data-stu-id="ccffb-353">Locking down binding on a per-usage basis</span></span>

<span data-ttu-id="ccffb-354">업데이트할 수 있는 속성의 명시적 "포함 목록"을 제공하여 사용별로 바인딩 정책을 잠글 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-354">You can lock down the binding policy on a per-usage basis by providing an explicit "include list" of properties that can be updated.</span></span> <span data-ttu-id="ccffb-355">이 작업은 다음과 같은 UpdateModel() 메서드에 추가 문자열 배열 매개 변수를 전달하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-355">This can be done by passing an extra string array parameter to the UpdateModel() method like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

<span data-ttu-id="ccffb-356">작업 메서드 매개 변수로 전달된 개체는 다음과 같이 허용된 속성의 "포함 목록"을 지정할 수 있는 [Bind] 특성도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-356">Objects passed as action method parameters also support a [Bind] attribute that enables an "include list" of allowed properties to be specified like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a><span data-ttu-id="ccffb-357">형식별로 바인딩 잠금</span><span class="sxs-lookup"><span data-stu-id="ccffb-357">Locking down binding on a type basis</span></span>

<span data-ttu-id="ccffb-358">형식별로 바인딩 규칙을 잠글 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-358">You can also lock down the binding rules on a per-type basis.</span></span> <span data-ttu-id="ccffb-359">이렇게 하면 바인딩 규칙을 한 번 지정한 다음 모든 컨트롤러 및 작업 메서드에서 모든 시나리오(UpdateModel 및 action 메서드 매개 변수 시나리오 포함)에 적용하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-359">This allows you to specify the binding rules once, and then have them apply in all scenarios (including both UpdateModel and action method parameter scenarios) across all controllers and action methods.</span></span>

<span data-ttu-id="ccffb-360">형식에 [Bind] 특성을 추가하거나 응용 프로그램의 Global.asax 파일 내에 등록하여 형식별 바인딩 규칙을 사용자 지정할 수 있습니다(형식을 소유하지 않은 시나리오에 유용).</span><span class="sxs-lookup"><span data-stu-id="ccffb-360">You can customize the per-type binding rules by adding a [Bind] attribute onto a type, or by registering it within the Global.asax file of the application (useful for scenarios where you don't own the type).</span></span> <span data-ttu-id="ccffb-361">그런 다음 Bind 특성의 Include 및 Exclude 속성을 사용하여 특정 클래스 또는 인터페이스에 바인딩할 수 있는 속성을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-361">You can then use the Bind attribute's Include and Exclude properties to control which properties are bindable for the particular class or interface.</span></span>

<span data-ttu-id="ccffb-362">NerdDinner 응용 프로그램에서 Dinner 클래스에 이 기술을 사용하고 바인딩 가능한 속성 목록을 다음으로 제한하는 [Bind] 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-362">We'll use this technique for the Dinner class in our NerdDinner application, and add a [Bind] attribute to it that restricts the list of bindable properties to the following:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

<span data-ttu-id="ccffb-363">바인딩을 통해 RSVS 컬렉션을 조작할 수 없으며 DinnerID 또는 HostedBy 속성을 바인딩을 통해 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-363">Notice we are not allowing the RSVPs collection to be manipulated via binding, nor are we allowing the DinnerID or HostedBy properties to be set via binding.</span></span> <span data-ttu-id="ccffb-364">보안상의 이유로 작업 메서드 내에서 명시적 코드를 사용하여 이러한 특정 속성만 조작합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-364">For security reasons we'll instead only manipulate these particular properties using explicit code within our action methods.</span></span>

### <a name="crud-wrap-up"></a><span data-ttu-id="ccffb-365">CRUD 랩업</span><span class="sxs-lookup"><span data-stu-id="ccffb-365">CRUD Wrap-Up</span></span>

<span data-ttu-id="ccffb-366">ASP.NET MVC에는 양식 게시 시나리오를 구현하는 데 도움이 되는 여러 기본 제공 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-366">ASP.NET MVC includes a number of built-in features that help with implementing form posting scenarios.</span></span> <span data-ttu-id="ccffb-367">우리는 우리의 DinnerRepository 의 상단에 CRUD UI 지원을 제공하기 위해 이러한 기능의 다양한 사용했다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-367">We used a variety of these features to provide CRUD UI support on top of our DinnerRepository.</span></span>

<span data-ttu-id="ccffb-368">우리는 우리의 응용 프로그램을 구현하기 위해 모델 중심의 접근 방식을 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-368">We are using a model-focused approach to implement our application.</span></span> <span data-ttu-id="ccffb-369">즉, 모든 유효성 검사 및 비즈니스 규칙 논리는 컨트롤러 나 뷰 내에서가 아니라 모델 계층 내에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-369">This means that all our validation and business rule logic is defined within our model layer – and not within our controllers or views.</span></span> <span data-ttu-id="ccffb-370">컨트롤러 클래스나 View 템플릿은 Dinner 모델 클래스에서 적용되는 특정 비즈니스 규칙에 대해 알지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-370">Neither our Controller class nor our View templates know anything about the specific business rules being enforced by our Dinner model class.</span></span>

<span data-ttu-id="ccffb-371">이렇게 하면 응용 프로그램 아키텍처를 깔끔하게 유지하고 테스트하기가 더 쉬워집니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-371">This will keep our application architecture clean and make it easier to test.</span></span> <span data-ttu-id="ccffb-372">나중에 모델 계층에 비즈니스 규칙을 추가할 수 있으며 지원하기 위해 컨트롤러 또는 뷰에 *코드를 변경할 필요가 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="ccffb-372">We can add additional business rules to our model layer in the future and *not have to make any code changes* to our Controller or View in order for them to be supported.</span></span> <span data-ttu-id="ccffb-373">이를 통해 향후 응용 프로그램을 발전시키고 변경할 수 있는 민첩성이 크게 제공될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-373">This is going to provide us with a great deal of agility to evolve and change our application in the future.</span></span>

<span data-ttu-id="ccffb-374">이제 DinnersController를 사용하면 저녁 식사 목록 / 세부 정보뿐만 아니라 지원을 생성, 편집 및 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-374">Our DinnersController now enables Dinner listings/details, as well as create, edit and delete support.</span></span> <span data-ttu-id="ccffb-375">클래스의 전체 코드는 아래에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-375">The complete code for the class can be found below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a><span data-ttu-id="ccffb-376">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ccffb-376">Next Step</span></span>

<span data-ttu-id="ccffb-377">이제 DinnersController 클래스 내에서 기본 CRUD(만들기, 읽기, 업데이트 및 삭제) 지원 구현이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-377">We now have basic CRUD (Create, Read, Update and Delete) support implement within our DinnersController class.</span></span>

<span data-ttu-id="ccffb-378">이제 ViewData 및 ViewModel 클래스를 사용하여 양식에서 더욱 풍부한 UI를 활성화하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ccffb-378">Let's now look at how we can use ViewData and ViewModel classes to enable even richer UI on our forms.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ccffb-379">[이전](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [다음](use-viewdata-and-implement-viewmodel-classes.md)</span><span class="sxs-lookup"><span data-stu-id="ccffb-379">[Previous](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
[Next](use-viewdata-and-implement-viewmodel-classes.md)</span></span>
