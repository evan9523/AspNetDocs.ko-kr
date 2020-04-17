---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: 컨트롤러 및 뷰를 사용하여 리스팅/세부 정보 UI 구현 | 마이크로 소프트 문서
author: rick-anderson
description: 4단계는 사용자에게 데이터 목록/세부 정보 탐색 환경을 제공하기 위해 모델을 활용하는 응용 프로그램에 컨트롤러를 추가하는 방법을 보여 주며...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 49c7dc977477a4edbfcfc68b166ae7ea3fa22f2a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541314"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a><span data-ttu-id="1b4c0-103">컨트롤러 및 보기를 사용하여 목록/세부 정보 UI 구현</span><span class="sxs-lookup"><span data-stu-id="1b4c0-103">Use Controllers and Views to Implement a Listing/Details UI</span></span>

<span data-ttu-id="1b4c0-104">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1b4c0-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="1b4c0-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="1b4c0-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="1b4c0-106">이것은 MVC 1을 ASP.NET 사용하여 작지만 완전한 웹 응용 프로그램을 빌드하는 방법을 안내하는 무료 ["NerdDinner" 응용 프로그램 자습서의](introducing-the-nerddinner-tutorial.md) 4단계입니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-106">This is step 4 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="1b4c0-107">4단계는 NerdDinner 사이트에서 저녁 식사에 대한 데이터 목록/세부 정보 탐색 환경을 사용자에게 제공하기 위해 모델을 활용하는 응용 프로그램에 컨트롤러를 추가하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-107">Step 4 shows how to add a Controller to the application that takes advantage of our model to provide users with a data listing/details navigation experience for dinners on our NerdDinner site.</span></span>
> 
> <span data-ttu-id="1b4c0-108">MVC 3을 ASP.NET 사용하는 경우 [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC 뮤직 스토어](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-4-controllers-and-views"></a><span data-ttu-id="1b4c0-109">얼간이 디너 4 단계 : 컨트롤러 및 전망</span><span class="sxs-lookup"><span data-stu-id="1b4c0-109">NerdDinner Step 4: Controllers and Views</span></span>

<span data-ttu-id="1b4c0-110">기존 웹 프레임워크(클래식 ASP, PHP, ASP.NET 웹 양식 등)를 사용하면 일반적으로 들어오는 URL이 디스크의 파일에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-110">With traditional web frameworks (classic ASP, PHP, ASP.NET Web Forms, etc), incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="1b4c0-111">예를 들어 "/Products.aspx" 또는 "/Products.php"와 같은 URL 요청은 "Products.aspx" 또는 "Products.php" 파일에서 처리될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="1b4c0-112">웹 기반 MVC 프레임워크는 URL을 약간 다른 방식으로 서버 코드에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="1b4c0-113">들어오는 URL을 파일에 매핑하는 대신 URL을 클래스의 메소드에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="1b4c0-114">이러한 클래스는 "컨트롤러"라고 하며 들어오는 HTTP 요청을 처리하고, 사용자 입력을 처리하고, 데이터를 검색 및 저장하고, 클라이언트로 다시 보낼 응답을 결정합니다(HTML 표시, 파일 다운로드, 다른 URL로 리디렉션 등).</span><span class="sxs-lookup"><span data-stu-id="1b4c0-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc).</span></span>

<span data-ttu-id="1b4c0-115">이제 NerdDinner 응용 프로그램에 대한 기본 모델을 구축했기 때문에 다음 단계는 이를 활용하여 사용자에게 당사 사이트의 Dinners에 대한 데이터 목록/세부 정보 탐색 환경을 제공하는 응용 프로그램에 컨트롤러를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-115">Now that we have built up a basic model for our NerdDinner application, our next step will be to add a Controller to the application that takes advantage of it to provide users with a data listing/details navigation experience for Dinners on our site.</span></span>

### <a name="adding-a-dinnerscontroller-controller"></a><span data-ttu-id="1b4c0-116">저녁 식사 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="1b4c0-116">Adding a DinnersController Controller</span></span>

<span data-ttu-id="1b4c0-117">먼저 웹 프로젝트 내의 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭한 다음 **추가&gt;컨트롤러** 메뉴 명령을 선택합니다(Ctrl-M, Ctrl-C를 입력하여 이 명령을 실행할 수도 있음).</span><span class="sxs-lookup"><span data-stu-id="1b4c0-117">We'll begin by right-clicking on the "Controllers" folder within our web project, and then select the **Add-&gt;Controller** menu command (you can also execute this command by typing Ctrl-M, Ctrl-C):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

<span data-ttu-id="1b4c0-118">그러면 "컨트롤러 추가" 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-118">This will bring up the "Add Controller" dialog:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

<span data-ttu-id="1b4c0-119">새 컨트롤러의 이름을 "DinnersController"로 지정하고 "추가" 버튼을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-119">We'll name the new controller "DinnersController" and click the "Add" button.</span></span> <span data-ttu-id="1b4c0-120">비주얼 스튜디오는 우리의 \Controllers 디렉토리아래에 DinnersController.cs 파일을 추가합니다 :</span><span class="sxs-lookup"><span data-stu-id="1b4c0-120">Visual Studio will then add a DinnersController.cs file under our \Controllers directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

<span data-ttu-id="1b4c0-121">또한 코드 편집기 내에서 새 DinnersController 클래스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-121">It will also open up the new DinnersController class within the code-editor.</span></span>

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a><span data-ttu-id="1b4c0-122">DinnersController 클래스에 인덱스() 및 세부 정보() 작업 메서드 추가</span><span class="sxs-lookup"><span data-stu-id="1b4c0-122">Adding Index() and Details() Action Methods to the DinnersController Class</span></span>

<span data-ttu-id="1b4c0-123">우리는 우리의 응용 프로그램을 사용하여 방문자가 곧 저녁 식사의 목록을 검색 할 수 있도록하고, 그들이 그것에 대해 특정 세부 사항을 볼 수있는 목록의 모든 저녁 식사를 클릭 할 수 있도록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-123">We want to enable visitors using our application to browse a list of upcoming dinners, and allow them to click on any Dinner in the list to see specific details about it.</span></span> <span data-ttu-id="1b4c0-124">응용 프로그램에서 다음 URL을 게시하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-124">We'll do this by publishing the following URLs from our application:</span></span>

| <span data-ttu-id="1b4c0-125">**URL**</span><span class="sxs-lookup"><span data-stu-id="1b4c0-125">**URL**</span></span> | <span data-ttu-id="1b4c0-126">**용도**</span><span class="sxs-lookup"><span data-stu-id="1b4c0-126">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="1b4c0-127">*/저녁 식사/*</span><span class="sxs-lookup"><span data-stu-id="1b4c0-127">*/Dinners/*</span></span> | <span data-ttu-id="1b4c0-128">다가오는 저녁 식사의 HTML 목록을 표시</span><span class="sxs-lookup"><span data-stu-id="1b4c0-128">Display an HTML list of upcoming dinners</span></span> |
| <span data-ttu-id="1b4c0-129">*/저녁 식사/세부 정보/[ID]*</span><span class="sxs-lookup"><span data-stu-id="1b4c0-129">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="1b4c0-130">URL 내에 포함된 "id" 매개 변수로 표시된 특정 저녁 식사에 대한 세부 정보를 표시하여 데이터베이스의 DinnerID와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-130">Display details about a specific dinner indicated by an "id" parameter embedded within the URL – which will match the DinnerID of the dinner in the database.</span></span> <span data-ttu-id="1b4c0-131">예: /Dinners/Details/2는 DinnerID 값이 2인 DinnerID에 대한 세부 정보가 있는 HTML 페이지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-131">For example: /Dinners/Details/2 would display an HTML page with details about the Dinner whose DinnerID value is 2.</span></span> |

