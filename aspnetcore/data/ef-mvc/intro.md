---
title: '자습서: ASP.NET MVC 웹앱에서 EF Core 시작'
description: 이는 Contoso University 샘플 애플리케이션을 처음부터 빌드하는 방법을 설명하는 일련의 자습서 중 첫 번째입니다.
author: rick-anderson
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/06/2019
ms.topic: tutorial
uid: data/ef-mvc/intro
ms.openlocfilehash: f7b557c8e560393ae886c46fad95c48ccbcc65b4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57043470"
---
# <a name="tutorial-get-started-with-ef-core-in-an-aspnet-mvc-web-app"></a><span data-ttu-id="47684-103">자습서: ASP.NET MVC 웹앱에서 EF Core 시작</span><span class="sxs-lookup"><span data-stu-id="47684-103">Tutorial: Get started with EF Core in an ASP.NET MVC web app</span></span>

[!INCLUDE [RP better than MVC](~/includes/RP-EF/rp-over-mvc.md)]

<span data-ttu-id="47684-104">Contoso University 샘플 웹 애플리케이션은 EF(Entity Framework) Core 2.0 및 Visual Studio 2017을 사용하여 ASP.NET Core 2.2 MVC 웹 애플리케이션을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="47684-104">The Contoso University sample web application demonstrates how to create ASP.NET Core 2.2 MVC web applications using Entity Framework (EF) Core 2.0 and Visual Studio 2017.</span></span>

<span data-ttu-id="47684-105">샘플 애플리케이션은 가상 Contoso University의 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="47684-105">The sample application is a web site for a fictional Contoso University.</span></span> <span data-ttu-id="47684-106">학생 입학, 강좌 개설 및 강사 할당과 같은 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-106">It includes functionality such as student admission, course creation, and instructor assignments.</span></span> <span data-ttu-id="47684-107">이는 Contoso University 샘플 애플리케이션을 처음부터 빌드하는 방법을 설명하는 일련의 자습서 중 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="47684-107">This is the first in a series of tutorials that explain how to build the Contoso University sample application from scratch.</span></span>

