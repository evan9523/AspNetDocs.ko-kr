---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: '비주얼 스튜디오를 사용한 ASP.NET 웹 배포: Web.config 파일 변환 | 마이크로 소프트 문서'
author: tdykstra
description: 이 자습서 시리즈에서는 usin을 통해 Azure App Service 웹 앱 또는 타사 호스팅 공급자에 ASP.NET 웹 응용 프로그램을 배포(게시)하는 방법을 보여 주며...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: a9d39547c94a63003442ba6fe1257693dde24b05
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675750"
---
# <a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a>Visual Studio를 사용한 ASP.NET 웹 배포: Web.config 파일 변환

로 [톰 다이크스트라](https://github.com/tdykstra)

[스타터 프로젝트 다운로드](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈에서는 Visual Studio 2012 또는 Visual Studio 2010을 사용하여 Azure App Service 웹 앱 또는 타사 호스팅 공급자에 ASP.NET 웹 응용 프로그램을 배포(게시)하는 방법을 보여 주며, 타사 호스팅 공급자에게 배포(게시)합니다. 시리즈에 대한 자세한 내용은 [시리즈의 첫 번째 자습서를](introduction.md)참조하십시오.

## <a name="overview"></a>개요

이 자습서에서는 *Web.config* 파일을 다른 대상 환경에 배포할 때 변경 하는 프로세스를 자동화 하는 방법을 보여 줍니다. 대부분의 응용 프로그램에는 *Web.config* 파일에 응용 프로그램을 배포할 때 달라야 하는 설정이 있습니다. 이러한 변경 프로세스를 자동화하면 배포할 때마다 수동으로 변경할 필요가 없으며, 이는 지루하고 오류가 발생하기 쉽습니다.

알림: 자습서를 진행하면서 오류 메시지가 나 문제가 작동하지 않는 경우 [문제 해결 페이지를](troubleshooting.md)확인하십시오.

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web.config 변환 과 웹 배포 매개 변수

*Web.config* 파일 설정을 변경하는 프로세스를 자동화하는 방법에는 [Web.config 변환](https://msdn.microsoft.com/library/dd465326.aspx) 및 [Web Deploy 매개 변수의](https://msdn.microsoft.com/library/ff398068.aspx)두 가지가 있습니다. *Web.config* 변환 파일에는 *Web.config* 파일을 배포할 때 변경하는 방법을 지정하는 XML 태그가 포함되어 있습니다. 특정 빌드 구성 및 특정 게시 프로필에 대해 다른 변경 내용을 지정할 수 있습니다. 기본 빌드 구성은 디버그 및 릴리스이며 사용자 지정 빌드 구성을 만들 수 있습니다. 게시 프로필은 일반적으로 대상 환경에 해당합니다. [(테스트 환경 자습서로 IIS에 배포에서](deploying-to-iis.md) 프로필 게시에 대 한 자세한 내용은)

Web Deploy 매개 변수를 사용하여 *Web.config* 파일에 있는 설정을 포함하여 배포 중에 구성해야 하는 다양한 종류의 설정을 지정할 수 있습니다. *Web.config* 파일 변경 내용을 지정하는 데 사용되는 경우 Web Deploy 매개 변수는 설정하기가 더 복잡하지만 배포할 때까지 설정할 값을 모르는 경우에 유용합니다. 예를 들어 엔터프라이즈 환경에서 *배포 패키지를* 만들어 IT 부서의 담당자에게 프로덕션 환경에 설치하도록 할 수 있으며, 해당 관리자는 모르는 연결 문자열이나 암호를 입력할 수 있어야 합니다.

이 자습서 시리즈에서 다루는 시나리오의 경우 *Web.config* 파일에 수행해야 하는 모든 작업을 미리 알고 있으므로 Web Deploy 매개 변수를 사용할 필요가 없습니다. 사용된 빌드 구성에 따라 다른 일부 변환과 사용된 게시 프로필에 따라 다른 변환을 구성합니다.

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a>Azure에서 Web.config 설정 지정

변경하려는 *Web.config* 파일 설정이 `<connectionStrings>` `<appSettings>` 요소 또는 요소에 있고 Azure 앱 서비스에서 웹 앱에 배포하는 경우 배포 하는 동안 변경 내용을 자동화하는 또 다른 옵션이 있습니다. 웹 앱에 대한 관리 포털 페이지의 **구성** 탭에서 Azure에서 적용하려는 설정을 입력할 수 **있습니다(앱 설정** 및 **연결 문자열** 섹션으로 스크롤). 프로젝트를 배포할 때 Azure는 변경 내용을 자동으로 적용합니다. 자세한 내용은 [Windows Azure 웹 사이트: 응용 프로그램 문자열 및 연결 문자열의 작동 방식을](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)참조하십시오.

## <a name="default-transformation-files"></a>기본 변환 파일

**솔루션 탐색기에서** *Web.config를* 확장하여 두 기본 빌드 구성에 대해 기본적으로 생성되는 *Web.Debug.config* 및 *Web.Release.config* 변환 파일을 볼 수 있습니다.

![웹.config_transform_files](web-config-transformations/_static/image1.png)

Web.config 파일을 마우스 오른쪽 단추로 클릭하고 컨텍스트 메뉴에서 **구성 변환 추가를** 선택하여 사용자 지정 빌드 구성에 대한 변환 파일을 만들 수 있습니다. 이 자습서에서는 사용자 지정 빌드 구성을 만들지 않았으므로 이 자습서에서는 이 작업을 수행할 필요가 없으며 메뉴 옵션이 비활성화됩니다.

나중에 테스트, 스테이징 및 프로덕션 게시 프로필에 대해 각각 하나씩 세 개의 변환 파일을 더 만듭니다. 대상 환경에 종속되므로 게시 프로필 변환 파일에서 처리할 설정의 일반적인 예는 테스트와 프로덕션에 대해 다른 WCF 끝점입니다. 이후 자습서에서 해당 파일과 함께 게시 프로필을 만든 후 게시 프로필 변환 파일을 만듭니다.

## <a name="disable-debug-mode"></a>디버그 모드 사용 안 함

대상 환경이 아닌 빌드 구성에 종속된 설정의 `debug` 예가 특성입니다. 릴리스 빌드의 경우 일반적으로 배포하는 환경에 관계없이 디버깅을 사용하지 않도록 설정하려고 합니다. 따라서 기본적으로 Visual Studio 프로젝트 템플릿은 `debug` `compilation` 요소에서 특성을 제거하는 코드를 사용하여 *Web.Release.config* 파일을 만듭니다. 다음은 기본 *Web.Release.config입니다*: 주석이 주석이 있는 일부 샘플 변환 `compilation` 코드 외에도 `debug` 특성을 제거하는 요소의 코드가 포함됩니다.

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

특성은 `xdt:Transform="RemoveAttributes(debug)"` 배포된 `debug` *Web.config* 파일의 요소에서 `system.web/compilation` 특성을 제거할 것을 지정합니다. 이 작업은 릴리스 빌드를 배포할 때마다 수행됩니다.

## <a name="limit-error-log-access-to-administrators"></a>관리자에 대한 오류 로그 액세스 제한

응용 프로그램이 실행되는 동안 오류가 있는 경우 응용 프로그램은 시스템에서 생성된 오류 페이지 대신 일반 오류 페이지를 표시하고 오류 로깅 및 보고에 [Elmah NuGet 패키지를](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) 사용합니다. 응용 `customErrors` 프로그램 *Web.config* 파일의 요소는 오류 페이지를 지정합니다.

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

오류 페이지를 보려면 `mode` `customErrors` 요소의 특성을 일시적으로 "RemoteOnly"에서 "켜기"로 변경하고 Visual Studio에서 응용 프로그램을 실행합니다. *Studentsxxx.aspx*.와 같은 잘못된 URL을 요청하여 오류가 발생합니다. IIS에서 생성한 "리소스를 찾을 수 없음" 오류 페이지 대신 *GenericErrorPage.aspx* 페이지가 표시됩니다.

![오류 페이지](web-config-transformations/_static/image2.png)

오류 로그를 보려면 포트 번호 다음의 URL에 있는 모든 것을 *elmah.axd(예:* `http://localhost:51130/elmah.axd`)로 바꾸고 Enter 키를 누릅니다.

![엘마 페이지](web-config-transformations/_static/image3.png)

완료되면 `customErrors` 요소를 "RemoteOnly" 모드로 다시 설정하는 것을 잊지 마십시오.

개발 컴퓨터에서는 오류 로그 페이지에 무료로 액세스할 수 있지만 프로덕션 환경에서는 보안 위험이 있습니다. 프로덕션 사이트의 경우 관리자에 대한 오류 로그 액세스를 제한하는 권한 부여 규칙을 추가하고 테스트 및 스테이징에서도 제한이 작동하는지 확인하려고 합니다. 따라서 이것은 릴리스 빌드를 배포할 때마다 구현하려는 또 다른 변경 사항이므로 *Web.Release.config* 파일에 속합니다.

*Web.Release.config를* 열고 여기에 `location` 표시된 대로 `configuration` 닫는 태그 바로 앞에 새 요소를 추가합니다.

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

`Transform` "Insert"의 특성 값으로 `location` 인해 이 요소를 `location` *Web.config 파일의* 기존 요소에 형제로 추가됩니다. (이미 업데이트 `location` **크레딧** 페이지에 대한 권한 부여 규칙을 지정하는 요소가 하나 있습니다.)

이제 변환을 미리 보고 올바르게 코딩했는지 확인할 수 있습니다.

**솔루션 탐색기에서** *Web.Release.config를* 마우스 오른쪽 단추로 클릭하고 **변환 미리 보기를**클릭합니다.

![변환 미리 보기 메뉴](web-config-transformations/_static/image4.png)

왼쪽에 있는 개발 *Web.config* 파일과 배포된 *Web.config* 파일이 오른쪽에 표시되는 모양을 보여 주는 페이지가 열리고 변경 내용이 강조 표시됩니다.

![디버그 변환 미리 보기](web-config-transformations/_static/image5.png)

![위치 변환 미리 보기](web-config-transformations/_static/image6.png)

(미리 보기에서 변환을 작성하지 않은 몇 가지 추가 변경 사항을 확인할 수 있습니다. 일반적으로 기능에 영향을 주지 않는 공백을 제거하는 것이 포함됩니다.)

배포 후 사이트를 테스트할 때 권한 부여 규칙이 효과적인지 테스트합니다.

> [!NOTE] 
> 
> **보안 참고 사항** 프로덕션 응용 프로그램에서 오류 세부 정보를 공개하거나 공용 위치에 저장하지 마십시오. 공격자는 오류 정보를 사용하여 사이트의 취약점을 발견할 수 있습니다. 자체 응용 프로그램에서 ELMAH를 사용하는 경우 ELMAH를 구성하여 보안 위험을 최소화합니다. 이 자습서의 ELMAH 예제는 권장되는 구성으로 간주해서는 안 됩니다. 응용 프로그램에서 파일을 만들 수 있어야 하는 폴더를 처리하는 방법을 설명하기 위해 선택한 예제입니다. 자세한 내용은 [ELMAH 끝점 보안을](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)참조하십시오.

## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a>프로필 변환 파일 게시에서 처리할 설정

일반적인 시나리오는 배포하는 각 환경에서 서로 다른 *Web.config* 파일 설정을 갖도록 하는 것입니다. 예를 들어 WCF 서비스를 호출하는 응용 프로그램에는 테스트 및 프로덕션 환경에서 다른 끝점이 필요할 수 있습니다. Contoso 대학 응용 프로그램에는 이러한 종류의 설정도 포함되어 있습니다. 이 설정은 개발, 테스트 또는 프로덕션과 같이 현재 있는 환경을 알려주는 사이트의 페이지에서 표시되는 표시기를 제어합니다. 설정 값은 응용 프로그램이 *Site.Master* 마스터 페이지의 기본 제목에 "(Dev)" 또는 "(Test)"를 더할지 여부를 결정합니다.

![환경 표시기](web-config-transformations/_static/image7.png)

응용 프로그램이 스테이징 또는 프로덕션 환경에서 실행 중일 때 환경 표시기는 생략됩니다.

Contoso University 웹 페이지는 `appSettings` *Web.config* 파일에 설정된 값을 읽고 응용 프로그램이 실행 중인 환경을 확인합니다.

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

값은 테스트 환경에서 "테스트"해야 하며 스테이징 및 프로덕션용은 "Prod"여야 합니다.

변환 파일의 다음 코드는 이 변환을 구현합니다.

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

특성 `xdt:Transform` 값 "SetAttributes"는 이 변환의 목적이 *Web.config* 파일의 기존 요소의 특성 값을 변경하는 것입니다. 특성 `xdt:Locator` 값 "Match(key)"는 수정할 요소가 여기에 지정된 `key` `key` 특성과 일치하는 특성임을 나타냅니다. `add` 요소의 유일한 다른 특성은 `value`에서 배포된 *Web.config* 파일에서 변경됩니다. 여기에 표시된 코드로 `value` 인해 `Environment` `appSettings` 배포된 *Web.config* 파일에서 요소의 특성이 "테스트"로 설정됩니다.

이 변환은 아직 만들지 않은 게시 프로필 변환 파일에 속합니다. 테스트, 스테이징 및 프로덕션 환경에 대한 게시 프로필을 만들 때 이 변경 사항을 구현하는 변환 파일을 만들고 업데이트합니다. [IIS에 배포하고](deploying-to-iis.md) [프로덕션 자습서에 배포합니다.](deploying-to-production.md)

> [!NOTE]
> 이 설정은 `<appSettings>` 요소에 있으므로 이 항목의 이전 항목의 앞에서 Azure의 [Web.config 설정 지정](#watransforms) 참조에서 웹 앱에 배포할 때 변환을 지정하는 또 다른 대안이 있습니다.

## <a name="setting-connection-strings"></a>연결 문자열 설정

기본 변환 파일에는 연결 문자열을 업데이트하는 방법을 보여 주는 예제가 포함되어 있지만 대부분의 경우 게시 프로필에서 연결 문자열을 지정할 수 있으므로 연결 문자열 변환을 설정할 필요가 없습니다. [IIS에 배포하고](deploying-to-iis.md) [프로덕션 자습서에 배포합니다.](deploying-to-production.md)

## <a name="summary"></a>요약

이제 게시 프로필을 만들기 전에 *Web.config* 변환을 사용하여 가능한 한 많은 작업을 수행했으며 배포된 Web.config 파일에 있는 내용을 미리 볼 수 있습니다.

![위치 변환 미리 보기](web-config-transformations/_static/image8.png)

다음 자습서에서는 프로젝트 속성을 설정해야 하는 배포 설정 작업을 처리합니다.

## <a name="more-information"></a>추가 정보

이 자습서에서 다루는 항목에 대한 자세한 내용은 Visual Studio 및 ASP.NET 웹 배포 콘텐츠 [맵에서 배포하는 동안 Web.config 파일 또는 app.config 파일의 설정을 변경하기 위해 Web.config 변환 사용을](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms) 참조하십시오.

> [!div class="step-by-step"]
> [이전](preparing-databases.md)
> [다음](project-properties.md)