<span data-ttu-id="1b4c0-132">아래와 같이 DinnersController 클래스에 두 개의 공개 "작업 메서드"를 추가하여 이러한 URL의 초기 구현을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-132">We will publish initial implementations of these URLs by adding two public "action methods" to our DinnersController class like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

<span data-ttu-id="1b4c0-133">그런 다음 NerdDinner 응용 프로그램을 실행하고 브라우저를 사용하여 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-133">We'll then run the NerdDinner application and use our browser to invoke them.</span></span> <span data-ttu-id="1b4c0-134">*"/Dinners/"* URL을 입력하면 *Index()* 메서드가 실행되고 다음 응답이 다시 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-134">Typing in the *"/Dinners/"* URL will cause our *Index()* method to run, and it will send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

<span data-ttu-id="1b4c0-135">*"/Dinners/Details/2"* URL을 입력하면 *Details()* 메서드가 실행되고 다음 응답을 다시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-135">Typing in the *"/Dinners/Details/2"* URL will cause our *Details()* method to run, and send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

<span data-ttu-id="1b4c0-136">당신은 궁금해 할 수 있습니다 - ASP.NET MVC는 어떻게 우리의 DinnersController 클래스를 만들고 그 방법을 호출하는 것을 알고 있었습니까?</span><span class="sxs-lookup"><span data-stu-id="1b4c0-136">You might be wondering - how did ASP.NET MVC know to create our DinnersController class and invoke those methods?</span></span> <span data-ttu-id="1b4c0-137">라우팅의 작동 방식을 간략하게 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-137">To understand that let's take a quick look at how routing works.</span></span>

### <a name="understanding-aspnet-mvc-routing"></a><span data-ttu-id="1b4c0-138">mVC 라우팅에 ASP.NET 이해</span><span class="sxs-lookup"><span data-stu-id="1b4c0-138">Understanding ASP.NET MVC Routing</span></span>

<span data-ttu-id="1b4c0-139">ASP.NET MVC에는 URL이 컨트롤러 클래스에 매핑되는 방식을 제어하는 데 많은 유연성을 제공하는 강력한 URL 라우팅 엔진이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-139">ASP.NET MVC includes a powerful URL routing engine that provides a lot of flexibility in controlling how URLs are mapped to controller classes.</span></span> <span data-ttu-id="1b4c0-140">이를 통해 ASP.NET MVC가 만들 컨트롤러 클래스를 선택하는 방법, 호출할 메서드를 완전히 사용자 지정할 수 있을 뿐만 아니라 URL/Querystring에서 변수를 자동으로 구문 분석하여 매개 변수 인수로 메서드에 전달할 수 있는 다양한 방법을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-140">It allows us to completely customize how ASP.NET MVC chooses which controller class to create, which method to invoke on it, as well as configure different ways that variables can be automatically parsed from the URL/Querystring and passed to the method as parameter arguments.</span></span> <span data-ttu-id="1b4c0-141">SEO(검색 엔진 최적화)에 대한 사이트를 완전히 최적화하고 응용 프로그램에서 원하는 URL 구조를 게시할 수 있는 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-141">It delivers the flexibility to totally optimize a site for SEO (search engine optimization) as well as publish any URL structure we want from an application.</span></span>

<span data-ttu-id="1b4c0-142">기본적으로 새 ASP.NET MVC 프로젝트에는 이미 등록된 미리 구성된 URL 라우팅 규칙 집합이 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-142">By default, new ASP.NET MVC projects come with a preconfigured set of URL routing rules already registered.</span></span> <span data-ttu-id="1b4c0-143">이렇게 하면 명시적으로 구성할 필요 없이 응용 프로그램에서 쉽게 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-143">This enables us to easily get started on an application without having to explicitly configure anything.</span></span> <span data-ttu-id="1b4c0-144">기본 라우팅 규칙 등록은 프로젝트의 "응용 프로그램" 클래스에서 찾을 수 있으며, 프로젝트 루트의 "Global.asax" 파일을 두 번 클릭하여 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-144">The default routing rule registrations can be found within the "Application" class of our projects – which we can open by double-clicking the "Global.asax" file in the root of our project:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

<span data-ttu-id="1b4c0-145">기본 ASP.NET MVC 라우팅 규칙은 이 클래스의 "RegisterRoutes" 메서드 내에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-145">The default ASP.NET MVC routing rules are registered within the "RegisterRoutes" method of this class:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

<span data-ttu-id="1b4c0-146">"경로입니다. 위의 MapRoute()" 메서드 호출은 들어오는 URL을 URL 형식을 사용하여 컨트롤러 클래스에 매핑하는 기본 라우팅 규칙을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-146">The "routes.MapRoute()" method call above registers a default routing rule that maps incoming URLs to controller classes using the URL format: "/{controller}/{action}/{id}" – where "controller" is the name of the controller class to instantiate, "action" is the name of a public method to invoke on it, and "id" is an optional parameter embedded within the URL that can be passed as an argument to the method.</span></span> <span data-ttu-id="1b4c0-147">"MapRoute()" 메서드 호출에 전달된 세 번째 매개 변수는 URL에 없는 경우 컨트롤러/작업/ID 값에 사용할 기본값 집합입니다(컨트롤러 = "홈", Action="Index", Id=").</span><span class="sxs-lookup"><span data-stu-id="1b4c0-147">The third parameter passed to the "MapRoute()" method call is a set of default values to use for the controller/action/id values in the event that they are not present in the URL (Controller = "Home", Action="Index", Id="").</span></span>

<span data-ttu-id="1b4c0-148">다음은 기본<em>"/{컨트롤러}/{action}/{id}"</em>경로 규칙을 사용하여 다양한 URL이 매핑되는 방법을 보여 주는 표입니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-148">Below is a table that demonstrates how a variety of URLs are mapped using the default "<em>/{controllers}/{action}/{id}"</em>route rule:</span></span>

