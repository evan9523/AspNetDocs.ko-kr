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
ms.openlocfilehash: be4e4d13e574b0fcb77d2d0fb8c6f58041b1ece2
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044923"
---
# <a name="search"></a><span data-ttu-id="8fa61-102">검색</span><span class="sxs-lookup"><span data-stu-id="8fa61-102">Search</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

## <a name="adding-a-search-method-and-search-view"></a><span data-ttu-id="8fa61-103">검색 방법 및 검색 보기 추가</span><span class="sxs-lookup"><span data-stu-id="8fa61-103">Adding a Search Method and Search View</span></span>

<span data-ttu-id="8fa61-104">이 섹션에서는 `Index` 장르 또는 이름을 기준으로 영화를 검색할 수 있는 작업 메서드에 검색 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-104">In this section you'll add search capability to the `Index` action method that lets you search movies by genre or name.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fa61-105">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="8fa61-105">Prerequisites</span></span>

<span data-ttu-id="8fa61-106">이 섹션의 스크린샷을 일치 시키려면 응용 프로그램을 실행 (F5) 하 고 다음 영화를 데이터베이스에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-106">To match this section's screenshots, you need to run the application (F5) and add the following movies to the database.</span></span>

| <span data-ttu-id="8fa61-107">제목</span><span class="sxs-lookup"><span data-stu-id="8fa61-107">Title</span></span> | <span data-ttu-id="8fa61-108">릴리스 날짜:</span><span class="sxs-lookup"><span data-stu-id="8fa61-108">Release Date</span></span> | <span data-ttu-id="8fa61-109">Genre</span><span class="sxs-lookup"><span data-stu-id="8fa61-109">Genre</span></span> | <span data-ttu-id="8fa61-110">가격</span><span class="sxs-lookup"><span data-stu-id="8fa61-110">Price</span></span> |
| ----- | ------------ | ----- | ----- |
| <span data-ttu-id="8fa61-111">Ghostbusters</span><span class="sxs-lookup"><span data-stu-id="8fa61-111">Ghostbusters</span></span> | <span data-ttu-id="8fa61-112">6/8/1984</span><span class="sxs-lookup"><span data-stu-id="8fa61-112">6/8/1984</span></span> | <span data-ttu-id="8fa61-113">코미디</span><span class="sxs-lookup"><span data-stu-id="8fa61-113">Comedy</span></span> | <span data-ttu-id="8fa61-114">6.99</span><span class="sxs-lookup"><span data-stu-id="8fa61-114">6.99</span></span> |
| <span data-ttu-id="8fa61-115">Ghostbusters II</span><span class="sxs-lookup"><span data-stu-id="8fa61-115">Ghostbusters II</span></span> | <span data-ttu-id="8fa61-116">6/16/1989</span><span class="sxs-lookup"><span data-stu-id="8fa61-116">6/16/1989</span></span> | <span data-ttu-id="8fa61-117">코미디</span><span class="sxs-lookup"><span data-stu-id="8fa61-117">Comedy</span></span> | <span data-ttu-id="8fa61-118">6.99</span><span class="sxs-lookup"><span data-stu-id="8fa61-118">6.99</span></span> |
| <span data-ttu-id="8fa61-119">Apes의 행성</span><span class="sxs-lookup"><span data-stu-id="8fa61-119">Planet of the Apes</span></span> | <span data-ttu-id="8fa61-120">3/27/1986</span><span class="sxs-lookup"><span data-stu-id="8fa61-120">3/27/1986</span></span> | <span data-ttu-id="8fa61-121">작업</span><span class="sxs-lookup"><span data-stu-id="8fa61-121">Action</span></span> | <span data-ttu-id="8fa61-122">5.99</span><span class="sxs-lookup"><span data-stu-id="8fa61-122">5.99</span></span> |

## <a name="updating-the-index-form"></a><span data-ttu-id="8fa61-123">인덱스 폼 업데이트</span><span class="sxs-lookup"><span data-stu-id="8fa61-123">Updating the Index Form</span></span>

