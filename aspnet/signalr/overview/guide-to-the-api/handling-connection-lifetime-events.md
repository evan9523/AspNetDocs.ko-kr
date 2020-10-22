---
uid: signalr/overview/guide-to-the-api/handling-connection-lifetime-events
title: SignalR의 연결 수명 이벤트 이해 및 처리 | Microsoft Docs
author: bradygaster
description: 이 문서에서는 허브 API에 의해 노출 되는 이벤트를 사용 하는 방법을 설명 합니다.
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 03960de2-8d95-4444-9169-4426dcc64913
msc.legacyurl: /signalr/overview/guide-to-the-api/handling-connection-lifetime-events
msc.type: authoredcontent
ms.openlocfilehash: 5bdf20549fccab5d644e35fdf4ce351540c8620d
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345224"
---
# <a name="understanding-and-handling-connection-lifetime-events-in-signalr"></a>SignalR의 연결 수명 이벤트 이해 및 처리

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 사용자가 처리할 수 있는 SignalR 연결, 다시 연결 및 연결 끊기 이벤트와, 구성할 수 있는 시간 제한 및 keepalive 설정에 대 한 개요를 제공 합니다.
>
> 이 문서에서는 SignalR 및 연결 수명 이벤트를 이미 알고 있다고 가정 합니다. SignalR에 대 한 소개는 [SignalR 소개](../getting-started/introduction-to-signalr.md)를 참조 하세요. 연결 수명 이벤트 목록은 다음 리소스를 참조 하세요.
>
> - [허브 클래스에서 연결 수명 이벤트를 처리 하는 방법](hubs-api-guide-server.md#connectionlifetime)
> - [JavaScript 클라이언트에서 연결 수명 이벤트를 처리 하는 방법](hubs-api-guide-javascript-client.md#connectionlifetime)
> - [.NET 클라이언트에서 연결 수명 이벤트를 처리 하는 방법](hubs-api-guide-net-client.md#connectionlifetime)
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

이 자료에는 다음과 같은 섹션이 포함되어 있습니다.

- [연결 수명 용어 및 시나리오](#terminology)

    - [SignalR 연결, 전송 연결 및 실제 연결](#signalrvstransport)
    - [전송 연결 끊기 시나리오](#transportdisconnect)
    - [클라이언트 연결 끊기 시나리오](#clientdisconnect)
    - [서버 연결 끊기 시나리오](#serverdisconnect)
- [시간 제한 및 keepalive 설정](#timeoutkeepalive)

    - [ConnectionTimeout](#connectiontimeout)
    - [Disconnecttimeout은](#disconnecttimeout)
    - [KeepAlive](#keepalive)
    - [시간 제한 및 keepalive 설정을 변경 하는 방법](#changetimeout)
- [사용자에 게 연결이 끊어지지 않도록 알리는 방법](#notifydisconnect)
- [지속적으로 다시 연결 하는 방법](#continuousreconnect)
- [서버 코드에서 클라이언트의 연결을 끊는 방법](#disconnectclientfromserver)
- [연결 끊기 이유 검색](#detectingreasonfordisconnection)

API 참조 항목에 대 한 링크는 .NET 4.5 버전의 API에 대 한 링크입니다. .NET 4를 사용 하 [는 경우 .net 4 버전의 API 항목](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)을 참조 하세요.

<a id="terminology"></a>

## <a name="connection-lifetime-terminology-and-scenarios"></a>연결 수명 용어 및 시나리오

`OnReconnected`SignalR Hub의 이벤트 처리기는 `OnConnected` `OnDisconnected` 지정 된 클라이언트에 대해 바로 다음에 실행할 수 있습니다. 연결을 끊지 않고 다시 연결할 수 있는 이유는 SignalR에서 "연결" 이라는 단어를 사용 하는 몇 가지 방법이 있습니다.

<a id="signalrvstransport"></a>

### <a name="signalr-connections-transport-connections-and-physical-connections"></a>SignalR 연결, 전송 연결 및 실제 연결

이 문서는 *SignalR 연결*, *전송 연결*및 *실제 연결*을 구분 합니다.

- **SignalR 연결은** SignalR API에서 유지 관리 되 고 연결 ID에 의해 고유 하 게 식별 되는 클라이언트와 서버 URL 간의 논리적 관계를 나타냅니다. 이 관계에 대 한 데이터는 SignalR에서 유지 관리 되며 전송 연결을 설정 하는 데 사용 됩니다. `Stop`SignalR가 손실 된 전송 연결을 다시 설정 하려고 시도 하는 동안 클라이언트에서 메서드를 호출 하거나 시간 제한에 도달할 때 관계는 end 및 SignalR 데이터를 삭제 합니다.
- **전송 연결은** 클라이언트와 서버 간의 논리적 관계를 나타내며,이는 네 가지 전송 Api (websocket, 서버에서 보낸 이벤트, 무한 프레임 또는 긴 폴링) 중 하나에서 유지 관리 됩니다. SignalR는 전송 API를 사용 하 여 전송 연결을 만들며 전송 API는 전송 연결을 만들기 위해 실제 네트워크 연결이 있는지 여부에 따라 달라 집니다. SignalR가 종료 되거나 전송 API가 물리적 연결이 끊어지는 것을 감지 하면 전송 연결이 종료 됩니다.
- **물리적 연결은** 클라이언트 컴퓨터와 서버 컴퓨터 간의 통신을 용이 하 게 하는 실제 네트워크 링크 (와이어, 무선 신호, 라우터 등)를 나타냅니다. 전송 연결을 설정 하려면 물리적 연결이 있어야 하며 SignalR 연결을 설정 하려면 전송 연결을 설정 해야 합니다. 그러나이 항목의 뒷부분에서 설명 하는 것 처럼 물리적 연결의 중단은 항상 전송 연결 또는 SignalR 연결을 즉시 종료 하지 않습니다.

다음 다이어그램에서 SignalR 연결은 허브 API 및 PersistentConnection API SignalR 계층으로 표시 되 고 전송 연결은 전송 계층으로 표시 되며 실제 연결은 서버와 클라이언트 사이의 줄로 표시 됩니다.

![SignalR 아키텍처 다이어그램](handling-connection-lifetime-events/_static/image1.png)

`Start`SignalR client에서 메서드를 호출 하면 서버에 대 한 실제 연결을 설정 하는 데 필요한 모든 정보가 포함 된 SignalR 클라이언트 코드를 제공 하 게 됩니다. SignalR client 코드는이 정보를 사용 하 여 HTTP 요청을 수행 하 고 네 가지 전송 방법 중 하나를 사용 하는 실제 연결을 설정 합니다. 전송 연결에 실패 하거나 서버에 오류가 발생 하면 클라이언트에 동일한 SignalR URL에 대 한 새 전송 연결을 자동으로 다시 설정 하는 데 필요한 정보가 여전히 있으므로 SignalR 연결이 즉시 중단 되지 않습니다. 이 시나리오에서는 사용자 응용 프로그램의 개입이 관여 하지 않으며, SignalR 클라이언트 코드가 새 전송 연결을 설정 하는 경우 새 SignalR 연결을 시작 하지 않습니다. SignalR 연결의 연속성은 메서드를 호출할 때 생성 되는 연결 ID가 변경 되지 않는다는 사실에 반영 됩니다 `Start` .

`OnReconnected`전송 연결이 손실 된 후 자동으로 다시 설정 되 면 허브의 이벤트 처리기가 실행 됩니다. `OnDisconnected`이벤트 처리기는 SignalR 연결이 끝날 때 실행 됩니다. SignalR 연결은 다음과 같은 방법으로 끝날 수 있습니다.

- 클라이언트에서 메서드를 호출 하면 `Stop` 중지 메시지가 서버로 전송 되 고 클라이언트와 서버 모두 SignalR 연결을 즉시 종료 합니다.
- 클라이언트와 서버 간의 연결이 끊어진 후 클라이언트는 다시 연결을 시도 하 고 클라이언트가 다시 연결 될 때까지 기다립니다. 다시 연결 하려는 시도가 실패 하 고 연결 끊기 제한 시간이 종료 되 면 클라이언트와 서버 모두 SignalR 연결을 종료 합니다. 클라이언트에서 다시 연결 시도를 중지 하 고 서버가 SignalR 연결의 표시를 삭제 합니다.
- 클라이언트에서 메서드를 호출 하지 않고 실행을 중지 하면 `Stop` 서버는 클라이언트가 다시 연결 될 때까지 기다린 후 연결 끊기 제한 시간 후에 SignalR 연결을 종료 합니다.
- 서버 실행이 중지 되 면 클라이언트는 다시 연결 (전송 연결 다시 만들기) 한 후 연결 끊기 시간 제한 기간 후에 SignalR 연결을 종료 합니다.

연결 문제가 없고 사용자 응용 프로그램이 메서드를 호출 하 여 SignalR 연결을 종료 하는 경우 `Stop` SignalR 연결과 전송 연결이 동시에 시작 되 고 종료 됩니다. 다음 섹션에서는 다른 시나리오에 대해 자세히 설명 합니다.

<a id="transportdisconnect"></a>

### <a name="transport-disconnection-scenarios"></a>전송 연결 끊기 시나리오

실제 연결이 느리거나 연결 중단이 있을 수 있습니다. 중단의 길이와 같은 요인에 따라 전송 연결이 끊어질 수 있습니다. 그런 다음 SignalR는 전송 연결을 다시 설정 하려고 시도 합니다. 경우에 따라 전송 연결 API는 중단을 감지 하 여 전송 연결을 삭제 하 고 SignalR는 연결이 끊어지는 것을 즉시 찾습니다. 다른 시나리오에서는 전송 연결 API와 SignalR 모두 연결이 끊어지는 즉시 인식 되지 않습니다. 긴 폴링을 제외한 모든 전송의 경우 SignalR 클라이언트는 *keepalive* 이라는 함수를 사용 하 여 전송 API에서 검색할 수 없는 연결의 손실을 확인 합니다. 긴 폴링 연결에 대 한 자세한 내용은이 항목의 뒷부분에 있는 [Timeout 및 keepalive settings](#timeoutkeepalive) 를 참조 하세요.

연결이 비활성 상태인 경우 서버는 주기적으로 keepalive 패킷을 클라이언트에 보냅니다. 이 문서를 작성 하는 날짜부터 기본 빈도는 10 초 마다입니다. 클라이언트는 이러한 패킷을 수신 하 여 연결 문제가 있는지를 알 수 있습니다. 예상 되는 경우 keepalive 패킷이 수신 되지 않으면 잠시 후 클라이언트에서 속도 저하 또는 중단 같은 연결 문제가 있다고 가정 합니다. 계속 해 서 keepalive를 수신 하지 않으면 클라이언트에서 연결이 끊어진 것으로 간주 하 고 다시 연결을 시도 합니다.

다음 다이어그램은 전송 API에서 즉시 인식 되지 않는 실제 연결에 문제가 있는 경우 일반적인 시나리오에서 발생 하는 클라이언트 및 서버 이벤트를 보여 줍니다. 다이어그램은 다음과 같은 경우에 적용 됩니다.

- 전송은 Websocket, 영원히 프레임 또는 서버에서 보낸 이벤트입니다.
- 실제 네트워크 연결의 중단 기간이 다양 합니다.
- 전송 API는 중단을 인식 하지 못하므로 SignalR는 keepalive 기능을 사용 하 여 해당 기능을 검색 합니다.

![전송 연결이 끊김](handling-connection-lifetime-events/_static/image2.png)

클라이언트가 다시 연결 모드로 전환 되지만 연결 끊기 제한 시간 내에 전송 연결을 설정할 수 없는 경우 서버는 SignalR 연결을 종료 합니다. 이 경우 서버는 허브의 메서드를 실행 하 `OnDisconnected` 고 클라이언트가 나중에 연결을 관리 하는 경우 클라이언트에 보낼 연결 끊기 메시지를 큐에 대기 시킵니다. 그런 다음 클라이언트가 다시 연결 하면 연결 끊기 명령을 수신 하 고 메서드를 호출 합니다 `Stop` . 이 시나리오에서 `OnReconnected` 는 클라이언트가 다시 연결 될 때 실행 되지 않으며 `OnDisconnected` 클라이언트가를 호출할 때 실행 되지 않습니다 `Stop` . 다음 다이어그램에서는이 시나리오를 보여 줍니다.

![전송 장애-서버 제한 시간](handling-connection-lifetime-events/_static/image3.png)

클라이언트에서 발생할 수 있는 SignalR 연결 수명 이벤트는 다음과 같습니다.

- `ConnectionSlow` 클라이언트 이벤트입니다.

    마지막 메시지 또는 keepalive ping을 받은 이후 keepalive 시간 제한 기간의 미리 설정 된 비율이 경과 된 경우 발생 합니다. 기본 keepalive 시간 제한 경고 기간은 keepalive 시간 제한의 2/3입니다. Keepalive 시간 제한은 20 초 이므로 약 13 초에 경고가 발생 합니다.

    기본적으로 서버는 10 초 마다 keepalive ping을 보내고 클라이언트는 2 초 마다 keepalive ping을 확인 합니다 (keepalive 시간 제한 값과 keepalive 시간 제한 경고 값 간의 차이점 중 하나).

    전송 API가 연결 끊기를 인식 하는 경우 keepalive 시간 제한 경고 기간이 전달 되기 전에 연결 끊기에 대 한 알림이 SignalR 될 수 있습니다. 이 경우 `ConnectionSlow` 이벤트가 발생 하지 않고 SignalR가 이벤트로 직접 이동 `Reconnecting` 합니다.
- `Reconnecting` 클라이언트 이벤트입니다.

    (A) 전송 API에서 연결이 끊어진 것을 감지 하거나 (b) 마지막 메시지 또는 keepalive ping을 받은 이후 keepalive 시간 제한 기간이 경과 하면 발생 합니다. SignalR 클라이언트 코드를 다시 연결 하는 중입니다. 전송 연결이 끊어질 때 응용 프로그램이 몇 가지 작업을 수행 하도록 하려면이 이벤트를 처리할 수 있습니다. 기본 keepalive 제한 시간은 현재 20 초입니다.

    SignalR이 다시 연결 모드에 있는 동안 클라이언트 코드에서 허브 메서드를 호출 하려고 하면 SignalR가 명령을 보내려고 시도 합니다. 대부분의 경우 이러한 시도는 실패 하지만 경우에 따라 성공할 수도 있습니다. 서버에서 전송 되는 이벤트, 영원히 프레임 및 긴 폴링 전송의 경우 SignalR는 두 통신 채널을 사용 합니다. 하나는 클라이언트에서 메시지를 전송 하는 데 사용 하 고 다른 하나는 메시지를 수신 하는 데 사용 합니다. 수신 하는 데 사용 되는 채널은 영구적으로 열린 채널 이며 실제 연결이 중단 될 때 닫힙니다. 전송에 사용 되는 채널을 계속 사용할 수 있으므로 물리적 연결이 복원 되 면 수신 채널이 다시 설정 되기 전에 클라이언트에서 서버로의 메서드 호출이 성공할 수 있습니다. 반환 값은 SignalR가 수신에 사용 되는 채널을 다시 열 때까지 수신 되지 않습니다.
- `Reconnected` 클라이언트 이벤트입니다.

    전송 연결이 다시 설정 될 때 발생 합니다. `OnReconnected`허브에 있는 이벤트 처리기가 실행 됩니다.
- `Closed` 클라이언트 이벤트 ( `disconnected` JavaScript의 이벤트)

    SignalR 클라이언트 코드가 전송 연결을 잃은 후 다시 연결을 시도 하는 동안 연결 끊기 제한 시간이 만료 되 면 발생 합니다. 기본 연결 끊기 제한 시간은 30 초입니다. 이 이벤트는 메서드가 호출 되기 때문에 연결이 종료 되는 경우에도 발생 `Stop` 합니다.

전송 API에서 검색 되지 않으며 keepalive 시간 제한 경고 기간 보다 오랫동안 서버에서 keepalive ping 수신을 지연 하지 않아 연결 수명 이벤트가 발생 하지 않을 수 있습니다.

일부 네트워크 환경은 의도적으로 유휴 연결을 종료 하 고 keepalive 패킷의 또 다른 기능은 이러한 네트워크에서 SignalR 연결이 사용 되 고 있음을 알 수 있도록 하 여이를 방지 하는 것입니다. 극단적인 경우 기본적으로 keepalive ping의 기본 빈도는 닫힌 연결을 방지 하기에 충분 하지 않을 수 있습니다. 이 경우 keepalive ping을 더 자주 전송 하도록 구성할 수 있습니다. 자세한 내용은이 항목의 뒷부분에 있는 [Timeout 및 keepalive settings](#timeoutkeepalive) 를 참조 하세요.

> [!NOTE]
>
> **중요**: 여기에 설명 된 이벤트 시퀀스는 보장 되지 않습니다. SignalR는이 체계에 따라 예측 가능한 방식으로 연결 수명 이벤트를 발생 시 키 려 하지만 네트워크 이벤트의 많은 변형이 있으며, 전송 Api와 같은 기본 통신 프레임 워크에서이를 처리 하는 여러 가지 방법이 있습니다. 예를 들어 클라이언트가 다시 연결 하는 `Reconnected` 경우 이벤트가 발생 하지 않을 수도 있고, `OnConnected` 연결을 설정 하지 못한 경우 서버의 처리기가 실행 될 수도 있습니다. 이 항목에서는 일반적인 특정 상황에서 일반적으로 생성 되는 효과에 대해서만 설명 합니다.

<a id="clientdisconnect"></a>

### <a name="client-disconnection-scenarios"></a>클라이언트 연결 끊기 시나리오

브라우저 클라이언트에서 SignalR 연결을 유지 관리 하는 SignalR 클라이언트 코드는 웹 페이지의 JavaScript 컨텍스트에서 실행 됩니다. 이는 한 페이지에서 다른 페이지로 이동할 때 SignalR 연결이 종료 되어야 하는 이유 이며, 여러 브라우저 창이 나 탭에서 연결 하는 경우 여러 연결 Id를 사용 하 여 여러 연결을 사용 하는 이유입니다. 사용자가 브라우저 창이 나 탭을 닫거나 새 페이지로 이동 하거나 페이지를 새로 고치면 SignalR 클라이언트 코드에서 브라우저 이벤트를 처리 하 고 메서드를 호출 하기 때문에 SignalR 연결이 즉시 종료 됩니다 `Stop` . 이러한 시나리오 또는 응용 프로그램에서 메서드를 호출할 때 클라이언트 플랫폼에서 `Stop` `OnDisconnected` 이벤트 처리기가 서버에서 즉시 실행 되 고 클라이언트가 이벤트를 발생 시킵니다 `Closed` .이 이벤트의 이름은 `disconnected` JavaScript로 지정 됩니다.

클라이언트 응용 프로그램이 나 실행 중인 컴퓨터가 충돌 하거나 절전 모드로 전환 되는 경우 (예: 사용자가 랩톱을 닫을 때) 서버에 발생 한 상황에 대 한 정보가 없습니다. 서버에서 알 수 있듯이, 연결이 중단 되어 클라이언트가 다시 연결 하려고 시도할 수 있습니다. 따라서 이러한 시나리오에서는 서버가 다시 연결할 수 있는 기회를 제공 하기 위해 대기 하 고, `OnDisconnected` 연결 끊기 제한 시간이 만료 될 때까지 (기본적으로 약 30 초) 실행 되지 않습니다. 다음 다이어그램에서는이 시나리오를 보여 줍니다.

![클라이언트 컴퓨터 오류](handling-connection-lifetime-events/_static/image4.png)

<a id="serverdisconnect"></a>

### <a name="server-disconnection-scenarios"></a>서버 연결 끊기 시나리오

서버를 오프 라인으로 전환 하는 경우-다시 부팅 하는 작업이 실패 하 고, 앱 도메인 재활용 등이 발생할 수 있습니다. 또는 전송 API와 SignalR는 서버가 없다는 것을 즉시 알 수 있으며 SignalR는 이벤트를 발생 시 키 지 않고 다시 연결 하려고 시도할 수 있습니다. `ConnectionSlow` 클라이언트가 다시 연결 모드로 전환 되는 경우 및 서버를 복구 또는 다시 시작 하거나 새 서버를 온라인 상태로 전환 하는 경우 연결이 끊긴 시간 제한이 만료 되기 전에 클라이언트는 복원 된 서버나 새 서버에 다시 연결 됩니다. 이 경우 SignalR 연결은 클라이언트에서 계속 진행 `Reconnected` 되 고 이벤트가 발생 합니다. 첫 번째 서버에서가 `OnDisconnected` 실행 되지 않으며 새 서버에서는이 이전에 해당 `OnReconnected` `OnConnected` 서버에서 해당 클라이언트에 대해 실행 되지 않은 경우에도이 실행 됩니다. 다시 부팅 또는 앱 도메인 재활용 후 클라이언트에서 동일한 서버에 다시 연결 하는 경우 서버를 다시 시작할 때 이전 연결 작업의 메모리가 없는 경우에도 결과가 동일 하 게 됩니다. 다음 다이어그램에서는 전송 API가 손실 된 연결을 즉시 인식 하 게 되는 것으로 가정 하므로 `ConnectionSlow` 이벤트가 발생 하지 않습니다.

![서버 오류 및 다시 연결](handling-connection-lifetime-events/_static/image5.png)

연결 끊기 제한 시간 내에 서버를 사용할 수 없게 되 면 SignalR 연결이 종료 됩니다. 이 시나리오에서 `Closed` `disconnected` JavaScript 클라이언트의 이벤트는 클라이언트에서 발생 하지만 `OnDisconnected` 서버에서 호출 되지 않습니다. 다음 다이어그램에서는 전송 API가 손실 된 연결을 인식 하지 못하는 것으로 가정 하므로 SignalR keepalive 기능을 통해 감지 되 고 `ConnectionSlow` 이벤트가 발생 합니다.

![서버 오류 및 시간 제한](handling-connection-lifetime-events/_static/image6.png)

<a id="timeoutkeepalive"></a>

## <a name="timeout-and-keepalive-settings"></a>시간 제한 및 keepalive 설정

기본 `ConnectionTimeout` , `DisconnectTimeout` 및 값은 `KeepAlive` 대부분의 시나리오에 적합 하지만 환경에 특별 한 요구 사항이 있는 경우 변경할 수 있습니다. 예를 들어 네트워크 환경에서 5 초 동안 유휴 상태인 연결을 닫으면 keepalive 값을 줄여야 할 수 있습니다.

<a id="connectiontimeout"></a>

### <a name="connectiontimeout"></a>ConnectionTimeout

이 설정은 전송 연결을 열고 응답을 기다린 후 닫은 후 새 연결을 여는 데 걸리는 시간을 나타냅니다. 기본값은 110 초입니다.

이 설정은 일반적으로 긴 폴링 전송에만 적용 되는 keepalive 기능이 사용 하지 않도록 설정 된 경우에만 적용 됩니다. 다음 다이어그램에서는 긴 폴링 전송 연결에 대 한이 설정의 효과를 보여 줍니다.

![긴 폴링 전송 연결](handling-connection-lifetime-events/_static/image7.png)

<a id="disconnecttimeout"></a>

### <a name="disconnecttimeout"></a>Disconnecttimeout은

이 설정은 이벤트를 발생 시키기 전에 전송 연결이 끊어진 후 대기 하는 시간을 나타냅니다 `Disconnected` . 기본값은 30초입니다. 를 설정 하면 `DisconnectTimeout` `KeepAlive` 값이 자동으로 1/3로 설정 됩니다 `DisconnectTimeout` .

<a id="keepalive"></a>

### <a name="keepalive"></a>KeepAlive

이 설정은 유휴 연결을 통해 keepalive 패킷을 보내기 전에 대기 하는 시간을 나타냅니다. 기본값은 10초입니다. 이 값은 1/3 보다 커야 합니다 `DisconnectTimeout` .

및를 둘 다 설정 하려면 `DisconnectTimeout` `KeepAlive` 다음을 설정 `KeepAlive` `DisconnectTimeout` 합니다. 그렇지 않으면 `KeepAlive` `DisconnectTimeout` 시간 제한 값을 자동으로 1/3로 설정 하는 경우 설정을 덮어씁니다 `KeepAlive` .

Keepalive 기능을 사용 하지 않도록 설정 하려면를 `KeepAlive` null로 설정 합니다. 자동으로 Keepalive 기능을 사용 하지 않도록 설정 하는 긴 폴링 전송 합니다.

<a id="changetimeout"></a>

### <a name="how-to-change-timeout-and-keepalive-settings"></a>시간 제한 및 keepalive 설정을 변경 하는 방법

이러한 설정에 대 한 기본값을 변경 하려면 `Application_Start` 다음 예제와 같이 *global.asax* 파일의에 설정 합니다. 예제 코드에 표시 된 값은 기본값과 같습니다.

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample1.cs)]

<a id="notifydisconnect"></a>

## <a name="how-to-notify-the-user-about-disconnections"></a>사용자에 게 연결이 끊어지지 않도록 알리는 방법

일부 응용 프로그램에서는 연결 문제가 있는 경우 사용자에 게 메시지를 표시 하는 것이 좋습니다. 이 작업을 수행 하는 방법 및 시기에 대 한 몇 가지 옵션이 있습니다. 다음 코드 샘플은 생성 된 프록시를 사용 하는 JavaScript 클라이언트를 위한 것입니다.

- `connectionSlow`SignalR가 연결 문제를 인식 한 후 다시 연결 모드로 전환 되기 전에 메시지를 표시 하는 이벤트를 처리 합니다.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample2.js)]
- `reconnecting`SignalR가 연결 끊기를 인식 하 고 다시 연결 모드로 전환 될 때 메시지를 표시 하는 이벤트를 처리 합니다.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample3.js)]
- 이벤트를 처리 `disconnected` 하 여 다시 연결 하려는 시도가 시간 초과 되었을 때 메시지를 표시 합니다. 이 시나리오에서 서버와의 연결을 다시 설정 하는 유일한 방법은 `Start` 새 연결 ID를 만드는 메서드를 호출 하 여 SignalR 연결을 다시 시작 하는 것입니다. 다음 코드 샘플에서는 플래그를 사용 하 여 메서드를 호출 하 여 SignalR 연결에 대 한 일반적인 종료 이후가 아니라 다시 연결 제한 시간 후에만 알림을 실행 하도록 합니다 `Stop` .

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample4.js)]

<a id="continuousreconnect"></a>

## <a name="how-to-continuously-reconnect"></a>지속적으로 다시 연결 하는 방법

일부 응용 프로그램에서는 연결이 끊어졌거나 다시 연결 하려는 시도가 시간 초과 된 후 자동으로 다시 설정 하는 것이 좋습니다. 이렇게 하려면 `Start` `Closed` 이벤트 처리기 ( `disconnected` JavaScript 클라이언트의 이벤트 처리기)에서 메서드를 호출할 수 있습니다. `Start`서버 또는 실제 연결을 사용할 수 없을 때이를 너무 자주 수행 하지 않도록 하기 위해를 호출 하기 전에 시간을 기다려야 할 수 있습니다. 다음 코드 샘플은 생성 된 프록시를 사용 하는 JavaScript 클라이언트를 위한 것입니다.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample5.js)]

모바일 클라이언트에서 알아야 할 잠재적인 문제는 서버 또는 물리적 연결을 사용할 수 없을 때 연속 다시 연결을 시도 하면 불필요 한 배터리가 소모 될 수 있다는 것입니다.

<a id="disconnectclientfromserver"></a>

## <a name="how-to-disconnect-a-client-in-server-code"></a>서버 코드에서 클라이언트의 연결을 끊는 방법

SignalR 버전 2에는 클라이언트 연결을 끊는 기본 제공 서버 API가 없습니다. [나중에이 기능을 추가할 계획이](https://github.com/SignalR/SignalR/issues/2101)있습니다. 현재 SignalR 릴리스에서 서버와 클라이언트의 연결을 끊는 가장 간단한 방법은 클라이언트에서 disconnect 메서드를 구현 하 고 서버에서 해당 메서드를 호출 하는 것입니다. 다음 코드 샘플에서는 생성 된 프록시를 사용 하는 JavaScript 클라이언트에 대 한 연결 끊기 메서드를 보여 줍니다.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample6.js)]

> [!WARNING]
> 보안-클라이언트 연결 끊기 또는 제안 된 기본 제공 API에 대 한이 방법은 악성 코드를 실행 하는 해킹 클라이언트의 시나리오를 해결 합니다. 클라이언트는 다시 연결 하거나 해킹 당한 코드에서 메서드를 제거 `stopClient` 하거나 수행 하는 작업을 변경할 수 있기 때문입니다. 상태 저장 DOS (서비스 거부) 보호를 구현 하는 적절 한 장소는 프레임 워크 또는 서버 계층이 아니라 프런트 엔드 인프라에 있는 것입니다.

<a id="detectingreasonfordisconnection"></a>
## <a name="detecting-the-reason-for-a-disconnection"></a>연결 끊기 이유 검색

SignalR 2.1 `OnDisconnect` 은 클라이언트의 제한 시간이 초과 되는 것이 아니라 의도적으로 해제 되었는지 여부를 나타내는 오버 로드를 서버 이벤트에 추가 합니다. `StopCalled` 클라이언트에서 연결을 명시적으로 닫은 경우 매개 변수는 true입니다. JavaScript에서 서버 오류가 발생 하면 클라이언트에서 연결을 끊을 수 있습니다. 오류 정보는로 클라이언트에 전달 됩니다 `$.connection.hub.lastError` .

**C # 서버 코드: `stopCalled` 매개 변수**

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample7.cs?highlight=1,3)]

**JavaScript 클라이언트 코드: `lastError` 이벤트에서 액세스 `disconnect` 합니다.**

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample8.js?highlight=2-3)]
