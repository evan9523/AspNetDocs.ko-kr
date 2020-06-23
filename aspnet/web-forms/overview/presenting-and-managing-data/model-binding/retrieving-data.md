---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: 모델 바인딩 및 web forms를 사용 하 여 데이터 검색 및 표시 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다. 모델 바인딩을 사용 하면 데이터 상호 작용이 더 간편 하 게-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: d5f1982196c5985b001ca42c2711174e036bb1ec
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240750"
---
# <a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a><span data-ttu-id="dcd49-104">모델 바인딩 및 web forms를 사용 하 여 데이터 검색 및 표시</span><span class="sxs-lookup"><span data-stu-id="dcd49-104">Retrieving and displaying data with model binding and web forms</span></span>

> <span data-ttu-id="dcd49-105">이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-105">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="dcd49-106">모델 바인딩을 사용 하면 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource)를 처리 하는 것 보다 데이터 상호 작용이 보다 간단 하 게 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-106">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="dcd49-107">이 시리즈는 소개 자료로 시작 하 고 이후 자습서에서 보다 고급 개념으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-107">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="dcd49-108">모델 바인딩 패턴은 모든 데이터 액세스 기술에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-108">The model binding pattern works with any data access technology.</span></span> <span data-ttu-id="dcd49-109">이 자습서에서는 Entity Framework를 사용 하지만 가장 친숙 한 데이터 액세스 기술을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-109">In this tutorial, you will use Entity Framework, but you could use the data access technology that is most familiar to you.</span></span> <span data-ttu-id="dcd49-110">GridView, ListView, DetailsView 또는 FormView 컨트롤과 같은 데이터 바인딩된 서버 컨트롤에서 데이터를 선택, 업데이트, 삭제 및 만드는 데 사용할 메서드의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-110">From a data-bound server control, such as a GridView, ListView, DetailsView, or FormView control, you specify the names of the methods to use for selecting, updating, deleting, and creating data.</span></span> <span data-ttu-id="dcd49-111">이 자습서에서는 SelectMethod의 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-111">In this tutorial, you will specify a value for the SelectMethod.</span></span> 
> 
> <span data-ttu-id="dcd49-112">이 메서드 내에서 데이터를 검색 하는 논리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-112">Within that method, you provide the logic for retrieving the data.</span></span> <span data-ttu-id="dcd49-113">다음 자습서에서는 UpdateMethod, DeleteMethod 및 InsertMethod에 대 한 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-113">In the next tutorial, you will set values for UpdateMethod, DeleteMethod and InsertMethod.</span></span>
>
> <span data-ttu-id="dcd49-114">전체 프로젝트는 c # 또는 Visual Basic에서 [다운로드할](https://go.microsoft.com/fwlink/?LinkId=286116) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-114">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or Visual Basic.</span></span> <span data-ttu-id="dcd49-115">다운로드 가능한 코드는 Visual Studio 2012 이상에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-115">The downloadable code works with Visual Studio 2012 and later.</span></span> <span data-ttu-id="dcd49-116">이 자습서에 표시 된 visual studio 2017 템플릿과 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-116">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2017 template shown in this tutorial.</span></span>
> 
> <span data-ttu-id="dcd49-117">이 자습서에서는 Visual Studio에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-117">In the tutorial you run the application in Visual Studio.</span></span> <span data-ttu-id="dcd49-118">또한 호스팅 공급자에 응용 프로그램을 배포 하 고 인터넷을 통해 사용할 수 있도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-118">You can also deploy the application to a hosting provider and make it available over the internet.</span></span> <span data-ttu-id="dcd49-119">Microsoft는에서 최대 10 개의 웹 사이트에 대 한 무료 웹 호스팅을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-119">Microsoft offers free web hosting for up to 10 web sites in a</span></span>  
> <span data-ttu-id="dcd49-120">[무료 Azure 평가판 계정](https://azure.microsoft.com/free/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="dcd49-120">[free Azure trial account](https://azure.microsoft.com/free/dotnet/).</span></span> <span data-ttu-id="dcd49-121">Visual Studio 웹 프로젝트를 Azure App Service Web Apps에 배포 하는 방법에 대 한 자세한 내용은 [Visual studio 시리즈를 사용 하 여 ASP.NET 웹 배포](../../deployment/visual-studio-web-deployment/introduction.md) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="dcd49-121">For information about how to deploy a Visual Studio web project to Azure App Service Web Apps, see the [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md) series.</span></span> <span data-ttu-id="dcd49-122">또한이 자습서에서는 Entity Framework Code First 마이그레이션 사용 하 여 SQL Server 데이터베이스를 Azure SQL Database에 배포 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-122">That tutorial also shows how to use Entity Framework Code First Migrations to deploy your SQL Server database to Azure SQL Database.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="dcd49-123">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="dcd49-123">Software versions used in the tutorial</span></span>
> 
> - <span data-ttu-id="dcd49-124">Microsoft Visual Studio 2017 또는 Microsoft Visual Studio Community 2017</span><span class="sxs-lookup"><span data-stu-id="dcd49-124">Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017</span></span>
>   
> <span data-ttu-id="dcd49-125">이 자습서는 Visual Studio 2012 및 Visual Studio 2013 에서도 작동 하지만 사용자 인터페이스와 프로젝트 템플릿에는 약간의 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-125">This tutorial also works with Visual Studio 2012 and Visual Studio 2013, but there are some differences in the user interface and project template.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="dcd49-126">빌드할 내용</span><span class="sxs-lookup"><span data-stu-id="dcd49-126">What you'll build</span></span>

<span data-ttu-id="dcd49-127">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-127">In this tutorial, you'll:</span></span>

* <span data-ttu-id="dcd49-128">강좌에 등록 된 학생 들과 대학을 반영 하는 데이터 개체 작성</span><span class="sxs-lookup"><span data-stu-id="dcd49-128">Build data objects that reflect a university with students enrolled in courses</span></span>
* <span data-ttu-id="dcd49-129">개체에서 데이터베이스 테이블 작성</span><span class="sxs-lookup"><span data-stu-id="dcd49-129">Build database tables from the objects</span></span>
* <span data-ttu-id="dcd49-130">테스트 데이터로 데이터베이스 채우기</span><span class="sxs-lookup"><span data-stu-id="dcd49-130">Populate the database with test data</span></span>
* <span data-ttu-id="dcd49-131">웹 폼에 데이터 표시</span><span class="sxs-lookup"><span data-stu-id="dcd49-131">Display data in a web form</span></span>

## <a name="create-the-project"></a><span data-ttu-id="dcd49-132">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="dcd49-132">Create the project</span></span>

1. <span data-ttu-id="dcd49-133">Visual Studio 2017에서 **ASP.NET 웹 응용 프로그램 (.NET Framework)** 프로젝트를 **만듭니다.**</span><span class="sxs-lookup"><span data-stu-id="dcd49-133">In Visual Studio 2017, create a **ASP.NET Web Application (.NET Framework)** project called **ContosoUniversityModelBinding**.</span></span>

   ![프로젝트 만들기](retrieving-data/_static/image19.png)

2. <span data-ttu-id="dcd49-135">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-135">Select **OK**.</span></span> <span data-ttu-id="dcd49-136">템플릿을 선택 하는 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-136">The dialog box to select a template appears.</span></span>

   ![web forms 선택](retrieving-data/_static/image3.png)

3. <span data-ttu-id="dcd49-138">**Web Forms** 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-138">Select the **Web Forms** template.</span></span> 

4. <span data-ttu-id="dcd49-139">필요한 경우 **개별 사용자 계정**에 대 한 인증을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-139">If necessary, change the authentication to **Individual User Accounts**.</span></span> 

5. <span data-ttu-id="dcd49-140">**확인**을 선택하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-140">Select **OK** to create the project.</span></span>

## <a name="modify-site-appearance"></a><span data-ttu-id="dcd49-141">사이트 모양 수정</span><span class="sxs-lookup"><span data-stu-id="dcd49-141">Modify site appearance</span></span>

   <span data-ttu-id="dcd49-142">사이트 모양을 사용자 지정 하려면 몇 가지 사항을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-142">Make a few changes to customize site appearance.</span></span> 
   
   1. <span data-ttu-id="dcd49-143">Site.master 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-143">Open the Site.Master file.</span></span>
   
   2. <span data-ttu-id="dcd49-144">제목을 변경 하 여 **내 ASP.NET 응용 프로그램이**아닌 **Contoso 대학** 을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-144">Change the title to display **Contoso University** and not **My ASP.NET Application**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

   3. <span data-ttu-id="dcd49-145">헤더 텍스트를 **응용 프로그램 이름** 에서 **Contoso 대학**으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-145">Change the header text from **Application name** to **Contoso University**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

   4. <span data-ttu-id="dcd49-146">탐색 헤더 링크를 적절 한 사이트에 대 한 링크를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-146">Change the navigation header links to site appropriate ones.</span></span> 
   
      <span data-ttu-id="dcd49-147">**및에 대 한** 링크를 제거 **하 고 대신** 만들 **학생** 페이지에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-147">Remove the links for **About** and **Contact** and, instead, link to a **Students** page, which you will create.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample3.aspx)]

   5. <span data-ttu-id="dcd49-148">Site.master를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-148">Save Site.Master.</span></span>

## <a name="add-a-web-form-to-display-student-data"></a><span data-ttu-id="dcd49-149">학생 데이터를 표시 하는 web form 추가</span><span class="sxs-lookup"><span data-stu-id="dcd49-149">Add a web form to display student data</span></span>

   1. <span data-ttu-id="dcd49-150">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** , **새 항목**을 차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-150">In **Solution Explorer**, right-click your project, select **Add** and then **New Item**.</span></span> 
   
   2. <span data-ttu-id="dcd49-151">**새 항목 추가** 대화 상자에서 **마스터 페이지 템플릿을 사용 하 여 웹 양식을** 선택 하 고 이름을 **학생과 .aspx**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-151">In the **Add New Item** dialog box, select the **Web Form with Master Page** template and name it **Students.aspx**.</span></span>

      ![페이지 만들기](retrieving-data/_static/image5.png)

   3. <span data-ttu-id="dcd49-153">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-153">Select **Add**.</span></span>
   
   4. <span data-ttu-id="dcd49-154">웹 양식의 마스터 페이지에서 **site.master**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-154">For the web form's master page, select **Site.Master**.</span></span>
   
   5. <span data-ttu-id="dcd49-155">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-155">Select **OK**.</span></span>

## <a name="add-the-data-model"></a><span data-ttu-id="dcd49-156">데이터 모델 추가</span><span class="sxs-lookup"><span data-stu-id="dcd49-156">Add the data model</span></span>

<span data-ttu-id="dcd49-157">**모델** 폴더에서 이름이 **UniversityModels.cs**인 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-157">In the **Models** folder, add a class named **UniversityModels.cs**.</span></span>

   1. <span data-ttu-id="dcd49-158">**모델**을 마우스 오른쪽 단추로 클릭 하 고 **추가**, **새 항목**을 차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-158">Right-click **Models**, select **Add**, and then **New Item**.</span></span> <span data-ttu-id="dcd49-159">**새 항목 추가** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-159">The **Add New Item** dialog box appears.</span></span>

   2. <span data-ttu-id="dcd49-160">왼쪽 탐색 메뉴에서 **코드**, **클래스**를 차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-160">From the left navigation menu, select **Code**, then **Class**.</span></span>

      ![모델 클래스 만들기](retrieving-data/_static/image20.png)

   3. <span data-ttu-id="dcd49-162">클래스 이름을 **UniversityModels.cs** 로 하 고 **추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-162">Name the class **UniversityModels.cs** and select **Add**.</span></span>

      <span data-ttu-id="dcd49-163">이 파일에서 `SchoolContext` ,, `Student` `Enrollment` 및 클래스를 다음과 `Course` 같이 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-163">In this file, define the `SchoolContext`, `Student`, `Enrollment`, and `Course` classes as follows:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample4.cs)]

      <span data-ttu-id="dcd49-164">`SchoolContext`클래스는 `DbContext` 데이터베이스 연결 및 데이터 변경 내용을 관리 하는에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-164">The `SchoolContext` class derives from `DbContext`, which manages the database connection and changes in the data.</span></span>

      <span data-ttu-id="dcd49-165">클래스에서 `Student` , 및 속성에 적용 되는 특성을 확인 `FirstName` `LastName` `Year` 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-165">In the `Student` class, notice the attributes applied to the `FirstName`, `LastName`, and `Year` properties.</span></span> <span data-ttu-id="dcd49-166">이 자습서에서는 이러한 특성을 사용 하 여 데이터 유효성 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-166">This tutorial uses these attributes for data validation.</span></span> <span data-ttu-id="dcd49-167">코드를 단순화 하기 위해 이러한 속성만 데이터 유효성 검사 특성으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-167">To simplify the code, only these properties are marked with data-validation attributes.</span></span> <span data-ttu-id="dcd49-168">실제 프로젝트에서는 유효성 검사가 필요한 모든 속성에 유효성 검사 특성을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-168">In a real project, you would apply validation attributes to all properties needing validation.</span></span>

   4. <span data-ttu-id="dcd49-169">UniversityModels.cs을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-169">Save UniversityModels.cs.</span></span>

## <a name="set-up-the-database-based-on-classes"></a><span data-ttu-id="dcd49-170">클래스를 기반으로 데이터베이스를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-170">Set up the database based on classes</span></span>

<span data-ttu-id="dcd49-171">이 자습서에서는 [Code First 마이그레이션](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/) 를 사용 하 여 개체와 데이터베이스 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-171">This tutorial uses [Code First Migrations](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/) to create objects and database tables.</span></span> <span data-ttu-id="dcd49-172">이러한 테이블에는 학생 및 해당 과정에 대 한 정보가 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-172">These tables store information about the students and their courses.</span></span>

   1. <span data-ttu-id="dcd49-173">**도구** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-173">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

   2. <span data-ttu-id="dcd49-174">**패키지 관리자 콘솔**에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-174">In **Package Manager Console**, run this command:</span></span>  
      `enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

      <span data-ttu-id="dcd49-175">명령이 성공적으로 완료 되 면 마이그레이션 사용 이라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-175">If the command completes successfully, a message stating migrations have been enabled appears.</span></span>

      ![마이그레이션 사용](retrieving-data/_static/image8.png)

      <span data-ttu-id="dcd49-177">*Configuration.cs* 라는 파일이 생성 된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-177">Notice that a file named *Configuration.cs* has been created.</span></span> <span data-ttu-id="dcd49-178">클래스에는 `Configuration` `Seed` 데이터베이스 테이블을 테스트 데이터로 미리 채울 수 있는 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-178">The `Configuration` class has a `Seed` method, which can pre-populate the database tables with test data.</span></span>

## <a name="pre-populate-the-database"></a><span data-ttu-id="dcd49-179">데이터베이스 미리 채우기</span><span class="sxs-lookup"><span data-stu-id="dcd49-179">Pre-populate the database</span></span>

   1. <span data-ttu-id="dcd49-180">Configuration.cs를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-180">Open Configuration.cs.</span></span>
   
   2. <span data-ttu-id="dcd49-181">`Seed` 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-181">Add the following code to the `Seed` method.</span></span> <span data-ttu-id="dcd49-182">또한 `using` 네임 스페이스에 대 한 문을 추가 `ContosoUniversityModelBinding. Models` 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-182">Also, add a `using` statement for the `ContosoUniversityModelBinding. Models` namespace.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample5.cs)]

   3. <span data-ttu-id="dcd49-183">Configuration.cs을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-183">Save Configuration.cs.</span></span>

   4. <span data-ttu-id="dcd49-184">패키지 관리자 콘솔에서 명령 **추가-마이그레이션 초기**를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-184">In the Package Manager Console, run the command **add-migration initial**.</span></span>

   5. <span data-ttu-id="dcd49-185">**업데이트-데이터베이스**명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-185">Run the command **update-database**.</span></span>

      <span data-ttu-id="dcd49-186">이 명령을 실행할 때 예외가 발생 하면 `StudentID` 및 `CourseID` 값이 메서드 값과 다를 수 있습니다 `Seed` .</span><span class="sxs-lookup"><span data-stu-id="dcd49-186">If you receive an exception when running this command, the `StudentID` and `CourseID` values might be different from the `Seed` method values.</span></span> <span data-ttu-id="dcd49-187">이러한 데이터베이스 테이블을 열고 및에 대 한 기존 값을 찾습니다 `StudentID` `CourseID` .</span><span class="sxs-lookup"><span data-stu-id="dcd49-187">Open those database tables and find existing values for `StudentID` and `CourseID`.</span></span> <span data-ttu-id="dcd49-188">테이블 시드를 위해 코드에 해당 값을 추가 `Enrollments` 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-188">Add those values to the code for seeding the `Enrollments` table.</span></span>

## <a name="add-a-gridview-control"></a><span data-ttu-id="dcd49-189">GridView 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="dcd49-189">Add a GridView control</span></span>

<span data-ttu-id="dcd49-190">채워진 데이터베이스 데이터를 사용 하 여 이제 해당 데이터를 검색 하 고 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-190">With populated database data, you're now ready to retrieve that data and display it.</span></span> 

1. <span data-ttu-id="dcd49-191">학생과 .aspx를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-191">Open Students.aspx.</span></span>

2. <span data-ttu-id="dcd49-192">`MainContent`자리 표시자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-192">Locate the `MainContent` placeholder.</span></span> <span data-ttu-id="dcd49-193">해당 자리 표시자 내에서이 코드를 포함 하는 **GridView** 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-193">Within that placeholder, add a **GridView** control that includes this code.</span></span>

   [!code-aspx-csharp[Main](retrieving-data/samples/sample6.aspx)]

   <span data-ttu-id="dcd49-194">참고 사항:</span><span class="sxs-lookup"><span data-stu-id="dcd49-194">Things to note:</span></span>
   * <span data-ttu-id="dcd49-195">GridView 요소의 속성에 설정 된 값을 확인 합니다 `SelectMethod` .</span><span class="sxs-lookup"><span data-stu-id="dcd49-195">Notice the value set for the `SelectMethod` property in the GridView element.</span></span> <span data-ttu-id="dcd49-196">이 값은 다음 단계에서 만드는 GridView 데이터를 검색 하는 데 사용 되는 메서드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-196">This value specifies the method used to retrieve GridView data, which you create in the next step.</span></span> 
   
   * <span data-ttu-id="dcd49-197">`ItemType`속성은 `Student` 앞에서 만든 클래스로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-197">The `ItemType` property is set to the `Student` class created earlier.</span></span> <span data-ttu-id="dcd49-198">이 설정을 사용 하면 태그의 클래스 속성을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-198">This setting allows you to reference class properties in the markup.</span></span> <span data-ttu-id="dcd49-199">예를 들어 클래스에는 `Student` 라는 컬렉션이 있습니다 `Enrollments` .</span><span class="sxs-lookup"><span data-stu-id="dcd49-199">For example, the `Student` class has a collection named `Enrollments`.</span></span> <span data-ttu-id="dcd49-200">를 사용 하 여 `Item.Enrollments` 해당 컬렉션을 검색 한 다음 [LINQ 구문을](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) 사용 하 여 각 학생의 등록 크레딧 합계를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-200">You can use `Item.Enrollments` to retrieve that collection and then use [LINQ syntax](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) to retrieve each student's enrolled credits sum.</span></span>
   
3. <span data-ttu-id="dcd49-201">학생 .aspx를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-201">Save Students.aspx.</span></span>

## <a name="add-code-to-retrieve-data"></a><span data-ttu-id="dcd49-202">데이터를 검색 하는 코드 추가</span><span class="sxs-lookup"><span data-stu-id="dcd49-202">Add code to retrieve data</span></span>

   <span data-ttu-id="dcd49-203">학생 코드 숨김이 파일에서 값에 대해 지정 된 메서드를 추가 합니다 `SelectMethod` .</span><span class="sxs-lookup"><span data-stu-id="dcd49-203">In the Students.aspx code-behind file, add the method specified for the `SelectMethod` value.</span></span> 
   
   1. <span data-ttu-id="dcd49-204">Students.aspx.cs를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-204">Open Students.aspx.cs.</span></span>
   
   2. <span data-ttu-id="dcd49-205">`using`및 네임 스페이스에 대 한 문을 추가 `ContosoUniversityModelBinding. Models` `System.Data.Entity` 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-205">Add `using` statements for the `ContosoUniversityModelBinding. Models` and `System.Data.Entity` namespaces.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample7.cs)]

   3. <span data-ttu-id="dcd49-206">에 대해 지정한 메서드를 추가 합니다 `SelectMethod` .</span><span class="sxs-lookup"><span data-stu-id="dcd49-206">Add the method you specified for `SelectMethod`:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample8.cs)]

      <span data-ttu-id="dcd49-207">`Include`절은 쿼리 성능을 향상 시키지만 반드시 필요한 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-207">The `Include` clause improves query performance but isn't required.</span></span> <span data-ttu-id="dcd49-208">절이 없으면 `Include` 데이터는 [*지연 로드*](https://en.wikipedia.org/wiki/Lazy_loading)를 사용 하 여 검색 되며,이는 관련 데이터가 검색 될 때마다 데이터베이스에 별도의 쿼리를 전송 하는 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-208">Without the `Include` clause, the data is retrieved using [*lazy loading*](https://en.wikipedia.org/wiki/Lazy_loading), which involves sending a separate query to the database each time related data is retrieved.</span></span> <span data-ttu-id="dcd49-209">절을 사용 하면 `Include` *즉시 로드*를 사용 하 여 데이터를 검색 합니다. 즉, 단일 데이터베이스 쿼리에서 모든 관련 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-209">With the `Include` clause, data is retrieved using *eager loading*, which means a single database query retrieves all related data.</span></span> <span data-ttu-id="dcd49-210">관련 데이터가 사용 되지 않는 경우 더 많은 데이터가 검색 되기 때문에 즉시 로드 효율성이 떨어집니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-210">If related data isn't used, eager loading is less efficient because more data is retrieved.</span></span> <span data-ttu-id="dcd49-211">그러나이 경우에는 각 레코드에 대해 관련 데이터가 표시 되기 때문에 즉시 로드는 최상의 성능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-211">However, in this case, eager loading gives you the best performance because the related data is displayed for each record.</span></span>

      <span data-ttu-id="dcd49-212">관련 데이터를 로드할 때의 성능 고려 사항에 대 한 자세한 내용은 [ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 관련 데이터 읽기](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 문서의 **지연, 즉시 및 명시적 로드** 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="dcd49-212">For more information about performance considerations when loading related data, see the **Lazy, Eager, and Explicit Loading of Related Data** section in the [Reading Related Data with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) article.</span></span>

      <span data-ttu-id="dcd49-213">기본적으로 데이터는 키로 표시 된 속성의 값을 기준으로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-213">By default, the data is sorted by the values of the property marked as the key.</span></span> <span data-ttu-id="dcd49-214">`OrderBy`다른 정렬 값을 지정 하는 절을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-214">You can add an `OrderBy` clause to specify a different sort value.</span></span> <span data-ttu-id="dcd49-215">이 예제에서는 기본 속성을 `StudentID` 정렬에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-215">In this example, the default `StudentID` property is used for sorting.</span></span> <span data-ttu-id="dcd49-216">[데이터 정렬, 페이징 및 필터링](sorting-paging-and-filtering-data.md) 아티클에서 사용자가 정렬할 열을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-216">In the [Sorting, Paging, and Filtering Data](sorting-paging-and-filtering-data.md) article, the user is enabled to select a column for sorting.</span></span>
 
   4. <span data-ttu-id="dcd49-217">Students.aspx.cs을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-217">Save Students.aspx.cs.</span></span>

## <a name="run-your-application"></a><span data-ttu-id="dcd49-218">애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="dcd49-218">Run your application</span></span> 

<span data-ttu-id="dcd49-219">웹 응용 프로그램 (**F5**)을 실행 하 고 **학생** 페이지로 이동 하 여 다음을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-219">Run your web application (**F5**) and navigate to the **Students** page, which displays the following:</span></span>

   ![데이터 표시](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a><span data-ttu-id="dcd49-221">모델 바인딩 메서드 자동 생성</span><span class="sxs-lookup"><span data-stu-id="dcd49-221">Automatic generation of model binding methods</span></span>

<span data-ttu-id="dcd49-222">이 자습서 시리즈를 통해 작업할 때 자습서의 코드를 프로젝트에 간단 하 게 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-222">When working through this tutorial series, you can simply copy the code from the tutorial to your project.</span></span> <span data-ttu-id="dcd49-223">그러나이 방법의 한 가지 단점은 Visual Studio에서 제공 하는 기능을 인식 하 여 모델 바인딩 메서드에 대 한 코드를 자동으로 생성 하는 것이 아니라는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-223">However, one disadvantage of this approach is that you may not become aware of the feature provided by Visual Studio to automatically generate code for model binding methods.</span></span> <span data-ttu-id="dcd49-224">사용자 고유의 프로젝트에서 작업 하는 경우 자동 코드 생성을 통해 시간을 절약 하 고 작업을 구현 하는 방법을 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-224">When working on your own projects, automatic code generation can save you time and help you gain a sense of how to implement an operation.</span></span> <span data-ttu-id="dcd49-225">이 단원에서는 자동 코드 생성 기능에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-225">This section describes the automatic code generation feature.</span></span> <span data-ttu-id="dcd49-226">이 섹션은 참고용 으로만 제공 되며 프로젝트에서 구현 해야 하는 코드는 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-226">This section is only informational and does not contain any code you need to implement in your project.</span></span> 

<span data-ttu-id="dcd49-227">`SelectMethod`태그 코드에서,, 또는 속성에 대 한 값을 설정할 때 `UpdateMethod` `InsertMethod` `DeleteMethod` **새 메서드 만들기** 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-227">When setting a value for the `SelectMethod`, `UpdateMethod`, `InsertMethod`, or `DeleteMethod` properties in the markup code, you can select the **Create New Method** option.</span></span>

![메서드 만들기](retrieving-data/_static/image18.png)

<span data-ttu-id="dcd49-229">Visual Studio는 적절 한 시그니처를 사용 하 여 코드 숨김으로 메서드를 만들 뿐만 아니라 작업을 수행 하기 위한 구현 코드도 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-229">Visual Studio not only creates a method in the code-behind with the proper signature, but also generates implementation code to perform the operation.</span></span> <span data-ttu-id="dcd49-230">`ItemType`자동 코드 생성 기능을 사용 하기 전에 먼저 속성을 설정 하는 경우 생성 된 코드는 해당 형식을 작업에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-230">If you first set the `ItemType` property before using the automatic code generation feature, the generated code uses that type for the operations.</span></span> <span data-ttu-id="dcd49-231">예를 들어 속성을 설정할 때 `UpdateMethod` 다음 코드가 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-231">For example, when setting the `UpdateMethod` property, the following code is automatically generated:</span></span>

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

<span data-ttu-id="dcd49-232">이 코드는 프로젝트에 추가할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-232">Again, this code doesn't need to be added to your project.</span></span> <span data-ttu-id="dcd49-233">다음 자습서에서는 새 데이터를 업데이트, 삭제 및 추가 하기 위한 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-233">In the next tutorial, you'll implement methods for updating, deleting, and adding new data.</span></span>

## <a name="summary"></a><span data-ttu-id="dcd49-234">요약</span><span class="sxs-lookup"><span data-stu-id="dcd49-234">Summary</span></span>

<span data-ttu-id="dcd49-235">이 자습서에서는 데이터 모델 클래스를 만들고 해당 클래스에서 데이터베이스를 생성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-235">In this tutorial, you created data model classes and generated a database from those classes.</span></span> <span data-ttu-id="dcd49-236">데이터베이스 테이블을 테스트 데이터로 채웠습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-236">You filled the database tables with test data.</span></span> <span data-ttu-id="dcd49-237">모델 바인딩을 사용 하 여 데이터베이스에서 데이터를 검색 한 다음 GridView에 데이터를 표시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-237">You used model binding to retrieve data from the database, and then displayed the data in a GridView.</span></span>

<span data-ttu-id="dcd49-238">이 시리즈의 다음 [자습서](updating-deleting-and-creating-data.md) 에서는 데이터 업데이트, 삭제 및 만들기를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcd49-238">In the next [tutorial](updating-deleting-and-creating-data.md) in this series, you'll enable updating, deleting, and creating data.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="dcd49-239">다음</span><span class="sxs-lookup"><span data-stu-id="dcd49-239">Next</span></span>](updating-deleting-and-creating-data.md)
