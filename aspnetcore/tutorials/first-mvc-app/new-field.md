---
title: ASP.NET Core MVC 앱에 새 필드 추가
author: rick-anderson
description: Entity Framework Code First 마이그레이션을 사용하여 모델에 새 필드를 추가하고 해당 변경 내용을 데이터베이스로 마이그레이션하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 12/13/2018
uid: tutorials/first-mvc-app/new-field
ms.openlocfilehash: 7993b36bf9115225e082d2929bb253aba5b18310
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039320"
---
# <a name="add-a-new-field-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="9fd0a-103">ASP.NET Core MVC 앱에 새 필드 추가</span><span class="sxs-lookup"><span data-stu-id="9fd0a-103">Add a new field to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="9fd0a-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="9fd0a-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="9fd0a-105">[Entity Framework](/ef/core/get-started/aspnetcore/new-db) 단원에서 Code First 마이그레이션은 다음 작업에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-105">In this section [Entity Framework](/ef/core/get-started/aspnetcore/new-db) Code First Migrations is used to:</span></span>

* <span data-ttu-id="9fd0a-106">모델에 새 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-106">Add a new field to the model.</span></span>
* <span data-ttu-id="9fd0a-107">새 필드를 데이터베이스로 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-107">Migrate the new field to the database.</span></span>

<span data-ttu-id="9fd0a-108">EF Code First를 사용하여 자동으로 데이터베이스를 만들 경우 Code First는:</span><span class="sxs-lookup"><span data-stu-id="9fd0a-108">When EF Code First is used to automatically create a database, Code First:</span></span>

* <span data-ttu-id="9fd0a-109">데이터베이스 스키마를 추적하기 위해 데이터베이스에 테이블을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-109">Adds a table to the database to  track the schema of the database.</span></span>
* <span data-ttu-id="9fd0a-110">데이터베이스가 생성된 모델 클래스와 동기화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-110">Verify the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="9fd0a-111">동기화되어 있지 않은 경우 EF에서 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-111">If they aren't in sync, EF throws an exception.</span></span> <span data-ttu-id="9fd0a-112">이렇게 하면 더 쉽게 일관성이 없는 데이터베이스/코드 문제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-112">This makes it easier to find inconsistent database/code issues.</span></span>

## <a name="add-a-rating-property-to-the-movie-model"></a><span data-ttu-id="9fd0a-113">영화 모델에 등급 속성 추가</span><span class="sxs-lookup"><span data-stu-id="9fd0a-113">Add a Rating Property to the Movie Model</span></span>

<span data-ttu-id="9fd0a-114">*Models/Movie.cs*에 `Rating` 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-114">Add a `Rating` property to *Models/Movie.cs*:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Models/MovieDateRating.cs?highlight=13&name=snippet)]

<span data-ttu-id="9fd0a-115">앱을 빌드합니다(Ctrl+Shift+B).</span><span class="sxs-lookup"><span data-stu-id="9fd0a-115">Build the app (Ctrl+Shift+B).</span></span>

<span data-ttu-id="9fd0a-116">`Movie` 클래스에 새 필드를 추가했으므로 이 새 속성이 포함되도록 바인딩 허용 목록을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-116">Because you've added a new field to the `Movie` class, you need to update the binding white list so this new property will be included.</span></span> <span data-ttu-id="9fd0a-117">*MoviesController.cs*에서 `Rating` 속성을 포함하도록 `Create` 및 `Edit` 동작 메서드에 대해 `[Bind]` 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-117">In *MoviesController.cs*, update the `[Bind]` attribute for both the `Create` and `Edit` action methods to include the `Rating` property:</span></span>

```csharp
[Bind("ID,Title,ReleaseDate,Genre,Price,Rating")]
   ```

