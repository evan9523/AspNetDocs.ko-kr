---
uid: signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
title: Azure 웹 역할에서 SignalR 성능 카운터 사용 | Microsoft Docs
author: guardrex
description: Azure 웹 역할에서 SignalR 성능 카운터를 설치 하 고 사용 하는 방법입니다.
keywords: ASP.NET, signalr, 성능 카운터, azure 웹 역할
ms.author: bradyg
ms.date: 10/03/2018
ms.assetid: 2a127d3b-21ed-4cc9-bec0-cdab4e742a25
msc.legacyurl: /signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
msc.type: authoredcontent
ms.openlocfilehash: 3de42435887113f93c6b8c36145793952af4d735
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240641"
---
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a>Azure 웹 역할에서 SignalR 성능 카운터 사용

[Luke Latham](https://github.com/guardrex)으로

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

SignalR 성능 카운터는 Azure 웹 역할에서 앱의 성능을 모니터링 하는 데 사용 됩니다. 카운터는 Microsoft Azure 진단에 의해 캡처됩니다. 독립 실행형 또는 온-프레미스 앱에 사용 되는 동일한 도구인 *signalr.exe*를 사용 하 여 Azure에 SignalR 성능 카운터를 설치 합니다. Azure 역할은 일시적 이므로 시작 시 SignalR 성능 카운터를 설치 하 고 등록 하도록 앱을 구성 합니다.

## <a name="prerequisites"></a>필수 조건

* Visual Studio 2015 또는 [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
* [MICROSOFT AZURE sdk For Visual Studio](https://azure.microsoft.com/downloads/) **참고: sdk를 설치한 후 컴퓨터를 다시 시작 합니다.**
* Microsoft Azure 구독: 무료 Azure 평가판 계정에 등록 하려면 [Azure 무료 평가판](https://azure.microsoft.com/free/dotnet/)을 참조 하세요.

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a>SignalR 성능 카운터를 노출 하는 Azure 웹 역할 응용 프로그램 만들기

1. Visual Studio를 엽니다.

2. Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.

3. **새 프로젝트** 대화 상자의 왼쪽에서 **Visual c #**  >  **클라우드** 범주를 선택 하 고 **Azure 클라우드 서비스** 템플릿을 선택 합니다. 앱 이름을 **SignalRPerfCounters** 로 선택 하 고 **확인을**선택 합니다.

   ![새 클라우드 응용 프로그램](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)

   > [!NOTE]
   > **클라우드** 템플릿 범주나 **azure 클라우드 서비스** 템플릿이 표시 되지 않는 경우 Visual Studio 2017에 대 한 **azure 개발** 워크 로드를 설치 해야 합니다. **새 프로젝트** 대화 상자의 왼쪽 아래에 있는 **Visual Studio 설치 관리자 열기** 링크를 선택 하 여 Visual Studio 설치 관리자를 엽니다. **Azure 개발** 워크 로드를 선택한 다음 **수정** 을 선택 하 여 워크 로드 설치를 시작 합니다.
   >
   > ![Visual Studio 설치 관리자의 Azure 개발 워크 로드](using-signalr-performance-counters-in-an-azure-web-role/_static/azure-development-workload.png)

4. **새 Microsoft Azure 클라우드 서비스** 대화 상자에서 **ASP.NET 웹 역할** 을 선택 하 고 > 단추를 선택 하 여 프로젝트에 역할을 추가 합니다. **확인**을 선택합니다.

   ![ASP.NET 웹 역할 추가](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)

5. **New ASP.NET 웹 응용 프로그램-WebRole1** 대화 상자에서 **MVC** 템플릿을 선택 하 고 **확인**을 선택 합니다.

   ![MVC 및 Web API 추가](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)

6. **솔루션 탐색기**에서 **WebRole1**아래에 있는 *diagnostics.wadcfgx* 파일을 엽니다.

   ![솔루션 탐색기 diagnostics.wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)

7. 파일의 내용을 다음 구성으로 바꾸고 파일을 저장 합니다.

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]

8. **도구**NuGet 패키지 관리자에서 **패키지 관리자 콘솔** 을 엽니다  >  **NuGet Package Manager**. 다음 명령을 입력 하 여 최신 버전의 SignalR 및 SignalR 유틸리티 패키지를 설치 합니다.

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]

9. SignalR 성능 카운터를 시작 하거나 재생할 때 역할 인스턴스에 설치 하도록 앱을 구성 합니다. **솔루션 탐색기**에서 **WebRole1** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**  >  **새 폴더**를 선택 합니다. 새 폴더의 이름을 *시작*으로 합니다.

   ![시작 폴더 추가](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)

10. *signalr.exe* **Microsoft.AspNet.SignalR.Utils** \<project folder> /SignalRPerfCounters/packages/Microsoft.AspNet.SignalR.Utils. \<version> 에서signalr.exe파일 (유틸리티 패키지와 함께 추가 됨)을 복사 합니다. /도구는 이전 단계에서 만든 *시작* 폴더에 있습니다.

11. **솔루션 탐색기**에서 *시작* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **Add**  >  **기존 항목**추가를 선택 합니다. 표시 되는 대화 상자에서 *signalr.exe* 를 선택 하 고 **추가**를 선택 합니다.

    ![프로젝트에 signalr.exe 추가](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)

12. 만든 *시작* 폴더를 마우스 오른쪽 단추로 클릭 합니다. **Add**  >  **새 항목**추가를 선택 합니다. **일반** 노드를 선택 하 고 **텍스트 파일**을 선택한 다음 새 항목의 이름을 SignalRPerfCounterInstall로 입력 합니다 *.* 이 명령 파일은 SignalR 성능 카운터를 웹 역할에 설치 합니다.

    ![SignalR 성능 카운터 설치 배치 파일 만들기](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)

13. Visual Studio에서 *SignalRPerfCounterInstall* 파일을 만들면 주 창에서 자동으로 열립니다. 파일의 내용을 다음 스크립트로 바꾼 다음 파일을 저장 하 고 닫습니다. 이 스크립트는 역할 인스턴스에 SignalR 성능 카운터를 추가 하는 *signalr.exe*를 실행 합니다.

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]

14. **솔루션 탐색기**에서 *signalr.exe* 파일을 선택 합니다. 파일의 **속성**에서 **출력 디렉터리로 복사** 를 **항상 복사**로 설정 합니다.

    ![출력 디렉터리로 복사를 항상 복사로 설정](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)

15. *SignalRPerfCounterInstall* 파일에 대해 이전 단계를 반복 합니다.

16. *SignalRPerfCounterInstall* 파일을 마우스 오른쪽 단추로 클릭 하 고 **연결 프로그램**을 선택 합니다. 표시 되는 대화 상자에서 **이진 편집기** 를 선택 하 고 **확인**을 선택 합니다.

    ![이진 편집기를 사용 하 여 열기](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)

17. 이진 편집기에서 파일의 선행 바이트를 선택 하 고 삭제 합니다. 파일을 저장하고 닫습니다.

    ![선행 바이트 삭제](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)

18. 서비스를 시작할 때 *SignalrPerfCounterInstall* 파일을 실행 하는 시작 작업을 추가 *합니다.*

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]

