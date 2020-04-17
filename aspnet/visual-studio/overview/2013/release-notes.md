---
uid: visual-studio/overview/2013/release-notes
title: 비주얼 스튜디오 2013 릴리스 노트를 위한 ASP.NET 및 웹 도구 | 마이크로 소프트 문서
author: rick-anderson
description: 이 문서에서는 Visual Studio 2013을 위한 ASP.NET 및 웹 도구 릴리스에 대해 설명합니다.
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: 4494b4acdd30384e1def89b7fff9bad30933e38e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543498"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a>Visual Studio 2013용 ASP.NET 및 Web Tools 릴리스 정보

[로 마이크로 소프트](https://github.com/microsoft)

> 이 문서에서는 Visual Studio 2013을 위한 ASP.NET 및 웹 도구 릴리스에 대해 설명합니다.

## <a name="contents"></a>콘텐츠

- [설치 노트](#TOC1)
- [문서](#TOC2)
- [소프트웨어 요구 사항](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>비주얼 스튜디오 2013을 위한 ASP.NET 및 웹 도구의 새로운 기능

- [ASP.NET 1개](#TOC6)
- [새로운 웹 프로젝트 환경](#newproj)
- [ASP.NET 비계](#scaffold)
- [브라우저 링크](#browser-link)
- [비주얼 스튜디오 웹 에디터 개선 사항](#web-editor)
- [비주얼 스튜디오에서 Azure 앱 서비스 웹 앱 지원](#waws)
- [웹 게시 개선 사항](#publish)
- [NuGet 2.7](#nuget)
- [ASP.NET 웹 양식](#TOC9)
- [ASP.NET MVC 5](#TOC10)
- [ASP.NET Web API 2](#TOC11)
- [ASP.NET SignalR](#TOC13)
- [ASP.NET ID](#TOC8)
- [마이크로 소프트 오윈 구성 요소](#TOC7)
- [Entity Framework 6](#ef6)
- [ASP.NET 면도기 3](#TOC14)
- [ASP.NET 앱 일시 중단](#TOC15)
- [알려진 문제 및 주요 변경 사항](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a>설치 참고 사항

ASP.NET 및 Visual Studio 2013용 웹 도구는 기본 설치 관리자에 번들로 [제공됩니다.](https://www.asp.net/downloads)

<a id="TOC2"></a>
## <a name="documentation"></a>문서화

Visual Studio 2013을 위한 ASP.NET 및 웹 도구에 대한 자습서 및 기타 정보는 [ASP.NET 웹 사이트에서](https://www.asp.net/)확인할 수 있습니다.

<a id="TOC4"></a>
## <a name="software-requirements"></a>소프트웨어 요구 사항

ASP.NET 및 웹 도구에는 Visual Studio 2013이 필요합니다.

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>비주얼 스튜디오 2013을 위한 ASP.NET 및 웹 도구의 새로운 기능

다음 섹션에서는 릴리스에서 도입된 기능에 대해 설명합니다.

<a id="TOC6"></a>
## <a name="one-aspnet"></a>ASP.NET 1개

Visual Studio 2013의 출시와 함께, 우리는 당신이 쉽게 혼합하고 당신이 원하는 것들을 일치시킬 수 있도록, ASP.NET 기술을 사용하는 경험을 통합하는 쪽으로 단계를 촬영하고있다. 예를 들어 MVC를 사용하여 프로젝트를 시작하고 나중에 프로젝트에 웹 양식 페이지를 쉽게 추가하거나 웹 폼 프로젝트에서 웹 API를 스캐폴드할 수 있습니다. 한 가지 ASP.NET 개발자가 ASP.NET 좋아하는 일을 더 쉽게 할 수 있도록 하는 것입니다. 어떤 기술을 선택하든 One ASP.NET 신뢰할 수 있는 기본 프레임워크를 구축하고 있다는 확신을 가질 수 있습니다.

<a id="newproj"></a>
## <a name="new-web-project-experience"></a>새로운 웹 프로젝트 환경

Visual Studio 2013에서 새로운 웹 프로젝트를 만드는 경험을 향상시켰습니다. 새 **ASP.NET 웹 프로젝트** 대화 상자에서 원하는 프로젝트 유형을 선택하고, 기술 조합(웹 양식, MVC, 웹 API)을 구성하고, 인증 옵션을 구성하고, 단위 테스트 프로젝트를 추가할 수 있습니다.

![새 ASP.NET 프로젝트](release-notes/_static/image1.png)

새 대화 상자를 사용하면 많은 템플릿에 대한 기본 인증 옵션을 변경할 수 있습니다. 예를 들어 ASP.NET Web Forms 프로젝트를 만들 때 다음 옵션 중 을 선택할 수 있습니다.

- 인증 없음
- 개인 사용자 계정(ASP.NET 멤버십 또는 소셜 공급자 로그인)
- 조직 계정(인터넷 응용 프로그램의 활성 디렉터리)
- Windows 인증(인트라넷 응용 프로그램의 활성 디렉터리)

![인증 옵션](release-notes/_static/image2.png)

웹 프로젝트를 만드는 새로운 프로세스에 대한 자세한 내용은 [Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기를](creating-web-projects-in-visual-studio.md)참조하십시오. 새 인증 옵션에 대한 자세한 내용은 이 문서의 ASP.NET [ID를](#TOC8) 참조하십시오.

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a>ASP.NET 비계

ASP.NET 스캐폴딩은 ASP.NET 웹 응용 프로그램을 위한 코드 생성 프레임워크입니다. 데이터 모델과 상호 작용하는 상용구 코드를 프로젝트에 쉽게 추가할 수 있습니다.

이전 버전의 Visual Studio에서는 스캐폴딩이 ASP.NET MVC 프로젝트로 제한되었습니다. Visual Studio 2013을 사용하면 이제 웹 양식을 비롯한 모든 ASP.NET 프로젝트에 스캐폴딩을 사용할 수 있습니다. Visual Studio 2013은 현재 Web Forms 프로젝트에 대한 페이지 생성을 지원하지 않지만 프로젝트에 MVC 종속성을 추가하여 웹 양식과 함께 스캐폴딩을 사용할 수 있습니다. 웹 양식에 대한 페이지 생성에 대한 지원은 향후 업데이트에 추가될 예정입니다.

스캐폴딩을 사용할 때 필요한 모든 종속성이 프로젝트에 설치되었는지 확인합니다. 예를 들어 ASP.NET Web Forms 프로젝트로 시작한 다음 스캐폴딩을 사용하여 웹 API 컨트롤러를 추가하는 경우 필요한 NuGet 패키지 및 참조가 프로젝트에 자동으로 추가됩니다.

웹 양식 프로젝트에 MVC 스캐폴딩을 추가하려면 **새 스캐폴드 항목을** 추가하고 대화 상자 창에서 **MVC 5 종속성을** 선택합니다. 스캐폴딩 MVC에는 두 가지 옵션이 있습니다. 최소 및 전체. 최소를 선택하면 ASP.NET MVC에 대한 NuGet 패키지 및 참조만 프로젝트에 추가됩니다. 전체 옵션을 선택하면 MVC 프로젝트에 필요한 콘텐츠 파일뿐만 아니라 최소 종속성이 추가됩니다.

비동기 컨트롤러 스캐폴딩에 대한 지원은 엔터티 프레임워크 6의 새 비동기 기능을 사용합니다.

자세한 정보 및 자습서는 [ASP.NET 스캐폴딩 개요를](aspnet-scaffolding-overview.md)참조하십시오.

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a>브라우저 링크 - 브라우저와 비주얼 스튜디오 사이의 신호 채널

새로운 [브라우저 링크](using-browser-link.md) 기능을 사용하면 도구 모음에서 단추를 클릭하여 여러 브라우저를 Visual Studio에 연결하고 모두 새로 고칠 수 있습니다. 모바일 에뮬레이터를 포함하여 여러 브라우저를 개발 사이트에 연결하고 새로 고침을 클릭하여 모든 브라우저를 동시에 새로 고칠 수 있습니다. 또한 브라우저 링크는 개발자가 브라우저 링크 확장을 작성할 수 있도록 API를 노출합니다.

![](release-notes/_static/image3.png)

개발자가 브라우저 링크 API를 활용할 수 있도록 하면 Visual Studio와 연결된 브라우저 간의 경계를 넘나들 수 있는 매우 진보된 시나리오를 만들 수 있습니다. Web Essentials는 API를 활용하여 Visual Studio와 브라우저의 개발자 도구, 원격 제어 모바일 에뮬레이터 및 기타 여러 가지 통합 환경을 만듭니다.

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a>비주얼 스튜디오 웹 에디터 개선 사항

Visual Studio 2013에는 Razor 파일및 웹 애플리케이션의 HTML 파일에 대한 새로운 HTML 편집기가 포함되어 있습니다. 새 HTML 편집기는 HTML5를 기반으로 하는 단일 통합 스키마를 제공합니다. 그것은 자동 중괄호 완료, jQuery UI 및 AngularJS 속성 IntelliSense, 속성 IntelliSense 그룹화, ID 및 클래스 이름 Intellisense, 그리고 더 나은 성능을 포함 하 여 다른 개선, 서식 및 SmartTags.

다음 스크린샷은 HTML 편집기에서 부트스트랩 속성 IntelliSense를 사용하는 것을 보여 줍니다.

![HTML 편집기의 인텔리센스](release-notes/_static/image4.png)

비주얼 스튜디오 2013 또한 함께 제공 커피 스크립트와 LESS 편집기 내장. LESS 편집기는 CSS 편집기의 모든 멋진 기능과 함께 제공되며 체인의 모든 LESS 문서에 걸쳐 @import 변수와 혼합에 대한 특정 Intellisense가 있습니다.

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a>비주얼 스튜디오에서 Azure 앱 서비스 웹 앱 지원

.NET 2.2에 대한 Azure SDK를 사용하는 Visual Studio 2013에서는 **서버 탐색기를** 사용하여 원격 웹 앱과 직접 상호 작용할 수 있습니다. Azure 계정에 로그인하고, 새 웹 앱을 만들고, 앱을 구성하고, 실시간 로그를 볼 수 있습니다. SDK 2.2가 출시된 후 곧 Azure에서 디버그 모드에서 원격으로 실행할 수 있습니다. Azure App Service 웹 앱에 대한 대부분의 새로운 기능은 .NET에 대한 Azure SDK의 현재 릴리스를 설치할 때 Visual Studio 2012에서도 작동합니다.

자세한 내용은 다음 자료를 참조하세요.

- [Azure 앱 서비스에서 ASP.NET 웹 앱 만들기](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [Visual Studio를 사용하여 Azure App Service에서 웹앱 문제 해결](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a>웹 게시 개선 사항

Visual Studio 2013에는 새롭고 향상된 웹 게시 기능이 포함되어 있습니다. 다음은 몇 가지 옵션입니다.

- [Web.config 파일 암호화를](https://go.microsoft.com/fwlink/?LinkId=325529)쉽게 자동화할 수 있습니다. (이 링크와 다음 두 가지 는 MSDN에 대한 설명서를 10/17에 늦게까지 사용할 수 없습니다.)
- 배포 하는 동안 응용 프로그램을 오프라인으로 전환하는 것을 쉽게 [자동화할 수 있습니다.](https://go.microsoft.com/fwlink/?LinkId=325530)
- 서버에 복사할 파일을 결정하기 위해 [마지막으로 변경된 날짜 대신 파일 체크섬을 사용하도록](https://go.microsoft.com/fwlink/?LinkId=325531) 웹 배포를 구성합니다.
- FTP 또는 파일 시스템 게시 메서드와 웹 배포를 사용할 때 선택한 개별 파일(Web.config 포함)을 빠르게 게시할 수 있습니다.

ASP.NET 웹 배포에 대한 자세한 내용은 [ASP.NET 사이트를](https://go.microsoft.com/fwlink/?LinkId=322027)참조하십시오.

<a id="nuget"></a>
## <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7에는 [NuGet 2.7 릴리스 노트에서](http://docs.nuget.org/docs/release-notes/nuget-2.7)자세히 설명하는 풍부한 새로운 기능 집합이 포함되어 있습니다.

또한 이 버전의 NuGet은 패키지를 다운로드하기 위해 NuGet의 패키지 복원 기능에 대한 명시적인 동의를 제공할 필요가 없습니다. NuGet의 기본 설정 대화 상자에서 연결된 확인란에 대한 동의가 이제 NuGet을 설치하여 부여됩니다. 이제 패키지 복원은 기본적으로 작동합니다.

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a>ASP.NET 웹 양식

### <a name="one-aspnet"></a>ASP.NET 1개

Web Forms 프로젝트 템플릿은 새로운 One ASP.NET 환경과 원활하게 통합됩니다. Web Forms 프로젝트에 MVC 및 웹 API 지원을 추가할 수 있으며 One ASP.NET 프로젝트 만들기 마법사를 사용하여 인증을 구성할 수 있습니다. 자세한 내용은 [Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기를](creating-web-projects-in-visual-studio.md)참조하십시오.

### <a name="aspnet-identity"></a>ASP.NET ID

Web Forms 프로젝트 템플릿은 새 ASP.NET ID 프레임워크를 지원합니다. 또한 이제 템플릿이 웹 양식 인트라넷 프로젝트 만들기를 지원합니다. 자세한 내용은 Visual Studio **2013에서 ASP.NET 웹 프로젝트 만들기의** [인증 방법을](creating-web-projects-in-visual-studio.md#auth) 참조하십시오.

### <a name="bootstrap"></a>부트스트랩

Web Forms 템플릿은 [부트스트랩을](http://twitter.github.io/bootstrap/) 사용하여 매끄럽고 반응성이 뛰어난 모양과 느낌을 쉽게 사용자 정의할 수 있습니다. 자세한 내용은 [Visual Studio 2013 웹 프로젝트 템플릿의 부트스트랩을](creating-web-projects-in-visual-studio.md#bootstrap)참조하십시오.

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a>ASP.NET MVC 5

### <a name="one-aspnet"></a>ASP.NET 1개

Web MVC 프로젝트 템플릿은 새로운 One ASP.NET 환경과 원활하게 통합됩니다. MVC 프로젝트를 사용자 지정하고 One ASP.NET 프로젝트 만들기 마법사를 사용하여 인증을 구성할 수 있습니다. MVC 5를 ASP.NET 입문 튜토리얼은 [ASP.NET MVC 5로 시작하기에서](../../../mvc/overview/getting-started/introduction/getting-started.md)찾을 수 있습니다.

MVC 4 프로젝트를 MVC 5로 업그레이드하는 방법에 대한 자세한 내용은 [MVC 5 및 웹 API 2를 ASP.NET ASP.NET MVC 4 및 웹 API 프로젝트를 업그레이드하는 방법을](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)참조하십시오.

### <a name="aspnet-identity"></a>ASP.NET ID

MVC 프로젝트 템플릿이 ASP.NET ID를 인증 및 ID 관리에 사용하도록 업데이트되었습니다. 페이스북과 구글 인증 및 새로운 멤버십 API를 특징으로 하는 튜토리얼은 [페이스북과 구글 OAuth2, OpenID 사인온을 통해 ASP.NET MVC 5 앱 만들기에서](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 찾을 수 있으며, [인증 및 SQL DB가 있는 ASP.NET MVC 앱을 생성하고 Azure 앱 서비스에 배포할](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)수 있습니다.

### <a name="bootstrap"></a>부트스트랩

MVC 프로젝트 템플릿은 부트 [스트랩을](http://getbootstrap.com/) 사용하여 매끄럽고 반응성이 뛰어난 모양과 느낌을 쉽게 사용자 정의 할 수 있도록 업데이트되었습니다. 자세한 내용은 [Visual Studio 2013 웹 프로젝트 템플릿의 부트스트랩을](creating-web-projects-in-visual-studio.md#bootstrap)참조하십시오.

### <a name="authentication-filters"></a>인증 필터

인증 필터는 ASP.NET MVC 파이프라인에서 권한 부여 필터 이전에 실행되고 모든 컨트롤러에 대해 작업당 인증 논리, 컨트롤러별 또는 전역을 지정할 수 있는 ASP.NET MVC의 새로운 종류의 필터입니다. 인증 필터는 요청에서 자격 증명을 처리하고 해당 보안 주체를 제공합니다. 인증 필터는 승인되지 않은 요청에 대한 응답으로 인증 문제를 추가할 수도 있습니다.

### <a name="filter-overrides"></a>필터 재정의

이제 재정의 필터를 지정하여 지정된 작업 메서드 또는 컨트롤러에 적용되는 필터를 재정의할 수 있습니다. 필터 재정의는 지정된 범위(작업 또는 컨트롤러)에 대해 실행해서는 안 되는 필터 유형 집합을 지정합니다. 이렇게 하면 전역적으로 적용되는 필터를 구성한 다음 특정 전역 필터가 특정 작업 또는 컨트롤러에 적용되지 않도록 제외할 수 있습니다.

### <a name="attribute-routing"></a>특성 라우팅

ASP.NET MVC는 이제 [http://attributerouting.net](http://attributerouting.net)의 저자 팀 맥콜의 기여 덕분에 특성 라우팅을 지원합니다. 특성 라우팅을 사용하면 작업 및 컨트롤러에 추가하여 경로를 지정할 수 있습니다.

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a>ASP.NET Web API 2

### <a name="attribute-routing"></a>특성 라우팅

ASP.NET 웹 API는 이제 의 작성자인 Tim McCall의 기여 [http://attributerouting.net](http://attributerouting.net)덕분에 특성 라우팅을 지원합니다. 특성 라우팅을 사용하면 다음과 같이 작업 및 컨트롤러에 추가하여 Web API 경로를 지정할 수 있습니다.

[!code-csharp[Main](release-notes/samples/sample1.cs)]

특성 라우팅을 사용하면 웹 API의 URI를 보다 세한 제어할 수 있습니다. 예를 들어 단일 API 컨트롤러를 사용하여 리소스 계층 구조를 쉽게 정의할 수 있습니다.

[!code-csharp[Main](release-notes/samples/sample2.cs)]

특성 라우팅은 선택적 매개 변수, 기본값 및 경로 제약 조건을 지정하기 위한 편리한 구문도 제공합니다.

[!code-csharp[Main](release-notes/samples/sample3.cs)]

특성 라우팅에 대한 자세한 내용은 [웹 API 2의 특성 라우팅을](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)참조하십시오.

### <a name="oauth-20"></a>OAuth 2.0

이제 웹 API 및 단일 페이지 응용 프로그램 응용 프로그램 템플릿은 OAuth 2.0을 사용하여 권한 부여를 지원합니다. OAuth 2.0은 보호된 리소스에 대한 클라이언트 액세스 권한을 부여하기 위한 프레임워크입니다. 그것은 브라우저와 모바일 장치를 포함한 클라이언트의 다양한 작동합니다.

OAuth 2.0에 대한 지원은 권한을 부여 서버 역할을 구현하기 위해 Microsoft OWIN 구성 요소에서 제공하는 새로운 보안 미들웨어를 기반으로 합니다. 또는 Windows Server 2012 R2의 Azure Active Directory 또는 ADFS와 같은 조직 권한 부여 서버를 사용하여 클라이언트를 인증할 수 있습니다.

### <a name="odata-improvements"></a>O데이터 개선 사항

**$select, $expand, $batch 및 $value 지원**

ASP.NET 웹 API OData는 이제 $select, $expand 및 $value 대한 완전한 지원을 합니다. 변경 집합의 일괄 처리 및 처리 요청에 $batch 사용할 수도 있습니다.

$select 및 $expand 옵션을 사용하면 OData 끝점에서 반환되는 데이터의 모양을 변경할 수 있습니다. 자세한 내용은 [웹 API OData에서 $select 및 $expand 지원 소개를](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)참조하십시오.

**향상된 확장성**

이제 OData 포터가 확장가능해졌습니다. Atom 항목 메타데이터를 추가하고, 명명된 스트림 및 미디어 링크 항목을 지원하고, 인스턴스 주석을 추가하고, 링크가 생성되는 방식을 사용자 지정할 수 있습니다.

**유형 없는 지원**

이제 엔터티 형식에 대한 CLR 형식을 정의할 필요 없이 OData 서비스를 빌드할 수 있습니다. 대신 OData 컨트롤러는 직렬화/역직렬화에 대한 OData formatters인 **IEdmObject의**인스턴스를 사용하거나 반환할 수 있습니다.

**기존 모델 재사용**

이미 EDM(기존 엔터티 데이터 모델)이 있는 경우 새 엔터티 데이터 모델을 빌드하는 대신 직접 다시 사용할 수 있습니다. 예를 들어 엔터티 프레임워크를 사용하는 경우 EF가 빌드하는 EDM을 사용할 수 있습니다.

### <a name="request-batching"></a>일괄 처리 요청

요청 일괄 처리는 여러 작업을 단일 HTTP POST 요청으로 결합하여 네트워크 트래픽을 줄이고 보다 원활하고 덜 수다스러운 사용자 인터페이스를 제공합니다. ASP.NET 웹 API는 이제 요청 일괄 처리에 대한 몇 가지 전략을 지원합니다.

- OData 서비스의 $batch 끝점을 사용합니다.
- 여러 요청을 단일 MIME 다중 파트 요청으로 패키징합니다.
- 사용자 지정 일괄 처리 형식을 사용합니다.

요청 일괄 처리를 사용하려면 일괄 처리기가 있는 경로를 웹 API 구성에 추가하기만 하면 됩니다.

[!code-csharp[Main](release-notes/samples/sample4.cs)]

요청 또는 순차적 또는 임의의 순서로 실행할지 여부를 제어할 수도 있습니다.

### <a name="portable-aspnet-web-api-client"></a>휴대용 ASP.NET 웹 API 클라이언트

이제 ASP.NET 웹 API 클라이언트를 사용하여 Windows 스토어 및 Windows Phone 8 응용 프로그램에서 작동하는 이식 가능한 클래스 라이브러리를 만들 수 있습니다. 클라이언트와 서버 간에 공유할 수 있는 이식 가능한 포matters를 만들 수도 있습니다.

### <a name="improved-testability"></a>향상된 테스트 용이성

웹 API 2를 사용하면 API 컨트롤러를 훨씬 쉽게 단위 테스트할 수 있습니다. 요청 메시지 및 구성으로 API 컨트롤러를 인스턴스화한 다음 테스트하려는 작업 메서드를 호출하기만 하면 됩니다. 링크 생성을 수행하는 작업 메서드에 대해 **UrlHelper** 클래스를 조롱하는 것도 쉽습니다.

### <a name="ihttpactionresult"></a>IHttpAction결과

이제 IHttpActionResult를 구현하여 웹 API 작업 메서드의 결과를 캡슐화할 수 있습니다. 웹 API 작업 메서드에서 반환된 IHttpActionResult는 ASP.NET 웹 API 런타임에 의해 실행되어 결과 응답 메시지를 생성합니다. IHttpActionResult 웹 API 구현의 단위 테스트를 단순화 하기 위해 모든 웹 API 작업에서 반환 될 수 있습니다. 편의를 위해 특정 상태 코드, 서식이 지정된 콘텐츠 또는 콘텐츠 협상 응답을 반환하는 결과를 포함하여 여러 IHttpActionResult 구현이 즉시 제공됩니다.

### <a name="httprequestcontext"></a>HttpRequest컨텍스트

새 **HttpRequestContext는** 요청에 연결되지만 요청에서 즉시 사용할 수 없는 모든 상태를 추적합니다. 예를 들어 **HttpRequestContext를** 사용하여 경로 데이터, 요청과 연결된 주 서버, 클라이언트 인증서, **UrlHelper** 및 가상 경로 루트를 얻을 수 있습니다. 단위 테스트를 위해 **HttpRequestContext를** 쉽게 만들 수 있습니다.

요청에 대한 주 서버는 **Thread.CurrentPrincipal에**의존하는 대신 요청과 함께 흐르므로 웹 API 파이프라인에 있는 동안 요청의 수명 동안 보안 주체를 사용할 수 있습니다.

### <a name="cors"></a>CORS

브록 앨런의 또 다른 큰 기여 덕분에, ASP.NET 이제 완전히 크로스 오리진 요청 공유 (CORS)를 지원합니다.

브라우저 보안은 웹 페이지에서 다른 도메인으로 AJAX 요청을 수행하지 못하도록 방지합니다. [CORS는](http://www.w3.org/TR/cors/) 서버가 동일한 원본 정책을 완화할 수 있는 W3C 표준입니다. CORS를 사용하면 서버에서 명시적으로 일부 원본 간 요청을 허용하는 한편 다른 요청은 거부할 수 있습니다.

이제 웹 API 2는 사전 비행 요청의 자동 처리를 포함하여 CORS를 지원합니다. 자세한 내용은 [ASP.NET 웹 API에서 크로스-원본 리소스 요청 사용](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)을 참조하세요.

### <a name="authentication-filters"></a>인증 필터

인증 필터는 ASP.NET 웹 API 파이프라인의 권한 부여 필터 이전에 실행되고 모든 컨트롤러에 대해 작업당 인증 논리, 컨트롤러별 또는 전역을 지정할 수 있는 ASP.NET 웹 API의 새로운 종류의 필터입니다. 인증 필터는 요청에서 자격 증명을 처리하고 해당 보안 주체를 제공합니다. 인증 필터는 승인되지 않은 요청에 대한 응답으로 인증 문제를 추가할 수도 있습니다.

### <a name="filter-overrides"></a>필터 재정의

이제 재정의 필터를 지정하여 지정된 작업 메서드 또는 컨트롤러에 적용되는 필터를 재정의할 수 있습니다. 필터 재정의는 지정된 범위(작업 또는 컨트롤러)에 대해 실행되지 않아야 하는 필터 유형 집합을 지정합니다. 이렇게 하면 전역 필터를 추가한 다음 특정 작업 또는 컨트롤러에서 일부를 제외할 수 있습니다.

### <a name="owin-integration"></a>오윈 통합

ASP.NET 웹 API는 이제 OWIN을 완벽하게 지원하며 OWIN 가능한 호스트에서 실행할 수 있습니다. OWIN 인증 시스템과의 통합을 제공하는 **호스트 인증 필터도** 포함되어 있습니다.

OWIN 통합을 사용하면 SignalR과 같은 다른 OWIN 미들웨어와 함께 자체 프로세스에서 웹 API를 자체 호스팅할 수 있습니다. 자세한 내용은 [OWIN에서 셀프 호스트ASP.NET 웹 API를 참조하십시오.](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a>ASP.NET 시그널R 2.0

다음 섹션에서는 SignalR 2.0의 기능에 대해 설명합니다.

- [오윈에 내장](#builtonowin)
- [맵허브와 맵연결이 이제 맵시널R로 바됩니다.](#MapSignalR)
- [도메인 간 지원](#crossdomain)
- [모노 터치와 모노 드로이드를 통해 아이폰 OS와 안드로이드 지원](#mobile)
- [휴대용 .NET 클라이언트](#portable)
- [새로운 셀프 호스트 패키지](#selfhost)
- [이전 버전과 호환되는 서버 지원](#backwardcompat)
- [.NET 4.0에 대한 서버 지원 제거](#remove40)
- [클라이언트 및 그룹 목록에 메시지 보내기](#messagelist)
- [특정 사용자에게 메시지 보내기](#sendtouser)
- [더 나은 오류 처리 지원](#errorhandling)
- [허브의 간편한 단위 테스트](#unittesting)
- [자바 스크립트 오류 처리](#javascripterror)

기존 1.x 프로젝트를 SignalR 2.0으로 업그레이드하는 방법의 예는 [SignalR 1.x 프로젝트 업그레이드를](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)참조하십시오.

<a id="builtonowin"></a>
### <a name="built-on-owin"></a>오윈에 내장

SignalR 2.0은 [OWIN(.NET용 개방형 웹 인터페이스)에](http://owin.org/)완전히 구축되었습니다. 이러한 변경으로 인해 SignalR에 대한 설정 프로세스가 웹 호스팅 및 자체 호스팅 SignalR 응용 프로그램 간에 훨씬 더 일관되게 유지되지만 여러 API 변경이 필요했습니다.

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a>맵허브와 맵연결이 이제 맵시널R로 바됩니다.

OWIN 표준과의 호환성을 위해 이러한 메서드의 이름이 로 `MapSignalR`변경되었습니다. `MapSignalR`매개 변수없이 호출 (버전 1.x에서와 같이) `MapHubs` 모든 허브를 매핑합니다; 개별 **PersistentConnection** 개체를 매핑하려면 연결 형식을 형식 매개 변수로 지정하고 연결에 대한 URL 확장을 첫 번째 인수로 지정합니다.

메서드는 `MapSignalR` Owin 시작 클래스에서 호출 됩니다. Visual Studio 2013에는 Owin 시작 클래스에 대한 새 템플릿이 포함되어 있습니다. 이 템플릿을 사용하려면 다음을 수행합니다.

1. 프로젝트를 마우스 오른쪽 버튼으로 클릭
2. 추가 , **새 항목 선택...** **Add**
3. **오윈 시작 클래스를**선택합니다. 새 클래스의 이름을 **Startup.cs.**

웹 **응용 프로그램에서** 메서드를 `MapSignalR` 포함하는 Owin 시작 클래스는 아래와 같이 Web.Config 파일의 응용 프로그램 설정 노드에 있는 항목을 사용하여 Owin의 시작 프로세스에 추가됩니다.

자체 **호스팅 응용 프로그램에서**시작 클래스는 `WebApp.Start` 메서드의 형식 매개 변수로 전달됩니다.

**SignalR 1.x의 허브 및 연결 매핑(웹 응용 프로그램의 전역 응용 프로그램 파일에서):** 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

**SignalR 2.0의 허브 및 연결 매핑(Owin Startup 클래스 파일에서):** 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

자체 **호스팅 응용 프로그램에서**Startup 클래스는 아래와 같이 `WebApp.Start` 메서드의 형식 매개 변수로 전달됩니다.

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a>도메인 간 지원

SignalR 1.x에서 교차 도메인 요청은 단일 EnableCrossDomain 플래그에 의해 제어되었습니다. 이 플래그는 JSONP 및 CORS 요청을 모두 제어했습니다. 유연성을 높이기 위해 모든 CORS 지원이 SignalR의 서버 구성 요소에서 제거되었습니다(JavaScript 클라이언트는 브라우저가 지원하는 것으로 감지되는 경우 CORS를 정상적으로 사용함) 이러한 시나리오를 지원하기 위해 새로운 OWIN 미들웨어를 사용할 수 있게 되었습니다.

SignalR 2.0에서 JSONP가 클라이언트에 필요한 경우(이전 브라우저에서 도메인 간 요청을 지원하려면) 아래와 `EnableJSONP` 같이 `HubConfiguration` 개체를 `true`설정하여 명시적으로 활성화해야 합니다. JSONP는 CORS보다 안전하지 때문에 기본적으로 비활성화됩니다.

SignalR 2.0에 새 CORS 미들웨어를 `Microsoft.Owin.Cors` 추가하려면 아래 섹션과 `UseCors` 같이 프로젝트에 라이브러리를 추가하고 SignalR 미들웨어 전에 호출합니다.

**프로젝트에 Microsoft.Owin.Cors 추가**: 이 라이브러리를 설치하려면 패키지 관리자 콘솔에서 다음 명령을 실행합니다.

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

이 명령은 2.0.0 버전의 패키지를 프로젝트에 추가합니다.

**유즈코르 스**

다음 코드 조각은 SignalR 1.x 및 2.0에서 도메인 간 연결을 구현하는 방법을 보여 줍니다.

**SignalR 1.x에서 도메인 간 요청 구현(글로벌 응용 프로그램 파일에서)**

[!code-csharp[Main](release-notes/samples/sample9.cs)]

**SignalR 2.0에서 도메인 간 요청 구현(C# 코드 파일)에서**

다음 코드는 SignalR 2.0 프로젝트에서 CORS 또는 JSONP를 사용하도록 설정하는 방법을 보여 줍니다. 이 코드 `Map` 샘플은 `RunSignalR` `MapSignalR`CORS 미들웨어가 CORS 지원이 필요한 SignalR 요청에 대해서만 실행되도록 을 대신 사용하며 `MapSignalR`.에 지정된 경로의 모든 트래픽에 대해 실행됩니다. `Map` 또한 전체 응용 프로그램이 아닌 특정 URL 접두사에 대해 실행해야 하는 다른 미들웨어에도 사용할 수 있습니다.

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a>모노 터치와 모노 드로이드를 통해 아이폰 OS와 안드로이드 지원

[자마린 라이브러리에서](https://xamarin.com/)모노터치 및 MonoDroid 구성 요소를 사용하여 iOS 및 Android 클라이언트에 대한 지원이 추가되었습니다. 사용 방법에 대한 자세한 내용은 [Xamarin 구성 요소 사용을](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)참조하십시오. 이러한 구성 요소는 SignalR RTW 릴리스를 사용할 수 있을 때 [Xamarin 스토어에서](https://store.xamarin.com/) 사용할 수 있습니다.

<a id="portable"></a>### 휴대용 .NET 클라이언트

플랫폼 간 개발을 보다 용이하게 하기 위해 Silverlight, WinRT 및 Windows Phone 클라이언트는 다음 플랫폼을 지원하는 단일 휴대용 .NET 클라이언트로 대체되었습니다.

- 순 4.5
- Silverlight 5
- WinRT (윈도우 스토어 앱용.NET)
- Windows Phone 8

<a id="selfhost"></a>

### <a name="new-self-host-package"></a>새로운 셀프 호스트 패키지

이제 SignalR 셀프 호스트(웹 서버에서 호스팅되는 대신 프로세스 또는 다른 응용 프로그램에서 호스팅되는 SignalR 응용 프로그램)를 더 쉽게 시작할 수 있도록 NuGet 패키지가 있습니다. SignalR 1.x로 빌드된 자체 호스트 프로젝트를 업그레이드하려면 Microsoft.AspNet.SignalR.Owin 패키지를 제거하고 Microsoft.AspNet.SignalR.SelfHost 패키지를 추가합니다. 셀프 호스트 패키지 시작에 대한 자세한 내용은 [자습서: SignalR 셀프 호스트](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)를 참조하십시오.

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a>이전 버전과 호환되는 서버 지원

이전 버전의 SignalR에서는 클라이언트와 서버에서 사용되는 SignalR 패키지 버전이 동일해야 했습니다. 업데이트하기 어려운 두꺼운 클라이언트 응용 프로그램을 지원하기 위해 SignalR 2.0은 이제 이전 클라이언트와 함께 최신 서버 버전을 사용할 수 있도록 지원합니다. **참고: SignalR 2.0은 최신 클라이언트로 이전 버전으로 빌드된 서버를 지원하지 않습니다.**

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a>.NET 4.0에 대한 서버 지원 제거

SignalR 2.0은 .NET 4.0을 통해 서버 상호 운용성에 대한 지원을 중단했습니다. .NET 4.5는 SignalR 2.0 서버에서 사용해야 합니다. SignalR 2.0에 대한 .NET 4.0 클라이언트는 여전히 존재합니다.

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a>클라이언트 및 그룹 목록에 메시지 보내기

SignalR 2.0에서는 클라이언트 및 그룹 아이디 목록을 사용하여 메시지를 보낼 수 있습니다. 다음 코드 조각에서는 이 작업을 수행하는 방법을 보여 줍니다.

**영구 연결을 사용하여 클라이언트 및 그룹 목록에 메시지 보내기**

[!code-csharp[Main](release-notes/samples/sample11.cs)]

**Hubs를 사용하여 클라이언트 및 그룹 목록에 메시지 보내기**

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a>특정 사용자에게 메시지 보내기

이 기능을 사용하면 사용자가 새 인터페이스 IUserIdProvider를 통해 IRequest를 기반으로 하는 userId를 지정할 수 있습니다.

**IUserIdProvider 인터페이스**

[!code-csharp[Main](release-notes/samples/sample13.cs)]

기본적으로 사용자의 IPrincipal.Identity.Name 사용자 이름으로 사용하는 구현이 있습니다.

허브에서는 새 API를 통해 이러한 사용자에게 메시지를 보낼 수 있습니다.

**클라이언트 사용.사용자 API**

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a>더 나은 오류 처리 지원

이제 사용자는 모든 허브 호출에서 **HubException을** throw할 수 있습니다. **HubException의** 생성자는 문자열 메시지와 개체 추가 오류 데이터를 취할 수 있습니다. SignalR은 예외를 자동으로 직렬화하고 허브 메서드 호출을 거부/실패하는 데 사용되는 클라이언트로 보냅니다.

**쇼 자세한 허브 예외** 설정은 **HubException클라이언트로** 다시 전송되거나 하지 않는 것에 아무런 영향을 미치지 않습니다. 항상 전송됩니다.

**클라이언트에 HubException을 보내는 것을 보여 주는 서버 측 코드**

[!code-csharp[Main](release-notes/samples/sample15.cs)]

**서버에서 보낸 HubException에 응답하는 JavaScript 클라이언트 코드**

[!code-html[Main](release-notes/samples/sample16.html)]

**서버에서 보낸 HubException에 응답하는 것을 보여 주는 .NET 클라이언트 코드**

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a>허브의 간편한 단위 테스트

SignalR 2.0에는 모의 클라이언트 측 호출을 쉽게 만들 수 있는 Hubs에 호출된 `IHubCallerConnectionContext` 인터페이스가 포함되어 있습니다. 다음 코드 조각은 xUnit.net [moq에서](https://code.google.com/p/moq/)인기 [xUnit.net](https://github.com/xunit/xunit) 있는 테스트 하네스와 함께 이 인터페이스를 사용하는 것을 보여 줍니다.

**xUnit.net 가진 단위 테스트 신호**

[!code-csharp[Main](release-notes/samples/sample18.cs)]

**단위 테스트 시그널R 와 moq**

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a>자바 스크립트 오류 처리

SignalR 2.0에서 모든 JavaScript 오류 처리 콜백은 원시 문자열 대신 JavaScript 오류 개체를 반환합니다. 이를 통해 SignalR은 오류 처리기로 풍부한 정보를 플로우할 수 있습니다. 오류의 속성에서 내부 `source` 예외를 얻을 수 있습니다.

**시작.Fail 예외를 처리하는 자바스크립트 클라이언트 코드**

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a>ASP.NET ID

### <a name="new-aspnet-membership-system"></a>새로운 ASP.NET 멤버십 시스템

ASP.NET ID는 ASP.NET 응용 프로그램에 대한 새로운 회원 자격 시스템입니다. ASP.NET ID를 사용하면 사용자별 프로필 데이터를 응용 프로그램 데이터와 쉽게 통합할 수 있습니다. ASP.NET ID를 사용하면 응용 프로그램에서 사용자 프로필에 대한 지속성 모델을 선택할 수도 있습니다. NoSQL 데이터 저장소(예: Azure Storage 테이블)를 비롯하여 SQL Server 데이터베이스나 다른 데이터 저장소에 데이터를 저장할 수 있습니다. 자세한 내용은 **Visual Studio 2013에서 웹 프로젝트 만들기의** [개별 사용자 계정을](creating-web-projects-in-visual-studio.md#indauth) ASP.NET.

### <a name="claims-based-authentication"></a>클레임 기반 인증

ASP.NET 이제 사용자의 ID가 신뢰할 수 있는 발급자의 클레임 집합으로 표시되는 클레임 기반 인증을 지원합니다. 사용자는 응용 프로그램 데이터베이스에 유지 관리되는 사용자 이름과 암호를 사용하거나 소셜 ID 공급자(예: Microsoft 계정, Facebook, Google, Twitter)를 사용하거나 Azure Active Directory 또는 ADFS(Active Directory Federation Services)를 통해 조직 계정을 사용하여 인증할 수 있습니다.

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a>Azure Active 디렉터리 및 Windows 서버 활성 디렉터리와의 통합

이제 인증을 위해 Azure Active Directory 또는 Windows 서버 활성 디렉터리(AD)를 사용하는 ASP.NET 프로젝트를 만들 수 있습니다. 자세한 내용은 **Visual Studio 2013에서 웹 프로젝트 만들기에서 ASP.NET**구성 [계정을](creating-web-projects-in-visual-studio.md#orgauth) 참조하세요.

### <a name="owin-integration"></a>오윈 통합

ASP.NET 인증은 이제 모든 OWIN 기반 호스트에서 사용할 수 있는 OWIN 미들웨어를 기반으로 합니다. OWIN에 대한 자세한 내용은 다음 [Microsoft OWIN 구성 요소](#TOC7) 섹션을 참조하십시오.

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a>Microsoft OWIN 구성 요소

[.NET(OWIN)에 대한 개방형 웹 인터페이스는](http://owin.org/) .NET 웹 서버와 웹 응용 프로그램 간의 추상화를 정의합니다. OWIN은 서버에서 웹 응용 프로그램을 분리하여 웹 응용 프로그램을 호스트에 구애받지 않습니다. 예를 들어 IIS에서 OWIN 기반 웹 응용 프로그램을 호스팅하거나 사용자 지정 프로세스에서 자체 호스트할 수 있습니다.

Microsoft OWIN 구성 요소(카타나 프로젝트라고도 함)에 도입된 변경 사항에는 새 서버 및 호스트 구성 요소, 새 도우미 라이브러리 및 미들웨어 및 새 인증 미들웨어가 포함됩니다.

OWIN과 카타나에 대한 자세한 내용은 [OWIN과 카타나에서 새로운 정보를](../../../aspnet/overview/owin-and-katana/index.md)참조하십시오.

**참고: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) 응용 프로그램은 IIS 클래식 모드에서 실행할 수 없습니다. 통합 모드에서 실행되어야 합니다.**

**참고: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) 응용 프로그램은 완전 신뢰로 실행되어야 합니다.**

### <a name="new-servers-and-hosts"></a>새 서버 및 호스트

이 릴리스에서는 자체 호스트 시나리오를 사용하도록 새 구성 요소가 추가되었습니다. 이러한 구성 요소에는 다음 NuGet 패키지가 포함됩니다.

- **마이크로소프트.Owin.Host.HttpListener**. **HttpListener를** 사용하여 HTTP 요청을 수신하고 OWIN 파이프라인으로 안내하는 OWIN 서버를 제공합니다.
- **Microsoft.Owin.Hosting** 콘솔 응용 프로그램 또는 Windows 서비스와 같은 사용자 지정 프로세스에서 OWIN 파이프라인을 자체 호스트하려는 개발자를 위한 라이브러리를 제공합니다.
- **오윈호스트**. 사용자 지정 호스트 응용 프로그램을 작성하지 `Microsoft.Owin.Hosting` 않고도 OWIN 파이프라인을 랩핑하고 자체 호스트할 수 있는 독립 실행 형 실행 프로그램을 제공합니다.

또한 `Microsoft.Owin.Host.SystemWeb` 이제 패키지를 사용하면 미들웨어가 **SystemWeb** 서버에 힌트를 제공할 수 있으므로 특정 ASP.NET 파이프라인 단계에서 미들웨어를 호출해야 합니다. 이 기능은 ASP.NET 파이프라인의 초기에 실행되어야 하는 인증 미들웨어에 특히 유용합니다.

### <a name="helper-libraries-and-middleware"></a>도우미 라이브러리 및 미들웨어

OWIN 사양의 함수 및 형식 정의만 사용하여 OWIN 구성 요소를 `Microsoft.Owin` 작성할 수 있지만 새 패키지는 보다 사용자 친화적인 추상화 집합을 제공합니다. 이 패키지는 여러 이전 패키지(예: `Owin.Extensions`, `Owin.Types`)를 다른 OWIN 구성 요소에서 쉽게 사용할 수 있는 잘 구성된 단일 개체 모델로 결합합니다. 실제로 대부분의 Microsoft OWIN 구성 요소는 이제 이 패키지를 사용합니다.

> [!NOTE]
> [OWIN](http://www.owin.org) 응용 프로그램은 IIS 클래식 모드에서 실행할 수 없습니다. 통합 모드에서 실행되어야 합니다.

> [!NOTE]
> [OWIN](http://www.owin.org) 응용 프로그램은 완전 신뢰로 실행되어야 합니다.

이 릴리스에는 실행 중인 OWIN 응용 프로그램의 유효성을 검사하는 미들웨어와 오류를 조사하는 데 도움이 되는 오류 페이지 미들웨어가 포함된 Microsoft.Owin.Diagnostics 패키지도 포함되어 있습니다.

### <a name="authentication-components"></a>인증 구성 요소

다음 인증 구성 요소를 사용할 수 있습니다.

- **마이크로소프트.오윈.시큐리티.액티브 디렉토리**. 온-프레미스 또는 클라우드 기반 디렉터리 서비스를 사용하여 인증을 활성화합니다.
- **Microsoft.Owin.Security.쿠키** 쿠키를 사용하여 인증을 활성화합니다. 이 패키지는 `Microsoft.Owin.Security.Forms`이전에 이름이 지정되었습니다.
- **Microsoft.Owin.Security.Facebook은** 페이스북의 OAuth 기반 서비스를 사용하여 인증을 지원합니다.
- **Microsoft.Owin.Security.Google은** 구글의 OpenID 기반 서비스를 사용하여 인증을 활성화합니다.
- **Microsoft.Owin.Security.Jwt** JWT 토큰을 사용하여 인증을 활성화합니다.
- **Microsoft.Owin.Security.Microsoft계정에서** 마이크로소프트 계정을 사용하여 인증을 활성화합니다.
- **마이크로소프트.오윈.시큐리티.OAuth**. 보유자 토큰을 인증하기 위한 미들웨어뿐만 아니라 OAuth 권한 부여 서버를 제공합니다.
- **Microsoft.Owin.Security.Twitter** 트위터의 OAuth 기반 서비스를 사용하여 인증을 활성화합니다.

이 릴리스에는 `Microsoft.Owin.Cors` 원본 간 HTTP 요청을 처리하기 위한 미들웨어가 포함된 패키지도 포함되어 있습니다.

> [!NOTE]
> JWT 서명에 대한 지원은 Visual Studio 2013의 최종 버전에서 제거되었습니다.

<a id="ef6"></a>
## <a name="entity-framework-6"></a>Entity Framework 6

엔터티 프레임워크 6의 새 기능 및 기타 변경 사항 목록은 [엔터티 프레임워크 버전 기록을](https://msdn.com/data/jj574253)참조하십시오.

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a>ASP.NET 면도기 3

ASP.NET Razor 3에는 다음과 같은 새로운 기능이 포함되어 있습니다.

- 탭 편집 지원. 이전에는 **탭 유지** 옵션을 사용할 때 Visual Studio의 **형식 문서** 명령, 자동 들여쓰기 및 자동 서식이 제대로 작동하지 않았습니다. 이 변경 사항은 탭 서식지정을 위해 Razor 코드에 대한 Visual Studio 서식을 수정합니다.
- 링크를 생성할 때 URL 다시 쓰기 규칙에 대한 지원입니다.
- 보안 투명 특성 제거.
  > [!NOTE]
  > 이것은 주요 변경, 그리고 면도기 3 MVC4 이전 호환 되지 않습니다., 면도기 2 MVC5 또는 MVC5에 대 한 컴파일 된 어셈블리와 호환 되지 않습니다.

시험판 버전에서 Visual Studio 2013에서 수정된 Razor 3 문제는 [여기에서](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)찾을 수 있습니다.

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a>ASP.NET 앱 일시 중단

ASP.NET App Suspend는 .NET Framework 4.5.1의 판도를 바꾸는 기능으로, 단일 컴퓨터에서 많은 수의 ASP.NET 사이트를 호스팅하기 위한 사용자 경험과 경제 모델을 근본적으로 변경합니다. 자세한 내용은 앱 일시 중단 ASP.NET 참조 [- 응답 공유 .NET 웹 호스팅.](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a>알려진 문제 및 주요 변경 사항

이 섹션에서는 Visual Studio 2013을 위한 ASP.NET 및 웹 도구의 알려진 문제 및 주요 변경 사항에 대해 설명합니다.

### <a name="nuget"></a>NuGet

- [SLN 파일을 사용할 때 새 패키지 복원](https://nuget.codeplex.com/workitem/3596) 은 모노에서 작동하지 않습니다 - 곧 nuget.exe 다운로드 및 [NuGet.CommandLine 패키지](http://www.nuget.org/packages/NuGet.CommandLine/) 업데이트에 고정됩니다.
- [새로운 패키지 복원 Wix 프로젝트와 함께 작동 하지 않습니다-곧](https://nuget.codeplex.com/workitem/3598) nuget.exe 다운로드 및 [NuGet.CommandLine 패키지](http://www.nuget.org/packages/NuGet.CommandLine/) 업데이트에 수정 됩니다.
- [자동 패키지 복원 솔루션 폴더 아래 프로젝트에 대 한 작동 하지](https://nuget.codeplex.com/workitem/3625) 않습니다-NuGet2.8에서 수정 됩니다.

### <a name="aspnet-web-api"></a>ASP.NET Web API

1. `ODataQueryOptions<T>.ApplyTo(IQueryable)`에 대한 `IQueryable<T>` `$select` 지원을 추가했기 때문에 항상 `$expand`반환되지는 않습니다.

    항상 에 반환 `ODataQueryOptions<T>` 값을 `ApplyTo` 캐스팅에 대한 `IQueryable<T>`이전 샘플 . `$filter`앞에서 지원한 `$orderby` `$skip` `$top`쿼리 옵션은 쿼리의 모양을 변경하지 않기 때문에 이전에 작동했습니다. 이제 우리는 `$select` 지원하고 `$expand` 반환 값에서 `ApplyTo` 항상되지 않습니다. `IQueryable<T>`

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    이전의 샘플 코드를 사용하는 경우 클라이언트가 보내고 `$select` `$expand`를 보내지 않으면 계속 작동합니다. 그러나 지원하려는 `$select` `$expand` 경우 해당 코드를 이 것으로 변경해야 합니다.

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. **Request.Url 또는 RequestContext.Url일괄 처리 요청 중에 null입니다.**

    일괄 처리 시나리오에서 **UrlHelper는** **Request.Url** 또는 **RequestContext.Url**에서 액세스할 때 null입니다.

    이 문제는 현재 여기에서 추적됩니다: [BatchRequestContext.Url 일괄 처리 요청에 대 한 null입니다.](http://aspnetwebstack.codeplex.com/workitem/1301)

    이 문제의 해결 방법은 다음 예제와 같이 **UrlHelper의**새 인스턴스를 만드는 것입니다.

    **UrlHelper의 새 인스턴스 만들기**

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a>ASP.NET MVC

1. MVC5 및 OrgAuth를 사용하는 경우 AntiForgerToken 유효성 검사를 수행하는 뷰가 있는 경우 뷰에 데이터를 게시할 때 다음과 같은 오류가 발생할 수 있습니다.

    **오류**:

    *'/' 애플리케이션의 서버 오류.*

    <em>제공된 클레임ID에<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>'또는'<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>유형의 클레임이 존재하지 않았습니다. 클레임 기반 인증을 사용하여 위조 방지 토큰 지원을 활성화하려면 구성된 클레임 공급자가 생성한 ClaimsIdentity 인스턴스에서 이러한 클레임을 모두 제공하고 있는지 확인하십시오. 구성된 클레임 공급자가 대신 다른 클레임 형식을 고유 식별자로 사용하는 경우 정적 속성 AntiForgeryConfig.UniqueClaimTypeIdentifier를 설정하여 구성할 수 있습니다.</em>

    **해결 방법**:

    Global.asax에서 다음 줄을 추가하여 수정합니다.

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    이 문제는 다음 릴리스에 대해 수정됩니다.
2. MVC4 앱을 MVC5로 업그레이드한 후 솔루션을 빌드하고 실행합니다. 다음과 같은 오류가 표시됩니다.

    [A] System.Web.WebPages.Razor.Configuration.HostSection은 [B]System.Web.WebPages.Razor.Configuration.HostSection에 캐스팅할 수 없습니다. 유형 A는 'System.Web.WebPages.Razor, 버전=2.0.0.0, 문화권=중립, PublicKeyToken=31bf3856ad364e35'\_위치 'C:\windows\Microsoft.Net\어셈블리\GAC MSIL\System.WebPages.Razor\v4.0\_2.0.0.0.0.0.0.0.0\_\_31bf3855ad364e35\System.WebPages.WebPages.Razor에서 '기본값'. 유형 B는 'System.Web.WebPages.Razor, 버전=3.0.0.0, 문화권=중립, PublicKeyToken=31bf3856ad364e35' 위치 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\임시 ASP.NET 파일\root\6에서 '기본값' d05bbd0\e8b5908e\어셈블리\dl3\c9cbca63\f8910382\_6273ce01\System.WebPages.Razor.dll..

    위의 오류를 해결하려면 프로젝트의 *모든* Web.config 파일(보기 폴더에 있는 파일 포함)을 열고 다음을 수행합니다.

   1. "System.Web.Mvc"의 버전 "4.0.0.0"의 모든 발생을 "5.0.0.0"으로 업데이트합니다.
   2. "System.Web.helpers", &quot;System.Web.WebPages 및&quot; &quot;System.Web.WebPages.Razor의&quot; 모든 버전 "2.0.0.0"을 "3.0.0.0"으로 업데이트합니다.

      예를 들어 위의 내용을 변경한 후 어셈블리 바인딩은 다음과 같아야 합니다.

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      MVC 4 프로젝트를 MVC 5로 업그레이드하는 방법에 대한 자세한 내용은 [MVC 5 및 웹 API 2를 ASP.NET ASP.NET MVC 4 및 웹 API 프로젝트를 업그레이드하는 방법을](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)참조하십시오.
3. jQuery 눈에 거슬리지 없는 유효성 검사와 클라이언트 측 유효성 검사를 사용 하는 경우 유효성 검사 메시지가 경우에 올바르지 않은 HTML 입력 요소에 대 한 type='number'. 필요한 값에 대한 유효성 검사 오류("연령 필드가 필요")는 유효한 번호가 필요하다는 올바른 메시지 대신 잘못된 번호를 입력할 때 표시됩니다.

    이 문제는 일반적으로 뷰 만들기 및 편집뷰에 정수 속성이 있는 모델에 대한 스캐폴드코드에서 찾을 수 있습니다.

    이 문제를 해결하려면 편집기 도우미를 다음에서 변경합니다.

    `@Html.EditorFor(person => person.Age)`

    아래와 같이 변경합니다.

    `@Html.TextBoxFor(person => person.Age)`
4. ASP.NET MVC 5는 더 이상 부분 신뢰를 지원하지 않습니다. MVC 또는 WebAPI 바이너리에 연결하는 프로젝트는 [보안투명](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) 특성과 [허용부분적으로 신뢰할 수 있는 호출자 특성을](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) 제거해야 합니다. 이러한 특성을 제거하면 다음과 같은 컴파일러 오류가 제거됩니다.

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > 이 것의 부작용으로 동일한 응용 프로그램에서 4.0 및 5.0 어셈블리를 사용할 수 없습니다. 모든 것을 5.0으로 업데이트해야 합니다.

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a>웹 사이트가 인트라넷 영역에서 호스팅되는 동안 Facebook 권한 부여가 있는 SPA 템플릿은 IE에서 불안정을 일으킬 수 있습니다.

SPA 템플릿은 Facebook에서 외부 로그인을 제공합니다. 템플릿으로 만든 프로젝트가 로컬로 실행중일 때 로그인하면 IE가 충돌할 수 있습니다.

해결 방법:

1. 인터넷 영역에서 웹 사이트를 호스팅합니다. 또는

2. IE 가 아닌 다른 브라우저에서 시나리오를 테스트합니다.

### <a name="web-forms-scaffolding"></a>Web Forms 스캐폴딩

웹 양식 스캐폴딩은 VS2013에서 제거되었으며 향후 Visual Studio 업데이트에서 사용할 수 있습니다. 그러나 MVC 종속성을 추가하고 MVC에 대한 스캐폴딩을 생성하여 웹 폼 프로젝트 내에서 스캐폴딩을 계속 사용할 수 있습니다. 프로젝트에는 웹 양식과 MVC의 조합이 포함됩니다.

웹 양식 프로젝트에 MVC를 추가하려면 새 스캐폴드된 항목을 추가하고 **MVC 5 종속성을**선택합니다. 스크립트와 같은 모든 콘텐츠 파일이 필요한지 여부에 따라 최소 또는 전체 중 하나를 선택합니다. 그런 다음 프로젝트에서 뷰와 컨트롤러를 만드는 MVC용 스캐폴드 항목을 추가합니다.

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC 및 웹 API 스캐폴딩 - HTTP 404, 찾을 수 없는 오류

프로젝트에 스캐폴드된 항목을 추가할 때 오류가 발생하면 프로젝트가 일관되지 않은 상태로 남아 있을 수 있습니다. 스캐폴딩으로 변경된 변경 사항 중 일부는 롤백되지만 설치된 NuGet 패키지와 같은 다른 변경 내용은 롤백되지 않습니다. 라우팅 구성 변경 내용이 롤백되면 스캐폴드된 항목으로 탐색할 때 HTTP 404 오류가 사용자에게 표시됩니다.

해결 방법:

- MVC에 대해 이 오류를 해결하려면 새 스캐폴드된 항목을 추가하고 MVC 5 종속성(최소 또는 전체)을 선택합니다. 이 프로세스는 프로젝트에 필요한 모든 변경 내용을 추가합니다.
- 웹 API에 대해 이 오류를 수정하려면 다음을 수행하십시오.

  1. 프로젝트에 WebApiConfig 클래스를 추가합니다.

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. WebApiConfig.등록을 Global.asax의 응용 프로그램\_시작 메서드에 다음과 같이 구성합니다.

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