<span data-ttu-id="9fd0a-118">브라우저 보기에서 새 `Rating` 속성을 표시, 작성 및 편집하기 위해 보기 템플릿을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-118">Update the view templates in order to display, create, and edit the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="9fd0a-119">*/Views/Movies/Index.cshtml* 파일을 편집하고 `Rating` 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-119">Edit the */Views/Movies/Index.cshtml* file and add a `Rating` field:</span></span>

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Views/Movies/IndexGenreRating.cshtml?highlight=16,38&range=24-64)]

<span data-ttu-id="9fd0a-120">`Rating` 필드로 */Views/Movies/Create.cshtml*을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-120">Update the */Views/Movies/Create.cshtml* with a `Rating` field.</span></span>

<!-- VS -------------------------->
# <a name="visual-studio--visual-studio-for-mactabvisual-studiovisual-studio-mac"></a>[<span data-ttu-id="9fd0a-121">Visual Studio / Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="9fd0a-121">Visual Studio / Visual Studio for Mac</span></span>](#tab/visual-studio+visual-studio-mac)

<span data-ttu-id="9fd0a-122">이전 "양식 그룹"을 복사/붙여넣기하고 intelliSense에서 필드를 업데이트하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-122">You can copy/paste the previous "form group" and let intelliSense help you update the fields.</span></span> <span data-ttu-id="9fd0a-123">IntelliSense는 [태그 도우미](xref:mvc/views/tag-helpers/intro)와 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-123">IntelliSense works with [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span>

![개발자가 보기의 두 번째 레이블 요소에서 asp-for의 특성 값에 대해 문자 R을 입력했습니다.](new-field/_static/cr.png)

<!-- Code -------------------------->
# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="9fd0a-127">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9fd0a-127">Visual Studio Code</span></span>](#tab/visual-studio-code)
<!-- This tab intentionally left blank. -->
---  
<!-- End of VS tabs -->

<span data-ttu-id="9fd0a-128">새 열에 대해 값을 제공하도록 `SeedData` 클래스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-128">Update the `SeedData` class so that it provides a value for the new column.</span></span> <span data-ttu-id="9fd0a-129">샘플 변경은 아래에 표시되지만 각 `new Movie`에 대해 이 변경을 수행하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-129">A sample change is shown below, but you'll want to make this change for each `new Movie`.</span></span>

[!code-csharp[](start-mvc/sample/MvcMovie/Models/SeedDataRating.cs?name=snippet1&highlight=6)]

<span data-ttu-id="9fd0a-130">앱은 새 필드를 포함하도록 DB가 업데이트될 때까지 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-130">The app won't work until the DB is updated to include the new field.</span></span> <span data-ttu-id="9fd0a-131">이제 실행된 경우 `SqlException`이 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-131">If it's run now, the following `SqlException` is thrown:</span></span>

`SqlException: Invalid column name 'Rating'.`

<span data-ttu-id="9fd0a-132">이 오류는 업데이트된 영화 모델 클래스가 기존 데이터베이스의 영화 테이블 스키마와 다르기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-132">This error occurs because the updated Movie model class is different than the schema of the Movie table of the existing database.</span></span> <span data-ttu-id="9fd0a-133">(데이터베이스 테이블에 `Rating` 열이 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="9fd0a-133">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="9fd0a-134">오류를 해결하는 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-134">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="9fd0a-135">Entity Framework에서 새 모델 클래스 스키마에 따라 데이터베이스를 자동으로 삭제하고 다시 만들도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-135">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="9fd0a-136">이 방법은 테스트 데이터베이스에서 활발한 개발을 수행할 때 개발 주기의 초기 단계에서 매우 편리하며 신속하게 모델 및 데이터베이스 스키마를 함께 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-136">This approach is very convenient early in the development cycle when you're doing active development on a test database; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="9fd0a-137">그러나 단점은 데이터베이스에서 기존 데이터를 손실한다는 것입니다. 따라서 프로덕션 데이터베이스에서 이 방법을 사용하지 않으려 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-137">The downside, though, is that you lose existing data in the database — so you don't want to use this approach on a production database!</span></span> <span data-ttu-id="9fd0a-138">테스트 데이터로 데이터베이스를 자동으로 시드하는 데 이니셜라이저를 사용하는 것은 종종 애플리케이션을 개발하는 효율적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-138">Using an initializer to automatically seed a database with test data is often a productive way to develop an application.</span></span> <span data-ttu-id="9fd0a-139">이는 초기 개발과 SQLite를 사용할 때 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-139">This is a good approach for early development and when using SQLite.</span></span>

2. <span data-ttu-id="9fd0a-140">모델 클래스와 일치하도록 기존 데이터베이스의 스키마를 명시적으로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-140">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="9fd0a-141">이 방법의 장점은 데이터를 유지한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-141">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="9fd0a-142">이러한 변경을 수동으로 수행하거나 데이터베이스 변경 스크립트를 만들어 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-142">You can make this change either manually or by creating a database change script.</span></span>

3. <span data-ttu-id="9fd0a-143">Code First 마이그레이션을 사용하여 데이터베이스 스키마를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-143">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="9fd0a-144">이 자습서의 경우 Code First 마이그레이션이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-144">For this tutorial, Code First Migrations is used.</span></span>

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="9fd0a-145">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9fd0a-145">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="9fd0a-146">**도구** 메뉴에서 **NuGet 패키지 관리자 > 패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-146">From the **Tools** menu, select **NuGet Package Manager > Package Manager Console**.</span></span>

  ![PMC 메뉴](adding-model/_static/pmc.png)

<span data-ttu-id="9fd0a-148">PMC에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-148">In the PMC, enter the following commands:</span></span>

```powershell
Add-Migration Rating
Update-Database
```

<span data-ttu-id="9fd0a-149">`Add-Migration` 명령은 마이그레이션 프레임워크에서 현재 `Movie` DB 스키마로 현재 `Movie` 모델을 검사하고 DB를 새 모델로 마이그레이션하는 데 필요한 코드를 만들도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-149">The `Add-Migration` command tells the migration framework to examine the current `Movie` model with the current `Movie` DB schema and create the necessary code to migrate the DB to the new model.</span></span>

# <a name="visual-studio-code--visual-studio-for-mactabvisual-studio-codevisual-studio-mac"></a>[<span data-ttu-id="9fd0a-150">Visual Studio Code / Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="9fd0a-150">Visual Studio Code / Visual Studio for Mac</span></span>](#tab/visual-studio-code+visual-studio-mac)

[!INCLUDE[](~/includes/RP-mvc-shared/sqlite-warn.md)]

<span data-ttu-id="9fd0a-151">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-151">Run the following command:</span></span>

```cli
dotnet ef migrations add Rating
dotnet ef database update
```

---  
<!-- End of VS tabs -->

<span data-ttu-id="9fd0a-152">"Rating" 이름은 임의로 지정되며 마이그레이션 파일의 이름을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-152">The name "Rating" is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="9fd0a-153">마이그레이션 파일에 의미 있는 이름을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-153">It's helpful to use a meaningful name for the migration file.</span></span>

<span data-ttu-id="9fd0a-154">DB의 모든 레코드가 삭제되면 initialize 메서드가 DB를 시드하고 `Rating` 필드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-154">If all the records in the DB are deleted, the initialize method will seed the DB and include the `Rating` field.</span></span>

<span data-ttu-id="9fd0a-155">앱을 실행하고 `Rating` 필드를 사용하여 동영상을 만들고/편집/표시할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-155">Run the app and verify you can create/edit/display movies with a `Rating` field.</span></span> <span data-ttu-id="9fd0a-156">`Edit`, `Details` 및 `Delete` 보기 템플릿에 `Rating` 필드를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd0a-156">You should add the `Rating` field to the `Edit`, `Details`, and `Delete` view templates.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9fd0a-157">[이전](search.md)
> [다음](validation.md)</span><span class="sxs-lookup"><span data-stu-id="9fd0a-157">[Previous](search.md)
[Next](validation.md)</span></span>  
