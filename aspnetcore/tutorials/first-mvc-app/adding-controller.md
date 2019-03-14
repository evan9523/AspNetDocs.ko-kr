---
title: ASP.NET Core MVC 앱에 컨트롤러 추가
author: rick-anderson
description: 간단한 ASP.NET Core MVC 앱에 컨트롤러를 추가하는 방법을 배웁니다.
ms.author: riande
ms.date: 02/28/2017
uid: tutorials/first-mvc-app/adding-controller
ms.openlocfilehash: bbb7b06e2c9c63f44cb7f7a8ee63bffa1e316b3e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040720"
---
# <a name="add-a-controller-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="d799b-103">ASP.NET Core MVC 앱에 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="d799b-103">Add a controller to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="d799b-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="d799b-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="d799b-105">MVC( Model-View-Controller) 아키텍처 패턴은 다음 세 가지 주요 구성 요소로 앱을 구분합니다. **M**odel, **V**iew 및 **C**ontroller.</span><span class="sxs-lookup"><span data-stu-id="d799b-105">The Model-View-Controller (MVC) architectural pattern separates an app into three main components: **M**odel, **V**iew, and **C**ontroller.</span></span> <span data-ttu-id="d799b-106">MVC 패턴을 통해 기존 모놀리식 응용 프로그램보다 쉽게 테스트 가능하고 업데이트할 수 있는 앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-106">The MVC pattern helps you create apps that are more testable and easier to update than traditional monolithic apps.</span></span> <span data-ttu-id="d799b-107">MVC 기반 앱에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-107">MVC-based apps contain:</span></span>

* <span data-ttu-id="d799b-108">**M**odels: 앱의 데이터를 나타내는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-108">**M**odels: Classes that represent the data of the app.</span></span> <span data-ttu-id="d799b-109">모델 클래스는 유효성 검사 논리를 사용하여 해당 데이터의 비즈니스 규칙을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-109">The model classes use validation logic to enforce business rules for that data.</span></span> <span data-ttu-id="d799b-110">일반적으로 모델 개체는 모델 상태를 검색하고 데이터베이스에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-110">Typically, model objects retrieve and store model state in a database.</span></span> <span data-ttu-id="d799b-111">이 자습서에서 `Movie` 모델은 데이터베이스에서 영화 데이터를 검색하고 뷰로 제공하거나 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-111">In this tutorial, a `Movie` model retrieves movie data from a database, provides it to the view or updates it.</span></span> <span data-ttu-id="d799b-112">업데이트된 데이터는 데이터베이스에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-112">Updated data is written to a database.</span></span>

* <span data-ttu-id="d799b-113">**V**iews: 보기는 앱의 UI(사용자 인터페이스)를 표시하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-113">**V**iews: Views are the components that display the app's user interface (UI).</span></span> <span data-ttu-id="d799b-114">일반적으로 이 UI는 모델 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-114">Generally, this UI displays the model data.</span></span>

* <span data-ttu-id="d799b-115">**C**ontrollers: 브라우저 요청을 처리하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-115">**C**ontrollers: Classes that handle browser requests.</span></span> <span data-ttu-id="d799b-116">모델 데이터를 검색하고 응답을 반환하는 뷰 템플릿을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-116">They retrieve model data and call view templates that return a response.</span></span> <span data-ttu-id="d799b-117">MVC 앱에서 뷰는 정보만 표시합니다. 컨트롤러가 사용자 입력 및 상호 작용을 처리하고 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-117">In an MVC app, the view only displays information; the controller handles and responds to user input and interaction.</span></span> <span data-ttu-id="d799b-118">예를 들어 컨트롤러는 경로 데이터 및 쿼리 문자열 값을 처리하고 모델에 이러한 값을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-118">For example, the controller handles route data and query-string values, and passes these values to the model.</span></span> <span data-ttu-id="d799b-119">모델은 이러한 값을 사용하여 데이터베이스를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-119">The model might use these values to query the database.</span></span> <span data-ttu-id="d799b-120">예를 들어 `https://localhost:1234/Home/About`에는 `Home`(컨트롤러) 및 `About`(홈 컨트롤러에서 호출하는 작업 메서드)라는 경로 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-120">For example, `https://localhost:1234/Home/About` has route data of `Home` (the controller) and `About` (the action method to call on the home controller).</span></span> <span data-ttu-id="d799b-121">`https://localhost:1234/Movies/Edit/5`는 영화 컨트롤러를 사용하는 ID=5를 포함한 영화를 편집하는 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-121">`https://localhost:1234/Movies/Edit/5` is a request to edit the movie with ID=5 using the movie controller.</span></span> <span data-ttu-id="d799b-122">경로 데이터는 자습서의 뒷 부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-122">Route data is explained later in the tutorial.</span></span>

