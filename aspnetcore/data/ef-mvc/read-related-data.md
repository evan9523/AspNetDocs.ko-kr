---
title: '자습서: 관련 데이터 읽기 - ASP.NET MVC 및 EF Core 사용'
description: 이 자습서에서는 관련 데이터 즉, Entity Framework에서 탐색 속성으로 로드하는 데이터를 읽고 표시합니다.
author: rick-anderson
ms.author: tdykstra
ms.date: 02/05/2019
ms.topic: tutorial
uid: data/ef-mvc/read-related-data
ms.openlocfilehash: 73e225c2cd6d9f88079c54115cccad48f43d7d0c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57056900"
---
# <a name="tutorial-read-related-data---aspnet-mvc-with-ef-core"></a><span data-ttu-id="6b99a-103">자습서: 관련 데이터 읽기 - ASP.NET MVC 및 EF Core 사용</span><span class="sxs-lookup"><span data-stu-id="6b99a-103">Tutorial: Read related data - ASP.NET MVC with EF Core</span></span>

<span data-ttu-id="6b99a-104">이전 자습서에서 School 데이터 모델을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-104">In the previous tutorial, you completed the School data model.</span></span> <span data-ttu-id="6b99a-105">이 자습서에서는 관련 데이터 즉, Entity Framework에서 탐색 속성으로 로드하는 데이터를 읽고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-105">In this tutorial, you'll read and display related data -- that is, data that the Entity Framework loads into navigation properties.</span></span>

<span data-ttu-id="6b99a-106">다음 그림에서는 사용할 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-106">The following illustrations show the pages that you'll work with.</span></span>

![강좌 인덱스 페이지](read-related-data/_static/courses-index.png)

![강사 인덱스 페이지](read-related-data/_static/instructors-index.png)

<span data-ttu-id="6b99a-109">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6b99a-110">관련 데이터를 로드하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="6b99a-110">Learn how to load related data</span></span>
> * <span data-ttu-id="6b99a-111">강좌 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="6b99a-111">Create a Courses page</span></span>
> * <span data-ttu-id="6b99a-112">강사 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="6b99a-112">Create an Instructors page</span></span>
> * <span data-ttu-id="6b99a-113">명시적 로드에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="6b99a-113">Learn about explicit loading</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b99a-114">전제 조건</span><span class="sxs-lookup"><span data-stu-id="6b99a-114">Prerequisites</span></span>

* [<span data-ttu-id="6b99a-115">ASP.NET Core MVC 웹앱용 EF Core를 사용하여 더 복잡한 데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="6b99a-115">Create a more complex data model with EF Core for an ASP.NET Core MVC web app</span></span>](complex-data-model.md)

## <a name="learn-how-to-load-related-data"></a><span data-ttu-id="6b99a-116">관련 데이터를 로드하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="6b99a-116">Learn how to load related data</span></span>

<span data-ttu-id="6b99a-117">Entity Framework와 같은 ORM(개체-관계형 매핑) 소프트웨어에서 관련된 데이터를 엔터티의 탐색 속성으로 로드할 수 있는 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-117">There are several ways that Object-Relational Mapping (ORM) software such as Entity Framework can load related data into the navigation properties of an entity:</span></span>

* <span data-ttu-id="6b99a-118">즉시 로드</span><span class="sxs-lookup"><span data-stu-id="6b99a-118">Eager loading.</span></span> <span data-ttu-id="6b99a-119">엔터티를 읽을 때 관련된 데이터가 함께 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-119">When the entity is read, related data is retrieved along with it.</span></span> <span data-ttu-id="6b99a-120">이는 일반적으로 필요한 데이터를 모두 검색하는 단일 조인 쿼리를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-120">This typically results in a single join query that retrieves all of the data that's needed.</span></span> <span data-ttu-id="6b99a-121">`Include` 및 `ThenInclude` 메서드를 사용하여 Entity Framework Core에 즉시 로드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-121">You specify eager loading in Entity Framework Core by using the `Include` and `ThenInclude` methods.</span></span>

  ![즉시 로드 예제](read-related-data/_static/eager-loading.png)

  <span data-ttu-id="6b99a-123">별도 쿼리에서 일부 데이터를 검색할 수 있으며 EF는 탐색 속성을 "수정합니다".</span><span class="sxs-lookup"><span data-stu-id="6b99a-123">You can retrieve some of the data in separate queries, and EF "fixes up" the navigation properties.</span></span>  <span data-ttu-id="6b99a-124">즉, EF는 이전에 검색된 엔터티의 탐색 속성에 속해 있는 개별적으로 검색된 엔터티를 자동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-124">That is, EF automatically adds the separately retrieved entities where they belong in navigation properties of previously retrieved entities.</span></span> <span data-ttu-id="6b99a-125">관련된 데이터를 검색하는 쿼리의 경우 `ToList` 또는 `Single`과 같은 목록 또는 개체를 반환하는 메서드 대신 `Load` 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-125">For the query that retrieves related data, you can use the `Load` method instead of a method that returns a list or object, such as `ToList` or `Single`.</span></span>

  ![별도 쿼리 예제](read-related-data/_static/separate-queries.png)

