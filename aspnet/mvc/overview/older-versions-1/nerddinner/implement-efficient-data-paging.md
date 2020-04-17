---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 효율적인 데이터 페이징 구현 | 마이크로 소프트 문서
author: rick-anderson
description: 8 단계는 한 번에 1000 s 의 저녁 식사를 표시하는 대신 10 개의 예정된 저녁 식사만 표시할 수 있도록 / Dinners URL에 페이징 지원을 추가하는 방법을 보여줍니다...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: a833553fe44b62b136f7eb55c7e00eca0b0462c6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541327"
---
# <a name="implement-efficient-data-paging"></a><span data-ttu-id="ac8c3-103">효율적인 데이터 페이징 구현</span><span class="sxs-lookup"><span data-stu-id="ac8c3-103">Implement Efficient Data Paging</span></span>

<span data-ttu-id="ac8c3-104">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ac8c3-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="ac8c3-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="ac8c3-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="ac8c3-106">이것은 MVC 1을 ASP.NET 사용하여 작지만 완전한 웹 응용 프로그램을 빌드하는 방법을 안내하는 무료 ["NerdDinner" 응용 프로그램 자습서의](introducing-the-nerddinner-tutorial.md) 8단계입니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-106">This is step 8 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="ac8c3-107">8단계는 한 번에 1000s의 저녁 식사만 표시하는 대신 한 번에 10개의 예정된 저녁 식사만 표시하고 최종 사용자가 SEO 친화적인 방식으로 전체 목록을 앞뒤로 페이지올릴 수 있도록/Dinners URL에 페이징 지원을 추가하는 방법을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-107">Step 8 shows how to add paging support to our /Dinners URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>
> 
> <span data-ttu-id="ac8c3-108">MVC 3을 ASP.NET 사용하는 경우 [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC 뮤직 스토어](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-8-paging-support"></a><span data-ttu-id="ac8c3-109">얼간이 디너 단계 8: 페이징 지원</span><span class="sxs-lookup"><span data-stu-id="ac8c3-109">NerdDinner Step 8: Paging Support</span></span>

<span data-ttu-id="ac8c3-110">우리의 사이트가 성공하면, 그것은 곧 저녁 식사의 수천을해야합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-110">If our site is successful, it will have thousands of upcoming dinners.</span></span> <span data-ttu-id="ac8c3-111">이러한 모든 저녁 식사를 처리 하도록 UI 확장 하 고 사용자가 그들을 찾아볼 수 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-111">We need to make sure that our UI scales to handle all of these dinners, and allows users to browse them.</span></span> <span data-ttu-id="ac8c3-112">이를 위해 */Dinners* URL에 페이징 지원을 추가하여 한 번에 1000s의 저녁 식사만 표시하고 최종 사용자가 SEO 친화적 인 방식으로 전체 목록을 앞뒤로 페이지 올릴 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-112">To enable this, we'll add paging support to our */Dinners* URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>

### <a name="index-action-method-recap"></a><span data-ttu-id="ac8c3-113">인덱스() 작업 메서드 요약</span><span class="sxs-lookup"><span data-stu-id="ac8c3-113">Index() Action Method Recap</span></span>

<span data-ttu-id="ac8c3-114">DinnersController 클래스 내의 Index() 작업 메서드는 현재 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-114">The Index() action method within our DinnersController class currently looks like below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

<span data-ttu-id="ac8c3-115">*/Dinners* URL에 대한 요청이 이루어지면 예정된 모든 저녁 식사 목록을 검색한 다음 모든 저녁 식사 목록을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-115">When a request is made to the */Dinners* URL, it retrieves a list of all upcoming dinners and then renders a listing of all of them out:</span></span>

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a><span data-ttu-id="ac8c3-116">IQueryable&lt;T 이해&gt;</span><span class="sxs-lookup"><span data-stu-id="ac8c3-116">Understanding IQueryable&lt;T&gt;</span></span>

<span data-ttu-id="ac8c3-117">*IQueryable&lt;&gt; T는* .NET 3.5의 일부로 LINQ와 함께 도입된 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-117">*IQueryable&lt;T&gt;* is an interface that was introduced with LINQ as part of .NET 3.5.</span></span> <span data-ttu-id="ac8c3-118">페이징 지원을 구현하는 데 활용할 수 있는 강력한 "연기된 실행" 시나리오를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-118">It enables powerful "deferred execution" scenarios that we can take advantage of to implement paging support.</span></span>

<span data-ttu-id="ac8c3-119">우리의 DinnerRepository에서 우리는 우리의 FindUpcomingDinners () 방법에서 IQueryable&lt;저녁 식사&gt; 시퀀스를 반환합니다 :</span><span class="sxs-lookup"><span data-stu-id="ac8c3-119">In our DinnerRepository we are returning an IQueryable&lt;Dinner&gt; sequence from our FindUpcomingDinners() method:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

<span data-ttu-id="ac8c3-120">FindUpcomingDinners() 메서드에서 반환된 IQueryable&lt;Dinner&gt; 개체는 LINQ를 사용하여 데이터베이스에서 SQL로 Dinner 개체를 검색하는 쿼리를 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-120">The IQueryable&lt;Dinner&gt; object returned by our FindUpcomingDinners() method encapsulates a query to retrieve Dinner objects from our database using LINQ to SQL.</span></span> <span data-ttu-id="ac8c3-121">중요한 것은 쿼리의 데이터에 액세스/반복을 시도하거나 ToList() 메서드를 호출할 때까지 데이터베이스에 대한 쿼리를 실행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-121">Importantly, it won't execute the query against the database until we attempt to access/iterate over the data in the query, or until we call the ToList() method on it.</span></span> <span data-ttu-id="ac8c3-122">FindUpcomingDinners() 메서드를 호출 하는 코드는 쿼리 가능한&lt;Dinner&gt; 쿼리 를 실행 하기 전에 추가 "체인" 작업/필터를 추가 하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-122">The code calling our FindUpcomingDinners() method can optionally choose to add additional "chained" operations/filters to the IQueryable&lt;Dinner&gt; object before executing the query.</span></span> <span data-ttu-id="ac8c3-123">그런 다음 LINQ에서 SQL로 는 데이터가 요청될 때 데이터베이스에 대해 결합된 쿼리를 실행할 수 있을 만큼 스마트합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-123">LINQ to SQL is then smart enough to execute the combined query against the database when the data is requested.</span></span>

<span data-ttu-id="ac8c3-124">페이징 논리를 구현하기 위해 ToList()를 호출하기 전에 반환된 IQueryable&lt;Dinner&gt; 시퀀스에 추가 "건너뛰기" 및 "Take" 연산자가 적용되도록 DinnersController의 Index() 작업 메서드를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-124">To implement paging logic we can update our DinnersController's Index() action method so that it applies additional "Skip" and "Take" operators to the returned IQueryable&lt;Dinner&gt; sequence before calling ToList() on it:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

<span data-ttu-id="ac8c3-125">위의 코드는 데이터베이스에서 예정된 첫 번째 10개의 저녁 식사를 건너뛰고 20개의 저녁 식사를 다시 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-125">The above code skips over the first 10 upcoming dinners in the database, and then returns back 20 dinners.</span></span> <span data-ttu-id="ac8c3-126">LINQ to SQL은 웹 서버가 아닌 SQL 데이터베이스에서 이 건너뛰는 논리를 수행하는 최적화된 SQL 쿼리를 생성할 수 있을 만큼 똑똑합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-126">LINQ to SQL is smart enough to construct an optimized SQL query that performs this skipping logic in the SQL database – and not in the web-server.</span></span> <span data-ttu-id="ac8c3-127">즉, 데이터베이스에 수백만 개의 예정된 Dinners가 있더라도 이 요청의 일부로 원하는 10개만 검색됩니다(효율적이고 확장 가능).</span><span class="sxs-lookup"><span data-stu-id="ac8c3-127">This means that even if we have millions of upcoming Dinners in the database, only the 10 we want will be retrieved as part of this request (making it efficient and scalable).</span></span>

### <a name="adding-a-page-value-to-the-url"></a><span data-ttu-id="ac8c3-128">URL에 '페이지' 값 추가</span><span class="sxs-lookup"><span data-stu-id="ac8c3-128">Adding a "page" value to the URL</span></span>

<span data-ttu-id="ac8c3-129">특정 페이지 범위를 하드 코딩하는 대신 URL에 사용자가 요청하는 Dinner 범위를 나타내는 "페이지" 매개변수를 포함하도록 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-129">Instead of hard-coding a specific page range, we'll want our URLs to include a "page" parameter that indicates which Dinner range a user is requesting.</span></span>

#### <a name="using-a-querystring-value"></a><span data-ttu-id="ac8c3-130">쿼리 문자열 값 사용</span><span class="sxs-lookup"><span data-stu-id="ac8c3-130">Using a Querystring value</span></span>

<span data-ttu-id="ac8c3-131">아래 코드는 쿼리 문자열 매개 변수를 지원하고 */Dinners?page=2와*같은 URL을 사용하도록 설정하기 위해 Index() 작업 메서드를 업데이트하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-131">The code below demonstrates how we can update our Index() action method to support a querystring parameter and enable URLs like */Dinners?page=2*:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

<span data-ttu-id="ac8c3-132">위의 Index() 작업 메서드에는 "page"라는 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-132">The Index() action method above has a parameter named "page".</span></span> <span data-ttu-id="ac8c3-133">매개 변수는 nullable 정수로 선언됩니다(int?</span><span class="sxs-lookup"><span data-stu-id="ac8c3-133">The parameter is declared as a nullable integer (that is what int? indicates).</span></span> <span data-ttu-id="ac8c3-134">즉, */Dinners?page=2* URL은 "2"의 값을 매개 변수 값으로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-134">This means that the */Dinners?page=2* URL will cause a value of "2" to be passed as the parameter value.</span></span> <span data-ttu-id="ac8c3-135">*/Dinners* URL(쿼리 문자열 값 제외)은 null 값을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-135">The */Dinners* URL (without a querystring value) will cause a null value to be passed.</span></span>

<span data-ttu-id="ac8c3-136">페이지 값에 페이지 크기(이 경우 10행)를 곱하여 건너뛸 저녁 식사 수를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-136">We are multiplying the page value by the page size (in this case 10 rows) to determine how many dinners to skip over.</span></span> <span data-ttu-id="ac8c3-137">null 형식을 처리할 때 유용한 [C# null "병합" 연산자(??)를](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-137">We are using the [C# null "coalescing" operator (??)](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) which is useful when dealing with nullable types.</span></span> <span data-ttu-id="ac8c3-138">위의 코드는 페이지 매개 변수가 null인 경우 페이지 값을 0으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-138">The code above assigns page the value of 0 if the page parameter is null.</span></span>

#### <a name="using-embedded-url-values"></a><span data-ttu-id="ac8c3-139">포함된 URL 값 사용</span><span class="sxs-lookup"><span data-stu-id="ac8c3-139">Using Embedded URL values</span></span>

<span data-ttu-id="ac8c3-140">쿼리 문자열 값을 사용하는 대신 실제 URL 자체에 페이지 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-140">An alternative to using a querystring value would be to embed the page parameter within the actual URL itself.</span></span> <span data-ttu-id="ac8c3-141">예: */Dinners/Page/2* 또는 */Dinners/2*.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-141">For example: */Dinners/Page/2* or */Dinners/2*.</span></span> <span data-ttu-id="ac8c3-142">ASP.NET MVC에는 이와 같은 시나리오를 쉽게 지원할 수 있는 강력한 URL 라우팅 엔진이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-142">ASP.NET MVC includes a powerful URL routing engine that makes it easy to support scenarios like this.</span></span>

<span data-ttu-id="ac8c3-143">들어오는 URL 또는 URL 형식을 원하는 컨트롤러 클래스 또는 작업 메서드에 매핑하는 사용자 지정 라우팅 규칙을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-143">We can register custom routing rules that map any incoming URL or URL format to any controller class or action method we want.</span></span> <span data-ttu-id="ac8c3-144">프로젝트 내에서 Global.asax 파일을 열기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-144">All we need to-do is to open the Global.asax file within our project:</span></span>

![](implement-efficient-data-paging/_static/image2.png)

<span data-ttu-id="ac8c3-145">그런 다음 라우트에 대한 첫 번째 호출과 같은 MapRoute() 도우미 메서드를 사용하여 새 매핑 규칙을 등록합니다. 지도 경로() 아래:</span><span class="sxs-lookup"><span data-stu-id="ac8c3-145">And then register a new mapping rule using the MapRoute() helper method like the first call to routes.MapRoute() below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

<span data-ttu-id="ac8c3-146">위에서는 "예정된 저녁 식사"라는 새 라우팅 규칙을 등록하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-146">Above we are registering a new routing rule named "UpcomingDinners".</span></span> <span data-ttu-id="ac8c3-147">{page}가 URL 내에 포함된 매개 변수 값인 URL 형식 "Dinners/Page/{page}"가 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-147">We are indicating it has the URL format "Dinners/Page/{page}" – where {page} is a parameter value embedded within the URL.</span></span> <span data-ttu-id="ac8c3-148">MapRoute() 메서드에 대한 세 번째 매개 변수는 이 형식과 일치하는 URL을 DinnersController 클래스의 Index() 작업 메서드에 매핑해야 한다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-148">The third parameter to the MapRoute() method indicates that we should map URLs that match this format to the Index() action method on the DinnersController class.</span></span>

<span data-ttu-id="ac8c3-149">쿼리 문자열 시나리오와 함께 이전에 사용했던 것과 동일한 Index() 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-149">We can use the exact same Index() code we had before with our Querystring scenario – except now our "page" parameter will come from the URL and not the querystring:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

<span data-ttu-id="ac8c3-150">이제 응용 프로그램을 실행하고 */Dinners를* 입력하면 첫 번째 10 개의 예정된 저녁 식사가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-150">And now when we run the application and type in */Dinners* we'll see the first 10 upcoming dinners:</span></span>

![](implement-efficient-data-paging/_static/image3.png)

<span data-ttu-id="ac8c3-151">그리고 *우리가 /Dinners/Page/1에* 입력하면 다음 저녁 식사 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-151">And when we type in */Dinners/Page/1* we'll see the next page of dinners:</span></span>

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a><span data-ttu-id="ac8c3-152">페이지 탐색 UI 추가</span><span class="sxs-lookup"><span data-stu-id="ac8c3-152">Adding page navigation UI</span></span>

<span data-ttu-id="ac8c3-153">페이징 시나리오를 완료하는 마지막 단계는 사용자가 Dinner 데이터를 쉽게 건너뛸 수 있도록 보기 템플릿 내에서 "다음" 및 "이전" 탐색 UI를 구현하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-153">The last step to complete our paging scenario will be to implement "next" and "previous" navigation UI within our view template to enable users to easily skip over the Dinner data.</span></span>

<span data-ttu-id="ac8c3-154">이를 올바르게 구현하려면 데이터베이스의 총 Dinners 수와 이로 변환되는 데이터의 페이지 수를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-154">To implement this correctly, we'll need to know the total number of Dinners in the database, as well as how many pages of data this translates to.</span></span> <span data-ttu-id="ac8c3-155">그런 다음 현재 요청된 "페이지" 값이 데이터의 시작 또는 끝에 있는지 여부를 계산하고 그에 따라 "이전" 및 "다음" UI를 표시하거나 숨겨야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-155">We'll then need to calculate whether the currently requested "page" value is at the beginning or end of the data, and show or hide the "previous" and "next" UI accordingly.</span></span> <span data-ttu-id="ac8c3-156">이 논리를 Index() 작업 메서드 내에서 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-156">We could implement this logic within our Index() action method.</span></span> <span data-ttu-id="ac8c3-157">또는 이 논리를 보다 재사용 가능한 방식으로 캡슐화하는 도우미 클래스를 프로젝트에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-157">Alternatively we can add a helper class to our project that encapsulates this logic in a more re-usable way.</span></span>

<span data-ttu-id="ac8c3-158">다음은 .NET Framework에 내장된 List&lt;T&gt; 컬렉션 클래스에서 파생된 간단한 "PaginatedList" 도우미 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-158">Below is a simple "PaginatedList" helper class that derives from the List&lt;T&gt; collection class built-into the .NET Framework.</span></span> <span data-ttu-id="ac8c3-159">IQueryable 데이터의 모든 시퀀스를 페이지트하는 데 사용할 수 있는 다시 사용할 수 있는 컬렉션 클래스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-159">It implements a re-usable collection class that can be used to paginate any sequence of IQueryable data.</span></span> <span data-ttu-id="ac8c3-160">NerdDinner 응용 프로그램에서는&lt;IQueryable Dinner&gt; 결과에 대해 작업을 수행하지만 IQueryable 제품&lt;&gt; 또는 IQueryable&lt;고객&gt; 결과에 대해 다른 응용 프로그램 시나리오에서 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-160">In our NerdDinner application we'll have it work over IQueryable&lt;Dinner&gt; results, but it could just as easily be used against IQueryable&lt;Product&gt; or IQueryable&lt;Customer&gt; results in other application scenarios:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

<span data-ttu-id="ac8c3-161">위의 방법을 확인하여 "PageIndex", "PageSize", "TotalCount" 및 "TotalPage"와 같은 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-161">Notice above how it calculates and then exposes properties like "PageIndex", "PageSize", "TotalCount", and "TotalPages".</span></span> <span data-ttu-id="ac8c3-162">그런 다음 컬렉션의 데이터 페이지가 원래 시퀀스의 시작 또는 끝에 있는지 여부를 나타내는 두 개의 도우미 속성 "HasNextPage" 및 "HasNextPage"를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-162">It also then exposes two helper properties "HasPreviousPage" and "HasNextPage" that indicate whether the page of data in the collection is at the beginning or end of the original sequence.</span></span> <span data-ttu-id="ac8c3-163">위의 코드는 두 개의 SQL 쿼리를 실행합니다 - 첫 번째는 Dinner 개체의 총 수의 수를 검색하는 첫 번째 (이 개체를 반환하지 않습니다 - 오히려 정수를 반환하는 "SELECT COUNT"문을 수행함), 두 번째는 데이터의 현재 페이지에 대해 데이터베이스에서 필요한 데이터 행만 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-163">The above code will cause two SQL queries to be run - the first to retrieve the count of the total number of Dinner objects (this doesn't return the objects – rather it performs a "SELECT COUNT" statement that returns an integer), and the second to retrieve just the rows of data we need from our database for the current page of data.</span></span>

<span data-ttu-id="ac8c3-164">그런 다음 DinnersController.Index() 도우미 메서드를 업데이트하여 DinnerRepository.FindUpcomingDinners() 결과에서 PaginatedList&lt;저녁 식사를&gt; 만들고 뷰 템플릿으로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-164">We can then update our DinnersController.Index() helper method to create a PaginatedList&lt;Dinner&gt; from our DinnerRepository.FindUpcomingDinners() result, and pass it to our view template:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

<span data-ttu-id="ac8c3-165">그런 다음 ViewPage@Dinners\Index.aspx 보기 템플릿을 업데이트하여&lt;ViewPage IEnumerable&lt;&gt; &gt; &lt;&lt;Dinner 대신 ViewPage NerdDinner.Helpers.PaginatedList Dinner에서&gt;&gt;상속한 다음 뷰 템플릿 하단에 다음 코드를 추가하여 다음 및 이전 탐색 UI를 표시하거나 숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-165">We can then update the \Views\Dinners\Index.aspx view template to inherit from ViewPage&lt;NerdDinner.Helpers.PaginatedList&lt;Dinner&gt;&gt; instead of ViewPage&lt;IEnumerable&lt;Dinner&gt;&gt;, and then add the following code to the bottom of our view-template to show or hide next and previous navigation UI:</span></span>

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

<span data-ttu-id="ac8c3-166">위의 공지는 하이퍼링크를 생성하기 위해 Html.RouteLink() 도우미 메서드를 사용하는 방법에 대해 알아두습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-166">Notice above how we are using the Html.RouteLink() helper method to generate our hyperlinks.</span></span> <span data-ttu-id="ac8c3-167">이 메서드는 이전에 사용 했던 Html.ActionLink() 도우미 메서드와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-167">This method is similar to the Html.ActionLink() helper method we've used previously.</span></span> <span data-ttu-id="ac8c3-168">차이점은 Global.asax 파일 내에서 설정한 "예정된 Dinners" 라우팅 규칙을 사용하여 URL을 생성한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-168">The difference is that we are generating the URL using the "UpcomingDinners" routing rule we setup within our Global.asax file.</span></span> <span data-ttu-id="ac8c3-169">이렇게 하면 {page} 값이 현재 PageIndex를 기반으로 위에서 제공하는 변수인 Index() 작업 메서드에 *URL을 생성합니다.*</span><span class="sxs-lookup"><span data-stu-id="ac8c3-169">This ensures that we'll generate URLs to our Index() action method that have the format: */Dinners/Page/{page}* – where the {page} value is a variable we are providing above based on the current PageIndex.</span></span>

<span data-ttu-id="ac8c3-170">그리고 지금 우리가 우리의 응용 프로그램을 다시 실행할 때 우리는 우리의 브라우저에서 한 번에 10 저녁 식사를 볼 수 있습니다 :</span><span class="sxs-lookup"><span data-stu-id="ac8c3-170">And now when we run our application again we'll see 10 dinners at a time in our browser:</span></span>

![](implement-efficient-data-paging/_static/image5.png)

<span data-ttu-id="ac8c3-171">또한 페이지 &lt; &lt; &lt; &gt; &gt; &gt; 하단에 검색 엔진 액세스 URL을 사용하여 데이터를 앞뒤로 건너뛸 수 있는 탐색 UI가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-171">We also have &lt;&lt;&lt; and &gt;&gt;&gt; navigation UI at the bottom of the page that allows us to skip forwards and backwards over our data using search engine accessible URLs:</span></span>

![](implement-efficient-data-paging/_static/image6.png)

| <span data-ttu-id="ac8c3-172">**측면 주제: IQueryable&lt;T의 의미 이해&gt;**</span><span class="sxs-lookup"><span data-stu-id="ac8c3-172">**Side Topic: Understanding the implications of IQueryable&lt;T&gt;**</span></span> |
| --- |
| <span data-ttu-id="ac8c3-173">IQueryable&lt;&gt; T는 페이징 및 컴포지션 기반 쿼리와 같은 다양한 흥미로운 지연 된 실행 시나리오를 가능하게하는 매우 강력한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-173">IQueryable&lt;T&gt; is a very powerful feature that enables a variety of interesting deferred execution scenarios (like paging and composition based queries).</span></span> <span data-ttu-id="ac8c3-174">모든 강력한 기능과 마찬가지로, 당신은 당신이 그것을 사용하는 방법에주의하고 남용되지 않도록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-174">As with all powerful features, you want to be careful with how you use it and make sure it is not abused.</span></span> <span data-ttu-id="ac8c3-175">리포지토리에서 IQueryable&lt;T&gt; 결과를 반환하면 코드를 호출하여 연결된 연산자 메서드에 추가하여 궁극적인 쿼리 실행에 참여할 수 있음을 인식하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-175">It is important to recognize that returning an IQueryable&lt;T&gt; result from your repository enables calling code to append on chained operator methods to it, and so participate in the ultimate query execution.</span></span> <span data-ttu-id="ac8c3-176">이 기능을 호출 코드에 제공하지 않으려면 이미 실행된&lt;쿼리&gt; 의 결과를 포함하는&lt;&gt; IList T 또는 IEnumerable T 결과를 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-176">If you do not want to provide calling code this ability, then you should return back IList&lt;T&gt; or IEnumerable&lt;T&gt; results - which contain the results of a query that has already executed.</span></span> <span data-ttu-id="ac8c3-177">페이지 조정 시나리오의 경우 실제 데이터 페이지 해제 논리를 호출되는 리포지토리 메서드로 푸시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-177">For pagination scenarios this would require you to push the actual data pagination logic into the repository method being called.</span></span> <span data-ttu-id="ac8c3-178">이 시나리오에서는 FindUpcomingDinners() 파인더 메서드를 업데이트하여&lt; PaginatedList: PaginatedList Dinners(int&gt; pageIndex, int pageSize) { 또는 IList&lt;Dinner를&gt;반환하거나 "totalCount" 매개 변수를 사용하여 "totalCount" 매개&lt;&gt; 변수를 사용하여 총 페이지 인을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-178">In this scenario we might update our FindUpcomingDinners() finder method to have a signature that either returned a PaginatedList: PaginatedList&lt; Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize) { } Or return back an IList&lt;Dinner&gt;, and use a "totalCount" out param to return the total count of Dinners: IList&lt;Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize, out int totalCount) { }</span></span> |

### <a name="next-step"></a><span data-ttu-id="ac8c3-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ac8c3-179">Next Step</span></span>

<span data-ttu-id="ac8c3-180">이제 응용 프로그램에 인증 및 권한 부여 지원을 추가하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8c3-180">Let's now look at how we can add authentication and authorization support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ac8c3-181">[이전](re-use-ui-using-master-pages-and-partials.md)
> [다음](secure-applications-using-authentication-and-authorization.md)</span><span class="sxs-lookup"><span data-stu-id="ac8c3-181">[Previous](re-use-ui-using-master-pages-and-partials.md)
[Next](secure-applications-using-authentication-and-authorization.md)</span></span>
