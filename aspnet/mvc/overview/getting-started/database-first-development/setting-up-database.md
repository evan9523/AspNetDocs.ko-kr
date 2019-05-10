---
uid: mvc/overview/getting-started/database-first-development/setting-up-database
title: '자습서: EF Database first MVC 5를 사용 하 여 시작'
description: 이 자습서에는 기존 데이터베이스 및 신속 하 게 데이터와 상호 작용할 수 있도록 하는 웹 응용 프로그램을 만들기 시작 하는 방법을 보여 줍니다.
author: Rick-Anderson
ms.author: riande
ms.date: 01/15/2019
ms.topic: tutorial
ms.assetid: 095abad4-3bfe-4f06-b092-ae6a735b7e49
msc.legacyurl: /mvc/overview/getting-started/database-first-development/setting-up-database
msc.type: authoredcontent
ms.openlocfilehash: a760767839a834a9c7e9fe358a3fd806a833261f
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65121172"
---
# <a name="tutorial-get-started-with-ef-database-first-using-mvc-5"></a><span data-ttu-id="8c8cc-103">자습서: EF Database first MVC 5를 사용 하 여 시작</span><span class="sxs-lookup"><span data-stu-id="8c8cc-103">Tutorial: Get started with EF Database First using MVC 5</span></span>

<span data-ttu-id="8c8cc-104">MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="8c8cc-105">이 자습서 시리즈에서는 자동으로 표시, 편집, 만들기, 사용자를 사용 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="8c8cc-106">생성된 된 코드는 데이터베이스 테이블의 열에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-106">The generated code corresponds to the columns in the database table.</span></span> <span data-ttu-id="8c8cc-107">배웁니다 시리즈의 마지막 부분에서는 데이터 주석 유효성 검사 요구 사항을 지정 하 여 서식 지정을 표시 하는 데이터 모델에 추가 하려면 어떻게 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-107">In the last part of the series, you learn how add data annotations to the data model to specify validation requirements and display formatting.</span></span> <span data-ttu-id="8c8cc-108">완료 되 면 Azure App Service에.NET 앱 및 SQL database를 배포 하는 방법을 알아보려면 Azure 문서에 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-108">When you're done, you can advance to an Azure article to learn how to deploy a .NET app and SQL database to Azure App Service.</span></span>

<span data-ttu-id="8c8cc-109">이 자습서에는 기존 데이터베이스 및 신속 하 게 데이터와 상호 작용할 수 있도록 하는 웹 응용 프로그램을 만들기 시작 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-109">This tutorial shows how to start with an existing database and quickly create a web application that enables users to interact with the data.</span></span> <span data-ttu-id="8c8cc-110">사용 하 여 Entity Framework 6 및 MVC 5 웹 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-110">It uses the Entity Framework 6 and MVC 5 to build the web application.</span></span> <span data-ttu-id="8c8cc-111">ASP.NET 스 캐 폴딩 기능을 사용 하면 자동으로 표시, 업데이트, 만들기, 데이터 삭제에 대 한 코드를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-111">The ASP.NET Scaffolding feature enables you to automatically generate code for displaying, updating, creating and deleting data.</span></span> <span data-ttu-id="8c8cc-112">Visual Studio 내에서 게시 도구를 사용 하 여 쉽게 배포할 수 있습니다 사이트 및 데이터베이스를 Azure로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-112">Using the publishing tools within Visual Studio, you can easily deploy the site and database to Azure.</span></span>

<span data-ttu-id="8c8cc-113">시리즈의이 부분 데이터베이스를 만들고 데이터로 채우는에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-113">This part of the series focuses on creating a database and populating it with data.</span></span>

<span data-ttu-id="8c8cc-114">이 시리즈는 Tom Dykstra 및 Rick Anderson 기여를 사용 하 여 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-114">This series was written with contributions from Tom Dykstra and Rick Anderson.</span></span> <span data-ttu-id="8c8cc-115">의견 섹션에는 사용자의 의견에로 기반 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-115">It was improved based on feedback from users in the comments section.</span></span>

<span data-ttu-id="8c8cc-116">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-116">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8c8cc-117">데이터베이스 설정</span><span class="sxs-lookup"><span data-stu-id="8c8cc-117">Set up the database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c8cc-118">전제 조건</span><span class="sxs-lookup"><span data-stu-id="8c8cc-118">Prerequisites</span></span>

