---
uid: signalr/overview/deployment/tutorial-signalr-self-host
title: '자습서: SignalR 자체 호스트 | Microsoft Docs'
author: bradygaster
description: 이 자습서에서는 자체 호스트 된 SignalR 2 서버를 만드는 방법과 JavaScript 클라이언트를 사용 하 여이 서버에 연결 하는 방법을 보여 줍니다. 자습서 V에서 사용 되는 소프트웨어 버전
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 400db427-27af-4f2f-abf0-5486d5e024b5
msc.legacyurl: /signalr/overview/deployment/tutorial-signalr-self-host
msc.type: authoredcontent
ms.openlocfilehash: 7470e0d6b68772ccfd979c834b7db81fbba3ca78
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240615"
---
# <a name="tutorial-signalr-self-host"></a>자습서: SignalR 자체 호스팅

[Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 자습서에서는 자체 호스트 된 SignalR 2 서버를 만드는 방법과 JavaScript 클라이언트를 사용 하 여이 서버에 연결 하는 방법을 보여 줍니다.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 버전 2
>
>
>
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a>이 자습서에서는 Visual Studio 2012 사용
>
>
> 이 자습서에서 Visual Studio 2012을 사용 하려면 다음을 수행 합니다.
>
> - [패키지 관리자](http://docs.nuget.org/docs/start-here/installing-nuget) 를 최신 버전으로 업데이트 합니다.
> - [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)를 설치 합니다.
> - 웹 플랫폼 설치 관리자에서 **Visual Studio 2012 용 ASP.NET 및 Web Tools 2013.1**를 검색 하 고 설치 합니다. 그러면 **허브**와 같은 SignalR 클래스에 대 한 Visual Studio 템플릿이 설치 됩니다.
> - 일부 템플릿 (예: **OWIN 시작 클래스**)은 사용할 수 없습니다. 이러한 경우 클래스 파일을 대신 사용 합니다.
>
>
> ## <a name="questions-and-comments"></a>질문 및 설명
>
> 이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요. 자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.

## <a name="overview"></a>개요

SignalR 서버는 일반적으로 IIS의 ASP.NET 응용 프로그램에서 호스트 되지만 자체 호스트 (예: 콘솔 응용 프로그램 또는 Windows 서비스)는 자체 호스트 라이브러리를 사용 하 여 호스트 될 수도 있습니다. SignalR 2와 같은이 라이브러리는 OWIN ([Open Web Interface for .net](http://owin.org))를 기반으로 합니다. OWIN는 .NET 웹 서버와 웹 응용 프로그램 간의 추상화를 정의 합니다. OWIN는 서버에서 웹 응용 프로그램을 분리 IIS 외부의 자체 프로세스에서 웹 응용 프로그램을 자체 호스트 하는 데 적합 합니다.

IIS에서를 호스팅하지 않는 이유는 다음과 같습니다.

- Iis가 없는 기존 서버 팜과 같이 IIS를 사용할 수 없거나 바람직하지 않은 환경
- IIS의 성능 오버 헤드를 방지 해야 합니다.
- SignalR 기능은 Windows 서비스, Azure 작업자 역할 또는 다른 프로세스에서 실행 되는 기존 응용 프로그램에 추가 됩니다.

성능상의 이유로 자체 호스트로 솔루션을 개발 하는 경우에는 IIS에서 호스트 되는 응용 프로그램을 테스트 하 여 성능상의 이점을 확인 하는 것이 좋습니다.

이 자습서에는 다음과 같은 섹션이 포함 되어 있습니다.

- [서버 만들기](#server)
- [JavaScript 클라이언트를 사용 하 여 서버에 액세스](#js)

<a id="server"></a>

## <a name="creating-the-server"></a>서버 만들기

이 자습서에서는 콘솔 응용 프로그램에서 호스트 되는 서버를 만들지만 Windows 서비스 또는 Azure 작업자 역할과 같은 모든 종류의 프로세스에서 서버를 호스트할 수 있습니다. Windows 서비스에서 SignalR 서버를 호스트 하는 샘플 코드는 [Windows 서비스의 자체 호스팅 SignalR](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3)을 참조 하세요.

1. 관리자 권한으로 Visual Studio 2013를 엽니다. **파일**, **새 프로젝트**를 차례로 선택 합니다. **템플릿** 창의 **Visual c #** 노드 아래에서 **Windows** 를 선택 하 고 **콘솔 응용 프로그램** 템플릿을 선택 합니다. 새 프로젝트의 이름을 "SignalRSelfHost"로 하 고 **확인**을 클릭 합니다.

    ![](tutorial-signalr-self-host/_static/image1.png)
2. **도구**  >  **nuget**패키지 관리자  >  **패키지 관리자 콘솔**을 선택 하 여 nuget 패키지 관리자 콘솔을 엽니다.
3. 패키지 관리자 콘솔에서 다음 명령을 입력 합니다.

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample1.ps1)]

    이 명령은 SignalR 2 자체 호스트 라이브러리를 프로젝트에 추가 합니다.
4. 패키지 관리자 콘솔에서 다음 명령을 입력 합니다.

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample2.ps1)]

    이 명령은 Owin 라이브러리를 프로젝트에 추가 합니다. 이 라이브러리는 SignalR를 호스트 하는 응용 프로그램 및 다른 도메인의 웹 페이지 클라이언트에 필요한 도메인 간 지원에 사용 됩니다. SignalR 서버와 웹 클라이언트를 서로 다른 포트에 호스트할 것 이므로 이러한 구성 요소 간 통신을 위해 도메인 간 사용을 설정 해야 합니다.
5. Program.cs 내용을 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-signalr-self-host/samples/sample3.cs)]

    위의 코드는 세 가지 클래스를 포함 합니다.

    - 기본 실행 경로를 정의 하는 **Main** 메서드를 포함 하는 **프로그램**입니다. 이 메서드에서 **Startup** 유형의 웹 응용 프로그램은 지정 된 URL ()에서 시작 됩니다 `http://localhost:8080` . 끝점에 보안을 설정 해야 하는 경우 SSL을 구현할 수 있습니다. 자세한 내용은 [방법: SSL 인증서로 포트 구성](https://msdn.microsoft.com/library/ms733791.aspx) 을 참조 하세요.
    - **시작**, SignalR 서버에 대 한 구성 (이 자습서에서 사용 하는 유일한 구성) 및에 대 한 호출을 포함 하는 클래스는 `UseCors` `MapSignalR` 프로젝트의 모든 허브 개체에 대 한 경로를 만듭니다.
    - **Myhub**-응용 프로그램이 클라이언트에 제공 하는 SignalR hub 클래스입니다. 이 클래스에는 클라이언트에서 연결 된 다른 모든 클라이언트에 메시지를 브로드캐스트하는를 호출 하는 단일 메서드인 **Send**가 있습니다.
6. 애플리케이션을 컴파일하고 실행합니다. 서버에서 실행 중인 주소가 콘솔 창에 표시 됩니다.

    ![](tutorial-signalr-self-host/_static/image2.png)
7. 예외로 인해 실행이 실패 하면 `System.Reflection.TargetInvocationException was unhandled` 관리자 권한으로 Visual Studio를 다시 시작 해야 합니다.
8. 다음 섹션으로 진행 하기 전에 응용 프로그램을 중지 합니다.

<a id="js"></a>

## <a name="accessing-the-server-with-a-javascript-client"></a>JavaScript 클라이언트를 사용 하 여 서버에 액세스

이 섹션에서는 초보자를 위한 [자습서](../getting-started/tutorial-getting-started-with-signalr.md)에서 동일한 JavaScript 클라이언트를 사용 합니다. 클라이언트에 대해 한 번만 수정 하면 됩니다 .이는 허브 URL을 명시적으로 정의 하는 것입니다. 자체 호스팅 응용 프로그램을 사용 하는 경우 서버는 역방향 프록시와 부하 분산 장치 때문에 연결 URL과 동일한 주소에 있을 수 없으므로 URL을 명시적으로 정의 해야 합니다.

1. **솔루션 탐색기**에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **추가**, **새 프로젝트**를 차례로 선택 합니다. **웹** 노드를 선택 하 고 **ASP.NET 웹 응용 프로그램** 템플릿을 선택 합니다. 프로젝트 이름을 "JavascriptClient"로 선택 하 고 **확인을**클릭 합니다.

    ![](tutorial-signalr-self-host/_static/image3.png)
2. **빈** 템플릿을 선택 하 고 나머지 옵션은 선택 하지 않은 상태로 둡니다. **프로젝트 만들기**를 선택 합니다.

    ![](tutorial-signalr-self-host/_static/image4.png)
3. 패키지 관리자 콘솔의 **기본 프로젝트** 드롭다운에서 "JavascriptClient" 프로젝트를 선택 하 고 다음 명령을 실행 합니다.

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample4.ps1)]

    이 명령은 클라이언트에 필요한 SignalR 및 JQuery 라이브러리를 설치 합니다.
