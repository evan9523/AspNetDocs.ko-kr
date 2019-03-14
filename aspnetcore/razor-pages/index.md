---
title: ASP.NET Core의 Razor 페이지 소개
author: Rick-Anderson
description: 페이지 코딩 중심의 시나리오에서 ASP.NET Core의 Razor 페이지를 사용하면 MVC를 사용할 때보다 어떻게 더 쉽고 생산적인지 알아봅니다.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 05/12/2018
uid: razor-pages/index
---
# <a name="introduction-to-razor-pages-in-aspnet-core"></a>ASP.NET Core의 Razor 페이지 소개

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Ryan Nowak](https://github.com/rynowak)

Razor 페이지는 페이지 코딩 중심의 시나리오를 보다 쉽고 생산적으로 만들어주는 ASP.NET Core MVC의 새로운 기능입니다.

모델-뷰-컨트롤러 방식을 사용하는 자습서를 찾고 있다면 [ASP.NET Core MVC 시작하기](xref:tutorials/first-mvc-app/start-mvc)를 참고하시기 바랍니다.

이 문서에서는 Razor 페이지에 대한 소개를 제공합니다. 단계별 자습서가 아닙니다. Visual Studio를 사용하여 Razor 페이지 프로젝트를 만드는 방법에 대한 자세한 내용은 [Razor 페이지 시작하기](xref:tutorials/razor-pages/razor-pages-start)를 참고하시기 바랍니다. ASP.NET Core에 대한 개요는 [ASP.NET Core 소개](xref:index)를 참고하시기 바랍니다.

## <a name="prerequisites"></a>전제 조건

[!INCLUDE[](~/includes/net-core-prereqs-all-2.2.md)]

<a name="rpvs17"></a>

## <a name="create-a-razor-pages-project"></a>Razor Pages 프로젝트 만들기

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

Razor Pages 프로젝트를 만드는 방법에 대한 자세한 내용은 [Razor Pages 시작](xref:tutorials/razor-pages/razor-pages-start)을 참조하세요.

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

::: moniker range=">= aspnetcore-2.1"

명령줄에서 `dotnet new webapp`을 실행합니다.

::: moniker-end

::: moniker range="= aspnetcore-2.0"

명령줄에서 `dotnet new razor`을 실행합니다.

::: moniker-end

Mac용 Visual Studio에서 생성된 *.csproj* 파일을 엽니다.

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

::: moniker range=">= aspnetcore-2.1"

명령줄에서 `dotnet new webapp`을 실행합니다.

::: moniker-end

::: moniker range="= aspnetcore-2.0"

명령줄에서 `dotnet new razor`을 실행합니다.

::: moniker-end

---

## <a name="razor-pages"></a>Razor 페이지

Razor 페이지는 *Startup.cs*에서 사용할 수 있게 설정됩니다.

[!code-cs[](index/sample/RazorPagesIntro/Startup.cs?name=snippet_Startup)]

기본적인 페이지를 살펴보겠습니다. <a name="OnGet"></a>

[!code-cshtml[](index/sample/RazorPagesIntro/Pages/Index.cshtml)]

위의 코드는 Razor 뷰 파일과 매우 비슷합니다. 차이점은 `@page` 지시문입니다. `@page`는 파일을 MVC 액션으로 만드는데, 이 말은 컨트롤러를 거치지 않고 이 파일이 요청을 직접 처리한다는 뜻입니다. `@page`는 페이지의 첫 번째 Razor 지시문이어야 합니다. `@page`는 다른 Razor 구조의 동작에 영향을 줍니다.

다음 두 파일은 `PageModel` 클래스를 사용하는 비슷한 페이지를 보여줍니다. *Pages/Index2.cshtml* 파일은 다음과 같습니다.

[!code-cshtml[](index/sample/RazorPagesIntro/Pages/Index2.cshtml)]

*Pages/Index2.cshtml.cs* 페이지 모델은 다음과 같습니다.

[!code-cs[](index/sample/RazorPagesIntro/Pages/Index2.cshtml.cs)]

규약에 따라 `PageModel` 클래스 파일의 이름은 *.cs*가 추가된 Razor 페이지 파일의 이름과 동일합니다. 예를 들어 위의 Razor 페이지는 *Pages/Index2.cshtml*입니다. 그리고 `PageModel` 클래스가 포함된 파일의 이름은 *Pages/Index2.cshtml.cs*입니다.

페이지에 대한 URL 경로 연결은 파일 시스템 상의 페이지 위치에 따라 결정됩니다. 다음 표는 Razor 페이지 경로 및 그와 일치하는 URL을 보여줍니다.

| 파일 이름 및 경로               | 일치하는 URL |
| ----------------- | ------------ |
| */Pages/Index.cshtml* | `/` 또는 `/Index` |
| */Pages/Contact.cshtml* | `/Contact` |
| */Pages/Store/Contact.cshtml* | `/Store/Contact` |
| */Pages/Store/Index.cshtml* | `/Store` 또는 `/Store/Index` |

메모:

* 런타임은 기본적으로 *Pages* 폴더에서 Razor 페이지 파일을 검색합니다.
* URL에 페이지가 지정되어 있지 않을 경우 `Index`가 기본 페이지입니다.

## <a name="write-a-basic-form"></a>기본적인 양식 작성하기

Razor 페이지는 앱을 만들때 웹 브라우저에서 사용되는 일반적인 패턴을 손쉽게 구현할 수 있도록 설계되었습니다. [모델 바인딩](xref:mvc/models/model-binding), [태그 도우미](xref:mvc/views/tag-helpers/intro) 및 HTML 도우미는 모두 Razor 페이지 클래스에 정의된 속성을 통해서 *정확하게 동작*합니다. `Contact` 모델에 대한 기본적인 "연락처" 양식을 구현하는 페이지를 생각해보겠습니다.

이 문서의 예제에서 `DbContext`는 [Startup.cs](https://github.com/aspnet/Docs/blob/master/aspnetcore/razor-pages/index/sample/RazorPagesContacts/Startup.cs#L15-L16) 파일에서 초기화됩니다.

[!code-cs[](index/sample/RazorPagesContacts/Startup.cs?highlight=15-16)]

데이터 모델은 다음과 같습니다.

[!code-cs[](index/sample/RazorPagesContacts/Data/Customer.cs)]

db 컨텍스트는 다음과 같습니다.

[!code-cs[](index/sample/RazorPagesContacts/Data/AppDbContext.cs)]

*Pages/Create.cshtml* 뷰 파일은 다음과 같습니다.

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Create.cshtml)]

