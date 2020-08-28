---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: 컨트롤러에서 모델의 데이터에 액세스 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 26d1a66cbc022664af14e4dfe4c4b4892d409b95
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045171"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="6fc3d-102">컨트롤러에서 모델의 데이터에 액세스</span><span class="sxs-lookup"><span data-stu-id="6fc3d-102">Accessing Your Model's Data from a Controller</span></span>

<span data-ttu-id="6fc3d-103">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="6fc3d-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="6fc3d-104">이 섹션에서는 새 클래스를 만들고 `MoviesController` 영화 데이터를 검색 하 고 보기 템플릿을 사용 하 여 브라우저에 표시 하는 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-104">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="6fc3d-105">다음 단계로 이동 하기 전에 **응용 프로그램을 빌드합니다** .</span><span class="sxs-lookup"><span data-stu-id="6fc3d-105">**Build the application** before going on to the next step.</span></span> <span data-ttu-id="6fc3d-106">응용 프로그램을 빌드하지 않으면 컨트롤러를 추가 하는 동안 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-106">If you don't build the application, you'll get an error adding a controller.</span></span>

<span data-ttu-id="6fc3d-107">솔루션 탐색기에서 *Controllers* 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **추가**, **컨트롤러**를 차례로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-107">In Solution Explorer, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="6fc3d-108">**스 캐 폴드 추가** 대화 상자에서 **Entity Framework를 사용 하 여 MVC 5 컨트롤러 (뷰 포함**)를 클릭 한 다음 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-108">In the **Add Scaffold** dialog box, click **MVC 5 Controller with views, using Entity Framework**, and then click **Add**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- <span data-ttu-id="6fc3d-109">모델 클래스에 대해 **동영상 (MvcMovie. 모델)** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-109">Select **Movie (MvcMovie.Models)** for the Model class.</span></span>
- <span data-ttu-id="6fc3d-110">데이터 컨텍스트 클래스에 대해 **MovieDBContext (MvcMovie. 모델)** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-110">Select **MovieDBContext (MvcMovie.Models)** for the Data context class.</span></span>
- <span data-ttu-id="6fc3d-111">컨트롤러 이름에 **moviescontroller.cs**을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-111">For the Controller name enter **MoviesController**.</span></span>

  <span data-ttu-id="6fc3d-112">아래 이미지는 완료 된 대화 상자를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-112">The image below shows the completed dialog.</span></span>  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

