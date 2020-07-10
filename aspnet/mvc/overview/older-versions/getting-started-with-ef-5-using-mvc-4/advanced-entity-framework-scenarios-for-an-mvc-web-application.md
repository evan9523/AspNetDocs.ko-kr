---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: MVC 웹 응용 프로그램에 대 한 고급 Entity Framework 시나리오 (10/10) | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 64906a1d-f734-41cf-9615-ee95f8740996
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: f8f079f6d8ea663c6888456be422a2bae93a4b87
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "86163581"
---
# <a name="advanced-entity-framework-scenarios-for-an-mvc-web-application-10-of-10"></a><span data-ttu-id="8022c-103">MVC 웹 응용 프로그램에 대 한 고급 Entity Framework 시나리오 (10/10)</span><span class="sxs-lookup"><span data-stu-id="8022c-103">Advanced Entity Framework Scenarios for an MVC Web Application (10 of 10)</span></span>

<span data-ttu-id="8022c-104">만든 사람 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="8022c-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="8022c-105">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="8022c-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="8022c-106">Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio 2012을 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="8022c-107">자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8022c-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="8022c-108">[이 챕터의](building-the-ef5-mvc4-chapter-downloads.md) 시작 또는 시작 프로젝트 다운로드에서 자습서 시리즈를 시작 하 고 여기에서 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="8022c-109">해결할 수 없는 문제가 발생 하는 경우 [완료 된 챕터를 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 하 여 문제를 재현해 보세요.</span><span class="sxs-lookup"><span data-stu-id="8022c-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="8022c-110">일반적으로 코드를 완성 된 코드와 비교 하 여 문제에 대 한 솔루션을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="8022c-111">몇 가지 일반적인 오류 및 해결 방법에 대 한 자세한 내용은 [오류 및 해결](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors) 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="8022c-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="8022c-112">이전 자습서에서는 리포지토리 및 작업 패턴 단위를 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-112">In the previous tutorial you implemented the repository and unit of work patterns.</span></span> <span data-ttu-id="8022c-113">이 자습서에서는 다음 항목을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-113">This tutorial covers the following topics:</span></span>

- <span data-ttu-id="8022c-114">원시 SQL 쿼리 수행</span><span class="sxs-lookup"><span data-stu-id="8022c-114">Performing raw SQL queries.</span></span>
- <span data-ttu-id="8022c-115">추적 하지 않는 쿼리 수행</span><span class="sxs-lookup"><span data-stu-id="8022c-115">Performing no-tracking queries.</span></span>
- <span data-ttu-id="8022c-116">데이터베이스로 전송 된 쿼리를 검사 하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-116">Examining queries sent to the database.</span></span>
- <span data-ttu-id="8022c-117">프록시 클래스 작업</span><span class="sxs-lookup"><span data-stu-id="8022c-117">Working with proxy classes.</span></span>
- <span data-ttu-id="8022c-118">변경 내용 자동 검색을 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="8022c-118">Disabling automatic detection of changes.</span></span>
- <span data-ttu-id="8022c-119">변경 내용을 저장할 때 유효성 검사 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="8022c-119">Disabling validation when saving changes.</span></span>
- [<span data-ttu-id="8022c-120">오류 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="8022c-120">Errors and Work Arounds</span></span>](#errors)

<span data-ttu-id="8022c-121">이러한 항목의 대부분은 이미 만든 페이지를 사용 하 여 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-121">For most of these topics, you'll work with pages that you already created.</span></span> <span data-ttu-id="8022c-122">원시 SQL을 사용 하 여 대량 업데이트를 수행 하려면 데이터베이스에 있는 모든 과정의 크레딧 수를 업데이트 하는 새 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-122">To use raw SQL to do bulk updates you'll create a new page that updates the number of credits of all courses in the database:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

<span data-ttu-id="8022c-124">추적 안 함 쿼리를 사용 하려면 부서 편집 페이지에 새 유효성 검사 논리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-124">And to use a no-tracking query you'll add new validation logic to the Department Edit page:</span></span>

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image2.png)

## <a name="performing-raw-sql-queries"></a><span data-ttu-id="8022c-126">원시 SQL 쿼리 수행</span><span class="sxs-lookup"><span data-stu-id="8022c-126">Performing Raw SQL Queries</span></span>

<span data-ttu-id="8022c-127">Entity Framework Code First API에는 SQL 명령을 데이터베이스에 직접 전달할 수 있는 메서드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-127">The Entity Framework Code First API includes methods that enable you to pass SQL commands directly to the database.</span></span> <span data-ttu-id="8022c-128">다음과 같은 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-128">You have the following options:</span></span>

- <span data-ttu-id="8022c-129">엔터티 형식을 반환하는 쿼리에 `DbSet.SqlQuery` 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-129">Use the `DbSet.SqlQuery` method for queries that return entity types.</span></span> <span data-ttu-id="8022c-130">반환 된 개체는 개체에 필요한 형식 이어야 `DbSet` 하며, 추적을 해제 하지 않는 한 데이터베이스 컨텍스트에 의해 자동으로 추적 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-130">The returned objects must be of the type expected by the `DbSet` object, and they are automatically tracked by the database context unless you turn tracking off.</span></span> <span data-ttu-id="8022c-131">메서드에 대 한 다음 섹션을 참조 하십시오 `AsNoTracking` .</span><span class="sxs-lookup"><span data-stu-id="8022c-131">(See the following section about the `AsNoTracking` method.)</span></span>
- <span data-ttu-id="8022c-132">`Database.SqlQuery`엔터티가 아닌 형식을 반환 하는 쿼리에 대해 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-132">Use the `Database.SqlQuery` method for queries that return types that aren't entities.</span></span> <span data-ttu-id="8022c-133">이 메서드를 사용하여 엔터티 형식을 검색하더라도 반환된 데이터는 데이터베이스 컨텍스트에 의해 추적되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-133">The returned data isn't tracked by the database context, even if you use this method to retrieve entity types.</span></span>
- <span data-ttu-id="8022c-134">쿼리가 아닌 명령에 [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx) 를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-134">Use the [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx) for non-query commands.</span></span>

<span data-ttu-id="8022c-135">Entity Framework를 사용할 때 장점 중 하나는 코드가 데이터를 저장하는 특정 메서드에 너무 얽매이지 않아도 된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-135">One of the advantages of using the Entity Framework is that it avoids tying your code too closely to a particular method of storing data.</span></span> <span data-ttu-id="8022c-136">이것은 사용자를 위한 SQL 쿼리와 명령이 생성되므로 가능하며 사용자는 코드를 직접 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-136">It does this by generating SQL queries and commands for you, which also frees you from having to write them yourself.</span></span> <span data-ttu-id="8022c-137">그러나 수동으로 만든 특정 SQL 쿼리를 실행 해야 하는 경우에는 예외적인 시나리오가 있습니다. 이러한 방법을 사용 하면 이러한 예외를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-137">But there are exceptional scenarios when you need to run specific SQL queries that you have manually created, and these methods make it possible for you to handle such exceptions.</span></span>

<span data-ttu-id="8022c-138">웹 애플리케이션에서 SQL 명령을 실행할 때 항상 그렇듯이 SQL 삽입 공격으로부터 사이트를 보호하기 위한 예방 조치를 취해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-138">As is always true when you execute SQL commands in a web application, you must take precautions to protect your site against SQL injection attacks.</span></span> <span data-ttu-id="8022c-139">이를 수행하는 한 가지 방법은 매개 변수가 있는 쿼리를 사용하여 웹 페이지에서 제출한 문자열을 SQL 명령으로 해석할 수 없도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-139">One way to do that is to use parameterized queries to make sure that strings submitted by a web page can't be interpreted as SQL commands.</span></span> <span data-ttu-id="8022c-140">이 자습서에서는 사용자 입력을 쿼리에 통합할 때 매개 변수가 있는 쿼리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-140">In this tutorial you'll use parameterized queries when integrating user input into a query.</span></span>

### <a name="calling-a-query-that-returns-entities"></a><span data-ttu-id="8022c-141">엔터티를 반환 하는 쿼리 호출</span><span class="sxs-lookup"><span data-stu-id="8022c-141">Calling a Query that Returns Entities</span></span>

<span data-ttu-id="8022c-142">`GenericRepository`클래스에서 추가 메서드를 사용 하 여 파생 클래스를 만들 필요 없이 추가 필터링 및 정렬 유연성을 제공 하려는 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-142">Suppose you want the `GenericRepository` class to provide additional filtering and sorting flexibility without requiring that you create a derived class with additional methods.</span></span> <span data-ttu-id="8022c-143">이를 수행 하는 한 가지 방법은 SQL 쿼리를 허용 하는 메서드를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-143">One way to achieve that would be to add a method that accepts a SQL query.</span></span> <span data-ttu-id="8022c-144">그런 다음 컨트롤러에서 원하는 종류의 필터링 또는 정렬 (예: `Where` 조인이 나 하위 쿼리를 따라 달라 지는 절)을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-144">You could then specify any kind of filtering or sorting you want in the controller, such as a `Where` clause that depends on a joins or a subquery.</span></span> <span data-ttu-id="8022c-145">이 섹션에서는 이러한 메서드를 구현 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-145">In this section you'll see how to implement such a method.</span></span>

<span data-ttu-id="8022c-146">`GetWithRawSql` *GenericRepository.cs*에 다음 코드를 추가 하 여 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-146">Create the `GetWithRawSql` method by adding the following code to *GenericRepository.cs*:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs)]

<span data-ttu-id="8022c-147">*CourseController.cs*에서 `Details` 다음 예제와 같이 메서드에서 새 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-147">In *CourseController.cs*, call the new method from the `Details` method, as shown in the following example:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

<span data-ttu-id="8022c-148">이 경우 메서드를 사용 했지만 메서드를 `GetByID` 사용 하 여 `GetWithRawSql` 메서드가 작동 하는지 확인 `GetWithRawSQL` 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-148">In this case you could have used the `GetByID` method, but you're using the `GetWithRawSql` method to verify that the `GetWithRawSQL` method works.</span></span>

<span data-ttu-id="8022c-149">세부 정보 페이지를 실행 하 여 select 쿼리가 작동 하는지 확인 합니다 ( **과정** 탭을 선택 하 고 한 과정에 대 한 **세부 정보** 를 선택).</span><span class="sxs-lookup"><span data-stu-id="8022c-149">Run the Details page to verify that the select query works (select the **Course** tab and then **Details** for one course).</span></span>

![Course_Details_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image3.png)

### <a name="calling-a-query-that-returns-other-types-of-objects"></a><span data-ttu-id="8022c-151">다른 형식의 개체를 반환 하는 쿼리 호출</span><span class="sxs-lookup"><span data-stu-id="8022c-151">Calling a Query that Returns Other Types of Objects</span></span>

<span data-ttu-id="8022c-152">이전에 등록 날짜별로 학생 수를 보여주는 [정보] 페이지의 학생 통계 표를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-152">Earlier you created a student statistics grid for the About page that showed the number of students for each enrollment date.</span></span> <span data-ttu-id="8022c-153">*HomeController.cs* 에서이 작업을 수행 하는 코드는 LINQ를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-153">The code that does this in *HomeController.cs* uses LINQ:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs)]

