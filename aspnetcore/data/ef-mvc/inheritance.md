---
title: '자습서: 상속 구현 - ASP.NET MVC 및 EF Core 사용'
description: 이 자습서에서는 ASP.NET Core 애플리케이션에서 Entity Framework Core를 사용하여 데이터 모델에서 상속을 구현하는 방법을 보여 줍니다.
author: rick-anderson
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/05/2019
ms.topic: tutorial
uid: data/ef-mvc/inheritance
ms.openlocfilehash: 0a5eb1aba43bc2adf746202772c7f98eff49b4ff
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57059060"
---
# <a name="tutorial-implement-inheritance---aspnet-mvc-with-ef-core"></a><span data-ttu-id="bd5ac-103">자습서: 상속 구현 - ASP.NET MVC 및 EF Core 사용</span><span class="sxs-lookup"><span data-stu-id="bd5ac-103">Tutorial: Implement inheritance - ASP.NET MVC with EF Core</span></span>

<span data-ttu-id="bd5ac-104">이전 자습서에서는 동시성 예외를 처리했습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-104">In the previous tutorial, you handled concurrency exceptions.</span></span> <span data-ttu-id="bd5ac-105">이 자습서에서는 데이터 모델에서 상속을 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-105">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="bd5ac-106">개체 지향 프로그래밍에서는 쉽게 코드를 재사용하기 위해 상속을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-106">In object-oriented programming, you can use inheritance to facilitate code reuse.</span></span> <span data-ttu-id="bd5ac-107">이 자습서에서는 강사와 학생 모두에게 공통적인 속성(예: `LastName`)이 포함된 `Person` 기본 클래스에서 클래스가 파생되도록 `Instructor` 및 `Student` 클래스를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-107">In this tutorial, you'll change the `Instructor` and `Student` classes so that they derive from a `Person` base class which contains properties such as `LastName` that are common to both instructors and students.</span></span> <span data-ttu-id="bd5ac-108">웹 페이지를 추가하거나 변경하지는 않지만 일부 코드를 변경하고 이러한 변경 내용이 데이터베이스에 자동으로 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-108">You won't add or change any web pages, but you'll change some of the code and those changes will be automatically reflected in the database.</span></span>

<span data-ttu-id="bd5ac-109">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bd5ac-110">데이터베이스에 상속 매핑</span><span class="sxs-lookup"><span data-stu-id="bd5ac-110">Map inheritance to database</span></span>
> * <span data-ttu-id="bd5ac-111">Person 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="bd5ac-111">Create the Person class</span></span>
> * <span data-ttu-id="bd5ac-112">강사 및 학생 업데이트</span><span class="sxs-lookup"><span data-stu-id="bd5ac-112">Update Instructor and Student</span></span>
> * <span data-ttu-id="bd5ac-113">모델에 개인 추가</span><span class="sxs-lookup"><span data-stu-id="bd5ac-113">Add Person to the model</span></span>
> * <span data-ttu-id="bd5ac-114">마이그레이션 만들기 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="bd5ac-114">Create and update migrations</span></span>
> * <span data-ttu-id="bd5ac-115">구현 테스트</span><span class="sxs-lookup"><span data-stu-id="bd5ac-115">Test the implementation</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd5ac-116">전제 조건</span><span class="sxs-lookup"><span data-stu-id="bd5ac-116">Prerequisites</span></span>

* [<span data-ttu-id="bd5ac-117">ASP.NET Core MVC 웹앱에서 EF Core를 사용하여 동시성 처리</span><span class="sxs-lookup"><span data-stu-id="bd5ac-117">Handle Concurrency with EF Core in an ASP.NET Core MVC web app</span></span>](concurrency.md)

## <a name="map-inheritance-to-database"></a><span data-ttu-id="bd5ac-118">데이터베이스에 상속 매핑</span><span class="sxs-lookup"><span data-stu-id="bd5ac-118">Map inheritance to database</span></span>

<span data-ttu-id="bd5ac-119">School 데이터 모델의 `Instructor` 및 `Student` 클래스는 동일한 여러 속성을 가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-119">The `Instructor` and `Student` classes in the School data model have several properties that are identical:</span></span>

![Student 및 Instructor 클래스](inheritance/_static/no-inheritance.png)

