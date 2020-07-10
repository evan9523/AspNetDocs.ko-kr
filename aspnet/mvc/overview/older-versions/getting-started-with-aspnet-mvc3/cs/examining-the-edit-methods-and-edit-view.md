---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/examining-the-edit-methods-and-edit-view
title: '편집 메서드 및 편집 보기 검사 (c #) | Microsoft Docs'
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1 (...)을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다.
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 1d266bf0-a61e-423b-a3d2-13773d7dafe2
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 0fb3d3cf6c1f4634834aaac1e9170218ca5730bb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "86163717"
---
# <a name="examining-the-edit-methods-and-edit-view-c"></a>편집 메서드 및 편집 보기 검사(C#)

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > ASP.NET MVC 5와 Visual Studio 2013를 사용 하는이 자습서의 업데이트 된 버전 [을 사용할 수 있습니다.](../../../getting-started/introduction/getting-started.md) 더 안전 하 고 더 간단 하 고 더 많은 기능을 보여 줍니다.
> 
> 
> 이 자습서에서는 Microsoft Visual Studio의 무료 버전인 Microsoft Visual Web Developer 2010 Express 서비스 팩 1을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다. 시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다. [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)링크를 클릭 하 여 모든 항목을 설치할 수 있습니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Web Developer 2010 대신 Visual Studio 2010을 사용 하는 경우 [Visual studio 2010 필수 조건](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)링크를 클릭 하 여 필수 구성 요소를 설치 합니다.
> 
> 이 항목에는 c # 소스 코드가 포함 된 Visual Web Developer 프로젝트가 제공 됩니다. [C # 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. Visual Basic 선호 하는 경우이 자습서의 [Visual Basic 버전](../vb/intro-to-aspnet-mvc-3.md) 으로 전환 합니다.

이 섹션에서는 동영상 컨트롤러에 대해 생성 된 작업 메서드 및 뷰를 검사 합니다. 그런 다음 사용자 지정 검색 페이지를 추가 합니다.

응용 프로그램을 실행 하 고 `Movies` 브라우저의 주소 표시줄에 있는 URL에 */sourcea* 를 추가 하 여 컨트롤러를 찾습니다. **편집** 링크 위에 마우스 포인터를 놓으면 링크 되는 URL을 볼 수 있습니다.

[![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image2.png)](examining-the-edit-methods-and-edit-view/_static/image1.png)

Views\Movies\Index.cshtml 뷰의 메서드에서 **편집** 링크를 생성 했습니다 `Html.ActionLink` . *Views\Movies\Index.cshtml*

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

[![Html.ActionLink](examining-the-edit-methods-and-edit-view/_static/image4.png)](examining-the-edit-methods-and-edit-view/_static/image3.png)

`Html`개체는 기본 클래스의 속성을 사용 하 여 노출 되는 도우미입니다 `WebViewPage` . `ActionLink`도우미의 메서드를 사용 하면 컨트롤러에서 작업 메서드에 연결 되는 HTML 하이퍼링크를 쉽게 동적으로 생성할 수 있습니다. 메서드의 첫 번째 인수는 `ActionLink` 렌더링할 링크 텍스트입니다 (예: `<a>Edit Me</a>` ). 두 번째 인수는 호출할 동작 메서드의 이름입니다. 마지막 인수는 경로 데이터를 생성 하는 [익명 개체](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) 입니다 (이 경우 ID 4).

이전 이미지에 표시 된 링크는 `http://localhost:xxxxx/Movies/Edit/4` 입니다. 기본 경로는 URL 패턴을 사용 합니다 `{controller}/{action}/{id}` . 따라서 ASP.NET는 `http://localhost:xxxxx/Movies/Edit/4` `Edit` `Movies` 매개 변수가 4 인 컨트롤러의 작업 메서드에 대 한 요청으로 변환 됩니다 `ID` .

쿼리 문자열을 사용 하 여 동작 메서드 매개 변수를 전달할 수도 있습니다. 예를 들어 URL은 `http://localhost:xxxxx/Movies/Edit?ID=4` 매개 변수 4를 `ID` `Edit` 컨트롤러의 동작 메서드에 전달 합니다 `Movies` .

[![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image6.png)](examining-the-edit-methods-and-edit-view/_static/image5.png)

컨트롤러를 엽니다 `Movies` . 두 `Edit` 작업 메서드는 다음과 같습니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs)]