<span data-ttu-id="8022c-154">LINQ를 사용 하지 않고 SQL에서 직접이 데이터를 검색 하는 코드를 작성 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-154">Suppose you want to write the code that retrieves this data directly in SQL rather than using LINQ.</span></span> <span data-ttu-id="8022c-155">이렇게 하려면 엔터티 개체가 아닌 다른 항목을 반환 하는 쿼리를 실행 해야 합니다. 즉, 메서드를 사용 해야 `Database.SqlQuery` 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-155">To do that you need to run a query that returns something other than entity objects, which means you need to use the `Database.SqlQuery` method.</span></span>

<span data-ttu-id="8022c-156">*HomeController.cs*에서 메서드의 LINQ 문을 `About` 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-156">In *HomeController.cs*, replace the LINQ statement in the `About` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

<span data-ttu-id="8022c-157">정보 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-157">Run the About page.</span></span> <span data-ttu-id="8022c-158">이전과 동일한 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-158">It displays the same data it did before.</span></span>

![About_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image4.png)

### <a name="calling-an-update-query"></a><span data-ttu-id="8022c-160">업데이트 쿼리 호출</span><span class="sxs-lookup"><span data-stu-id="8022c-160">Calling an Update Query</span></span>

<span data-ttu-id="8022c-161">Contoso 대학 관리자가 모든 과정에 대 한 크레딧 수를 변경 하는 등 데이터베이스에서 대량 변경을 수행할 수 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-161">Suppose Contoso University administrators want to be able to perform bulk changes in the database, such as changing the number of credits for every course.</span></span> <span data-ttu-id="8022c-162">대학에 과목이 많은 경우 엔터티로 모두 검색하여 개별적으로 변경하는 것은 비효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-162">If the university has a large number of courses, it would be inefficient to retrieve them all as entities and change them individually.</span></span> <span data-ttu-id="8022c-163">이 섹션에서는 사용자가 모든 과정에 대 한 크레딧 수를 변경 하는 데 필요한 인수를 지정할 수 있는 웹 페이지를 구현 하 고 SQL 문을 실행 하 여 변경 작업을 수행 합니다 `UPDATE` .</span><span class="sxs-lookup"><span data-stu-id="8022c-163">In this section you'll implement a web page that allows the user to specify a factor by which to change the number of credits for all courses, and you'll make the change by executing a SQL `UPDATE` statement.</span></span> <span data-ttu-id="8022c-164">그러면 웹 페이지가 다음 그림과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-164">The web page will look like the following illustration:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image5.png)

