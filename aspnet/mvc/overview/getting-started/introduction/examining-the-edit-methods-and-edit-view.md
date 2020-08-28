---
uid: mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
title: 편집 메서드 및 편집 보기 검사 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/06/2019
ms.assetid: 52a4d5fe-aa31-4471-b3cb-a064f82cb791
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 1894971430c4febee19f095373411ed319edc015
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045210"
---
# <a name="examining-the-edit-methods-and-edit-view"></a>편집 메서드 및 편집 보기 검사

[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

이 섹션에서는 `Edit` 동영상 컨트롤러에 대해 생성 된 작업 메서드 및 뷰를 검사 합니다. 하지만 먼저, 릴리스 날짜를 보다 정확 하 게 표시 하기 위해 짧은 diversion를 사용 합니다. *Models\Movie.cs* 파일을 열고 아래에 표시 된 강조 표시 된 줄을 추가 합니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cs?highlight=2,12-14)]

날짜 문화권이 다음과 같이 지정 될 수도 있습니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs?highlight=3)]

다음 자습서에서는 [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)를 다룹니다. [Display](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayattribute.aspx) 특성은 필드의 이름으로 표시할 내용을 지정합니다(이 경우 "ReleaseDate" 대신 "Release Date") [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성은 데이터의 유형을 지정 합니다 .이 경우 날짜 이므로 필드에 저장 된 시간 정보가 표시 되지 않습니다. 날짜 형식을 잘못 렌더링 하는 Chrome 브라우저의 버그에는 [Displayformat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 특성이 필요 합니다.

응용 프로그램을 실행 하 고 컨트롤러를 찾습니다 `Movies` . **편집** 링크 위에 마우스 포인터를 놓으면 링크 되는 URL을 볼 수 있습니다.

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

Views\Movies\Index.cshtml 뷰의 메서드에서 **편집** 링크를 생성 했습니다 `Html.ActionLink` . *Views\Movies\Index.cshtml*

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

![Html.ActionLink](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html`개체는 [system.web](https://msdn.microsoft.com/library/gg402107(VS.98).aspx) 의 속성을 사용 하 여 노출 되는 도우미입니다. `ActionLink`도우미의 메서드를 사용 하면 컨트롤러에서 작업 메서드에 연결 되는 HTML 하이퍼링크를 쉽게 동적으로 생성할 수 있습니다. 메서드의 첫 번째 인수는 `ActionLink` 렌더링할 링크 텍스트입니다 (예: `<a>Edit Me</a>` ). 두 번째 인수는 호출할 동작 메서드의 이름 (이 경우 `Edit` 작업)입니다. 마지막 인수는 경로 데이터를 생성 하는 [익명 개체](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) 입니다 (이 경우 ID 4).

이전 이미지에 표시 된 링크는 `http://localhost:1234/Movies/Edit/4` 입니다. 기본 경로 ( *App \_ Start\RouteConfig.cs*에서 설정)는 URL 패턴을 사용 합니다 `{controller}/{action}/{id}` . 따라서 ASP.NET는 `http://localhost:1234/Movies/Edit/4` `Edit` `Movies` 매개 변수가 4 인 컨트롤러의 작업 메서드에 대 한 요청으로 변환 됩니다 `ID` . *앱 \_ Start\RouteConfig.cs* 파일에서 다음 코드를 검사 합니다. [Maproute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) 메서드는 HTTP 요청을 올바른 컨트롤러 및 작업 메서드로 라우팅하고 선택적 ID 매개 변수를 제공 하는 데 사용 됩니다. [Maproute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) 메서드는 [HtmlHelpers](https://msdn.microsoft.com/library/system.web.mvc.htmlhelper(v=vs.108).aspx) `ActionLink` 컨트롤러, 작업 메서드 및 경로 데이터를 지정 하 여 url을 생성 하는 등의 htmlhelpers도 사용 합니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cs?highlight=7)]

쿼리 문자열을 사용 하 여 동작 메서드 매개 변수를 전달할 수도 있습니다. 예를 들어 URL은 `http://localhost:1234/Movies/Edit?ID=3` 3의 매개 변수를 `ID` `Edit` 컨트롤러의 작업 메서드로 전달 합니다 `Movies` .

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

컨트롤러를 엽니다 `Movies` . 두 `Edit` 작업 메서드는 다음과 같습니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs?highlight=19-21)]

두 번째 `Edit` 작업 메서드 앞에 `HttpPost` 특성이 지정되어 있는 것에 유의하세요. 이 특성은 `Edit` POST 요청에 대해서만 메서드의 오버 로드를 호출할 수 있도록 지정 합니다. `HttpGet`특성을 첫 번째 edit 메서드에 적용할 수 있지만 이것이 기본값 이기 때문에 필요 하지 않습니다. (특성을 메서드로 명시적으로 할당 하는 작업 메서드를 참조 `HttpGet` `HttpGet` 합니다.) [Bind](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) 특성은 해커가 데이터를 모델에 과도 하 게 게시 하는 것을 막는 또 다른 중요 한 보안 메커니즘입니다. 변경 하려는 바인드 특성에만 속성을 포함 해야 합니다. 과도 한 게시 및 [보안](https://go.microsoft.com/fwlink/?LinkId=317598)정보에 대 한 바인딩 특성을 읽을 수 있습니다. 이 자습서에서 사용 되는 단순 모델에서는 모델의 모든 데이터를 바인딩합니다. [ValidateAntiForgeryToken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) 특성은 요청 위조를 방지 하는 데 사용 되며 `@Html.AntiForgeryToken()` 편집 뷰 파일 (*Views\Movies\Edit.cshtml*)에서와 쌍을 이룹니다. 일부는 아래와 같습니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cshtml?highlight=9)]

`@Html.AntiForgeryToken()` 컨트롤러의 메서드에서 일치 해야 하는 숨겨진 폼 위조 방지 토큰을 생성 합니다 `Edit` `Movies` . [MVC의 XSRF/Csrf 예방](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)자습서에서 교차 사이트 요청 위조 (XSRF 또는 csrf 라고도 함)에 대해 자세히 알아볼 수 있습니다.

`HttpGet` `Edit` 메서드는 movie ID 매개 변수를 사용 하 고, Entity Framework 메서드를 사용 하 여 동영상을 조회 하 `Find` 고, 선택 된 동영상을 편집 보기로 반환 합니다. 동영상을 찾을 수 없는 경우 [Httpnotfound](https://msdn.microsoft.com/library/gg453938(VS.98).aspx) 가 반환 됩니다. 스캐폴딩 시스템은 Edit 보기를 만들 때 `Movie` 클래스를 검토하고 클래스의 각 속성에 대해 `<label>` 및 `<input>` 요소를 렌더링하기 위한 코드를 만들었습니다. 다음 예제에서는 visual studio 스 캐 폴딩 시스템에서 생성 된 편집 뷰를 보여 줍니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

뷰 템플릿에는 `@model MvcMovie.Models.Movie` 파일 위쪽에 문이 포함 되어 있습니다 .이는 뷰에서 뷰 템플릿의 모델을 형식으로 예상 하도록 지정 합니다 `Movie` .

스 캐 폴드 코드는 몇 가지 *도우미 메서드* 를 사용 하 여 HTML 태그를 간소화 합니다. [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx)도우미는 필드 이름 ( &quot; 제목 &quot; , &quot; releasedate &quot; , &quot; 장르 &quot; 또는 &quot; Price &quot; )을 표시 합니다. [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx)도우미는 HTML 요소를 렌더링 합니다 `<input>` . [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx)도우미는 해당 속성과 연결 된 유효성 검사 메시지를 표시 합니다.

응용 프로그램을 실행 하 고 */영화* URL로 이동 합니다. **Edit** 링크를 클릭합니다. 브라우저에서 페이지의 소스를 봅니다. Form 요소의 HTML은 다음과 같습니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cshtml?highlight=1-2)]

`<input>`요소는 `<form>` `action` */Movies/Edit* URL에 post로 설정 된 특성이 있는 HTML 요소에 있습니다. **저장** 단추를 클릭 하면 폼 데이터가 서버에 게시 됩니다. 두 번째 줄은 호출로 생성 된 숨겨진 [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) 토큰을 보여 줍니다 `@Html.AntiForgeryToken()` .

## <a name="processing-the-post-request"></a>POST 요청 처리

다음 목록은 `Edit` 작업 메서드의 `HttpPost` 버전을 보여줍니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

[ValidateAntiForgeryToken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) 특성은 뷰에서 호출에 의해 생성 된 [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) 토큰의 유효성을 검사 `@Html.AntiForgeryToken()` 합니다.

[ASP.NET MVC 모델 바인더](https://msdn.microsoft.com/library/dd410405.aspx) 는 게시 된 양식 값을 사용 하 고 `Movie` 매개 변수로 전달 되는 개체를 만듭니다 `movie` . 는 `ModelState.IsValid` 폼에 제출 된 데이터를 사용 하 여 개체를 수정 (편집 또는 업데이트) 할 수 있는지 확인 합니다 `Movie` . 데이터가 유효 하면 동영상 데이터가 `Movies` `db` (인스턴스)의 컬렉션에 저장 됩니다 `MovieDBContext` . 새 동영상 데이터는의 메서드를 호출 하 여 데이터베이스에 저장 됩니다 `SaveChanges` `MovieDBContext` . 데이터를 저장한 후 코드는 사용자를 `MoviesController` 클래스의 `Index` 작업 메서드로 다시 전달하며, 여기에서는 방금 수행한 변경 사항을 포함한 영화 컬렉션이 표시됩니다.

클라이언트 쪽 유효성 검사에서 필드의 값이 잘못 된 것으로 확인 되는 즉시 오류 메시지가 표시 됩니다. JavaScript를 사용 하지 않도록 설정 하면 클라이언트 쪽 유효성 검사가 사용 되지 않습니다. 그러나 서버는 게시 된 값이 유효 하지 않은 것을 감지 하 고 양식 값이 오류 메시지와 함께 다시 표시 됩니다.

유효성 검사는 자습서의 뒷부분에서 자세히 검토 합니다.

`Html.ValidationMessageFor` *편집. cshtml* 뷰 템플릿의 도우미는 적절 한 오류 메시지를 표시 합니다.

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

모든 `HttpGet` 메서드는 비슷한 패턴을 따릅니다. 동영상 개체 (또는의 경우 개체 목록)를 가져오고 `Index` 모델을 뷰에 전달 합니다. `Create`메서드는 빈 동영상 개체를 만들기 뷰에 전달 합니다. 생성, 편집, 삭제 또는 어떤 식으로든 데이터를 수정하는 모든 메서드는 메서드의 `HttpPost` 오버로드에서 해당 작업을 수행합니다. HTTP GET 메서드에서 데이터를 수정 하는 것은 ASP.NET MVC 팁 #46의 블로그 게시물 항목에 설명 된 것 처럼 보안 위험입니다. [보안 허점을 만들기 때문에 삭제 링크를 사용 하지 마세요](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx). GET 메서드에서 데이터를 수정 하면 HTTP 모범 사례와 구조적 [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer) 패턴이 위반 되어 get 요청이 응용 프로그램의 상태를 변경 하지 않도록 지정 합니다. 다시 말해 GET 작업 수행은 부작용 없이 안전하고 영속 데이터를 수정하지 않는 방법으로 이루어져야 합니다.

## <a name="jquery-validation-for-non-english-locales"></a>영어가 아닌 로캘에 대 한 jQuery 유효성 검사

미국-영어 컴퓨터를 사용 하는 경우이 섹션을 건너뛰고 다음 자습서로 이동할 수 있습니다. [여기](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=16475)에서이 자습서의 세계화 버전을 다운로드할 수 있습니다. 국제화에 대 한 뛰어난 두 부분 자습서는 [Nadeem 's ASP.NET MVC 5 국제화](http://afana.me/post/aspnet-mvc-internationalization.aspx)를 참조 하세요.

> [!NOTE]
> 소수점에 쉼표 (,)를 사용 하는 영어가 아닌 로캘 및 미국 영어가 아닌 날짜 형식에 대해 jQuery 유효성 검사를 지원 하려면 &quot; &quot; 사용할 *globalize.js* 및 특정 *문화/globalize.cultures.js* 파일 (부터 [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) 및 JavaScript를 포함 해야 합니다 `Globalize.parseFloat` . NuGet에서 jQuery 영어가 아닌 유효성 검사를 가져올 수 있습니다. 영어 로캘을 사용 하는 경우에는 세계화를 설치 하지 마세요.

1. **도구** 메뉴에서 **nuget 패키지 관리자**를 클릭 한 다음 **솔루션에 대 한 nuget 패키지 관리**를 클릭 합니다.

    ![](examining-the-edit-methods-and-edit-view/_static/image5.png)
2. 왼쪽 창에서 찾아보기를 선택 <strong>*합니다.</strong> * 아래 이미지를 참조 하세요.
3. 입력 상자에 * 전역화 * *를 입력 합니다.

    ![](examining-the-edit-methods-and-edit-view/_static/image6.png)`jQuery.Validation.Globalize`을 선택 하 `MvcMovie` 고 **설치**를 클릭 합니다. *Scripts\jquery.globalize\globalize.js* 파일이 프로젝트에 추가 됩니다. * Scripts\jquery.globalize\cultures 폴더에는 \* 많은 문화 JavaScript 파일이 포함 됩니다. 이 패키지를 설치 하는 데 5 분 정도 걸릴 수 있습니다.

   다음 코드는 Views\Movies\Edit.cshtml 파일에 대 한 수정 사항을 보여 줍니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

모든 편집 보기에서이 코드를 반복 하지 않으려면 레이아웃 파일로 이동할 수 있습니다. 스크립트 다운로드를 최적화 하려면 내 자습서 [묶음 및 축소](../../performance/bundling-and-minification.md)를 참조 하세요.

자세한 내용은 [ASP.NET MVC 3 국제화](http://afana.me/post/aspnet-mvc-internationalization.aspx) 및 [ASP.NET mvc 3 국제화-2 부 (공동의 ddinner)](http://afana.me/post/aspnet-mvc-internationalization-part-2.aspx)를 참조 하세요.

임시 픽스로, 로캘에서 유효성 검사를 수행할 수 없는 경우 컴퓨터에서 미국 영어를 사용 하도록 강제 하거나 브라우저에서 JavaScript를 사용 하지 않도록 설정할 수 있습니다. 컴퓨터에서 미국 영어를 사용 하도록 하려면 프로젝트 루트 *web.config* 파일에 전역화 요소를 추가 하면 됩니다. 다음 코드에서는 문화권이 미국 영어로 설정 된 세계화 요소를 보여 줍니다.

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample11.xml)]

<a id="gettingstarted"></a><a id="jQueryAjaxJSON"></a> 다음 자습서에서는 검색 기능을 구현 합니다.

> [!div class="step-by-step"]
> [이전](accessing-your-models-data-from-a-controller.md)
> [다음](adding-search.md)
