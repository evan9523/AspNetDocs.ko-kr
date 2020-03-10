---
uid: aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
title: Azure 작업자 역할의 호스트 OWIN | Microsoft Docs
author: MikeWasson
description: 이 자습서에서는 Microsoft Azure 작업자 역할에서 OWIN를 자체 호스트 하는 방법을 보여 줍니다. OWIN (Open Web Interface for .NET)는 .NET 웹 서버 간의 추상화를 정의 합니다.
ms.author: riande
ms.date: 04/11/2014
ms.assetid: 07aa855a-92ee-4d43-ba66-5bfd7de20ee6
msc.legacyurl: /aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 59d2e0d549427093f8a2424b17af81169b78ef30
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472397"
---
# <a name="host-owin-in-an-azure-worker-role"></a>Azure 작업자 역할에 OWIN 호스트

[Mike Wasson](https://github.com/MikeWasson)

> 이 자습서에서는 Microsoft Azure 작업자 역할에서 OWIN를 자체 호스트 하는 방법을 보여 줍니다.
>
> OWIN ( [Open Web Interface for .net](http://owin.org/) )는 .net 웹 서버와 웹 응용 프로그램 간의 추상화를 정의 합니다. OWIN는 서버에서 웹 응용 프로그램을 분리 하 여 IIS 외부 (예: Azure 작업자 역할 내부)에서 웹 응용 프로그램을 자체 호스트 하는 데 적합 합니다.
>
> 이 자습서에서는 Microsoft Azure 작업자 역할 내에서 OWIN 응용 프로그램을 자체 호스트 하는 방법에 대해 알아봅니다. 작업자 역할에 대해 자세히 알아보려면 [Azure 실행 모델](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices)을 참조 하세요.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - [.NET 용 Azure SDK 2.3](https://azure.microsoft.com/downloads/)
> - [Owin. Selfhost 2.1.0](http://www.nuget.org/packages/Microsoft.Owin.SelfHost/2.1.0)

## <a name="create-a-microsoft-azure-project"></a>Microsoft Azure 프로젝트 만들기

관리자 권한으로 Visual Studio를 시작 합니다. Azure 계산 에뮬레이터를 사용 하 여 응용 프로그램을 로컬로 디버깅 하려면 관리자 권한이 필요 합니다.

**파일** 메뉴에서 **새로 만들기**를 클릭 한 다음 **프로젝트**를 클릭 합니다. **설치 된 템플릿**의 시각적 개체 C#에서 **클라우드** 를 클릭 한 다음 **Windows Azure 클라우드 서비스**를 클릭 합니다. 프로젝트 이름을 "AzureApp"으로 선택 하 고 **확인**을 클릭 합니다.

[![](host-owin-in-an-azure-worker-role/_static/image2.png)](host-owin-in-an-azure-worker-role/_static/image1.png)

**새 Windows Azure 클라우드 서비스** 대화 상자에서 **작업자 역할**을 두 번 클릭 합니다. 기본 이름 ("WorkerRole1")을 그대로 둡니다. 이 단계에서는 솔루션에 작업자 역할을 추가 합니다. **확인**을 클릭합니다.

[![](host-owin-in-an-azure-worker-role/_static/image4.png)](host-owin-in-an-azure-worker-role/_static/image3.png)

생성 되는 Visual Studio 솔루션에는 두 개의 프로젝트가 포함 됩니다.

- &quot;AzureApp&quot;는 Azure 응용 프로그램에 대 한 역할 및 구성을 정의 합니다.
- &quot;WorkerRole1&quot;에는 작업자 역할에 대 한 코드가 포함 되어 있습니다.

일반적으로이 자습서에서는 단일 역할을 사용 하지만 Azure 응용 프로그램에는 여러 역할이 포함 될 수 있습니다.

![](host-owin-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-owin-self-host-packages"></a>OWIN 자체 호스트 패키지 추가

**도구** 메뉴에서 **NuGet 패키지 관리자**를 클릭 한 다음 **패키지 관리자 콘솔**을 클릭 합니다.

패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.

[!code-console[Main](host-owin-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a>HTTP 끝점 추가

솔루션 탐색기에서 AzureApp 프로젝트를 확장 합니다. 역할 노드를 확장 하 고 WorkerRole1를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 선택 합니다.

![](host-owin-in-an-azure-worker-role/_static/image6.png)

**엔드포인트**를 클릭한 다음, **엔드포인트 추가**를 클릭합니다.

**프로토콜** 드롭다운 목록에서 "http"를 선택 합니다. **공용 포트** 및 **개인 포트**에 80을 입력 합니다. 이러한 포트 번호는 다를 수 있습니다. 공용 포트는 역할에 요청을 보낼 때 클라이언트에서 사용 하는 것입니다.

[![](host-owin-in-an-azure-worker-role/_static/image8.png)](host-owin-in-an-azure-worker-role/_static/image7.png)

## <a name="create-the-owin-startup-class"></a>OWIN 시작 클래스 만들기

솔루션 탐색기에서 WorkerRole1 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 / **클래스** **추가** 를 선택 하 여 새 클래스를 추가 합니다. 클래스 `Startup` 이름을 지정합니다.

모든 상용구 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample2.cs)]

`UseWelcomePage` 확장 메서드는 응용 프로그램에 간단한 HTML 페이지를 추가 하 여 사이트가 작동 하는지 확인 합니다.

## <a name="start-the-owin-host"></a>OWIN 호스트 시작

WorkerRole.cs 파일을 엽니다. 이 클래스는 작업자 역할이 시작 및 중지 될 때 실행 되는 코드를 정의 합니다.

다음 using 문을 추가합니다.

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample3.cs)]

`WorkerRole` 클래스에 **IDisposable** 멤버를 추가 합니다.

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample4.cs)]

`OnStart` 메서드에서 호스트를 시작 하는 다음 코드를 추가 합니다.

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample5.cs?highlight=5)]