<span data-ttu-id="8fa61-124">먼저 `Index` 작업 메서드를 기존 `MoviesController` 클래스로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-124">Start by updating the `Index` action method to the existing `MoviesController` class.</span></span> <span data-ttu-id="8fa61-125">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-125">Here's the code:</span></span>

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

<span data-ttu-id="8fa61-126">메서드의 첫 번째 줄에서는 `Index` 다음 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 쿼리를 만들어 영화를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-126">The first line of the `Index` method creates the following [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) query to select the movies:</span></span>

[!code-csharp[Main](adding-search/samples/sample2.cs)]

<span data-ttu-id="8fa61-127">쿼리가이 시점에 정의 되었지만 아직 데이터베이스에 대해 실행 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-127">The query is defined at this point, but hasn't yet been run against the database.</span></span>

<span data-ttu-id="8fa61-128">`searchString`매개 변수에 문자열이 포함 된 경우 다음 코드를 사용 하 여 검색 문자열의 값을 필터링 하도록 동영상 쿼리를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-128">If the `searchString` parameter contains a string, the movies query is modified to filter on the value of the search string, using the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample3.cs)]

<span data-ttu-id="8fa61-129">위의 `s => s.Title` 코드는 [람다 식](https://msdn.microsoft.com/library/bb397687.aspx)입니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-129">The `s => s.Title` code above is a [Lambda Expression](https://msdn.microsoft.com/library/bb397687.aspx).</span></span> <span data-ttu-id="8fa61-130">람다 식은 메서드 기반 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 쿼리에서 위의 코드에서 사용 된 [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) 메서드와 같은 표준 쿼리 연산자 메서드의 인수로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-130">Lambdas are used in method-based [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) queries as arguments to standard query operator methods such as the [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) method used in the above code.</span></span> <span data-ttu-id="8fa61-131">LINQ 쿼리는 정의 될 때 또는 또는와 같은 메서드를 호출 하 여 수정 될 때 실행 되지 `Where` 않습니다 `OrderBy` .</span><span class="sxs-lookup"><span data-stu-id="8fa61-131">LINQ queries are not executed when they are defined or when they are modified by calling a method such as `Where` or `OrderBy`.</span></span> <span data-ttu-id="8fa61-132">대신 쿼리 실행이 지연 됩니다. 즉, 실현 된 값이 실제로 반복 되거나 메서드가 호출 될 때까지 식의 계산이 지연 됩니다 [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) .</span><span class="sxs-lookup"><span data-stu-id="8fa61-132">Instead, query execution is deferred, which means that the evaluation of an expression is delayed until its realized value is actually iterated over or the [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) method is called.</span></span> <span data-ttu-id="8fa61-133">`Search`이 샘플에서 쿼리는 *인덱스. cshtml* 뷰에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-133">In the `Search` sample, the query is executed in the *Index.cshtml* view.</span></span> <span data-ttu-id="8fa61-134">지연된 쿼리 실행에 대한 자세한 내용은 [쿼리 실행](https://msdn.microsoft.com/library/bb738633.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fa61-134">For more information about deferred query execution, see [Query Execution](https://msdn.microsoft.com/library/bb738633.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="8fa61-135">[Contains](https://msdn.microsoft.com/library/bb155125.aspx) 메서드는 위의 c # 코드가 아닌 데이터베이스에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-135">The [Contains](https://msdn.microsoft.com/library/bb155125.aspx) method is run on the database, not the c# code above.</span></span> <span data-ttu-id="8fa61-136">데이터베이스에서 [Contains](https://msdn.microsoft.com/library/bb155125.aspx) 는 대/소문자를 구분 하지 않는 [SQL과](https://msdn.microsoft.com/library/ms179859.aspx)매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-136">On the database, [Contains](https://msdn.microsoft.com/library/bb155125.aspx) maps to [SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx), which is case insensitive.</span></span>

<span data-ttu-id="8fa61-137">이제 `Index` 사용자에 게 폼을 표시 하는 뷰를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-137">Now you can update the `Index` view that will display the form to the user.</span></span>

<span data-ttu-id="8fa61-138">응용 프로그램을 실행 하 고 */Movies/Index*로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-138">Run the application and navigate to */Movies/Index*.</span></span> <span data-ttu-id="8fa61-139">쿼리 문자열(예: `?searchString=ghost`)을 URL에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-139">Append a query string such as `?searchString=ghost` to the URL.</span></span> <span data-ttu-id="8fa61-140">필터링된 영화가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-140">The filtered movies are displayed.</span></span>

![SearchQryStr](adding-search/_static/image1.png)

<span data-ttu-id="8fa61-142">`Index`이라는 매개 변수를 포함 하도록 메서드의 시그니처를 변경 하는 경우 `id` `id` 매개 변수는 `{id}` *App \_ Start\RouteConfig.cs* 파일에 설정 된 기본 경로에 대 한 자리 표시자와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-142">If you change the signature of the `Index` method to have a parameter named `id`, the `id` parameter will match the `{id}` placeholder for the default routes set in the *App\_Start\RouteConfig.cs* file.</span></span>

[!code-json[Main](adding-search/samples/sample4.txt)]

<span data-ttu-id="8fa61-143">원래 메서드는 다음과 같습니다 `Index` .</span><span class="sxs-lookup"><span data-stu-id="8fa61-143">The original `Index` method looks like this::</span></span>

[!code-csharp[Main](adding-search/samples/sample5.cs)]

<span data-ttu-id="8fa61-144">수정 된 메서드는 다음과 같습니다 `Index` .</span><span class="sxs-lookup"><span data-stu-id="8fa61-144">The modified `Index` method would look as follows:</span></span>

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

<span data-ttu-id="8fa61-145">이제 쿼리 문자열 값 대신 경로 데이터(URL 세그먼트)로 검색 제목을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-145">You can now pass the search title as route data (a URL segment) instead of as a query string value.</span></span>

![](adding-search/_static/image2.png)

<span data-ttu-id="8fa61-146">그러나 사용자가 영화를 검색하려고 할 때마다 URL을 수정하리라고 기대하지는 않을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-146">However, you can't expect users to modify the URL every time they want to search for a movie.</span></span> <span data-ttu-id="8fa61-147">따라서 이제 영화를 필터링하는 데 도움이 되는 UI를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-147">So now you'll add UI to help them filter movies.</span></span> <span data-ttu-id="8fa61-148">메서드의 서명을 변경 하 여 `Index` 경로 바인딩된 ID 매개 변수를 전달 하는 방법을 테스트 하는 경우 `Index` 메서드가 라는 문자열 매개 변수를 사용 하도록 다시 변경 합니다 `searchString` .</span><span class="sxs-lookup"><span data-stu-id="8fa61-148">If you changed the signature of the `Index` method to test how to pass the route-bound ID parameter, change it back so that your `Index` method takes a string parameter named `searchString`:</span></span>

[!code-csharp[Main](adding-search/samples/sample7.cs)]

<span data-ttu-id="8fa61-149">*Views\Movies\Index.cshtml* 파일을 열고 바로 뒤에 `@Html.ActionLink("Create New", "Create")` 아래에 강조 표시 된 폼 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-149">Open the *Views\Movies\Index.cshtml* file, and just after `@Html.ActionLink("Create New", "Create")`, add the form markup highlighted below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

<span data-ttu-id="8fa61-150">`Html.BeginForm`도우미는 여는 태그를 만듭니다 `<form>` .</span><span class="sxs-lookup"><span data-stu-id="8fa61-150">The `Html.BeginForm` helper creates an opening `<form>` tag.</span></span> <span data-ttu-id="8fa61-151">도우미를 사용 하면 `Html.BeginForm` 사용자가 **필터** 단추를 클릭 하 여 양식을 전송할 때 폼이 자신에 게 게시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-151">The `Html.BeginForm` helper causes the form to post to itself when the user submits the form by clicking the **Filter** button.</span></span>

<span data-ttu-id="8fa61-152">Visual Studio 2013 보기 파일을 표시 하 고 편집할 때 향상 된 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-152">Visual Studio 2013 has a nice improvement when displaying and editing View files.</span></span> <span data-ttu-id="8fa61-153">뷰 파일이 열려 있는 상태에서 응용 프로그램을 실행 하면 Visual Studio 2013 올바른 컨트롤러 작업 메서드를 호출 하 여 뷰를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-153">When you run the application with a view file open, Visual Studio 2013 invokes the correct controller action method to display the view.</span></span>

![](adding-search/_static/image3.png)

<span data-ttu-id="8fa61-154">위의 이미지에 표시 된 것 처럼 Visual Studio에서 인덱스 뷰가 열린 상태에서 Ctr F5 또는 F5 키를 눌러 응용 프로그램을 실행 한 다음 영화 검색을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-154">With the Index view open in Visual Studio (as shown in the image above), tap Ctr F5 or F5 to run the application and then try searching for a movie.</span></span>

![](adding-search/_static/image4.png)

<span data-ttu-id="8fa61-155">`HttpPost`메서드의 오버 로드가 없습니다 `Index` .</span><span class="sxs-lookup"><span data-stu-id="8fa61-155">There's no `HttpPost` overload of the `Index` method.</span></span> <span data-ttu-id="8fa61-156">메서드가 응용 프로그램의 상태를 변경 하는 것이 아니라 데이터만 필터링 하기 때문에 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-156">You don't need it, because the method isn't changing the state of the application, just filtering data.</span></span>

<span data-ttu-id="8fa61-157">다음 `HttpPost Index` 메서드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-157">You could add the following `HttpPost Index` method.</span></span> <span data-ttu-id="8fa61-158">이 경우 작업 호출자는 `HttpPost Index` 메서드와 일치 하 고 `HttpPost Index` 메서드는 아래 이미지와 같이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-158">In that case, the action invoker would match the `HttpPost Index` method, and the `HttpPost Index` method would run as shown in the image below.</span></span>

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![SearchPostGhost](adding-search/_static/image5.png)

<span data-ttu-id="8fa61-160">그러나 이 `HttpPost` 버전의 `Index` 메서드를 추가하는 경우에도 이를 모두 구현하는 방법은 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-160">However, even if you add this `HttpPost` version of the `Index` method, there's a limitation in how this has all been implemented.</span></span> <span data-ttu-id="8fa61-161">특정 검색을 책갈피로 설정하거나 동일하게 필터링된 영화 목록을 보기 위해 클릭할 수 있는 링크를 친구에게 보내려고 한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-161">Imagine that you want to bookmark a particular search or you want to send a link to friends that they can click in order to see the same filtered list of movies.</span></span> <span data-ttu-id="8fa61-162">HTTP POST 요청에 대 한 URL은 GET 요청 (localhost: xxxxx/영화/인덱스)의 URL과 동일 합니다. URL 자체에는 검색 정보가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-162">Notice that the URL for the HTTP POST request is the same as the URL for the GET request (localhost:xxxxx/Movies/Index) -- there's no search information in the URL itself.</span></span> <span data-ttu-id="8fa61-163">지금은 검색 문자열 정보가 양식 필드 값으로 서버에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-163">Right now, the search string information is sent to the server as a form field value.</span></span> <span data-ttu-id="8fa61-164">즉, 책갈피에 대 한 검색 정보를 캡처하거나 URL의 친구에 게 보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-164">This means you can't capture that search information to bookmark or send to friends in a URL.</span></span>

<span data-ttu-id="8fa61-165">이 솔루션은 `BeginForm` POST 요청에서 검색 정보를 URL에 추가 하 고이를 메서드 버전으로 라우팅해야 함을 지정 하는의 오버 로드를 사용 하는 것입니다 `HttpGet` `Index` .</span><span class="sxs-lookup"><span data-stu-id="8fa61-165">The solution is to use an overload of `BeginForm` that specifies that the POST request should add the search information to the URL and that it should be routed to the `HttpGet` version of the `Index` method.</span></span> <span data-ttu-id="8fa61-166">매개 변수가 없는 기존 `BeginForm` 메서드를 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-166">Replace the existing parameterless `BeginForm` method with the following markup:</span></span>

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

<span data-ttu-id="8fa61-168">이제 검색을 제출할 때 URL에 검색 쿼리 문자열이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-168">Now when you submit a search, the URL contains a search query string.</span></span> <span data-ttu-id="8fa61-169">`HttpPost Index` 메서드가 존재하더라도 검색은 `HttpGet Index` 작업 메서드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-169">Searching will also go to the `HttpGet Index` action method, even if you have a `HttpPost Index` method.</span></span>

![IndexWithGetURL](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a><span data-ttu-id="8fa61-171">장르 별 검색 추가</span><span class="sxs-lookup"><span data-stu-id="8fa61-171">Adding Search by Genre</span></span>

<span data-ttu-id="8fa61-172">`HttpPost`메서드 버전을 추가한 경우 `Index` 지금 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-172">If you added the `HttpPost` version of the `Index` method, delete it now.</span></span>

<span data-ttu-id="8fa61-173">다음으로, 사용자가 장르로 영화를 검색할 수 있는 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-173">Next, you'll add a feature to let users search for movies by genre.</span></span> <span data-ttu-id="8fa61-174">`Index` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-174">Replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample11.cs)]