두 번째 `Edit` 작업 메서드 앞에 `HttpPost` 특성이 지정되어 있는 것에 유의하세요. 이 특성은 `Edit` POST 요청에 대해서만 메서드의 오버 로드를 호출할 수 있도록 지정 합니다. `HttpGet`특성을 첫 번째 edit 메서드에 적용할 수 있지만 이것이 기본값 이기 때문에 필요 하지 않습니다. (특성을 메서드로 명시적으로 할당 하는 작업 메서드를 참조 `HttpGet` `HttpGet` 합니다.)

`HttpGet` `Edit` 메서드는 movie ID 매개 변수를 사용 하 고, Entity Framework 메서드를 사용 하 여 동영상을 조회 하 `Find` 고, 선택 된 동영상을 편집 보기로 반환 합니다. 스캐폴딩 시스템은 Edit 보기를 만들 때 `Movie` 클래스를 검토하고 클래스의 각 속성에 대해 `<label>` 및 `<input>` 요소를 렌더링하기 위한 코드를 만들었습니다. 다음 예에서는 생성 된 편집 뷰를 보여 줍니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

뷰 템플릿에는 `@model MvcMovie.Models.Movie` 파일 위쪽에 문이 포함 되어 있습니다 .이는 뷰에서 뷰 템플릿의 모델을 형식으로 예상 하도록 지정 합니다 `Movie` .

스 캐 폴드 코드는 몇 가지 *도우미 메서드* 를 사용 하 여 HTML 태그를 간소화 합니다. [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx)도우미는 필드 이름 ("제목", "ReleaseDate", "장르" 또는 "Price")을 표시 합니다. [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx)도우미는 HTML 요소를 표시 합니다 `<input>` . [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx)도우미는 해당 속성과 연결 된 유효성 검사 메시지를 표시 합니다.

응용 프로그램을 실행 하 고 */영화* URL로 이동 합니다. **Edit** 링크를 클릭합니다. 브라우저에서 페이지의 소스를 봅니다. 페이지의 HTML은 다음 예제와 같습니다. 메뉴 태그는 명확 하 게 하기 위해 제외 되었습니다.

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample4.html)]

`<input>`요소는 `<form>` `action` */Movies/Edit* URL에 post로 설정 된 특성이 있는 HTML 요소에 있습니다. **편집** 단추를 클릭 하면 폼 데이터가 서버에 게시 됩니다.

## <a name="processing-the-post-request"></a>POST 요청 처리

다음 목록은 `Edit` 작업 메서드의 `HttpPost` 버전을 보여줍니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs)]

ASP.NET framework 모델 바인더는 게시 된 양식 값을 사용 하 고 `Movie` 매개 변수로 전달 되는 개체를 만듭니다 `movie` . `ModelState.IsValid`코드를 체크 인하면 폼에 전송 된 데이터를 사용 하 여 개체를 수정할 수 있는지 확인 합니다 `Movie` . 데이터가 유효한 경우 코드는 동영상 데이터를 인스턴스의 컬렉션에 저장 합니다 `Movies` `MovieDBContext` . 그런 다음 코드는 데이터베이스에 대 한 `SaveChanges` 변경 내용을 유지 하는의 메서드를 호출 하 여 새 동영상 데이터를 데이터베이스에 저장 합니다 `MovieDBContext` . 데이터를 저장 한 후 코드는 사용자를 `Index` 클래스의 작업 메서드로 리디렉션하고이로 `MoviesController` 인해 업데이트 된 동영상이 동영상 목록에 표시 됩니다.

게시 된 값이 유효 하지 않으면 폼으로 다시 표시 됩니다. `Html.ValidationMessageFor` *편집. cshtml* 뷰 템플릿의 도우미는 적절 한 오류 메시지를 표시 합니다.

[![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image8.png)](examining-the-edit-methods-and-edit-view/_static/image7.png)