**WebApp** 메서드는 OWIN 호스트를 시작 합니다. `Startup` 클래스의 이름은 메서드의 형식 매개 변수입니다. 규칙에 따라 호스트는이 클래스의 `Configure` 메서드를 호출 합니다.

`OnStop`를 재정의 하 여 *\_app* instance를 삭제 합니다.

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample6.cs)]

WorkerRole.cs에 대 한 전체 코드는 다음과 같습니다.

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample7.cs)]

솔루션을 빌드하고 F5 키를 눌러 Azure 계산 에뮬레이터에서 응용 프로그램을 로컬로 실행 합니다. 방화벽 설정에 따라 에뮬레이터를 방화벽을 통해 허용 해야 할 수도 있습니다.

계산 에뮬레이터는 끝점에 로컬 IP 주소를 할당 합니다. 계산 에뮬레이터 UI를 확인 하 여 IP 주소를 찾을 수 있습니다. 작업 표시줄 알림 영역에서 에뮬레이터 아이콘을 마우스 오른쪽 단추로 클릭 하 고 **계산 에뮬레이터 UI 표시**를 선택 합니다.

[![](host-owin-in-an-azure-worker-role/_static/image10.png)](host-owin-in-an-azure-worker-role/_static/image9.png)

서비스 배포, 배포 [id], 서비스 세부 정보에서 IP 주소를 찾습니다. 웹 브라우저를 열고 http:\/\/*주소로*이동 합니다. 여기서 *address* 는 계산 에뮬레이터에서 할당 한 IP 주소입니다. 예를 들어 `http://127.0.0.1:80`합니다. OWIN 시작 페이지가 표시 됩니다.

![](host-owin-in-an-azure-worker-role/_static/image11.png)

## <a name="deploy-to-azure"></a>Deploy to Azure

이 단계에서는 Azure 계정이 있어야 합니다. 아직 없는 경우 몇 분만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Microsoft Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)을 참조 하세요.

솔루션 탐색기에서 AzureApp 프로젝트를 마우스 오른쪽 단추로 클릭 합니다. **게시**를 선택합니다.

![](host-owin-in-an-azure-worker-role/_static/image12.png)

Azure 계정에 로그인 하지 않은 경우 **로그인**을 클릭 합니다.

[![](host-owin-in-an-azure-worker-role/_static/image14.png)](host-owin-in-an-azure-worker-role/_static/image13.png)

로그인 한 후 구독을 선택 하 고 **다음**을 클릭 합니다.

[![](host-owin-in-an-azure-worker-role/_static/image16.png)](host-owin-in-an-azure-worker-role/_static/image15.png)

클라우드 서비스의 이름을 입력 하 고 지역을 선택 합니다. **만들기**를 클릭합니다.

![](host-owin-in-an-azure-worker-role/_static/image17.png)

**게시**를 클릭합니다.

[![](host-owin-in-an-azure-worker-role/_static/image19.png)](host-owin-in-an-azure-worker-role/_static/image18.png)

Azure 활동 로그 창에는 배포 진행률이 표시 됩니다. 앱이 배포 되 면 `http://appname.cloudapp.net/`로 이동 합니다. 여기서 *appname* 은 클라우드 서비스의 이름입니다.

## <a name="additional-resources"></a>추가 리소스

- [프로젝트 Katana 개요](an-overview-of-project-katana.md)
- [GitHub의 Katana 프로젝트](https://github.com/aspnet/AspNetKatana/)