<span data-ttu-id="bd5ac-121">`Instructor` 및 `Student` 엔터티에서 공유하는 속성에 대해 중복 코드를 제거하려고 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-121">Suppose you want to eliminate the redundant code for the properties that are shared by the `Instructor` and `Student` entities.</span></span> <span data-ttu-id="bd5ac-122">또는 강사 또는 학생의 이름인지 여부를 신경쓰지 않고 이름의 형식을 지정할 수 있는 서비스를 작성하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-122">Or you want to write a service that can format names without caring whether the name came from an instructor or a student.</span></span> <span data-ttu-id="bd5ac-123">공유 속성만 포함하는 `Person` 기본 클래스를 만든 후 다음 그림과 같이 해당 기본 클래스에서 `Instructor` 및 `Student` 클래스를 상속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-123">You could create a `Person` base class that contains only those shared properties, then make the `Instructor` and `Student` classes inherit from that base class, as shown in the following illustration:</span></span>

![Person 클래스에서 파생된 Student 및 Instructor 클래스](inheritance/_static/inheritance.png)

<span data-ttu-id="bd5ac-125">데이터베이스에 이 상속 구조를 여러 가지 방법으로 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-125">There are several ways this inheritance structure could be represented in the database.</span></span> <span data-ttu-id="bd5ac-126">학생과 강사에 관한 정보를 하나의 테이블에 포함하는 Person 테이블을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-126">You could have a Person table that includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="bd5ac-127">일부 열은 강사(HireDate)에게만, 일부는 학생(EnrollmentDate)에게만, 일부는 둘 다(LastName, FirstName)에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-127">Some of the columns could apply only to instructors (HireDate), some only to students (EnrollmentDate), some to both (LastName, FirstName).</span></span> <span data-ttu-id="bd5ac-128">일반적으로 각 행의 형식을 나타내는 판별자 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-128">Typically, you'd have a discriminator column to indicate which type each row represents.</span></span> <span data-ttu-id="bd5ac-129">예를 들어, 판별자 열은 강사에 대해 "Instructor"를, 학생에 대해 "Student"를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-129">For example, the discriminator column might have "Instructor" for instructors and "Student" for students.</span></span>

![계층당 하나의 테이블 예제](inheritance/_static/tph.png)

<span data-ttu-id="bd5ac-131">단일 데이터베이스 테이블에서 엔터티 상속 구조를 생성하는 이 패턴을 TPH(계층당 하나의 테이블) 상속이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-131">This pattern of generating an entity inheritance structure from a single database table is called table-per-hierarchy (TPH) inheritance.</span></span>

<span data-ttu-id="bd5ac-132">다른 방법은 데이터베이스를 상속 구조와 유사하게 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-132">An alternative is to make the database look more like the inheritance structure.</span></span> <span data-ttu-id="bd5ac-133">예를 들어 Person 테이블에 이름 필드만 있고 날짜 필드가 있는 별도의 Instructor 및 Student 테이블을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-133">For example, you could have only the name fields in the Person table and have separate Instructor and Student tables with the date fields.</span></span>

![형식당 하나의 테이블 상속](inheritance/_static/tpt.png)

<span data-ttu-id="bd5ac-135">각 엔터티 클래스에 대한 데이터베이스 테이블을 만드는 이 패턴을 TPT(형식당 하나의 테이블) 상속이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-135">This pattern of making a database table for each entity class is called table per type (TPT) inheritance.</span></span>

<span data-ttu-id="bd5ac-136">또 다른 옵션은 모든 비추상 형식을 개별 테이블에 매핑하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-136">Yet another option is to map all non-abstract types to individual tables.</span></span> <span data-ttu-id="bd5ac-137">상속된 속성을 포함한 모든 클래스 속성을 해당 테이블의 열에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-137">All properties of a class, including inherited properties, map to columns of the corresponding table.</span></span> <span data-ttu-id="bd5ac-138">이 패턴을 TPC(구체적 클래스당 하나의 테이블) 상속이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-138">This pattern is called Table-per-Concrete Class (TPC) inheritance.</span></span> <span data-ttu-id="bd5ac-139">앞에서 표시된 것처럼 Person, Student 및 Instructor 클래스에 대한 TPC 상속을 구현한 경우, Student 및 Instructor 테이블은 상속을 구현한 후에도 이전과 다르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-139">If you implemented TPC inheritance for the Person, Student, and Instructor classes as shown earlier, the Student and Instructor tables would look no different after implementing inheritance than they did before.</span></span>

<span data-ttu-id="bd5ac-140">TPT 패턴이 복잡한 조인 쿼리를 초래할 수 있기 때문에 TPC 및 TPH 상속 패턴은 일반적으로 TPT 상속 패턴보다 우수한 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-140">TPC and TPH inheritance patterns generally deliver better performance than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span>