19. `Views/Shared/_Layout.cshtml`파일의 끝에서 jQuery 번들 스크립트를 열고 제거 합니다.

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]

20. 서버에서 메서드를 계속 호출 하는 JavaScript 클라이언트를 추가 `increment` 합니다. 을 열고 `Views/Home/Index.cshtml` 내용을 다음 코드로 바꿉니다.

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]

21. **WebRole1** 프로젝트에서 *허브*라는 새 폴더를 만듭니다. **솔루션 탐색기** 에서 *허브* 폴더를 마우스 오른쪽 단추로 클릭 하 **Add**고  >  **새 항목**추가를 선택 합니다. **새 항목 추가** 대화 상자에서 **Web**  >  **SignalR** 범주를 선택 하 고 **SignalR Hub 클래스 (v2)** 항목 템플릿을 선택 합니다. 새 허브의 이름을 *MyHub.cs* 하 고 **추가**를 선택 합니다.

    ![새 항목 추가 대화 상자의 허브 폴더에 SignalR Hub 클래스 추가](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. *MyHub.cs* 가 주 창에서 자동으로 열립니다. 내용을 다음 코드로 바꾼 다음 파일을 저장 하 고 닫습니다.

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]

23. *[Crank.exe](signalr-connection-density-testing-with-crank.md)* 는 SignalR 코드 베이스와 함께 제공 되는 연결 밀도 테스트 도구입니다. 크랭크에는 영구 연결이 필요 하므로 테스트할 때 사용할 사이트에 하나를 추가 합니다. *PersistentConnections*라는 **WebRole1** 프로젝트에 새 폴더를 추가 합니다. 이 폴더를 마우스 오른쪽 단추로 클릭 하 고 클래스 **추가**를 선택  >  **Class**합니다. 새 클래스 파일의 이름을 *MyPersistentConnections.cs* 로, **추가**를 선택 합니다.