<span data-ttu-id="d799b-123">MVC 패턴을 통해 이러한 요소 간의 느슨한 결합을 제공하는 앱의 다양한 측면(입력 논리, 비즈니스 논리 및 UI 논리)을 구분하는 앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-123">The MVC pattern helps you create apps that separate the different aspects of the app (input logic, business logic, and UI logic), while providing a loose coupling between these elements.</span></span> <span data-ttu-id="d799b-124">패턴은 각 종류의 논리가 앱에 있어야 하는 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-124">The pattern specifies where each kind of logic should be located in the app.</span></span> <span data-ttu-id="d799b-125">UI 논리는 뷰에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-125">The UI logic belongs in the view.</span></span> <span data-ttu-id="d799b-126">입력 논리는 컨트롤러에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-126">Input logic belongs in the controller.</span></span> <span data-ttu-id="d799b-127">비즈니스 논리는 모델에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-127">Business logic belongs in the model.</span></span> <span data-ttu-id="d799b-128">이러한 분리를 통해 다른 코드에 영향을 주지 않고 한 번에 구현의 하나의 측면에서 작업할 수 있기 때문에 앱을 빌드하는 경우 복잡성을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-128">This separation helps you manage complexity when you build an app, because it enables you to work on one aspect of the implementation at a time without impacting the code of another.</span></span> <span data-ttu-id="d799b-129">예를 들어 비즈니스 논리 코드에 따라 달리지지 않고 뷰 코드에서 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-129">For example, you can work on the view code without depending on the business logic code.</span></span>

<span data-ttu-id="d799b-130">이 자습서 시리즈에서 이러한 개념을 설명하고 영화 앱을 빌드하기 위해 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-130">We cover these concepts in this tutorial series and show you how to use them to build a movie app.</span></span> <span data-ttu-id="d799b-131">MVC 프로젝트에는 *컨트롤러* 및 *뷰*에 대한 폴더가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-131">The MVC project contains folders for the *Controllers* and *Views*.</span></span>

## <a name="add-a-controller"></a><span data-ttu-id="d799b-132">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="d799b-132">Add a controller</span></span>

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="d799b-133">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d799b-133">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="d799b-134">**솔루션 탐색기**에서 \*\* 컨트롤러 > 추가 > 컨트롤러\*\*
  ![바로 가기 메뉴](adding-controller/_static/add_controller.png)를 오른쪽 단추로 클릭</span><span class="sxs-lookup"><span data-stu-id="d799b-134">In **Solution Explorer**, right-click **Controllers > Add > Controller**
![Contextual menu](adding-controller/_static/add_controller.png)</span></span>

* <span data-ttu-id="d799b-135">**스캐폴드 추가** 대화 상자에서 **MVC 컨트롤러 - 비어 있음**을 선택</span><span class="sxs-lookup"><span data-stu-id="d799b-135">In the **Add Scaffold** dialog box, select **MVC Controller - Empty**</span></span>

  ![MVC 컨트롤러 추가 및 이름 지정](adding-controller/_static/ac.png)

* <span data-ttu-id="d799b-137">**빈 MVC 컨트롤러 추가 대화 상자**에 **HelloWorldController**를 입력하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-137">In the **Add Empty MVC Controller dialog**, enter **HelloWorldController** and select **ADD**.</span></span>

<!-- Code -------------------------->
# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="d799b-138">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d799b-138">Visual Studio Code</span></span>](#tab/visual-studio-code)

<span data-ttu-id="d799b-139">**탐색기** 아이콘을 선택한 다음, **컨트롤러 > 새 파일**을 컨트롤 클릭(마우스 오른쪽 단추로 클릭)하고 새 파일의 이름을 *HelloWorldController.cs*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-139">Select the **EXPLORER** icon and then control-click (right-click) **Controllers > New File** and name the new file *HelloWorldController.cs*.</span></span>

  ![바로 가기 메뉴](~/tutorials/first-mvc-app-xplat/adding-controller/_static/new_file.png)

<!-- Mac -------------------------->
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="d799b-141">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="d799b-141">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

<span data-ttu-id="d799b-142">**솔루션 탐색기**에서 **컨트롤러 > 추가 > 새 파일**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-142">In **Solution Explorer**, right-click **Controllers > Add > New File**.</span></span>
<span data-ttu-id="d799b-143">![바로 가기 메뉴](~/tutorials/first-mvc-app-mac/adding-controller/_static/add_controller.png)</span><span class="sxs-lookup"><span data-stu-id="d799b-143">![Contextual menu](~/tutorials/first-mvc-app-mac/adding-controller/_static/add_controller.png)</span></span>

