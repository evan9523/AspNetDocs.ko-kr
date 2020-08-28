---
uid: mvc/overview/getting-started/introduction/adding-a-new-field
title: 새 필드 추가 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 4085de68-d243-4378-8a64-86236ea8d2da
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 7018de3eab9d7cced72c76d0b74a79f7c8154f9d
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045145"
---
# <a name="adding-a-new-field"></a><span data-ttu-id="d0bfc-102">새 필드 추가</span><span class="sxs-lookup"><span data-stu-id="d0bfc-102">Adding a New Field</span></span>

<span data-ttu-id="d0bfc-103">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="d0bfc-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="d0bfc-104">이 섹션에서는 변경 내용이 데이터베이스에 적용 되도록 Entity Framework Code First 마이그레이션를 사용 하 여 일부 변경 사항을 모델 클래스로 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-104">In this section you'll use Entity Framework Code First Migrations to migrate some changes to the model classes so the change is applied to the database.</span></span>

<span data-ttu-id="d0bfc-105">기본적으로이 Code First 자습서의 앞부분에서와 같이 Entity Framework Code First를 사용 하 여 데이터베이스를 자동으로 만드는 경우 데이터베이스에 테이블을 추가 하 여 데이터베이스의 스키마가 생성 된 모델 클래스와 동기화 되어 있는지 여부를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-105">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="d0bfc-106">동기화 되지 않은 경우 Entity Framework에서 오류를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-106">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="d0bfc-107">이렇게 하면 런타임에 발생 하는 문제를 쉽게 추적할 수 있습니다. 단, 런타임에는 명확 하지 않은 오류를 통해서만 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-107">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span>

## <a name="setting-up-code-first-migrations-for-model-changes"></a><span data-ttu-id="d0bfc-108">모델 변경에 대 한 Code First 마이그레이션 설정</span><span class="sxs-lookup"><span data-stu-id="d0bfc-108">Setting up Code First Migrations for Model Changes</span></span>

<span data-ttu-id="d0bfc-109">솔루션 탐색기로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-109">Navigate to Solution Explorer.</span></span> <span data-ttu-id="d0bfc-110">*동영상 .mdf* 파일을 마우스 오른쪽 단추로 클릭 하 고 **삭제** 를 선택 하 여 동영상 데이터베이스를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-110">Right click on the *Movies.mdf* file and select **Delete** to remove the movies database.</span></span> <span data-ttu-id="d0bfc-111">*영화 .mdf* 파일이 표시 되지 않으면 아래에 표시 된 **모든 파일 표시** 아이콘을 빨간색 윤곽선에 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-111">If you don't see the *Movies.mdf* file, click on the **Show All Files** icon shown below in the red outline.</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="d0bfc-112">애플리케이션을 빌드하여 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-112">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="d0bfc-113">**도구** 메뉴에서 **NuGet 패키지 관리자** , **패키지 관리자 콘솔**을 차례로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-113">From the **Tools** menu, click **NuGet Package Manager** and then **Package Manager Console**.</span></span>

![Pack Man 추가](adding-a-new-field/_static/image2.png)

<span data-ttu-id="d0bfc-115">**패키지 관리자 콘솔** 창의 프롬프트에 다음을 `PM>` 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-115">In the **Package Manager Console** window at the `PM>` prompt enter</span></span>

<span data-ttu-id="d0bfc-116">사용-마이그레이션-MovieDBContext</span><span class="sxs-lookup"><span data-stu-id="d0bfc-116">Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext</span></span>

![](adding-a-new-field/_static/image3.png)

<span data-ttu-id="d0bfc-117">위의 **마이그레이션 사용** 명령 (위에 표시 됨)은 새 *마이그레이션* 폴더에 *Configuration.cs* 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-117">The **Enable-Migrations** command (shown above) creates a *Configuration.cs* file in a new *Migrations* folder.</span></span>

![](adding-a-new-field/_static/image4.png)

<span data-ttu-id="d0bfc-118">Visual Studio에서 *Configuration.cs* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-118">Visual Studio opens the *Configuration.cs* file.</span></span> <span data-ttu-id="d0bfc-119">`Seed` *Configuration.cs* 파일의 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-119">Replace the `Seed` method in the *Configuration.cs* file with the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

<span data-ttu-id="d0bfc-120">아래의 빨간색 물결선을 마우스로 가리킨 `Movie` `Show Potential Fixes` 다음 클릭 하 고 **mvcmovie를 사용 합니다. 모델을 클릭 합니다.** **using**</span><span class="sxs-lookup"><span data-stu-id="d0bfc-120">Hover over the red squiggly line under `Movie` and click `Show Potential Fixes` and then click **using** **MvcMovie.Models;**</span></span>

