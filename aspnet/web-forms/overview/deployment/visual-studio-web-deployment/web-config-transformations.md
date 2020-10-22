---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: Web.config 파일 변환 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 ASP.NET 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자 (usin ...)에 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: a9d39547c94a63003442ba6fe1257693dde24b05
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345619"
---
# <a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: Web.config 파일 변환

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈에서는 Visual Studio 2012 또는 Visual Studio 2010를 사용 하 여 Azure App Service Web Apps 또는 타사 호스팅 공급자에 게 ASP.NET 웹 응용 프로그램을 배포 (게시) 하는 방법을 보여 줍니다. 계열에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)를 참조 하십시오.

## <a name="overview"></a>개요

이 자습서에서는 다른 대상 환경에 배포할 때 *Web.config* 파일을 변경 하는 프로세스를 자동화 하는 방법을 보여 줍니다. 응용 프로그램을 배포할 때는 대부분의 응용 프로그램에 *Web.config* 파일의 설정이 달라 야 합니다. 이러한 변경을 수행 하는 프로세스를 자동화 하면 배포할 때마다 수동으로 작업을 수행할 필요가 없으며,이는 지루한 오류가 발생 하기 쉽습니다.

미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](troubleshooting.md)를 확인 해야 합니다.

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web.config 변환과 웹 배포 매개 변수 비교

