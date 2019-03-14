---
title: ASP.NET Core의 앵커 태그 도우미
author: pkellner
description: ASP.NET Core 앵커 태그 도우미 특성 및 HTML 앵커 태그의 동작을 확장할 때 각 특성이 담당하는 역할을 확인합니다.
ms.author: scaddie
ms.custom: mvc
ms.date: 12/18/2018
uid: mvc/views/tag-helpers/builtin-th/anchor-tag-helper
ms.openlocfilehash: 60fa0c00e40878a8227ca2bc8bdb0bc2bf9f8336
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57033130"
---
# <a name="anchor-tag-helper-in-aspnet-core"></a>ASP.NET Core의 앵커 태그 도우미

작성자: [Peter Kellner](http://peterkellner.net) 및 [Scott Addie](https://github.com/scottaddie)

[앵커 태그 도우미](xref:Microsoft.AspNetCore.Mvc.TagHelpers.AnchorTagHelper)는 새 특성을 추가하여 표준 HTML 앵커(`<a ... ></a>`) 태그를 향상시킵니다. 규칙에 따라 해당 특성들의 이름은 `asp-` 접두사로 시작됩니다. 렌더링 된 앵커 요소의 `href` 특성값은 `asp-` 특성값에 따라 결정됩니다.

태그 도우미에 대한 개요는 <xref:mvc/views/tag-helpers/intro>를 참조하세요.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/tag-helpers/built-in/samples) ([다운로드 방법](xref:index#how-to-download-a-sample))

이 문서의 예제 전반에서는 다음의 *SpeakerController*가 사용됩니다. 

[!code-csharp[](samples/TagHelpersBuiltIn/Controllers/SpeakerController.cs?name=snippet_SpeakerController)]

`asp-` 특성의 목록은 다음과 같습니다.

## <a name="asp-controller"></a>asp-controller

[asp-controller](xref:Microsoft.AspNetCore.Mvc.TagHelpers.AnchorTagHelper.Controller*) 특성은 URL 생성에 사용되는 컨트롤러를 지정합니다. 다음 태그는 모든 스피커를 나열합니다.

[!code-cshtml[](samples/TagHelpersBuiltIn/Views/Home/Index.cshtml?name=snippet_AspController)]

생성된 HTML:

```html
<a href="/Speaker">All Speakers</a>
```

`asp-controller` 특성이 지정되고 `asp-action`이 지정되지 않았을 경우, 기본 `asp-action` 값은 현재 실행 중인 뷰와 연결된 컨트롤러 액션입니다. *HomeController*의 *Index* 뷰(*/Home*)에서 위의 태그에서 `asp-action`을 생략한 앵커 태그 도우미를 사용할 경우, 생성되는 HTML은 다음과 같습니다.

```html
<a href="/Home">All Speakers</a>
```

## <a name="asp-action"></a>asp-action

[asp-action](xref:Microsoft.AspNetCore.Mvc.TagHelpers.AnchorTagHelper.Action*) 특성값은 생성되는 `href` 특성에 포함될 컨트롤러 액션의 이름을 나타냅니다. 다음 태그는 생성된 `href` 특성값을 스피커 평가 페이지로 설정합니다.

[!code-cshtml[](samples/TagHelpersBuiltIn/Views/Home/Index.cshtml?name=snippet_AspAction)]

생성된 HTML:

```html
<a href="/Speaker/Evaluations">Speaker Evaluations</a>
```

`asp-controller` 특성을 지정하지 않으면 현재 뷰를 실행 중인 뷰를 호출하는 기본 컨트롤러가 사용됩니다.

`asp-action` 특성값이 `Index`면 URL에 아무런 액션도 추가되지 않으며 기본 `Index` 액션이 호출됩니다. 지정된 (또는 기본값으로 설정된) 액션은 `asp-controller`에서 참조되는 컨트롤러에 존재해야 합니다. 

## <a name="asp-route-value"></a>asp-route-{value}

[asp-route-{value}](xref:Microsoft.AspNetCore.Mvc.TagHelpers.AnchorTagHelper.RouteValues*) 특성을 사용하면 와일드카드 경로 접두사를 사용할 수 있습니다. `{value}` 자리 표시자에 위치하는 모든 값은 잠재적인 경로 매개 변수로 해석됩니다.  기본 경로가 발견되지 않으면 이 경로 접두사는 생성되는 `href` 특성에 요청 매개 변수 및 값으로 추가됩니다. 그렇지 않으면 경로 템플릿에서 이 경로 접두사가 대체됩니다.

다음 컨트롤러 액션을 살펴보시기 바랍니다.

[!code-csharp[](samples/TagHelpersBuiltIn/Controllers/BuiltInTagController.cs?name=snippet_AnchorTagHelperAction)]

*Startup.Configure*에 정의된 기본 경로 템플릿을 사용할 경우: 

[!code-csharp[](samples/TagHelpersBuiltIn/Startup.cs?name=snippet_UseMvc&highlight=8-10)]

다음 MVC 뷰는 액션을 통해서 제공되는 모델을 사용합니다.

```cshtml
@model Speaker
<!DOCTYPE html>
<html>
<body>
    <a asp-controller="Speaker"
       asp-action="Detail" 
       asp-route-id="@Model.SpeakerId">SpeakerId: @Model.SpeakerId</a>
</body>
</html>
```

이 경우 기본 경로의 `{id?}` 자리 표시자가 일치합니다. 생성된 HTML:

```html
<a href="/Speaker/Detail/12">SpeakerId: 12</a>
```

이번에는 다음 MVC 뷰와 같이 경로 접두사가 라우팅 템플릿의 일부와 일치하지 않는다고 가정해보겠습니다.

```cshtml
@model Speaker
<!DOCTYPE html>
<html>
<body>
    <a asp-controller="Speaker"
       asp-action="Detail"
       asp-route-speakerid="@Model.SpeakerId">SpeakerId: @Model.SpeakerId</a>
<body>
</html>
```

일치하는 경로에서 `speakerid`를 찾을 수 없기 때문에 생성된 HTML은 다음과 같습니다.

```html
<a href="/Speaker/Detail?speakerid=12">SpeakerId: 12</a>
```

`asp-controller` 또는 `asp-action`이 지정되지 않으면 `asp-route` 특성과 동일한 기본 처리가 그대로 수행됩니다.

## <a name="asp-route"></a>asp-route

[asp-route](xref:Microsoft.AspNetCore.Mvc.TagHelpers.AnchorTagHelper.Route*) 특성은 명명된 경로에 직접 연결되는 URL을 생성하기 위해서 사용됩니다. [라우팅 특성](xref:mvc/controllers/routing#attribute-routing)을 사용하면 경로가 `SpeakerController`에 표시된 이름으로 지정되고 해당 `Evaluations` 메서드에서 사용할 수 있습니다.

[!code-csharp[](samples/TagHelpersBuiltIn/Controllers/SpeakerController.cs?range=22-24)]

다음 태그에서 `asp-route` 특성은 명명된 경로를 참조합니다.

[!code-cshtml[](samples/TagHelpersBuiltIn/Views/Home/Index.cshtml?name=snippet_AspRoute)]

앵커 태그 도우미는 */Speaker/Evaluations* URL을 사용하여 해당 컨트롤러 액션을 직접 가리키는 경로를 생성합니다. 생성된 HTML:

```html
<a href="/Speaker/Evaluations">Speaker Evaluations</a>
```

`asp-route` 와 `asp-controller` 또는 `asp-action` 을 동시에 지정하면 기대하는 것과 다른 경로가 생성될 수 있습니다. 경로 충돌을 방지하려면 `asp-route`를 `asp-controller` 및 `asp-action` 특성과 함께 사용하지 않아야 합니다. 

## <a name="asp-all-route-data"></a>asp-all-route-data

[asp-all-route-data](xref:Microsoft.AspNetCore.Mvc.TagHelpers.AnchorTagHelper.RouteValues*) 특성은 키-값 쌍 사전을 만들 수 있도록 지원해줍니다. 키는 매개 변수 이름이고, 값은 매개 변수값입니다.

다음 예제에서는 사전이 초기화되어 Razor 뷰로 전달됩니다. 또는 모델을 사용하여 데이터를 전달할 수도 있습니다.

[!code-cshtml[](samples/TagHelpersBuiltIn/Views/Home/Index.cshtml?name=snippet_AspAllRouteData)]

위의 코드로 생성되는 HTML은 다음과 같습니다.

```html
<a href="/Speaker/EvaluationsCurrent?speakerId=11&currentYear=true">Speaker Evaluations</a>
```

`asp-all-route-data` 사전은 투영되어 오버로드된 `Evaluations` 액션의 요구 사항을 충족하는 쿼리 문자열을 생성합니다.

[!code-csharp[](samples/TagHelpersBuiltIn/Controllers/SpeakerController.cs?range=26-30)]

사전에 존재하는 키가 경로 매개 변수와 일치하면 경로에서 해당 값이 적절하게 대체됩니다. 반면 일치하지 않는 다른 값은 요청 매개 변수로 생성됩니다.

## <a name="asp-fragment"></a>asp-fragment

[asp-fragment](xref:Microsoft.AspNetCore.Mvc.TagHelpers.AnchorTagHelper.Fragment*) 특성은 URL에 추가할 URL 조각을 정의합니다. 앵커 태그 도우미는 해시 문자(#)를 추가합니다. 다음 태그를 살펴보시기 바랍니다.

[!code-cshtml[](samples/TagHelpersBuiltIn/Views/Home/Index.cshtml?name=snippet_AspFragment)]

생성된 HTML:

```html
<a href="/Speaker/Evaluations#SpeakerEvaluations">Speaker Evaluations</a>
```

해시 태그는 클라이언트 측 앱을 만들 때 유용합니다. 예를 들어 JavaScript에서 손쉽게 표시하고 검색하는 데 사용할 수 있습니다.

## <a name="asp-area"></a>asp-area

[asp-area](xref:Microsoft.AspNetCore.Mvc.TagHelpers.AnchorTagHelper.Area*) 특성은 적절한 경로를 설정하기 위해 사용되는 영역 이름을 설정합니다. 다음 예제에서는 `asp-area` 특성으로 인해 경로가 다시 매핑되는 방식을 보여 줍니다.

### <a name="usage-in-razor-pages"></a>Razor Pages에서 사용

Razor Pages 영역은 ASP.NET Core 2.1 이상에서 지원됩니다.

다음 디렉터리 계층 구조를 고려합니다.

* **{Project name}**
  * **wwwroot**
  * **Areas**
    * **세션**
      * **페이지**
        * *\_ViewStart.cshtml*
        * *Index.cshtml*
        * *Index.cshtml.cs*
  * **페이지**

*세션* 영역 *인덱스* Razor Page를 참조하는 태그는 다음과 같습니다.

[!code-cshtml[](samples/TagHelpersBuiltIn/Views/Home/Index.cshtml?name=snippet_AspAreaRazorPages)]

생성된 HTML:

```html
<a href="/Sessions">View Sessions</a>
```

> [!TIP]
> Razor Pages 앱의 영역을 지원하려면 `Startup.ConfigureServices`에서 다음 중 하나를 수행합니다.
>
> * [호환성 버전](xref:mvc/compatibility-version)을 2.1 이상으로 설정합니다.
> * [RazorPagesOptions.AllowAreas](xref:Microsoft.AspNetCore.Mvc.RazorPages.RazorPagesOptions.AllowAreas*) 속성을 `true`로 설정합니다.
>
>   [!code-csharp[](samples/TagHelpersBuiltIn/Startup.cs?name=snippet_AllowAreas)]

### <a name="usage-in-mvc"></a>MVC에서의 사용법

다음 디렉터리 계층 구조를 고려합니다.

* **{Project name}**
  * **wwwroot**
  * **Areas**
    * **Blogs**
      * **Controllers**
        * *HomeController.cs*
      * **Views**
        * **Home**
          * *AboutBlog.cshtml*
          * *Index.cshtml*
        * *\_ViewStart.cshtml*
  * **Controllers**

`asp-area`를 "Blogs"로 설정하면 이 앵커 태그에 연결된 컨트롤러 및 뷰의 경로에 *Areas/Blogs* 디렉터리가 접두사로 추가됩니다. *AboutBlog* 보기를 참조하는 태그는 다음과 같습니다.

[!code-cshtml[](samples/TagHelpersBuiltIn/Views/Home/Index.cshtml?name=snippet_AspArea)]

생성된 HTML:

```html
<a href="/Blogs/Home/AboutBlog">About Blog</a>
```

> [!TIP]
> MVC 앱의 영역을 지원하려면 경로 템플릿에 해당 영역에 대한 참조가 포함되어야 합니다(존재할 경우). 해당 템플릿은 *Startup.Configure*에서 `routes.MapRoute` 메서드 호출의 두 번째 매개 변수로 표시됩니다.
>
> [!code-csharp[](samples/TagHelpersBuiltIn/Startup.cs?name=snippet_UseMvc&highlight=5)]

## <a name="asp-protocol"></a>asp-protocol

[asp-protocol](xref:Microsoft.AspNetCore.Mvc.TagHelpers.AnchorTagHelper.Protocol*) 특성은 URL의 프로토콜(예: `https`)을 지정하는 데 사용됩니다. 예를 들어:

[!code-cshtml[](samples/TagHelpersBuiltIn/Views/Home/Index.cshtml?name=snippet_AspProtocol)]

생성된 HTML:

```html
<a href="https://localhost/Home/About">About</a>
```

예제의 호스트 이름은 localhost입니다. 앵커 태그 도우미는 URL을 생성할 때 웹 사이트의 공용 도메인을 사용합니다.

## <a name="asp-host"></a>asp-host

[asp-host](xref:Microsoft.AspNetCore.Mvc.TagHelpers.AnchorTagHelper.Host*) 특성은 URL의 호스트 이름을 지정하는 데 사용됩니다. 예를 들어:

[!code-cshtml[](samples/TagHelpersBuiltIn/Views/Home/Index.cshtml?name=snippet_AspHost)]

생성된 HTML:

```html
<a href="https://microsoft.com/Home/About">About</a>
```

## <a name="asp-page"></a>asp-page

[asp-page](xref:Microsoft.AspNetCore.Mvc.TagHelpers.AnchorTagHelper.Page*) 특성은 Razor 페이지와 함께 사용됩니다. 이 특성은 앵커 태그의 `href` 특성값을 특정 페이지로 설정하기 위해서 사용됩니다. 페이지 이름 앞에 슬래시("/")를 접두사로 사용해서 URL을 생성합니다.

다음 예제는 참석자 Razor 페이지를 가리킵니다.

[!code-cshtml[](samples/TagHelpersBuiltIn/Views/Home/Index.cshtml?name=snippet_AspPage)]

생성된 HTML:

```html
<a href="/Attendee">All Attendees</a>
```

`asp-page` 특성은 `asp-route`, `asp-controller` 및 `asp-action` 특성과 함께 사용할 수 없습니다. 그러나 다음 태그에서 볼 수 있는 것처럼 `asp-page`는 `asp-route-{value}`와 함께 사용해서 라우팅을 제어할 수 있습니다.

[!code-cshtml[](samples/TagHelpersBuiltIn/Views/Home/Index.cshtml?name=snippet_AspPageAspRouteId)]

생성된 HTML:

```html
<a href="/Attendee?attendeeid=10">View Attendee</a>
```

## <a name="asp-page-handler"></a>asp-page-handler

[asp-page-handler](xref:Microsoft.AspNetCore.Mvc.TagHelpers.AnchorTagHelper.PageHandler*) 특성은 Razor 페이지와 함께 사용됩니다. 이 특성을 특정 페이지 처리기에 연결하기 위한 것입니다.

다음 페이지 처리기를 살펴보시기 바랍니다.

[!code-csharp[](samples/TagHelpersBuiltIn/Pages/Attendee.cshtml.cs?name=snippet_OnGetProfileHandler)]

페이지 모델의 관련 태그는 `OnGetProfile` 페이지 처리기에 연결됩니다. 페이지 처리기 메서드 이름의 `On<Verb>` 접두사는 `asp-page-handler` 특성값에서 생략됩니다. 메서드가 비동기화되면 `Async` 접미사도 생략됩니다.

[!code-cshtml[](samples/TagHelpersBuiltIn/Views/Home/Index.cshtml?name=snippet_AspPageHandler)]

생성된 HTML:

```html
<a href="/Attendee?attendeeid=12&handler=Profile">Attendee Profile</a>
```

## <a name="additional-resources"></a>추가 자료

* <xref:mvc/controllers/areas>
* <xref:razor-pages/index>
* <xref:mvc/compatibility-version>