![](adding-a-new-field/_static/image5.png)

<span data-ttu-id="d0bfc-121">이렇게 하면 다음 using 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-121">Doing so adds the following using statement:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

> [!NOTE]
> 
> <span data-ttu-id="d0bfc-122">Code First 마이그레이션 `Seed` 은 모든 마이그레이션 후 메서드를 호출 하 고 (즉, 패키지 관리자 콘솔에서 **업데이트-데이터베이스** 를 호출),이 메서드는 이미 삽입 된 행을 업데이트 하거나 아직 존재 하지 않는 경우 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-122">Code First Migrations calls the `Seed` method after every migration (that is, calling **update-database** in the Package Manager Console), and this method updates rows that have already been inserted, or inserts them if they don't exist yet.</span></span>
> 
> <span data-ttu-id="d0bfc-123">다음 코드의 [Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드는 "upsert" 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-123">The [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method in the following code performs an "upsert" operation:</span></span>
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample3.cs)]
> 
> <span data-ttu-id="d0bfc-124">[초기값](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 은 마이그레이션할 때마다 실행 되기 때문에 추가 하려는 행은 데이터베이스를 만드는 첫 번째 마이그레이션 후에 이미 있기 때문에 데이터를 삽입 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-124">Because the [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) method runs with every migration, you can't just insert data, because the rows you are trying to add will already be there after the first migration that creates the database.</span></span> <span data-ttu-id="d0bfc-125">"[Upsert](http://en.wikipedia.org/wiki/Upsert)" 작업은 이미 있는 행을 삽입 하려고 할 때 발생 하는 오류를 방지 하지만 응용 프로그램을 테스트 하는 동안 수행 된 데이터의 변경 내용을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-125">The "[upsert](http://en.wikipedia.org/wiki/Upsert)" operation prevents errors that would happen if you try to insert a row that already exists, but it overrides any changes to data that you may have made while testing the application.</span></span> <span data-ttu-id="d0bfc-126">일부 테이블에서 테스트 데이터를 사용 하는 경우 이러한 상황이 발생 하지 않을 수 있습니다. 테스트 하는 동안 데이터를 변경 하는 경우 데이터베이스 업데이트 후에 변경 내용을 유지 하려는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-126">With test data in some tables you might not want that to happen: in some cases when you change data while testing you want your changes to remain after database updates.</span></span> <span data-ttu-id="d0bfc-127">조건부 삽입 작업을 수행 하려는 경우: 행이 아직 없는 경우에만 행을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-127">In that case you want to do a conditional insert operation: insert a row only if it doesn't already exist.</span></span>   
> 
> <span data-ttu-id="d0bfc-128">[Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드에 전달 된 첫 번째 매개 변수는 행이 이미 있는지 여부를 확인 하는 데 사용할 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-128">The first parameter passed to the [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method specifies the property to use to check if a row already exists.</span></span> <span data-ttu-id="d0bfc-129">제공 하는 테스트 동영상 데이터의 경우 `Title` 목록에서 각 제목이 고유 하므로 속성을이 용도로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-129">For the test movie data that you are providing, the `Title` property can be used for this purpose since each title in the list is unique:</span></span>
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample4.cs)]
> 
> <span data-ttu-id="d0bfc-130">이 코드에서는 제목이 고유한 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-130">This code assumes that titles are unique.</span></span> <span data-ttu-id="d0bfc-131">중복 제목을 수동으로 추가 하는 경우 다음에 마이그레이션을 수행할 때 다음과 같은 예외가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-131">If you manually add a duplicate title, you'll get the following exception the next time you perform a migration.</span></span>   
> 
> <span data-ttu-id="d0bfc-132">*시퀀스에 둘 이상의 요소가 포함 되어 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="d0bfc-132">*Sequence contains more than one element*</span></span>  
> 
> <span data-ttu-id="d0bfc-133">[Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 방법에 대 한 자세한 내용은 [EF 4.3 Addorupdate 메서드를 사용 하 여 처리](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-133">For more information about the [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method, see [Take care with EF 4.3 AddOrUpdate Method](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)..</span></span>

<span data-ttu-id="d0bfc-134">**CTRL + SHIFT + B를 눌러 프로젝트를 빌드합니다.** 이 시점에서 빌드하지 않은 경우 다음 단계가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-134">**Press CTRL-SHIFT-B to build the project.**(The following steps will fail if you don't build at this point.)</span></span>

<span data-ttu-id="d0bfc-135">다음 단계는 초기 마이그레이션의 클래스를 만드는 것입니다 `DbMigration` .</span><span class="sxs-lookup"><span data-stu-id="d0bfc-135">The next step is to create a `DbMigration` class for the initial migration.</span></span> <span data-ttu-id="d0bfc-136">이 마이그레이션은 새 데이터베이스를 만들기 때문에 이전 단계에서 *영화 .mdf* 파일을 삭제 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-136">This migration creates a new database, that's why you deleted the *movie.mdf* file in a previous step.</span></span>

<span data-ttu-id="d0bfc-137">**패키지 관리자 콘솔** 창에서 명령을 입력 `add-migration Initial` 하 여 초기 마이그레이션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-137">In the **Package Manager Console** window, enter the command `add-migration Initial` to create the initial migration.</span></span> <span data-ttu-id="d0bfc-138">"초기" 이름은 임의로 생성 되며 만들어진 마이그레이션 파일의 이름을 사용 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-138">The name "Initial" is arbitrary and is used to name the migration file created.</span></span>

![](adding-a-new-field/_static/image6.png)

<span data-ttu-id="d0bfc-139">Code First 마이그레이션는 *마이그레이션* 폴더 ( *{datestamp} \_ Initial.cs* )에 다른 클래스 파일을 만들고,이 클래스에는 데이터베이스 스키마를 만드는 코드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-139">Code First Migrations creates another class file in the *Migrations* folder (with the name *{DateStamp}\_Initial.cs* ), and this class contains code that creates the database schema.</span></span> <span data-ttu-id="d0bfc-140">마이그레이션 파일 이름은 순서를 지정 하는 데 도움이 되는 타임 스탬프로 미리 고정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-140">The migration filename is pre-fixed with a timestamp to help with ordering.</span></span> <span data-ttu-id="d0bfc-141">*{Datestamp} \_ Initial.cs* 파일을 검토 합니다. 여기에는 `Movies` Movie DB에 대 한 테이블을 만드는 지침이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-141">Examine the *{DateStamp}\_Initial.cs* file, it contains the instructions to create the `Movies` table for the Movie DB.</span></span> <span data-ttu-id="d0bfc-142">아래 지침에서 데이터베이스를 업데이트 하는 경우이 *{Datestamp} \_ Initial.cs* 파일이 실행 되어 DB 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-142">When you update the database in the instructions below, this *{DateStamp}\_Initial.cs* file will run and create the DB schema.</span></span> <span data-ttu-id="d0bfc-143">그런 다음 **시드** 메서드를 실행 하 여 DB를 테스트 데이터로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-143">Then the **Seed** method will run to populate the DB with test data.</span></span>

<span data-ttu-id="d0bfc-144">**패키지 관리자 콘솔**에서 명령을 입력 `update-database` 하 여 데이터베이스를 만들고 메서드를 실행 `Seed` 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-144">In the **Package Manager Console**, enter the command `update-database` to create the database and run the `Seed` method.</span></span>

![](adding-a-new-field/_static/image7.png)

<span data-ttu-id="d0bfc-145">테이블이 이미 존재 하 고 만들 수 없음을 나타내는 오류가 발생 하는 경우 데이터베이스를 삭제 하 고 실행 하기 전에 응용 프로그램을 실행 했기 때문일 수 있습니다 `update-database` .</span><span class="sxs-lookup"><span data-stu-id="d0bfc-145">If you get an error that indicates a table already exists and can't be created, it is probably because you ran the application after you deleted the database and before you executed `update-database`.</span></span> <span data-ttu-id="d0bfc-146">이 경우에는 *동영상 .mdf* 파일을 다시 삭제 하 고 명령을 다시 시도 하십시오 `update-database` .</span><span class="sxs-lookup"><span data-stu-id="d0bfc-146">In that case, delete the *Movies.mdf* file again and retry the `update-database` command.</span></span> <span data-ttu-id="d0bfc-147">그래도 오류가 발생 하면 마이그레이션 폴더와 내용을 삭제 한 후이 페이지 맨 위에 있는 지침부터 시작 합니다. 즉, 영화를 삭제 *합니다.*</span><span class="sxs-lookup"><span data-stu-id="d0bfc-147">If you still get an error, delete the migrations folder and contents then start with the instructions at the top of this page (that is delete the *Movies.mdf* file then proceed to Enable-Migrations).</span></span> <span data-ttu-id="d0bfc-148">그래도 오류가 발생 하면 SQL Server 개체 탐색기를 열고 목록에서 데이터베이스를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-148">If you still get an error, open SQL Server Object Explorer and remove the database from the list.</span></span>

<span data-ttu-id="d0bfc-149">응용 프로그램을 실행 하 고 */영화* URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-149">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="d0bfc-150">초기값 데이터가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-150">The seed data is displayed.</span></span>

![](adding-a-new-field/_static/image8.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="d0bfc-151">영화 모델에 등급 속성 추가</span><span class="sxs-lookup"><span data-stu-id="d0bfc-151">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="d0bfc-152">기존 클래스에 새 속성을 추가 하 여 시작 `Rating` `Movie` 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-152">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="d0bfc-153">*Models\Movie.cs* 파일을 열고 `Rating` 다음과 같은 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-153">Open the *Models\Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

<span data-ttu-id="d0bfc-154">이제 전체 `Movie` 클래스는 다음 코드와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-154">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs?highlight=12)]

<span data-ttu-id="d0bfc-155">응용 프로그램을 빌드합니다 (Ctrl + Shift + B).</span><span class="sxs-lookup"><span data-stu-id="d0bfc-155">Build the application (Ctrl+Shift+B).</span></span>

<span data-ttu-id="d0bfc-156">클래스에 새 필드를 추가 했으므로 `Movie` 이 새 속성이 포함 되도록 바인딩 *목록* 도 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-156">Because you've added a new field to the `Movie` class, you also need to update the binding *white list* so this new property will be included.</span></span> <span data-ttu-id="d0bfc-157">속성을 `bind` `Create` `Edit` 포함 하도록 및 작업 메서드에 대 한 특성을 업데이트 합니다 `Rating` .</span><span class="sxs-lookup"><span data-stu-id="d0bfc-157">Update the `bind` attribute for `Create` and `Edit` action methods to include the `Rating` property:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs?highlight=1)]

<span data-ttu-id="d0bfc-158">브라우저 보기에서 새 `Rating` 속성을 표시, 작성 및 편집하기 위해 보기 템플릿도 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-158">You also need to update the view templates in order to display, create and edit the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="d0bfc-159">*\Views\Movies\Index.cshtml* 파일을 열고 `<th>Rating</th>` **Price** 열 바로 뒤에 열 머리글을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-159">Open the *\Views\Movies\Index.cshtml* file and add a `<th>Rating</th>` column heading just after the **Price** column.</span></span> <span data-ttu-id="d0bfc-160">그런 다음 `<td>` 템플릿 끝 근처에 열을 추가 하 여 값을 렌더링 `@item.Rating` 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-160">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="d0bfc-161">다음은 업데이트 된 *인덱스입니다. cshtml* 뷰 템플릿은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-161">Below is what the updated *Index.cshtml* view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample8.cshtml?highlight=31-33,52-54)]

<span data-ttu-id="d0bfc-162">그런 다음 *\Views\Movies\Create.cshtml* 파일을 열고 `Rating` 다음 강조 표시 된 태그를 사용 하 여 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-162">Next, open the *\Views\Movies\Create.cshtml* file and add the `Rating` field with the following highlighted markup.</span></span> <span data-ttu-id="d0bfc-163">그러면 새 동영상이 생성 될 때 등급을 지정할 수 있도록 텍스트 상자가 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-163">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample9.cshtml?highlight=9-15)]

