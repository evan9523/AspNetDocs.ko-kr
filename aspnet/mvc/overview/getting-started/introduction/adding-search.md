---
uid: mvc/overview/getting-started/introduction/adding-search
title: 검색 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/17/2019
ms.assetid: df001954-18bf-4550-b03d-43911a0ea186
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-search
msc.type: authoredcontent
ms.openlocfilehash: ada125c917656f3a83524ff39e53b4cfc041a497
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029700"
---
<a name="search"></a><span data-ttu-id="bf1c6-102">검색</span><span class="sxs-lookup"><span data-stu-id="bf1c6-102">Search</span></span>
====================

[!INCLUDE [Tutorial Note](sample/code-location.md)]

## <a name="adding-a-search-method-and-search-view"></a><span data-ttu-id="bf1c6-103">검색 방법 및 검색 뷰를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-103">Adding a Search Method and Search View</span></span>

<span data-ttu-id="bf1c6-104">이 섹션에서는 검색 기능을 추가 합니다 `Index` 작업 메서드를 사용 하면 영화 장르 또는 이름으로 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-104">In this section you'll add search capability to the `Index` action method that lets you search movies by genre or name.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf1c6-105">전제 조건</span><span class="sxs-lookup"><span data-stu-id="bf1c6-105">Prerequisites</span></span>

<span data-ttu-id="bf1c6-106">이 섹션의 스크린이 샷을 일치 하려면 f5 키를 눌러 응용 프로그램을 실행 하 고 데이터베이스에 다음 영화를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-106">To match this section's screenshots, you need to run the application (F5) and add the following movies to the database.</span></span>

| <span data-ttu-id="bf1c6-107">제목</span><span class="sxs-lookup"><span data-stu-id="bf1c6-107">Title</span></span> | <span data-ttu-id="bf1c6-108">릴리스 날짜</span><span class="sxs-lookup"><span data-stu-id="bf1c6-108">Release Date</span></span> | <span data-ttu-id="bf1c6-109">장르</span><span class="sxs-lookup"><span data-stu-id="bf1c6-109">Genre</span></span> | <span data-ttu-id="bf1c6-110">가격</span><span class="sxs-lookup"><span data-stu-id="bf1c6-110">Price</span></span> |
| ----- | ------------ | ----- | ----- |
| <span data-ttu-id="bf1c6-111">Ghostbusters</span><span class="sxs-lookup"><span data-stu-id="bf1c6-111">Ghostbusters</span></span> | <span data-ttu-id="bf1c6-112">6/8/1984</span><span class="sxs-lookup"><span data-stu-id="bf1c6-112">6/8/1984</span></span> | <span data-ttu-id="bf1c6-113">코미디</span><span class="sxs-lookup"><span data-stu-id="bf1c6-113">Comedy</span></span> | <span data-ttu-id="bf1c6-114">6.99</span><span class="sxs-lookup"><span data-stu-id="bf1c6-114">6.99</span></span> |
| <span data-ttu-id="bf1c6-115">Ghostbusters II</span><span class="sxs-lookup"><span data-stu-id="bf1c6-115">Ghostbusters II</span></span> | <span data-ttu-id="bf1c6-116">6/16/1989</span><span class="sxs-lookup"><span data-stu-id="bf1c6-116">6/16/1989</span></span> | <span data-ttu-id="bf1c6-117">코미디</span><span class="sxs-lookup"><span data-stu-id="bf1c6-117">Comedy</span></span> | <span data-ttu-id="bf1c6-118">6.99</span><span class="sxs-lookup"><span data-stu-id="bf1c6-118">6.99</span></span> |
| <span data-ttu-id="bf1c6-119">전시관이 네의 전 세계</span><span class="sxs-lookup"><span data-stu-id="bf1c6-119">Planet of the Apes</span></span> | <span data-ttu-id="bf1c6-120">3/27/1986</span><span class="sxs-lookup"><span data-stu-id="bf1c6-120">3/27/1986</span></span> | <span data-ttu-id="bf1c6-121">작업</span><span class="sxs-lookup"><span data-stu-id="bf1c6-121">Action</span></span> | <span data-ttu-id="bf1c6-122">5.99</span><span class="sxs-lookup"><span data-stu-id="bf1c6-122">5.99</span></span> |


