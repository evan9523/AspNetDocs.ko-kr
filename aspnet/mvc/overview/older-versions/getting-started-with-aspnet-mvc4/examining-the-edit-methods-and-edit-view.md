---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
title: 편집 메서드 및 편집 보기 검사 | Microsoft Docs
author: Rick-Anderson
description: 참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013를 사용 하는 여기에서 사용할 수 있습니다. 보다 안전 하 고, 보다 간단 하 고 데모를 수행 하는 것이 더 간단 합니다.
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 41eb99ca-e88f-4720-ae6d-49a958da8116
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 85ad9a5758d70b5fe4ed792efb80217d7b3e2132
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "86163055"
---
# <a name="examining-the-edit-methods-and-edit-view"></a>편집 메서드 및 편집 보기 검사

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > ASP.NET MVC 5와 Visual Studio 2013를 사용 하는이 자습서의 업데이트 된 버전 [을 사용할 수 있습니다.](../../getting-started/introduction/getting-started.md) 더 안전 하 고 더 간단 하 고 더 많은 기능을 보여 줍니다.

이 섹션에서는 동영상 컨트롤러에 대해 생성 된 작업 메서드 및 뷰를 검사 합니다. 그런 다음 사용자 지정 검색 페이지를 추가 합니다.

응용 프로그램을 실행 하 고 `Movies` 브라우저의 주소 표시줄에 있는 URL에 */sourcea* 를 추가 하 여 컨트롤러를 찾습니다. **편집** 링크 위에 마우스 포인터를 놓으면 링크 되는 URL을 볼 수 있습니다.

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

Views\Movies\Index.cshtml 뷰의 메서드에서 **편집** 링크를 생성 했습니다 `Html.ActionLink` . *Views\Movies\Index.cshtml*

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

![Html.ActionLink](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html`개체는 [system.web](https://msdn.microsoft.com/library/gg402107(VS.98).aspx) 의 속성을 사용 하 여 노출 되는 도우미입니다. `ActionLink`도우미의 메서드를 사용 하면 컨트롤러에서 작업 메서드에 연결 되는 HTML 하이퍼링크를 쉽게 동적으로 생성할 수 있습니다. 메서드의 첫 번째 인수는 `ActionLink` 렌더링할 링크 텍스트입니다 (예: `<a>Edit Me</a>` ). 두 번째 인수는 호출할 동작 메서드의 이름입니다. 마지막 인수는 경로 데이터를 생성 하는 [익명 개체](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) 입니다 (이 경우 ID 4).

이전 이미지에 표시 된 링크는 `http://localhost:xxxxx/Movies/Edit/4` 입니다. 기본 경로 ( *App \_ Start\RouteConfig.cs*에서 설정)는 URL 패턴을 사용 합니다 `{controller}/{action}/{id}` . 따라서 ASP.NET는 `http://localhost:xxxxx/Movies/Edit/4` `Edit` `Movies` 매개 변수가 4 인 컨트롤러의 작업 메서드에 대 한 요청으로 변환 됩니다 `ID` . *앱 \_ Start\RouteConfig.cs* 파일에서 다음 코드를 검사 합니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs)]

쿼리 문자열을 사용 하 여 동작 메서드 매개 변수를 전달할 수도 있습니다. 예를 들어 URL은 `http://localhost:xxxxx/Movies/Edit?ID=4` 매개 변수 4를 `ID` `Edit` 컨트롤러의 동작 메서드에 전달 합니다 `Movies` .

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

컨트롤러를 엽니다 `Movies` . 두 `Edit` 작업 메서드는 다음과 같습니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cs)]

두 번째 `Edit` 작업 메서드 앞에 `HttpPost` 특성이 지정되어 있는 것에 유의하세요. 이 특성은 `Edit` POST 요청에 대해서만 메서드의 오버 로드를 호출할 수 있도록 지정 합니다. `HttpGet`특성을 첫 번째 edit 메서드에 적용할 수 있지만 이것이 기본값 이기 때문에 필요 하지 않습니다. (특성을 메서드로 명시적으로 할당 하는 작업 메서드를 참조 `HttpGet` `HttpGet` 합니다.)