<span data-ttu-id="d0bfc-164">이제 새 속성을 지원 하도록 응용 프로그램 코드를 업데이트 했습니다 `Rating` .</span><span class="sxs-lookup"><span data-stu-id="d0bfc-164">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="d0bfc-165">응용 프로그램을 실행 하 고 */영화* URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-165">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="d0bfc-166">그러나이 작업을 수행 하면 다음 오류 중 하나가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-166">When you do this, though, you'll see one of the following errors:</span></span>

![](adding-a-new-field/_static/image9.png)  
  
<span data-ttu-id="d0bfc-167">' MovieDBContext ' 컨텍스트를 지 원하는 모델이 데이터베이스를 만든 이후 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-167">The model backing the 'MovieDBContext' context has changed since the database was created.</span></span> <span data-ttu-id="d0bfc-168">Code First 마이그레이션를 사용 하 여 데이터베이스를 업데이트 하는 것이 좋습니다 https://go.microsoft.com/fwlink/?LinkId=238269) .</span><span class="sxs-lookup"><span data-stu-id="d0bfc-168">Consider using Code First Migrations to update the database (https://go.microsoft.com/fwlink/?LinkId=238269).</span></span>

![](adding-a-new-field/_static/image10.png)

<span data-ttu-id="d0bfc-169">`Movie`응용 프로그램의 업데이트 된 모델 클래스가 이제 기존 데이터베이스 테이블의 스키마와 다르기 때문에이 오류가 표시 됩니다 `Movie` .</span><span class="sxs-lookup"><span data-stu-id="d0bfc-169">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="d0bfc-170">(데이터베이스 테이블에 `Rating` 열이 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="d0bfc-170">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="d0bfc-171">이 오류를 해결할 수 있는 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-171">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="d0bfc-172">Entity Framework에서 새 모델 클래스 스키마에 따라 데이터베이스를 자동으로 삭제하고 다시 만들도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-172">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="d0bfc-173">이 방법은 테스트 데이터베이스에서 활발한 개발을 수행할 때 개발 주기의 초기 단계에서 매우 편리하며 신속하게 모델 및 데이터베이스 스키마를 함께 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-173">This approach is very convenient early in the development cycle when you are doing active development on a test database; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="d0bfc-174">그러나 단점은 데이터베이스의 기존 데이터를 잃지 않으므로 프로덕션 데이터베이스에서이 방법을 사용 *하지* 않는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-174">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span> <span data-ttu-id="d0bfc-175">테스트 데이터로 데이터베이스를 자동으로 시드하는 데 이니셜라이저를 사용하는 것은 종종 애플리케이션을 개발하는 효율적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-175">Using an initializer to automatically seed a database with test data is often a productive way to develop an application.</span></span> <span data-ttu-id="d0bfc-176">Entity Framework 데이터베이스 이니셜라이저에 대 한 자세한 내용은 [ASP.NET MVC/Entity Framework 자습서](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-176">For more information on Entity Framework database initializers, see [ASP.NET MVC/Entity Framework tutorial](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
2. <span data-ttu-id="d0bfc-177">모델 클래스와 일치하도록 기존 데이터베이스의 스키마를 명시적으로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-177">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="d0bfc-178">이 방법의 장점은 데이터가 유지된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-178">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="d0bfc-179">이러한 변경을 수동으로 수행하거나 데이터베이스 변경 스크립트를 만들어 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-179">You can make this change either manually or by creating a database change script.</span></span>
3. <span data-ttu-id="d0bfc-180">Code First 마이그레이션을 사용하여 데이터베이스 스키마를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-180">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="d0bfc-181">이 자습서의 경우 Code First 마이그레이션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-181">For this tutorial, we'll use Code First Migrations.</span></span>

<span data-ttu-id="d0bfc-182">초기값 메서드를 업데이트 하 여 새 열에 대 한 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-182">Update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="d0bfc-183">Migrations\ configuration.cs 파일을 열고 각 영화 개체에 등급 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-183">Open Migrations\Configuration.cs file and add a Rating field to each Movie object.</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample10.cs?highlight=6)]

