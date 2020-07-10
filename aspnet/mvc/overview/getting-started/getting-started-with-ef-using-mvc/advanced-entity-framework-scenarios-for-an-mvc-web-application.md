---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: '자습서: MVC 5 웹 앱에 대 한 고급 EF 시나리오 알아보기'
description: 이 자습서에는 Entity Framework Code First를 사용 하는 ASP.NET 웹 응용 프로그램을 개발 하는 기본 사항을 벗어날 때 알아 두어야 하는 몇 가지 항목이 소개 되어 있습니다.
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: f35a9b0c-49ef-4cde-b06d-19d1543feb0b
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: d7cc83a5b78a60f575f5c3065079679189296a0c
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "86188737"
---
# <a name="tutorial-learn-about-advanced-ef-scenarios-for-an-mvc-5-web-app"></a><span data-ttu-id="17222-103">자습서: MVC 5 웹 앱에 대 한 고급 EF 시나리오 알아보기</span><span class="sxs-lookup"><span data-stu-id="17222-103">Tutorial: Learn about advanced EF Scenarios for an MVC 5 Web app</span></span>

<span data-ttu-id="17222-104">이전 자습서에서는 계층당 하나의 테이블 상속을 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-104">In the previous tutorial you implemented table-per-hierarchy inheritance.</span></span> <span data-ttu-id="17222-105">이 자습서에는 Entity Framework Code First를 사용 하는 ASP.NET 웹 응용 프로그램을 개발 하는 기본 사항을 벗어날 때 알아 두어야 하는 몇 가지 항목이 소개 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-105">This tutorial includes introduces several topics that are useful to be aware of when you go beyond the basics of developing ASP.NET web applications that use Entity Framework Code First.</span></span> <span data-ttu-id="17222-106">첫 번째 섹션에는 코드를 안내 하 고 Visual Studio를 사용 하 여 작업을 완료 하는 단계별 지침이 나와 있습니다. 다음 섹션에서는 간략 한 소개와 함께 몇 가지 항목을 소개 하 고 자세한 내용을 보려면 리소스에 대 한 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-106">The first few sections have step-by-step instructions that walk you through the code and using Visual Studio to complete tasks The sections that follow introduce several topics with brief introductions followed by links to resources for more information.</span></span>

<span data-ttu-id="17222-107">이러한 항목의 대부분은 이미 만든 페이지를 사용 하 여 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-107">For most of these topics, you'll work with pages that you already created.</span></span> <span data-ttu-id="17222-108">원시 SQL을 사용 하 여 대량 업데이트를 수행 하려면 데이터베이스에 있는 모든 과정의 크레딧 수를 업데이트 하는 새 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17222-108">To use raw SQL to do bulk updates you'll create a new page that updates the number of credits of all courses in the database:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

<span data-ttu-id="17222-110">이 자습서에서는 다음과 같은 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-110">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="17222-111">원시 SQL 쿼리 수행</span><span class="sxs-lookup"><span data-stu-id="17222-111">Perform raw SQL queries</span></span>
> * <span data-ttu-id="17222-112">추적 안 함 쿼리 수행</span><span class="sxs-lookup"><span data-stu-id="17222-112">Perform no-tracking queries</span></span>
> * <span data-ttu-id="17222-113">데이터베이스로 전송 되는 SQL 쿼리 검사</span><span class="sxs-lookup"><span data-stu-id="17222-113">Examine SQL queries sent to database</span></span>

<span data-ttu-id="17222-114">다음에 대해서도 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="17222-114">You also learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="17222-115">추상화 계층 만들기</span><span class="sxs-lookup"><span data-stu-id="17222-115">Creating an abstraction layer</span></span>
> * <span data-ttu-id="17222-116">프록시 클래스</span><span class="sxs-lookup"><span data-stu-id="17222-116">Proxy classes</span></span>
> * <span data-ttu-id="17222-117">자동 변경 내용 검색</span><span class="sxs-lookup"><span data-stu-id="17222-117">Automatic change detection</span></span>
> * <span data-ttu-id="17222-118">자동 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="17222-118">Automatic validation</span></span>
> * <span data-ttu-id="17222-119">Entity Framework 파워 도구</span><span class="sxs-lookup"><span data-stu-id="17222-119">Entity Framework Power Tools</span></span>
> * <span data-ttu-id="17222-120">소스 코드 Entity Framework</span><span class="sxs-lookup"><span data-stu-id="17222-120">Entity Framework source code</span></span>

## <a name="prerequisite"></a><span data-ttu-id="17222-121">필수 조건</span><span class="sxs-lookup"><span data-stu-id="17222-121">Prerequisite</span></span>