4. 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**, **새 항목**을 차례로 선택 합니다. **웹** 노드를 선택 하 고 HTML 페이지를 선택 합니다. 페이지의 이름을 **Default.html**로 합니다.

    ![](tutorial-signalr-self-host/_static/image5.png)
5. 새 HTML 페이지의 내용을 다음 코드로 바꿉니다. 여기에서 스크립트 참조가 프로젝트의 Scripts 폴더에 있는 스크립트와 일치 하는지 확인 합니다.

    [!code-html[Main](tutorial-signalr-self-host/samples/sample5.html?highlight=31-32)]

    위의 코드 샘플에 강조 표시 된 다음 코드는 시작 자습서에서 사용 되는 클라이언트에 대 한 추가 작업 (코드를 SignalR 버전 2 베타로 업그레이드 하는 것 외에)입니다. 이 코드 줄은 서버에서 SignalR에 대 한 기본 연결 URL을 명시적으로 설정 합니다.

    [!code-javascript[Main](tutorial-signalr-self-host/samples/sample6.js)]
6. 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **시작 프로젝트 설정**...을 선택 합니다. **여러 개의 시작 프로젝트** 라디오 단추를 선택 하 고 두 프로젝트의 **작업** 을 **시작**으로 설정 합니다.

    ![](tutorial-signalr-self-host/_static/image6.png)
7. "Default.html"을 마우스 오른쪽 단추로 클릭 하 고 **시작 페이지로 설정**을 선택 합니다.
8. 애플리케이션을 실행합니다. 서버와 페이지가 시작 됩니다. 서버를 시작 하기 전에 페이지를 로드 하는 경우 웹 페이지를 다시 로드 하거나 디버거에서 **계속** 을 선택 해야 할 수 있습니다.
9. 브라우저에서 메시지가 표시 되 면 사용자 이름을 입력 합니다. 페이지의 URL을 다른 브라우저 탭 또는 창에 복사 하 고 다른 사용자 이름을 입력 합니다. 시작 자습서에서와 같이 브라우저 창 간에 메시지를 보낼 수 있습니다.
