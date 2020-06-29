---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC 응용 프로그램에서 Entity Framework 정렬, 필터링 및 페이징 (3/10) | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 8af630e0-fffa-4110-9eca-c96e201b2724
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 48938b378a741a0f1c351c2cb1d33b5140c6cf93
ms.sourcegitcommit: 8d34fb54e790cfba2d64097afc8276da5b22283e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85484611"
---
# <a name="sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application-3-of-10"></a><span data-ttu-id="34c14-103">ASP.NET MVC 응용 프로그램에서 Entity Framework 정렬, 필터링 및 페이징 (3/10)</span><span class="sxs-lookup"><span data-stu-id="34c14-103">Sorting, Filtering, and Paging with the Entity Framework in an ASP.NET MVC Application (3 of 10)</span></span>

<span data-ttu-id="34c14-104">만든 사람 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="34c14-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="34c14-105">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="34c14-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="34c14-106">Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio 2012을 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="34c14-107">자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34c14-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="34c14-108">[이 챕터의](building-the-ef5-mvc4-chapter-downloads.md) 시작 또는 시작 프로젝트 다운로드에서 자습서 시리즈를 시작 하 고 여기에서 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="34c14-109">해결할 수 없는 문제가 발생 하는 경우 [완료 된 챕터를 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 하 여 문제를 재현해 보세요.</span><span class="sxs-lookup"><span data-stu-id="34c14-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="34c14-110">일반적으로 코드를 완성 된 코드와 비교 하 여 문제에 대 한 솔루션을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="34c14-111">몇 가지 일반적인 오류 및 해결 방법에 대 한 자세한 내용은 [오류 및 해결](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors) 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="34c14-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="34c14-112">이전 자습서에서는 엔터티에 대 한 기본 CRUD 작업을 위한 일련의 웹 페이지를 구현 `Student` 했습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-112">In the previous tutorial you implemented a set of web pages for basic CRUD operations for `Student` entities.</span></span> <span data-ttu-id="34c14-113">이 자습서에서는 **학생** 인덱스 페이지에 정렬, 필터링 및 페이징 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-113">In this tutorial you'll add sorting, filtering, and paging functionality to the **Students** Index page.</span></span> <span data-ttu-id="34c14-114">단순 그룹화를 수행하는 페이지도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-114">You'll also create a page that does simple grouping.</span></span>

<span data-ttu-id="34c14-115">다음 그림에서는 작업이 완료되었을 때 페이지 모양을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-115">The following illustration shows what the page will look like when you're done.</span></span> <span data-ttu-id="34c14-116">열 제목은 해당 열로 정렬하기 위해 사용자가 클릭할 수 있는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-116">The column headings are links that the user can click to sort by that column.</span></span> <span data-ttu-id="34c14-117">열 제목을 반복해서 클릭하면 오름차순 및 내림차순으로 정렬 순서가 토글됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-117">Clicking a column heading repeatedly toggles between ascending and descending sort order.</span></span>

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a><span data-ttu-id="34c14-119">학생 인덱스 페이지에 열 정렬 링크 추가</span><span class="sxs-lookup"><span data-stu-id="34c14-119">Add Column Sort Links to the Students Index Page</span></span>

<span data-ttu-id="34c14-120">학생 인덱스 페이지에 정렬을 추가 하려면 컨트롤러의 메서드를 변경 하 `Index` `Student` 고 인덱스 뷰에 코드를 추가 `Student` 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-120">To add sorting to the Student Index page, you'll change the `Index` method of the `Student` controller and add code to the `Student` Index view.</span></span>

### <a name="add-sorting-functionality-to-the-index-method"></a><span data-ttu-id="34c14-121">인덱스 메서드에 정렬 기능 추가</span><span class="sxs-lookup"><span data-stu-id="34c14-121">Add Sorting Functionality to the Index Method</span></span>

<span data-ttu-id="34c14-122">*Controllers\StudentController.cs*에서 `Index` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-122">In *Controllers\StudentController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="34c14-123">이 코드는 URL의 쿼리 문자열에서 `sortOrder` 매개 변수를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-123">This code receives a `sortOrder` parameter from the query string in the URL.</span></span> <span data-ttu-id="34c14-124">쿼리 문자열 값은 ASP.NET MVC에서 작업 메서드에 대 한 매개 변수로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-124">The query string value is provided by ASP.NET MVC as a parameter to the action method.</span></span> <span data-ttu-id="34c14-125">매개 변수는 "Name" 또는 "Date" 문자열이며 필요에 따라 밑줄과 내림차순을 지정하는 문자열 "desc"가 옵니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-125">The parameter will be a string that's either "Name" or "Date", optionally followed by an underscore and the string "desc" to specify descending order.</span></span> <span data-ttu-id="34c14-126">기본 정렬 순서는 오름차순입니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-126">The default sort order is ascending.</span></span>

<span data-ttu-id="34c14-127">인덱스 페이지를 처음 요청하면 쿼리 문자열은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-127">The first time the Index page is requested, there's no query string.</span></span> <span data-ttu-id="34c14-128">학습자는 문에 대 한 제어에 의해 설정 된 기본값 인 오름차순으로 표시 됩니다 `LastName` `switch` .</span><span class="sxs-lookup"><span data-stu-id="34c14-128">The students are displayed in ascending order by `LastName`, which is the default as established by the fall-through case in the `switch` statement.</span></span> <span data-ttu-id="34c14-129">사용자가 열 제목 하이퍼링크를 클릭하면 쿼리 문자열에 해당 `sortOrder` 값이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-129">When the user clicks a column heading hyperlink, the appropriate `sortOrder` value is provided in the query string.</span></span>

<span data-ttu-id="34c14-130">`ViewBag`뷰가 적절 한 쿼리 문자열 값을 사용 하 여 열 머리글 하이퍼링크를 구성할 수 있도록 두 개의 변수가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-130">The two `ViewBag` variables are used so that the view can configure the column heading hyperlinks with the appropriate query string values:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="34c14-131">이것은 3개로 구성된 문입니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-131">These are ternary statements.</span></span> <span data-ttu-id="34c14-132">첫 번째 `sortOrder` 매개 변수는 매개 변수가 null 이거나 비어 있는 경우 `ViewBag.NameSortParm` "이름 desc"로 설정 해야 함을 지정 하 고, 그렇지 않은 경우에는 \_ 빈 문자열로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-132">The first one specifies that if the `sortOrder` parameter is null or empty, `ViewBag.NameSortParm` should be set to "name\_desc"; otherwise, it should be set to an empty string.</span></span> <span data-ttu-id="34c14-133">이러한 두 문을 사용하면 뷰에서 다음과 같이 열 제목 하이퍼링크를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-133">These two statements enable the view to set the column heading hyperlinks as follows:</span></span>

| <span data-ttu-id="34c14-134">현재 정렬 순서</span><span class="sxs-lookup"><span data-stu-id="34c14-134">Current sort order</span></span> | <span data-ttu-id="34c14-135">성 하이퍼링크</span><span class="sxs-lookup"><span data-stu-id="34c14-135">Last Name Hyperlink</span></span> | <span data-ttu-id="34c14-136">날짜 하이퍼링크</span><span class="sxs-lookup"><span data-stu-id="34c14-136">Date Hyperlink</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34c14-137">성 오름차순</span><span class="sxs-lookup"><span data-stu-id="34c14-137">Last Name ascending</span></span> | <span data-ttu-id="34c14-138">descending</span><span class="sxs-lookup"><span data-stu-id="34c14-138">descending</span></span> | <span data-ttu-id="34c14-139">ascending</span><span class="sxs-lookup"><span data-stu-id="34c14-139">ascending</span></span> |
| <span data-ttu-id="34c14-140">성 내림차순</span><span class="sxs-lookup"><span data-stu-id="34c14-140">Last Name descending</span></span> | <span data-ttu-id="34c14-141">ascending</span><span class="sxs-lookup"><span data-stu-id="34c14-141">ascending</span></span> | <span data-ttu-id="34c14-142">ascending</span><span class="sxs-lookup"><span data-stu-id="34c14-142">ascending</span></span> |
| <span data-ttu-id="34c14-143">날짜 오름차순</span><span class="sxs-lookup"><span data-stu-id="34c14-143">Date ascending</span></span> | <span data-ttu-id="34c14-144">ascending</span><span class="sxs-lookup"><span data-stu-id="34c14-144">ascending</span></span> | <span data-ttu-id="34c14-145">descending</span><span class="sxs-lookup"><span data-stu-id="34c14-145">descending</span></span> |
| <span data-ttu-id="34c14-146">날짜 내림차순</span><span class="sxs-lookup"><span data-stu-id="34c14-146">Date descending</span></span> | <span data-ttu-id="34c14-147">ascending</span><span class="sxs-lookup"><span data-stu-id="34c14-147">ascending</span></span> | <span data-ttu-id="34c14-148">ascending</span><span class="sxs-lookup"><span data-stu-id="34c14-148">ascending</span></span> |

<span data-ttu-id="34c14-149">메서드는 [LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx) 을 사용 하 여 정렬 기준으로 사용할 열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-149">The method uses [LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx) to specify the column to sort by.</span></span> <span data-ttu-id="34c14-150">이 코드는 문 앞에 [IQueryable](https://msdn.microsoft.com/library/bb351562.aspx) 변수 `switch` 를 만들고, 문에서이 변수를 수정 하 `switch` 고, `ToList` 문 다음에 메서드를 호출 합니다 `switch` .</span><span class="sxs-lookup"><span data-stu-id="34c14-150">The code creates an [IQueryable](https://msdn.microsoft.com/library/bb351562.aspx) variable before the `switch` statement, modifies it in the `switch` statement, and calls the `ToList` method after the `switch` statement.</span></span> <span data-ttu-id="34c14-151">`IQueryable` 변수를 작성하고 수정하면 데이터베이스에 쿼리가 보내지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-151">When you create and modify `IQueryable` variables, no query is sent to the database.</span></span> <span data-ttu-id="34c14-152">`IQueryable`와 같은 메서드를 호출 하 여 개체를 컬렉션으로 변환할 때까지 쿼리가 실행 되지 않습니다 `ToList` .</span><span class="sxs-lookup"><span data-stu-id="34c14-152">The query is not executed until you convert the `IQueryable` object into a collection by calling a method such as `ToList`.</span></span> <span data-ttu-id="34c14-153">따라서이 코드는 문까지 실행 되지 않는 단일 쿼리를 생성 합니다 `return View` .</span><span class="sxs-lookup"><span data-stu-id="34c14-153">Therefore, this code results in a single query that is not executed until the `return View` statement.</span></span>

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a><span data-ttu-id="34c14-154">학생 인덱스 뷰에 열 제목 하이퍼링크 추가</span><span class="sxs-lookup"><span data-stu-id="34c14-154">Add Column Heading Hyperlinks to the Student Index View</span></span>

<span data-ttu-id="34c14-155">*Views\Student\Index.cshtml*에서 `<tr>` `<th>` 제목 행의 및 요소를 강조 표시 된 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-155">In *Views\Student\Index.cshtml*, replace the `<tr>` and `<th>` elements for the heading row with the highlighted code:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

<span data-ttu-id="34c14-156">이 코드는 속성의 정보를 사용 하 여 `ViewBag` 적절 한 쿼리 문자열 값으로 하이퍼링크를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-156">This code uses the information in the `ViewBag` properties to set up hyperlinks with the appropriate query string values.</span></span>

<span data-ttu-id="34c14-157">페이지를 실행 하 고 **Last Name** 및 **등록 날짜** 열 제목을 클릭 하 여 정렬이 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-157">Run the page and click the **Last Name** and **Enrollment Date** column headings to verify that sorting works.</span></span>

![Students_Index_page_with_sort_hyperlinks](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="34c14-159">**성** 머리글을 클릭 하면 학생이 내림차순 성 순서로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-159">After you click the **Last Name** heading, students are displayed in descending last name order.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="add-a-search-box-to-the-students-index-page"></a><span data-ttu-id="34c14-160">학생 인덱스 페이지에 검색 상자 추가</span><span class="sxs-lookup"><span data-stu-id="34c14-160">Add a Search Box to the Students Index Page</span></span>

<span data-ttu-id="34c14-161">학생 인덱스 페이지에 필터링을 추가하려면 뷰에 텍스트 상자와 [제출] 단추를 추가하고 `Index` 메서드에 해당 변경 내용을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-161">To add filtering to the Students Index page, you'll add a text box and a submit button to the view and make corresponding changes in the `Index` method.</span></span> <span data-ttu-id="34c14-162">텍스트 상자를 통해 이름 및 성 필드에서 검색할 문자열을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-162">The text box will let you enter a string to search for in the first name and last name fields.</span></span>

### <a name="add-filtering-functionality-to-the-index-method"></a><span data-ttu-id="34c14-163">인덱스 메서드에 필터링 기능 추가</span><span class="sxs-lookup"><span data-stu-id="34c14-163">Add Filtering Functionality to the Index Method</span></span>

<span data-ttu-id="34c14-164">*Controllers\StudentController.cs*에서 `Index` 메서드를 다음 코드로 바꿉니다 (변경 내용이 강조 표시 됨).</span><span class="sxs-lookup"><span data-stu-id="34c14-164">In *Controllers\StudentController.cs*, replace the `Index` method with the following code (the changes are highlighted):</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

<span data-ttu-id="34c14-165">`searchString` 매개 변수를 `Index` 메서드에 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-165">You've added a `searchString` parameter to the `Index` method.</span></span> <span data-ttu-id="34c14-166">또한 `where` 이름 또는 성이 검색 문자열을 포함 하 고 있는 학생만 선택 하는 절을 LINQ statement에 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-166">You've also added to the LINQ statement a `where` clause that selects only students whose first name or last name contains the search string.</span></span> <span data-ttu-id="34c14-167">인덱스 뷰에 추가할 텍스트 상자에서 검색 문자열 값이 수신 됩니다. [Where](https://msdn.microsoft.com/library/bb535040.aspx) 절을 추가 하는 문은 검색할 값이 있는 경우에만 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-167">The search string value is received from a text box that you'll add to the Index view.The statement that adds the [where](https://msdn.microsoft.com/library/bb535040.aspx) clause is executed only if there's a value to search for.</span></span>

> [!NOTE]
> <span data-ttu-id="34c14-168">대부분의 경우 Entity Framework 엔터티 집합에 대해 동일한 메서드를 호출 하거나 메모리 내 컬렉션에서 확장 메서드로 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-168">In many cases you can call the same method either on an Entity Framework entity set or as an extension method on an in-memory collection.</span></span> <span data-ttu-id="34c14-169">결과는 일반적으로 동일 하지만 경우에 따라 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-169">The results are normally the same but in some cases may be different.</span></span> <span data-ttu-id="34c14-170">예를 들어 메서드의 .NET Framework 구현은 `Contains` 빈 문자열을 전달할 때 모든 행을 반환 하지만 SQL Server Compact 4.0에 대 한 Entity Framework 공급자는 빈 문자열에 대해 0 개의 행을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-170">For example, the .NET Framework implementation of the `Contains` method returns all rows when you pass an empty string to it, but the Entity Framework provider for SQL Server Compact 4.0 returns zero rows for empty strings.</span></span> <span data-ttu-id="34c14-171">따라서이 예제의 코드 (문 `Where` 내에 문을 배치)는 `if` 모든 버전의 SQL Server에 대해 동일한 결과를 얻을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-171">Therefore the code in the example (putting the `Where` statement inside an `if` statement) makes sure that you get the same results for all versions of SQL Server.</span></span> <span data-ttu-id="34c14-172">또한 메서드의 .NET Framework 구현은 `Contains` 기본적으로 대/소문자를 구분 하는 비교를 수행 하지만 Entity Framework SQL Server 공급자는 기본적으로 대/소문자를 구분 하지 않는 비교를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-172">Also, the .NET Framework implementation of the `Contains` method performs a case-sensitive comparison by default, but Entity Framework SQL Server providers perform case-insensitive comparisons by default.</span></span> <span data-ttu-id="34c14-173">따라서 메서드를 호출 `ToUpper` 하 여 테스트를 명시적으로 대/소문자를 구분 하지 않도록 설정 하면 나중에 리포지토리를 사용 하도록 코드를 변경할 때 결과가 변경 되지 않습니다 `IEnumerable` . 그러면 개체가 아닌 컬렉션이 반환 됩니다 `IQueryable` .</span><span class="sxs-lookup"><span data-stu-id="34c14-173">Therefore, calling the `ToUpper` method to make the test explicitly case-insensitive ensures that results do not change when you change the code later to use a repository, which will return an `IEnumerable` collection instead of an `IQueryable` object.</span></span> <span data-ttu-id="34c14-174">(`IEnumerable` 컬렉션에서 `Contains` 메서드를 호출하면 .NET Framework 구현을 가져오고 `IQueryable` 개체에서 호출하면 데이터베이스 공급자 구현을 가져옵니다.)</span><span class="sxs-lookup"><span data-stu-id="34c14-174">(When you call the `Contains` method on an `IEnumerable` collection, you get the .NET Framework implementation; when you call it on an `IQueryable` object, you get the database provider implementation.)</span></span>

### <a name="add-a-search-box-to-the-student-index-view"></a><span data-ttu-id="34c14-175">Students 인덱스 뷰에 검색 상자 추가</span><span class="sxs-lookup"><span data-stu-id="34c14-175">Add a Search Box to the Student Index View</span></span>

<span data-ttu-id="34c14-176">*Views\Student\Index.cshtml*에서 `table` 캡션, 텍스트 상자 및 **검색** 단추를 만들기 위해 강조 표시 된 코드를 여는 태그 바로 앞에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-176">In *Views\Student\Index.cshtml*, add the highlighted code immediately before the opening `table` tag in order to create a caption, a text box, and a **Search** button.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=5-10)]

<span data-ttu-id="34c14-177">페이지를 실행 하 고 검색 문자열을 입력 한 다음 **검색** 을 클릭 하 여 필터링이 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-177">Run the page, enter a search string, and click **Search** to verify that filtering is working.</span></span>

![Students_Index_page_with_search_box](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="34c14-179">URL에 "a" 검색 문자열이 포함 되어 있지 않습니다. 즉,이 페이지를 책갈피로 만들면 책갈피를 사용할 때 필터링 된 목록을 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-179">Notice the URL doesn't contain the "an" search string, which means that if you bookmark this page, you won't get the filtered list when you use the bookmark.</span></span> <span data-ttu-id="34c14-180">**검색** 단추를 변경 하 여 자습서의 뒷부분에서 필터 조건에 대 한 쿼리 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-180">You'll change the **Search** button to use query strings for filter criteria later in the tutorial.</span></span>

## <a name="add-paging-to-the-students-index-page"></a><span data-ttu-id="34c14-181">학생 인덱스 페이지에 페이징 추가</span><span class="sxs-lookup"><span data-stu-id="34c14-181">Add Paging to the Students Index Page</span></span>

<span data-ttu-id="34c14-182">학생 인덱스 페이지에 페이징을 추가 하려면 **PagedList** NuGet 패키지를 설치 하는 것으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-182">To add paging to the Students Index page, you'll start by installing the **PagedList.Mvc** NuGet package.</span></span> <span data-ttu-id="34c14-183">그런 다음 메서드를 추가로 변경 하 `Index` 고 뷰에 페이징 링크를 추가 `Index` 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-183">Then you'll make additional changes in the `Index` method and add paging links to the `Index` view.</span></span> <span data-ttu-id="34c14-184">**PagedList** 는 ASP.NET Mvc에 대 한 다양 한 페이징 및 정렬 패키지 중 하나 이며, 여기에서 사용 하는 것은 다른 옵션에 대 한 권장 사항이 아닌 예제로만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-184">**PagedList.Mvc** is one of many good paging and sorting packages for ASP.NET MVC, and its use here is intended only as an example, not as a recommendation for it over other options.</span></span> <span data-ttu-id="34c14-185">다음 그림에서는 페이징 링크를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-185">The following illustration shows the paging links.</span></span>

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

### <a name="install-the-pagedlistmvc-nuget-package"></a><span data-ttu-id="34c14-187">PagedList NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-187">Install the PagedList.MVC NuGet Package</span></span>

<span data-ttu-id="34c14-188">NuGet **PagedList** 패키지는 자동으로 **PagedList** 패키지를 종속성으로 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-188">The NuGet **PagedList.Mvc** package automatically installs the **PagedList** package as a dependency.</span></span> <span data-ttu-id="34c14-189">**PagedList** 패키지는 및 컬렉션 `PagedList` 에 대 한 컬렉션 형식 및 확장 메서드를 설치 합니다 `IQueryable` `IEnumerable` .</span><span class="sxs-lookup"><span data-stu-id="34c14-189">The **PagedList** package installs a `PagedList` collection type and extension methods for `IQueryable` and `IEnumerable` collections.</span></span> <span data-ttu-id="34c14-190">확장 메서드는 또는에서 컬렉션에 데이터의 단일 페이지를 만들며 `PagedList` `IQueryable` `IEnumerable` , `PagedList` 컬렉션은 페이징을 용이 하 게 하는 여러 속성과 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-190">The extension methods create a single page of data in a `PagedList` collection out of your `IQueryable` or `IEnumerable`, and the `PagedList` collection provides several properties and methods that facilitate paging.</span></span> <span data-ttu-id="34c14-191">**PagedList** 패키지는 페이징 단추를 표시 하는 페이징 도우미를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-191">The **PagedList.Mvc** package installs a paging helper that displays the paging buttons.</span></span>

<span data-ttu-id="34c14-192">**도구** 메뉴에서 **nuget 패키지 관리자** 를 선택한 다음 **솔루션에 대 한 nuget 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-192">From the **Tools** menu, select **NuGet Package Manager** and then **Manage NuGet Packages for Solution**.</span></span>

<span data-ttu-id="34c14-193">**NuGet 패키지 관리** 대화 상자에서 왼쪽의 **온라인** 탭을 클릭 한 다음 검색 상자에 "페이징"을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-193">In the **Manage NuGet Packages** dialog box, click the **Online** tab on the left and then enter "paged" in the search box.</span></span> <span data-ttu-id="34c14-194">**PagedList** 패키지가 표시 되 면 **설치**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-194">When you see the **PagedList.Mvc** package, click **Install**.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="34c14-195">**프로젝트 선택** 상자에서 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-195">In the **Select Projects** box, click **OK**.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="add-paging-functionality-to-the-index-method"></a><span data-ttu-id="34c14-196">인덱스 메서드에 페이징 기능 추가</span><span class="sxs-lookup"><span data-stu-id="34c14-196">Add Paging Functionality to the Index Method</span></span>

<span data-ttu-id="34c14-197">*Controllers\StudentController.cs*에서 `using` 네임 스페이스에 대 한 문을 추가 합니다 `PagedList` .</span><span class="sxs-lookup"><span data-stu-id="34c14-197">In *Controllers\StudentController.cs*, add a `using` statement for the `PagedList` namespace:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="34c14-198">`Index` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-198">Replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="34c14-199">이 코드는 다음과 같이 `page` 매개 변수, 현재 정렬 순서 매개 변수 및 현재 필터 매개 변수를 메서드 시그니처에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-199">This code adds a `page` parameter, a current sort order parameter, and a current filter parameter to the method signature, as shown here:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="34c14-200">페이지가 처음 표시되거나 사용자가 페이징 또는 정렬 링크를 클릭하지 않으면 모든 매개 변수가 Null이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-200">The first time the page is displayed, or if the user hasn't clicked a paging or sorting link, all the parameters will be null.</span></span> <span data-ttu-id="34c14-201">페이징 링크를 클릭 하면 `page` 표시할 페이지 번호가 변수에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-201">If a paging link is clicked, the `page` variable will contain the page number to display.</span></span>

<span data-ttu-id="34c14-202">`A ViewBag`속성은 현재 정렬 순서를 사용 하 여 뷰를 제공 합니다 .이는 페이징 링크에 정렬 순서를 유지 하기 위해 페이징 링크에 포함 되어야 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-202">`A ViewBag` property provides the view with the current sort order, because this must be included in the paging links in order to keep the sort order the same while paging:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="34c14-203">또 다른 속성인는 `ViewBag.CurrentFilter` 현재 필터 문자열을 사용 하 여 뷰를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-203">Another property, `ViewBag.CurrentFilter`, provides the view with the current filter string.</span></span> <span data-ttu-id="34c14-204">이 값은 페이징 중 필터 설정을 유지하기 위해 페이징 링크에 포함되어야 하며 페이지를 다시 표시할 때 텍스트 상자에 복원되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-204">This value must be included in the paging links in order to maintain the filter settings during paging, and it must be restored to the text box when the page is redisplayed.</span></span> <span data-ttu-id="34c14-205">페이징 중에 검색 문자열이 변경되면 새 필터로 인해 다른 데이터가 표시될 수 있으므로 페이지는 1로 재설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-205">If the search string is changed during paging, the page has to be reset to 1, because the new filter can result in different data to display.</span></span> <span data-ttu-id="34c14-206">텍스트 상자에 값을 입력 하 고 제출 단추를 누르면 검색 문자열이 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-206">The search string is changed when a value is entered in the text box and the submit button is pressed.</span></span> <span data-ttu-id="34c14-207">이 경우 `searchString` 매개 변수는 null이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-207">In that case, the `searchString` parameter is not null.</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

<span data-ttu-id="34c14-208">메서드 끝에서 `ToPagedList` 학생 개체의 확장 메서드는 `IQueryable` 학생 쿼리를 페이징을 지 원하는 컬렉션 형식으로 학생의 단일 페이지로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-208">At the end of the method, the `ToPagedList` extension method on the students `IQueryable` object converts the student query to a single page of students in a collection type that supports paging.</span></span> <span data-ttu-id="34c14-209">그런 다음 학생의 단일 페이지가 보기에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-209">That single page of students is then passed to the view:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="34c14-210">`ToPagedList` 메서드는 페이지 번호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-210">The `ToPagedList` method takes a page number.</span></span> <span data-ttu-id="34c14-211">두 물음표는 [null 병합 연산자](https://msdn.microsoft.com/library/ms173224.aspx)를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-211">The two question marks represent the [null-coalescing operator](https://msdn.microsoft.com/library/ms173224.aspx).</span></span> <span data-ttu-id="34c14-212">Null 병합 연산자는 nullable 형식의 기본값을 정의합니다. `(page ?? 1)` 식은 값이 있는 경우 `page` 값을 반환하고 `page`가 Null이면 1일 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-212">The null-coalescing operator defines a default value for a nullable type; the expression `(page ?? 1)` means return the value of `page` if it has a value, or return 1 if `page` is null.</span></span>

### <a name="add-paging-links-to-the-student-index-view"></a><span data-ttu-id="34c14-213">학생 인덱스 뷰에 페이징 링크 추가</span><span class="sxs-lookup"><span data-stu-id="34c14-213">Add Paging Links to the Student Index View</span></span>

<span data-ttu-id="34c14-214">*Views\Student\Index.cshtml*에서 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-214">In *Views\Student\Index.cshtml*, replace the existing code with the following code:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=6,9,14-20,56-58)]

<span data-ttu-id="34c14-215">페이지 맨 위에 `@model` 문은 뷰가 `List` 개체 대신 `PagedList` 개체를 가져오는 것을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-215">The `@model` statement at the top of the page specifies that the view now gets a `PagedList` object instead of a `List` object.</span></span>

<span data-ttu-id="34c14-216">`using`에 대 한 문은 `PagedList.Mvc` 페이징 단추의 MVC 도우미에 대 한 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-216">The `using` statement for `PagedList.Mvc` gives access to the MVC helper for the paging buttons.</span></span>

<span data-ttu-id="34c14-217">코드는 [Formmethod. Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css)을 지정할 수 있는 [html.beginform](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) 의 오버 로드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-217">The code uses an overload of [BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) that allows it to specify [FormMethod.Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css).</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

<span data-ttu-id="34c14-218">기본 [HTML.BEGINFORM](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) POST를 사용 하 여 폼 데이터를 전송 합니다. 즉, 매개 변수가 HTTP 메시지 본문에 전달 되 고 URL에 쿼리 문자열로 전달 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-218">The default [BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) submits form data with a POST, which means that parameters are passed in the HTTP message body and not in the URL as query strings.</span></span> <span data-ttu-id="34c14-219">HTTP GET을 지정하면 폼 데이터가 URL에 쿼리 문자열로 전달되고 이를 통해 사용자는 URL을 책갈피로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-219">When you specify HTTP GET, the form data is passed in the URL as query strings, which enables users to bookmark the URL.</span></span> <span data-ttu-id="34c14-220">[HTTP get 사용에 대 한 W3C 지침](http://www.w3.org/2001/tag/doc/whenToUseGet.html) 에서는 작업으로 인해 업데이트가 발생 하지 않을 때 get을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-220">The [W3C guidelines for the use of HTTP GET](http://www.w3.org/2001/tag/doc/whenToUseGet.html) specify that you should use GET when the action does not result in an update.</span></span>

<span data-ttu-id="34c14-221">텍스트 상자는 현재 검색 문자열로 초기화 되므로 새 페이지를 클릭 하면 현재 검색 문자열을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-221">The text box is initialized with the current search string so when you click a new page you can see the current search string.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

<span data-ttu-id="34c14-222">열 머리글 링크는 쿼리 문자열을 사용하여 현재 검색 문자열을 컨트롤러에 전달하므로 사용자가 필터 결과 내에서 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-222">The column header links use the query string to pass the current search string to the controller so that the user can sort within filter results:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

<span data-ttu-id="34c14-223">현재 페이지와 총 페이지 수가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-223">The current page and total number of pages are displayed.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

<span data-ttu-id="34c14-224">표시할 페이지가 없으면 "0/0 페이지"가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-224">If there are no pages to display, "Page 0 of 0" is shown.</span></span> <span data-ttu-id="34c14-225">이 경우 페이지 번호는 `Model.PageNumber` 가 1이 고가 0 이므로 페이지 수는 페이지 수보다 큽니다 `Model.PageCount` .</span><span class="sxs-lookup"><span data-stu-id="34c14-225">(In that case the page number is greater than the page count because `Model.PageNumber` is 1, and `Model.PageCount` is 0.)</span></span>

<span data-ttu-id="34c14-226">도우미는 페이징 단추를 표시 합니다 `PagedListPager` .</span><span class="sxs-lookup"><span data-stu-id="34c14-226">The paging buttons are displayed by the `PagedListPager` helper:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

<span data-ttu-id="34c14-227">`PagedListPager`도우미는 url 및 스타일을 포함 하 여 사용자 지정할 수 있는 다양 한 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-227">The `PagedListPager` helper provides a number of options that you can customize, including URLs and styling.</span></span> <span data-ttu-id="34c14-228">자세한 내용은 GitHub 사이트에서 [TroyGoode/PagedList](https://github.com/TroyGoode/PagedList) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="34c14-228">For more information, see [TroyGoode / PagedList](https://github.com/TroyGoode/PagedList) on the GitHub site.</span></span>

<span data-ttu-id="34c14-229">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-229">Run the page.</span></span>

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

<span data-ttu-id="34c14-231">다른 정렬 순서의 페이징 링크를 클릭하여 페이징이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-231">Click the paging links in different sort orders to make sure paging works.</span></span> <span data-ttu-id="34c14-232">그런 다음, 검색 문자열을 입력하고 페이징을 다시 시도하여 정렬 및 필터링을 통해 페이징이 제대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-232">Then enter a search string and try paging again to verify that paging also works correctly with sorting and filtering.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="create-an-about-page-that-shows-student-statistics"></a><span data-ttu-id="34c14-233">학생 통계를 표시 하는 정보 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="34c14-233">Create an About Page That Shows Student Statistics</span></span>

<span data-ttu-id="34c14-234">Contoso University 웹 사이트의 정보 페이지에는 각 등록 날짜에 등록된 학생 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-234">For the Contoso University website's About page, you'll display how many students have enrolled for each enrollment date.</span></span> <span data-ttu-id="34c14-235">여기에는 그룹화와 그룹에 대한 간단한 계산이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-235">This requires grouping and simple calculations on the groups.</span></span> <span data-ttu-id="34c14-236">이 작업을 수행하기 위해 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-236">To accomplish this, you'll do the following:</span></span>

- <span data-ttu-id="34c14-237">뷰에 전달해야 하는 데이터에 대해 뷰 모델 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-237">Create a view model class for the data that you need to pass to the view.</span></span>
- <span data-ttu-id="34c14-238">`About`컨트롤러에서 메서드를 수정 `Home` 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-238">Modify the `About` method in the `Home` controller.</span></span>
- <span data-ttu-id="34c14-239">뷰를 수정 `About` 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-239">Modify the `About` view.</span></span>

### <a name="create-the-view-model"></a><span data-ttu-id="34c14-240">뷰 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="34c14-240">Create the View Model</span></span>

<span data-ttu-id="34c14-241">*Viewmodels* 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-241">Create a *ViewModels* folder.</span></span> <span data-ttu-id="34c14-242">해당 폴더에서 *EnrollmentDateGroup.cs* 클래스를 추가 하 고 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-242">In that folder, add a class file *EnrollmentDateGroup.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a><span data-ttu-id="34c14-243">홈 컨트롤러 수정</span><span class="sxs-lookup"><span data-stu-id="34c14-243">Modify the Home Controller</span></span>

<span data-ttu-id="34c14-244">*HomeController.cs*에서 `using` 파일 맨 위에 다음 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-244">In *HomeController.cs*, add the following `using` statements at the top of the file:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

<span data-ttu-id="34c14-245">클래스에 대 한 여는 중괄호 바로 뒤에 데이터베이스 컨텍스트에 대 한 클래스 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-245">Add a class variable for the database context immediately after the opening curly brace for the class:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

<span data-ttu-id="34c14-246">`About` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-246">Replace the `About` method with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

<span data-ttu-id="34c14-247">LINQ 문은 등록 날짜별로 학생 엔터티를 그룹화하고 각 그룹의 엔터티 수를 계산하며 결과를 `EnrollmentDateGroup` 뷰 모델 개체의 컬렉션에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-247">The LINQ statement groups the student entities by enrollment date, calculates the number of entities in each group, and stores the results in a collection of `EnrollmentDateGroup` view model objects.</span></span>

<span data-ttu-id="34c14-248">메서드를 추가 합니다 `Dispose` .</span><span class="sxs-lookup"><span data-stu-id="34c14-248">Add a `Dispose` method:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a><span data-ttu-id="34c14-249">정보 뷰 수정</span><span class="sxs-lookup"><span data-stu-id="34c14-249">Modify the About View</span></span>

<span data-ttu-id="34c14-250">*Views\Home\About.cshtml* 파일의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-250">Replace the code in the *Views\Home\About.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

<span data-ttu-id="34c14-251">앱을 실행 하 고 **정보** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-251">Run the app and click the **About** link.</span></span> <span data-ttu-id="34c14-252">각 등록 날짜에 대한 학생 수가 테이블에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-252">The count of students for each enrollment date is displayed in a table.</span></span>

![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

## <a name="optional-deploy-the-app-to-windows-azure"></a><span data-ttu-id="34c14-254">선택 사항: Windows Azure에 앱 배포</span><span class="sxs-lookup"><span data-stu-id="34c14-254">Optional: Deploy the app to Windows Azure</span></span>

<span data-ttu-id="34c14-255">지금까지 응용 프로그램은 개발 컴퓨터의 IIS Express에서 로컬로 실행 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-255">So far your application has been running locally in IIS Express on your development computer.</span></span> <span data-ttu-id="34c14-256">다른 사용자가 인터넷을 통해 사용할 수 있도록 하려면 웹 호스팅 공급자에 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-256">To make it available for other people to use over the Internet, you have to deploy it to a web hosting provider.</span></span> <span data-ttu-id="34c14-257">자습서의이 섹션에서는 Windows Azure 웹 사이트에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-257">In this optional section of the tutorial you'll deploy it to a Windows Azure Web Site.</span></span>

### <a name="using-code-first-migrations-to-deploy-the-database"></a><span data-ttu-id="34c14-258">Code First 마이그레이션를 사용 하 여 데이터베이스 배포</span><span class="sxs-lookup"><span data-stu-id="34c14-258">Using Code First Migrations to Deploy the Database</span></span>

<span data-ttu-id="34c14-259">데이터베이스를 배포 하려면 Code First 마이그레이션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-259">To deploy the database you'll use Code First Migrations.</span></span> <span data-ttu-id="34c14-260">Visual Studio에서 배포에 대 한 설정을 구성 하는 데 사용 하는 게시 프로필을 만들 때 **Code First 마이그레이션 실행 (응용 프로그램 시작 시 실행)** 이라는 레이블이 지정 된 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-260">When you create the publish profile that you use to configure settings for deploying from Visual Studio, you'll select a check box that is labeled **Execute Code First Migrations (runs on application start)**.</span></span> <span data-ttu-id="34c14-261">이 설정을 사용 하면 Code First 이니셜라이저 클래스를 사용 하도록 배포 프로세스에서 대상 서버의 응용 프로그램 *Web.config* 파일을 자동으로 구성 합니다 `MigrateDatabaseToLatestVersion` .</span><span class="sxs-lookup"><span data-stu-id="34c14-261">This setting causes the deployment process to automatically configure the application *Web.config* file on the destination server so that Code First uses the `MigrateDatabaseToLatestVersion` initializer class.</span></span>

<span data-ttu-id="34c14-262">Visual Studio는 배포 프로세스 중에 데이터베이스에서 어떤 작업도 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-262">Visual Studio does not do anything with the database during the deployment process.</span></span> <span data-ttu-id="34c14-263">배포 된 응용 프로그램이 배포 후 처음으로 데이터베이스에 액세스 하는 경우 Code First에서 자동으로 데이터베이스를 만들거나 데이터베이스 스키마를 최신 버전으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-263">When the deployed application accesses the database for the first time after deployment, Code First automatically creates the database or updates the database schema to the latest version.</span></span> <span data-ttu-id="34c14-264">응용 프로그램이 마이그레이션 방법을 구현 하는 경우이 `Seed` 메서드는 데이터베이스가 만들어지거나 스키마가 업데이트 된 후에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-264">If the application implements a Migrations `Seed` method, the method runs after the database is created or the schema is updated.</span></span>

<span data-ttu-id="34c14-265">마이그레이션 `Seed` 방법은 테스트 데이터를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-265">Your Migrations `Seed` method inserts test data.</span></span> <span data-ttu-id="34c14-266">프로덕션 환경에 배포 하는 경우 `Seed` 프로덕션 데이터베이스에 삽입 하려는 데이터만 삽입 하도록 메서드를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-266">If you were deploying to a production environment, you would have to change the `Seed` method so that it only inserts data that you want to be inserted into your production database.</span></span> <span data-ttu-id="34c14-267">예를 들어 현재 데이터 모델에서는 개발 데이터베이스에 실제 강의를 포함 하 고 가상 학생이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-267">For example, in your current data model you might want to have real courses but fictional students in the development database.</span></span> <span data-ttu-id="34c14-268">개발 중에를 `Seed` 로드 하는 메서드를 작성 한 다음 프로덕션에 배포 하기 전에 가상 학생을 주석으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-268">You can write a `Seed` method to load both in development, and then comment out the fictional students before you deploy to production.</span></span> <span data-ttu-id="34c14-269">또는 `Seed` 단지 강좌를 로드 하는 메서드를 작성 하 고 응용 프로그램의 UI를 사용 하 여 테스트 데이터베이스에 가상 학생을 수동으로 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-269">Or you can write a `Seed` method to load only courses, and enter the fictional students in the test database manually by using the application's UI.</span></span>

### <a name="get-a-windows-azure-account"></a><span data-ttu-id="34c14-270">Microsoft Azure 계정 가져오기</span><span class="sxs-lookup"><span data-stu-id="34c14-270">Get a Windows Azure account</span></span>

<span data-ttu-id="34c14-271">Microsoft Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-271">You'll need a Windows Azure account.</span></span> <span data-ttu-id="34c14-272">아직 없는 경우 몇 분만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-272">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="34c14-273">자세한 내용은 [Windows Azure 무료 평가판](https://azure.microsoft.com/free/dotnet/)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="34c14-273">For details, see [Windows Azure Free Trial](https://azure.microsoft.com/free/dotnet/).</span></span>

### <a name="create-a-web-site-and-a-sql-database-in-windows-azure"></a><span data-ttu-id="34c14-274">Microsoft Azure에서 웹 사이트 및 SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="34c14-274">Create a web site and a SQL database in Windows Azure</span></span>

<span data-ttu-id="34c14-275">Microsoft Azure 웹 사이트는 공유 호스팅 환경에서 실행 됩니다. 즉, 다른 Windows Azure 클라이언트와 공유 되는 Vm (가상 컴퓨터)에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-275">Your Windows Azure Web Site will run in a shared hosting environment, which means it runs on virtual machines (VMs) that are shared with other Windows Azure clients.</span></span> <span data-ttu-id="34c14-276">공유 호스팅 환경은 클라우드를 시작하는 저비용 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-276">A shared hosting environment is a low-cost way to get started in the cloud.</span></span> <span data-ttu-id="34c14-277">나중에 웹 트래픽이 증가하면 애플리케이션이 전용 VM에서 실행되어 요구에 맞게 확장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-277">Later, if your web traffic increases, the application can scale to meet the need by running on dedicated VMs.</span></span> <span data-ttu-id="34c14-278">더 복잡 한 아키텍처가 필요한 경우 Windows Azure 클라우드 서비스로 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-278">If you need a more complex architecture, you can migrate to a Windows Azure Cloud Service.</span></span> <span data-ttu-id="34c14-279">클라우드 서비스는 요구에 따라 구성할 수 있는 전용 VM에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-279">Cloud services run on dedicated VMs that you can configure according to your needs.</span></span>

<span data-ttu-id="34c14-280">Windows Azure SQL Database은 SQL Server 기술을 기반으로 구축 된 클라우드 기반의 관계형 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-280">Windows Azure SQL Database is a cloud-based relational database service that is built on SQL Server technologies.</span></span> <span data-ttu-id="34c14-281">SQL Server와 함께 작동 하는 도구 및 응용 프로그램은 SQL Database 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-281">Tools and applications that work with SQL Server also work with SQL Database.</span></span>

1. <span data-ttu-id="34c14-282">[Windows Azure 관리 포털](https://manage.windowsazure.com/)의 왼쪽 탭에서 **웹 사이트** 를 클릭 한 다음 **새로 만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-282">In the [Windows Azure Management Portal](https://manage.windowsazure.com/), click **Web Sites** in the left tab, and then click **New**.</span></span>

    ![관리 포털의 새 단추](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)
2. <span data-ttu-id="34c14-284">**사용자 지정 만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-284">Click **CUSTOM CREATE**.</span></span>

    ![관리 포털에서 데이터베이스 링크를 사용 하 여 만들기](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

   <span data-ttu-id="34c14-286">**새 웹 사이트-사용자 지정 만들기** 마법사가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-286">The **New Web Site - Custom Create** wizard opens.</span></span>
3. <span data-ttu-id="34c14-287">마법사의 **새 웹 사이트** 단계에서 **url** 상자에 문자열을 입력 하 여 응용 프로그램에 대 한 고유 url로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-287">In the **New Web Site** step of the wizard, enter a string in the **URL** box to use as the unique URL for your application.</span></span> <span data-ttu-id="34c14-288">전체 URL은 여기에 입력한 문자열과 텍스트 상자 옆에 표시되는 접미사로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-288">The complete URL will consist of what you enter here plus the suffix that you see next to the text box.</span></span> <span data-ttu-id="34c14-289">이 그림에는 "ConU"가 표시 되지만 해당 URL을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-289">The illustration shows "ConU", but that URL is probably taken so you will have to choose a different one.</span></span>

    ![관리 포털에서 데이터베이스 링크를 사용 하 여 만들기](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)
4. <span data-ttu-id="34c14-291">**지역** 드롭다운 목록에서 가까운 지역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-291">In the **Region** drop-down list, choose a region close to you.</span></span> <span data-ttu-id="34c14-292">이 설정은 웹 사이트를 실행 하는 데이터 센터를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-292">This setting specifies which data center your web site will run in.</span></span>
5. <span data-ttu-id="34c14-293">**데이터베이스** 드롭다운 목록에서 **무료 20Mb SQL 데이터베이스 만들기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-293">In the **Database** drop-down list, choose **Create a free 20 MB SQL database**.</span></span>

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)
6. <span data-ttu-id="34c14-294">**DB 연결 문자열 이름**에 *schoolcontext.cs*를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-294">In the **DB CONNECTION STRING NAME**, enter *SchoolContext*.</span></span>

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)
7. <span data-ttu-id="34c14-295">상자 아래쪽의 오른쪽을 가리키는 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-295">Click the arrow that points to the right at the bottom of the box.</span></span> <span data-ttu-id="34c14-296">마법사에서 **데이터베이스 설정** 단계로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-296">The wizard advances to the **Database Settings** step.</span></span>
8. <span data-ttu-id="34c14-297">**이름** 상자에 다음 *을 입력 합니다*.</span><span class="sxs-lookup"><span data-stu-id="34c14-297">In the **Name** box, enter *ContosoUniversityDB*.</span></span>
9. <span data-ttu-id="34c14-298">**서버** 상자에서 **새로 만들기 SQL Database 서버**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-298">In the **Server** box, select **New SQL Database server**.</span></span> <span data-ttu-id="34c14-299">또는 이전에 서버를 만든 경우 드롭다운 목록에서 해당 서버를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-299">Alternatively, if you previously created a server, you can select that server from the drop-down list.</span></span>
10. <span data-ttu-id="34c14-300">관리자 **로그인 이름** 및 **암호**를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-300">Enter an administrator **LOGIN NAME** and **PASSWORD**.</span></span> <span data-ttu-id="34c14-301">**New SQL Database 서버**를 선택한 경우 여기서 기존 이름과 암호를 입력하지 않고 나중에 데이터베이스에 액세스할 때 사용하기 위해 지금 정의하는 새 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-301">If you selected **New SQL Database server** you aren't entering an existing name and password here, you're entering a new name and password that you're defining now to use later when you access the database.</span></span> <span data-ttu-id="34c14-302">이전에 만든 서버를 선택한 경우 해당 서버에 대 한 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-302">If you selected a server that you created previously, you'll enter credentials for that server.</span></span> <span data-ttu-id="34c14-303">이 자습서에서는 ***고급*** 확인란을 선택 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-303">For this tutorial, you won't select the ***Advanced*** check box.</span></span> <span data-ttu-id="34c14-304">***고급*** 옵션을 사용 하 여 데이터베이스 [데이터 정렬을](https://msdn.microsoft.com/library/aa174903(v=SQL.80).aspx)설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-304">The ***Advanced*** options enable you to set the database [collation](https://msdn.microsoft.com/library/aa174903(v=SQL.80).aspx).</span></span>
11. <span data-ttu-id="34c14-305">웹 사이트에 대해 선택한 것과 동일한 **지역을** 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-305">Choose the same **Region** that you chose for the web site.</span></span>
12. <span data-ttu-id="34c14-306">상자 오른쪽 아래에 있는 확인 표시를 클릭 하 여 완료 되었음을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-306">Click the check mark at the bottom right of the box to indicate that you're finished.</span></span>   
  
    ![새 웹 사이트의 데이터베이스 설정 단계-데이터베이스 마법사를 사용 하 여 만들기](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image16.png)  

    <span data-ttu-id="34c14-308">다음 이미지는 기존 SQL Server 및 로그인을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-308">The following image shows using an existing SQL Server and Login.</span></span>   
  
    ![새 웹 사이트의 데이터베이스 설정 단계-데이터베이스 마법사를 사용 하 여 만들기](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image17.png)  
  
    <span data-ttu-id="34c14-310">관리 포털은 웹 사이트 페이지로 반환 되 고 **상태** 열에는 사이트가 만들어지고 있는 것으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-310">The Management Portal returns to the Web Sites page, and the **Status** column shows that the site is being created.</span></span> <span data-ttu-id="34c14-311">잠시 후 (일반적으로 1 분 미만) **상태** 열에는 사이트가 성공적으로 생성 된 것으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-311">After a while (typically less than a minute), the **Status** column shows that the site was successfully created.</span></span> <span data-ttu-id="34c14-312">왼쪽의 탐색 모음에서 계정에 있는 사이트 수가 **웹 사이트** 아이콘 옆에 나타나고 데이터베이스 수가 **SQL 데이터베이스** 아이콘 옆에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-312">In the navigation bar at the left, the number of sites you have in your account appears next to the **Web Sites** icon, and the number of databases appears next to the **SQL Databases** icon.</span></span>

## <a name="deploy-the-application-to-windows-azure"></a><span data-ttu-id="34c14-313">Windows Azure에 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="34c14-313">Deploy the application to Windows Azure</span></span>

1. <span data-ttu-id="34c14-314">Visual Studio의 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-314">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>  
  
    ![프로젝트 상황에 맞는 메뉴의 게시](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image18.png)
2. <span data-ttu-id="34c14-316">**웹 게시** 마법사의 **프로필** 탭에서 **가져오기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-316">In the **Profile** tab of the **Publish Web** wizard, click **Import**.</span></span>  
  
    ![게시 설정 가져오기](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image19.png)
3. <span data-ttu-id="34c14-318">이전에 Visual Studio에서 Windows Azure 구독을 추가 하지 않은 경우 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-318">If you have not previously added your Windows Azure subscription in Visual Studio, perform the following steps.</span></span> <span data-ttu-id="34c14-319">이러한 단계에서는 **Windows Azure 웹 사이트에서 가져오기** 아래의 드롭다운 목록에 웹 사이트가 포함 되도록 구독을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-319">In these steps you add your subscription so that the drop-down list under **Import from a Windows Azure web site** will include your web site.</span></span>

    <span data-ttu-id="34c14-320">a.</span><span class="sxs-lookup"><span data-stu-id="34c14-320">a.</span></span> <span data-ttu-id="34c14-321">**게시 프로필 가져오기** 대화 상자에서 **windows azure 웹 사이트에서 가져오기**를 클릭 한 다음 **windows azure 구독 추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-321">In the **Import Publish Profile** dialog box, click **Import from a Windows Azure web site**, and then click **Add Windows Azure subscription**.</span></span>

    ![Windows Azure 구독 추가](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image20.png)

    <span data-ttu-id="34c14-323">b.</span><span class="sxs-lookup"><span data-stu-id="34c14-323">b.</span></span> <span data-ttu-id="34c14-324">**Windows Azure 구독 가져오기** 대화 상자에서 **구독 파일 다운로드**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-324">In the **Import Windows Azure Subscriptions** dialog box, click **Download subscription file**.</span></span>

    ![구독 파일 다운로드](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image21.png)

    <span data-ttu-id="34c14-326">c.</span><span class="sxs-lookup"><span data-stu-id="34c14-326">c.</span></span> <span data-ttu-id="34c14-327">브라우저 창에서 *publishsettings* 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-327">In your browser window, save the *.publishsettings* file.</span></span>

    ![publishsettings 파일 다운로드](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image22.png)

    > [!WARNING]
    > <span data-ttu-id="34c14-329">보안- *publishsettings* 파일에는 microsoft Azure 구독 및 서비스를 관리 하는 데 사용 되는 자격 증명 (인코딩되지 않음)이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-329">Security - The *publishsettings* file contains your credentials (unencoded) that are used to administer your Windows Azure subscriptions and services.</span></span> <span data-ttu-id="34c14-330">이 파일에 대 한 보안 모범 사례는 원본 디렉터리 외부 (예: *: libraries\documents* 폴더)에 임시로 저장 한 다음 가져오기가 완료 되 면 삭제 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-330">The security best practice for this file is to store it temporarily outside your source directories (for example in the *Libraries\Documents* folder), and then delete it once the import has completed.</span></span> <span data-ttu-id="34c14-331">파일에 대 한 액세스 권한을 획득 하는 악의적인 사용자는 `.publishsettings` Microsoft Azure 서비스를 편집, 생성 및 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-331">A malicious user who gains access to the `.publishsettings` file can edit, create, and delete your Windows Azure services.</span></span>

    <span data-ttu-id="34c14-332">d.</span><span class="sxs-lookup"><span data-stu-id="34c14-332">d.</span></span> <span data-ttu-id="34c14-333">**Windows Azure 구독 가져오기** 대화 상자에서 **찾아보기** 를 클릭 하 고 *publishsettings* 파일로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-333">In the **Import Windows Azure Subscriptions** dialog box, click **Browse** and navigate to the *.publishsettings* file.</span></span>

    ![하위 다운로드](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image23.png)

    <span data-ttu-id="34c14-335">e.</span><span class="sxs-lookup"><span data-stu-id="34c14-335">e.</span></span> <span data-ttu-id="34c14-336">**가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-336">Click **Import**.</span></span>

    ![import](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image24.png)
4. <span data-ttu-id="34c14-338">**게시 프로필 가져오기** 대화 상자에서 **Windows Azure 웹 사이트에서 가져오기**를 선택 하 고 드롭다운 목록에서 웹 사이트를 선택한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-338">In the **Import Publish Profile** dialog box, select **Import from a Windows Azure web site**, select your web site from the drop-down list, and then click **OK**.</span></span>  
  
    ![게시 프로필 가져오기](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image25.png)
5. <span data-ttu-id="34c14-340">**연결** 탭에서 **연결 유효성 검사** 를 클릭 하 여 설정이 올바른지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-340">In the **Connection** tab, click **Validate Connection** to make sure that the settings are correct.</span></span>  
  
    ![연결 유효성 검사](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)
6. <span data-ttu-id="34c14-342">연결의 유효성을 검사 한 경우 **연결 유효성 검사** 단추 옆에 녹색 확인 표시가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-342">When the connection has been validated, a green check mark is shown next to the **Validate Connection** button.</span></span> <span data-ttu-id="34c14-343">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-343">Click **Next**.</span></span>  
  
    ![연결의 유효성을 검사 했습니다.](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image27.png)
7. <span data-ttu-id="34c14-345">**Schoolcontext.cs** 아래에 있는 **원격 연결 문자열** 드롭다운 목록을 열고 사용자가 만든 데이터베이스에 대 한 연결 문자열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-345">Open the **Remote connection string** drop-down list under **SchoolContext** and select the connection string for the database you created.</span></span>
8. <span data-ttu-id="34c14-346">**Code First 마이그레이션 실행 (응용 프로그램 시작 시 실행)** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-346">Select **Execute Code First Migrations (runs on application start)**.</span></span>
9. <span data-ttu-id="34c14-347">이 응용 프로그램에서 멤버 자격 데이터베이스를 사용 하지 않으므로 **Usercontext (defaultconnection)** 에 대해 **런타임에이 연결 문자열 사용** 을 선택 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-347">Uncheck **Use this connection string at runtime** for the **UserContext (DefaultConnection)**, since this application is not using the membership database.</span></span>   
  
    ![설정 탭](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image28.png)
10. <span data-ttu-id="34c14-349">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-349">Click **Next**.</span></span>
11. <span data-ttu-id="34c14-350">**미리 보기** 탭에서 **미리 보기 시작**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-350">In the **Preview** tab, click **Start Preview**.</span></span>  
  
    ![미리 보기 탭의 StartPreview 단추](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image29.png)  
  
    <span data-ttu-id="34c14-352">이 탭에는 서버에 복사 되는 파일의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-352">The tab displays a list of the files that will be copied to the server.</span></span> <span data-ttu-id="34c14-353">미리 보기를 표시 하는 것은 응용 프로그램을 게시 하는 데 필요 하지 않지만 인식 하기 위한 유용한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-353">Displaying the preview isn't required to publish the application but is a useful function to be aware of.</span></span> <span data-ttu-id="34c14-354">이 경우 표시 되는 파일 목록을 사용 하 여 아무런 작업을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-354">In this case, you don't need to do anything with the list of files that is displayed.</span></span> <span data-ttu-id="34c14-355">다음에이 응용 프로그램을 배포할 때 변경 된 파일만이 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-355">The next time you deploy this application, only the files that have changed will be in this list.</span></span>  
  
    ![StartPreview 파일 출력](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image30.png)
12. <span data-ttu-id="34c14-357">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-357">Click **Publish**.</span></span>  
    <span data-ttu-id="34c14-358">Visual Studio에서 Windows Azure 서버에 파일을 복사 하는 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-358">Visual Studio begins the process of copying the files to the Windows Azure server.</span></span>
13. <span data-ttu-id="34c14-359">**출력** 창에 수행된 배포 작업이 표시되고 성공적인 배포 완료가 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-359">The **Output** window shows what deployment actions were taken and reports successful completion of the deployment.</span></span>  
  
    ![성공적인 배포를 보고 하는 출력 창](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image31.png)
14. <span data-ttu-id="34c14-361">성공적으로 배포 되 면 배포 된 웹 사이트의 URL에 대 한 기본 브라우저가 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-361">Upon successful deployment, the default browser automatically opens to the URL of the deployed web site.</span></span>  
    <span data-ttu-id="34c14-362">만든 애플리케이션이 이제 클라우드에서 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-362">The application you created is now running in the cloud.</span></span> <span data-ttu-id="34c14-363">학생 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-363">Click the Students tab.</span></span>  
  
    ![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image32.png)

<span data-ttu-id="34c14-365">이제 **Code First 마이그레이션 실행 (앱 시작 시 실행)** 을 선택 했기 때문에 *schoolcontext.cs* 데이터베이스가 Windows Azure SQL Database에서 생성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-365">At this point your *SchoolContext* database has been created in the Windows Azure SQL Database because you selected **Execute Code First Migrations (runs on app start)**.</span></span> <span data-ttu-id="34c14-366">배포 된 웹 사이트의 *Web.config* 파일이 변경 되어 코드가 처음으로 데이터베이스에서 데이터를 읽거나 쓸 때 ( **학생** 탭을 선택 했을 때 발생) [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) 이니셜라이저가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-366">The *Web.config* file in the deployed web site has been changed so that the [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) initializer would run the first time your code reads or writes data in the database (which happened when you selected the **Students** tab):</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image33.png)

<span data-ttu-id="34c14-367">또한 배포 프로세스에서는 데이터베이스 스키마를 업데이트 하 고 데이터베이스를 시드 하는 데 사용할 Code First 마이그레이션에 대 한 새 연결 문자열 *(Schoolcontext.cs \_ databasepublish*)을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-367">The deployment process also created a new connection string *(SchoolContext\_DatabasePublish*) for Code First Migrations to use for updating the database schema and seeding the database.</span></span>

![연결 문자열 Database_Publish](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image34.png)

<span data-ttu-id="34c14-369">*Defaultconnection* 연결 문자열은 멤버 자격 데이터베이스 (이 자습서에서는 사용 하지 않음)에 대 한 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-369">The *DefaultConnection* connection string is for the membership database (which we are not using in this tutorial).</span></span> <span data-ttu-id="34c14-370">*Schoolcontext.cs* 연결 문자열은 ContosoUniversity 데이터베이스에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-370">The *SchoolContext* connection string is for the ContosoUniversity database.</span></span>

<span data-ttu-id="34c14-371">*ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*의 사용자 컴퓨터에서 Web.config 파일의 배포 된 버전을 찾을 수 있습니다. FTP를 사용 하 여 배포 된 *Web.config* 파일 자체에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-371">You can find the deployed version of the Web.config file on your own computer in *ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*. You can access the deployed *Web.config* file itself by using FTP.</span></span> <span data-ttu-id="34c14-372">지침은 [Visual Studio를 사용 하 여 웹 배포 ASP.NET: 코드 업데이트 배포](../../../../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="34c14-372">For instructions, see [ASP.NET Web Deployment using Visual Studio: Deploying a Code Update](../../../../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md).</span></span> <span data-ttu-id="34c14-373">"FTP 도구를 사용 하려면 FTP URL, 사용자 이름 및 암호를 사용 해야 합니다."로 시작 하는 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="34c14-373">Follow the instructions that start with "To use an FTP tool, you need three things: the FTP URL, the user name, and the password."</span></span>

> [!NOTE]
> <span data-ttu-id="34c14-374">웹 앱은 보안을 구현 하지 않으므로 URL을 검색 하는 모든 사용자가 데이터를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-374">The web app doesn't implement security, so anyone who finds the URL can change the data.</span></span> <span data-ttu-id="34c14-375">웹 사이트를 보호 하는 방법에 대 한 자세한 내용은 [Windows Azure 웹 사이트에 멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET MVC 앱 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="34c14-375">For instructions on how to secure the web site, see [Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to a Windows Azure Web Site](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="34c14-376">다른 사용자가 Visual Studio에서 Windows Azure 관리 포털 또는 **서버 탐색기** 를 사용 하 여 사이트를 사용 하지 못하도록 하 여 사이트를 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-376">You can prevent other people from using the site by using the Windows Azure Management Portal or **Server Explorer** in Visual Studio to stop the site.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image35.png)

## <a name="code-first-initializers"></a><span data-ttu-id="34c14-377">Code First 이니셜라이저</span><span class="sxs-lookup"><span data-stu-id="34c14-377">Code First Initializers</span></span>

<span data-ttu-id="34c14-378">배포 섹션에서 사용 되는 [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) 이니셜라이저를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-378">In the deployment section you saw the [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) initializer being used.</span></span> <span data-ttu-id="34c14-379">[Createdatabaseifnotexists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (기본값), [Dropcreatedatabaseifmodelchanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) 및 [dropcreatedatabasealways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx)를 포함 하 여 사용할 수 있는 다른 이니셜라이저가 Code First 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-379">Code First also provides other initializers that you can use, including [CreateDatabaseIfNotExists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (the default), [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) and [DropCreateDatabaseAlways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx).</span></span> <span data-ttu-id="34c14-380">`DropCreateAlways`이니셜라이저는 단위 테스트에 대 한 조건을 설정 하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-380">The `DropCreateAlways` initializer can be useful for setting up conditions for unit tests.</span></span> <span data-ttu-id="34c14-381">사용자 고유의 이니셜라이저를 작성 하 고 응용 프로그램이 데이터베이스에서 읽거나 데이터베이스에 쓸 때까지 기다리지 않으려는 경우 이니셜라이저를 명시적으로 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-381">You can also write your own initializers, and you can call an initializer explicitly if you don't want to wait until the application reads from or writes to the database.</span></span> <span data-ttu-id="34c14-382">이니셜라이저에 대 한 자세한 설명은 Julie Lerman 및 Rowan에서 Code First 하는 책 [프로그래밍 Entity Framework](http://shop.oreilly.com/product/0636920022220.do) 의 6 장을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="34c14-382">For a comprehensive explanation of initializers, see chapter 6 of the book [Programming Entity Framework: Code First](http://shop.oreilly.com/product/0636920022220.do) by Julie Lerman and Rowan Miller.</span></span>

## <a name="summary"></a><span data-ttu-id="34c14-383">요약</span><span class="sxs-lookup"><span data-stu-id="34c14-383">Summary</span></span>

<span data-ttu-id="34c14-384">이 자습서에서는 데이터 모델을 만들고 기본 CRUD, 정렬, 필터링, 페이징 및 그룹화 기능을 구현 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-384">In this tutorial you've seen how to create a data model and implement basic CRUD, sorting, filtering, paging, and grouping functionality.</span></span> <span data-ttu-id="34c14-385">다음 자습서에서는 데이터 모델을 확장 하 여 고급 항목을 확인 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-385">In the next tutorial you'll begin looking at more advanced topics by expanding the data model.</span></span>

<span data-ttu-id="34c14-386">[ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c14-386">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="34c14-387">[이전](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
> [다음](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="34c14-387">[Previous](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
[Next](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)</span></span>