<span data-ttu-id="8022c-166">이전 자습서에서는 제네릭 리포지토리를 사용 하 여 `Course` 컨트롤러에서 엔터티를 읽고 업데이트 `Course` 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-166">In the previous tutorial you used the generic repository to read and update `Course` entities in the `Course` controller.</span></span> <span data-ttu-id="8022c-167">이 대량 업데이트 작업을 수행 하려면 일반 리포지토리에 없는 새 리포지토리 메서드를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-167">For this bulk update operation, you need to create a new repository method that isn't in the generic repository.</span></span> <span data-ttu-id="8022c-168">이렇게 하려면 `CourseRepository` 클래스에서 파생 되는 전용 클래스를 만듭니다 `GenericRepository` .</span><span class="sxs-lookup"><span data-stu-id="8022c-168">To do that, you'll create a dedicated `CourseRepository` class that derives from the `GenericRepository` class.</span></span>

<span data-ttu-id="8022c-169">*DAL* 폴더에서 *CourseRepository.cs* 을 만들고 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-169">In the *DAL* folder, create *CourseRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cs)]

<span data-ttu-id="8022c-170">*UnitOfWork.cs*에서 `Course` 리포지토리 형식을에서로 변경 합니다 `GenericRepository<Course>` .`CourseRepository:`</span><span class="sxs-lookup"><span data-stu-id="8022c-170">In *UnitOfWork.cs*, change the `Course` repository type from `GenericRepository<Course>` to `CourseRepository:`</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.cs)]

<span data-ttu-id="8022c-171">*CourseController.cs*에서 메서드를 추가 합니다 `UpdateCourseCredits` .</span><span class="sxs-lookup"><span data-stu-id="8022c-171">In *CourseController.cs*, add an `UpdateCourseCredits` method:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

<span data-ttu-id="8022c-172">이 메서드는 및에 모두 사용 `HttpGet` 됩니다 `HttpPost` .</span><span class="sxs-lookup"><span data-stu-id="8022c-172">This method will be used for both `HttpGet` and `HttpPost`.</span></span> <span data-ttu-id="8022c-173">`HttpGet` `UpdateCourseCredits` 메서드가 실행 될 때 변수는 `multiplier` null이 되며 앞의 그림에 표시 된 것 처럼 뷰가 빈 텍스트 상자와 제출 단추를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-173">When the `HttpGet` `UpdateCourseCredits` method runs, the `multiplier` variable will be null and the view will display an empty text box and a submit button, as shown in the preceding illustration.</span></span>

<span data-ttu-id="8022c-174">**업데이트** 단추를 클릭 하 고 메서드를 `HttpPost` 실행 하면에는 `multiplier` 텍스트 상자에 입력 된 값이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-174">When the **Update** button is clicked and the `HttpPost` method runs, `multiplier` will have the value entered in the text box.</span></span> <span data-ttu-id="8022c-175">그런 다음 코드는 영향을 `UpdateCourseCredits` 받는 행의 수를 반환 하는 리포지토리 메서드를 호출 하 고, 해당 값은 개체에 저장 됩니다 `ViewBag` .</span><span class="sxs-lookup"><span data-stu-id="8022c-175">The code then calls the repository `UpdateCourseCredits` method, which returns the number of affected rows, and that value is stored in the `ViewBag` object.</span></span> <span data-ttu-id="8022c-176">뷰에서 개체의 영향을 받는 행 수를 받으면 `ViewBag` 다음 그림과 같이 텍스트 상자 및 전송 단추 대신 해당 숫자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-176">When the view receives the number of affected rows in the `ViewBag` object, it displays that number instead of the text box and submit button, as shown in the following illustration:</span></span>

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image6.png)

<span data-ttu-id="8022c-178">업데이트 과정 크레딧 페이지의 *Views\Course* 폴더에 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-178">Create a view in the *Views\Course* folder for the Update Course Credits page:</span></span>

![Add_View_dialog_box_for_Update_Course_Credits](https://asp.net/media/2578203/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Add_View_dialog_box_for_Update_Course_Credits.png)

<span data-ttu-id="8022c-180">*Views\Course\UpdateCourseCredits.cshtml*에서 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-180">In *Views\Course\UpdateCourseCredits.cshtml*, replace the template code with the following code:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

<span data-ttu-id="8022c-181">**Courses(과정)** 탭을 선택하여 `UpdateCourseCredits` 메서드를 실행한 후 브라우저의 주소 표시줄에서 URL 끝에 "/UpdateCourseCredits"를 추가합니다(예: `http://localhost:50205/Course/UpdateCourseCredits`).</span><span class="sxs-lookup"><span data-stu-id="8022c-181">Run the `UpdateCourseCredits` method by selecting the **Courses** tab, then adding "/UpdateCourseCredits" to the end of the URL in the browser's address bar (for example: `http://localhost:50205/Course/UpdateCourseCredits`).</span></span> <span data-ttu-id="8022c-182">텍스트 상자에 숫자를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-182">Enter a number in the text box:</span></span>

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image7.png)

<span data-ttu-id="8022c-184">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-184">Click **Update**.</span></span> <span data-ttu-id="8022c-185">영향을 받은 행 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-185">You see the number of rows affected:</span></span>

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image8.png)

<span data-ttu-id="8022c-187">학점 수가 수정된 과정 목록을 보려면 **목록으로 돌아가기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-187">Click **Back to List** to see the list of courses with the revised number of credits.</span></span>

![Courses_Index_page_showing_revised_credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image9.png)