<span data-ttu-id="47684-108">EF Core 2.0은 최신 버전의 EF이지만 EF 6.x의 모든 기능을 가지고 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-108">EF Core 2.0 is the latest version of EF but doesn't yet have all the features of EF 6.x.</span></span> <span data-ttu-id="47684-109">EF 6.x 및 EF Core 중에 선택하는 방법에 대한 내용은 [EF Core와  EF6.x 비교](/ef/efcore-and-ef6/)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-109">For information about how to choose between EF 6.x and EF Core, see [EF Core vs. EF6.x](/ef/efcore-and-ef6/).</span></span> <span data-ttu-id="47684-110">EF 6.x를 선택하는 경우 [이 자습서 시리즈의 이전 버전](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47684-110">If you choose EF 6.x, see [the previous version of this tutorial series](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

> [!NOTE]
> <span data-ttu-id="47684-111">이 자습서의 ASP.NET Core 1.1 버전의 경우 [PDF 형식에서 이 자습서의 VS 2017 업데이트 2 버전](https://webpifeed.blob.core.windows.net/webpifeed/Partners/efmvc1.1.pdf)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47684-111">For the ASP.NET Core 1.1 version of this tutorial, see the [VS 2017 Update 2 version of this tutorial in PDF format](https://webpifeed.blob.core.windows.net/webpifeed/Partners/efmvc1.1.pdf).</span></span>

<span data-ttu-id="47684-112">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-112">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="47684-113">ASP.NET Core MVC 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="47684-113">Create ASP.NET Core MVC web app</span></span>
> * <span data-ttu-id="47684-114">사이트 스타일 설정</span><span class="sxs-lookup"><span data-stu-id="47684-114">Set up the site style</span></span>
> * <span data-ttu-id="47684-115">EF Core NuGet 패키지에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="47684-115">Learn about EF Core NuGet packages</span></span>
> * <span data-ttu-id="47684-116">데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="47684-116">Create the data model</span></span>
> * <span data-ttu-id="47684-117">데이터베이스 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="47684-117">Create the database context</span></span>
> * <span data-ttu-id="47684-118">SchoolContext 등록</span><span class="sxs-lookup"><span data-stu-id="47684-118">Register the SchoolContext</span></span>
> * <span data-ttu-id="47684-119">테스트 데이터로 DB 초기화</span><span class="sxs-lookup"><span data-stu-id="47684-119">Initialize DB with test data</span></span>
> * <span data-ttu-id="47684-120">컨트롤러 및 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="47684-120">Create controller and views</span></span>
> * <span data-ttu-id="47684-121">데이터베이스 보기</span><span class="sxs-lookup"><span data-stu-id="47684-121">View the database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47684-122">전제 조건</span><span class="sxs-lookup"><span data-stu-id="47684-122">Prerequisites</span></span>

[!INCLUDE [](~/includes/net-core-prereqs.md)]

## <a name="troubleshooting"></a><span data-ttu-id="47684-123">문제 해결</span><span class="sxs-lookup"><span data-stu-id="47684-123">Troubleshooting</span></span>

<span data-ttu-id="47684-124">해결할 수 없는 문제가 발생한 경우 일반적으로 [완료된 프로젝트](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)와 코드를 비교하여 해결책을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-124">If you run into a problem you can't resolve, you can generally find the solution by comparing your code to the [completed project](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final).</span></span> <span data-ttu-id="47684-125">일반적인 오류 목록 및 해결 방법은 [시리즈에서 마지막 자습서의 문제 해결 섹션](advanced.md#common-errors)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47684-125">For a list of common errors and how to solve them, see [the Troubleshooting section of the last tutorial in the series](advanced.md#common-errors).</span></span> <span data-ttu-id="47684-126">필요한 내용을 찾지 못한 경우 질문을 [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) 또는 [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core)에 대한 StackOverflow.com에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-126">If you don't find what you need there, you can post a question to StackOverflow.com for [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) or [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core).</span></span>

> [!TIP]
> <span data-ttu-id="47684-127">10 자습서의 시리즈이며, 각각은 이전 자습서에서 수행된 작업을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-127">This is a series of 10 tutorials, each of which builds on what is done in earlier tutorials.</span></span> <span data-ttu-id="47684-128">각 자습서를 성공적으로 완료한 후에 프로젝트 복사본의 저장을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-128">Consider saving a copy of the project after each successful tutorial completion.</span></span> <span data-ttu-id="47684-129">그런 다음, 문제가 발생한 경우 전체 시리즈의 처음으로 다시 이동하는 대신 이전 자습서부터 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-129">Then if you run into problems, you can start over from the previous tutorial instead of going back to the beginning of the whole series.</span></span>

## <a name="contoso-university-web-app"></a><span data-ttu-id="47684-130">Contoso University 웹앱</span><span class="sxs-lookup"><span data-stu-id="47684-130">Contoso University web app</span></span>

<span data-ttu-id="47684-131">이 자습서에서 빌드하는 애플리케이션은 간단한 대학 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="47684-131">The application you'll be building in these tutorials is a simple university web site.</span></span>

<span data-ttu-id="47684-132">사용자는 학생, 강좌 및 강사 정보를 보고 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-132">Users can view and update student, course, and instructor information.</span></span> <span data-ttu-id="47684-133">다음은 만들 몇 가지 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="47684-133">Here are a few of the screens you'll create.</span></span>

![학생 인덱스 페이지](intro/_static/students-index.png)

![학생 편집 페이지](intro/_static/student-edit.png)

<span data-ttu-id="47684-136">자습서가 Entity Framework를 사용하는 방법에 주로 초점을 맞출 수 있도록 이 사이트의 UI 스타일은 기본 제공 템플릿에서 생성된 내용에 가깝게 유지되었습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-136">The UI style of this site has been kept close to what's generated by the built-in templates, so that the tutorial can focus mainly on how to use the Entity Framework.</span></span>

## <a name="create-aspnet-core-mvc-web-app"></a><span data-ttu-id="47684-137">ASP.NET Core MVC 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="47684-137">Create ASP.NET Core MVC web app</span></span>

<span data-ttu-id="47684-138">Visual Studio를 열고 "ContosoUniversity"라는 새로운 ASP.NET Core C# 웹 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47684-138">Open Visual Studio and create a new ASP.NET Core C# web project named "ContosoUniversity".</span></span>

* <span data-ttu-id="47684-139">**파일** 메뉴에서 **새로 만들기 > 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-139">From the **File** menu, select **New > Project**.</span></span>

* <span data-ttu-id="47684-140">왼쪽 창에서 **설치됨 > Visual C# > 웹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-140">From the left pane, select **Installed > Visual C# > Web**.</span></span>

* <span data-ttu-id="47684-141">**ASP.NET Core 웹 애플리케이션** 프로젝트 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-141">Select the **ASP.NET Core Web Application** project template.</span></span>

* <span data-ttu-id="47684-142">이름으로 **ContosoUniversity**를 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-142">Enter **ContosoUniversity** as the name and click **OK**.</span></span>

  ![새 프로젝트 대화 상자](intro/_static/new-project2.png)

* <span data-ttu-id="47684-144">**새 ASP.NET Core 웹 애플리케이션(.NET Core)** 대화 상자가 표시될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="47684-144">Wait for the **New ASP.NET Core Web Application (.NET Core)** dialog to appear</span></span>

  ![새 ASP.NET Core 프로젝트 대화 상자](intro/_static/new-aspnet2.png)

* <span data-ttu-id="47684-146">**ASP.NET Core 2.2** 및 **웹 애플리케이션(Model-View-Controller)** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-146">Select **ASP.NET Core 2.2** and the **Web Application (Model-View-Controller)** template.</span></span>

  <span data-ttu-id="47684-147">**참고:** 이 자습서에는 ASP.NET Core 2.2 및 EF Core 2.0 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-147">**Note:** This tutorial requires ASP.NET Core 2.2 and EF Core 2.0 or later.</span></span>

* <span data-ttu-id="47684-148">**인증**이 **인증 없음**으로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-148">Make sure **Authentication** is set to **No Authentication**.</span></span>

* <span data-ttu-id="47684-149"> *\*확인*\*을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-149">Click **OK**</span></span>

## <a name="set-up-the-site-style"></a><span data-ttu-id="47684-150">사이트 스타일 설정</span><span class="sxs-lookup"><span data-stu-id="47684-150">Set up the site style</span></span>

<span data-ttu-id="47684-151">몇 가지 간단한 변경 내용으로 사이트 메뉴, 레이아웃 및 홈 페이지를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-151">A few simple changes will set up the site menu, layout, and home page.</span></span>

<span data-ttu-id="47684-152">*Views/Shared/_Layout.cshtml*을 열고 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-152">Open *Views/Shared/_Layout.cshtml* and make the following changes:</span></span>

* <span data-ttu-id="47684-153">모든 “ContosoUniversity”를 “Contoso University”로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-153">Change each occurrence of "ContosoUniversity" to "Contoso University".</span></span> <span data-ttu-id="47684-154">세 번 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="47684-154">There are three occurrences.</span></span>

* <span data-ttu-id="47684-155">**정보**, **학생**, **강좌**, **강사** 및 **부서** 메뉴 항목을 추가하고 **개인 정보** 메뉴 항목을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-155">Add menu entries for **About**, **Students**, **Courses**, **Instructors**, and **Departments**, and delete the **Privacy** menu entry.</span></span>

<span data-ttu-id="47684-156">변경 내용은 강조 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-156">The changes are highlighted.</span></span>

[!code-cshtml[](intro/samples/cu/Views/Shared/_Layout.cshtml?highlight=6,32-36,51)]

<span data-ttu-id="47684-157">*Views/Home/Index.cshtml*에서 다음 코드로 파일의 콘텐츠를 텍스트를 대체하여 ASP.NET 및 MVC에 대한 텍스트를 이 애플리케이션에 대한 텍스트로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="47684-157">In *Views/Home/Index.cshtml*, replace the contents of the file with the following code to replace the text about ASP.NET and MVC with text about this application:</span></span>

[!code-cshtml[](intro/samples/cu/Views/Home/Index.cshtml)]

<span data-ttu-id="47684-158">CTRL+F5 키를 눌러 프로젝트를 실행하거나 메뉴 모음에서 **디버그 > 디버깅하지 않고 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-158">Press CTRL+F5 to run the project or choose **Debug > Start Without Debugging** from the menu.</span></span> <span data-ttu-id="47684-159">이 자습서에서 만드는 페이지에 대한 탭이 포함된 홈페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="47684-159">You see the home page with tabs for the pages you'll create in these tutorials.</span></span>

![Contoso University 홈페이지](intro/_static/home-page.png)

## <a name="about-ef-core-nuget-packages"></a><span data-ttu-id="47684-161">EF Core NuGet 패키지 정보</span><span class="sxs-lookup"><span data-stu-id="47684-161">About EF Core NuGet packages</span></span>

<span data-ttu-id="47684-162">프로젝트에 EF Core 지원을 추가하려면 대상으로 지정하려는 데이터베이스 공급자를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-162">To add EF Core support to a project, install the database provider that you want to target.</span></span> <span data-ttu-id="47684-163">이 자습서에서는 SQL Server를 사용하며 공급자 패키지는 [Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/)입니다.</span><span class="sxs-lookup"><span data-stu-id="47684-163">This tutorial uses SQL Server, and the provider package is [Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/).</span></span> <span data-ttu-id="47684-164">이 패키지는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에 포함되어 있으므로 앱에 `Microsoft.AspNetCore.App` 패키지에 대한 패키지 참조가 있는 경우 패키지를 참조할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-164">This package is included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app), so you don't need to reference the package if your app has a package reference for the `Microsoft.AspNetCore.App` package.</span></span>

<span data-ttu-id="47684-165">이 패키지 및 해당 종속성(`Microsoft.EntityFrameworkCore` 및 `Microsoft.EntityFrameworkCore.Relational`)은 EF에 대한 런타임 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-165">This package and its dependencies (`Microsoft.EntityFrameworkCore` and `Microsoft.EntityFrameworkCore.Relational`) provide runtime support for EF.</span></span> <span data-ttu-id="47684-166">[마이그레이션](migrations.md) 자습서에서 나중에 도구 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-166">You'll add a tooling package later, in the [Migrations](migrations.md) tutorial.</span></span>

<span data-ttu-id="47684-167">Entity Framework Core에 사용할 수 있는 다른 데이터베이스 공급자에 대한 정보는 [데이터베이스 공급자](/ef/core/providers/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47684-167">For information about other database providers that are available for Entity Framework Core, see [Database providers](/ef/core/providers/).</span></span>

## <a name="create-the-data-model"></a><span data-ttu-id="47684-168">데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="47684-168">Create the data model</span></span>

<span data-ttu-id="47684-169">다음으로 Contoso University 애플리케이션에 대한 엔터티 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47684-169">Next you'll create entity classes for the Contoso University application.</span></span> <span data-ttu-id="47684-170">다음과 같은 세 가지 엔터티로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-170">You'll start with the following three entities.</span></span>

![강좌-등록-학생 데이터 모델 다이어그램](intro/_static/data-model-diagram.png)

<span data-ttu-id="47684-172">`Student` 및 `Enrollment` 엔터티 간에 일대다 관계가 있으며 `Course` 및 `Enrollment` 엔터티 간에 일대다 관계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-172">There's a one-to-many relationship between `Student` and `Enrollment` entities, and there's a one-to-many relationship between `Course` and `Enrollment` entities.</span></span> <span data-ttu-id="47684-173">즉, 학생은 개수에 관계 없이 강좌에 등록될 수 있으며 강좌는 등록된 학생이 여러 명일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-173">In other words, a student can be enrolled in any number of courses, and a course can have any number of students enrolled in it.</span></span>

<span data-ttu-id="47684-174">다음 섹션에서 이러한 엔터티 각각에 대한 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47684-174">In the following sections you'll create a class for each one of these entities.</span></span>

### <a name="the-student-entity"></a><span data-ttu-id="47684-175">학생 엔터티</span><span class="sxs-lookup"><span data-stu-id="47684-175">The Student entity</span></span>

![학생 엔터티 다이어그램](intro/_static/student-entity.png)

<span data-ttu-id="47684-177">*Models* 폴더에서 *Student.cs*라는 클래스 파일을 만들고 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="47684-177">In the *Models* folder, create a class file named *Student.cs* and replace the template code with the following code.</span></span>

[!code-csharp[](intro/samples/cu/Models/Student.cs?name=snippet_Intro)]

<span data-ttu-id="47684-178">`ID` 속성은 이 클래스에 해당하는 데이터베이스 테이블의 기본 키 열이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47684-178">The `ID` property will become the primary key column of the database table that corresponds to this class.</span></span> <span data-ttu-id="47684-179">기본적으로 Entity Framework는 `ID` 또는 `classnameID`로 명명된 속성을 기본 키로 해석합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-179">By default, the Entity Framework interprets a property that's named `ID` or `classnameID` as the primary key.</span></span>

<span data-ttu-id="47684-180">`Enrollments` 속성은 [탐색 속성](/ef/core/modeling/relationships)입니다.</span><span class="sxs-lookup"><span data-stu-id="47684-180">The `Enrollments` property is a [navigation property](/ef/core/modeling/relationships).</span></span> <span data-ttu-id="47684-181">탐색 속성은 이 엔터티와 관련된 다른 엔터티를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-181">Navigation properties hold other entities that are related to this entity.</span></span> <span data-ttu-id="47684-182">이 경우 `Student entity`의 `Enrollments` 속성은 해당 `Student` 엔터티에 관련된 모든 `Enrollment` 엔터티를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-182">In this case, the `Enrollments` property of a `Student entity` will hold all of the `Enrollment` entities that are related to that `Student` entity.</span></span> <span data-ttu-id="47684-183">즉, 데이터베이스의 지정된 학생 행에 두 개의 관련된 등록 행(해당 StudentID 외래 키 열에 해당 학생의 기본 키 값을 포함하는 행)이 있는 경우 해당 `Student` 엔터티의 `Enrollments` 탐색 속성은 두 개의 `Enrollment` 엔터티를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-183">In other words, if a given Student row in the database has two related Enrollment rows (rows that contain that student's primary key value in their StudentID foreign key column), that `Student` entity's `Enrollments` navigation property will contain those two `Enrollment` entities.</span></span>

<span data-ttu-id="47684-184">탐색 속성이 여러 엔터티를 포함할 수 있는 경우(다대다 또는 일대다 관계로), 해당 형식은 `ICollection<T>`와 같이 항목이 추가, 삭제 및 업데이트될 수 있는 목록이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-184">If a navigation property can hold multiple entities (as in many-to-many or one-to-many relationships), its type must be a list in which entries can be added, deleted, and updated, such as `ICollection<T>`.</span></span> <span data-ttu-id="47684-185">`List<T>` 또는 `HashSet<T>`와 같은 형식 또는 `ICollection<T>`를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-185">You can specify `ICollection<T>` or a type such as `List<T>` or `HashSet<T>`.</span></span> <span data-ttu-id="47684-186">`ICollection<T>`를 지정하는 경우 EF는 기본적으로 `HashSet<T>` 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47684-186">If you specify `ICollection<T>`, EF creates a `HashSet<T>` collection by default.</span></span>

### <a name="the-enrollment-entity"></a><span data-ttu-id="47684-187">등록 엔터티</span><span class="sxs-lookup"><span data-stu-id="47684-187">The Enrollment entity</span></span>

![등록 엔터티 다이어그램](intro/_static/enrollment-entity.png)

<span data-ttu-id="47684-189">*Models* 폴더에서*Enrollment.cs*를 만들고 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="47684-189">In the *Models* folder, create *Enrollment.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Models/Enrollment.cs?name=snippet_Intro)]

<span data-ttu-id="47684-190">`EnrollmentID` 속성은 기본 키가 됩니다. 이 엔터티는 `Student` 엔터티에서 본 것과 같이 자체적으로 `ID` 대신 `classnameID` 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-190">The `EnrollmentID` property will be the primary key; this entity uses the `classnameID` pattern instead of `ID` by itself as you saw in the `Student` entity.</span></span> <span data-ttu-id="47684-191">일반적으로 하나의 패턴을 선택하고 이를 데이터 모델 전체에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-191">Ordinarily you would choose one pattern and use it throughout your data model.</span></span> <span data-ttu-id="47684-192">여기에서 변형은 패턴 중 하나를 사용할 수 있음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="47684-192">Here, the variation illustrates that you can use either pattern.</span></span> <span data-ttu-id="47684-193">[자습서의 뒷부분](inheritance.md)에서는 클래스 이름 없이 ID를 사용하여 더 손쉽게 데이터 모델에서 상속을 구현하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="47684-193">In a [later tutorial](inheritance.md), you'll see how using ID without classname makes it easier to implement inheritance in the data model.</span></span>

<span data-ttu-id="47684-194">`Grade` 속성은 `enum`입니다.</span><span class="sxs-lookup"><span data-stu-id="47684-194">The `Grade` property is an `enum`.</span></span> <span data-ttu-id="47684-195">`Grade` 형식 선언 뒤에 있는 물음표는 `Grade` 속성이 nullable이라는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="47684-195">The question mark after the `Grade` type declaration indicates that the `Grade` property is nullable.</span></span> <span data-ttu-id="47684-196">Null인 등급은 0 등급과는 다릅니다. Null은 알려지지 않거나 아직 등록되지 않은 등급을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-196">A grade that's null is different from a zero grade -- null means a grade isn't known or hasn't been assigned yet.</span></span>

<span data-ttu-id="47684-197">`StudentID` 속성은 외래 키로, 해당 탐색 속성은 `Student`입니다.</span><span class="sxs-lookup"><span data-stu-id="47684-197">The `StudentID` property is a foreign key, and the corresponding navigation property is `Student`.</span></span> <span data-ttu-id="47684-198">`Enrollment` 엔터티는 하나의 `Student` 엔터티와 연결되어 있으므로 속성은 단일 `Student` 엔터티만 포함할 수 있습니다(이전에 살펴본 여러 `Enrollment` 엔터티를 포함할 수 있는 `Student.Enrollments` 탐색 속성과 달리).</span><span class="sxs-lookup"><span data-stu-id="47684-198">An `Enrollment` entity is associated with one `Student` entity, so the property can only hold a single `Student` entity (unlike the `Student.Enrollments` navigation property you saw earlier, which can hold multiple `Enrollment` entities).</span></span>

<span data-ttu-id="47684-199">`CourseID` 속성은 외래 키로, 해당 탐색 속성은 `Course`입니다.</span><span class="sxs-lookup"><span data-stu-id="47684-199">The `CourseID` property is a foreign key, and the corresponding navigation property is `Course`.</span></span> <span data-ttu-id="47684-200">`Enrollment` 엔터티는 하나의 `Course` 엔터티와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="47684-200">An `Enrollment` entity is associated with one `Course` entity.</span></span>

<span data-ttu-id="47684-201">Entity Framework는 속성 이름이 `<navigation property name><primary key property name>`인 경우 외래 키 속성으로는 해석합니다(예: `Student` 엔터티의 기본 키가 `ID`이므로 `Student` 탐색 속성의 경우 `StudentID`).</span><span class="sxs-lookup"><span data-stu-id="47684-201">Entity Framework interprets a property as a foreign key property if it's named `<navigation property name><primary key property name>` (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="47684-202">외래 키 속성의 이름을 단순히 `<primary key property name>`으로 지정할 수 있습니다(예: `Course` 엔터티의 기본 키가 `CourseID`이므로 `CourseID`).</span><span class="sxs-lookup"><span data-stu-id="47684-202">Foreign key properties can also be named simply `<primary key property name>` (for example, `CourseID` since the `Course` entity's primary key is `CourseID`).</span></span>