* <span data-ttu-id="6b99a-127">명시적 로드</span><span class="sxs-lookup"><span data-stu-id="6b99a-127">Explicit loading.</span></span> <span data-ttu-id="6b99a-128">엔터티를 처음 읽을 때 관련된 데이터가 검색되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-128">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="6b99a-129">필요한 경우 관련된 데이터를 검색하는 코드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-129">You write code that retrieves the related data if it's needed.</span></span> <span data-ttu-id="6b99a-130">별도 쿼리가 있는 즉시 로드의 경우처럼 명시적 로드로 인해 여러 쿼리가 데이터베이스로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-130">As in the case of eager loading with separate queries, explicit loading results in multiple queries sent to the database.</span></span> <span data-ttu-id="6b99a-131">명시적 로드와의 차이점은 코드는 로드될 탐색 속성을 지정한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-131">The difference is that with explicit loading, the code specifies the navigation properties to be loaded.</span></span> <span data-ttu-id="6b99a-132">Entity Framework Core 1.1에서 `Load` 메서드를 사용하여 명시적 로드를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-132">In Entity Framework Core 1.1 you can use the `Load` method to do explicit loading.</span></span> <span data-ttu-id="6b99a-133">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="6b99a-133">For example:</span></span>

  ![명시적 로드 예제](read-related-data/_static/explicit-loading.png)

* <span data-ttu-id="6b99a-135">지연 로드</span><span class="sxs-lookup"><span data-stu-id="6b99a-135">Lazy loading.</span></span> <span data-ttu-id="6b99a-136">엔터티를 처음 읽을 때 관련된 데이터가 검색되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-136">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="6b99a-137">그러나 탐색 속성에 처음으로 액세스하려고 할 때 해당 탐색 속성에 필요한 데이터가 자동으로 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-137">However, the first time you attempt to access a navigation property, the data required for that navigation property is automatically retrieved.</span></span> <span data-ttu-id="6b99a-138">탐색 속성에서 처음으로 데이터를 가져오려고 할 때마다 쿼리가 데이터베이스에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-138">A query is sent to the database each time you try to get data from a navigation property for the first time.</span></span> <span data-ttu-id="6b99a-139">Entity Framework Core 1.0은 지연 로드를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-139">Entity Framework Core 1.0 doesn't support lazy loading.</span></span>

### <a name="performance-considerations"></a><span data-ttu-id="6b99a-140">성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="6b99a-140">Performance considerations</span></span>

<span data-ttu-id="6b99a-141">검색된 모든 엔터티에 대해 관련된 데이터가 필요한 경우 데이터베이스에 전송된 단일 쿼리는 검색된 각 엔터티에 대한 별도 쿼리보다 일반적으로 더 효율적이므로 즉시 로드는 종종 최상의 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-141">If you know you need related data for every entity retrieved, eager loading often offers the best performance, because a single query sent to the database is typically more efficient than separate queries for each entity retrieved.</span></span> <span data-ttu-id="6b99a-142">예를 들어 각 부서에 10개의 관련된 강좌가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-142">For example, suppose that each department has ten related courses.</span></span> <span data-ttu-id="6b99a-143">모든 관련된 데이터의 즉시 로드로 인해 데이터베이스에 대한 단일(조인) 쿼리 및 단일 왕복이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-143">Eager loading of all related data would result in just a single (join) query and a single round trip to the database.</span></span> <span data-ttu-id="6b99a-144">각 부서의 강좌에 대한 별도 쿼리는 데이터베이스에 대한 11개 왕복을 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-144">A separate query for courses for each department would result in eleven round trips to the database.</span></span> <span data-ttu-id="6b99a-145">데이터베이스에 대한 추가 왕복은 대기 시간이 길 때 성능에 특히 악영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-145">The extra round trips to the database are especially detrimental to performance when latency is high.</span></span>

