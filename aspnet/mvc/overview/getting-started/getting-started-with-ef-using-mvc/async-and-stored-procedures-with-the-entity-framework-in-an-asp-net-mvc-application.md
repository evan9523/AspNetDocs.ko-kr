---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
title: '자습서: ASP.NET MVC 앱에서 EF를 사용 하 여 비동기 및 저장된 프로시저 사용'
description: 이 자습서는 비동기 프로그래밍 모델을 구현 하 고 저장된 프로시저를 사용 하는 방법을 알아봅니다 하는 방법을 볼 수 있습니다.
author: tdykstra
ms.author: riande
ms.date: 01/18/2019
ms.topic: tutorial
ms.assetid: 27d110fc-d1b7-4628-a763-26f1e6087549
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 5612f2f25d06feb904a205505ed8f048d2263266
ms.sourcegitcommit: dd0dc556a3d99a31d8fdbc763e9a2e53f3441b70
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67410934"
---
# <a name="tutorial-use-async-and-stored-procedures-with-ef-in-an-aspnet-mvc-app"></a><span data-ttu-id="ae425-103">자습서: ASP.NET MVC 앱에서 EF를 사용 하 여 비동기 및 저장된 프로시저 사용</span><span class="sxs-lookup"><span data-stu-id="ae425-103">Tutorial: Use async and stored procedures with EF in an ASP.NET MVC App</span></span>

<span data-ttu-id="ae425-104">이전 자습서에서 읽고 동기 프로그래밍 모델을 사용 하 여 데이터를 업데이트 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-104">In earlier tutorials you learned how to read and update data using the synchronous programming model.</span></span> <span data-ttu-id="ae425-105">이 자습서는 비동기 프로그래밍 모델을 구현 하는 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-105">In this tutorial you see how to implement the asynchronous programming model.</span></span> <span data-ttu-id="ae425-106">비동기 코드는 더 나은 서버 리소스 사용 했기 때문에 더 잘 수행 하는 응용 프로그램을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-106">Asynchronous code can help an application perform better because it makes better use of server resources.</span></span>

<span data-ttu-id="ae425-107">이 자습서에서는 삽입, 업데이트 및 삭제 작업 엔터티에 대 한 저장된 프로시저를 사용 하는 방법을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-107">In this tutorial you also see how to use stored procedures for insert, update, and delete operations on an entity.</span></span>

<span data-ttu-id="ae425-108">마지막으로, 모든 데이터베이스 변경 내용을 처음 배포한 이후 구현한와 함께 azure에 응용 프로그램에 다시 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-108">Finally, you redeploy the application to Azure, along with all of the database changes that you've implemented since the first time you deployed.</span></span>

<span data-ttu-id="ae425-109">다음 그림에서는 사용할 일부 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-109">The following illustrations show some of the pages that you'll work with.</span></span>

