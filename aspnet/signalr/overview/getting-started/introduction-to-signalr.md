---
uid: signalr/overview/getting-started/introduction-to-signalr
title: 시그널R 소개 | 마이크로 소프트 문서
author: bradygaster
description: 이 문서에서는 SignalR이 무엇인지, 그리고 이를 만들도록 설계된 솔루션 중 일부에 대해 설명합니다.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 8dbc31a5c8d59fa55dc5b513c1a51d24d18a685f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675942"
---
# <a name="introduction-to-signalr"></a>SignalR 소개

로 [패트릭 플레처](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 SignalR이 무엇인지, 그리고 이를 만들도록 설계된 솔루션 중 일부에 대해 설명합니다. 
> 
> ## <a name="questions-and-comments"></a>질문 및 의견
> 
> 이 자습서를 어떻게 좋아했는지, 그리고 페이지 하단의 댓글에서 개선할 수 있는 내용에 대한 피드백을 남겨주세요. 당신은 튜토리얼과 직접 관련이없는 질문이있는 경우, 당신은 [ASP.NET SignalR 포럼에](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 게시하거나 [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr).

## <a name="what-is-signalr"></a>시그널R이란?

ASP.NET SignalR은 응용 프로그램에 실시간 웹 기능을 추가하는 프로세스를 간소화하는 ASP.NET 개발자를 위한 라이브러리입니다. 실시간 웹 기능은 서버가 클라이언트가 새 데이터를 요청할 때까지 기다리지 않고 서버 코드가 연결된 클라이언트에 콘텐츠를 푸시하는 기능을 사용할 수 있게 되면 즉시 사용할 수 있도록 하는 기능입니다.

SignalR은 ASP.NET 응용 프로그램에 모든 종류의 "실시간" 웹 기능을 추가하는 데 사용할 수 있습니다. 채팅은 종종 예로 사용되지만 훨씬 더 많은 작업을 수행할 수 있습니다. 사용자가 새 데이터를 보기 위해 웹 페이지를 새로 고치거나 페이지가 새 데이터를 검색하기 위해 [긴 폴링을](http://en.wikipedia.org/wiki/Push_technology#Long_polling) 구현할 때마다 SignalR을 사용할 수 있습니다. 예를 들어 대시보드 및 모니터링 응용 프로그램, 공동 작업 응용 프로그램(예: 문서 동시 편집), 작업 진행 률 업데이트 및 실시간 양식이 있습니다.

SignalR은 또한 서버에서 고주파 업데이트가 필요한 완전히 새로운 유형의 웹 애플리케이션(예: 실시간 게임)을 지원합니다.

SignalR은 서버 측 .NET 코드에서 클라이언트 브라우저(및 기타 클라이언트 플랫폼)에서 JavaScript 함수를 호출하는 RPC(서버 간 원격 프로시저 호출)를 만들기 위한 간단한 API를 제공합니다. SignalR에는 연결 관리(예: 이벤트 연결 및 연결 해제) 및 연결 그룹화용 API도 포함됩니다.

![SignalR을 사용 하 고 메서드를 호출](introduction-to-signalr/_static/image1.png)

SignalR은 연결 관리를 자동으로 처리하며, 대화방처럼 메시지를 연결된 모든 클라이언트에 동시에 브로드캐스트할 수 있습니다. 메시지를 특정 클라이언트에 보낼 수도 있습니다. 클라이언트와 서버 간의 연결은 기존 HTTP 연결과 달리 영구적이며, 각 통신에 대해 다시 설정됩니다.

SignalR은 서버 코드가 현재 웹에서 일반적인 요청 응답 모델이 아니라 RPC(원격 프로시저 호출)를 사용하여 브라우저에서 클라이언트 코드에 호출할 수 있는 "서버 푸시" 기능을 지원합니다.

SignalR 애플리케이션은 기본 제공 및 타사 확장 공급자를 사용하여 수천 개의 클라이언트로 확장할 수 있습니다.

기본 제공 공급자는 다음과 같습니다.
* [Service Bus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [SQL Server](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [Redis](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

타사 공급자는 다음과 같습니다.
* [N캐시](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).

SignalR은 [GitHub를](https://github.com/signalr)통해 액세스할 수 있는 오픈 소스입니다.

## <a name="signalr-and-websocket"></a>시그널러 및 웹소켓

SignalR은 사용 가능한 경우 새 WebSocket 전송을 사용하며 필요한 경우 이전 전송으로 돌아갑니다. WebSocket을 사용하여 앱을 직접 작성할 수 있지만 SignalR을 사용하면 구현해야 하는 많은 추가 기능이 이미 완료되었습니다. 가장 중요한 것은 이전 클라이언트에 대한 별도의 코드 경로를 만들지 않고도 WebSocket을 활용하도록 앱을 코딩할 수 있다는 것입니다. 또한 SignalR은 기본 전송의 변경 사항을 지원하도록 업데이트되어 응용 프로그램에 WebSocket 버전 간에 일관된 인터페이스를 제공하므로 WebSocket 업데이트에 대해 걱정할 필요가 없습니다.

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a>운송 및 대체

SignalR은 클라이언트와 서버 간에 실시간 작업을 수행하는 데 필요한 일부 전송에 대한 추상화입니다. SignalR 연결은 HTTP로 시작하여 사용 가능한 경우 WebSocket 연결로 승격됩니다. WebSocket은 서버 메모리를 가장 효율적으로 사용하고 대기 시간이 가장 낮으며 가장 기본적인 기능(예: 클라이언트와 서버 간의 전체 이중 통신)을 가지므로 SignalR에 이상적인 전송수단이지만, 가장 엄격한 요구 사항도 있습니다. 이러한 요구 사항이 충족되지 않으면 SignalR은 다른 전송을 사용하여 연결을 시도합니다.

### <a name="html-5-transports"></a>HTML 5 전송

이러한 전송은 HTML [5에](http://en.wikipedia.org/wiki/HTML5)대한 지원에 따라 달라집니다. 클라이언트 브라우저가 HTML 5 표준을 지원하지 않는 경우 이전 전송이 사용됩니다.

- **WebSocket(서버와** 브라우저 가 모두 Websocket을 지원할 수 있음을 나타내는 경우) WebSocket은 클라이언트와 서버 간의 진정한 지속적 양방향 연결을 설정하는 유일한 전송입니다. 그러나 WebSocket에는 가장 엄격한 요구 사항도 있습니다. 그것은 완전히 마이크로 소프트 인터넷 익스플로러의 최신 버전에서 만 지원, 구글 크롬, 모질라 파이어 폭스, 오페라와 사파리와 같은 다른 브라우저에서 부분 구현만.
- EventSource라고도 하는 **서버 전송 이벤트(브라우저가**Internet Explorer를 제외한 기본적으로 모든 브라우저인 서버 전송 이벤트를 지원하는 경우).

### <a name="comet-transports"></a>혜성 수송

다음 전송은 브라우저 또는 다른 클라이언트가 오래 유지된 HTTP 요청을 유지 관리하는 [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) 웹 응용 프로그램 모델을 기반으로 하며, 서버는 클라이언트가 특별히 요청하지 않고 클라이언트에 데이터를 푸시하는 데 사용할 수 있습니다.

- **영원히 프레임** (인터넷 익스플로러 전용). Forever Frame은 완료되지 않은 서버의 끝점에 요청을 하는 숨겨진 IFrame을 만듭니다. 그런 다음 서버는 즉시 실행되는 스크립트를 클라이언트로 계속 전송하여 서버에서 클라이언트로의 단방향 실시간 연결을 제공합니다. 클라이언트에서 서버로의 연결은 서버에서 클라이언트 연결로의 별도의 연결을 사용하며 표준 HTTP 요청과 마찬가지로 전송해야 하는 각 데이터에 대해 새 연결이 만들어집니다.
- **아약스 긴 폴링**. 긴 폴링은 영구 연결을 만들지 않지만 대신 서버가 응답할 때까지 열려 있는 요청으로 서버를 폴링하고, 이 시점에서 연결이 닫히고 새 연결이 즉시 요청됩니다. 이렇게 하면 연결이 재설정되는 동안 약간의 대기 시간이 발생할 수 있습니다.

어떤 구성에서 지원되는 전송에 대한 자세한 내용은 [지원되는 플랫폼을](supported-platforms.md)참조하십시오.

### <a name="transport-selection-process"></a>운송 선택 프로세스

다음 목록은 SignalR에서 사용할 전송을 결정하는 데 사용하는 단계를 보여 주며 있습니다.

1. 브라우저가 Internet Explorer 8 이전인 경우 긴 폴링이 사용됩니다.
2. JSONP가 구성된 경우(즉, `jsonp` 매개 변수가 `true` 연결이 시작될 때로 설정됨) 긴 폴링이 사용됩니다.
3. 도메인 간 연결이 이루어지는 경우(즉, SignalR 끝점이 호스팅 페이지와 동일한 도메인에 없는 경우) 다음 기준이 충족되면 WebSocket이 사용됩니다.

   - 클라이언트는 CORS(원본 간 리소스 공유)를 지원합니다. CORS를 지원하는 클라이언트에 대한 자세한 내용은 [caniuse.com CORS를](http://www.caniuse.com/CORS)참조하십시오.
   - 클라이언트는 웹 소켓을 지원합니다.
   - 서버는 웹 소켓을 지원합니다.

     이러한 기준 중 어느 것이라도 충족되지 않으면 긴 폴링이 사용됩니다. 도메인 간 연결에 대한 자세한 내용은 [도메인 간 연결을 설정하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)참조하세요.
4. JSONP가 구성되지 않고 연결이 도메인 간이 아닌 경우 클라이언트와 서버가 모두 지원하는 경우 WebSocket이 사용됩니다.
5. 클라이언트 또는 서버가 WebSocket을 지원하지 않는 경우 서버 전송 이벤트를 사용할 수 있는 경우 사용됩니다.
6. 서버 전송 이벤트를 사용할 수 없는 경우 영원히 프레임이 시도됩니다.
7. 영원히 프레임이 실패하면 긴 폴링이 사용됩니다.

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a>전송 모니터링

허브에 로깅을 활성화하고 브라우저에서 콘솔 창을 열어 응용 프로그램이 사용하는 전송을 확인할 수 있습니다.

브라우저에서 허브 의 이벤트에 대한 로깅을 사용하려면 클라이언트 응용 프로그램에 다음 명령을 추가합니다.

`$.connection.hub.logging = true;`

- 인터넷 익스플로러에서 F12를 눌러 개발자 도구를 열고 콘솔 탭을 클릭합니다.

    ![마이크로소프트 인터넷 익스플로러의 콘솔](introduction-to-signalr/_static/image2.png)
- 크롬에서 Ctrl+Shift+J를 눌러 본체를 엽니다.

    ![구글 크롬의 콘솔](introduction-to-signalr/_static/image3.png)

콘솔을 열고 로깅을 사용하도록 설정하면 SignalR에서 사용 중인 전송을 확인할 수 있습니다.

![웹 소켓 전송을 보여주는 인터넷 익스플로러의 콘솔](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a>전송 지정

전송을 협상하는 데는 일정 한 시간과 클라이언트/서버 리소스가 필요합니다. 클라이언트 기능이 알려진 경우 클라이언트 연결을 시작할 때 전송을 지정할 수 있습니다. 다음 코드 스니펫은 클라이언트가 다른 프로토콜을 지원하지 않는 것으로 알려진 경우와 마찬가지로 Ajax Long Polling 전송을 사용하여 연결을 시작하는 것을 보여 줍니다.

`connection.start({ transport: 'longPolling' });`

클라이언트가 특정 전송을 순서대로 시도하도록 하려면 대체 순서를 지정할 수 있습니다. 다음 코드 스니펫은 WebSocket을 시도하고 실패하여 Long Polling로 직접 이동했음을 보여 줍니다.

`connection.start({ transport: ['webSockets','longPolling'] });`

전송을 지정하기 위한 문자열 상수는 다음과 같이 정의됩니다.

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a>연결 및 허브

SignalR API에는 클라이언트와 서버 간의 통신을 위한 두 가지 모델인 영구 연결 및 허브가 포함되어 있습니다.

연결은 단일 받는 사람, 그룹화된 메시지 또는 브로드캐스트 메시지를 보내기 위한 간단한 끝점을 나타냅니다. 영구 연결 API(PersistentConnection 클래스에서 .NET 코드로 표시)는 개발자에게 SignalR이 노출하는 하위 수준 통신 프로토콜에 직접 액세스할 수 있도록 합니다. 연결 통신 모델을 사용하면 Windows 통신 재단과 같은 연결 기반 API를 사용한 개발자에게 익숙할 수 있습니다.

허브는 클라이언트와 서버가 서로 직접 메서드를 호출할 수 있도록 하는 연결 API를 기반으로 구축된 보다 높은 수준의 파이프라인입니다. SignalR은 마치 마술처럼 시스템 경계를 넘어 디스패치를 처리하므로 클라이언트가 로컬 메서드처럼 쉽게 서버에서 메서드를 호출할 수 있으며 그 반대의 경우도 마찬가지입니다. 허브 통신 모델을 사용하면 .NET Remoting과 같은 원격 호출 API를 사용한 개발자에게 익숙할 수 있습니다. 또한 Hub를 사용하면 강력하게 입력된 매개 변수를 메서드에 전달하여 모델 바인딩을 활성화할 수도 있습니다.

### <a name="architecture-diagram"></a>아키텍처 다이어그램

다음 다이어그램에서는 허브, 영구 연결 및 전송에 사용되는 기본 기술 간의 관계를 보여 주며 있습니다.

![API, 전송 및 클라이언트를 보여 주며 SignalR 아키텍처 다이어그램](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a>허브 작동 방식

서버 측 코드가 클라이언트에서 메서드를 호출하면 호출할 메서드의 이름과 매개 변수가 포함된 활성 전송을 통해 패킷이 전송됩니다(개체가 메서드 매개 변수로 전송되면 JSON을 사용하여 직렬화됩니다). 그런 다음 클라이언트는 메서드 이름을 클라이언트 쪽 코드에 정의된 메서드와 일치시다. 일치하는 경우 클라이언트 메서드는 직렬화된 매개 변수 데이터를 사용하여 실행됩니다.

메서드 호출은 [Fiddler와](http://fiddler2.com/) 같은 도구를 사용하여 모니터링할 수 있습니다. 다음 이미지는 Fiddler의 로그 창에서 SignalR 서버에서 웹 브라우저 클라이언트로 전송된 메서드 호출을 보여 주며, 메서드 호출은 호출된 `MoveShapeHub`허브에서 전송되고 있으며 호출되는 `updateShape`메서드가 호출됩니다.

![SignalR 트래픽을 보여주는 피들러 로그의 보기](introduction-to-signalr/_static/image6.png)

이 예제에서는 허브 이름이 `H` 매개 변수로 식별됩니다. 메서드 이름은 `M` 매개 변수로 식별되고 메서드로 전송되는 데이터는 `A` 매개 변수로 식별됩니다. 이 메시지를 생성한 응용 프로그램은 [고주파 실시간](tutorial-high-frequency-realtime-with-signalr.md) 자습서에서 만들어집니다.

### <a name="choosing-a-communication-model"></a>통신 모델 선택

대부분의 응용 프로그램은 허브 API를 사용해야 합니다. 연결 API는 다음과 같은 상황에서 사용할 수 있습니다.

- 전송된 실제 메시지의 형식을 지정해야 합니다.
- 개발자는 원격 호출 모델보다는 메시징 및 디스패치 모델로 작업하는 것을 선호합니다.
- 메시징 모델을 사용하는 기존 응용 프로그램이 SignalR을 사용하도록 포팅되고 있습니다.