> **로캘에 대 한 참고 사항** 일반적으로 영어가 아닌 로캘로 작업 하는 경우 [영어가 아닌 로캘로 ASP.NET MVC 3 유효성 검사 지원](https://msdn.microsoft.com/library/gg674880(VS.98).aspx) 을 참조 하세요.

## <a name="making-the-edit-method-more-robust"></a>Edit 메서드를 보다 강력 하 게 만들기

`HttpGet` `Edit` 스 캐 폴딩 시스템에서 생성 된 메서드는 전달 된 ID가 유효한 지 확인 하지 않습니다. 사용자가 URL ()에서 ID 세그먼트를 제거 하면 `http://localhost:xxxxx/Movies/Edit` 다음과 같은 오류가 표시 됩니다.

[![Null_ID](examining-the-edit-methods-and-edit-view/_static/image10.png)](examining-the-edit-methods-and-edit-view/_static/image9.png)

사용자가 데이터베이스에 없는 ID (예:)를 전달할 수도 있습니다 `http://localhost:xxxxx/Movies/Edit/1234` . `HttpGet` `Edit` 작업 메서드를 변경 하 여 이러한 제한을 해결할 수 있습니다. 먼저 `ID` ID가 명시적으로 전달 되지 않는 경우 매개 변수를 기본값인 0으로 변경 합니다. 또한 `Find` 동영상 개체를 뷰 템플릿에 반환 하기 전에 메서드가 실제로 영화를 검색 했는지 확인할 수 있습니다. 업데이트 된 `Edit` 메서드는 다음과 같습니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cs)]

동영상이 없으면 `HttpNotFound` 메서드가 호출 됩니다.

모든 `HttpGet` 메서드는 비슷한 패턴을 따릅니다. 동영상 개체 (또는의 경우 개체 목록)를 가져오고 `Index` 모델을 뷰에 전달 합니다. `Create`메서드는 빈 동영상 개체를 만들기 뷰에 전달 합니다. 생성, 편집, 삭제 또는 어떤 식으로든 데이터를 수정하는 모든 메서드는 메서드의 `HttpPost` 오버로드에서 해당 작업을 수행합니다. HTTP GET 메서드에서 데이터를 수정 하는 것은 ASP.NET MVC 팁 #46의 블로그 게시물 항목에 설명 된 것 처럼 보안 위험입니다. [보안 허점을 만들기 때문에 삭제 링크를 사용 하지 마세요](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx). GET 메서드에서 데이터를 수정 하면 HTTP 모범 사례와 구조적 REST 패턴이 위반 되어 GET 요청이 응용 프로그램의 상태를 변경 하지 않도록 지정 합니다. 즉, GET 작업을 수행 하는 것은 부작용이 없는 안전한 작업 이어야 합니다.

## <a name="adding-a-search-method-and-search-view"></a>검색 방법 및 검색 보기 추가

이 섹션에서는 `SearchIndex` 장르 또는 이름을 기준으로 영화를 검색할 수 있는 작업 메서드를 추가 합니다. */Movies/SearchIndex* URL을 사용 하 여이를 사용할 수 있습니다. 이 요청은 사용자가 영화를 검색 하기 위해 채울 수 있는 입력 요소를 포함 하는 HTML 폼을 표시 합니다. 사용자가 폼을 제출 하면 동작 메서드가 사용자가 게시 한 검색 값을 가져오고이 값을 사용 하 여 데이터베이스를 검색 합니다.

## <a name="displaying-the-searchindex-form"></a>SearchIndex 폼 표시

`SearchIndex`기존 클래스에 작업 메서드를 추가 하 여 시작 `MoviesController` 합니다. 메서드는 HTML 폼이 포함 된 뷰를 반환 합니다. 코드는 다음과 같습니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cs)]

메서드의 첫 번째 줄에서는 `SearchIndex` 다음 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 쿼리를 만들어 영화를 선택 합니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cs)]

쿼리가이 시점에 정의 되었지만 데이터 저장소에 대해 아직 실행 되지 않았습니다.

`searchString`매개 변수에 문자열이 포함 된 경우 다음 코드를 사용 하 여 검색 문자열의 값을 필터링 하도록 동영상 쿼리를 수정 합니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

