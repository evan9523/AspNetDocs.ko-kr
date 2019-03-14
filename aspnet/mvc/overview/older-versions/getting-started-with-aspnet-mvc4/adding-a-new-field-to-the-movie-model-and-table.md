---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
title: 영화 모델 및 테이블에 새 필드 추가 | Microsoft Docs
author: Rick-Anderson
description: '참고: 업데이트 된이이 자습서는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 하는 있습니다. 것이 더 안전 하 고 더 간단 하 게 따르고 데모 중...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 9ef2c4f1-a305-4e0a-9fb8-bfbd9ef331d9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
msc.type: authoredcontent
ms.openlocfilehash: 0f9b659b67a9a62635091b1e87169bce1218281a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57060700"
---
<a name="adding-a-new-field-to-the-movie-model-and-table"></a><span data-ttu-id="30c01-104">영화 모델 및 테이블에 새 필드 추가</span><span class="sxs-lookup"><span data-stu-id="30c01-104">Adding a New Field to the Movie Model and Table</span></span>
====================
<span data-ttu-id="30c01-105">[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="30c01-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> > [!NOTE]
> > <span data-ttu-id="30c01-106">이 자습서는 업데이트 된 버전을 사용할 수 [여기](../../getting-started/introduction/getting-started.md) 는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="30c01-107">보다 안전 하 고 더 간단 하 게 수행 되며 더 많은 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="30c01-108">이 섹션에서는 Entity Framework Code First 마이그레이션을 데이터베이스에 변경 내용이 적용 되므로 일부 변경 내용은 모델 클래스로 마이그레이션하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-108">In this section you'll use Entity Framework Code First Migrations to migrate some changes to the model classes so the change is applied to the database.</span></span>

<span data-ttu-id="30c01-109">기본적으로 사용 하는 경우 Entity Framework Code First 데이터베이스를 자동으로 만들려면이 자습서의 앞부분에서 수행한 것 처럼 Code First 테이블에 추가 데이터베이스를 데이터베이스의 스키마에서 생성 된 모델 클래스와 동기화 되어 있는지 여부를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-109">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="30c01-110">동기화 하지 않은 경우 Entity Framework는 오류를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-110">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="30c01-111">이 쉽게 발생할 수 있는 그렇지 않은 경우만 (모호한 오류가) 하 여 런타임 시 개발 시 문제를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-111">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span>

## <a name="setting-up-code-first-migrations-for-model-changes"></a><span data-ttu-id="30c01-112">모델 변경에 대 한 Code First 마이그레이션을 설정</span><span class="sxs-lookup"><span data-stu-id="30c01-112">Setting up Code First Migrations for Model Changes</span></span>

<span data-ttu-id="30c01-113">Visual Studio 2012를 사용 하는 경우 두 번 클릭 합니다 *Movies.mdf* 데이터베이스 도구를 열려면 솔루션 탐색기에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-113">If you are using Visual Studio 2012, double click the *Movies.mdf* file from Solution Explorer to open the database tool.</span></span> <span data-ttu-id="30c01-114">Visual Studio Express for Web 알아보겠습니다 데이터베이스 탐색기, Visual Studio 2012 서버 탐색기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-114">Visual Studio Express for Web will show Database Explorer, Visual Studio 2012 will show Server Explorer.</span></span> <span data-ttu-id="30c01-115">Visual Studio 2010를 사용 하는 경우 SQL Server 개체 탐색기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-115">If you are using Visual Studio 2010, use SQL Server Object Explorer.</span></span>

<span data-ttu-id="30c01-116">데이터베이스 도구 (데이터베이스 탐색기, 서버 탐색기 또는 SQL Server 개체 탐색기)에서 마우스 오른쪽 단추로 클릭 `MovieDBContext` 선택한 **삭제** 영화 데이터베이스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-116">In the database tool (Database Explorer, Server Explorer or SQL Server Object Explorer), right click on `MovieDBContext` and select **Delete** to drop the movies database.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image1.png)

<span data-ttu-id="30c01-117">솔루션 탐색기로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-117">Navigate back to Solution Explorer.</span></span> <span data-ttu-id="30c01-118">마우스 오른쪽 단추로 클릭 합니다 *Movies.mdf* 파일을 선택 **삭제** 영화 데이터베이스를 제거 하려면.</span><span class="sxs-lookup"><span data-stu-id="30c01-118">Right click on the *Movies.mdf* file and select **Delete** to remove the movies database.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image2.png)

<span data-ttu-id="30c01-119">오류가 없는지 확인 하려면 응용 프로그램을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="30c01-119">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="30c01-120">**도구** 메뉴에서 클릭 **NuGet 패키지 관리자** 차례로 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-120">From the **Tools** menu, click **NuGet Package Manager** and then **Package Manager Console**.</span></span>

![팩 Man 추가](adding-a-new-field-to-the-movie-model-and-table/_static/image3.png)

<span data-ttu-id="30c01-122">에 **패키지 관리자 콘솔** 창에는 `PM>` 프롬프트 "Enable-migrations-ContextTypeName MvcMovie.Models.MovieDBContext"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-122">In the **Package Manager Console** window at the `PM>` prompt enter "Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext".</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image4.png)

<span data-ttu-id="30c01-123">합니다 **Enable-migrations** 명령은 (위에 표시 됨)을 만듭니다는 *Configuration.cs* 새 파일 *마이그레이션을* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-123">The **Enable-Migrations** command (shown above) creates a *Configuration.cs* file in a new *Migrations* folder.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image5.png)

<span data-ttu-id="30c01-124">Visual Studio가 열립니다는 *Configuration.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-124">Visual Studio opens the *Configuration.cs* file.</span></span> <span data-ttu-id="30c01-125">대체는 `Seed` 의 메서드를 *Configuration.cs* 를 다음 코드로 파일:</span><span class="sxs-lookup"><span data-stu-id="30c01-125">Replace the `Seed` method in the *Configuration.cs* file with the following code:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample1.cs)]

<span data-ttu-id="30c01-126">아래의 빨간색 물결선을 마우스 오른쪽 단추로 클릭 `Movie` 선택한 **해결** 한 다음 **사용 하 여** **MvcMovie.Models;**</span><span class="sxs-lookup"><span data-stu-id="30c01-126">Right click on the red squiggly line under `Movie` and select **Resolve** then **using** **MvcMovie.Models;**</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image6.png)

