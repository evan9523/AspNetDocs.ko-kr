---
uid: visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
title: 비주얼 스튜디오 2013 릴리스 노트에 대한 ASP.NET 및 웹 도구 2013.2 | 마이크로 소프트 문서
author: rick-anderson
description: ''
ms.author: riande
ms.date: 03/06/2014
ms.assetid: 7ef5f73c-ca60-43c1-bdb2-702800347e7e
msc.legacyurl: /visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
msc.type: authoredcontent
ms.openlocfilehash: 41b0f3ad43846bc5799ecd398188b0f6ffcc0d66
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543628"
---
# <a name="aspnet-and-web-tools-20132--for-visual-studio-2013-release-notes"></a>Visual Studio 2013용 ASP.NET 및 Web Tools 2013.2 릴리스 정보

[로 마이크로 소프트](https://github.com/microsoft)

## <a name="installation-notes"></a>설치 참고 사항

ASP.NET 및 Visual Studio 2013.2용 웹 도구는 기본 설치 관리자에 [Visual Studio 2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521)번들로 제공됩니다.

## <a name="documentation"></a>문서화

ASP.NET [웹 사이트에서](https://www.asp.net/)ASP.NET 및 Visual Studio 2013.2용 웹 도구에 대한 자습서 및 기타 정보를 확인할 수 있습니다.

## <a name="software-requirements"></a>소프트웨어 요구 사항

ASP.NET 및 Visual Studio 2013.2용 웹 도구에는 Visual Studio 2013이 필요합니다.

## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-20132"></a>비주얼 스튜디오 2013.2를 위한 ASP.NET 및 웹 도구의 새로운 기능

다음 섹션에서는 릴리스에서 도입된 기능에 대해 설명합니다.

- [하나의 ASP.NET 프로젝트 템플릿](#oneaspnet)
- [IIS Express에서 웹 응용 프로그램을 시작할 때 SSL 지원](#ssl)
- [비주얼 스튜디오 웹 에디터 개선 사항](#vswebeditor)
- [브라우저 링크](#browserlink)
- [비주얼 스튜디오에서 Azure 앱 서비스 웹 앱 지원](#waws)
- [새 웹 프로젝트를 만들 때 원격 Azure 리소스 만들기](#AzureResources)
- [웹 게시 개선 사항](#webpublish)
- [ASP.NET 비계](#scaffolding)
- [NuGet 2.8.1](#nuget)
- [ASP.NET 웹 양식](#webforms)
- [ASP.NET MVC 5.1.2](#mvc)
- [ASP.NET 웹 API 2.1.2](#webapi)
- [ASP.NET 웹 페이지 3.1.2](#webpages)
- [엔티티 프레임워크 6.1](#ef)
- [ASP.NET 아이덴티티 2.0.0](#identity)
- [Microsoft OWIN 구성 요소](#owin)
- [ASP.NET 시그널R 2.0.2](#signalr)

<a id="oneaspnet"></a>
### <a name="one-aspnet-project-templates"></a>하나의 ASP.NET 프로젝트 템플릿

- 계정 확인 및 암호 재설정을 지원하기 위해 ASP.NET 프로젝트 템플릿을 업데이트합니다.
- ASP.NET 웹 API 템플릿을 업데이트하여 온-프레미스 조직 계정을 사용하여 인증을 지원합니다.
- 이제 ASP.NET SPA 템플릿에는 MVC 및 서버 측 보기를 기반으로 하는 인증이 포함되어 있습니다. 템플릿에는 인증된 사용자만 액세스할 수 있는 WebAPI 컨트롤러가 있습니다.

<a id="ssl"></a>
### <a name="support-ssl-when-launching-web-applications-on-iis-express"></a>IIS Express에서 웹 응용 프로그램을 시작할 때 SSL 지원

로컬 호스트에서 HTTPS를 탐색하고 디버깅할 때 보안 경고를 제거하기 위해 Internet Explorer와 Chrome에서 자체 서명된 IIS 익스프레스 SSL 인증서를 신뢰할 수 있도록 대화 상자를 추가했습니다.

예를 들어 웹 프로젝트 속성을 SSL을 사용하도록 설정할 수 있습니다. F4를 클릭하여 속성 대화 상자를 가져옵니다. **SSL을** true로 변경합니다. SSL URL을 복사합니다.

![SSL 사용 속성](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image1.png)

HTTPS 기반 URL을 사용하도록 웹 프로젝트 속성 페이지 웹 탭을 `https://localhost:44300/` 설정합니다(이전에 SSL 웹 사이트를 만든 적이 없는 경우 SSL URL이 됩니다.)

![프로젝트 URL 설정(HTTPS)](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image2.png)

Ctrl+F5를 눌러 애플리케이션을 실행합니다. 지침에 따라 IIS Express에서 생성한 자체 서명된 인증서를 신뢰합니다.

![SSL 경고](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image3.png)

보안 **경고** 대화 상자를 읽은 다음 localhost를 나타내는 인증서를 설치하려면 **예를** 클릭합니다.

![보안 경고](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image4.png)

이 사이트는 브라우저에서 인증서 경고없이 IE 또는 크롬에 표시됩니다.

![경고없이 HTTPS 페이지](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image5.png)

Firefox는 자체 인증서 저장소를 사용하므로 경고가 표시됩니다.

<a id="vswebeditor"></a>
### <a name="visual-studio-web-editor-enhancements"></a>비주얼 스튜디오 웹 에디터 개선 사항

- **새로운 JSON 프로젝트 항목 및 편집기**: 비주얼 스튜디오에 JSON 프로젝트 항목 및 편집기를 추가했습니다. 현재 JSON 편집기 기능에는 색상 화, 구문 유효성 검사, 중괄호 완성, 개요, 도구 옵션 설정 등이 포함됩니다.

    ![JSON 에디터](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image6.png)

    인텔리센스는 이제 [JSON 스키마](http://json-schema.org/) v3 및 v4를 지원합니다. 기존 스키마를 선택하거나, 로컬 스키마 경로를 편집하거나, 프로젝트 JSON 파일을 드래그하여 상대 경로를 얻는 스키마 콤보 상자가 있습니다.

    ![JSON 인텔리센스](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image7.png)    ![JSON 스키마 편집기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image8.png)
- **새로운 Sass (SCSS) 편집기**: 우리는 VS2013 RTM에 LESS를 추가, 우리는 지금 사스 프로젝트 항목 및 편집기. Sass 편집기 기능은 LESS 편집기와 비교할 수 있으며 색상, 변수 및 Mixins IntelliSense, 주석/ 주석/ 주석 해제, 빠른 정보, 서식, 구문 유효성 검사, 개요, goto 정의, 색상 선택기, 도구 옵션 설정 등을 포함합니다.

    ![새 항목 추가: SCSS 스타일 시트](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image9.png)    ![스타일 시트 편집기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image10.png)
- **HTML, 면도기, CSS, LESS 및 Sass 문서의 새 URL 선택기:** VS 2013 웹 양식 페이지 외부의 URL 선택기없이 제공되었습니다. HTML, 면도기, CSS, LESS 및 Sass 편집기의 새로운 URL 선택기는 '.'를 이해하는 대화 상자가 없고 유창한 타이핑 선택기입니다. 및 img 태그 및 링크에 맞게 파일 목록을 필터링합니다.

    ![이미지 태그에 대한 URL 선택기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image11.png)    ![보기에 대 한 URL 선택기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image12.png)    ![CSS에 대한 URL 선택기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image13.png)
- **더 많은 기능을 추가하여 LESS 편집기로 업데이트**
- **녹아웃 인텔리센스 업그레이드**: VS intelliSense, "ko-vs-editor viewModel:" 구문에 비표준 KnockOut 구문을 추가했습니다. 양식의 주석을 사용하여 페이지의 여러 보기 모델에 바인딩하는 데 사용할 수 있습니다.

    ![녹아웃 인텔리센스](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image14.png)

    또한 중첩된 ViewModel IntelliSense에 대한 지원을 추가하여 ViewModel에서 깊이 중첩된 개체를 드릴다운할 수 있습니다.

    `<div data-bind="text: foo.bar.baz.etc" />`

    표시되는 IntelliSense는 자바스크립트 개체의 전체 IntelliSense입니다.

    ![전체 자바 스크립트 개체를 보여주는 intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image15.png)
- **HTML, 면도기, CSS, LESS 및 Sass 문서의 새 URL 선택기**: VS 2013웹 양식 페이지 외부에 URL 선택기없이 제공. HTML, 면도기, CSS, LESS 및 Sass 편집기의 새로운 URL 선택기는 '.'를 이해하는 대화 상자가 없고 유창한 타이핑 선택기입니다. 및 img 태그 및 링크에 맞게 파일 목록을 필터링합니다.

    ![이미지 태그에 대한 URL 선택기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image16.png)    ![보기에 대 한 URL 선택기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image17.png)    ![CSS에 대한 URL 선택기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image18.png)

<a id="browserlink"></a>
### <a name="browser-link"></a>브라우저 링크

- 브라우저 링크는 이제 HTTPS 연결을 지원하며 브라우저에서 인증서를 신뢰할 수 있는 한 대시보드에서 다른 연결이 있는 것으로 나열됩니다.
- 정적 HTML 소스 매핑
- 매핑 데이터에 대한 SPA 지원
- 매핑 데이터 자동 업데이트

<a id="waws"></a>
### <a name="support-for-azure-app-service-web-apps-in-visual-studio"></a>비주얼 스튜디오에서 Azure 앱 서비스 웹 앱 지원

- **Azure 로그인을 지원합니다.**
- **웹 앱에 대한 원격 디버깅 및 원격 보기**: 이제 [Azure App Service의 웹 앱에 대한 원격 디버깅과](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio) 서버 탐색기의 웹 앱 콘텐츠 파일의 원격 보기를 지원합니다.

<a id="AzureResources"></a>
### <a name="create-remote-azure-resources-when-creating-a-new-web-project"></a>새 웹 프로젝트를 만들 때 원격 Azure 리소스 만들기

새 웹 응용 프로그램 대화 상자에 Azure ["원격 리소스 만들기"](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) 확인란을 추가했습니다. 이를 선택하면 새 웹 응용 프로그램을 만들고, 테스트를 위해 Azure 게시 사이트를 설정하고, 몇 가지 간단한 단계에서 게시 프로필을 만드는 환경을 통합할 수 있습니다.

![Azure 리소스가 있는 새 프로젝트](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image19.png)![Azure에 게시](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image20.png)

<a id="webpublish"></a>
### <a name="web-publish-enhancements"></a>웹 게시 개선 사항

- 게시에 대한 사용자 환경을 개선합니다.

<a id="scaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 비계

- **열거형 지원:** 모델이 열거형임을 사용하는 경우 MVC Scaffolder는 열거형에 대한 드롭다운을 생성합니다. MVC의 열거형 도우미를 사용합니다.
- **부트스트랩 지원**: 부트스트랩 클래스를 사용하도록 MVC 스캐폴딩의 편집기 템플릿을 업데이트했습니다.
- **패키지 지원**: MVC 및 웹 API Scaffolders는 MVC 및 웹 API에 대한 5.1 패키지를 추가합니다.

다음 스크린샷은 스캐폴딩 모델을 보여 줍니다.

- 모델 코드:

     ![모델 코드](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image21.png)
- 모델 코드를 컴파일하고 마우스 오른쪽 단추로 클릭하고 새 **스캐폴드 항목** **추가를**선택합니다.

     ![새 비계 항목 추가](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image22.png)
- **엔터티 프레임워크를 사용하여 뷰가 있는 MVC5 컨트롤러선택:**

     ![뷰가 있는 새 MVC5 컨트롤러 추가](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image23.png)
- 모델을 사용하여 **컨트롤러 추가:**

    ![](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image24.png)
- 생성된 코드를 확인합니다(예: 보기/평일 모델/편집.cshtml 포함 `@Html.EnumDropDownListFor`: ![EnumDropDownListFor 포함 보기)](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image25.png)
- 생성 된 열거형 콤보 박스를 볼 수있는 페이지를 실행, 값이 null 수 있는 경우, 빈 문자열은 콤보 상자에 대해 선택할 수 있습니다. 예를 들어 **만들기** 페이지에는 다음이 표시됩니다.

    ![빈 문자열을 허용하는 콤보 상자](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image26.png)

<a id="nuget"></a>
### <a name="nuget-281"></a>NuGet 2.8.1

NuGet 2.8.1 RTM은 2014년 4월에 출시될 예정입니다. 다음은 릴리스 노트의 중요한 점이지만 이러한 변경 사항에 대한 자세한 내용은 [전체 릴리스 정보를](http://docs.nuget.org/docs/release-notes/nuget-2.8) 확인하십시오.

- **대상 윈도우 폰 8.1 응용 프로그램**: NuGet 2.8.1 이제 대상 프레임 워크 모니커 '윈도우 폰 앱', 'WPA', '윈도우 폰 앱81', 'WPA81'을 사용하여 윈도우 폰 8.1 응용 프로그램을 대상으로 지원합니다.

- **종속성에 대한 패치 해결**: 패키지 종속성을 해결할 때 NuGet은 패키지에 대한 종속성을 제공하는 가장 낮은 주 및 부 패키지 버전을 선택하는 전략을 구현했습니다. 그러나 주 버전과 부 버전과 달리 패치 버전은 항상 가장 높은 버전으로 해결되었습니다. 이 동작은 의도된 것이었지만 종속성이 있는 패키지를 설치하기 위한 결정성이 부족했습니다.
- **종속성 버전 스위치**: NuGet 2.8은 종속성을 해결하기 위한 *기본* 동작을 변경하지만 패키지 관리자 콘솔에서 -DependencyVersion 스위치를 통해 종속성 해결 프로세스를 보다 정밀하게 제어합니다. 이 스위치를 사용하면 종속성을 가능한 가장 낮은 버전(기본 동작), 가능한 가장 높은 버전 또는 가장 높은 마이너 또는 패치 버전으로 해결할 수 있습니다. 이 스위치는 powershell 명령에서 패키지 설치에만 작동합니다.
- **종속성 버전 속성**: 위에서 자세히 설명한 -DependencyVersion 스위치 외에도 NuGet은 설치 패키지 호출에 -DependencyVersion 스위치가 지정되지 않은 경우 기본값을 정의하는 nuget.config 파일에서 새 특성을 설정할 수 있습니다. 이 값은 설치 패키지 작업에 대해 NuGet 패키지 관리자 대화 상자에서도 적용됩니다. 이 값을 설정하려면 nuget.config 파일에 아래 속성을 추가합니다.

    `<config> <add key="dependencyversion" value="Highest" /> </config>`
- **미리 보기 NuGet 작업 -WhatIf**: 일부 NuGet 패키지에는 깊은 종속성 그래프가 있을 수 있으므로 설치, 제거 또는 업데이트 작업 중에 먼저 발생할 작업을 확인하는 데 도움이 될 수 있습니다. NuGet 2.8은 표준 PowerShell-what을 설치 패키지로 전환하면, 제거 패키지 및 업데이트 패키지 명령을 추가하여 명령이 적용되는 패키지의 전체 클로저를 시각화할 수 있도록 합니다.
- **다운그레이드 패키지**: 새로운 기능을 조사한 다음 마지막 안정 버전으로 롤백하기로 결정하기 위해 패키지의 시험판 버전을 설치하는 것은 드문 일이 아닙니다. NuGet 2.8 이전에는 시험판 패키지와 해당 종속성을 제거한 다음 이전 버전을 설치하는 다단계 프로세스였습니다. 그러나 NuGet 2.8을 사용하면 업데이트 패키지가 전체 패키지 클로저(예: 패키지의 종속성 트리)를 이전 버전으로 롤백합니다.
- **개발 종속성**: 개발 프로세스를 최적화하는 데 사용되는 도구를 포함하여 다양한 유형의 기능을 NuGet 패키지로 전달할 수 있습니다. 이러한 구성 요소는 새 패키지를 개발하는 데 도움이 될 수 있지만 나중에 게시될 때 새 패키지의 종속성으로 간주해서는 안 됩니다. NuGet 2.8을 사용하면 패키지가 .nuspec 파일에서 개발 종속성으로 자신을 식별할 수 있습니다. 설치하면 이 메타데이터도 패키지가 설치된 프로젝트의 packages.config 파일에 추가됩니다. 해당 packages.config 파일nuget.exe 팩 동안 NuGet 종속성에 대 한 나중에 분석 하는 경우 개발 종속성으로 표시 된 해당 종속성을 제외 합니다.
- **개별 packages.config 파일 다른 플랫폼에 대 한:** 여러 대상 플랫폼에 대 한 응용 프로그램을 개발할 때 각 빌드 환경에 대 한 다른 프로젝트 파일을 가지고 하는 것이 일반적입니다. 또한 패키지는 서로 다른 플랫폼에 대한 다양한 지원 수준을 가지고 있으므로 서로 다른 프로젝트 파일에서 다른 NuGet 패키지를 사용하는 것이 일반적입니다. NuGet 2.8은 플랫폼별 프로젝트 파일에 대해 서로 다른 패키지.config 파일을 만들어 이 시나리오에 대한 향상된 지원을 제공합니다.
- **로컬 캐시로 돌아가기:** NuGet 패키지는 일반적으로 네트워크 연결을 사용하여 [NuGet 갤러리와](http://www.nuget.org) 같은 원격 갤러리에서 사용되지만 클라이언트가 연결되지 않은 많은 시나리오가 있습니다. 네트워크 연결이 없으면 NuGet 클라이언트가 로컬 NuGet 캐시에서 해당 패키지가 이미 클라이언트의 컴퓨터에 있는 경우에도 패키지를 성공적으로 설치할 수 없었습니다. NuGet 2.8은 패키지 관리자 콘솔에 자동 캐시 대체를 추가합니다.

    캐시 대체 기능에는 특정 명령 인수가 필요하지 않습니다. 또한 캐시 대체는 현재 패키지 관리자 콘솔에서만 작동하며, 이 동작은 현재 패키지 관리자 대화 상자에서 작동하지 않습니다.
- **버그 수정**: 주요 버그 수정 중 하나는 업데이트 패키지 -다시 설치 명령의 성능 향상이었습니다.

    이러한 기능 및 앞서 언급 한 성능 수정 외에도 NuGet의이 릴리스에는 다른 많은 버그 수정 사항도 포함되어 있습니다. 릴리스에서 해결된 총 181개의 문제가 있었습니다. NuGet 2.8에 고정된 작업 항목의 전체 목록은 이 릴리스의 [NuGet 문제 추적기를](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all) 참조하십시오.

<a id="webforms"></a>
### <a name="aspnet-web-forms"></a>ASP.NET 웹 양식

- 이제 웹 양식 템플릿에 ASP.NET ID에 대한 계정 확인 및 암호 재설정 을 수행하는 방법을 보여 줍니다.
- 엔터티 데이터 원본 컨트롤 및 엔터티 프레임워크에 대한 동적 데이터 공급자 6. 자세한 내용은 다음 MSDN 블로그를 참조하십시오: [동적 데이터 공급자 및 EntityDataSource 엔터티 프레임워크 6에 대한 제어.](https://blogs.msdn.com/b/webdev/archive/2014/01/30/announcing-preview-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)

<a id="mvc"></a>
### <a name="aspnet-mvc-512"></a>ASP.NET MVC 5.1.2

- [특성 라우팅 개선 사항](../../../mvc/overview/releases/mvc51-release-notes.md#AttributeRouting)
- [편집기 템플릿에 대한 부트스트랩 지원](../../../mvc/overview/releases/mvc51-release-notes.md#Bootstrap)
- [뷰에서 열거형 지원](../../../mvc/overview/releases/mvc51-release-notes.md#Enum)
- [최소 길이/최대 길이 속성에 대한 눈에 거슬리지 지원](../../../mvc/overview/releases/mvc51-release-notes.md#Unobtrusive)
- [눈에 거슬리지 아약스의 '이' 맥락 지원](../../../mvc/overview/releases/mvc51-release-notes.md#thisContext)
- 다양한 [버그 수정](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=MVC&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webapi"></a>
### <a name="aspnet-web-api-212"></a>ASP.NET 웹 API 2.1.2

- [전역 오류 처리](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#global-error)
- [특성 라우팅 개선 사항](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#attribute-routing)
- [도움말 페이지 개선 사항](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#help-page)
- [무시경로 지원](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#ignoreroute)
- [BSON 미디어 형 포터](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#bson)
- [비동기 필터에 대한 더 나은 지원](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#async-filters)
- [클라이언트 서식 라이브러리에 대한 쿼리 구문 분석](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#query-parsing)
- 다양한 [버그 수정](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20API%7cWeb%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webpages"></a>
### <a name="aspnet-web-pages-312"></a>ASP.NET 웹 페이지 3.1.2

- 다양한 [버그 수정](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20Pages/Razor&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="ef"></a>
### <a name="entity-framework-61"></a>엔티티 프레임워크 6.1

엔터티 프레임워크는 런타임 및 툴링 모두에 대해 버전 6.1로 업데이트되었습니다. 엔터티 프레임워크(EF) 6.1은 엔터티 프레임워크 6에 대한 사소한 업데이트이며 여러 버그 수정 및 새로운 기능이 포함되어 있습니다. 새 기능에 대한 설명서 링크를 포함하여 EF6.1에 대한 자세한 내용은 [엔터티 프레임워크 버전 기록을](https://msdn.microsoft.com/data/jj574253)참조하십시오. 이 릴리스의 새로운 기능은 다음과 같습니다.

- **툴링 통합은** 새 EF 모델을 만드는 일관된 방법을 제공합니다. 이 기능은 ADO.NET 엔터티 데이터 모델 마법사를 확장하여 기존 데이터베이스의 리버스 엔지니어링을 포함하여 Code First 모델 생성을 지원합니다. 이러한 기능은 이전에 EF 전동 공구의 베타 품질에서 사용할 수 있었습니다.
- **트랜잭션 커밋 실패처리는** 새로 도입된 트랜잭션 작업을 가로채는 기능을 사용하는 새 [System.Data.Entity.Infrastructure.CommitFailureHandler를](https://msdn.microsoft.com/library/system.data.entity.infrastructure.commitfailurehandler(v=vs.113).aspx) 제공합니다. **CommitFailureHandler** 트랜잭션을 커밋 하는 동안 연결 오류에서 자동으로 복구할 수 있습니다.
- **IndexAttribute를** 사용하면 Code First 모델의 속성(또는 속성)에 특성을 배치하여 인덱스를 지정할 수 있습니다. 그런 다음 코드 First는 데이터베이스에 해당 인덱스를 만듭니다.
- **공용 매핑 API는** 데이터베이스의 열 및 테이블에 속성 및 형식을 매핑하는 방법에 대한 EF가 가지고 있는 정보에 대한 액세스를 제공합니다. 이전 릴리스에서는 이 API가 내부 버전이었습니다.
- **App/Web.config 파일을 통해 인터셉터를 구성할**수 있습니다(응용 프로그램을 다시 컴파일하지 않고도 인터셉터를 추가할 수 있음).
- **DatabaseLogger는** 모든 데이터베이스 작업을 파일에 쉽게 기록할 수 있는 새로운 인터셉터입니다. 이전 기능과 함께 사용하면 다시 컴파일할 필요 없이 배포된 응용 프로그램에 대한 데이터베이스 작업 로깅을 쉽게 전환할 수 있습니다.
- 스캐폴드 마이그레이션이 보다 정확할 수 있도록 **마이그레이션 모델 변경 검색이** 개선되었습니다. 변경 감지 프로세스의 성능도 크게 향상되었습니다.
- 초기화 하는 동안 감소 된 데이터베이스 작업, LINQ 쿼리에서 null 같음 비교에 대 한 최적화, 더 많은 시나리오에서 빠른 보기 생성 (모델 만들기) 및 여러 연결 추적 된 엔터티의 보다 효율적인 구체화를 포함 하 여 **성능 향상.**

<a id="identity"></a>
### <a name="aspnet-identity-200"></a>ASP.NET 아이덴티티 2.0.0

- **이중 인증**: ASP.NET ID는 이제 2단계 인증을 지원합니다. 이중 인증은 암호가 손상된 경우 사용자 계정에 추가 보안 계층을 제공합니다. 또한 두 요소 코드에 대한 무차별 암호 대입 공격에 대한 보호기능도 있습니다.
- **계정 잠금:** 사용자가 암호 또는 이중 요소 코드를 잘못 입력하면 사용자를 잠글 수 있는 방법을 제공합니다. 잘못된 시도 횟수와 사용자의 시간 범위를 잠글 수 있습니다. 개발자는 필요한 경우 특정 사용자 계정에 대해 계정 잠금을 선택적으로 해제할 수 있습니다.
- **계정 확인:** 이제 ASP.NET ID 시스템이 계정 확인을 지원합니다. 이것은 오늘날 대부분의 웹 사이트에서 매우 일반적인 시나리오로, 웹 사이트에서 새 계정을 등록 할 때 웹 사이트에서 아무것도 하기 전에 이메일을 확인해야합니다. 이메일 확인은 가짜 계정이 생성되지 않도록 하기 때문에 유용합니다. 이 기능은 전자 메일을 포럼 사이트, 은행, 전자 상거래 또는 소셜 웹 사이트와 같은 웹 사이트 사용자와 통신하는 방법으로 사용하는 경우에 매우 유용합니다.
- **암호 재설정:** 암호 재설정은 사용자가 암호를 잊어버린 경우 암호를 재설정할 수 있는 기능입니다.
- **보안 스탬프(모든 곳에서 로그아웃):** 사용자가 암호 또는 관련 로그인 제거(예: Facebook, Google, Microsoft 계정 등)를 제거하는 등의 기타 보안 관련 정보를 변경하는 경우 사용자에 대한 보안 토큰을 다시 생성하는 방법을 지원합니다. 이전 암호로 생성된 토큰이 무효화되도록 하려면 이 문제가 필요합니다. 샘플 프로젝트에서 사용자의 암호를 변경하면 사용자에 대해 새 토큰이 생성되고 이전 토큰이 무효화됩니다. 이 기능은 암호를 변경할 때 이 응용 프로그램에 로그인한 모든 곳(다른 모든 브라우저)에서 로그아웃되므로 응용 프로그램에 추가 보안 계층을 제공합니다.
- **사용자 및 역할에 대해 기본 키 유형을 확장 가능하게 만듭니다:** id 1.0에서 ASP.NET 테이블 사용자 및 역할의 기본 키 유형은 문자열이었습니다. 즉, ASP.NET ID 시스템이 엔터티 프레임워크를 사용하여 SQL Server에서 유지되었을 때 nvarchar를 사용했습니다. 스택 오버플로에 대한 이 기본 구현과 들어오는 피드백을 기반으로 하는 많은 논의가 있었습니다. 사용자 및 역할 테이블의 기본 키를 지정할 수 있는 확장성 후크를 제공했습니다. 이 확장성 후크는 응용 프로그램을 마이그레이션하고 응용 프로그램이 UserIds 또는 ints를 저장하는 경우에 특히 유용합니다.
- **사용자 및 역할에 대한 IQueryable 지원**: UsersStore 및 RolesStore에서 IQueryable에 대한 추가 지원을 사용하면 사용자 및 역할 목록을 쉽게 얻을 수 있습니다.
- **사용자 관리자를 통한 작업 삭제 지원**
- **사용자 이름에 대한 인덱싱**: ASP.NET ID 엔터티 프레임워크 구현에서 EF 6.1.0의 새 IndexAttribute을 사용하여 사용자 이름에 고유한 인덱스를 추가했습니다. 이렇게 하면 사용자 이름이 항상 고유하며 중복된 사용자 이름으로 끝날 수 있는 경합 조건이 없습니다.
- **향상된 암호 유효성 검사기:** id 1.0에 ASP.NET 제공된 암호 유효성 검사기는 최소 길이만 유효성을 검사하는 매우 기본적인 암호 유효성 검사기였습니다. 암호의 복잡성을 보다 세한 제어할 수 있는 새로운 암호 유효성 검사기가 있습니다. 이 암호의 모든 설정을 켜더라도 사용자 계정에 대해 2단계 인증을 사용하도록 설정하는 것이 좋습니다.
- **아이덴티티팩토리 미들웨어/ 창조퍼로윈컨텍스트**:

    - **사용자 관리자**: 팩터리 구현을 사용하여 OWIN 컨텍스트에서 UserManager 인스턴스를 가져올 수 있습니다. 이 패턴은 SignIn 및 SignOut에 대한 OWIN 컨텍스트에서 인증 관리자를 가져오는 데 사용하는 것과 유사합니다. 이는 응용 프로그램에 대한 요청당 UserManager 인스턴스를 가져오는 권장 방법입니다.
    - **DbContextFactory**: ASP.NET ID는 SQL Server에서 ID 시스템을 유지하기 위해 엔터티 프레임워크를 사용합니다. 이렇게 하려면 ID 시스템에는 ApplicationDbContext에 대한 참조가 있습니다. DbContextFactory 미들웨어는 응용 프로그램에서 사용할 수 있는 요청당 ApplicationDbContext의 인스턴스를 반환합니다.
- **ASP.NET ID 샘플 NuGet 패키지**: 샘플 NuGet 패키지를 사용하면 ASP.NET ID에 대한 샘플을 쉽게 설치하고 실행하고 모범 사례를 따를 수 있습니다. 이것은 MVC 응용 ASP.NET 샘플입니다. 프로덕션 환경에서 배포하기 전에 응용 프로그램에 맞게 코드를 수정하십시오. 샘플은 빈 ASP.NET 응용 프로그램에 설치해야 합니다. 패키지에 대한 자세한 내용은 다음 블로그 게시물로 이동하십시오: [ASP.NET ID 2.0.0의 RTM 발표](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)

<a id="owin"></a>
### <a name="microsoft-owin-components"></a>Microsoft OWIN 구성 요소

이 릴리스에서는 많은 버그가 수정되었습니다. 자세한 내용은 [2.1.0 릴리스의 릴리스 정보를](https://katanaproject.codeplex.com/releases/view/113281) 참조하십시오.

<a id="signalr"></a>
### <a name="aspnet-signalr-202"></a>ASP.NET 시그널R 2.0.2

이 릴리스에서는 많은 버그가 수정되었습니다. 자세한 내용은 [2.0.2 릴리스의 릴리스 정보를](https://github.com/SignalR/SignalR/releases/tag/2.0.2) 참조하십시오.
