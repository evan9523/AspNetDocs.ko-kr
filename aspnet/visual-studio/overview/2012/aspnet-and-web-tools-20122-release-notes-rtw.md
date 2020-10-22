---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET 및 Web Tools 2012.2 릴리스 정보 | Microsoft Docs
author: rick-anderson
description: ASP.NET 및 Web Tools 2012.2에 대 한 릴리스 정보입니다.
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: abd6d8ce0646852a194369589cb730fc98ecb3ad
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345592"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a>ASP.NET 및 Web Tools 2012.2 릴리스 정보

> 이 문서에서는 ASP.NET 및 Web Tools 2012.2의 릴리스를 설명 합니다. Visual Studio 웹 도구 및 ASP.NET에 대 한 업데이트입니다.

- [설치 참고 사항](#_Installation)
- [설명서](#_Documentation)
- [지원](#_Support)
- [소프트웨어 요구 사항](#_Software_Requirements)
- [ASP.NET 및 Web Tools 2012.2의 새로운 기능](#_New_Features_in)

    - [도구](#_Tooling)
    - [웹 게시](#_Web_Publishing)
    - [ASP.NET MVC 템플릿](#_Templates)
    - [ASP.NET Web API](#_ASP.NET_Web_API)

    - [ASP.NET SignalR](#_ASP.NET_SignalR)
    - [ASP.NET URL](#_ASP.NET_Friendly_URLs)
- [알려진 문제 및 주요 변경 내용](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a>설치 참고 사항

[웹 플랫폼 설치 관리자](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)를 사용 하 여 Visual Studio 2012 ASP.NET 및 Web Tools 2012.2를 설치할 수 있습니다. 이 업데이트는 Visual Studio 2012 또는 Web의 Visual Studio Express 2012 (필수) 업데이트입니다. Visual Studio가 설치 되어 있지 않으면 웹에 대 한 Visual Studio Express 2012이 설치 됩니다.

ASP.NET 및 Web Tools 2012.2를 수동으로 설치할 수도 있습니다. Visual Studio 2012 또는 Visual Studio Express 2012 for Web이 설치 되어 있어야 합니다. 그런 다음, 다음 지침을 사용 합니다. 

1. 다운로드 센터에서 [ASP.NET 및 웹 프레임 워크 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) 설치 관리자를 다운로드 합니다.
2. 메시지가 표시 되 면 실행을 클릭 합니다. 나중에 실행할 수 있도록 파일을 저장할 수도 있습니다.
3. 업데이트 되는 Visual Studio 버전을 확인 합니다. 업데이트 하려는 Visual Studio를 시작 하 여이 작업을 수행할 수 있습니다. 그런 다음 도움말 메뉴 항목을 클릭 합니다.   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. &quot;웹에 대 한 Microsoft Visual Studio 2012에 대 한 메뉴 항목이 표시 되 면 웹 &quot; [개발자 도구 2012.2-Visual Studio Express 2012 for web을](https://go.microsoft.com/fwlink/?LinkID=282228)다운로드 합니다. 그렇지 않으면 [웹 개발자 도구 2012.2-Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228)를 다운로드 합니다.
5. 메시지가 표시 되 면 실행을 클릭 합니다. 나중에 실행할 수 있도록 파일을 저장할 수도 있습니다.

> [!NOTE]
> ASP.NET 및 Web Tools 2012.2 릴리스에는 SQL Server Data Tools 포함 되지 않습니다. SQL Server 및 Windows Azure SQL 데이터베이스는 오프 라인 프로젝트 지원 개발, 스키마 비교 및 향상 된 데이터베이스 배포 기능을 비롯 한 다양 한 데이터베이스 도구 집합을 제공 합니다. 자세한 내용을 보거나 설치 하려면 SQL Server Data Tools 방문 [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127) 하세요.

<a id="_Documentation"></a>
## <a name="documentation"></a>문서화

ASP.NET 및 Web Tools 2012.2에 대 한 자습서 및 기타 정보는 ASP.NET 웹 사이트 ()에서 제공 됩니다 https://www.asp.net) .

<a id="_Support"></a>
## <a name="support"></a>지원

ASP.NET 및 Web Tools 2012.2은 공식적으로 출시 되 고 지원 됩니다. 일반 지원 채널을 사용할 수 있습니다. [https://forums.asp.net/](https://forums.asp.net/)ASP.NET 커뮤니티의 멤버가 비공식적 지원을 자주 제공할 수 있는 ASP.NET 포럼 ()에도 질문을 게시할 수 있습니다.

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>소프트웨어 요구 사항

ASP.NET 및 Web Tools 2012.2에는 Visual Studio 2012 또는 Visual Studio Express 2012 for Web이 필요 합니다.

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>ASP.NET 및 Web Tools 2012.2의 새로운 기능

이 섹션에서는 ASP.NET 및 Web Tools 2012.2 릴리스에 도입 된 기능을 설명 합니다.

<a id="_Tooling"></a>
### <a name="tooling"></a>도구

- 페이지 검사기 

    - JavaScript 선택 매핑을 지원 하 여 페이지에 동적으로 추가 된 항목을 해당 JavaScript 코드로 다시 매핑할 수 페이지 검사기.
    - CSS 업데이트를 실시간으로 볼 수 있는 기능입니다.
    - 자세한 내용은 [페이지 검사기에서 CSS 자동 동기화 및 JavaScript 선택 매핑](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)을 참조 하세요.
- 편집기 

    - CoffeeScript, Mustache, Handlebars 및 JsRender에 대 한 구문 강조 표시를 지원 합니다.
    - HTML 편집기는 녹아웃 바인딩을 위한 Intellisense를 제공 합니다.
    - LESS를 사용 하 여 동적 CSS를 구축할 수 있도록 하는 편집 및 컴파일러 지원이 줄어듭니다.
    - JSON을 .NET 클래스로 붙여 넣습니다. 이 특수 붙여넣기 명령을 사용 하 여 c # 또는 VB.NET 코드 파일에 JSON을 붙여넣으면 Visual Studio에서는 JSON에서 유추 된 .NET 클래스를 자동으로 생성 합니다.
- 모바일 에뮬레이터 지원에서는 타사 에뮬레이터가 VSIX로 설치 될 수 있도록 확장성 후크를 추가 합니다. 개발자가 다양 한 모바일 장치에서 웹 사이트를 미리 볼 수 있도록 설치 된 에뮬레이터가 F5 드롭다운에 표시 됩니다. 이 기능에 대 한 자세한 내용은 [Visual Studio와의 새 BrowserStack 통합](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)의 Scott Hanselman의 블로그 항목을 참조 하세요.

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>웹 게시

- 웹 사이트 프로젝트는 이제 Windows Azure 웹 사이트에 게시를 비롯 한 웹 응용 프로그램 프로젝트와 동일한 게시 환경을 제공 합니다.
- 하나 이상의 파일에 대 한 선택적 게시 &#8211; 웹 배포 끝점에 게시 한 후 다음 작업을 수행할 수 있습니다. 

    - 선택한 파일을 게시 합니다.
    - 로컬 파일과 원격 파일의 차이점을 참조 하세요.
    - 원격 파일을 사용 하 여 로컬 파일을 업데이트 하거나 로컬 파일을 사용 하 여 원격 파일을 업데이트 합니다.

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>ASP.NET MVC 템플릿

- 새로운 Facebook 응용 프로그램 템플릿 덕분에 Facebook Canvas 응용 프로그램을 쉽게 쓸 수 있습니다. 간단한 몇 단계 만에 로그인한 사용자로부터 데이터를 가져오고 해당 사용자의 친구와 통합하는 Facebook 응용 프로그램을 만들 수 있습니다. 템플릿에는 인증, 사용 권한, Facebook 데이터 액세스 등을 비롯하여 Facebook 응용 프로그램 작성과 관련된 모든 배관을 처리하기 위한 새 라이브러리가 포함되어 있어 Facebook 응용 프로그램 템플릿 사용에 대 한 자세한 내용은을 참조 하십시오 [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921) .
- 새로운 단일 페이지 응용 프로그램 MVC 템플릿을 통해 개발자는 ASP.NET Web API뿐 아니라 HTML 5, CSS 3, 잘 알려진 Knockout 및 jQuery JavaScript 라이브러리를 사용하여 대화형 클라이언트 쪽 웹 응용 프로그램을 만들 수 있습니다. 템플릿에는 RESTful 서버 API를 사용 하는 JavaScript HTML5 응용 프로그램을 빌드하는 일반적인 방법을 보여 주는 "todo" 목록 응용 프로그램이 포함 되어 있습니다. 자세한 내용은에서 확인할 수 있습니다 [https://www.asp.net/single-page-application](../../../single-page-application/index.md) .
- 이제 ASP.NET MVC 새 프로젝트 대화 상자에 새 템플릿을 추가 하는 VSIX를 만들 수 있습니다. 자세한 내용은 다음을 참조 하세요. [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- FixedDisplayModes 패키지 &#8211; MVC 프로젝트 템플릿이 새로운 ' FixedDisplayModes ' NuGet 패키지를 포함 하도록 업데이트 되었습니다 .이 패키지에는 MVC 4에서 버그에 대 한 해결 방법이 포함 되어 있습니다. 패키지에 포함 된 수정 사항에 대 한 자세한 내용은 MVC 팀의이 블로그 게시물 ()을 참조 하세요 [https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) .

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET Web API은 몇 가지 새로운 기능으로 향상 되었습니다.

- ASP.NET Web API OData
- ASP.NET Web API 추적
- ASP.NET Web API 도움말 페이지

#### <a name="aspnet-web-api-odata"></a>ASP.NET Web API OData

ASP.NET Web API OData는 모든 데이터 원본에 대해 풍부한 비즈니스 논리를 사용 하 여 OData 끝점을 빌드하는 데 필요한 유연성을 제공 합니다. ASP.NET Web API OData를 통해 노출 하려는 OData 의미 체계의 양을 제어할 수 있습니다. ASP.NET Web API OData는 ASP.NET MVC 4 프로젝트 템플릿에 포함 되어 있으며 NuGet () 에서도 사용할 수 있습니다 [http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata) .

ASP.NET Web API OData는 현재 다음 기능을 지원 합니다.

- [쿼리 가능한] 특성을 적용 하 여 OData 쿼리 의미 체계를 사용 하도록 설정 합니다.
- OData 쿼리의 유효성을 쉽게 검사 하 고 지원 되는 쿼리 옵션, 연산자 및 함수 집합을 제한 합니다.
- 매개 변수는 ODataQueryOptions에 직접 바인딩하여 IQueryable 또는 IEnumerable에 유효성을 검사 하 고 적용할 수 있는 쿼리의 추상 구문 트리 표현을 가져옵니다.
- [쿼리 가능한] 특성에 대 한 결과 제한을 지정 하 여 서비스 기반 페이징 및 다음 페이지 링크 생성을 사용 하도록 설정 합니다.
- $Inlinecount를 사용 하 여 일치 하는 총 리소스 수의 인라인 수를 요청 합니다.
- Null 전파를 제어 합니다.
- $Filter의 Any/All 연산자입니다.
- 규칙에 따라 엔터티 데이터 모델을 유추 하거나 Entity Framework 코드 우선와 비슷한 방식으로 모델을 명시적으로 사용자 지정 합니다.
- EntitySetController에서 파생 하 여 엔터티 집합을 노출 합니다.
- 탐색 속성을 노출 하 고, 링크를 조작 하 고, OData 작업을 구현 하기 위한 간단한 사용자 지정 규칙입니다.
- MapODataRoute 확장 메서드를 사용 하는 간소화 된 라우팅입니다.
- 여러 EDM 모델을 노출 하 여 버전 관리를 지원 합니다.
- 웹 API에 대 한 클라이언트 (.NET, Windows Phone, Windows 스토어 등)를 생성할 수 있도록 서비스 문서와 $metadata를 노출 합니다.
- OData Atom, JSON 및 JSON 상세 형식에 대 한 지원.
- 엔터티를 만들고, 업데이트 하 고, 부분적으로 업데이트 (패치) 하 고 삭제 합니다.
- 엔터티 간의 관계를 쿼리하고 조작 합니다.
- 경로에 연결 되는 관계 링크를 만듭니다.
- 복합 형식
- 엔터티 형식 상속.
- 컬렉션 속성입니다.
- 열거.
- OData 작업입니다.
- WCF Data Services, 즉 ODataLib ()와 동일한 기반을 기반으로 작성 [http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata) 되었습니다.

ASP.NET Web API OData에 대 한 자세한 내용은을 참조 하십시오 [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141) .

#### <a name="aspnet-web-api-tracing"></a>ASP.NET Web API 추적

ASP.NET Web API 추적은 웹 Api의 추적 데이터를 .NET 추적과 통합 합니다. 이제 Web API 프로젝트 템플릿에서 기본적으로 사용 하도록 설정 됩니다. 웹 Api에 대 한 추적 데이터는 출력 창으로 전송 되며 IntelliTrace를 통해 사용할 수 있습니다. ASP.NET Web API 추적을 사용 하면 windows [Azure 진단](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx)와의 통합을 통해 windows Azure에서 호스트 되는 웹 API에 대 한 정보를 추적할 수 있습니다. ASP.NET Web API 추적 NuGet 패키지 ()를 사용 하 여 모든 응용 프로그램에서 ASP.NET Web API 추적을 설치 하 고 사용 하도록 설정할 수도 있습니다 [http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing) .

ASP.NET Web API 추적을 구성 하 고 사용 하는 방법에 대 한 자세한 내용은을 참조 하십시오 [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874) .

#### <a name="aspnet-web-api-help-page"></a>ASP.NET Web API 도움말 페이지

이제 ASP.NET Web API 도움말 페이지가 웹 API 프로젝트 템플릿에 기본적으로 포함 되어 있습니다. ASP.NET Web API 도움말 페이지는 HTTP 끝점, 지원 되는 HTTP 메서드, 매개 변수 및 예제 요청 및 응답 메시지 페이로드를 포함 하 여 웹 Api에 대 한 설명서를 자동으로 생성 합니다. 문서는 코드의 주석에서 자동으로 가져옵니다. ASP.NET Web API 도움말 페이지 NuGet 패키지 ()를 사용 하 여 모든 응용 프로그램에 ASP.NET Web API 도움말 페이지를 추가할 수도 있습니다 [http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage) .

ASP.NET Web API 도움말 페이지를 설정 하 고 사용자 지정 하는 방법에 대 한 자세한 내용은을 참조 하십시오 [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140) .

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>ASP.NET SignalR

ASP.NET SignalR를 사용 하면 사용 가능한 경우 Websocket을 사용 하 여 ASP.NET 응용 프로그램에 실시간 웹 기능을 간편 하 게 추가할 수 있으며, 그렇지 않은 경우 다른 기술로 자동으로 대체 됩니다.

ASP.NET SignalR 사용에 대 한 자세한 내용은을 참조 하십시오 [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271) .

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>ASP.NET URL

ASP.NET FriendlyURLs를 사용 하면 web forms 개발자가 간단한 Url (.aspx 확장명 제외)을 쉽게 생성할 수 있습니다. 구성이 거의 필요 하지 않으며 기존 ASP.NET v 4.0 응용 프로그램에서 사용할 수 있습니다. FriendlyURLs 기능을 사용 하면 개발자가 데스크톱과 모바일 보기 간의 전환을 지원 하 여 응용 프로그램에 모바일 지원을 더 쉽게 추가할 수 있습니다.

ASP.NET 친화적인 Url의 설치 및 사용에 대 한 자세한 내용은을 참조 하십시오 [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx) .

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>알려진 문제 및 주요 변경 내용

이 섹션에서는 ASP.NET 및 Web Tools 2012.2 릴리스에 있는 알려진 문제 및 주요 변경 내용에 대해 설명 합니다.

### <a name="installation-issues"></a>설치 이슈

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>Visual Studio 2012의 잘못 된 설치

ASP.NET 및 Web Tools 2012.2을 설치한 후 Visual Studio 2012의 추가 SKU를 설치 하려면 복구 작업이 필요 합니다. 다음과 같은 시퀀스를 고려해 보세요.

1. Visual Studio 2012 Express for Web 설치
2. ASP.NET 및 Web Tools 2012.2 설치
3. Visual Studio 2012 Professional, Premium 또는 Ultimate 설치

2 단계는 Express for Web에 대 한 업데이트를 설치 하는 경우에만 발생 합니다. 3 단계에서 설치 된 추가 SKU가 업데이트를 포함 하도록 하려면 설치 된 마지막 SKU에 대 한 업데이트를 설치 하기 위해 ASP.NET 및 Web Tools 2012.2를 복구 해야 합니다. 이는 1 단계 및 3 단계의 Sku가 반대로 된 경우에도 적용 됩니다.

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>Visual Studio를 열 때 Microsoft ASP.NET 및 Web Tools 2012.2 설치

Microsoft ASP.NET 및 Web Tools 2012.2을 설치 하는 동안 VS가 열려 있는 경우 Visual Studio가 잘못 된 상태가 될 수 있습니다. 설치를 계속 하기 전에 사용자가 Visual Studio의 모든 인스턴스를 닫는 것이 좋습니다.

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>설치 도중 ASP.NET 및 Web Tools 2012.2 설치를 취소 하는 중

설치 도중 ASP.NET 및 Web Tools 2012.2 설치를 취소 하면 Visual Studio가 잘못 된 상태로 유지 됩니다. 이 문제를 해결 하려면 다음 단계를 수행 합니다. 

- 프로그램 추가/제거로 이동합니다.
- Microsoft ASP.NET 및 Web Tools 2012.2 (있는 경우)을 제거 합니다.
- Microsoft ASP.NET 및 Web Tools 2012.2 다시 설치

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>ASP.NET 및 Web Tools 2012.2를 제거한 후 ASP.NET MVC 4 템플릿과 Razor v2 웹 사이트 템플릿이 누락 됨

ASP.NET 및 Web Tools 2012.2를 제거 하면 Visual Studio 2012에서 ASP.NET MVC 4 및 Razor v2 웹 사이트 템플릿도 모두 제거 됩니다.

해결 방법은 Visual Studio 2012 설치를 복구 하 여 ASP.NET MVC 4 및 Razor v2 웹 사이트 템플릿을 다시 설치 하는 것입니다.

### <a name="tooling-issues"></a>도구 문제

#### <a name="nuget-error-reported-during-project-creation"></a>프로젝트를 만드는 동안 NuGet 오류가 보고 되었습니다.

ASP.NET 및 Web Tools 2012.2를 설치한 후 MVC 4 프로젝트를 만들 때 다음과 같은 오류가 표시 될 수 있습니다.

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

ASP.NET 및 Web Tools 2012.2는 NuGet 2.1를 제공 하며 Visual Studio 2012에서 확장을 업그레이드 합니다. VSIX 설치 관리자가 VSIX를 올바르게 업데이트 하지 못하는 경우도 있습니다. 다음 단계를 통해이 문제를 해결할 수 있습니다.

1. 관리자 권한으로 Visual Studio 2012 시작
2. 도구- &gt; 확장 및 업데이트로 이동 하 고 NuGet을 제거 합니다.
3. Visual Studio 닫기
4. ASP.NET 및 Web Tools 2012.2 설치 폴더로 이동 합니다.

    1. Visual Studio 2012: **Program FILES\MICROSOFT Asp.net 웹 Stack\Visual studio 2012**
    2. Visual Studio 2012 Express for Web: **Program Files\Microsoft Visual Studio Express 2012 For web**
5. Nuget을 두 번 클릭 하 여 NuGet을 다시 설치 합니다.

### <a name="web-api-issues"></a>웹 API 문제

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>$filter 및 DateTime 리터럴의 구문 분석 문제

OData URI 파서가 부분 datetime 리터럴을 올바르게 구문 분석 하지 못했습니다. 예를 들어 $filter = start eq datetime ' 2012-12-31T12:00 '은 제대로 구문 분석 되지 않습니다. 해결 방법은 전체 리터럴 $filter = start eq datetime ' 2012-12-31T12:00:00 '을 사용 하는 것입니다.

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData는 대/소문자를 구분 하지 않는 속성 이름을 지원 하지 않습니다.

Odata는 OData 쿼리 및 odata 경로에서 대/소문자를 구분 하지 않는 속성 이름을 지원 하지 않습니다. 작업 항목을 참조 하세요.

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

사용자가 javascript 클라이언트 쪽 및 서버 쪽에서 대/소문자가 다른 경우에는이 문제가 발생할 수 있습니다. 이 문제는 odata 프로토콜에서 의도 된 것입니다. 그러나 많은 사용자가이 문제를 보고 합니다. 이러한 문제를 해결 하려면 사용자가 URL에서 해당 사례를 수정 해야 합니다.

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>기본 OData 라우팅 규칙은 탐색 속성에서 POST/PUT을 지원 하지 않습니다.

기본 OData 라우팅 규칙은 탐색 속성에서 POST/PUT을 지원 하지 않습니다. 작업 항목 [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366) 을 참조 하세요. 기본 규칙에서 일반적으로 사용 되는 규칙이 없습니다.

이 문제를 해결 하려면 사용자가 새 라우팅 규칙을 확장 하 여 지원 해야 합니다.

### <a name="facebook-template-issues"></a>Facebook 템플릿 문제

#### <a name="facebook-application-template-only-works-using-net-45"></a>Facebook 응용 프로그램 템플릿은 .NET 4.5을 사용 하는 경우에만 작동 합니다.

ASP.NET MVC 4에서 Facebook 응용 프로그램 템플릿을 보려면 새 프로젝트 대화 상자의 프레임 워크 드롭다운 목록에서 .NET 4.5을 선택 해야 합니다.

#### <a name="real-time-update-controller"></a>실시간 업데이트 컨트롤러

Facebook 응용 프로그램 템플릿을 사용 하면 사용자가 Facebook에서 실시간 업데이트를 처리 하는 Web API 컨트롤러를 쉽게 만들 수 있습니다. 개발 컴퓨터가 NAT 뒤에 있는 경우 추가 네트워크 구성 없이 컨트롤러가 작동 하지 않을 수 있습니다. 자세한 내용은 여기를 참조 하세요. [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>쿼리 문자열 값이 Facebook OAuth 매개 변수와 충돌 합니다.

다음 필드는 Facebook OAuth 대화 상자의 콜백 URL과 충돌 합니다. 다음 이름으로 고유한 쿼리 문자열 값을 추가 하지 마세요. 코드, 오류, 오류 \_ 설명, 오류 \_ 이유.

#### <a name="using-page-inspector-with-facebook-template"></a>Facebook 템플릿과 페이지 검사기 사용

Facebook 응용 프로그램을 디버그 하는 동안에는 Visual Studio 2012의 페이지 검사기 기능을 사용할 수 없습니다. 페이지 검사기는 현재 iframe을 지원 하지 않습니다.

### <a name="single-page-application-template-issues"></a>단일 페이지 응용 프로그램 템플릿 문제

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>JQuery 1.9/녹아웃 2.2.1 업데이트를 사용 하는 경우 기본 MVC SPA 프로젝트를 실행 하면 새 todo item edit focus 포커스 이벤트가 올바르게 처리 되지 않습니다.

JQuery 1.9/녹아웃 2.2.1 업데이트를 사용 하는 경우 기본 MVC SPA 프로젝트를 실행할 때 새 todo 항목 편집은 새 todo 항목을 todo 목록에 입력 한 후 더 이상 새 할 일 항목 편집 상자에 포커스를 다시 표시 하지 않습니다.

문제를 해결 하기 위해 [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html) 다음 샘플 코드에 대 한 유사한 수정 작업을 수행 합니다.

파일 todo.model.js  
 todolist (data) 함수를 추가 하 고 다음을 추가 합니다.  
 **isSelected = ko-kr (false);**

함수 todoList 다음 블랙 아웃 텍스트를 추가 합니다.  
 **isSelected (true);**  
 newTodoTitle ( &quot; &quot; );

파일 인덱스인 경우 다음 블랙 ed 텍스트를 추가 합니다.  
 &lt;양식 데이터 바인딩 = &quot; 제출: addTodo&quot;&gt;  
 &lt;input class = &quot; addtodo &quot; type = &quot; 텍스트 &quot; 데이터-바인딩 = &quot; 값: newTodoTitle, 자리 표시자: ' Type to add ', blurOnEnter: True, **hasfocus: isSelected**, event: {흐림: addtodo}&quot; /&gt;  
 &lt;/form&gt;
