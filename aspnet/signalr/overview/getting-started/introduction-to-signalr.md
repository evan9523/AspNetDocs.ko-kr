---
uid: signalr/overview/getting-started/introduction-to-signalr
title: SignalR 소개 | Microsoft Docs
author: bradygaster
description: 이 문서에서는 SignalR 무엇 이며, 만들려는 솔루션 중 일부를 설명 합니다.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 76e8fd03292eafa4b0b579ee1746fb54b57ac66b
ms.sourcegitcommit: 45754124123403520b9fa2e706a4d1292494159b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643679"
---
# <a name="introduction-to-signalr"></a>SignalR 소개

[Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 SignalR 무엇 이며, 만들려는 솔루션 중 일부를 설명 합니다. 
> 
> ## <a name="questions-and-comments"></a>질문 및 설명
> 
> 이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요. 자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)에 게시할 수 있습니다.

## <a name="what-is-signalr"></a>SignalR 란?

ASP.NET SignalR는 응용 프로그램에 실시간 웹 기능을 추가 하는 프로세스를 간소화 하는 ASP.NET 개발자를 위한 라이브러리입니다. 실시간 웹 기능은 서버가 클라이언트에서 새 데이터를 요청할 때까지 대기 하는 것이 아니라 서버 코드에서 연결 된 클라이언트에 콘텐츠를 즉시 푸시하는 기능을 제공 합니다.