<span data-ttu-id="6b99a-146">반면에 일부 시나리오에서 별도 쿼리는 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-146">On the other hand, in some scenarios separate queries is more efficient.</span></span> <span data-ttu-id="6b99a-147">하나의 쿼리에서 관련된 모든 데이터의 즉시 로드로 인해 SQL Server에서 효율적으로 처리할 수 없는 매우 복잡한 조인이 생성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-147">Eager loading of all related data in one query might cause a very complex join to be generated, which SQL Server can't process efficiently.</span></span> <span data-ttu-id="6b99a-148">또는 처리하는 엔터티 집합의 하위 집합에 대해서만 엔터티의 탐색 속성에 액세스해야 하는 경우 별도 쿼리는 이전의 모든 즉시 로드에서 필요한 것보다 더 많은 데이터를 검색하므로 더 잘 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-148">Or if you need to access an entity's navigation properties only for a subset of a set of the entities you're processing, separate queries might perform better because eager loading of everything up front would retrieve more data than you need.</span></span> <span data-ttu-id="6b99a-149">성능이 중요한 경우 최상의 선택을 위해 두 가지 방식으로 성능을 테스트하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-149">If performance is critical, it's best to test performance both ways in order to make the best choice.</span></span>

## <a name="create-a-courses-page"></a><span data-ttu-id="6b99a-150">강좌 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="6b99a-150">Create a Courses page</span></span>

<span data-ttu-id="6b99a-151">강좌 엔터티는 강좌에 할당된 부서의 부서 엔터티를 포함하는 탐색 속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-151">The Course entity includes a navigation property that contains the Department entity of the department that the course is assigned to.</span></span> <span data-ttu-id="6b99a-152">강좌의 목록에 할당된 부서의 이름을 표시하려면 `Course.Department` 탐색 속성에 있는 부서 엔터티에서 이름 속성을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-152">To display the name of the assigned department in a list of courses, you need to get the Name property from the Department entity that's in the `Course.Department` navigation property.</span></span>

<span data-ttu-id="6b99a-153">보기로 **MVC 컨트롤러에 대한 동일한 옵션을 사용하고, 다음 그림에서 표시된 것과 같이 학생 컨트롤러에 대해 앞에서 수행한 Entity Framework** 스캐폴더를 사용하여 강좌 엔터티 형식에 대해 CoursesController라는 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-153">Create a controller named CoursesController for the Course entity type, using the same options for the **MVC Controller with views, using Entity Framework** scaffolder that you did earlier for the Students controller, as shown in the following illustration:</span></span>

![강좌 컨트롤러 추가](read-related-data/_static/add-courses-controller.png)

<span data-ttu-id="6b99a-155">*CoursesController.cs*를 열고 `Index` 메서드를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-155">Open *CoursesController.cs* and examine the `Index` method.</span></span> <span data-ttu-id="6b99a-156">자동 스캐폴딩은 `Include` 메서드를 사용하여 `Department` 탐색 속성에 대해 즉시 로드를 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-156">The automatic scaffolding has specified eager loading for the `Department` navigation property by using the `Include` method.</span></span>

<span data-ttu-id="6b99a-157">`Index` 메서드를 강좌 엔터티를 반환하는 `IQueryable`에 대해 더욱 적절한 이름을 사용하는 다음 코드로 바꿉니다(`schoolContext` 대신 `courses`).</span><span class="sxs-lookup"><span data-stu-id="6b99a-157">Replace the `Index` method with the following code that uses a more appropriate name for the `IQueryable` that returns Course entities (`courses` instead of `schoolContext`):</span></span>

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_RevisedIndexMethod)]

<span data-ttu-id="6b99a-158">*Views/Courses/Index.cshtml*을 열고 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-158">Open *Views/Courses/Index.cshtml* and replace the template code with the following code.</span></span> <span data-ttu-id="6b99a-159">변경 내용은 강조 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-159">The changes are highlighted:</span></span>

[!code-html[](intro/samples/cu/Views/Courses/Index.cshtml?highlight=4,7,15-17,34-36,44)]

<span data-ttu-id="6b99a-160">스캐폴드 코드에 다음 변경 내용을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-160">You've made the following changes to the scaffolded code:</span></span>

* <span data-ttu-id="6b99a-161">인덱스에서 강좌로 제목이 변경됐습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-161">Changed the heading from Index to Courses.</span></span>

* <span data-ttu-id="6b99a-162">`CourseID` 속성 값을 보여 주는 **Number** 열을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-162">Added a **Number** column that shows the `CourseID` property value.</span></span> <span data-ttu-id="6b99a-163">일반적으로 최종 사용자에게 의미가 없으므로 기본적으로 기본 키는 스캐폴드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-163">By default, primary keys aren't scaffolded because normally they're meaningless to end users.</span></span> <span data-ttu-id="6b99a-164">그러나 이 경우 기본 키는 의미가 있으며 표시하길 원합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-164">However, in this case the primary key is meaningful and you want to show it.</span></span>

* <span data-ttu-id="6b99a-165">부서 이름을 표시하도록 **부서** 열을 변경했습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-165">Changed the **Department** column to display the department name.</span></span> <span data-ttu-id="6b99a-166">코드는 `Department` 탐색 속성으로 로드되는 부서 엔터티의 `Name` 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-166">The code displays the `Name` property of the Department entity that's loaded into the `Department` navigation property:</span></span>

  ```html
  @Html.DisplayFor(modelItem => item.Department.Name)
  ```