<span data-ttu-id="8022c-189">원시 SQL 쿼리에 대 한 자세한 내용은 Entity Framework 팀 블로그의 [원시 Sql 쿼리](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="8022c-189">For more information about raw SQL queries, see [Raw SQL Queries](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx) on the Entity Framework team blog.</span></span>

## <a name="no-tracking-queries"></a><span data-ttu-id="8022c-190">비 추적 쿼리</span><span class="sxs-lookup"><span data-stu-id="8022c-190">No-Tracking Queries</span></span>

<span data-ttu-id="8022c-191">데이터베이스 컨텍스트가 데이터베이스 행을 검색 하 고이를 나타내는 엔터티 개체를 만드는 경우 기본적으로 메모리의 엔터티가 데이터베이스에 있는 항목과 동기화 되는지 여부를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-191">When a database context retrieves database rows and creates entity objects that represent them, by default it keeps track of whether the entities in memory are in sync with what's in the database.</span></span> <span data-ttu-id="8022c-192">메모리의 데이터는 캐시의 역할을 하고 엔터티를 업데이트할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-192">The data in memory acts as a cache and is used when you update an entity.</span></span> <span data-ttu-id="8022c-193">컨텍스트 인스턴스는 일반적으로 수명이 짧으며(각 요청에 대해 새 것이 만들어지고 삭제됨) 엔터티를 읽는 컨텍스트는 일반적으로 해당 엔터티가 다시 사용되기 전에 삭제되므로 이 캐싱은 웹 애플리케이션에 종종 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-193">This caching is often unnecessary in a web application because context instances are typically short-lived (a new one is created and disposed for each request) and the context that reads an entity is typically disposed before that entity is used again.</span></span>

<span data-ttu-id="8022c-194">메서드가 메서드를 사용 하 여 쿼리에 대 한 엔터티 개체를 추적할지 여부를 지정할 수 있습니다 `AsNoTracking` .</span><span class="sxs-lookup"><span data-stu-id="8022c-194">You can specify whether the context tracks entity objects for a query by using the `AsNoTracking` method.</span></span> <span data-ttu-id="8022c-195">이러한 작업을 수행할 수 있는 일반적인 시나리오는 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-195">Typical scenarios in which you might want to do that include the following:</span></span>

- <span data-ttu-id="8022c-196">이 쿼리는 추적 기능을 해제 하는 대량의 데이터를 검색 하 여 성능을 현저 하 게 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-196">The query retrieves such a large volume of data that turning off tracking might noticeably enhance performance.</span></span>
- <span data-ttu-id="8022c-197">엔터티를 업데이트 하기 위해 연결 하려고 하지만 이전에 다른 용도로 동일한 엔터티를 검색 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-197">You want to attach an entity in order to update it, but you earlier retrieved the same entity for a different purpose.</span></span> <span data-ttu-id="8022c-198">엔터티는 데이터베이스 컨텍스트에서 이미 추적 중이므로 변경하려는 엔터티를 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-198">Because the entity is already being tracked by the database context, you can't attach the entity that you want to change.</span></span> <span data-ttu-id="8022c-199">이러한 상황을 방지 하는 한 가지 방법은 `AsNoTracking` 이전 쿼리와 함께 옵션을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-199">One way to prevent this from happening is to use the `AsNoTracking` option with the earlier query.</span></span>

<span data-ttu-id="8022c-200">이 섹션에서는 이러한 두 가지 시나리오를 설명 하는 비즈니스 논리를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-200">In this section you'll implement business logic that illustrates the second of these scenarios.</span></span> <span data-ttu-id="8022c-201">특히 강사가 둘 이상의 부서의 관리자가 될 수 없다는 비즈니스 규칙을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-201">Specifically, you'll enforce a business rule that says that an instructor can't be the administrator of more than one department.</span></span>

<span data-ttu-id="8022c-202">*DepartmentController.cs*에서 및 메서드를 호출할 수 있는 새 메서드를 추가 `Edit` `Create` 하 여 두 부서가 동일한 관리자를 포함 하지 않는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-202">In *DepartmentController.cs*, add a new method that you can call from the `Edit` and `Create` methods to make sure that no two departments have the same administrator:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.cs)]

<span data-ttu-id="8022c-203">`try` `HttpPost` `Edit` 유효성 검사 오류가 없는 경우 메서드의 블록에 코드를 추가 하 여이 새 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-203">Add code in the `try` block of the `HttpPost` `Edit` method to call this new method if there are no validation errors.</span></span> <span data-ttu-id="8022c-204">`try`이제 블록은 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-204">The `try` block now looks like the following example:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample11.cs?highlight=9-12)]

<span data-ttu-id="8022c-205">부서 편집 페이지를 실행 하 고 이미 다른 부서의 관리자 인 강사에 게 학과의 관리자를 변경 해 보세요.</span><span class="sxs-lookup"><span data-stu-id="8022c-205">Run the Department Edit page and try to change a department's administrator to an instructor who is already the administrator of a different department.</span></span> <span data-ttu-id="8022c-206">필요한 오류 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-206">You get the expected error message:</span></span>

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

<span data-ttu-id="8022c-208">이제 부서 편집 페이지를 다시 실행 하 고 이번에는 **예산** 크기를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-208">Now run the Department Edit page again and this time change the **Budget** amount.</span></span> <span data-ttu-id="8022c-209">**저장**을 클릭 하면 다음과 같은 오류 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-209">When you click **Save**, you see an error page:</span></span>

![Department_Edit_page_with_object_state_manager_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image11.png)

<span data-ttu-id="8022c-211">예외 오류 메시지는 `An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.` 다음 이벤트 시퀀스로 인해 발생 하는 ""입니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-211">The exception error message is "`An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.`" This happened because of the following sequence of events:</span></span>

- <span data-ttu-id="8022c-212">`Edit`메서드는 메서드를 호출 합니다 .이 메서드는 `ValidateOneAdministratorAssignmentPerInstructor` Kim Abercrombie가 관리자 인 모든 부서를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-212">The `Edit` method calls the `ValidateOneAdministratorAssignmentPerInstructor` method, which retrieves all departments that have Kim Abercrombie as their administrator.</span></span> <span data-ttu-id="8022c-213">그러면 영어 부서를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-213">That causes the English department to be read.</span></span> <span data-ttu-id="8022c-214">이는 편집 중인 부서 이므로 오류가 보고 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-214">Because that's the department being edited, no error is reported.</span></span> <span data-ttu-id="8022c-215">그러나이 읽기 작업의 결과로 데이터베이스에서 읽은 English 학과 엔터티는 이제 데이터베이스 컨텍스트에 의해 추적 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-215">As a result of this read operation, however, the English department entity that was read from the database is now being tracked by the database context.</span></span>
- <span data-ttu-id="8022c-216">`Edit`메서드는 `Modified` MVC 모델 바인더에서 만든 english 학과 엔터티에 대 한 플래그를 설정 하려고 하지만, 컨텍스트가 영어 부서에 대 한 엔터티를 이미 추적 하 고 있으므로 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-216">The `Edit` method tries to set the `Modified` flag on the English department entity created by the MVC model binder, but that fails because the context is already tracking an entity for the English department.</span></span>

<span data-ttu-id="8022c-217">이 문제에 대 한 한 가지 해결책은 유효성 검사 쿼리에서 검색 된 메모리 내 부서 엔터티를 추적 하지 못하도록 컨텍스트를 유지 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-217">One solution to this problem is to keep the context from tracking in-memory department entities retrieved by the validation query.</span></span> <span data-ttu-id="8022c-218">이 작업을 수행 하는 경우에는 문제가 발생 하지 않습니다 .이 엔터티는 메모리에 캐시 되는 방식으로이 엔터티를 업데이트 하거나 다시 읽을 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-218">There's no disadvantage to doing this, because you won't be updating this entity or reading it again in a way that would benefit from it being cached in memory.</span></span>

