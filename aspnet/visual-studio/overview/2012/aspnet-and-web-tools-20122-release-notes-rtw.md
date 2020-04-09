---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET 및 웹 도구 2012.2 릴리스 노트 | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET 및 웹 도구 2012.2에 대한 릴리스 정보.
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: abd6d8ce0646852a194369589cb730fc98ecb3ad
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675906"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a>ASP.NET 및 Web Tools 2012.2 릴리스 정보

> 이 문서에서는 ASP.NET 및 웹 도구 2012.2의 릴리스에 대해 설명합니다. 그것은 비주얼 스튜디오 웹 도구 및 ASP.NET 대한 업데이트입니다.

- [설치 노트](#_Installation)
- [문서](#_Documentation)
- [지원](#_Support)
- [소프트웨어 요구 사항](#_Software_Requirements)
- [ASP.NET 및 웹 도구 2012.2의 새로운 기능](#_New_Features_in)

    - [도구](#_Tooling)
    - [웹 게시](#_Web_Publishing)
    - [ASP.NET MVC 템플릿](#_Templates)
    - [ASP.NET Web API](#_ASP.NET_Web_API)

    - [ASP.NET SignalR](#_ASP.NET_SignalR)
    - [ASP.NET URL](#_ASP.NET_Friendly_URLs)
- [알려진 문제 및 주요 변경 사항](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a>설치 참고 사항

ASP.NET 및 웹 도구 2012 Visual Studio 2012용 웹 [플랫폼 설치 관리자를](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)사용하여 설치할 수 있습니다. 이 업데이트는 웹용 Visual Studio 2012 또는 Visual Studio Express 2012에 대한 업데이트입니다. Visual Studio가 설치되어 있지 않으면 웹용 Visual Studio Express 2012가 설치됩니다.

ASP.NET 및 웹 도구 2012.2를 수동으로 설치할 수도 있습니다. 웹에 대해 Visual Studio 2012 또는 Visual Studio Express 2012가 설치되어 있어야 합니다. 그런 다음 다음 지침을 사용합니다. 

1. 다운로드 센터에서 [ASP.NET 및 웹 프레임워크 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) 설치 프로그램을 다운로드합니다.
2. 메시지가 표시되면 실행을 클릭합니다. 파일을 저장하여 나중에 실행할 수도 있습니다.
3. 업데이트할 Visual Studio 버전을 확인합니다. 업데이트하려는 Visual Studio를 실행하여 이 작업을 수행할 수 있습니다. 그런 다음 도움말 메뉴 항목을 클릭합니다.   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. 웹용 Microsoft Visual &quot;Studio 2012에 대한&quot; 메뉴 항목이 표시되면 [웹 개발자 도구 2012.2 - Visual Studio Express 2012 웹을](https://go.microsoft.com/fwlink/?LinkID=282228)다운로드합니다. 그렇지 않으면 [다운로드 웹 개발자 도구 2012.2 - Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228).
5. 메시지가 표시되면 실행을 클릭합니다. 파일을 저장하여 나중에 실행할 수도 있습니다.

> [!NOTE]
> ASP.NET 및 웹 도구 2012.2 릴리스에는 SQL Server 데이터 도구가 포함되어 있지 않습니다. SQL Server 및 Windows Azure SQL Databases는 오프라인 프로젝트 지원 개발, 스키마 비교 및 향상된 데이터베이스 배포 기능을 비롯한 다양한 데이터베이스 도구 집합을 제공합니다. 자세한 내용은 또는 SQL Server 데이터 [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127)도구를 설치하려면 을 방문하십시오.

<a id="_Documentation"></a>
## <a name="documentation"></a>문서화

ASP.NET 및 웹 도구 2012.2에 대한 자습서 및 기타 https://www.asp.net)정보는 ASP.NET 웹 사이트 (.

<a id="_Support"></a>
## <a name="support"></a>고객 지원팀

ASP.NET 및 웹 도구 2012.2는 공식적으로 릴리스 및 지원됩니다. 일반 지원 채널을 사용할 수 있습니다. ASP.NET 커뮤니티 구성원이 자주 비공식적인[https://forums.asp.net/](https://forums.asp.net/)지원을 제공할 수 있는 ASP.NET 포럼()에 질문을 게시할 수도 있습니다.

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>소프트웨어 요구 사항

ASP.NET 및 웹 도구 2012.2에는 웹용 Visual Studio 2012 또는 Visual Studio Express 2012가 필요합니다.

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>ASP.NET 및 웹 도구 2012.2의 새로운 기능

이 섹션에서는 ASP.NET 및 웹 도구 2012.2 릴리스에서 소개된 기능에 대해 설명합니다.

<a id="_Tooling"></a>
### <a name="tooling"></a>도구

- 페이지 검사기 

    - 페이지 검사기에서 페이지에 동적으로 추가된 항목을 해당 JavaScript 코드로 다시 매핑할 수 있도록 JavaScript 선택 매핑을 지원합니다.
    - CSS업데이트를 실시간으로 확인할 수 있는 기능.
    - 자세한 내용은 [페이지 검사기에서 CSS 자동 동기화 및 자바 스크립트 선택 매핑을](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)참조하십시오.
- 편집기 

    - 커피스크립트, 콧수염, 핸들바 및 JSRender에 대한 강조 표시 구문을 지원합니다.
    - HTML 편집기는 녹아웃 바인딩에 대한 Intellisense를 제공합니다.
    - LESS를 사용하여 동적 CSS를 구축할 수 있도록 적은 편집 및 컴파일러 지원.
    - JSON을 .NET 클래스로 붙여 넣습니다. 이 특수 붙여넣기 명령을 사용하여 JSON을 C# 또는 VB.NET 코드 파일에 붙여 넣으며 Visual Studio는 JSON에서 유추된 .NET 클래스를 자동으로 생성합니다.
- 모바일 에뮬레이터 지원은 확장성 후크를 추가하여 타사 에뮬레이터를 VSIX로 설치할 수 있습니다. 설치된 에뮬레이터는 F5 드롭다운에 표시되므로 개발자는 다양한 모바일 장치에서 웹 사이트를 미리 볼 수 있습니다. 이 기능에 대한 자세한 내용은 [Visual Studio와의 새로운 BrowserStack 통합에](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)대한 Scott Hanselman의 블로그 항목에서 확인합니다.

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>웹 게시

- 이제 웹 사이트 프로젝트에 Windows Azure 웹 사이트에 게시하는 것을 비롯한 웹 응용 프로그램 프로젝트와 동일한 게시 환경이 있습니다.
- 하나 이상의 파일에 대해 선택적 게시 &#8211; 다음 작업을 수행할 수 있습니다(웹 배포 끝점에 게시한 후):. 

    - 선택한 파일을 게시합니다.
    - 로컬 파일과 원격 파일의 차이점을 확인합니다.
    - 원격 파일로 로컬 파일을 업데이트하거나 로컬 파일로 원격 파일을 업데이트합니다.

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>ASP.NET MVC 템플릿

- 새로운 Facebook 응용 프로그램 템플릿 덕분에 Facebook Canvas 응용 프로그램을 쉽게 쓸 수 있습니다. 간단한 몇 단계 만에 로그인한 사용자로부터 데이터를 가져오고 해당 사용자의 친구와 통합하는 Facebook 응용 프로그램을 만들 수 있습니다. 템플릿에는 인증, 사용 권한, Facebook 데이터 액세스 등을 비롯하여 Facebook 응용 프로그램 작성과 관련된 모든 배관을 처리하기 위한 새 라이브러리가 포함되어 있어 Facebook 응용 프로그램 템플릿 사용에 [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921)대한 자세한 내용은 을 참조하십시오.
- 새로운 단일 페이지 응용 프로그램 MVC 템플릿을 통해 개발자는 ASP.NET Web API뿐 아니라 HTML 5, CSS 3, 잘 알려진 Knockout 및 jQuery JavaScript 라이브러리를 사용하여 대화형 클라이언트 쪽 웹 응용 프로그램을 만들 수 있습니다. 템플릿에는 RESTful 서버 API를 사용하는 JavaScript HTML5 응용 프로그램을 빌드하는 일반적인 방법을 보여 주는 "할 일" 목록 응용 프로그램이 포함되어 있습니다. 자세한 내용은 에서 [https://www.asp.net/single-page-application](../../../single-page-application/index.md)확인할 수 있습니다.
- 이제 ASP.NET MVC 새 프로젝트 대화 상자에 새 템플릿을 추가하는 VSIX를 만들 수 있습니다. 여기에서 방법을 알아보십시오.[https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- FixedDisplayModes 패키지 &#8211; MVC 프로젝트 템플릿은 새로운 'FixedDisplayModes' NuGet 패키지를 포함 하도록 업데이트 되었습니다., MVC 4에서 버그에 대 한 해결 방법을 포함 하는. 패키지에 포함된 수정 문서에 대한 자세한 내용은 MVC[https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)팀의 이 블로그 게시물()을 참조하십시오.

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET 웹 API는 다음과 같은 몇 가지 새로운 기능으로 향상되었습니다.

- ASP.NET 웹 API OData
- ASP.NET 웹 API 추적
- ASP.NET 웹 API 도움말 페이지

#### <a name="aspnet-web-api-odata"></a>ASP.NET 웹 API OData

ASP.NET 웹 API OData는 모든 데이터 원본에 대한 풍부한 비즈니스 논리를 사용하여 OData 끝점을 구축하는 데 필요한 유연성을 제공합니다. ASP.NET 웹 API OData를 사용하면 노출하려는 OData 의미 체계의 양을 제어할 수 있습니다. ASP.NET 웹 API OData는 ASP.NET MVC 4 프로젝트 템플릿에 포함되어[http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)있으며 NuGet ()에서도 사용할 수 있습니다.

ASP.NET 웹 API OData는 현재 다음과 같은 기능을 지원합니다.

- [쿼리 가능] 특성을 적용하여 OData 쿼리 의미 체계를 활성화합니다.
- OData 쿼리의 유효성을 쉽게 검사하고 지원되는 쿼리 옵션, 연산자 및 함수 집합을 제한합니다.
- 매개 변수는 ODataQueryOptions에 직접 바인딩하여 IQueryable 또는 IEnumerable에 유효성을 검사하고 적용할 수 있는 쿼리의 추상 구문 트리 표현을 가져옵니다.
- [쿼리 가능] 특성에 결과 제한을 지정하여 서비스 기반 페이징 및 다음 페이지 링크 생성을 활성화합니다.
- $inlinecount 사용하여 일치하는 총 리소스 수의 인라인 된 수를 요청합니다.
- null 전파를 제어합니다.
- $filter 모든 연산자.
- 규칙에 따라 엔터티 데이터 모델을 추론하거나 엔터티 프레임워크 코드-First와 유사한 방식으로 모델을 명시적으로 사용자 지정합니다.
- EntitySetController에서 파생 하여 엔터티 집합을 노출 합니다.
- 탐색 속성을 노출하고 링크를 조작하며 OData 작업을 구현하기 위한 간단하고 사용자 지정 가능한 규칙입니다.
- MapODataRoute 확장 방법을 사용하여 간소화된 라우팅입니다.
- 여러 EDM 모델을 노출하여 버전 전환 지원
- 웹 API에 대한 클라이언트(.NET, Windows Phone, Windows 스토어 등)를 생성할 수 있도록 서비스 문서 및 $metadata 노출합니다.
- OData 원자, JSON 및 JSON 자세한 형식에 대한 지원.
- 엔터티를 생성, 업데이트, 부분적으로 업데이트(PATCH) 및 삭제합니다.
- 엔터티 간의 관계를 쿼리하고 조작합니다.
- 경로에 연결되는 관계 링크를 만듭니다.
- 복합 형식
- 엔터티 형식 상속입니다.
- 컬렉션 속성입니다.
- 열거형.
- OData 작업입니다.
- WCF 데이터 서비스와 동일한 기반, 즉 ODataLib[http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)()에 구축.

ASP.NET 웹 API OData에 [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141)대한 자세한 내용은 를 참조하십시오.

#### <a name="aspnet-web-api-tracing"></a>ASP.NET 웹 API 추적

ASP.NET 웹 API 추적은 웹 API의 추적 데이터를 .NET 추적과 통합합니다. 이제 웹 API 프로젝트 템플릿에서 기본적으로 활성화됩니다. 웹 API에 대한 추적 데이터는 출력 창으로 전송되며 IntelliTrace를 통해 사용할 수 있습니다. ASP.NET 웹 API 추적을 사용하면 Windows Azure 진단과의 통합을 통해 Windows Azure에서 호스팅될 때 웹 API에 대한 정보를 [추적할 수 있습니다.](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx) ASP.NET 웹 API 추적 NuGet 패키지()를[http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)사용하여 모든 응용 프로그램에서 ASP.NET 웹 API 추적을 설치하고 활성화할 수도 있습니다.

웹 API 추적을 구성하고 사용하는 방법에 대한 [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874)자세한 내용은 ASP.NET.

#### <a name="aspnet-web-api-help-page"></a>ASP.NET 웹 API 도움말 페이지

이제 ASP.NET 웹 API 도움말 페이지가 기본적으로 웹 API 프로젝트 템플릿에 포함됩니다. ASP.NET 웹 API 도움말 페이지는 HTTP 끝점, 지원되는 HTTP 메서드, 매개 변수 및 예제 요청 및 응답 메시지 페이로드를 포함한 웹 API에 대한 설명서를 자동으로 생성합니다. 코드의 주석에서 설명서가 자동으로 가져옵니다. ASP.NET 웹 API 도움말 페이지 NuGet 패키지 ()를[http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)사용하여 모든 응용 프로그램에 ASP.NET 웹 API 도움말 페이지를 추가할 수도 있습니다.

ASP.NET 웹 API 도움말 페이지를 설정하고 사용자 지정하는 [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140)방법에 대한 자세한 내용은 을 참조하십시오.

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>ASP.NET SignalR

ASP.NET SignalR을 사용하면 사용 가능한 경우 WebSockets를 사용하여 ASP.NET 응용 프로그램에 실시간 웹 기능을 쉽게 추가할 수 있으며 그렇지 않을 경우 자동으로 다른 기술로 되돌아갑니다.

ASP.NET 신호기 사용에 대한 [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271)자세한 내용은 를 참조하십시오.

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>ASP.NET URL

ASP.NET FriendlyURLs를 사용하면 웹 양식 개발자가 .aspx 확장 없이 도서 URL을 더욱 쉽게 생성할 수 있습니다. 구성이 거의 또는 전혀 필요하지 않으며 기존 ASP.NET v4.0 응용 프로그램과 함께 사용할 수 있습니다. 또한 FriendlyURLs 기능을 사용하면 데스크톱과 모바일 보기 간의 전환을 지원하여 개발자가 응용 프로그램에 모바일 지원을 더 쉽게 추가할 수 있습니다.

ASP.NET 사용 친화적 인 URL을 설치및 [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)사용하는 방법에 대한 자세한 내용은 를 참조하십시오.

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>알려진 문제 및 주요 변경 사항

이 섹션에서는 ASP.NET 및 웹 도구 2012.2 릴리스에 있는 알려진 문제 및 주요 변경 사항에 대해 설명합니다.

### <a name="installation-issues"></a>설치 이슈

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>비주얼 스튜디오 2012의 순서 에서 설치

ASP.NET 및 웹 도구 2012.2를 설치한 후 Visual Studio 2012의 SKU를 추가로 설치하려면 복구 작업이 필요합니다. 다음과 같은 시퀀스를 고려해 보세요.

1. 웹용 비주얼 스튜디오 2012 익스프레스 설치
2. ASP.NET 및 웹 도구 설치 2012.2
3. 비주얼 스튜디오 설치 2012 전문가, 프리미엄 또는 궁극적 인

2단계는 웹용 Express용 업데이트만 설치합니다. 3단계에서 설치된 추가 SKU에 업데이트가 포함되어 있는지 확인하려면 ASP.NET 및 웹 도구 2012.2를 복구하여 마지막으로 설치된 SKU에 대한 업데이트를 설치해야 합니다. 이는 1단계와 3단계의 SCO가 역전되는 경우에도 적용됩니다.

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>Visual Studio가 열려 있을 때 Microsoft ASP.NET 및 웹 도구 설치 2012.2

MICROSOFT ASP.NET 및 웹 도구 2012.2를 설치하는 동안 VS가 열려 있으면 Visual Studio가 불량 상태가 될 수 있습니다. 설치를 진행하기 전에 Visual Studio의 모든 인스턴스를 닫는 것이 좋습니다.

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>설치 중에 ASP.NET 및 웹 도구 2012.2 설치 취소

설치 중에 ASP.NET 및 웹 도구 2012.2 설정을 취소하면 Visual Studio가 불량 상태가 됩니다. 이 문제를 해결하려면 다음 단계를 따르십시오. 

- 프로그램 추가/제거로 이동합니다.
- 제거 마이크로 소프트 ASP.NET 웹 도구 2012.2, 있는 경우.
- 마이크로소프트 ASP.NET 및 웹 도구 2012.2 다시 설치

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>ASP.NET 및 웹 도구 2012.2를 제거 한 후 ASP.NET MVC 4 템플릿 및 Razor v2 웹 사이트 템플릿이 누락되었습니다.

ASP.NET 및 웹 도구 2012.2를 제거하면 Visual Studio 2012에서 ASP.NET MVC 4 및 Razor v2 웹 사이트 템플릿도 모두 제거됩니다.

해결 방법은 Visual Studio 2012 설치를 복구하여 ASP.NET MVC 4 및 Razor v2 웹 사이트 템플릿을 다시 설치하는 것입니다.

### <a name="tooling-issues"></a>툴링 문제

#### <a name="nuget-error-reported-during-project-creation"></a>NuGet 프로젝트 생성 중에 보고된 오류

ASP.NET 및 웹 도구 2012.2를 설치한 후 MVC 4 프로젝트를 만들 때 다음과 같은 오류가 표시될 수 있습니다.

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

ASP.NET 및 웹 도구 2012.2는 NuGet 2.1을 제공하며 Visual Studio 2012에서 확장을 업그레이드합니다. 경우에 따라 VSIX 설치 프로그램이 VSIX를 올바르게 업데이트하지 못합니다. 다음 단계를 통해 이 문제를 해결할 수 있습니다.

1. 관리자로 Visual Studio 2012 시작
2. 도구-&gt;확장 및 업데이트로 이동하여 NuGet을 제거합니다.
3. Visual Studio를 닫습니다.
4. ASP.NET 및 웹 도구 2012.2 설치 폴더로 이동:

    1. 비주얼 스튜디오 2012: **프로그램 파일\마이크로소프트 ASP.NET\ASP.NET 웹 스택\비주얼 스튜디오 2012**
    2. 웹용 비주얼 스튜디오 2012 익스프레스: **프로그램 파일\Microsoft ASP.NET\ASP.NET 웹 스택\비주얼 스튜디오 익스프레스 2012 웹용**
5. NuGet.Tools.v6를 두 번 클릭하여 NuGet을 다시 설치합니다.

### <a name="web-api-issues"></a>웹 API 문제

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>$filter 및 DateTime 리터럴의 구문 분석 문제

OData URI 파서는 부분 datetime 리터럴을 제대로 구문 분석하지 못합니다. 예를 들어 $filter=시작 eq datetime'2012-12-31T12:00'이 제대로 구문 분석되지 않습니다. 해결 방법은 전체 리터럴 $filter=start eq datetime'2012-12-31T12:00:00'를 사용하는 것입니다.

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData대/소문자를 구분하지 않는 속성 이름을 지원하지 않습니다.

OData는 OData 쿼리 및 odata 경로에서 대/소문자를 구분하지 않는 속성 이름을 지원하지 않습니다. 작업 항목 보기:

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

사용자가 자바 스크립트 클라이언트 측과 서버 측에서 다른 대/소문자를 가지고 있다면 이 문제가 발생할 수 있습니다. 이 문제는 odata 프로토콜의 설계에 의한 문제입니다. 그러나 많은 사용자가이 문제를 보고 합니다. 이 방법을 해결하려면 사용자가 URL에서 서비스 케이스를 수정해야 합니다.

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>기본 OData 라우팅 규칙은 탐색 속성에 POST/PUT을 지원하지 않습니다.

기본 OData 라우팅 규칙은 탐색 속성에 POST/PUT을 지원하지 않습니다. 작업 항목 [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)을 참조하십시오. 기본 규칙에서 일반적으로 사용되는 이 규칙이 없습니다.

이 방법을 해결하려면 이를 지원하기 위해 새 라우팅 규칙을 확장해야 합니다.

### <a name="facebook-template-issues"></a>페이스 북 템플릿 문제

#### <a name="facebook-application-template-only-works-using-net-45"></a>페이스 북 응용 프로그램 템플릿은 .NET 4.5를 사용하여 작동

새 프로젝트 대화 상자의 프레임워크 드롭다운 목록에서 .NET 4.5를 선택하여 MVC 4에서 Facebook 응용 프로그램 템플릿을 ASP.NET.

#### <a name="real-time-update-controller"></a>실시간 업데이트 컨트롤러

페이스 북 응용 프로그램 템플릿은 사용자가 쉽게 페이스 북에서 실시간 업데이트를 처리하는 웹 API 컨트롤러를 만들 수 있습니다. 개발 컴퓨터가 NAT 뒤에 있는 경우 추가 네트워크 구성 없이 컨트롤러가 작동하지 않을 수 있습니다. 자세한 내용은 여기를 참조하십시오.[http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>쿼리 문자열 값은 Facebook OAuth 매개 변수와 충돌합니다.

다음 필드는 Facebook OAuth 대화 상자의 호출 다시 URL과 충돌합니다. 코드, 오류, 오류\_설명, 오류\_이유 : 다음 이름으로 자신의 쿼리 문자열 값을 추가하지 마십시오.

#### <a name="using-page-inspector-with-facebook-template"></a>페이스 북 템플릿페이지 관리자를 사용하여

Facebook 응용 프로그램을 디버깅하는 동안 Visual Studio 2012의 페이지 검사기 기능을 사용할 수 없습니다. 페이지 검사기는 현재 iframes를 지원하지 않습니다.

### <a name="single-page-application-template-issues"></a>단일 페이지 응용 프로그램 템플릿 문제

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>JQuery 1.9/녹아웃 2.2.1 업데이트를 사용하면 기본 MVC SPA 프로젝트를 실행할 때 새 할 일 항목 편집 enter 포커스 이벤트가 제대로 처리되지 않습니다.

JQuery 1.9/녹아웃 2.2.1 업데이트를 통해 기본 MVC SPA 프로젝트를 실행할 때 새로운 할 일 항목 편집이 더 이상 새 할 일 항목을 할 일 목록에 입력한 후 새 할 일 항목 편집 상자에 다시 초점을 맞추지 않습니다.

해결 방법 [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html)참조 및 다음 샘플 코드와 유사한 수정을 수행하려면 다음을 수행합니다.

파일 todo.model.js  
 함수 todolist(데이터)를 추가하고 다음을 추가합니다.  
 **self.is선택 = ko.관찰 가능(false);**

함수 todoList.prototype.addTodo, 다음 검게 칠한 텍스트를 추가합니다.  
 **self.is선택됨(true);**  
 self.newTodoTitle&quot;&quot;();

File index.cshtml을 추가하고 다음 검정 텍스트를 추가합니다.  
 &lt;양식 데이터 바인딩=&quot;제출: addTodo&quot;&gt;  
 &lt;입력 클래스&quot;=&quot; addTodo&quot; type =&quot;&quot;텍스트 데이터 바인딩 = 값: newTodoTitle, 자리 표시자: '추가하려면 여기 입력', blurOnEnter: true, **hasfocus: 선택됨**, 이벤트: { 흐림: addTodo }&quot; /&gt;  
 &lt;/양식&gt;
