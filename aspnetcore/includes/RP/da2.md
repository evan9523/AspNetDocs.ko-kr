---
ms.openlocfilehash: a0546c44284a78ce0e8d06b0f2b9f65ecf66fac7
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031690"
---

Entity Framework Core가 `Price`를 데이터베이스의 통화에 올바르게 매핑할 수 있도록 `[Column(TypeName = "decimal(18, 2)")]` 데이터 주석이 필요합니다. 자세한 내용은 [데이터 형식](/ef/core/modeling/relational/data-types)을 참조하세요.

완성된 모델은 다음과 같습니다.

[!code-csharp[Main](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Models/MovieDateFixed.cs?name=snippet_1)]

다음 자습서에서 [DataAnnotations](/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6)를 다룹니다. [Display](/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.metadata.displaymetadata) 특성은 필드의 이름에 표시할 대상을 지정합니다(이 경우 "ReleaseDate" 대신 "Release Date"). [DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) 특성은 필드에 저장된 시간 정보가 표시되지 않도록 데이터의 형식(날짜)을 지정합니다.

페이지/동영상으로 이동하고 **편집** 링크로 마우스를 가져가 대상 URL을 봅니다.

![브라우저 창에서 편집 링크에 마우스를 가져가면 http://localhost:1234/Movies/Edit/5의 링크 Url이 표시됩니다.](~/tutorials/razor-pages/da1/edit7.png)

**편집**, **세부 정보** 및 **삭제** 링크는 *Pages/Movies/Index.cshtml* 파일에서 [앵커 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)에 의해 생성됩니다.

[!code-cshtml[](~/tutorials/razor-pages/razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Index.cshtml?highlight=16-18&range=32-)]

[태그 도우미](xref:mvc/views/tag-helpers/intro)를 사용하면 서버 쪽 코드를 Razor 파일에서 HTML 요소를 만들고 렌더링하는 데 사용할 수 있습니다. 위의 코드에서 `AnchorTagHelper`는 Razor 페이지에서 HTML `href` 특성 값(경로는 상대적), `asp-page` 및 경로 ID(`asp-route-id`)를 동적으로 생성합니다. 자세한 내용은 [페이지에 대한 URL 생성](xref:razor-pages/index#url-generation-for-pages)을 참조하세요.

선호하는 브라우저에서 **소스 보기**를 사용하여 생성된 표시를 검사합니다. 생성된 HTML의 일부는 다음과 같습니다.

```html
<td>
  <a href="/Movies/Edit?id=1">Edit</a> |
  <a href="/Movies/Details?id=1">Details</a> |
  <a href="/Movies/Delete?id=1">Delete</a>
</td>
```

동적으로 생성된 링크는 쿼리 문자열이 포함된 동영상 ID를 전달합니다(예: `http://localhost:5000/Movies/Details?id=2`).

편집, 세부 정보 및 삭제 Razor 페이지를 "{id:int}" 경로 템플릿을 사용하도록 업데이트합니다. 이러한 각 페이지에 대한 page 지시문을 `@page`에서 `@page "{id:int}"`로 변경합니다. 앱을 실행한 다음 소스를 봅니다. 생성된 HTML에서 URL의 경로 부분에 ID를 추가합니다.

```html
<td>
  <a href="/Movies/Edit/1">Edit</a> |
  <a href="/Movies/Details/1">Details</a> |
  <a href="/Movies/Delete/1">Delete</a>
</td>
```

정수를 포함하지 **않는** "{id:int}" 경로 템플릿이 있는 페이지에 대한 요청은 HTTP 404(찾을 수 없음) 오류를 반환합니다. 예를 들어 `http://localhost:5000/Movies/Details`는 404 오류를 반환합니다. ID를 옵션으로 설정하려면 경로 제약 조건에 `?`를 추가합니다.

 ```cshtml
@page "{id:int?}"
```

::: moniker range="= aspnetcore-2.0"

### <a name="update-concurrency-exception-handling"></a>동시성 예외 처리 업데이트

*Pages/Movies/Edit.cshtml.cs* 파일에서 `OnPostAsync` 메서드를 업데이트합니다. 다음 강조 표시된 코드는 변경 내용을 보여 줍니다.

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Edit.cshtml.cs?name=snippet1&highlight=16-23)]

앞의 코드는 첫 번째 동시 클라이언트가 동영상을 삭제하고 두 번째 동시 클라이언트가 동영상에 대한 변경 내용을 게시하는 경우에만 동시성 예외를 검색합니다.

`catch` 블록을 테스트하려면:

*  `catch (DbUpdateConcurrencyException)`
* 동영상을 편집합니다.
* 다른 브라우저 창에서 동일한 동영상에 대한 **삭제** 링크를 선택한 다음 동영상을 삭제합니다.
* 이전 브라우저 창에서 동영상에 변경 내용을 게시합니다.

프로덕션 코드는 일반적으로 둘 이상의 클라이언트가 동시에 레코드를 업데이트한 경우 동시성 충돌을 검색합니다. 자세한 내용은 [동시성 충돌 처리](xref:data/ef-rp/concurrency)를 참조하세요.

### <a name="posting-and-binding-review"></a>검토 게시 및 바인딩

*Pages/Movies/Edit.cshtml.cs* 파일을 검사합니다.

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Edit21.cshtml.cs?name=snippet2)]

동영상/편집 페이지에 대해 HTTP GET 요청이 만들어지는 경우(예: `http://localhost:5000/Movies/Edit/2`):

* `OnGetAsync` 메서드는 데이터베이스에서 동영상을 가져오고 `Page` 메서드를 반환합니다. 
* `Page` 메서드는 *Pages/Movies/Edit.cshtml* Razor 페이지를 렌더링합니다. *Pages/Movies/Edit.cshtml* 파일은 동영상 모델을 페이지에서 사용할 수 있도록 하는 모델 지시문(`@model RazorPagesMovie.Pages.Movies.EditModel`)을 포함합니다.
* 편집 양식은 동영상에서 값으로 표시됩니다.

동영상/편집 페이지가 게시될 때:

* 페이지에서 양식 값은 `Movie` 속성으로 바인딩됩니다. `[BindProperty]` 특성은 [모델 바인딩](xref:mvc/models/model-binding)을 활성화합니다.

  ```csharp
  [BindProperty]
  public Movie Movie { get; set; }
  ```

* 모델 상태에 오류가 있는 경우(예: `ReleaseDate`를 날짜로 변환할 수 없는 경우) 양식이 제출된 값으로 다시 게시됩니다.
* 모델 오류가 없는 경우 동영상이 저장됩니다.

인덱스, 만들기 및 삭제 Razor 페이지의 HTTP GET 메서드는 유사한 패턴을 따릅니다. 만들기 Razor 페이지에서 HTTP POST `OnPostAsync` 메서드는 편집 Razor 페이지의 `OnPostAsync` 메서드와 유사한 패턴을 따릅니다.

검색은 다음 자습서에 추가됩니다.