| <span data-ttu-id="1b4c0-149">**URL**</span><span class="sxs-lookup"><span data-stu-id="1b4c0-149">**URL**</span></span> | <span data-ttu-id="1b4c0-150">**컨트롤러 클래스**</span><span class="sxs-lookup"><span data-stu-id="1b4c0-150">**Controller Class**</span></span> | <span data-ttu-id="1b4c0-151">**작업 방법**</span><span class="sxs-lookup"><span data-stu-id="1b4c0-151">**Action Method**</span></span> | <span data-ttu-id="1b4c0-152">**통과된 매개 변수**</span><span class="sxs-lookup"><span data-stu-id="1b4c0-152">**Parameters Passed**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1b4c0-153">*/저녁 식사/세부 정보/2*</span><span class="sxs-lookup"><span data-stu-id="1b4c0-153">*/Dinners/Details/2*</span></span> | <span data-ttu-id="1b4c0-154">저녁 식사 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="1b4c0-154">DinnersController</span></span> | <span data-ttu-id="1b4c0-155">세부 정보(id)</span><span class="sxs-lookup"><span data-stu-id="1b4c0-155">Details(id)</span></span> | <span data-ttu-id="1b4c0-156">id=2</span><span class="sxs-lookup"><span data-stu-id="1b4c0-156">id=2</span></span> |
| <span data-ttu-id="1b4c0-157">*/저녁 식사/편집/5*</span><span class="sxs-lookup"><span data-stu-id="1b4c0-157">*/Dinners/Edit/5*</span></span> | <span data-ttu-id="1b4c0-158">저녁 식사 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="1b4c0-158">DinnersController</span></span> | <span data-ttu-id="1b4c0-159">편집(id)</span><span class="sxs-lookup"><span data-stu-id="1b4c0-159">Edit(id)</span></span> | <span data-ttu-id="1b4c0-160">id=5</span><span class="sxs-lookup"><span data-stu-id="1b4c0-160">id=5</span></span> |
| <span data-ttu-id="1b4c0-161">*/저녁 식사/만들기*</span><span class="sxs-lookup"><span data-stu-id="1b4c0-161">*/Dinners/Create*</span></span> | <span data-ttu-id="1b4c0-162">저녁 식사 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="1b4c0-162">DinnersController</span></span> | <span data-ttu-id="1b4c0-163">Create()</span><span class="sxs-lookup"><span data-stu-id="1b4c0-163">Create()</span></span> | <span data-ttu-id="1b4c0-164">해당 없음</span><span class="sxs-lookup"><span data-stu-id="1b4c0-164">N/A</span></span> |
| <span data-ttu-id="1b4c0-165">*/디너*</span><span class="sxs-lookup"><span data-stu-id="1b4c0-165">*/Dinners*</span></span> | <span data-ttu-id="1b4c0-166">저녁 식사 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="1b4c0-166">DinnersController</span></span> | <span data-ttu-id="1b4c0-167">색인()</span><span class="sxs-lookup"><span data-stu-id="1b4c0-167">Index()</span></span> | <span data-ttu-id="1b4c0-168">해당 없음</span><span class="sxs-lookup"><span data-stu-id="1b4c0-168">N/A</span></span> |
| <span data-ttu-id="1b4c0-169">*/home*</span><span class="sxs-lookup"><span data-stu-id="1b4c0-169">*/Home*</span></span> | <span data-ttu-id="1b4c0-170">홈 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="1b4c0-170">HomeController</span></span> | <span data-ttu-id="1b4c0-171">색인()</span><span class="sxs-lookup"><span data-stu-id="1b4c0-171">Index()</span></span> | <span data-ttu-id="1b4c0-172">해당 없음</span><span class="sxs-lookup"><span data-stu-id="1b4c0-172">N/A</span></span> |
| */* | <span data-ttu-id="1b4c0-173">홈 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="1b4c0-173">HomeController</span></span> | <span data-ttu-id="1b4c0-174">색인()</span><span class="sxs-lookup"><span data-stu-id="1b4c0-174">Index()</span></span> | <span data-ttu-id="1b4c0-175">해당 없음</span><span class="sxs-lookup"><span data-stu-id="1b4c0-175">N/A</span></span> |

<span data-ttu-id="1b4c0-176">마지막 세 행에는 사용 중인 기본값(컨트롤러 = 홈, 작업 = 인덱스, ID = "")이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-176">The last three rows show the default values (Controller = Home, Action = Index, Id = "") being used.</span></span> <span data-ttu-id="1b4c0-177">"Index" 메서드가 지정되지 않은 경우 기본 작업 이름으로 등록되므로 "/Dinners" 및 "/Home" URL은 Index() 작업 메서드를 컨트롤러 클래스에서 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-177">Because the "Index" method is registered as the default action name if one isn't specified, the "/Dinners" and "/Home" URLs cause the Index() action method to be invoked on their Controller classes.</span></span> <span data-ttu-id="1b4c0-178">"홈" 컨트롤러가 지정되지 않은 경우 기본 컨트롤러로 등록되므로 "/" URL을 사용하면 HomeController가 만들어지고 해당 컨트롤러의 Index() 작업 메서드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-178">Because the "Home" controller is registered as the default controller if one isn't specified, the "/" URL causes the HomeController to be created, and the Index() action method on it to be invoked.</span></span>

<span data-ttu-id="1b4c0-179">이러한 기본 URL 라우팅 규칙이 마음에 들지 않으면 좋은 소식은 변경하기 쉽다는 것입니다 .</span><span class="sxs-lookup"><span data-stu-id="1b4c0-179">If you don't like these default URL routing rules, the good news is that they are easy to change - just edit them within the RegisterRoutes method above.</span></span> <span data-ttu-id="1b4c0-180">하지만 NerdDinner 응용 프로그램의 경우 기본 URL 라우팅 규칙을 변경하지 는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-180">For our NerdDinner application, though, we aren't going to change any of the default URL routing rules – instead we'll just use them as-is.</span></span>

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a><span data-ttu-id="1b4c0-181">저녁 식사 사용우리의 저녁 식사에서 리포지토리컨트롤러</span><span class="sxs-lookup"><span data-stu-id="1b4c0-181">Using the DinnerRepository from our DinnersController</span></span>

<span data-ttu-id="1b4c0-182">이제 DinnersController의 인덱스() 및 Details() 작업 메서드의 현재 구현을 모델을 사용하는 구현으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-182">Let's now replace our current implementation of the DinnersController's Index() and Details() action methods with implementations that use our model.</span></span>

<span data-ttu-id="1b4c0-183">이전에 빌드한 DinnerRepository 클래스를 사용하여 동작을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-183">We'll use the DinnerRepository class we built earlier to implement the behavior.</span></span> <span data-ttu-id="1b4c0-184">먼저 "NerdDinner.Models" 네임스페이스를 참조하는 "사용" 문을 추가한 다음 DinnerController 클래스의 필드로 DinnerRepository 인스턴스를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-184">We'll begin by adding a "using" statement that references the "NerdDinner.Models" namespace, and then declare an instance of our DinnerRepository as a field on our DinnerController class.</span></span>

<span data-ttu-id="1b4c0-185">이 장의 후반부에서는 "종속성 주입"의 개념을 소개하고 컨트롤러가 더 나은 단위 테스트를 가능하게 하는 DinnerRepository에 대한 참조를 얻을 수 있는 또 다른 방법을 보여 드리지만, 지금은 아래와 같이 DinnerRepository 인라인의 인스턴스를 만들 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-185">Later in this chapter we'll introduce the concept of "Dependency Injection" and show another way for our Controllers to obtain a reference to a DinnerRepository that enables better unit testing – but for right now we'll just create an instance of our DinnerRepository inline like below.</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

<span data-ttu-id="1b4c0-186">이제 검색된 데이터 모델 개체를 사용하여 HTML 응답을 다시 생성할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-186">Now we are ready to generate a HTML response back using our retrieved data model objects.</span></span>

### <a name="using-views-with-our-controller"></a><span data-ttu-id="1b4c0-187">컨트롤러와 뷰 사용</span><span class="sxs-lookup"><span data-stu-id="1b4c0-187">Using Views with our Controller</span></span>

<span data-ttu-id="1b4c0-188">작업 메서드 내에서 코드를 작성하여 HTML을 어셈블한 다음 *Response.Write()* 도우미 메서드를 사용하여 클라이언트로 다시 보낼 수 있지만 해당 접근 방식은 매우 다루기 어려워집니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-188">While it is possible to write code within our action methods to assemble HTML and then use the *Response.Write()* helper method to send it back to the client, that approach becomes fairly unwieldy quickly.</span></span> <span data-ttu-id="1b4c0-189">훨씬 더 나은 방법은 DinnersController 작업 메서드 내에서 응용 프로그램 및 데이터 논리만 수행 한 다음 HTML 표현을 입력하는 별도의 "보기" 템플릿에 HTML 응답을 렌더링하는 데 필요한 데이터를 전달하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-189">A much better approach is for us to only perform application and data logic inside our DinnersController action methods, and to then pass the data needed to render a HTML response to a separate "view" template that is responsible for outputting the HTML representation of it.</span></span> <span data-ttu-id="1b4c0-190">잠시 후 볼 수 있듯이 "보기" 템플릿은 일반적으로 HTML 태그와 포함된 렌더링 코드의 조합을 포함하는 텍스트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-190">As we'll see in a moment, a "view" template is a text file that typically contains a combination of HTML markup and embedded rendering code.</span></span>

<span data-ttu-id="1b4c0-191">뷰 렌더링에서 컨트롤러 논리를 분리하면 몇 가지 큰 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-191">Separating our controller logic from our view rendering brings several big benefits.</span></span> <span data-ttu-id="1b4c0-192">특히 응용 프로그램 코드와 UI 서식/렌더링 코드 간에 명확한 "문제 분리"를 적용하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-192">In particular it helps enforce a clear "separation of concerns" between the application code and UI formatting/rendering code.</span></span> <span data-ttu-id="1b4c0-193">이렇게 하면 UI 렌더링 논리에서 격리하여 응용 프로그램 논리를 단위 테스트하기가 훨씬 쉬워집니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-193">This makes it much easier to unit-test application logic in isolation from UI rendering logic.</span></span> <span data-ttu-id="1b4c0-194">나중에 응용 프로그램 코드를 변경하지 않고도 UI 렌더링 템플릿을 쉽게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-194">It makes it easier to later modify the UI rendering templates without having to make application code changes.</span></span> <span data-ttu-id="1b4c0-195">또한 개발자와 디자이너가 프로젝트에서 함께 공동 작업을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-195">And it can make it easier for developers and designers to collaborate together on projects.</span></span>

<span data-ttu-id="1b4c0-196">DinnersController 클래스를 업데이트하여 두 작업 메서드의 메서드 시그니처를 반환 형식의 "void"에서 "ActionResult"의 반환 형식을 변경하는 대신 HTML UI 응답을 다시 보내려면 뷰 템플릿을 사용할 수 있음을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-196">We can update our DinnersController class to indicate that we want to use a view template to send back an HTML UI response by changing the method signatures of our two action methods from having a return type of "void" to instead have a return type of "ActionResult".</span></span> <span data-ttu-id="1b4c0-197">그런 다음 Controller 기본 클래스의 *View()* 도우미 메서드를 호출하여 아래와 같은 "ViewResult" 개체를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-197">We can then call the *View()* helper method on the Controller base class to return back a "ViewResult" object like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

<span data-ttu-id="1b4c0-198">위에서 사용 중인 *View()* 도우미 메서드의 서명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-198">The signature of the *View()* helper method we are using above looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

<span data-ttu-id="1b4c0-199">*View()* 도우미 메서드의 첫 번째 매개 변수는 HTML 응답을 렌더링하는 데 사용할 뷰 템플릿 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-199">The first parameter to the *View()* helper method is the name of the view template file we want to use to render the HTML response.</span></span> <span data-ttu-id="1b4c0-200">두 번째 매개 변수는 HTML 응답을 렌더링하기 위해 뷰 템플릿에 필요한 데이터를 포함하는 모델 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-200">The second parameter is a model object that contains the data that the view template needs in order to render the HTML response.</span></span>

<span data-ttu-id="1b4c0-201">Index() 작업 메서드 내에서 *View()* 도우미 메서드를 호출 하 고 "Index" 보기 템플릿을 사용 하 여 저녁 식사의 HTML 목록을 렌더링 하려는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-201">Within our Index() action method we are calling the *View()* helper method and indicating that we want to render an HTML listing of dinners using an "Index" view template.</span></span> <span data-ttu-id="1b4c0-202">우리는 보기 템플릿에서 목록을 생성하는 Dinner 개체의 시퀀스를 전달하고 있습니다 .</span><span class="sxs-lookup"><span data-stu-id="1b4c0-202">We are passing the view template a sequence of Dinner objects to generate the list from:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

<span data-ttu-id="1b4c0-203">Details() 작업 메서드 내에서 URL 내에 제공된 ID를 사용하여 Dinner 개체를 검색하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-203">Within our Details() action method we attempt to retrieve a Dinner object using the id provided within the URL.</span></span> <span data-ttu-id="1b4c0-204">유효한 Dinner가 발견되면 *View()* 도우미 메서드를 호출하여 "세부 정보" 보기 템플릿을 사용하여 검색된 Dinner 개체를 렌더링할 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-204">If a valid Dinner is found we call the *View()* helper method, indicating we want to use a "Details" view template to render the retrieved Dinner object.</span></span> <span data-ttu-id="1b4c0-205">잘못된 Dinner가 요청되면 Dinner가 "NotFound" 보기 템플릿(및 템플릿 이름을 사용하는 *View()* 도우미 메서드의 오버로드된 버전을 사용하여 존재하지 않음을 나타내는 유용한 오류 메시지를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-205">If an invalid dinner is requested, we render a helpful error message that indicates that the Dinner doesn't exist using a "NotFound" view template (and an overloaded version of the *View()* helper method that just takes the template name):</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

<span data-ttu-id="1b4c0-206">이제 "NotFound", "세부 정보" 및 "색인" 보기 템플릿을 구현해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-206">Let's now implement the "NotFound", "Details", and "Index" view templates.</span></span>

### <a name="implementing-the-notfound-view-template"></a><span data-ttu-id="1b4c0-207">"찾을 수 없는" 보기 템플릿 구현</span><span class="sxs-lookup"><span data-stu-id="1b4c0-207">Implementing the "NotFound" View Template</span></span>

<span data-ttu-id="1b4c0-208">먼저 요청한 저녁 식사를 찾을 수 없다는 친숙한 오류 메시지를 표시하는 "NotFound" 보기 템플릿을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-208">We'll begin by implementing the "NotFound" view template – which displays a friendly error message indicating that the requested dinner can't be found.</span></span>

<span data-ttu-id="1b4c0-209">컨트롤러 작업 메서드 내에서 텍스트 커서를 배치하여 새 보기 템플릿을 만든 다음 마우스 오른쪽 단추로 클릭하고 "보기 추가" 메뉴 명령을 선택합니다(Ctrl-M, Ctrl-V를 입력하여 이 명령을 실행할 수도 있음).</span><span class="sxs-lookup"><span data-stu-id="1b4c0-209">We'll create a new view template by positioning our text cursor within a controller action method, and then right click and choose the "Add View" menu command (we can also execute this command by typing Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

<span data-ttu-id="1b4c0-210">그러면 아래와 같은 "보기 추가" 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-210">This will bring up an "Add View" dialog like below.</span></span> <span data-ttu-id="1b4c0-211">기본적으로 대화 상자는 대화 상자가 시작될 때 커서가 있던 작업 메서드의 이름과 일치하도록 만들 뷰의 이름을 미리 채웁니다(이 경우 "세부 정보").</span><span class="sxs-lookup"><span data-stu-id="1b4c0-211">By default the dialog will pre-populate the name of the view to create to match the name of the action method the cursor was in when the dialog was launched (in this case "Details").</span></span> <span data-ttu-id="1b4c0-212">먼저 "NotFound" 템플릿을 구현하려고 하기 때문에 이 보기 이름을 재정의하고 대신 "NotFound"로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-212">Because we want to first implement the "NotFound" template, we'll override this view name and set it to instead be "NotFound":</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

<span data-ttu-id="1b4c0-213">"추가" 단추를 클릭하면 Visual Studio에서 "\View\Dinners" 디렉토리 내에서 새 "NotFound.aspx" 보기 템플릿을 만듭니다(디렉토리가 아직 없는 경우에도 생성됨).</span><span class="sxs-lookup"><span data-stu-id="1b4c0-213">When we click the "Add" button, Visual Studio will create a new "NotFound.aspx" view template for us within the "\Views\Dinners" directory (which it will also create if the directory doesn't already exist):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

<span data-ttu-id="1b4c0-214">또한 코드 편집기 내에서 새로운 "NotFound.aspx" 보기 템플릿을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-214">It will also open up our new "NotFound.aspx" view template within the code-editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

<span data-ttu-id="1b4c0-215">기본적으로 보기 템플릿에는 콘텐츠와 코드를 추가할 수 있는 두 개의 "콘텐츠 영역"이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-215">View templates by default have two "content regions" where we can add content and code.</span></span> <span data-ttu-id="1b4c0-216">첫 번째는 우리가 다시 전송 된 HTML 페이지의 "제목"을 사용자 정의 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-216">The first allows us to customize the "title" of the HTML page sent back.</span></span> <span data-ttu-id="1b4c0-217">두 번째는 우리가 다시 전송 된 HTML 페이지의 "주요 콘텐츠"를 사용자 정의 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-217">The second allows us to customize the "main content" of the HTML page sent back.</span></span>

<span data-ttu-id="1b4c0-218">"NotFound" 보기 템플릿을 구현하기 위해 몇 가지 기본 콘텐츠를 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-218">To implement our "NotFound" view template we'll add some basic content:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

<span data-ttu-id="1b4c0-219">우리는 다음 브라우저 내에서 그것을 밖으로 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-219">We can then try it out within the browser.</span></span> <span data-ttu-id="1b4c0-220">이렇게 하려면 *"/저녁 식사/세부 정보/9999" URL을* 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-220">To do this let's request the *"/Dinners/Details/9999"* URL.</span></span> <span data-ttu-id="1b4c0-221">이것은 현재 데이터베이스에 존재하지 않는 DinnersController.Details() 작업 메서드가 "NotFound" 보기 템플릿을 렌더링하는 데 필요한 DinnersController.Details(작업 메서드)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-221">This will refer to a dinner that doesn't currently exist in the database, and will cause our DinnersController.Details() action method to render our "NotFound" view template:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

<span data-ttu-id="1b4c0-222">위의 스크린 샷에서 알 수 있는 한 가지는 기본 보기 템플릿이 화면의 주요 콘텐츠를 둘러싸는 많은 HTML을 상속했다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-222">One thing you'll notice in the screen-shot above is that our basic view template has inherited a bunch of HTML that surrounds the main content on the screen.</span></span> <span data-ttu-id="1b4c0-223">뷰 템플릿이 사이트의 모든 뷰에 일관된 레이아웃을 적용할 수 있는 "마스터 페이지" 템플릿을 사용하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-223">This is because our view-template is using a "master page" template that enables us to apply a consistent layout across all views on the site.</span></span> <span data-ttu-id="1b4c0-224">이 자습서의 후반부에서 마스터 페이지가 어떻게 작동하는지 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-224">We'll discuss how master pages work more in a later part of this tutorial.</span></span>

### <a name="implementing-the-details-view-template"></a><span data-ttu-id="1b4c0-225">"세부 정보" 보기 템플릿 구현</span><span class="sxs-lookup"><span data-stu-id="1b4c0-225">Implementing the "Details" View Template</span></span>

<span data-ttu-id="1b4c0-226">이제 단일 Dinner 모델에 대한 HTML을 생성하는 "세부 정보" 보기 템플릿을 구현해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-226">Let's now implement the "Details" view template – which will generate HTML for a single Dinner model.</span></span>

<span data-ttu-id="1b4c0-227">세부 정보 작업 메서드 내에서 텍스트 커서를 배치한 다음 마우스 오른쪽 단추를 클릭하고 "보기 추가" 메뉴 명령을 선택합니다(또는 Ctrl-M, Ctrl-V 를 누릅니다).</span><span class="sxs-lookup"><span data-stu-id="1b4c0-227">We'll do this by positioning our text cursor within the Details action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

<span data-ttu-id="1b4c0-228">그러면 "보기 추가" 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-228">This will bring up the "Add View" dialog.</span></span> <span data-ttu-id="1b4c0-229">기본 보기 이름("세부 정보")을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-229">We'll keep the default view name ("Details").</span></span> <span data-ttu-id="1b4c0-230">또한 대화 상자에서 "강력한 형식의 보기 만들기" 확인란을 선택하고 컨트롤러에서 뷰로 전달하는 모델 유형의 이름을 선택합니다(콤보박스 드롭다운 사용).</span><span class="sxs-lookup"><span data-stu-id="1b4c0-230">We'll also select the "Create a strongly-typed View" checkbox in the dialog and select (using the combobox dropdown) the name of the model type we are passing from the Controller to the View.</span></span> <span data-ttu-id="1b4c0-231">이 보기의 경우 Dinner 개체를 전달합니다(이 형식의 정규화된 이름은 "NerdDinner.Models.Dinner"입니다).</span><span class="sxs-lookup"><span data-stu-id="1b4c0-231">For this view we are passing a Dinner object (the fully qualified name for this type is: "NerdDinner.Models.Dinner"):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

<span data-ttu-id="1b4c0-232">"빈 보기"를 만들기로 선택한 이전 템플릿과 달리 이번에는 "세부 정보" 템플릿을 사용하여 뷰를 자동으로 "스캐폴드"하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-232">Unlike the previous template, where we chose to create an "Empty View", this time we will choose to automatically "scaffold" the view using a "Details" template.</span></span> <span data-ttu-id="1b4c0-233">위의 대화 상자에서 "콘텐츠 보기" 드롭다운을 변경하여 이를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-233">We can indicate this by changing the "View content" drop-down in the dialog above.</span></span>

<span data-ttu-id="1b4c0-234">"스캐폴딩"은 우리가 전달하는 Dinner 개체를 기반으로 세부 정보 보기 템플릿의 초기 구현을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-234">"Scaffolding" will generate an initial implementation of our details view template based on the Dinner object we are passing to it.</span></span> <span data-ttu-id="1b4c0-235">이렇게 하면 뷰 템플릿 구현을 빠르게 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-235">This provides an easy way for us to quickly get started on our view template implementation.</span></span>

<span data-ttu-id="1b4c0-236">"추가" 단추를 클릭하면 Visual Studio에서 "\View\Dinners" 디렉토리 내에서 새 "Details.aspx" 보기 템플릿 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-236">When we click the "Add" button, Visual Studio will create a new "Details.aspx" view template file for us within our "\Views\Dinners" directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

<span data-ttu-id="1b4c0-237">또한 코드 편집기 내에서 새로운 "Details.aspx" 보기 템플릿을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-237">It will also open up our new "Details.aspx" view template within the code-editor.</span></span> <span data-ttu-id="1b4c0-238">Dinner 모델을 기반으로 하는 세부 정보 보기의 초기 스캐폴드 구현을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-238">It will contain an initial scaffold implementation of a details view based on a Dinner model.</span></span> <span data-ttu-id="1b4c0-239">스캐폴딩 엔진은 .NET 리플렉션을 사용하여 전달된 클래스에 노출된 공용 속성을 살펴보고 찾은 각 유형에 따라 적절한 콘텐츠를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-239">The scaffolding engine uses .NET reflection to look at the public properties exposed on the class passed it, and will add appropriate content based on each type it finds:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

<span data-ttu-id="1b4c0-240">*"/Dinners/Details/1" URL을* 요청하여 브라우저에서 이 "세부 정보" 스캐폴드 구현이 어떻게 보이는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-240">We can request the *"/Dinners/Details/1"* URL to see what this "details" scaffold implementation looks like in the browser.</span></span> <span data-ttu-id="1b4c0-241">이 URL을 사용하면 처음 만들 때 데이터베이스에 수동으로 추가한 dinner중 하나가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-241">Using this URL will display one of the dinners we manually added to our database when we first created it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

<span data-ttu-id="1b4c0-242">이를 통해 빠르게 실행되고 Details.aspx 뷰의 초기 구현을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-242">This gets us up and running quickly, and provides us with an initial implementation of our Details.aspx view.</span></span> <span data-ttu-id="1b4c0-243">그런 다음 UI를 사용자 정의하여 만족할 수 있도록 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-243">We can then go and tweak it to customize the UI to our satisfaction.</span></span>

<span data-ttu-id="1b4c0-244">Details.aspx 템플릿을 자세히 살펴보면 정적 HTML과 포함된 렌더링 코드가 포함되어 있음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-244">When we look at the Details.aspx template more closely, we'll find that it contains static HTML as well as embedded rendering code.</span></span> <span data-ttu-id="1b4c0-245">&lt;%&gt; % 코드 너겟은 뷰 템플릿이 렌더링 &lt;될&gt; 때 코드를 실행하고 %= % 코드 너겟은 그 안에 포함 된 코드를 실행한 다음 결과를 템플릿의 출력 스트림으로 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-245">&lt;% %&gt; code nuggets execute code when the view template renders, and &lt;%= %&gt; code nuggets execute the code contained within them and then render the result to the output stream of the template.</span></span>

<span data-ttu-id="1b4c0-246">강력한 형식의 "모델" 속성을 사용하여 컨트롤러에서 전달된 "Dinner" 모델 개체에 액세스하는 코드를 뷰 내에서 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-246">We can write code within our View that accesses the "Dinner" model object that was passed from our controller using a strongly-typed "Model" property.</span></span> <span data-ttu-id="1b4c0-247">Visual Studio는 편집기 내에서 이 "모델" 속성에 액세스할 때 전체 코드 인텔리센스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-247">Visual Studio provides us with full code-intellisense when accessing this "Model" property within the editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

<span data-ttu-id="1b4c0-248">최종 세부 정보 보기 템플릿의 소스가 다음과 같이 보이도록 몇 가지 사항을 조정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-248">Let's make some tweaks so that the source for our final Details view template looks like below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

<span data-ttu-id="1b4c0-249">*"저녁 식사/세부 정보/1"* URL에 다시 액세스하면 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-249">When we access the *"/Dinners/Details/1"* URL again it will now render like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a><span data-ttu-id="1b4c0-250">"인덱스" 보기 템플릿 구현</span><span class="sxs-lookup"><span data-stu-id="1b4c0-250">Implementing the "Index" View Template</span></span>

<span data-ttu-id="1b4c0-251">이제 곧 저녁 식사의 목록을 생성하는 "인덱스"보기 템플릿을 구현해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-251">Let's now implement the "Index" view template – which will generate a listing of upcoming Dinners.</span></span> <span data-ttu-id="1b4c0-252">이렇게 하려면 텍스트 커서를 색인 작업 메서드 내에 배치한 다음 마우스 오른쪽 단추를 클릭하고 "보기 추가" 메뉴 명령(또는 Ctrl-M, Ctrl-V 를 누름)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-252">To-do this we'll position our text cursor within the Index action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V).</span></span>

<span data-ttu-id="1b4c0-253">"보기 추가" 대화 상자 내에서 "색인"이라는 보기 템플릿을 유지하고 "강력한 형식의 보기 만들기" 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-253">Within the "Add View" dialog we'll keep the view template named "Index" and select the "Create a strongly-typed view" checkbox.</span></span> <span data-ttu-id="1b4c0-254">이번에는 자동으로 "목록" 보기 템플릿을 생성 하고 "NerdDinner.Models.Dinner"를 선택 하여 모델 유형이 뷰에 전달됨("목록" 스캐폴드을 만드는 것으로 표시했기 때문에 추가 보기 대화 상자가 컨트롤러에서 뷰로 Dinner 개체 시퀀스를 전달하고 있다고 가정합니다).</span><span class="sxs-lookup"><span data-stu-id="1b4c0-254">This time we will choose to automatically generate a "List" view template, and select "NerdDinner.Models.Dinner" as the model type passed to the view (which because we have indicated we are creating a "List" scaffold will cause the Add View dialog to assume we are passing a sequence of Dinner objects from our Controller to the View):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

<span data-ttu-id="1b4c0-255">"추가" 단추를 클릭하면 Visual Studio에서 "\View\Dinners" 디렉토리 내에서 새 "Index.aspx" 보기 템플릿 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-255">When we click the "Add" button, Visual Studio will create a new "Index.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="1b4c0-256">뷰에 전달하는 Dinners의 HTML 테이블 목록을 제공하는 초기 구현을 "스캐폴드"합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-256">It will "scaffold" an initial implementation within it that provides an HTML table listing of the Dinners we pass to the view.</span></span>

<span data-ttu-id="1b4c0-257">우리가 응용 프로그램을 실행하고 *"/ 저녁 식사 / "URL에* 액세스 하면 다음과 같은 저녁 식사의 우리의 목록을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-257">When we run the application and access the *"/Dinners/"* URL it will render our list of dinners like so:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

<span data-ttu-id="1b4c0-258">위의 테이블 솔루션은 Dinner 데이터의 그리드와 같은 레이아웃을 제공합니다 .</span><span class="sxs-lookup"><span data-stu-id="1b4c0-258">The table solution above gives us a grid-like layout of our Dinner data – which isn't quite what we want for our consumer facing Dinner listing.</span></span> <span data-ttu-id="1b4c0-259">Index.aspx 뷰 템플릿을 업데이트하고 수정하여 더 적은 수의 데이터 &lt;&gt; 열을 나열하고 ul 요소를 사용하여 아래 코드를 사용하여 테이블 대신 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-259">We can update the Index.aspx view template and modify it to list fewer columns of data, and use a &lt;ul&gt; element to render them instead of a table using the code below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

<span data-ttu-id="1b4c0-260">우리는 우리가 우리의 모델에서 각 저녁 식사를 통해 루프로 위의 foreach 문 내에서 "var"키워드를 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-260">We are using the "var" keyword within the above foreach statement as we loop over each dinner in our Model.</span></span> <span data-ttu-id="1b4c0-261">C# 3.0에 익숙하지 않은 사람들은 "var"을 사용하면 dinner 개체가 늦게 바인딩된 것을 의미한다고 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-261">Those unfamiliar with C# 3.0 might think that using "var" means that the dinner object is late-bound.</span></span> <span data-ttu-id="1b4c0-262">대신 컴파일러가 강력하게 입력된 "Model" 속성("IEnumerable&lt;Dinner")에&gt;대해 형식 추론을 사용하고 로컬 "Dinner" 변수를 Dinner 유형으로 컴파일한다는 의미이며, 이는 코드 블록 내에서 전체 intellisense 및 컴파일 타임 검사를 받을 수 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-262">It instead means that the compiler is using type-inference against the strongly typed "Model" property (which is of type "IEnumerable&lt;Dinner&gt;") and compiling the local "dinner" variable as a Dinner type – which means we get full intellisense and compile-time checking for it within code blocks:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

<span data-ttu-id="1b4c0-263">브라우저의 */Dinners* URL에서 새로 고침을 누르면 업데이트된 보기가 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-263">When we hit refresh on the */Dinners* URL in our browser our updated view now looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