<span data-ttu-id="6b99a-167">앱을 실행하고 **강좌** 탭을 선택하여 부서 이름이 있는 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-167">Run the app and select the **Courses** tab to see the list with department names.</span></span>

![과정 인덱스 페이지](read-related-data/_static/courses-index.png)

## <a name="create-an-instructors-page"></a><span data-ttu-id="6b99a-169">강사 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="6b99a-169">Create an Instructors page</span></span>

<span data-ttu-id="6b99a-170">이 섹션에서는 강사 페이지를 표시하기 위해 강사 엔터티에 대한 컨트롤러 및 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-170">In this section, you'll create a controller and view for the Instructor entity in order to display the Instructors page:</span></span>

![강사 인덱스 페이지](read-related-data/_static/instructors-index.png)

<span data-ttu-id="6b99a-172">이 페이지는 다음과 같은 방법으로 관련된 데이터를 읽고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-172">This page reads and displays related data in the following ways:</span></span>

* <span data-ttu-id="6b99a-173">강사 목록은 OfficeAssignment 엔터티에서 관련된 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-173">The list of instructors displays related data from the OfficeAssignment entity.</span></span> <span data-ttu-id="6b99a-174">강사와 OfficeAssignment 엔터티는 일대영 또는 일 관계에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-174">The Instructor and OfficeAssignment entities are in a one-to-zero-or-one relationship.</span></span> <span data-ttu-id="6b99a-175">OfficeAssignment 엔터티에 대해 즉시 로드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-175">You'll use eager loading for the OfficeAssignment entities.</span></span> <span data-ttu-id="6b99a-176">이전에 설명한 대로 기본 테이블의 검색된 모든 행에 관련된 데이터가 필요한 경우 즉시 로드는 일반적으로 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-176">As explained earlier, eager loading is typically more efficient when you need the related data for all retrieved rows of the primary table.</span></span> <span data-ttu-id="6b99a-177">이 경우 표시된 모든 강사에 대한 사무실 할당을 표시하길 원합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-177">In this case, you want to display office assignments for all displayed instructors.</span></span>

* <span data-ttu-id="6b99a-178">사용자가 강사를 선택하면 관련된 강좌 엔터티가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-178">When the user selects an instructor, related Course entities are displayed.</span></span> <span data-ttu-id="6b99a-179">강사 및 강좌 엔터티는 다대다 관계에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-179">The Instructor and Course entities are in a many-to-many relationship.</span></span> <span data-ttu-id="6b99a-180">강좌 엔터티 및 관련된 해당 부서 엔터티에 대해 즉시 로드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-180">You'll use eager loading for the Course entities and their related Department entities.</span></span> <span data-ttu-id="6b99a-181">이 경우 선택한 강사에 대해서만 강좌가 필요하기 때문에 별도 쿼리가 더 효율적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-181">In this case, separate queries might be more efficient because you need courses only for the selected instructor.</span></span> <span data-ttu-id="6b99a-182">그러나 이 예제에서는 탐색 속성에 있는 엔터티 내에서 탐색 속성에 대한 즉시 로드를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-182">However, this example shows how to use eager loading for navigation properties within entities that are themselves in navigation properties.</span></span>

* <span data-ttu-id="6b99a-183">사용자가 강좌를 선택하면 등록 엔터티 집합에서 관련된 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-183">When the user selects a course, related data from the Enrollments entity set is displayed.</span></span> <span data-ttu-id="6b99a-184">강좌 및 등록 엔터티는 일대다 관계에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-184">The Course and Enrollment entities are in a one-to-many relationship.</span></span> <span data-ttu-id="6b99a-185">등록 엔터티 및 관련된 해당 학생 엔터티에 대해 별도 쿼리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-185">You'll use separate queries for Enrollment entities and their related Student entities.</span></span>

### <a name="create-a-view-model-for-the-instructor-index-view"></a><span data-ttu-id="6b99a-186">강사 인덱스 보기에 대한 뷰 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="6b99a-186">Create a view model for the Instructor Index view</span></span>

<span data-ttu-id="6b99a-187">강사 페이지는 서로 다른 세 테이블에서 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-187">The Instructors page shows data from three different tables.</span></span> <span data-ttu-id="6b99a-188">따라서 각각이 테이블 중 하나에 대한 데이터를 보유하는 세 가지 속성을 포함하는 보기 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-188">Therefore, you'll create a view model that includes three properties, each holding the data for one of the tables.</span></span>

<span data-ttu-id="6b99a-189">*SchoolViewModels* 폴더에서 *InstructorIndexData.cs*를 만들고 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-189">In the *SchoolViewModels* folder, create *InstructorIndexData.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Models/SchoolViewModels/InstructorIndexData.cs)]

