---
uid: mvc/mvc3
title: ASP.NET MVC 3
author: rick-anderson
description: (2011년 4월 도구 업데이트 포함) ASP.NET MVC 3은 잘 구축된 설계 패턴을 사용하여 확장 가능한 표준 기반 웹 응용 프로그램을 구축하기 위한 프레임워크입니다.
ms.author: riande
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 6fe734dc0d0106bb346df154e1e03f97b307567a
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675133"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

> *(2011년 4월 도구 업데이트 포함)*
> 
> ASP.NET MVC 3은 잘 구축된 디자인 패턴과 ASP.NET 및 .NET Framework의 강력한 힘을 사용하여 확장 가능한 표준 기반 웹 응용 프로그램을 구축하기 위한 프레임워크입니다.
> 
> MVC 2와 ASP.NET 나란히 설치하므로 오늘 부터 사용하기 시작하십시오!
> 
> 여기에서 [설치 관리자를 다운로드하십시오.](https://microsoft.com/download/details.aspx?id=4211)

## <a name="top-features"></a>주요 기능

- NuGet을 통해 확장 가능한 통합 스캐폴딩 시스템
- HTML 5 지원 프로젝트 템플릿
- 새로운 면도기 보기 엔진을 포함한 표현보기
- 종속성 주입 및 전역 작업 필터가 있는 강력한 후크
- 눈에 거슬리지 자바 스크립트, j쿼리 유효성 검사 및 JSON 바인딩으로 풍부한 자바 스크립트 지원
- *[아래의](#overview) 전체 기능 목록 읽기*

## <a name="top-links"></a>상위 링크

ASP.NET MVC 3의 새로운 점

- 필 하악: [ASP.NET MVC 3 출시](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)
- 스콧 헨젤만: [ASP.NET MVC3, 웹 매트릭스, NuGet, IIS 익스프레스와 과수원 출시 - 컨텍스트에서 마이크로 소프트 1 월 웹 릴리스](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)
- 스콧 거스리: [ASP.NET MVC 의 출시 발표 3, IIS 익스프레스, SQL CE 4, 웹 팜 프레임 워크, 과수원, 웹 매트릭스](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)
- [ASP.NET MVC 3에 대한 릴리스 정보](../whitepapers/mvc3-release-notes.md)

설치 및 도움말

- 웹 플랫폼 설치 관리자를 사용하여 MVC 3에 ASP.NET [설치(권장)](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)
- [설치 ASP.NET 실행 ASP.NET](https://go.microsoft.com/fwlink/?LinkID=208140) 사용하여 MVC 3 설치
- [비주얼 스튜디오 11 개발자 미리 보기에 대 한 ASP.NET MVC 3](https://go.microsoft.com/fwlink/?LinkID=208140) 설치
- [MVC 3 자습서를 ASP.NET 소개 읽기](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)
- 포럼에서 도움을 받고 ASP.NET MVC 3에 대해 [논의합니다.](https://forums.asp.net/1146.aspx)

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a>ASP.NET MVC 3 Overview

ASP.NET MVC 3은 mVC 1과 2를 ASP.NET 기반으로 하며, 코드를 단순화하고 더 깊은 확장성을 허용하는 훌륭한 기능을 추가합니다. 이 항목에서는 이 릴리스에 포함된 많은 새로운 기능에 대한 개요를 제공하며 다음 섹션으로 구성됩니다.

- [MvcScaffold 통합을 통해 확장 가능한 비계](#BM_MvcScaffolding)
- [HTML 5 지원 프로젝트 템플릿](#BM_HTML5)
- [면도기 보기 엔진](#BM_TheRazorViewEngine)
- [다중 뷰 엔진 지원](#BM_Support_for_Multiple_View_Engines)
- [컨트롤러 개선 사항](#BM_Controller_Improvements)
- [자바 스크립트와 아약스](#BM_JavaScript_and_Ajax_Improvements)
- [모델 유효성 검사 개선 사항](#BM_Model_Validation_Improvements)
- [종속성 주입 개선](#BM_Dependency_Injection_Improvements)
- [기타 새로운 기능](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a>MvcScaffold 통합을 통해 확장 가능한 비계

새로운 스캐폴딩 시스템을 사용하면 프레임워크를 완전히 새로 접을 경우 생산적으로 사용하고, 경험이 많고 이미 무엇을 하고 있는지 알고 있는 경우 일반적인 개발 작업을 자동화할 수 있습니다.

**MvcScaffolding이라는**새로운 NuGet *스캐폴딩* 패키지에서 지원됩니다. "스캐폴딩"이라는 용어는 많은 소프트웨어 기술에서 "소프트웨어의 기본 윤곽을 빠르게 생성하여 편집하고 사용자 지정할 수 있는"을 의미합니다. ASP.NET MVC를 위해 만드는 스캐폴딩 패키지는 다음과 같은 여러 시나리오에서 매우 유용합니다.

- **MVC를 처음 ASP.NET 배우는 경우**유용한 작업 코드를 빠르게 얻을 수 있으므로 필요에 따라 편집하고 조정할 수 있습니다. 그것은 빈 페이지를보고 어디서부터 시작해야할지 모른다는 트라우마에서 당신을 구해줄 것입니다!
- **MVC를 잘 ASP.NET 알고** 있고 객체 관계형 매퍼, 뷰 엔진, 테스트 라이브러리 등과 같은 새로운 추가 기술을 탐색하고 있는 경우 해당 기술의 작성자가 스캐폴딩 패키지를 만들었을 수도 있습니다.
- **작업이 유사한 클래스 또는 파일을 반복적으로 만드는**경우 테스트 설비, 배포 스크립트 또는 필요한 모든 것을 출력하는 사용자 지정 scaffolders를 만들 수 있기 때문입니다. 팀의 모든 사용자도 사용자 지정 scaffolders를 사용할 수 있습니다.

MvcScaffolding의 다른 기능은 다음과 같습니다.

- C# 및 VB 프로젝트 지원
- 면도기 및 ASPX 뷰 엔진 지원
- ASP.NET MVC 영역으로스캐폴딩 및 사용자 지정 보기 레이아웃/마스터 사용 지원
- T4 템플릿을 편집하여 출력을 쉽게 사용자 정의 할 수 있습니다.
- 사용자 지정 PowerShell 논리 및 사용자 지정 T4 템플릿을 사용하여 완전히 새로운 scaffolders를 추가할 수 있습니다. 이러한 매개 변수(및 지정한 모든 사용자 지정 매개 변수)는 콘솔 탭 완료 목록에 자동으로 나타납니다.
- 다른 기술에 대한 추가 scaffolders가 들어있는 NuGet 패키지를 얻을 수 있습니다 (예 : LINQ에서 SQL에 대한 개념 증명 패키지가 있습니다)를 혼합하고 함께 일치시킬 수 있습니다.

ASP.NET MVC 3 도구 업데이트에는 다음과 같은 이 스캐폴딩 시스템에 대한 훌륭한 Visual Studio 지원이 포함되어 있습니다.

- 컨트롤러 대화 상자 추가는 이제 컨트롤러 작업 및 해당 보기 만들기, 읽기, 업데이트 및 삭제의 전체 자동 스캐폴딩을 지원합니다. 기본적으로 이 스캐폴드는 EF 코드 우선을 사용하여 데이터 액세스 코드를 사용합니다.
- 컨트롤러 대화 추가는 *MvcScaffolding과*같은 NuGet 패키지를 통해 *확장 가능한 스캐폴드를* 지원합니다. 이렇게 하면 사용자 지정 스캐폴드를 대화 상자에 연결하면 NHibernate와 같은 다른 데이터 액세스 기술에 대한 스캐폴드를 만들 수 있으며, 경사면에는 ODBCDirect를 사용하여 JET를 만들 수 있습니다!

ASP.NET MVC 3의 스캐폴딩에 대한 자세한 내용은 다음 리소스를 참조하십시오.

- 스티브 샌더슨의 포스트 시리즈, 포함: 

    1. [소개: MvcScaffolding 패키지로 ASP.NET MVC 3 프로젝트를 스캐폴드](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [표준 사용법: 일반적인 사용 사례 및 옵션](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [일대다 관계](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [스캐폴딩 작업 및 단위 테스트](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [T4 템플릿 재정의](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [이 게시물: 사용자 지정 scaffolders 만들기](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- 스콧 핸셀먼의 PDC 2010 세션에서 [마이크로소프트와 블로그 구축 "웹 사랑의 이름 없는 패키지"](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)
- [MVC 3 릴리스 노트](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a>HTML 5 프로젝트 템플릿

새 프로젝트 대화 상자에는 HTML 5 버전의 프로젝트 템플릿을 사용하도록 설정하는 확인란이 포함되어 있습니다. 이러한 템플릿은 Modernizr 1.7을 활용하여 하위 수준 브라우저에서 HTML 5 및 CSS 3에 대한 호환성 지원을 제공합니다.

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a>면도기 보기 엔진

ASP.NET MVC 3에는 다음과 같은 이점을 제공하는 Razor라는 새로운 뷰 엔진이 함께 제공됩니다.

- Razor 구문은 깨끗하고 간결하므로 최소 키 입력 수가 필요합니다.
- 면도기는 C# 및 Visual Basic과 같은 기존 언어를 기반으로 하기 때문에 배우기 쉽습니다.
- 비주얼 스튜디오는 면도기 구문에 대한 IntelliSense 및 코드 색상화가 포함되어 있습니다.
- Razor 보기는 응용 프로그램을 실행하거나 웹 서버를 시작할 필요 없이 단위 테스트를 수행할 수 있습니다.

몇 가지 새로운 Razor 기능은 다음과 같습니다.

- `@model`뷰에 전달되는 형식을 지정하기 위한 구문입니다.
- `@* *@`주석 구문.
- 전체 사이트에 대해 기본값을 `layoutpage`한 번 지정하는 기능입니다.
- HTML `Html.Raw` 인코딩없이 텍스트를 표시하는 방법입니다.
- 여러 보기 간에 코드 공유*\_지원(viewstart.cshtml* 또는 * \_viewstart.vbhtml* 파일)

Razor에는 다음과 같은 새로운 HTML 도우미도 포함되어 있습니다.

- `Chart`. 차트를 렌더링하여 ASP.NET 4의 차트 컨트롤과 동일한 기능을 제공합니다.
- `WebGrid`. 페이징 및 정렬 기능이 포함된 데이터 그리드를 렌더링합니다.
- `Crypto`. 해싱 알고리즘을 사용하여 제대로 솔트되고 해시된 암호를 만듭니다.
- `WebImage`. 이미지를 렌더링합니다.
- `WebMail`. 메일 메시지를 전송합니다.

Razor에 대한 자세한 내용은 다음 리소스를 참조하십시오.

- [면도기 소개 스콧 거스리의 블로그 게시물](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [@model 키워드를 소개하는 스콧 거스리의 블로그 게시물](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [면도기 레이아웃을 소개하는 스콧 거스리의 블로그 게시물](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [면도기 API 빠른 참조](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [MVC 3 릴리스 노트](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a>다중 뷰 엔진 지원

MVC 3ASP.NET **보기 대화** 상자에서 작업할 뷰 엔진을 선택할 수 있으며 **새 프로젝트** 대화 상자를 사용하면 프로젝트의 기본 뷰 엔진을 지정할 수 있습니다. 웹 양식 보기 엔진(ASPX), Razor 또는 [스파크,](http://sparkviewengine.com/) [NHaml](https://code.google.com/p/nhaml/)또는 [NDjango와](http://ndjango.org/)같은 오픈 소스 보기 엔진을 선택할 수 있습니다.

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a>컨트롤러 개선 사항

### <a name="global-action-filters"></a>전역 작업 필터

때로는 작업 메서드가 실행되기 전이나 작업 메서드가 실행된 후에 논리를 수행하려고 합니다. 이를 지원하기 위해 ASP.NET MVC 2는 작업 필터를 제공했습니다. 작업 필터는 특정 컨트롤러 작업 메서드에 사전 작업 및 사후 작업 동작을 추가하는 선언적 수단을 제공하는 사용자 지정 특성입니다. 그러나 경우에 따라 모든 작업 메서드에 적용되는 사전 작업 또는 사후 작업 동작을 지정할 수 있습니다. MVC 3을 사용하면 `GlobalFilters` 전역 필터를 컬렉션에 추가하여 지정할 수 있습니다. 전역 작업 필터에 대한 자세한 내용은 다음 리소스를 참조하십시오.

- [MVC 3 미리보기에 스콧 거스리의 블로그](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- [ASP.NET MVC의 필터링](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)

### <a name="new-viewbag-property"></a>새 "뷰백" 속성

MVC 2 컨트롤러는 `ViewData` 한정된 사전 API를 사용하여 뷰 템플릿에 데이터를 전달할 수 있는 속성을 지원합니다. MVC 3에서는 `ViewBag` 속성과 다소 간단한 구문을 사용하여 동일한 목적을 달성할 수도 있습니다. 예를 들어 을 `ViewData["Message"]="text"`작성하는 대신 `ViewBag.Message="text"`을 작성할 수 있습니다. `ViewBag` 속성을 사용하기 위해 강력한 형식의 클래스를 정의할 필요는 없습니다. 동적 속성이기 때문에 대신 속성을 얻거나 설정할 수 있으며 런타임에 동적으로 해결할 수 있습니다. 내부적으로 `ViewBag` 속성은 사전의 `ViewData` 이름/값 쌍으로 저장됩니다. (참고: 대부분의 시험판 버전인 MVC 3에서는 `ViewBag` 속성이름이 `ViewModel` 지정되었습니다.)

### <a name="new-actionresult-types"></a>새로운 "작업 결과" 유형

다음 `ActionResult` 형식 및 해당 도우미 메서드는 MVC 3에서 새 또는 향상 됩니다.

- [HttpNotFound결과](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx). 클라이언트에 404 HTTP 상태 코드를 반환합니다.
- [리디렉션Result](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx). 부울 매개 변수에 따라 임시 리디렉션(HTTP 302 상태 코드) 또는 영구 리디렉션(HTTP 301 상태 코드)을 반환합니다. 이 변경 사항과 함께 [Controller](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx) 클래스에는 이제 영구 리디렉션을 `RedirectPermanent` `RedirectToRoutePermanent`수행하기 `RedirectToActionPermanent`위한 세 가지 메서드가 있습니다. 이러한 메서드는 `RedirectResult` `Permanent` 속성이 로 설정된 `true`인스턴스를 반환합니다.
- [Http상태코드결과](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx). 사용자가 지정한 HTTP 상태 코드를 반환합니다.

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a>자바 스크립트 및 아약스 개선 사항

기본적으로 MVC 3의 Ajax 및 유효성 검사 도우미는 눈에 거슬리지 않는 JavaScript 접근 방식을 사용합니다. 눈에 거슬리지 자바 스크립트는 HTML에 인라인 자바 스크립트를 주입 방지 할 수 있습니다. 이렇게 하면 HTML이 작아지고 복잡해지며 JavaScript 라이브러리를 쉽게 교체하거나 사용자 지정할 수 있습니다. MVC 3의 유효성 검사 `jQueryValidate` 도우미도 기본적으로 플러그인을 사용합니다. MVC 2 동작을 원하는 경우 *web.config* 파일 설정을 사용하여 눈에 거슬리지 않는 JavaScript를 비활성화할 수 있습니다. 자바 스크립트 및 아약스 개선 사항에 대한 자세한 내용은 다음 리소스를 참조하십시오.

- [위키백과 사이트의 눈에 거슬리지 않는 자바스크립트에 대한 기본 소개](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [브래드 윌슨의 눈에 거슬리지 자바 스크립트 게시물](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [브래드 윌슨의 눈에 거슬리지 자바 스크립트 유효성 검사 게시물](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- [면도기와 눈에 거슬리지 자바 스크립트와 MVC 3 응용 프로그램 만들기](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md) (ASP.NET 사이트의 튜토리얼)
- [MVC 3 릴리스 노트](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a>기본적으로 클라이언트 측 유효성 검사 사용 가능

이전 버전의 MVC에서는 클라이언트 측 유효성 `Html.EnableClientValidation` 검사를 사용하려면 뷰에서 메서드를 명시적으로 호출해야 합니다. MVC 3에서는 클라이언트 측 유효성 검사가 기본적으로 활성화되어 있으므로 더 이상 필요하지 않습니다. *(web.config* 파일에서 설정을 사용 하 여이 비활성화할 수 있습니다.)

클라이언트 측 유효성 검사가 작동하려면 사이트의 적절한 jQuery 및 jQuery 유효성 검사 라이브러리를 참조해야 합니다. 사용자 고유의 서버에서 해당 라이브러리를 호스팅하거나 Microsoft 또는 Google의 CDN과 같은 CDN(콘텐츠 전송 네트워크)에서 해당 라이브러리를 참조할 수 있습니다.

### <a name="remote-validator"></a>원격 유효성 검사기

ASP.NET MVC 3는 jQuery 유효성 검사 플러그인의 원격 유효성 검사기 지원을 활용할 수 있는 새로운 [RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx) 클래스를 지원합니다. 이렇게 하면 클라이언트 측 유효성 검사 라이브러리에서 서버 측에서만 수행할 수 있는 유효성 검사 논리를 수행하기 위해 서버에서 정의한 사용자 지정 메서드를 자동으로 호출할 수 있습니다.

다음 예제에서 `Remote` 특성은 클라이언트 유효성 검사가 `UserNameAvailable` `UsersController` `UserName` 필드의 유효성을 검사하기 위해 클래스에서 명명된 작업을 호출하도록 지정합니다.

[!code-csharp[Main](mvc3/samples/sample1.cs)]

다음 예제에서는 해당 컨트롤러를 보여 주다.

[!code-csharp[Main](mvc3/samples/sample2.cs)]

특성을 사용하는 방법에 대한 자세한 내용은 MSDN [라이브러리의 ASP.NET MVC에서 원격 유효성 검사 구현 방법을](https://msdn.microsoft.com/library/gg508808(VS.98).aspx) 참조하십시오. `Remote`

### <a name="json-binding-support"></a>JSON 바인딩 지원

ASP.NET MVC 3에는 작업 메서드가 JSON 인코딩된 데이터를 수신하고 action-method 매개 변수에 모델 바인딩할 수 있는 기본 제공 JSON 바인딩 지원이 포함되어 있습니다. 이 기능은 클라이언트 템플릿 및 데이터 바인딩과 관련된 시나리오에서 유용합니다. 클라이언트 템플릿을 사용하면 클라이언트에서 실행되는 템플릿을 사용하여 단일 데이터 항목 또는 데이터 항목 집합을 포맷하고 표시할 수 있습니다. MVC 3을 사용하면 JSON 데이터를 보내고 받는 서버의 작업 메서드와 클라이언트 템플릿을 쉽게 연결할 수 있습니다. JSON 바인딩 지원에 대한 자세한 내용은 [Scott Guthrie의 MVC 3 미리 보기 블로그 게시물의](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx) **자바스크립트 및 AJAX 개선** 섹션을 참조하십시오.

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a>모델 유효성 검사 개선 사항

### <a name="dataannotations-metadata-attributes"></a>"데이터주석" 메타데이터 특성

ASP.NET MVC `DataAnnotations` 3는 `DisplayAttribute`와 같은 메타데이터 특성을 지원합니다.

### <a name="validationattribute-class"></a>"유효성 검사 특성" 클래스

.NET Framework 4에서 `ValidationAttribute` 유효성을 검사하는 `IsValid` 개체와 같이 현재 유효성 검사 컨텍스트에 대한 자세한 정보를 제공하는 새 오버로드를 지원하도록 클래스가 개선되었습니다. 이렇게 하면 모델의 다른 속성을 기반으로 현재 값의 유효성을 검사할 수 있는 풍부한 시나리오를 사용할 수 있습니다. 예를 들어 새 `CompareAttribute` 특성을 사용하면 모델의 두 속성 값을 비교할 수 있습니다. 다음 예제에서는 속성이 `ComparePassword` 유효하려면 `Password` 필드와 일치해야 합니다.

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a>유효성 검사 인터페이스

[IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx) 인터페이스를 사용하면 모델 수준 유효성 검사를 수행할 수 있으며 전체 모델의 상태 또는 모델 내의 두 속성 간에 특정유효성 검사 오류 메시지를 제공할 수 있습니다. 이제 MVC 3은 모델 `IValidatableObject` 바인딩 시 인터페이스에서 오류를 검색하고 기본 제공 HTML 양식 도우미를 사용하여 뷰 내에서 영향을 받는 필드에 자동으로 플래그를 표시하거나 강조 표시합니다.

[IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx) 인터페이스를 사용하면 ASP.NET MVC가 유효성 검사기의 클라이언트 유효성 검사에 대한 지원이 있는지 여부를 런타임에 검색할 수 있습니다. 이 인터페이스는 다양한 유효성 검사 프레임워크와 통합될 수 있도록 설계되었습니다.

유효성 검사 인터페이스에 대한 자세한 내용은 [Scott Guthrie의 MVC 3 미리 보기 블로그 게시물의](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx) **모델 유효성 검사 개선** 섹션을 참조하십시오. 그러나 블로그의 "IValidateObject"에 대한 참조는 "IValidatableObject"여야 합니다.

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a>종속성 주입 개선

ASP.NET MVC 3은 종속성 주입(DI)을 적용하고 종속성 주입 또는 IOC(제어 반전) 컨테이너와 통합하는 데 더 나은 지원을 제공합니다. DI에 대한 지원이 다음 영역에 추가되었습니다.

- 컨트롤러(컨트롤러 공장 등록 및 주입, 컨트롤러 주입).
- 뷰(뷰 엔진 등록 및 삽입, 뷰 페이지에 종속성을 삽입).
- 작업 필터(필터 찾기 및 삽입).
- 모델 바인더(등록 및 주입).
- 모델 유효성 검사 공급자(등록 및 삽입).
- 메타데이터 공급자(등록 및 삽입)를 모델링합니다.
- 가치 공급자(등록 및 삽입).

MVC 3은 [공통 서비스 로케이터](https://github.com/unitycontainer/commonservicelocator) 라이브러리와 해당 라이브러리의 `IServiceLocator` 인터페이스를 지원하는 모든 DI 컨테이너를 지원합니다. 또한 DI 프레임워크를 보다 쉽게 통합할 수 있는 새로운 `IDependencyResolver` 인터페이스를 지원합니다.

MVC 3의 DI에 대한 자세한 내용은 다음 리소스를 참조하십시오.

- [브래드 윌슨의 서비스 위치에 대한 블로그 게시물 시리즈](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [MVC 3 릴리스 노트](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a>기타 새로운 기능

### <a name="nuget-integration"></a>NuGet 통합

ASP.NET MVC 3은 자동으로 설치및 설치의 일환으로 NuGet을 활성화합니다. NuGet은 프로젝트에서 .NET 라이브러리 및 도구를 쉽게 찾고, 설치하고, 사용할 수 있는 무료 오픈 소스 패키지 관리자입니다. 모든 Visual Studio 프로젝트 유형(웹 양식 및 ASP.NET MVC 포함)ASP.NET 함께 작동합니다.

NuGet을 사용하면 오픈 소스 프로젝트(예: Moq, NHibernate, Ninject, StructureMap, NUnit, Windsor, RhinoMocks 및 Elmah)를 유지 관리하는 개발자가 라이브러리를 패키징하고 온라인 갤러리에 등록할 수 있습니다. 그런 다음 이러한 라이브러리 중 하나를 사용하여 패키지를 찾고 작업 중인 프로젝트에 설치하려는 .NET 개발자가 쉽게 사용할 수 있습니다.

ASP.NET 3 도구 업데이트와 함께, 프로젝트 템플릿은 자바 스크립트 라이브러리가 사전 설치된 NuGet 패키지를 포함, 그래서 그들은 NuGet을 통해 업 데이터. 엔터티 프레임워크 코드 우선은 NuGet 패키지로 사전 설치됩니다.

NuGet에 대한 자세한 내용은 [NuGet 설명서](https://docs.microsoft.com/nuget/)를 참조하세요.

### <a name="partial-page-output-caching"></a>부분 페이지 출력 캐싱

ASP.NET MVC는 버전 1 이후 전체 페이지 응답의 출력 캐싱을 지원했습니다. 또한 MVC 3는 부분 페이지 출력 캐싱을 지원하므로 응답의 영역이나 조각을 쉽게 캐시할 수 있습니다. 캐싱에 대한 자세한 내용은 MVC 3 릴리스 후보및 [MVC 3 릴리스 노트의](../whitepapers/mvc3-release-notes.md) **자식 작업 출력 캐싱** [섹션에 대한 Scott Guthrie의 블로그 게시물의](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) **부분 페이지 출력 캐싱** 섹션을 참조하십시오.

### <a name="granular-control-over-request-validation"></a>요청 유효성 검사에 대한 세분화된 제어

ASP.NET MVC에는 XSS 및 HTML 주입 공격으로부터 자동으로 보호하는 데 도움이 되는 기본 제공 요청 유효성 검사가 있습니다. 그러나 사용자가 HTML 콘텐츠(예: 블로그 항목 또는 CMS 콘텐츠)를 게시하도록 하려는 경우와 같이 요청 유효성 검사를 명시적으로 사용하지 않도록 설정하려는 경우가 있습니다. 이제 [AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx) 특성을 모델 또는 뷰 모델에 추가하여 모델 바인딩 중에 속성별로 요청 유효성 검사를 비활성화할 수 있습니다. 요청 유효성 검사에 대한 자세한 내용은 다음 리소스를 참조하십시오.

- [MVC 3 릴리스 후보에 대한 스콧 거스리의 블로그 게시물에](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)있는 **눈에 거슬리지 않는 자바스크립트 및 유효성 검사** 섹션.
- [MVC 3 릴리스 노트](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a>확장 가능한 "새 프로젝트" 대화 상자

ASP.NET MVC 3에서는 **새 프로젝트** 대화 상자에 프로젝트 템플릿, 보기 엔진 및 단위 테스트 프로젝트 프레임워크를 추가할 수 있습니다.

### <a name="template-scaffolding-improvements"></a>템플릿 스캐폴딩 개선 사항

ASP.NET MVC 3 스캐폴딩 템플릿은 모델에서 기본 키 속성을 식별하고 이전 버전의 MVC보다 적절하게 처리하는 작업을 수행합니다. 예를 들어 스캐폴딩 템플릿은 이제 기본 키가 편집 가능한 양식 필드로 스캐폴딩되지 않았는지 확인합니다.

기본적으로 스캐폴드 만들기 및 편집은 이제 `Html.EditorFor` 도우미 대신 `Html.TextBoxFor` 도우미를 사용합니다. 이렇게 하면 **보기 추가** 대화 상자에서 뷰를 생성할 때 데이터 추가 특성 의 형태로 모델의 메타데이터에 대한 지원이 향상됩니다.

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a>"Html.LabelFor" 및 "Html.LabelForModel"에 대한 새 오버로드

및 `LabelForModel` 도우미 메서드에 대해 `LabelFor` 새 메서드 오버로드가 추가되었습니다. 새 오버로드를 사용하면 레이블 텍스트를 지정하거나 재정의할 수 있습니다.

### <a name="sessionless-controller-support"></a>세션리스 컨트롤러 지원

ASP.NET MVC 3에서는 컨트롤러 클래스가 세션 상태를 사용할지 여부를 나타낼 수 있으며, 그렇다면 세션 상태를 읽기/쓰기 또는 읽기 전용으로 사용할지 여부를 나타낼 수 있습니다. 세션리스 컨트롤러 지원에 대한 자세한 내용은 [MVC 3 릴리스 노트를](../whitepapers/mvc3-release-notes.md)참조하십시오.

### <a name="new-additionalmetadataattribute-class"></a>새로운 "추가 메타성 특성" 클래스

[AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx) 특성을 사용하여 모델 속성에 대한 사전을 `ModelMetadata.AdditionalValues` 채울 수 있습니다. 예를 들어 뷰 모델에 관리자에게만 표시해야 하는 속성이 있는 경우 다음 예제와 같이 해당 속성에 추가할 수 있습니다.

[!code-csharp[Main](mvc3/samples/sample4.cs)]

이 메타데이터는 제품 뷰 모델이 렌더링될 때 모든 디스플레이 또는 편집기 템플릿에서 사용할 수 있습니다. 메타데이터 정보를 해석하는 것은 귀하의 것입니다.

### <a name="accountcontroller-improvements"></a>계정 컨트롤러 개선 사항

인터넷 프로젝트 템플릿의 AccountController가 크게 개선되었습니다.

### <a name="new-intranet-project-template"></a>새 인트라넷 프로젝트 템플릿

Windows 인증을 활성화하고 AccountController를 제거하는 새 인트라넷 프로젝트 템플릿이 포함되어 있습니다.