<span data-ttu-id="1b4c0-264">이것은 더 나은 찾고 – 하지만 완전히 거기 아직.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-264">This is looking better – but isn't entirely there yet.</span></span> <span data-ttu-id="1b4c0-265">마지막 단계는 최종 사용자가 목록에서 개별 저녁 식사를 클릭하고 자세한 내용을 볼 수 있도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-265">Our last step is to enable end-users to click individual Dinners in the list and see details about them.</span></span> <span data-ttu-id="1b4c0-266">DinnersController에서 세부 정보 작업 메서드에 연결 하는 HTML 하이퍼링크 요소를 렌더링 하 여이 구현 거 야.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-266">We'll implement this by rendering HTML hyperlink elements that link to the Details action method on our DinnersController.</span></span>

<span data-ttu-id="1b4c0-267">두 가지 방법 중 하나로 인덱스 보기 내에서 이러한 하이퍼링크를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-267">We can generate these hyperlinks within our Index view in one of two ways.</span></span> <span data-ttu-id="1b4c0-268">첫 &lt;번째는 HTML&gt; 요소 내에 &lt;&gt; &lt;&gt; % % 블록을 포함하는 아래와 같은 요소를 수동으로 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-268">The first is to manually create HTML &lt;a&gt; elements like below, where we embed &lt;% %&gt; blocks within the &lt;a&gt; HTML element:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

