---
title: ASP.NET Core의 부분 보기
author: ardalis
description: 부분 보기를 사용하여 큰 태그 파일을 나누고 ASP.NET Core 앱의 웹 페이지에서 공통 태그의 중복을 줄이는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 09/11/2018
uid: mvc/views/partial
ms.openlocfilehash: ff4b99580990edbd768128d77214e664a1e29e56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57033300"
---
# <a name="partial-views-in-aspnet-core"></a>ASP.NET Core의 부분 보기

작성자: [Steve Smith](https://ardalis.com/), [Luke Latham](https://github.com/guardrex), [Maher JENDOUBI](https://twitter.com/maherjend), [Rick Anderson](https://twitter.com/RickAndMSFT), [Scott Sauber](https://twitter.com/scottsauber)

부분 보기는 다른 태그 파일의 렌더링된 출력  *내에서* HTML 출력을 렌더링하는 [Razor](xref:mvc/views/razor) 태그 파일(*.cshtml*)입니다.

::: moniker range=">= aspnetcore-2.1"

‘부분 보기’라는 용어는 MVC 앱(여기서 태그 파일을 ‘보기’라고 함) 또는 Razor Pages 앱(여기서 태그 파일을 ‘페이지’라고 함)을 개발하는 데 사용됩니다. 이 주제에서는 일반적으로 MVC 보기 및 Razor Pages 페이지를 ‘태그 파일’로 참조합니다.

::: moniker-end

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/partial/sample) ([다운로드 방법](xref:index#how-to-download-a-sample))

## <a name="when-to-use-partial-views"></a>부분 보기를 사용하는 경우

부분 보기는 다음을 수행하는 효과적인 방법입니다.

* 큰 태그 파일을 작은 구성 요소로 나눕니다.

  여러 논리적 조각으로 구성된 크고 복잡한 태그 파일에서는 부분 보기로 구분된 각 부분에 대해 작업하는 것이 유용합니다. 태그에는 전체 페이지 구조와 부분 보기에 대한 참조만 포함되므로 태그 파일의 코드는 관리 가능합니다.
* 태그 파일에서 공통 태그 콘텐츠의 중복을 줄입니다.

  태그 파일에서 동일한 태그 요소가 사용되면 부분 보기가 태그 콘텐츠의 중복을 하나의 부분 보기 파일로 제거합니다. 부분 보기에서 태그가 변경되면 부분 보기를 사용하는 태그 파일의 렌더링된 출력을 업데이트합니다.

부분 보기는 일반 레이아웃 요소를 유지 관리하는 데 사용해서는 안 됩니다. 일반 레이아웃 요소는 [_Layout.cshtml](xref:mvc/views/layout) 파일에서 지정해야 합니다.

태그를 렌더링하려면 복잡한 렌더링 논리 또는 코드 실행이 필요한 부분 보기를 사용하지 마세요. 부분 보기 대신 [보기 구성 요소](xref:mvc/views/view-components)를 사용합니다.

## <a name="declare-partial-views"></a>부분 보기 선언

::: moniker range=">= aspnetcore-2.0"

부분 보기는 ‘보기’ 폴더(MVC) 또는 *Pages* 폴더(Razor Pages)에서 유지 관리되는 *.cshtml* 태그 파일입니다.

ASP.NET Core MVC에서 컨트롤러의 <xref:Microsoft.AspNetCore.Mvc.ViewResult>는 보기 또는 부분 보기를 반환할 수 있습니다. 비슷한 기능이 ASP.NET Core 2.2의 Razor Pages에 대해 계획되어 있습니다. Razor Pages에서 <xref:Microsoft.AspNetCore.Mvc.RazorPages.PageModel>은 <xref:Microsoft.AspNetCore.Mvc.PartialViewResult>를 반환할 수 있습니다. 부분 보기 참조 및 렌더링은 [부분 보기 참조](#reference-a-partial-view) 섹션에 설명되어 있습니다.

MVC 보기 또는 페이지 렌더링과 달리 부분 보기는 *_ViewStart.cshtml*을 실행하지 않습니다. *_ViewStart.cshtml*에 대한 자세한 내용은 <xref:mvc/views/layout>을 참조하세요.

부분 보기 파일 이름은 종종 밑줄(`_`)로 시작됩니다. 이 명명 규칙은 필수는 아니지만 부분 보기를 보기 및 페이지와 시각적으로 구분하는 데 도움이 됩니다.

::: moniker-end

::: moniker range="< aspnetcore-2.0"

부분 보기는 ‘보기’ 폴더에서 유지 관리되는 *.cshtml* 태그 파일입니다.

컨트롤러의 <xref:Microsoft.AspNetCore.Mvc.ViewResult>는 보기 또는 부분 보기를 반환할 수 있습니다.

MVC 보기 렌더링과 달리 부분 보기는 *_ViewStart.cshtml*을 실행하지 않습니다. *_ViewStart.cshtml*에 대한 자세한 내용은 <xref:mvc/views/layout>을 참조하세요.

부분 보기 파일 이름은 종종 밑줄(`_`)로 시작됩니다. 이 명명 규칙은 필수는 아니지만 부분 보기를 보기와 시각적으로 구분하는 데 도움이 됩니다.

::: moniker-end

## <a name="reference-a-partial-view"></a>부분 보기 참조

::: moniker range=">= aspnetcore-2.1"

태그 파일 내에서 부분 보기를 참조할 수 있는 여러 가지 방법이 있습니다. 앱에서 다음과 같은 비동기 렌더링 방법 중 하나를 사용하는 것이 좋습니다.

* [부분 태그 도우미](#partial-tag-helper)
* [비동기 HTML 도우미](#asynchronous-html-helper)

::: moniker-end

::: moniker range="< aspnetcore-2.1"

태그 파일 내에서 부분 보기를 참조할 수 있는 두 가지 방법이 있습니다.

* [비동기 HTML 도우미](#asynchronous-html-helper)
* [동기 HTML 도우미](#synchronous-html-helper)

앱에서 [비동기 HTML 도우미](#asynchronous-html-helper)를 사용하는 것이 좋습니다.

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

### <a name="partial-tag-helper"></a>부분 태그 도우미

[부분 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)에는 ASP.NET Core 2.1 이상이 필요합니다.

부분 태그 도우미는 콘텐츠를 비동기식으로 렌더링하며 HTML 같은 구문을 사용합니다.

```cshtml
<partial name="_PartialName" />
```

파일 확장자가 있는 경우 태그 도우미는 부분 보기를 호출하는 태그 파일과 동일한 폴더에 있어야 하는 부분 보기를 참조합니다.

```cshtml
<partial name="_PartialName.cshtml" />
```

다음 예제에서는 앱 루트의 부분 보기를 참조합니다. 물결표-슬래시(`~/`) 또는 슬래시(`/`)로 시작되는 경로는 앱 루트를 참조합니다.

**Razor 페이지**

```cshtml
<partial name="~/Pages/Folder/_PartialName.cshtml" />
<partial name="/Pages/Folder/_PartialName.cshtml" />
```

**MVC**

```cshtml
<partial name="~/Views/Folder/_PartialName.cshtml" />
<partial name="/Views/Folder/_PartialName.cshtml" />
```

다음 예제는 상대 경로가 있는 부분 보기를 참조합니다.

```cshtml
<partial name="../Account/_PartialName.cshtml" />
```

자세한 내용은 <xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper>을 참조하세요.

::: moniker-end

### <a name="asynchronous-html-helper"></a>비동기 HTML 도우미

HTML 도우미를 사용할 때 가장 좋은 방법은 <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.PartialAsync*>를 사용하는 것입니다. `PartialAsync`는 <xref:System.Threading.Tasks.Task`1>에 래핑된 <xref:Microsoft.AspNetCore.Html.IHtmlContent> 형식을 반환합니다. 대기된 호출 접두사로 `@` 문자를 사용하여 메서드를 참조합니다.

```cshtml
@await Html.PartialAsync("_PartialName")
```

파일 확장자가 있는 경우 HTML 도우미는 부분 보기를 호출하는 태그 파일과 동일한 폴더에 있어야 하는 부분 보기를 참조합니다.

```cshtml
@await Html.PartialAsync("_PartialName.cshtml")
```

다음 예제에서는 앱 루트의 부분 보기를 참조합니다. 물결표-슬래시(`~/`) 또는 슬래시(`/`)로 시작되는 경로는 앱 루트를 참조합니다.

::: moniker range=">= aspnetcore-2.1"

**Razor 페이지**

```cshtml
@await Html.PartialAsync("~/Pages/Folder/_PartialName.cshtml")
@await Html.PartialAsync("/Pages/Folder/_PartialName.cshtml")
```

**MVC**

::: moniker-end

```cshtml
@await Html.PartialAsync("~/Views/Folder/_PartialName.cshtml")
@await Html.PartialAsync("/Views/Folder/_PartialName.cshtml")
```

다음 예제는 상대 경로가 있는 부분 보기를 참조합니다.

```cshtml
@await Html.PartialAsync("../Account/_LoginPartial.cshtml")
```

또는 <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.RenderPartialAsync*>를 사용하여 부분 보기를 렌더링할 수 있습니다. 이 메서드는 <xref:Microsoft.AspNetCore.Html.IHtmlContent>를 반환하지 않습니다. 렌더링된 출력을 응답에 직접 스트리밍합니다. 이 메서드는 결과를 반환하지 않기 때문에 Razor 코드 블록 내에서 호출되어야 합니다.

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Home/Discovery.cshtml?name=snippet_RenderPartialAsync)]

`RenderPartialAsync` 스트림은 콘텐츠를 렌더링했으므로 일부 시나리오에서 더 나은 성능을 제공합니다. 성능이 중요한 상황에서는 두 가지 방법을 모두 사용하여 페이지를 벤치마크하고 빠른 응답을 생성하는 방법을 사용합니다.

### <a name="synchronous-html-helper"></a>동기 HTML 도우미

`PartialAsync` 및 `RenderPartialAsync`의 해당하는 동기 항목은 각각 <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.Partial*> 및 <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.RenderPartial*>입니다. 교착 상태인 시나리오가 있으므로 동기 해당 항목을 사용하지 않는 것이 좋습니다. 동기 메서드는 이후 릴리스에서 제거 대상으로 지정됩니다.

> [!IMPORTANT]
> 코드를 실행해야 하는 경우 부분 보기 대신 [보기 구성 요소](xref:mvc/views/view-components)를 사용합니다.

::: moniker range=">= aspnetcore-2.1"

`Partial` 또는 `RenderPartial` 호출 시 Visual Studio 분석기 경고가 발생합니다. 예를 들어 `Partial`의 존재는 다음 경고 메시지를 생성합니다.

> IHtmlHelper.Partial 사용 시 애플리케이션이 교착 상태가 될 수 있습니다. &lt;부분&gt; 태그 도우미 또는 IHtmlHelper.PartialAsync를 사용하세요.

`@Html.Partial` 호출을 `@await Html.PartialAsync` 또는 [부분 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)로 바꿉니다. 부분 태그 도우미 마이그레이션에 대한 자세한 내용은 [HTML 도우미에서 마이그레이션](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper#migrate-from-an-html-helper)을 참조합니다.

::: moniker-end

## <a name="partial-view-discovery"></a>부분 보기 검색

파일 확장자 없는 이름으로 부분 보기를 참조하는 경우, 다음 위치가 명시된 순서로 검색됩니다.

::: moniker range=">= aspnetcore-2.1"

**Razor 페이지**

1. 현재 페이지의 폴더를 실행 중
1. 페이지의 폴더 위에 있는 디렉터리 그래프
1. `/Shared`
1. `/Pages/Shared`
1. `/Views/Shared`

**MVC**

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

1. `/Areas/<Area-Name>/Views/<Controller-Name>`
1. `/Areas/<Area-Name>/Views/Shared`
1. `/Views/Shared`
1. `/Pages/Shared`

::: moniker-end

::: moniker range="< aspnetcore-2.0"

1. `/Areas/<Area-Name>/Views/<Controller-Name>`
1. `/Areas/<Area-Name>/Views/Shared`
1. `/Views/Shared`

::: moniker-end

다음 규칙이 부분 보기 검색에 적용됩니다.

* 부분 보기가 다른 폴더에 있는 경우 파일 이름이 같은 다른 부분 보기가 허용됩니다.
* 파일 확장명 없는 이름으로 부분 보기를 참조할 때 부분 보기가 호출자의 폴더와 ‘공유’ 폴더에 모두 있는 경우 호출자 폴더에 있는 부분 보기가 부분 보기를 제공합니다. 호출자의 폴더에 부분 보기가 없는 경우 부분 보기는 ‘공유’ 폴더에서 제공됩니다. ‘공유’ 폴더의 부분 보기를 ‘공유 부분 보기’ 또는 ‘기본 부분 보기’라고 합니다.
* 부분 보기는 ‘연결’ 가능하며, 순환 참조가 호출에 의해 형성되지 않는 경우 다른 부분 보기를 호출할 수 있습니다. 상대 경로는 항상, 파일의 루트 또는 부모가 아닌 현재 파일에 상대적입니다.

> [!NOTE]
> 부분 보기에 정의된 [Razor](xref:mvc/views/razor) `section`은 부모 태그 파일에 표시되지 않습니다. `section`만 정의되어 있는 부분 보기에 표시됩니다.

## <a name="access-data-from-partial-views"></a>부분 보기에서 데이터 액세스

부분 보기가 인스턴스화되면 부모의 `ViewData` 사전의 ‘사본’을 수신합니다. 부분 보기 내에서 데이터에 대한 업데이트는 부모 보기에 유지되지 않습니다. 부분 보기에서 변경된 `ViewData`는 부분 보기가 반환될 때 손실됩니다.

다음 예는 [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) 인스턴스를 부분 보기에 전달하는 방법을 보여 줍니다.

```cshtml
@await Html.PartialAsync("_PartialName", customViewData)
```

모델을 부분 보기에 전달할 수 있습니다. 모델은 사용자 지정 개체일 수 있습니다. `PartialAsync`(콘텐츠 블록을 호출자에게 렌더링함) 또는 `RenderPartialAsync`(콘텐츠를 출력으로 스트리밍함)를 사용하여 모델을 전달할 수 있습니다.

```cshtml
@await Html.PartialAsync("_PartialName", model)
```

::: moniker range=">= aspnetcore-2.1"

**Razor 페이지**

샘플 앱의 다음 태그는 *Pages/ArticlesRP/ReadRP.cshtml* 페이지에서 가져온 것입니다. 페이지에는 두 개의 부분 보기가 있습니다. 두 번째 부분 보기는 모델 및 `ViewData`를 부분 보기에 전달합니다. `ViewDataDictionary` 생성자 오버로드를 사용하여 기존 `ViewData` 사전을 유지하면서 새로운 `ViewData` 사전을 전달합니다.

[!code-cshtml[](partial/sample/PartialViewsSample/Pages/ArticlesRP/ReadRP.cshtml?name=snippet_ReadPartialViewRP&highlight=5,15-19)]

*Pages/Shared/_AuthorPartialRP.cshtml*은 *ReadRP.cshtml* 태그 파일에서 참조하는 첫 번째 부분 보기입니다.

[!code-cshtml[](partial/sample/PartialViewsSample/Pages/Shared/_AuthorPartialRP.cshtml)]

*Pages/ArticlesRP/_ArticleSectionRP.cshtml*은 *ReadRP.cshtml* 태그 파일에서 참조하는 두 번째 부분 보기입니다.

[!code-cshtml[](partial/sample/PartialViewsSample/Pages/ArticlesRP/_ArticleSectionRP.cshtml)]

**MVC**

::: moniker-end

샘플 앱의 다음 태그는 *Views/Articles/Read.cshtml* 보기를 표시합니다. 보기에는 두 개의 부분 보기가 있습니다. 두 번째 부분 보기는 모델 및 `ViewData`를 부분 보기에 전달합니다. `ViewDataDictionary` 생성자 오버로드를 사용하여 기존 `ViewData` 사전을 유지하면서 새로운 `ViewData` 사전을 전달합니다.

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Articles/Read.cshtml?name=snippet_ReadPartialView&highlight=5,15-19)]

*Views/Shared/_AuthorPartial.cshtml*은 *ReadRP.cshtml* 태그 파일에서 참조하는 첫 번째 부분 보기입니다.

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Shared/_AuthorPartial.cshtml)]

*Views/Articles/_ArticleSection.cshtml*은 *Read.cshtml* 태그 파일에서 참조하는 두 번째 부분 보기입니다.

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Articles/_ArticleSection.cshtml)]

런타임 시 부분은 부모 태그 파일의 렌더링된 출력에 렌더링됩니다. 여기서 자체는 공유 *_Layout.cshtml* 내에서 렌더링됩니다. 첫 번째 부분 보기는 문서 작성자의 이름과 게시 날짜를 렌더링합니다.

> Abraham Lincoln
>
> &lt;공유 부분 보기 파일 경로&gt;의 부분 보기입니다.
> 1863/11/19 12:00:00 AM

두 번째 부분 보기는 문서의 섹션을 렌더링합니다.

> 섹션 1 인덱스: 0
>
> 4개의 점수, 7년 전 ...
>
> 섹션 2 인덱스: 1
>
> 지금 멋진 전투에 참여하고 있습니다. 테스트 중...
>
> 섹션 3 인덱스: 2
>
> 그러나 크게 볼 때 우리는 전념할 수 없습 ...

## <a name="additional-resources"></a>추가 자료

::: moniker range=">= aspnetcore-2.1"

* <xref:mvc/views/razor>
* <xref:mvc/views/tag-helpers/intro>
* <xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper>
* <xref:mvc/views/view-components>
* <xref:mvc/controllers/areas>

::: moniker-end

::: moniker range="< aspnetcore-2.1"

* <xref:mvc/views/razor>
* <xref:mvc/views/view-components>
* <xref:mvc/controllers/areas>

::: moniker-end