<span data-ttu-id="8fa61-175">이 버전의 `Index` 메서드는 추가 매개 변수를 사용 `movieGenre` 합니다. 즉,</span><span class="sxs-lookup"><span data-stu-id="8fa61-175">This version of the `Index` method takes an additional parameter, namely `movieGenre`.</span></span> <span data-ttu-id="8fa61-176">코드의 처음 몇 줄은 개체를 만들어 `List` 데이터베이스에서 영화 장르를 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-176">The first few lines of code create a `List` object to hold movie genres from the database.</span></span>

<span data-ttu-id="8fa61-177">다음 코드는 데이터베이스에서 모든 장르를 검색하는 LINQ 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-177">The following code is a LINQ query that retrieves all the genres from the database.</span></span>

[!code-csharp[Main](adding-search/samples/sample12.cs)]

<span data-ttu-id="8fa61-178">코드는 `AddRange` 제네릭 컬렉션의 메서드를 사용 하 여 `List` 모든 고유 장르를 목록에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-178">The code uses the `AddRange` method of the generic `List` collection to add all the distinct genres to the list.</span></span> <span data-ttu-id="8fa61-179">한정자를 사용 하지 않고 `Distinct` 중복 장르를 추가 합니다. 예를 들어 코미디는 샘플에서 두 번 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-179">(Without the `Distinct` modifier, duplicate genres would be added — for example, comedy would be added twice in our sample).</span></span> <span data-ttu-id="8fa61-180">그런 다음 코드는 장르 목록을 개체에 저장 합니다 `ViewBag.MovieGenre` .</span><span class="sxs-lookup"><span data-stu-id="8fa61-180">The code then stores the list of genres in the `ViewBag.MovieGenre` object.</span></span> <span data-ttu-id="8fa61-181">에서 범주 데이터 (예: 영화 장르)를 [selectlist](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) 개체로 저장 `ViewBag` 한 다음 드롭다운 목록 상자에서 범주 데이터에 액세스 하는 것은 MVC 응용 프로그램에 대 한 일반적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-181">Storing category data (such a movie genres) as a [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) object in a `ViewBag`, then accessing the category data in a dropdown list box is a typical approach for MVC applications.</span></span>