<span data-ttu-id="1b4c0-269">우리가 사용할 수있는 또 다른 방법은 프로그래밍 방식으로 HTML을 &lt;만드는 것을 지원하는 ASP.NET MVC 내에서 내장 된 "Html.ActionLink()"도우미 방법을 활용하는 것입니다 컨트롤러의 다른 작업 방법에 링크하는&gt; 요소 :</span><span class="sxs-lookup"><span data-stu-id="1b4c0-269">An alternative approach we can use is to take advantage of the built-in "Html.ActionLink()" helper method within ASP.NET MVC that supports programmatically creating an HTML &lt;a&gt; element that links to another action method on a Controller:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

<span data-ttu-id="1b4c0-270">Html.ActionLink() 도우미 메서드의 첫 번째 매개 변수는 표시 할 링크 텍스트 (이 경우 저녁 식사의 제목), 두 번째 매개 변수는 링크를 생성 하려는 컨트롤러 작업 이름 (이 경우 Details 메서드), 세 번째 매개 변수는 작업에 보낼 매개 변수 집합 (속성 이름/값을 가진 익명 유형으로 구현).</span><span class="sxs-lookup"><span data-stu-id="1b4c0-270">The first parameter to the Html.ActionLink() helper method is the link-text to display (in this case the title of the dinner), the second parameter is the Controller action name we want to generate the link to (in this case the Details method), and the third parameter is a set of parameters to send to the action (implemented as an anonymous type with property name/values).</span></span> <span data-ttu-id="1b4c0-271">이 경우 연결하려는 dinner의 "id" 매개 변수를 지정하고 ASP.NET MVC의 기본 URL 라우팅 규칙이 "{Controller}/{Action}/{id}"이기 때문에 Html.ActionLink() 도우미 메서드는 다음 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-271">In this case we are specifying the "id" parameter of the dinner we want to link to, and because the default URL routing rule in ASP.NET MVC is "{Controller}/{Action}/{id}" the Html.ActionLink() helper method will generate the following output:</span></span>

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

