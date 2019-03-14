---
title: ASP.NET Core MVC에서 뷰
author: ardalis
description: ASP.NET Core MVC에서 뷰가 앱의 데이터 프레젠테이션과 사용자 상호 작용을 처리하는 방식에 대해 알아봅니다.
ms.author: riande
ms.date: 12/12/2017
uid: mvc/views/overview
ms.openlocfilehash: 6c5b4d7b89ac07a85b5aad626e37855de98064eb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036100"
---
# <a name="views-in-aspnet-core-mvc"></a><span data-ttu-id="04ec4-103">ASP.NET Core MVC에서 뷰</span><span class="sxs-lookup"><span data-stu-id="04ec4-103">Views in ASP.NET Core MVC</span></span>

<span data-ttu-id="04ec4-104">작성자: [Steve Smith](https://ardalis.com/) 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="04ec4-104">By [Steve Smith](https://ardalis.com/) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="04ec4-105">이 문서에서는 ASP.NET Core MVC 애플리케이션에서 사용된 뷰에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-105">This document explains views used in ASP.NET Core MVC applications.</span></span> <span data-ttu-id="04ec4-106">Razor 페이지에 대한 자세한 내용은 [Razor 페이지 소개](xref:razor-pages/index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04ec4-106">For information on Razor Pages, see [Introduction to Razor Pages](xref:razor-pages/index).</span></span>

<span data-ttu-id="04ec4-107">MVC(Model-View-Controller) 패턴에서 *보기*는 앱의 데이터 프레젠테이션과 사용자 상호 작용을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-107">In the Model-View-Controller (MVC) pattern, the *view* handles the app's data presentation and user interaction.</span></span> <span data-ttu-id="04ec4-108">뷰는 [Razor 태그](xref:mvc/views/razor)가 포함된 HTML 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-108">A view is an HTML template with embedded [Razor markup](xref:mvc/views/razor).</span></span> <span data-ttu-id="04ec4-109">Razor 태그는 클라이언트에 전송된 웹 페이지를 생성하기 위해 HTML과 상호 작용하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-109">Razor markup is code that interacts with HTML markup to produce a webpage that's sent to the client.</span></span>

<span data-ttu-id="04ec4-110">ASP.NET Core MVC에서 뷰는 Razor 태그에서 [C# 프로그래밍 언어](/dotnet/csharp/)를 사용하는 *.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-110">In ASP.NET Core MVC, views are *.cshtml* files that use the [C# programming language](/dotnet/csharp/) in Razor markup.</span></span> <span data-ttu-id="04ec4-111">일반적으로 뷰 파일은 앱의 [컨트롤러](xref:mvc/controllers/actions) 각각에 대해 명명된 폴더로 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-111">Usually, view files are grouped into folders named for each of the app's [controllers](xref:mvc/controllers/actions).</span></span> <span data-ttu-id="04ec4-112">이 폴더는 앱의 루트에서 *Views* 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-112">The folders are stored in a *Views* folder at the root of the app:</span></span>

![Visual Studio의 솔루션 탐색기에서 Views 폴더는 About.cshtml, Contact.cshtml 및 Index.cshtml 파일을 표시하도록 Home 폴더가 열린 상태로 열려 있습니다.](overview/_static/views_solution_explorer.png)

<span data-ttu-id="04ec4-114">*Home* 컨트롤러는 *Views* 폴더 내에 *Home* 폴더로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-114">The *Home* controller is represented by a *Home* folder inside the *Views* folder.</span></span> <span data-ttu-id="04ec4-115">*Home* 폴더에는 *About*, *Contact* 및 *Index*(홈페이지)에 대한 뷰가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-115">The *Home* folder contains the views for the *About*, *Contact*, and *Index* (homepage) webpages.</span></span> <span data-ttu-id="04ec4-116">사용자가 이러한 세 웹 페이지 중 하나를 요청하면 *Home* 컨트롤러의 컨트롤러 작업에 따라 웹 페이지를 작성하고 사용자에게 반환하는 데 사용되는 세 가지 뷰가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-116">When a user requests one of these three webpages, controller actions in the *Home* controller determine which of the three views is used to build and return a webpage to the user.</span></span>

<span data-ttu-id="04ec4-117">[레이아웃](xref:mvc/views/layout)을 사용하여 일관된 웹 페이지 섹션을 제공하고 코드 반복을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-117">Use [layouts](xref:mvc/views/layout) to provide consistent webpage sections and reduce code repetition.</span></span> <span data-ttu-id="04ec4-118">레이아웃에는 보통 머리글, 탐색 및 메뉴 요소 및 바닥글이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-118">Layouts often contain the header, navigation and menu elements, and the footer.</span></span> <span data-ttu-id="04ec4-119">머리글 및 바닥글에는 일반적으로 다양한 메타데이터 요소에 대한 상용구 태그와 스크립트 및 스타일 자산에 대한 링크가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-119">The header and footer usually contain boilerplate markup for many metadata elements and links to script and style assets.</span></span> <span data-ttu-id="04ec4-120">레이아웃을 통해 뷰에서 이 상용구 태그를 피할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-120">Layouts help you avoid this boilerplate markup in your views.</span></span>

<span data-ttu-id="04ec4-121">[부분 뷰](xref:mvc/views/partial)는 재사용 가능한 뷰 부분을 관리하여 코드 중복을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-121">[Partial views](xref:mvc/views/partial) reduce code duplication by managing reusable parts of views.</span></span> <span data-ttu-id="04ec4-122">예를 들어, 부분 뷰는 여러 뷰에 나타나는 블로그 웹 사이트의 작성자 약력에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-122">For example, a partial view is useful for an author biography on a blog website that appears in several views.</span></span> <span data-ttu-id="04ec4-123">작성자 약력은 일반적인 뷰 콘텐츠이며 웹 페이지의 콘텐츠를 생성하기 위해 코드를 실행하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-123">An author biography is ordinary view content and doesn't require code to execute in order to produce the content for the webpage.</span></span> <span data-ttu-id="04ec4-124">작성자 약력 콘텐츠는 모델 바인딩만으로 뷰에 제공되므로 이러한 콘텐츠 유형에는 부분 뷰를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-124">Author biography content is available to the view by model binding alone, so using a partial view for this type of content is ideal.</span></span>

<span data-ttu-id="04ec4-125">[뷰 구성 요소](xref:mvc/views/view-components)는 반복 코드를 줄일 수 있다는 점에서 부분 뷰와 유사하지만 웹 페이지를 렌더링하기 위해 코드를 서버에서 실행해야 하는 뷰 콘텐츠에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-125">[View components](xref:mvc/views/view-components) are similar to partial views in that they allow you to reduce repetitive code, but they're appropriate for view content that requires code to run on the server in order to render the webpage.</span></span> <span data-ttu-id="04ec4-126">뷰 구성 요소는 렌더링된 콘텐츠가 웹 사이트 장바구니와 같이 데이터베이스 상호 작용을 필요로 할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-126">View components are useful when the rendered content requires database interaction, such as for a website shopping cart.</span></span> <span data-ttu-id="04ec4-127">뷰 구성 요소는 웹 페이지 출력을 생성하기 위한 모델 바인딩에만 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-127">View components aren't limited to model binding in order to produce webpage output.</span></span>

## <a name="benefits-of-using-views"></a><span data-ttu-id="04ec4-128">뷰 사용 시 이점</span><span class="sxs-lookup"><span data-stu-id="04ec4-128">Benefits of using views</span></span>

<span data-ttu-id="04ec4-129">뷰를 통해 사용자 인터페이스 태그를 앱의 다른 부분과 구분하여 MVC 앱 내에서 [문제의 분리](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#separation-of-concerns)를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-129">Views help to establish [separation of concerns](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#separation-of-concerns) within an MVC app by separating the user interface markup from other parts of the app.</span></span> <span data-ttu-id="04ec4-130">SoC 디자인을 따르면 앱을 모듈화할 수 있으며 다음과 같은 여러 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-130">Following SoC design makes your app modular, which provides several benefits:</span></span>

* <span data-ttu-id="04ec4-131">앱이 더 잘 구성되어 있기 때문에 유지 관리가 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-131">The app is easier to maintain because it's better organized.</span></span> <span data-ttu-id="04ec4-132">뷰는 일반적으로 앱 기능별로 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-132">Views are generally grouped by app feature.</span></span> <span data-ttu-id="04ec4-133">이렇게 하면 기능을 사용할 때 관련 뷰를 보다 쉽게 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-133">This makes it easier to find related views when working on a feature.</span></span>
* <span data-ttu-id="04ec4-134">앱의 일부는 느슨하게 결합되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-134">The parts of the app are loosely coupled.</span></span> <span data-ttu-id="04ec4-135">비즈니스 논리 및 데이터 액세스 구성 요소와 별도로 앱의 뷰를 작성하고 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-135">You can build and update the app's views separately from the business logic and data access components.</span></span> <span data-ttu-id="04ec4-136">앱의 다른 부분을 업데이트하지 않고도 앱의 뷰를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-136">You can modify the views of the app without necessarily having to update other parts of the app.</span></span>
* <span data-ttu-id="04ec4-137">뷰는 별도의 단위이므로 앱의 사용자 인터페이스 부분을 보다 쉽게 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-137">It's easier to test the user interface parts of the app because the views are separate units.</span></span>
* <span data-ttu-id="04ec4-138">구성이 개선되어 사용자 인터페이스 섹션을 실수로 반복하는 일이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-138">Due to better organization, it's less likely that you'll accidentally repeat sections of the user interface.</span></span>

## <a name="creating-a-view"></a><span data-ttu-id="04ec4-139">뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="04ec4-139">Creating a view</span></span>

<span data-ttu-id="04ec4-140">컨트롤러에 관한 뷰는 *Views/[ControllerName]* 폴더에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-140">Views that are specific to a controller are created in the *Views/[ControllerName]* folder.</span></span> <span data-ttu-id="04ec4-141">컨트롤러 간에 공유되는 뷰는 *Views/Shared* 폴더에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-141">Views that are shared among controllers are placed in the *Views/Shared* folder.</span></span> <span data-ttu-id="04ec4-142">뷰를 만들려면 새 파일을 추가하고 연결된 컨트롤러 작업과 동일한 이름을 *.cshtml* 파일 확장명으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-142">To create a view, add a new file and give it the same name as its associated controller action with the *.cshtml* file extension.</span></span> <span data-ttu-id="04ec4-143">*Home* 컨트롤러에서 *About* 작업에 해당하는 뷰를 만들려면 *Views/Home* 폴더에 *About.cshtml* 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-143">To create a view that corresponds with the *About* action in the *Home* controller, create an *About.cshtml* file in the *Views/Home* folder:</span></span>

[!code-cshtml[](../../common/samples/WebApplication1/Views/Home/About.cshtml)]

<span data-ttu-id="04ec4-144">*Razor* 태그는 `@` 기호로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-144">*Razor* markup starts with the `@` symbol.</span></span> <span data-ttu-id="04ec4-145">C# 코드를 중괄호(`{ ... }`)로 설정된 [Razor 코드 블록](xref:mvc/views/razor#razor-code-blocks) 내에 배치하여 C# 문을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-145">Run C# statements by placing C# code within [Razor code blocks](xref:mvc/views/razor#razor-code-blocks) set off by curly braces (`{ ... }`).</span></span> <span data-ttu-id="04ec4-146">예를 들어 위에 표시된 `ViewData["Title"]`에 "About"이 할당된 부분을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04ec4-146">For example, see the assignment of "About" to `ViewData["Title"]` shown above.</span></span> <span data-ttu-id="04ec4-147">`@` 기호로 값을 참조하기만 하면 HTML 내에 값을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-147">You can display values within HTML by simply referencing the value with the `@` symbol.</span></span> <span data-ttu-id="04ec4-148">위의 `<h2>` 및 `<h3>` 요소의 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04ec4-148">See the contents of the `<h2>` and `<h3>` elements above.</span></span>

<span data-ttu-id="04ec4-149">위에 표시된 뷰 콘텐츠는 사용자에게 렌더링되는 전체 웹 페이지의 일부분일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-149">The view content shown above is only part of the entire webpage that's rendered to the user.</span></span> <span data-ttu-id="04ec4-150">나머지 페이지 레이아웃과 뷰의 다른 일반적인 측면은 다른 뷰 파일에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-150">The rest of the page's layout and other common aspects of the view are specified in other view files.</span></span> <span data-ttu-id="04ec4-151">자세한 내용은 [레이아웃 항목](xref:mvc/views/layout)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04ec4-151">To learn more, see the [Layout topic](xref:mvc/views/layout).</span></span>

## <a name="how-controllers-specify-views"></a><span data-ttu-id="04ec4-152">컨트롤러에서 뷰를 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="04ec4-152">How controllers specify views</span></span>

<span data-ttu-id="04ec4-153">일반적으로 뷰는 [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult) 형식인 [ViewResult](/dotnet/api/microsoft.aspnetcore.mvc.viewresult)로 작업에서 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-153">Views are typically returned from actions as a [ViewResult](/dotnet/api/microsoft.aspnetcore.mvc.viewresult), which is a type of [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult).</span></span> <span data-ttu-id="04ec4-154">사용자 작업 메서드로 `ViewResult`를 직접 만들고 반환할 수 있지만 일반적으로 이렇게 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-154">Your action method can create and return a `ViewResult` directly, but that isn't commonly done.</span></span> <span data-ttu-id="04ec4-155">대부분의 컨트롤러는 [Controller](/dotnet/api/microsoft.aspnetcore.mvc.controller)를 상속하므로 `View` 도우미 메서드를 사용하여 `ViewResult`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-155">Since most controllers inherit from [Controller](/dotnet/api/microsoft.aspnetcore.mvc.controller), you simply use the `View` helper method to return the `ViewResult`:</span></span>

<span data-ttu-id="04ec4-156">*HomeController.cs*</span><span class="sxs-lookup"><span data-stu-id="04ec4-156">*HomeController.cs*</span></span>

[!code-csharp[](../../common/samples/WebApplication1/Controllers/HomeController.cs?highlight=5&range=16-21)]

<span data-ttu-id="04ec4-157">이 작업이 반환되면 *About.cshtml* 뷰가 다음 웹 페이지로 렌더링된 마지막 섹션에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-157">When this action returns, the *About.cshtml* view shown in the last section is rendered as the following webpage:</span></span>

![Microsoft Edge 브라우저에서 렌더링된 About 페이지](overview/_static/about-page.png)

<span data-ttu-id="04ec4-159">`View` 도우미 메서드는 몇 가지 오버로드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-159">The `View` helper method has several overloads.</span></span> <span data-ttu-id="04ec4-160">필요에 따라 다음을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-160">You can optionally specify:</span></span>

* <span data-ttu-id="04ec4-161">반환할 명시적 보기:</span><span class="sxs-lookup"><span data-stu-id="04ec4-161">An explicit view to return:</span></span>

  ```csharp
  return View("Orders");
  ```
* <span data-ttu-id="04ec4-162">뷰에 전달할 [모델](xref:mvc/models/model-binding):</span><span class="sxs-lookup"><span data-stu-id="04ec4-162">A [model](xref:mvc/models/model-binding) to pass to the view:</span></span>

  ```csharp
  return View(Orders);
  ```
* <span data-ttu-id="04ec4-163">뷰 및 모델 모두:</span><span class="sxs-lookup"><span data-stu-id="04ec4-163">Both a view and a model:</span></span>

  ```csharp
  return View("Orders", Orders);
  ```

### <a name="view-discovery"></a><span data-ttu-id="04ec4-164">뷰 검색</span><span class="sxs-lookup"><span data-stu-id="04ec4-164">View discovery</span></span>

<span data-ttu-id="04ec4-165">작업에서 뷰를 반환하면 *뷰 검색*이라는 프로세스가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-165">When an action returns a view, a process called *view discovery* takes place.</span></span> <span data-ttu-id="04ec4-166">이 프로세스는 뷰 이름에 따라 어떤 뷰 파일을 사용할지가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-166">This process determines which view file is used based on the view name.</span></span> 

<span data-ttu-id="04ec4-167">`View` 메서드(`return View();`)의 기본 동작은 호출된 작업 메서드와 같은 이름으로 뷰를 반환하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-167">The default behavior of the `View` method (`return View();`) is to return a view with the same name as the action method from which it's called.</span></span> <span data-ttu-id="04ec4-168">예를 들어 컨트롤러의 *About* `ActionResult` 메서드 이름은 *About.cshtml*이라는 이름의 뷰 파일을 검색하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-168">For example, the *About* `ActionResult` method name of the controller is used to search for a view file named *About.cshtml*.</span></span> <span data-ttu-id="04ec4-169">먼저, 런타임은 뷰에 대한 *Views/[ControllerName]* 폴더를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-169">First, the runtime looks in the *Views/[ControllerName]* folder for the view.</span></span> <span data-ttu-id="04ec4-170">이 위치에서 일치하는 뷰를 찾지 못하면 뷰에 대한 *Shared* 폴더를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-170">If it doesn't find a matching view there, it searches the *Shared* folder for the view.</span></span>

<span data-ttu-id="04ec4-171">`return View();`로 암시적으로 `ViewResult`를 반환하거나 `return View("<ViewName>");`로 명시적으로 뷰 이름을 `View` 메서드에 전달하는 것은 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-171">It doesn't matter if you implicitly return the `ViewResult` with `return View();` or explicitly pass the view name to the `View` method with `return View("<ViewName>");`.</span></span> <span data-ttu-id="04ec4-172">두 경우 모두, 뷰 검색 시 일치하는 뷰 파일을 다음 순서로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-172">In both cases, view discovery searches for a matching view file in this order:</span></span>

   1. <span data-ttu-id="04ec4-173">*Views/\[ControllerName]/\[ViewName].cshtml*</span><span class="sxs-lookup"><span data-stu-id="04ec4-173">*Views/\[ControllerName]/\[ViewName].cshtml*</span></span>
   1. <span data-ttu-id="04ec4-174">*Views/Shared/\[ViewName].cshtml*</span><span class="sxs-lookup"><span data-stu-id="04ec4-174">*Views/Shared/\[ViewName].cshtml*</span></span>

<span data-ttu-id="04ec4-175">뷰 이름 대신 뷰 파일 경로를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-175">A view file path can be provided instead of a view name.</span></span> <span data-ttu-id="04ec4-176">앱 루트에서 시작하는 절대 경로를 사용하는 경우(필요에 따라 "/" 또는 "~ /"로 시작) *.cshtml* 확장명을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-176">If using an absolute path starting at the app root (optionally starting with "/" or "~/"), the *.cshtml* extension must be specified:</span></span>

```csharp
return View("Views/Home/About.cshtml");
```

<span data-ttu-id="04ec4-177">상재 경로를 사용하여 *.cshtml* 확장명 없이 다른 디렉터리에 뷰를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-177">You can also use a relative path to specify views in different directories without the *.cshtml* extension.</span></span> <span data-ttu-id="04ec4-178">`HomeController` 내에서 상대 경로로 *Manage* 뷰의 *Index* 뷰를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-178">Inside the `HomeController`, you can return the *Index* view of your *Manage* views with a relative path:</span></span>

```csharp
return View("../Manage/Index");
```

<span data-ttu-id="04ec4-179">마찬가지로, "./" 접두사로 현재 컨트롤러 관련 디렉터리를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-179">Similarly, you can indicate the current controller-specific directory with the "./" prefix:</span></span>

```csharp
return View("./About");
```

<span data-ttu-id="04ec4-180">[부분 뷰](xref:mvc/views/partial) 및 [뷰 구성 요소](xref:mvc/views/view-components)는 비슷하지만 다른 검색 메커니즘을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-180">[Partial views](xref:mvc/views/partial) and [view components](xref:mvc/views/view-components) use similar (but not identical) discovery mechanisms.</span></span>

<span data-ttu-id="04ec4-181">사용자 지정 [IViewLocationExpander](/dotnet/api/microsoft.aspnetcore.mvc.razor.iviewlocationexpander)를 사용하여 뷰가 앱 내에 어떻게 위치하는지에 대한 기본 규칙을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-181">You can customize the default convention for how views are located within the app by using a custom [IViewLocationExpander](/dotnet/api/microsoft.aspnetcore.mvc.razor.iviewlocationexpander).</span></span>

<span data-ttu-id="04ec4-182">뷰 검색은 파일 이름으로 뷰 파일을 찾는 방식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-182">View discovery relies on finding view files by file name.</span></span> <span data-ttu-id="04ec4-183">기본 파일 시스템이 대/소문자를 구분하는 경우 뷰 이름도 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-183">If the underlying file system is case sensitive, view names are probably case sensitive.</span></span> <span data-ttu-id="04ec4-184">운영 체제 간 호환성을 위해, 컨트롤러 및 작업 이름, 관련 뷰 폴더 및 파일 이름 간에 대/소문자를 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-184">For compatibility across operating systems, match case between controller and action names and associated view folders and file names.</span></span> <span data-ttu-id="04ec4-185">대/소문자 구분 파일 시스템으로 작업하는 동안 파일 뷰를 찾을 수 없는 오류가 발생하면, 요청된 뷰 파일과 실제 뷰 파일 이름 간에 대/소문자가 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-185">If you encounter an error that a view file can't be found while working with a case-sensitive file system, confirm that the casing matches between the requested view file and the actual view file name.</span></span>

<span data-ttu-id="04ec4-186">유지 관리 및 명확성을 위해 컨트롤러, 작업 및 뷰 간의 관계를 반영하도록 뷰에 대한 파일 구조를 구성하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-186">Follow the best practice of organizing the file structure for your views to reflect the relationships among controllers, actions, and views for maintainability and clarity.</span></span>

## <a name="passing-data-to-views"></a><span data-ttu-id="04ec4-187">뷰에 데이터 전달</span><span class="sxs-lookup"><span data-stu-id="04ec4-187">Passing data to views</span></span>

<span data-ttu-id="04ec4-188">여러 가지 방법으로 뷰에 데이터를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-188">Pass data to views using several approaches:</span></span>

* <span data-ttu-id="04ec4-189">강력한 형식의 데이터: viewmodel</span><span class="sxs-lookup"><span data-stu-id="04ec4-189">Strongly typed data: viewmodel</span></span>
* <span data-ttu-id="04ec4-190">약한 형식의 데이터</span><span class="sxs-lookup"><span data-stu-id="04ec4-190">Weakly typed data</span></span>
  * <span data-ttu-id="04ec4-191">`ViewData` (`ViewDataAttribute`)</span><span class="sxs-lookup"><span data-stu-id="04ec4-191">`ViewData` (`ViewDataAttribute`)</span></span>
  * `ViewBag`

### <a name="strongly-typed-data-viewmodel"></a><span data-ttu-id="04ec4-192">강력한 형식의 데이터(viewmodel)</span><span class="sxs-lookup"><span data-stu-id="04ec4-192">Strongly typed data (viewmodel)</span></span>

<span data-ttu-id="04ec4-193">가장 강력한 방법은 뷰에서 [모델](xref:mvc/models/model-binding) 형식을 지정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-193">The most robust approach is to specify a [model](xref:mvc/models/model-binding) type in the view.</span></span> <span data-ttu-id="04ec4-194">이 모델은 일반적으로 *viewmodel*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-194">This model is commonly referred to as a *viewmodel*.</span></span> <span data-ttu-id="04ec4-195">viewmodel 형식의 인스턴스를 작업의 뷰에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-195">You pass an instance of the viewmodel type to the view from the action.</span></span>

<span data-ttu-id="04ec4-196">viewmodel을 사용하여 뷰에 데이터를 전달하면 뷰에서 *강력한* 형식 검사를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-196">Using a viewmodel to pass data to a view allows the view to take advantage of *strong* type checking.</span></span> <span data-ttu-id="04ec4-197">*강력한 형식화*(또는 *강력한 형식의*)는 모든 변수 및 상수가 명시적으로 정의된 형식(예: `string`, `int` 또는 `DateTime`)을 포함함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-197">*Strong typing* (or *strongly typed*) means that every variable and constant has an explicitly defined type (for example, `string`, `int`, or `DateTime`).</span></span> <span data-ttu-id="04ec4-198">뷰에 사용된 형식의 유효성 검사는 컴파일 시간에 검사됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-198">The validity of types used in a view is checked at compile time.</span></span>

<span data-ttu-id="04ec4-199">[Visual Studio](https://www.visualstudio.com/vs/) 및 [Visual Studio Code](https://code.visualstudio.com/)는 [IntelliSense](/visualstudio/ide/using-intellisense)라는 기능을 사용하여 강력한 형식의 클래스 멤버를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-199">[Visual Studio](https://www.visualstudio.com/vs/) and [Visual Studio Code](https://code.visualstudio.com/) list strongly typed class members using a feature called [IntelliSense](/visualstudio/ide/using-intellisense).</span></span> <span data-ttu-id="04ec4-200">viewmodel 속성을 보려는 경우 viewmodel에 대한 변수 이름과 마침표(`.`)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-200">When you want to see the properties of a viewmodel, type the variable name for the viewmodel followed by a period (`.`).</span></span> <span data-ttu-id="04ec4-201">이렇게 하면 오류를 줄이면서 보다 빠르게 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-201">This helps you write code faster with fewer errors.</span></span>

<span data-ttu-id="04ec4-202">`@model` 지시문을 사용하여 모델을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-202">Specify a model using the `@model` directive.</span></span> <span data-ttu-id="04ec4-203">`@Model`로 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-203">Use the model with `@Model`:</span></span>

```cshtml
@model WebApplication1.ViewModels.Address

<h2>Contact</h2>
<address>
    @Model.Street<br>
    @Model.City, @Model.State @Model.PostalCode<br>
    <abbr title="Phone">P:</abbr> 425.555.0100
</address>
```

<span data-ttu-id="04ec4-204">모델을 뷰에 제공하기 위해 컨트롤러는 이를 매개 변수로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-204">To provide the model to the view, the controller passes it as a parameter:</span></span>

```csharp
public IActionResult Contact()
{
    ViewData["Message"] = "Your contact page.";

    var viewModel = new Address()
    {
        Name = "Microsoft",
        Street = "One Microsoft Way",
        City = "Redmond",
        State = "WA",
        PostalCode = "98052-6399"
    };

    return View(viewModel);
}
```

<span data-ttu-id="04ec4-205">뷰에 제공할 수 있는 모델 유형에 대한 제한은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-205">There are no restrictions on the model types that you can provide to a view.</span></span> <span data-ttu-id="04ec4-206">동작(메서드)가 거의 또는 전혀 정의되지 않은 POCO(Plain Old CLR Object) viewmodel을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-206">We recommend using Plain Old CLR Object (POCO) viewmodels with little or no behavior (methods) defined.</span></span> <span data-ttu-id="04ec4-207">일반적으로 viewmodel 클래스는 앱의 루트에서 *Models* 폴더 또는 별도의 *ViewModels* 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-207">Usually, viewmodel classes are either stored in the *Models* folder or a separate *ViewModels* folder at the root of the app.</span></span> <span data-ttu-id="04ec4-208">위의 예제에 사용된 *Address* viewmodel은 *Address.cs*라는 파일에 저장된 POCO viewmodel입니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-208">The *Address* viewmodel used in the example above is a POCO viewmodel stored in a file named *Address.cs*:</span></span>

```csharp
namespace WebApplication1.ViewModels
{
    public class Address
    {
        public string Name { get; set; }
        public string Street { get; set; }
        public string City { get; set; }
        public string State { get; set; }
        public string PostalCode { get; set; }
    }
}
```

<span data-ttu-id="04ec4-209">viewmodel 형식 및 비즈니스 모델 형식 모두에 같은 클래스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-209">Nothing prevents you from using the same classes for both your viewmodel types and your business model types.</span></span> <span data-ttu-id="04ec4-210">그러나 별도의 모델을 사용하면 뷰를 통해 앱의 비즈니스 논리 및 데이터 액세스 부분을 독립적으로 구분하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-210">However, using separate models allows your views to vary independently from the business logic and data access parts of your app.</span></span> <span data-ttu-id="04ec4-211">모델과 viewmodel을 분리하면 모델에서 사용자에 의해 앱에 전송된 데이터에 대해 [모델 바인딩](xref:mvc/models/model-binding) 및 [유효성 검사](xref:mvc/models/validation)를 사용할 때 보안상 이점도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-211">Separation of models and viewmodels also offers security benefits when models use [model binding](xref:mvc/models/model-binding) and [validation](xref:mvc/models/validation) for data sent to the app by the user.</span></span>

<a name="VD_VB"></a>

### <a name="weakly-typed-data-viewdata-viewdata-attribute-and-viewbag"></a><span data-ttu-id="04ec4-212">약한 형식의 데이터(ViewData, ViewData 특성 및 ViewBag)</span><span class="sxs-lookup"><span data-stu-id="04ec4-212">Weakly typed data (ViewData, ViewData attribute, and ViewBag)</span></span>

<span data-ttu-id="04ec4-213">`ViewBag` *은 Razor 페이지에서 사용할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="04ec4-213">`ViewBag` *isn't available in Razor Pages.*</span></span>

<span data-ttu-id="04ec4-214">강력한 형식의 뷰 외에도, 뷰는 *약한 형식*(*느슨한 형식*이라고도 함) 데이터 컬렉션에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-214">In addition to strongly typed views, views have access to a *weakly typed* (also called *loosely typed*) collection of data.</span></span> <span data-ttu-id="04ec4-215">강력한 형식과 달리, *약한 형식*(또는 *느슨한 형식*)은 사용 중인 데이터 형식을 명시적으로 선언하지 않는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-215">Unlike strong types, *weak types* (or *loose types*) means that you don't explicitly declare the type of data you're using.</span></span> <span data-ttu-id="04ec4-216">컨트롤러 및 뷰 간에 적은 양의 데이터를 전달하기 위해 약한 형식의 데이터 컬렉션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-216">You can use the collection of weakly typed data for passing small amounts of data in and out of controllers and views.</span></span>

| <span data-ttu-id="04ec4-217">다음 사이에 데이터 전달 ...</span><span class="sxs-lookup"><span data-stu-id="04ec4-217">Passing data between a ...</span></span>                        | <span data-ttu-id="04ec4-218">예제</span><span class="sxs-lookup"><span data-stu-id="04ec4-218">Example</span></span>                                                                        |
| ------------------------------------------------- | ------------------------------------------------------------------------------ |
| <span data-ttu-id="04ec4-219">컨트롤러 및 뷰</span><span class="sxs-lookup"><span data-stu-id="04ec4-219">Controller and a view</span></span>                             | <span data-ttu-id="04ec4-220">드롭다운 목록을 데이터로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-220">Populating a dropdown list with data.</span></span>                                          |
| <span data-ttu-id="04ec4-221">뷰 및 [레이아웃 뷰](xref:mvc/views/layout)</span><span class="sxs-lookup"><span data-stu-id="04ec4-221">View and a [layout view](xref:mvc/views/layout)</span></span>   | <span data-ttu-id="04ec4-222">뷰 파일의 레이아웃 뷰에서 **\<title>** 요소 콘텐츠를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-222">Setting the **\<title>** element content in the layout view from a view file.</span></span>  |
| <span data-ttu-id="04ec4-223">[부분 뷰](xref:mvc/views/partial) 및 뷰</span><span class="sxs-lookup"><span data-stu-id="04ec4-223">[Partial view](xref:mvc/views/partial) and a view</span></span> | <span data-ttu-id="04ec4-224">사용자가 요청한 웹 페이지에 따라 데이터를 표시하는 위젯입니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-224">A widget that displays data based on the webpage that the user requested.</span></span>      |

<span data-ttu-id="04ec4-225">이 컬렉션은 컨트롤러 및 뷰의 `ViewData` 또는 `ViewBag` 속성을 통해 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-225">This collection can be referenced through either the `ViewData` or `ViewBag` properties on controllers and views.</span></span> <span data-ttu-id="04ec4-226">`ViewData` 속성은 약한 형식 개체의 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-226">The `ViewData` property is a dictionary of weakly typed objects.</span></span> <span data-ttu-id="04ec4-227">`ViewBag` 속성은 기본 `ViewData` 컬렉션에 대해 동적 속성을 제공하는 `ViewData` 주변의 래퍼입니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-227">The `ViewBag` property is a wrapper around `ViewData` that provides dynamic properties for the underlying `ViewData` collection.</span></span>

<span data-ttu-id="04ec4-228">`ViewData` 및 `ViewBag`은 런타임에 동적으로 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-228">`ViewData` and `ViewBag` are dynamically resolved at runtime.</span></span> <span data-ttu-id="04ec4-229">컴파일 시간 형식 검사를 제공하지 않으므로 일반적으로 둘 다 viewmodel을 사용하는 것보다 오류가 발생하기 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-229">Since they don't offer compile-time type checking, both are generally more error-prone than using a viewmodel.</span></span> <span data-ttu-id="04ec4-230">이러한 이유로, 일부 개발자는 `ViewData` 및 `ViewBag`을 최소한으로 사용하거나 아예 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-230">For that reason, some developers prefer to minimally or never use `ViewData` and `ViewBag`.</span></span>

<a name="VD"></a>

<span data-ttu-id="04ec4-231">**ViewData**</span><span class="sxs-lookup"><span data-stu-id="04ec4-231">**ViewData**</span></span>

<span data-ttu-id="04ec4-232">`ViewData`는 `string` 키를 통해 액세스된 [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-232">`ViewData` is a [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) object accessed through `string` keys.</span></span> <span data-ttu-id="04ec4-233">문자열 데이터는 캐스트할 필요 없이 직접 저장 및 사용할 수 있지만 추출할 때는 다른 `ViewData` 개체 값을 특정 형식으로 캐스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-233">String data can be stored and used directly without the need for a cast, but you must cast other `ViewData` object values to specific types when you extract them.</span></span> <span data-ttu-id="04ec4-234">`ViewData`를 사용하여 컨트롤러에서 뷰로, [부분 뷰](xref:mvc/views/partial) 및 [레이아웃](xref:mvc/views/layout)을 포함한 뷰 내에서 데이터를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-234">You can use `ViewData` to pass data from controllers to views and within views, including [partial views](xref:mvc/views/partial) and [layouts](xref:mvc/views/layout).</span></span>

<span data-ttu-id="04ec4-235">다음은 작업에서 `ViewData`를 사용하여 인사말 및 주소에 대한 값을 설정하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-235">The following is an example that sets values for a greeting and an address using `ViewData` in an action:</span></span>

```csharp
public IActionResult SomeAction()
{
    ViewData["Greeting"] = "Hello";
    ViewData["Address"]  = new Address()
    {
        Name = "Steve",
        Street = "123 Main St",
        City = "Hudson",
        State = "OH",
        PostalCode = "44236"
    };

    return View();
}
```

<span data-ttu-id="04ec4-236">뷰에서 데이터 사용:</span><span class="sxs-lookup"><span data-stu-id="04ec4-236">Work with the data in a view:</span></span>

```cshtml
@{
    // Since Address isn't a string, it requires a cast.
    var address = ViewData["Address"] as Address;
}

@ViewData["Greeting"] World!

<address>
    @address.Name<br>
    @address.Street<br>
    @address.City, @address.State @address.PostalCode
</address>
```

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="04ec4-237">**ViewData 특성**</span><span class="sxs-lookup"><span data-stu-id="04ec4-237">**ViewData attribute**</span></span>

<span data-ttu-id="04ec4-238">[ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary)를 사용하는 또 다른 방법은 [ViewDataAttribute](/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute)입니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-238">Another approach that uses the [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) is [ViewDataAttribute](/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute).</span></span> <span data-ttu-id="04ec4-239">`[ViewData]`로 데코레이팅된 컨트롤러 또는 Razor 페이지 모델의 속성은 값을 사전에서 저장하고 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-239">Properties on controllers or Razor Page models decorated with `[ViewData]` have their values stored and loaded from the dictionary.</span></span>

<span data-ttu-id="04ec4-240">다음 예제에서 홈 컨트롤러에는 `[ViewData]`로 데코레이팅된 `Title` 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-240">In the following example, the Home controller contains a `Title` property decorated with `[ViewData]`.</span></span> <span data-ttu-id="04ec4-241">`About` 메서드는 정보 보기에 대한 제목을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-241">The `About` method sets the title for the About view:</span></span>

```csharp
public class HomeController : Controller
{
    [ViewData]
    public string Title { get; set; }

    public IActionResult About()
    {
        Title = "About Us";
        ViewData["Message"] = "Your application description page.";

        return View();
    }
}
```

<span data-ttu-id="04ec4-242">정보 보기에서 모델 속성인 `Title` 속성에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-242">In the About view, access the `Title` property as a model property:</span></span>

```cshtml
<h1>@Model.Title</h1>
```

<span data-ttu-id="04ec4-243">레이아웃에서는 ViewData 사전으로부터 이 제목을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-243">In the layout, the title is read from the ViewData dictionary:</span></span>

```cshtml
<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ViewData["Title"] - WebApplication</title>
    ...
```

::: moniker-end

<span data-ttu-id="04ec4-244">**ViewBag**</span><span class="sxs-lookup"><span data-stu-id="04ec4-244">**ViewBag**</span></span>

<span data-ttu-id="04ec4-245">`ViewBag` *은 Razor 페이지에서 사용할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="04ec4-245">`ViewBag` *isn't available in Razor Pages.*</span></span>

<span data-ttu-id="04ec4-246">`ViewBag`은 `ViewData`에 저장된 개체에 대한 동적 액세스를 제공하는 [DynamicViewData](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-246">`ViewBag` is a [DynamicViewData](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata) object that provides dynamic access to the objects stored in `ViewData`.</span></span> <span data-ttu-id="04ec4-247">캐스팅이 필요하지 않으므로 `ViewBag`이 작업하기 더 편리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-247">`ViewBag` can be more convenient to work with, since it doesn't require casting.</span></span> <span data-ttu-id="04ec4-248">다음 예제에서는 `ViewData`를 사용할 때와 동일한 결과로 `ViewBag`을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-248">The following example shows how to use `ViewBag` with the same result as using `ViewData` above:</span></span>

```csharp
public IActionResult SomeAction()
{
    ViewBag.Greeting = "Hello";
    ViewBag.Address  = new Address()
    {
        Name = "Steve",
        Street = "123 Main St",
        City = "Hudson",
        State = "OH",
        PostalCode = "44236"
    };

    return View();
}
```

```cshtml
@ViewBag.Greeting World!

<address>
    @ViewBag.Address.Name<br>
    @ViewBag.Address.Street<br>
    @ViewBag.Address.City, @ViewBag.Address.State @ViewBag.Address.PostalCode
</address>
```

<span data-ttu-id="04ec4-249">**ViewData 및 ViewBag을 동시에 사용**</span><span class="sxs-lookup"><span data-stu-id="04ec4-249">**Using ViewData and ViewBag simultaneously**</span></span>

<span data-ttu-id="04ec4-250">`ViewBag` *은 Razor 페이지에서 사용할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="04ec4-250">`ViewBag` *isn't available in Razor Pages.*</span></span>

<span data-ttu-id="04ec4-251">`ViewData` 및 `ViewBag`은 동일한 기본 `ViewData` 컬렉션을 사용하므로 `ViewData` 및 `ViewBag`을 모두 사용하고 값을 읽고 쓸 때 이들을 혼합 및 일치시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-251">Since `ViewData` and `ViewBag` refer to the same underlying `ViewData` collection, you can use both `ViewData` and `ViewBag` and mix and match between them when reading and writing values.</span></span>

<span data-ttu-id="04ec4-252">*About.cshtml* 뷰의 맨 위에서 `ViewBag`을 사용하여 제목을, `ViewData`를 사용하여 설명을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-252">Set the title using `ViewBag` and the description using `ViewData` at the top of an *About.cshtml* view:</span></span>

```cshtml
@{
    Layout = "/Views/Shared/_Layout.cshtml";
    ViewBag.Title = "About Contoso";
    ViewData["Description"] = "Let us tell you about Contoso's philosophy and mission.";
}
```

<span data-ttu-id="04ec4-253">속성을 읽지만 `ViewData` 및 `ViewBag`을 반대로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-253">Read the properties but reverse the use of `ViewData` and `ViewBag`.</span></span> <span data-ttu-id="04ec4-254">*_Layout.cshtml* 파일에서 `ViewData`를 사용하여 제목을 가져오고 `ViewBag`을 사용하여 설명을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-254">In the *_Layout.cshtml* file, obtain the title using `ViewData` and obtain the description using `ViewBag`:</span></span>

```cshtml
<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ViewData["Title"]</title>
    <meta name="description" content="@ViewBag.Description">
    ...
```

<span data-ttu-id="04ec4-255">문자열에는 `ViewData`에 대한 캐스트가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-255">Remember that strings don't require a cast for `ViewData`.</span></span> <span data-ttu-id="04ec4-256">캐스팅없이 `@ViewData["Title"]`를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-256">You can use `@ViewData["Title"]` without casting.</span></span>

<span data-ttu-id="04ec4-257">`ViewData`와 `ViewBag`을 동시에 사용하면 속성을 읽고 쓰는 작업을 혼합 및 일치시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-257">Using both `ViewData` and `ViewBag` at the same time works, as does mixing and matching reading and writing the properties.</span></span> <span data-ttu-id="04ec4-258">다음 태그가 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-258">The following markup is rendered:</span></span>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>About Contoso</title>
    <meta name="description" content="Let us tell you about Contoso's philosophy and mission.">
    ...
```

<span data-ttu-id="04ec4-259">**ViewData 및 ViewBag 간 차이를 표시하는 요약**</span><span class="sxs-lookup"><span data-stu-id="04ec4-259">**Summary of the differences between ViewData and ViewBag**</span></span>

 <span data-ttu-id="04ec4-260">`ViewBag`은 Razor 페이지에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-260">`ViewBag` isn't available in the Razor Pages.</span></span>

* `ViewData`
  * <span data-ttu-id="04ec4-261">[ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary)에서 파생되므로 유용한 `ContainsKey`, `Add`, `Remove` 및 `Clear`와 같은 사전 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-261">Derives from [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary), so it has dictionary properties that can be useful, such as `ContainsKey`, `Add`, `Remove`, and `Clear`.</span></span>
  * <span data-ttu-id="04ec4-262">사전의 키는 문자열이므로 공백을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-262">Keys in the dictionary are strings, so whitespace is allowed.</span></span> <span data-ttu-id="04ec4-263">예: `ViewData["Some Key With Whitespace"]`</span><span class="sxs-lookup"><span data-stu-id="04ec4-263">Example: `ViewData["Some Key With Whitespace"]`</span></span>
  * <span data-ttu-id="04ec4-264">`string` 이외의 모든 형식을 뷰에서 `ViewData`를 사용하도록 캐스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-264">Any type other than a `string` must be cast in the view to use `ViewData`.</span></span>
* `ViewBag`
  * <span data-ttu-id="04ec4-265">[DynamicViewData](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata)에서 파생되므로 점 표기법(`@ViewBag.SomeKey = <value or object>`)을 사용하여 동적 속성을 생성할 수 있으며 캐스팅이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-265">Derives from [DynamicViewData](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata), so it allows the creation of dynamic properties using dot notation (`@ViewBag.SomeKey = <value or object>`), and no casting is required.</span></span> <span data-ttu-id="04ec4-266">`ViewBag` 구문을 사용하면 신속하게 컨트롤러와 뷰를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-266">The syntax of `ViewBag` makes it quicker to add to controllers and views.</span></span>
  * <span data-ttu-id="04ec4-267">간단하게 Null 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-267">Simpler to check for null values.</span></span> <span data-ttu-id="04ec4-268">예: `@ViewBag.Person?.Name`</span><span class="sxs-lookup"><span data-stu-id="04ec4-268">Example: `@ViewBag.Person?.Name`</span></span>

<span data-ttu-id="04ec4-269">**ViewData 또는 ViewBag을 사용하는 경우**</span><span class="sxs-lookup"><span data-stu-id="04ec4-269">**When to use ViewData or ViewBag**</span></span>

<span data-ttu-id="04ec4-270">`ViewData` 및 `ViewBag` 둘 다 컨트롤러 및 뷰 간에 적은 양의 데이터를 전달하는 데 유효한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-270">Both `ViewData` and `ViewBag` are equally valid approaches for passing small amounts of data among controllers and views.</span></span> <span data-ttu-id="04ec4-271">기본 설정에 따라 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-271">The choice of which one to use is based on preference.</span></span> <span data-ttu-id="04ec4-272">`ViewData` 및 `ViewBag` 개체를 혼합 및 일치시키실 수 있지만, 일관되게 사용된 한 가지 방법으로 코드를 보다 쉽게 읽고 유지 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-272">You can mix and match `ViewData` and `ViewBag` objects, however, the code is easier to read and maintain with one approach used consistently.</span></span> <span data-ttu-id="04ec4-273">두 가지 방법 모두 런타임에 동적으로 확인되므로 런타임 오류가 발생하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-273">Both approaches are dynamically resolved at runtime and thus prone to causing runtime errors.</span></span> <span data-ttu-id="04ec4-274">일부 개발 팀은 이 방법을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-274">Some development teams avoid them.</span></span>

### <a name="dynamic-views"></a><span data-ttu-id="04ec4-275">동적 뷰</span><span class="sxs-lookup"><span data-stu-id="04ec4-275">Dynamic views</span></span>

<span data-ttu-id="04ec4-276">`@model`을 사용하여 모델 형식을 선언하지는 않지만 전달된 모델 인스턴스가 있는 뷰(예: `return View(Address);`)는 인스턴스의 속성을 동적으로 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-276">Views that don't declare a model type using `@model` but that have a model instance passed to them (for example, `return View(Address);`) can reference the instance's properties dynamically:</span></span>

```cshtml
<address>
    @Model.Street<br>
    @Model.City, @Model.State @Model.PostalCode<br>
    <abbr title="Phone">P:</abbr> 425.555.0100
</address>
```

<span data-ttu-id="04ec4-277">이 기능은 유연성을 제공하지만 컴파일 보호 또는 IntelliSense는 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-277">This feature offers flexibility but doesn't offer compilation protection or IntelliSense.</span></span> <span data-ttu-id="04ec4-278">속성이 존재하지 않으면 런타임 시 웹 페이지 생성에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-278">If the property doesn't exist, webpage generation fails at runtime.</span></span>

## <a name="more-view-features"></a><span data-ttu-id="04ec4-279">추가 뷰 기능</span><span class="sxs-lookup"><span data-stu-id="04ec4-279">More view features</span></span>

<span data-ttu-id="04ec4-280">[태그 도우미](xref:mvc/views/tag-helpers/intro)를 통해 기존 HTML 태그에 서버 쪽 동작을 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-280">[Tag Helpers](xref:mvc/views/tag-helpers/intro) make it easy to add server-side behavior to existing HTML tags.</span></span> <span data-ttu-id="04ec4-281">태그 도우미를 사용하면 뷰 내에서 사용자 지정 코드 또는 도우미를 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-281">Using Tag Helpers avoids the need to write custom code or helpers within your views.</span></span> <span data-ttu-id="04ec4-282">태그 도우미는 HTML 요소에 특성으로 적용되고 처리할 수 없는 편집기에 의해 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-282">Tag helpers are applied as attributes to HTML elements and are ignored by editors that can't process them.</span></span> <span data-ttu-id="04ec4-283">따라서 다양한 도구로 뷰 태그를 편집 및 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-283">This allows you to edit and render view markup in a variety of tools.</span></span>

<span data-ttu-id="04ec4-284">많은 기본 제공 HTML 도우미를 통해 사용자 지정 HTML 태그를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-284">Generating custom HTML markup can be achieved with many built-in HTML Helpers.</span></span> <span data-ttu-id="04ec4-285">더 복잡한 사용자 인터페이스 논리는 [뷰 구성 요소](xref:mvc/views/view-components)로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-285">More complex user interface logic can be handled by [View Components](xref:mvc/views/view-components).</span></span> <span data-ttu-id="04ec4-286">뷰 구성 요소는 컨트롤러 및 뷰에서 제공하는 동일한 SoC를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-286">View components provide the same SoC that controllers and views offer.</span></span> <span data-ttu-id="04ec4-287">일반적인 사용자 인터페이스 요소에서 사용하는 데이터를 처리하는 작업 및 뷰에 대한 필요성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-287">They can eliminate the need for actions and views that deal with data used by common user interface elements.</span></span>

<span data-ttu-id="04ec4-288">ASP.NET Core의 다른 많은 요소와 마찬가지로 뷰는 [종속성 주입](xref:fundamentals/dependency-injection)을 지원하며, [뷰에 서비스를 주입](xref:mvc/views/dependency-injection)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ec4-288">Like many other aspects of ASP.NET Core, views support [dependency injection](xref:fundamentals/dependency-injection), allowing services to be [injected into views](xref:mvc/views/dependency-injection).</span></span>