`HttpGet` `Edit` 메서드는 movie ID 매개 변수를 사용 하 고, Entity Framework 메서드를 사용 하 여 동영상을 조회 하 `Find` 고, 선택 된 동영상을 편집 보기로 반환 합니다. [default value](https://msdn.microsoft.com/library/dd264739.aspx) `Edit` 메서드가 매개 변수 없이 호출 되는 경우 ID 매개 변수는 기본값 0을 지정 합니다. 동영상을 찾을 수 없는 경우 [Httpnotfound](https://msdn.microsoft.com/library/gg453938(VS.98).aspx) 가 반환 됩니다. 스캐폴딩 시스템은 Edit 보기를 만들 때 `Movie` 클래스를 검토하고 클래스의 각 속성에 대해 `<label>` 및 `<input>` 요소를 렌더링하기 위한 코드를 만들었습니다. 다음 예에서는 생성 된 편집 뷰를 보여 줍니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cshtml)]

뷰 템플릿에는 `@model MvcMovie.Models.Movie` 파일 위쪽에 문이 포함 되어 있습니다 .이는 뷰에서 뷰 템플릿의 모델을 형식으로 예상 하도록 지정 합니다 `Movie` .

스 캐 폴드 코드는 몇 가지 *도우미 메서드* 를 사용 하 여 HTML 태그를 간소화 합니다. [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx)도우미는 필드 이름 ( &quot; 제목 &quot; , &quot; releasedate &quot; , &quot; 장르 &quot; 또는 &quot; Price &quot; )을 표시 합니다. [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx)도우미는 HTML 요소를 렌더링 합니다 `<input>` . [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx)도우미는 해당 속성과 연결 된 유효성 검사 메시지를 표시 합니다.

응용 프로그램을 실행 하 고 */영화* URL로 이동 합니다. **Edit** 링크를 클릭합니다. 브라우저에서 페이지의 소스를 봅니다. Form 요소의 HTML은 다음과 같습니다.

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample5.html?highlight=7,10-11)]

`<input>`요소는 `<form>` `action` */Movies/Edit* URL에 post로 설정 된 특성이 있는 HTML 요소에 있습니다. **편집** 단추를 클릭 하면 폼 데이터가 서버에 게시 됩니다.

## <a name="processing-the-post-request"></a>POST 요청 처리

다음 목록은 `Edit` 작업 메서드의 `HttpPost` 버전을 보여줍니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cs)]

[ASP.NET MVC 모델 바인더](https://msdn.microsoft.com/magazine/hh781022.aspx) 는 게시 된 양식 값을 사용 하 고 `Movie` 매개 변수로 전달 되는 개체를 만듭니다 `movie` . `ModelState.IsValid` 메서드는 양식에서 제출된 데이터가 `Movie` 개체를 수정하는 데(편집 또는 수정) 사용될 수 있는지 확인합니다. 데이터가 유효 하면 동영상 데이터가 인스턴스의 컬렉션에 저장 됩니다 `Movies` `db(MovieDBContext` . 새 동영상 데이터는의 메서드를 호출 하 여 데이터베이스에 저장 됩니다 `SaveChanges` `MovieDBContext` . 데이터를 저장 한 후에는 코드에서 사용자를 `Index` 클래스의 작업 메서드로 리디렉션합니다 `MoviesController` .이 메서드는 단순히 변경한 내용을 포함 하 여 동영상 컬렉션의를 표시 합니다.

게시 된 값이 유효 하지 않으면 폼으로 다시 표시 됩니다. `Html.ValidationMessageFor` *편집. cshtml* 뷰 템플릿의 도우미는 적절 한 오류 메시지를 표시 합니다.

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

> [!NOTE]
> 소수점에 쉼표 (,)를 사용 하는 영어가 아닌 로캘에서 jQuery 유효성 검사를 지원 하려면 &quot; &quot; 사용할 *globalize.js* 및 특정 *문화권/globalize.cultures.js* 파일 (원본 [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) 및 JavaScript를 포함 해야 합니다 `Globalize.parseFloat` . 다음 코드에서는 fr-fr 문화권을 사용 하기 위해 Views\Movies\Edit.cshtml 파일을 수정 하는 방법을 보여 줍니다 &quot; &quot; .

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

Decimal 필드에는 소수점이 아닌 쉼표가 필요할 수 있습니다. 임시 수정을 위해 프로젝트 루트 web.config 파일에 전역화 요소를 추가할 수 있습니다. 다음 코드에서는 문화권이 미국 영어로 설정 된 세계화 요소를 보여 줍니다.

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.xml)]