<span data-ttu-id="bd5ac-141">이 자습서에서는 TPH 상속을 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-141">This tutorial demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="bd5ac-142">TPH는 Entity Framework Core에서 지원하는 유일한 상속 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-142">TPH is the only inheritance pattern that the Entity Framework Core supports.</span></span>  <span data-ttu-id="bd5ac-143">사용자는 `Person` 클래스를 만들고, `Person`에서 파생되도록 `Instructor` 및 `Student` 클래스를 변경하며 `DbContext`에 새 클래스를 추가하고, 마이그레이션을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-143">What you'll do is create a `Person` class, change the `Instructor` and `Student` classes to derive from `Person`, add the new class to the `DbContext`, and create a migration.</span></span>

> [!TIP]
> <span data-ttu-id="bd5ac-144">다음 내용을 변경하기 전에 프로젝트 사본을 저장하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-144">Consider saving a copy of the project before making the following changes.</span></span>  <span data-ttu-id="bd5ac-145">그러면 문제가 발생하여 처음부터 다시 시작해야 하는 경우, 이 자습서의 단계를 역순으로 하거나 전체 시리즈의 처음으로 돌아가는 대신 저장된 프로젝트에서 쉽게 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-145">Then if you run into problems and need to start over, it will be easier to start from the saved project instead of reversing steps done for this tutorial or going back to the beginning of the whole series.</span></span>

## <a name="create-the-person-class"></a><span data-ttu-id="bd5ac-146">Person 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="bd5ac-146">Create the Person class</span></span>

<span data-ttu-id="bd5ac-147">Models 폴더에서 Person.cs 만들고 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-147">In the Models folder, create Person.cs and replace the template code with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Models/Person.cs)]

## <a name="update-instructor-and-student"></a><span data-ttu-id="bd5ac-148">강사 및 학생 업데이트</span><span class="sxs-lookup"><span data-stu-id="bd5ac-148">Update Instructor and Student</span></span>

<span data-ttu-id="bd5ac-149">*Instructor.cs*에서 Person 클래스에서 Instructor 클래스를 파생시키고 키 및 이름 필드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-149">In *Instructor.cs*, derive the Instructor class from the Person class and remove the key and name fields.</span></span> <span data-ttu-id="bd5ac-150">해당 코드는 다음 예제와 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-150">The code will look like the following example:</span></span>

[!code-csharp[](intro/samples/cu/Models/Instructor.cs?name=snippet_AfterInheritance&highlight=8)]

<span data-ttu-id="bd5ac-151">*Student.cs*에서 동일하게 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-151">Make the same changes in *Student.cs*.</span></span>

[!code-csharp[](intro/samples/cu/Models/Student.cs?name=snippet_AfterInheritance&highlight=8)]

## <a name="add-person-to-the-model"></a><span data-ttu-id="bd5ac-152">모델에 개인 추가</span><span class="sxs-lookup"><span data-stu-id="bd5ac-152">Add Person to the model</span></span>

<span data-ttu-id="bd5ac-153">Person 엔터티 형식을 *SchoolContext.cs*에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-153">Add the Person entity type to *SchoolContext.cs*.</span></span> <span data-ttu-id="bd5ac-154">새 줄이 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-154">The new lines are highlighted.</span></span>

[!code-csharp[](intro/samples/cu/Data/SchoolContext.cs?name=snippet_AfterInheritance&highlight=19,30)]

<span data-ttu-id="bd5ac-155">계층당 하나의 테이블 상속을 구성하기 위해 Entity Framework에 필요한 모든 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-155">This is all that the Entity Framework needs in order to configure table-per-hierarchy inheritance.</span></span> <span data-ttu-id="bd5ac-156">보다시피, 데이터베이스가 업데이트되면 Student 테이블과 Instructor 테이블 대신 Person 테이블이 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-156">As you'll see, when the database is updated, it will have a Person table in place of the Student and Instructor tables.</span></span>

## <a name="create-and-update-migrations"></a><span data-ttu-id="bd5ac-157">마이그레이션 만들기 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="bd5ac-157">Create and update migrations</span></span>

<span data-ttu-id="bd5ac-158">변경 내용을 저장하고 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-158">Save your changes and build the project.</span></span> <span data-ttu-id="bd5ac-159">그런 다음, 프로젝트 폴더에서 명령 창을 열고 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-159">Then open the command window in the project folder and enter the following command:</span></span>

```console
dotnet ef migrations add Inheritance
```

