---
title: ASP.NET Core MVC 앱에 검색 추가
author: rick-anderson
description: 기본 ASP.NET Core MVC 앱에 검색을 추가하는 방법을 보여줍니다.
ms.author: riande
ms.date: 12/13/2018
uid: tutorials/first-mvc-app/search
ms.openlocfilehash: e5dce35b60080ef752f8e6c6004158219015cbf5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029730"
---
# <a name="add-search-to-an-aspnet-core-mvc-app"></a>ASP.NET Core MVC 앱에 검색 추가

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

이 섹션에서는 *장르* 또는 *이름*별로 영화를 검색할 수 있는 `Index` 작업 메서드에 검색 기능을 추가합니다.

`Index` 메서드를 다음 코드로 업데이트합니다.

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_1stSearch)]

`Index` 작업 메서드의 첫 번째 줄은 영화를 선택하는 [LINQ](/dotnet/standard/using-linq) 쿼리를 만듭니다.

```csharp
var movies = from m in _context.Movie
             select m;
```

쿼리는 이 시점에서*만* 정의되며 데이터베이스에 대해 실행되지 **않았습니다**.

`searchString` 매개 변수에 문자열이 포함되는 경우 영화 쿼리는 검색 문자열의 값에 대해 필터링하도록 수정됩니다.

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_SearchNull2)]

위의 `s => s.Title.Contains()` 코드는 [람다 식](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions)입니다. 람다 식은 메서드 기반 [LINQ](/dotnet/standard/using-linq) 쿼리에서 [Where](/dotnet/api/system.linq.enumerable.where) 메서드 또는 `Contains`(위의 코드에서 사용됨)와 같은 표준 쿼리 연산자 메서드의 인수로 사용됩니다. LINQ 쿼리는 정의될 때 또는 메서드(예: `Where`, `Contains` 또는 `OrderBy`)를 호출하여 수정될 때 실행되지 않습니다. 대신 쿼리 실행이 지연됩니다.  즉, 실제로 실현된 값이 반복되거나 `ToListAsync` 메서드가 호출될 때까지 식의 계산이 지연되는 것을 의미합니다. 지연된 쿼리 실행에 대한 자세한 내용은 [쿼리 실행](/dotnet/framework/data/adonet/ef/language-reference/query-execution)을 참조하세요.

참고: [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) 메서드는 위에 표시된 C# 코드에서가 아닌 데이터베이스에서 실행됩니다. 쿼리에 대한 대/소문자 구분은 데이터베이스 및 데이터 정렬에 따라 달라집니다. SQL Server에서 [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains)는 대/소문자를 구분하는 [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql)로 매핑됩니다. SQLlite에서 기본 데이터 정렬과 함께 대/소문자를 구분합니다.

`/Movies/Index`로 이동합니다. 쿼리 문자열(예: `?searchString=Ghost`)을 URL에 추가합니다. 필터링된 영화가 표시됩니다.

![인덱스 보기](~/tutorials/first-mvc-app/search/_static/ghost.png)

`id`라는 매개 변수를 포함하도록 `Index` 메서드의 서명을 변경하는 경우 `id` 매개 변수는 *Startup.cs*에서 설정된 기본 경로의 선택적 `{id}` 자리 표시자와 일치합니다.

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?highlight=5&name=snippet_1)]

매개 변수를 `id`로, `searchString`의 모든 항목을 `id`로 변경합니다.

위의 `Index` 메서드는 다음과 같습니다.

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1,6,8&name=snippet_1stSearch)]

`id` 매개 변수를 포함한 업데이트된 `Index` 메서드:

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1,6,8&name=snippet_SearchID)]

이제 쿼리 문자열 값이 아닌 경로 데이터(URL 세그먼트)로 검색 제목을 전달할 수 있습니다.

![URL에 추가된 단어 ghost와 Ghostbusters 및 Ghostbusters 2라는 두 개의 반환된 영화 목록이 있는 인덱스 보기](~/tutorials/first-mvc-app/search/_static/g2.png)

그러나 사용자가 영화를 검색하려고 할 때마다 URL을 수정하지는 않습니다. 따라서 이제 영화를 필터링하는 데 도움이 되는 UI 요소를 추가합니다. `Index` 메서드의 서명을 변경하여 경로 바인딩 `ID` 매개 변수 전달 방법을 테스트하는 경우 `searchString`이라는 매개 변수를 사용하도록 다시 변경합니다.

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1,6,8&name=snippet_1stSearch)]

*Views/Movies/Index.cshtml* 파일을 열고 아래에서 강조 표시된 `<form>` 표시를 추가합니다.

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Movies/IndexForm1.cshtml?highlight=10-16&range=4-21)]

HTML `<form>` 태그는 [양식 태그 도우미](xref:mvc/views/working-with-forms)를 사용하므로 양식을 제출하는 경우 필터 문자열은 영화 컨트롤러의 `Index` 작업에 게시됩니다. 변경 내용을 저장하고 필터를 테스트합니다.

![제목 필터 텍스트 상자에 단어 ghost를 입력하여 인덱스 보기](~/tutorials/first-mvc-app/search/_static/filter.png)

예상할 수 있는 대로 `Index` 메서드의 `[HttpPost]` 오버로드가 없습니다. 메서드가 앱의 상태를 변경하지 않고 데이터를 필터링하기 때문에 필요하지 않습니다.

다음 `[HttpPost] Index` 메서드를 추가할 수 있습니다.

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1&name=snippet_SearchPost)]

`notUsed` 매개 변수는 `Index` 메서드의 오버로드를 만드는 데 사용됩니다. 자습서의 뒷부분에서 이에 대해 알아봅니다.