모든 `HttpGet` 메서드는 비슷한 패턴을 따릅니다. 동영상 개체 (또는의 경우 개체 목록)를 가져오고 `Index` 모델을 뷰에 전달 합니다. `Create`메서드는 빈 동영상 개체를 만들기 뷰에 전달 합니다. 생성, 편집, 삭제 또는 어떤 식으로든 데이터를 수정하는 모든 메서드는 메서드의 `HttpPost` 오버로드에서 해당 작업을 수행합니다. HTTP GET 메서드에서 데이터를 수정 하는 것은 ASP.NET MVC 팁 #46의 블로그 게시물 항목에 설명 된 것 처럼 보안 위험입니다. [보안 허점을 만들기 때문에 삭제 링크를 사용 하지 마세요](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx). GET 메서드에서 데이터를 수정 하면 HTTP 모범 사례와 구조적 [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer) 패턴이 위반 되어 get 요청이 응용 프로그램의 상태를 변경 하지 않도록 지정 합니다. 다시 말해 GET 작업 수행은 부작용 없이 안전하고 영속 데이터를 수정하지 않는 방법으로 이루어져야 합니다.

## <a name="adding-a-search-method-and-search-view"></a>검색 방법 및 검색 보기 추가

이 섹션에서는 `SearchIndex` 장르 또는 이름을 기준으로 영화를 검색할 수 있는 작업 메서드를 추가 합니다. */Movies/SearchIndex* URL을 사용 하 여이를 사용할 수 있습니다. 이 요청은 사용자가 영화를 검색 하기 위해 입력할 수 있는 입력 요소를 포함 하는 HTML 폼을 표시 합니다. 사용자가 폼을 제출 하면 동작 메서드가 사용자가 게시 한 검색 값을 가져오고이 값을 사용 하 여 데이터베이스를 검색 합니다.

## <a name="displaying-the-searchindex-form"></a>SearchIndex 폼 표시

`SearchIndex`기존 클래스에 작업 메서드를 추가 하 여 시작 `MoviesController` 합니다. 메서드는 HTML 폼이 포함 된 뷰를 반환 합니다. 코드는 다음과 같습니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

메서드의 첫 번째 줄에서는 `SearchIndex` 다음 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 쿼리를 만들어 영화를 선택 합니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cs)]

쿼리가이 시점에 정의 되었지만 데이터 저장소에 대해 아직 실행 되지 않았습니다.

`searchString`매개 변수에 문자열이 포함 된 경우 다음 코드를 사용 하 여 검색 문자열의 값을 필터링 하도록 동영상 쿼리를 수정 합니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample11.cs)]

위의 `s => s.Title` 코드는 [람다 식](https://msdn.microsoft.com/library/bb397687.aspx)입니다. 람다 식은 메서드 기반 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 쿼리에서 위의 코드에서 사용 된 [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) 메서드와 같은 표준 쿼리 연산자 메서드의 인수로 사용 됩니다. LINQ 쿼리는 정의 될 때 또는 또는와 같은 메서드를 호출 하 여 수정 될 때 실행 되지 `Where` 않습니다 `OrderBy` . 대신 쿼리 실행이 지연 됩니다. 즉, 실현 된 값이 실제로 반복 되거나 메서드가 호출 될 때까지 식의 계산이 지연 됩니다 [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) . `SearchIndex`이 샘플에서는 SearchIndex 뷰에서 쿼리가 실행 됩니다. 지연된 쿼리 실행에 대한 자세한 내용은 [쿼리 실행](https://msdn.microsoft.com/library/bb738633.aspx)을 참조하세요.

이제 `SearchIndex` 사용자에 게 폼을 표시 하는 뷰를 구현할 수 있습니다. 메서드 내부를 마우스 오른쪽 단추로 클릭 한 `SearchIndex` 다음 **뷰 추가**를 클릭 합니다. **보기 추가** 대화 상자에서 `Movie` 개체를 뷰 템플릿에 모델 클래스로 전달 하도록 지정 합니다. **스 캐 폴드 템플릿** 목록에서 **목록**을 선택한 다음 **추가**를 클릭 합니다.

![AddSearchView](examining-the-edit-methods-and-edit-view/_static/image5.png)

**추가** 단추를 클릭 하면 *Views\Movies\SearchIndex.cshtml* view 템플릿이 만들어집니다. **스 캐 폴드 템플릿** 목록에서 **목록** 을 선택 했기 때문에 Visual Studio가 뷰에서 일부 기본 태그를 자동으로 생성 (스 캐 폴드) 합니다. 스 캐 폴딩이 HTML 폼을 만들었습니다. 클래스를 검사 하 `Movie` 고 `<label>` 클래스의 각 속성에 대 한 요소를 렌더링 하는 코드를 만들었습니다. 아래 목록에는 생성 된 만들기 뷰가 나와 있습니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample12.cshtml)]