*Pages/Create.cshtml.cs* 페이지 모델은 다음과 같습니다.

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_ALL)]

규약에 따라 `PageModel` 클래스의 이름은 `<PageName>Model`로 지정하며 페이지와 동일한 네임스페이스에 위치합니다.

`PageModel` 클래스를 사용하면 페이지의 논리를 페이지의 표현으로부터 분리할 수 있습니다. 이 클래스는 페이지로 전송된 요청에 대한 페이지 처리기와 페이지를 렌더링하기 위해 사용되는 데이터를 정의합니다. 이렇게 분리함으로써 [종속성 주입](xref:fundamentals/dependency-injection)을 통해서 페이지의 종속성을 관리할 수 있고 페이지를 [단위 테스트](xref:test/razor-pages-tests) 할 수 있습니다.

이 페이지는 `POST` 요청 시(사용자가 양식을 게시할 때) 실행되는 `OnPostAsync` *처리기 메서드*를 갖고 있습니다. 모든 HTTP 동사에 대한 처리기 메서드를 추가할 수 있습니다. 가장 일반적인 처리기는 다음과 같습니다.

* `OnGet`: 페이지에 필요한 상태를 초기화합니다. [OnGet](#OnGet) 예제.
* `OnPost`: 양식 제출을 처리합니다.

`Async` 명명 접미사는 선택 사항이지만 비동기 함수에 대한 규약으로 자주 사용됩니다. 위의 예제에 사용된 `OnPostAsync`의 코드는 일반적으로 컨트롤러에서 작성하던 코드와 비슷해 보입니다. 위의 코드는 Razor 페이지의 일반적인 코드입니다. [모델 바인딩](xref:mvc/models/model-binding), [유효성 검사](xref:mvc/models/validation) 및 액션 결과 같은 MVC의 기본적인 기능들이 대부분 공유됩니다.  <!-- Review: Ryan, can we get a list of what is shared and what isn't? -->

위의 `OnPostAsync` 메서드는 다음과 같습니다.

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync)]

그리고 `OnPostAsync`의 기본적인 흐름은 다음과 같습니다.

유효성 검사 오류를 확인합니다.