### <a name="the-course-entity"></a><span data-ttu-id="47684-203">강좌 엔터티</span><span class="sxs-lookup"><span data-stu-id="47684-203">The Course entity</span></span>

![강좌 엔터티 다이어그램](intro/_static/course-entity.png)

<span data-ttu-id="47684-205">*Models* 폴더에서*Course.cs*를 만들고 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="47684-205">In the *Models* folder, create *Course.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Models/Course.cs?name=snippet_Intro)]

<span data-ttu-id="47684-206">`Enrollments` 속성은 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="47684-206">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="47684-207">`Course` 엔터티는 `Enrollment` 엔터티의 개수와 관련이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-207">A `Course` entity can be related to any number of `Enrollment` entities.</span></span>

<span data-ttu-id="47684-208">이 시리즈의 [이후의 자습서](complex-data-model.md)에서 `DatabaseGenerated` 특성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-208">We'll say more about the `DatabaseGenerated` attribute in a [later tutorial](complex-data-model.md) in this series.</span></span> <span data-ttu-id="47684-209">기본적으로 이 특성을 통해 생성하는 데이터베이스를 갖는 대신 강좌에 대한 기본 키를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-209">Basically, this attribute lets you enter the primary key for the course rather than having the database generate it.</span></span>

## <a name="create-the-database-context"></a><span data-ttu-id="47684-210">데이터베이스 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="47684-210">Create the database context</span></span>