### <a name="create-the-instructor-controller-and-views"></a><span data-ttu-id="6b99a-190">강사 컨트롤러 및 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="6b99a-190">Create the Instructor controller and views</span></span>

<span data-ttu-id="6b99a-191">다음 그림에 나와 있는 것처럼 EF 읽기/쓰기 동작으로 강사 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-191">Create an Instructors controller with EF read/write actions as shown in the following illustration:</span></span>

![강사 컨트롤러 추가](read-related-data/_static/add-instructors-controller.png)

<span data-ttu-id="6b99a-193">*InstructorsController.cs*를 열고 ViewModels 네임스페이스에 대해 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-193">Open *InstructorsController.cs* and add a using statement for the ViewModels namespace:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_Using)]

<span data-ttu-id="6b99a-194">인덱스 메서드를 다음 코드로 바꿔 관련된 데이터의 즉시 로드를 수행하고 보기 모델에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-194">Replace the Index method with the following code to do eager loading of related data and put it in the view model.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_EagerLoading)]

<span data-ttu-id="6b99a-195">메서드는 선택한 강사 및 선택한 강좌의 ID 값을 제공하는 선택적 경로 데이터(`id`) 및 쿼리 문자열 매개 변수(`courseID`)를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-195">The method accepts optional route data (`id`) and a query string parameter (`courseID`) that provide the ID values of the selected instructor and selected course.</span></span> <span data-ttu-id="6b99a-196">매개 변수는 페이지의 **선택** 하이퍼링크에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-196">The parameters are provided by the **Select** hyperlinks on the page.</span></span>

<span data-ttu-id="6b99a-197">코드는 보기 모델의 인스턴스를 만들고 강사 목록에 배치하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-197">The code begins by creating an instance of the view model and putting in it the list of instructors.</span></span> <span data-ttu-id="6b99a-198">코드는 `Instructor.OfficeAssignment` 및 `Instructor.CourseAssignments` 탐색 속성에 대한 즉시 로드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-198">The code specifies eager loading for the `Instructor.OfficeAssignment` and the `Instructor.CourseAssignments` navigation properties.</span></span> <span data-ttu-id="6b99a-199">`CourseAssignments` 속성 내에서 `Course` 속성이 로드되고, 해당 속성 내에서 `Enrollments` 및 `Department` 속성이 로드되고, 각 `Enrollment` 엔터티 내에서 `Student` 속성이 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-199">Within the `CourseAssignments` property, the `Course` property is loaded, and within that, the `Enrollments` and `Department` properties are loaded, and within each `Enrollment` entity the `Student` property is loaded.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_ThenInclude)]

<span data-ttu-id="6b99a-200">보기는 항상 OfficeAssignment 엔터티가 필요하므로 동일한 쿼리에서 인출하는 것이 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-200">Since the view always requires the OfficeAssignment entity, it's more efficient to fetch that in the same query.</span></span> <span data-ttu-id="6b99a-201">강좌 엔터티는 강사가 웹 페이지에서 선택된 경우에 필요하므로 단일 쿼리는 페이지가 선택된 강좌와 함께 더 자주 표시되는 경우에만(함께 표시되지 않는 것보다) 여러 쿼리보다 낫습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-201">Course entities are required when an instructor is selected in the web page, so a single query is better than multiple queries only if the page is displayed more often with a course selected than without.</span></span>

<span data-ttu-id="6b99a-202">`Course`에서 두 개의 속성이 필요하므로 코드는 `CourseAssignments` 및 `Course`를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-202">The code repeats `CourseAssignments` and `Course` because you need two properties from `Course`.</span></span> <span data-ttu-id="6b99a-203">`ThenInclude` 호출의 첫 번째 문자열은 `CourseAssignment.Course`, `Course.Enrollments` 및 `Enrollment.Student`를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-203">The first string of `ThenInclude` calls gets `CourseAssignment.Course`, `Course.Enrollments`, and `Enrollment.Student`.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_ThenInclude&highlight=3-6)]

<span data-ttu-id="6b99a-204">코드의 해당 지점에서 다른 `ThenInclude`는 필요하지 않은 `Student`의 탐색 속성에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-204">At that point in the code, another `ThenInclude` would be for navigation properties of `Student`, which you don't need.</span></span> <span data-ttu-id="6b99a-205">하지만 `Include`를 호출하면 `Instructor` 속성으로 다시 시작하므로 체인을 통해 다시 이동해야 합니다. 이 때 `Course.Enrollments` 대신 `Course.Department`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-205">But calling `Include` starts over with `Instructor` properties, so you have to go through the chain again, this time specifying `Course.Department` instead of `Course.Enrollments`.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_ThenInclude&highlight=7-9)]