* [<span data-ttu-id="17222-122">상속 구현</span><span class="sxs-lookup"><span data-stu-id="17222-122">Implementing Inheritance</span></span>](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="perform-raw-sql-queries"></a><span data-ttu-id="17222-123">원시 SQL 쿼리 수행</span><span class="sxs-lookup"><span data-stu-id="17222-123">Perform raw SQL queries</span></span>

<span data-ttu-id="17222-124">Entity Framework Code First API에는 SQL 명령을 데이터베이스에 직접 전달할 수 있는 메서드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-124">The Entity Framework Code First API includes methods that enable you to pass SQL commands directly to the database.</span></span> <span data-ttu-id="17222-125">다음과 같은 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-125">You have the following options:</span></span>

- <span data-ttu-id="17222-126">엔터티 형식을 반환 하는 쿼리에 대해 [Dbset](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx) 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-126">Use the [DbSet.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx) method for queries that return entity types.</span></span> <span data-ttu-id="17222-127">반환 된 개체는 개체에 필요한 형식 이어야 `DbSet` 하며, 추적을 해제 하지 않는 한 데이터베이스 컨텍스트에 의해 자동으로 추적 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17222-127">The returned objects must be of the type expected by the `DbSet` object, and they are automatically tracked by the database context unless you turn tracking off.</span></span> <span data-ttu-id="17222-128">[AsNoTracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx) 메서드에 대 한 다음 섹션을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="17222-128">(See the following section about the [AsNoTracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx) method.)</span></span>
- <span data-ttu-id="17222-129">엔터티가 아닌 형식을 반환 하는 쿼리에는 [SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx) 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-129">Use the [Database.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx) method for queries that return types that aren't entities.</span></span> <span data-ttu-id="17222-130">이 메서드를 사용하여 엔터티 형식을 검색하더라도 반환된 데이터는 데이터베이스 컨텍스트에 의해 추적되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-130">The returned data isn't tracked by the database context, even if you use this method to retrieve entity types.</span></span>
- <span data-ttu-id="17222-131">쿼리가 아닌 명령에 [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx) 를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-131">Use the [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx) for non-query commands.</span></span>

<span data-ttu-id="17222-132">Entity Framework를 사용할 때 장점 중 하나는 코드가 데이터를 저장하는 특정 메서드에 너무 얽매이지 않아도 된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="17222-132">One of the advantages of using the Entity Framework is that it avoids tying your code too closely to a particular method of storing data.</span></span> <span data-ttu-id="17222-133">이것은 사용자를 위한 SQL 쿼리와 명령이 생성되므로 가능하며 사용자는 코드를 직접 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-133">It does this by generating SQL queries and commands for you, which also frees you from having to write them yourself.</span></span> <span data-ttu-id="17222-134">그러나 수동으로 만든 특정 SQL 쿼리를 실행 해야 하는 경우에는 예외적인 시나리오가 있습니다. 이러한 방법을 사용 하면 이러한 예외를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-134">But there are exceptional scenarios when you need to run specific SQL queries that you have manually created, and these methods make it possible for you to handle such exceptions.</span></span>

<span data-ttu-id="17222-135">웹 애플리케이션에서 SQL 명령을 실행할 때 항상 그렇듯이 SQL 삽입 공격으로부터 사이트를 보호하기 위한 예방 조치를 취해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-135">As is always true when you execute SQL commands in a web application, you must take precautions to protect your site against SQL injection attacks.</span></span> <span data-ttu-id="17222-136">이를 수행하는 한 가지 방법은 매개 변수가 있는 쿼리를 사용하여 웹 페이지에서 제출한 문자열을 SQL 명령으로 해석할 수 없도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="17222-136">One way to do that is to use parameterized queries to make sure that strings submitted by a web page can't be interpreted as SQL commands.</span></span> <span data-ttu-id="17222-137">이 자습서에서는 사용자 입력을 쿼리에 통합할 때 매개 변수가 있는 쿼리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-137">In this tutorial you'll use parameterized queries when integrating user input into a query.</span></span>

### <a name="calling-a-query-that-returns-entities"></a><span data-ttu-id="17222-138">엔터티를 반환 하는 쿼리 호출</span><span class="sxs-lookup"><span data-stu-id="17222-138">Calling a Query that Returns Entities</span></span>

<span data-ttu-id="17222-139">[Dbset &lt; &gt; ](https://msdn.microsoft.com/library/gg696460.aspx) 엔터티 클래스는 형식의 엔터티를 반환 하는 쿼리를 실행 하는 데 사용할 수 있는 메서드를 제공 합니다 `TEntity` .</span><span class="sxs-lookup"><span data-stu-id="17222-139">The [DbSet&lt;TEntity&gt;](https://msdn.microsoft.com/library/gg696460.aspx) class provides a method that you can use to execute a query that returns an entity of type `TEntity`.</span></span> <span data-ttu-id="17222-140">이 기능이 어떻게 작동 하는지 확인 하려면 `Details` 컨트롤러의 메서드에서 코드를 변경 `Department` 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-140">To see how this works you'll change the code in the `Details` method of the `Department` controller.</span></span>

<span data-ttu-id="17222-141">*DepartmentController.cs*의 `Details` 메서드에서 `db.Departments.FindAsync` `db.Departments.SqlQuery` 다음 강조 표시 된 코드에 표시 된 것 처럼 메서드 호출을 메서드 호출로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="17222-141">In *DepartmentController.cs*, in the `Details` method, replace the `db.Departments.FindAsync` method call with a `db.Departments.SqlQuery` method call, as shown in the following highlighted code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs?highlight=8-14)]

<span data-ttu-id="17222-142">새 코드가 올바르게 작동하는지 확인하려면 **부서** 탭을 선택한 후 부서 중 하나에 대해 **세부 정보**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-142">To verify that the new code works correctly, select the **Departments** tab and then **Details** for one of the departments.</span></span> <span data-ttu-id="17222-143">모든 데이터가 예상 대로 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-143">Make sure all of the data displays as expected.</span></span>

### <a name="calling-a-query-that-returns-other-types-of-objects"></a><span data-ttu-id="17222-144">다른 형식의 개체를 반환 하는 쿼리 호출</span><span class="sxs-lookup"><span data-stu-id="17222-144">Calling a Query that Returns Other Types of Objects</span></span>

<span data-ttu-id="17222-145">이전에 등록 날짜별로 학생 수를 보여주는 [정보] 페이지의 학생 통계 표를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-145">Earlier you created a student statistics grid for the About page that showed the number of students for each enrollment date.</span></span> <span data-ttu-id="17222-146">*HomeController.cs* 에서이 작업을 수행 하는 코드는 LINQ를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-146">The code that does this in *HomeController.cs* uses LINQ:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

<span data-ttu-id="17222-147">LINQ를 사용 하지 않고 SQL에서 직접이 데이터를 검색 하는 코드를 작성 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-147">Suppose you want to write the code that retrieves this data directly in SQL rather than using LINQ.</span></span> <span data-ttu-id="17222-148">이렇게 하려면 엔터티 개체가 아닌 다른 항목을 반환 하는 쿼리를 실행 해야 합니다. 즉, [SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx) 메서드를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-148">To do that you need to run a query that returns something other than entity objects, which means you need to use the [Database.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx) method.</span></span>

<span data-ttu-id="17222-149">*HomeController.cs*에서 `About` 다음 강조 표시 된 코드에 표시 된 것 처럼 메서드의 LINQ 문을 SQL 문으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="17222-149">In *HomeController.cs*, replace the LINQ statement in the `About` method with a SQL statement, as shown in the following highlighted code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs?highlight=3-18)]

<span data-ttu-id="17222-150">정보 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-150">Run the About page.</span></span> <span data-ttu-id="17222-151">이전에 수행한 것과 동일한 데이터를 표시 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-151">Verify that it displays the same data it did before.</span></span>

### <a name="calling-an-update-query"></a><span data-ttu-id="17222-152">업데이트 쿼리 호출</span><span class="sxs-lookup"><span data-stu-id="17222-152">Calling an Update Query</span></span>

<span data-ttu-id="17222-153">Contoso 대학 관리자가 모든 과정에 대 한 크레딧 수를 변경 하는 등 데이터베이스에서 대량 변경을 수행할 수 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-153">Suppose Contoso University administrators want to be able to perform bulk changes in the database, such as changing the number of credits for every course.</span></span> <span data-ttu-id="17222-154">대학에 과목이 많은 경우 엔터티로 모두 검색하여 개별적으로 변경하는 것은 비효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="17222-154">If the university has a large number of courses, it would be inefficient to retrieve them all as entities and change them individually.</span></span> <span data-ttu-id="17222-155">이 섹션에서는 사용자가 모든 과정에 대 한 크레딧 수를 변경 하는 인수를 지정할 수 있는 웹 페이지를 구현 하 고 SQL 문을 실행 하 여 변경 작업을 수행 합니다 `UPDATE` .</span><span class="sxs-lookup"><span data-stu-id="17222-155">In this section you'll implement a web page that enables the user to specify a factor by which to change the number of credits for all courses, and you'll make the change by executing a SQL `UPDATE` statement.</span></span> 

<span data-ttu-id="17222-156">*CourseController.cs*에서 `UpdateCourseCredits` 및에 대 한 메서드를 추가 합니다 `HttpGet` `HttpPost` .</span><span class="sxs-lookup"><span data-stu-id="17222-156">In *CourseController.cs*, add `UpdateCourseCredits` methods for `HttpGet` and `HttpPost`:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

<span data-ttu-id="17222-157">컨트롤러에서 요청을 처리할 때 `HttpGet` 변수에 아무 것도 반환 되지 `ViewBag.RowsAffected` 않고, 뷰에 빈 텍스트 상자와 제출 단추가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17222-157">When the controller processes an `HttpGet` request, nothing is returned in the `ViewBag.RowsAffected` variable, and the view displays an empty text box and a submit button.</span></span>