24. Visual Studio가 주 창에서 *MyPersistentConnections.cs* 파일을 엽니다. 내용을 다음 코드로 바꾼 다음 파일을 저장 하 고 닫습니다.

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]

25. 클래스를 사용 하 여 `Startup` SignalR 개체는 OWIN 시작 될 때 시작 됩니다. *Startup.cs* 를 열거나 만들고 내용을 다음 코드로 바꿉니다.

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]

    위의 코드에서 `OwinStartup` 특성은이 클래스를 OWIN 시작으로 표시 합니다. `Configuration`메서드가 SignalR을 시작 합니다.

26. **F5**키를 눌러 Microsoft Azure 에뮬레이터에서 응용 프로그램을 테스트 합니다.

    > [!NOTE]
    > **MapSignalR**에서 **FileLoadException** 이 발생 하는 경우 *web.config* 에서 바인딩 리디렉션을 다음과 같이 변경 합니다.

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]

27. 1 분 정도 기다립니다. Visual Studio에서 클라우드 탐색기 도구 창을 열고 (클라우드 탐색기**보기**  >  **Cloud Explorer**) 경로를 확장 `(Local)/Storage Accounts/(Development)/Tables` 합니다. **WADPerformanceCountersTable**를 두 번 클릭 합니다. 테이블 데이터에 SignalR 카운터가 표시 되어야 합니다. 테이블이 표시 되지 않으면 Azure Storage 자격 증명을 다시 입력 해야 할 수 있습니다. **클라우드 탐색기** 에서 테이블을 확인 하거나 테이블 열기 창에서 **새로 고침** 단추를 선택 하 여 테이블의 데이터를 표시 하려면 **새로 고침** 단추를 선택 해야 할 수 있습니다.

    ![Visual Studio 클라우드 탐색기에서 WAD 성능 카운터 표 선택](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![WAD 성능 카운터 테이블에 수집 된 카운터 표시](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)

28. 클라우드에서 응용 프로그램을 테스트 하려면 **serviceconfiguration.cscfg** 파일을 업데이트 하 고를 `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` 유효한 Azure Storage 계정 연결 문자열로 설정 합니다.

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. 응용 프로그램을 Azure 구독에 배포 합니다. Azure에 응용 프로그램을 배포 하는 방법에 대 한 자세한 내용은 [클라우드 서비스를 만들고 배포 하는 방법](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)을 참조 하세요.

30. 잠시 기다립니다. **클라우드 탐색기**에서 위에서 구성한 저장소 계정을 찾고 `WADPerformanceCountersTable` 여기에서 테이블을 찾습니다. 테이블 데이터에 SignalR 카운터가 표시 되어야 합니다. 테이블이 표시 되지 않으면 Azure Storage 자격 증명을 다시 입력 해야 할 수 있습니다. **클라우드 탐색기** 에서 테이블을 확인 하거나 테이블 열기 창에서 **새로 고침** 단추를 선택 하 여 테이블의 데이터를 표시 하려면 **새로 고침** 단추를 선택 해야 할 수 있습니다.

이 자습서에서 사용 되는 원래 콘텐츠에 대해 [Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) 를 사용 합니다.