<span data-ttu-id="30c01-127">다음 항목을 추가 이렇게 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="30c01-127">Doing so adds the following using statement:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample2.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="30c01-128">첫 번째 마이그레이션을 호출 코드를 `Seed` 모든 마이그레이션 후 메서드 (즉, 호출 **데이터베이스 업데이트** 패키지 관리자 콘솔에서),이 메서드가 이미 삽입 되었거나 경우 삽입 된 행을 업데이트 하 고 있습니다 아직 존재 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="30c01-128">Code First Migrations calls the `Seed` method after every migration (that is, calling **update-database** in the Package Manager Console), and this method updates rows that have already been inserted, or inserts them if they don't exist yet.</span></span>


<span data-ttu-id="30c01-129">**프로젝트를 빌드하려면 CTRL-SHIFT-B를 누릅니다.** (다음 단계를 실패 하는 경우에 시점에서 빌드하지 마세요.)</span><span class="sxs-lookup"><span data-stu-id="30c01-129">**Press CTRL-SHIFT-B to build the project.**(The following steps will fail if your don't build at this point.)</span></span>

<span data-ttu-id="30c01-130">다음 단계를 만드는 것을 `DbMigration` 초기 마이그레이션에 대 한 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-130">The next step is to create a `DbMigration` class for the initial migration.</span></span> <span data-ttu-id="30c01-131">으로이 마이그레이션하는 것이 때문에 새 데이터베이스를 만들고 삭제 하는 *movie.mdf* 이전 단계에서 파일.</span><span class="sxs-lookup"><span data-stu-id="30c01-131">This migration to creates a new database, that's why you deleted the *movie.mdf* file in a previous step.</span></span>

<span data-ttu-id="30c01-132">에 **패키지 관리자 콘솔** 창 "add-migration Initial" 명령을 초기 마이그레이션을 만들려면.</span><span class="sxs-lookup"><span data-stu-id="30c01-132">In the **Package Manager Console** window, enter the command "add-migration Initial" to create the initial migration.</span></span> <span data-ttu-id="30c01-133">이름을 "초기"는 임의 이며 만든 마이그레이션 파일의 이름을 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-133">The name "Initial" is arbitrary and is used to name the migration file created.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image7.png)

<span data-ttu-id="30c01-134">Code First 마이그레이션을에 다른 클래스 파일을 만듭니다는 *마이그레이션* 폴더 (이름의 *{날짜 스탬프}\_Initial.cs* ),이 클래스는 데이터베이스 스키마를 만드는 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-134">Code First Migrations creates another class file in the *Migrations* folder (with the name *{DateStamp}\_Initial.cs* ), and this class contains code that creates the database schema.</span></span> <span data-ttu-id="30c01-135">마이그레이션 파일 이름이 사전 순서 지정에 도움이 되도록 타임 스탬프를 사용 하 여 고정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-135">The migration filename is pre-fixed with a timestamp to help with ordering.</span></span> <span data-ttu-id="30c01-136">검사는 *{날짜 스탬프}\_Initial.cs* 파일인 동영상 DB에 대 한 동영상 테이블을 만드는 지침을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-136">Examine the *{DateStamp}\_Initial.cs* file, it contains the instructions to create the Movies table for the Movie DB.</span></span> <span data-ttu-id="30c01-137">이 지침에서 데이터베이스를 업데이트 하는 경우 *{날짜 스탬프}\_Initial.cs* 파일에서는 실행 하 고 DB 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-137">When you update the database in the instructions below, this *{DateStamp}\_Initial.cs* file will run and create the DB schema.</span></span> <span data-ttu-id="30c01-138">그런 다음 **시드** 메서드 테스트 데이터로 DB를 채우기 위해 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-138">Then the **Seed** method will run to populate the DB with test data.</span></span>

<span data-ttu-id="30c01-139">에 **패키지 관리자 콘솔**, 명령 "업데이트-데이터베이스" 데이터베이스를 만들고 실행 하는 **초기값** 메서드.</span><span class="sxs-lookup"><span data-stu-id="30c01-139">In the **Package Manager Console**, enter the command "update-database" to create the database and run the **Seed** method.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image8.png)

