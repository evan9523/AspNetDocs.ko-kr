---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
title: 웹 배포 게시용 웹 서버 구성 (원격 에이전트) | Microsoft Docs
author: jrjlee
description: 이 항목에서는 iis 웹 배포를 사용 하 여 웹 게시 및 배포를 지원 하도록 인터넷 정보 서비스 (IIS) 웹 서버를 구성 하는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 239c7aa8-d09a-4d02-9c0e-6bd52be5f0d5
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
msc.type: authoredcontent
ms.openlocfilehash: 39064045bccfe01d00ded60df17f1e152e5c1190
ms.sourcegitcommit: 4ed0b65ae32d9f35e42ee6296b877747e063df4d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90609680"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-remote-agent"></a>웹 배포 게시용 웹 서버 구성(원격 에이전트)

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 iis (웹 배포) 원격 에이전트 서비스를 사용 하 여 웹 게시 및 배포를 지원 하도록 인터넷 정보 서비스 (IIS) 웹 서버를 구성 하는 방법에 대해 설명 합니다.
> 
> 웹 배포 2.0 이상에서 작업 하는 경우 응용 프로그램 또는 사이트를 웹 서버로 가져오는 데 사용할 수 있는 세 가지 주요 방법이 있습니다. 다음과 같습니다.
> 
> - *웹 배포 원격 에이전트 서비스*를 사용 합니다. 이 방법을 사용 하려면 웹 서버를 구성 해야 하지만 서버에 모든 항목을 배포 하려면 로컬 서버 관리자의 자격 증명을 제공 해야 합니다.
> - *웹 배포 처리기*를 사용 합니다. 이 방법은 훨씬 복잡 하며 웹 서버를 설정 하는 데 더 많은 초기 노력이 필요 합니다. 그러나이 방법을 사용 하면 관리자가 아닌 사용자가 배포를 수행할 수 있도록 IIS를 구성할 수 있습니다. 웹 배포 처리기는 IIS 버전 7 이상 에서만 사용할 수 있습니다.
> - *오프 라인 배포*를 사용 합니다. 이 방법을 사용 하려면 웹 서버를 최소한으로 구성 해야 하지만 서버 관리자는 웹 패키지를 서버에 수동으로 복사 하 여 IIS 관리자를 통해 가져와야 합니다.
> 
> 이러한 접근 방식의 주요 기능, 장점 및 단점에 대 한 자세한 내용은 [웹 배포에 대 한 올바른 접근 방법 선택](choosing-the-right-approach-to-web-deployment.md)을 참조 하세요.

## <a name="is-the-web-deploy-remote-agent-the-right-approach-for-you"></a>웹 배포 원격 에이전트가 올바른 방법 입니까?

예, 콘텐츠를 배포 하는 사용자가 대상 서버에서 관리자의 자격 증명을 제공할 수 있습니다. 이 방법은 다음과 같은 시나리오에서 유용한 경우가 많습니다.

- 개발 또는 테스트 환경. 개발자는 대상 웹 서버와 데이터베이스 서버에 대 한 모든 권한을 가집니다.
- 단일 사용자 또는 소규모 사용자 그룹이 전체 응용 프로그램 수명 주기를 제어 하는 소규모 조직

대규모의 많은 조직에서 특히 스테이징 또는 프로덕션 환경에서 사용자에 게 웹 서버에 대 한 관리자 권한을 부여 하는 것은 현실적이 지 않습니다. 호스트 된 웹 서버의 경우이 경우에는 특히 그렇습니다. 또한 빌드 서버에서 배포를 자동화 하려는 경우 배포 프로세스에 관리자 자격 증명을 사용 하지 않는 것이 좋습니다. 이러한 시나리오에서는 [웹 배포 처리기](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md) 를 사용 하 여 배포를 지원 하도록 웹 서버를 구성 하는 것이 더 적절 한 선택입니다.

## <a name="task-overview"></a>작업 개요

이 항목에서는 웹 배포 원격 에이전트 접근 방법을 사용 하 여 원격 컴퓨터에서 웹 패키지를 수락 및 배포 하도록 인터넷 정보 서비스 (IIS) 7.5 웹 서버를 구성 하는 방법에 대해 설명 합니다. 다음 작업을 수행 해야 합니다.

- IIS 7.5 및 IIS 7 권장 구성을 설치 합니다.
- 웹 배포 2.1 이상 버전을 설치 합니다.
- 배포 된 콘텐츠를 호스팅하는 IIS 웹 사이트를 만듭니다.
- 웹 Deployment Agent 서비스가 실행 중인지 확인 합니다.