<span data-ttu-id="47684-211">특정 데이터 모델에 맞게 Entity Framework 기능을 조정하는 주 클래스는 데이터베이스 컨텍스트 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="47684-211">The main class that coordinates Entity Framework functionality for a given data model is the database context class.</span></span> <span data-ttu-id="47684-212">`Microsoft.EntityFrameworkCore.DbContext` 클래스에서 파생시키는 방식으로 이 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47684-212">You create this class by deriving from the `Microsoft.EntityFrameworkCore.DbContext` class.</span></span> <span data-ttu-id="47684-213">코드에서 데이터 모델에 포함되는 엔터티를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-213">In your code you specify which entities are included in the data model.</span></span> <span data-ttu-id="47684-214">특정 Entity Framework 동작을 사용자 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-214">You can also customize certain Entity Framework behavior.</span></span> <span data-ttu-id="47684-215">이 프로젝트에서 클래스 이름은 `SchoolContext`로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="47684-215">In this project, the class is named `SchoolContext`.</span></span>

<span data-ttu-id="47684-216">프로젝트 폴더에서 *Data*라는 이름의 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47684-216">In the project folder, create a folder named *Data*.</span></span>

<span data-ttu-id="47684-217">*Data* 폴더에서 *SchoolContext.cs*라는 새로운 클래스 파일을 만들고 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="47684-217">In the *Data* folder create a new class file named *SchoolContext.cs*, and replace the template code with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Data/SchoolContext.cs?name=snippet_Intro)]

<span data-ttu-id="47684-218">이 코드는 각 엔터티 집합에 대한 `DbSet` 속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47684-218">This code creates a `DbSet` property for each entity set.</span></span> <span data-ttu-id="47684-219">Entity Framework 용어에서 엔터티 집합은 일반적으로 데이터베이스 테이블에 해당하고 엔터티는 테이블의 행에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-219">In Entity Framework terminology, an entity set typically corresponds to a database table, and an entity corresponds to a row in the table.</span></span>

<span data-ttu-id="47684-220">`DbSet<Enrollment>` 및 `DbSet<Course>` 문을 생략할 수 있으며 이는 동일하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-220">You could've omitted the `DbSet<Enrollment>` and `DbSet<Course>` statements and it would work the same.</span></span> <span data-ttu-id="47684-221">`Student` 엔터티는 `Enrollment` 엔터티를 참조하고 `Enrollment` 엔터티는 `Course` 엔터티를 참조하기 때문에 Entity Framework는 이를 암시적으로 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-221">The Entity Framework would include them implicitly because the `Student` entity references the `Enrollment` entity and the `Enrollment` entity references the `Course` entity.</span></span>

<span data-ttu-id="47684-222">데이터베이스가 만들어지면 EF는 `DbSet` 속성 이름과 동일한 이름을 갖는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47684-222">When the database is created, EF creates tables that have names the same as the `DbSet` property names.</span></span> <span data-ttu-id="47684-223">컬렉션에 대한 속성 이름은 일반적으로 복수형이지만(Student보다는 Students) 개발자는 테이블 이름을 복수화할지 여부에 대해 동의하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-223">Property names for collections are typically plural (Students rather than Student), but developers disagree about whether table names should be pluralized or not.</span></span> <span data-ttu-id="47684-224">이러한 자습서의 경우 DbContext에서 단수 테이블 이름을 지정하여 기본 동작을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-224">For these tutorials you'll override the default behavior by specifying singular table names in the DbContext.</span></span> <span data-ttu-id="47684-225">이렇게 하려면 마지막 DbSet 속성 뒤에 강조 표시된 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-225">To do that, add the following highlighted code after the last DbSet property.</span></span>

[!code-csharp[](intro/samples/cu/Data/SchoolContext.cs?name=snippet_TableNames&highlight=16-21)]

## <a name="register-the-schoolcontext"></a><span data-ttu-id="47684-226">SchoolContext 등록</span><span class="sxs-lookup"><span data-stu-id="47684-226">Register the SchoolContext</span></span>

<span data-ttu-id="47684-227">ASP.NET Core는 기본적으로 [종속성 주입](../../fundamentals/dependency-injection.md)을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-227">ASP.NET Core implements [dependency injection](../../fundamentals/dependency-injection.md) by default.</span></span> <span data-ttu-id="47684-228">서비스(예: EF 데이터베이스 컨텍스트)는 애플리케이션 시작 중에 종속성 주입에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="47684-228">Services (such as the EF database context) are registered with dependency injection during application startup.</span></span> <span data-ttu-id="47684-229">이러한 서비스(예: MVC 컨트롤러)가 필요한 구성 요소에는 생성자 매개 변수를 통해 이러한 서비스가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="47684-229">Components that require these services (such as MVC controllers) are provided these services via constructor parameters.</span></span> <span data-ttu-id="47684-230">이 자습서의 뒷부분에서 컨텍스트 인스턴스를 가져오는 컨트롤러 생성자 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-230">You'll see the controller constructor code that gets a context instance later in this tutorial.</span></span>