LINQ 쿼리는 정의 될 때 또는 또는와 같은 메서드를 호출 하 여 수정 될 때 실행 되지 `Where` 않습니다 `OrderBy` . 대신 쿼리 실행이 지연 됩니다. 즉, 실현 된 값이 실제로 반복 되거나 메서드가 호출 될 때까지 식의 계산이 지연 됩니다 [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) . `SearchIndex`이 샘플에서는 SearchIndex 뷰에서 쿼리가 실행 됩니다. 지연된 쿼리 실행에 대한 자세한 내용은 [쿼리 실행](https://msdn.microsoft.com/library/bb738633.aspx)을 참조하세요.

이제 `SearchIndex` 사용자에 게 폼을 표시 하는 뷰를 구현할 수 있습니다. 메서드 내부를 마우스 오른쪽 단추로 클릭 한 `SearchIndex` 다음 **뷰 추가**를 클릭 합니다. **보기 추가** 대화 상자에서 `Movie` 개체를 뷰 템플릿에 모델 클래스로 전달 하도록 지정 합니다. **스 캐 폴드 템플릿** 목록에서 **목록**을 선택한 다음 **추가**를 클릭 합니다.

[![AddSearchView](examining-the-edit-methods-and-edit-view/_static/image12.png)](examining-the-edit-methods-and-edit-view/_static/image11.png)

**추가** 단추를 클릭 하면 *Views\Movies\SearchIndex.cshtml* view 템플릿이 만들어집니다. **스 캐 폴드 템플릿** 목록에서 **목록** 을 선택 했기 때문에 Visual Web Developer에서 뷰의 일부 기본 콘텐츠를 자동으로 생성 (스 캐 폴드) 합니다. 스 캐 폴딩이 HTML 폼을 만들었습니다. 클래스를 검사 하 `Movie` 고 `<label>` 클래스의 각 속성에 대 한 요소를 렌더링 하는 코드를 만들었습니다. 아래 목록에는 생성 된 만들기 뷰가 나와 있습니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

응용 프로그램을 실행 하 고 */Movies/SearchIndex*로 이동 합니다. 쿼리 문자열(예: `?searchString=ghost`)을 URL에 추가합니다. 필터링된 영화가 표시됩니다.

[![SearchQryStr](examining-the-edit-methods-and-edit-view/_static/image14.png)](examining-the-edit-methods-and-edit-view/_static/image13.png)

`SearchIndex`이라는 매개 변수를 포함 하도록 메서드의 서명을 변경 하는 경우 `id` `id` 매개 변수는 `{id}` *global.asax* 파일에 설정 된 기본 경로에 대 한 자리 표시자와 일치 합니다.

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample11.json)]

수정 된 메서드는 다음과 같습니다 `SearchIndex` .

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample12.cs)]

이제 쿼리 문자열 값 대신 경로 데이터(URL 세그먼트)로 검색 제목을 전달할 수 있습니다.

[![SearchRouteData](examining-the-edit-methods-and-edit-view/_static/image16.png)](examining-the-edit-methods-and-edit-view/_static/image15.png)

그러나 사용자가 영화를 검색하려고 할 때마다 URL을 수정하리라고 기대하지는 않을 것입니다. 이제 영화를 필터링 하는 데 도움이 되는 UI를 추가 합니다. 메서드의 서명을 변경 하 여 `SearchIndex` 경로 바인딩된 ID 매개 변수를 전달 하는 방법을 테스트 하는 경우 `SearchIndex` 메서드가 라는 문자열 매개 변수를 사용 하도록 다시 변경 합니다 `searchString` .

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample13.cs)]

*Views\Movies\SearchIndex.cshtml* 파일을 열고 바로 뒤에 `@Html.ActionLink("Create New", "Create")` 다음을 추가 합니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample14.cshtml)]

다음 예제에서는 필터링 태그가 추가 된 *Views\Movies\SearchIndex.cshtml* 파일의 일부를 보여 줍니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample15.cshtml)]

`Html.BeginForm`도우미는 여는 태그를 만듭니다 `<form>` . 도우미를 사용 하면 `Html.BeginForm` 사용자가 **필터** 단추를 클릭 하 여 양식을 전송할 때 폼이 자신에 게 게시 됩니다.

응용 프로그램을 실행 하 고 영화 검색을 시도 합니다.

[![SearchIndxIE9_title](examining-the-edit-methods-and-edit-view/_static/image18.png)](examining-the-edit-methods-and-edit-view/_static/image17.png)

`HttpPost`메서드의 오버 로드가 없습니다 `SearchIndex` . 메서드가 응용 프로그램의 상태를 변경 하는 것이 아니라 데이터만 필터링 하기 때문에 필요 하지 않습니다.

다음 `HttpPost SearchIndex` 메서드를 추가할 수 있습니다. 이 경우 작업 호출자는 `HttpPost SearchIndex` 메서드와 일치 하 고 `HttpPost SearchIndex` 메서드는 아래 이미지와 같이 실행 됩니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample16.cs)]