특히 샘플 솔루션을 호스트 하려면 다음을 수행 해야 합니다.

- .NET Framework 4.0을 설치 합니다.
- ASP.NET MVC 3을 설치 합니다.

이 항목에서는 이러한 각 절차를 수행 하는 방법을 보여 줍니다. 이 항목의 작업 및 연습에서는 Windows Server 2008 r 2를 실행 하는 클린 서버 빌드를 시작 한다고 가정 합니다. 계속 하기 전에 다음을 확인 하십시오.

- Windows Server 2008 R2 서비스 팩 1 및 사용 가능한 모든 업데이트가 설치 되어 있습니다.
- 서버가 도메인에 가입 되어 있습니다.
- 서버에 고정 IP 주소가 있습니다.

> [!NOTE]
> 컴퓨터를 도메인에 가입 하는 방법에 대 한 자세한 내용은 [도메인에 컴퓨터 가입 및 로그온](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)을 참조 하세요. 고정 IP 주소를 구성 하는 방법에 대 한 자세한 내용은 [고정 Ip 주소 구성](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)을 참조 하세요. 원격 에이전트 서비스는 IIS 6부터 지원 되며 도메인에 가입할 필요가 없습니다. 그러나이 자습서의 단계는 IIS 7.5에서 개발 및 테스트 되었으며 다른 버전의 절차는 달라질 수 있습니다.

## <a name="install-products-and-components"></a>제품 및 구성 요소 설치

이 섹션에서는 웹 서버에 필요한 제품 및 구성 요소를 설치 하는 과정을 안내 합니다. 시작 하기 전에 Windows 업데이트를 실행 하 여 서버가 최신 상태 인지 확인 하는 것이 좋습니다.

이 경우 다음 항목을 설치 해야 합니다.

- **IIS 7 권장 구성**. 웹 서버에서 **웹 서버 (iis)** 역할을 사용 하도록 설정 하 고 ASP.NET 응용 프로그램을 호스트 하기 위해 필요한 iis 모듈 및 구성 요소 집합을 설치 합니다.
- **.NET Framework 4.0**. 이는이 버전의 .NET Framework에서 빌드된 응용 프로그램을 실행 하는 데 필요 합니다.
- **웹 배포 도구 2.1**이상. 그러면 웹 배포 (및 해당 기본 실행 파일 MSDeploy.exe)가 서버에 설치 됩니다. 이 프로세스의 일부로 웹 Deployment Agent 서비스를 설치 하 고 시작 합니다. 이 서비스를 사용 하면 원격 컴퓨터에서 웹 패키지를 배포할 수 있습니다.
- **ASP.NET MVC 3**. 그러면 MVC 3 응용 프로그램을 실행 하는 데 필요한 어셈블리가 설치 됩니다.

> [!NOTE]
> 이 연습에서는 웹 플랫폼 설치 관리자를 사용 하 여 필수 구성 요소를 설치 하 고 구성 하는 방법을 설명 합니다. 웹 플랫폼 설치 관리자를 사용할 필요는 없지만 종속성을 자동으로 감지 하 고 항상 최신 제품 버전을 확보 하 여 설치 프로세스를 간소화 합니다. 자세한 내용은 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/?linkid=9805118)을 참조 하세요.

**필요한 제품 및 구성 요소를 설치 하려면**

1. [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9805118)를 다운로드 하 여 설치 합니다.
2. 설치가 완료 되 면 웹 플랫폼 설치 관리자가 자동으로 시작 됩니다.

    > [!NOTE]
    > 이제 언제 든 지 **시작** 메뉴에서 웹 플랫폼 설치 관리자를 시작할 수 있습니다. 이렇게 하려면 **시작** 메뉴에서 **모든 프로그램**을 클릭 한 다음 **Microsoft 웹 플랫폼 설치 관리자**를 클릭 합니다.
3. **웹 플랫폼 설치 관리자 3.0** 창의 위쪽에서 **제품**을 클릭 합니다.
4. 창의 왼쪽에 있는 탐색 창에서 **프레임 워크**를 클릭 합니다.
5. **Microsoft .NET Framework 4** 행에서 .NET Framework이 아직 설치 되지 않은 경우 **추가**를 클릭 합니다.

    > [!NOTE]
    > Windows 업데이트를 통해 .NET Framework 4.0를 이미 설치 했을 수 있습니다. 제품 또는 구성 요소가 이미 설치 되어 있는 경우 웹 플랫폼 설치 관리자는 **추가** 단추를 **설치**된 텍스트로 바꿔이를 표시 합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image1.png)
