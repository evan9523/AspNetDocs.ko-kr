---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: ASP.NET Web API 2에서 특성 라우팅을 사용 하 여 REST API 만들기 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: f6ff5fa18a44b3e6717ec0141ebe101bcdc0bee4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045184"
---
# <a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="64871-102">ASP.NET Web API 2에서 특성 라우팅을 사용 하 여 REST API 만들기</span><span class="sxs-lookup"><span data-stu-id="64871-102">Create a REST API with Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="64871-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="64871-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="64871-104">Web API 2는 *특성 라우팅*이라는 새로운 유형의 라우팅을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-104">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="64871-105">특성 라우팅에 대 한 일반적인 개요는 [WEB API 2에서 특성 라우팅](attribute-routing-in-web-api-2.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="64871-105">For a general overview of attribute routing, see [Attribute Routing in Web API 2](attribute-routing-in-web-api-2.md).</span></span> <span data-ttu-id="64871-106">이 자습서에서는 특성 라우팅을 사용 하 여 책 컬렉션에 대 한 REST API를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64871-106">In this tutorial, you will use attribute routing to create a REST API for a collection of books.</span></span> <span data-ttu-id="64871-107">API는 다음 작업을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-107">The API will support the following actions:</span></span>

| <span data-ttu-id="64871-108">작업</span><span class="sxs-lookup"><span data-stu-id="64871-108">Action</span></span> | <span data-ttu-id="64871-109">예제 URI</span><span class="sxs-lookup"><span data-stu-id="64871-109">Example URI</span></span> |
| --- | --- |
| <span data-ttu-id="64871-110">모든 책의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="64871-110">Get a list of all books.</span></span> | <span data-ttu-id="64871-111">/api/서적</span><span class="sxs-lookup"><span data-stu-id="64871-111">/api/books</span></span> |
| <span data-ttu-id="64871-112">ID 별로 책을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="64871-112">Get a book by ID.</span></span> | <span data-ttu-id="64871-113">/api/books/1</span><span class="sxs-lookup"><span data-stu-id="64871-113">/api/books/1</span></span> |
| <span data-ttu-id="64871-114">책의 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="64871-114">Get the details of a book.</span></span> | <span data-ttu-id="64871-115">/api/books/1/details</span><span class="sxs-lookup"><span data-stu-id="64871-115">/api/books/1/details</span></span> |
| <span data-ttu-id="64871-116">장르별로 책 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="64871-116">Get a list of books by genre.</span></span> | <span data-ttu-id="64871-117">/api/books/fantasy</span><span class="sxs-lookup"><span data-stu-id="64871-117">/api/books/fantasy</span></span> |
| <span data-ttu-id="64871-118">게시 날짜별로 책 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="64871-118">Get a list of books by publication date.</span></span> | <span data-ttu-id="64871-119">/api/books/date/2013-02-16/api/books/date/2013/02/16 (대체 양식)</span><span class="sxs-lookup"><span data-stu-id="64871-119">/api/books/date/2013-02-16 /api/books/date/2013/02/16 (alternate form)</span></span> |
| <span data-ttu-id="64871-120">특정 저자의 책 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="64871-120">Get a list of books by a particular author.</span></span> | <span data-ttu-id="64871-121">/api/authors/1/books</span><span class="sxs-lookup"><span data-stu-id="64871-121">/api/authors/1/books</span></span> |

<span data-ttu-id="64871-122">모든 메서드는 읽기 전용입니다 (HTTP GET 요청).</span><span class="sxs-lookup"><span data-stu-id="64871-122">All methods are read-only (HTTP GET requests).</span></span>

<span data-ttu-id="64871-123">데이터 계층의 경우 Entity Framework를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-123">For the data layer, we'll use Entity Framework.</span></span> <span data-ttu-id="64871-124">책 레코드에는 다음 필드가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64871-124">Book records will have the following fields:</span></span>

- <span data-ttu-id="64871-125">ID</span><span class="sxs-lookup"><span data-stu-id="64871-125">ID</span></span>
- <span data-ttu-id="64871-126">제목</span><span class="sxs-lookup"><span data-stu-id="64871-126">Title</span></span>
- <span data-ttu-id="64871-127">Genre</span><span class="sxs-lookup"><span data-stu-id="64871-127">Genre</span></span>
- <span data-ttu-id="64871-128">게시 날짜</span><span class="sxs-lookup"><span data-stu-id="64871-128">Publication date</span></span>
- <span data-ttu-id="64871-129">가격</span><span class="sxs-lookup"><span data-stu-id="64871-129">Price</span></span>
- <span data-ttu-id="64871-130">설명</span><span class="sxs-lookup"><span data-stu-id="64871-130">Description</span></span>
- <span data-ttu-id="64871-131">AuthorID (외래 키를 Authors 테이블로)</span><span class="sxs-lookup"><span data-stu-id="64871-131">AuthorID (foreign key to an Authors table)</span></span>