## <a name="updating-the-index-form"></a><span data-ttu-id="bf1c6-123">인덱스 형식 업데이트</span><span class="sxs-lookup"><span data-stu-id="bf1c6-123">Updating the Index Form</span></span>

<span data-ttu-id="bf1c6-124">업데이트 하 여 시작 합니다 `Index` 동작 메서드를 기존 `MoviesController` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-124">Start by updating the `Index` action method to the existing `MoviesController` class.</span></span> <span data-ttu-id="bf1c6-125">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-125">Here's the code:</span></span>

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

<span data-ttu-id="bf1c6-126">첫 번째 줄을 `Index` 메서드는 다음 항목을 만듭니다 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 영화를 선택 하는 쿼리:</span><span class="sxs-lookup"><span data-stu-id="bf1c6-126">The first line of the `Index` method creates the following [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) query to select the movies:</span></span>

[!code-csharp[Main](adding-search/samples/sample2.cs)]

<span data-ttu-id="bf1c6-127">쿼리가 시점에서 정의 되었지만 데이터베이스에 대해 아직 실행 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-127">The query is defined at this point, but hasn't yet been run against the database.</span></span>

<span data-ttu-id="bf1c6-128">경우는 `searchString` 문자열을 포함 하는 매개 변수, 영화 쿼리는 다음 코드를 사용 하 여 검색 문자열의 값에 필터링 하도록 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-128">If the `searchString` parameter contains a string, the movies query is modified to filter on the value of the search string, using the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample3.cs)]