6. **ASP.NET MVC 3 (Visual Studio 2010)** 행에서 **추가**를 클릭 합니다.
7. 탐색 창에서 **서버**를 클릭 합니다.
8. **IIS 7 권장 구성** 행에서 **추가**를 클릭 합니다.
9. **웹 배포 도구 2.1** 행에서 **추가**를 클릭 합니다.
10. **설치**를 클릭합니다. 웹 플랫폼 설치 관리자는 설치&#x2014;연결 된 종속성과 함께&#x2014;제품 목록과 사용 조건에 동의 하 라는 메시지를 표시 합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image2.png)
11. 사용 약관을 검토 하 고 약관에 동의 하는 경우 동의 **함**을 클릭 합니다.
12. 설치가 완료 되 면 **마침**을 클릭 하 고 **웹 플랫폼 설치 관리자 3.0** 창을 닫습니다.

IIS를 설치 하기 전에 .NET Framework 4.0를 설치한 경우 ASP.NET의 최신 버전을 IIS에 등록 하려면 [ASP.NET IIS 등록 도구](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnetregiis.exe)를 실행 해야 합니다 \_ . 이렇게 하지 않으면 IIS에서 문제 없이 정적 콘텐츠 (HTML 파일)를 제공 하는 것을 알 수 있지만 ASP.NET 콘텐츠를 검색 하려고 할 때에는 **HTTP 오류 404.0 – 찾을** 수 없음이 반환 됩니다. 이 절차를 사용 하 여 ASP.NET 4.0이 등록 되었는지 확인할 수 있습니다.

**IIS에 ASP.NET 4.0를 등록 하려면**

1. **시작**을 클릭 한 다음 **명령 프롬프트**를 입력 합니다.
2. 검색 결과에서 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 한 다음 **관리자 권한으로 실행**을 클릭 합니다.
3. 명령 프롬프트 창에서 **\ v 4.0.30319** 디렉터리로 이동 합니다.
4. 다음 명령을 입력 하 고 Enter 키를 누릅니다.

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample1.cmd)]
5. 어느 시점에서 든 64 비트 웹 응용 프로그램을 호스트 하려는 경우 ASP.NET의 64 비트 버전을 IIS에 등록 해야 합니다. 이렇게 하려면 명령 프롬프트 창에서 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** 디렉터리로 이동 합니다.
6. 다음 명령을 입력 하 고 Enter 키를 누릅니다.

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample2.cmd)]

지금까지 Windows 업데이트를 사용 하 여 설치한 새 제품 및 구성 요소에 대 한 사용 가능한 업데이트를 다운로드 하 고 설치 하는 것이 좋습니다.

## <a name="configure-the-iis-website"></a>IIS 웹 사이트 구성

웹 콘텐츠를 서버에 배포 하려면 먼저 콘텐츠를 호스팅하는 IIS 웹 사이트를 만들고 구성 해야 합니다. 웹 배포는 기존 IIS 웹 사이트에만 웹 패키지를 배포할 수 있습니다. 웹 사이트를 만들 수 없습니다. 개략적인 수준에서 다음 작업을 완료 해야 합니다.

- 콘텐츠를 호스트할 파일 시스템에 폴더를 만듭니다.
- 콘텐츠를 제공 하는 IIS 웹 사이트를 만들고 로컬 폴더에 연결 합니다.
- 로컬 폴더의 응용 프로그램 풀 id에 대 한 읽기 권한을 부여 합니다.

IIS의 기본 웹 사이트에 콘텐츠를 배포 하는 것은 아무 작업도 수행 하지 않지만 테스트 또는 데모 시나리오 이외의 다른 항목에는이 방법을 사용 하지 않는 것이 좋습니다. 프로덕션 환경을 시뮬레이트하려면 응용 프로그램의 요구 사항과 관련 된 설정을 사용 하 여 새 IIS 웹 사이트를 만들어야 합니다.

**IIS 웹 사이트를 만들고 구성 하려면**

1. 로컬 파일 시스템에서 콘텐츠를 저장할 폴더를 만듭니다 (예: **C:\demosite**).
2. **시작** 메뉴에서 **관리 도구**를 가리킨 다음 **인터넷 정보 서비스 (IIS) 관리자**를 클릭 합니다.
3. IIS 관리자의 **연결** 창에서 서버 노드를 확장 합니다 (예: **TESTWEB1**).

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image3.png)
4. **사이트** 노드를 마우스 오른쪽 단추로 클릭 한 다음 **웹 사이트 추가**를 클릭 합니다.
5. **사이트 이름** 상자에 IIS 웹 사이트의 이름을 입력 합니다 (예: **demosite**).
6. **실제 경로** 상자에 로컬 폴더 경로 (예: **c:\demosite**)를 입력 하거나 해당 경로를 찾습니다.
7. **포트** 상자에 웹 사이트를 호스트 하려는 포트 번호 (예: **85**)를 입력 합니다.

    > [!NOTE]
    > 표준 포트 번호는 HTTP의 경우 80이 고 HTTPS의 경우 443입니다. 그러나 포트 80에서이 웹 사이트를 호스팅하는 경우 사이트에 액세스 하려면 먼저 기본 웹 사이트를 중지 해야 합니다.