*  오류가 없는 경우 데이터를 저장하고 리디렉션합니다.
*  오류가 있을 경우 유효성 검사 메시지가 포함된 페이지를 다시 표시합니다. 클라이언트 측 유효성 검사는 기존의 ASP.NET Core MVC 애플리케이션과 동일합니다. 대부분의 경우 유효성 검사 오류는 클라이언트에서 감지되어 서버에는 제출되지 않습니다.

데이터가 성공적으로 입력되면 `OnPostAsync` 처리기 메서드가 `RedirectToPage` 도우미 메서드를 호출하여 `RedirectToPageResult`의 인스턴스를 반환합니다. `RedirectToPage`는 `RedirectToAction`이나 `RedirectToRoute`와 비슷하지만 페이지에 맞춰진 새로운 액션 결과입니다. 위의 예제에서 이 메서드는 루트 인덱스 페이지(`/Index`)로 리디렉션합니다. `RedirectToPage`는 [페이지에 대한 URL 생성](#url_gen) 섹션에서 자세히 설명합니다.

서버로 전달된 제출 양식에 유효성 검사 오류가 존재할 경우 `OnPostAsync` 처리기 메서드가 `Page` 도우미 메서드를 호출합니다. `Page`는 `PageResult`의 인스턴스를 반환합니다. `Page`를 반환하는 것은 컨트롤의 액션에서 `View`를 반환하는 것과 비슷합니다. `PageResult`는 처리기 메서드의 기본 <!-- Review  --> 반환 형식입니다. `void`를 반환하는 처리기 메서드는 페이지를 렌더링합니다.

`Customer` 속성은 `[BindProperty]` 특성을 이용해서 모델 바인딩 대상으로 명시적으로 지정(opt in)합니다.

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_PageModel&highlight=10-11)]

Razor 페이지는 기본적으로 비 GET 동사에 대해서만 속성을 바인딩합니다. 속성을 바인딩하면 작성해야 하는 코드의 양을 줄일 수 있습니다. 바인딩은 양식 필드 렌더링할 때와 (`<input asp-for="Customer.Name" />`) 입력을 받아들일 때 동일한 속성을 사용하여 코드를 줄입니다.

[!INCLUDE[](~/includes/bind-get.md)]

홈페이지(*Index.cshtml*)는 다음과 같습니다.

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Index.cshtml)]

연결된 `PageModel` 클래스(*Index.cshtml.cs*)는 다음과 같습니다.

[!code-cs[](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs)]

*Index.cshtml* 파일에는 각 연락처에 대한 편집 링크를 만들기 위한 다음의 태그가 포함되어 있습니다.

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=21)]

이 [앵커 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)는 Edit 페이지에 대한 링크를 생성하기 위해 `asp-route-{value}` 특성을 사용합니다. 링크에는 연락처 ID와 함께 경로 데이터가 포함됩니다. 예를 들어 `http://localhost:5000/Edit/1`과 같은 형식입니다.

*Pages/Edit.cshtml* 파일은 다음과 같습니다.

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Edit.cshtml?highlight=1)]

첫 번째 줄에는 `@page "{id:int}"` 지시문이 작성되어 있습니다. 라우팅 제약 조건인 `"{id:int}"`는 `int` 경로 데이터가 포함된 이 페이지에 대한 요청만 허용하도록 페이지에 지시합니다. 페이지에 대한 요청에 `int`로 변환할 수 있는 경로 데이터가 없으면 런타임이 HTTP 404 (찾을 수 없음) 오류를 반환합니다. ID를 옵션으로 설정하려면 경로 제약 조건에 `?`를 추가하면 됩니다.

 ```cshtml
@page "{id:int?}"
```

*Pages/Edit.cshtml.cs* 파일은 다음과 같습니다.

[!code-cs[](index/sample/RazorPagesContacts/Pages/Edit.cshtml.cs)]

또한 *Index.cshtml* 파일에는 각 고객 연락처에 대한 삭제 버튼을 만들기 위한 태그가 포함되어 있습니다.

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=22-23)]

삭제 단추가 HTML로 렌더링될 때 해당 태그의 `formaction`에는 다음에 관한 매개 변수가 지정됩니다.

* `asp-route-id` 특성으로 지정된 고객 연락처의 ID.
* `asp-page-handler` 특성으로 지정된 `handler`

고객 연락처 ID `1`에 대해 렌더링된 삭제 단추의 예는 다음과 같습니다.