<span data-ttu-id="30c01-140">테이블에서 이미 존재 하 고 만들 수 없습니다를 나타내는 오류를 받게 되 면 것 및 실행 하기 전에 데이터베이스를 삭제 한 후 응용 프로그램을 실행 했으므로 `update-database`합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-140">If you get an error that indicates a table already exists and can't be created, it is probably because you ran the application after you deleted the database and before you executed `update-database`.</span></span> <span data-ttu-id="30c01-141">이 경우 삭제 합니다 *Movies.mdf* 파일을 다시 시도 `update-database` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-141">In that case, delete the *Movies.mdf* file again and retry the `update-database` command.</span></span> <span data-ttu-id="30c01-142">오류가 여전히 발생 하면, 마이그레이션 폴더 및 내용을 삭제 한 후이 페이지의 맨 위에 있는 지침을 사용 하 여 시작 (삭제 되는 *Movies.mdf* Enable-migrations 진행 한 다음 파일).</span><span class="sxs-lookup"><span data-stu-id="30c01-142">If you still get an error, delete the migrations folder and contents then start with the instructions at the top of this page (that is delete the *Movies.mdf* file then proceed to Enable-Migrations).</span></span>

<span data-ttu-id="30c01-143">응용 프로그램을 실행 하 고 이동 합니다 */Movies* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-143">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="30c01-144">초기값 데이터가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-144">The seed data is displayed.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image9.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="30c01-145">영화 모델에 등급 속성 추가</span><span class="sxs-lookup"><span data-stu-id="30c01-145">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="30c01-146">새로 추가 하 여 시작 `Rating` 속성을 기존 `Movie` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-146">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="30c01-147">엽니다는 *Models\Movie.cs* 파일을 추가 합니다 `Rating` 다음과 같은 속성:</span><span class="sxs-lookup"><span data-stu-id="30c01-147">Open the *Models\Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample3.cs)]

<span data-ttu-id="30c01-148">전체 `Movie` 다음 코드는 이제 다음과 클래스:</span><span class="sxs-lookup"><span data-stu-id="30c01-148">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample4.cs?highlight=8)]

<span data-ttu-id="30c01-149">사용 하 여 응용 프로그램 빌드를 **빌드할** &gt; **영화 빌드** 메뉴 명령 또는 CTRL SHIFT. 키를 눌러</span><span class="sxs-lookup"><span data-stu-id="30c01-149">Build the application using the **Build** &gt;**Build Movie** menu command or by pressing CTRL-SHIFT-B.</span></span>