8. 웹 사이트에 대 한 DNS (Domain Name System) 레코드를 구성 하려는 경우가 아니면 **호스트 이름** 상자를 비워 둡니다. 그런 다음 **확인**을 클릭 합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image4.png)

    > [!NOTE]
    > 프로덕션 환경에서는 포트 80에서 웹 사이트를 호스트 하 고 일치 하는 DNS 레코드와 함께 호스트 헤더를 구성할 수 있습니다. IIS 7에서 호스트 헤더를 구성 하는 방법에 대 한 자세한 내용은 [웹 사이트의 호스트 헤더 구성 (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx)을 참조 하십시오. Windows Server 2008 r 2의 DNS 서버 역할에 대 한 자세한 내용은 [Dns 서버 개요](https://technet.microsoft.com/library/cc770392.aspx) 및 [dns 서버](https://technet.microsoft.com/windowsserver/dd448607)를 참조 하세요.
9. **작업** 창의 **사이트 편집**에서 **바인딩**을 클릭합니다.
10. **사이트 바인딩** 대화 상자에서 **추가**를 클릭합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image5.png)
11. **사이트 바인딩 추가** 대화 상자에서 기존 사이트 구성과 일치 하는 **IP 주소** 및 **포트** 를 설정 합니다.
12. **호스트 이름** 상자에 웹 서버의 이름 (예: **TESTWEB1**)을 입력 한 다음 **확인**을 클릭 합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image6.png)

    > [!NOTE]
    > 첫 번째 사이트 바인딩을 사용 하면 IP 주소와 포트 또는를 사용 하 여 로컬에서 사이트에 액세스할 수 있습니다 `http://localhost:85` . 두 번째 사이트 바인딩을 사용 하면 컴퓨터 이름 (예:)을 사용 하 여 도메인에 있는 다른 컴퓨터에서 사이트에 액세스할 수 있습니다 http://testweb1:85) .
13. **사이트 바인딩** 대화 상자에서 **닫기**를 클릭합니다.
14. **연결** 창에서 **애플리케이션 풀**을 클릭합니다.
15. **응용 프로그램 풀** 창에서 응용 프로그램 풀의 이름을 마우스 오른쪽 단추로 클릭 한 다음 **기본 설정**을 클릭 합니다. 기본적으로 응용 프로그램 풀의 이름은 웹 사이트의 이름 (예: **Demosite**)과 일치 합니다.
16. **.NET Framework 버전** 목록에서 **.NET Framework v 4.0.30319**를 선택한 다음 **확인**을 클릭 합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image7.png)

    > [!NOTE]
    > 샘플 솔루션에는 .NET Framework 4.0가 필요 합니다. 이는 일반적으로 웹 배포 필요 하지 않습니다.

웹 사이트가 콘텐츠를 제공 하기 위해 응용 프로그램 풀 id에 콘텐츠를 저장 하는 로컬 폴더에 대 한 읽기 권한이 있어야 합니다. IIS 7.5에서 응용 프로그램 풀은 기본적으로 고유한 응용 프로그램 풀 id로 실행 됩니다 (응용 프로그램 풀은 일반적으로 Network Service 계정을 사용 하 여 실행 되는 이전 버전의 IIS와 대조). 응용 프로그램 풀 id는 실제 사용자 계정이 아니므로 대신 사용자 또는&#x2014;그룹 목록에 표시 되지 않습니다. 대신 응용 프로그램 풀이 시작 될 때 동적으로 생성 됩니다. 각 응용 프로그램 풀 id는 로컬 **IIS \_ iusrs** 보안 그룹에 숨겨진 항목으로 추가 됩니다.

파일이 나 폴더에서 응용 프로그램 풀 id에 대 한 사용 권한을 부여 하려면 다음 두 가지 옵션을 사용할 수 있습니다.