<span data-ttu-id="17222-158">**업데이트** 단추를 클릭 하면 `HttpPost` 메서드가 호출 되 고 `multiplier` 텍스트 상자에 입력 된 값이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17222-158">When the **Update** button is clicked, the `HttpPost` method is called, and `multiplier` has the value entered in the text box.</span></span> <span data-ttu-id="17222-159">그런 다음 코드는 과정을 업데이트 하는 SQL을 실행 하 고 영향을 받는 행 수를 변수의 뷰에 반환 합니다 `ViewBag.RowsAffected` .</span><span class="sxs-lookup"><span data-stu-id="17222-159">The code then executes the SQL that updates courses and returns the number of affected rows to the view in the `ViewBag.RowsAffected` variable.</span></span> <span data-ttu-id="17222-160">뷰가 해당 변수에서 값을 가져오는 경우 텍스트 상자 및 제출 단추 대신 업데이트 된 행 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-160">When the view gets a value in that variable, it displays the number of rows updated instead of the text box and submit button.</span></span>

<span data-ttu-id="17222-161">*CourseController.cs*에서 메서드 중 하나를 마우스 오른쪽 단추로 클릭 한 `UpdateCourseCredits` 다음 **뷰 추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-161">In *CourseController.cs*, right-click one of the `UpdateCourseCredits` methods, and then click **Add View**.</span></span> <span data-ttu-id="17222-162">**뷰 추가** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="17222-162">The **Add View** dialog appears.</span></span> <span data-ttu-id="17222-163">기본값을 그대로 두고 **추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-163">Leave the defaults and select **Add**.</span></span>

<span data-ttu-id="17222-164">*Views\Course\UpdateCourseCredits.cshtml*에서 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="17222-164">In *Views\Course\UpdateCourseCredits.cshtml*, replace the template code with the following code:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cshtml)]

<span data-ttu-id="17222-165">**Courses(과정)** 탭을 선택하여 `UpdateCourseCredits` 메서드를 실행한 후 브라우저의 주소 표시줄에서 URL 끝에 "/UpdateCourseCredits"를 추가합니다(예: `http://localhost:50205/Course/UpdateCourseCredits`).</span><span class="sxs-lookup"><span data-stu-id="17222-165">Run the `UpdateCourseCredits` method by selecting the **Courses** tab, then adding "/UpdateCourseCredits" to the end of the URL in the browser's address bar (for example: `http://localhost:50205/Course/UpdateCourseCredits`).</span></span> <span data-ttu-id="17222-166">텍스트 상자에 숫자를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-166">Enter a number in the text box:</span></span>

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

<span data-ttu-id="17222-168">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-168">Click **Update**.</span></span> <span data-ttu-id="17222-169">영향을 받는 행 수가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17222-169">You see the number of rows affected.</span></span>

<span data-ttu-id="17222-170">학점 수가 수정된 과정 목록을 보려면 **목록으로 돌아가기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-170">Click **Back to List** to see the list of courses with the revised number of credits.</span></span>

<span data-ttu-id="17222-171">원시 SQL 쿼리에 대 한 자세한 내용은 MSDN의 [원시 Sql 쿼리](https://msdn.microsoft.com/data/jj592907) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="17222-171">For more information about raw SQL queries, see [Raw SQL Queries](https://msdn.microsoft.com/data/jj592907) on MSDN.</span></span>

## <a name="no-tracking-queries"></a><span data-ttu-id="17222-172">비 추적 쿼리</span><span class="sxs-lookup"><span data-stu-id="17222-172">No-tracking queries</span></span>

<span data-ttu-id="17222-173">데이터베이스 컨텍스트가 테이블 행을 검색하고 해당 내용을 나타내는 엔터티 개체를 만드는 경우 기본적으로 메모리의 엔터티가 데이터베이스의 해당 내용과 동기화 상태인지 여부의 추적을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-173">When a database context retrieves table rows and creates entity objects that represent them, by default it keeps track of whether the entities in memory are in sync with what's in the database.</span></span> <span data-ttu-id="17222-174">메모리의 데이터는 캐시의 역할을 하고 엔터티를 업데이트할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="17222-174">The data in memory acts as a cache and is used when you update an entity.</span></span> <span data-ttu-id="17222-175">컨텍스트 인스턴스는 일반적으로 수명이 짧으며(각 요청에 대해 새 것이 만들어지고 삭제됨) 엔터티를 읽는 컨텍스트는 일반적으로 해당 엔터티가 다시 사용되기 전에 삭제되므로 이 캐싱은 웹 애플리케이션에 종종 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-175">This caching is often unnecessary in a web application because context instances are typically short-lived (a new one is created and disposed for each request) and the context that reads an entity is typically disposed before that entity is used again.</span></span>

<span data-ttu-id="17222-176">[AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) 메서드를 사용 하 여 메모리에서 엔터티 개체 추적을 사용 하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-176">You can disable tracking of entity objects in memory by using the [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) method.</span></span> <span data-ttu-id="17222-177">이러한 작업을 수행할 수 있는 일반적인 시나리오는 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-177">Typical scenarios in which you might want to do that include the following:</span></span>

- <span data-ttu-id="17222-178">쿼리는 추적 기능을 해제 하는 대량의 데이터를 검색 하 여 성능을 현저 하 게 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-178">A query retrieves such a large volume of data that turning off tracking might noticeably enhance performance.</span></span>
- <span data-ttu-id="17222-179">엔터티를 업데이트 하기 위해 연결 하려고 하지만 이전에 다른 용도로 동일한 엔터티를 검색 했습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-179">You want to attach an entity in order to update it, but you earlier retrieved the same entity for a different purpose.</span></span> <span data-ttu-id="17222-180">엔터티는 데이터베이스 컨텍스트에서 이미 추적 중이므로 변경하려는 엔터티를 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-180">Because the entity is already being tracked by the database context, you can't attach the entity that you want to change.</span></span> <span data-ttu-id="17222-181">이러한 상황을 처리 하는 한 가지 방법은 `AsNoTracking` 이전 쿼리와 함께 옵션을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="17222-181">One way to handle this situation is to use the `AsNoTracking` option with the earlier query.</span></span>

<span data-ttu-id="17222-182">[AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) 메서드를 사용 하는 방법을 보여 주는 예제는 [이 자습서의 이전 버전](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="17222-182">For an example that demonstrates how to use the [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) method, see [the earlier version of this tutorial](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md).</span></span> <span data-ttu-id="17222-183">이 자습서 버전은 Edit 메서드에서 모델 바인더에서 만든 엔터티에 수정 된 플래그를 설정 하지 않으므로 필요 하지 않습니다 `AsNoTracking` .</span><span class="sxs-lookup"><span data-stu-id="17222-183">This version of the tutorial doesn't set the Modified flag on a model-binder-created entity in the Edit method, so it doesn't need `AsNoTracking`.</span></span>

## <a name="examine-sql-sent-to-database"></a><span data-ttu-id="17222-184">데이터베이스로 전송 되는 SQL 검사</span><span class="sxs-lookup"><span data-stu-id="17222-184">Examine SQL sent to database</span></span>

<span data-ttu-id="17222-185">때로는 데이터베이스로 전송된 실제 SQL 쿼리를 볼 수 있는 것이 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17222-185">Sometimes it's helpful to be able to see the actual SQL queries that are sent to the database.</span></span> <span data-ttu-id="17222-186">이전 자습서에서는 인터셉터 코드에서이 작업을 수행 하는 방법을 살펴보았습니다. 이제 인터셉터 코드를 작성 하지 않고이 작업을 수행 하는 몇 가지 방법이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-186">In an earlier tutorial you saw how to do that in interceptor code; now you'll see some ways to do it without writing interceptor code.</span></span> <span data-ttu-id="17222-187">이 작업을 수행 하려면 간단한 쿼리를 살펴본 다음 즉시 로드, 필터링, 정렬 등의 옵션을 추가할 때 발생 하는 상황을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-187">To try this out, you'll look at a simple query and then look at what happens to it as you add options such eager loading, filtering, and sorting.</span></span>

<span data-ttu-id="17222-188">*Controller/CourseController*에서 `Index` 메서드를 다음 코드로 바꾸어 즉시 로드를 일시적으로 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-188">In *Controllers/CourseController*, replace the `Index` method with the following code, in order to temporarily stop eager loading:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

<span data-ttu-id="17222-189">이제 문에 중단점을 설정 `return` 합니다 (해당 줄에서 커서를 사용 하 여 F9).</span><span class="sxs-lookup"><span data-stu-id="17222-189">Now set a breakpoint on the `return` statement (F9 with the cursor on that line).</span></span> <span data-ttu-id="17222-190">**F5** 키를 눌러 디버그 모드에서 프로젝트를 실행 하 고 과정 인덱스 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-190">Press **F5** to run the project in debug mode, and select the Course Index page.</span></span> <span data-ttu-id="17222-191">코드가 중단점에 도달 하면 변수를 검사 `sql` 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-191">When the code reaches the breakpoint, examine the `sql` variable.</span></span> <span data-ttu-id="17222-192">SQL Server로 전송 된 쿼리가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17222-192">You see the query that's sent to SQL Server.</span></span> <span data-ttu-id="17222-193">간단한 `Select` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="17222-193">It's a simple `Select` statement.</span></span>

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.json)]