<span data-ttu-id="30c01-150">업데이트 했으므로 합니다 `Model` 클래스도 업데이트 해야 합니다 *\Views\Movies\Index.cshtml* 및 *\Views\Movies\Create.cshtml* 새 표시하기위해템플릿을보려면`Rating`브라우저 보기에서 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-150">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.cshtml* and *\Views\Movies\Create.cshtml* view templates in order to display the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="30c01-151">엽니다는<em>\Views\Movies\Index.cshtml</em> 파일을 추가 `<th>Rating</th>` 열 머리글 바로 뒤를 <strong>가격</strong> 열입니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-151">Open the<em>\Views\Movies\Index.cshtml</em> file and add a `<th>Rating</th>` column heading just after the <strong>Price</strong> column.</span></span> <span data-ttu-id="30c01-152">추가한를 `<td>` 렌더링 템플릿의 끝 열을 `@item.Rating` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-152">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="30c01-153">업데이트 된 다음과 같습니다 <em>Index.cshtml</em> 보기 템플릿은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-153">Below is what the updated <em>Index.cshtml</em> view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample5.cshtml?highlight=26-28,46-48)]

<span data-ttu-id="30c01-154">다음으로 열고 합니다 *\Views\Movies\Create.cshtml* 파일과 폼의 끝 부분에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-154">Next, open the *\Views\Movies\Create.cshtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="30c01-155">이 입력란을 렌더링 하는 새 영화를 만들 때 등급을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-155">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample6.cshtml)]

<span data-ttu-id="30c01-156">이제 새 지원 응용 프로그램 코드를 업데이트 했으므로 `Rating` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-156">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="30c01-157">이제 응용 프로그램을 실행 하 고 이동 합니다 */Movies* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-157">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="30c01-158">이 작업을 수행 하지만 나타납니다 다음 오류 중 하나:</span><span class="sxs-lookup"><span data-stu-id="30c01-158">When you do this, though, you'll see one of the following errors:</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image10.png)

![](adding-a-new-field-to-the-movie-model-and-table/_static/image11.png)

<span data-ttu-id="30c01-159">때문에이 오류를 표시 하는 업데이트 된 `Movie` 응용 프로그램에서 모델 클래스의 스키마와 다릅니다 이제는 `Movie` 기존 데이터베이스의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-159">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="30c01-160">(데이터베이스 테이블에 `Rating` 열이 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="30c01-160">(There's no `Rating` column in the database table.)</span></span>


<span data-ttu-id="30c01-161">오류를 해결하는 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-161">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="30c01-162">Entity Framework에서 새 모델 클래스 스키마에 따라 데이터베이스를 자동으로 삭제하고 다시 만들도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-162">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="30c01-163">이 방법은 편리에서 테스트 데이터베이스는 활발 한 개발을 수행 하는 경우 신속 하 게 모델 및 데이터베이스 스키마를 함께 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-163">This approach is very convenient when doing active development on a test database; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="30c01-164">그러나 단점은 데이터베이스의 기존 데이터를 손실 하는-있도록 있습니다 *하지* 프로덕션 데이터베이스에서이 방법을 사용 하려면!</span><span class="sxs-lookup"><span data-stu-id="30c01-164">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span> <span data-ttu-id="30c01-165">테스트 데이터로 데이터베이스를 자동으로 시드하는 이니셜라이저를 사용 하는 종종 응용 프로그램을 개발 하는 효율적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-165">Using an initializer to automatically seed a database with test data is often a productive way to develope an application.</span></span> <span data-ttu-id="30c01-166">Entity Framework 데이터베이스 이니셜라이저에 대 한 자세한 내용은 참조 Tom Dykstra [ASP.NET MVC/Entity Framework 자습서](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-166">For more information on Entity Framework database initializers, see Tom Dykstra's [ASP.NET MVC/Entity Framework tutorial](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
2. <span data-ttu-id="30c01-167">모델 클래스와 일치하도록 기존 데이터베이스의 스키마를 명시적으로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-167">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="30c01-168">이 방법의 장점은 데이터를 유지한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-168">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="30c01-169">이러한 변경을 수동으로 수행하거나 데이터베이스 변경 스크립트를 만들어 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-169">You can make this change either manually or by creating a database change script.</span></span>
3. <span data-ttu-id="30c01-170">Code First 마이그레이션을 사용하여 데이터베이스 스키마를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-170">Use Code First Migrations to update the database schema.</span></span>


<span data-ttu-id="30c01-171">이 자습서의 경우 Code First 마이그레이션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-171">For this tutorial, we'll use Code First Migrations.</span></span>

<span data-ttu-id="30c01-172">새 열에 대 한 값을 제공 하도록 Seed 메서드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-172">Update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="30c01-173">Migrations\ configuration.cs 파일을 열고 각 영화 개체에 등급 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-173">Open Migrations\Configuration.cs file and add a Rating field to each Movie object.</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample7.cs?highlight=6)]