<span data-ttu-id="d799b-144">**ASP.NET Core** 및 **MVC 컨트롤러 클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-144">Select **ASP.NET Core** and **MVC Controller Class**.</span></span>

<span data-ttu-id="d799b-145">컨트롤러의 이름을 **HelloWorldController**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-145">Name the controller **HelloWorldController**.</span></span>

![MVC 컨트롤러 추가 및 이름 지정](~/tutorials/first-mvc-app-mac/adding-controller/_static/ac.png)

---
<!-- End of VS tabs -->

<span data-ttu-id="d799b-147">*Controllers/HelloWorldController.cs*의 내용을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-147">Replace the contents of *Controllers/HelloWorldController.cs* with the following:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/HelloWorldController.cs?name=snippet_1)]

<span data-ttu-id="d799b-148">컨트롤러의 모든 `public` 메서드는 HTTP 엔드포인트로 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-148">Every `public` method in a controller is callable as an HTTP endpoint.</span></span> <span data-ttu-id="d799b-149">위의 샘플에서 메서드는 모두 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-149">In the sample above, both methods return a string.</span></span> <span data-ttu-id="d799b-150">각 메서드 앞의 주석을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-150">Note the comments preceding each method.</span></span>

<span data-ttu-id="d799b-151">HTTP 엔드포인트는 웹 애플리케이션에서 대상으로 지정 가능한 URL(예: `https://localhost:5001/HelloWorld`)으로써 사용되는 프로토콜(`HTTPS`), 웹 서버(TCP 포트 포함)의 네트워크 위치(`localhost:5001`) 및 대상 URI `HelloWorld`을 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-151">An HTTP endpoint is a targetable URL in the web application, such as `https://localhost:5001/HelloWorld`, and combines the protocol used: `HTTPS`, the network location of the web server (including the TCP port): `localhost:5001` and the target URI `HelloWorld`.</span></span>