```html
<button type="submit" formaction="/?id=1&amp;handler=delete">delete</button>
```

단추를 선택하면 양식의 `POST` 요청이 서버로 전송됩니다. 규약에 따라 처리기 메서드의 이름은 `handler` 매개 변수의 값을 기반으로 `OnPost[handler]Async` 체계에 의해 선택됩니다.

이번 예제에서는 `handler`가 `delete`이므로 `POST` 요청을 처리하기 위해 `OnPostDeleteAsync` 처리기 메서드가 사용됩니다. `asp-page-handler`가 `remove` 같은 다른 값으로 설정되면 `OnPostRemoveAsync`라는 이름의 페이지 처리기 메서드가 선택됩니다.

[!code-cs[](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs?range=26-37)]

`OnPostDeleteAsync` 메서드는 다음 작업을 수행합니다.

* 쿼리 문자열에서 `id`를 가져옵니다.
* `FindAsync`를 사용하여 데이터베이스에서 고객 연락처를 쿼리합니다.
* 고객 연락처를 찾으면 고객 연락처 목록에서 제거합니다. 데이터베이스를 업데이트 합니다.
* `RedirectToPage`를 호출하여 루트 인덱스 페이지(`/Index`)로 리디렉션합니다.

::: moniker range=">= aspnetcore-2.1"

## <a name="mark-page-properties-as-required"></a>페이지 속성을 필수로 표시하기

`PageModel`의 속성에는 [Required](/dotnet/api/system.componentmodel.dataannotations.requiredattribute) 특성을 적용할 수 있습니다.

[!code-cs[](index/sample/Create.cshtml.cs?highlight=3,15-16)]

자세한 내용은 [모델 유효성 검사](xref:mvc/models/validation)를 참고하시기 바랍니다.

## <a name="manage-head-requests-with-the-onget-handler"></a>OnGet 처리기로 HEAD 요청 관리하기

HEAD 요청을 사용하면 특정 리소스의 헤더를 검색할 수 있습니다. GET 요청과는 달리 HEAD 요청은 응답 본문을 반환하지 않습니다.

일반적으로 HEAD 요청에 대한 HEAD 처리기를 만들고 호출합니다. 

```csharp
public void OnHead()
{
    HttpContext.Response.Headers.Add("HandledBy", "Handled by OnHead!");
}
```

만약 정의된 HEAD 처리기(`OnHead`)가 없다면 ASP.NET Core 2.1 이상에서는 Razor 페이지가 GET 페이지 처리기(`OnGet`) 호출로 대체합니다. ASP.NET Core 2.1 및 2.2에서 이 동작은 `Startup.Configure`의 [SetCompatibilityVersion](xref:mvc/compatibility-version)에 의해서 발생합니다.

```csharp
services.AddMvc()
    .SetCompatibilityVersion(Microsoft.AspNetCore.Mvc.CompatibilityVersion.Version_2_1);
```

기본 템플릿은 ASP.NET Core 2.1 및 2.2에서 `SetCompatibilityVersion` 호출을 생성합니다.

`SetCompatibilityVersion`은 효과적으로 Razor 페이지 옵션 `AllowMappingHeadRequestsToGetHandler`를 `true`로 설정합니다.

`SetCompatibilityVersion`을 사용하여 2.1의 모든 동작을 허용하는 대신 명시적으로 특정 동작을 허용할 수 있습니다. 다음 코드는 HEAD 요청을 GET 처리기로 매핑하는 것을 허용합니다.

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        options.AllowMappingHeadRequestsToGetHandler = true;
    });
