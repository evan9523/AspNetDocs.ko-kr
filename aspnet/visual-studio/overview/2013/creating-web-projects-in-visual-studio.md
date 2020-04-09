---
uid: visual-studio/overview/2013/creating-web-projects-in-visual-studio
title: 비주얼 스튜디오 2013에서 ASP.NET 웹 프로젝트 만들기 | 마이크로 소프트 문서
author: tdykstra
description: 이 항목에서는 Visual Studio 2013에서 웹 프로젝트를 ASP.NET 만들기 위한 옵션에 대해 설명합니다 3 업데이트 3 웹 개발 c에 대 한 새로운 기능 중 일부입니다.
ms.author: riande
ms.date: 12/01/2014
ms.assetid: 61941e64-0c0d-4996-9270-cb8ccfd0cabc
msc.legacyurl: /visual-studio/overview/2013/creating-web-projects-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: fbb4cd7afa2506879d47bce980bf0164aad40c2c
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675684"
---
# <a name="creating-aspnet-web-projects-in-visual-studio-2013"></a>Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기

로 [톰 다이크스트라](https://github.com/tdykstra)

> 이 항목에서는 Visual Studio 2013에서 업데이트 3을 통해 ASP.NET 웹 프로젝트를 만드는 옵션에 대해 설명합니다.
> 
> 다음은 이전 버전의 Visual Studio와 비교하여 웹 개발을 위한 몇 가지 새로운 기능입니다.
> 
> - 여러 ASP.NET 프레임워크(웹 양식, MVC 및 웹 [API)에 대한 지원을](#add) 제공하는 프로젝트를 만들기 위한 간단한 UI입니다.
> - [ASP.NET ID는](#indauth)모든 ASP.NET 프레임워크에서 동일하게 작동하고 IIS 이외의 웹 호스팅 소프트웨어와 함께 작동하는 새로운 ASP.NET 멤버십 시스템입니다.
> - [부트 스트랩의](#bootstrap) 사용은 응답 디자인과 테마 기능을 제공합니다.
> - [자동 테스트 프로젝트 만들기](#testproj) 및 [인트라넷 사이트 템플릿과](#winauth)같이 MVC에서만 제공되던 웹 양식의 새로운 기능.
> 
> Azure 클라우드 서비스 또는 Azure 모바일 서비스에 대한 웹 프로젝트를 만드는 방법에 대한 자세한 내용은 [Azure 클라우드 서비스 시작 및 ASP.NET](https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-get-started/) 및 Azure Mobile Services [.NET 백엔드를 사용하여 리더보드 앱 만들기를](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)참조하십시오.

<a id="prerequisites"></a>
## <a name="prerequisites"></a>사전 요구 사항

이 문서는 [업데이트 3이](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409) 설치된 [Visual Studio 2013에](https://go.microsoft.com/fwlink/?LinkId=306566) 적용됩니다.

<a id="wap"></a>
## <a name="web-application-projects-versus-web-site-projects"></a>웹 응용 프로그램 프로젝트 와 웹 사이트 프로젝트 비교

ASP.NET 웹 *응용 프로그램* 프로젝트와 웹 사이트 프로젝트의 두 가지 종류의 웹 프로젝트 중에서 선택할 수 *있습니다.* 새로운 개발을 위해 웹 응용 프로그램 프로젝트를 권장하며 이 문서는 웹 응용 프로그램 프로젝트에만 적용됩니다. 자세한 내용은 MSDN 사이트의 [Visual Studio의 웹 응용 프로그램 프로젝트 와 웹 사이트 프로젝트를](https://msdn.microsoft.com/library/dd547590(v=vs.120).aspx) 참조하십시오.

<a id="overview"></a>
## <a name="overview-of-web-application-project-creation"></a>웹 응용 프로그램 프로젝트 생성 개요

다음 단계에서는 웹 프로젝트를 만드는 방법을 보여 주며,

1. **시작** 페이지 또는 **파일** 메뉴에서 **새 프로젝트를** 클릭합니다.
2. 새 **프로젝트** 대화 상자에서 왼쪽 창에서 **웹을** 클릭하고 중간 창에서 **웹 응용 프로그램을 ASP.NET.**

    ![새 프로젝트 대화 상자](creating-web-projects-in-visual-studio/_static/image1.png)

    왼쪽 창에서 **클라우드를** 선택하여 [Azure 클라우드 서비스,](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)Azure [모바일 서비스](https://msdn.microsoft.com/library/windows/apps/dn629482.aspx)또는 [Azure WebJob](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-webjobs)을 만들 수 있습니다. 이 항목에서는 이러한 템플릿을 다루지 않습니다.
3. 오른쪽 창에서 응용 프로그램에 대한 상태 및 사용 모니터링을 원하는 경우 **프로젝트에 응용 프로그램 인사이트 추가** 확인란을 클릭합니다. 자세한 내용은 [웹 애플리케이션의 성능 모니터링](https://azure.microsoft.com/documentation/articles/app-insights-web-monitor-performance/)을 참조하세요.
4. 프로젝트 **이름,** **위치**및 기타 옵션을 지정한 다음 **확인**을 클릭합니다.

    **새 ASP.NET 프로젝트** 대화 상자가 표시됩니다.

    ![새 프로젝트 대화 상자](creating-web-projects-in-visual-studio/_static/image2.png)
5. 템플릿을 클릭합니다.

    ![템플릿 선택](creating-web-projects-in-visual-studio/_static/image3.png)
6. 템플릿에 포함되지 않은 추가 프레임워크에 대한 지원을 추가하려면 해당 확인란을 클릭합니다. 표시된 예제에서는 웹 양식 프로젝트에 MVC 및/또는 웹 API를 추가할 수 있습니다.

    ![프레임워크 추가](creating-web-projects-in-visual-studio/_static/image4.png)
7. <a id="testproj"></a>단위 테스트 프로젝트를 추가하려면 단위 **테스트 추가를**클릭합니다.

    ![단위 테스트 추가](creating-web-projects-in-visual-studio/_static/image5.png)
8. 기본적으로 템플릿에서 제공하는 것과 다른 인증 방법을 원하는 경우 **인증 변경을**클릭합니다.

    ![인증 버튼 구성](creating-web-projects-in-visual-studio/_static/image6.png)

    ![인증 대화 상자 구성](creating-web-projects-in-visual-studio/_static/image7.png)

<a id="azurenewproj"></a>
### <a name="create-a-web-app-or-virtual-machine-in-azure"></a>Azure에서 웹 앱 또는 가상 컴퓨터 만들기

Visual Studio에는 웹 응용 프로그램을 호스팅하기 위해 Azure 서비스를 쉽게 사용할 수 있는 기능이 포함되어 있습니다. 예를 들어 Visual Studio IDE에서 다음 을 모두 수행할 수 있습니다.

- 인터넷을 통해 응용 프로그램을 사용할 수 있도록 하는 웹 앱 또는 가상 컴퓨터를 만들고 관리합니다.
- 응용 프로그램이 클라우드에서 실행될 때 만든 로그를 봅니다.
- 응용 프로그램이 클라우드에서 실행되는 동안 디버그 모드에서 원격으로 실행됩니다.
- SQL 데이터베이스와 같은 다른 Azure 서비스를 보고 관리합니다.

웹 앱과 같은 기본 서비스를 무료로 포함하는 [Azure 계정을 만들](https://www.windowsazure.com/pricing/free-trial/) 수 있으며 MSDN 구독자인 경우 추가 Azure 서비스에 대한 월별 크레딧을 제공하는 혜택을 [활성화할](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/) 수 있습니다. 

기본적으로 **새 ASP.NET 프로젝트** 대화 상자를 사용하면 새 웹 프로젝트에 대한 웹 앱 또는 가상 컴퓨터를 만들 수 있습니다. 새 웹 앱 또는 가상 컴퓨터를 만들지 않으려면 **클라우드에서 호스트를** 지우세요.

![원격 리소스 만들기](creating-web-projects-in-visual-studio/_static/image8.png)

확인란 캡션은 **클라우드의 호스트** 또는 **원격 리소스 만들기일**수 있으며 두 경우 모두 효과가 동일합니다. 확인란을 선택한 상태로 두면 Visual Studio는 기본적으로 Azure 앱 서비스에서 웹 앱을 만듭니다. 원하는 경우 드롭다운 상자를 사용하여 가상 **컴퓨터로** 변경할 수 있습니다. 아직 Azure에 로그인하지 않은 경우 Azure 자격 증명에 대한 메시지가 표시됩니다. 로그인한 후 대화 상자를 사용하면 Visual Studio에서 프로젝트에 대해 만들 리소스를 구성할 수 있습니다. 다음 그림에서는 웹 앱에 대한 대화 상자를 보여 주며, 가상 컴퓨터를 만들도록 선택하면 다른 옵션이 나타납니다.

![Azure 앱 설정 구성](creating-web-projects-in-visual-studio/_static/image9.png)

Azure 리소스를 만드는 데 이 프로세스를 사용하는 방법에 대한 자세한 내용은 [Azure 및 ASP.NET 시작](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) 가져오기 및 Visual [Studio를 사용하여 웹 사이트에 대한 가상 시스템 만들기를](https://azure.microsoft.com/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/)참조하십시오.

이 문서의 나머지 부분에서는 사용 가능한 템플릿 및 해당 옵션에 대한 자세한 정보를 제공합니다. 이 문서에서는 또한 부트 스트랩, 템플릿에 사용 되는 레이아웃 및 테마 프레임 워크를 소개 합니다.

<a id="vs2013"></a>
## <a name="visual-studio-2013-web-project-templates"></a>비주얼 스튜디오 2013 웹 프로젝트 템플릿

Visual Studio는 템플릿을 사용하여 웹 프로젝트를 만듭니다. 프로젝트 템플릿은 새 프로젝트에서 파일 및 폴더를 만들고 NuGet 패키지를 설치하고 기본적인 작업 응용 프로그램에 대한 샘플 코드를 제공할 수 있습니다. 템플릿은 최신 웹 표준을 구현하며 ASP.NET 기술을 사용하는 방법에 대한 모범 사례를 보여주고 사용자 고유의 응용 프로그램을 만드는 데 사용할 수 있도록 하기 위한 것입니다.

Visual Studio 2013은 .NET 4.5 이상 버전의 .NET 프레임워크를 대상으로 하는 프로젝트에 대한 웹 프로젝트 템플릿에 대해 다음과 같은 옵션을 제공합니다.

- [빈 템플릿](#empty)
- [웹 양식 템플릿](#wf)
- [MVC 템플릿](#mvc)
- [웹 API 템플릿](#webapi)
- [단일 페이지 응용 프로그램 템플릿](#spa)
- [Azure 모바일 서비스 템플릿](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)
- [비주얼 스튜디오 2012 템플릿](#vs2012)

[Facebook 템플릿을](#facebook)제공하는 Visual Studio 확장을 설치할 수도 있습니다.

.NET 4를 대상으로 하는 프로젝트를 만드는 방법에 대한 자세한 내용은 이 항목의 후반부 [Visual Studio 2012 템플릿을](#vs2012) 참조하십시오.

모바일 클라이언트를 위한 ASP.NET 응용 프로그램을 만드는 방법에 대한 자세한 내용은 ASP.NET 모바일 [지원을](../../../mobile/overview.md)참조하십시오.

<a id="empty"></a>
### <a name="empty-template"></a>빈 템플릿

빈 템플릿은 프로젝트 ASP.NET 파일 *(.csproj* 또는 .* vbproj)* 및 *Web.config* 파일. 폴더 추가 및 핵심 참조: 레이블 아래에 있는 확인란을 사용하여 웹 양식, MVC 및/또는 웹 **API에 대한** 지원을 추가할 수 있습니다.

빈 템플릿의 경우 인증 옵션을 사용할 수 없습니다. 인증 기능은 샘플 응용 프로그램에서 구현되며 Empty 템플릿은 샘플 응용 프로그램을 만들지 않습니다.

<a id="wf"></a>
### <a name="web-forms-template"></a>웹 양식 템플릿

Web Forms 프레임워크는 UI 및 데이터 액세스 기능이 풍부한 웹 사이트를 신속하게 빌드할 수 있는 다음 기능을 제공합니다.

- 비주얼 스튜디오의 WYSIWYG 디자이너.
- HTML을 렌더링하고 속성 및 스타일을 설정하여 사용자 지정할 수 있는 서버 컨트롤입니다.
- 데이터 액세스 및 데이터 표시를 위한 다양한 컨트롤구색입니다.
- WPF와 같은 클라이언트 응용 프로그램을 프로그래밍하는 것처럼 프로그래밍할 수 있는 이벤트를 노출하는 이벤트 모델입니다.
- HTTP 요청 간의 상태(데이터) 자동 보존.

일반적으로 Web Forms 응용 프로그램을 만들려면 ASP.NET MVC 프레임워크를 사용하여 동일한 응용 프로그램을 만드는 것보다 프로그래밍 노력이 덜 필요합니다. 그러나 웹 양식은 신속한 응용 프로그램 개발을 위한 것이 아닙니다. Web Forms 위에 구축된 복잡한 상용 응용 프로그램 및 프레임워크가 많이 있습니다.

웹 폼 페이지와 페이지의 컨트롤은 브라우저로 전송되는 많은 태그를 자동으로 생성하므로 ASP.NET MVC가 제공하는 HTML에 대한 세분화된 컨트롤이 없습니다. 페이지 및 컨트롤을 구성하기 위한 선언적 모델은 작성해야 하는 코드의 양을 최소화하지만 HTML 및 HTTP의 동작 중 일부를 숨깁니다. 예를 들어 컨트롤에서 생성할 수 있는 태그를 정확히 지정할 수 있는 것은 아닙니다.

Web Forms 프레임워크는 [테스트 기반 개발,](http://en.wikipedia.org/wiki/Test-driven_development) [문제 분리,](http://en.wikipedia.org/wiki/Separation_of_concerns) [제어 반전](http://en.wikipedia.org/wiki/Inversion_of_control)및 [종속성 주입과](http://en.wikipedia.org/wiki/Dependency_injection)같은 패턴 기반 개발 사례에 ASP.NET MVC처럼 쉽게 빌려주지 않습니다. 그런 식으로 팩터링된 코드를 작성하려면 다음을 수행할 수 있습니다. ASP.NET MVC 프레임워크에서와 마찬가지로 자동이 아닙니다. [ASP.NET Web Forms MVP](http://webformsmvp.com/) 프로젝트는 Web Forms가 제공하도록 구축된 신속한 개발을 유지하면서 우려 사항과 테스트 가능성을 쉽게 분리하는 방법을 보여 준다. Microsoft SharePoint는 웹 양식 MVP를 기반으로 합니다.

Web Forms 템플릿은 [부트스트랩을](#bootstrap) 사용하여 응답성이 있는 디자인과 테마 기능을 제공하는 샘플 Web Forms 응용 프로그램을 만듭니다. 다음 그림은 홈 페이지를 보여 주며 있습니다.

![웹 양식 템플릿 앱 홈 페이지](creating-web-projects-in-visual-studio/_static/image10.png)

웹 양식에 대한 자세한 내용은 [ASP.NET 웹 양식을](https://asp.net/web-forms)참조하십시오. 웹 양식 템플릿이 수행하는 작업을 보려면 [Visual Studio 2013을 사용하여 기본 웹 폼 응용 프로그램 빌드를](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx)참조하십시오.

<a id="mvc"></a>
### <a name="mvc-template"></a>MVC 템플릿

ASP.NET MVC는 [테스트 기반 개발,](http://en.wikipedia.org/wiki/Test-driven_development) [우려 분리,](http://en.wikipedia.org/wiki/Separation_of_concerns) [제어 반전](http://en.wikipedia.org/wiki/Inversion_of_control)및 [종속성 주입과](http://en.wikipedia.org/wiki/Dependency_injection)같은 패턴 기반 개발 관행을 용이하게 하도록 설계되었습니다. 프레임워크는 웹 응용 프로그램의 비즈니스 논리 계층을 프레젠테이션 계층과 분리하는 것을 권장합니다. MVC를 ASP.NET 응용 프로그램을 모델(M), 뷰(V) 및 컨트롤러(C)로 분할하면 대규모 응용 프로그램에서 복잡성을 보다 쉽게 관리할 수 있습니다.

ASP.NET MVC를 사용하면 웹 양식보다 HTML 및 HTTP로 더 직접적으로 작업할 수 있습니다. 예를 들어 Web Forms는 HTTP 요청 간에 상태를 자동으로 보존할 수 있지만 MVC에서 명시적으로 코딩해야 합니다. MVC 모델의 장점은 응용 프로그램이 수행하는 내용과 웹 환경에서 작동 방식을 완벽하게 제어할 수 있다는 것입니다. 단점은 더 많은 코드를 작성해야 한다는 것입니다.

MVC는 확장 가능하도록 설계되어 전력 개발자가 응용 프로그램 요구에 맞게 프레임워크를 사용자 지정할 수 있습니다. 또한 ASP.NET MVC 소스 코드는 OSI 라이선스에 따라 사용할 수 있습니다.

MVC 템플릿은 [부트스트랩을](#bootstrap) 사용하여 응답성이 있는 디자인과 테마 기능을 제공하는 샘플 MVC 5 응용 프로그램을 만듭니다. 다음 그림은 홈 페이지를 보여 주며 있습니다.

![MVC 샘플 응용 프로그램](creating-web-projects-in-visual-studio/_static/image11.png)

MVC에 대한 자세한 내용은 [ASP.NET MVC](https://asp.net/mvc)를 참조하십시오. MVC 4 템플릿을 선택하는 방법에 대한 자세한 내용은 이 문서의 [후반부Visual Studio 2012 템플릿을](#vs2012) 참조하십시오.

<a id="webapi"></a>
### <a name="web-api-template"></a>웹 API 템플릿

웹 API 템플릿은 MVC를 기반으로 하는 API 도움말 페이지를 포함하여 웹 API를 기반으로 하는 샘플 웹 서비스를 만듭니다.

ASP.NET Web API는 브라우저 및 모바일 디바이스를 비롯한 광범위한 클라이언트에 연결하는 HTTP 서비스를 쉽게 빌드할 수 있게 해 주는 프레임워크입니다. ASP.NET 웹 API는 .NET 프레임워크에서 RESTful 서비스를 구축하기 위한 이상적인 플랫폼입니다.

웹 API 템플릿은 샘플 웹 서비스를 만듭니다. 다음 그림에서는 도움말 도움말 페이지를 보여 줍니다.

![웹 API 도움말 페이지](creating-web-projects-in-visual-studio/_static/image12.png)

![GET API에 대한 웹 API 도움말 페이지](creating-web-projects-in-visual-studio/_static/image13.png)

웹 API에 대한 자세한 내용은 [ASP.NET 웹 API를](https://asp.net/web-api)참조하십시오.

<a id="spa"></a>
### <a name="single-page-application-template"></a>단일 페이지 응용 프로그램 템플릿

단일 페이지 응용 프로그램(SPA) 템플릿은 클라이언트에서 자바스크립트, HTML 5 및 [KnockoutJS를](http://knockoutjs.com/) 사용하는 샘플 응용 프로그램을 만들고 서버의 웹 API를 ASP.NET.

SPA 템플릿에 대한 유일한 인증 옵션은 [개별 사용자 계정입니다.](#indauth)

다음 그림에서는 SPA 템플릿이 빌드하는 샘플 응용 프로그램의 초기 상태를 보여 주며 있습니다.

![SPA 샘플 응용 프로그램](creating-web-projects-in-visual-studio/_static/image14.png)

SPA 템플릿을 사용하여 응용 프로그램을 만드는 방법에 대한 자세한 내용은 [웹 API - 외부 인증 서비스](../../../web-api/overview/security/external-authentication-services.md)를 참조하십시오.

단일 페이지 응용 프로그램 ASP.NET 및 KnockoutJS 이외의 JavaScript 프레임워크를 사용하는 추가 SPA 템플릿에 대한 자세한 내용은 다음 리소스를 참조하십시오.

- [ASP.NET 단일 페이지 응용 프로그램입니다.](../../../single-page-application/index.md)
- [VS2013 RC용 SPA 템플릿의 보안 기능 이해](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)
- [단일 페이지 응용 프로그램: ASP.NET 함께 최신의 반응형 웹 앱 빌드](https://msdn.microsoft.com/magazine/dn463786.aspx)

<a id="facebook"></a>
### <a name="facebook-template"></a>페이스 북 템플릿

[Facebook 템플릿을 제공하는 Visual Studio 확장을 설치할](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409)수 있습니다. 이 템플릿은 Facebook 웹 사이트 내에서 실행되도록 설계된 샘플 응용 프로그램을 만듭니다. ASP.NET MVC를 기반으로 하며 실시간 업데이트 기능에 웹 API를 사용합니다.

페이스 북 응용 프로그램은 페이스 북 사이트 내에서 실행하고 페이스 북의 인증에 의존하기 때문에 페이스 북 템플릿에 사용할 수있는 인증 옵션이 없습니다.

ASP.NET 페이스 북 응용 프로그램에 대한 자세한 내용은 [MVC 페이스 북 API 업데이트를](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx)참조하십시오.

<a id="vs2012"></a>
### <a name="visual-studio-2012-templates"></a>비주얼 스튜디오 2012 템플릿

Visual Studio 2013 웹 프로젝트 만들기 대화 상자는 Visual Studio 2012에서 사용할 수 있는 일부 템플릿에 대한 액세스를 제공하지 않습니다. 이러한 템플릿 중 하나를 사용하려는 경우 Visual Studio 새 프로젝트 대화 상자의 왼쪽 창에서 Visual Studio 2012 노드를 클릭할 수 있습니다.

![비주얼 스튜디오 2012 템플릿](creating-web-projects-in-visual-studio/_static/image15.png)

**Visual Studio 2012** 노드를 사용하면 Visual Studio 2013의 기본 템플릿 목록에서 액세스할 수 없는 다음 웹 템플릿을 선택할 수 있습니다.

- ASP.NET MVC 4 웹 애플리케이션
- ASP.NET 동적 데이터 엔터티 웹 애플리케이션
- ASP.NET AJAX 서버 제어
- ASP.NET AJAX 서버 제어 익스텐더
- ASP.NET 서버 제어

<a id="bootstrap"></a>
## <a name="bootstrap-in-the-visual-studio-2013-web-project-templates"></a>비주얼 스튜디오 2013 웹 프로젝트 템플릿의 부트 스트랩

Visual Studio 2013 프로젝트 템플릿은 트위터에서 만든 레이아웃 및 테마 프레임워크인 [부트스트랩을](http://getbootstrap.com/)사용합니다. 부트스트랩은 CSS3를 사용하여 반응형 디자인을 제공하므로 레이아웃이 다양한 브라우저 창 크기에 동적으로 적응할 수 있습니다. 예를 들어 넓은 브라우저 창에서 Web Forms 템플릿으로 만든 홈 페이지는 다음과 같습니다.

![웹 양식 템플릿 앱 홈 페이지](creating-web-projects-in-visual-studio/_static/image16.png)

창을 좁게 만들고 가로로 배열된 열을 세로 배열로 이동합니다.

![부트 스트랩 수직 컬럼 배열](creating-web-projects-in-visual-studio/_static/image17.png)

창을 조금 더 좁히면 가로 상단 메뉴가 클릭하여 세로 방향 메뉴로 확장할 수 있는 아이콘으로 바뀝니다.

![부트스트랩 메뉴 아이콘](creating-web-projects-in-visual-studio/_static/image18.png)

![부트스트랩 수직 메뉴](creating-web-projects-in-visual-studio/_static/image19.png)

또한 부트스트랩의 테마 기능을 사용하여 응용 프로그램의 모양과 느낌을 쉽게 변경할 수 있습니다. 예를 들어 다음 단계를 수행하여 테마를 변경할 수 있습니다.

1. 브라우저에서 로 이동하여 [http://Bootswatch.com](http://Bootswatch.com)테마를 선택한 다음 **다운로드를**클릭합니다. (이것은 기본적으로 *bootstrap.min.css를* 다운로드합니다. CSS 코드를 검사하려면 minified 버전 대신 *bootstrap.css를* 가져옵니다.)
2. 다운로드한 CSS 파일의 내용을 복사합니다.
3. Visual Studio에서 *콘텐츠* 폴더에 *부트스트랩-theme.css라는* 새 **스타일 시트** 파일을 만들고 다운로드한 CSS 코드를 붙여넣습니다.
4. *앱\_시작/Bundle.config를* 열고 *bootstrap.css를* *부트스트랩-theme.css로*변경합니다.

프로젝트를 다시 실행하면 응용 프로그램이 새 모양으로 보입니다. 다음 그림에서는 아멜리아 테마의 효과를 보여 주었습니다.

![부트스트랩 아멜리아 테마](creating-web-projects-in-visual-studio/_static/image20.png)

많은 부트 스트랩 테마를 사용할 수 있습니다., 무료 및 프리미엄 버전. 부트스트랩은 [드롭다운,](http://twitter.github.io/bootstrap/components.html#dropdowns) [단추 그룹](http://twitter.github.io/bootstrap/components.html#buttonGroups)및 [아이콘과](http://twitter.github.io/bootstrap/base-css.html#images)같은 다양한 UI 구성 요소를 제공합니다. 부트스트랩에 대한 자세한 내용은 [부트스트랩 사이트를](http://twitter.github.io/bootstrap/)참조하십시오.

Visual Studio에서 웹 양식 디자이너를 사용하는 경우 디자이너는 CSS3를 지원하지 않으므로 Bootstrap 테마 또는 반응형 레이아웃 변경의 모든 효과를 정확하게 표시하지는 않습니다. 그러나 브라우저에서 볼 때 웹 양식 페이지가 올바르게 표시됩니다.

<a id="add"></a>
## <a name="adding-support-for-additional-frameworks"></a>추가 프레임워크에 대한 지원 추가

템플릿을 선택하면 템플릿에서 사용하는 프레임워크에 대한 확인란이 자동으로 선택됩니다. 예를 들어 **웹 양식** 템플릿을 선택하면 **웹 양식** 확인란이 선택되어 지울 수 없습니다.

![템플릿 선택](creating-web-projects-in-visual-studio/_static/image21.png)

![프레임워크 추가](creating-web-projects-in-visual-studio/_static/image22.png)

프로젝트를 만들 때 해당 프레임워크에 대한 지원을 추가하기 위해 템플릿에 포함되지 않은 프레임워크의 확인란을 선택할 수 있습니다. 예를 들어 MVC 템플릿을 선택한 경우 Web Forms *.aspx* 페이지를 사용하도록 설정하려면 **웹 양식** 확인란을 선택합니다. 또는 웹 양식 템플릿을 사용할 때 **MVC를** 사용하려면 MVC 확인란을 클릭합니다. 프레임워크를 추가하면 디자인 타임과 런타임 지원을 사용할 수 있습니다. 예를 들어 웹 폼 프로젝트에 MVC 지원을 추가하면 컨트롤러 및 뷰를 스캐폴드할 수 있습니다.

프로젝트에서 웹 양식및 MVC를 결합하고 웹 Forms에서 [친숙한 URL을](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx) 사용하도록 설정하는 경우 한 URL에 여러 개의 가능한 대상이 있는 예기치 않은 라우팅 문제가 있을 수 있습니다. 먼저 정의된 경로가 우선합니다. 예를 `Home` 들어 컨트롤러와 *Home.aspx* 페이지가 있는 `http://contoso.com/home` 경우 *RouteConfig.cs* `Home` `MapRoute` `EnableFriendlyUrls` `EnableFriendlyUrls` `MapRoute` 메서드를 호출하기 전에 메서드를 호출하는 경우 URL이 *Home.aspx로* 이동하거나 동일한 URL이 컨트롤러의 기본 보기로 이동합니다.

프레임워크를 추가해도 샘플 응용 프로그램 기능이 추가되지 않습니다. 예를 들어 MVC 템플릿을 선택한 경우 웹 양식 지원을 추가하는 경우 *Default.aspx* 홈 페이지 파일이 만들어지지 않습니다. 프레임워크를 지원하는 데 필요한 폴더, 파일 및 참조만 추가됩니다. 이러한 이유로 프레임워크를 추가해도 템플릿에서 만든 샘플 응용 프로그램의 코드에 의해 구현되는 인증 옵션이 변경되지 않습니다. 예를 들어 빈 템플릿을 선택하고 웹 양식 또는 MVC 지원을 추가하는 경우 **인증 구성** 단추는 여전히 비활성화됩니다.

다음 섹션에서는 각 확인란의 효과를 간략하게 설명합니다.

### <a name="add-web-forms-support"></a>웹 양식 지원 추가

빈 *앱\_데이터* 및 *모델* 폴더와 *Global.asax* 파일을 만듭니다. 빈 템플릿 이외의 모든 템플릿에서 이미 만들어지므로 웹 양식 확인란을 선택하면 다른 템플릿에 차이가 없습니다.

웹 양식 템플릿은 기본적으로 친숙한 URL을 사용할 수 있지만 웹 양식 확인란을 선택하여 다른 템플릿에 웹 양식 지원을 추가하면 친숙한 URL이 자동으로 활성화되지 않습니다.

### <a name="add-mvc-support"></a>MVC 지원 추가

MVC, Razor 및 WebPages NuGet 패키지를 설치하고, 빈 *앱\_데이터,* *컨트롤러,* *모델*및 *보기* 폴더를 만들고, *RouteConfig.cs* 파일로 *앱\_시작* 폴더를 *만들고, Global.asax* 파일을 만듭니다.

### <a name="add-web-api-support"></a>웹 API 지원 추가

WebApi 및 Newtonsoft.Json NuGet 패키지를 설치하고, 빈 *앱\_데이터,* 컨트롤러 및 *모델* *폴더를*만들고, *WebApiConfig.cs* 파일로 *앱\_시작* 폴더를 *만들고, Global.asax* 파일을 만듭니다.

<a id="auth"></a>
## <a name="authentication-methods"></a>인증 방법

Visual Studio 2013은 웹 양식, MVC 및 웹 API 템플릿에 대한 몇 가지 인증 옵션을 제공합니다.

- [인증 없음](#noauth)
- [개별 사용자 계정(ASP.NET](#indauth) ID, 이전 ASP.NET 멤버십)
- [조직 계정(Windows](#orgauth) 서버 활성 디렉터리 또는 Azure Active Directory)
- [윈도우](#winauth) 인증(인트라넷)

![인증 대화 상자 구성](creating-web-projects-in-visual-studio/_static/image23.png)

<a id="noauth"></a>

### <a name="no-authentication"></a>인증 없음

**인증 없음을**선택하면 샘플 응용 프로그램에 로그인할 웹 페이지가 없고, 로그인한 사람을 나타내는 UI가 없으며, 멤버 자격 데이터베이스에 대한 엔터티 클래스가 없으며 멤버 자격 데이터베이스에 대한 연결 문자열이 없습니다.

<a id="indauth"></a>
### <a name="individual-user-accounts"></a>개별 사용자 계정

**개별 사용자 계정을**선택하면 샘플 응용 프로그램이 사용자 인증에 ASP.NET ID(이전의 ASP.NET 멤버 자격)를 사용하도록 구성됩니다. ASP.NET ID를 사용하면 사용자가 사이트에 사용자 이름과 암호를 만들거나 Facebook, Google, Microsoft 계정 또는 트위터와 같은 소셜 공급자와 로그인하여 계정을 등록할 수 있습니다. ASP.NET ID의 사용자 프로필에 대한 기본 데이터 저장소는 프로덕션 사이트에 대해 SQL Server 또는 Azure SQL Database에 배포할 수 있는 SQL Server LocalDB 데이터베이스입니다.

Visual Studio 2013에서 이러한 기능은 Visual Studio 2012와 동일하지만 ASP.NET 멤버 자격 시스템의 기본 코드가 다시 작성되었습니다. 새 코드 베이스의 장점은 다음과 같습니다.

- 새 멤버십 시스템은 ASP.NET 양식 인증 모듈이 아닌 [OWIN을](http://owin.org/) 기반으로 합니다. 즉, IIS에서 웹 양식 또는 MVC를 사용하든 웹 API 또는 SignalR을 자체 호스팅하든 동일한 인증 메커니즘을 사용할 수 있습니다.
- 새 멤버 자격 데이터베이스는 엔터티 프레임워크 코드 우선에 의해 관리되며 모든 테이블은 수정할 수 있는 엔터티 클래스로 표시됩니다. 즉, 자신의 필요에 맞게 데이터베이스 스키마 및 프로필 관련 웹 UI를 쉽게 사용자 지정할 수 있으며 Code First 마이그레이션을 사용하여 업데이트를 쉽게 배포할 수 있습니다.

새 멤버 자격 시스템은 새 템플릿에서 자동으로 구현되며 .NET 4.5 이상을 대상으로 하는 모든 프로젝트에서 수동으로 구현할 수 있습니다.

ASP.NET ID는 주로 외부 고객을 위한 인터넷 웹 사이트를 만드는 경우에 적합합니다. 조직에서 Active Directory 또는 Office 365를 사용하고 직원 및 비즈니스 파트너에 대해 단일 사인온을 활성화하는 프로젝트를 만들려는 경우 **조직 계정** 옵션이 더 나은 선택일 수 있습니다.

개별 사용자 계정 옵션에 대한 자세한 내용은 다음 리소스를 참조하십시오.

- [www.asp.net/identity](../../../identity/index.md). ASP.NET 웹 사이트의 ASP.NET ID에 대한 설명서입니다.
- [페이스 북과 구글 OAuth2 및 오픈 ID 로그인과 ASP.NET MVC 5 응용 프로그램을 만듭니다.](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 또한 사용자 프로필 데이터를 사용자 지정하는 방법을 보여줍니다.
- [웹 API - 외부 인증 서비스](../../../web-api/overview/security/external-authentication-services.md)
- [Visual Studio 2013에서 ASP.NET 응용 프로그램에 외부 로그인 추가](https://blogs.msdn.com/b/webdev/archive/2013/06/27/adding-external-logins-to-your-asp-net-application-in-visual-studio-2013.aspx)

<a id="orgauth"></a>
### <a name="organizational-accounts"></a>조직 계정

**조직 계정을**선택하면 샘플 응용 프로그램은 Azure Active Directory(Office 365포함) 또는 Windows 서버 활성 디렉터리에서 사용자 계정을 기반으로 인증에 WIF(Windows ID Foundation)를 사용하도록 구성됩니다. 자세한 내용은 이 항목의 다음 부분에서 [조직 계정 인증 옵션을](#orgauthoptions) 참조하세요.

<a id="winauth"></a>
### <a name="windows-authentication"></a>Windows 인증

**Windows 인증을**선택하면 인증에 Windows 인증 IIS 모듈을 사용하도록 샘플 응용 프로그램이 구성됩니다. 응용 프로그램에는 Windows에 로그인하지만 사용자 등록 또는 로그인 UI는 포함되지 않는 Active 디렉터리 또는 로컬 컴퓨터 계정의 도메인 및 사용자 ID가 표시됩니다. 이 옵션은 인트라넷 웹 사이트를 위한 것입니다.

또는 [조직 계정에서 온-프레미스 옵션을](#orgauthonprem)선택하여 AD 인증을 사용하는 인트라넷 사이트를 만들 수 있습니다. 온-프레미스 옵션은 Windows 인증 모듈 대신 WIF(Windows ID Foundation)를 사용합니다. 온-프레미스 옵션을 설정하려면 몇 가지 추가 단계가 필요하지만 WIF는 Windows 인증 모듈에서 사용할 수 없는 기능을 사용할 수 있도록 합니다. 예를 들어 WIF를 사용하면 Active Directory 및 쿼리 디렉터리 데이터에서 응용 프로그램 액세스를 구성할 수 있습니다.

<a id="orgauthoptions"></a>
## <a name="organizational-account-authentication-options"></a>조직 계정 인증 옵션

**인증 구성** 대화 상자는 Azure Active Directory(Office 365포함) 또는 Windows 서버 활성 디렉터리(AD) 계정 인증에 대한 몇 가지 옵션을 제공합니다.

- [클라우드 - 단일 조직(Azure](#orgauthsingle) AD와의 디렉터리 통합을 사용하는 Azure AD 또는 AD)
- [클라우드 - 다중 조직(Azure](#orgauthmulti) AD와의 디렉터리 통합을 사용하는 Azure AD 또는 AD)
- [온-프레미스(AD)](#orgauthonprem)

Azure AD 옵션 중 하나를 시도하지만 아직 계정이 없는 경우 [여기를 클릭하여 Azure AD 계정에 등록합니다.](https://go.microsoft.com/fwlink/?LinkId=309942)

> [!NOTE]
> Azure AD 옵션 중 하나를 선택하는 경우 프로젝트에 데이터베이스가 필요하며 Azure AD 테넌트의 전역 관리자 계정에 로그인해야 합니다. Azure AD 테넌트에 대한 관리 admin@contoso.onmicrosoft.com권한이 있는 조직 계정(예:)의 이름과 암호를 입력합니다.
> 
> **로그인 대화 상자에 Microsoft contoso@hotmail.com계정(예:)에 대한 자격 증명을 입력하지 마십시오.**

<a id="orgauthsingle"></a>
### <a name="cloud---single-organization-authentication"></a>클라우드 - 단일 조직 인증

![단일 조직 인증](creating-web-projects-in-visual-studio/_static/image24.png)

하나의 Azure AD [테넌트에](https://technet.microsoft.com/library/jj573650.aspx)정의된 사용자 계정에 대한 인증을 사용하려면 이 옵션을 선택합니다. 예를 들어, 이 사이트는 contoso.com 있으며 contoso.onmicrosoft.com 테넌트에 있는 Contoso Company의 직원이 사용할 수 있습니다. 다른 테넌트의 사용자가 응용 프로그램에 액세스할 수 있도록 Azure AD를 구성할 수 없습니다.

#### <a name="domain"></a>도메인

응용 `contoso.onmicrosoft.com`프로그램을 설정하려는 Azure AD 도메인을 입력합니다. 과 같은 [사용자 지정 도메인이](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/) `contoso.com` 있는 경우 여기에 입력할 수 있습니다. `contoso.onmicrosoft.com`

#### <a name="access-level"></a>액세스 수준

응용 프로그램이 그래프 API를 사용하여 디렉터리 정보를 쿼리하거나 업데이트해야 하는 경우 **Single Sign-On, 읽기 디렉터리 데이터** 또는 **단일 사인온, 읽기 및 쓰기 디렉터리 데이터를**선택합니다. 그렇지 않으면 **단일 사인온**을 선택합니다. 자세한 내용은 [응용 프로그램 액세스 수준](https://msdn.microsoft.com/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels) 및 그래프 [API를 사용하여 Azure AD를 쿼리합니다.](https://msdn.microsoft.com/library/windowsazure/dn151791.aspx)

#### <a name="application-id-uri"></a>응용 프로그램 ID URI

기본적으로 템플릿은 Azure AD 도메인에 프로젝트 이름을 추가하여 응용 프로그램 ID URI를 만듭니다. 예를 들어 프로젝트 이름이 `Example` 도메인인 경우 `contoso.onmicrosoft.com`응용 프로그램 ID `https://contoso.onmicrosoft.com/Example`URI가 됩니다. 응용 프로그램 ID URI를 수동으로 지정하려면 **추가 옵션** 섹션을 확장하고 텍스트 상자에 응용 프로그램 ID URI를 입력합니다. 응용 프로그램 ID URI는 에서 시작해야 `https://`합니다.

기본적으로 Azure AD에서 이미 프로비전된 응용 프로그램에 Visual Studio가 프로젝트에 사용하는 응용 프로그램 ID URI와 동일한 응용 프로그램 ID URI를 사용하는 경우 프로젝트는 새 응용 프로그램을 프로비전하는 대신 기존 응용 프로그램에 연결됩니다. 이 경우 새 응용 프로그램을 프로비전하려면 ID가 동일한 응용 프로그램이 이미 있는 경우 **응용 프로그램 항목 덮어쓰기 확인란을** 지우십시오.

**덮어쓰기** 확인란이 지워지고 Visual Studio에서 동일한 응용 프로그램 ID URI를 사용하는 기존 응용 프로그램을 찾은 경우 사용하려는 URI에 번호를 추가하여 새 URI를 만듭니다. 예를 들어 프로젝트 이름이 `Example`다음과 같아서 텍스트 상자를 비워 두고 **덮어쓰기** 확인란을 지우고 Azure AD `https://contoso.onmicrosoft.com/Example`테넌트에 URI 가 있는 응용 프로그램이 이미 있다고 가정합니다. 이 경우 새 응용 프로그램은 응용 프로그램 ID URI와 같은 `https://contoso.onmicrosoft.com/Example_20130619330903`프로비전됩니다.

#### <a name="provisioning-the-application-in-azure-ad"></a>Azure AD에서 응용 프로그램 프로비전

Azure AD에서 응용 프로그램을 프로비전하거나 프로젝트를 기존 응용 프로그램에 연결하려면 Visual Studio에서 도메인에 대한 글로벌 관리자의 자격 증명이 필요합니다. **인증 구성** 대화 상자에서 **확인을** 클릭하면 지정한 도메인에 대한 전역 관리자의 사용자 이름과 암호가 표시됩니다. 나중에 **새 ASP.NET 프로젝트** 대화 상자에서 프로젝트 **만들기를** 클릭하면 Visual Studio에서 Azure AD에서 응용 프로그램을 프로비전합니다. 이 프로세스의 일부로 Visual Studio는 생성 후 1년 이후에 만료되는 Web.config 파일에 클라이언트 비밀 값을 포함합니다.

**클라우드 - 단일 조직** 인증을 사용하는 응용 프로그램을 만드는 방법에 대한 자세한 내용은 다음 리소스를 참조하십시오.

- [Azure 인증](../2012/windows-azure-authentication.md)
- [Azure AD를 사용하여 웹 애플리케이션에 로그온 추가](https://msdn.microsoft.com/library/windowsazure/dn151790.aspx)
- [Azure Active Directory를 사용하여 ASP.NET 앱 개발](../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)
- [Azure AD 및 Microsoft OWIN 구성 요소를 통한 안전한 ASP.NET 웹 API](https://msdn.microsoft.com/magazine/dn463788.aspx)

이 자습서는 Visual Studio 2013에 대해 아직 업데이트되지 않았습니다. 자습서에서 수동으로 수행하도록 지시하는 작업 중 일부는 Visual Studio 2013에서 자동화되어 있습니다.

<a id="orgauthmulti"></a>
### <a name="cloud---multi-organization-authentication"></a>클라우드 - 다중 조직 인증

![여러 조직 인증](creating-web-projects-in-visual-studio/_static/image25.png)

여러 Azure AD [테넌에](https://technet.microsoft.com/library/jj573650.aspx)정의된 사용자 계정에 대한 인증을 사용하려면 이 옵션을 선택합니다. 예를 들어, 이 사이트는 contoso.com 있으며 contoso.onmicrosoft.com 테넌트에 있는 Contoso 회사의 직원과 fabrikam.onmicrosoft.com 테넌트에 있는 Fabrikam 회사의 직원에게 제공됩니다.

입력하는 설정과 응용 프로그램 프로비저닝 단계는 [단일 조직 인증과](#orgauthsingle)유사합니다.

**클라우드 - 다중 조직** 인증을 사용하는 응용 프로그램을 만드는 방법에 대한 자세한 내용은 다음 리소스를 참조하십시오.

- [Azure Active 디렉터리, ASP.NET &amp; Active Directory 팀 블로그에서 Visual Studio와 의간편한 웹 앱 통합을](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx) 통해
- [Azure AD 자습서를 사용 하 고 다중 테넌트 웹 응용 프로그램 개발.](https://msdn.microsoft.com/library/windowsazure/dn151789.aspx) 이 튜토리얼은 아직 Visual Studio 2013에 대해 업데이트되지 않았습니다. 이 자습서에서 수동으로 수행하도록 지시하는 일부 는 Visual Studio 2013에서 자동화되어 있습니다.
- 로그인하려면 앱을 [ASP.NET 여러 조직에 가입해야 합니다.](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/) 비토리오 베르토치의 블로그는 다중 조직 인증을 사용하는 프로젝트를 만들 때 사람들이 직면하는 일반적인 문제를 해결하는 방법을 설명합니다.

<a id="orgauthonprem"></a>
### <a name="on-premises-organizational-authentication"></a>온-프레미스 조직 인증

![온-프레미스 조직 인증](creating-web-projects-in-visual-studio/_static/image26.png)

AD(Windows Server Active Directory)에 정의된 사용자 계정에 대한 인증을 사용하도록 설정하고 Azure AD를 사용하지 않으려는 경우 이 옵션을 선택합니다. 이 옵션을 사용하여 인트라넷 사이트 또는 인터넷 사이트를 만들 수 있습니다. 인터넷 사이트의 경우 ADFS(Active Directory Federation 서비스)를 사용하여 AD에 대한 액세스를 제공합니다. 자세한 내용은 [Visual Studio 2013에서 ASP.NET 있는 온-프레미스 조직 인증 옵션(ADFS) 사용을](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)참조하십시오.

인트라넷 사이트의 경우 이 옵션 대신 [Windows 인증을](#winauth) 선택할 수 있습니다. Windows 인증 옵션의 경우 메타데이터 문서 URL을 제공할 필요가 없습니다. 그러나 Windows 인증은 Active Directory에서 응용 프로그램 액세스를 제어하거나 디렉터리 데이터를 쿼리하는 기능을 제공하지 않습니다.

#### <a name="on-premises-authority"></a>온-프레미스 기관

메타데이터 문서를 가리키는 URL을 입력합니다. 메타데이터 문서에는 기관의 좌표가 포함되어 있습니다. 응용 프로그램은 이러한 좌표를 사용하여 웹 사인온 흐름을 구동합니다.

#### <a name="application-id-uri"></a>응용 프로그램 ID URI

AD가 이 응용 프로그램을 식별하는 데 사용할 수 있는 고유한 URI를 제공하거나 Visual Studio에서 응용 프로그램을 만들 수 있도록 비워 둡니다.

<a id="nextsteps"></a>
## <a name="next-steps"></a>다음 단계

이 문서에서는 Visual Studio 2013에서 새로운 ASP.NET 웹 프로젝트를 만드는 데 몇 가지 기본적인 도움말을 제공했습니다. 웹 개발을 위한 Visual Studio 사용에 대한 [https://www.asp.net/visual-studio/](../../index.md)자세한 내용은 을 참조하십시오.