<span data-ttu-id="d0bfc-184">솔루션을 빌드한 다음 **패키지 관리자 콘솔** 창을 열고 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-184">Build the solution, and then open the **Package Manager Console** window and enter the following command:</span></span>

`add-migration Rating`

<span data-ttu-id="d0bfc-185">이 `add-migration` 명령은 마이그레이션 프레임 워크에 현재 MOVIE db 스키마를 사용 하 여 현재 동영상 모델을 검사 하 고 DB를 새 모델로 마이그레이션하는 데 필요한 코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-185">The `add-migration` command tells the migration framework to examine the current movie model with the current movie DB schema and create the necessary code to migrate the DB to the new model.</span></span> <span data-ttu-id="d0bfc-186">이름 등급은 임의 이며 마이그레이션 파일의 이름을 *지정한* 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-186">The name *Rating* is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="d0bfc-187">마이그레이션 단계에서 의미 있는 이름을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-187">It's helpful to use a meaningful name for the migration step.</span></span>

<span data-ttu-id="d0bfc-188">이 명령이 완료 되 면 Visual Studio가 새 파생 클래스를 정의 하는 클래스 파일을 열고 `DbMigration` `Up` 메서드에서 새 열을 만드는 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-188">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` derived class, and in the `Up` method you can see the code that creates the new column.</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample11.cs)]