<span data-ttu-id="30c01-174">솔루션을 연 다음 합니다 **패키지 관리자 콘솔** 창 하 고 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-174">Build the solution, and then open the **Package Manager Console** window and enter the following command:</span></span>

`add-migration AddRatingMig`

<span data-ttu-id="30c01-175">`add-migration` 명령은 마이그레이션 프레임 워크에 DB 새 모델로 마이그레이션하는 데 필요한 코드를 만들고 현재 동영상 DB 스키마를 사용 하 여 현재 영화 모델 검사를 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-175">The `add-migration` command tells the migration framework to examine the current movie model with the current movie DB schema and create the necessary code to migrate the DB to the new model.</span></span> <span data-ttu-id="30c01-176">AddRatingMig는 임의 이며 마이그레이션 파일 이름을 지정 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-176">The AddRatingMig is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="30c01-177">마이그레이션 단계에 대 한 의미 있는 이름을 사용 하는 것이 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-177">It's helpful to use a meaningful name for the migration step.</span></span>

<span data-ttu-id="30c01-178">이 명령은 완료 되 면 Visual Studio 새 정의 하는 클래스 파일을 엽니다 `DbMIgration` 파생 클래스에서 및를 `Up` 메서드는 새 열을 만드는 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-178">When this command finishes, Visual Studio opens the class file that defines the new `DbMIgration` derived class, and in the `Up` method you can see the code that creates the new column.</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample8.cs)]

<span data-ttu-id="30c01-179">솔루션을 빌드하고에서 "데이터베이스 업데이트" 명령을 입력 합니다 **패키지 관리자 콘솔** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-179">Build the solution, and then enter the "update-database" command in the **Package Manager Console** window.</span></span>

<span data-ttu-id="30c01-180">다음 이미지는 출력을 표시 합니다 **패키지 관리자 콘솔** 창 (AddRatingMig 앞에 추가 하는 날짜 스탬프는 이와 다릅니다.)</span><span class="sxs-lookup"><span data-stu-id="30c01-180">The following image shows the output in the **Package Manager Console** window (The date stamp prepending AddRatingMig will be different.)</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image12.png)

<span data-ttu-id="30c01-181">다시 응용 프로그램을 실행 하 고 /Movies URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-181">Re-run the application and navigate to the /Movies URL.</span></span> <span data-ttu-id="30c01-182">새 등급 필드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-182">You can see the new Rating field.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image13.png)

<span data-ttu-id="30c01-183">클릭 합니다 **새로 만들기** 새 영화를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-183">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="30c01-184">참고 등급을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-184">Note that you can add a rating.</span></span>

![7_CreateRioII](adding-a-new-field-to-the-movie-model-and-table/_static/image14.png)

<span data-ttu-id="30c01-186">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-186">Click **Create**.</span></span> <span data-ttu-id="30c01-187">등급을 포함 하 여 새 동영상을는 이제 영화 목록에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-187">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field-to-the-movie-model-and-table/_static/image15.png)

<span data-ttu-id="30c01-189">도 추가 해야 합니다 `Rating` 템플릿 보기를 편집, 세부 정보 및 SearchIndex 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-189">You should also add the `Rating` field to the Edit, Details and SearchIndex view templates.</span></span>

<span data-ttu-id="30c01-190">"데이터베이스 업데이트" 명령에 입력할 수 있습니다 합니다 **패키지 관리자 콘솔** 창을 다시 및 내용이 적용 될, 스키마는 모델과 일치 하므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-190">You could enter the "update-database" command in the **Package Manager Console** window again and no changes would be made, because the schema matches the model.</span></span>

<span data-ttu-id="30c01-191">이 섹션에서는 모델 개체를 수정 및 변경 내용과 동기화 데이터베이스를 유지 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-191">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="30c01-192">시나리오를 시도해 볼 수 있도록 샘플 데이터를 사용 하 여 새로 만든된 데이터베이스를 채우는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-192">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="30c01-193">다음으로, 다양 한 유효성 검사 논리 모델 클래스를 추가 적용 될 몇 가지 비즈니스 규칙을 사용 하도록 설정 하는 방법에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="30c01-193">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="30c01-194">[이전](examining-the-edit-methods-and-edit-view.md)
> [다음](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="30c01-194">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>