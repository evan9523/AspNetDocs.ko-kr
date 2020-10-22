---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET SignalR Hubs API 가이드-JavaScript 클라이언트 | Microsoft Docs
author: bradygaster
description: 이 문서에서는 JavaScript 클라이언트에서 SignalR 버전 2 용 허브 API를 사용 하는 방법을 소개 합니다. 예를 들어 브라우저 및 Windows 스토어 (WinJS)의
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345427"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a>ASP.NET SignalR Hubs API 가이드-JavaScript 클라이언트

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 브라우저 및 WinJS (Windows 스토어) 응용 프로그램과 같은 JavaScript 클라이언트에서 SignalR 버전 2 용 허브 API를 사용 하는 방법을 소개 합니다.
>
> SignalR Hubs API를 사용 하면 서버에서 연결 된 클라이언트로 또는 클라이언트에서 서버로 Rpc (원격 프로시저 호출)를 수행할 수 있습니다. 서버 코드에서는 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다. 클라이언트 코드에서는 서버에서 호출할 수 있는 메서드를 정의 하 고 서버에서 실행 되는 메서드를 호출 합니다. SignalR는 모든 클라이언트에서 서버로의 작업을 수행 합니다.
>
> 또한 SignalR는 영구 연결 이라고 하는 하위 수준 API를 제공 합니다. SignalR, 허브 및 영구 연결에 대 한 소개는 [SignalR 소개](../getting-started/introduction-to-signalr.md)를 참조 하세요.
>
> ## <a name="software-versions-used-in-this-topic"></a>이 항목에서 사용 되는 소프트웨어 버전
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
> - .NET 4.5
> - SignalR 버전 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>이 항목의 이전 버전
>
> 이전 버전의 SignalR에 대 한 자세한 내용은 [SignalR 이전 버전](../older-versions/index.md)을 참조 하세요.
>
> ## <a name="questions-and-comments"></a>질문 및 설명
>
> 이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요. 자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.

## <a name="overview"></a>개요

이 문서는 다음 섹션으로 구성됩니다.