```

::: moniker-end

<a name="xsrf"></a>

## <a name="xsrfcsrf-and-razor-pages"></a>XSRF/CSRF 및 Razor 페이지

[위조 방지 유효성 검사](xref:security/anti-request-forgery)에 대한 어떠한 코드도 작성할 필요가 없습니다. 위조 방지 토큰 생성 및 유효성 검사는 Razor 페이지에 자동으로 포함됩니다.

<a name="layout"></a>
## <a name="using-layouts-partials-templates-and-tag-helpers-with-razor-pages"></a>Razor 페이지에서 레이아웃, 부분 뷰, 템플릿 및 태그 도우미 사용하기

페이지는 Razor 뷰 엔진의 모든 기능과 함께 동작합니다. 레이아웃, 부분 뷰, 템플릿, 태그 도우미, *_ViewStart.cshtml*, *_ViewImports.cshtml*은 기존의 Razor 뷰와 동일한 방식으로 동작합니다.

이 기능들 중 일부를 활용하여 페이지를 개선해 보겠습니다.

::: moniker range=">= aspnetcore-2.1"

[레이아웃 페이지](xref:mvc/views/layout)를 *Pages/Shared/_Layout.cshtml*에 추가합니다.

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[레이아웃 페이지](xref:mvc/views/layout)를 *Pages/_Layout.cshtml*에 추가합니다.

::: moniker-end

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_LayoutSimple.cshtml)]

[레이아웃](xref:mvc/views/layout)은 다음과 같은 역할을 수행합니다.

* 각 페이지의 레이아웃을 제어합니다(페이지가 명시적으로 레이아웃을 사용하지 않는 경우 제외).
* JavaScript 및 스타일시트 같은 HTML 구조를 가져옵니다.

자세한 내용은 [레이아웃 페이지](xref:mvc/views/layout)를 참고하시기 바랍니다.

[Layout](xref:mvc/views/layout#specifying-a-layout) 속성은 *Pages/_ViewStart.cshtml*에서 설정됩니다.

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_ViewStart.cshtml)]

::: moniker range=">= aspnetcore-2.1"

레이아웃은 *Pages/Shared* 폴더에 위치합니다. 페이지는 현재 페이지와 동일한 폴더에서부터 시작하여 계층적으로 다른 뷰(레이아웃, 템플릿, 부분 뷰)들을 검색합니다. *Pages/Shared* 폴더의 레이아웃은 *Pages* 폴더 하위의 모든 Razor 페이지에서 사용할 수 있습니다.

레이아웃 파일은 *Pages/Shared* 폴더에 위치해야 합니다.

::: moniker-end

::: moniker range="= aspnetcore-2.0"

레이아웃은 *Pages* 폴더에 위치합니다. 페이지는 현재 페이지와 동일한 폴더에서부터 시작하여 계층적으로 다른 뷰들(레이아웃, 템플릿, 부분 뷰)을 검색합니다. *Pages* 폴더의 레이아웃은 *Pages* 폴더 하위의 모든 Razor 페이지에서 사용할 수 있습니다.

::: moniker-end

레이아웃 파일은 *Views/Shared* 폴더에 두지 **않는** 것이 좋습니다. *Views/Shared*는 MVC 뷰 패턴입니다. Razor 페이지는 경로 규약이 아닌 폴더 계층 구조를 사용해야 합니다.

Razor 페이지의 뷰 검색에는 *Pages* 폴더가 포함됩니다. MVC 컨트롤러 및 기존 Razor 뷰에서 사용 중인 레이아웃, 템플릿 및 부분 뷰는 *정상적으로 동작*합니다.

*Pages/_ViewImports.cshtml* 파일을 추가합니다.

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml)]

`@namespace`는 잠시 뒤에 설명합니다. `@addTagHelper` 지시문은 [기본 제공 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/Index)를 *Pages* 폴더의 모든 페이지에 도입합니다.

<a name="namespace"></a>

`@namespace` 지시문을 페이지에서 명시적으로 사용하면 다음과 같습니다.

[!code-cshtml[](index/sample/RazorPagesIntro/Pages/Customers/Namespace2.cshtml?highlight=2)]

이 지시문은 페이지에 대한 네임스페이스를 설정합니다. 이렇게 하면 `@model` 지시문은 네임스페이스를 포함할 필요가 없습니다.

`@namespace` 지시문이 *_ViewImports.cshtml*에 포함되어 있으면 지정된 네임스페이스가 `@namespace` 지시문을 가져오는 페이지에서 생성된 네임스페이스에 대한 접두사를 제공합니다. 생성된 네임스페이스의 나머지 부분(접미사 부분)은 *_ViewImports.cshtml*이 위치한 폴더와 페이지가 위치한 폴더 간의 점으로 구분된 상대 경로입니다.

예를 들어 `PageModel` 클래스 *Pages/Customers/Edit.cshtml.cs*는 네임스페이스를 명시적으로 설정합니다.

[!code-cs[](index/sample/RazorPagesContacts2/Pages/Customers/Edit.cshtml.cs?name=snippet_namespace)]

*Pages/_ViewImports.cshtml* 파일에서는 다음과 같이 네임스페이스를 설정합니다.

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml?highlight=1)]

*Pages/Customers/Edit.cshtml* Razor 페이지에 대해 생성되는 네임스페이스는 `PageModel` 클래스와 동일합니다.

`@namespace`*는 기존 Razor 뷰에서도 동작합니다.*

기존의 *Pages/Create.cshtml* 뷰 파일은 다음과 같습니다.

[!code-cshtml[](index/sample/RazorPagesContacts/Pages/Create.cshtml?highlight=2)]

변경된 *Pages/Create.cshtml* 뷰 파일은 다음과 같습니다.

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/Create.cshtml?highlight=2)]

[Razor 페이지 시작 프로젝트](#rpvs17)에는 클라이언트 측 유효성 검사를 연결하는 *Pages/_ValidationScriptsPartial.cshtml*이 포함되어 있습니다.

부분 뷰에 대한 자세한 내용은 <xref:mvc/views/partial>를 참고하시기 바랍니다.

<a name="url_gen"></a>

## <a name="url-generation-for-pages"></a>페이지에 대한 URL 생성하기

앞에서 살펴본 `Create` 페이지는 `RedirectToPage`를 사용합니다.

[!code-cs[](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync&highlight=10)]

예제 앱은 다음과 같은 파일/폴더 구조를 갖고 있습니다.

* */Pages*

  * *Index.cshtml*
  * */Customers*

    * *Create.cshtml*
    * *Edit.cshtml*
    * *Index.cshtml*

*Pages/Customers/Create.cshtml* 및 *Pages/Customers/Edit.cshtml* 페이지는 정상적으로 작업을 마친 후 *Pages/Index.cshtml*로 리디렉션됩니다. 문자열 `/Index`는 이전 페이지에 접근하기 위한 URI의 일부입니다. 문자열 `/Index`는 *Pages/Index.cshtml* 페이지에 대한 URI를 생성하기 위해 사용할 수 있습니다. 예들 들어 다음과 같습니다.

* `Url.Page("/Index", ...)`
* `<a asp-page="/Index">My Index Page</a>`
* `RedirectToPage("/Index")`

페이지 이름은 선행 `/`를 포함하는 루트 */Pages* 폴더로부터 시작되는 페이지에 대한 경로입니다(예: `/Index`). 위의 URL 생성 예제는 URL 하드 코딩에 비해 향상된 옵션과 기능적 성능을 제공합니다. URL 생성에는 [라우팅](xref:mvc/controllers/routing)이 사용되며 경로가 대상 경로에서 정의되는 방식에 따라 매개 변수를 생성하고 인코딩할 수 있습니다.

페이지에 대한 URL 생성은 상대적 이름을 지원합니다. 다음 표는 *Pages/Customers/Create.cshtml*에서 다른 `RedirectToPage` 매개 변수를 사용할 때 어떤 인덱스 페이지가 선택되는지를 보여줍니다.

| RedirectToPage(x)| 페이지 |
| ----------------- | ------------ |
| RedirectToPage("/Index") | *Pages/Index* |
| RedirectToPage("./Index") | *Pages/Customers/Index* |
| RedirectToPage("../Index") | *Pages/Index* |
| RedirectToPage("Index")  | *Pages/Customers/Index* |

`RedirectToPage("Index")`, `RedirectToPage("./Index")` 및 `RedirectToPage("../Index")`는 <em>상대적 이름</em>입니다. `RedirectToPage`의 매개 변수는 현재 페이지의 경로와 <em>결합</em>되어 대상 페이지의 이름을 계산합니다.  <!-- Review: Original had The provided string is combined with the page name of the current page to compute the name of the destination page.  page name, not page path -->

상대적 이름 연결은 구조가 복잡한 사이트를 만들때 유용합니다. 상대적 이름을 사용하여 한 폴더의 여러 페이지들을 연결하면 해당 폴더의 이름을 바꿀 수 있습니다. 그래도 여전히 모든 링크는 동작합니다(링크에 폴더 이름이 포함되어 있지 않기 때문입니다).

::: moniker range=">= aspnetcore-2.1"

## <a name="viewdata-attribute"></a>ViewData 특성

[ViewDataAttribute](/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute)를 사용하여 데이터를 페이지에 전달할 수 있습니다. `[ViewData]`가 지정된 컨트롤러나 Razor 페이지 모델의 속성은 [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary)에 값이 저장되고 로드됩니다.

다음 예제에서 `AboutModel`에는 `[ViewData]`가 지정된 `Title` 속성이 존재합니다. 이 `Title` 속성은 About 페이지의 제목으로 설정됩니다.

```csharp
public class AboutModel : PageModel
{
    [ViewData]
    public string Title { get; } = "About";