<span data-ttu-id="1b4c0-272">Index.aspx 보기의 경우 Html.ActionLink() 도우미 메서드 방법을 사용하고 목록의 각 저녁 식사가 적절한 세부 정보 URL에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-272">For our Index.aspx view we'll use the Html.ActionLink() helper method approach and have each dinner in the list link to the appropriate details URL:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

<span data-ttu-id="1b4c0-273">그리고 지금 우리가 */Dinners URL을* 칠 때 우리의 저녁 식사 목록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-273">And now when we hit the */Dinners* URL our dinner list looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

<span data-ttu-id="1b4c0-274">목록에서 Dinners중 일부를 클릭하면 해당 에 대한 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-274">When we click any of the Dinners in the list we'll navigate to see details about it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a><span data-ttu-id="1b4c0-275">규칙 기반 이름 지정 및 \View 디렉터리 구조</span><span class="sxs-lookup"><span data-stu-id="1b4c0-275">Convention-based naming and the \Views directory structure</span></span>

<span data-ttu-id="1b4c0-276">기본적으로 MVC 응용 프로그램에서 ASP.NET 보기 템플릿을 확인할 때 규칙 기반 디렉터리 이름 지정 구조를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-276">ASP.NET MVC applications by default use a convention-based directory naming structure when resolving view templates.</span></span> <span data-ttu-id="1b4c0-277">따라서 개발자는 Controller 클래스 내에서 뷰를 참조할 때 위치 경로를 완전히 한정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-277">This allows developers to avoid having to fully-qualify a location path when referencing views from within a Controller class.</span></span> <span data-ttu-id="1b4c0-278">기본적으로 ASP.NET MVC는 응용 프로그램 아래의 \*\View\[ControllerName]\* 디렉터리 내에서 뷰 템플릿 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-278">By default ASP.NET MVC will look for the view template file within the \*\Views\[ControllerName]\* directory underneath the application.</span></span>