<span data-ttu-id="47684-231">`SchoolContext`를 서비스로 등록하려면 *Startup.cs*를 열고 강조 표시된 줄을 `ConfigureServices` 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-231">To register `SchoolContext` as a service, open *Startup.cs*, and add the highlighted lines to the `ConfigureServices` method.</span></span>

[!code-csharp[](intro/samples/cu/Startup.cs?name=snippet_SchoolContext&highlight=3-4)]

<span data-ttu-id="47684-232">`DbContextOptionsBuilder` 개체에서 메서드를 호출하여 연결 문자열의 이름을 컨텍스트에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-232">The name of the connection string is passed in to the context by calling a method on a `DbContextOptionsBuilder` object.</span></span> <span data-ttu-id="47684-233">로컬 개발의 경우 [ASP.NET Core 구성 시스템](xref:fundamentals/configuration/index)은 *appsettings.json* 파일에서 연결 문자열을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-233">For local development, the [ASP.NET Core configuration system](xref:fundamentals/configuration/index) reads the connection string from the *appsettings.json* file.</span></span>

<span data-ttu-id="47684-234">`ContosoUniversity.Data` 및 `Microsoft.EntityFrameworkCore` 네임스페이스에 대해 `using` 문을 추가한 다음, 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-234">Add `using` statements for `ContosoUniversity.Data` and `Microsoft.EntityFrameworkCore` namespaces, and then build the project.</span></span>

[!code-csharp[](intro/samples/cu/Startup.cs?name=snippet_Usings)]

<span data-ttu-id="47684-235">*appsettings.json* 파일을 열고 다음 예제에 표시된 대로 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-235">Open the *appsettings.json* file and add a connection string as shown in the following example.</span></span>

[!code-json[](./intro/samples/cu/appsettings1.json?highlight=2-4)]

### <a name="sql-server-express-localdb"></a><span data-ttu-id="47684-236">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="47684-236">SQL Server Express LocalDB</span></span>

<span data-ttu-id="47684-237">연결 문자열은 SQL Server LocalDB 데이터베이스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-237">The connection string specifies a SQL Server LocalDB database.</span></span> <span data-ttu-id="47684-238">LocalDB는 프로덕션 사용이 아닌 애플리케이션 개발용으로 고안된 SQL Server Express 데이터베이스 엔진의 경량 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="47684-238">LocalDB is a lightweight version of the SQL Server Express Database Engine and is intended for application development, not production use.</span></span> <span data-ttu-id="47684-239">LocalDB는 요청 시 시작하고 사용자 모드에서 실행되므로 복잡한 구성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-239">LocalDB starts on demand and runs in user mode, so there's no complex configuration.</span></span> <span data-ttu-id="47684-240">기본적으로 LocalDB는 *.mdf* 데이터베이스 파일을 `C:/Users/<user>` 디렉터리에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47684-240">By default, LocalDB creates *.mdf* database files in the `C:/Users/<user>` directory.</span></span>

## <a name="initialize-db-with-test-data"></a><span data-ttu-id="47684-241">테스트 데이터로 DB 초기화</span><span class="sxs-lookup"><span data-stu-id="47684-241">Initialize DB with test data</span></span>

<span data-ttu-id="47684-242">Entity Framework에서 빈 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47684-242">The Entity Framework will create an empty database for you.</span></span> <span data-ttu-id="47684-243">이 섹션에서는 테스트 데이터로 채우기 위해 데이터베이스를 만든 후 호출되는 메서드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-243">In this section, you write a method that's called after the database is created in order to populate it with test data.</span></span>

<span data-ttu-id="47684-244">여기에서 `EnsureCreated` 메서드를 사용하여 자동으로 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47684-244">Here you'll use the `EnsureCreated` method to automatically create the database.</span></span> <span data-ttu-id="47684-245">[이후의 자습서](migrations.md)에서는 데이터베이스를 삭제하고 다시 작성하는 대신 데이터베이스 스키마를 변경하도록 Code First 마이그레이션을 사용하여 모델 변경 내용을 처리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="47684-245">In a [later tutorial](migrations.md) you'll see how to handle model changes by using Code First Migrations to change the database schema instead of dropping and re-creating the database.</span></span>

<span data-ttu-id="47684-246">*Data* 폴더에서 *DbInitializer.cs*라는 새 클래스 파일을 만들고 템플릿 코드를 다음 코드로 바꿉니다. 이로 인해 필요할 때 데이터베이스가 만들어지며 테스트 데이터를 새 데이터베이스로 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-246">In the *Data* folder, create a new class file named *DbInitializer.cs* and replace the template code with the following code, which causes a database to be created when needed and loads test data into the new database.</span></span>

[!code-csharp[](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Intro)]

<span data-ttu-id="47684-247">코드는 데이터베이스에 학생이 있는지를 확인하고 없는 경우 데이터베이스가 새 것이며 테스트 데이터로 시드되어야 한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-247">The code checks if there are any students in the database, and if not, it assumes the database is new and needs to be seeded with test data.</span></span> <span data-ttu-id="47684-248">`List<T>` 컬렉션이 아닌 배열에 테스트 데이터를 로드하여 성능을 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-248">It loads test data into arrays rather than `List<T>` collections to optimize performance.</span></span>

<span data-ttu-id="47684-249">*Program.cs*에서 애플리케이션 시작 시에 다음을 수행하는 `Main` 메서드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-249">In *Program.cs*, modify the `Main` method to do the following on application startup:</span></span>

* <span data-ttu-id="47684-250">종속성 주입 컨테이너에서 데이터베이스 컨텍스트 인스턴스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="47684-250">Get a database context instance from the dependency injection container.</span></span>
* <span data-ttu-id="47684-251">컨텍스트를 전달하는 시드 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-251">Call the seed method, passing to it the context.</span></span>
* <span data-ttu-id="47684-252">시드 메서드가 완료되면 컨텍스트를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-252">Dispose the context when the seed method is done.</span></span>

[!code-csharp[](intro/samples/cu/Program.cs?name=snippet_Seed&highlight=3-20)]