[<span data-ttu-id="8c8cc-119">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="8c8cc-119">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)

## <a name="set-up-the-database"></a><span data-ttu-id="8c8cc-120">데이터베이스 설정</span><span class="sxs-lookup"><span data-stu-id="8c8cc-120">Set up the database</span></span>

<span data-ttu-id="8c8cc-121">기존 데이터베이스의 환경, 모방 하기 위해 먼저 데이터베이스 일부 미리 채워진 데이터로 만들고 데이터베이스에 연결 하는 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-121">To mimic the environment of having an existing database, you will first create a database with some pre-filled data, and then create your web application that connects to the database.</span></span>

<span data-ttu-id="8c8cc-122">이 자습서는 Visual Studio 2017을 사용 하 여 LocalDB를 사용 하 여 개발 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-122">This tutorial was developed using LocalDB with Visual Studio 2017.</span></span> <span data-ttu-id="8c8cc-123">기존 데이터베이스 서버를 사용 하 여 LocalDB 대신 있지만 버전, Visual Studio 및 데이터베이스의 사용자 형식에 따라 모든 데이터 도구가 Visual Studio에서 지원 되지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-123">You can use an existing database server instead of LocalDB, but depending on your version of Visual Studio and your type of database, all of the data tools in Visual Studio might not be supported.</span></span> <span data-ttu-id="8c8cc-124">도구를 데이터베이스에 대해 사용할 수 없는 경우에 데이터베이스에 대 한 일부 관리 도구 모음 내에서 데이터베이스 관련 단계를 수행 하는 것이 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-124">If the tools are not available for your database, you may need to perform some of the database-specific steps within the management suite for your database.</span></span>

<span data-ttu-id="8c8cc-125">Visual Studio 버전에서 데이터베이스 도구를 사용 하 여 문제가 있는 경우 최신 버전의 데이터베이스 도구를 설치 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-125">If you have a problem with the database tools in your version of Visual Studio, make sure you have installed the latest version of the database tools.</span></span> <span data-ttu-id="8c8cc-126">업데이트 또는 데이터베이스 도구를 설치 하는 방법에 대 한 내용은 [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/hh297027)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-126">For information about updating or installing the database tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/hh297027).</span></span>

<span data-ttu-id="8c8cc-127">Visual Studio를 시작 하 고 만듭니다는 **SQL Server 데이터베이스 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-127">Launch Visual Studio and create a **SQL Server Database Project**.</span></span> <span data-ttu-id="8c8cc-128">프로젝트 이름을 **ContosoUniversityData**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-128">Name the project **ContosoUniversityData**.</span></span>

![데이터베이스 프로젝트 만들기](setting-up-database/_static/image1.png)

<span data-ttu-id="8c8cc-130">이제 빈 데이터베이스 프로젝트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-130">You now have an empty database project.</span></span> <span data-ttu-id="8c8cc-131">이 데이터베이스를 Azure에 배포할 수 있습니다 있는지, 프로젝트에 대 한 대상 플랫폼으로 Azure SQL Database를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-131">To make sure that you can deploy this database to Azure, you'll set Azure SQL Database as the target platform for the project.</span></span> <span data-ttu-id="8c8cc-132">대상 플랫폼을 설정 실제로 배포 되지는 않습니다 데이터베이스 데이터베이스 프로젝트 데이터베이스 디자인 대상 플랫폼과 호환 되는지 확인 합니다만 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-132">Setting the target platform does not actually deploy the database; it only means that the database project will verify that the database design is compatible with the target platform.</span></span> <span data-ttu-id="8c8cc-133">대상 플랫폼을 설정 하려면 엽니다는 **속성** 선택한 프로젝트에 대 한 **Microsoft Azure SQL Database** 대상 플랫폼에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-133">To set the target platform, open the **Properties** for the project and select **Microsoft Azure SQL Database** for the target platform.</span></span>