<span data-ttu-id="d0bfc-189">솔루션을 빌드한 다음 `update-database` **패키지 관리자 콘솔** 창에 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-189">Build the solution, and then enter the `update-database` command in the **Package Manager Console** window.</span></span>

<span data-ttu-id="d0bfc-190">다음 이미지는 **패키지 관리자 콘솔** 창에 출력을 보여 줍니다 (날짜 스탬프 앞에 나오는 *등급* 은 다름).</span><span class="sxs-lookup"><span data-stu-id="d0bfc-190">The following image shows the output in the **Package Manager Console** window (The date stamp prepending *Rating* will be different.)</span></span>

![](adding-a-new-field/_static/image11.png)

<span data-ttu-id="d0bfc-191">응용 프로그램을 다시 실행 하 고/또는 비디오 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-191">Re-run the application and navigate to the /Movies URL.</span></span> <span data-ttu-id="d0bfc-192">새 등급 필드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-192">You can see the new Rating field.</span></span>

![](adding-a-new-field/_static/image12.png)

<span data-ttu-id="d0bfc-193">새 동영상을 추가 하려면 **새로 만들기** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-193">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="d0bfc-194">등급을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-194">Note that you can add a rating.</span></span>

![7_CreateRioII](adding-a-new-field/_static/image13.png)