<span data-ttu-id="64871-132">그러나 대부분의 요청에서 API는이 데이터의 하위 집합 (제목, 저자 및 장르)을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-132">For most requests, however, the API will return a subset of this data (title, author, and genre).</span></span> <span data-ttu-id="64871-133">전체 레코드를 가져오기 위해 클라이언트는를 요청 `/api/books/{id}/details` 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-133">To get the complete record, the client requests `/api/books/{id}/details`.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64871-134">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="64871-134">Prerequisites</span></span>

<span data-ttu-id="64871-135">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional 또는 Enterprise edition입니다.</span><span class="sxs-lookup"><span data-stu-id="64871-135">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional or Enterprise edition.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="64871-136">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="64871-136">Create the Visual Studio Project</span></span>

<span data-ttu-id="64871-137">Visual Studio를 실행 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-137">Start by running Visual Studio.</span></span> <span data-ttu-id="64871-138">**파일** 메뉴에서 **새로 만들기**를 선택한 후 **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-138">From the **File** menu, select **New** and then select **Project**.</span></span>

<span data-ttu-id="64871-139">**설치 된**  >  **Visual c #** 범주를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-139">Expand the **Installed** > **Visual C#** category.</span></span> <span data-ttu-id="64871-140">**Visual c #** 에서 **웹**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-140">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="64871-141">프로젝트 템플릿 목록에서 **ASP.NET 웹 응용 프로그램 (.NET Framework)** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-141">In the list of project templates, select **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="64871-142">프로젝트 이름을 &quot; booksapi로 &quot; 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-142">Name the project &quot;BooksAPI&quot;.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

<span data-ttu-id="64871-143">**새 ASP.NET 웹 응용 프로그램** 대화 상자에서 **빈** 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-143">In the **New ASP.NET Web Application** dialog, select the **Empty** template.</span></span> <span data-ttu-id="64871-144">"에 대 한 폴더 및 핵심 참조 추가"에서 **WEB API** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-144">Under "Add folders and core references for", select the **Web API** checkbox.</span></span> <span data-ttu-id="64871-145">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-145">Click **OK**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

<span data-ttu-id="64871-146">이렇게 하면 Web API 기능에 대해 구성 된 기본 프로젝트가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64871-146">This creates a skeleton project that is configured for Web API functionality.</span></span>

### <a name="domain-models"></a><span data-ttu-id="64871-147">도메인 모델</span><span class="sxs-lookup"><span data-stu-id="64871-147">Domain Models</span></span>

<span data-ttu-id="64871-148">다음으로 도메인 모델에 대 한 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-148">Next, add classes for domain models.</span></span> <span data-ttu-id="64871-149">솔루션 탐색기에서 Models 폴더를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-149">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="64871-150">**추가**를 선택한 다음 **클래스**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-150">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="64871-151">클래스 `Author` 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-151">Name the class `Author`.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

<span data-ttu-id="64871-152">Author.cs의 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="64871-152">Replace the code in Author.cs with the following:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

<span data-ttu-id="64871-153">이제 라는 다른 클래스 `Book` 를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-153">Now add another class named `Book`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a><span data-ttu-id="64871-154">Web API 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="64871-154">Add a Web API Controller</span></span>

<span data-ttu-id="64871-155">이 단계에서는 Entity Framework를 데이터 계층으로 사용 하는 Web API 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-155">In this step, we'll add a Web API controller that uses Entity Framework as the data layer.</span></span>

<span data-ttu-id="64871-156">Ctrl+Shift+B를 눌러 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-156">Press CTRL+SHIFT+B to build the project.</span></span> <span data-ttu-id="64871-157">Entity Framework는 리플렉션을 사용 하 여 모델의 속성을 검색 하므로 데이터베이스 스키마를 만들기 위해 컴파일된 어셈블리가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-157">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

<span data-ttu-id="64871-158">솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-158">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="64871-159">**추가**를 선택한 다음 **컨트롤러**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-159">Select **Add**, then select **Controller**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