<span data-ttu-id="8c8cc-134">테이블을 정의 하는 SQL 스크립트를 추가 하 여이 자습서에 필요한 테이블을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-134">You can create the tables needed for this tutorial by adding SQL scripts that define the tables.</span></span> <span data-ttu-id="8c8cc-135">프로젝트를 마우스 오른쪽 단추로 클릭 하 고 새 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-135">Right-click your project and add a new item.</span></span> <span data-ttu-id="8c8cc-136">선택 **테이블 및 뷰** > **테이블** 하 고 이름을 *학생*합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-136">Select **Tables and Views** > **Table** and name it *Student*.</span></span>

<span data-ttu-id="8c8cc-137">테이블 파일에서 T-SQL 명령이 테이블을 만들려면 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-137">In the table file, replace the T-SQL command with the following code to create the table.</span></span>

[!code-sql[Main](setting-up-database/samples/sample1.sql)]

<span data-ttu-id="8c8cc-138">디자인 창 코드를 사용 하 여 자동으로 동기화 하는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-138">Notice that the design window automatically synchronizes with the code.</span></span> <span data-ttu-id="8c8cc-139">코드 또는 디자이너를 사용 하 여 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-139">You can work with either the code or designer.</span></span>

![코드와 디자인 표시](setting-up-database/_static/image5.png)

<span data-ttu-id="8c8cc-141">다른 테이블을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-141">Add another table.</span></span> <span data-ttu-id="8c8cc-142">이 이번 과정을 이름을 지정 하 고 다음 T-SQL 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-142">This time name it Course and use the following T-SQL command.</span></span>

[!code-sql[Main](setting-up-database/samples/sample2.sql)]

<span data-ttu-id="8c8cc-143">및 등록 라는 테이블을 만들려면 한 번 더 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-143">And, repeat one more time to create a table named Enrollment.</span></span>

[!code-sql[Main](setting-up-database/samples/sample3.sql)]

<span data-ttu-id="8c8cc-144">데이터베이스를 배포한 후 실행 되는 스크립트를 통해 데이터를 사용 하 여 데이터베이스를 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-144">You can populate your database with data through a script that is run after the database is deployed.</span></span> <span data-ttu-id="8c8cc-145">배포 후 스크립트를 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-145">Add a Post-Deployment Script to the project.</span></span> <span data-ttu-id="8c8cc-146">프로젝트를 마우스 오른쪽 단추로 클릭 하 고 새 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-146">Right-click your project and add a new item.</span></span> <span data-ttu-id="8c8cc-147">선택 **사용자 스크립트** > **배포 후 스크립트**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-147">Select **User Scripts** > **Post-Deployment Script**.</span></span> <span data-ttu-id="8c8cc-148">기본 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-148">You can use the default name.</span></span>

<span data-ttu-id="8c8cc-149">배포 후 스크립트에 다음 T-SQL 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-149">Add the following T-SQL code to the post-deployment script.</span></span> <span data-ttu-id="8c8cc-150">이 스크립트에 추가 하기만 하면 데이터 데이터베이스 없는 일치 하는 레코드가 발견 되 면 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-150">This script simply adds data to the database when no matching record is found.</span></span> <span data-ttu-id="8c8cc-151">덮어쓰기 하거나 데이터베이스에 입력 데이터를 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-151">It does not overwrite or delete any data you may have entered into the database.</span></span>

[!code-sql[Main](setting-up-database/samples/sample4.sql)]

<span data-ttu-id="8c8cc-152">데이터베이스 프로젝트를 배포할 때마다 배포 후 스크립트를 실행 하는 것이 반드시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-152">It is important to note that the post-deployment script is run every time you deploy your database project.</span></span> <span data-ttu-id="8c8cc-153">따라서이 스크립트를 작성 하는 경우 요구 사항을 신중 하 게 검토 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-153">Therefore, you need to carefully consider your requirements when writing this script.</span></span> <span data-ttu-id="8c8cc-154">경우에 따라 프로젝트를 배포할 때마다 알려진된 데이터 집합에서 다시 시작 하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-154">In some cases, you may wish to start over from a known set of data every time the project is deployed.</span></span> <span data-ttu-id="8c8cc-155">다른 경우에 어떤 방식으로 기존 데이터를 변경 하려는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-155">In other cases, you may not want to alter the existing data in any way.</span></span> <span data-ttu-id="8c8cc-156">요구 사항에 따라, 배포 후 스크립트 또는 스크립트에 포함 해야 하는 새로운 필요 여부를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-156">Based on your requirements, you can decide whether you need a post-deployment script or what you need to include in the script.</span></span> <span data-ttu-id="8c8cc-157">배포 후 스크립트를 사용 하 여 데이터베이스에 대 한 자세한 내용은 참조 하세요. [SQL Server 데이터베이스 프로젝트의 데이터를 포함 하 여](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx)입니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-157">For more information about populating your database with a post-deployment script, see [Including Data in a SQL Server Database Project](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx).</span></span>