<span data-ttu-id="6fc3d-113">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-113">Click **Add**.</span></span> <span data-ttu-id="6fc3d-114">오류가 발생 하면 컨트롤러 추가를 시작 하기 전에 응용 프로그램을 빌드하지 않았을 수 있습니다. Visual Studio에서 다음과 같은 파일 및 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-114">(If you get an error, you probably didn't build the application before starting adding the controller.) Visual Studio creates the following files and folders:</span></span>

- <span data-ttu-id="6fc3d-115">*Controllers* 폴더에 있는 *MoviesController.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-115">*A MoviesController.cs* file in the *Controllers* folder.</span></span>
- <span data-ttu-id="6fc3d-116">*Views\Movies* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-116">A *Views\Movies* folder.</span></span>
- <span data-ttu-id="6fc3d-117">새 *Views\Movies* 폴더에서 *. cshtml, Delete cshtml, Details, Edit. cshtml*및 *인덱스* 를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-117">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="6fc3d-118">Visual Studio에서 자동으로 [crud](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (만들기, 읽기, 업데이트 및 삭제) 작업 메서드 및 보기를 만들었습니다 (crud 작업 메서드 및 보기의 자동 생성을 스 캐 폴딩 이라고 함).</span><span class="sxs-lookup"><span data-stu-id="6fc3d-118">Visual Studio automatically created the [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="6fc3d-119">이제 동영상 항목을 만들고, 나열 하 고, 편집 하 고, 삭제할 수 있는 완전히 작동 하는 웹 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-119">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="6fc3d-120">응용 프로그램을 실행 하 고 **MVC 영화** 링크를 클릭 하거나, `Movies` 브라우저의 주소 표시줄에 있는 URL에 */da* 를 추가 하 여 컨트롤러를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-120">Run the application and click on the **MVC Movie** link (or browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser).</span></span> <span data-ttu-id="6fc3d-121">응용 프로그램은 기본 라우팅 ( *App \_ Start\RouteConfig.cs* 파일에 정의 됨)을 기반으로 하기 때문에 브라우저 요청은 `http://localhost:xxxxx/Movies` `Index` 컨트롤러의 기본 작업 메서드로 라우팅됩니다 `Movies` .</span><span class="sxs-lookup"><span data-stu-id="6fc3d-121">Because the application is relying on the default routing (defined in the *App\_Start\RouteConfig.cs* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="6fc3d-122">즉, 브라우저 요청은 `http://localhost:xxxxx/Movies` 실제로 브라우저 요청과 동일 합니다 `http://localhost:xxxxx/Movies/Index` .</span><span class="sxs-lookup"><span data-stu-id="6fc3d-122">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="6fc3d-123">아직 추가 하지 않았기 때문에 빈 영화 목록이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-123">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a><span data-ttu-id="6fc3d-124">동영상 만들기</span><span class="sxs-lookup"><span data-stu-id="6fc3d-124">Creating a Movie</span></span>

<span data-ttu-id="6fc3d-125">**새로 만들기** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-125">Select the **Create New** link.</span></span> <span data-ttu-id="6fc3d-126">동영상에 대 한 세부 정보를 입력 한 다음 **만들기** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-126">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="6fc3d-127">Price 필드에는 소수점 또는 쉼표를 입력할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-127">You may not be able to enter decimal points or commas in the Price field.</span></span> <span data-ttu-id="6fc3d-128">소수점에 쉼표 (,)를 사용 하는 영어가 아닌 로캘 및 미국 영어가 아닌 날짜 형식에 대해 jQuery 유효성 검사를 지원 하려면 &quot; &quot; 사용할 *globalize.js* 및 특정 *문화/globalize.cultures.js* 파일 (부터 [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) 및 JavaScript를 포함 해야 합니다 `Globalize.parseFloat` .</span><span class="sxs-lookup"><span data-stu-id="6fc3d-128">To support jQuery validation for non-English locales that use a comma (&quot;,&quot;) for a decimal point, and non US-English date formats, you must include *globalize.js* and your specific *cultures/globalize.cultures.js* file(from [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) and JavaScript to use `Globalize.parseFloat`.</span></span> <span data-ttu-id="6fc3d-129">다음 자습서에서이 작업을 수행 하는 방법을 보여 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-129">I'll show how to do this in the next tutorial.</span></span> <span data-ttu-id="6fc3d-130">이제 10 같은 정수를 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-130">For now, just enter whole numbers like 10.</span></span>

<span data-ttu-id="6fc3d-131">[ **만들기** ] 단추를 클릭 하면 양식이 서버에 게시 되 고,이 경우 동영상 정보가 데이터베이스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-131">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="6fc3d-132">그런 다음 목록에서 새로 만든 동영상을 볼 수 있는 */Clurl* 로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-132">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="6fc3d-133">나머지 몇 개의 동영상 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-133">Create a couple more movie entries.</span></span> <span data-ttu-id="6fc3d-134">모두 작동하는 **편집**, **세부 정보** 및 **삭제** 링크를 사용해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-134">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="6fc3d-135">생성 된 코드 검사</span><span class="sxs-lookup"><span data-stu-id="6fc3d-135">Examining the Generated Code</span></span>

<span data-ttu-id="6fc3d-136">*Controllers\MoviesController.cs* 파일을 열고 생성 된 메서드를 검사 합니다 `Index` .</span><span class="sxs-lookup"><span data-stu-id="6fc3d-136">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="6fc3d-137">메서드를 사용 하는 동영상 컨트롤러의 일부는 `Index` 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-137">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="6fc3d-138">컨트롤러에 대 한 요청은 `Movies` 테이블의 모든 항목을 반환 `Movies` 하 고 결과를 뷰에 전달 합니다 `Index` .</span><span class="sxs-lookup"><span data-stu-id="6fc3d-138">A request to the `Movies` controller returns all the entries in the `Movies` table and then passes the results to the `Index` view.</span></span> <span data-ttu-id="6fc3d-139">클래스의 다음 줄은 `MoviesController` 앞에서 설명한 대로 영화 데이터베이스 컨텍스트를 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-139">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="6fc3d-140">동영상 데이터베이스 컨텍스트를 사용 하 여 영화를 쿼리, 편집 및 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-140">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="6fc3d-141">강력한 형식의 모델 및 @model 키워드</span><span class="sxs-lookup"><span data-stu-id="6fc3d-141">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="6fc3d-142">이 자습서의 앞부분에서 볼 때 컨트롤러에서 개체를 사용 하 여 데이터 또는 개체를 뷰 템플릿에 전달 하는 방법을 살펴보았습니다 `ViewBag` .</span><span class="sxs-lookup"><span data-stu-id="6fc3d-142">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="6fc3d-143">는 `ViewBag` 뷰에 정보를 전달 하는 데 편리한 런타임에 바인딩되는 방법을 제공 하는 동적 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-143">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="6fc3d-144">또한 MVC는 *강력한* 형식의 개체를 뷰 템플릿에 전달 하는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-144">MVC also provides the ability to pass *strongly* typed objects to a view template.</span></span> <span data-ttu-id="6fc3d-145">강력 하 게 형식화 된이 방법은 Visual Studio 편집기에서 코드 및 더 다양 한 [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) 의 컴파일 시간 검사를 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-145">This strongly typed approach enables better compile-time checking of your code and richer [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) in the Visual Studio editor.</span></span> <span data-ttu-id="6fc3d-146">Visual Studio의 스 캐 폴딩 메커니즘은 *strongly* `MoviesController` 메서드 및 뷰를 만들 때 클래스 및 뷰 템플릿을 사용 하 여 강력한 형식의 모델을 전달 하는이 방법을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-146">The scaffolding mechanism in Visual Studio used this approach (that is, passing a *strongly* typed model) with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="6fc3d-147">*Controllers\MoviesController.cs* 파일에서 생성 된 메서드를 검사 합니다 `Details` .</span><span class="sxs-lookup"><span data-stu-id="6fc3d-147">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="6fc3d-148">`Details`메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-148">The `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

<span data-ttu-id="6fc3d-149">`id`매개 변수는 일반적으로 경로 데이터로 전달 됩니다. 예를 들어는 `http://localhost:1234/movies/details/1` 컨트롤러를 movie controller로 설정 하 고 작업을 `details` 및 `id` 로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-149">The `id` parameter is generally passed as route data, for example `http://localhost:1234/movies/details/1` will set the controller to the movie controller, the action to `details` and the `id` to 1.</span></span> <span data-ttu-id="6fc3d-150">다음과 같이 쿼리 문자열을 사용 하 여 id를 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-150">You could also pass in the id with a query string as follows:</span></span>

`http://localhost:1234/movies/details?id=1`

<span data-ttu-id="6fc3d-151">이 있으면 `Movie` 모델의 인스턴스가 `Movie` 뷰에 전달 됩니다 `Details` .</span><span class="sxs-lookup"><span data-stu-id="6fc3d-151">If a `Movie` is found, an instance of the `Movie` model is passed to the `Details` view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

<span data-ttu-id="6fc3d-152">*Views\Movies\Details.cshtml* 파일의 내용을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-152">Examine the contents of the *Views\Movies\Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

<span data-ttu-id="6fc3d-153">`@model`뷰 템플릿 파일의 맨 위에 문을 포함 하 여 뷰가 예상 하는 개체 유형을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-153">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="6fc3d-154">영화 컨트롤러를 만들 때 Visual Studio에서는 *Details.cshtml* 파일의 맨 위에 다음 `@model` 문을 자동으로 포함했습니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-154">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="6fc3d-155">이 `@model` 지시문을 사용하면 강력한 형식인 `Model` 개체를 사용하여 컨트롤러가 뷰에 전달된 영화에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-155">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="6fc3d-156">예를 들어, *Details* 템플릿에서는 코드는 각 동영상 필드를 강력한 형식의 개체를 사용 하 여 `DisplayNameFor` HTML 도우미 [에 전달](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) 합니다 `Model` .</span><span class="sxs-lookup"><span data-stu-id="6fc3d-156">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="6fc3d-157">`Create`및 `Edit` 메서드 및 뷰 템플릿은 또한 동영상 모델 개체를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-157">The `Create` and `Edit` methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="6fc3d-158">MoviesController.cs 파일에서 *Index. cshtml* 뷰 템플릿 및 메서드를 검토 합니다 `Index` *MoviesController.cs* .</span><span class="sxs-lookup"><span data-stu-id="6fc3d-158">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="6fc3d-159">[`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx)작업 메서드에서 도우미 메서드를 호출할 때 코드에서 개체를 만드는 방법을 확인 `View` `Index` 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-159">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="6fc3d-160">그런 다음 코드는이 `Movies` 목록을 `Index` 동작 메서드에서 뷰로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-160">The code then passes this `Movies` list from the `Index` action method to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

<span data-ttu-id="6fc3d-161">동영상 컨트롤러를 만들 때 Visual Studio는 다음 문을 자동으로 `@model` *Index. cshtml* 파일의 맨 위에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-161">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

<span data-ttu-id="6fc3d-162">이 `@model` 지시문을 사용 하면 강력한 형식의 개체를 사용 하 여 컨트롤러에서 뷰로 전달 된 동영상 목록에 액세스할 수 있습니다 `Model` .</span><span class="sxs-lookup"><span data-stu-id="6fc3d-162">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="6fc3d-163">예를 들어, *인덱스인* 템플릿에서 코드는 강력한 형식의 개체에 대해 문을 수행 하 여 동영상을 반복 합니다 `foreach` `Model` .</span><span class="sxs-lookup"><span data-stu-id="6fc3d-163">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="6fc3d-164">개체는 강력한 형식의 개체 이기 때문에 `Model` `IEnumerable<Movie>` `item` 루프의 각 개체는로 형식화 됩니다 `Movie` .</span><span class="sxs-lookup"><span data-stu-id="6fc3d-164">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="6fc3d-165">다른 이점 중 하나는 코드 편집기에서 코드 및 전체 IntelliSense 지원에 대 한 컴파일 시간 검사를 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-165">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="6fc3d-167">SQL Server LocalDB 사용</span><span class="sxs-lookup"><span data-stu-id="6fc3d-167">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="6fc3d-168">Entity Framework Code First 제공 된 데이터베이스 연결 문자열이 `Movies` 아직 존재 하지 않은 데이터베이스를 가리키고 있으므로 데이터베이스를 자동으로 만들 Code First.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-168">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="6fc3d-169">*앱 \_ 데이터* 폴더를 살펴보면이를 만들었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-169">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="6fc3d-170">*동영상 .mdf* 파일이 표시 되지 않으면 **솔루션 탐색기** 도구 모음에서 **모든 파일 표시** 단추를 클릭 하 고 **새로 고침** 단추를 클릭 한 다음 *앱 \_ 데이터* 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-170">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image9.png)

<span data-ttu-id="6fc3d-171">*동영상과* 를 두 번 클릭 하 여 **서버 탐색기**를 연 다음 **Tables** 폴더를 확장 하 여 영화 테이블을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-171">Double-click *Movies.mdf* to open **SERVER EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span> <span data-ttu-id="6fc3d-172">ID 옆의 키 아이콘을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-172">Note the key icon next to ID.</span></span> <span data-ttu-id="6fc3d-173">기본적으로 EF는 ID가 기본 키 인 속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-173">By default, EF will make a property named ID the primary key.</span></span> <span data-ttu-id="6fc3d-174">EF 및 MVC에 대 한 자세한 내용은 Tom Dykstra 's의 우수한 자습서 [mvc 및 EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-174">For more information on EF and MVC, see Tom Dykstra's excellent tutorial on [MVC and EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="6fc3d-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="6fc3d-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span></span>

<span data-ttu-id="6fc3d-176">테이블을 마우스 오른쪽 단추로 클릭 `Movies` 하 고 **테이블 데이터 표시** 를 선택 하 여 만든 데이터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-176">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

<span data-ttu-id="6fc3d-177">테이블을 마우스 오른쪽 단추로 클릭 하 `Movies` 고 **테이블 정의 열기** 를 선택 하 여 Entity Framework Code First 생성 된 테이블 구조를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-177">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

<span data-ttu-id="6fc3d-178">테이블의 스키마가 앞에서 `Movies` 만든 클래스에 매핑되는 방식을 확인 `Movie` 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-178">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="6fc3d-179">Entity Framework Code First는 클래스를 기반으로이 스키마를 자동으로 만들었습니다 `Movie` .</span><span class="sxs-lookup"><span data-stu-id="6fc3d-179">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="6fc3d-180">완료 되 면 *MovieDBContext* 를 마우스 오른쪽 단추로 클릭 하 고 **연결 닫기**를 선택 하 여 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-180">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="6fc3d-181">연결을 닫지 않은 경우 다음에 프로젝트를 실행할 때 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-181">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

<span data-ttu-id="6fc3d-182">이제 데이터를 표시, 편집, 업데이트 및 삭제할 데이터베이스 및 페이지가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-182">You now have a database and pages to display, edit, update and delete data.</span></span> <span data-ttu-id="6fc3d-183">다음 자습서에서는 스 캐 폴드 코드의 나머지 부분을 검토 하 고 `SearchIndex` `SearchIndex` 이 데이터베이스에서 영화를 검색할 수 있는 메서드 및 뷰를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-183">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span> <span data-ttu-id="6fc3d-184">MVC와 함께 Entity Framework를 사용 하는 방법에 대 한 자세한 내용은 [ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델 만들기](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6fc3d-184">For more information on using Entity Framework with MVC, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6fc3d-185">[이전](creating-a-connection-string.md)
> [다음](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="6fc3d-185">[Previous](creating-a-connection-string.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