    public void OnGet()
    {
    }
}
```

정보 페이지에서는 모델의 속성으로 `Title` 속성에 접근합니다.

```cshtml
<h1>@Model.Title</h1>
```

레이아웃에서는 ViewData 사전으로부터 이 제목을 읽습니다.

```cshtml
<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ViewData["Title"] - WebApplication</title>
    ...
```

::: moniker-end

## <a name="tempdata"></a>TempData

ASP.NET Core는 [컨트롤러](/dotnet/api/microsoft.aspnetcore.mvc.controller)에서 [TempData](/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) 속성을 노출합니다. 이 속성은 해당 속성이 읽혀질 때까지만 데이터를 저장합니다. `Keep` 및 `Peek` 메서드를 사용하면 삭제하지 않고도 데이터를 확인할 수 있습니다. `TempData`는 두 단계 이상의 요청에 대한 데이터가 필요할 경우의 리디렉션에 유용합니다.

`[TempData]` 특성은 ASP.NET Core 2.0의 새로운 기능으로 컨트롤러 및 페이지에서 지원됩니다.

다음 코드는 `TempData`를 사용하여 `Message`의 값을 설정합니다.

[!code-cs[](index/sample/RazorPagesContacts2/Pages/Customers/CreateDot.cshtml.cs?highlight=10-11,25&name=snippet_Temp)]

*Pages/Customers/Index.cshtml* 파일의 다음 태그는 `TempData`를 사용하여 `Message` 값을 출력합니다.

```cshtml
<h3>Msg: @Model.Message</h3>
```

*Pages/Customers/Index.cshtml.cs* 페이지 모델은 `Message` 속성에 `[TempData]` 특성을 적용합니다.

```cs
[TempData]
public string Message { get; set; }
```

자세한 내용은 [TempData](xref:fundamentals/app-state#tempdata)를 참고하시기 바랍니다.

<a name="mhpp"></a>
## <a name="multiple-handlers-per-page"></a>한 페이지에 대한 여러 처리기

다음 페이지는 `asp-page-handler` 태그 도우미를 사용하여 두 개의 페이지 처리기에 대한 태그를 생성합니다.

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?highlight=12-13)]

<!-- Review: the FormActionTagHelper applies to all <form /> elements on a Razor page, even when there's no `asp-` attribute   -->

위 예제의 양식에는 두 개의 제출 단추가 존재하며, 각 단추는 `FormActionTagHelper`를 사용하여 서로 다른 URL로 제출됩니다. `asp-page-handler` 특성은 `asp-page`와 함께 사용됩니다. `asp-page-handler`는 페이지에 정의된 각 처리기 메서드로 제출되는 URL을 생성합니다. 이 예제의 경우 현재 페이지로 연결므로 `asp-page`는 지정되지 않았습니다.

페이지 모델은 다음과 같습니다.

[!code-cs[](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml.cs?highlight=20,32)]

이 코드는 *명명된 처리기 메서드*를 사용합니다. 명명된 처리기 메서드는 `On<HTTP Verb>` 뒤와 `Async`(있는 경우) 앞에 이름의 텍스트를 결합해서 만들어집니다. 위의 예제에서 페이지 메서드는 OnPost**JoinList**Async와 OnPost**JoinListUC**Async입니다. *OnPost* 및 *Async*가 제거된 처리기 이름은 `JoinList`와 `JoinListUC`입니다.

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?range=12-13)]

위의 코드를 사용할 경우 `OnPostJoinListAsync`에 제출되는 URL 경로는 `http://localhost:5000/Customers/CreateFATH?handler=JoinList`입니다. `OnPostJoinListUCAsync`에 제출되는 URL 경로는 `http://localhost:5000/Customers/CreateFATH?handler=JoinListUC`입니다.