<span data-ttu-id="6b99a-206">다음 코드는 강사가 선택되었을 때 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-206">The following code executes when an instructor was selected.</span></span> <span data-ttu-id="6b99a-207">선택한 강사는 보기 모델의 강사 목록에서 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-207">The selected instructor is retrieved from the list of instructors in the view model.</span></span> <span data-ttu-id="6b99a-208">보기 모델의 `Courses` 속성은 해당 강사의 `CourseAssignments` 탐색 속성에서 강좌 엔터티로 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-208">The view model's `Courses` property is then loaded with the Course entities from that instructor's `CourseAssignments` navigation property.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?range=56-62)]

<span data-ttu-id="6b99a-209">`Where` 메서드는 컬렉션을 반환하지만 이 경우 해당 메서드에 전달된 조건으로 반환되는 단일 강사 엔터티만 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-209">The `Where` method returns a collection, but in this case the criteria passed to that method result in only a single Instructor entity being returned.</span></span> <span data-ttu-id="6b99a-210">`Single` 메서드는 컬렉션을 단일 강사 엔터티로 변환합니다. 이는 해당 엔터티의 `CourseAssignments` 속성에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-210">The `Single` method converts the collection into a single Instructor entity, which gives you access to that entity's `CourseAssignments` property.</span></span> <span data-ttu-id="6b99a-211">`CourseAssignments` 속성은 `CourseAssignment` 엔터티를 포함합니다. 여기에서 관련된 `Course` 엔터티만을 원합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-211">The `CourseAssignments` property contains `CourseAssignment` entities, from which you want only the related `Course` entities.</span></span>

<span data-ttu-id="6b99a-212">하나의 항목만을 가질 컬렉션을 아는 경우 컬렉션에서 `Single` 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-212">You use the `Single` method on a collection when you know the collection will have only one item.</span></span> <span data-ttu-id="6b99a-213">단일 메서드는 전달된 컬렉션이 비어 있거나 둘 이상의 항목이 있는 경우 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-213">The Single method throws an exception if the collection passed to it's empty or if there's more than one item.</span></span> <span data-ttu-id="6b99a-214">대안은 `SingleOrDefault`입니다. 컬렉션이 비어 있는 경우 기본값을 반환합니다(이 경우 Null).</span><span class="sxs-lookup"><span data-stu-id="6b99a-214">An alternative is `SingleOrDefault`, which returns a default value (null in this case) if the collection is empty.</span></span> <span data-ttu-id="6b99a-215">그러나 이 경우에 여전히 예외가 발생하며(null 참조에서 `Courses` 속성을 찾으려는 시도에서), 예외 메시지는 문제의 원인을 덜 명확하게 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-215">However, in this case that would still result in an exception (from trying to find a `Courses` property on a null reference), and the exception message would less clearly indicate the cause of the problem.</span></span> <span data-ttu-id="6b99a-216">`Single` 메서드를 호출하는 경우 `Where` 메서드를 별도로 호출하는 대신 Where 조건을 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-216">When you call the `Single` method, you can also pass in the Where condition instead of calling the `Where` method separately:</span></span>

```csharp
.Single(i => i.ID == id.Value)
```

<span data-ttu-id="6b99a-217">위 코드를 아래 코드 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-217">Instead of:</span></span>

```csharp
.Where(i => i.ID == id.Value).Single()
```

<span data-ttu-id="6b99a-218">다음으로 강좌를 선택한 경우 선택한 강좌가 보기 모델의 강좌 목록에서 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-218">Next, if a course was selected, the selected course is retrieved from the list of courses in the view model.</span></span> <span data-ttu-id="6b99a-219">보기 모델의 `Enrollments` 속성은 해당 강좌의 `Enrollments` 탐색 속성에서 등록 엔터티로 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-219">Then the view model's `Enrollments` property is loaded with the Enrollment entities from that course's `Enrollments` navigation property.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?range=64-69)]

### <a name="modify-the-instructor-index-view"></a><span data-ttu-id="6b99a-220">강사 인덱스 뷰 수정</span><span class="sxs-lookup"><span data-stu-id="6b99a-220">Modify the Instructor Index view</span></span>

<span data-ttu-id="6b99a-221">*Views/Instructors/Index.cshtml*에서 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-221">In *Views/Instructors/Index.cshtml*, replace the template code with the following code.</span></span> <span data-ttu-id="6b99a-222">변경 내용은 강조 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-222">The changes are highlighted.</span></span>

[!code-html[](intro/samples/cu/Views/Instructors/Index1.cshtml?range=1-64&highlight=1,3-7,15-19,24,26-31,41-54,56)]

<span data-ttu-id="6b99a-223">기존 코드에 다음 변경 내용을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-223">You've made the following changes to the existing code:</span></span>

* <span data-ttu-id="6b99a-224">모델 클래스를 `InstructorIndexData`로 변경했습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-224">Changed the model class to `InstructorIndexData`.</span></span>