응용 프로그램을 실행 하 고 */Movies/SearchIndex*로 이동 합니다. 쿼리 문자열(예: `?searchString=ghost`)을 URL에 추가합니다. 필터링된 영화가 표시됩니다.

![SearchQryStr](examining-the-edit-methods-and-edit-view/_static/image6.png)

`SearchIndex`이라는 매개 변수를 포함 하도록 메서드의 서명을 변경 하는 경우 `id` `id` 매개 변수는 `{id}` *global.asax* 파일에 설정 된 기본 경로에 대 한 자리 표시자와 일치 합니다.

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample13.json)]

원래 메서드는 다음과 같습니다 `SearchIndex` .

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample14.cs)]

수정 된 메서드는 다음과 같습니다 `SearchIndex` .

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample15.cs?highlight=1,3)]

이제 쿼리 문자열 값 대신 경로 데이터(URL 세그먼트)로 검색 제목을 전달할 수 있습니다.

![SearchRouteData](examining-the-edit-methods-and-edit-view/_static/image7.png)

그러나 사용자가 영화를 검색하려고 할 때마다 URL을 수정하리라고 기대하지는 않을 것입니다. 이제 영화를 필터링 하는 데 도움이 되는 UI를 추가 합니다. 메서드의 서명을 변경 하 여 `SearchIndex` 경로 바인딩된 ID 매개 변수를 전달 하는 방법을 테스트 하는 경우 `SearchIndex` 메서드가 라는 문자열 매개 변수를 사용 하도록 다시 변경 합니다 `searchString` .

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample16.cs)]

*Views\Movies\SearchIndex.cshtml* 파일을 열고 바로 뒤에 `@Html.ActionLink("Create New", "Create")` 다음을 추가 합니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample17.cshtml?highlight=2)]

다음 예제에서는 필터링 태그가 추가 된 *Views\Movies\SearchIndex.cshtml* 파일의 일부를 보여 줍니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample18.cshtml?highlight=12-15)]

`Html.BeginForm`도우미는 여는 태그를 만듭니다 `<form>` . 도우미를 사용 하면 `Html.BeginForm` 사용자가 **필터** 단추를 클릭 하 여 양식을 전송할 때 폼이 자신에 게 게시 됩니다.

응용 프로그램을 실행 하 고 영화 검색을 시도 합니다.

![](examining-the-edit-methods-and-edit-view/_static/image8.png)

`HttpPost`메서드의 오버 로드가 없습니다 `SearchIndex` . 메서드가 응용 프로그램의 상태를 변경 하는 것이 아니라 데이터만 필터링 하기 때문에 필요 하지 않습니다.

다음 `HttpPost SearchIndex` 메서드를 추가할 수 있습니다. 이 경우 작업 호출자는 `HttpPost SearchIndex` 메서드와 일치 하 고 `HttpPost SearchIndex` 메서드는 아래 이미지와 같이 실행 됩니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample19.cs)]

![SearchPostGhost](examining-the-edit-methods-and-edit-view/_static/image9.png)