<span data-ttu-id="bd5ac-160">`database update` 명령을 아직 실행하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-160">Don't run the `database update` command yet.</span></span> <span data-ttu-id="bd5ac-161">이 명령은 Instructor 테이블을 삭제하고 Student 테이블 이름을 Person으로 변경하므로 데이터가 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-161">That command will result in lost data because it will drop the Instructor table and rename the Student table to Person.</span></span> <span data-ttu-id="bd5ac-162">기존 데이터를 유지하려면 사용자 지정 코드를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-162">You need to provide custom code to preserve existing data.</span></span>

<span data-ttu-id="bd5ac-163">*Migrations/\<timestamp>_Inheritance.cs*를 여고 `Up` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-163">Open *Migrations/\<timestamp>_Inheritance.cs* and replace the `Up` method with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Migrations/20170216215525_Inheritance.cs?name=snippet_Up)]

<span data-ttu-id="bd5ac-164">이 코드는 다음과 같은 데이터베이스 업데이트 작업을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-164">This code takes care of the following database update tasks:</span></span>

* <span data-ttu-id="bd5ac-165">Student 테이블을 가리키는 외래 키 제약 조건 및 인덱스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-165">Removes foreign key constraints and indexes that point to the Student table.</span></span>

* <span data-ttu-id="bd5ac-166">Instructor 테이블 이름을 Person으로 바꾸고 Student 데이터를 저장하기 위해 필요한 변경을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-166">Renames the Instructor table as Person and makes changes needed for it to store Student data:</span></span>

* <span data-ttu-id="bd5ac-167">학생에 대한 Nullable EnrollmentDate를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-167">Adds nullable EnrollmentDate for students.</span></span>

* <span data-ttu-id="bd5ac-168">행이 학생용인지, 강사용인지 나타내는 판별자 열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-168">Adds Discriminator column to indicate whether a row is for a student or an instructor.</span></span>

* <span data-ttu-id="bd5ac-169">학생 행은 고용 날짜를 포함하지 않으므로 HireDate를 Nullable로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-169">Makes HireDate nullable since student rows won't have hire dates.</span></span>

* <span data-ttu-id="bd5ac-170">학생을 가리키는 외래 키를 업데이트하는 데 사용할 임시 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-170">Adds a temporary field that will be used to update foreign keys that point to students.</span></span> <span data-ttu-id="bd5ac-171">학생을 Person 테이블에 복사하면 새로운 기본 키 값이 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-171">When you copy students into the Person table they will get new primary key values.</span></span>

* <span data-ttu-id="bd5ac-172">Student 테이블에서 Person 테이블로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-172">Copies data from the Student table into the Person table.</span></span> <span data-ttu-id="bd5ac-173">그러면 학생에게 새 기본 키 값이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-173">This causes students to get assigned new primary key values.</span></span>

* <span data-ttu-id="bd5ac-174">학생을 가리키는 외래 키 값을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-174">Fixes foreign key values that point to students.</span></span>

* <span data-ttu-id="bd5ac-175">이제 Person 테이블을 가리키도록 외래 키 제약 조건 및 인덱스를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-175">Re-creates foreign key constraints and indexes, now pointing them to the Person table.</span></span>