<span data-ttu-id="8fa61-182">다음 코드에서는 매개 변수를 확인 하는 방법을 보여 줍니다 `movieGenre` .</span><span class="sxs-lookup"><span data-stu-id="8fa61-182">The following code shows how to check the `movieGenre` parameter.</span></span> <span data-ttu-id="8fa61-183">비어 있지 않은 경우 코드는 선택한 영화를 지정 된 장르로 제한 하도록 동영상 쿼리를 추가로 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-183">If it's not empty, the code further constrains the movies query to limit the selected movies to the specified genre.</span></span>

[!code-csharp[Main](adding-search/samples/sample13.cs)]

<span data-ttu-id="8fa61-184">앞에서 설명한 것 처럼, 작업 메서드가 반환 된 후 보기에서 발생 하는 동영상 목록이 반복 될 때까지 데이터베이스에서 쿼리가 실행 되지 않습니다 `Index` .</span><span class="sxs-lookup"><span data-stu-id="8fa61-184">As stated previously, the query is not run on the database until the movie list is iterated over (which happens in the View, after the `Index` action method returns).</span></span>

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a><span data-ttu-id="8fa61-185">장르 검색을 지원 하기 위해 인덱스 뷰에 태그 추가</span><span class="sxs-lookup"><span data-stu-id="8fa61-185">Adding Markup to the Index View to Support Search by Genre</span></span>