![부서 페이지](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![부서를 만듭니다](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="ae425-112">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-112">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ae425-113">비동기 코드에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="ae425-113">Learn about asynchronous code</span></span>
> * <span data-ttu-id="ae425-114">부서 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="ae425-114">Create a Department controller</span></span>
> * <span data-ttu-id="ae425-115">저장된 프로시저를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-115">Use stored procedures</span></span>
> * <span data-ttu-id="ae425-116">Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="ae425-116">Deploy to Azure</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae425-117">전제 조건</span><span class="sxs-lookup"><span data-stu-id="ae425-117">Prerequisites</span></span>

* [<span data-ttu-id="ae425-118">관련 데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="ae425-118">Updating Related Data</span></span>](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="why-use-asynchronous-code"></a><span data-ttu-id="ae425-119">비동기 코드를 사용 하는 이유</span><span class="sxs-lookup"><span data-stu-id="ae425-119">Why use asynchronous code</span></span>

<span data-ttu-id="ae425-120">웹 서버에는 사용할 수 있는 스레드 수가 제한적이며, 로드 양이 많은 상황에서는 사용 가능한 모든 스레드가 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-120">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="ae425-121">이 경우 서버는 스레드가 해제될 때까지 새 요청을 처리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-121">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="ae425-122">동기 코드를 사용하면 I/O 완료를 대기하느라 작업을 실제로 수행하지 않는 동안에 많은 스레드가 정체될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-122">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="ae425-123">비동기 코드를 사용하면 프로세스가 I/O 완료를 대기할 때 다른 요청을 처리하는 데 사용하도록 해당 스레드가 서버에서 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-123">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="ae425-124">결과적으로, 비동기 코드를 사용 하면 서버 리소스를를 보다 효율적으로 사용 되며 서버 지연 없이 더 많은 트래픽을 처리할 수 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-124">As a result, asynchronous code enables server resources to be use more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="ae425-125">.NET의 이전 버전에서 작성 하 고 비동기 코드를 테스트 된 복잡 한 오류가 발생 하기 쉽고, 디버깅 하기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-125">In earlier versions of .NET, writing and testing asynchronous code was complex, error prone, and hard to debug.</span></span> <span data-ttu-id="ae425-126">.NET 4.5 작성, 테스트 및 비동기 코드를 디버깅은 훨씬 쉬워졌기 때문에 한 이유가 없다면 없는 비동기 코드 일반적으로 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-126">In .NET 4.5, writing, testing, and debugging asynchronous code is so much easier that you should generally write asynchronous code unless you have a reason not to.</span></span> <span data-ttu-id="ae425-127">비동기 코드는 적은 양의 오버 헤드를 도입 하지만 트래픽이 낮은 상황의 성능 저하는 미미 합니다 하는 동안 트래픽이 높은 상황에서는 잠재적 성능 향상이 상당한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-127">Asynchronous code does introduce a small amount of overhead, but for low traffic situations the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="ae425-128">비동기 프로그래밍에 대 한 자세한 내용은 참조 하세요. [호출을 차단 하지 않기 위해 사용 하 여.NET 4.5의 비동기 지원](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-128">For more information about asynchronous programming, see [Use .NET 4.5's async support to avoid blocking calls](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async).</span></span>

## <a name="create-department-controller"></a><span data-ttu-id="ae425-129">부서 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="ae425-129">Create Department controller</span></span>

<span data-ttu-id="ae425-130">이 시간을 제외 하 고 이전 컨트롤러에 수행한 것과 동일한 방식으로 선택 하는 부서 컨트롤러를 만들려면 합니다 **비동기 컨트롤러 동작을 사용 하 여** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-130">Create a Department controller the same way you did the earlier controllers, except this time select the **Use async controller actions** check box.</span></span>

<span data-ttu-id="ae425-131">다음 강조 표시에 대 한 동기 코드에 추가 된 기능을 `Index` 메서드를 비동기:</span><span class="sxs-lookup"><span data-stu-id="ae425-131">The following highlights show what was added to the synchronous code for the `Index` method to make it asynchronous:</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=1,4)]

<span data-ttu-id="ae425-132">비동기적으로 실행 하는 Entity Framework 데이터베이스 쿼리를 사용 하도록 설정 하려면 네 가지 변경 내용이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-132">Four changes were applied to enable the Entity Framework database query to execute asynchronously:</span></span>

- <span data-ttu-id="ae425-133">메서드가 사용 하 여 표시 합니다 `async` 키워드는 컴파일러가 메서드 본문 부분에 대 한 콜백을 생성 하 고 자동으로 만들 수 있는 `Task<ActionResult>` 반환 되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-133">The method is marked with the `async` keyword, which tells the compiler to generate callbacks for parts of the method body and to automatically create the `Task<ActionResult>` object that is returned.</span></span>
- <span data-ttu-id="ae425-134">반환 형식을 변경한 `ActionResult` 에 `Task<ActionResult>`입니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-134">The return type was changed from `ActionResult` to `Task<ActionResult>`.</span></span> <span data-ttu-id="ae425-135">합니다 `Task<T>` 형식을 나타내는 형식의 결과 사용 하 여 진행 중인 작업 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-135">The `Task<T>` type represents ongoing work with a result of type `T`.</span></span>
- <span data-ttu-id="ae425-136">`await` 키워드 웹 서비스 호출에 적용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-136">The `await` keyword was applied to the web service call.</span></span> <span data-ttu-id="ae425-137">컴파일러가이 키워드를 인식 하는 경우 백그라운드에서 해당 메서드를 두 부분으로 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-137">When the compiler sees this keyword, behind the scenes it splits the method into two parts.</span></span> <span data-ttu-id="ae425-138">첫 번째 부분은 비동기적으로 시작 되는 작업을 사용 하 여 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-138">The first part ends with the operation that is started asynchronously.</span></span> <span data-ttu-id="ae425-139">두 번째 부분은 작업이 완료 될 때 호출 되는 콜백 메서드에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-139">The second part is put into a callback method that is called when the operation completes.</span></span>
- <span data-ttu-id="ae425-140">비동기 버전을 `ToList` 확장 메서드가 호출 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-140">The asynchronous version of the `ToList` extension method was called.</span></span>

<span data-ttu-id="ae425-141">이유는 합니다 `departments.ToList` 문을 수정 하지만 `departments = db.Departments` 문을?</span><span class="sxs-lookup"><span data-stu-id="ae425-141">Why is the `departments.ToList` statement modified but not the `departments = db.Departments` statement?</span></span> <span data-ttu-id="ae425-142">이유는 쿼리 또는 명령을 데이터베이스를 전송할 수 있도록 하는 명령문만 비동기적으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-142">The reason is that only statements that cause queries or commands to be sent to the database are executed asynchronously.</span></span> <span data-ttu-id="ae425-143">`departments = db.Departments` 문은 쿼리 설정 되지만 쿼리 될 때까지 실행 되지 않습니다는 `ToList` 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-143">The `departments = db.Departments` statement sets up a query but the query is not executed until the `ToList` method is called.</span></span> <span data-ttu-id="ae425-144">따라서만 `ToList` 메서드를 비동기적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-144">Therefore, only the `ToList` method is executed asynchronously.</span></span>

<span data-ttu-id="ae425-145">에 `Details` 메서드 및 `HttpGet` `Edit` 하 고 `Delete` 메서드를 `Find` 메서드는 비동기적으로 실행 되는 메서드는 데이터베이스를 전송할 수 있도록 쿼리를 발생 시키는 것:</span><span class="sxs-lookup"><span data-stu-id="ae425-145">In the `Details` method and the `HttpGet` `Edit` and `Delete` methods, the `Find` method is the one that causes a query to be sent to the database, so that's the method that gets executed asynchronously:</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs?highlight=7)]

<span data-ttu-id="ae425-146">에 `Create`, `HttpPost Edit`, 및 `DeleteConfirmed` 메서드를 합니다 `SaveChanges` 실행할 명령을 발생 시키는 메서드 호출, 같은 문의 하지 `db.Departments.Add(department)` 엔터티 수정할 메모리에만 발생 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-146">In the `Create`, `HttpPost Edit`, and `DeleteConfirmed` methods, it is the `SaveChanges` method call that causes a command to be executed, not statements such as `db.Departments.Add(department)` which only cause entities in memory to be modified.</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=6)]

<span data-ttu-id="ae425-147">오픈 *Views\Department\Index.cshtml*, 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-147">Open *Views\Department\Index.cshtml*, and replace the template code with the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=3,5,20-22,36-38)]

<span data-ttu-id="ae425-148">이 코드 제목을 변경 하는 인덱스에서 부서, 관리자 이름 오른쪽으로 이동한 후 관리자의 전체 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-148">This code changes the title from Index to Departments, moves the Administrator name to the right, and provides the full name of the administrator.</span></span>

<span data-ttu-id="ae425-149">만들기, 삭제, 세부화, 고 뷰를 편집에 대 한 캡션을 변경는 `InstructorID` 필드를 "Administrator" 같은 방식으로 강좌 보기에 "부서"으로 부서 이름 필드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-149">In the Create, Delete, Details, and Edit views, change the caption for the `InstructorID` field to "Administrator" the same way you changed the department name field to "Department" in the Course views.</span></span>

<span data-ttu-id="ae425-150">뷰는 만들기 및 편집에 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-150">In the Create and Edit views use the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml)]

<span data-ttu-id="ae425-151">삭제 및 세부 정보 보기에서 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-151">In the Delete and Details views use the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

<span data-ttu-id="ae425-152">응용 프로그램을 실행 하 고 클릭 합니다 **부서** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-152">Run the application, and click the **Departments** tab.</span></span>

<span data-ttu-id="ae425-153">모든 다른 컨트롤러와 동일 하 게 작동 하지만이 컨트롤러의 모든 SQL 쿼리는 비동기적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-153">Everything works the same as in the other controllers, but in this controller all of the SQL queries are executing asynchronously.</span></span>

<span data-ttu-id="ae425-154">Entity Framework를 사용한 비동기 프로그래밍을 사용할 때 알아야 할 몇 가지 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-154">Some things to be aware of when you are using asynchronous programming with the Entity Framework:</span></span>

- <span data-ttu-id="ae425-155">비동기 코드를 스레드로부터 안전 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-155">The async code is not thread safe.</span></span> <span data-ttu-id="ae425-156">즉, 즉, 하려고 하지 마세요 동일한 컨텍스트 인스턴스를 사용 하 여 병렬로 여러 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-156">In other words, in other words, don't try to do multiple operations in parallel using the same context instance.</span></span>
- <span data-ttu-id="ae425-157">비동기 코드의 성능 이점을 활용하려는 경우 사용 중인(예: 페이징) 라이브러리 패키지 또한 쿼리를 데이터베이스에 전송하도록 하는 Entity Framework 메서드를 호출하는 경우 비동기를 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-157">If you want to take advantage of the performance benefits of async code, make sure that any library packages that you're using (such as for paging), also use async if they call any Entity Framework methods that cause queries to be sent to the database.</span></span>

## <a name="use-stored-procedures"></a><span data-ttu-id="ae425-158">저장된 프로시저를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-158">Use stored procedures</span></span>

<span data-ttu-id="ae425-159">일부 개발자와 dba가 데이터베이스 액세스를 위한 저장된 프로시저를 사용 하려면.</span><span class="sxs-lookup"><span data-stu-id="ae425-159">Some developers and DBAs prefer to use stored procedures for database access.</span></span> <span data-ttu-id="ae425-160">이전 버전의 Entity Framework에서 저장된 프로시저를 사용 하 여 데이터를 검색할 수 있습니다 [원시 SQL 쿼리 실행](advanced-entity-framework-scenarios-for-an-mvc-web-application.md), 하지만 업데이트 작업에 대 한 저장된 프로시저를 사용 하는 EF를 지시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-160">In earlier versions of Entity Framework you can retrieve data using a stored procedure by [executing a raw SQL query](advanced-entity-framework-scenarios-for-an-mvc-web-application.md), but you can't instruct EF to use stored procedures for update operations.</span></span> <span data-ttu-id="ae425-161">EF 6에서 Code First 저장된 프로시저를 사용 하도록 구성 하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-161">In EF 6 it's easy to configure Code First to use stored procedures.</span></span>

1. <span data-ttu-id="ae425-162">*DAL\SchoolContext.cs*, 강조 표시 된 코드를 추가 하 여 `OnModelCreating` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ae425-162">In *DAL\SchoolContext.cs*, add the highlighted code to the `OnModelCreating` method.</span></span>

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=9)]

    <span data-ttu-id="ae425-163">업데이트 및 삭제 작업에이 코드를 사용 하 여 저장 프로시저는 삽입, Entity Framework는 지시 된 `Department` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="ae425-163">This code instructs Entity Framework to use stored procedures for insert, update, and delete operations on the `Department` entity.</span></span>