<span data-ttu-id="bd5ac-176">(기본 키 형식으로 정수 대신 GUID를 사용한 경우, 학생 기본 키 값을 변경할 필요가 없으며 이 단계 중 일부가 생략되었을 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="bd5ac-176">(If you had used GUID instead of integer as the primary key type, the student primary key values wouldn't have to change, and several of these steps could have been omitted.)</span></span>

<span data-ttu-id="bd5ac-177">`database update` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-177">Run the `database update` command:</span></span>

```console
dotnet ef database update
```

<span data-ttu-id="bd5ac-178">(프로덕션 시스템에서는 이전 데이터베이스 버전으로 돌아가기 위해 사용해야 할 경우를 대비해서 `Down` 메서드에 해당 변경 내용을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-178">(In a production system you would make corresponding changes to the `Down` method in case you ever had to use that to go back to the previous database version.</span></span> <span data-ttu-id="bd5ac-179">이 자습서에서는 `Down` 메서드를 사용하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="bd5ac-179">For this tutorial you won't be using the `Down` method.)</span></span>

> [!NOTE]
> <span data-ttu-id="bd5ac-180">기존 데이터가 있는 데이터베이스에서 스키마를 변경할 때 다른 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-180">It's possible to get other errors when making schema changes in a database that has existing data.</span></span> <span data-ttu-id="bd5ac-181">해결할 수 없는 마이그레이션 오류가 발생하면 연결 문자열에서 데이터베이스 이름을 변경하거나 데이터베이스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-181">If you get migration errors that you can't resolve, you can either change the database name in the connection string or delete the database.</span></span> <span data-ttu-id="bd5ac-182">새 데이터베이스에는 마이그레이션할 데이터가 없으므로 update-database 명령은 오류없이 완료될 가능성이 큽니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-182">With a new database, there's no data to migrate, and the update-database command is more likely to complete without errors.</span></span> <span data-ttu-id="bd5ac-183">데이터베이스를 삭제하려면 SSOX를 사용하거나 `database drop` CLI 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-183">To delete the database, use SSOX or run the `database drop` CLI command.</span></span>

## <a name="test-the-implementation"></a><span data-ttu-id="bd5ac-184">구현 테스트</span><span class="sxs-lookup"><span data-stu-id="bd5ac-184">Test the implementation</span></span>

<span data-ttu-id="bd5ac-185">앱을 실행하고 다양한 페이지를 시도해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-185">Run the app and try various pages.</span></span> <span data-ttu-id="bd5ac-186">모든 항목이 이전과 같이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-186">Everything works the same as it did before.</span></span>

<span data-ttu-id="bd5ac-187">**SQL Server 개체 탐색기**에서 **데이터 연결/SchoolContext**, **테이블**을 차례로 확장하면 Student 및 Instructor 테이블이 Person 테이블로 바뀐 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-187">In **SQL Server Object Explorer**, expand **Data Connections/SchoolContext** and then **Tables**, and you see that the Student and Instructor tables have been replaced by a Person table.</span></span> <span data-ttu-id="bd5ac-188">Person 테이블 디자이너를 열면 Student 및 Instructor 테이블에 있던 모든 열이 나타나는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-188">Open the Person table designer and you see that it has all of the columns that used to be in the Student and Instructor tables.</span></span>

![SSOX에서 Person 테이블](inheritance/_static/ssox-person-table.png)

<span data-ttu-id="bd5ac-190">Person 테이블을 마우스 오른쪽 단추로 클릭한 후 **테이블 데이터 표시**를 클릭하여 판별자 열을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-190">Right-click the Person table, and then click **Show Table Data** to see the discriminator column.</span></span>

![SSOX에서 Person 테이블 - 테이블 데이터](inheritance/_static/ssox-person-data.png)

## <a name="get-the-code"></a><span data-ttu-id="bd5ac-192">코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="bd5ac-192">Get the code</span></span>

[<span data-ttu-id="bd5ac-193">완성된 애플리케이션을 다운로드하거나 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-193">Download or view the completed application.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)

## <a name="additional-resources"></a><span data-ttu-id="bd5ac-194">추가 자료</span><span class="sxs-lookup"><span data-stu-id="bd5ac-194">Additional resources</span></span>

<span data-ttu-id="bd5ac-195">Entity Framework Core의 상속에 대한 자세한 내용은 [상속](/ef/core/modeling/inheritance)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-195">For more information about inheritance in Entity Framework Core, see [Inheritance](/ef/core/modeling/inheritance).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd5ac-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bd5ac-196">Next steps</span></span>

<span data-ttu-id="bd5ac-197">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-197">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bd5ac-198">데이터베이스에 상속 매핑</span><span class="sxs-lookup"><span data-stu-id="bd5ac-198">Mapped inheritance to database</span></span>
> * <span data-ttu-id="bd5ac-199">Person 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="bd5ac-199">Created the Person class</span></span>
> * <span data-ttu-id="bd5ac-200">강사 및 학생 업데이트</span><span class="sxs-lookup"><span data-stu-id="bd5ac-200">Updated Instructor and Student</span></span>
> * <span data-ttu-id="bd5ac-201">모델에 개인 추가</span><span class="sxs-lookup"><span data-stu-id="bd5ac-201">Added Person to the model</span></span>
> * <span data-ttu-id="bd5ac-202">마이그레이션 만들기 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="bd5ac-202">Created and update migrations</span></span>
> * <span data-ttu-id="bd5ac-203">구현 테스트</span><span class="sxs-lookup"><span data-stu-id="bd5ac-203">Tested the implementation</span></span>

<span data-ttu-id="bd5ac-204">다양한 고급 Entity Framework 시나리오를 처리하는 방법을 알아보려면 다음 문서로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5ac-204">Advance to the next article to learn how to handle a variety of relatively advanced Entity Framework scenarios.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="bd5ac-205">고급 항목</span><span class="sxs-lookup"><span data-stu-id="bd5ac-205">Advanced topics</span></span>](advanced.md)