<span data-ttu-id="17222-194">**텍스트 시각화 도우미**에서 쿼리를 보려면 돋보기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-194">Click the magnifying glass to see the query in the **Text Visualizer**.</span></span>

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

<span data-ttu-id="17222-195">이제 사용자가 특정 부서에 대해 필터링 할 수 있도록 강좌 인덱스 페이지에 드롭다운 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-195">Now you'll add a drop-down list to the Courses Index page so that users can filter for a particular department.</span></span> <span data-ttu-id="17222-196">코스를 제목별로 정렬 하 고 탐색 속성에 대해 즉시 로드를 지정 `Department` 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-196">You'll sort the courses by title, and you'll specify eager loading for the `Department` navigation property.</span></span>

<span data-ttu-id="17222-197">*CourseController.cs*에서 `Index` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="17222-197">In *CourseController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

<span data-ttu-id="17222-198">문에 중단점을 복원 `return` 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-198">Restore the breakpoint on the `return` statement.</span></span>

<span data-ttu-id="17222-199">메서드는 매개 변수의 드롭다운 목록에서 선택한 값을 받습니다 `SelectedDepartment` .</span><span class="sxs-lookup"><span data-stu-id="17222-199">The method receives the selected value of the drop-down list in the `SelectedDepartment` parameter.</span></span> <span data-ttu-id="17222-200">아무 것도 선택 하지 않으면이 매개 변수는 null이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17222-200">If nothing is selected, this parameter will be null.</span></span>

<span data-ttu-id="17222-201">`SelectList`모든 부서를 포함 하는 컬렉션은 드롭다운 목록에 대 한 보기로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17222-201">A `SelectList` collection containing all departments is passed to the view for the drop-down list.</span></span> <span data-ttu-id="17222-202">생성자에 전달 된 매개 변수는 `SelectList` 값 필드 이름, 텍스트 필드 이름 및 선택 된 항목을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-202">The parameters passed to the `SelectList` constructor specify the value field name, the text field name, and the selected item.</span></span>

<span data-ttu-id="17222-203">`Get`리포지토리의 메서드에 대해 `Course` 코드는 탐색 속성에 대 한 필터 식, 정렬 순서 및 즉시 로드를 지정 합니다 `Department` .</span><span class="sxs-lookup"><span data-stu-id="17222-203">For the `Get` method of the `Course` repository, the code specifies a filter expression, a sort order, and eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="17222-204">`true`드롭다운 목록에서 선택 된 항목이 없는 경우 (즉, null 임) 필터 식은 항상를 반환 합니다 `SelectedDepartment` .</span><span class="sxs-lookup"><span data-stu-id="17222-204">The filter expression always returns `true` if nothing is selected in the drop-down list (that is, `SelectedDepartment` is null).</span></span>

<span data-ttu-id="17222-205">*Views\Course\Index.cshtml*에서 여는 태그 바로 앞에 `table` 다음 코드를 추가 하 여 드롭다운 목록과 제출 단추를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17222-205">In *Views\Course\Index.cshtml*, immediately before the opening `table` tag, add the following code to create the drop-down list and a submit button:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

<span data-ttu-id="17222-206">중단점이 여전히 설정 된 상태에서 과정 인덱스 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-206">With the breakpoint still set, run the Course Index page.</span></span> <span data-ttu-id="17222-207">코드가 중단점에 처음으로 이동 하 여 페이지가 브라우저에 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-207">Continue through the first times that the code hits a breakpoint, so that the page is displayed in the browser.</span></span> <span data-ttu-id="17222-208">드롭다운 목록에서 부서를 선택 하 고 **필터**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-208">Select a department from the drop-down list and click **Filter**.</span></span>

<span data-ttu-id="17222-209">이번에는 드롭다운 목록에 대 한 부서 쿼리의 첫 번째 중단점이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17222-209">This time the first breakpoint will be for the departments query for the drop-down list.</span></span> <span data-ttu-id="17222-210">이를 건너뛰고 다음에 `query` 코드가 중단점에 도달 했을 때 해당 변수가 어떻게 표시 되는지 확인 합니다 `Course` .</span><span class="sxs-lookup"><span data-stu-id="17222-210">Skip that and view the `query` variable the next time the code reaches the breakpoint in order to see what the `Course` query now looks like.</span></span> <span data-ttu-id="17222-211">다음과 같은 내용이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17222-211">You'll see something like the following:</span></span>

[!code-sql[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.sql)]

<span data-ttu-id="17222-212">이제 쿼리는 `JOIN` `Department` 데이터와 함께 데이터를 로드 하는 쿼리 `Course` 이며 절이 포함 되어 있음을 알 수 있습니다 `WHERE` .</span><span class="sxs-lookup"><span data-stu-id="17222-212">You can see that the query is now a `JOIN` query that loads `Department` data along with the `Course` data, and that it includes a `WHERE` clause.</span></span>

<span data-ttu-id="17222-213">줄을 제거 `var sql = courses.ToString()` 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-213">Remove the `var sql = courses.ToString()` line.</span></span>

## <a name="create-an-abstraction-layer"></a><span data-ttu-id="17222-214">추상화 계층 만들기</span><span class="sxs-lookup"><span data-stu-id="17222-214">Create an abstraction layer</span></span>

