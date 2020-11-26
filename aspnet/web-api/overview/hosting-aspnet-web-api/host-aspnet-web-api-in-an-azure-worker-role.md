---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: Azure 작업자 역할의 호스트 ASP.NET Web API 2-ASP.NET 4.x
author: MikeWasson
description: '자습서: OWIN를 사용 하 여 Web API 프레임 워크를 자체 호스트 하는 Azure 작업자 역할의 ASP.NET Web API를 호스팅합니다.'
ms.author: riande
ms.date: 04/02/2014
ms.custom: seoapril2019
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 06bd33a7d30ab38d851d929d72ae8c539e16873c
ms.sourcegitcommit: 4b78855427f1397df0a7be3559e04ec94a78c308
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96151908"
---
# <a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a>Azure 작업자 역할의 호스트 ASP.NET Web API 2

[Mike Wasson](https://github.com/MikeWasson)

> 이 자습서에서는 OWIN를 사용 하 여 Web API 프레임 워크를 자체 호스트 하는 Azure 작업자 역할의 ASP.NET Web API를 호스트 하는 방법을 보여 줍니다.
>
> OWIN ( [Open Web Interface for .net](http://owin.org/) )는 .net 웹 서버와 웹 응용 프로그램 간의 추상화를 정의 합니다. OWIN는 서버에서 웹 응용 프로그램을 분리 하 여 IIS 외부 (예: Azure 작업자 역할 내부)에서 웹 응용 프로그램을 자체 호스트 하는 데 적합 합니다.
>
> 이 자습서에서는 OWIN 응용 프로그램을 자체 호스트 하는 데 사용 되는 HTTP 서버를 제공 하는 Owin HttpListener 패키지를 사용 합니다.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - Web API 2
> - [Azure SDK for .NET 2.3](https://azure.microsoft.com/downloads/)

## <a name="create-a-microsoft-azure-project"></a>Microsoft Azure 프로젝트 만들기

관리자 권한으로 Visual Studio를 시작 합니다. Azure 계산 에뮬레이터를 사용 하 여 응용 프로그램을 로컬로 디버깅 하려면 관리자 권한이 필요 합니다.

**파일** 메뉴에서 **새로 만들기** 를 클릭 한 다음 **프로젝트** 를 클릭 합니다. **설치 된 템플릿** 의 Visual c # 아래에서 **클라우드** 를 클릭 한 다음 **Windows Azure 클라우드 서비스** 를 클릭 합니다. 프로젝트 이름을 "AzureApp"으로 선택 하 고 **확인** 을 클릭 합니다.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

**새 Windows Azure 클라우드 서비스** 대화 상자에서 **작업자 역할** 을 두 번 클릭 합니다. 기본 이름 ("WorkerRole1")을 그대로 둡니다. 이 단계에서는 솔루션에 작업자 역할을 추가 합니다. **확인** 을 클릭합니다.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

생성 되는 Visual Studio 솔루션에는 두 개의 프로젝트가 포함 됩니다.

- &quot;AzureApp은 &quot; Azure 응용 프로그램에 대 한 역할 및 구성을 정의 합니다.
- &quot;WorkerRole1에는 &quot; 작업자 역할에 대 한 코드가 포함 되어 있습니다.

일반적으로이 자습서에서는 단일 역할을 사용 하지만 Azure 응용 프로그램에는 여러 역할이 포함 될 수 있습니다.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a>Web API 및 OWIN 패키지 추가

**도구** 메뉴에서 **NuGet 패키지 관리자** 를 클릭 한 다음 **패키지 관리자 콘솔** 을 클릭 합니다.

패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a>HTTP 끝점 추가

솔루션 탐색기에서 AzureApp 프로젝트를 확장 합니다. 역할 노드를 확장 하 고 WorkerRole1를 마우스 오른쪽 단추로 클릭 한 다음 **속성** 을 선택 합니다.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

**엔드포인트** 를 클릭한 다음, **엔드포인트 추가** 를 클릭합니다.

**프로토콜** 드롭다운 목록에서 "http"를 선택 합니다. **공용 포트** 및 **개인 포트** 에 80을 입력 합니다. 이러한 포트 번호는 다를 수 있습니다. 공용 포트는 역할에 요청을 보낼 때 클라이언트에서 사용 하는 것입니다.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a>Self-Host 웹 API 구성

솔루션 탐색기에서 WorkerRole1 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**  /  **클래스** 를 선택 하 여 새 클래스를 추가 합니다. 클래스 `Startup` 이름을 지정합니다.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

이 파일의 모든 상용구 코드를 다음으로 바꿉니다.

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a>Web API 컨트롤러 추가

그런 다음 웹 API 컨트롤러 클래스를 추가 합니다. WorkerRole1 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클래스 **추가** 를 선택  /  **Class** 합니다. TestController 클래스의 이름을로 합니다. 이 파일의 모든 상용구 코드를 다음으로 바꿉니다.

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

편의상이 컨트롤러는 일반 텍스트를 반환 하는 두 개의 GET 메서드를 정의 합니다.

## <a name="start-the-owin-host"></a>OWIN 호스트 시작

WorkerRole.cs 파일을 엽니다. 이 클래스는 작업자 역할이 시작 및 중지 될 때 실행 되는 코드를 정의 합니다.

다음 using 문을 추가합니다.

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

클래스에 **IDisposable** 멤버를 추가 합니다 `WorkerRole` .

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

`OnStart`메서드에서 호스트를 시작 하는 다음 코드를 추가 합니다.

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

**WebApp** 메서드는 OWIN 호스트를 시작 합니다. 클래스의 이름은 `Startup` 메서드의 형식 매개 변수입니다. 규칙에 따라 호스트는 `Configure` 이 클래스의 메서드를 호출 합니다.

`OnStop` *\_ 앱* 인스턴스를 삭제 하려면를 재정의 합니다.

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

WorkerRole.cs에 대 한 전체 코드는 다음과 같습니다.

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

솔루션을 빌드하고 F5 키를 눌러 Azure 계산 에뮬레이터에서 응용 프로그램을 로컬로 실행 합니다. 방화벽 설정에 따라 에뮬레이터를 방화벽을 통해 허용 해야 할 수도 있습니다.

> [!NOTE]
> 다음과 같은 예외가 발생 하는 경우 해결 방법은 [이 블로그 게시물](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) 을 참조 하세요. "파일 또는 어셈블리 ' Owin, Version = 2.0.2.0, Culture = 중립, PublicKeyToken = 31bf3856ad364e35 ' 또는 해당 종속성 중 하나를 로드할 수 없습니다. 찾은 어셈블리의 매니페스트 정의가 어셈블리 참조와 일치 하지 않습니다. (HRESULT의 예외: 0x80131040) "

계산 에뮬레이터는 끝점에 로컬 IP 주소를 할당 합니다. 계산 에뮬레이터 UI를 확인 하 여 IP 주소를 찾을 수 있습니다. 작업 표시줄 알림 영역에서 에뮬레이터 아이콘을 마우스 오른쪽 단추로 클릭 하 고 **계산 에뮬레이터 UI 표시** 를 선택 합니다.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

서비스 배포, 배포 [id], 서비스 세부 정보에서 IP 주소를 찾습니다. 웹 브라우저를 열고 http://<em>address</em>/test/1로 이동 합니다. 여기서 <em>address</em> 는 계산 에뮬레이터에서 할당 한 IP 주소입니다. 예를 들면 `http://127.0.0.1:80/test/1` 입니다. 웹 API 컨트롤러에서 응답이 표시 되어야 합니다.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a>Azure에 배포

이 단계에서는 Azure 계정이 있어야 합니다. 아직 없는 경우 몇 분만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Microsoft Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)을 참조 하세요.

솔루션 탐색기에서 AzureApp 프로젝트를 마우스 오른쪽 단추로 클릭 합니다. **게시** 를 선택합니다.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

Azure 계정에 로그인 하지 않은 경우 **로그인** 을 클릭 합니다.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

로그인 한 후 구독을 선택 하 고 **다음** 을 클릭 합니다.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

클라우드 서비스의 이름을 입력 하 고 지역을 선택 합니다. **만들기** 를 클릭합니다.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

**게시** 를 클릭합니다.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

Azure 활동 로그 창에는 배포 진행률이 표시 됩니다. 앱이 배포 되 면로 이동 http://appname.cloudapp.net/test/1 합니다.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a>추가 리소스

- [프로젝트 Katana 개요](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [GitHub의 Katana 프로젝트](https://github.com/aspnet/AspNetKatana)