<span data-ttu-id="47684-253">`using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-253">Add `using` statements:</span></span>

[!code-csharp[](intro/samples/cu/Program.cs?name=snippet_Usings)]

<span data-ttu-id="47684-254">이전 자습서에서는 *Startup.cs*의 `Configure` 메서드에서 유사한 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-254">In older tutorials, you may see similar code in the `Configure` method in *Startup.cs*.</span></span> <span data-ttu-id="47684-255">요청 파이프라인을 설정하는 데에만 `Configure` 메서드를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-255">We recommend that you use the `Configure` method only to set up the request pipeline.</span></span> <span data-ttu-id="47684-256">애플리케이션 시작 코드는 `Main` 메서드에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-256">Application startup code belongs in the `Main` method.</span></span>

<span data-ttu-id="47684-257">이제 애플리케이션을 처음으로 실행하면 데이터베이스가 생성되고 테스트 데이터로 시드됩니다.</span><span class="sxs-lookup"><span data-stu-id="47684-257">Now the first time you run the application, the database will be created and seeded with test data.</span></span> <span data-ttu-id="47684-258">데이터 모델을 변경할 때마다 데이터베이스를 삭제하고, 시드 메서드를 업데이트하고, 동일한 방식으로 새 데이터베이스를 사용하여 새로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-258">Whenever you change your data model, you can delete the database, update your seed method, and start afresh with a new database the same way.</span></span> <span data-ttu-id="47684-259">이후의 자습서에서는 데이터 모델이 변경될 때 데이터베이스를 삭제하고 다시 작성하지 않고 데이터베이스를 수정하는 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-259">In later tutorials, you'll see how to modify the database when the data model changes, without deleting and re-creating it.</span></span>

## <a name="create-controller-and-views"></a><span data-ttu-id="47684-260">컨트롤러 및 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="47684-260">Create controller and views</span></span>

<span data-ttu-id="47684-261">다음으로 Visual Studio에서 스캐폴딩 엔진을 사용하여 EF에서 데이터를 쿼리하고 저장하는 데 사용하는 MVC 컨트롤러 및 보기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-261">Next, you'll use the scaffolding engine in Visual Studio to add an MVC controller and views that will use EF to query and save data.</span></span>

<span data-ttu-id="47684-262">CRUD 작업 메서드와 보기를 자동으로 만드는 작업을 스캐폴딩이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-262">The automatic creation of CRUD action methods and views is known as scaffolding.</span></span> <span data-ttu-id="47684-263">스캐폴딩은 사용자 고유의 요구 사항에 맞게 수정할 수 있는 스캐폴드된 코드가 시작 지점인 코드 생성과 다릅니다. 반면에 일반적으로 생성된 코드를 수정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-263">Scaffolding differs from code generation in that the scaffolded code is a starting point that you can modify to suit your own requirements, whereas you typically don't modify generated code.</span></span> <span data-ttu-id="47684-264">생성된 코드를 사용자 지정해야 하는 경우 partial 클래스를 사용하거나 항목이 변경될 때 코드를 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-264">When you need to customize generated code, you use partial classes or you regenerate the code when things change.</span></span>

* <span data-ttu-id="47684-265">**솔루션 탐색기**에서 **컨트롤러** 폴더를 마우스 오른쪽 단추로 클릭하고 **추가 -> 스캐폴드 항목 새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-265">Right-click the **Controllers** folder in **Solution Explorer** and select **Add > New Scaffolded Item**.</span></span>

<span data-ttu-id="47684-266">**MVC 종속성 추가** 대화 상자가 나타나는 경우:</span><span class="sxs-lookup"><span data-stu-id="47684-266">If the **Add MVC Dependencies** dialog appears:</span></span>

* <span data-ttu-id="47684-267">[Visual Studio를 최신 버전으로 업데이트합니다](https://www.visualstudio.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span><span class="sxs-lookup"><span data-stu-id="47684-267">[Update Visual Studio to the latest version](https://www.visualstudio.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span> <span data-ttu-id="47684-268">Visual Studio 15.5 이전 버전이 이 대화 상자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-268">Visual Studio versions prior to 15.5 show this dialog.</span></span>
* <span data-ttu-id="47684-269">업데이트할 수 없는 경우 **추가**를 선택한 다음 컨트롤러 추가 단계를 다시 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="47684-269">If you can't update, select **ADD**, and then follow the add controller steps again.</span></span>

* <span data-ttu-id="47684-270">**스캐폴드 추가** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="47684-270">In the **Add Scaffold** dialog box:</span></span>

  * <span data-ttu-id="47684-271">**Entity Framework를 사용하며 뷰가 포함된 MVC 컨트롤러**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-271">Select **MVC controller with views, using Entity Framework**.</span></span>

  * <span data-ttu-id="47684-272">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-272">Click **Add**.</span></span> <span data-ttu-id="47684-273">**Entity Framework를 사용하여 뷰 포함 MVC 컨트롤러 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="47684-273">The **Add MVC Controller with views, using Entity Framework** dialog box appears.</span></span>

    ![학생 스캐폴드](intro/_static/scaffold-student2.png)

  * <span data-ttu-id="47684-275">**모델 클래스**에서 **학생**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-275">In **Model class** select **Student**.</span></span>

  * <span data-ttu-id="47684-276">**데이터 컨텍스트 클래스**에서 **SchoolContext**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-276">In **Data context class** select **SchoolContext**.</span></span>

  * <span data-ttu-id="47684-277">기본값 **StudentsController**를 이름으로 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-277">Accept the default **StudentsController** as the name.</span></span>

  * <span data-ttu-id="47684-278">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-278">Click **Add**.</span></span>

  <span data-ttu-id="47684-279">**추가**를 클릭하면 Visual Studio 스캐폴딩 엔진은 *StudentsController.cs* 파일과 컨트롤러와 작동하는 뷰 집합(*.cshtml* 파일)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47684-279">When you click **Add**, the Visual Studio scaffolding engine creates a *StudentsController.cs* file and a set of views (*.cshtml* files) that work with the controller.</span></span>

<span data-ttu-id="47684-280">(스캐폴딩 엔진은 이 자습서의 앞에서 수행한 것과 같이 수동으로 먼저 만들지 않은 경우 데이터베이스 컨텍스트를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-280">(The scaffolding engine can also create the database context for you if you don't create it manually first as you did earlier for this tutorial.</span></span> <span data-ttu-id="47684-281">**데이터 컨텍스트 클래스**의 오른쪽에 있는 더하기 기호를 클릭하여 **컨트롤러 추가** 상자에 새 컨텍스트 클래스를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-281">You can specify a new context class in the **Add Controller** box by clicking the plus sign to the right of **Data context class**.</span></span>  <span data-ttu-id="47684-282">그런 다음, Visual Studio는 `DbContext` 클래스 뿐만 아니라 컨트롤러와 뷰도 만듭니다.)</span><span class="sxs-lookup"><span data-stu-id="47684-282">Visual Studio will then create your `DbContext` class as well as the controller and views.)</span></span>

<span data-ttu-id="47684-283">컨트롤러는 `SchoolContext`를 생성자 매개 변수로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-283">You'll notice that the controller takes a `SchoolContext` as a constructor parameter.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_Context&highlight=5,7,9)]

<span data-ttu-id="47684-284">ASP.NET Core 종속성 주입은 `SchoolContext`의 인스턴스를 컨트롤러에 전달하는 것을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-284">ASP.NET Core dependency injection takes care of passing an instance of `SchoolContext` into the controller.</span></span> <span data-ttu-id="47684-285">이전에 *Startup.cs* 파일에서 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-285">You configured that in the *Startup.cs* file earlier.</span></span>

<span data-ttu-id="47684-286">컨트롤러는 데이터베이스에 모든 학생을 표시하는 `Index` 작업 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-286">The controller contains an `Index` action method, which displays all students in the database.</span></span> <span data-ttu-id="47684-287">메서드는 데이터베이스 컨텍스트 인스턴스의 `Students` 속성을 읽어 학생 엔터티 집합에서 학생의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="47684-287">The method gets a list of students from the Students entity set by reading the `Students` property of the database context instance:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_ScaffoldedIndex&highlight=3)]

<span data-ttu-id="47684-288">이 자습서의 뒷부분에 나오는 이 코드에서 비동기 프로그래밍 요소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="47684-288">You'll learn about the asynchronous programming elements in this code later in the tutorial.</span></span>

<span data-ttu-id="47684-289">*Views/Students/Index.cshtml* 보기가 테이블에 이 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-289">The *Views/Students/Index.cshtml* view displays this list in a table:</span></span>

[!code-cshtml[](intro/samples/cu/Views/Students/Index1.cshtml)]

<span data-ttu-id="47684-290">CTRL+F5 키를 눌러 프로젝트를 실행하거나 메뉴 모음에서 **디버그 > 디버깅하지 않고 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-290">Press CTRL+F5 to run the project or choose **Debug > Start Without Debugging** from the menu.</span></span>

<span data-ttu-id="47684-291">학생 탭을 클릭하여 `DbInitializer.Initialize` 메서드가 삽입된 테스트 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="47684-291">Click the Students tab to see the test data that the `DbInitializer.Initialize` method inserted.</span></span> <span data-ttu-id="47684-292">브라우저 창의 폭에 따라 페이지의 맨 위에 `Student` 탭 링크가 표시되거나 링크를 보기 위해 오른쪽 맨 위의 탐색 아이콘을 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-292">Depending on how narrow your browser window is, you'll see the `Student` tab link at the top of the page or you'll have to click the navigation icon in the upper right corner to see the link.</span></span>

![좁은 Contoso University 홈페이지](intro/_static/home-page-narrow.png)

![학생 인덱스 페이지](intro/_static/students-index.png)

## <a name="view-the-database"></a><span data-ttu-id="47684-295">데이터베이스 보기</span><span class="sxs-lookup"><span data-stu-id="47684-295">View the database</span></span>

<span data-ttu-id="47684-296">애플리케이션을 시작했을 때 `DbInitializer.Initialize` 메서드는 `EnsureCreated`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-296">When you started the application, the `DbInitializer.Initialize` method calls `EnsureCreated`.</span></span> <span data-ttu-id="47684-297">EF는 데이터베이스가 없는 것을 확인하고 하나를 만들었습니다. 그런 다음, `Initialize` 메서드 코드의 나머지 부분은 데이터베이스를 데이터로 채웠습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-297">EF saw that there was no database and so it created one, then the remainder of the `Initialize` method code populated the database with data.</span></span> <span data-ttu-id="47684-298">**SQL Server 개체 탐색기**(SSOX)를 사용하여 Visual Studio에서 데이터베이스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-298">You can use **SQL Server Object Explorer** (SSOX) to view the database in Visual Studio.</span></span>

<span data-ttu-id="47684-299">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-299">Close the browser.</span></span>

<span data-ttu-id="47684-300">SSOX 창이 열려 있지 않은 경우 Visual Studio의 **보기** 메뉴에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-300">If the SSOX window isn't already open, select it from the **View** menu in Visual Studio.</span></span>

<span data-ttu-id="47684-301">SSOX에서 **(localdb) \MSSQLLocalDB > 데이터베이스**를 클릭한 다음, *appsettings.json* 파일의 연결 문자열에 있는 데이터베이스 이름에 대한 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-301">In SSOX, click **(localdb)\MSSQLLocalDB > Databases**, and then click the entry for the database name that's in the connection string in your *appsettings.json* file.</span></span>

<span data-ttu-id="47684-302">**테이블** 노드를 확장하여 데이터베이스의 테이블을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="47684-302">Expand the **Tables** node to see the tables in your database.</span></span>

![SSOX의 테이블](intro/_static/ssox-tables.png)

<span data-ttu-id="47684-304">**학생** 테이블을 마우스 오른쪽 단추로 클릭하고, **데이터 보기**를 클릭하여 만들어진 열 및 테이블에 삽입된 행을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="47684-304">Right-click the **Student** table and click **View Data** to see the columns that were created and the rows that were inserted into the table.</span></span>

![SSOX의 학생 테이블](intro/_static/ssox-student-table.png)

<span data-ttu-id="47684-306"><em>.mdf</em> 및 <em>.ldf</em> 데이터베이스 파일은 <em>C:\Users\\<yourusername></em> 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-306">The <em>.mdf</em> and <em>.ldf</em> database files are in the <em>C:\Users\\<yourusername></em> folder.</span></span>

<span data-ttu-id="47684-307">앱 시작 시 실행되는 이니셜라이저 메서드에서 `EnsureCreated`를 호출하기 때문에 이제 `Student` 클래스에 변경 내용을 만들고, 데이터베이스를 삭제하고, 애플리케이션을 다시 시작할 수 있으며, 데이터베이스는 변경 내용에 맞도록 자동으로 다시 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="47684-307">Because you're calling `EnsureCreated` in the initializer method that runs on app start, you could now make a change to the `Student` class, delete the database, run the application again, and the database would automatically be re-created to match your change.</span></span> <span data-ttu-id="47684-308">예를 들어 `EmailAddress` 속성을 `Student` 클래스에 추가하는 경우 다시 만들어진 테이블에 새 `EmailAddress` 열이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="47684-308">For example, if you add an `EmailAddress` property to the `Student` class, you'll see a new `EmailAddress` column in the re-created table.</span></span>

## <a name="conventions"></a><span data-ttu-id="47684-309">규칙</span><span class="sxs-lookup"><span data-stu-id="47684-309">Conventions</span></span>

<span data-ttu-id="47684-310">Entity Framework에서 전체 데이터베이스를 만들 수 있도록 작성해야 했던 코드의 양은 규칙의 사용 또는 Entity Framework에서 만드는 가정으로 인해 최소입니다.</span><span class="sxs-lookup"><span data-stu-id="47684-310">The amount of code you had to write in order for the Entity Framework to be able to create a complete database for you is minimal because of the use of conventions, or assumptions that the Entity Framework makes.</span></span>

* <span data-ttu-id="47684-311">`DbSet` 속성의 이름은 테이블 이름으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="47684-311">The names of `DbSet` properties are used as table names.</span></span> <span data-ttu-id="47684-312">`DbSet` 속성에서 참조하지 않는 엔터티의 경우 엔터티 클래스 이름이 테이블 이름으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="47684-312">For entities not referenced by a `DbSet` property, entity class names are used as table names.</span></span>

* <span data-ttu-id="47684-313">엔터티 속성 이름은 열 이름에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="47684-313">Entity property names are used for column names.</span></span>

* <span data-ttu-id="47684-314">ID 또는 classnameID로 명명된 엔터티 속성은 기본 키 속성으로 인식됩니다.</span><span class="sxs-lookup"><span data-stu-id="47684-314">Entity properties that are named ID or classnameID are recognized as primary key properties.</span></span>

* <span data-ttu-id="47684-315">속성 이름이 *<navigation property name><primary key property name>* 인 경우 외래 키 속성으로는 해석됩니다(예: `Student` 엔터티의 기본 키가 `ID`이므로 `Student` 탐색 속성의 경우 `StudentID`).</span><span class="sxs-lookup"><span data-stu-id="47684-315">A property is interpreted as a foreign key property if it's named *<navigation property name><primary key property name>* (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="47684-316">외래 키 속성의 이름을 단순히 *<primary key property name>* 으로 지정할 수 있습니다(예: `Enrollment` 엔터티의 기본 키가 `EnrollmentID`이므로 `EnrollmentID`).</span><span class="sxs-lookup"><span data-stu-id="47684-316">Foreign key properties can also be named simply *<primary key property name>* (for example, `EnrollmentID` since the `Enrollment` entity's primary key is `EnrollmentID`).</span></span>

<span data-ttu-id="47684-317">기본 동작은 재정의될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-317">Conventional behavior can be overridden.</span></span> <span data-ttu-id="47684-318">예를 들어 이 자습서의 앞부분에서 본 것처럼 테이블 이름을 명시적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-318">For example, you can explicitly specify table names, as you saw earlier in this tutorial.</span></span> <span data-ttu-id="47684-319">또한 이 시리즈의 [이후의 자습서](complex-data-model.md)에서 볼 수 있듯이 열 이름을 설정하고 기본 키 또는 외래 키로 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-319">And you can set column names and set any property as primary key or foreign key, as you'll see in a [later tutorial](complex-data-model.md) in this series.</span></span>

## <a name="asynchronous-code"></a><span data-ttu-id="47684-320">비동기 코드</span><span class="sxs-lookup"><span data-stu-id="47684-320">Asynchronous code</span></span>

<span data-ttu-id="47684-321">비동기 프로그래밍은 ASP.NET Core 및 EF Core에 대한 기본 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="47684-321">Asynchronous programming is the default mode for ASP.NET Core and EF Core.</span></span>

<span data-ttu-id="47684-322">웹 서버에는 사용할 수 있는 스레드 수가 제한적이며, 로드 양이 많은 상황에서는 사용 가능한 모든 스레드가 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-322">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="47684-323">이 경우 서버는 스레드가 해제될 때까지 새 요청을 처리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-323">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="47684-324">동기 코드를 사용하면 I/O 완료를 대기하느라 작업을 실제로 수행하지 않는 동안에 많은 스레드가 정체될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-324">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="47684-325">비동기 코드를 사용하면 프로세스가 I/O 완료를 대기할 때 다른 요청을 처리하는 데 사용하도록 해당 스레드가 서버에서 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="47684-325">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="47684-326">따라서 비동기 코드를 사용하면 서버 리소스를 더 효율적으로 사용할 수 있으며 서버가 지연 없이 더 많은 트래픽을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-326">As a result, asynchronous code enables server resources to be used more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="47684-327">비동기 코드는 런타임 시 약간의 오버헤드를 도입하지만 트래픽이 높은 상황에서는 잠재적 성능 향상이 상당한 반면, 트래픽이 낮은 상황의 경우 성능 저하는 미미합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-327">Asynchronous code does introduce a small amount of overhead at run time, but for low traffic situations the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="47684-328">다음 코드에서 `async` 키워드, `Task<T>` 반환 값, `await` 키워드 및 `ToListAsync` 메서드는 비동기적으로 코드 실행을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-328">In the following code, the `async` keyword, `Task<T>` return value, `await` keyword, and `ToListAsync` method make the code execute asynchronously.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_ScaffoldedIndex)]

* <span data-ttu-id="47684-329">`async` 키워드는 컴파일러에서 메서드 본문의 부분에 대한 콜백을 생성하고 반환되는 `Task<IActionResult>` 개체를 자동으로 만들도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-329">The `async` keyword tells the compiler to generate callbacks for parts of the method body and to automatically create the `Task<IActionResult>` object that's returned.</span></span>

* <span data-ttu-id="47684-330">반환 형식 `Task<IActionResult>`는 `IActionResult` 형식의 결과와 함께 진행 중인 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="47684-330">The return type `Task<IActionResult>` represents ongoing work with a result of type `IActionResult`.</span></span>

* <span data-ttu-id="47684-331">`await` 키워드로 인해 컴파일러는 메서드를 두 부분으로 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-331">The `await` keyword causes the compiler to split the method into two parts.</span></span> <span data-ttu-id="47684-332">첫 번째 부분은 비동기적으로 시작되는 작업을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-332">The first part ends with the operation that's started asynchronously.</span></span> <span data-ttu-id="47684-333">두 번째 부분은 작업이 완료될 때 호출되는 콜백 메서드에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="47684-333">The second part is put into a callback method that's called when the operation completes.</span></span>

* <span data-ttu-id="47684-334">`ToListAsync`는 `ToList` 확장 메서드의 비동기 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="47684-334">`ToListAsync` is the asynchronous version of the `ToList` extension method.</span></span>

<span data-ttu-id="47684-335">Entity Framework를 사용하는 비동기 코드를 작성할 때 고려해야 할 몇 가지 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-335">Some things to be aware of when you are writing asynchronous code that uses the Entity Framework:</span></span>

* <span data-ttu-id="47684-336">쿼리 또는 명령을 데이터베이스에 보내는 명령문만 비동기적으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="47684-336">Only statements that cause queries or commands to be sent to the database are executed asynchronously.</span></span> <span data-ttu-id="47684-337">예를 들어 `ToListAsync`, `SingleOrDefaultAsync` 및 `SaveChangesAsync`를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-337">That includes, for example, `ToListAsync`, `SingleOrDefaultAsync`, and `SaveChangesAsync`.</span></span> <span data-ttu-id="47684-338">예를 들어 `var students = context.Students.Where(s => s.LastName == "Davolio")`와 같은 `IQueryable`을 변경하는 명령문은 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-338">It doesn't include, for example, statements that just change an `IQueryable`, such as `var students = context.Students.Where(s => s.LastName == "Davolio")`.</span></span>

* <span data-ttu-id="47684-339">EF 컨텍스트는 스레드로부터 안전하지 않습니다. 동시에 여러 작업을 수행하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="47684-339">An EF context isn't thread safe: don't try to do multiple operations in parallel.</span></span> <span data-ttu-id="47684-340">비동기 EF 메서드를 호출하는 경우 항상 `await` 키워드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-340">When you call any async EF method, always use the `await` keyword.</span></span>

* <span data-ttu-id="47684-341">비동기 코드의 성능 이점을 활용하려는 경우 사용 중인(예: 페이징) 라이브러리 패키지 또한 쿼리를 데이터베이스에 전송하도록 하는 Entity Framework 메서드를 호출하는 경우 비동기를 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-341">If you want to take advantage of the performance benefits of async code, make sure that any library packages that you're using (such as for paging), also use async if they call any Entity Framework methods that cause queries to be sent to the database.</span></span>

<span data-ttu-id="47684-342">.NET에서의 비동기 프로그래밍에 대한 자세한 내용은 [비동기 개요](/dotnet/articles/standard/async)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47684-342">For more information about asynchronous programming in .NET, see [Async Overview](/dotnet/articles/standard/async).</span></span>

## <a name="get-the-code"></a><span data-ttu-id="47684-343">코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="47684-343">Get the code</span></span>

[<span data-ttu-id="47684-344">완성된 애플리케이션을 다운로드하거나 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-344">Download or view the completed application.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)

## <a name="next-steps"></a><span data-ttu-id="47684-345">다음 단계</span><span class="sxs-lookup"><span data-stu-id="47684-345">Next steps</span></span>

<span data-ttu-id="47684-346">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="47684-346">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="47684-347">ASP.NET Core MVC 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="47684-347">Created ASP.NET Core MVC web app</span></span>
> * <span data-ttu-id="47684-348">사이트 스타일 설정</span><span class="sxs-lookup"><span data-stu-id="47684-348">Set up the site style</span></span>
> * <span data-ttu-id="47684-349">EF Core NuGet 패키지에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="47684-349">Learned about EF Core NuGet packages</span></span>
> * <span data-ttu-id="47684-350">데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="47684-350">Created the data model</span></span>
> * <span data-ttu-id="47684-351">데이터베이스 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="47684-351">Created the database context</span></span>
> * <span data-ttu-id="47684-352">SchoolContext 등록</span><span class="sxs-lookup"><span data-stu-id="47684-352">Registered the SchoolContext</span></span>
> * <span data-ttu-id="47684-353">테스트 데이터로 DB 초기화</span><span class="sxs-lookup"><span data-stu-id="47684-353">Initialized DB with test data</span></span>
> * <span data-ttu-id="47684-354">컨트롤러 및 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="47684-354">Created controller and views</span></span>
> * <span data-ttu-id="47684-355">데이터베이스 보기</span><span class="sxs-lookup"><span data-stu-id="47684-355">Viewed the database</span></span>

<span data-ttu-id="47684-356">다음 자습서에서는 기본 CRUD(만들기, 읽기, 업데이트, 삭제) 작업을 수행하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="47684-356">In the following tutorial, you'll learn how to perform basic CRUD (create, read, update, delete) operations.</span></span>

<span data-ttu-id="47684-357">기본 CRUD(만들기, 읽기, 업데이트, 삭제) 작업을 수행하는 방법을 알아보려면 다음 문서로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="47684-357">Advance to the next article to learn how to perform basic CRUD (create, read, update, delete) operations.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="47684-358">기본 CRUD 기능 구현</span><span class="sxs-lookup"><span data-stu-id="47684-358">Implement basic CRUD functionality</span></span>](crud.md)