SignalR는 ASP.NET 응용 프로그램에 "실시간" 웹 기능을 추가 하는 데 사용할 수 있습니다. 채팅은 종종 예로 사용 되지만 전체적으로 더 많은 작업을 수행할 수 있습니다. 사용자가 새 데이터를 볼 수 있도록 웹 페이지를 새로 고치거 나 페이지에서 [긴 폴링을](http://en.wikipedia.org/wiki/Push_technology#Long_polling) 구현 하 여 새 데이터를 검색 하는 경우에는 SignalR을 사용 하는 후보가 됩니다. 예를 들면 대시보드 및 모니터링 응용 프로그램, 공동 작업 응용 프로그램 (예: 문서를 동시에 편집), 작업 진행률 업데이트 및 실시간 양식이 있습니다.

또한 SignalR를 사용 하면 실시간 게임과 같이 서버에서 빈도가 높은 업데이트가 필요한 웹 응용 프로그램을 완전히 새로운 형식으로 사용할 수 있습니다.

SignalR는 서버 쪽 .NET 코드에서 클라이언트 브라우저 (및 다른 클라이언트 플랫폼)의 JavaScript 함수를 호출 하는 서버-클라이언트 원격 프로시저 호출 (RPC)을 만들기 위한 간단한 API를 제공 합니다. SignalR에는 연결 관리 (예를 들어, 이벤트 연결 및 연결 끊기), 연결 그룹화를 위한 API도 포함 됩니다.

![SignalR를 사용 하 여 메서드 호출](introduction-to-signalr/_static/image1.png)

SignalR은 연결 관리를 자동으로 처리하며, 대화방처럼 메시지를 연결된 모든 클라이언트에 동시에 브로드캐스트할 수 있습니다. 메시지를 특정 클라이언트에 보낼 수도 있습니다. 클라이언트와 서버 간의 연결은 기존 HTTP 연결과 달리 영구적이며, 각 통신에 대해 다시 설정됩니다.

SignalR는 "서버 푸시" 기능을 지원 합니다 .이 기능은 서버 코드가 현재 웹에서 자주 사용 하는 요청-응답 모델 대신 RPC (원격 프로시저 호출)를 사용 하 여 브라우저에서 클라이언트 코드를 호출할 수 있습니다.

SignalR 응용 프로그램은 기본 제공 및 타사 스케일 아웃 공급자를 사용 하 여 수천 개의 클라이언트로 확장할 수 있습니다.

기본 제공 공급자는 다음과 같습니다.
* [Service Bus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [SQL Server](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [Redis](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

타사 공급자는 다음과 같습니다.
* [NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).

SignalR는 [GitHub](https://github.com/signalr)를 통해 액세스할 수 있는 오픈 소스입니다.

## <a name="signalr-and-websocket"></a>SignalR 및 WebSocket

SignalR는 사용 가능한 경우 새 WebSocket 전송을 사용 하 고 필요한 경우 이전 전송으로 대체 합니다. WebSocket을 직접 사용 하 여 앱을 직접 작성할 수 있지만 SignalR를 사용 하면 구현 해야 할 많은 추가 기능이 이미 수행 된 것입니다. 가장 중요 한 점은 이전 클라이언트에 대 한 별도의 코드 경로를 만드는 방법에 대해 걱정할 필요 없이 WebSocket을 활용 하기 위해 앱을 코딩할 수 있음을 의미 합니다. 또한 SignalR는 websocket에 대 한 업데이트에 대해 걱정 하지 않아도 됩니다. SignalR가 기본 전송의 변경을 지원 하도록 업데이트 되므로 응용 프로그램에 WebSocket 버전 간에 일관 된 인터페이스를 제공 합니다.

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a>전송 및 대체

SignalR는 클라이언트와 서버 간의 실시간 작업을 수행 하는 데 필요한 일부 전송에 대 한 추상화입니다. SignalR는 가능한 경우 WebSocket 연결을 설정 하려고 시도 합니다. WebSocket은 다음을 포함 하 여 SignalR에 대 한 최적의 전송입니다.

* 서버 메모리를 가장 효율적으로 사용 합니다.
* 가장 짧은 대기 시간입니다.
* 클라이언트와 서버 간의 전이중 통신과 같은 가장 기본적인 기능입니다.
* 가장 엄격한 요구 사항은 WebSocket에 서버가 필요 합니다.
  * Windows Server 2012 또는 Windows 8에서 실행 합니다.
  * .NET Framework 4.5.

이러한 요구 사항이 충족 되지 않으면 SignalR는 다른 전송을 사용 하 여 연결을 시도 합니다.

### <a name="html-5-transports"></a>HTML 5 전송

이러한 전송은 [HTML 5](http://en.wikipedia.org/wiki/HTML5)에 대 한 지원에 따라 달라 집니다. 클라이언트 브라우저에서 HTML 5 표준을 지원 하지 않는 경우 이전 전송이 사용 됩니다.

- **Websocket** (서버와 브라우저가 모두 websocket을 지원할 수 있음을 나타냄). WebSocket은 클라이언트와 서버 간에 진정한 영구 양방향 연결을 설정 하는 유일한 전송입니다. 그러나 WebSocket에는 가장 엄격한 요구 사항이 있습니다. 최신 버전의 Microsoft Internet Explorer, Google Chrome 및 Mozilla Firefox 에서만 완전히 지원 되며 Opera 및 Safari와 같은 다른 브라우저에서는 부분 구현이 있습니다.
- **서버에서 이벤트를 보냈습니다**(브라우저에서 서버 전송 이벤트를 지 원하는 경우 기본적으로 Internet Explorer를 제외한 모든 브라우저).

### <a name="comet-transports"></a>Comet 전송

다음 전송은 [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) 웹 응용 프로그램 모델을 기반으로 합니다 .이 모델에서는 브라우저 또는 다른 클라이언트에서 장기 보유 HTTP 요청을 유지 관리 하며,이를 통해 클라이언트는 특정 클라이언트를 요청 하지 않고 클라이언트에 데이터를 푸시할 수 있습니다.

- **영원히 Frame** (Internet Explorer에만 해당). 영원히 Frame은 서버의 끝점에 대 한 요청을 완료 하지 않는 숨겨진 IFrame을 만듭니다. 그런 다음 서버는 즉시 실행 되는 클라이언트로 스크립트를 지속적으로 전송 하 여 서버에서 클라이언트로의 단방향 실시간 연결을 제공 합니다. 클라이언트에서 서버로의 연결에서는 서버와 클라이언트 간의 별도 연결을 사용 하 고 표준 HTTP 요청과 마찬가지로 전송 해야 하는 각 데이터 조각에 대해 새 연결을 만듭니다.
- **Ajax 긴 폴링**. Long 폴링은 영구 연결을 만들지 않고 대신 서버가 응답할 때까지 열린 상태로 유지 되는 요청을 사용 하 여 서버를 폴링합니다. 그러면 연결이 닫히고 새 연결이 즉시 요청 됩니다. 연결을 다시 설정 하는 동안 약간의 대기 시간이 발생할 수 있습니다.

구성에서 지원 되는 전송에 대 한 자세한 내용은 [지원 되는 플랫폼](supported-platforms.md)을 참조 하세요.

### <a name="transport-selection-process"></a>전송 선택 프로세스

다음 목록에서는 SignalR에서 사용할 전송을 결정 하는 데 사용 하는 단계를 보여 줍니다.

1. 브라우저가 Internet Explorer 8이 하 이면 긴 폴링이 사용 됩니다.
2. JSONP가 구성 된 경우 (즉, `jsonp` 연결이 시작 될 때 매개 변수가로 설정 된 경우 `true` ) 긴 폴링이 사용 됩니다.
3. 도메인 간 연결이 설정 되는 경우 (즉, SignalR 끝점이 호스팅 페이지와 동일한 도메인에 있지 않은 경우) 다음 조건을 충족 하는 경우 WebSocket이 사용 됩니다.

   - 클라이언트는 CORS (크로스-원본 자원 공유)를 지원 합니다. CORS를 지 원하는 클라이언트에 대 한 자세한 내용은 [caniuse.com에서 cors](http://www.caniuse.com/CORS)를 참조 하세요.
   - 클라이언트가 WebSocket을 지원 합니다.
   - 서버에서 WebSocket을 지원 합니다.

     이러한 조건 중 하나라도 충족 되지 않으면 긴 폴링이 사용 됩니다. 도메인 간 연결에 대 한 자세한 내용은 [도메인 간 연결을 설정 하는 방법](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)을 참조 하세요.
4. JSONP가 구성 되지 않은 경우 연결이 도메인이 아닌 경우 클라이언트와 서버에서 모두 지 원하는 경우 WebSocket이 사용 됩니다.
5. 클라이언트나 서버에서 WebSocket을 지원 하지 않는 경우 사용할 수 있는 경우 서버에서 보낸 이벤트를 사용 합니다.
6. 서버에서 보낸 이벤트를 사용할 수 없는 경우 영원히 프레임을 시도 합니다.
7. 계속 해 서 프레임에 오류가 발생 하면 긴 폴링이 사용 됩니다.

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a>전송 모니터링

허브에서 로깅을 사용 하도록 설정 하 고 브라우저에서 콘솔 창을 열어 응용 프로그램에서 사용 하는 전송을 확인할 수 있습니다.

브라우저에서 허브 이벤트에 대 한 로깅을 사용 하도록 설정 하려면 클라이언트 응용 프로그램에 다음 명령을 추가 합니다.

`$.connection.hub.logging = true;`

- Internet Explorer에서 F12 키를 눌러 개발자 도구를 열고 콘솔 탭을 클릭 합니다.

    ![Microsoft Internet Explorer의 콘솔](introduction-to-signalr/_static/image2.png)
- Chrome에서 Ctrl + Shift + J를 눌러 콘솔을 엽니다.

    ![Google Chrome의 콘솔](introduction-to-signalr/_static/image3.png)

콘솔 열기 및 로깅을 사용 하도록 설정 하면 SignalR에서 어떤 전송을 사용 하는지 확인할 수 있습니다.

![WebSocket 전송을 보여 주는 Internet Explorer의 콘솔](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a>전송 지정

전송 협상은 특정 시간 및 클라이언트/서버 리소스를 사용 합니다. 클라이언트 기능을 알고 있는 경우 클라이언트 연결을 시작할 때 전송을 지정할 수 있습니다. 다음 코드 조각에서는 Ajax 긴 폴링 전송을 사용 하 여 연결을 시작 하는 방법을 보여 줍니다. 클라이언트에서 다른 프로토콜을 지원 하지 않는 것으로 알려진 경우에 사용 됩니다.

`connection.start({ transport: 'longPolling' });`

클라이언트가 특정 전송을 순서 대로 시도 하도록 하려면 대체 (fallback) 순서를 지정할 수 있습니다. 다음 코드 조각에서는 WebSocket을 시도 하 고 실패 하 여 긴 폴링으로 직접 이동 하는 방법을 보여 줍니다.

`connection.start({ transport: ['webSockets','longPolling'] });`

전송을 지정 하는 문자열 상수는 다음과 같이 정의 됩니다.

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a>연결 및 허브

SignalR API에는 클라이언트와 서버 간 통신을 위한 두 가지 모델 (영구 연결 및 허브)이 포함 되어 있습니다.

연결은 단일 받는 사람, 그룹화 또는 브로드캐스트 메시지를 보내기 위한 간단한 끝점을 나타냅니다. PersistentConnection 클래스를 사용 하 여 .NET 코드에 표시 된 영구 연결 API를 통해 개발자는 SignalR가 노출 하는 하위 수준 통신 프로토콜에 직접 액세스할 수 있습니다. 연결 통신 모델 사용은 Windows Communication Foundation와 같은 연결 기반 Api를 사용 하는 개발자에 게 친숙 합니다.

허브는 클라이언트와 서버에서 직접 메서드를 호출할 수 있도록 하는 연결 API를 기반으로 하는 더 높은 수준의 파이프라인입니다. SignalR는 클라이언트에서 서버에 대 한 메서드를 로컬 메서드로 호출할 수 있도록 하는 것 처럼 컴퓨터 경계 간 디스패치를 처리 하 고 그 반대의 경우도 마찬가지입니다. 허브 통신 모델 사용은 .NET Remoting과 같은 원격 호출 Api를 사용 하는 개발자에 게 친숙 합니다. 또한 허브를 사용 하면 강력한 형식의 매개 변수를 메서드에 전달 하 여 모델 바인딩을 사용 하도록 설정할 수 있습니다.

### <a name="architecture-diagram"></a>아키텍처 다이어그램

다음 다이어그램에서는 허브, 영구 연결 및 전송에 사용 되는 기본 기술 간의 관계를 보여 줍니다.

![Api, 전송 및 클라이언트를 보여 주는 SignalR 아키텍처 다이어그램](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a>허브 작동 방법

서버 쪽 코드에서 클라이언트의 메서드를 호출 하면 호출 될 메서드의 이름 및 매개 변수를 포함 하는 활성 전송에서 패킷이 전송 됩니다 (개체를 메서드 매개 변수로 보냈을 때 JSON을 사용 하 여 serialize). 클라이언트는 메서드 이름과 클라이언트 쪽 코드에 정의 된 메서드를 일치 시킵니다. 일치 하는 항목이 있는 경우 클라이언트 메서드는 deserialize 된 매개 변수 데이터를 사용 하 여 실행 됩니다.

Fiddler와 같은 도구를 사용 하 여 메서드 호출을 모니터링할 수 있습니다 [.](http://fiddler2.com/) 다음 이미지는 Fiddler의 로그 창에서 SignalR 서버에서 웹 브라우저 클라이언트로 전송 된 메서드 호출을 보여 줍니다. 호출 된 허브에서 메서드 호출을 보내고 `MoveShapeHub` 호출 되는 메서드를 호출 합니다 `updateShape` .

![SignalR 트래픽을 보여 주는 Fiddler 로그 보기](introduction-to-signalr/_static/image6.png)

이 예제에서 허브 이름은 `H` 매개 변수로 식별 됩니다. 메서드 이름은 `M` 매개 변수로 식별 되며 메서드로 전송 되는 데이터는 매개 변수를 사용 하 여 식별 됩니다 `A` . 이 메시지를 생성 한 응용 프로그램은 [빈도가 높은 실시간](tutorial-high-frequency-realtime-with-signalr.md) 자습서에서 만들어집니다.

### <a name="choosing-a-communication-model"></a>통신 모델 선택

대부분의 응용 프로그램은 허브 API를 사용 해야 합니다. 연결 API는 다음과 같은 경우에 사용할 수 있습니다.

- 보낸 실제 메시지의 형식을 지정 해야 합니다.
- 개발자는 원격 호출 모델 대신 메시징 및 디스패치 모델을 사용 하는 것이 선호 됩니다.
- 메시징 모델을 사용 하는 기존 응용 프로그램은 SignalR를 사용 하도록 포팅 됩니다.