2. <span data-ttu-id="ae425-164">패키지 관리 콘솔에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-164">In Package Manage Console, enter the following command:</span></span>

    `add-migration DepartmentSP`

    <span data-ttu-id="ae425-165">오픈 *마이그레이션을\\&lt;타임 스탬프&gt;\_DepartmentSP.cs* 의 코드를 참조 하는 `Up` 만드는 메서드를 삽입, 업데이트 및 삭제 저장 프로시저:</span><span class="sxs-lookup"><span data-stu-id="ae425-165">Open *Migrations\\&lt;timestamp&gt;\_DepartmentSP.cs* to see the code in the `Up` method that creates Insert, Update, and Delete stored procedures:</span></span>

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs?highlight=3-4,26-27,42-43)]
3. <span data-ttu-id="ae425-166">패키지 관리 콘솔에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-166">In Package Manage Console, enter the following command:</span></span>

     `update-database`
4. <span data-ttu-id="ae425-167">디버그 모드에서 응용 프로그램 실행을 클릭 합니다 **부서** 탭을 클릭 한 다음 **새로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-167">Run the application in debug mode, click the **Departments** tab, and then click **Create New**.</span></span>
5. <span data-ttu-id="ae425-168">새 학과 대 한 데이터를 입력 한 다음 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-168">Enter data for a new department, and then click **Create**.</span></span>