- **Iis AppPool \[ 응용 프로그램 풀 이름** 형식 (예: **iis AppPool\DemoSite**)을 사용 하 여 응용 프로그램 풀 id에 직접 사용 권한을 할당 합니다.
- **IIS \_ iusrs** 그룹에 사용 권한을 할당 합니다.

가장 일반적인 방법은 로컬 **IIS \_ iusrs** 그룹에 사용 권한을 할당 하는 것입니다 .이 방법을 사용 하면 파일 시스템 권한을 다시 구성 하지 않고 응용 프로그램 풀을 변경할 수 있습니다. 다음 절차에서는이 그룹 기반 방법을 사용 합니다.

> [!NOTE]
> IIS 7.5의 응용 프로그램 풀 id에 대 한 자세한 내용은 [응용 프로그램 풀 id](https://go.microsoft.com/?linkid=9805123)를 참조 하십시오.

**IIS 웹 사이트에 대 한 폴더 사용 권한을 구성 하려면**

1. Windows 탐색기에서 로컬 폴더의 위치로 이동 합니다.
2. 폴더를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.
3. **Security** 탭에서 **Edit**을 클릭한 다음 **Add**를 클릭합니다.
4. **위치**를 클릭합니다. **위치** 대화 상자에서 로컬 서버를 선택 하 고 **확인**을 클릭 합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image8.png)
5. **사용자 또는 그룹 선택** 대화 상자에서 **IIS \_ iusrs**를 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.
6. **에 대 한 사용 권한 (폴더 이름) 대화 상자**에서 새 그룹에 **읽기 & 실행**, **폴더 내용**보기 및 기본적으로 **읽기** 권한이 할당 된 것을 확인할 수 있습니다. 이를 변경 되지 않은 상태로 두고 **확인**을 클릭 합니다.
7. **확인** 을 클릭 하 여 **(폴더 이름) 속성** 대화 상자를 닫습니다.

서버에 웹 패키지를 배포 하기 전에 최종 작업으로 웹 Deployment Agent 서비스가 실행 되 고 있는지 확인 해야 합니다. 원격 컴퓨터에서 패키지를 배포 하는 경우 웹 Deployment Agent 서비스는 패키지의 콘텐츠를 추출 하 고 설치 하는 일을 담당 합니다. 이 서비스는 웹 배포 도구를 설치 하 고 네트워크 서비스 id로 실행 하는 경우 기본적으로 시작 됩니다.

다양 한 명령줄 유틸리티나 Windows PowerShell cmdlet을 사용 하 여 서비스가 여러 다른 방법으로 실행 되 고 있는지 확인할 수 있습니다. 이 절차에서는 간단한 UI 기반 접근 방식을 설명 합니다.

**웹 Deployment Agent 서비스가 실행 중인지 확인 하려면**

1. **시작** 메뉴에서 **관리 도구**를 가리킨 다음 **서비스**를 클릭합니다.
2. **웹 Deployment Agent 서비스** 행을 찾아 **상태가** **시작**됨으로 설정 되어 있는지 확인 합니다.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image9.png)
3. 서비스가 아직 시작 되지 않았으면 **시작**을 클릭 합니다.

## <a name="configure-firewall-exceptions"></a>방화벽 예외 구성

기본적으로 원격 에이전트 서비스는 다음 URL에서 TCP 포트 80에서 수신 대기 합니다.

<http://servername.com/MSDEPLOYAGENTSERVICE>

대부분의 경우 웹 서버는 일반적으로 포트 80에서 HTTP 요청을 수신 하기 때문에 원격 에이전트 서비스에 대해 추가 방화벽 규칙을 구성할 필요가 없습니다. 비표준 포트에서 수신 하도록 설치를 사용자 지정한 경우 필요에 따라 방화벽 예외를 구성 해야 합니다.

## <a name="conclusion"></a>결론

이 시점에서 웹 서버는 원격 컴퓨터에서 웹 패키지를 수락 하 고 설치할 준비가 된 것입니다. 서버에 웹 응용 프로그램을 배포 하기 전에 다음과 같은 주요 사항을 확인 하는 것이 좋습니다.

- ASP.NET 4.0를 IIS에 등록 했습니까?
- 응용 프로그램 풀 id에 웹 사이트의 원본 폴더에 대 한 읽기 권한이 있나요?
- 웹 Deployment Agent 서비스를 실행 하 고 있습니까?

## <a name="further-reading"></a>추가 정보

사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 구성 하 여 원격 에이전트 서비스에 웹 패키지를 배포 하는 방법에 대 한 지침은 [대상 환경에 대 한 배포 속성 구성](configuring-deployment-properties-for-a-target-environment.md)을 참조 하세요.

> [!div class="step-by-step"]
> [이전](scenario-configuring-a-production-environment-for-web-deployment.md)
> [다음](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