<span data-ttu-id="1b4c0-279">예를 들어 DinnersController 클래스에서 작업했습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-279">For example, we've been working on the DinnersController class – which explicitly references three view templates: "Index", "Details" and "NotFound".</span></span> <span data-ttu-id="1b4c0-280">ASP.NET MVC는 기본적으로 응용 프로그램 루트 디렉터리 아래의 *\View\Dinners* 디렉터리 에서 이러한 보기를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-280">ASP.NET MVC will by default look for these views within the *\Views\Dinners* directory underneath our application root directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

<span data-ttu-id="1b4c0-281">프로젝트 내에 현재 세 개의 컨트롤러 클래스가 있는 방법(DinnersController, HomeController 및 AccountController - 프로젝트를 만들 때 마지막 두 개가 기본적으로 추가됨) 및 \Views 디렉터리 내에 세 개의 하위 디렉터리(각 컨트롤러에 대해 하나씩)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-281">Notice above how there are currently three controller classes within the project (DinnersController, HomeController and AccountController – the last two were added by default when we created the project), and there are three sub-directories (one for each controller) within the \Views directory.</span></span>

<span data-ttu-id="1b4c0-282">홈 및 계정 컨트롤러에서 참조하는 뷰는 각 *\View\Home* 및 *\View\Account* 디렉터리에서 보기 템플릿을 자동으로 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-282">Views referenced from the Home and Accounts controllers will automatically resolve their view templates from the respective *\Views\Home* and *\Views\Account* directories.</span></span> <span data-ttu-id="1b4c0-283">*\Views\Shared* 하위 디렉터리에서는 응용 프로그램 내의 여러 컨트롤러에서 다시 사용되는 뷰 템플릿을 저장하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-283">The *\Views\Shared* sub-directory provides a way to store view templates that are re-used across multiple controllers within the application.</span></span> <span data-ttu-id="1b4c0-284">ASP.NET MVC가 뷰 템플릿을 확인하려고 하면 *먼저 \View\[Controller]* 특정 디렉터리 내에서 확인하고 뷰 템플릿을 찾을 수 없는 경우 *\Views\Shared* 디렉터리 내에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-284">When ASP.NET MVC attempts to resolve a view template, it will first check within the *\Views\[Controller]* specific directory, and if it can't find the view template there it will look within the *\Views\Shared* directory.</span></span>