## <a name="custom-routes"></a>사용자 지정 경로

`@page` 지시문을 사용하여 다음을 수행합니다.

* 페이지에 대한 사용자 지정 경로를 지정합니다. 예를 들어 `@page "/Some/Other/Path"`를 사용하여 About 페이지에 대한 경로를 `/Some/Other/Path`로 설정할 수 있습니다.
* 페이지의 기본 경로에 세그먼트를 추가합니다. 예를 들어 `@page "item"`을 사용하여 페이지의 기본 경로에 "item" 세그먼트를 추가할 수 있습니다.
* 페이지의 기본 경로에 매개 변수를 추가합니다. 예를 들어 `@page "{id}"`를 사용하여 ID 매개 변수 `id`를 페이지에 필수로 지정할 수 있습니다.

경로의 시작 부분에 물결표(`~`)로 지정된 루트 상대 경로가 지원됩니다. 예를 들어 `@page "~/Some/Other/Path"`은 `@page "/Some/Other/Path"`과 같습니다.

경로 템플릿 `@page "{handler?}"`를 지정하여 URL의 쿼리 문자열 `?handler=JoinList`를 경로 세그먼트 `/JoinList`로 변경할 수 있습니다.

URL에서 쿼리 문자열 `?handler=JoinList`를 사용하지 않으려면 경로를 변경하여 처리기 이름을 URL의 경로 부분에 넣습니다. `@page` 지시문 뒤에 큰따옴표로 묶은 경로 템플릿을 추가하여 경로를 사용자 지정할 수 있습니다.