<span data-ttu-id="bf1c6-129">위의 `s => s.Title` 코드는 [람다 식](https://msdn.microsoft.com/library/bb397687.aspx)입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-129">The `s => s.Title` code above is a [Lambda Expression](https://msdn.microsoft.com/library/bb397687.aspx).</span></span> <span data-ttu-id="bf1c6-130">람다 식은 메서드 기반 되는 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 와 같은 표준 쿼리 연산자 메서드의 인수로 쿼리는 [여기서](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) 메서드 위의 코드에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-130">Lambdas are used in method-based [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) queries as arguments to standard query operator methods such as the [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) method used in the above code.</span></span> <span data-ttu-id="bf1c6-131">LINQ 쿼리는 정의 될 때 또는 같은 메서드를 호출 하 여 수정 될 때 실행 되지 않습니다 `Where` 또는 `OrderBy`합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-131">LINQ queries are not executed when they are defined or when they are modified by calling a method such as `Where` or `OrderBy`.</span></span> <span data-ttu-id="bf1c6-132">대신 쿼리 실행이 지연, 즉, 실현된 된 값이 실제로 반복 될 때까지 식의 계산이 지연 되는 또는 [ `ToList` ](https://msdn.microsoft.com/library/bb342261.aspx) 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-132">Instead, query execution is deferred, which means that the evaluation of an expression is delayed until its realized value is actually iterated over or the [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) method is called.</span></span> <span data-ttu-id="bf1c6-133">에 `Search` 샘플에서 쿼리가 실행 되는 *Index.cshtml* 보기.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-133">In the `Search` sample, the query is executed in the *Index.cshtml* view.</span></span> <span data-ttu-id="bf1c6-134">지연된 쿼리 실행에 대한 자세한 내용은 [쿼리 실행](https://msdn.microsoft.com/library/bb738633.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-134">For more information about deferred query execution, see [Query Execution](https://msdn.microsoft.com/library/bb738633.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="bf1c6-135">합니다 [Contains](https://msdn.microsoft.com/library/bb155125.aspx) 메서드 c# 코드가 아니라 위의 데이터베이스에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-135">The [Contains](https://msdn.microsoft.com/library/bb155125.aspx) method is run on the database, not the c# code above.</span></span> <span data-ttu-id="bf1c6-136">데이터베이스에서 [Contains](https://msdn.microsoft.com/library/bb155125.aspx) 매핑됩니다 [SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx)는 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-136">On the database, [Contains](https://msdn.microsoft.com/library/bb155125.aspx) maps to [SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx), which is case insensitive.</span></span>

<span data-ttu-id="bf1c6-137">업데이트할 수 있습니다 이제는 `Index` 폼을 사용자에 게 표시 되는 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-137">Now you can update the `Index` view that will display the form to the user.</span></span>

<span data-ttu-id="bf1c6-138">응용 프로그램을 실행 하 고 이동 */Movies/Index*합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-138">Run the application and navigate to */Movies/Index*.</span></span> <span data-ttu-id="bf1c6-139">쿼리 문자열(예: `?searchString=ghost`)을 URL에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-139">Append a query string such as `?searchString=ghost` to the URL.</span></span> <span data-ttu-id="bf1c6-140">필터링된 동영상이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-140">The filtered movies are displayed.</span></span>

![SearchQryStr](adding-search/_static/image1.png)

<span data-ttu-id="bf1c6-142">시그니처를 변경 하는 경우는 `Index` 명명 된 매개 변수를 포함 하는 방법 `id`, `id` 매개 변수는 일치를 `{id}` 기본값에 대 한 자리 표시자 경로 집합에는 *앱\_시작 RouteConfig.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-142">If you change the signature of the `Index` method to have a parameter named `id`, the `id` parameter will match the `{id}` placeholder for the default routes set in the *App\_Start\RouteConfig.cs* file.</span></span>

[!code-json[Main](adding-search/samples/sample4.json)]

<span data-ttu-id="bf1c6-143">원래 `Index` 메서드는 다음과 같습니다:</span><span class="sxs-lookup"><span data-stu-id="bf1c6-143">The original `Index` method looks like this::</span></span>

[!code-csharp[Main](adding-search/samples/sample5.cs)]

<span data-ttu-id="bf1c6-144">수정 된 `Index` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-144">The modified `Index` method would look as follows:</span></span>

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

<span data-ttu-id="bf1c6-145">이제 쿼리 문자열 값이 아닌 경로 데이터(URL 세그먼트)로 검색 제목을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-145">You can now pass the search title as route data (a URL segment) instead of as a query string value.</span></span>

![](adding-search/_static/image2.png)

<span data-ttu-id="bf1c6-146">그러나 사용자가 영화를 검색하려고 할 때마다 URL을 수정하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-146">However, you can't expect users to modify the URL every time they want to search for a movie.</span></span> <span data-ttu-id="bf1c6-147">따라서 이제 영화를 필터링하는 데 도움이 되는 UI를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-147">So now you'll add UI to help them filter movies.</span></span> <span data-ttu-id="bf1c6-148">시그니처를 변경 하는 경우는 `Index` 경로 바인딩 ID 매개 변수를 전달 하는 방법을 테스트 하는 방법 변경는 하 `Index` 라는 문자열 매개 변수를 사용 하는 메서드 `searchString`:</span><span class="sxs-lookup"><span data-stu-id="bf1c6-148">If you changed the signature of the `Index` method to test how to pass the route-bound ID parameter, change it back so that your `Index` method takes a string parameter named `searchString`:</span></span>

[!code-csharp[Main](adding-search/samples/sample7.cs)]

<span data-ttu-id="bf1c6-149">열기는 *Views\Movies\Index.cshtml* 파일을 열고 바로 뒤 `@Html.ActionLink("Create New", "Create")`, 아래 강조 표시 된 폼 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-149">Open the *Views\Movies\Index.cshtml* file, and just after `@Html.ActionLink("Create New", "Create")`, add the form markup highlighted below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

<span data-ttu-id="bf1c6-150">합니다 `Html.BeginForm` 도우미를 만듭니다 `<form>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-150">The `Html.BeginForm` helper creates an opening `<form>` tag.</span></span> <span data-ttu-id="bf1c6-151">합니다 `Html.BeginForm` 도우미 하면 폼이 사용자가 클릭 하 여 폼을 제출 하는 경우 자신에 게 게시 합니다 **필터** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-151">The `Html.BeginForm` helper causes the form to post to itself when the user submits the form by clicking the **Filter** button.</span></span>

<span data-ttu-id="bf1c6-152">Visual Studio 2013이 표시 하 고 보기 파일을 편집 하는 경우 유용한 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-152">Visual Studio 2013 has a nice improvement when displaying and editing View files.</span></span> <span data-ttu-id="bf1c6-153">를 실행 하면 응용 프로그램 뷰 파일을 사용 하 여 open Visual Studio 2013 뷰를 표시 하는 올바른 컨트롤러 작업 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-153">When you run the application with a view file open, Visual Studio 2013 invokes the correct controller action method to display the view.</span></span>

![](adding-search/_static/image3.png)

<span data-ttu-id="bf1c6-154">인덱스 뷰를 사용 하 여 위의 이미지에서과 같이 Visual Studio에서 열기, 탭 Ctr F5 또는 f5 키를 응용 프로그램을 실행 한 다음 동영상을 검색 해 보세요.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-154">With the Index view open in Visual Studio (as shown in the image above), tap Ctr F5 or F5 to run the application and then try searching for a movie.</span></span>

![](adding-search/_static/image4.png)

<span data-ttu-id="bf1c6-155">방법이 없는 `HttpPost` 오버 로드는 `Index` 메서드.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-155">There's no `HttpPost` overload of the `Index` method.</span></span> <span data-ttu-id="bf1c6-156">필요 없는, 메서드는 응용 프로그램의 상태를 변경 하지 않고 때문에 데이터를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-156">You don't need it, because the method isn't changing the state of the application, just filtering data.</span></span>

<span data-ttu-id="bf1c6-157">다음 `HttpPost Index` 메서드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-157">You could add the following `HttpPost Index` method.</span></span> <span data-ttu-id="bf1c6-158">작업 호출자는 일치 하는 경우는 `HttpPost Index` 메서드 및 `HttpPost Index` 메서드는 아래 이미지에 표시 된 대로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-158">In that case, the action invoker would match the `HttpPost Index` method, and the `HttpPost Index` method would run as shown in the image below.</span></span>

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![SearchPostGhost](adding-search/_static/image5.png)

<span data-ttu-id="bf1c6-160">그러나 이 `HttpPost` 버전의 `Index` 메서드를 추가하는 경우에도 이를 모두 구현하는 방법은 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-160">However, even if you add this `HttpPost` version of the `Index` method, there's a limitation in how this has all been implemented.</span></span> <span data-ttu-id="bf1c6-161">특정 검색을 책갈피로 설정하거나 동일하게 필터링된 영화 목록을 보기 위해 클릭할 수 있는 링크를 친구에게 보내려고 한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-161">Imagine that you want to bookmark a particular search or you want to send a link to friends that they can click in order to see the same filtered list of movies.</span></span> <span data-ttu-id="bf1c6-162">HTTP POST에 대 한 URL를 요청 하는 GET 요청 (xxxxx/Movies/Index)에 대 한 URL과 동일한-URL 자체의 검색 정보가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-162">Notice that the URL for the HTTP POST request is the same as the URL for the GET request (localhost:xxxxx/Movies/Index) -- there's no search information in the URL itself.</span></span> <span data-ttu-id="bf1c6-163">오른쪽 이제 검색 문자열 정보를 서버로 전송 됩니다는 양식 필드 값으로.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-163">Right now, the search string information is sent to the server as a form field value.</span></span> <span data-ttu-id="bf1c6-164">즉, URL에 친구를 보내거나 책갈피에 해당 검색 정보를 캡처할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-164">This means you can't capture that search information to bookmark or send to friends in a URL.</span></span>

<span data-ttu-id="bf1c6-165">솔루션의 오버 로드를 사용 하는 것 `BeginForm` 에 POST 요청을 URL로 검색 정보를 추가 하도록 하 고를 라우팅할 수 해야를 지정 하는 `HttpGet` 버전의는 `Index` 메서드.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-165">The solution is to use an overload of `BeginForm` that specifies that the POST request should add the search information to the URL and that it should be routed to the `HttpGet` version of the `Index` method.</span></span> <span data-ttu-id="bf1c6-166">매개 변수가 없는 기존 항목 바꾸기 `BeginForm` 다음 태그를 사용 하 여 메서드:</span><span class="sxs-lookup"><span data-stu-id="bf1c6-166">Replace the existing parameterless `BeginForm` method with the following markup:</span></span>

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

<span data-ttu-id="bf1c6-168">이제 검색을 제출할 때 URL 검색 쿼리 문자열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-168">Now when you submit a search, the URL contains a search query string.</span></span> <span data-ttu-id="bf1c6-169">`HttpPost Index` 메서드가 있는 경우에도 검색은 `HttpGet Index` 작업 메서드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-169">Searching will also go to the `HttpGet Index` action method, even if you have a `HttpPost Index` method.</span></span>

![IndexWithGetURL](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a><span data-ttu-id="bf1c6-171">장르별 검색 추가</span><span class="sxs-lookup"><span data-stu-id="bf1c6-171">Adding Search by Genre</span></span>

<span data-ttu-id="bf1c6-172">추가한 경우에 `HttpPost` 버전의는 `Index` 메서드를 지금 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-172">If you added the `HttpPost` version of the `Index` method, delete it now.</span></span>

<span data-ttu-id="bf1c6-173">다음으로, 사용자가 영화 장르 하 여 검색할 수 있도록 하는 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-173">Next, you'll add a feature to let users search for movies by genre.</span></span> <span data-ttu-id="bf1c6-174">`Index` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-174">Replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample11.cs)]

<span data-ttu-id="bf1c6-175">이 버전의 `Index` 메서드는 추가 매개 변수, 즉 `movieGenre`합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-175">This version of the `Index` method takes an additional parameter, namely `movieGenre`.</span></span> <span data-ttu-id="bf1c6-176">코드의 처음 몇 줄 만들기는 `List` 데이터베이스에서 영화 장르를 포함 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-176">The first few lines of code create a `List` object to hold movie genres from the database.</span></span>

<span data-ttu-id="bf1c6-177">다음 코드는 데이터베이스에서 모든 장르를 검색하는 LINQ 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-177">The following code is a LINQ query that retrieves all the genres from the database.</span></span>

[!code-csharp[Main](adding-search/samples/sample12.cs)]

<span data-ttu-id="bf1c6-178">코드를 사용 하는 `AddRange` 제네릭 메서드의 `List` 목록에는 모든 고유 장르를 추가할 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-178">The code uses the `AddRange` method of the generic `List` collection to add all the distinct genres to the list.</span></span> <span data-ttu-id="bf1c6-179">(없이 `Distinct` 한정자를 중복 장르가 추가-코미디 샘플에서 두 번 추가할 수는 예를 들어).</span><span class="sxs-lookup"><span data-stu-id="bf1c6-179">(Without the `Distinct` modifier, duplicate genres would be added — for example, comedy would be added twice in our sample).</span></span> <span data-ttu-id="bf1c6-180">코드에는 장르 목록을 저장 된 `ViewBag.MovieGenre` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-180">The code then stores the list of genres in the `ViewBag.MovieGenre` object.</span></span> <span data-ttu-id="bf1c6-181">범주 데이터 (이러한는 영화 장르)으로 저장을 [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) 개체는 `ViewBag`, MVC 응용 프로그램에 대 한 일반적인 방식은 드롭다운 목록 상자에서 범주 데이터에 액세스 한 다음.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-181">Storing category data (such a movie genres) as a [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) object in a `ViewBag`, then accessing the category data in a dropdown list box is a typical approach for MVC applications.</span></span>

<span data-ttu-id="bf1c6-182">다음 코드를 확인 하는 방법을 보여 줍니다는 `movieGenre` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-182">The following code shows how to check the `movieGenre` parameter.</span></span> <span data-ttu-id="bf1c6-183">비어 있지 않으면 코드를 추가로 지정된 장르에 선택한 영화를 제한 하려면 영화 쿼리를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-183">If it's not empty, the code further constrains the movies query to limit the selected movies to the specified genre.</span></span>

[!code-csharp[Main](adding-search/samples/sample13.cs)]

<span data-ttu-id="bf1c6-184">영화 목록 반복 될 때까지 쿼리가 데이터베이스에서 실행 되지에서 설명한 대로 (후 보기에서 발생 하는 `Index` 작업 메서드는 반환).</span><span class="sxs-lookup"><span data-stu-id="bf1c6-184">As stated previously, the query is not run on the database until the movie list is iterated over (which happens in the View, after the `Index` action method returns).</span></span>

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a><span data-ttu-id="bf1c6-185">장르별 검색을 지원 하도록 인덱스 보기에 태그 추가</span><span class="sxs-lookup"><span data-stu-id="bf1c6-185">Adding Markup to the Index View to Support Search by Genre</span></span>

<span data-ttu-id="bf1c6-186">추가 `Html.DropDownList` 도우미를 *Views\Movies\Index.cshtml* 파일을 바로 앞의 `TextBox` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-186">Add an `Html.DropDownList` helper to the *Views\Movies\Index.cshtml* file, just before the `TextBox` helper.</span></span> <span data-ttu-id="bf1c6-187">완료 된 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-187">The completed markup is shown below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

<span data-ttu-id="bf1c6-188">다음 코드에서</span><span class="sxs-lookup"><span data-stu-id="bf1c6-188">In the following code:</span></span>

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

<span data-ttu-id="bf1c6-189">매개 변수 "MovieGenre"에 대 한 키를 제공 합니다 `DropDownList` 찾으려고 도우미를 `IEnumerable<SelectListItem>` 에서 `ViewBag`.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-189">The parameter "MovieGenre" provides the key for the `DropDownList` helper to find a `IEnumerable<SelectListItem>` in the `ViewBag`.</span></span> <span data-ttu-id="bf1c6-190">`ViewBag` 작업 메서드에서 채워졌습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-190">The `ViewBag` was populated in the action method:</span></span>

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

<span data-ttu-id="bf1c6-191">옵션 레이블을 제공 "All" 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-191">The parameter "All" provides an option label.</span></span> <span data-ttu-id="bf1c6-192">브라우저에서 선택한 항목을 검사 하는 경우 해당 "value" 특성이 비어 있음을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-192">If you inspect that choice in your browser, you'll see that its "value" attribute is empty.</span></span> <span data-ttu-id="bf1c6-193">컨트롤러만 필터링 때문 `if` 문자열이 아닙니다 `null` 이거나 비어 있으면 빈 값에 대 한 제출 `movieGenre` 모든 장르를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-193">Since our controller only filters `if` the string is not `null` or empty, submitting an empty value for `movieGenre` shows all genres.</span></span>

<span data-ttu-id="bf1c6-194">또한 기본적으로 선택 하는 옵션을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-194">You can also set an option to be selected by default.</span></span> <span data-ttu-id="bf1c6-195">컨트롤러의 코드를 변경 하는 기본 옵션으로 "코미디" 하려는 경우 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-195">If you wanted "Comedy" as your default option, you would change the code in the Controller like so:</span></span>

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

<span data-ttu-id="bf1c6-196">응용 프로그램을 실행 하 고 이동할 */Movies/Index*합니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-196">Run the application and browse to */Movies/Index*.</span></span> <span data-ttu-id="bf1c6-197">장르별, 동영상 이름별 및 모두 기준으로 검색을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-197">Try a search by genre, by movie name, and by both criteria.</span></span>

![](adding-search/_static/image8.png)

<span data-ttu-id="bf1c6-198">이 섹션에서는 검색 작업 메서드 및 사용자가 영화 제목과 장르 하 여 검색할 수 있는 보기를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-198">In this section you created a search action method and view that let users search by movie title and genre.</span></span> <span data-ttu-id="bf1c6-199">다음 섹션에서 살펴보겠습니다 속성을 추가 하는 방법의 `Movie` 모델과 테스트 데이터베이스를 자동으로 만들어집니다 하는 이니셜라이저를 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="bf1c6-199">In the next section, you'll look at how to add a property to the `Movie` model and how to add an initializer that will automatically create a test database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bf1c6-200">[이전](examining-the-edit-methods-and-edit-view.md)
> [다음](adding-a-new-field.md)</span><span class="sxs-lookup"><span data-stu-id="bf1c6-200">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-a-new-field.md)</span></span>