- [생성 된 프록시와 사용자를 위해 수행 하는 작업](#genproxy)

    - [생성 된 프록시를 사용 하는 경우](#cantusegenproxy)
- [클라이언트 설정](#clientsetup)

    - [동적으로 생성 된 프록시를 참조 하는 방법](#dynamicproxy)
    - [SignalR 생성 프록시에 대 한 물리적 파일을 만드는 방법](#manualproxy)
- [연결을 설정 하는 방법](#establishconnection)

    - [$. hubConnection ()에서 생성 하는 것과 동일한 개체입니다.](#connequivalence)
    - [시작 메서드의 비동기 실행](#asyncstart)
- [도메인 간 연결을 설정 하는 방법](#crossdomain)
- [연결을 구성 하는 방법](#configureconnection)

    - [쿼리 문자열 매개 변수를 지정 하는 방법](#querystring)
    - [전송 방법을 지정 하는 방법](#transport)
- [허브 클래스에 대 한 프록시를 가져오는 방법](#getproxy)
- [서버에서 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법](#callclient)
- [클라이언트에서 서버 메서드를 호출 하는 방법](#callserver)
- [연결 수명 이벤트를 처리 하는 방법](#connectionlifetime)
- [오류를 처리 하는 방법](#handleerrors)
- [클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법](#logging)

서버 또는 .NET 클라이언트를 프로그래밍 하는 방법에 대 한 설명서는 다음 리소스를 참조 하세요.

- [SignalR Hubs API 가이드-서버](hubs-api-guide-server.md)
- [SignalR Hubs API 가이드-.NET 클라이언트](hubs-api-guide-net-client.md)

SignalR 2 서버 구성 요소는 .net 4.5 에서만 사용할 수 있습니다. .net 4.0에는 SignalR 2 용 .NET 클라이언트가 있습니다.

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a>생성 된 프록시와 사용자를 위해 수행 하는 작업

SignalR에서 생성 하는 프록시를 사용 하거나 사용 하지 않고 SignalR 서비스와 통신 하도록 JavaScript 클라이언트를 프로그래밍할 수 있습니다. 프록시는 사용자가 연결 하는 데 사용 하는 코드의 구문을 간소화 하 고, 서버에서 호출 하는 메서드를 작성 하 고, 서버에서 메서드를 호출 합니다.

서버 메서드를 호출 하는 코드를 작성할 때 생성 된 프록시를 사용 하면 로컬 함수를 실행 하는 것 처럼 보이는 구문을 사용할 수 있습니다. 대신을 작성할 수 있습니다 `serverMethod(arg1, arg2)` `invoke('serverMethod', arg1, arg2)` . 서버 메서드 이름을 잘못 입력 한 경우에는 생성 된 프록시 구문을 사용 하 여 즉각적인 있는 클라이언트 쪽 오류가 발생할 수도 있습니다. 또한 프록시를 정의 하는 파일을 수동으로 만드는 경우 서버 메서드를 호출 하는 코드를 작성할 수 있도록 IntelliSense 지원을 받을 수 있습니다.

예를 들어 서버에 다음과 같은 허브 클래스가 있다고 가정 합니다.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

다음 코드 예제에서는 서버에서 메서드를 호출 `NewContosoChatMessage` 하 고 서버에서 메서드 호출을 수신 하는 JavaScript 코드를 보여 줍니다 `addContosoChatMessageToPage` .

**생성 된 프록시 사용**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

**생성 된 프록시 제외**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a>생성 된 프록시를 사용 하는 경우

서버에서 호출 하는 클라이언트 메서드에 대해 여러 이벤트 처리기를 등록 하려는 경우에는 생성 된 프록시를 사용할 수 없습니다. 그렇지 않으면 코딩 기본 설정에 따라 생성 된 프록시를 사용 하거나 사용 하지 않도록 선택할 수 있습니다. 사용 하지 않도록 선택 하는 경우 `script` 클라이언트 코드의 요소에서 "signalr/hubs" URL을 참조할 필요가 없습니다.

<a id="clientsetup"></a>

## <a name="client-setup"></a>클라이언트 설치

JavaScript 클라이언트에는 jQuery 및 SignalR core JavaScript 파일에 대 한 참조가 필요 합니다. JQuery 버전은 1.7.2, 1.8.2 또는 1.9.1와 같은 1.6.4 또는 주 이후 버전 이어야 합니다. 생성 된 프록시를 사용 하기로 결정 한 경우 SignalR 생성 된 프록시 JavaScript 파일에 대 한 참조도 필요 합니다. 다음 예제에서는 생성 된 프록시를 사용 하는 HTML 페이지에서 참조의 모양을 보여 줍니다.

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

이러한 참조는 jQuery first, SignalR core 이후, SignalR 프록시가 마지막 순서로 포함 되어야 합니다.

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a>동적으로 생성 된 프록시를 참조 하는 방법

앞의 예제에서 SignalR 생성 된 프록시에 대 한 참조는 물리적 파일이 아니라 동적으로 생성 되는 JavaScript 코드에 대 한 것입니다. SignalR는 프록시에 대 한 JavaScript 코드를 즉석에서 만들고 "/signalr/hubs" URL에 대 한 응답으로 클라이언트에 제공 합니다. 메서드의 서버에서 SignalR 연결에 대해 다른 기준 URL을 지정한 경우 `MapSignalR` 동적으로 생성 된 프록시 파일의 url은 "/hubs"가 추가 된 사용자 지정 url입니다.

> [!NOTE]
> Windows 8 (Windows 스토어) JavaScript 클라이언트의 경우 동적으로 생성 되는 것이 아니라 실제 프록시 파일을 사용 합니다. 자세한 내용은이 항목의 뒷부분에 나오는 [SignalR 생성 된 프록시에 대 한 물리적 파일을 만드는 방법](#manualproxy) 을 참조 하십시오.

ASP.NET MVC 4 또는 5 Razor 보기에서 물결표를 사용 하 여 프록시 파일 참조의 응용 프로그램 루트를 참조 합니다.

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

MVC 5에서 SignalR를 사용 하는 방법에 대 한 자세한 내용은 [SignalR 및 mvc 5 시작](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)을 참조 하세요.

ASP.NET MVC 3 Razor 뷰에서 `Url.Content` 프록시 파일 참조에 대해를 사용 합니다.

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

ASP.NET Web Forms 응용 프로그램에서 `ResolveClientUrl` 프록시 파일 참조에 사용 하거나, 앱 루트 상대 경로 (물결표로 시작)를 사용 하 여 ScriptManager를 통해 등록 합니다.

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

일반적인 규칙으로, CSS 또는 JavaScript 파일에 사용 하는 "/signalr/hubs" URL을 지정 하는 데 동일한 방법을 사용 합니다. 물결표를 사용 하지 않고 URL을 지정 하는 경우 일부 시나리오에서는 IIS Express를 사용 하 여 Visual Studio에서 테스트 하는 경우 응용 프로그램이 올바르게 작동 하지만 전체 IIS에 배포할 때 404 오류가 발생 하 고 실패 합니다. 자세한 내용은 MSDN 사이트에서 [Visual Studio for ASP.NET 웹 프로젝트의 웹 서버](https://msdn.microsoft.com/library/58wxa9w5.aspx) 에서 Root-Level 리소스에 대 한 **참조 확인** 을 참조 하세요.

디버그 모드에서 Visual Studio 2017을 사용 하 여 웹 프로젝트를 실행 하 고 Internet Explorer를 브라우저로 사용 하는 경우 **스크립트**의 **솔루션 탐색기** 에서 프록시 파일을 볼 수 있습니다.

파일의 내용을 보려면 **허브**를 두 번 클릭 합니다. Visual Studio 2012 또는 2013 및 Internet Explorer를 사용 하지 않거나 디버그 모드가 아닌 경우 "/signalR/hubs" URL로 이동 하 여 파일의 내용을 가져올 수도 있습니다. 예를 들어 사이트가에서 실행 되는 경우 `http://localhost:56699` `http://localhost:56699/SignalR/hubs` 브라우저에서로 이동 합니다.

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a>SignalR 생성 프록시에 대 한 물리적 파일을 만드는 방법

동적으로 생성 된 프록시에 대 한 대 안으로 프록시 코드를 포함 하는 물리적 파일을 만들고 해당 파일을 참조할 수 있습니다. 이러한 작업을 수행 하 여 캐싱 또는 번들 동작을 제어 하거나 서버 메서드를 코딩 하는 경우 IntelliSense를 가져올 수 있습니다.

프록시 파일을 만들려면 다음 단계를 수행 합니다.

1. [SignalR 유틸리티](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet 패키지를 설치 합니다.
2. 명령 프롬프트를 열고 SignalR.exe 파일이 포함 된 *tools* 폴더로 이동 합니다. Tools 폴더는 다음 위치에 있습니다.

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. 다음 명령을 입력합니다.

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    *.Dll* 의 경로는 일반적으로 프로젝트 폴더의 *bin* 폴더입니다.

    이 명령은 *signalr.exe*와 동일한 폴더에 *server.js* 라는 파일을 만듭니다.
4. *server.js* 파일을 프로젝트의 적절 한 폴더에 배치 하 고, 응용 프로그램에 맞게 이름을 바꾸고, "signalr/hubs" 참조 대신 해당 폴더에 대 한 참조를 추가 합니다.

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>연결을 설정 하는 방법

연결을 설정 하려면 먼저 연결 개체를 만들고 프록시를 만든 다음 서버에서 호출할 수 있는 메서드에 대 한 이벤트 처리기를 등록 해야 합니다. 프록시 및 이벤트 처리기를 설정 하는 경우 메서드를 호출 하 여 연결을 설정 합니다 `start` .

생성 된 프록시를 사용 하는 경우 생성 된 프록시 코드가 사용자에 게이를 수행 하므로 연결 개체를 직접 만들 필요가 없습니다.

<a id="nogenconnection"></a>

**생성 된 프록시를 사용 하 여 연결 설정**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

**생성 된 프록시를 사용 하지 않고 연결 설정**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

샘플 코드는 기본 "/signalr" URL을 사용 하 여 SignalR 서비스에 연결 합니다. 다른 기준 URL을 지정 하는 방법에 대 한 자세한 내용은 [ASP.NET SignalR HUBS API Guide-Server-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)을 참조 하세요.

기본적으로 허브 위치는 현재 서버입니다. 다른 서버에 연결 하는 경우 다음 예제와 같이 메서드를 호출 하기 전에 URL을 지정 합니다 `start` .

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> 일반적으로 메서드를 호출 하 여 연결을 설정 하기 전에 이벤트 처리기를 등록 `start` 합니다. 연결을 설정한 후 일부 이벤트 처리기를 등록 하려는 경우에는이 작업을 수행할 수 있지만 메서드를 호출 하기 전에 이벤트 처리기를 하나 이상 등록 해야 합니다 `start` . 한 가지 이유는 응용 프로그램에 많은 허브가 있을 수 있지만,이 중 `OnConnected` 하나에만 사용 하려는 경우 모든 허브에서 이벤트를 트리거하지 않으려는 것입니다. 연결이 설정 되 면 허브의 프록시에 클라이언트 메서드가 있으면 이벤트를 SignalR 알려 주는 것입니다 `OnConnected` . 메서드를 호출 하기 전에 이벤트 처리기를 등록 하지 않으면 `start` 허브에서 메서드를 호출할 수 있지만 허브의 메서드는 호출 되지 않으며 `OnConnected` 서버에서 클라이언트 메서드가 호출 되지 않습니다.

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a>$. hubConnection ()에서 생성 하는 것과 동일한 개체입니다.

예제에서 볼 수 있듯이 생성 된 프록시를 사용 하는 경우은 `$.connection.hub` 연결 개체를 참조 합니다. 이는 `$.hubConnection()` 생성 된 프록시를 사용 하지 않을 때를 호출 하 여 가져오는 것과 동일한 개체입니다. 생성 된 프록시 코드는 다음 문을 실행 하 여 연결을 만듭니다.

![생성 된 프록시 파일에서 연결 만들기](hubs-api-guide-javascript-client/_static/image3.png)

생성 된 프록시를 사용 하는 경우 `$.connection.hub` 생성 된 프록시를 사용 하지 않는 경우 연결 개체로 수행할 수 있는 모든 작업을 수행할 수 있습니다.

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a>시작 메서드의 비동기 실행

`start`메서드는 비동기적으로 실행 됩니다. [JQuery 지연 개체](http://api.jquery.com/category/deferred-object/)를 반환 합니다. 즉,, 등의 메서드를 호출 하 여 콜백 함수를 추가할 수 있습니다 `pipe` `done` `fail` . 서버 메서드 호출과 같이 연결이 설정 된 후에 실행 하려는 코드가 있는 경우 해당 코드를 콜백 함수에 넣거나 콜백 함수에서 호출 합니다. `.done`콜백 메서드는 연결이 설정 된 후, `OnConnected` 서버의 이벤트 처리기 메서드에 있는 코드의 실행이 완료 된 후에 실행 됩니다.

앞의 예제에 있는 "현재 연결 된" 문을 메서드 호출 뒤의 다음 코드 줄로 입력 하면 `start` ( `.done` 콜백이 아닌) `console.log` 다음 예제와 같이 연결이 설정 되기 전에 줄이 실행 됩니다.

![연결이 설정 된 후 실행 되는 코드를 작성 하는 잘못 된 방법](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a>도메인 간 연결을 설정 하는 방법

일반적으로 브라우저에서에서 페이지를 로드 하는 경우 `http://contoso.com` SignalR 연결은에서 동일한 도메인에 `http://contoso.com/signalr` 있습니다. 에서 페이지가에 연결 되는 경우 `http://contoso.com` `http://fabrikam.com/signalr` 이는 도메인 간 연결입니다. 보안상의 이유로 도메인 간 연결은 기본적으로 사용 하지 않도록 설정 됩니다.

SignalR 1.x에서 도메인 간 요청은 단일 EnableCrossDomain 플래그에 의해 제어 됩니다. 이 플래그는 JSONP 및 CORS 요청을 모두 제어 합니다. 유연성을 높이기 위해 SignalR의 서버 구성 요소에서 모든 CORS 지원이 제거 되었습니다. JavaScript 클라이언트는 여전히 CORS를 사용 하 여 브라우저에서 지 원하는 경우에는 CORS를 정상적으로 사용 하 고, 이러한 시나리오를 지원 하기 위해 새로운 OWIN 미들웨어를 사용할 수 있게 되었습니다.

클라이언트에서 JSONP가 필요한 경우 (이전 브라우저에서 도메인 간 요청을 지원 하려면 `EnableJSONP` 아래와 같이 개체에 대해를로 설정 하 여 명시적으로 사용 하도록 설정 해야 합니다 `HubConfiguration` `true` . JSONP는 CORS 보다 안전 하지 않으므로 기본적으로 사용 하지 않도록 설정 되어 있습니다.

**프로젝트에 Owin를 추가 하는 중입니다.** 이 라이브러리를 설치 하려면 패키지 관리자 콘솔에서 다음 명령을 실행 합니다.

`Install-Package Microsoft.Owin.Cors`

이 명령은 2.1.0 버전의 패키지를 프로젝트에 추가 합니다.

### <a name="calling-usecors"></a>UseCors 호출

 다음 코드 조각에서는 SignalR 2에서 도메인 간 연결을 구현 하는 방법을 보여 줍니다.

**SignalR 2에서 도메인 간 요청 구현**

다음 코드에서는 SignalR 2 프로젝트에서 CORS 또는 JSONP를 사용 하도록 설정 하는 방법을 보여 줍니다. 이 코드 샘플에서는 `Map` 대신 및를 사용 `RunSignalR` `MapSignalR` 하므로 cors 미들웨어는에 지정 된 경로의 모든 트래픽이 아닌 cors를 지원 해야 하는 SignalR 요청에 대해서만 실행 됩니다 `MapSignalR` . Map은 전체 응용 프로그램이 아닌 특정 URL 접두사에 대해 실행 해야 하는 다른 미들웨어에도 사용할 수 있습니다.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - `jQuery.support.cors`코드에서를 true로 설정 하지 마세요.
>
>     ![JQuery를 true로 설정 하지 마세요.](hubs-api-guide-javascript-client/_static/image7.png)
>
>     SignalR는 CORS 사용을 처리 합니다. `jQuery.support.cors`True로 설정 하면 SignalR에서 브라우저가 CORS를 지원 한다고 가정 하기 때문에 JSONP를 사용 하지 않도록 설정 합니다.
> - Localhost URL에 연결 하는 경우 Internet Explorer 10은 도메인 간 연결을 고려 하지 않으므로 서버에서 도메인 간 연결을 사용 하도록 설정 하지 않은 경우에도 응용 프로그램은 IE 10에서 로컬로 작동 합니다.
> - Internet Explorer 9에서 도메인 간 연결을 사용 하는 방법에 대 한 자세한 내용은 [이 StackOverflow 스레드](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)를 참조 하세요.
> - Chrome에서 도메인 간 연결을 사용 하는 방법에 대 한 자세한 내용은 [이 StackOverflow 스레드](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)를 참조 하세요.
> - 샘플 코드는 기본 "/signalr" URL을 사용 하 여 SignalR 서비스에 연결 합니다. 다른 기준 URL을 지정 하는 방법에 대 한 자세한 내용은 [ASP.NET SignalR HUBS API Guide-Server-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)을 참조 하세요.

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>연결을 구성 하는 방법

연결을 설정 하기 전에 쿼리 문자열 매개 변수를 지정 하거나 전송 방법을 지정할 수 있습니다.

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>쿼리 문자열 매개 변수를 지정 하는 방법

클라이언트에서 연결할 때 서버에 데이터를 전송 하려는 경우 연결 개체에 쿼리 문자열 매개 변수를 추가할 수 있습니다. 다음 예에서는 클라이언트 코드에서 쿼리 문자열 매개 변수를 설정 하는 방법을 보여 줍니다.

**생성 된 프록시를 사용 하 여 시작 메서드를 호출 하기 전에 쿼리 문자열 값을 설정 합니다.**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

**생성 된 프록시 없이 start 메서드를 호출 하기 전에 쿼리 문자열 값을 설정 합니다.**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

다음 예에서는 서버 코드에서 쿼리 문자열 매개 변수를 읽는 방법을 보여 줍니다.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>전송 방법을 지정 하는 방법

연결 프로세스의 일부로 SignalR 클라이언트는 서버와 클라이언트 모두에서 지원 되는 최상의 전송을 결정 하기 위해 일반적으로 서버와 협상 합니다. 사용할 전송을 이미 알고 있는 경우 메서드를 호출할 때 전송 방법을 지정 하 여이 협상 프로세스를 건너뛸 수 있습니다 `start` .

**전송 메서드를 지정 하는 클라이언트 코드 (생성 된 프록시 포함)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

**전송 메서드를 지정 하는 클라이언트 코드 (생성 된 프록시 제외)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

또는 SignalR에서 시도 하는 순서 대로 여러 전송 방법을 지정할 수 있습니다.

**생성 된 프록시를 사용 하 여 사용자 지정 전송 대체 (fallback) 체계를 지정 하는 클라이언트 코드**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

**생성 된 프록시를 사용 하지 않고 사용자 지정 전송 대체 (fallback) 체계를 지정 하는 클라이언트 코드**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

전송 방법 지정에 다음 값을 사용할 수 있습니다.

- Websocket
- "foreverFrame"
- "serverSentEvents"
- "고 폴링"

다음 예에서는 연결에서 사용 되는 전송 방법을 확인 하는 방법을 보여 줍니다.

**연결에서 사용 하는 전송 방법 (생성 된 프록시 포함)을 표시 하는 클라이언트 코드**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

**생성 된 프록시를 사용 하지 않고 연결에서 사용 되는 전송 방법을 표시 하는 클라이언트 코드**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

서버 코드에서 전송 방법을 확인 하는 방법에 대 한 자세한 내용은 [ASP.NET SignalR HUBS API 가이드-서버-컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법](hubs-api-guide-server.md#contextproperty)을 참조 하세요. 전송 및 대체에 대 한 자세한 내용은 [SignalR에 대 한 소개-전송 및 대체](../getting-started/introduction-to-signalr.md#transports)를 참조 하세요.

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a>허브 클래스에 대 한 프록시를 가져오는 방법

사용자가 만드는 각 연결 개체는 하나 이상의 허브 클래스를 포함 하는 SignalR 서비스에 대 한 연결 정보를 캡슐화 합니다. 허브 클래스와 통신 하려면 직접 만든 프록시 개체 (생성 된 프록시를 사용 하지 않는 경우) 또는 사용자를 위해 생성 된 프록시 개체를 사용 합니다.

클라이언트에서 프록시 이름은 카멜식 대/소문자를 구분 하는 허브 클래스 이름 버전입니다. SignalR는 JavaScript 코드가 JavaScript 규칙을 준수할 수 있도록 이러한 변경을 자동으로 수행 합니다.

**서버의 허브 클래스**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

**허브에 대해 생성 된 클라이언트 프록시에 대 한 참조 가져오기**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

**프록시를 생성 하지 않고 허브 클래스에 대 한 클라이언트 프록시를 만듭니다.**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

허브 클래스를 특성으로 데코레이팅 하는 경우 `HubName` 대/소문자를 변경 하지 않고 정확한 이름을 사용 합니다.

**HubName 특성이 있는 서버의 허브 클래스**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

**허브에 대해 생성 된 클라이언트 프록시에 대 한 참조 가져오기**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

**프록시를 생성 하지 않고 허브 클래스에 대 한 클라이언트 프록시를 만듭니다.**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>서버에서 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법

서버에서 허브를 통해 호출할 수 있는 메서드를 정의 하려면 생성 된 프록시의 속성을 사용 하 여 허브 프록시에 이벤트 처리기를 추가 `client` 하거나 `on` 생성 된 프록시를 사용 하지 않는 경우 메서드를 호출 합니다. 매개 변수는 복잡 한 개체 일 수 있습니다.

메서드를 호출 하기 전에 이벤트 처리기를 추가 `start` 하 여 연결을 설정 합니다. 메서드를 호출한 후 이벤트 처리기를 추가 하려면 `start` 이 문서의 앞부분에서 [연결을 설정](#establishconnection) 하는 방법의 참고를 참조 하 고 생성 된 프록시를 사용 하지 않고 메서드를 정의 하는 데 표시 된 구문을 사용 합니다.

메서드 이름 일치는 대/소문자를 구분 하지 않습니다. 예를 들어 서버에 있는는 `Clients.All.addContosoChatMessageToPage` `AddContosoChatMessageToPage` 클라이언트에서, 또는를 실행 합니다 `addContosoChatMessageToPage` `addcontosochatmessagetopage` .

**클라이언트에서 메서드 정의 (생성 된 프록시 포함)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

**클라이언트에서 메서드를 정의 하는 다른 방법 (생성 된 프록시 포함)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

**클라이언트에서 메서드를 정의 합니다 (생성 된 프록시를 사용 하지 않거나 시작 메서드를 호출한 후 추가 하는 경우).**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

**클라이언트 메서드를 호출 하는 서버 코드**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

다음 예제에서는 복합 개체를 메서드 매개 변수로 포함 합니다.

**클라이언트에서 생성 된 프록시를 사용 하 여 복잡 한 개체를 사용 하는 메서드를 정의 합니다.**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

**클라이언트에서 생성 된 프록시 없이 복잡 한 개체를 사용 하는 메서드를 정의 합니다.**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

**복합 개체를 정의 하는 서버 코드**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

**복합 개체를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>클라이언트에서 서버 메서드를 호출 하는 방법

클라이언트에서 서버 메서드를 호출 하려면 생성 된 프록시를 `server` 사용 하지 않는 경우 생성 된 프록시의 속성 또는 `invoke` 허브 프록시의 메서드를 사용 합니다. 반환 값 또는 매개 변수는 복잡 한 개체 일 수 있습니다.

허브에 있는 메서드 이름의 카멜식 대/소문자 버전을 전달 합니다. SignalR는 JavaScript 코드가 JavaScript 규칙을 준수할 수 있도록 이러한 변경을 자동으로 수행 합니다.

다음 예에서는 반환 값이 없는 서버 메서드를 호출 하는 방법과 반환 값이 있는 서버 메서드를 호출 하는 방법을 보여 줍니다.

**HubMethodName 특성이 없는 서버 메서드**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

**매개 변수에 전달 된 복합 개체를 정의 하는 서버 코드**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

**생성 된 프록시를 사용 하 여 서버 메서드를 호출 하는 클라이언트 코드**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

**생성 된 프록시를 사용 하지 않고 서버 메서드를 호출 하는 클라이언트 코드**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

특성을 사용 하 여 허브 메서드를 데코레이팅하는 경우 `HubMethodName` 대/소문자를 변경 하지 않고 해당 이름을 사용 합니다.

HubMethodName 특성이 있는 **서버 메서드**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

**생성 된 프록시를 사용 하 여 서버 메서드를 호출 하는 클라이언트 코드**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

**생성 된 프록시를 사용 하지 않고 서버 메서드를 호출 하는 클라이언트 코드**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

앞의 예제에서는 반환 값이 없는 서버 메서드를 호출 하는 방법을 보여 줍니다. 다음 예에서는 반환 값이 있는 서버 메서드를 호출 하는 방법을 보여 줍니다.

**반환 값을 포함 하는 메서드의 서버 코드**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

반환 값 **에 사용 되는 스톡 클래스입니다** .

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

**생성 된 프록시를 사용 하 여 서버 메서드를 호출 하는 클라이언트 코드**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

**생성 된 프록시를 사용 하지 않고 서버 메서드를 호출 하는 클라이언트 코드**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>연결 수명 이벤트를 처리 하는 방법

SignalR는 처리할 수 있는 다음 연결 수명 이벤트를 제공 합니다.

- `starting`: 연결을 통해 데이터를 보내기 전에 발생 합니다.
- `received`: 연결에서 데이터를 받을 때 발생 합니다. 받은 데이터를 제공 합니다.
- `connectionSlow`: 클라이언트에서 느리거나 자주 삭제 되는 연결을 검색 하는 경우 발생 합니다.
- `reconnecting`: 기본 전송에서 다시 연결을 시작할 때 발생 합니다.
- `reconnected`: 기본 전송이 다시 연결 되었을 때 발생 합니다.
- `stateChanged`: 연결 상태가 변경 될 때 발생 합니다. 이전 상태와 새 상태 (연결, 연결, 다시 연결 또는 연결 끊김)를 제공 합니다.
- `disconnected`: 연결을 끊을 때 발생 합니다.

예를 들어, 눈에 띄는 지연을 일으킬 수 있는 연결 문제가 있을 때 경고 메시지를 표시 하려면 이벤트를 처리 `connectionSlow` 합니다.

**생성 된 프록시를 사용 하 여 connectionSlow 이벤트를 처리 합니다.**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

**생성 된 프록시를 사용 하지 않고 connectionSlow 이벤트를 처리 합니다.**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

자세한 내용은 [SignalR의 연결 수명 이벤트 이해 및 처리](handling-connection-lifetime-events.md)를 참조 하세요.

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>오류를 처리 하는 방법

SignalR JavaScript 클라이언트는 `error` 에 대 한 처리기를 추가할 수 있는 이벤트를 제공 합니다. 또한 fail 메서드를 사용 하 여 서버 메서드 호출로 인해 발생 하는 오류에 대 한 처리기를 추가할 수 있습니다.

서버에서 자세한 오류 메시지를 명시적으로 사용 하도록 설정 하지 않은 경우 오류 발생 후 SignalR에서 반환 하는 예외 개체는 오류에 대 한 최소 정보를 포함 합니다. 예를 들어,에 대 한 호출이 `newContosoChatMessage` 실패 하면 오류 개체의 오류 메시지에는 `There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.` 보안을 위해 프로덕션 환경에서 클라이언트에 자세한 오류 메시지를 보내는 것이 권장 되지 않습니다. 그러나 문제 해결을 위해 자세한 오류 메시지를 사용 하려면 서버에서 다음 코드를 사용 합니다.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

다음 예제에서는 오류 이벤트에 대 한 처리기를 추가 하는 방법을 보여 줍니다.

**생성 된 프록시를 사용 하 여 오류 처리기 추가**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

**생성 된 프록시를 사용 하지 않고 오류 처리기 추가**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

다음 예제에서는 메서드 호출에서 오류를 처리 하는 방법을 보여 줍니다.

**생성 된 프록시를 사용 하 여 메서드 호출에서 오류를 처리 합니다.**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

**생성 된 프록시를 사용 하지 않고 메서드 호출에서 오류를 처리 합니다.**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

메서드 호출이 실패 하면 `error` 이벤트도 발생 하므로 `error` 메서드 처리기 및 `.fail` 메서드 콜백에서 코드를 실행 합니다.

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법

연결에 대 한 클라이언트 쪽 로깅을 사용 하도록 설정 하려면 메서드를 호출 하 여 연결을 `logging` 설정 하기 전에 connection 개체의 속성을 설정 합니다 `start` .

**생성 된 프록시를 사용 하 여 로깅 사용**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

**로깅 사용 (생성 된 프록시 제외)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

로그를 보려면 브라우저의 개발자 도구를 열고 콘솔 탭으로 이동 합니다. 이 작업을 수행 하는 방법을 보여 주는 단계별 지침 및 스크린 샷을 보여 주는 자습서는 ASP.NET Signalr를 사용 하 [여 서버 브로드캐스트-로깅 사용](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging)을 참조 하세요.