<span data-ttu-id="1b4c0-285">개별 뷰 템플릿의 이름을 지정할 때 는 뷰 템플릿이 렌더링을 발생시킨 작업 메서드와 동일한 이름을 공유하도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-285">When it comes to naming individual view templates, the recommended guidance is to have the view template share the same name as the action method that caused it to render.</span></span> <span data-ttu-id="1b4c0-286">예를 들어 위의 "Index" 작업 메서드는 "Index" 뷰 보기를 사용하여 뷰 결과를 렌더링하고 "세부 정보" 작업 메서드는 "세부 정보" 뷰를 사용하여 결과를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-286">For example, above our "Index" action method is using the "Index" view to render the view result, and the "Details" action method is using the "Details" view to render its results.</span></span> <span data-ttu-id="1b4c0-287">이렇게 하면 각 작업과 연관된 템플릿을 쉽게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-287">This makes it easy to quickly see which template is associated with each action.</span></span>

<span data-ttu-id="1b4c0-288">개발자는 뷰 템플릿이 컨트롤러에서 호출되는 작업 메서드와 이름이 같을 때 뷰 템플릿 이름을 명시적으로 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-288">Developers do not need to explicitly specify the view template name when the view template has the same name as the action method being invoked on the controller.</span></span> <span data-ttu-id="1b4c0-289">대신 모델 개체를 "View()" 도우미 메서드에 전달할 수 있으며(뷰 이름을 지정하지 않고) ASP.NET MVC는 디스크에서 *\View\[\[ControllerName] ActionName]* 보기 템플릿을 사용하여 렌더링할 것을 자동으로 유추합니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-289">We can instead just pass the model object to the "View()" helper method (without specifying the view name), and ASP.NET MVC will automatically infer that we want to use the *\Views\[ControllerName]\[ActionName]* view template on disk to render it.</span></span>

<span data-ttu-id="1b4c0-290">이렇게 하면 컨트롤러 코드를 약간 정리하고 코드에서 이름을 두 번 복제하지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-290">This allows us to clean up our controller code a little, and avoid duplicating the name twice in our code:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

<span data-ttu-id="1b4c0-291">위의 코드는 사이트에 대한 멋진 Dinner 목록 / 세부 정보 환경을 구현하는 데 필요한 모든 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-291">The above code is all that is needed to implement a nice Dinner listing/details experience for the site.</span></span>

#### <a name="next-step"></a><span data-ttu-id="1b4c0-292">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1b4c0-292">Next Step</span></span>

<span data-ttu-id="1b4c0-293">우리는 지금 구축 된 좋은 저녁 식사 브라우징 경험을 가지고있다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-293">We now have a nice Dinner browsing experience built.</span></span>

<span data-ttu-id="1b4c0-294">이제 CRUD(데이터 양식 편집 지원 만들기, 읽기, 업데이트, 삭제)를 사용하도록 설정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1b4c0-294">Let's now enable CRUD (Create, Read, Update, Delete) data form editing support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1b4c0-295">[이전](build-a-model-with-business-rule-validations.md)
> [다음](provide-crud-create-read-update-delete-data-form-entry-support.md)</span><span class="sxs-lookup"><span data-stu-id="1b4c0-295">[Previous](build-a-model-with-business-rule-validations.md)
[Next](provide-crud-create-read-update-delete-data-form-entry-support.md)</span></span>