<span data-ttu-id="64871-160">**스 캐 폴드 추가** 대화 상자에서 **Entity Framework를 사용 하 여 웹 API 2 컨트롤러 (작업 포함**)를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-160">In the **Add Scaffold** dialog, select **Web API 2 Controller with actions, using Entity Framework**.</span></span>

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

<span data-ttu-id="64871-161">**컨트롤러 추가** 대화 상자에서 **컨트롤러 이름**에 &quot; bookscontroller를 입력 &quot; 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-161">In the **Add Controller** dialog, for **Controller name**, enter &quot;BooksController&quot;.</span></span> <span data-ttu-id="64871-162">&quot;비동기 컨트롤러 작업 사용 확인란을 선택 &quot; 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-162">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="64871-163">**모델 클래스**에 대해 Book을 선택 &quot; &quot; 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-163">For **Model class**, select &quot;Book&quot;.</span></span> <span data-ttu-id="64871-164">드롭다운에 나열 된 클래스가 표시 되지 않는 경우 `Book` 프로젝트를 빌드 했는지 확인 합니다. 그런 다음 "+" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-164">(If you don't see the `Book` class listed in the dropdown, make sure that you built the project.) Then click the "+" button.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

<span data-ttu-id="64871-165">**새 데이터 컨텍스트** 대화 상자에서 **추가** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-165">Click **Add** in the **New Data Context** dialog.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

<span data-ttu-id="64871-166">**컨트롤러 추가** 대화 상자에서 **추가** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-166">Click **Add** in the **Add Controller** dialog.</span></span> <span data-ttu-id="64871-167">스 캐 폴딩은 `BooksController` API 컨트롤러를 정의 하는 라는 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-167">The scaffolding adds a class named `BooksController` that defines the API controller.</span></span> <span data-ttu-id="64871-168">또한 `BooksAPIContext` Entity Framework의 데이터 컨텍스트를 정의 하는 모델 폴더에 라는 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-168">It also adds a class named `BooksAPIContext` in the Models folder, which defines the data context for Entity Framework.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a><span data-ttu-id="64871-169">데이터베이스 시드</span><span class="sxs-lookup"><span data-stu-id="64871-169">Seed the Database</span></span>

<span data-ttu-id="64871-170">도구 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-170">From the Tools menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span>

<span data-ttu-id="64871-171">패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-171">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

<span data-ttu-id="64871-172">이 명령은 마이그레이션 폴더를 만들고 Configuration.cs 라는 새 코드 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-172">This command creates a Migrations folder and adds a new code file named Configuration.cs.</span></span> <span data-ttu-id="64871-173">이 파일을 열고 다음 코드를 메서드에 추가 합니다 `Configuration.Seed` .</span><span class="sxs-lookup"><span data-stu-id="64871-173">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

<span data-ttu-id="64871-174">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-174">In the Package Manager Console window, type the following commands.</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

<span data-ttu-id="64871-175">이러한 명령은 로컬 데이터베이스를 만들고 초기값 메서드를 호출 하 여 데이터베이스를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="64871-175">These commands create a local database and invoke the Seed method to populate the database.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a><span data-ttu-id="64871-176">DTO 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="64871-176">Add DTO Classes</span></span>

<span data-ttu-id="64871-177">지금 응용 프로그램을 실행 하 고/api/books/1에 GET 요청을 보내면 응답이 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64871-177">If you run the application now and send a GET request to /api/books/1, the response looks similar to the following.</span></span> <span data-ttu-id="64871-178">(가독성을 위해 들여쓰기를 추가 했습니다.)</span><span class="sxs-lookup"><span data-stu-id="64871-178">(I added indentation for readability.)</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

<span data-ttu-id="64871-179">대신이 요청에서 필드의 하위 집합을 반환 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-179">Instead, I want this request to return a subset of the fields.</span></span> <span data-ttu-id="64871-180">작성자 ID 대신 작성자의 이름도 반환 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-180">Also, I want it to return the author's name, rather than the author ID.</span></span> <span data-ttu-id="64871-181">이를 위해 EF 모델 대신 DTO ( *데이터 전송 개체* )를 반환 하도록 컨트롤러 메서드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-181">To accomplish this, we'll modify the controller methods to return a *data transfer object* (DTO) instead of the EF model.</span></span> <span data-ttu-id="64871-182">DTO은 데이터를 전달 하기 위해 디자인 된 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="64871-182">A DTO is an object that is designed only to carry data.</span></span>

<span data-ttu-id="64871-183">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**  |  **새 폴더**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-183">In Solution Explorer, right-click the project and select **Add** | **New Folder**.</span></span> <span data-ttu-id="64871-184">폴더 이름을 &quot; dto로 &quot; 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-184">Name the folder &quot;DTOs&quot;.</span></span> <span data-ttu-id="64871-185">다음 정의를 사용 하 여 라는 클래스를 `BookDto` dto 폴더에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-185">Add a class named `BookDto` to the DTOs folder, with the following definition:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

<span data-ttu-id="64871-186">`BookDetailDto`(이)라는 다른 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-186">Add another class named `BookDetailDto`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

<span data-ttu-id="64871-187">그런 다음 인스턴스를 `BooksController` 반환 하도록 클래스를 업데이트 합니다 `BookDto` .</span><span class="sxs-lookup"><span data-stu-id="64871-187">Next, update the `BooksController` class to return `BookDto` instances.</span></span> <span data-ttu-id="64871-188">쿼리할 수 있는 [. Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) 메서드를 사용 하 여 인스턴스 `Book` 를 `BookDto` 인스턴스에 프로젝션 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-188">We'll use the [Queryable.Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) method to project `Book` instances to `BookDto` instances.</span></span> <span data-ttu-id="64871-189">컨트롤러 클래스에 대 한 업데이트 된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="64871-189">Here is the updated code for the controller class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> <span data-ttu-id="64871-190">`PutBook`, `PostBook` 및 `DeleteBook` 메서드는이 자습서에 필요 하지 않기 때문에 삭제 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="64871-190">I deleted the `PutBook`, `PostBook`, and `DeleteBook` methods, because they aren't needed for this tutorial.</span></span>

<span data-ttu-id="64871-191">이제 응용 프로그램을 실행 하 고/api/books/1를 요청 하면 응답 본문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="64871-191">Now if you run the application and request /api/books/1, the response body should look like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a><span data-ttu-id="64871-192">경로 특성 추가</span><span class="sxs-lookup"><span data-stu-id="64871-192">Add Route Attributes</span></span>

<span data-ttu-id="64871-193">다음으로, 특성 라우팅을 사용 하도록 컨트롤러를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-193">Next, we'll convert the controller to use attribute routing.</span></span> <span data-ttu-id="64871-194">먼저 컨트롤러에 **RoutePrefix** 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-194">First, add a **RoutePrefix** attribute to the controller.</span></span> <span data-ttu-id="64871-195">이 특성은이 컨트롤러의 모든 메서드에 대 한 초기 URI 세그먼트를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-195">This attribute defines the initial URI segments for all methods on this controller.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

<span data-ttu-id="64871-196">그런 다음 다음과 같이 **[Route]** 특성을 컨트롤러 작업에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-196">Then add **[Route]** attributes to the controller actions, as follows:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

<span data-ttu-id="64871-197">각 컨트롤러 메서드의 경로 템플릿은 접두사와 **경로** 특성에 지정 된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="64871-197">The route template for each controller method is the prefix plus the string specified in the **Route** attribute.</span></span> <span data-ttu-id="64871-198">메서드의 경우 `GetBook` 경로 템플릿에는 &quot; &quot; URI 세그먼트에 정수 값이 포함 된 경우와 일치 하는 매개 변수가 있는 문자열 {id: int}가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64871-198">For the `GetBook` method, the route template includes the parameterized string &quot;{id:int}&quot;, which matches if the URI segment contains an integer value.</span></span>

| <span data-ttu-id="64871-199">방법</span><span class="sxs-lookup"><span data-stu-id="64871-199">Method</span></span> | <span data-ttu-id="64871-200">경로 템플릿</span><span class="sxs-lookup"><span data-stu-id="64871-200">Route Template</span></span> | <span data-ttu-id="64871-201">예제 URI</span><span class="sxs-lookup"><span data-stu-id="64871-201">Example URI</span></span> |
| --- | --- | --- |
| `GetBooks` | <span data-ttu-id="64871-202">"api/서적"</span><span class="sxs-lookup"><span data-stu-id="64871-202">"api/books"</span></span> | `http://localhost/api/books` |
| `GetBook` | <span data-ttu-id="64871-203">"api/books/{id: int}"</span><span class="sxs-lookup"><span data-stu-id="64871-203">"api/books/{id:int}"</span></span> | `http://localhost/api/books/5` |

## <a name="get-book-details"></a><span data-ttu-id="64871-204">책 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="64871-204">Get Book Details</span></span>

<span data-ttu-id="64871-205">책 정보를 얻기 위해 클라이언트는에 GET 요청을 보냅니다 `/api/books/{id}/details` . 여기서 *{id}* 는 책의 id입니다.</span><span class="sxs-lookup"><span data-stu-id="64871-205">To get book details, the client will send a GET request to `/api/books/{id}/details`, where *{id}* is the ID of the book.</span></span>

<span data-ttu-id="64871-206">`BooksController` 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-206">Add the following method to the `BooksController` class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

<span data-ttu-id="64871-207">를 요청 하 `/api/books/1/details` 는 경우 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="64871-207">If you request `/api/books/1/details`, the response looks like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a><span data-ttu-id="64871-208">장르 별 서적 가져오기</span><span class="sxs-lookup"><span data-stu-id="64871-208">Get Books By Genre</span></span>

<span data-ttu-id="64871-209">특정 장르에서 책 목록을 가져오기 위해 클라이언트는에 GET 요청을 보냅니다 `/api/books/genre` . 여기서 *장르* 는 장르 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="64871-209">To get a list of books in a specific genre, the client will send a GET request to `/api/books/genre`, where *genre* is the name of the genre.</span></span> <span data-ttu-id="64871-210">(예: `/api/books/fantasy`)</span><span class="sxs-lookup"><span data-stu-id="64871-210">(For example, `/api/books/fantasy`.)</span></span>

<span data-ttu-id="64871-211">에 다음 메서드를 추가 `BooksController` 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-211">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

<span data-ttu-id="64871-212">여기서는 URI 템플릿에서 {장르} 매개 변수를 포함 하는 경로를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-212">Here we are defining a route that contains a {genre} parameter in the URI template.</span></span> <span data-ttu-id="64871-213">Web API는 이러한 두 Uri를 구분 하 고 다른 메서드로 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64871-213">Notice that Web API is able to distinguish these two URIs and route them to different methods:</span></span>

`/api/books/1`

`/api/books/fantasy`

<span data-ttu-id="64871-214">이는 메서드는 `GetBook` "id" 세그먼트가 정수 값 이어야 하는 제약 조건을 포함 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="64871-214">That's because the `GetBook` method includes a constraint that the "id" segment must be an integer value:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

<span data-ttu-id="64871-215">/Api/books/fantasy를 요청 하는 경우 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="64871-215">If you request /api/books/fantasy, the response looks like this:</span></span>

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a><span data-ttu-id="64871-216">저자 별 책 가져오기</span><span class="sxs-lookup"><span data-stu-id="64871-216">Get Books By Author</span></span>

<span data-ttu-id="64871-217">특정 저자에 대 한 책 목록을 가져오기 위해 클라이언트는에 GET 요청을 보냅니다 `/api/authors/id/books` . 여기서 *id* 는 저자의 id입니다.</span><span class="sxs-lookup"><span data-stu-id="64871-217">To get a list of a books for a particular author, the client will send a GET request to `/api/authors/id/books`, where *id* is the ID of the author.</span></span>

<span data-ttu-id="64871-218">에 다음 메서드를 추가 `BooksController` 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-218">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

<span data-ttu-id="64871-219">이 예제는 &quot; 책 &quot; 이 저자 들의 자식 리소스로 처리 되기 때문에 흥미롭습니다 &quot; &quot; .</span><span class="sxs-lookup"><span data-stu-id="64871-219">This example is interesting because &quot;books&quot; is treated a child resource of &quot;authors&quot;.</span></span> <span data-ttu-id="64871-220">이 패턴은 RESTful Api에서 매우 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="64871-220">This pattern is quite common in RESTful APIs.</span></span>

<span data-ttu-id="64871-221">경로 템플릿의 물결표 (~)는 **RoutePrefix** 특성의 경로 접두사를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-221">The tilde (~) in the route template overrides the route prefix in the **RoutePrefix** attribute.</span></span>

## <a name="get-books-by-publication-date"></a><span data-ttu-id="64871-222">게시 날짜별 서적 가져오기</span><span class="sxs-lookup"><span data-stu-id="64871-222">Get Books By Publication Date</span></span>

<span data-ttu-id="64871-223">게시 날짜별로 책 목록을 가져오려면 클라이언트는에 GET 요청을 보냅니다 `/api/books/date/yyyy-mm-dd` . 여기서 *yyyy-mm-dd* 는 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="64871-223">To get a list of books by publication date, the client will send a GET request to `/api/books/date/yyyy-mm-dd`, where *yyyy-mm-dd* is the date.</span></span>

<span data-ttu-id="64871-224">이 작업을 수행 하는 한 가지 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="64871-224">Here is one way to do this:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

<span data-ttu-id="64871-225">`{pubdate:datetime}`매개 변수는 **DateTime** 값과 일치 하도록 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64871-225">The `{pubdate:datetime}` parameter is constrained to match a **DateTime** value.</span></span> <span data-ttu-id="64871-226">이는 작동 하지만 실제로는 원하는 것 보다 더 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64871-226">This works, but it's actually more permissive than we'd like.</span></span> <span data-ttu-id="64871-227">예를 들어 다음 Uri는 경로와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-227">For example, these URIs will also match the route:</span></span>

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

<span data-ttu-id="64871-228">이러한 Uri를 허용 하는 것이 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="64871-228">There's nothing wrong with allowing these URIs.</span></span> <span data-ttu-id="64871-229">그러나 경로 템플릿에 정규식 제약 조건을 추가 하 여 경로를 특정 형식으로 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64871-229">However, you can restrict the route to a particular format by adding a regular-expression constraint to the route template:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

<span data-ttu-id="64871-230">이제 &quot; yyyy-mm-dd 형식의 날짜만 &quot; 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-230">Now only dates in the form &quot;yyyy-mm-dd&quot; will match.</span></span> <span data-ttu-id="64871-231">정규식을 사용 하 여 실제 날짜의 유효성을 검사 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64871-231">Notice that we don't use the regex to validate that we got a real date.</span></span> <span data-ttu-id="64871-232">Web API가 URI 세그먼트를 **DateTime** 인스턴스로 변환 하려고 할 때 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64871-232">That is handled when Web API tries to convert the URI segment into a **DateTime** instance.</span></span> <span data-ttu-id="64871-233">' 2012-47-99 '과 같은 잘못 된 날짜는 변환 되지 않으므로 클라이언트에서 404 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-233">An invalid date such as '2012-47-99' will fail to be converted, and the client will get a 404 error.</span></span>

<span data-ttu-id="64871-234">다른 regex를 사용 하 여 `/api/books/date/yyyy/mm/dd` 다른 **[Route]** 특성을 추가 하 여 슬래시 구분 기호 ()를 지원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64871-234">You can also support a slash separator (`/api/books/date/yyyy/mm/dd`) by adding another **[Route]** attribute with a different regex.</span></span>

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

<span data-ttu-id="64871-235">여기에는 미묘한 중요 한 세부 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64871-235">There is a subtle but important detail here.</span></span> <span data-ttu-id="64871-236">두 번째 경로 템플릿의 \* {pubdate} 매개 변수 시작 부분에 와일드 카드 문자 ()가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64871-236">The second route template has a wildcard character (\*) at the start of the {pubdate} parameter:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.txt)]

