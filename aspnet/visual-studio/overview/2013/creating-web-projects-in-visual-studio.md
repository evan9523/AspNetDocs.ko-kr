---
uid: visual-studio/overview/2013/creating-web-projects-in-visual-studio
title: Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기 | Microsoft Docs
author: tdykstra
description: 이 항목에서는 업데이트 3을 사용 하 Visual Studio 2013에서 ASP.NET 웹 프로젝트를 만들기 위한 옵션에 대해 설명 합니다. 다음은 웹 개발에 대 한 몇 가지 새로운 기능입니다.
ms.author: riande
ms.date: 12/01/2014
ms.assetid: 61941e64-0c0d-4996-9270-cb8ccfd0cabc
msc.legacyurl: /visual-studio/overview/2013/creating-web-projects-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: fbb4cd7afa2506879d47bce980bf0164aad40c2c
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345466"
---
# <a name="creating-aspnet-web-projects-in-visual-studio-2013"></a>Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

> 이 항목에서는 업데이트 3 Visual Studio 2013에서 ASP.NET 웹 프로젝트를 만들기 위한 옵션에 대해 설명 합니다.
> 
> 다음은 이전 버전의 Visual Studio와 비교 했을 때 웹 개발을 위한 몇 가지 새로운 기능입니다.
> 
> - 여러 ASP.NET 프레임 워크 (Web Forms, MVC 및 Web API) [에 대 한 지원을](#add) 제공 하는 프로젝트를 만드는 간단한 UI입니다.
> - [ASP.NET Identity](#indauth)모든 ASP.NET 프레임 워크에서 동일 하 게 작동 하며 IIS 이외의 웹 호스팅 소프트웨어와 작동 하는 새로운 ASP.NET 멤버 자격 시스템입니다.
> - [부트스트랩](#bootstrap) 을 사용 하 여 반응 형 디자인 및 테마 기능을 제공 합니다.
> - [자동 테스트 프로젝트 만들기](#testproj) 및 [인트라넷 사이트 템플릿과](#winauth)같이 MVC에 대해서만 제공 되는 Web Forms에 대 한 새로운 기능입니다.
> 
> Azure Cloud Services 또는 Azure Mobile Services 웹 프로젝트를 만드는 방법에 대 한 자세한 내용은 [azure Cloud Services 시작](https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-get-started/) 및 [Azure Mobile Services .net 백 엔드를 사용 하 여 ASP.NET 및 순위표 앱 만들기](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)를 참조 하세요.

<a id="prerequisites"></a>
## <a name="prerequisites"></a>사전 요구 사항

이 문서는 [업데이트 3](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409) 이 설치 된 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) 에 적용 됩니다.

<a id="wap"></a>
## <a name="web-application-projects-versus-web-site-projects"></a>웹 응용 프로그램 프로젝트와 웹 사이트 프로젝트 비교

ASP.NET에서는 두 가지 종류의 웹 프로젝트, 즉 *웹 응용 프로그램 프로젝트* 와 *웹 사이트 프로젝트*중에서 선택할 수 있습니다. 새 개발을 위해 웹 응용 프로그램 프로젝트를 권장 하며,이 문서는 웹 응용 프로그램 프로젝트에만 적용 됩니다. 자세한 내용은 MSDN 사이트의 [웹 응용 프로그램 프로젝트와 Visual Studio의 웹 사이트 프로젝트](https://msdn.microsoft.com/library/dd547590(v=vs.120).aspx) 를 참조 하세요.

<a id="overview"></a>
## <a name="overview-of-web-application-project-creation"></a>웹 응용 프로그램 프로젝트 만들기 개요

다음 단계는 웹 프로젝트를 만드는 방법을 보여 줍니다.

1. **시작** 페이지 또는 **파일** 메뉴에서 **새 프로젝트** 를 클릭 합니다.
2. **새 프로젝트** 대화 상자의 왼쪽 창에서 **웹** 을 클릭 하 고 가운데 창에서 **ASP.NET 웹 응용 프로그램** 을 클릭 합니다.

    ![새 프로젝트 대화 상자](creating-web-projects-in-visual-studio/_static/image1.png)

    왼쪽 창에서 **클라우드** 를 선택 하 여 [azure 클라우드 서비스](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy), [Azure 모바일 서비스](https://msdn.microsoft.com/library/windows/apps/dn629482.aspx)또는 [azure WebJob](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-webjobs)을 만들 수 있습니다. 이 항목에서는 이러한 템플릿에 대해 다루지 않습니다.
3. 응용 프로그램에 대 한 상태 및 사용 모니터링을 원하는 경우 오른쪽 창에서 **프로젝트에 Application Insights 추가** 확인란을 클릭 합니다. 자세한 내용은 [웹 애플리케이션의 성능 모니터링](https://azure.microsoft.com/documentation/articles/app-insights-web-monitor-performance/)을 참조하세요.
4. 프로젝트 **이름**, **위치**및 기타 옵션을 지정한 다음 **확인**을 클릭 합니다.

    **새 ASP.NET 프로젝트** 대화 상자가 표시됩니다.

    ![새 프로젝트 대화 상자](creating-web-projects-in-visual-studio/_static/image2.png)
5. 템플릿을 클릭 합니다.

    ![템플릿 선택](creating-web-projects-in-visual-studio/_static/image3.png)
6. 템플릿에 포함 되지 않은 추가 프레임 워크에 대 한 지원을 추가 하려면 해당 확인란을 클릭 합니다. (표시 된 예제에서는 Web Forms 프로젝트에 MVC 및/또는 Web API를 추가할 수 있습니다.)

    ![프레임 워크 추가](creating-web-projects-in-visual-studio/_static/image4.png)
7. <a id="testproj"></a>단위 테스트 프로젝트를 추가 하려면 **단위 테스트 추가**를 클릭 합니다.

    ![단위 테스트 추가](creating-web-projects-in-visual-studio/_static/image5.png)
8. 템플릿이 기본적으로 제공 하는 것과 다른 인증 방법을 원하는 경우 **인증 변경**을 클릭 합니다.

    ![인증 구성 단추](creating-web-projects-in-visual-studio/_static/image6.png)

    ![인증 구성 대화 상자](creating-web-projects-in-visual-studio/_static/image7.png)

<a id="azurenewproj"></a>
### <a name="create-a-web-app-or-virtual-machine-in-azure"></a>Azure에서 웹 앱 또는 가상 머신 만들기

Visual Studio에는 웹 응용 프로그램을 호스팅하기 위해 Azure 서비스를 쉽게 사용할 수 있도록 하는 기능이 포함 되어 있습니다. 예를 들어 Visual Studio IDE에서 다음의 모든 권한을 수행할 수 있습니다.

- 인터넷을 통해 응용 프로그램을 사용할 수 있도록 하는 웹 앱 또는 가상 머신을 만들고 관리 합니다.
- 클라우드에서 실행 되는 응용 프로그램에 의해 생성 된 로그를 봅니다.
- 응용 프로그램이 클라우드에서 실행 되는 동안 원격으로 디버그 모드에서 실행 합니다.
- SQL 데이터베이스와 같은 다른 Azure 서비스를 보고 관리 합니다.

웹 앱과 같은 기본 서비스를 무료로 포함 하는 [Azure 계정을 만들](https://www.windowsazure.com/pricing/free-trial/) 수 있습니다. MSDN 구독자 인 경우 추가 Azure 서비스에 대 한 월간 크레딧을 제공 하는 [혜택을 활성화할](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/) 수 있습니다. 

기본적으로 **새 ASP.NET 프로젝트** 대화 상자를 사용 하 여 새 웹 프로젝트에 대 한 웹 앱 또는 가상 컴퓨터를 만들 수 있습니다. 새 웹 앱 또는 가상 머신을 만들지 않으려는 경우 **클라우드의 호스트** 확인란을 선택 취소 합니다.

![원격 리소스 만들기](creating-web-projects-in-visual-studio/_static/image8.png)

확인란 캡션은 **클라우드에서 호스트** 되거나 **원격 리소스를 만들**수 있으며, 두 경우 모두 결과가 동일 합니다. 확인란을 선택 된 상태로 두면 Visual Studio에서 기본적으로 Azure App Service에서 웹 앱을 만듭니다. 원하는 경우 드롭다운 상자를 사용 하 여이를 **가상 머신으로** 변경할 수 있습니다. Azure에 아직 로그인 하지 않은 경우 Azure 자격 증명을 입력 하 라는 메시지가 표시 됩니다. 로그인 한 후에는 대화 상자를 사용 하 여 Visual Studio에서 프로젝트에 대해 만들 리소스를 구성할 수 있습니다. 다음 그림에서는 웹 앱에 대 한 대화 상자를 보여 줍니다. 가상 컴퓨터를 만들도록 선택 하는 경우 다양 한 옵션이 표시 됩니다.

![Azure 앱 설정 구성](creating-web-projects-in-visual-studio/_static/image9.png)

Azure 리소스를 만드는 데이 프로세스를 사용 하는 방법에 대 한 자세한 내용은 [Azure 시작 및 ASP.NET](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) 을 참조 하 고 [Visual Studio를 사용 하 여 웹 사이트에 대 한 가상 머신 만들기](https://azure.microsoft.com/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/)를 참조 하세요.

이 문서의 나머지 부분에서는 사용 가능한 템플릿 및 해당 옵션에 대 한 자세한 정보를 제공 합니다. 이 문서에는 템플릿에 사용 되는 부트스트랩, 레이아웃 및 테마 프레임 워크도 도입 되었습니다.

<a id="vs2013"></a>
## <a name="visual-studio-2013-web-project-templates"></a>Visual Studio 2013 웹 프로젝트 템플릿

Visual Studio는 템플릿을 사용 하 여 웹 프로젝트를 만듭니다. 프로젝트 템플릿은 새 프로젝트에 파일 및 폴더를 만들고, NuGet 패키지를 설치 하 고, 기초적인 작업 응용 프로그램에 대 한 샘플 코드를 제공할 수 있습니다. 템플릿은 최신 웹 표준을 구현 하며 ASP.NET 기술을 사용 하는 방법에 대 한 모범 사례를 설명 하 고 사용자 고유의 응용 프로그램을 만들기 위한 빠른 시작을 제공 하기 위한 것입니다.

Visual Studio 2013 .NET framework의 .NET 4.5 이상 버전을 대상으로 하는 프로젝트의 웹 프로젝트 템플릿에 대 한 다음 선택 항목을 제공 합니다.

- [빈 템플릿](#empty)
- [Web Forms 템플릿](#wf)
- [MVC 템플릿](#mvc)
- [Web API 템플릿](#webapi)
- [단일 페이지 응용 프로그램 템플릿](#spa)
- [Azure 모바일 서비스 템플릿](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)
- [Visual Studio 2012 템플릿](#vs2012)

[Facebook 템플릿을](#facebook)제공 하는 Visual Studio 확장을 설치할 수도 있습니다.

.NET 4를 대상으로 하는 프로젝트를 만드는 방법에 대 한 자세한 내용은이 항목의 뒷부분에 나오는 [Visual Studio 2012 템플릿](#vs2012) 을 참조 하세요.

모바일 클라이언트용 ASP.NET 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 [ASP.NET의 모바일 지원](../../../mobile/overview.md)을 참조 하세요.

<a id="empty"></a>
### <a name="empty-template"></a>빈 템플릿

빈 템플릿은 프로젝트 파일 (*.csproj* 또는)과 같은 ASP.NET 웹 앱에 대 한 최소 폴더와 파일을 제공 합니다.* .vbproj*) 및 *Web.config* 파일을 만듭니다. **다음에 대 한 폴더 및 핵심 참조 추가:** 레이블에 있는 확인란을 사용 하 여 WEB FORMS, MVC 및/또는 Web API에 대 한 지원을 추가할 수 있습니다.

빈 템플릿에서는 인증 옵션을 사용할 수 없습니다. 인증 기능은 샘플 응용 프로그램에서 구현 되며, 빈 템플릿은 샘플 응용 프로그램을 만들지 않습니다.

<a id="wf"></a>
### <a name="web-forms-template"></a>Web Forms 템플릿

Web Forms 프레임 워크는 UI 및 데이터 액세스 기능에 다양 한 웹 사이트를 신속 하 게 빌드할 수 있도록 지 원하는 다음과 같은 기능을 제공 합니다.

- Visual Studio의 WYSIWYG 디자이너.
- HTML을 렌더링 하 고 속성 및 스타일을 설정 하 여 사용자 지정할 수 있는 서버 컨트롤입니다.
- 데이터 액세스 및 데이터를 표시 하는 다양 한 컨트롤입니다.
- WPF와 같은 클라이언트 응용 프로그램을 프로그래밍 하는 것 처럼 프로그래밍할 수 있는 이벤트를 노출 하는 이벤트 모델입니다.
- HTTP 요청 간에 상태 (데이터)를 자동으로 보존 합니다.

일반적으로 Web Forms 응용 프로그램을 만들려면 ASP.NET MVC 프레임 워크를 사용 하 여 동일한 응용 프로그램을 만드는 것 보다 더 많은 프로그래밍 노력이 필요 합니다. 그러나 Web Forms는 신속한 응용 프로그램 개발을 위한 것이 아닙니다. Web Forms을 기반으로 하는 복잡 한 상용 응용 프로그램 및 프레임 워크가 많이 있습니다.

Web Forms 페이지와 페이지의 컨트롤은 브라우저에 전송 된 많은 태그를 자동으로 생성 하기 때문에 ASP.NET MVC에서 제공 하는 HTML을 세밀 하 게 제어할 수 없습니다. 페이지 및 컨트롤을 구성 하기 위한 선언적 모델은 작성 해야 할 코드의 양을 최소화 하지만 HTML 및 HTTP의 일부 동작을 숨깁니다. 예를 들어, 컨트롤에서 생성 될 수 있는 태그를 정확 하 게 지정할 수는 없습니다.

Web Forms framework는 [테스트 기반 개발](http://en.wikipedia.org/wiki/Test-driven_development), [문제 분리](http://en.wikipedia.org/wiki/Separation_of_concerns), [제어의 반전](http://en.wikipedia.org/wiki/Inversion_of_control), [종속성 주입](http://en.wikipedia.org/wiki/Dependency_injection)등의 패턴 기반 개발 방법으로 MVC를 ASP.NET 하는 것과는 다른 기능을 쉽게 활용 하지 못합니다. 이러한 방식으로 코드를 작성 하려는 경우 다음을 수행할 수 있습니다. ASP.NET MVC 프레임 워크에 있는 것 처럼 자동이 아니라는 것입니다. [ASP.NET WEB FORMS MVP](http://webformsmvp.com/) 프로젝트는 Web Forms에서 제공 하는 신속한 개발을 유지 하면서 문제와 테스트 용이성을 쉽게 구분할 수 있는 방법을 보여 줍니다. Microsoft SharePoint는 Web Forms MVP를 기반으로 합니다.

Web Forms 템플릿은 [부트스트랩](#bootstrap) 을 사용 하 여 응답성이 뛰어난 디자인 및 테마 기능을 제공 하는 샘플 Web Forms 응용 프로그램을 만듭니다. 다음 그림에서는 홈 페이지를 보여 줍니다.

![Web Forms 템플릿 앱 홈 페이지](creating-web-projects-in-visual-studio/_static/image10.png)

Web Forms에 대 한 자세한 내용은 [ASP.NET Web Forms](https://asp.net/web-forms)를 참조 하세요. Web Forms 템플릿에 대 한 자세한 내용은 [Visual Studio 2013를 사용 하 여 기본 Web Forms 응용 프로그램 빌드](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx)를 참조 하세요.

<a id="mvc"></a>
### <a name="mvc-template"></a>MVC 템플릿

ASP.NET MVC는 [테스트 기반 개발](http://en.wikipedia.org/wiki/Test-driven_development), [문제 분리](http://en.wikipedia.org/wiki/Separation_of_concerns), [제어의 반전](http://en.wikipedia.org/wiki/Inversion_of_control), [종속성 주입](http://en.wikipedia.org/wiki/Dependency_injection)등의 패턴 기반 개발 방법을 용이 하 게 하기 위해 설계 되었습니다. 프레임 워크는 웹 응용 프로그램의 비즈니스 논리 계층을 프레젠테이션 계층과 분리 하는 것을 권장 합니다. 응용 프로그램을 모델 (M), 뷰 (V) 및 컨트롤러 (C)로 나누면 ASP.NET MVC를 사용 하 여 더 큰 응용 프로그램에서 복잡 한 작업을 쉽게 관리할 수 있습니다.

ASP.NET MVC를 사용 하면 Web Forms 보다 HTML 및 HTTP를 사용 하 여 직접 작업할 수 있습니다. 예를 들어 Web Forms는 HTTP 요청 간의 상태를 자동으로 유지할 수 있지만 MVC에서 명시적으로 코딩 해야 합니다. MVC 모델의 장점은 응용 프로그램에서 수행 하는 작업과 웹 환경에서 작동 하는 방식에 대 한 완전 한 제어를 얻을 수 있다는 것입니다. 단점은 더 많은 코드를 작성 해야 한다는 것입니다.

MVC는 확장 가능 하도록 설계 되었으며, 개발자에 게 응용 프로그램 요구 사항에 맞게 프레임 워크를 사용자 지정할 수 있는 기능을 제공 합니다. 또한 ASP.NET MVC 소스 코드는 OSI 라이선스에서 사용할 수 있습니다.

MVC 템플릿에서는 [부트스트랩](#bootstrap) 을 사용 하 여 반응 형 디자인 및 테마 기능을 제공 하는 샘플 MVC 5 응용 프로그램을 만듭니다. 다음 그림에서는 홈 페이지를 보여 줍니다.

![MVC 샘플 응용 프로그램](creating-web-projects-in-visual-studio/_static/image11.png)

MVC에 대 한 자세한 내용은 [ASP.NET mvc](https://asp.net/mvc)를 참조 하세요. MVC 4 템플릿을 선택 하는 방법에 대 한 자세한 내용은이 문서의 뒷부분에 나오는 [Visual Studio 2012 템플릿](#vs2012) 을 참조 하세요.

<a id="webapi"></a>
### <a name="web-api-template"></a>Web API 템플릿

Web API 템플릿에서는 MVC 기반 API 도움말 페이지를 포함 하 여 Web API를 기반으로 샘플 웹 서비스를 만듭니다.

ASP.NET Web API는 브라우저 및 모바일 디바이스를 비롯한 광범위한 클라이언트에 연결하는 HTTP 서비스를 쉽게 빌드할 수 있게 해 주는 프레임워크입니다. ASP.NET Web API은 .NET Framework에서 RESTful services를 빌드하기 위한 이상적인 플랫폼입니다.

Web API 템플릿은 샘플 웹 서비스를 만듭니다. 다음 그림에서는 예제 도움말 페이지를 보여 줍니다.

![Web API 도움말 페이지](creating-web-projects-in-visual-studio/_static/image12.png)

![API 가져오기에 대 한 Web API 도움말 페이지](creating-web-projects-in-visual-studio/_static/image13.png)

Web API에 대 한 자세한 내용은 [ASP.NET Web API](https://asp.net/web-api)를 참조 하세요.

<a id="spa"></a>
### <a name="single-page-application-template"></a>단일 페이지 응용 프로그램 템플릿

SPA (단일 페이지 응용 프로그램) 템플릿은 클라이언트에서 JavaScript, HTML 5 및 [KnockoutJS](http://knockoutjs.com/) 를 사용 하 고 서버에 ASP.NET Web API 하는 예제 응용 프로그램을 만듭니다.

SPA 템플릿에 대 한 유일한 인증 옵션은 [개별 사용자 계정](#indauth)입니다.

다음 그림에서는 SPA 템플릿이 빌드하는 샘플 응용 프로그램의 초기 상태를 보여 줍니다.

![SPA 샘플 응용 프로그램](creating-web-projects-in-visual-studio/_static/image14.png)

SPA 템플릿을 사용 하 여 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 [WEB API-외부 인증 서비스](../../../web-api/overview/security/external-authentication-services.md)를 참조 하세요.

ASP.NET 단일 페이지 응용 프로그램에 대 한 자세한 내용과 KnockoutJS 이외의 JavaScript 프레임 워크를 사용 하는 추가 SPA 템플릿에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 단일 페이지 응용 프로그램](../../../single-page-application/index.md)입니다.
- [VS2013 RC 용 SPA 템플릿의 보안 기능 이해](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)
- [단일 페이지 응용 프로그램: ASP.NET를 사용 하 여 최신의 응답성이 뛰어난 Web Apps 빌드](https://msdn.microsoft.com/magazine/dn463786.aspx)

<a id="facebook"></a>
### <a name="facebook-template"></a>Facebook 템플릿

[Facebook 템플릿을 제공 하는 Visual Studio 확장](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409)을 설치할 수 있습니다. 이 템플릿은 Facebook 웹 사이트 내에서 실행 되도록 설계 된 샘플 응용 프로그램을 만듭니다. ASP.NET MVC를 기반으로 하며, 실시간 업데이트 기능을 위해 Web API를 사용 합니다.

Facebook 응용 프로그램은 facebook 사이트 내에서 실행 되 고 Facebook의 인증을 사용 하기 때문에 Facebook 템플릿에는 인증 옵션을 사용할 수 없습니다.

ASP.NET Facebook 응용 프로그램에 대 한 자세한 내용은 [MVC FACEBOOK API 업데이트](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx)를 참조 하세요.

<a id="vs2012"></a>
### <a name="visual-studio-2012-templates"></a>Visual Studio 2012 템플릿

Visual Studio 2013 웹 프로젝트 만들기 대화 상자는 Visual Studio 2012에서 사용할 수 있는 일부 템플릿에 대 한 액세스를 제공 하지 않습니다. 이러한 템플릿 중 하나를 사용 하려는 경우 Visual Studio 새 프로젝트 대화 상자의 왼쪽 창에서 Visual Studio 2012 노드를 클릭 하면 됩니다.

![Visual Studio 2012 템플릿](creating-web-projects-in-visual-studio/_static/image15.png)

**Visual Studio 2012** 노드를 사용 하 여 Visual Studio 2013에 대 한 기본 템플릿 목록에서 액세스할 수 없는 다음 웹 템플릿을 선택할 수 있습니다.

- ASP.NET MVC 4 웹 애플리케이션
- ASP.NET 동적 데이터 엔터티 웹 애플리케이션
- ASP.NET AJAX 서버 컨트롤
- ASP.NET AJAX 서버 컨트롤 Extender
- ASP.NET 서버 컨트롤

<a id="bootstrap"></a>
## <a name="bootstrap-in-the-visual-studio-2013-web-project-templates"></a>Visual Studio 2013 웹 프로젝트 템플릿의 부트스트랩

Visual Studio 2013 프로젝트 템플릿은 Twitter를 사용 하 여 생성 된 레이아웃 및 테마 프레임 워크인 [부트스트랩](http://getbootstrap.com/)을 사용 합니다. 부트스트랩은 CSS3를 사용 하 여 반응 형 디자인을 제공 합니다. 즉, 레이아웃이 여러 브라우저 창 크기에 맞게 동적으로 조정 될 수 있습니다. 예를 들어, 넓은 브라우저 창에서 Web Forms 템플릿으로 만든 홈 페이지는 다음 그림과 같습니다.

![Web Forms 템플릿 앱 홈 페이지](creating-web-projects-in-visual-studio/_static/image16.png)

창을 더 좁게 하 고 가로로 정렬 된 열은 세로 정렬로 이동 합니다.

![부트스트랩 세로 열 정렬](creating-web-projects-in-visual-studio/_static/image17.png)

창을 좀 더 좁게 하 고 가로 위쪽 메뉴를 클릭 하 여 세로 방향 메뉴로 확장할 수 있는 아이콘으로 전환 합니다.

![부트스트랩 메뉴 아이콘](creating-web-projects-in-visual-studio/_static/image18.png)

![부트스트랩 세로 메뉴](creating-web-projects-in-visual-studio/_static/image19.png)

부트스트랩의 테마 기능을 사용 하 여 응용 프로그램의 모양과 느낌을 쉽게 변경할 수도 있습니다. 예를 들어 다음 단계를 수행 하 여 테마를 변경할 수 있습니다.

1. 브라우저에서로 이동 하 여 [http://Bootswatch.com](http://Bootswatch.com) 테마를 선택 하 고 **다운로드**를 클릭 합니다. 이는 기본적으로 *부트스트랩. min .css* 를 다운로드 합니다. css 코드를 검사 하려는 경우에는 확인 되지 않은 버전 대신 *부트스트래핑* 을 가져옵니다.
2. 다운로드 한 CSS 파일의 내용을 복사 합니다.
3. Visual Studio에서 *Content* 폴더에 *Bootstrap-theme* 라는 새 **스타일 시트** 파일을 만들고 다운로드 한 css 코드를 붙여넣습니다.
4. *앱 \_ 시작/Bundle.config* 를 열고 bootstrap-theme *를 변경* 합니다. *bootstrap-theme.css*

프로젝트를 다시 실행 하면 응용 프로그램에 새로운 모양이 표시 됩니다. 다음 그림은 Amelia 테마의 효과를 보여 줍니다.

![부트스트랩 Amelia 테마](creating-web-projects-in-visual-studio/_static/image20.png)

무료 및 프리미엄 버전 모두에서 많은 부트스트랩 테마를 사용할 수 있습니다. 또한 부트스트랩은 [드롭다운](http://twitter.github.io/bootstrap/components.html#dropdowns), [단추 그룹](http://twitter.github.io/bootstrap/components.html#buttonGroups)및 [아이콘과](http://twitter.github.io/bootstrap/base-css.html#images)같은 다양 한 UI 구성 요소를 제공 합니다. 부트스트랩에 대 한 자세한 내용은 [부트스트랩 사이트](http://twitter.github.io/bootstrap/)를 참조 하십시오.

Visual Studio에서 Web Forms 디자이너를 사용 하는 경우 디자이너는 CSS3을 지원 하지 않으므로 부트스트랩 테마 또는 반응 형 레이아웃 변경의 모든 효과를 정확 하 게 표시 하지 않습니다. 그러나 브라우저를 사용 하 여 볼 때 Web Forms 페이지가 제대로 표시 됩니다.

<a id="add"></a>
## <a name="adding-support-for-additional-frameworks"></a>추가 프레임 워크에 대 한 지원 추가

템플릿을 선택 하면 템플릿에 사용 되는 프레임 워크의 확인란이 자동으로 선택 됩니다. 예를 들어 **Web Forms** 템플릿을 선택 하는 경우 **Web Forms** 확인란을 선택 하 고이 확인란을 선택 취소할 수 없습니다.

![템플릿 선택](creating-web-projects-in-visual-studio/_static/image21.png)

![프레임 워크 추가](creating-web-projects-in-visual-studio/_static/image22.png)

프로젝트를 만들 때 해당 프레임 워크에 대 한 지원을 추가 하기 위해 템플릿에 포함 되지 않은 프레임 워크의 확인란을 선택할 수 있습니다. 예를 들어 MVC 템플릿을 선택한 경우 Web Forms *.aspx* 페이지를 사용할 수 있도록 **Web Forms** 확인란을 선택 합니다. 또는 Web Forms 템플릿을 사용할 때 MVC를 사용 하도록 설정 하려면 **mvc** 확인란을 클릭 합니다. 프레임 워크를 추가 하면 디자인 타임 및 런타임 지원을 사용할 수 있습니다. 예를 들어 Web Forms 프로젝트에 MVC 지원을 추가 하는 경우 컨트롤러 및 뷰를 스 캐 폴드 수 있습니다.

프로젝트에 Web Forms 및 MVC를 결합 하 고 Web Forms에서 [친숙](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx) 한 url을 사용 하도록 설정 하는 경우 한 URL에 가능한 대상이 여러 개 있는 경우 예기치 않은 라우팅 문제가 발생할 수 있습니다. 먼저 정의 된 경로가 우선적으로 적용 됩니다. 예를 들어 `Home` 컨트롤러와 *home.aspx* 페이지가 있는 경우 `http://contoso.com/home` RouteConfig.cs에서 메서드를 호출 하기 전에 메서드를 호출 하면 url이 *홈페이지로* 이동 하 고, `EnableFriendlyUrls` 이전에를 호출 하면 `MapRoute` 동일한 url *RouteConfig.cs*이 컨트롤러에 대 한 기본 뷰로 이동 `Home` `MapRoute` `EnableFriendlyUrls` 합니다.

프레임 워크를 추가 하는 것은 샘플 응용 프로그램 기능을 추가 하지 않습니다. 예를 들어 MVC 템플릿을 선택한 경우 Web Forms 지원을 추가 하면 default.aspx 홈 페이지 파일이 생성 되지 *않습니다.* 프레임 워크를 지 원하는 데 필요한 폴더, 파일 및 참조만 추가 됩니다. 이러한 이유로 프레임 워크를 추가 해도 인증 옵션이 변경 되지 않으며 템플릿에서 생성 된 샘플 응용 프로그램의 코드에 의해 구현 됩니다. 예를 들어 빈 템플릿을 선택 하 고 Web Forms 또는 MVC 지원을 추가 하면 **인증 구성** 단추를 사용할 수 없게 됩니다.

다음 섹션에서는 각 확인란의 효과를 간략하게 설명 합니다.

### <a name="add-web-forms-support"></a>Web Forms 지원 추가

빈 *앱 \_ 데이터* 및 *모델* 폴더와 *global.asax* 파일을 만듭니다. 이는 비어 있는 템플릿 이외의 모든 템플릿에서 이미 만들어졌으므로 Web Forms 확인란을 선택 하면 다른 템플릿에는 차이가 없습니다.

Web Forms 템플릿은 기본적으로 친숙 한 Url을 사용 하도록 설정 하지만 Web Forms 확인란을 선택 하 여 다른 템플릿에 지원 Web Forms 추가 하면 친숙 한 Url이 자동으로 사용 되지 않습니다.

### <a name="add-mvc-support"></a>MVC 지원 추가

MVC, Razor 및 웹 페이지 NuGet 패키지를 설치 하 고, 빈 *앱 \_ 데이터*, *컨트롤러*, *모델*및 *뷰* 폴더를 만들며, *RouteConfig.cs* file을 사용 하 여 *앱 \_ 시작* 폴더 *를 만들고, global.asax 파일을* 만듭니다.

### <a name="add-web-api-support"></a>Web API 지원 추가

NuGet 패키지에 WebApi 및 Newtonsoft.Js를 설치 하 고, 빈 *앱 \_ 데이터*, *컨트롤러*및 *모델* 폴더를 만들며, *WebApiConfig.cs* 파일을 사용 하 여 *앱 \_ 시작* 폴더 *를 만들고, global.asax 파일을* 만듭니다.

<a id="auth"></a>
## <a name="authentication-methods"></a>인증 방법

Visual Studio 2013 Web Forms, MVC 및 Web API 템플릿에 대 한 몇 가지 인증 옵션을 제공 합니다.

- [인증 없음](#noauth)
- [개별 사용자 계정](#indauth) (ASP.NET Identity, 이전의 ASP.NET 멤버 자격)
- [조직 계정](#orgauth) (Windows Server Active Directory 또는 Azure Active Directory)
- [Windows 인증](#winauth) (인트라넷)

![인증 구성 대화 상자](creating-web-projects-in-visual-studio/_static/image23.png)

<a id="noauth"></a>

### <a name="no-authentication"></a>인증 없음

**인증 안 함**을 선택 하는 경우 샘플 응용 프로그램에는 로그인 하는 데 사용할 웹 페이지, 로그인 한 사용자를 나타내는 UI, 멤버 자격 데이터베이스에 대 한 엔터티 클래스 및 멤버 자격 데이터베이스에 대 한 연결 문자열이 없습니다 .가 포함 됩니다.

<a id="indauth"></a>
### <a name="individual-user-accounts"></a>개별 사용자 계정

**개별 사용자 계정을**선택 하는 경우 샘플 응용 프로그램은 사용자 인증을 위해 ASP.NET Identity (이전의 ASP.NET membership)를 사용 하도록 구성 됩니다. ASP.NET Identity를 사용 하면 사용자가 사이트에서 사용자 이름 및 암호를 만들거나 Facebook, Google, Microsoft 계정, Twitter 등의 소셜 공급자를 사용 하 여 로그인 하 여 계정을 등록할 수 있습니다. ASP.NET Identity의 사용자 프로필에 대 한 기본 데이터 저장소는 SQL Server LocalDB 데이터베이스로, 프로덕션 사이트에 대해 SQL Server 하거나 Azure SQL Database에 배포할 수 있습니다.

Visual Studio 2013이 기능은 Visual Studio 2012와 동일 하지만 ASP.NET 멤버 자격 시스템의 기본 코드는 다시 작성 되었습니다. 새 코드 베이스의 장점은 다음과 같습니다.

- 새 멤버 자격 시스템은 ASP.NET Forms 인증 모듈이 아닌 [OWIN](http://owin.org/) 을 기반으로 합니다. 즉, IIS에서 Web Forms 또는 MVC를 사용 하 고 있는지 또는 자체 호스팅 웹 API 또는 SignalR와 같은 인증 메커니즘을 사용할 수 있습니다.
- 새 멤버 자격 데이터베이스는 Entity Framework Code First에 의해 관리 되며, 모든 테이블은 수정할 수 있는 엔터티 클래스로 표시 됩니다. 즉, 고유한 요구 사항에 맞게 데이터베이스 스키마 및 프로필 관련 웹 UI를 쉽게 사용자 지정할 수 있으며 Code First 마이그레이션를 사용 하 여 업데이트를 쉽게 배포할 수 있습니다.

새 멤버 자격 시스템은 새 템플릿에서 자동으로 구현 되며 .NET 4.5 이상을 대상으로 하는 모든 프로젝트에서 수동으로 구현할 수 있습니다.

ASP.NET Identity는 주로 외부 고객용 인터넷 웹 사이트를 만드는 경우에 적합 합니다. 조직에서 Active Directory 또는 Office 365를 사용 하 고 직원과 비즈니스 파트너에 대 한 single sign-on을 사용 하도록 설정 하는 프로젝트를 만들려는 경우 **조직 계정** 옵션을 선택 하는 것이 더 좋을 수 있습니다.

개별 사용자 계정 옵션에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [www.asp.net/identity](../../../identity/index.md). ASP.NET 웹 사이트의 ASP.NET Identity에 대 한 설명서입니다.
- [Facebook 및 Google OAuth2 및 Openid connect sign-on을 사용 하 여 ASP.NET MVC 5 앱을 만듭니다](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md). 또한 사용자 프로필 데이터를 사용자 지정 하는 방법을 보여 줍니다.
- [웹 API-외부 인증 서비스](../../../web-api/overview/security/external-authentication-services.md)
- [Visual Studio 2013에서 ASP.NET 응용 프로그램에 외부 로그인 추가](https://blogs.msdn.com/b/webdev/archive/2013/06/27/adding-external-logins-to-your-asp-net-application-in-visual-studio-2013.aspx)

<a id="orgauth"></a>
### <a name="organizational-accounts"></a>조직 계정

**조직 계정을**선택 하는 경우 샘플 응용 프로그램은 Azure Active Directory의 사용자 계정 (Office 365을 포함 하는 Azure AD) 또는 windows Server Active Directory를 기반으로 인증에 WIF (Windows Identity Foundation)를 사용 하도록 구성 됩니다. 자세한 내용은이 항목의 뒷부분에 나오는 [조직 계정 인증 옵션](#orgauthoptions) 을 참조 하십시오.

<a id="winauth"></a>
### <a name="windows-authentication"></a>Windows 인증

**Windows 인증**을 선택 하는 경우 응용 프로그램 예제는 인증을 위해 WINDOWS 인증 IIS 모듈을 사용 하도록 구성 됩니다. 응용 프로그램은 Windows에 로그인 되어 있지만 사용자 등록 또는 로그인 UI를 포함 하지 않는 Active directory 또는 로컬 컴퓨터 계정의 도메인 및 사용자 ID를 표시 합니다. 이 옵션은 인트라넷 웹 사이트를 위한 것입니다.

또는 [조직 계정에서 온-프레미스 옵션](#orgauthonprem)을 선택 하 여 AD 인증을 사용 하는 인트라넷 사이트를 만들 수 있습니다. 온-프레미스 옵션은 Windows 인증 모듈 대신 WIF (Windows Identity Foundation)를 사용 합니다. 온-프레미스 옵션을 설정 하기 위해 몇 가지 추가 단계가 필요 하지만, WIF는 Windows 인증 모듈에서 사용할 수 없는 기능을 사용 하도록 설정 합니다. 예를 들어 WIF를 사용 하 여 Active Directory에서 응용 프로그램 액세스를 구성 하 고 디렉터리 데이터를 쿼리할 수 있습니다.

<a id="orgauthoptions"></a>
## <a name="organizational-account-authentication-options"></a>조직 계정 인증 옵션

**인증 구성** 대화 상자는 Azure Active Directory (Office 365을 포함 하는 Azure ad) 또는 Windows Server ACTIVE DIRECTORY (ad) 계정 인증에 대 한 몇 가지 옵션을 제공 합니다.

- [클라우드-단일 조직](#orgauthsingle) (azure Ad 또는 azure ad와의 디렉터리 통합을 사용한 ad)
- [클라우드-다중 조직](#orgauthmulti) (azure Ad 또는 azure ad와의 디렉터리 통합을 사용한 ad)
- [온-프레미스](#orgauthonprem) (AD)

Azure AD 옵션 중 하나를 시도 하지만 아직 계정이 없는 경우 [여기를 클릭 하 여 AZURE ad 계정에 등록](https://go.microsoft.com/fwlink/?LinkId=309942)합니다.

> [!NOTE]
> Azure AD 옵션 중 하나를 선택 하는 경우 프로젝트에 데이터베이스가 필요 하 고 Azure AD 테 넌 트의 전역 관리자 계정에 로그인 해야 합니다. admin@contoso.onmicrosoft.comAZURE AD 테 넌 트에 대 한 관리 권한이 있는 조직 계정 (예:)에 대 한 이름 및 암호를 입력 합니다.
> 
> **로그인 대화 상자에서 Microsoft 계정에 대 한 자격 증명을 입력 하지 않습니다 (예: contoso@hotmail.com ).**

<a id="orgauthsingle"></a>
### <a name="cloud---single-organization-authentication"></a>클라우드-단일 조직 인증

![단일 조직 인증](creating-web-projects-in-visual-studio/_static/image24.png)

하나의 Azure AD [테 넌 트](https://technet.microsoft.com/library/jj573650.aspx)에 정의 된 사용자 계정에 대 한 인증을 사용 하도록 설정 하려면이 옵션을 선택 합니다. 예를 들어 사이트는 contoso.com이 고 contoso.onmicrosoft.com 테 넌 트에 있는 Contoso 회사 직원 들이 사용할 수 있게 됩니다. 다른 테 넌 트의 사용자가 응용 프로그램에 액세스할 수 있도록 Azure AD를 구성할 수 없습니다.

#### <a name="domain"></a>도메인

응용 프로그램을 설정 하려는 Azure AD 도메인을 입력 합니다 (예:) `contoso.onmicrosoft.com` . 대신 [사용자 지정 도메인](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/)(예:)이 있는 경우 `contoso.com` `contoso.onmicrosoft.com` 여기에 입력할 수 있습니다.

#### <a name="access-level"></a>액세스 수준

응용 프로그램이 Graph API를 사용 하 여 디렉터리 정보를 쿼리하거나 업데이트 해야 하는 경우 **Single sign-on, 디렉터리 데이터 읽기** 또는 **Single Sign-on, 디렉터리 데이터 읽기 및 쓰기**를 선택 합니다. 그렇지 않으면 **Single sign-on**을 선택 합니다. 자세한 내용은 [응용 프로그램 액세스 수준](https://msdn.microsoft.com/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels) 및 Graph API를 [사용 하 여 Azure AD 쿼리](https://msdn.microsoft.com/library/windowsazure/dn151791.aspx)를 참조 하세요.

#### <a name="application-id-uri"></a>애플리케이션 ID URI

기본적으로 템플릿은 Azure AD 도메인에 프로젝트 이름을 추가 하 여 응용 프로그램 ID URI를 만듭니다. 예를 들어 프로젝트 이름이이 `Example` 고 도메인이 인 경우 `contoso.onmicrosoft.com` 응용 프로그램 ID URI는가 됩니다 `https://contoso.onmicrosoft.com/Example` . 응용 프로그램 ID URI를 수동으로 지정 하려면 **추가 옵션** 섹션을 확장 하 고 텍스트 상자에 응용 프로그램 id uri를 입력 합니다. 응용 프로그램 ID URI는로 시작 해야 합니다 `https://` .

기본적으로 Azure AD에 이미 프로 비전 된 응용 프로그램에 Visual Studio가 프로젝트에 사용 하는 것과 동일한 응용 프로그램 ID URI가 있는 경우 프로젝트는 새 응용 프로그램을 프로 비전 하는 대신 기존 응용 프로그램에 연결 됩니다. 이 경우 새 응용 프로그램을 프로 비전 하려면 **동일한 ID를 가진 응용 프로그램 항목이 있으면 덮어쓰기** 확인란의 선택을 취소 합니다.

**덮어쓰기** 확인란의 선택을 취소 한 경우 Visual Studio에서 동일한 응용 프로그램 ID URI를 사용 하는 기존 응용 프로그램을 찾으면 사용할 uri에 번호를 추가 하 여 새 uri를 만듭니다. 예를 들어 프로젝트 이름이 이면 `Example` 텍스트 상자를 비워 두고, **덮어쓰기** 확인란의 선택을 취소 하 고, Azure AD 테 넌 트에 이미 URI가 있는 응용 프로그램이 있다고 가정 합니다 `https://contoso.onmicrosoft.com/Example` . 이 경우 새 응용 프로그램은와 같은 응용 프로그램 ID URI를 사용 하 여 프로 비전 됩니다 `https://contoso.onmicrosoft.com/Example_20130619330903` .

#### <a name="provisioning-the-application-in-azure-ad"></a>Azure AD에서 응용 프로그램 프로 비전

Azure AD에서 응용 프로그램을 프로 비전 하거나 프로젝트를 기존 응용 프로그램에 연결 하기 위해 Visual Studio에는 도메인에 대 한 전역 관리자의 자격 증명이 필요 합니다. **인증 구성** 대화 상자에서 **확인** 을 클릭 하면 지정한 도메인에 대 한 전역 관리자의 사용자 이름 및 암호를 입력 하 라는 메시지가 표시 됩니다. 나중에 **새 ASP.NET 프로젝트** 대화 상자에서 **프로젝트 만들기** 를 클릭 하면 VISUAL Studio는 Azure AD에서 응용 프로그램을 프로 비전 합니다. 이 프로세스의 일부로 Visual Studio는 만든 후 1 년이 지나면 만료 되는 Web.config 파일에 클라이언트 암호 값을 포함 합니다.

**클라우드 단일 조직** 인증을 사용 하는 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Azure 인증](../2012/windows-azure-authentication.md)
- [Azure AD를 사용하여 웹 애플리케이션에 로그온 추가](https://msdn.microsoft.com/library/windowsazure/dn151790.aspx)
- [Azure Active Directory를 사용하여 ASP.NET 앱 개발](../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)
- [Azure AD 및 Microsoft OWIN 구성 요소를 사용 하 여 보안 ASP.NET Web API](https://msdn.microsoft.com/magazine/dn463788.aspx)

Visual Studio 2013에 대 한 자습서는 아직 업데이트 되지 않았습니다. 수동으로 수행할 수 있는 자습서의 일부는 Visual Studio 2013에서 자동화 됩니다.

<a id="orgauthmulti"></a>
### <a name="cloud---multi-organization-authentication"></a>클라우드-다중 조직 인증

![여러 조직 인증](creating-web-projects-in-visual-studio/_static/image25.png)

여러 Azure AD [테 넌 트](https://technet.microsoft.com/library/jj573650.aspx)에 정의 된 사용자 계정에 대 한 인증을 사용 하도록 설정 하려면이 옵션을 선택 합니다. 예를 들어 사이트는 contoso.com이 고 contoso.onmicrosoft.com 테 넌 트에 있는 Contoso 회사 직원 및 fabrikam.onmicrosoft.com 테 넌 트에 있는 Fabrikam 회사 직원 들이 사용할 수 있게 됩니다.

입력 하는 설정과 응용 프로그램 프로 비전 단계는 [단일 조직 인증과](#orgauthsingle)유사 합니다.

**클라우드 다중 조직** 인증을 사용 하는 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Azure Active Directory, ASP.NET &amp; 와의 손쉬운 웹 앱 통합 ](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx) Active Directory 팀 블로그의 Visual Studio
- [AZURE AD를 사용 하 여 다중 테 넌 트 웹 응용 프로그램 개발](https://msdn.microsoft.com/library/windowsazure/dn151789.aspx) 자습서. Visual Studio 2013에 대 한 자습서는 아직 업데이트 되지 않았습니다. 자습서에서 수동으로 수행할 수 있는 작업 중 일부는 Visual Studio 2013에서 자동화 됩니다.
- [로그인 하려면 여러 조직 ASP.NET 앱을 사용 하 여 등록](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/)해야 합니다. 다중 조직 인증을 사용 하는 프로젝트를 만들 때 발생 하는 일반적인 문제를 해결 하는 방법을 설명 하는 Vittorio Bertocci의 블로그입니다.

<a id="orgauthonprem"></a>
### <a name="on-premises-organizational-authentication"></a>온-프레미스 조직 인증

![온-프레미스 조직 인증](creating-web-projects-in-visual-studio/_static/image26.png)

Windows Server Active Directory (AD)에 정의 된 사용자 계정에 대 한 인증을 사용 하도록 설정 하 고 Azure AD를 사용 하지 않으려는 경우이 옵션을 선택 합니다. 이 옵션을 사용 하 여 인트라넷 사이트 또는 인터넷 사이트를 만들 수 있습니다. 인터넷 사이트의 경우 ADFS (Active Directory Federation Services)를 사용 하 여 AD에 대 한 액세스를 제공 합니다. 자세한 내용은 [Visual Studio 2013에서 ASP.NET를 사용 하 여 온-프레미스 조직 인증 옵션 (ADFS) 사용](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)을 참조 하세요.

인트라넷 사이트의 경우이 옵션 대신 [Windows 인증](#winauth) 을 선택할 수 있습니다. Windows 인증 옵션의 경우 메타 데이터 문서 URL을 제공할 필요가 없습니다. 그러나 Windows 인증은 Active Directory 또는 디렉터리 데이터 쿼리를 통해 응용 프로그램 액세스를 제어 하는 기능을 제공 하지 않습니다.

#### <a name="on-premises-authority"></a>온-프레미스 인증 기관

메타 데이터 문서를 가리키는 URL을 입력 합니다. 메타 데이터 문서는 기관의 좌표를 포함 합니다. 응용 프로그램에서는 이러한 좌표를 사용 하 여 웹 로그온 흐름을 구동 합니다.

#### <a name="application-id-uri"></a>애플리케이션 ID URI

AD에서이 응용 프로그램을 식별 하는 데 사용할 수 있는 고유한 URI를 제공 하거나, Visual Studio에서이 응용 프로그램을 만들도록 하려면 비워 둡니다.

<a id="nextsteps"></a>
## <a name="next-steps"></a>다음 단계

이 문서에서는 Visual Studio 2013에서 새 ASP.NET 웹 프로젝트를 만들기 위한 몇 가지 기본적인 도움말을 제공 합니다. 웹 개발을 위한 Visual Studio 용 사용에 대 한 자세한 내용은을 참조 하십시오 [https://www.asp.net/visual-studio/](../../index.md) .