그러나 이 `HttpPost` 버전의 `SearchIndex` 메서드를 추가하는 경우에도 이를 모두 구현하는 방법은 제한됩니다. 특정 검색을 책갈피로 설정하거나 동일하게 필터링된 영화 목록을 보기 위해 클릭할 수 있는 링크를 친구에게 보내려고 한다고 가정합니다. HTTP POST 요청에 대 한 URL은 GET 요청에 대 한 url (localhost: xxxxx/영화/SearchIndex)과 동일 합니다. URL 자체에는 검색 정보가 없습니다. 지금은 검색 문자열 정보가 양식 필드 값으로 서버에 전송 됩니다. 즉, 책갈피에 대 한 검색 정보를 캡처하거나 URL의 친구에 게 보낼 수 없습니다.

이 솔루션은 `BeginForm` POST 요청에서 검색 정보를 URL에 추가 하 고 HttpGet 버전의 메서드로 라우팅해야 한다는 것을 지정 하는의 오버 로드를 사용 하는 것입니다 `SearchIndex` . 매개 변수가 없는 기존 `BeginForm` 메서드를 다음으로 바꿉니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample20.cshtml)]

![BeginFormPost_SM](examining-the-edit-methods-and-edit-view/_static/image10.png)

이제 검색을 제출할 때 URL에 검색 쿼리 문자열이 포함 됩니다. `HttpPost SearchIndex` 메서드가 존재하더라도 검색은 `HttpGet SearchIndex` 작업 메서드로 이동합니다.

![SearchIndexWithGetURL](examining-the-edit-methods-and-edit-view/_static/image11.png)

## <a name="adding-search-by-genre"></a>장르 별 검색 추가

`HttpPost`메서드 버전을 추가한 경우 `SearchIndex` 지금 삭제 합니다.

다음으로, 사용자가 장르로 영화를 검색할 수 있는 기능을 추가 합니다. `SearchIndex` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample21.cs)]

이 버전의 `SearchIndex` 메서드는 추가 매개 변수를 사용 `movieGenre` 합니다. 즉, 코드의 처음 몇 줄은 개체를 만들어 `List` 데이터베이스에서 영화 장르를 보관 합니다.

다음 코드는 데이터베이스에서 모든 장르를 검색하는 LINQ 쿼리입니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample22.cs)]

코드는 `AddRange` 제네릭 컬렉션의 메서드를 사용 하 여 `List` 모든 고유 장르를 목록에 추가 합니다. 한정자를 사용 하지 않고 `Distinct` 중복 장르를 추가 합니다. 예를 들어 코미디는 샘플에서 두 번 추가 됩니다. 그런 다음 코드는 장르 목록을 개체에 저장 합니다 `ViewBag` .

다음 코드에서는 매개 변수를 확인 하는 방법을 보여 줍니다 `movieGenre` . 비어 있지 않은 경우 코드는 선택한 영화를 지정 된 장르로 제한 하도록 동영상 쿼리를 추가로 제한 합니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample23.cs)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>장르 검색을 지원 하기 위해 SearchIndex 뷰에 태그 추가

도우미 `Html.DropDownList` 바로 앞에 *Views\Movies\SearchIndex.cshtml* 파일에 도우미를 추가 `TextBox` 합니다. 완성 된 태그는 다음과 같습니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample24.cshtml?highlight=4)]

응용 프로그램을 실행 하 고 */Movies/SearchIndex*로 이동 합니다. 장르, 영화 이름 및 두 조건에 따라 검색을 수행 합니다.

![](examining-the-edit-methods-and-edit-view/_static/image12.png)

이 섹션에서는 프레임 워크에 의해 생성 된 CRUD 작업 메서드 및 뷰를 검사 했습니다. 사용자가 영화 제목 및 장르로 검색할 수 있는 검색 작업 메서드 및 보기를 만들었습니다. 다음 섹션에서는 모델에 속성을 추가 하는 방법 `Movie` 및 테스트 데이터베이스를 자동으로 만드는 이니셜라이저를 추가 하는 방법을 살펴봅니다.

> [!div class="step-by-step"]
> [이전](accessing-your-models-data-from-a-controller.md)
> [다음](adding-a-new-field-to-the-movie-model-and-table.md)