<span data-ttu-id="8fa61-186">도우미 `Html.DropDownList` 바로 앞에 *Views\Movies\Index.cshtml* 파일에 도우미를 추가 `TextBox` 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-186">Add an `Html.DropDownList` helper to the *Views\Movies\Index.cshtml* file, just before the `TextBox` helper.</span></span> <span data-ttu-id="8fa61-187">완성 된 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-187">The completed markup is shown below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

<span data-ttu-id="8fa61-188">다음 코드에서:</span><span class="sxs-lookup"><span data-stu-id="8fa61-188">In the following code:</span></span>

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

<span data-ttu-id="8fa61-189">"MovieGenre" 매개 변수는 `DropDownList` 도우미가에서을 찾을 수 있는 키를 제공 합니다 `IEnumerable<SelectListItem>` `ViewBag` .</span><span class="sxs-lookup"><span data-stu-id="8fa61-189">The parameter "MovieGenre" provides the key for the `DropDownList` helper to find a `IEnumerable<SelectListItem>` in the `ViewBag`.</span></span> <span data-ttu-id="8fa61-190">`ViewBag`작업 메서드에서가 입력 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-190">The `ViewBag` was populated in the action method:</span></span>

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

<span data-ttu-id="8fa61-191">"All" 매개 변수는 옵션 레이블을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-191">The parameter "All" provides an option label.</span></span> <span data-ttu-id="8fa61-192">브라우저에서 해당 선택을 검사 하면 해당 "value" 특성이 비어 있는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-192">If you inspect that choice in your browser, you'll see that its "value" attribute is empty.</span></span> <span data-ttu-id="8fa61-193">컨트롤러는 문자열을 필터링 `if` 하거나 비어 있지 않으므로 `null` 에 대해 빈 값을 제출 하면 `movieGenre` 모든 장르를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-193">Since our controller only filters `if` the string is not `null` or empty, submitting an empty value for `movieGenre` shows all genres.</span></span>