6. <span data-ttu-id="ae425-169">Visual Studio에서 로그를 확인 합니다 **출력** 창 새 부서 행을 삽입 하려면 저장된 프로시저를 사용 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-169">In Visual Studio, look at the logs in the **Output** window to see that a stored procedure was used to insert the new Department row.</span></span>

     ![부서 삽입 SP](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="ae425-171">코드는 먼저 기본 저장 프로시저 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-171">Code First creates default stored procedure names.</span></span> <span data-ttu-id="ae425-172">기존 데이터베이스를 사용 하는 경우 데이터베이스에 이미 정의 된 저장된 프로시저를 사용 하려면 저장된 프로시저 이름을 사용자 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-172">If you are using an existing database, you might need to customize the stored procedure names in order to use stored procedures already defined in the database.</span></span> <span data-ttu-id="ae425-173">그렇게 하는 방법에 대 한 정보를 참조 하세요 [Entity Framework 코드 첫 번째 Insert/Update/Delete 저장 프로시저](https://msdn.microsoft.com/data/dn468673)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-173">For information about how to do that, see [Entity Framework Code First Insert/Update/Delete Stored Procedures](https://msdn.microsoft.com/data/dn468673).</span></span>

<span data-ttu-id="ae425-174">항목 생성 저장된 프로시저를 수행 하는 사용자 지정 하려는 경우 마이그레이션 스 캐 폴드 된 코드를 편집할 수 있습니다 `Up` 메서드는 저장된 프로시저를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-174">If you want to customize what generated stored procedures do, you can edit the scaffolded code for the migrations `Up` method that creates the stored procedure.</span></span> <span data-ttu-id="ae425-175">이런 방식으로 변경 내용이 반영 됩니다 때마다 마이그레이션 실행 하 고 마이그레이션 배포 된 후 프로덕션에서 자동으로 실행 될 때 프로덕션 데이터베이스에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-175">That way your changes are reflected whenever that migration is run and will be applied to your production database when migrations runs automatically in production after deployment.</span></span>

<span data-ttu-id="ae425-176">추가 마이그레이션 명령을 사용 하 여 새 마이그레이션을 생성 하 고 수동으로 호출 하는 코드를 작성할 수 마이그레이션 이전에 만든 기존 저장된 프로시저를 변경 하려는 경우는 [AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx) 메서드 .</span><span class="sxs-lookup"><span data-stu-id="ae425-176">If you want to change an existing stored procedure that was created in a previous migration, you can use the Add-Migration command to generate a blank migration, and then manually write code that calls the [AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx) method.</span></span>

## <a name="deploy-to-azure"></a><span data-ttu-id="ae425-177">Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="ae425-177">Deploy to Azure</span></span>

<span data-ttu-id="ae425-178">이 섹션에서는 선택적 완료 해야 **Azure에 앱을 배포** 섹션을 [마이그레이션 및 배포](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md) 이 시리즈의 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-178">This section requires you to have completed the optional **Deploying the app to Azure** section in the [Migrations and Deployment](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial of this series.</span></span> <span data-ttu-id="ae425-179">로컬 프로젝트에서 데이터베이스를 삭제 하 여 해결 하는 마이그레이션 오류를 설치한 경우이 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-179">If you had migrations errors that you resolved by deleting the database in your local project, skip this section.</span></span>

1. <span data-ttu-id="ae425-180">Visual studio에서에서 프로젝트를 마우스 오른쪽 단추로 **솔루션 탐색기** 선택한 **게시** 상황에 맞는 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-180">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
2. <span data-ttu-id="ae425-181">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-181">Click **Publish**.</span></span>

    <span data-ttu-id="ae425-182">Visual Studio에는 응용 프로그램을 azure에 배포 하 고 응용 프로그램이 Azure에서 실행 중인 기본 브라우저에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-182">Visual Studio deploys the application to Azure, and the application opens in your default browser, running in Azure.</span></span>
3. <span data-ttu-id="ae425-183">확인을 위해 응용 프로그램을 테스트 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-183">Test the application to verify it's working.</span></span>

    <span data-ttu-id="ae425-184">실행 하는 페이지는 처음에는 데이터베이스에 액세스, Entity Framework를 실행 하 여 마이그레이션의 모든 `Up` 데이터베이스를 현재 데이터 모델을 사용 하 여 최신 상태로 만드는 데 필요한 메서드.</span><span class="sxs-lookup"><span data-stu-id="ae425-184">The first time you run a page that accesses the database, the Entity Framework runs all of the migrations `Up` methods required to bring the database up to date with the current data model.</span></span> <span data-ttu-id="ae425-185">이제 마지막으로이 자습서에서 추가한 부서 페이지를 포함 하 여 배포한 이후에 추가 된 웹 페이지의 모든 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-185">You can now use all of the web pages that you added since the last time you deployed, including the Department pages that you added in this tutorial.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="ae425-186">코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="ae425-186">Get the code</span></span>

[<span data-ttu-id="ae425-187">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="ae425-187">Download the Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="ae425-188">추가 자료</span><span class="sxs-lookup"><span data-stu-id="ae425-188">Additional resources</span></span>

<span data-ttu-id="ae425-189">다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 합니다 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-189">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae425-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae425-190">Next steps</span></span>

<span data-ttu-id="ae425-191">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-191">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ae425-192">비동기 코드에 대 한 학습</span><span class="sxs-lookup"><span data-stu-id="ae425-192">Learned about asynchronous code</span></span>
> * <span data-ttu-id="ae425-193">부서 컨트롤러 생성</span><span class="sxs-lookup"><span data-stu-id="ae425-193">Created a Department controller</span></span>
> * <span data-ttu-id="ae425-194">저장된 프로시저를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae425-194">Used stored procedures</span></span>
> * <span data-ttu-id="ae425-195">Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="ae425-195">Deployed to Azure</span></span>

<span data-ttu-id="ae425-196">여러 사용자가 동시에 동일한 엔터티를 업데이트 하는 경우 충돌을 처리 하는 방법을 알아보려면 다음 문서로 계속 진행 하세요.</span><span class="sxs-lookup"><span data-stu-id="ae425-196">Advance to the next article to learn how to handle conflicts when multiple users update the same entity at the same time.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ae425-197">동시성 처리</span><span class="sxs-lookup"><span data-stu-id="ae425-197">Handling concurrency</span></span>](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
