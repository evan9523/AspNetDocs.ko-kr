---
uid: signalr/overview/performance/signalr-performance
title: 시그널R 성능 | 마이크로 소프트 문서
author: bradygaster
description: SignalR 성능
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675720"
---
# <a name="signalr-performance"></a>SignalR 성능

로 [패트릭 플레처](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 항목에서는 SignalR 응용 프로그램의 성능을 설계, 측정 및 개선하는 방법에 대해 설명합니다.
>
> ## <a name="software-versions-used-in-this-topic"></a>이 항목에 사용된 소프트웨어 버전
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
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

SignalR 성능 및 확장에 대한 최근 프레젠테이션은 [ASP.NET SignalR로 실시간 웹 크기 조정을](https://channel9.msdn.com/Events/Build/2013/3-502)참조하십시오.

이 항목에는 다음과 같은 섹션이 포함되어 있습니다.

- [디자인 고려 사항](#design)
- [SignalR 서버의 성능 조정](#tuning)
- [성능 문제 해결](#troubleshooting)
- [SignalR 성능 카운터 사용](#perfcounters)
- [다른 성능 카운터 사용](#othercounters)
- [기타 리소스](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a>디자인 고려 사항

이 섹션에서는 SignalR 응용 프로그램을 디자인하는 동안 구현할 수 있는 패턴에 대해 설명하여 불필요한 네트워크 트래픽을 생성하여 성능이 저하되지 않도록 합니다.

### <a name="throttling-message-frequency"></a>메시지 빈도 제한

실시간 게임 응용 프로그램과 같이 고주파로 메시지를 보내는 응용 프로그램에서도 대부분의 응용 프로그램은 초당 몇 개 이상의 메시지를 보낼 필요가 없습니다. 각 클라이언트가 생성하는 트래픽의 양을 줄이기 위해 큐를 구현하고 메시지를 고정 된 속도보다 더 자주 보내지 않는 메시지 루프를 구현 할 수 있습니다 (즉, 해당 시간 간격에 메시지가 있는 경우 매 초마다 특정 수의 메시지가 전송됩니다). 메시지를 클라이언트와 서버 모두에서 특정 속도로 제한하는 샘플 응용 프로그램의 경우 [SignalR을 사용하여 고주파 실시간을](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)참조하십시오.

### <a name="reducing-message-size"></a>메시지 크기 줄이기

직렬화된 개체의 크기를 줄여 SignalR 메시지의 크기를 줄일 수 있습니다. 서버 코드에서 전송할 필요가 없는 속성을 포함하는 개체를 보내는 경우 특성을 `JsonIgnore` 사용하여 해당 속성이 직렬화되지 않도록 합니다. 속성 이름도 메시지에 저장됩니다. 속성의 이름은 특성을 `JsonProperty` 사용하여 줄일 수 있습니다. 다음 코드 샘플에서는 속성이 클라이언트로 전송되는 것을 제외하는 방법과 속성 이름을 줄이는 방법을 보여 줍니다.

**JsonIgnore 특성을 보여 주는 .NET 서버 코드는 클라이언트로 전송되는 데이터를 제외하고 JsonProperty 특성은 메시지 크기를 줄입니다.**

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

클라이언트 코드에서 가독성/유지 관리 가능성을 유지하기 위해 메시지를 받은 후 약식 속성 이름을 사용자 친화적인 이름으로 다시 매핑할 수 있습니다. 다음 코드 샘플에서는 메시지 계약(매핑)을 정의하고 함수를 `reMap` 사용하여 최적화된 메시지 클래스에 계약을 적용하여 단축된 이름을 더 긴 이름으로 다시 매핑하는 한 가지 방법을 보여 줍니다.

**사람이 읽을 수 있는 이름으로 단축된 속성 이름을 다시 매핑하는 클라이언트 측 JavaScript 코드**

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

동일한 방법을 사용하여 클라이언트에서 서버로 메시지를 줄일 수도 있습니다.

메시지 개체의 메모리 사용 공간(즉, 메시지에 사용되는 메모리 양)을 줄이면 성능도 향상될 수 있습니다. 예를 들어, 전체 `int` 범위가 필요하지 않은 경우 `short` `byte` 대신 a 또는 를 사용할 수 있습니다.

메시지는 서버 메모리의 메시지 버스에 저장되므로 메시지 크기를 줄이면 서버 메모리 문제도 해결할 수 있습니다.

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a>SignalR 서버의 성능 조정

다음 구성 설정을 사용하여 SignalR 응용 프로그램에서 더 나은 성능을 위해 서버를 조정할 수 있습니다. ASP.NET 응용 프로그램의 성능을 개선하는 방법에 대한 일반적인 내용은 [성능 ASP.NET 향상을](https://msdn.microsoft.com/library/ff647787.aspx)참조하십시오.

**시그널R 구성 설정**

- **DefaultMessageBufferSize**: 기본적으로 SignalR는 연결당 허브당 1000개의 메시지를 메모리에 유지합니다. 큰 메시지를 사용 하는 경우 이 값을 줄임으로써 완화 될 수 있는 메모리 문제를 만들 수 있습니다. 이 설정은 ASP.NET `Application_Start` 응용 프로그램의 이벤트 처리기 또는 `Configuration` 자체 호스팅 응용 프로그램의 OWIN 시작 클래스 의 메서드에서 설정할 수 있습니다. 다음 샘플에서는 사용되는 서버 메모리 양을 줄이기 위해 응용 프로그램의 메모리 공간을 줄이기 위해 이 값을 줄이는 방법을 보여 줍니다.

    **기본 메시지 버퍼 크기를 줄이기 위한 Startup.cs .NET 서버 코드**

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

**IIS 구성 설정**

- **응용 프로그램당 최대 동시 요청:** 동시 IIS 요청 수를 늘리면 요청을 제공하는 데 사용할 수 있는 서버 리소스가 증가합니다. 기본값은 5000입니다. 이 설정을 늘리려면 상승된 명령 프롬프트에서 다음 명령을 실행합니다.

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- **응용 프로그램 풀 큐길이**: Http.sys가 응용 프로그램 풀에 대해 큐에 대기하는 최대 요청 수입니다. 큐가 가득 차면 새 요청은 503 "서비스 사용 불가" 응답을 받습니다. 기본값은 1000입니다.

    응용 프로그램을 호스팅하는 응용 프로그램 풀에서 작업자 프로세스의 큐 길이를 줄이면 메모리 리소스가 절약됩니다. 자세한 내용은 [응용 프로그램 풀 관리, 튜닝 및 구성을](https://technet.microsoft.com/library/cc745955.aspx)참조하십시오.

**ASP.NET 구성 설정**

이 섹션에는 파일에서 설정할 수 `aspnet.config` 있는 구성 설정이 포함되어 있습니다. 이 파일은 플랫폼에 따라 두 위치 중 하나에서 찾을 수 있습니다.

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

SignalR 성능을 향상시킬 수 있는 ASP.NET 설정은 다음과 같습니다.

- **CPU당 최대 동시 요청**: 이 설정을 늘리면 성능 병목 현상이 완화될 수 있습니다. 이 설정을 늘리려면 다음 구성 설정을 `aspnet.config` 파일에 추가합니다.

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- **요청 대기열 제한**: 총 연결 수가 `maxConcurrentRequestsPerCPU` 설정을 초과하면 ASP.NET 큐를 사용하여 요청을 제한하기 시작합니다. 큐 크기를 늘리려면 `requestQueueLimit` 설정을 늘릴 수 있습니다. 이렇게 하려면 다음 구성 설정을 다음(대신) `processModel` `config/machine.config` `aspnet.config`노드에 추가합니다.

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a>성능 문제 해결

이 섹션에서는 응용 프로그램에서 성능 병목 현상을 찾는 방법을 설명합니다.

### <a name="verifying-that-websocket-is-being-used"></a>웹 소켓이 사용되고 있는지 확인

SignalR은 클라이언트와 서버 간의 통신을 위해 다양한 전송을 사용할 수 있지만 WebSocket은 상당한 성능 이점을 제공하며 클라이언트와 서버가 이를 지원하는 경우 사용해야 합니다. 클라이언트와 서버가 WebSocket에 대한 요구 사항을 충족하는지 확인하려면 [전송 및 대체 를](../getting-started/introduction-to-signalr.md#transports)참조하십시오. 응용 프로그램에서 사용되는 전송을 확인하려면 브라우저 개발자 도구를 사용하고 로그를 검사하여 연결에 사용되는 전송을 확인할 수 있습니다. 인터넷 익스플로러 및 크롬에서 브라우저 개발 도구를 사용하는 방법에 대한 자세한 내용은 [전송 및 대체를](../getting-started/introduction-to-signalr.md#transports)참조하십시오.

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a>SignalR 성능 카운터 사용

이 섹션에서는 `Microsoft.AspNet.SignalR.Utils` 패키지에 있는 SignalR 성능 카운터를 사용하도록 설정하고 사용하는 방법에 대해 설명합니다.

### <a name="installing-signalrexe"></a>시그널러(signalr.exe) 설치

SignalR.exe라는 유틸리티를 사용하여 성능 카운터를 서버에 추가할 수 있습니다. 이 유틸리티를 설치하려면 다음 단계를 따르십시오.

1. 비주얼 스튜디오에서 **솔루션에** > 대한 NuGet 패키지 관리자 관리 도구**NuGet 패키지 관리자를** > **선택합니다.**
2. **signalr.utils를 검색하고 설치를 선택합니다.**

    ![](signalr-performance/_static/image1.png)
3. 패키지 설치를 위한 사용권 계약에 동의합니다.
4. 시그널R.exe에 `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`설치됩니다.

### <a name="installing-performance-counters-with-signalrexe"></a>SignalR.exe를 가진 성능 카운터 설치

SignalR 성능 카운터를 설치하려면 다음 매개 변수를 사용하여 상승된 명령 프롬프트에서 SignalR.exe를 실행합니다.

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

SignalR 성능 카운터를 제거하려면 다음 매개 변수를 사용하여 상승된 명령 프롬프트에서 SignalR.exe를 실행합니다.

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a>시그널R 성능 카운터

유틸리티 패키지는 다음과 같은 성능 카운터를 설치합니다. "Total" 카운터는 마지막 응용 프로그램 풀 또는 서버가 다시 시작된 이후의 이벤트 수를 측정합니다.

**연결 메트릭**

다음 메트릭은 발생하는 연결 수명 이벤트를 측정합니다. 자세한 내용은 [연결 수명 이벤트 이해 및 처리를](../guide-to-the-api/handling-connection-lifetime-events.md)참조하십시오.

- **연결된 연결**
- **연결이 다시 연결됨**
- **연결이 끊어졌습니다.**
- **연결 전류**

**메시지 메트릭**

다음 메트릭은 SignalR에서 생성된 메시지 트래픽을 측정합니다.

- **수신된 연결 메시지 합계**
- **전송된 연결 메시지 총**
- **수신된 연결 메시지/초**
- **전송된 연결 메시지/초**

**메시지 버스 메트릭**

다음 메트릭은 모든 수신 및 발신 SignalR 메시지가 배치되는 큐인 내부 SignalR 메시지 버스를 통해 트래픽을 측정합니다. 메시지를 보내거나 브로드캐스트할 때 **게시됩니다.** 이 컨텍스트의 **구독자는** 메시지 버스의 구독입니다. 이는 클라이언트 수와 서버 자체의 수와 같아야 합니다. **할당된 작업자는** 활성 연결에 데이터를 보내는 구성 요소입니다. **바쁜 작업자는** 적극적으로 메시지를 보내는 작업자입니다.

- **메시지 버스 메시지 수신 합계**
- **메시지 버스 메시지 수신/초**
- **메시지 버스 메시지 게시 된 총**
- **메시지 버스 메시지 게시/초**
- **메시지 버스 구독자 최신**
- **메시지 버스 구독자 합계**
- **메시지 버스 구독자/초**
- **메시지 버스 할당 된 작업자**
- **메시지 버스 바쁜 작업자**
- **메시지 버스 주제 현재**

**오류 메트릭**

다음 메트릭은 SignalR 메시지 트래픽에서 생성된 오류를 측정합니다. **허브 또는 허브** 메서드를 확인할 수 없는 경우 허브 해결 오류가 발생합니다. **허브 호출** 오류는 허브 메서드를 호출하는 동안 throw된 예외입니다. **전송** 오류는 HTTP 요청 또는 응답 중에 발생한 연결 오류입니다.

- **오류: 모든 합계**
- **오류: 모든/초**
- **오류: 허브 해상도 합계**
- **오류: 허브 해상도/초**
- **오류: 허브 호출 합계**
- **오류: 허브 호출/초**
- **오류: 전송 총**
- **오류: 전송/초**

<a id="scaleout_metrics"></a>

**스케일아웃 메트릭**

다음 메트릭은 스케일아웃 공급자가 생성한 트래픽 및 오류를 측정합니다. 이 컨텍스트의 **스트림은** 스케일아웃 공급자가 사용하는 축척 단위입니다. 이 테이블은 SQL Server를 사용하는 경우, 서비스 버스가 사용되는 경우 항목 및 Redis가 사용되는 경우 구독입니다. 각 스트림은 정렬된 읽기 및 쓰기 작업을 보장합니다. 단일 스트림은 잠재적인 스케일 병목 현상이므로 스트림 수를 늘려 병목 현상을 줄일 수 있습니다. 여러 스트림을 사용하는 경우 SignalR은 지정된 연결에서 전송된 메시지가 순서대로 정렬되도록 하는 방식으로 이러한 스트림에 메시지를 자동으로 배포(샤드) 합니다.

[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) 설정은 SignalR에서 유지 관리하는 스케일아웃 송신 큐의 길이를 제어합니다. 값을 0보다 큰 값으로 설정하면 모든 메시지가 구성된 메시징 백플레인으로 한 번에 하나씩 전송될 송신 큐에 배치됩니다. 큐의 크기가 구성된 길이를 초과하면 큐의 메시지 수가 다시 설정보다 작을 때까지 보낼 후속 호출이 [InvalidOperationException을](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) 사용하여 즉시 실패합니다. 구현된 백플레인에는 일반적으로 자체 큐또는 플로우 제어가 있기 때문에 큐링은 기본적으로 비활성화됩니다. SQL Server의 경우 연결 풀링은 한 번에 진행되는 전송 수를 효과적으로 제한합니다.

기본적으로 SQL Server 및 Redis에는 하나의 스트림만 사용되며 서비스 버스에는 5개의 스트림이 사용되고 큐는 비활성화되지만 이러한 설정은 SQL Server 및 Service Bus의 구성을 통해 변경할 수 있습니다.

**SQL Server 백플레인의 테이블 수 및 큐 길이를 구성하기 위한 .NET 서버 코드**

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

**서비스 버스 백플레인에 대한 토픽 수 및 큐 길이를 구성하기 위한 .NET 서버 코드**

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

**버퍼링** 스트림은 오류가 있는 상태로 들어간 스트림입니다. 스트림이 오류 상태에 있으면 백플레인으로 전송된 모든 메시지는 스트림에 더 이상 오류가 없을 때까지 즉시 실패합니다. **큐 보내기 길이는** 게시되었지만 아직 전송되지 않은 메시지 수입니다.

- **스케일아웃 메시지 버스 메시지 수신/초**
- **스케일아웃 스트림 합계**
- **스케일아웃 스트림 열기**
- **스케일아웃 스트림 버퍼링**
- **스케일아웃 오류 합계**
- **스케일아웃 오류/초**
- **스케일아웃 송신 큐 길이**

이러한 카운터가 측정하는 내용에 대한 자세한 내용은 [Azure Service Bus의 SignalR 확장을](scaleout-with-windows-azure-service-bus.md)참조하십시오.

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a>다른 성능 카운터 사용

다음 성능 카운터는 응용 프로그램의 성능을 모니터링하는 데에도 유용할 수 있습니다.

**메모리**

- 모든 힙에서\\.NET CLR 메모리 # 바이트 (w3wp의 경우)

**ASP.NET**

- ASP.NET\요청 현재
- ASP.NET\큐
- ASP.NET\거부됨

**Cpu**

- 프로세서 정보\프로세서 시간

**TCP/IP**

- TCPv6/연결 설정
- TCPv4/연결 설정

**웹 서비스**

- 웹 서비스\현재 연결
- 웹 서비스\최대 연결

**스레딩**

- 현재 논리 스레드의\\.NET CLR 잠금 및 스레드 #
- 현재 물리적 스레드의 .NET CLR 잠금 및 스레드\\#

<a id="otherresources"></a>

## <a name="other-resources"></a>관련 자료

ASP.NET 성능 모니터링 및 튜닝에 대한 자세한 내용은 다음 항목을 참조하십시오.

- [ASP.NET 성능 개요](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)
- [IIS 7.5, IIS 7.0 및 IIS 6.0에서 스레드 사용량을 ASP.NET](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [&lt;응용&gt; 프로그램풀 요소(웹 설정)](https://msdn.microsoft.com/library/dd560842.aspx)
