---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: 비주얼 스튜디오 2012에 대한 ASP.NET 및 웹 도구 2013.1에 대한 릴리스 정보 | 마이크로 소프트 문서
author: rick-anderson
description: 이 문서에서는 Visual Studio 2012에 대한 ASP.NET 및 웹 도구 2013.1 릴리스에 대해 설명합니다.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: d4aced4e77a150d52358c2d2513ff79e6594a9de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543576"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Visual Studio 2012용 ASP.NET 및 Web Tools 2013.1 릴리스 정보

[로 마이크로 소프트](https://github.com/microsoft)

> 이 문서에서는 Visual Studio 2012에 대한 ASP.NET 및 웹 도구 2013.1 릴리스에 대해 설명합니다.

## <a name="contents"></a>콘텐츠

- [설치 노트](#install)
- [소프트웨어 요구 사항](#requirements)
- ASP.NET 및 웹 도구의 새로운 기능 2013.1 Visual Studio 2012

    - [부트스트랩](#bootstrap)
    - [템플릿](#templates)

        - [ASP.NET MVC 5 템플릿](#mvc5template)
        - [ASP.NET 웹 API 2 템플릿](#apitemplate)
        - [항목 템플릿](#itemtemplate)
    - [Entity Framework 6](#ef6)
    - [ASP.NET 비계](#scaffold)
    - [면도기 편집기](#razor)
    - [NuGet 2.7](#nuget)
- 알려진 문제 및 주요 변경 사항

    - [ASP.NET 비계](#issuescaffolding)

        - [MVC 및 웹 API 스캐폴딩 - HTTP 404, 찾을 수 없는 오류](#404issue)
        - [비계 항목을 추가 한 후 웹 작업을 중지하는 Visual Studio Express 2012](#expressissue)
    - [ASP.NET 면도기 3](#issuerazor)

        - [찾아보기 또는 F5로 cshtml 파일을 보는 것은 서버 오류를 발생](#browseissue)
        - [URL 다시 쓰기 및 틸데(~)](#rewriteissue)
    - [템플릿](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a>설치 참고 사항

[설치 중](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET 및 웹 도구 2013.1 Visual Studio 2012.

<a id="requirements"></a>
## <a name="software-requirements"></a>소프트웨어 요구 사항

웹용 Visual Studio 2012 또는 Visual Studio Express 2012가 있어야 합니다.

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>ASP.NET 및 웹 도구의 새로운 기능 2013.1 Visual Studio 2012

<a id="bootstrap"></a>
### <a name="bootstrap"></a>부트스트랩

MVC 5 컨트롤러 및 뷰를 스캐폴드하면 뷰의 태그가 [부트스트랩을](http://getbootstrap.com/)사용합니다.

<a id="templates"></a>
### <a name="templates"></a>템플릿

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a>ASP.NET MVC 5 템플릿

새 MVC 5 템플릿을 추가했습니다. 최신 MVC 5 NuGet 패키지를 참조하며 스캐폴딩을 사용하여 컨트롤러와 뷰를 추가할 수 있습니다.

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a>ASP.NET 웹 API 2 템플릿

새 웹 API 2 템플릿을 추가했습니다. 최신 웹 API 2 NuGet 패키지를 참조하며 스캐폴딩을 사용하여 컨트롤러 및 뷰를 추가할 수 있습니다.

<a id="itemtemplate"></a>
#### <a name="item-templates"></a>항목 템플릿

MVC 5 뷰, 웹 페이지(Razor 3) 및 웹 API 2 컨트롤러에 대한 새 항목 템플릿을 추가했습니다. 새 항목을 추가하는 동안 프로젝트에 관련 NuGet 패키지를 설치합니다.

<a id="ef6"></a>
### <a name="entity-framework-6"></a>Entity Framework 6

엔터티 프레임워크를 사용하여 MVC 또는 웹 API 컨트롤러를 스캐폴드할 때 프레임워크 6를 사용합니다. 엔터티 프레임워크에 대한 자세한 내용은 [엔터티 프레임워크 버전 기록을](https://msdn.com/data/jj574253)참조하십시오.

또한 Visual Studio 2012를 위한 엔터티 프레임워크 6 도구를 다운로드하여 설치할 수도 있습니다. 엔터티 [받기 프레임워크](https://msdn.com/data/ee712906#tooling)를 참조하십시오.

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 비계

ASP.NET 스캐폴딩은 ASP.NET 웹 응용 프로그램을 위한 코드 생성 프레임워크입니다. 데이터 모델과 상호 작용하는 상용구 코드를 프로젝트에 쉽게 추가할 수 있습니다.

이전 버전의 Visual Studio에서는 스캐폴딩이 ASP.NET MVC 프로젝트로 제한되었습니다. 이 업데이트를 통해 이제 웹 양식을 포함한 모든 ASP.NET 프로젝트에 스캐폴딩을 사용할 수 있습니다. 이 업데이트는 Web Forms 프로젝트에 대 한 페이지 생성을 지원 하지 않습니다 하지만 여전히 프로젝트에 MVC 종속성을 추가 하 여 웹 폼과 스캐폴딩을 사용할 수 있습니다. 웹 양식에 대한 페이지 생성에 대한 지원은 향후 업데이트에 추가될 예정입니다.

스캐폴딩을 사용할 때 필요한 모든 종속성이 프로젝트에 설치되었는지 확인합니다. 예를 들어 ASP.NET Web Forms 프로젝트로 시작한 다음 스캐폴딩을 사용하여 웹 API 컨트롤러를 추가하는 경우 필요한 NuGet 패키지 및 참조가 프로젝트에 자동으로 추가됩니다.

웹 양식 프로젝트에 MVC 스캐폴딩을 추가하려면 **새 스캐폴드 항목을** 추가하고 대화 상자 창에서 **MVC 5 종속성을** 선택합니다. 스캐폴딩 MVC에는 두 가지 옵션이 있습니다. 최소 및 전체. 최소를 선택하면 ASP.NET MVC에 대한 NuGet 패키지 및 참조만 프로젝트에 추가됩니다. 전체 옵션을 선택하면 MVC 프로젝트에 필요한 콘텐츠 파일뿐만 아니라 최소 종속성이 추가됩니다.

비동기 컨트롤러 스캐폴딩에 대한 지원은 엔터티 프레임워크 6의 새 비동기 기능을 사용합니다.

자세한 정보 및 자습서는 [ASP.NET 스캐폴딩 개요를](../2013/aspnet-scaffolding-overview.md)참조하십시오. 이 자습서에서는 Visual Studio 2013을 사용하여 스캐폴딩을 보여 주지만 Visual Studio 2012의 ASP.NET 및 웹 도구 2013.1에도 적용할 수 있습니다.

<a id="razor"></a>
### <a name="razor-editor"></a>면도기 편집기

이 업데이트와 함께, Visual Studio 2012 지금 지원 면도기 3 툴링/편집.

<a id="nuget"></a>
### <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7에는 [NuGet 2.7 릴리스 노트에서](http://docs.nuget.org/docs/release-notes/nuget-2.7)자세히 설명하는 풍부한 새로운 기능 집합이 포함되어 있습니다.

이 버전의 NuGet은 사용자가 NuGet에서 누락된 패키지를 복원하도록 명시적으로 허용할 필요가 없습니다. NuGet 2.7을 설치할 때 사용자는 누락된 패키지를 자동으로 복원하는 데 암시적으로 동의합니다. 사용자는 Visual Studio의 NuGet 설정을 통해 패키지 복원을 명시적으로 옵트아웃할 수 있습니다. 이렇게 변경하면 패키지 복원의 작동 방식이 간소화됩니다.

## <a name="known-issues-and-breaking-changes"></a>알려진 문제 및 주요 변경 사항

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 비계

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC 및 웹 API 스캐폴딩 - HTTP 404, 찾을 수 없는 오류

프로젝트에 스캐폴드된 항목을 추가할 때 오류가 발생하면 프로젝트가 일관되지 않은 상태로 남아 있을 수 있습니다. 스캐폴딩으로 변경된 변경 사항 중 일부는 롤백되지만 설치된 NuGet 패키지와 같은 다른 변경 내용은 롤백되지 않습니다. 라우팅 구성 변경 내용이 롤백되면 스캐폴드된 항목으로 탐색할 때 HTTP 404 오류가 사용자에게 표시됩니다.

MVC에 대해 이 오류를 해결하려면 새 스캐폴드된 항목을 추가하고 MVC 5 종속성(최소 또는 전체)을 선택합니다. 이 프로세스는 프로젝트에 필요한 모든 변경 내용을 추가합니다.

웹 API에 대해 이 오류를 수정하려면 다음을 수행하십시오.

1. 프로젝트에 다음 WebApiConfig 클래스를 추가합니다.

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. WebApiConfig.등록을 Global.asax의 응용 프로그램\_시작 메서드에 다음과 같이 구성합니다.

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a>비계 항목을 추가 한 후 웹 작업을 중지하는 Visual Studio Express 2012

웹용 Visual Studio Express 2012가 엔터티 프레임워크를 사용하여 스캐폴드된 항목을 추가한 후 작업을 중지하는 경우(예: 엔터티 프레임워크를 사용하는 작업이 있는 웹 API 2 컨트롤러) Visual Studio Express가 System.Web.Extensions에 종속된 어셈블리의 기본 이미지를 로드하지 못했을 수 있습니다.

이 문제를 해결하려면 Visual Studio Express를 구성하여 System.Web.Extensions의 MSIL 이미지로 작업하도록 구성합니다.

1. 관리자 모드에서 명령 프롬프트를 엽니다.
2. %ProgramFiles%\마이크로소프트 비주얼 스튜디오 11.0\Common7\IDE 또는 %ProgramFiles (x86)%\마이크로소프트 비주얼 스튜디오 11.0\Common7\IDE (64 비트 윈도우)로 이동합니다.
3. 텍스트 편집기에서 VWDExpress.exe.config를 엽니다.
4. &lt;&gt;구성/런타임&gt; 요소 아래에 다음 줄을 추가합니다.&lt;  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. 웹용 비주얼 스튜디오 익스프레스 2012를 다시 시작합니다.

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a>ASP.NET 면도기 3

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a>찾아보기 또는 F5로 cshtml 파일을 보는 것은 서버 오류를 발생

Visual Studio 2012에서 MVC 5 프로젝트를 만들고(또는 Visual Studio 2012에서 열린 Visual Studio 2013에서 열림) 찾아보기 또는 F5를 사용하여 cshtml 파일을 보려고 하면 **'/' 응용 프로그램에서 서버 오류와**같은 오류가 표시됩니다. 서버가`http://localhost:XXXX/Views/../XXXX.cshtml`

이 문제를 해결하려면 프로젝트의 **시작 설정** 설정을 **특정 페이지로**변경합니다. 페이지에 대한 값을 제공할 필요는 없습니다.

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

이 변경 후 F5를 선택하면 응용 프로그램의 루트()로`http://localhost:XXXX`이동합니다. 이 동작은 **현재 페이지** 설정이 열린 페이지를 시작되는 Visual Studio 2013의 MVC 5 프로젝트의 동작과 다름없습니다.

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a>URL 다시 쓰기 및 틸데(~)

ASP.NET Razor 3 또는 ASP.NET MVC 5로 업그레이드한 후 URL 다시 쓰기를 사용하는 경우 물결표(~) 표기가 더 이상 제대로 작동하지 않을 수 있습니다. URL &lt;다시 쓰기는 A/&gt;및 스크립트/ &lt;&gt;LINK/ &lt;&gt;와 같은 HTML 요소의 표기에 영향을 미치므로 물결표가 더 이상 루트 디렉토리에 매핑되지 않습니다.

예를 들어 **asp.net asp.net/content** 요청을 다시 **asp.net**작성하는 경우 &lt;href="~/content/"//에서&gt; href 특성을 **/content/content/대신 /content/content/로** **/** 확인합니다. 이 변경을 억제하려면 **IIS\_WasUrlRewritten** 컨텍스트를 각 웹 페이지 또는 Global.asax의 **응용 프로그램\_BeginRequest에서** false로 설정할 수 있습니다.

<a id="templateissue"></a>
### <a name="templates"></a>템플릿

Windows 8.1 또는 Windows 서버 2012 R2에서 Visual Studio 2012를 사용하여 ASP.NET MVC 프로젝트를 만들 때 Visual Studio는 "ASP.NET 4.5에 대한 웹 [url] 구성 실패"라는 오류 메시지가 표시됩니다.

![구성 오류](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

Visual Studio 2012는 Windows 릴리스에 설치될 때 ASP.NET 4.5 기능을 사용하지 않으므로 이 오류가 표시됩니다. ASP.NET 4.5를 사용하려면 Windows 켜기 기능에 설명된 단계를 [수행하거나 끕니다.](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)

![Windows 기능 켜기 또는 끄기](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

또는 명령줄을 통해 ASP.NET 4.5를 활성화할 수 있습니다.

1. 관리자 모드에서 명령 프롬프트를 엽니다.
2. 다음 명령을 실행하여 ASP.NET 4.5를 활성화합니다.  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