* <span data-ttu-id="6b99a-225">페이지 제목을 **인덱스**에서 **강사**로 변경했습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-225">Changed the page title from **Index** to **Instructors**.</span></span>

* <span data-ttu-id="6b99a-226">`item.OfficeAssignment`가 Null이 아닌 경우에만 `item.OfficeAssignment.Location`을 표시하는 **사무실** 열을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-226">Added an **Office** column that displays `item.OfficeAssignment.Location` only if `item.OfficeAssignment` isn't null.</span></span> <span data-ttu-id="6b99a-227">(이는 일대영 또는 일 관계이기 때문에 관련된 OfficeAssignment 엔터티가 있을 수 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="6b99a-227">(Because this is a one-to-zero-or-one relationship, there might not be a related OfficeAssignment entity.)</span></span>

  ```html
  @if (item.OfficeAssignment != null)
  {
      @item.OfficeAssignment.Location
  }
  ```

* <span data-ttu-id="6b99a-228">각 강사가 가르치는 강좌를 표시하는 **강좌** 열을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-228">Added a **Courses** column that displays courses taught by each instructor.</span></span> <span data-ttu-id="6b99a-229">이 razor 구문에 대한 자세한 내용은 [`@:`를 사용하여 명시적 줄 전환](xref:mvc/views/razor#explicit-line-transition-with-)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b99a-229">See [Explicit Line Transition with `@:`](xref:mvc/views/razor#explicit-line-transition-with-) for more about this razor syntax.</span></span>

* <span data-ttu-id="6b99a-230">선택된 강사의 `tr` 요소에 `class="success"`를 동적으로 추가하는 코드를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-230">Added code that dynamically adds `class="success"` to the `tr` element of the selected instructor.</span></span> <span data-ttu-id="6b99a-231">부트스트랩 클래스를 사용하여 선택된 행에 대한 배경색을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-231">This sets a background color for the selected row using a Bootstrap class.</span></span>

  ```html
  string selectedRow = "";
  if (item.ID == (int?)ViewData["InstructorID"])
  {
      selectedRow = "success";
  }
  <tr class="@selectedRow">
  ```

* <span data-ttu-id="6b99a-232">선택된 강사의 ID가 `Index` 메서드에 전송되도록 하는 각 행의 다른 링크 앞에 새 하이퍼링크 레이블이 지정된 **Select**를 즉시 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-232">Added a new hyperlink labeled **Select** immediately before the other links in each row, which causes the selected instructor's ID to be sent to the `Index` method.</span></span>

  ```html
  <a asp-action="Index" asp-route-id="@item.ID">Select</a> |
  ```

<span data-ttu-id="6b99a-233">앱을 실행하고 **강사** 탭을 선택합니다. 페이지는 관련된 OfficeAssignment 엔터티가 없는 경우 관련된 OfficeAssignment 엔터티의 위치 속성 및 빈 테이블 셀을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-233">Run the app and select the **Instructors** tab. The page displays the Location property of related OfficeAssignment entities and an empty table cell when there's no related OfficeAssignment entity.</span></span>

![선택한 항목이 없는 강사 인덱스 페이지](read-related-data/_static/instructors-index-no-selection.png)

<span data-ttu-id="6b99a-235">*Views/Instructors/Index.cshtml* 파일에서 닫는 테이블 요소(파일의 끝부분) 뒤에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-235">In the *Views/Instructors/Index.cshtml* file, after the closing table element (at the end of the file), add the following code.</span></span> <span data-ttu-id="6b99a-236">이 코드는 강사가 선택된 경우 강사와 관련된 강좌의 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-236">This code displays a list of courses related to an instructor when an instructor is selected.</span></span>

[!code-html[](intro/samples/cu/Views/Instructors/Index1.cshtml?range=66-101)]

<span data-ttu-id="6b99a-237">이 코드는 보기 모델의 `Courses` 속성을 읽어 강좌의 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-237">This code reads the `Courses` property of the view model to display a list of courses.</span></span> <span data-ttu-id="6b99a-238">또한 선택된 강좌의 ID를 `Index` 동작 메서드에 전송하는 **Select** 하이퍼링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-238">It also provides a **Select** hyperlink that sends the ID of the selected course to the `Index` action method.</span></span>

<span data-ttu-id="6b99a-239">페이지를 새로 고치고 강사를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-239">Refresh the page and select an instructor.</span></span> <span data-ttu-id="6b99a-240">이제 선택된 강사에 할당된 강좌를 표시하는 표가 표시되고 각 강좌에 대해 할당된 부서의 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-240">Now you see a grid that displays courses assigned to the selected instructor, and for each course you see the name of the assigned department.</span></span>

![강사가 선택된 강사 인덱스 페이지](read-related-data/_static/instructors-index-instructor-selected.png)

<span data-ttu-id="6b99a-242">방금 추가한 코드 블록 뒤에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-242">After the code block you just added, add the following code.</span></span> <span data-ttu-id="6b99a-243">해당 강좌가 선택된 경우에 강좌에 등록된 학생의 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-243">This displays a list of the students who are enrolled in a course when that course is selected.</span></span>

[!code-html[](intro/samples/cu/Views/Instructors/Index1.cshtml?range=103-125)]

<span data-ttu-id="6b99a-244">이 코드는 강좌에 등록한 학생의 목록을 표시하기 위해 보기 모델의 등록 속성을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-244">This code reads the Enrollments property of the view model in order to display a list of students enrolled in the course.</span></span>

<span data-ttu-id="6b99a-245">페이지를 다시 새로 고치고 강사를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-245">Refresh the page again and select an instructor.</span></span> <span data-ttu-id="6b99a-246">그런 다음, 강좌를 선택하여 등록된 학생 및 해당 등급의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-246">Then select a course to see the list of enrolled students and their grades.</span></span>

![강사 및 과정이 선택된 강사 인덱스 페이지](read-related-data/_static/instructors-index.png)

## <a name="about-explicit-loading"></a><span data-ttu-id="6b99a-248">명시적 로드 정보</span><span class="sxs-lookup"><span data-stu-id="6b99a-248">About explicit loading</span></span>

<span data-ttu-id="6b99a-249">*InstructorsController.cs*에서 강사 목록을 검색한 경우 `CourseAssignments` 탐색 속성에 대한 즉시 로드를 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-249">When you retrieved the list of instructors in *InstructorsController.cs*, you specified eager loading for the `CourseAssignments` navigation property.</span></span>

<span data-ttu-id="6b99a-250">사용자가 선택된 강사 및 강좌에서 등록을 드물게 확인하려고 한다는 것을 예상했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-250">Suppose you expected users to only rarely want to see enrollments in a selected instructor and course.</span></span> <span data-ttu-id="6b99a-251">이 경우 요청된 경우에만 등록 데이터를 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-251">In that case, you might want to load the enrollment data only if it's requested.</span></span> <span data-ttu-id="6b99a-252">명시적 로드를 수행하는 방법의 예를 보려면 `Index` 메서드를 등록에 대한 즉시 로드를 제거하고 해당 속성을 명시적으로 로드하는 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-252">To see an example of how to do explicit loading, replace the `Index` method with the following code, which removes eager loading for Enrollments and loads that property explicitly.</span></span> <span data-ttu-id="6b99a-253">코드 변경 내용은 강조 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-253">The code changes are highlighted.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_ExplicitLoading&highlight=23-29)]

<span data-ttu-id="6b99a-254">새 코드는 강사 엔터티를 검색하는 코드에서 등록 데이터에 대한 *ThenInclude* 메서드 호출을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-254">The new code drops the *ThenInclude* method calls for enrollment data from the code that retrieves instructor entities.</span></span> <span data-ttu-id="6b99a-255">강사 및 강좌가 선택된 경우 강조 표시된 코드는 선택된 강좌에 대한 등록 엔터티 및 각 등록에 대한 학생 엔터티를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-255">If an instructor and course are selected, the highlighted code retrieves Enrollment entities for the selected course, and Student entities for each Enrollment.</span></span>

<span data-ttu-id="6b99a-256">앱을 실행하고, 강사 인덱스 페이지로 이동하면 데이터가 검색되는 방법을 변경했더라도 페이지에 표시되는 내용에 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-256">Run the app, go to the Instructors Index page now and you'll see no difference in what's displayed on the page, although you've changed how the data is retrieved.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="6b99a-257">코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="6b99a-257">Get the code</span></span>

[<span data-ttu-id="6b99a-258">완성된 애플리케이션을 다운로드하거나 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-258">Download or view the completed application.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)

## <a name="next-steps"></a><span data-ttu-id="6b99a-259">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b99a-259">Next steps</span></span>

<span data-ttu-id="6b99a-260">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-260">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6b99a-261">관련 데이터를 로드하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="6b99a-261">Learned how to load related data</span></span>
> * <span data-ttu-id="6b99a-262">강좌 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="6b99a-262">Created a Courses page</span></span>
> * <span data-ttu-id="6b99a-263">강사 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="6b99a-263">Created an Instructors page</span></span>
> * <span data-ttu-id="6b99a-264">명시적 로드에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="6b99a-264">Learned about explicit loading</span></span>

<span data-ttu-id="6b99a-265">관련 데이터를 업데이트하는 방법을 알아보려면 다음 문서로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="6b99a-265">Advance to the next article to learn how to update related data.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="6b99a-266">관련 데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="6b99a-266">Update related data</span></span>](update-related-data.md)