*Web.config* 파일 설정을 변경 하는 프로세스를 자동화 하는 방법에는 [Web.config 변환과](https://msdn.microsoft.com/library/dd465326.aspx) [웹 배포 매개 변수](https://msdn.microsoft.com/library/ff398068.aspx)등 두 가지가 있습니다. *Web.config* 변환 파일은 배포할 때 *Web.config* 파일을 변경 하는 방법을 지정 하는 XML 태그를 포함 합니다. 특정 빌드 구성과 특정 게시 프로필에 대해 서로 다른 변경 내용을 지정할 수 있습니다. 기본 빌드 구성은 디버그 및 릴리스 이며 사용자 지정 빌드 구성을 만들 수 있습니다. 게시 프로필은 일반적으로 대상 환경에 해당 합니다. ( [테스트 환경으로 IIS에 배포](deploying-to-iis.md) 자습서에서 게시 프로필에 대해 자세히 알아봅니다.)

웹 배포 매개 변수는 *Web.config* 파일에 있는 설정을 포함 하 여 배포 중에 구성 해야 하는 다양 한 종류의 설정을 지정 하는 데 사용할 수 있습니다. *Web.config* 파일 변경 내용을 지정 하는 데 사용 하는 경우 웹 배포 매개 변수는 설정 하기 더 복잡 하지만, 배포할 때까지 설정할 값을 알 수 없는 경우에 유용 합니다. 예를 들어 엔터프라이즈 환경에서 *배포 패키지* 를 만들어 it 부서의 사용자에 게 제공 하 여 프로덕션 환경에 설치할 수 있으며, 사용자가 알지 못하는 연결 문자열이 나 암호를 입력할 수 있어야 합니다.

이 자습서 시리즈에 포함 된 시나리오에서는 *Web.config* 파일에 대해 수행 해야 하는 모든 것을 미리 알고 있으므로 웹 배포 매개 변수를 사용할 필요가 없습니다. 사용 되는 빌드 구성에 따라 다르고 사용 되는 게시 프로필에 따라 달라 지는 일부 변환을 구성 합니다.

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a>Azure에서 Web.config 설정 지정

변경 하려는 *Web.config* 파일 설정이 `<connectionStrings>` 또는 `<appSettings>` 요소에 있고 Web Apps를 Azure App Service에 배포 하는 경우 배포 중에 변경 내용을 자동화 하는 또 다른 옵션이 있습니다. 웹 앱에 대 한 관리 포털 페이지의 **구성** 탭에서 Azure에 적용 하려는 설정을 입력할 수 있습니다 ( **앱 설정** 및 **연결 문자열** 섹션까지 아래로 스크롤). 프로젝트를 배포 하면 Azure에서 변경 내용을 자동으로 적용 합니다. 자세한 내용은 [Windows Azure 웹 사이트: 응용 프로그램 문자열 및 연결 문자열 작동 방식](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)을 참조 하세요.

## <a name="default-transformation-files"></a>기본 변환 파일

**솔루션 탐색기**에서 *Web.config* 를 확장 하 여 두 기본 빌드 구성에 대해 기본적으로 생성 되는 *Web.Debug.config* 및 *Web.Release.config* 변환 파일을 볼 수 있습니다.

![Web.config_transform_files](web-config-transformations/_static/image1.png)

Web.config 파일을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 **구성 변환 추가** 를 선택 하 여 사용자 지정 빌드 구성에 대 한 변환 파일을 만들 수 있습니다. 이 자습서에서는 사용자 지정 빌드 구성을 만들지 않았기 때문에이 작업을 수행할 필요가 없으며 메뉴 옵션을 사용할 수 없습니다.

나중에 테스트, 준비 및 프로덕션 게시 프로필에 대해 각각 하나씩 세 개의 변환 파일을 만듭니다. 게시 프로필 변환 파일에서 처리 하는 설정의 일반적인 예는 대상 환경에 따라 달라 지기 때문에 테스트 및 프로덕션에 대해 다른 WCF 끝점입니다. 이후 자습서에서 게시 프로필을 만든 후 게시 프로필 변환 파일을 만듭니다.

## <a name="disable-debug-mode"></a>디버그 모드 사용 안 함

대상 환경이 아닌 빌드 구성에 따라 달라 지는 설정의 예로는 `debug` 특성이 있습니다. 릴리스 빌드의 경우 배포 하는 환경에 관계 없이 디버깅을 사용 하지 않도록 설정 하는 것이 좋습니다. 따라서 기본적으로 Visual Studio 프로젝트 템플릿은 요소에서 특성을 제거 하는 코드를 사용 하 여 *Web.Release.config* 변환 파일을 만듭니다 `debug` `compilation` . 다음은 기본 *Web.Release.config*입니다. 주석 처리 된 일부 샘플 변환 코드 외에도 `compilation` 특성을 제거 하는 요소에 코드를 포함 합니다 `debug` .

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

`xdt:Transform="RemoveAttributes(debug)"`특성은 `debug` 배포 된 `system.web/compilation` *Web.config* 파일의 요소에서 특성을 제거 하도록 지정 합니다. 이 작업은 릴리스 빌드를 배포할 때마다 수행 됩니다.

## <a name="limit-error-log-access-to-administrators"></a>관리자에 대 한 오류 로그 액세스 제한

응용 프로그램을 실행 하는 동안 오류가 발생 하는 경우 응용 프로그램은 시스템 생성 오류 페이지 대신 일반 오류 페이지를 표시 하 고 오류 로깅 및 보고를 위해 [Elmah NuGet 패키지](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) 를 사용 합니다. `customErrors`응용 프로그램 *Web.config* 파일의 요소는 오류 페이지를 지정 합니다.

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

오류 페이지를 보려면 `mode` 요소의 특성을 `customErrors` "RemoteOnly"에서 "On"으로 일시적으로 변경 하 고 Visual Studio에서 응용 프로그램을 실행 합니다. *Studentsxxx*와 같은 잘못 된 URL을 요청 하 여 오류를 발생 시킵니다. IIS에서 생성 된 "리소스를 찾을 수 없습니다" 오류 페이지 대신 *Genericerrorpage .aspx* 페이지가 표시 됩니다.

![오류 페이지](web-config-transformations/_static/image2.png)

오류 로그를 보려면 URL에서 포트 번호 뒤에 있는 모든 항목을 *elmah* (예 `http://localhost:51130/elmah.axd` :)로 바꾸고 enter 키를 누릅니다.

![ELMAH 페이지](web-config-transformations/_static/image3.png)

`customErrors`완료 되 면 요소를 다시 "RemoteOnly" 모드로 설정 해야 합니다.

개발 컴퓨터에서는 오류 로그 페이지에 대 한 무료 액세스를 허용 하는 것이 편리 하지만 프로덕션 환경에서는 보안상 위험할 수 있습니다. 프로덕션 사이트의 경우에는 관리자에 게 오류 로그 액세스를 제한 하는 권한 부여 규칙을 추가 하 고 테스트 및 스테이징에도 제한이 적용 되도록 할 수 있습니다. 따라서이는 릴리스 빌드를 배포할 때마다 구현 하려는 다른 변경 내용으로, *Web.Release.config* 파일에 속합니다.

여기 *Web.Release.config* 에 `location` 표시 된 것 처럼Web.Release.config을 열고 닫는 태그 바로 앞에 새 요소를 추가 합니다 `configuration` .

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

`Transform`"Insert"의 특성 값으로 인해이 `location` 요소가 `location` *Web.config* 파일의 기존 요소에 형제로 추가 됩니다. ( `location` **크레딧 업데이트** 페이지에 대 한 권한 부여 규칙을 지정 하는 요소가 이미 하나 있습니다.)

이제 변환을 미리 보고 올바르게 코딩 되었는지 확인할 수 있습니다.

**솔루션 탐색기**에서 *Web.Release.config* 를 마우스 오른쪽 단추로 클릭 하 고 **변환 미리 보기**를 클릭 합니다.

![변환 메뉴 미리 보기](web-config-transformations/_static/image4.png)

왼쪽에 개발 *Web.config* 파일이 표시 되 고, 배포 된 *Web.config* 파일이 오른쪽에 표시 되 고 변경 내용이 강조 표시 되는 페이지가 열립니다.

![디버그 변환 미리 보기](web-config-transformations/_static/image5.png)

![위치 변환 미리 보기](web-config-transformations/_static/image6.png)

(미리 보기에는 변환을 작성 하지 않은 몇 가지 추가 변경 내용이 표시 될 수 있습니다. 일반적으로이는 기능에 영향을 주지 않는 공백 제거를 포함 합니다.)

배포 후에 사이트를 테스트 하는 경우에도 테스트 하 여 권한 부여 규칙이 적용 되는지 확인 합니다.

> [!NOTE] 
> 
> **보안 정보** 프로덕션 응용 프로그램에서 오류 정보를 공용에 표시 하지 않거나 해당 정보를 공용 위치에 저장 합니다. 공격자는 오류 정보를 사용 하 여 사이트의 취약성을 검색할 수 있습니다. 사용자 고유의 응용 프로그램에서 ELMAH를 사용 하는 경우 보안 위험을 최소화 하도록 ELMAH를 구성 합니다. 이 자습서의 ELMAH 예제는 권장 구성으로 간주 되지 않아야 합니다. 응용 프로그램에서 파일을 만들 수 있어야 하는 폴더를 처리 하는 방법을 설명 하기 위해 선택한 예제입니다. 자세한 내용은 [ELMAH 끝점 보안](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)을 참조 하세요.

## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a>게시 프로필 변환 파일에서 처리할 설정

일반적인 시나리오는에 배포 하는 각 환경에서 *Web.config* 파일 설정이 달라 야 하는 것입니다. 예를 들어 WCF 서비스를 호출 하는 응용 프로그램은 테스트 및 프로덕션 환경에서 다른 끝점을 필요로 할 수 있습니다. Contoso 대학 응용 프로그램에는 이러한 종류의 설정도 포함 되어 있습니다. 이 설정은 현재 개발, 테스트 또는 프로덕션 환경과 같은 환경을 알려 주는 사이트 페이지에서 표시 되는 표시기를 제어 합니다. 설정 값은 응용 프로그램이 사이트의 주 제목에 "(Dev)" 또는 "(Test)"를 추가할지 여부를 결정 합니다 *. 마스터* 마스터 페이지:

![환경 표시기](web-config-transformations/_static/image7.png)

응용 프로그램을 스테이징 또는 프로덕션 환경에서 실행 하는 경우 환경 표시기가 생략 됩니다.

Contoso 대학 웹 페이지는 `appSettings` 응용 프로그램이 실행 되는 환경을 확인 하기 위해 *Web.config* 파일의에 설정 된 값을 읽습니다.

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

값은 테스트 환경에서 "Test"로, 스테이징 및 프로덕션의 경우 "Prod" 여야 합니다.

변환 파일의 다음 코드는이 변환을 구현 합니다.

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

`xdt:Transform`특성 값 "SetAttributes"는이 변환의 목적이 *Web.config* 파일의 기존 요소에 대 한 특성 값을 변경 하는 것을 나타냅니다. `xdt:Locator`특성 값 "Match (key)"는 수정할 요소가 `key` `key` 여기에 지정 된 특성과 일치 하는 특성을 갖는 것을 나타냅니다. 요소의 다른 특성은 이며 `add` `value` 배포 된 *Web.config* 파일에서 변경 됩니다. 여기에 표시 된 코드는 `value` `Environment` `appSettings` 배포 된 *Web.config* 파일에서 요소의 특성을 "Test"로 설정 합니다.

이 변환은 아직 만들지 않은 게시 프로필 변환 파일에 속합니다. 테스트, 스테이징 및 프로덕션 환경에 대 한 게시 프로필을 만들 때이 변경 내용을 구현 하는 변환 파일을 만들고 업데이트 합니다. [IIS에 배포](deploying-to-iis.md) 및 [프로덕션에 배포](deploying-to-production.md) 자습서에서이 작업을 수행 합니다.

> [!NOTE]
> 이 설정이 요소에 있기 때문 `<appSettings>` 에이 항목의 앞부분에 나오는 [Azure에서 Web.config 설정 지정](#watransforms) 을 참조 Azure App Service Web Apps 배포 하는 경우 변환을 지정 하는 또 다른 대안이 있습니다.

## <a name="setting-connection-strings"></a>연결 문자열 설정

기본 변환 파일에는 연결 문자열을 업데이트 하는 방법을 보여 주는 예제가 포함 되어 있지만, 대부분의 경우에는 게시 프로필에서 연결 문자열을 지정할 수 있으므로 연결 문자열 변환을 설정할 필요가 없습니다. [IIS에 배포](deploying-to-iis.md) 및 [프로덕션에 배포](deploying-to-production.md) 자습서에서이 작업을 수행 합니다.

## <a name="summary"></a>요약

이제 게시 프로필을 만들기 전에 *Web.config* 변환에 대해 수행할 수 있는 작업을 완료 했으며 배포 된 Web.config 파일에 포함 될 항목의 미리 보기를 살펴보았습니다.

![위치 변환 미리 보기](web-config-transformations/_static/image8.png)

다음 자습서에서는 프로젝트 속성을 설정 해야 하는 배포 설정 작업을 처리 합니다.

## <a name="more-information"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 Visual Studio 및 ASP.NET 용 웹 배포 콘텐츠 맵에서 [배포 하는 동안 Web.config 변환을 사용 하 여 대상 Web.config 파일 또는 app.config 파일의 설정 변경을](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms) 참조 하세요.

> [!div class="step-by-step"]
> [이전](preparing-databases.md)
> [다음](project-properties.md)