<span data-ttu-id="8022c-219">*DepartmentController.cs*의 `ValidateOneAdministratorAssignmentPerInstructor` 메서드에서 다음에 표시 된 것 처럼 추적 안 함을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-219">In *DepartmentController.cs*, in the `ValidateOneAdministratorAssignmentPerInstructor` method, specify no tracking, as shown in the following:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample12.cs?highlight=4)]

<span data-ttu-id="8022c-220">부서의 **예산** 금액을 편집 하는 시도를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-220">Repeat your attempt to edit the **Budget** amount of a department.</span></span> <span data-ttu-id="8022c-221">이번에는 작업이 성공적으로 수행 되 고 사이트는 수정 된 예산 값을 표시 하는 부서 인덱스 페이지에 예상 대로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-221">This time the operation is successful, and the site returns as expected to the Departments Index page, showing the revised budget value.</span></span>

## <a name="examining-queries-sent-to-the-database"></a><span data-ttu-id="8022c-222">데이터베이스로 전송 된 쿼리 검사</span><span class="sxs-lookup"><span data-stu-id="8022c-222">Examining Queries Sent to the Database</span></span>

<span data-ttu-id="8022c-223">때로는 데이터베이스로 전송된 실제 SQL 쿼리를 볼 수 있는 것이 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-223">Sometimes it's helpful to be able to see the actual SQL queries that are sent to the database.</span></span> <span data-ttu-id="8022c-224">이렇게 하려면 디버거에서 쿼리 변수를 검사 하거나 쿼리의 메서드를 호출할 수 있습니다 `ToString` .</span><span class="sxs-lookup"><span data-stu-id="8022c-224">To do this, you can examine a query variable in the debugger or call the query's `ToString` method.</span></span> <span data-ttu-id="8022c-225">이 작업을 수행 하려면 간단한 쿼리를 살펴본 다음 즉시 로드, 필터링, 정렬 등의 옵션을 추가할 때 발생 하는 상황을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-225">To try this out, you'll look at a simple query and then look at what happens to it as you add options such eager loading, filtering, and sorting.</span></span>

<span data-ttu-id="8022c-226">*Controllers/CourseController*에서 `Index` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-226">In *Controllers/CourseController*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample13.cs?highlight=3)]

<span data-ttu-id="8022c-227">이제의 *GenericRepository.cs* `return query.ToList();` 및 메서드의 문에 중단점을 설정 `return orderBy(query).ToList();` `Get` 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-227">Now set a breakpoint in *GenericRepository.cs* on the `return query.ToList();` and the `return orderBy(query).ToList();` statements of the `Get` method.</span></span> <span data-ttu-id="8022c-228">디버그 모드에서 프로젝트를 실행 하 고 과정 인덱스 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-228">Run the project in debug mode and select the Course Index page.</span></span> <span data-ttu-id="8022c-229">코드가 중단점에 도달 하면 변수를 검사 `query` 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-229">When the code reaches the breakpoint, examine the `query` variable.</span></span> <span data-ttu-id="8022c-230">SQL Server로 전송 된 쿼리가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-230">You see the query that's sent to SQL Server.</span></span> <span data-ttu-id="8022c-231">간단한 `Select` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-231">It's a simple `Select` statement:</span></span>

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample14.json)]

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

<span data-ttu-id="8022c-232">쿼리가 너무 길어서 Visual Studio의 디버깅 창에 표시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-232">Queries can be too long to display in the debugging windows in Visual Studio.</span></span> <span data-ttu-id="8022c-233">전체 쿼리를 보려면 변수 값을 복사 하 여 텍스트 편집기에 붙여 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-233">To see the entire query, you can copy the variable value and paste it into a text editor:</span></span>

![Copy_value_of_variable_in_debug_mode](https://asp.net/media/2578239/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Copy_value_of_variable_in_debug_mode_0902a2b1-b799-47a6-9b4b-f266c79d83c1.png)

<span data-ttu-id="8022c-235">이제 사용자가 특정 부서에 대해 필터링 할 수 있도록 강좌 인덱스 페이지에 드롭다운 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-235">Now you'll add a drop-down list to the Course Index page so that users can filter for a particular department.</span></span> <span data-ttu-id="8022c-236">코스를 제목별로 정렬 하 고 탐색 속성에 대해 즉시 로드를 지정 `Department` 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-236">You'll sort the courses by title, and you'll specify eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="8022c-237">*CourseController.cs*에서 `Index` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-237">In *CourseController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample15.cs)]

<span data-ttu-id="8022c-238">메서드는 매개 변수의 드롭다운 목록에서 선택한 값을 받습니다 `SelectedDepartment` .</span><span class="sxs-lookup"><span data-stu-id="8022c-238">The method receives the selected value of the drop-down list in the `SelectedDepartment` parameter.</span></span> <span data-ttu-id="8022c-239">아무 것도 선택 하지 않으면이 매개 변수는 null이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-239">If nothing is selected, this parameter will be null.</span></span>

<span data-ttu-id="8022c-240">`SelectList`모든 부서를 포함 하는 컬렉션은 드롭다운 목록에 대 한 보기로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-240">A `SelectList` collection containing all departments is passed to the view for the drop-down list.</span></span> <span data-ttu-id="8022c-241">생성자에 전달 된 매개 변수는 `SelectList` 값 필드 이름, 텍스트 필드 이름 및 선택 된 항목을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-241">The parameters passed to the `SelectList` constructor specify the value field name, the text field name, and the selected item.</span></span>

<span data-ttu-id="8022c-242">`Get`리포지토리의 메서드에 대해 `Course` 코드는 탐색 속성에 대 한 필터 식, 정렬 순서 및 즉시 로드를 지정 합니다 `Department` .</span><span class="sxs-lookup"><span data-stu-id="8022c-242">For the `Get` method of the `Course` repository, the code specifies a filter expression, a sort order, and eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="8022c-243">`true`드롭다운 목록에서 선택 된 항목이 없는 경우 (즉, null 임) 필터 식은 항상를 반환 합니다 `SelectedDepartment` .</span><span class="sxs-lookup"><span data-stu-id="8022c-243">The filter expression always returns `true` if nothing is selected in the drop-down list (that is, `SelectedDepartment` is null).</span></span>

<span data-ttu-id="8022c-244">*Views\Course\Index.cshtml*에서 여는 태그 바로 앞에 `table` 다음 코드를 추가 하 여 드롭다운 목록과 제출 단추를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-244">In *Views\Course\Index.cshtml*, immediately before the opening `table` tag, add the following code to create the drop-down list and a submit button:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample16.cshtml)]

<span data-ttu-id="8022c-245">클래스에서 중단점을 설정한 상태에서 `GenericRepository` 과정 인덱스 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-245">With the breakpoints still set in the `GenericRepository` class, run the Course Index page.</span></span> <span data-ttu-id="8022c-246">코드가 중단점에 도달 하는 처음 두 번을 계속 진행 하 여 페이지가 브라우저에 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-246">Continue through the first two times that the code hits a breakpoint, so that the page is displayed in the browser.</span></span> <span data-ttu-id="8022c-247">드롭다운 목록에서 부서를 선택 하 고 **필터**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-247">Select a department from the drop-down list and click **Filter**:</span></span>

![Course_Index_page_with_department_selected](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

<span data-ttu-id="8022c-249">이번에는 드롭다운 목록에 대 한 부서 쿼리의 첫 번째 중단점이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-249">This time the first breakpoint will be for the departments query for the drop-down list.</span></span> <span data-ttu-id="8022c-250">이를 건너뛰고 다음에 `query` 코드가 중단점에 도달 했을 때 해당 변수가 어떻게 표시 되는지 확인 합니다 `Course` .</span><span class="sxs-lookup"><span data-stu-id="8022c-250">Skip that and view the `query` variable the next time the code reaches the breakpoint in order to see what the `Course` query now looks like.</span></span> <span data-ttu-id="8022c-251">다음과 같은 내용이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-251">You'll see something like the following:</span></span>

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample17.json)]