이 메서드를 추가하는 경우 작업 호출자는 `[HttpPost] Index` 메서드와 일치하고 `[HttpPost] Index` 메서드는 아래 이미지에 나와 있는 대로 실행됩니다.

![HttpPost 인덱스에서의 애플리케이션 응답을 포함한 브라우저 창: ghost에 대한 필터](~/tutorials/first-mvc-app/search/_static/fo.png)

그러나 이 `[HttpPost]` 버전의 `Index` 메서드를 추가하는 경우에도 이를 모두 구현하는 방법은 제한됩니다. 특정 검색을 책갈피로 설정하거나 동일하게 필터링된 영화 목록을 보기 위해 클릭할 수 있는 링크를 친구에게 보내려고 한다고 가정합니다. HTTP POST 요청의 URL은 GET 요청의 URL(localhost:xxxxx/Movies/Index)과 동일합니다. URL에는 검색 정보가 없습니다. 검색 문자열 정보는 [양식 필드 값](https://developer.mozilla.org/docs/Learn/HTML/Forms/Sending_and_retrieving_form_data)으로 서버에 전송됩니다. 브라우저 개발자 도구 또는 뛰어난 [Fiddler 도구](http://www.telerik.com/fiddler)에서 확인할 수 있습니다. 아래 이미지에서는 Chrome 브라우저 개발자 도구를 보여줍니다.

![Microsoft Edge에 있는 개발자 도구의 네트워크 탭은 ghost의 searchString 값을 가진 요청 본문을 보여줍니다.](~/tutorials/first-mvc-app/search/_static/f12_rb.png)

요청 본문에서 검색 매개 변수 및 [XSRF](xref:security/anti-request-forgery) 토큰을 볼 수 있습니다. 이전 자습서에서 설명했듯이 [양식 태그 도우미](xref:mvc/views/working-with-forms)는 [XSRF](xref:security/anti-request-forgery) 위조 방지 토큰을 생성합니다. 컨트롤러 메서드에서 토큰 유효성을 검사할 필요가 없도록 데이터를 수정하지 않습니다.

검색 매개 변수가 URL이 아닌 요청 본문에 있기 때문에 책갈피에 해당 검색 정보를 캡처하거나 다른 사용자와 공유할 수 없습니다. 요청을 `HTTP GET`로 지정하여 이 문제를 해결합니다.

[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Views/Movies/IndexGet.cshtml?highlight=12&range=1-23)]

이제 검색을 제출할 때 URL에는 검색 쿼리 문자열이 포함됩니다. `HttpPost Index` 메서드가 있는 경우에도 검색은 `HttpGet Index` 작업 메서드로 이동합니다.

![URL에서 searchString=ghost 및 Ghostbusters 및 Ghostbusters 2라는 두 개의 반환된 영화를 표시하는 브라우저 창은 단어 ghost를 포함합니다.](~/tutorials/first-mvc-app/search/_static/search_get.png)

다음 표시는 `form` 태그에 대한 변경 내용을 표시합니다.

```html
<form asp-controller="Movies" asp-action="Index" method="get">
   ```

## <a name="add-search-by-genre"></a>장르별 검색 추가

다음 `MovieGenreViewModel` 클래스를 *Models* 폴더에 추가합니다.

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieGenreViewModel.cs)]

영화 장르 보기 모델은 다음을 포함합니다.

   * 영화 목록
   * 장르 목록을 포함한 `SelectList` 이를 통해 사용자는 목록에서 장르를 선택할 수 있습니다.
   * 선택한 장르가 포함된 `MovieGenre`
   * 사용자가 검색 텍스트 상자에 입력한 텍스트가 포함된 `SearchString`.

`MoviesController.cs`에서 `Index` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Controllers/MoviesController.cs?name=snippet_SearchGenre)]

다음 코드는 데이터베이스에서 모든 장르를 검색하는 `LINQ` 쿼리입니다.

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Controllers/MoviesController.cs?name=snippet_LINQ)]

특정 장르를 프로젝트하여 장르의 `SelectList`를 생성합니다(선택 목록에 중복 장르가 없도록 함).

사용자가 항목을 검색하면 검색 상자에 검색 값이 유지됩니다.

## <a name="add-search-by-genre-to-the-index-view"></a>인덱스 보기에 장르별 검색 추가

다음과 같이 `Index.cshtml`을 업그레이드합니다.

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Views/Movies/IndexFormGenreNoRating.cshtml?highlight=1,15,16,17,28,31,34,37,43)]

다음 HTML 도우미에서 사용되는 람다 식을 살펴봅니다.

`@Html.DisplayNameFor(model => model.Movies[0].Title)`

이전 코드에서 `DisplayNameFor` HTML 도우미는 람다 식에서 참조되는 `Title` 속성을 검사하여 표시 이름을 확인합니다. 람다 식을 평가하지 않고 검사하기 때문에 `model`, `model.Movies` 또는 `model.Movies[0]`가 `null`이거나 비어 있을 경우 액세스 위반을 수신하지 않습니다. 람다 식이 계산될 경우(예: `@Html.DisplayFor(modelItem => item.Title)`) 모델의 속성 값이 계산됩니다.

장르별, 동영상 제목별 및 둘 다로 검색하여 앱을 테스트합니다.

![https://localhost:5001/Movies?MovieGenre=Comedy&SearchString=2의 결과를 보여주는 브라우저 창](~/tutorials/first-mvc-app/search/_static/s2.png)

> [!div class="step-by-step"]
> [이전](controller-methods-views.md)
> [다음](new-field.md)  