<span data-ttu-id="8fa61-194">옵션이 기본적으로 선택 되도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-194">You can also set an option to be selected by default.</span></span> <span data-ttu-id="8fa61-195">기본 옵션으로 "코미디"을 원하는 경우 컨트롤러의 코드를 다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-195">If you wanted "Comedy" as your default option, you would change the code in the Controller like so:</span></span>

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

<span data-ttu-id="8fa61-196">응용 프로그램을 실행 하 고 */Movies/Index*로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-196">Run the application and browse to */Movies/Index*.</span></span> <span data-ttu-id="8fa61-197">장르, 영화 이름 및 두 조건에 따라 검색을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-197">Try a search by genre, by movie name, and by both criteria.</span></span>

![](adding-search/_static/image8.png)

<span data-ttu-id="8fa61-198">이 섹션에서는 사용자가 영화 제목 및 장르로 검색할 수 있는 검색 작업 메서드 및 보기를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-198">In this section you created a search action method and view that let users search by movie title and genre.</span></span> <span data-ttu-id="8fa61-199">다음 섹션에서는 모델에 속성을 추가 하는 방법 `Movie` 및 테스트 데이터베이스를 자동으로 만드는 이니셜라이저를 추가 하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="8fa61-199">In the next section, you'll look at how to add a property to the `Movie` model and how to add an initializer that will automatically create a test database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8fa61-200">[이전](examining-the-edit-methods-and-edit-view.md)
> [다음](adding-a-new-field.md)</span><span class="sxs-lookup"><span data-stu-id="8fa61-200">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-a-new-field.md)</span></span>