[![SearchPostGhost](examining-the-edit-methods-and-edit-view/_static/image20.png)](examining-the-edit-methods-and-edit-view/_static/image19.png)

그러나 이 `HttpPost` 버전의 `SearchIndex` 메서드를 추가하는 경우에도 이를 모두 구현하는 방법은 제한됩니다. 특정 검색을 책갈피로 설정하거나 동일하게 필터링된 영화 목록을 보기 위해 클릭할 수 있는 링크를 친구에게 보내려고 한다고 가정합니다. HTTP POST 요청에 대 한 URL은 GET 요청에 대 한 url (localhost: xxxxx/영화/SearchIndex)과 동일 합니다. URL 자체에는 검색 정보가 없습니다. 지금은 검색 문자열 정보가 양식 필드 값으로 서버에 전송 됩니다. 즉, 책갈피에 대 한 검색 정보를 캡처하거나 URL의 친구에 게 보낼 수 없습니다.

이 솔루션은 POST 요청에서 검색 정보를 URL에 추가 하도록 지정 하는의 오버 로드를 사용 하 여 `BeginForm` 메서드의 HttpGet 버전으로 라우팅해야 한다는 것을 나타냅니다 `SearchIndex` . 매개 변수가 없는 기존 `BeginForm` 메서드를 다음으로 바꿉니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample17.cshtml)]

[![BeginFormPost_SM](examining-the-edit-methods-and-edit-view/_static/image22.png)](examining-the-edit-methods-and-edit-view/_static/image21.png)

이제 검색을 제출할 때 URL에 검색 쿼리 문자열이 포함 됩니다. `HttpPost SearchIndex` 메서드가 존재하더라도 검색은 `HttpGet SearchIndex` 작업 메서드로 이동합니다.

[![SearchIndexWithGetURL](examining-the-edit-methods-and-edit-view/_static/image24.png)](examining-the-edit-methods-and-edit-view/_static/image23.png)

## <a name="adding-search-by-genre"></a>장르 별 검색 추가

`HttpPost`메서드 버전을 추가한 경우 `SearchIndex` 지금 삭제 합니다.

다음으로, 사용자가 장르로 영화를 검색할 수 있는 기능을 추가 합니다. `SearchIndex` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample18.cs)]

이 버전의 `SearchIndex` 메서드는 추가 매개 변수를 사용 `movieGenre` 합니다. 즉, 코드의 처음 몇 줄은 개체를 만들어 `List` 데이터베이스에서 영화 장르를 보관 합니다.

다음 코드는 데이터베이스에서 모든 장르를 검색하는 LINQ 쿼리입니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample19.cs)]

코드는 `AddRange` 제네릭 컬렉션의 메서드를 사용 하 여 `List` 모든 고유 장르를 목록에 추가 합니다. 한정자를 사용 하지 않고 `Distinct` 중복 장르를 추가 합니다. 예를 들어 코미디는 샘플에서 두 번 추가 됩니다. 그런 다음 코드는 장르 목록을 개체에 저장 합니다 `ViewBag` .

다음 코드에서는 매개 변수를 확인 하는 방법을 보여 줍니다 `movieGenre` . 비어 있지 않은 경우 코드는 선택한 영화를 지정 된 장르로 제한 하도록 동영상 쿼리를 추가로 제한 합니다.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample20.cs)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>장르 검색을 지원 하기 위해 SearchIndex 뷰에 태그 추가

도우미 `Html.DropDownList` 바로 앞에 *Views\Movies\SearchIndex.cshtml* 파일에 도우미를 추가 `TextBox` 합니다. 완성 된 태그는 다음과 같습니다.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample21.cshtml)]

응용 프로그램을 실행 하 고 */Movies/SearchIndex*로 이동 합니다. 장르, 영화 이름 및 두 조건에 따라 검색을 수행 합니다.

이 섹션에서는 프레임 워크에 의해 생성 된 CRUD 작업 메서드 및 뷰를 검사 했습니다. 사용자가 영화 제목 및 장르로 검색할 수 있는 검색 작업 메서드 및 보기를 만들었습니다. 다음 섹션에서는 모델에 속성을 추가 하는 방법 `Movie` 및 테스트 데이터베이스를 자동으로 만드는 이니셜라이저를 추가 하는 방법을 살펴봅니다.

> [!div class="step-by-step"]
> [이전](accessing-your-models-data-from-a-controller.md)
> [다음](adding-a-new-field.md)