<span data-ttu-id="d799b-152">첫 번째 주석은 이 항목을 기본 URL에 `/HelloWorld/`를 추가하여 호출되는 [HTTP GET](https://www.w3schools.com/tags/ref_httpmethods.asp) 메서드라고 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-152">The first comment states this is an [HTTP GET](https://www.w3schools.com/tags/ref_httpmethods.asp) method that's invoked by appending `/HelloWorld/` to the base URL.</span></span> <span data-ttu-id="d799b-153">두 번째 주석은 URL에 `/HelloWorld/Welcome/`를 추가하여 호출되는 [HTTP GET](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) 메서드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-153">The second comment specifies an [HTTP GET](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) method that's invoked by appending `/HelloWorld/Welcome/` to the URL.</span></span> <span data-ttu-id="d799b-154">나중에 자습서에서 스캐폴딩 엔진은 데이터를 업데이트하는 `HTTP POST` 메서드를 생성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-154">Later on in the tutorial the scaffolding engine is used to generate `HTTP POST` methods which update data.</span></span>

<span data-ttu-id="d799b-155">디버그가 아닌 모드로 앱을 실행하고 주소 표시줄의 경로에 "HelloWorld"를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-155">Run the app in non-debug mode and append "HelloWorld" to the path in the address bar.</span></span> <span data-ttu-id="d799b-156">`Index` 메서드가 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-156">The `Index` method returns a string.</span></span>

![브라우저 창은 내 기본 작업입니다.라는 애플리케이션 응답을 표시합니다.](~/tutorials/first-mvc-app/adding-controller/_static/hell1.png)

<span data-ttu-id="d799b-158">MVC는 들어오는 URL에 따라 컨트롤러 클래스(및 그 안에 작업 메서드)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-158">MVC invokes controller classes (and the action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="d799b-159">MVC에서 사용하는 기본 [URL 라우팅 논리](xref:mvc/controllers/routing)는 다음과 같은 형식을 사용하여 호출할 코드를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-159">The default [URL routing logic](xref:mvc/controllers/routing) used by MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="d799b-160">라우팅 형식은 *Startup.cs* 파일의 `Configure` 메서드로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-160">The routing format is set in the `Configure` method in *Startup.cs* file.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?name=snippet_1&highlight=5)]

<!-- 
Add link to explain lambda.
Remove link for simplified tutorial.
-->

<span data-ttu-id="d799b-161">앱으로 이동하고 URL 세그먼트를 제공하지 않는 경우 "Home" 컨트롤러에 기본값으로 지정되고 위에 강조 표시된 템플릿 줄에 "Index" 메서드가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-161">When you browse to the app and don't supply any URL segments, it defaults to the "Home" controller and the "Index" method specified in the template line highlighted above.</span></span>

<span data-ttu-id="d799b-162">첫 번째 URL 세그먼트는 실행할 컨트롤러 클래스를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-162">The first URL segment determines the controller class to run.</span></span> <span data-ttu-id="d799b-163">따라서 `localhost:xxxx/HelloWorld`은 `HelloWorldController` 클래스에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-163">So `localhost:xxxx/HelloWorld` maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="d799b-164">URL 세그먼트의 두 번째 부분은 클래스에 대한 작업 메서드를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-164">The second part of the URL segment determines the action method on the class.</span></span> <span data-ttu-id="d799b-165">따라서 `localhost:xxxx/HelloWorld/Index`는 실행할 `HelloWorldController` 클래스의 `Index` 메서드를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-165">So `localhost:xxxx/HelloWorld/Index` would cause the `Index` method of the `HelloWorldController` class to run.</span></span> <span data-ttu-id="d799b-166">`localhost:xxxx/HelloWorld`로 이동하고 기본적으로 `Index` 메서드를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-166">Notice that you only had to browse to `localhost:xxxx/HelloWorld` and the `Index` method was called by default.</span></span> <span data-ttu-id="d799b-167">메서드 이름이 명시적으로 지정되지 않으면 `Index`가 컨트롤러에서 호출되는 기본 메서드이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-167">This is because `Index` is the default method that will be called on a controller if a method name isn't explicitly specified.</span></span> <span data-ttu-id="d799b-168">URL 세그먼트(`id`)의 세 번째 부분은 경로 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-168">The third part of the URL segment ( `id`) is for route data.</span></span> <span data-ttu-id="d799b-169">경로 데이터는 자습서의 뒷 부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-169">Route data is explained later in the tutorial.</span></span>

<span data-ttu-id="d799b-170">`https://localhost:xxxx/HelloWorld/Welcome`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-170">Browse to `https://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="d799b-171">`Welcome` 메서드가 실행되고 문자열 `This is the Welcome action method...`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-171">The `Welcome` method runs and returns the string `This is the Welcome action method...`.</span></span> <span data-ttu-id="d799b-172">이 URL의 경우 컨트롤러는 `HelloWorld`이고 `Welcome`은 작업 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-172">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="d799b-173">아직 URL의 `[Parameters]` 부분을 사용하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-173">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![브라우저 창은 시작 작업 메서드입니다.라는 애플리케이션 응답을 표시합니다.](~/tutorials/first-mvc-app/adding-controller/_static/welcome.png)

<span data-ttu-id="d799b-175">URL의 일부 매개 변수 정보를 컨트롤러에 전달하도록 코드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-175">Modify the code to pass some parameter information from the URL to the controller.</span></span> <span data-ttu-id="d799b-176">예를 들어, `/HelloWorld/Welcome?name=Rick&numtimes=4`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-176">For example, `/HelloWorld/Welcome?name=Rick&numtimes=4`.</span></span> <span data-ttu-id="d799b-177">`Welcome` 메서드가 다음 코드와 같이 두 개의 매개 변수를 포함하도록 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-177">Change the `Welcome` method to include two parameters as shown in the following code.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/HelloWorldController.cs?name=snippet_2)]

<span data-ttu-id="d799b-178">위의 코드는:</span><span class="sxs-lookup"><span data-stu-id="d799b-178">The preceding code:</span></span>

* <span data-ttu-id="d799b-179">C# 선택적 매개 변수 기능을 사용하여 `numTimes` 매개 변수에 대해 전달된 값이 없는 경우 해당 매개 변수의 기본값이 1임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-179">Uses the C# optional-parameter feature to indicate that the `numTimes` parameter defaults to 1 if no value is passed for that parameter.</span></span> <!-- remove for simplified -->
* <span data-ttu-id="d799b-180">`HtmlEncoder.Default.Encode`를 사용하여 악의적인 입력(예: JavaScript)에서 응용 프로그램을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-180">Uses`HtmlEncoder.Default.Encode` to protect the app from malicious input (namely JavaScript).</span></span>
* <span data-ttu-id="d799b-181">`$"Hello {name}, NumTimes is: {numTimes}"`에서 [보간된 문자열](/dotnet/articles/csharp/language-reference/keywords/interpolated-strings)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-181">Uses [Interpolated Strings](/dotnet/articles/csharp/language-reference/keywords/interpolated-strings) in `$"Hello {name}, NumTimes is: {numTimes}"`.</span></span> <!-- remove for simplified -->

<span data-ttu-id="d799b-182">앱을 실행하고 다음으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-182">Run the app and browse to:</span></span>

   `https://localhost:xxxx/HelloWorld/Welcome?name=Rick&numtimes=4`

<span data-ttu-id="d799b-183">(xxxx를 포트 번호로 바꿉니다.) URL에서 `name` 및 `numtimes`에 다른 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-183">(Replace xxxx with your port number.) You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="d799b-184">MVC [모델 바인딩](xref:mvc/models/model-binding) 시스템은 주소 표시줄의 쿼리 문자열에서 메서드의 매개 변수로 명명된 매개 변수를 자동으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-184">The MVC [model binding](xref:mvc/models/model-binding) system automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span> <span data-ttu-id="d799b-185">자세한 정보는 [모델 바인딩](xref:mvc/models/model-binding)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d799b-185">See [Model Binding](xref:mvc/models/model-binding) for more information.</span></span>

![Hello Rick, NumTimes의 애플리케이션 응답을 보여주는 브라우저 창은 다음과 같습니다. 4](~/tutorials/first-mvc-app/adding-controller/_static/rick4.png)

<span data-ttu-id="d799b-187">위의 이미지에서 URL 세그먼트(`Parameters`)를 사용하지 않고 `name` 및 `numTimes` 매개 변수가 [쿼리 문자열](https://wikipedia.org/wiki/Query_string)로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-187">In the image above, the URL segment (`Parameters`) isn't used, the `name` and `numTimes` parameters are passed as [query strings](https://wikipedia.org/wiki/Query_string).</span></span> <span data-ttu-id="d799b-188">위 URL에서 `?`(물음표)는 구분 기호이고 쿼리 문자열이 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-188">The `?` (question mark) in the above URL is a separator, and the query strings follow.</span></span> <span data-ttu-id="d799b-189">`&` 문자는 쿼리 문자열을 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-189">The `&` character separates query strings.</span></span>

<span data-ttu-id="d799b-190">`Welcome` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-190">Replace the `Welcome` method with the following code:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/HelloWorldController.cs?name=snippet_3)]

<span data-ttu-id="d799b-191">앱을 실행하고 `https://localhost:xxx/HelloWorld/Welcome/3?name=Rick` URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-191">Run the app and enter the following URL: `https://localhost:xxx/HelloWorld/Welcome/3?name=Rick`</span></span>

<span data-ttu-id="d799b-192">이번에 세 번째 URL 세그먼트는 `id` 경로 매개 변수와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-192">This time the third URL segment matched the route parameter `id`.</span></span> <span data-ttu-id="d799b-193">`Welcome` 메서드는 `MapRoute` 메서드에서 URL 템플릿과 일치하는 `id` 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-193">The `Welcome` method contains a parameter `id` that matched the URL template in the `MapRoute` method.</span></span> <span data-ttu-id="d799b-194">후행 `?`(`id?`에 위치)는 `id` 매개 변수가 선택 사항임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-194">The trailing `?` (in `id?`) indicates the `id` parameter is optional.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?name=snippet_1&highlight=5)]

<span data-ttu-id="d799b-195">이러한 예제에서 컨트롤러는 MVC의 "VC" 부분을 사용했습니다. 즉, 보기 및 컨트롤러 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-195">In these examples the controller has been doing the "VC" portion of MVC - that is, the view and controller work.</span></span> <span data-ttu-id="d799b-196">컨트롤러는 HTML을 직접 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-196">The controller is returning HTML directly.</span></span> <span data-ttu-id="d799b-197">일반적으로 코드 및 유지 관리가 매우 복잡해지므로 컨트롤러에서 HTML을 직접 반환하지 않으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-197">Generally you don't want controllers returning HTML directly, since that becomes very cumbersome to code and maintain.</span></span> <span data-ttu-id="d799b-198">대신 일반적으로 별도의 Razor 뷰 템플릿 파일을 사용하여 HTML 응답을 생성하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-198">Instead you typically use a separate Razor view template file to help generate the HTML response.</span></span> <span data-ttu-id="d799b-199">다음 자습서에서 해당 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d799b-199">You do that in the next tutorial.</span></span>


> [!div class="step-by-step"]
> <span data-ttu-id="d799b-200">[이전](start-mvc.md)
> [다음](adding-view.md)</span><span class="sxs-lookup"><span data-stu-id="d799b-200">[Previous](start-mvc.md)
[Next](adding-view.md)</span></span>