<span data-ttu-id="d0bfc-196">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-196">Click **Create**.</span></span> <span data-ttu-id="d0bfc-197">이제 등급을 포함 하 여 새 동영상이 영화 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-197">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field/_static/image14.png)

<span data-ttu-id="d0bfc-199">이제 프로젝트에서 마이그레이션을 사용 하 고 있으므로 새 필드를 추가 하거나 스키마를 업데이트할 때 데이터베이스를 삭제할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-199">Now that the project is using migrations, you won't need to drop the database when you add a new field or otherwise update the schema.</span></span> <span data-ttu-id="d0bfc-200">다음 섹션에서는 더 많은 스키마 변경을 수행 하 고 마이그레이션을 사용 하 여 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-200">In the next section, we'll make more schema changes and use migrations to update the database.</span></span>

<span data-ttu-id="d0bfc-201">또한 `Rating` 필드를 편집, 세부 정보 및 삭제 보기 템플릿에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-201">You should also add the `Rating` field to the Edit, Details, and Delete view templates.</span></span>

<span data-ttu-id="d0bfc-202">스키마가 모델과 일치 하므로 **패키지 관리자 콘솔** 창에서 "업데이트-데이터베이스" 명령을 다시 입력 하면 마이그레이션 코드가 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-202">You could enter the "update-database" command in the **Package Manager Console** window again and no migration code would run, because the schema matches the model.</span></span> <span data-ttu-id="d0bfc-203">그러나 "upsert"를 실행 하면 메서드가 다시 실행 되며 `Seed` 초기값 데이터를 변경한 경우 메서드에서 데이터를 변경 하면 변경 내용이 손실 됩니다 `Seed` .</span><span class="sxs-lookup"><span data-stu-id="d0bfc-203">However, running "update-database" will run the `Seed` method again, and if you changed any of the Seed data, the changes will be lost because the `Seed` method upserts data.</span></span> <span data-ttu-id="d0bfc-204">이 메서드에 대 한 자세한 내용은 `Seed` Tom Dykstra의 인기 있는 [ASP.NET MVC/Entity Framework 자습서](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-204">You can read more about the `Seed` method in Tom Dykstra's popular [ASP.NET MVC/Entity Framework tutorial](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="d0bfc-205">이 섹션에서는 모델 개체를 수정 하 고 데이터베이스를 변경 내용과 동기화 된 상태로 유지 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-205">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="d0bfc-206">시나리오를 시험해 볼 수 있도록 새로 만든 데이터베이스를 샘플 데이터로 채우는 방법도 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-206">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="d0bfc-207">이는 Code First에 대 한 간략 한 소개입니다. 주제에 대 한 전체 자습서는 [ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델 만들기](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-207">This was just a quick introduction to Code First, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) for a more complete tutorial on the subject.</span></span> <span data-ttu-id="d0bfc-208">다음으로 모델 클래스에 더 다양 한 유효성 검사 논리를 추가 하 고 일부 비즈니스 규칙을 적용할 수 있도록 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d0bfc-208">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d0bfc-209">[이전](adding-search.md)
> [다음](adding-validation.md)</span><span class="sxs-lookup"><span data-stu-id="d0bfc-209">[Previous](adding-search.md)
[Next](adding-validation.md)</span></span>