<span data-ttu-id="8c8cc-158">이제 SQL 스크립트 파일을 4 하지만 실제 테이블이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-158">You now have 4 SQL script files but no actual tables.</span></span> <span data-ttu-id="8c8cc-159">Localdb에 데이터베이스 프로젝트를 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-159">You are ready to deploy your database project to localdb.</span></span> <span data-ttu-id="8c8cc-160">Visual Studio에서 빌드 및 데이터베이스 프로젝트를 배포 하려면 시작 단추 (또는 f5 키)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-160">In Visual Studio, click the Start button (or F5) to build and deploy your database project.</span></span> <span data-ttu-id="8c8cc-161">확인 합니다 **출력** 탭을 빌드 및 배포에 성공 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-161">Check the **Output** tab to verify that the build and deployment succeeded.</span></span>

<span data-ttu-id="8c8cc-162">새 데이터베이스 생성 되어 있는지를 보려면 **SQL Server 개체 탐색기** 올바른 로컬 데이터베이스 서버에 있는 프로젝트의 이름을 찾습니다 (이 예제의 **(localdb) \ProjectsV13**).</span><span class="sxs-lookup"><span data-stu-id="8c8cc-162">To see that the new database has been created, open **SQL Server Object Explorer** and look for the name of the project in the correct local database server (in this case **(localdb)\ProjectsV13**).</span></span>

<span data-ttu-id="8c8cc-163">테이블 데이터와 채워져 있는지를 확인 하려면 테이블을 마우스 오른쪽 단추로 클릭 하 고 선택 **데이터 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-163">To see that the tables are populated with data, right-click a table, and select **View Data**.</span></span>

![테이블 데이터 표시](setting-up-database/_static/image9.png)

<span data-ttu-id="8c8cc-165">테이블 데이터의 편집 가능한 뷰에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-165">An editable view of the table data is displayed.</span></span> <span data-ttu-id="8c8cc-166">예를 들어 선택한 **테이블** > **dbo.course** > **데이터 보기**, 세 개의 열이 있는 테이블을 참조 하세요 (**과정**, **제목**, 및 **크레딧**) 및 4 개 행입니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-166">For example, if you select **Tables** > **dbo.course** > **View Data**, you see a table with three columns (**Course**, **Title**, and **Credits**) and four rows.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8c8cc-167">추가 자료</span><span class="sxs-lookup"><span data-stu-id="8c8cc-167">Additional resources</span></span>

<span data-ttu-id="8c8cc-168">Code First 개발을 소개 하는 예제를 보려면 [ASP.NET MVC 5 시작](../introduction/getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-168">For an introductory example of Code First development, see [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md).</span></span> <span data-ttu-id="8c8cc-169">고급 예제를 보려면 [ASP.NET MVC 4 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-169">For a more advanced example, see [Creating an Entity Framework Data Model for an ASP.NET MVC 4 App](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="8c8cc-170">Entity Framework 접근 방식을 사용할 것인지를 선택 하는 지침을 참조 하세요 [Entity Framework 개발 방법](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-170">For guidance on selecting which Entity Framework approach to use, see [Entity Framework Development Approaches](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c8cc-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8c8cc-171">Next steps</span></span>

<span data-ttu-id="8c8cc-172">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-172">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8c8cc-173">데이터베이스 설정</span><span class="sxs-lookup"><span data-stu-id="8c8cc-173">Set up the database</span></span>

<span data-ttu-id="8c8cc-174">웹 응용 프로그램 및 데이터 모델을 만드는 방법에 알아보려면 다음 자습서로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c8cc-174">Advance to the next tutorial to learn how to create the web application and data models.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="8c8cc-175">웹 응용 프로그램 및 데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="8c8cc-175">Create the web application and data models</span></span>](creating-the-web-application.md)