<span data-ttu-id="8022c-252">이제 쿼리는 `JOIN` `Department` 데이터와 함께 데이터를 로드 하는 쿼리 `Course` 이며 절이 포함 되어 있음을 알 수 있습니다 `WHERE` .</span><span class="sxs-lookup"><span data-stu-id="8022c-252">You can see that the query is now a `JOIN` query that loads `Department` data along with the `Course` data, and that it includes a `WHERE` clause.</span></span>

<a id="proxyclasses"></a>

## <a name="working-with-proxy-classes"></a><span data-ttu-id="8022c-253">프록시 클래스 작업</span><span class="sxs-lookup"><span data-stu-id="8022c-253">Working with Proxy Classes</span></span>

<span data-ttu-id="8022c-254">Entity Framework에서 엔터티 인스턴스를 만들 때 (예: 쿼리를 실행 하는 경우) 엔터티에 대 한 프록시 역할을 하는 동적으로 생성 된 파생 형식의 인스턴스로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-254">When the Entity Framework creates entity instances (for example, when you execute a query), it often creates them as instances of a dynamically generated derived type that acts as a proxy for the entity.</span></span> <span data-ttu-id="8022c-255">이 프록시는 엔터티의 일부 가상 속성을 재정의 하 여 속성에 액세스할 때 작업을 자동으로 수행 하기 위한 후크를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-255">This proxy overrides some virtual properties of the entity to insert hooks for performing actions automatically when the property is accessed.</span></span> <span data-ttu-id="8022c-256">예를 들어이 메커니즘은 관계 지연 로드를 지 원하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-256">For example, this mechanism is used to support lazy loading of relationships.</span></span>

<span data-ttu-id="8022c-257">대부분의 경우 이러한 프록시 사용을 인식 하지 않아도 되지만 다음과 같은 예외가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-257">Most of the time you don't need to be aware of this use of proxies, but there are exceptions:</span></span>

- <span data-ttu-id="8022c-258">일부 시나리오에서는 Entity Framework에서 프록시 인스턴스를 만들지 못하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-258">In some scenarios you might want to prevent the Entity Framework from creating proxy instances.</span></span> <span data-ttu-id="8022c-259">예를 들어 프록시 인스턴스를 serialize 하는 것 보다 프록시 인스턴스를 serialize 하는 것이 더 효율적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-259">For example, serializing non-proxy instances might be more efficient than serializing proxy instances.</span></span>
- <span data-ttu-id="8022c-260">연산자를 사용 하 여 엔터티 클래스 `new` 를 인스턴스화하면 프록시 인스턴스를 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-260">When you instantiate an entity class using the `new` operator, you don't get a proxy instance.</span></span> <span data-ttu-id="8022c-261">즉, 지연 로드 및 자동 변경 내용 추적과 같은 기능을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-261">This means you don't get functionality such as lazy loading and automatic change tracking.</span></span> <span data-ttu-id="8022c-262">이는 일반적으로 정상입니다. 일반적으로는 데이터베이스에 없는 새 엔터티를 만들고 엔터티를로 명시적으로 표시 하는 경우 일반적으로 변경 내용 추적이 필요 하지 않으므로 지연 로드가 필요 하지 않습니다 `Added` .</span><span class="sxs-lookup"><span data-stu-id="8022c-262">This is typically okay; you generally don't need lazy loading, because you're creating a new entity that isn't in the database, and you generally don't need change tracking if you're explicitly marking the entity as `Added`.</span></span> <span data-ttu-id="8022c-263">그러나 지연 로드가 필요 하 고 변경 내용 추적이 필요한 경우 클래스의 메서드를 사용 하 여 프록시를 사용 하 여 새 엔터티 인스턴스를 만들 수 있습니다 `Create` `DbSet` .</span><span class="sxs-lookup"><span data-stu-id="8022c-263">However, if you do need lazy loading and you need change tracking, you can create new entity instances with proxies using the `Create` method of the `DbSet` class.</span></span>
- <span data-ttu-id="8022c-264">프록시 형식에서 실제 엔터티 형식을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-264">You might want to get an actual entity type from a proxy type.</span></span> <span data-ttu-id="8022c-265">`GetObjectType`클래스의 메서드를 사용 하 여 `ObjectContext` 프록시 형식 인스턴스의 실제 엔터티 형식을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-265">You can use the `GetObjectType` method of the `ObjectContext` class to get the actual entity type of a proxy type instance.</span></span>