[!code-cshtml[](index/sample/RazorPagesContacts2/Pages/Customers/CreateRoute.cshtml?highlight=1)]

이 코드를 사용할 경우 `OnPostJoinListAsync`에 제출되는 URL 경로는 `http://localhost:5000/Customers/CreateFATH/JoinList`입니다. `OnPostJoinListUCAsync`에 제출되는 URL 경로는 `http://localhost:5000/Customers/CreateFATH/JoinListUC`입니다.

`handler` 뒤의 `?`는 경로 매개 변수가 선택 사항임을 의미합니다.

## <a name="configuration-and-settings"></a>구성 및 설정하기

고급 옵션을 구성하려면 MVC 빌더에서 확장 메서드 `AddRazorPagesOptions`를 사용합니다.

[!code-cs[](index/sample/RazorPagesContacts/StartupAdvanced.cs?name=snippet_1)]

현재 `RazorPagesOptions`를 사용하여 페이지의 루트 디렉터리를 설정하거나 페이지에 대한 애플리케이션 모델 규칙을 추가할 수 있습니다. 앞으로 이 방식으로 더 많은 확장성을 지원할 예정입니다.

뷰를 미리 컴파일하려면 [Razor 뷰 컴파일](xref:mvc/views/view-compilation)을 참고하시기 바랍니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/index/sample).

본문의 소개에 따라 예제를 만들어보는 [Razor 페이지 시작하기](xref:tutorials/razor-pages/razor-pages-start)도 참고하시기 바랍니다.

### <a name="specify-that-razor-pages-are-at-the-content-root"></a>Razor 페이지를 콘텐츠 루트로 지정하기

기본적으로 Razor 페이지의 루트 경로는 */Pages* 디렉터리입니다. [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_)에 [WithRazorPagesAtContentRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.withrazorpagesatcontentroot)를 추가하여 Razor 페이지를 앱의 콘텐츠 루트([ContentRootPath](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.contentrootpath))로 지정합니다.

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        ...
    })
    .WithRazorPagesAtContentRoot();
```

### <a name="specify-that-razor-pages-are-at-a-custom-root-directory"></a>Razor 페이지가 사용자 지정 루트 디렉터리에 위치하도록 지정하기

[AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc#Microsoft_Extensions_DependencyInjection_MvcServiceCollectionExtensions_AddMvc_Microsoft_Extensions_DependencyInjection_IServiceCollection_)에 [WithRazorPagesRoot](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvccorebuilderextensions.withrazorpagesroot)를 추가하여 Razor 페이지가 앱의 사용자 지정 루트 디렉터리에 있도록 지정합니다(상대 경로 제공).

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
    {
        ...
    })
    .WithRazorPagesRoot("/path/to/razor/pages");
```

## <a name="additional-resources"></a>추가 자료

* <xref:index>
* <xref:mvc/views/razor>
* <xref:tutorials/razor-pages/razor-pages-start>
* <xref:security/authorization/razor-pages-authorization>
* <xref:razor-pages/razor-pages-conventions>
* <xref:test/razor-pages-tests>
* <xref:mvc/views/partial>