<span data-ttu-id="17222-215">대부분의 개발자는 리포지토리 및 작업 패턴 단위를 구현하기 위한 코드를 Entity Framework에서 작동하는 코드를 둘러싼 래퍼로 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-215">Many developers write code to implement the repository and unit of work patterns as a wrapper around code that works with the Entity Framework.</span></span> <span data-ttu-id="17222-216">이러한 패턴은 애플리케이션의 데이터 액세스 계층 및 비즈니스 논리 계층 간에 추상화 계층을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="17222-216">These patterns are intended to create an abstraction layer between the data access layer and the business logic layer of an application.</span></span> <span data-ttu-id="17222-217">이러한 패턴을 구현하면 데이터 저장소의 변경 내용으로부터 애플리케이션을 격리할 수 있으며 자동화된 단위 테스트 또는 TDD(테스트 중심 개발)를 용이하게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-217">Implementing these patterns can help insulate your application from changes in the data store and can facilitate automated unit testing or test-driven development (TDD).</span></span> <span data-ttu-id="17222-218">그러나 이러한 패턴을 구현 하는 추가 코드를 작성 하는 것은 여러 가지 이유로 EF를 사용 하는 응용 프로그램에는 적합 한 선택이 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-218">However, writing additional code to implement these patterns is not always the best choice for applications that use EF, for several reasons:</span></span>

- <span data-ttu-id="17222-219">EF 컨텍스트 클래스 자체에서 데이터 저장소별 코드로부터 사용자 코드를 격리합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-219">The EF context class itself insulates your code from data-store-specific code.</span></span>
- <span data-ttu-id="17222-220">EF 컨텍스트 클래스는 EF를 사용하여 수행하는 데이터베이스 업데이트에 대해 작업 단위 클래스로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-220">The EF context class can act as a unit-of-work class for database updates that you do using EF.</span></span>
- <span data-ttu-id="17222-221">Entity Framework 6에서 도입 된 기능을 사용 하면 리포지토리 코드를 작성 하지 않고도 TDD를 보다 쉽게 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-221">Features introduced in Entity Framework 6 make it easier to implement TDD without writing repository code.</span></span>

