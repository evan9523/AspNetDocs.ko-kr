---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: 'ASP.NET SignalR Hubs API 가이드-서버 (c #) | Microsoft Docs'
author: bradygaster
description: 이 문서에서는 SignalR 버전 2 용 ASP.NET SignalR Hubs API의 서버 쪽 프로그래밍에 대해 소개 하 고, 코드 샘플을 보여 줍니다.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345379"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a>ASP.NET SignalR Hubs API 가이드-서버 (c #)

[Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 일반적인 옵션을 보여 주는 코드 샘플을 사용 하 여 SignalR 버전 2 용 ASP.NET SignalR Hubs API의 서버 쪽 프로그래밍에 대 한 소개를 제공 합니다.
> 
> SignalR Hubs API를 사용 하면 서버에서 연결 된 클라이언트로 또는 클라이언트에서 서버로 Rpc (원격 프로시저 호출)를 수행할 수 있습니다. 서버 코드에서는 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다. 클라이언트 코드에서는 서버에서 호출할 수 있는 메서드를 정의 하 고 서버에서 실행 되는 메서드를 호출 합니다. SignalR는 모든 클라이언트에서 서버로의 작업을 수행 합니다.
> 
> 또한 SignalR는 영구 연결 이라고 하는 하위 수준 API를 제공 합니다. SignalR, 허브 및 영구 연결에 대 한 소개는 [SignalR 2 소개](../getting-started/introduction-to-signalr.md)를 참조 하세요.
> 
> ## <a name="software-versions-used-in-this-topic"></a>이 항목에서 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - SignalR 버전 2
>   
> 
> 
> ## <a name="topic-versions"></a>토픽 버전
> 
> 이전 버전의 SignalR에 대 한 자세한 내용은 [SignalR 이전 버전](../older-versions/index.md)을 참조 하세요.
> 
> ## <a name="questions-and-comments"></a>질문 및 설명
> 
> 이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요. 자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.

## <a name="overview"></a>개요

이 문서는 다음 섹션으로 구성됩니다.

- [SignalR 미들웨어를 등록 하는 방법](#route)

    - [/Signalr URL](#signalrurl)
    - [SignalR 옵션 구성](#options)
- [허브 클래스를 만들고 사용 하는 방법](#hubclass)

    - [허브 개체 수명](#transience)
    - [카멜식-JavaScript 클라이언트에서 허브 이름의 대/소문자 구분](#hubnames)
    - [여러 허브](#multiplehubs)
    - [강력한 형식의 허브](#stronglytypedhubs)
- [클라이언트가 호출할 수 있는 허브 클래스에서 메서드를 정의 하는 방법](#hubmethods)

    - [카멜식-JavaScript 클라이언트에서 메서드 이름의 대/소문자 구분](#methodnames)
    - [비동기적으로 실행 하는 경우](#asyncmethods)
    - [오버 로드 정의](#overloads)
    - [허브 메서드 호출의 진행률 보고](#progress)
- [허브 클래스에서 클라이언트 메서드를 호출 하는 방법](#callfromhub)

    - [RPC를 수신 하는 클라이언트 선택](#selectingclients)
    - [메서드 이름에 대 한 컴파일 타임 유효성 검사 없음](#dynamicmethodnames)
    - [대/소문자를 구분 하지 않는 메서드 이름 일치](#caseinsensitive)
    - [비동기 실행](#asyncclient)
- [허브 클래스에서 그룹 멤버 자격을 관리 하는 방법](#groupsfromhub)

    - [Add 및 Remove 메서드의 비동기 실행](#asyncgroupmethods)
    - [그룹 멤버 자격 지 속성](#grouppersistence)
    - [단일 사용자 그룹](#singleusergroups)
- [허브 클래스에서 연결 수명 이벤트를 처리 하는 방법](#connectionlifetime)

    - [OnConnected, Onconnected 및 Onconnected가 호출 되는 경우](#onreconnected)
    - [호출자 상태가 채워지지 않음](#nocallerstate)
- [컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법](#contextproperty)
- [클라이언트와 허브 클래스 간의 상태를 전달 하는 방법](#passstate)
- [허브 클래스에서 오류를 처리 하는 방법](#handleErrors)
- [허브 클래스 외부에서 클라이언트 메서드를 호출 하 고 그룹을 관리 하는 방법](#callfromoutsidehub)

    - [클라이언트 메서드 호출](#callingclientsoutsidehub)
    - [그룹 멤버 자격 관리](#managinggroupsoutsidehub)
- [추적을 사용 하도록 설정 하는 방법](#tracing)
- [허브 파이프라인을 사용자 지정 하는 방법](#hubpipeline)

클라이언트를 프로그래밍 하는 방법에 대 한 설명서는 다음 리소스를 참조 하세요.

- [SignalR Hubs API 가이드-JavaScript 클라이언트](hubs-api-guide-javascript-client.md)
- [SignalR Hubs API 가이드-.NET 클라이언트](hubs-api-guide-net-client.md)

SignalR 2 용 서버 구성 요소는 .NET 4.5 에서만 사용할 수 있습니다. .NET 4.0를 실행 하는 서버는 SignalR v1. x를 사용 해야 합니다.

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a>SignalR 미들웨어를 등록 하는 방법

클라이언트가 허브에 연결 하는 데 사용할 경로를 정의 하려면 `MapSignalR` 응용 프로그램이 시작 될 때 메서드를 호출 합니다. `MapSignalR` 는 클래스의 [확장 메서드입니다](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) `OwinExtensions` . 다음 예제에서는 OWIN startup 클래스를 사용 하 여 SignalR Hubs 경로를 정의 하는 방법을 보여 줍니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

SignalR 기능을 ASP.NET MVC 응용 프로그램에 추가 하는 경우 SignalR 경로가 다른 경로 앞에 추가 되었는지 확인 합니다. 자세한 내용은 [자습서: SignalR 2 및 MVC 5 시작](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)을 참조 하세요.

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a>/Signalr URL

기본적으로 클라이언트에서 허브에 연결 하는 데 사용할 경로 URL은 "/signalr"입니다. 이 URL은 자동으로 생성 된 JavaScript 파일에 대 한 "/signalr/hubs" URL과 혼동 하지 마세요. 생성 된 프록시에 대 한 자세한 내용은 [SignalR HUBS API 가이드-JavaScript 클라이언트-생성 된 프록시와 사용자를 위해 수행](hubs-api-guide-javascript-client.md#genproxy)하는 작업을 참조 하세요.

SignalR에 대해이 기본 URL을 사용할 수 없도록 하는 특별 한 상황이 있을 수 있습니다. 예를 들어 프로젝트에 이름이 *signalr* 인 폴더가 있으며 이름을 변경 하지 않으려는 경우 이 경우 다음 예제와 같이 기준 URL을 변경할 수 있습니다 (샘플 코드에서 "/signalr"을 원하는 URL로 바꿉니다).

**URL을 지정 하는 서버 코드**

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

**생성 된 프록시를 사용 하 여 URL을 지정 하는 JavaScript 클라이언트 코드**

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

**생성 된 프록시 없이 URL을 지정 하는 JavaScript 클라이언트 코드**

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

**URL을 지정 하는 .NET 클라이언트 코드**

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a>SignalR 옵션 구성

메서드의 오버 로드를 사용 하 여 `MapSignalR` 사용자 지정 URL, 사용자 지정 종속성 해결 프로그램 및 다음 옵션을 지정할 수 있습니다.

- 브라우저 클라이언트에서 CORS 또는 JSONP를 사용 하 여 도메인 간 호출을 사용 하도록 설정 합니다.

    일반적으로 브라우저에서에서 페이지를 로드 하는 경우 `http://contoso.com` SignalR 연결은에서 동일한 도메인에 `http://contoso.com/signalr` 있습니다. 에서 페이지가에 연결 되는 경우 `http://contoso.com` `http://fabrikam.com/signalr` 이는 도메인 간 연결입니다. 보안상의 이유로 도메인 간 연결은 기본적으로 사용 하지 않도록 설정 됩니다. 자세한 내용은 [ASP.NET SignalR HUBS API 가이드-JavaScript 클라이언트-도메인 간 연결을 설정 하는 방법](hubs-api-guide-javascript-client.md#crossdomain)을 참조 하세요.
- 자세한 오류 메시지를 사용 합니다.

    오류가 발생 하는 경우 SignalR의 기본 동작은 클라이언트에 알림 메시지를 전송 하 여 발생 한 상황에 대 한 세부 정보를 제공 하지 않는 것입니다. 악의적인 사용자가 응용 프로그램에 대 한 공격 정보를 사용할 수 있기 때문에 클라이언트에 자세한 오류 정보를 보내는 것은 프로덕션 환경에서 권장 되지 않습니다. 문제를 해결 하려면이 옵션을 사용 하 여 더 많은 정보를 제공 하는 오류 보고를 일시적으로 사용 합니다.
- 자동으로 생성 된 JavaScript 프록시 파일을 사용 하지 않도록 설정 합니다.

    기본적으로 허브 클래스에 대 한 프록시를 포함 하는 JavaScript 파일은 URL "/signalr/hubs"에 대 한 응답으로 생성 됩니다. JavaScript 프록시를 사용 하지 않으려는 경우 또는이 파일을 수동으로 생성 하 고 클라이언트의 물리적 파일을 참조 하려는 경우이 옵션을 사용 하 여 프록시 생성을 사용 하지 않도록 설정할 수 있습니다. 자세한 내용은 [SignalR HUBS API 가이드-JavaScript 클라이언트-SignalR 생성 프록시에 대 한 물리적 파일을 만드는 방법](hubs-api-guide-javascript-client.md#manualproxy)을 참조 하세요.

다음 예제에서는 메서드 호출에서 SignalR 연결 URL 및 이러한 옵션을 지정 하는 방법을 보여 줍니다 `MapSignalR` . 사용자 지정 URL을 지정 하려면 예의 "/signalr"를 사용 하려는 URL로 바꿉니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a>허브 클래스를 만들고 사용 하는 방법

허브를 만들려면 [Signalr](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)에서 파생 되는 클래스를 만듭니다. 다음 예제에서는 채팅 응용 프로그램에 대 한 간단한 허브 클래스를 보여 줍니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

이 예제에서 연결 된 클라이언트는 메서드를 호출할 수 있으며,이 `NewContosoChatMessage` 경우 수신 된 데이터는 연결 된 모든 클라이언트에 브로드캐스트 됩니다.

<a id="transience"></a>

### <a name="hub-object-lifetime"></a>허브 개체 수명

서버에서 허브 클래스를 인스턴스화하거나 사용자의 코드에서 해당 메서드를 호출 하지 않습니다. 모든 작업은 SignalR Hubs 파이프라인에서 수행 됩니다. SignalR는 클라이언트가 서버에 연결, 연결 끊기 또는 메서드 호출을 수행 하는 경우와 같은 허브 작업을 처리 해야 할 때마다 허브 클래스의 새 인스턴스를 만듭니다.

허브 클래스의 인스턴스는 일시적 이므로이를 사용 하 여 하나의 메서드 호출에서 다음으로 상태를 유지할 수 없습니다. 서버가 클라이언트에서 메서드 호출을 받을 때마다 허브 클래스의 새 인스턴스가 메시지를 처리 합니다. 여러 연결과 메서드 호출을 통해 상태를 유지 하려면 데이터베이스, 허브 클래스의 정적 변수 또는에서 파생 되지 않은 다른 클래스와 같은 다른 메서드를 사용 `Hub` 합니다. 허브 클래스에서 정적 변수와 같은 메서드를 사용 하 여 메모리에 데이터를 저장 하는 경우 응용 프로그램 도메인이 재활용 되 면 데이터가 손실 됩니다.

허브 클래스 외부에서 실행 되는 자체 코드에서 클라이언트에 메시지를 보내려는 경우 허브 클래스 인스턴스를 인스턴스화하여 수행할 수 없지만 허브 클래스의 SignalR context 개체에 대 한 참조를 가져오면 됩니다. 자세한 내용은이 항목의 뒷부분에 나오는 [클라이언트 메서드를 호출 하 고 허브 클래스 외부에서 그룹을 관리 하는 방법](#callfromoutsidehub) 을 참조 하세요.

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a>카멜식-JavaScript 클라이언트에서 허브 이름의 대/소문자 구분

기본적으로 JavaScript 클라이언트는 카멜식 대/소문자 버전의 클래스 이름을 사용 하 여 허브를 참조 합니다. SignalR는 JavaScript 코드가 JavaScript 규칙을 준수할 수 있도록 이러한 변경을 자동으로 수행 합니다. 이전 예제를 `contosoChatHub` JavaScript 코드에서 라고 합니다.

**서버**

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

**생성 된 프록시를 사용 하는 JavaScript 클라이언트**

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

클라이언트에서 사용할 다른 이름을 지정 하려면 특성을 추가 `HubName` 합니다. 특성을 사용 하는 경우 `HubName` JavaScript 클라이언트에서 카멜식 대/소문자로 이름이 변경 되지 않습니다.

**서버**

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

**생성 된 프록시를 사용 하는 JavaScript 클라이언트**

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a>여러 허브

응용 프로그램에서 여러 허브 클래스를 정의할 수 있습니다. 이렇게 하면 연결이 공유 되지만 그룹은 다음과 같이 구분 됩니다.

- 모든 클라이언트는 동일한 URL을 사용 하 여 서비스 ("/signalr") 또는 사용자 지정 URL (지정 된 경우)과 SignalR 연결을 설정 하 고, 해당 연결은 서비스에서 정의 된 모든 허브에 사용 됩니다.

    단일 클래스의 모든 허브 기능을 정의 하는 것과 비교 했을 때 여러 허브에 대 한 성능 차이는 없습니다.
- 모든 허브는 동일한 HTTP 요청 정보를 가져옵니다.

    모든 허브가 동일한 연결을 공유 하므로 서버에서 발생 하는 HTTP 요청 정보는 SignalR 연결을 설정 하는 원래 HTTP 요청에 제공 됩니다. 쿼리 문자열을 지정 하 여 클라이언트에서 서버로 정보를 전달 하는 데 연결 요청을 사용 하는 경우 다른 허브에 다른 쿼리 문자열을 제공할 수 없습니다. 모든 허브는 동일한 정보를 받습니다.
- 생성 된 JavaScript 프록시 파일은 한 파일의 모든 허브에 대 한 프록시를 포함 합니다.

    JavaScript 프록시에 대 한 자세한 내용은 [SignalR HUBS API 가이드-Javascript 클라이언트-생성 된 프록시와 사용자를 위해 수행 하는 작업](hubs-api-guide-javascript-client.md#genproxy)을 참조 하세요.
- 그룹은 허브 내에서 정의 됩니다.

    SignalR에서 명명 된 그룹을 정의 하 여 연결 된 클라이언트의 하위 집합에 브로드캐스트할 수 있습니다. 그룹은 각 허브에 대해 개별적으로 유지 관리 됩니다. 예를 들어 "Administrators" 라는 그룹에는 클래스에 대 한 하나의 클라이언트 집합이 포함 `ContosoChatHub` 되며 동일한 그룹 이름은 클래스의 다른 클라이언트 집합을 참조 합니다 `StockTickerHub` .

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a>Strongly-Typed 허브

클라이언트에서 참조할 수 있는 허브 메서드에 대 한 인터페이스를 정의 하 고 허브 메서드에서 Intellisense를 사용 하도록 설정 하려면 다음을 수행 하는 `Hub<T>` 것이 아니라 (SignalR 2.1에 도입 됨)에서 허브를 파생 합니다 `Hub` .

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a>클라이언트가 호출할 수 있는 허브 클래스에서 메서드를 정의 하는 방법

허브의 메서드를 클라이언트에서 호출할 수 있도록 하려면 다음 예제와 같이 public 메서드를 선언 합니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

모든 c # 메서드에서와 같이 복합 형식 및 배열을 포함 하 여 반환 형식 및 매개 변수를 지정할 수 있습니다. 매개 변수로 받거나 호출자에 게 반환 되는 모든 데이터는 JSON을 사용 하 여 클라이언트와 서버 간에 전달 되며 SignalR는 복잡 한 개체의 바인딩과 개체의 배열을 자동으로 처리 합니다.

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a>카멜식-JavaScript 클라이언트에서 메서드 이름의 대/소문자 구분

기본적으로 JavaScript 클라이언트는 카멜식 대/소문자를 사용 하는 메서드 이름 버전을 사용 하 여 허브 메서드를 참조 합니다. SignalR는 JavaScript 코드가 JavaScript 규칙을 준수할 수 있도록 이러한 변경을 자동으로 수행 합니다.

**서버**

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

**생성 된 프록시를 사용 하는 JavaScript 클라이언트**

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

클라이언트에서 사용할 다른 이름을 지정 하려면 특성을 추가 `HubMethodName` 합니다.

**서버**

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

**생성 된 프록시를 사용 하는 JavaScript 클라이언트**

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a>비동기적으로 실행 하는 경우

메서드가 장기 실행 되거나 데이터베이스 조회 나 웹 서비스 호출과 같이 대기와 관련 된 작업을 수행 해야 하는 경우 반환 형식 대신 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) ( `void` 반환 대신) 또는 [작업 &lt; T &gt; ](https://msdn.microsoft.com/library/dd321424.aspx) 개체를 반환 하 여 허브 메서드를 비동기식으로 만듭니다 `T` . 메서드에서 개체를 반환 하는 경우 `Task` SignalR은가 완료 될 때까지 대기한 `Task` 다음 래핑 해제 된 결과를 다시 클라이언트에 보냅니다. 따라서 클라이언트에서 메서드 호출을 코딩 하는 방법에는 차이가 없습니다.

허브 메서드를 비동기적으로 만들면 WebSocket 전송을 사용할 때 연결 차단이 방지 됩니다. 허브 메서드가 동기적으로 실행 되 고 전송이 WebSocket 인 경우 허브 메서드가 완료 될 때까지 동일한 클라이언트에서 허브에 있는 메서드를 이후에 호출 하는 것은 차단 됩니다.

다음 예제에서는 동기적 또는 비동기적으로 실행 되도록 코딩 된 동일한 메서드를 보여 주고, 두 버전을 호출 하는 데 사용할 수 있는 JavaScript 클라이언트 코드를 보여 줍니다.

**동기**

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

**비동기**

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

**생성 된 프록시를 사용 하는 JavaScript 클라이언트**

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

ASP.NET 4.5에서 비동기 메서드를 사용 하는 방법에 대 한 자세한 내용은 [ASP.NET MVC 4에서 비동기 메서드 사용](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)을 참조 하세요.

<a id="overloads"></a>

### <a name="defining-overloads"></a>오버 로드 정의

메서드에 대 한 오버 로드를 정의 하려면 각 오버 로드의 매개 변수 수가 서로 달라 야 합니다. 서로 다른 매개 변수 형식을 지정 하 여 오버 로드를 구분 하는 경우 허브 클래스가 컴파일되지만 SignalR 서비스는 클라이언트가 오버 로드 중 하나를 호출 하려고 할 때 런타임에 예외를 throw 합니다.

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a>허브 메서드 호출의 진행률 보고

SignalR 2.1에는 .NET 4.5에 도입 된 [진행률 보고 패턴](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) 에 대 한 지원이 추가 되었습니다. 진행률 보고를 구현 하려면 `IProgress<T>` 클라이언트가 액세스할 수 있는 허브 메서드에 대 한 매개 변수를 정의 합니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

장기 실행 서버 메서드를 작성 하는 경우 허브 스레드를 차단 하는 대신 비동기/대기와 같은 비동기 프로그래밍 패턴을 사용 하는 것이 중요 합니다.

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a>허브 클래스에서 클라이언트 메서드를 호출 하는 방법

서버에서 클라이언트 메서드를 호출 하려면 `Clients` 허브 클래스의 메서드에서 속성을 사용 합니다. 다음 예제에서는 연결 된 모든 클라이언트에서를 호출 하는 서버 코드 `addNewMessageToPage` 와 JavaScript 클라이언트에서 메서드를 정의 하는 클라이언트 코드를 보여 줍니다.

**서버**

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

클라이언트 메서드 호출은 비동기 작업 이며를 반환 `Task` 합니다. `await`는 다음 용도로 사용합니다.

* 메시지를 오류 없이 보낼지 확인 합니다. 
* Try-catch 블록에서 오류를 catch 하 고 처리할 수 있도록 합니다.

**생성 된 프록시를 사용 하는 JavaScript 클라이언트**

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

클라이언트 메서드에서 반환 값을 가져올 수 없습니다. 와 같은 구문은 `int x = Clients.All.add(1,1)` 작동 하지 않습니다.

매개 변수에 대 한 복합 형식 및 배열을 지정할 수 있습니다. 다음 예제에서는 메서드 매개 변수에서 복합 형식을 클라이언트에 전달 합니다.

**복합 개체를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

**복합 개체를 정의 하는 서버 코드**

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

**생성 된 프록시를 사용 하는 JavaScript 클라이언트**

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a>RPC를 수신 하는 클라이언트 선택

Clients 속성은 RPC를 수신 하는 클라이언트를 지정 하는 여러 옵션을 제공 하는 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) 개체를 반환 합니다.

- 연결된 모든 클라이언트입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- 호출 클라이언트만

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- 호출 클라이언트를 제외한 모든 클라이언트입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- 연결 ID로 식별 되는 특정 클라이언트입니다.

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    이 예제에서는 `addContosoChatMessageToPage` 호출 클라이언트에서를 호출 하 고를 사용 하는 것과 동일한 효과를 가집니다 `Clients.Caller` .
- 지정 된 클라이언트를 제외한 연결 된 모든 클라이언트는 연결 ID로 식별 됩니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- 지정 된 그룹의 모든 연결 된 클라이언트입니다.

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- 지정 된 그룹에서 연결 ID로 식별 된 지정 된 클라이언트를 제외한 모든 연결 된 클라이언트입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- 호출 클라이언트를 제외한 지정 된 그룹에 있는 모든 연결 된 클라이언트입니다.

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- 사용자 Id로 식별 되는 특정 사용자입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    기본적으로이는 이지만 `IPrincipal.Identity.Name` [IUserIdProvider의 구현을 전역 호스트에 등록](mapping-users-to-connections.md#IUserIdProvider)하 여 변경할 수 있습니다.
- 연결 Id 목록의 모든 클라이언트 및 그룹

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- 그룹 목록입니다.

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- 이름으로 된 사용자입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- SignalR 2.1에 도입 된 사용자 이름 목록입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a>메서드 이름에 대 한 컴파일 타임 유효성 검사 없음

지정 하는 메서드 이름은 동적 개체로 해석 됩니다. 즉, IntelliSense 또는 컴파일 타임 유효성 검사를 수행 하지 않습니다. 식은 런타임에 계산 됩니다. 메서드 호출이 실행 되 면 SignalR는 메서드 이름 및 매개 변수 값을 클라이언트에 보내고, 클라이언트에 이름과 일치 하는 메서드가 있으면 해당 메서드가 호출 되 고 매개 변수 값이 전달 됩니다. 클라이언트에서 일치 하는 메서드를 찾을 수 없는 경우 오류가 발생 하지 않습니다. 클라이언트 메서드를 호출할 때 SignalR가 백그라운드에서 클라이언트로 전송 하는 데이터 형식에 대 한 자세한 내용은 [SignalR 소개](../getting-started/introduction-to-signalr.md)를 참조 하세요.

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a>대/소문자를 구분 하지 않는 메서드 이름 일치

메서드 이름 일치는 대/소문자를 구분 하지 않습니다. 예를 들어 서버에 있는는 `Clients.All.addContosoChatMessageToPage` `AddContosoChatMessageToPage` 클라이언트에서, 또는를 실행 합니다 `addcontosochatmessagetopage` `addContosoChatMessageToPage` .

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a>비동기 실행

호출 하는 메서드는 비동기적으로 실행 됩니다. 클라이언트에 대 한 메서드 호출 후에 발생 하는 모든 코드는 다음 코드 줄이 메서드 완료를 기다리도록 지정 하지 않는 한 SignalR가 클라이언트에 데이터 전송을 완료할 때까지 기다리지 않고 즉시 실행 됩니다. 다음 코드 예제에서는 두 개의 클라이언트 메서드를 순차적으로 실행 하는 방법을 보여 줍니다.

**Wait 사용 (.NET 4.5)**

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

를 사용 하 여 `await` 다음 코드 줄이 실행 되기 전에 클라이언트 메서드가 완료 될 때까지 대기 하는 경우 클라이언트는 다음 코드 줄이 실행 되기 전에 실제로 메시지를 수신 하는 것을 의미 하지는 않습니다. 클라이언트 메서드 호출의 "완료"는 SignalR 메시지를 보내는 데 필요한 모든 작업을 수행 했음을 의미 합니다. 클라이언트에서 메시지를 받았는지 확인 해야 하는 경우 해당 메커니즘을 직접 프로그래밍 해야 합니다. 예를 들어 허브에서 메서드를 코딩 하 고 클라이언트에서 `MessageReceived` `addContosoChatMessageToPage` 수행 해야 하는 작업을 수행한 후에 호출할 수 있는 메서드를 호출할 수 있습니다 `MessageReceived` . 허브의에서 `MessageReceived` 실제 클라이언트 수신 및 원래 메서드 호출 처리에 따라 달라 지는 작업을 수행할 수 있습니다.

### <a name="how-to-use-a-string-variable-as-the-method-name"></a>문자열 변수를 메서드 이름으로 사용 하는 방법

문자열 변수를 메서드 이름으로 사용 하 여 클라이언트 메서드를 호출 하려면 `Clients.All` (또는 `Clients.Others` , 등 `Clients.Caller` )를로 캐스팅 한 `IClientProxy` 다음 [invoke (methodName, args ...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)를 호출 합니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a>허브 클래스에서 그룹 멤버 자격을 관리 하는 방법

SignalR의 그룹은 연결 된 클라이언트의 지정 된 하위 집합에 메시지를 브로드캐스팅하는 메서드를 제공 합니다. 그룹에는 원하는 수의 클라이언트가 있을 수 있으며, 클라이언트는 원하는 수의 그룹의 구성원이 될 수 있습니다.

그룹 멤버 자격을 관리 하려면 허브 클래스의 속성에서 제공 하는 [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) 및 [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) 메서드를 사용 합니다 `Groups` . 다음 예제에서는 `Groups.Add` `Groups.Remove` 클라이언트 코드에서 호출 되는 허브 메서드에서 사용 되는 및 메서드와이를 호출 하는 JavaScript 클라이언트 코드를 보여 줍니다.

**서버**

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

**생성 된 프록시를 사용 하는 JavaScript 클라이언트**

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

그룹을 명시적으로 만들 필요는 없습니다. 실제로는에 대 한 호출에서 처음으로 해당 이름을 지정할 때 그룹이 자동으로 생성 `Groups.Add` 되며, 해당 그룹의 멤버 자격에서 마지막 연결을 제거 하면 그룹이 삭제 됩니다.

그룹 구성원 목록이 나 그룹 목록을 가져오기 위한 API는 없습니다. SignalR는 [pub/sub 모델](http://en.wikipedia.org/wiki/Publish/subscribe)을 기반으로 클라이언트 및 그룹에 메시지를 보내고 서버는 그룹 또는 그룹 멤버 자격 목록을 유지 하지 않습니다. 이를 통해 웹 팜에 노드를 추가할 때마다 SignalR가 유지 관리 하는 모든 상태를 새 노드에 전파 해야 하므로 확장성을 최대화할 수 있습니다.

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a>Add 및 Remove 메서드의 비동기 실행

`Groups.Add`및 `Groups.Remove` 메서드는 비동기적으로 실행 됩니다. 그룹에 클라이언트를 추가 하 고 해당 그룹을 사용 하 여 클라이언트에 즉시 메시지를 보내려면 `Groups.Add` 메서드가 먼저 완료 되는지 확인 해야 합니다. 다음 코드 예제에서는이 작업을 수행 하는 방법을 보여 줍니다.

**클라이언트를 그룹에 추가한 다음 해당 클라이언트에 메시징**

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a>그룹 멤버 자격 지 속성

SignalR는 사용자가 아닌 연결을 추적 하므로 사용자가 연결을 설정할 때마다 사용자가 동일한 그룹에 포함 되도록 하려면 `Groups.Add` 사용자가 새 연결을 설정할 때마다를 호출 해야 합니다.

일시적으로 연결이 끊어지면 SignalR에서 자동으로 연결을 복원할 수 있습니다. 이 경우 SignalR는 새 연결을 설정 하지 않고 동일한 연결을 복원 하므로 클라이언트의 그룹 멤버 자격은 자동으로 복원 됩니다. 이는 그룹 멤버 자격을 포함 하 여 각 클라이언트에 대 한 연결 상태가 클라이언트에 게 라운드트립 되기 때문에 일시적 중단이 서버 재부팅 또는 실패의 결과일 때에도 가능 합니다. 연결 시간이 초과 되기 전에 서버가 중단 되 고 새 서버로 교체 되는 경우 클라이언트는 새 서버에 자동으로 다시 연결 하 고 해당 그룹이 속한 그룹에 다시 등록할 수 있습니다.

연결 손실 후 자동으로 연결을 복원할 수 없거나 연결 시간이 초과 되거나 클라이언트가 연결을 끊을 때 (예: 브라우저가 새 페이지로 이동 하는 경우) 그룹 멤버 자격이 손실 됩니다. 사용자가 다음에 연결할 때 새 연결이 됩니다. 동일한 사용자가 새 연결을 설정할 때 그룹 멤버 자격을 유지 하려면 응용 프로그램에서 사용자와 그룹 간의 연결을 추적 하 고 사용자가 새 연결을 설정할 때마다 그룹 멤버 자격을 복원 해야 합니다.

연결 및 횟수에 대 한 자세한 내용은이 항목의 뒷부분에 있는 [허브 클래스에서 연결 수명 이벤트를 처리 하는 방법](#connectionlifetime) 을 참조 하세요.

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a>단일 사용자 그룹

SignalR를 사용 하는 응용 프로그램은 일반적으로 메시지를 보낸 사용자와 메시지를 수신 해야 하는 사용자를 확인 하기 위해 사용자와 연결 간의 연결을 추적 해야 합니다. 이러한 작업을 수행 하기 위해 일반적으로 사용 되는 두 패턴 중 하나에서 그룹이 사용 됩니다.

- 단일 사용자 그룹.

    사용자 이름을 그룹 이름으로 지정 하 고 사용자가 연결 하거나 다시 연결할 때마다 현재 연결 ID를 그룹에 추가할 수 있습니다. 그룹에 보내는 사용자에 게 메시지를 보냅니다. 이 방법의 단점은 그룹이 사용자를 온라인 또는 오프 라인 상태 인지 여부를 확인 하는 방법을 제공 하지 않는다는 것입니다.
- 사용자 이름과 연결 Id 간의 연결을 추적 합니다.

    사전 또는 데이터베이스에 각 사용자 이름과 하나 이상의 연결 Id 사이에 연결을 저장 하 고, 사용자가 연결 하거나 연결을 끊을 때마다 저장 된 데이터를 업데이트할 수 있습니다. 사용자에 게 메시지를 보내려면 연결 Id를 지정 합니다. 이 방법의 단점은 더 많은 메모리를 사용 하는 것입니다.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a>허브 클래스에서 연결 수명 이벤트를 처리 하는 방법

연결 수명 이벤트를 처리 하는 일반적인 이유는 사용자가 연결 되었는지 여부를 추적 하 고 사용자 이름과 연결 Id 간의 연결을 추적 하는 것입니다. 클라이언트에서 연결 하거나 연결을 끊을 때 사용자 고유의 코드를 실행 `OnConnected` 하려면 `OnDisconnected` `OnReconnected` 다음 예제와 같이 허브 클래스의, 및 가상 메서드를 재정의 합니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a>OnConnected, Onconnected 및 Onconnected가 호출 되는 경우

브라우저가 새 페이지로 이동할 때마다 새 연결을 설정 해야 합니다. 즉, SignalR는 메서드를 실행 한 후 메서드를 실행 `OnDisconnected` `OnConnected` 합니다. SignalR는 새 연결이 설정 될 때 항상 새 연결 ID를 만듭니다.

`OnReconnected`이 메서드는 연결 시간이 초과 되기 전에 케이블을 일시적으로 분리 하 고 다시 연결 하는 경우와 같이 SignalR가 자동으로 복구 하는 연결이 일시적으로 끊어질 때 호출 됩니다. `OnDisconnected`메서드는 브라우저가 새 페이지로 이동 하는 경우와 같이 클라이언트 연결이 끊어져 SignalR가 자동으로 다시 연결할 수 없는 경우에 호출 됩니다. 따라서 지정 된 클라이언트에 대해 가능한 이벤트 시퀀스는 `OnConnected` ,,, `OnReconnected` `OnDisconnected` 또는 `OnConnected` `OnDisconnected` 입니다. `OnConnected` `OnDisconnected` `OnReconnected` 지정 된 연결에 대 한 시퀀스는 표시 되지 않습니다.

`OnDisconnected`서버 작동이 중단 되거나 응용 프로그램 도메인이 재활용 되는 등의 일부 시나리오에서는 메서드가 호출 되지 않습니다. 다른 서버를 온라인 상태로 만들거나 앱 도메인에서 재활용이 완료 되 면 일부 클라이언트는 이벤트를 다시 연결 하 여 실행할 수 있습니다 `OnReconnected` .

자세한 내용은 [SignalR의 연결 수명 이벤트 이해 및 처리](handling-connection-lifetime-events.md)를 참조 하세요.

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a>호출자 상태가 채워지지 않음

연결 수명 이벤트 처리기 메서드는 서버에서 호출 됩니다. 즉, 클라이언트의 개체에 배치 하는 모든 상태가 `state` 서버의 속성에 채워지지 않습니다 `Caller` . 개체 및 속성에 대 한 자세한 내용은 `state` `Caller` 이 항목의 뒷부분에 나오는 [클라이언트와 허브 클래스 간의 상태를 전달 하는 방법](#passstate) 을 참조 하십시오.

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a>컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법

클라이언트에 대 한 정보를 가져오려면 `Context` 허브 클래스의 속성을 사용 합니다. `Context`속성은 다음 정보에 대 한 액세스를 제공 하는 [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) 개체를 반환 합니다.

- 호출 클라이언트의 연결 ID입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    연결 ID는 SignalR에서 할당 한 GUID입니다 (사용자 고유의 코드에서 값을 지정할 수 없음). 각 연결에 대해 하나의 연결 ID가 있으며, 응용 프로그램에 허브가 여러 개 있는 경우 모든 허브에서 동일한 연결 ID를 사용 합니다.
- HTTP 헤더 데이터입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    에서 HTTP 헤더를 가져올 수도 있습니다 `Context.Headers` . 동일한 작업을 수행 하는 이유는 먼저 생성 된 것이 고 `Context.Headers` , `Context.Request` 속성은 나중에 추가 되었으며, `Context.Headers` 이전 버전과의 호환성을 위해 유지 되었습니다.
- 쿼리 문자열 데이터입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    에서 쿼리 문자열 데이터를 가져올 수도 있습니다 `Context.QueryString` .

    이 속성에서 가져오는 쿼리 문자열은 SignalR 연결을 설정 하는 HTTP 요청에 사용 된 문자열입니다. 클라이언트에서 서버로 클라이언트에 대 한 데이터를 전달 하는 편리한 방법인 연결을 구성 하 여 클라이언트에서 쿼리 문자열 매개 변수를 추가할 수 있습니다. 다음 예에서는 생성 된 프록시를 사용할 때 JavaScript 클라이언트에서 쿼리 문자열을 추가 하는 한 가지 방법을 보여 줍니다.

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    쿼리 문자열 매개 변수를 설정 하는 방법에 대 한 자세한 내용은 [JavaScript](hubs-api-guide-javascript-client.md) 및 [.net](hubs-api-guide-net-client.md) 클라이언트에 대 한 API 가이드를 참조 하세요.

    SignalR에서 내부적으로 사용 되는 다른 값과 함께 쿼리 문자열 데이터에서 연결에 사용 되는 전송 방법을 찾을 수 있습니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    값은 `transportMethod` "websocket", "serverSentEvents", "foreverFrame" 또는 "가 중 폴링"입니다. 이벤트 처리기 메서드에서이 값을 확인 하는 경우 `OnConnected` 일부 시나리오에서 처음에는 연결에 대해 협상 된 최종 전송 방법이 아닌 전송 값을 가져올 수 있습니다. 이 경우 메서드는 예외를 throw 하 고 나중에 최종 전송 메서드가 설정 될 때 다시 호출 됩니다.
- 쿠키.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    에서 쿠키를 가져올 수도 있습니다 `Context.RequestCookies` .
- 사용자 정보입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- 요청에 대 한 HttpContext 개체:

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    `HttpContext.Current` `HttpContext` SignalR 연결에 대 한 개체를 가져오는 대신이 메서드를 사용 합니다.

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a>클라이언트와 허브 클래스 간의 상태를 전달 하는 방법

클라이언트 프록시는 `state` 각 메서드 호출을 사용 하 여 서버로 전송 하려는 데이터를 저장할 수 있는 개체를 제공 합니다. 서버에서 `Clients.Caller` 클라이언트에 의해 호출 되는 허브 메서드의 속성에서이 데이터에 액세스할 수 있습니다. `Clients.Caller`속성은 연결 수명 이벤트 처리기 메서드인, 및에 대해 채워지지 `OnConnected` 않습니다 `OnDisconnected` `OnReconnected` .

개체와 속성의 데이터를 만들거나 업데이트 하는 것은 양방향 `state` `Clients.Caller` 으로 작동 합니다. 서버에서 값을 업데이트할 수 있으며 클라이언트에 다시 전달 됩니다.

다음 예제에서는 모든 메서드 호출을 통해 서버로 전송 되는 상태를 저장 하는 JavaScript 클라이언트 코드를 보여 줍니다.

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

다음 예제에서는 .NET 클라이언트의 해당 코드를 보여 줍니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

허브 클래스에서 속성의이 데이터에 액세스할 수 있습니다 `Clients.Caller` . 다음 예제에서는 이전 예제에서 참조 되는 상태를 검색 하는 코드를 보여 줍니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> 상태를 유지 하기 위한이 메커니즘은 많은 양의 데이터를 위한 것이 아닙니다. 또는 속성에 넣은 모든 항목 `state` `Clients.Caller` 은 모든 메서드 호출에서 라운드트립 되기 때문입니다. 사용자 이름 또는 카운터와 같은 작은 항목에 유용 합니다.

VB.NET 또는 강력한 형식의 허브에서 호출자 상태 개체에 액세스할 수 없습니다 `Clients.Caller` . 대신을 사용 합니다 `Clients.CallerState` (SignalR 2.1에 도입 됨).

**C에서 CallerState 사용 #**

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

**Visual Basic에서 CallerState 사용**

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a>허브 클래스에서 오류를 처리 하는 방법

허브 클래스 메서드에서 발생 하는 오류를 처리 하려면 먼저를 사용 하 여 비동기 작업 (예: 클라이언트 메서드 호출)에서 발생 하는 모든 예외를 "관찰" `await` 합니다. 다음 방법 중 하나 이상을 사용 합니다.

- Try-catch 블록에서 메서드 코드를 래핑하고 예외 개체를 기록 합니다. 디버깅을 위해 클라이언트에 예외를 보낼 수 있지만, 보안상의 이유로 프로덕션 환경에서 클라이언트에 자세한 정보를 전송 하는 것은 권장 되지 않습니다.
- [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) 메서드를 처리 하는 허브 파이프라인 모듈을 만듭니다. 다음 예제에서는 오류를 기록 하 고, 모듈을 허브 파이프라인에 삽입 하는 Startup.cs의 코드를 기록 하는 파이프라인 모듈을 보여 줍니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- `HubException`SignalR 2에 도입 된 클래스를 사용 합니다. 이 오류는 모든 허브 호출에서 throw 될 수 있습니다. `HubError`생성자는 문자열 메시지를 사용 하 고 추가 오류 데이터를 저장 하기 위한 개체를 사용 합니다. SignalR는 예외를 자동으로 직렬화 하 고 클라이언트에 보냅니다. 그러면이 예외를 사용 하 여 허브 메서드 호출을 거부 하거나 실패 하 게 됩니다.

    다음 코드 샘플에서는 허브 호출 중에을 throw 하는 방법과 `HubException` JavaScript 및 .net 클라이언트에서 예외를 처리 하는 방법을 보여 줍니다.

    **HubException 클래스를 보여 주는 서버 코드**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    **허브에서 HubException을 throw 하는 응답을 보여 주는 JavaScript 클라이언트 코드**

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    **허브에서 HubException을 throw 하는 응답을 보여 주는 .NET 클라이언트 코드**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

허브 파이프라인 모듈에 대 한 자세한 내용은이 항목의 뒷부분에 나오는 [허브 파이프라인을 사용자 지정 하는 방법](#hubpipeline) 을 참조 하세요.

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a>추적을 사용 하도록 설정 하는 방법

서버 쪽 추적을 사용 하도록 설정 하려면 다음 예제와 같이 Web.config 파일에 시스템 진단 요소를 추가 합니다.

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

Visual Studio에서 응용 프로그램을 실행 하면 **출력** 창에서 로그를 볼 수 있습니다.

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a>허브 클래스 외부에서 클라이언트 메서드를 호출 하 고 그룹을 관리 하는 방법

허브 클래스와 다른 클래스에서 클라이언트 메서드를 호출 하려면 허브에 대 한 SignalR context 개체에 대 한 참조를 가져온 다음 클라이언트에서 메서드를 호출 하거나 그룹을 관리 하는 데 사용 합니다.

다음 샘플 `StockTicker` 클래스는 컨텍스트 개체를 가져와 클래스의 인스턴스에 저장 하 고, 클래스 인스턴스를 정적 속성에 저장 하 고, singleton 클래스 인스턴스의 컨텍스트를 사용 하 여 `updateStockPrice` 라는 허브에 연결 된 클라이언트에서 메서드를 호출 합니다 `StockTickerHub` .

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

수명이 긴 개체에서 여러 번 컨텍스트를 사용 해야 하는 경우에는 참조를 한 번 가져온 다음 매번 다시 가져오는 대신 저장 합니다. 컨텍스트를 한 번 가져오면 SignalR에서 허브 메서드가 클라이언트 메서드 호출을 수행 하는 것과 동일한 순서로 메시지를 클라이언트에 보냅니다. 허브에 SignalR 컨텍스트를 사용 하는 방법을 보여 주는 자습서는 [ASP.NET SignalR를 사용 하 여 서버 브로드캐스트](../getting-started/tutorial-server-broadcast-with-signalr.md)를 참조 하세요.

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a>클라이언트 메서드 호출

RPC를 받을 클라이언트를 지정할 수 있지만 허브 클래스에서를 호출 하는 경우 보다 더 낮은 옵션을 사용할 수 있습니다. 그 이유는 컨텍스트가 클라이언트의 특정 호출과 연결 되지 않기 때문 이며,, 또는와 같은 현재 연결 ID를 알고 있어야 하는 메서드는 `Clients.Others` `Clients.Caller` `Clients.OthersInGroup` 사용할 수 없습니다. 다음 옵션을 사용할 수 있습니다.

- 연결된 모든 클라이언트입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- 연결 ID로 식별 되는 특정 클라이언트입니다.

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- 지정 된 클라이언트를 제외한 연결 된 모든 클라이언트는 연결 ID로 식별 됩니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- 지정 된 그룹의 모든 연결 된 클라이언트입니다.

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- 지정 된 그룹에서 연결 ID로 식별 된 지정 된 클라이언트를 제외한 모든 연결 된 클라이언트입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

허브 클래스의 메서드에서 비 허브 클래스를 호출 하는 경우 현재 연결 ID를 전달 하 고, 또는와 함께 사용 하 여 `Clients.Client` `Clients.AllExcept` `Clients.Group` , 또는을 시뮬레이션할 수 있습니다 `Clients.Caller` `Clients.Others` `Clients.OthersInGroup` . 다음 예제에서 클래스는 클래스에 `MoveShapeHub` 대 한 연결 ID를 전달 하 여 클래스를 `Broadcaster` `Broadcaster` 시뮬레이션할 수 있게 `Clients.Others` 합니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a>그룹 멤버 자격 관리

그룹 관리의 경우 허브 클래스와 동일한 옵션을 사용할 수 있습니다.

- 그룹에 클라이언트 추가

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- 그룹에서 클라이언트 제거

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a>허브 파이프라인을 사용자 지정 하는 방법

SignalR를 사용 하면 허브 파이프라인에 사용자 고유의 코드를 삽입할 수 있습니다. 다음 예제에서는 클라이언트에서 수신 된 각 들어오는 메서드 호출 및 클라이언트에서 호출 된 나가는 메서드 호출을 기록 하는 사용자 지정 허브 파이프라인 모듈을 보여 줍니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

*Startup.cs* 파일의 다음 코드는 허브 파이프라인에서 실행 되도록 모듈을 등록 합니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

재정의할 수 있는 여러 가지 방법이 있습니다. 전체 목록은 [HubPipelineModule 메서드](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)를 참조 하세요.
