---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET 시그널R 허브 API 가이드 - 자바 스크립트 클라이언트 | 마이크로 소프트 문서
author: bradygaster
description: 이 문서에서는 브라우저 및 Windows 스토어(WinJS) 어플리케이션과 같은 JavaScript 클라이언트에서 SignalR 버전 2용 허브 API를 사용하는 방법을 소개합니다.
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675714"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a>ASP.NET 시그널R 허브 API 가이드 - 자바 스크립트 클라이언트

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 브라우저 및 Windows 스토어(WinJS) 응용 프로그램과 같은 JavaScript 클라이언트에서 SignalR 버전 2에 대한 허브 API를 사용하는 방법을 소개합니다.
>
> SignalR Hubs API를 사용하면 서버에서 연결된 클라이언트로, 클라이언트에서 서버로 원격 프로시저 호출(RPC)을 수행할 수 있습니다. 서버 코드에서 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다. 클라이언트 코드에서는 서버에서 호출할 수 있는 메서드를 정의하고 서버에서 실행되는 메서드를 호출합니다. SignalR은 모든 클라이언트-서버 배관을 처리합니다.
>
> SignalR는 또한 영구 연결이라는 하위 수준 API를 제공합니다. SignalR, 허브 및 영구 연결에 대한 소개는 [SignalR 소개를](../getting-started/introduction-to-signalr.md)참조하십시오.
>
> ## <a name="software-versions-used-in-this-topic"></a>이 항목에 사용된 소프트웨어 버전
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
> - .NET 4.5
> - 시그널R 버전 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>이 항목의 이전 버전
>
> 이전 버전의 SignalR에 대한 자세한 내용은 [SignalR 이전 버전을](../older-versions/index.md)참조하십시오.
>
> ## <a name="questions-and-comments"></a>질문 및 의견
>
> 이 자습서를 어떻게 좋아했는지, 그리고 페이지 하단의 댓글에서 개선할 수 있는 내용에 대한 피드백을 남겨주세요. 당신은 튜토리얼과 직접 관련이없는 질문이있는 경우, 당신은 [ASP.NET SignalR 포럼에](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 게시하거나 [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>개요

이 문서는 다음 섹션으로 구성됩니다.

- [생성된 프록시 및 프록시가 수행하는 작동](#genproxy)

    - [생성된 프록시를 사용할 시기](#cantusegenproxy)
- [클라이언트 설정](#clientsetup)

    - [동적으로 생성된 프록시를 참조하는 방법](#dynamicproxy)
    - [SignalR 생성 프록시에 대한 실제 파일을 만드는 방법](#manualproxy)
- [연결을 설정하는 방법](#establishconnection)

    - [$.connection.hub는 $.hubConnection()가 생성하는 것과 동일한 개체입니다.](#connequivalence)
    - [시작 메서드의 비동기 실행](#asyncstart)
- [도메인 간 연결을 설정하는 방법](#crossdomain)
- [연결을 구성하는 방법](#configureconnection)

    - [쿼리 문자열 매개 변수를 지정하는 방법](#querystring)
    - [전송 방법을 지정하는 방법](#transport)
- [허브 클래스에 대한 프록시를 얻는 방법](#getproxy)
- [서버가 호출할 수 있는 메서드를 클라이언트에서 정의하는 방법](#callclient)
- [클라이언트에서 서버 메서드를 호출하는 방법](#callserver)
- [연결 수명 이벤트를 처리하는 방법](#connectionlifetime)
- [오류 처리 방법](#handleerrors)
- [클라이언트 측 로깅을 활성화하는 방법](#logging)

서버 또는 .NET 클라이언트를 프로그래밍하는 방법에 대한 설명서는 다음 리소스를 참조하십시오.

- [시그널R 허브 API 가이드 - 서버](hubs-api-guide-server.md)
- [시그널R 허브 API 가이드 - .NET 클라이언트](hubs-api-guide-net-client.md)

SignalR 2 서버 구성 요소는 .NET 4.5에서만 사용할 수 있습니다(.NET 4.0의 SignalR 2용 .NET 클라이언트가 있음).

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a>생성된 프록시 및 프록시가 수행하는 작동

SignalR이 생성하는 프록시유무에 관계없이 JavaScript 클라이언트를 프로그래밍하여 SignalR 서비스와 통신할 수 있습니다. 프록시가 수행하는 일은 연결하는 데 사용하는 코드의 구문을 단순화하고, 서버에서 호출하는 메서드를 작성하고, 서버에서 메서드를 호출하는 것입니다.

서버 메서드를 호출하는 코드를 작성할 때 생성된 프록시를 사용하면 로컬 함수를 실행하는 것처럼 보이는 구문을 `serverMethod(arg1, arg2)` 사용할 `invoke('serverMethod', arg1, arg2)`수 있습니다. 또한 생성된 프록시 구문을 사용하면 서버 메서드 이름을 잘못 입력하는 경우 즉각적이고 이해하기 쉬운 클라이언트 측 오류가 발생합니다. 프록시를 정의하는 파일을 수동으로 만드는 경우 서버 메서드를 호출하는 코드를 작성하기 위한 IntelliSense 지원을 받을 수도 있습니다.

예를 들어 서버에 다음과 같은 Hub 클래스가 있다고 가정합니다.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

다음 코드 예제에서는 서버에서 `NewContosoChatMessage` 메서드를 호출하고 서버에서 `addContosoChatMessageToPage` 메서드 호출을 수신하기 위해 JavaScript 코드가 어떻게 보이는지 보여 준다.

**생성된 프록시를 사용하면**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

**생성된 프록시 가 없는 경우**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a>생성된 프록시를 사용할 시기

서버가 호출하는 클라이언트 메서드에 대해 여러 이벤트 처리기를 등록하려면 생성된 프록시를 사용할 수 없습니다. 그렇지 않으면 생성된 프록시를 사용하거나 코딩 기본 설정에 따라 사용하지 않도록 선택할 수 있습니다. 사용하지 않도록 선택하면 클라이언트 코드의 요소에서 "시그널/허브" URL을 `script` 참조할 필요가 없습니다.

<a id="clientsetup"></a>

## <a name="client-setup"></a>클라이언트 설치

자바 스크립트 클라이언트는 jQuery 및 SignalR 코어 자바 스크립트 파일에 대한 참조가 필요합니다. jQuery 버전은 1.6.4 또는 1.7.2, 1.8.2 또는 1.9.1과 같은 주요 이후 버전이어야 합니다. 생성된 프록시를 사용하기로 결정한 경우 SignalR생성 프록시 JavaScript 파일에 대한 참조도 필요합니다. 다음 예제에서는 생성된 프록시를 사용하는 HTML 페이지에서 참조의 모양을 보여 주며 있습니다.

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

이러한 참조는 이 순서에 포함되어야 합니다: jQuery 먼저, 그 후 SignalR 코어, 그리고 SignalR 프록시마지막.

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a>동적으로 생성된 프록시를 참조하는 방법

앞의 예에서 SignalR 생성 프록시에 대한 참조는 물리적 파일이 아닌 동적으로 생성된 JavaScript 코드를 참조하는 것입니다. SignalR은 즉석에서 프록시에 대한 자바 스크립트 코드를 생성하고 "/ 신호기 / 허브"URL에 대한 응답으로 클라이언트에 제공합니다. `MapSignalR` 메서드의 서버에서 SignalR 연결에 대해 다른 기본 URL을 지정한 경우 동적으로 생성된 프록시 파일의 URL은 "/hubs"가 추가된 사용자 지정 URL입니다.

> [!NOTE]
> Windows 8(Windows 스토어) JavaScript 클라이언트의 경우 동적으로 생성된 프록시 파일 대신 물리적 프록시 파일을 사용합니다. 자세한 내용은 이 항목의 후반부에서 [SignalR 생성 프록시에 대한 실제 파일을 만드는 방법을](#manualproxy) 참조하세요.

ASP.NET MVC 4 또는 5 Razor 보기에서 물결표를 사용하여 프록시 파일 참조의 응용 프로그램 루트를 참조합니다.

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

MVC 5에서 SignalR 사용에 대한 자세한 내용은 [SignalR 및 MVC 5로 시작하기](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)를 참조하십시오.

ASP.NET MVC 3 Razor 보기에서 프록시 파일 참조에 사용합니다. `Url.Content`

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

ASP.NET Web Forms 응용 `ResolveClientUrl` 프로그램에서 프록시 파일 참조에 사용하거나 앱 루트 상대 경로(물결선으로 시작)를 사용하여 ScriptManager를 통해 등록합니다.

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

일반적으로 CSS 또는 JavaScript 파일에 사용하는 "/시그널러/허브" URL을 지정하는 데 동일한 방법을 사용합니다. 물결표를 사용하지 않고 URL을 지정하는 경우 일부 시나리오에서는 IIS Express를 사용하여 Visual Studio에서 테스트할 때 응용 프로그램이 올바르게 작동하지만 전체 IIS에 배포할 때 404 오류가 발생합니다. 자세한 내용은 MSDN 사이트의 [웹 프로젝트에 대한 Visual Studio의 웹 서버의](https://msdn.microsoft.com/library/58wxa9w5.aspx) 루트 수준 리소스 에 대한 참조 **해결을** ASP.NET.

디버그 모드에서 Visual Studio 2017에서 웹 프로젝트를 실행하고 Internet Explorer를 브라우저로 사용하는 경우 스크립트 아래의 **솔루션 탐색기에서** 프록시 파일을 볼 수 **있습니다.**

파일의 내용을 보려면 허브를 두 번 **클릭합니다.** Visual Studio 2012 또는 2013 및 Internet Explorer를 사용하지 않거나 디버그 모드에 있지 않은 경우 "/signalR/hubs" URL을 탐색하여 파일내용을 얻을 수도 있습니다. 예를 들어 사이트에서 사이트가 실행 `http://localhost:56699`중인 `http://localhost:56699/SignalR/hubs` 경우 브라우저에서 로 이동합니다.

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a>SignalR 생성 프록시에 대한 실제 파일을 만드는 방법

동적으로 생성된 프록시대신 프록시 코드가 있는 물리적 파일을 만들고 해당 파일을 참조할 수 있습니다. 캐싱 또는 번들 동작을 제어하거나 서버 메서드에 대한 호출을 코딩할 때 IntelliSense를 얻으려면 이 작업을 수행할 수 있습니다.

프록시 파일을 만들려면 다음 단계를 수행합니다.

1. 마이크로 [소프트.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet 패키지를 설치합니다.
2. 명령 프롬프트를 열고 SignalR.exe 파일이 포함된 *도구* 폴더를 찾아봅습니다. 도구 폴더는 다음과 같은 위치에 있습니다.

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. 다음 명령을 입력합니다.

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    *.dll에* 대한 경로는 일반적으로 프로젝트 폴더의 *bin* 폴더입니다.

    이 명령은 *signalr.exe와*동일한 폴더에 *server.js라는* 파일을 만듭니다.
4. *server.js* 파일을 프로젝트의 적절한 폴더에 넣고 응용 프로그램에 적합한 이름으로 이름을 변경한 다음 "signalr/hubs" 참조 대신 에 대한 참조를 추가합니다.

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>연결을 설정하는 방법

연결을 설정하려면 연결 개체를 만들고, 프록시를 만들고, 서버에서 호출할 수 있는 메서드에 대한 이벤트 처리기를 등록해야 합니다. 프록시 및 이벤트 처리기가 설정되면 `start` 메서드를 호출하여 연결을 설정합니다.

생성된 프록시를 사용하는 경우 생성된 프록시 코드가 사용자용으로 수행되므로 자체 코드에서 연결 개체를 만들 필요가 없습니다.

<a id="nogenconnection"></a>

**연결 설정(생성된 프록시).**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

**생성된 프록시 없이 연결 설정**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

샘플 코드는 기본 "/signalr" URL을 사용하여 SignalR 서비스에 연결합니다. 다른 기본 URL을 지정하는 방법에 대한 자세한 내용은 [ASP.NET SignalR 허브 API 가이드 - 서버 - /signalr URL을](hubs-api-guide-server.md#signalrurl)참조하십시오.

기본적으로 허브 위치는 현재 서버입니다. 다른 서버에 연결하는 경우 다음 예제와 같이 `start` 메서드를 호출하기 전에 URL을 지정합니다.

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> 일반적으로 연결을 설정 하기 위해 `start` 메서드를 호출 하기 전에 이벤트 처리기를 등록 합니다. 연결을 설정한 후 일부 이벤트 처리기를 등록하려면 이 작업을 수행할 수 있지만 `start` 메서드를 호출하기 전에 이벤트 처리기 중 하나 이상을 등록해야 합니다. 한 가지 이유는 응용 프로그램에 많은 Hubs가 있을 수 있지만 그 중 `OnConnected` 하나만 사용하려는 경우 모든 Hub에서 이벤트를 트리거하지 않으려는 것입니다. 연결이 설정되면 Hub의 프록시에 클라이언트 메서드가 있으면 SignalR이 `OnConnected` 이벤트를 트리거하도록 지시합니다. `start` 메서드를 호출하기 전에 이벤트 처리기를 등록하지 않으면 Hub에서 메서드를 호출할 수 있지만 Hub의 `OnConnected` 메서드는 호출되지 않으며 서버에서 클라이언트 메서드가 호출되지 않습니다.

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a>$.connection.hub는 $.hubConnection()가 생성하는 것과 동일한 개체입니다.

예제에서 볼 수 있듯이 생성된 프록시를 사용할 `$.connection.hub` 때 연결 개체를 참조합니다. 생성된 프록시를 사용하지 않을 때 `$.hubConnection()` 호출하여 얻는 것과 동일한 개체입니다. 생성된 프록시 코드는 다음 문을 실행하여 연결을 만듭니다.

![생성된 프록시 파일에서 연결 만들기](hubs-api-guide-javascript-client/_static/image3.png)

생성된 프록시를 사용하는 경우 생성된 프록시를 `$.connection.hub` 사용하지 않을 때 연결 개체로 수행할 수 있는 작업을 수행할 수 있습니다.

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a>시작 메서드의 비동기 실행

메서드는 `start` 비동기적으로 실행됩니다. "를 호출하여 `pipe` `done`콜백 함수를 추가할 수 있는 [jQuery 지연 개체를](http://api.jquery.com/category/deferred-object/) `fail`반환합니다. 서버 메서드에 대한 호출과 같이 연결이 설정된 후 실행하려는 코드가 있는 경우 해당 코드를 콜백 함수에 넣거나 콜백 함수에서 호출합니다. 콜백 메서드는 `.done` 연결이 설정된 후 실행되며 서버의 `OnConnected` 이벤트 처리기 메서드에 있는 코드가 실행된 후에 실행됩니다.

메서드 호출 후 `start` 다음 코드 줄로 `.done` 앞예제예제의 "Now Connected" 문을 넣으면 다음 예제와 `console.log` 같이 연결이 설정되기 전에 줄이 실행됩니다.

![연결이 설정된 후 실행되는 코드를 작성하는 잘못된 방법](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a>도메인 간 연결을 설정하는 방법

일반적으로 브라우저에서 페이지를 로드하는 경우 `http://contoso.com`에서 SignalR 연결이 동일한 `http://contoso.com/signalr`도메인에 있습니다. 에서 `http://contoso.com` 페이지가 `http://fabrikam.com/signalr`에 연결하는 경우 도메인 간 연결입니다. 보안상의 이유로 도메인 간 연결은 기본적으로 비활성화됩니다.

SignalR 1.x에서 교차 도메인 요청은 단일 EnableCrossDomain 플래그에 의해 제어되었습니다. 이 플래그는 JSONP 및 CORS 요청을 모두 제어했습니다. 유연성을 높이기 위해 모든 CORS 지원이 SignalR의 서버 구성 요소에서 제거되었습니다(JavaScript 클라이언트는 브라우저가 지원하는 것으로 감지되는 경우 CORS를 정상적으로 사용함) 이러한 시나리오를 지원하기 위해 새로운 OWIN 미들웨어를 사용할 수 있게 되었습니다.

클라이언트에서 JSONP가 필요한 경우(이전 브라우저에서 도메인 간 요청을 지원하려면 아래와 같이 `EnableJSONP` `HubConfiguration` 개체를 `true`에 설정하여 명시적으로 사용하도록 설정해야 합니다.) JSONP는 CORS보다 안전하지 때문에 기본적으로 비활성화됩니다.

**프로젝트에 Microsoft.Owin.Cors 추가:** 이 라이브러리를 설치하려면 패키지 관리자 콘솔에서 다음 명령을 실행합니다.

`Install-Package Microsoft.Owin.Cors`

이 명령은 2.1.0 버전의 패키지를 프로젝트에 추가합니다.

### <a name="calling-usecors"></a>유즈코르 스

 다음 코드 조각은 SignalR 2에서 도메인 간 연결을 구현하는 방법을 보여 줍니다.

**SignalR 2에서 도메인 간 요청 구현**

다음 코드는 SignalR 2 프로젝트에서 CORS 또는 JSONP를 사용하도록 설정하는 방법을 보여 줍니다. 이 코드 `Map` 샘플은 `RunSignalR` `MapSignalR`CORS 미들웨어가 CORS 지원이 필요한 SignalR 요청에 대해서만 실행되도록 을 대신 사용하며 `MapSignalR`.에 지정된 경로의 모든 트래픽에 대해 실행됩니다. 맵은 전체 응용 프로그램이 아니라 특정 URL 접두사에 대해 실행해야 하는 다른 미들웨어에도 사용할 수 있습니다.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - 코드에서 true로 설정하지 `jQuery.support.cors` 마십시오.
>
>     ![jQuery.support.cors를 true로 설정하지 마십시오.](hubs-api-guide-javascript-client/_static/image7.png)
>
>     SignalR는 CORS 사용을 처리합니다. true로 설정하면 `jQuery.support.cors` SignalR이 브라우저가 CORS를 지원한다고 가정하기 때문에 JSONP가 비활성화됩니다.
> - 로컬 호스트 URL에 연결할 때 Internet Explorer 10은 도메인 간 연결로 간주하지 않으므로 서버에서 도메인 간 연결을 활성화하지 않은 경우에도 응용 프로그램이 IE 10에서 로컬로 작동합니다.
> - Internet Explorer 9에서 도메인 간 연결을 사용하는 자세한 내용은 [이 StackOverflow 스레드를](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)참조하십시오.
> - Chrome에서 도메인 간 연결을 사용하는 자세한 내용은 [이 StackOverflow 스레드를](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)참조하십시오.
> - 샘플 코드는 기본 "/signalr" URL을 사용하여 SignalR 서비스에 연결합니다. 다른 기본 URL을 지정하는 방법에 대한 자세한 내용은 [ASP.NET SignalR 허브 API 가이드 - 서버 - /signalr URL을](hubs-api-guide-server.md#signalrurl)참조하십시오.

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>연결을 구성하는 방법

연결을 설정하기 전에 쿼리 문자열 매개 변수를 지정하거나 전송 메서드를 지정할 수 있습니다.

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>쿼리 문자열 매개 변수를 지정하는 방법

클라이언트가 연결할 때 서버에 데이터를 보내려면 연결 개체에 쿼리 문자열 매개 변수를 추가할 수 있습니다. 다음 예제에서는 클라이언트 코드에서 쿼리 문자열 매개 변수를 설정하는 방법을 보여 주습니다.

**시작 메서드를 호출하기 전에 쿼리 문자열 값을 설정합니다(생성된 프록시 사용)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

**시작 메서드를 호출하기 전에 쿼리 문자열 값을 설정합니다(생성된 프록시 제외).**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

다음 예제에서는 서버 코드에서 쿼리 문자열 매개 변수를 읽는 방법을 보여 주입니다.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>전송 방법을 지정하는 방법

연결하는 프로세스의 일부로 SignalR 클라이언트는 일반적으로 서버와 협상하여 서버와 클라이언트 모두에서 지원되는 최상의 전송을 결정합니다. 사용하려는 전송을 이미 알고 있는 경우 메서드를 호출할 때 전송 메서드를 지정하여 이 협상 프로세스를 `start` 우회할 수 있습니다.

**전송 메서드를 지정하는 클라이언트 코드(생성된 프록시 사용)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

**전송 메서드를 지정하는 클라이언트 코드(생성된 프록시 제외)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

또는 SignalR을 시도할 순서대로 여러 전송 메서드를 지정할 수 있습니다.

**사용자 지정 전송 대체 체계를 지정하는 클라이언트 코드(생성된 프록시).**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

**생성된 프록시 없이 사용자 지정 전송 대체 스키마를 지정하는 클라이언트 코드**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

전송 메서드를 지정할 때 다음 값을 사용할 수 있습니다.

- "웹 소켓"
- "포에버프레임"
- "서버센트이벤트"
- "롱폴링"

다음 예제는 연결에서 사용 중인 전송 방법을 확인하는 방법을 보여 주며 있습니다.

**연결에서 사용되는 전송 방법을 표시하는 클라이언트 코드(생성된 프록시 사용)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

**생성된 프록시 없이 연결에서 사용하는 전송 방법을 표시하는 클라이언트 코드**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

서버 코드에서 전송 방법을 확인하는 방법에 대한 자세한 내용은 [ASP.NET SignalR Hubs API 가이드 - 서버 - Context 속성에서 클라이언트에 대한 정보를 얻는 방법을](hubs-api-guide-server.md#contextproperty)참조하십시오. 전송 및 대체에 대한 자세한 내용은 [SignalR - 전송 및 대체 소개를](../getting-started/introduction-to-signalr.md#transports)참조하십시오.

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a>허브 클래스에 대한 프록시를 얻는 방법

만드는 각 연결 개체는 하나 이상의 Hub 클래스를 포함하는 SignalR 서비스에 대한 연결에 대한 정보를 캡슐화합니다. Hub 클래스와 통신하려면 생성된 프록시를 사용하지 않는 경우 또는 생성되는 프록시 개체를 사용합니다.

클라이언트에서 프록시 이름은 Hub 클래스 이름의 낙타 대/소문자 버전입니다. SignalR은 자바스크립트 코드가 자바스크립트 규칙을 준수할 수 있도록 자동으로 변경합니다.

**서버의 허브 클래스**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

**허브에 대해 생성된 클라이언트 프록시에 대한 참조를 가져옵니다.**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

**생성된 프록시 없이 Hub 클래스에 대한 클라이언트 프록시 만들기**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

특성으로 Hub 클래스를 `HubName` 장식하는 경우 대/소문자를 변경하지 않고 정확한 이름을 사용합니다.

**HubName 특성이 있는 서버의 허브 클래스**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

**허브에 대해 생성된 클라이언트 프록시에 대한 참조를 가져옵니다.**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

**생성된 프록시 없이 Hub 클래스에 대한 클라이언트 프록시 만들기**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>서버가 호출할 수 있는 메서드를 클라이언트에서 정의하는 방법

서버가 Hub에서 호출할 수 있는 메서드를 정의하려면 생성된 프록시의 `client` 속성을 사용하여 Hub 프록시에 `on` 이벤트 처리기를 추가하거나 생성된 프록시를 사용하지 않는 경우 메서드를 호출합니다. 매개 변수는 복잡한 개체일 수 있습니다.

연결을 설정 하기 위해 `start` 메서드를 호출 하기 전에 이벤트 처리기를 추가 합니다. 메서드를 호출한 `start` 후 이벤트 처리기를 추가하려면 이 문서의 앞에서 [연결을 설정하는 방법과](#establishconnection) 생성된 프록시를 사용하지 않고 메서드를 정의하는 데 표시된 구문을 사용하는 방법에 대한 참고를 참조하십시오.

메서드 이름 일치는 대/소문자를 구분하지 않습니다. 예를 들어 `Clients.All.addContosoChatMessageToPage` 서버에서 를 `AddContosoChatMessageToPage` `addContosoChatMessageToPage`실행하거나 `addcontosochatmessagetopage` 클라이언트에서 실행합니다.

**클라이언트에서 메서드 정의(생성된 프록시 사용)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

**클라이언트에서 메서드를 정의하는 다른 방법(생성된 프록시 사용)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

**클라이언트에서 메서드 정의(생성된 프록시 없이 또는 시작 메서드를 호출한 후 추가하는 경우)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

**클라이언트 메서드를 호출하는 서버 코드**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

다음 예제에는 메서드 매개 변수로 복잡한 개체가 포함됩니다.

**생성된 프록시를 사용하여 복잡한 개체를 사용하는 클라이언트에서 메서드 정의**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

**생성된 프록시 없이 복잡한 개체를 사용하는 클라이언트에서 메서드 정의**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

**복잡한 개체를 정의하는 서버 코드**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

**복잡한 개체를 사용하여 클라이언트 메서드를 호출하는 서버 코드**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>클라이언트에서 서버 메서드를 호출하는 방법

클라이언트에서 서버 메서드를 호출하려면 `server` 생성된 프록시를 사용하지 `invoke` 않는 경우 생성된 프록시또는 Hub 프록시에서 메서드의 속성을 사용합니다. 반환 값 또는 매개 변수는 복잡한 개체일 수 있습니다.

Hub에서 메서드 이름의 낙타 대/소문자 버전을 전달합니다. SignalR은 자바스크립트 코드가 자바스크립트 규칙을 준수할 수 있도록 자동으로 변경합니다.

다음 예제는 반환 값이 없는 서버 메서드를 호출 하는 방법과 반환 값이 있는 서버 메서드를 호출 하는 방법을 보여 주입니다.

**HubMethodName 특성이 없는 서버 메서드**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

**매개 변수에서 전달된 복잡한 개체를 정의하는 서버 코드**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

**서버 메서드를 호출하는 클라이언트 코드(생성된 프록시 포함)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

**서버 메서드를 호출하는 클라이언트 코드(생성된 프록시 제외)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

Hub 메서드를 특성으로 `HubMethodName` 장식한 경우 대/소문자를 변경하지 않고 해당 이름을 사용합니다.

HubMethodName 특성이 있는 **서버 메서드**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

**서버 메서드를 호출하는 클라이언트 코드(생성된 프록시 포함)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

**서버 메서드를 호출하는 클라이언트 코드(생성된 프록시 제외)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

앞의 예제는 반환 값이 없는 서버 메서드를 호출하는 방법을 보여 주며 있습니다. 다음 예제는 반환 값이 있는 서버 메서드를 호출 하는 방법을 보여 주입니다.

**반환 값이 있는 메서드의 서버 코드**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

반환 **값에 사용되는 Stock 클래스**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

**서버 메서드를 호출하는 클라이언트 코드(생성된 프록시 포함)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

**서버 메서드를 호출하는 클라이언트 코드(생성된 프록시 제외)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>연결 수명 이벤트를 처리하는 방법

SignalR은 처리할 수 있는 다음과 같은 연결 수명 이벤트를 제공합니다.

- `starting`: 연결을 통해 데이터를 전송하기 전에 발생합니다.
- `received`: 연결시 데이터가 수신될 때 발생합니다. 수신된 데이터를 제공합니다.
- `connectionSlow`: 클라이언트가 느리거나 자주 끊어지는 연결을 감지할 때 발생합니다.
- `reconnecting`: 기본 전송이 다시 연결될 때 발생합니다.
- `reconnected`: 기본 전송이 다시 연결될 때 발생합니다.
- `stateChanged`: 연결 상태가 변경될 때 발생합니다. 이전 상태와 새 상태(연결, 연결, 다시 연결 또는 연결이 끊긴 됨)를 제공합니다.
- `disconnected`: 연결이 끊어졌을 때 발생합니다.

예를 들어 눈에 띄는 지연을 일으킬 수 있는 연결 문제가 있을 `connectionSlow` 때 경고 메시지를 표시하려면 이벤트를 처리합니다.

**연결 처리느린 이벤트(생성된 프록시)를 사용합니다.**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

**연결 처리Slow 이벤트(생성된 프록시 제외)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

자세한 내용은 [SignalR의 연결 수명 이벤트 이해 및 처리를](handling-connection-lifetime-events.md)참조하십시오.

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>오류 처리 방법

SignalR JavaScript 클라이언트는 `error` 처리기를 추가할 수 있는 이벤트를 제공합니다. fail 메서드를 사용하여 서버 메서드 호출로 인한 오류에 대한 처리기를 추가할 수도 있습니다.

서버에서 자세한 오류 메시지를 명시적으로 활성화하지 않으면 오류 후 SignalR이 반환하는 예외 개체에는 오류에 대한 최소한의 정보가 포함됩니다. 예를 들어 호출이 `newContosoChatMessage` 실패하는 경우 오류 개체의 오류`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`메시지에는 "프로덕션 환경에서 클라이언트에 자세한 오류 메시지를 보내는 것은 보안상의 이유로 권장되지 않지만 문제 해결을 위해 자세한 오류 메시지를 사용하도록 설정하려면 서버에서 다음 코드를 사용합니다.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

다음 예제에서는 오류 이벤트에 대 한 처리기를 추가 하는 방법을 보여 주며 있습니다.

**오류 처리기 추가(생성된 프록시 사용)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

**오류 처리기 추가(생성된 프록시 제외)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

다음 예제에서는 메서드 호출에서 오류를 처리하는 방법을 보여 주었습니다.

**메서드 호출에서 오류를 처리(생성된 프록시 사용)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

**메서드 호출에서 오류를 처리합니다(생성된 프록시 제외).**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

메서드 호출에 실패 하면 `error` 이벤트도 발생 하므로 `error` 메서드 처리기및 메서드 `.fail` 콜백의 코드가 실행 됩니다.

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>클라이언트 측 로깅을 활성화하는 방법

연결에 클라이언트 측 로깅을 사용하려면 `logging` `start` 메서드를 호출하기 전에 연결 개체의 속성을 설정하여 연결을 설정합니다.

**로깅 사용(생성된 프록시 사용)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

**로깅 사용(생성된 프록시 제외)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

로그를 보려면 브라우저의 개발자 도구를 열고 콘솔 탭으로 이동합니다. 이 작업을 수행하는 방법을 보여 주는 단계별 지침 및 스크린 샷을 보여 주는 자습서의 경우 [ASP.NET 시그널러를 사용하여 서버 브로드캐스트 - 로깅 사용 을](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging)참조하세요.