<span data-ttu-id="17222-222">리포지토리 및 작업 단위 패턴을 구현 하는 방법에 대 한 자세한 내용은 [이 자습서 시리즈의 Entity Framework 5 버전](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="17222-222">For more information about how to implement the repository and unit of work patterns, see [the Entity Framework 5 version of this tutorial series](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="17222-223">Entity Framework 6에서 TDD를 구현 하는 방법에 대 한 자세한 내용은 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="17222-223">For information about ways to implement TDD in Entity Framework 6, see the following resources:</span></span>

- [<span data-ttu-id="17222-224">EF6에서 모의 DbSets를 보다 쉽게 사용할 수 있게 하는 방법</span><span class="sxs-lookup"><span data-stu-id="17222-224">How EF6 Enables Mocking DbSets more easily</span></span>](http://thedatafarm.com/data-access/how-ef6-enables-mocking-dbsets-more-easily/)
- [<span data-ttu-id="17222-225">모의 프레임 워크를 사용 하 여 테스트</span><span class="sxs-lookup"><span data-stu-id="17222-225">Testing with a mocking framework</span></span>](https://msdn.microsoft.com/data/dn314429)
- [<span data-ttu-id="17222-226">사용자 고유의 테스트를 사용 하 여 테스트 두 배</span><span class="sxs-lookup"><span data-stu-id="17222-226">Testing with your own test doubles</span></span>](https://msdn.microsoft.com/data/dn314431)

<a id="proxies"></a>

## <a name="proxy-classes"></a><span data-ttu-id="17222-227">프록시 클래스</span><span class="sxs-lookup"><span data-stu-id="17222-227">Proxy classes</span></span>

<span data-ttu-id="17222-228">Entity Framework에서 엔터티 인스턴스를 만들 때 (예: 쿼리를 실행 하는 경우) 엔터티에 대 한 프록시 역할을 하는 동적으로 생성 된 파생 형식의 인스턴스로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17222-228">When the Entity Framework creates entity instances (for example, when you execute a query), it often creates them as instances of a dynamically generated derived type that acts as a proxy for the entity.</span></span> <span data-ttu-id="17222-229">예를 들어 다음 두 개의 디버거 이미지를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="17222-229">For example, see the following two debugger images.</span></span> <span data-ttu-id="17222-230">첫 번째 이미지에서는 엔터티를 인스턴스화한 직후에 `student` 변수가 예상한 형식 인지 확인 합니다 `Student` .</span><span class="sxs-lookup"><span data-stu-id="17222-230">In the first image, you see that the `student` variable is the expected `Student` type immediately after you instantiate the entity.</span></span> <span data-ttu-id="17222-231">두 번째 이미지에서는 EF를 사용 하 여 데이터베이스에서 학생 엔터티를 읽은 후 프록시 클래스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-231">In the second image, after EF has been used to read a student entity from the database, you see the proxy class.</span></span>

![프록시 클래스 이전](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

![프록시 클래스 후](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

<span data-ttu-id="17222-234">이 프록시 클래스는 엔터티의 일부 가상 속성을 재정의 하 여 속성에 액세스할 때 자동으로 작업을 수행 하기 위한 후크를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-234">This proxy class overrides some virtual properties of the entity to insert hooks for performing actions automatically when the property is accessed.</span></span> <span data-ttu-id="17222-235">이 메커니즘을 사용 하는 하나의 함수는 지연 로드입니다.</span><span class="sxs-lookup"><span data-stu-id="17222-235">One function this mechanism is used for is lazy loading.</span></span>

<span data-ttu-id="17222-236">대부분의 경우 이러한 프록시 사용을 인식 하지 않아도 되지만 다음과 같은 예외가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-236">Most of the time you don't need to be aware of this use of proxies, but there are exceptions:</span></span>

- <span data-ttu-id="17222-237">일부 시나리오에서는 Entity Framework에서 프록시 인스턴스를 만들지 못하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-237">In some scenarios you might want to prevent the Entity Framework from creating proxy instances.</span></span> <span data-ttu-id="17222-238">예를 들어 엔터티를 serialize 하는 경우 일반적으로 프록시 클래스가 아니라 POCO 클래스를 원합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-238">For example, when you're serializing entities you generally want the POCO classes, not the proxy classes.</span></span> <span data-ttu-id="17222-239">Serialization 문제를 방지 하는 한 가지 방법은 [Entity Framework 웹 API 사용](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md) 자습서에 표시 된 것 처럼 엔터티 개체 대신 dto (데이터 전송 개체)를 serialize 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="17222-239">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects, as shown in the [Using Web API with Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md) tutorial.</span></span> <span data-ttu-id="17222-240">또 다른 방법은 [프록시 생성을 사용 하지 않도록 설정](https://msdn.microsoft.com/data/jj592886.aspx)하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="17222-240">Another way is to [disable proxy creation](https://msdn.microsoft.com/data/jj592886.aspx).</span></span>
- <span data-ttu-id="17222-241">연산자를 사용 하 여 엔터티 클래스 `new` 를 인스턴스화하면 프록시 인스턴스를 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-241">When you instantiate an entity class using the `new` operator, you don't get a proxy instance.</span></span> <span data-ttu-id="17222-242">즉, 지연 로드 및 자동 변경 내용 추적과 같은 기능을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-242">This means you don't get functionality such as lazy loading and automatic change tracking.</span></span> <span data-ttu-id="17222-243">이는 일반적으로 정상입니다. 일반적으로는 데이터베이스에 없는 새 엔터티를 만들고 엔터티를로 명시적으로 표시 하는 경우 일반적으로 변경 내용 추적이 필요 하지 않으므로 지연 로드가 필요 하지 않습니다 `Added` .</span><span class="sxs-lookup"><span data-stu-id="17222-243">This is typically okay; you generally don't need lazy loading, because you're creating a new entity that isn't in the database, and you generally don't need change tracking if you're explicitly marking the entity as `Added`.</span></span> <span data-ttu-id="17222-244">그러나 지연 로드가 필요 하 고 변경 내용 추적이 필요한 경우 클래스의 [만들기](https://msdn.microsoft.com/library/gg679504.aspx) 메서드를 사용 하 여 프록시를 사용 하 여 새 엔터티 인스턴스를 만들 수 있습니다 `DbSet` .</span><span class="sxs-lookup"><span data-stu-id="17222-244">However, if you do need lazy loading and you need change tracking, you can create new entity instances with proxies using the [Create](https://msdn.microsoft.com/library/gg679504.aspx) method of the `DbSet` class.</span></span>
- <span data-ttu-id="17222-245">프록시 형식에서 실제 엔터티 형식을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-245">You might want to get an actual entity type from a proxy type.</span></span> <span data-ttu-id="17222-246">클래스의 [Getobjecttype](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx) 메서드를 사용 하 여 `ObjectContext` 프록시 형식 인스턴스의 실제 엔터티 형식을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-246">You can use the [GetObjectType](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx) method of the `ObjectContext` class to get the actual entity type of a proxy type instance.</span></span>

<span data-ttu-id="17222-247">자세한 내용은 MSDN에서 [프록시 작업](https://msdn.microsoft.com/data/JJ592886.aspx) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="17222-247">For more information, see [Working with Proxies](https://msdn.microsoft.com/data/JJ592886.aspx) on MSDN.</span></span>

## <a name="automatic-change-detection"></a><span data-ttu-id="17222-248">자동 변경 내용 검색</span><span class="sxs-lookup"><span data-stu-id="17222-248">Automatic change detection</span></span>

<span data-ttu-id="17222-249">Entity Framework는 엔터티의 현재 값을 원래 값과 비교하여 엔터티가 변경된 방법(즉, 데이터베이스에 전송해야 하는 업데이트)을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-249">The Entity Framework determines how an entity has changed (and therefore which updates need to be sent to the database) by comparing the current values of an entity with the original values.</span></span> <span data-ttu-id="17222-250">원래 값은 엔터티가 쿼리 또는 연결될 때 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="17222-250">The original values are stored when the entity is queried or attached.</span></span> <span data-ttu-id="17222-251">자동 변경 내용 검색을 발생시키는 일부 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-251">Some of the methods that cause automatic change detection are the following:</span></span>

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

<span data-ttu-id="17222-252">많은 수의 엔터티를 추적 하 고 루프에서 이러한 메서드 중 하나를 여러 번 호출 하는 경우 [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx) 속성을 사용 하 여 자동 변경 검색 기능을 일시적으로 해제 하면 성능이 크게 향상 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-252">If you're tracking a large number of entities and you call one of these methods many times in a loop, you might get significant performance improvements by temporarily turning off automatic change detection using the [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx) property.</span></span> <span data-ttu-id="17222-253">자세한 내용은 MSDN의 [변경 내용 자동 검색](https://msdn.microsoft.com/data/jj556205) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="17222-253">For more information, see [Automatically Detecting Changes](https://msdn.microsoft.com/data/jj556205) on MSDN.</span></span>

## <a name="automatic-validation"></a><span data-ttu-id="17222-254">자동 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="17222-254">Automatic validation</span></span>

<span data-ttu-id="17222-255">메서드를 호출 하는 경우 `SaveChanges` 기본적으로 Entity Framework는 데이터베이스를 업데이트 하기 전에 변경 된 모든 엔터티의 모든 속성에 있는 데이터의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-255">When you call the `SaveChanges` method, by default the Entity Framework validates the data in all properties of all changed entities before updating the database.</span></span> <span data-ttu-id="17222-256">많은 수의 엔터티를 업데이트 하 고 이미 데이터의 유효성을 검사 한 경우이 작업은 필요 하지 않으며, 유효성 검사를 일시적으로 해제 하 여 변경 내용을 저장 하는 프로세스에 시간이 더 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="17222-256">If you've updated a large number of entities and you've already validated the data, this work is unnecessary and you could make the process of saving the changes take less time by temporarily turning off validation.</span></span> <span data-ttu-id="17222-257">[Validateonsaveenabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx) 속성을 사용 하 여이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-257">You can do that using the [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx) property.</span></span> <span data-ttu-id="17222-258">자세한 내용은 MSDN의 [유효성 검사](https://msdn.microsoft.com/data/gg193959) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="17222-258">For more information, see [Validation](https://msdn.microsoft.com/data/gg193959) on MSDN.</span></span>

## <a name="entity-framework-power-tools"></a><span data-ttu-id="17222-259">Entity Framework 파워 도구</span><span class="sxs-lookup"><span data-stu-id="17222-259">Entity Framework Power Tools</span></span>

<span data-ttu-id="17222-260">[Entity Framework 파워 도구](https://marketplace.visualstudio.com/items?itemName=ErikEJ.EntityFramework6PowerToolsCommunityEdition) 는 이러한 자습서에 표시 된 데이터 모델 다이어그램을 만드는 데 사용 된 Visual Studio 추가 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="17222-260">[Entity Framework Power Tools](https://marketplace.visualstudio.com/items?itemName=ErikEJ.EntityFramework6PowerToolsCommunityEdition) is a Visual Studio add-in that was used to create the data model diagrams shown in these tutorials.</span></span> <span data-ttu-id="17222-261">또한 도구는 기존 데이터베이스의 테이블을 기반으로 엔터티 클래스 생성과 같은 다른 기능을 수행 하 여 Code First에서 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-261">The tools can also do other function such as generate entity classes based on the tables in an existing database so that you can use the database with Code First.</span></span> <span data-ttu-id="17222-262">도구를 설치한 후에는 상황에 맞는 메뉴에 몇 가지 추가 옵션이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17222-262">After you install the tools, some additional options appear in context menus.</span></span> <span data-ttu-id="17222-263">예를 들어 **솔루션 탐색기**에서 컨텍스트 클래스를 마우스 오른쪽 단추로 클릭 하면 및 **Entity Framework** 옵션이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17222-263">For example, when you right-click your context class in **Solution Explorer**, you see and **Entity Framework** option.</span></span> <span data-ttu-id="17222-264">이렇게 하면 다이어그램을 생성 하는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-264">This gives you the ability to generate a diagram.</span></span> <span data-ttu-id="17222-265">Code First를 사용 하는 경우 다이어그램에서 데이터 모델을 변경할 수 없지만 이해 하기 쉽도록 항목을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-265">When you're using Code First you can't change the data model in the diagram, but you can move things around to make it easier to understand.</span></span>

![EF 다이어그램](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image15.png)

## <a name="entity-framework-source-code"></a><span data-ttu-id="17222-267">소스 코드 Entity Framework</span><span class="sxs-lookup"><span data-stu-id="17222-267">Entity Framework source code</span></span>

<span data-ttu-id="17222-268">Entity Framework 6의 소스 코드는 [GitHub](https://github.com/aspnet/EntityFramework6)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-268">The source code for Entity Framework 6 is available at [GitHub](https://github.com/aspnet/EntityFramework6).</span></span> <span data-ttu-id="17222-269">버그를 파일에 제공할 수 있으며 EF 소스 코드에 대 한 향상 된 기능을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-269">You can file bugs, and you can contribute your own enhancements to the EF source code.</span></span>

<span data-ttu-id="17222-270">소스 코드는 열려 있지만 Entity Framework은 Microsoft 제품으로 완전히 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17222-270">Although the source code is open, Entity Framework is fully supported as a Microsoft product.</span></span> <span data-ttu-id="17222-271">Microsoft Entity Framework 팀이 어떤 참가자를 수락할지 관리하고 각 릴리스의 품질을 보장하기 위해 모든 코드 변경 내용을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-271">The Microsoft Entity Framework team keeps control over which contributions are accepted and tests all code changes to ensure the quality of each release.</span></span>

## <a name="acknowledgments"></a><span data-ttu-id="17222-272">감사의 글</span><span class="sxs-lookup"><span data-stu-id="17222-272">Acknowledgments</span></span>

- <span data-ttu-id="17222-273">Tom Dykstra는이 자습서의 원래 버전을 작성 하 고 EF 5 업데이트를 공동 작성 하 고 EF 6 업데이트를 작성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-273">Tom Dykstra wrote the original version of this tutorial, co-authored the EF 5 update, and wrote the EF 6 update.</span></span> <span data-ttu-id="17222-274">Tom은 Microsoft 웹 플랫폼 및 도구 콘텐츠 팀의 선임 프로그래밍 기록기입니다.</span><span class="sxs-lookup"><span data-stu-id="17222-274">Tom is a senior programming writer on the Microsoft Web Platform and Tools Content Team.</span></span>
- <span data-ttu-id="17222-275">Twitter ( [Rick Anderson](https://blogs.msdn.com/b/rickandy/) )는 [@RickAndMSFT](http://twitter.com/RickAndMSFT) EF 5 및 MVC 4의 자습서를 업데이트 하 고 ef 6 업데이트를 공동 작성 하는 대부분의 작업을 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-275">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) did most of the work updating the tutorial for EF 5 and MVC 4 and co-authored the EF 6 update.</span></span> <span data-ttu-id="17222-276">Rick는 Azure 및 MVC를 중심으로 하는 Microsoft의 선임 프로그래밍 기록기입니다.</span><span class="sxs-lookup"><span data-stu-id="17222-276">Rick is a senior programming writer for Microsoft focusing on Azure and MVC.</span></span>
- <span data-ttu-id="17222-277">[행](http://www.romiller.com) 하 고 Entity Framework 팀의 다른 구성원이 코드 검토를 사용 하 고 ef 5 및 ef 6에 대 한 자습서를 업데이트 하는 동안 발생 한 마이그레이션의 많은 문제를 디버그 하는 데 도움이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-277">[Rowan Miller](http://www.romiller.com) and other members of the Entity Framework team assisted with code reviews and helped debug many issues with migrations that arose while we were updating the tutorial for EF 5 and EF 6.</span></span>

## <a name="troubleshoot-common-errors"></a><span data-ttu-id="17222-278">일반적인 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="17222-278">Troubleshoot common errors</span></span>

### <a name="cannot-createshadow-copy"></a><span data-ttu-id="17222-279">복사본을 만들거나 섀도 복사할 수 없음</span><span class="sxs-lookup"><span data-stu-id="17222-279">Cannot create/shadow copy</span></span>

<span data-ttu-id="17222-280">오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="17222-280">Error Message:</span></span>

> <span data-ttu-id="17222-281">' &lt; Filename &gt; '이 이미 있는 경우 해당 파일을 만들거나 섀도 복사할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-281">Cannot create/shadow copy '&lt;filename&gt;' when that file already exists.</span></span>

<span data-ttu-id="17222-282">솔루션</span><span class="sxs-lookup"><span data-stu-id="17222-282">Solution</span></span>

<span data-ttu-id="17222-283">몇 초 정도 기다렸다가 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="17222-283">Wait a few seconds and refresh the page.</span></span>

### <a name="update-database-not-recognized"></a><span data-ttu-id="17222-284">업데이트-데이터베이스를 인식할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-284">Update-Database not recognized</span></span>

<span data-ttu-id="17222-285">오류 메시지 ( `Update-Database` PMC의 명령에서):</span><span class="sxs-lookup"><span data-stu-id="17222-285">Error Message (from the `Update-Database` command in the PMC):</span></span>

> <span data-ttu-id="17222-286">' 업데이트-데이터베이스 ' 라는 용어는 cmdlet, 함수, 스크립트 파일 또는 실행할 수 있는 프로그램의 이름으로 인식 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-286">The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program.</span></span> <span data-ttu-id="17222-287">이름의 철자를 확인하거나 경로가 포함되어 있으면 경로가 올바른지 확인하고 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-287">Check the spelling of the name, or if a path was included, verify that the path is correct and try again.</span></span>

<span data-ttu-id="17222-288">솔루션</span><span class="sxs-lookup"><span data-stu-id="17222-288">Solution</span></span>

<span data-ttu-id="17222-289">Visual Studio를 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="17222-289">Exit Visual Studio.</span></span> <span data-ttu-id="17222-290">프로젝트를 다시 열고 다시 시도 하세요.</span><span class="sxs-lookup"><span data-stu-id="17222-290">Reopen project and try again.</span></span>

### <a name="validation-failed"></a><span data-ttu-id="17222-291">유효성 검사 실패</span><span class="sxs-lookup"><span data-stu-id="17222-291">Validation failed</span></span>

<span data-ttu-id="17222-292">오류 메시지 ( `Update-Database` PMC의 명령에서):</span><span class="sxs-lookup"><span data-stu-id="17222-292">Error Message (from the `Update-Database` command in the PMC):</span></span>

> <span data-ttu-id="17222-293">하나 이상의 엔터티에 대 한 유효성 검사에 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-293">Validation failed for one or more entities.</span></span> <span data-ttu-id="17222-294">자세한 내용은 ' EntityValidationErrors ' 속성을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="17222-294">See 'EntityValidationErrors' property for more details.</span></span>

<span data-ttu-id="17222-295">솔루션</span><span class="sxs-lookup"><span data-stu-id="17222-295">Solution</span></span>

<span data-ttu-id="17222-296">이 문제의 한 가지 원인은 메서드가 실행 될 때 유효성 검사 오류입니다 `Seed` .</span><span class="sxs-lookup"><span data-stu-id="17222-296">One cause of this problem is validation errors when the `Seed` method runs.</span></span> <span data-ttu-id="17222-297">메서드를 디버깅 하는 방법에 대 한 팁은 [EF (시드 및 디버깅 Entity Framework) db](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) 를 참조 하세요 `Seed` .</span><span class="sxs-lookup"><span data-stu-id="17222-297">See [Seeding and Debugging Entity Framework (EF) DBs](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) for tips on debugging the `Seed` method.</span></span>

### <a name="http-50019-error"></a><span data-ttu-id="17222-298">HTTP 500.19 오류</span><span class="sxs-lookup"><span data-stu-id="17222-298">HTTP 500.19 error</span></span>

<span data-ttu-id="17222-299">오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="17222-299">Error Message:</span></span>

> <span data-ttu-id="17222-300">HTTP 오류 500.19-내부 서버 오류 페이지에 대 한 관련 구성 데이터가 잘못 되어 요청 된 페이지에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-300">HTTP Error 500.19 - Internal Server Error The requested page cannot be accessed because the related configuration data for the page is invalid.</span></span>

<span data-ttu-id="17222-301">솔루션</span><span class="sxs-lookup"><span data-stu-id="17222-301">Solution</span></span>

<span data-ttu-id="17222-302">이 오류를 발생 시킬 수 있는 한 가지 방법은 각각 동일한 포트 번호를 사용 하 여 솔루션의 복사본을 여러 개 포함 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="17222-302">One way you can get this error is from having multiple copies of the solution, each of them using the same port number.</span></span> <span data-ttu-id="17222-303">일반적으로 Visual Studio의 모든 인스턴스를 종료 한 다음 작업 중인 프로젝트를 다시 시작 하 여이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-303">You can usually solve this problem by exiting all instances of Visual Studio, then restarting the project you're working on.</span></span> <span data-ttu-id="17222-304">작동 하지 않는 경우 포트 번호를 변경해 보세요.</span><span class="sxs-lookup"><span data-stu-id="17222-304">If that doesn't work, try changing the port number.</span></span> <span data-ttu-id="17222-305">프로젝트 파일을 마우스 오른쪽 단추로 클릭 한 다음 속성을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-305">Right click on the project file and then click properties.</span></span> <span data-ttu-id="17222-306">**웹** 탭을 선택한 다음 **프로젝트 Url** 텍스트 상자에서 포트 번호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-306">Select the **Web** tab and then change the port number in the **Project Url** text box.</span></span>

### <a name="error-locating-sql-server-instance"></a><span data-ttu-id="17222-307">SQL Server 인스턴스 찾기 오류</span><span class="sxs-lookup"><span data-stu-id="17222-307">Error locating SQL Server instance</span></span>

<span data-ttu-id="17222-308">오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="17222-308">Error Message:</span></span>

> <span data-ttu-id="17222-309">SQL Server에 연결하는 중에 네트워크 관련 오류 또는 인스턴스별 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-309">A network-related or instance-specific error occurred while establishing a connection to SQL Server.</span></span> <span data-ttu-id="17222-310">서버를 찾을 수 없거나 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-310">The server was not found or was not accessible.</span></span> <span data-ttu-id="17222-311">인스턴스 이름이 올바르고 SQL Server가 원격 연결을 허용하도록 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-311">Verify that the instance name is correct and that SQL Server is configured to allow remote connections.</span></span> <span data-ttu-id="17222-312">(공급자: SQL 네트워크 인터페이스, 오류: 26 - 지정된 서버/인스턴스 찾기 오류)</span><span class="sxs-lookup"><span data-stu-id="17222-312">(provider: SQL Network Interfaces, error: 26 - Error Locating Server/Instance Specified)</span></span>

<span data-ttu-id="17222-313">솔루션</span><span class="sxs-lookup"><span data-stu-id="17222-313">Solution</span></span>

<span data-ttu-id="17222-314">연결 문자열을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-314">Check the connection string.</span></span> <span data-ttu-id="17222-315">데이터베이스를 수동으로 삭제 한 경우 생성 문자열에서 데이터베이스 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-315">If you have manually deleted the database, change the name of the database in the construction string.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="17222-316">코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="17222-316">Get the code</span></span>

[<span data-ttu-id="17222-317">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="17222-317">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="17222-318">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="17222-318">Additional resources</span></span>

 <span data-ttu-id="17222-319">Entity Framework를 사용 하 여 데이터로 작업 하는 방법에 대 한 자세한 내용은 [MSDN의 EF 설명서 페이지](https://msdn.microsoft.com/data/ee712907) 및 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="17222-319">For more information about how to work with data using the Entity Framework, see the [EF documentation page on MSDN](https://msdn.microsoft.com/data/ee712907) and [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

<span data-ttu-id="17222-320">웹 응용 프로그램을 빌드한 후 배포 하는 방법에 대 한 자세한 내용은 MSDN Library에서 [ASP.NET 웹 배포-권장 리소스](../../../../whitepapers/aspnet-web-deployment-content-map.md) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="17222-320">For more information about how to deploy your web application after you've built it, see [ASP.NET Web Deployment - Recommended Resources](../../../../whitepapers/aspnet-web-deployment-content-map.md) in the MSDN Library.</span></span>

<span data-ttu-id="17222-321">인증 및 권한 부여와 같은 MVC와 관련 된 다른 항목에 대 한 자세한 내용은 [ASP.NET Mvc 권장 리소스](../recommended-resources-for-mvc.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="17222-321">For information about other topics related to MVC, such as authentication and authorization, see the [ASP.NET MVC - Recommended Resources](../recommended-resources-for-mvc.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="17222-322">다음 단계</span><span class="sxs-lookup"><span data-stu-id="17222-322">Next steps</span></span>

<span data-ttu-id="17222-323">이 자습서에서는 다음과 같은 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-323">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="17222-324">원시 SQL 쿼리 수행</span><span class="sxs-lookup"><span data-stu-id="17222-324">Performed raw SQL queries</span></span>
> * <span data-ttu-id="17222-325">추적 안 함 쿼리 수행</span><span class="sxs-lookup"><span data-stu-id="17222-325">Performed no-tracking queries</span></span>
> * <span data-ttu-id="17222-326">데이터베이스로 전송 된 SQL 쿼리를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="17222-326">Examined SQL queries sent to the database</span></span>

<span data-ttu-id="17222-327">또한 다음에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-327">You also learned about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="17222-328">추상화 계층 만들기</span><span class="sxs-lookup"><span data-stu-id="17222-328">Creating an abstraction layer</span></span>
> * <span data-ttu-id="17222-329">프록시 클래스</span><span class="sxs-lookup"><span data-stu-id="17222-329">Proxy classes</span></span>
> * <span data-ttu-id="17222-330">자동 변경 내용 검색</span><span class="sxs-lookup"><span data-stu-id="17222-330">Automatic change detection</span></span>
> * <span data-ttu-id="17222-331">자동 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="17222-331">Automatic validation</span></span>
> * <span data-ttu-id="17222-332">Entity Framework 파워 도구</span><span class="sxs-lookup"><span data-stu-id="17222-332">Entity Framework Power Tools</span></span>
> * <span data-ttu-id="17222-333">소스 코드 Entity Framework</span><span class="sxs-lookup"><span data-stu-id="17222-333">Entity Framework source code</span></span>

<span data-ttu-id="17222-334">ASP.NET MVC 응용 프로그램에서 Entity Framework 사용에 대 한이 일련의 자습서를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="17222-334">This completes this series of tutorials on using the Entity Framework in an ASP.NET MVC application.</span></span> <span data-ttu-id="17222-335">EF Database First에 대해 알아보려면 DB First tutorial 시리즈를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="17222-335">If you want to learn about EF Database First, see the DB First tutorial series.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="17222-336">Entity Framework Database First</span><span class="sxs-lookup"><span data-stu-id="17222-336">Entity Framework Database First</span></span>](../database-first-development/setting-up-database.md)