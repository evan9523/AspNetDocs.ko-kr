---
uid: signalr/overview/guide-to-the-api/handling-connection-lifetime-events
title: SignalR의 연결 수명 이벤트 이해 및 처리 | 마이크로 소프트 문서
author: bradygaster
description: 이 문서에서는 Hubs API에서 노출되는 이벤트를 사용하는 방법을 설명합니다.
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 03960de2-8d95-4444-9169-4426dcc64913
msc.legacyurl: /signalr/overview/guide-to-the-api/handling-connection-lifetime-events
msc.type: authoredcontent
ms.openlocfilehash: 5bdf20549fccab5d644e35fdf4ce351540c8620d
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675828"
---
# <a name="understanding-and-handling-connection-lifetime-events-in-signalr"></a>SignalR의 연결 수명 이벤트 이해 및 처리

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 처리할 수 있는 SignalR 연결, 다시 연결 및 연결 끊김 이벤트, 구성할 수 있는 시간 초과 및 keepalive 설정에 대한 개요를 제공합니다.
>
> 이 문서에서는 SignalR 및 연결 수명 이벤트에 대한 지식이 이미 있다고 가정합니다. 시그널R에 대한 소개는 [시그널R 소개를](../getting-started/introduction-to-signalr.md)참조하십시오. 연결 수명 이벤트 목록은 다음 리소스를 참조하십시오.
>
> - [Hub 클래스에서 연결 수명 이벤트를 처리하는 방법](hubs-api-guide-server.md#connectionlifetime)
> - [JavaScript 클라이언트에서 연결 수명 이벤트를 처리하는 방법](hubs-api-guide-javascript-client.md#connectionlifetime)
> - [.NET 클라이언트에서 연결 수명 이벤트를 처리하는 방법](hubs-api-guide-net-client.md#connectionlifetime)
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

이 문서에는 다음과 같은 섹션이 포함되어 있습니다.

- [연결 수명 용어 및 시나리오](#terminology)

    - [SignalR 연결, 전송 연결 및 물리적 연결](#signalrvstransport)
    - [전송 연결 끊김 시나리오](#transportdisconnect)
    - [클라이언트 연결 끊기 시나리오](#clientdisconnect)
    - [서버 연결 끊기 시나리오](#serverdisconnect)
- [시간 시간 및 유지 설정](#timeoutkeepalive)

    - [연결 시간 시간](#connectiontimeout)
    - [연결 해제 시간](#disconnecttimeout)
    - [Keepalive](#keepalive)
    - [시간 시간 및 keepalive 설정을 변경하는 방법](#changetimeout)
- [연결 끊김에 대해 사용자에게 알리는 방법](#notifydisconnect)
- [지속적으로 다시 연결하는 방법](#continuousreconnect)
- [서버 코드에서 클라이언트 연결을 끊는 방법](#disconnectclientfromserver)
- [연결 끊기 이유 감지](#detectingreasonfordisconnection)

API 참조 항목에 대한 링크는 .NET 4.5 버전의 API에 대한 것입니다. .NET 4를 사용하는 경우 [.NET 4 버전의 API 항목을](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)참조하십시오.

<a id="terminology"></a>

## <a name="connection-lifetime-terminology-and-scenarios"></a>연결 수명 용어 및 시나리오

SignalR Hub의 이벤트 처리기는 `OnReconnected` `OnConnected` 지정된 클라이언트에 대해 직접 실행할 수 있지만 이후에는 `OnDisconnected` 실행할 수 없습니다. 연결이 끊어지지지지 않고 다시 연결할 수 있는 이유는 SignalR에서 "연결"이라는 단어가 사용되는 여러 가지 방법이 있기 때문입니다.

<a id="signalrvstransport"></a>

### <a name="signalr-connections-transport-connections-and-physical-connections"></a>SignalR 연결, 전송 연결 및 물리적 연결

이 문서에서는 *SignalR 연결,* *전송 연결*및 *물리적 연결을*구분합니다.

- **SignalR 연결은** SignalR API에 의해 유지 관리되고 연결 ID로 고유하게 식별되는 클라이언트와 서버 URL 간의 논리적 관계를 나타냅니다. 이 관계에 대한 데이터는 SignalR에 의해 유지되며 전송 연결을 설정하는 데 사용됩니다. SignalR이 손실된 전송 연결을 다시 설정하려고 `Stop` 시도하는 동안 클라이언트가 메서드또는 시간 제한 제한에 도달하면 관계가 종료되고 SignalR이 데이터를 삭제합니다.
- **전송 연결은** 클라이언트와 서버 간의 논리적 관계를 말하며, 웹소켓, 서버 전송 이벤트, 영원히 프레임 또는 긴 폴링의 네 가지 전송 API 중 하나에 의해 유지관리됩니다. SignalR는 전송 API를 사용하여 전송 연결을 만들고 전송 API는 전송 연결을 만들기 위해 물리적 네트워크 연결의 존재에 따라 달라집니다. 전송 연결은 SignalR이 종료하거나 전송 API가 물리적 연결이 끊어졌음을 감지할 때 종료됩니다.
- **물리적 연결은** 클라이언트 컴퓨터와 서버 컴퓨터 간의 통신을 용이하게 하는 전선, 무선 신호, 라우터 등 물리적 네트워크 링크를 말합니다. 전송 연결을 설정하려면 물리적 연결이 있어야 하며 SignalR 연결을 설정하려면 전송 연결을 설정해야 합니다. 그러나 물리적 연결을 끊는 것이 항상 전송 연결 또는 SignalR 연결을 즉시 종료하지는 않습니다.

다음 다이어그램에서 SignalR 연결은 허브 API 및 영구 연결 API SignalR 계층으로 표시되고 전송 연결은 전송 계층으로 표시되고 물리적 연결은 서버와 클라이언트 사이의 선으로 표시됩니다.

![시그널R 아키텍처 다이어그램](handling-connection-lifetime-events/_static/image1.png)

SignalR 클라이언트에서 메서드를 `Start` 호출할 때 서버에 대한 물리적 연결을 설정하는 데 필요한 모든 정보를 SignalR 클라이언트 코드에 제공합니다. SignalR 클라이언트 코드는 이 정보를 사용하여 HTTP 요청을 하고 네 가지 전송 방법 중 하나를 사용하는 물리적 연결을 설정합니다. 전송 연결이 실패하거나 서버가 실패하면 클라이언트가 동일한 SignalR URL에 대한 새 전송 연결을 자동으로 다시 설정하는 데 필요한 정보를 여전히 가지고 있기 때문에 SignalR 연결이 즉시 사라지지 않습니다. 이 시나리오에서는 사용자 응용 프로그램의 개입이 관련 되지 않습니다 및 SignalR 클라이언트 코드 새 전송 연결을 설정 하는 경우 새 SignalR 연결을 시작 하지 않습니다. SignalR 연결의 연속성은 `Start` 메서드를 호출할 때 생성되는 연결 ID가 변경되지 않는다는 사실에 반영됩니다.

Hub의 `OnReconnected` 이벤트 처리기는 전송 연결이 손실된 후 자동으로 다시 설정될 때 실행됩니다. 이벤트 `OnDisconnected` 처리기는 SignalR 연결의 끝에서 실행됩니다. SignalR 연결은 다음 방법으로 종료될 수 있습니다.

- 클라이언트가 메서드를 `Stop` 호출하면 중지 메시지가 서버로 전송되고 클라이언트와 서버 모두 SignalR 연결을 즉시 종료합니다.
- 클라이언트와 서버 간의 연결이 끊어진 후 클라이언트는 다시 연결을 시도하고 서버는 클라이언트가 다시 연결될 때까지 기다립니다. 다시 연결시도가 실패하고 연결 해제 시간 지정 기간이 끝나면 클라이언트와 서버 모두 SignalR 연결을 종료합니다. 클라이언트는 다시 연결하려고 중지하고 서버는 SignalR 연결의 표현을 삭제합니다.
- 클라이언트가 `Stop` 메서드를 호출할 수 없이 실행을 중지하면 서버는 클라이언트가 다시 연결될 때까지 기다린 다음 연결 해제 시간 지정 기간 이후에 SignalR 연결을 종료합니다.
- 서버 실행이 중지되면 클라이언트는 다시 연결(전송 연결 다시 생성)을 시도한 다음 연결 해제 시간 지정 기간 이후에 SignalR 연결을 종료합니다.

연결 문제가 없고 사용자 애플리케이션이 `Stop` 메서드를 호출하여 SignalR 연결을 종료하면 SignalR 연결과 전송 연결이 거의 동시에 시작되고 끝납니다. 다음 섹션에서는 다른 시나리오에 대해 자세히 설명합니다.

<a id="transportdisconnect"></a>

### <a name="transport-disconnection-scenarios"></a>전송 연결 끊김 시나리오

물리적 연결이 느려지거나 연결이 중단될 수 있습니다. 중단 길이와 같은 요인에 따라 전송 연결이 끊어질 수 있습니다. 그런 다음 SignalR은 전송 연결을 다시 설정하려고 시도합니다. 경우에 따라 전송 연결 API가 중단을 감지하고 전송 연결을 삭제하고 SignalR은 연결이 끊어지는 것을 즉시 알아냅니다. 다른 시나리오에서는 전송 연결 API나 SignalR 모두 연결이 손실되었음을 즉시 인식하지 않습니다. 긴 폴링을 제외한 모든 전송의 경우 SignalR 클라이언트는 *keepalive라는* 함수를 사용하여 전송 API가 감지할 수 없는 연결 손실을 확인합니다. 긴 폴링 연결에 대한 자세한 내용은 이 항목의 후반부에서 [시간 설정 및 keepalive 설정을](#timeoutkeepalive) 참조하십시오.

연결이 비활성 상태이면 서버는 주기적으로 keepalive 패킷을 클라이언트에 보냅니다. 이 문서가 작성된 날짜를 기준으로 기본 빈도는 10초마다 입니다. 이러한 패킷을 수신 대기하면 클라이언트는 연결 문제가 있는지 알 수 있습니다. 예상대로 keepalive 패킷이 수신되지 않으면 잠시 후 클라이언트는 느림 이나 중단과 같은 연결 문제가 있다고 가정합니다. 더 긴 시간 후에도 keepalive가 계속 수신되지 않으면 클라이언트는 연결이 끊긴 것으로 가정하고 다시 연결하려고 시작합니다.

다음 다이어그램은 전송 API에서 즉시 인식하지 못하는 물리적 연결에 문제가 있는 경우 일반적인 시나리오에서 발생하는 클라이언트 및 서버 이벤트를 보여 줍니다. 이 다이어그램은 다음과 같은 경우에 적용됩니다.

- 전송은 WebSockets, 영원히 프레임 또는 서버 전송 이벤트입니다.
- 실제 네트워크 연결에는 다양한 중단 기간이 있습니다.
- 전송 API는 중단을 인식하지 못하므로 SignalR은 keepalive 기능을 사용하여 이를 감지합니다.

![운송 연결 끊김](handling-connection-lifetime-events/_static/image2.png)

클라이언트가 다시 연결 모드로 전환되지만 연결 해제 제한 시간 내에 전송 연결을 설정할 수 없는 경우 서버는 SignalR 연결을 종료합니다. 이 경우 서버는 Hub의 `OnDisconnected` 메서드를 실행하고 클라이언트가 나중에 연결할 수 있는 경우에 대비하여 연결 끊기 메시지를 클라이언트에 보냅니다. 그런 다음 클라이언트가 다시 연결되면 연결 해제 `Stop` 명령을 받고 메서드를 호출합니다. 이 시나리오에서는 `OnReconnected` 클라이언트가 다시 연결될 때 `OnDisconnected` 실행되지 않으며 클라이언트가 `Stop`을 호출할 때 실행되지 않습니다. 다음 다이어그램은 이 시나리오를 보여 줍니다.

![전송 중단 - 서버 시간 시간](handling-connection-lifetime-events/_static/image3.png)

클라이언트에서 발생할 수 있는 SignalR 연결 수명 이벤트는 다음과 같습니다.

- `ConnectionSlow`클라이언트 이벤트.

    마지막 메시지 또는 keepalive ping이 수신된 이후 keepalive 시간 아웃 기간의 미리 설정된 비율이 경과한 경우에 발생합니다. 기본 keepalive 시간 시간 경고 기간은 keepalive 시간 설정의 2/3입니다. keepalive 시간 설정은 20초이므로 경고는 약 13초에서 발생합니다.

    기본적으로 서버는 10초마다 keepalive ping을 보내고 클라이언트는 약 2초마다 keepalive ping을 확인합니다(keepalive 시간 시간 값과 keepalive 시간 시간 경고 값 간의 차이의 3분의 1).

    전송 API가 연결 끊김을 인식하게 되면 Keepalive 시간 시간 경고 기간이 경과하기 전에 SignalR에 연결 끊김이 알려질 수 있습니다. 이 경우 `ConnectionSlow` 이벤트가 발생되지 않으며 SignalR이 `Reconnecting` 이벤트로 직접 이동합니다.
- `Reconnecting`클라이언트 이벤트.

    (a) 전송 API가 연결이 끊어졌다는 것을 감지하거나 (b) 마지막 메시지 또는 keepalive ping이 수신된 이후 keepalive 시간 아웃 기간이 경과한 경우 발생합니다. SignalR 클라이언트 코드가 다시 연결되기 시작합니다. 전송 연결이 끊어지면 응용 프로그램에서 일부 작업을 수행하려는 경우 이 이벤트를 처리할 수 있습니다. 기본 keepalive 시간 설정 기간은 현재 20초입니다.

    SignalR이 다시 연결 모드에 있는 동안 클라이언트 코드가 Hub 메서드를 호출하려고 하면 SignalR에서 명령을 보내려고 시도합니다. 대부분의 경우 이러한 시도는 실패하지만 경우에 따라 성공할 수도 있습니다. Server 에서 보낸 이벤트, 영원히 프레임 및 긴 폴링 전송의 경우 SignalR은 클라이언트가 메시지를 보내는 데 사용하는 통신 채널과 메시지를 수신하는 데 사용하는 통신 채널 두 개를 사용합니다. 수신에 사용되는 채널은 영구적으로 열려 있는 채널이며 물리적 연결이 중단될 때 닫힙입니다. 전송에 사용되는 채널은 계속 사용할 수 있으므로 물리적 연결이 복원되면 수신 채널을 다시 설정하기 전에 클라이언트에서 서버로메서드 호출이 성공할 수 있습니다. SignalR 수신에 사용되는 채널을 다시 열 때까지 반환 값이 수신되지 않습니다.
- `Reconnected`클라이언트 이벤트.

    전송 연결이 다시 설정될 때 발생합니다. 허브의 `OnReconnected` 이벤트 처리기가 실행됩니다.
- `Closed`클라이언트 이벤트`disconnected` (자바 스크립트의 이벤트).

    SignalR 클라이언트 코드가 전송 연결을 끊은 후 다시 연결을 시도하는 동안 연결 해제 시간 시간이 만료될 때 발생합니다. 기본 연결 해제 시간 설정은 30초입니다. 이 이벤트는 `Stop` 메서드가 호출되어 연결이 종료될 때도 발생합니다.

전송 API에서 검색되지 않고 keepalive 시간 초과 경고 기간보다 더 오래 서버에서 keepalive ping 수신을 지연시키지 않는 전송 연결 중단으로 인해 연결 수명 이벤트가 발생하지 않을 수 있습니다.

일부 네트워크 환경은 의도적으로 유휴 연결을 닫고 keepalive 패킷의 또 다른 기능은 이러한 네트워크에 SignalR 연결이 사용 중임을 알려줌으로써 이를 방지하는 것입니다. 극단적인 경우 keepalive ping의 기본 빈도가 닫힌 연결을 방지하기에 충분하지 않을 수 있습니다. 이 경우 keepalive ping을 더 자주 보내도록 구성할 수 있습니다. 자세한 내용은 이 항목의 후반부에서 [시간 설정 및 keepalive 설정을](#timeoutkeepalive) 참조하세요.

> [!NOTE]
>
> **중요**: 여기에 설명된 이벤트의 순서는 보장되지 않습니다. SignalR은 이 체계에 따라 예측 가능한 방식으로 연결 수명 이벤트를 발생시키려고 시도하지만 네트워크 이벤트의 변형과 전송 API와 같은 기본 통신 프레임워크가 이를 처리하는 여러 가지 방법이 있습니다. 예를 들어 `Reconnected` 클라이언트가 다시 연결될 때 이벤트가 발생하지 `OnConnected` 않거나 연결을 설정하려는 시도가 실패할 때 서버의 처리기가 실행될 수 있습니다. 이 항목에서는 일반적으로 특정 일반적인 상황에서 생성되는 효과만 설명합니다.

<a id="clientdisconnect"></a>

### <a name="client-disconnection-scenarios"></a>클라이언트 연결 끊기 시나리오

브라우저 클라이언트에서 SignalR 연결을 유지 관리하는 SignalR 클라이언트 코드는 웹 페이지의 JavaScript 컨텍스트에서 실행됩니다. 따라서 한 페이지에서 다른 페이지로 이동할 때 SignalR 연결이 종료되고 여러 브라우저 창이나 탭에서 연결하는 경우 여러 연결 아이디와 여러 연결이 있는 이유가 됩니다. 사용자가 브라우저 창이나 탭을 닫거나 새 페이지로 이동하거나 페이지를 새로 고치면 SignalR 클라이언트 코드가 해당 브라우저 이벤트를 처리하고 메서드를 `Stop` 호출하기 때문에 SignalR 연결이 즉시 종료됩니다. 이러한 시나리오에서 또는 응용 `Stop` 프로그램이 메서드를 호출할 `OnDisconnected` 때 클라이언트 플랫폼에서 이벤트 처리기가 서버에서 `Closed` 즉시 실행되고 `disconnected` 클라이언트가 이벤트를 발생시면 됩니다(이벤트는 JavaScript에서 명명됩니다).

클라이언트 응용 프로그램이나 실행 중인 컴퓨터가 충돌하거나 절전 모드로 이동하는 경우(예: 사용자가 랩톱을 닫을 때) 서버는 어떤 일이 일어났는지 에 대한 알림을 받지 않습니다. 서버가 아는 한 클라이언트가 손실되면 연결 중단으로 인한 것일 수 있으며 클라이언트가 다시 연결을 시도할 수 있습니다. 따라서 이러한 시나리오에서 서버는 클라이언트에 다시 연결할 수 있는 `OnDisconnected` 기회를 제공하기 위해 대기하며 연결 해제 시간(기본적으로 약 30초)이 만료될 때까지 실행되지 않습니다. 다음 다이어그램은 이 시나리오를 보여 줍니다.

![클라이언트 컴퓨터 오류](handling-connection-lifetime-events/_static/image4.png)

<a id="serverdisconnect"></a>

### <a name="server-disconnection-scenarios"></a>서버 연결 끊기 시나리오

서버가 오프라인 상태가 되면 재부팅, 실패, 앱 도메인 재활용 등 연결이 끊어지거나 전송 API와 SignalR이 서버가 사라졌다는 것을 즉시 알 수 있으며 SignalR은 `ConnectionSlow` 이벤트를 발생하지 않고 다시 연결하려고 시도할 수 있습니다. 클라이언트가 다시 연결 모드로 전환되고 서버가 복구되거나 다시 시작되거나 연결 해제 시간 만료 기간이 만료되기 전에 새 서버가 온라인 상태가 되면 클라이언트는 복원된 서버 또는 새 서버에 다시 연결됩니다. 이 경우 SignalR 연결이 클라이언트에서 계속되고 `Reconnected` 이벤트가 발생합니다. 첫 번째 서버에서는 `OnDisconnected` 실행되지 않으며 새 서버에서는 이전에 해당 서버에서 해당 클라이언트에 대해 실행되지 않았지만 `OnReconnected` `OnConnected` 실행됩니다. (서버가 다시 시작될 때 이전 연결 작업의 메모리가 없기 때문에 클라이언트가 재부팅 또는 앱 도메인 재활용 후 동일한 서버에 다시 연결하는 경우 효과입니다.) 다음 다이어그램에서는 전송 API가 손실된 연결을 즉시 `ConnectionSlow` 인식하므로 이벤트가 발생되지 않는다고 가정합니다.

![서버 오류 및 재연결](handling-connection-lifetime-events/_static/image5.png)

연결 해제 시간 시간 동안 서버를 사용할 수 없게 되면 SignalR 연결이 종료됩니다. 이 시나리오에서는 `Closed` 이벤트`disconnected` (자바 스크립트 클라이언트)는 클라이언트에서 `OnDisconnected` 발생 하지만 서버에서 호출 되지 않습니다. 다음 다이어그램에서는 전송 API가 연결이 손실된 것을 인식하지 못하므로 SignalR keepalive 기능에 `ConnectionSlow` 의해 감지되고 이벤트가 발생한다고 가정합니다.

![서버 오류 및 시간 시간](handling-connection-lifetime-events/_static/image6.png)

<a id="timeoutkeepalive"></a>

## <a name="timeout-and-keepalive-settings"></a>시간 시간 및 유지 설정

기본값 `ConnectionTimeout` `DisconnectTimeout`및 `KeepAlive` 값은 대부분의 시나리오에 적합하지만 환경에 특별한 요구 사항이 있는 경우 변경할 수 있습니다. 예를 들어 네트워크 환경이 5초 동안 유휴 상태인 연결을 닫는 경우 keepalive 값을 줄이어야 할 수 있습니다.

<a id="connectiontimeout"></a>

### <a name="connectiontimeout"></a>ConnectionTimeout

이 설정은 전송 연결을 열고 응답을 기다리는 시간을 나타냅니다. 기본값은 110초입니다.

이 설정은 keepalive 기능이 비활성화된 경우에만 적용되며 일반적으로 긴 폴링 전송에만 적용됩니다. 다음 다이어그램은 이 설정이 긴 폴링 전송 연결에 미치는 영향을 보여 줍니다.

![긴 폴링 전송 연결](handling-connection-lifetime-events/_static/image7.png)

<a id="disconnecttimeout"></a>

### <a name="disconnecttimeout"></a>연결 해제 시간

이 설정은 `Disconnected` 이벤트를 발생시키기 전에 전송 연결이 손실된 후 대기할 시간을 나타냅니다. 기본값은 30초입니다. 을 `DisconnectTimeout` `KeepAlive` 설정하면 `DisconnectTimeout` 값의 1/3로 자동으로 설정됩니다.

<a id="keepalive"></a>

### <a name="keepalive"></a>KeepAlive

이 설정은 유휴 연결을 통해 keepalive 패킷을 보내기 전에 기다려야 하는 시간을 나타냅니다. 기본값은 10초입니다. 이 값은 `DisconnectTimeout` 값의 1/3을 초과해서는 안 됩니다.

두 를 `DisconnectTimeout` 모두 설정하고 `KeepAlive`을 `KeepAlive` `DisconnectTimeout`설정하려면 . 그렇지 `KeepAlive` 않으면 시간 제한 `DisconnectTimeout` 값의 `KeepAlive` 1/3으로 자동으로 설정하면 설정이 덮어씁입니다.

keepalive 기능을 사용하지 않도록 설정하려면 null로 설정합니다. `KeepAlive` 긴 폴링 전송시 Keepalive 기능이 자동으로 비활성화됩니다.

<a id="changetimeout"></a>

### <a name="how-to-change-timeout-and-keepalive-settings"></a>시간 시간 및 keepalive 설정을 변경하는 방법

이러한 설정의 기본값을 변경하려면 다음 `Application_Start` 예제와 같이 *Global.asax* 파일에 설정합니다. 샘플 코드에 표시된 값은 기본값과 동일합니다.

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample1.cs)]

<a id="notifydisconnect"></a>

## <a name="how-to-notify-the-user-about-disconnections"></a>연결 끊김에 대해 사용자에게 알리는 방법

일부 응용 프로그램에서는 연결 문제가 있을 때 사용자에게 메시지를 표시할 수 있습니다. 이 작업을 수행하는 방법과 시기에 대한 몇 가지 옵션이 있습니다. 다음 코드 샘플은 생성된 프록시를 사용하는 JavaScript 클라이언트에 대한 것입니다.

- `connectionSlow` SignalR이 연결 문제를 인식하는 즉시 다시 연결 모드로 전환하기 전에 메시지를 표시하도록 이벤트를 처리합니다.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample2.js)]
- SignalR이 연결 끊김을 인식하고 다시 연결 모드로 전환될 때 `reconnecting` 메시지를 표시하도록 이벤트를 처리합니다.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample3.js)]
- 다시 `disconnected` 연결하려는 시도가 시간 만료되면 이벤트를 처리하여 메시지를 표시합니다. 이 시나리오에서 서버와의 연결을 다시 설정하는 유일한 방법은 `Start` 새 연결 ID를 만드는 메서드를 호출하여 SignalR 연결을 다시 시작하는 것입니다. 다음 코드 샘플에서는 메서드를 호출하여 발생하는 SignalR 연결이 정상 종료된 후가 아니라 다시 연결 시간 후에만 알림을 발행하도록 플래그를 `Stop` 사용합니다.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample4.js)]

<a id="continuousreconnect"></a>

## <a name="how-to-continuously-reconnect"></a>지속적으로 다시 연결하는 방법

일부 응용 프로그램에서는 연결이 손실되고 다시 연결하려는 시도가 시간 시간이 지난 후 연결을 자동으로 다시 설정할 수 있습니다. 이렇게하려면 이벤트 처리기 `Start` (JavaScript `Closed` `disconnected` 클라이언트의 이벤트 처리기)에서 메서드를 호출 할 수 있습니다. 서버 또는 물리적 연결을 사용할 수 `Start` 없을 때 너무 자주 이 작업을 수행하지 않도록 호출하기 전에 잠시 기다려야 할 수 있습니다. 다음 코드 샘플은 생성된 프록시를 사용하는 JavaScript 클라이언트에 대한 것입니다.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample5.js)]

모바일 클라이언트에서 알아야 할 잠재적인 문제는 서버 또는 물리적 연결을 사용할 수 없을 때 지속적인 재연결 시도로 인해 불필요한 배터리 소모가 발생할 수 있다는 것입니다.

<a id="disconnectclientfromserver"></a>

## <a name="how-to-disconnect-a-client-in-server-code"></a>서버 코드에서 클라이언트 연결을 끊는 방법

SignalR 버전 2에는 클라이언트 연결을 끊기 위한 기본 제공 서버 API가 없습니다. 이 [기능을 나중에 추가할 계획이 있습니다.](https://github.com/SignalR/SignalR/issues/2101) 현재 SignalR 릴리스에서 클라이언트를 서버에서 분리하는 가장 간단한 방법은 클라이언트에서 연결 끊기 메서드를 구현하고 서버에서 해당 메서드를 호출하는 것입니다. 다음 코드 샘플에서는 생성된 프록시를 사용하여 JavaScript 클라이언트에 대한 연결 끊기 메서드를 보여 주어집니다.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample6.js)]

> [!WARNING]
> 보안 - 클라이언트 연결을 끊는 이 방법이나 제안된 기본 제공 API는 클라이언트가 다시 연결하거나 해킹된 코드가 `stopClient` 메서드를 제거하거나 메서드를 변경할 수 있으므로 악성 코드를 실행하는 해킹된 클라이언트의 시나리오를 다루지 않습니다. DOS(상태 관리 거부) 보호를 구현하기 위한 적절한 장소는 프레임워크 나 서버 계층이 아니라 프런트 엔드 인프라에 있습니다.

<a id="detectingreasonfordisconnection"></a>
## <a name="detecting-the-reason-for-a-disconnection"></a>연결 끊기 이유 감지

SignalR 2.1은 서버 `OnDisconnect` 이벤트에 오버로드를 추가하여 클라이언트가 타이밍 을 초과하지 않고 의도적으로 연결이 끊어지는지 나타냅니다. `StopCalled` 매개 변수는 클라이언트가 명시적으로 연결을 닫은 경우 true입니다. JavaScript에서 서버 오류로 인해 클라이언트의 연결이 끊어지면 오류 정보가 `$.connection.hub.lastError`클라이언트에 로 전달됩니다.

**C# 서버 `stopCalled` 코드: 매개 변수**

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample7.cs?highlight=1,3)]

**자바 스크립트 클라이언트 코드 `lastError` : `disconnect` 이벤트에 액세스.**

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample8.js?highlight=2-3)]