<span data-ttu-id="8022c-266">자세한 내용은 Entity Framework 팀 블로그에서 [프록시 작업](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="8022c-266">For more information, see [Working with Proxies](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx) on the Entity Framework team blog.</span></span>

## <a name="disabling-automatic-detection-of-changes"></a><span data-ttu-id="8022c-267">변경 내용 자동 검색 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="8022c-267">Disabling Automatic Detection of Changes</span></span>

<span data-ttu-id="8022c-268">Entity Framework는 엔터티의 현재 값을 원래 값과 비교하여 엔터티가 변경된 방법(즉, 데이터베이스에 전송해야 하는 업데이트)을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-268">The Entity Framework determines how an entity has changed (and therefore which updates need to be sent to the database) by comparing the current values of an entity with the original values.</span></span> <span data-ttu-id="8022c-269">원래 값은 엔터티를 쿼리하거나 연결할 때 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-269">The original values are stored when the entity was queried or attached.</span></span> <span data-ttu-id="8022c-270">자동 변경 내용 검색을 발생시키는 일부 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-270">Some of the methods that cause automatic change detection are the following:</span></span>

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

<span data-ttu-id="8022c-271">많은 수의 엔터티를 추적 하 고 루프에서 이러한 메서드 중 하나를 여러 번 호출 하는 경우 [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx) 속성을 사용 하 여 자동 변경 검색 기능을 일시적으로 해제 하면 성능이 크게 향상 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-271">If you're tracking a large number of entities and you call one of these methods many times in a loop, you might get significant performance improvements by temporarily turning off automatic change detection using the [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx) property.</span></span> <span data-ttu-id="8022c-272">자세한 내용은 [자동으로 변경 내용 검색](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="8022c-272">For more information, see [Automatically Detecting Changes](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx).</span></span>

## <a name="disabling-validation-when-saving-changes"></a><span data-ttu-id="8022c-273">변경 내용을 저장할 때 유효성 검사 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="8022c-273">Disabling Validation When Saving Changes</span></span>

<span data-ttu-id="8022c-274">메서드를 호출 하는 경우 `SaveChanges` 기본적으로 Entity Framework는 데이터베이스를 업데이트 하기 전에 변경 된 모든 엔터티의 모든 속성에 있는 데이터의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-274">When you call the `SaveChanges` method, by default the Entity Framework validates the data in all properties of all changed entities before updating the database.</span></span> <span data-ttu-id="8022c-275">많은 수의 엔터티를 업데이트 하 고 이미 데이터의 유효성을 검사 한 경우이 작업은 필요 하지 않으며, 유효성 검사를 일시적으로 해제 하 여 변경 내용을 저장 하는 프로세스에 시간이 더 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-275">If you've updated a large number of entities and you've already validated the data, this work is unnecessary and you could make the process of saving the changes take less time by temporarily turning off validation.</span></span> <span data-ttu-id="8022c-276">[Validateonsaveenabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx) 속성을 사용 하 여이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-276">You can do that using the [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx) property.</span></span> <span data-ttu-id="8022c-277">자세한 내용은 [유효성 검사](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="8022c-277">For more information, see [Validation](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="8022c-278">요약</span><span class="sxs-lookup"><span data-stu-id="8022c-278">Summary</span></span>

<span data-ttu-id="8022c-279">ASP.NET MVC 응용 프로그램에서 Entity Framework 사용에 대 한이 일련의 자습서를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-279">This completes this series of tutorials on using the Entity Framework in an ASP.NET MVC application.</span></span> <span data-ttu-id="8022c-280">[ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-280">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

<span data-ttu-id="8022c-281">웹 응용 프로그램을 빌드한 후 배포 하는 방법에 대 한 자세한 내용은 MSDN Library에서 [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx) 을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8022c-281">For more information about how to deploy your web application after you've built it, see [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx) in the MSDN Library.</span></span>

<span data-ttu-id="8022c-282">인증 및 권한 부여와 같은 MVC와 관련 된 다른 항목에 대 한 자세한 내용은 [Mvc 권장 리소스](../../getting-started/recommended-resources-for-mvc.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="8022c-282">For information about other topics related to MVC, such as authentication and authorization, see the [MVC Recommended Resources](../../getting-started/recommended-resources-for-mvc.md).</span></span>

<a id="acknowledgments"></a>

## <a name="acknowledgments"></a><span data-ttu-id="8022c-283">감사의 글</span><span class="sxs-lookup"><span data-stu-id="8022c-283">Acknowledgments</span></span>

- <span data-ttu-id="8022c-284">Tom Dykstra는이 자습서의 원래 버전을 작성 했으며 Microsoft 웹 플랫폼 및 도구 콘텐츠 팀의 선임 프로그래밍 기록기입니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-284">Tom Dykstra wrote the original version of this tutorial and is a senior programming writer on the Microsoft Web Platform and Tools Content Team.</span></span>
- <span data-ttu-id="8022c-285">Twitter ( [Rick Anderson](https://blogs.msdn.com/b/rickandy/) ) [@RickAndMSFT](http://twitter.com/RickAndMSFT) 는이 자습서를 공동 작성 하 여 대부분의 작업을 EF 5 및 MVC 4로 업데이트 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-285">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) co-authored this tutorial and did most of the work updating it for EF 5 and MVC 4.</span></span> <span data-ttu-id="8022c-286">Rick는 Azure 및 MVC를 중심으로 하는 Microsoft의 선임 프로그래밍 기록기입니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-286">Rick is a senior programming writer for Microsoft focusing on Azure and MVC.</span></span>
- <span data-ttu-id="8022c-287">[행](http://www.romiller.com) Entity Framework 팀의 고객 및 기타 멤버는 코드 검토를 사용 하 여이를 지원 하 고 EF 5에 대 한 자습서를 업데이트 하는 동안 발생 한 마이그레이션의 많은 문제를 디버그 하는 데 도움이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-287">[Rowan Miller](http://www.romiller.com) and other members of the Entity Framework team assisted with code reviews and helped debug many issues with migrations that arose while we were updating the tutorial for EF 5.</span></span>

## <a name="vb"></a><span data-ttu-id="8022c-288">VB</span><span class="sxs-lookup"><span data-stu-id="8022c-288">VB</span></span>

<span data-ttu-id="8022c-289">자습서를 처음 생성 했을 때 완성 된 다운로드 프로젝트의 c # 및 VB 버전을 모두 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-289">When the tutorial was originally produced, we provided both C# and VB versions of the completed download project.</span></span> <span data-ttu-id="8022c-290">이 업데이트를 사용 하면 각 챕터에 대 한 c # 다운로드 가능한 프로젝트를 제공 하므로 시리즈의 어디에서 나 쉽게 시작할 수 있지만 시간 제한과 기타 우선 순위에 따라 VB에 대해 수행 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-290">With this update we are providing a C# downloadable project for each chapter to make it easier to get started anywhere in the series, but due to time limitations and other priorities we did not do that for VB.</span></span> <span data-ttu-id="8022c-291">이러한 자습서를 사용 하 여 VB 프로젝트를 빌드하고 다른 사용자와 공유 하려는 경우 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="8022c-291">If you build a VB project using these tutorials and would be willing to share that with others, please let us know.</span></span>

<a id="errors"></a>

## <a name="errors-and-workarounds"></a><span data-ttu-id="8022c-292">오류 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="8022c-292">Errors and Workarounds</span></span>

### <a name="cannot-createshadow-copy"></a><span data-ttu-id="8022c-293">복사본을 만들거나 섀도 복사할 수 없음</span><span class="sxs-lookup"><span data-stu-id="8022c-293">Cannot create/shadow copy</span></span>

<span data-ttu-id="8022c-294">오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="8022c-294">Error Message:</span></span>

<span data-ttu-id="8022c-295">*' DotNetOpenAuth. Openid connect '가 이미 있는 경우 해당 파일을 만들거나 섀도 복사할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="8022c-295">*Cannot create/shadow copy 'DotNetOpenAuth.OpenId' when that file already exists.*</span></span>

<span data-ttu-id="8022c-296">해결책:</span><span class="sxs-lookup"><span data-stu-id="8022c-296">Solution:</span></span>

<span data-ttu-id="8022c-297">몇 초 정도 기다렸다가 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-297">Wait a few seconds and refresh the page.</span></span>

### <a name="update-database-not-recognized"></a><span data-ttu-id="8022c-298">업데이트-데이터베이스를 인식할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-298">Update-Database not recognized</span></span>

<span data-ttu-id="8022c-299">오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="8022c-299">Error Message:</span></span>

<span data-ttu-id="8022c-300">*' 업데이트-데이터베이스 ' 라는 용어는 cmdlet, 함수, 스크립트 파일 또는 실행할 수 있는 프로그램의 이름으로 인식 되지 않습니다. 이름의 철자를 확인 하거나, 경로가 포함 된 경우 경로가 올바른지 확인 한 후 다시 시도 하십시오.* ( *`Update-Database`* PMC의 명령에서)</span><span class="sxs-lookup"><span data-stu-id="8022c-300">*The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.*(From the *`Update-Database`* command in the PMC.)</span></span>

<span data-ttu-id="8022c-301">해결책:</span><span class="sxs-lookup"><span data-stu-id="8022c-301">Solution:</span></span>

<span data-ttu-id="8022c-302">Visual Studio를 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-302">Exit Visual Studio.</span></span> <span data-ttu-id="8022c-303">프로젝트를 다시 열고 다시 시도 하세요.</span><span class="sxs-lookup"><span data-stu-id="8022c-303">Reopen project and try again.</span></span>

### <a name="validation-failed"></a><span data-ttu-id="8022c-304">유효성 검사 실패</span><span class="sxs-lookup"><span data-stu-id="8022c-304">Validation failed</span></span>

<span data-ttu-id="8022c-305">오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="8022c-305">Error Message:</span></span>

<span data-ttu-id="8022c-306">*하나 이상의 엔터티에 대 한 유효성 검사에 실패 했습니다. 자세한 내용은 ' EntityValidationErrors ' 속성을 참조 하세요.*</span><span class="sxs-lookup"><span data-stu-id="8022c-306">*Validation failed for one or more entities. See 'EntityValidationErrors' property for more details.*</span></span> <span data-ttu-id="8022c-307">( *`Update-Database`* PMC의 명령에서)</span><span class="sxs-lookup"><span data-stu-id="8022c-307">(From the *`Update-Database`* command in the PMC.)</span></span>

<span data-ttu-id="8022c-308">해결책:</span><span class="sxs-lookup"><span data-stu-id="8022c-308">Solution:</span></span>

<span data-ttu-id="8022c-309">이 문제의 한 가지 원인은 메서드가 실행 될 때 유효성 검사 오류입니다 `Seed` .</span><span class="sxs-lookup"><span data-stu-id="8022c-309">One cause of this problem is validation errors when the `Seed` method runs.</span></span> <span data-ttu-id="8022c-310">메서드를 디버깅 하는 방법에 대 한 팁은 [EF (시드 및 디버깅 Entity Framework) db](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) 를 참조 하세요 `Seed` .</span><span class="sxs-lookup"><span data-stu-id="8022c-310">See [Seeding and Debugging Entity Framework (EF) DBs](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) for tips on debugging the `Seed` method.</span></span>

### <a name="http-50019-error"></a><span data-ttu-id="8022c-311">HTTP 500.19 오류</span><span class="sxs-lookup"><span data-stu-id="8022c-311">HTTP 500.19 error</span></span>

<span data-ttu-id="8022c-312">오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="8022c-312">Error Message:</span></span>

<span data-ttu-id="8022c-313">*HTTP 오류 500.19-내부 서버 오류 페이지에 대 한 관련 구성 데이터가 잘못 되어 요청 된 페이지에 액세스할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="8022c-313">*HTTP Error 500.19 - Internal Server Error The requested page cannot be accessed because the related configuration data for the page is invalid.*</span></span>

<span data-ttu-id="8022c-314">해결책:</span><span class="sxs-lookup"><span data-stu-id="8022c-314">Solution:</span></span>

<span data-ttu-id="8022c-315">이 오류를 발생 시킬 수 있는 한 가지 방법은 각각 동일한 포트 번호를 사용 하 여 솔루션의 복사본을 여러 개 포함 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-315">One way you can get this error is from having multiple copies of the solution, each of them using the same port number.</span></span> <span data-ttu-id="8022c-316">일반적으로 Visual Studio의 모든 인스턴스를 종료 한 다음 작업 중인 프로젝트를 다시 시작 하 여이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-316">You can usually solve this problem by exiting all instances of Visual Studio, then restarting the project your working on.</span></span> <span data-ttu-id="8022c-317">작동 하지 않는 경우 포트 번호를 변경해 보세요.</span><span class="sxs-lookup"><span data-stu-id="8022c-317">If that doesn't work, try changing the port number.</span></span> <span data-ttu-id="8022c-318">프로젝트 파일을 마우스 오른쪽 단추로 클릭 한 다음 속성을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-318">Right click on the project file and then click properties.</span></span> <span data-ttu-id="8022c-319">**웹** 탭을 선택한 다음 **프로젝트 Url** 텍스트 상자에서 포트 번호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-319">Select the **Web** tab and then change the port number in the **Project Url** text box.</span></span>

### <a name="error-locating-sql-server-instance"></a><span data-ttu-id="8022c-320">SQL Server 인스턴스 찾기 오류</span><span class="sxs-lookup"><span data-stu-id="8022c-320">Error locating SQL Server instance</span></span>

<span data-ttu-id="8022c-321">오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="8022c-321">Error Message:</span></span>

<span data-ttu-id="8022c-322">*SQL Server에 대 한 연결을 설정 하는 동안 네트워크 관련 또는 인스턴스 관련 오류가 발생 했습니다. 서버를 찾을 수 없거나 액세스할 수 없습니다. 인스턴스 이름이 올바르고 SQL Server가 원격 연결을 허용 하도록 구성 되어 있는지 확인 하십시오. (공급자: SQL 네트워크 인터페이스, 오류: 26-지정 된 서버/인스턴스 찾기 오류)*</span><span class="sxs-lookup"><span data-stu-id="8022c-322">*A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: SQL Network Interfaces, error: 26 - Error Locating Server/Instance Specified)*</span></span>

<span data-ttu-id="8022c-323">해결책:</span><span class="sxs-lookup"><span data-stu-id="8022c-323">Solution:</span></span>

<span data-ttu-id="8022c-324">연결 문자열을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8022c-324">Check connection string.</span></span> <span data-ttu-id="8022c-325">데이터베이스를 수동으로 삭제 한 경우 생성 문자열에서 데이터베이스 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022c-325">If you have manually deleted the database, change the name of the database in the construction string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8022c-326">[이전](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
> [다음](building-the-ef5-mvc4-chapter-downloads.md)</span><span class="sxs-lookup"><span data-stu-id="8022c-326">[Previous](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
[Next](building-the-ef5-mvc4-chapter-downloads.md)</span></span>