<span data-ttu-id="64871-237">이렇게 하면 {pubdate}가 URI의 나머지 부분과 일치 해야 한다는 것을 라우팅 엔진에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="64871-237">This tells the routing engine that {pubdate} should match the rest of the URI.</span></span> <span data-ttu-id="64871-238">기본적으로 템플릿 매개 변수는 단일 URI 세그먼트와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-238">By default, a template parameter matches a single URI segment.</span></span> <span data-ttu-id="64871-239">이 경우에는 {pubdate}를 여러 개의 URI 세그먼트로 확장 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-239">In this case, we want {pubdate} to span several URI segments:</span></span>

`/api/books/date/2013/06/17`

## <a name="controller-code"></a><span data-ttu-id="64871-240">컨트롤러 코드</span><span class="sxs-lookup"><span data-stu-id="64871-240">Controller Code</span></span>

<span data-ttu-id="64871-241">BooksController 클래스에 대 한 전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="64871-241">Here is the complete code for the BooksController class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a><span data-ttu-id="64871-242">요약</span><span class="sxs-lookup"><span data-stu-id="64871-242">Summary</span></span>

<span data-ttu-id="64871-243">특성 라우팅은 API에 대 한 Uri를 설계할 때 더 많은 제어와 유연성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="64871-243">Attribute routing gives you more control and greater flexibility when designing the URIs for your API.</span></span>
