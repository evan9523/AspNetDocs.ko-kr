---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: ASP.NET 시그널R 허브 API 가이드 - 서버(C#) | 마이크로 소프트 문서
author: bradygaster
description: 이 문서에서는 SignalR 버전 2에 대한 ASP.NET SignalR Hubs API의 서버 측면을 프로그래밍하는 방법을 소개하며 코드 샘플을 시연합니다.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675804"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a>ASP.NET 시그널R 허브 API 가이드 - 서버(C#)

로 [패트릭 플레처,](https://github.com/pfletcher) [톰 다이크스트라](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 SignalR 버전 2에 대한 ASP.NET SignalR Hubs API의 서버 측면을 프로그래밍하는 방법을 소개하며, 공통 옵션을 보여 주는 코드 샘플을 제공합니다.
> 
> SignalR Hubs API를 사용하면 서버에서 연결된 클라이언트로, 클라이언트에서 서버로 원격 프로시저 호출(RPC)을 수행할 수 있습니다. 서버 코드에서 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다. 클라이언트 코드에서는 서버에서 호출할 수 있는 메서드를 정의하고 서버에서 실행되는 메서드를 호출합니다. SignalR은 모든 클라이언트-서버 배관을 처리합니다.
> 
> SignalR는 또한 영구 연결이라는 하위 수준 API를 제공합니다. SignalR, 허브 및 영구 연결에 대한 소개는 [SignalR 2 소개를](../getting-started/introduction-to-signalr.md)참조하십시오.
> 
> ## <a name="software-versions-used-in-this-topic"></a>이 항목에 사용된 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - 시그널R 버전 2
>   
> 
> 
> ## <a name="topic-versions"></a>주제 버전
> 
> 이전 버전의 SignalR에 대한 자세한 내용은 [SignalR 이전 버전을](../older-versions/index.md)참조하십시오.
> 
> ## <a name="questions-and-comments"></a>질문 및 의견
> 
> 이 자습서를 어떻게 좋아했는지, 그리고 페이지 하단의 댓글에서 개선할 수 있는 내용에 대한 피드백을 남겨주세요. 당신은 튜토리얼과 직접 관련이없는 질문이있는 경우, 당신은 [ASP.NET SignalR 포럼에](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 게시하거나 [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>개요

이 문서는 다음 섹션으로 구성됩니다.

- [SignalR 미들웨어를 등록하는 방법](#route)

    - [/시그널러 URL](#signalrurl)
    - [신호R 옵션 구성](#options)
- [허브 클래스를 만들고 사용하는 방법](#hubclass)

    - [허브 개체 수명](#transience)
    - [자바 스크립트 클라이언트에서 허브 이름의 낙타 케이스](#hubnames)
    - [다중 허브](#multiplehubs)
    - [강력한 형식의 허브](#stronglytypedhubs)
- [클라이언트가 호출할 수 있는 Hub 클래스에서 메서드를 정의하는 방법](#hubmethods)

    - [자바 스크립트 클라이언트에서 메소드 이름의 낙타 대/소문자](#methodnames)
    - [비동기적으로 실행되는 경우](#asyncmethods)
    - [오버로드 정의](#overloads)
    - [허브 메서드 호출에서 진행률 보고](#progress)
- [Hub 클래스에서 클라이언트 메서드를 호출하는 방법](#callfromhub)

    - [RPC를 받을 클라이언트 선택](#selectingclients)
    - [메서드 이름에 대한 컴파일 타임 유효성 검사가 없습니다.](#dynamicmethodnames)
    - [대/소문자 구분 메서드 이름 일치](#caseinsensitive)
    - [비동기 실행](#asyncclient)
- [허브 클래스에서 그룹 구성원을 관리하는 방법](#groupsfromhub)

    - [메서드 추가 및 제거의 비동기 실행](#asyncgroupmethods)
    - [그룹 구성원 유지](#grouppersistence)
    - [단일 사용자 그룹](#singleusergroups)
- [Hub 클래스에서 연결 수명 이벤트를 처리하는 방법](#connectionlifetime)

    - [연결 됨, 연결이 끊긴 및 다시 연결해제된 경우](#onreconnected)
    - [호출자 상태가 채워지지 않음](#nocallerstate)
- [Context 속성에서 클라이언트에 대 한 정보를 얻는 방법](#contextproperty)
- [클라이언트와 Hub 클래스 간에 상태를 전달하는 방법](#passstate)
- [Hub 클래스에서 오류를 처리하는 방법](#handleErrors)
- [클라이언트 메서드를 호출하고 Hub 클래스 외부에서 그룹을 관리하는 방법](#callfromoutsidehub)

    - [클라이언트 메서드 호출](#callingclientsoutsidehub)
    - [그룹 구성원 관리](#managinggroupsoutsidehub)
- [추적을 활성화하는 방법](#tracing)
- [허브 파이프라인을 사용자 지정하는 방법](#hubpipeline)

클라이언트를 프로그래밍하는 방법에 대한 설명서는 다음 리소스를 참조하십시오.

- [시그널R 허브 API 가이드 - 자바 스크립트 클라이언트](hubs-api-guide-javascript-client.md)
- [시그널R 허브 API 가이드 - .NET 클라이언트](hubs-api-guide-net-client.md)

SignalR 2의 서버 구성 요소는 .NET 4.5에서만 사용할 수 있습니다. .NET 4.0을 실행하는 서버는 SignalR v1.x를 사용해야 합니다.

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a>SignalR 미들웨어를 등록하는 방법

클라이언트가 Hub에 연결하는 데 사용할 경로를 정의하려면 `MapSignalR` 응용 프로그램이 시작될 때 메서드를 호출합니다. `MapSignalR`는 클래스의 확장 `OwinExtensions` [메서드입니다.](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) 다음 예제에서는 OWIN 시작 클래스를 사용하여 SignalR 허브 경로를 정의하는 방법을 보여 주습니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

ASP.NET MVC 응용 프로그램에 SignalR 기능을 추가하는 경우 SignalR 경로가 다른 경로보다 앞에 추가되었는지 확인합니다. 자세한 내용은 [자습서: SignalR 2 및 MVC 5로 시작하기](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)를 참조하십시오.

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a>/시그널러 URL

기본적으로 클라이언트가 허브에 연결하는 데 사용할 경로 URL은 "/signalr"입니다. (이 URL을 자동으로 생성된 JavaScript 파일에 대한 "/시그널러/허브" URL과 혼동하지 마십시오. 생성된 프록시에 대한 자세한 내용은 [SignalR 허브 API 가이드 - JavaScript 클라이언트 - 생성된 프록시 및 프록시가 수행하는 작업을](hubs-api-guide-javascript-client.md#genproxy)참조하십시오.)

이 기본 URL을 SignalR에 사용할 수 없게 만드는 특별한 상황이 있을 수 있습니다. 예를 들어 프로젝트에 *signalr라는* 폴더가 있고 이름을 변경하지 않으려고 합니다. 이 경우 다음 예제와 같이 기본 URL을 변경할 수 있습니다(샘플 코드의 "/signalr"를 원하는 URL로 바꿉니다).

**URL을 지정하는 서버 코드**

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

**URL을 지정하는 JavaScript 클라이언트 코드(생성된 프록시).**

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

**URL을 지정하는 JavaScript 클라이언트 코드(생성된 프록시 제외)**

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

**URL을 지정하는 .NET 클라이언트 코드**

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a>신호 R 옵션 구성

메서드의 오버로드를 `MapSignalR` 사용하면 사용자 지정 URL, 사용자 지정 종속성 확인자 및 다음 옵션을 지정할 수 있습니다.

- 브라우저 클라이언트에서 CORS 또는 JSONP를 사용하여 도메인 간 호출을 활성화합니다.

    일반적으로 브라우저에서 페이지를 로드하는 경우 `http://contoso.com`에서 SignalR 연결이 동일한 `http://contoso.com/signalr`도메인에 있습니다. 에서 `http://contoso.com` 페이지가 `http://fabrikam.com/signalr`에 연결하는 경우 도메인 간 연결입니다. 보안상의 이유로 도메인 간 연결은 기본적으로 비활성화됩니다. 자세한 내용은 [ASP.NET SignalR 허브 API 가이드 - JavaScript 클라이언트 - 도메인 간 연결을 설정하는 방법을](hubs-api-guide-javascript-client.md#crossdomain)참조하십시오.
- 자세한 오류 메시지를 사용하도록 설정합니다.

    오류가 발생하면 SignalR의 기본 동작은 무슨 일이 있었는지에 대한 세부 정보없이 클라이언트에게 알림 메시지를 보내는 것입니다. 악의적인 사용자가 응용 프로그램에 대한 공격에서 정보를 사용할 수 있으므로 프로덕션 환경에서는 자세한 오류 정보를 클라이언트에 보내는 것이 권장되지 않습니다. 문제 해결을 위해 이 옵션을 사용하여 보다 유용한 오류 보고를 일시적으로 활성화할 수 있습니다.
- 자동으로 생성된 자바스크립트 프록시 파일을 비활성화합니다.

    기본적으로 허브 클래스에 대한 프록시가 있는 JavaScript 파일은 URL "/signalr/hubs"에 대한 응답으로 생성됩니다. JavaScript 프록시를 사용하지 않으려거나 이 파일을 수동으로 생성하고 클라이언트의 실제 파일을 참조하려는 경우 이 옵션을 사용하여 프록시 생성을 비활성화할 수 있습니다. 자세한 내용은 [SignalR 허브 API 가이드 - JavaScript 클라이언트 - SignalR 생성 프록시에 대한 실제 파일을 만드는 방법을](hubs-api-guide-javascript-client.md#manualproxy)참조하십시오.

다음 예제에서는 `MapSignalR` 메서드를 호출할 때 SignalR 연결 URL 및 이러한 옵션을 지정 하는 방법을 보여 주입니다. 사용자 지정 URL을 지정하려면 예제의 "/signalr"를 사용하려는 URL로 바꿉습니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a>허브 클래스를 만들고 사용하는 방법

허브를 만들려면 [Microsoft.Aspnet.Signalr.Hub에서](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)파생된 클래스를 만듭니다. 다음 예제에서는 채팅 응용 프로그램에 대 한 간단한 Hub 클래스를 보여 주다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

이 예제에서는 연결된 클라이언트가 `NewContosoChatMessage` 메서드를 호출할 수 있으며, 이 경우 수신된 데이터는 연결된 모든 클라이언트에 브로드캐스트됩니다.

<a id="transience"></a>

### <a name="hub-object-lifetime"></a>허브 개체 수명

Hub 클래스를 인스턴스화하거나 서버의 사용자 고유 코드에서 메서드를 호출하지 않습니다. SignalR 허브 파이프라인을 통해 모든 작업을 수행할 수 있습니다. SignalR은 클라이언트가 서버에 연결, 연결 해제 또는 메서드 호출을 할 때와 같이 Hub 작업을 처리해야 할 때마다 Hub 클래스의 새 인스턴스를 만듭니다.

Hub 클래스의 인스턴스는 일시적이기 때문에 한 메서드 호출에서 다음 메서드 호출로 상태를 유지하는 데 사용할 수 없습니다. 서버가 클라이언트에서 메서드 호출을 받을 때마다 Hub 클래스의 새 인스턴스가 메시지를 처리합니다. 여러 연결 및 메서드 호출을 통해 상태를 유지하려면 데이터베이스 또는 Hub 클래스의 정적 변수 또는 에서 파생되지 `Hub`않는 다른 클래스와 같은 다른 메서드를 사용합니다. Hub 클래스의 정적 변수와 같은 메서드를 사용하여 메모리에 데이터를 유지하면 앱 도메인이 재활용될 때 데이터가 손실됩니다.

Hub 클래스 외부에서 실행되는 고유한 코드에서 클라이언트에 메시지를 보내려면 Hub 클래스 인스턴스를 인스턴스화하여 클라이언트에 메시지를 보낼 수 없지만 Hub 클래스에 대한 SignalR 컨텍스트 개체에 대한 참조를 얻어서 수행할 수 있습니다. 자세한 내용은 [이 항목의 후반부Hub 클래스 외부에서 클라이언트 메서드를 호출하고 그룹을 관리하는 방법을](#callfromoutsidehub) 참조하세요.

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a>자바 스크립트 클라이언트에서 허브 이름의 낙타 케이스

기본적으로 JavaScript 클라이언트는 클래스 이름의 낙타 대/소문자 버전을 사용하여 Hubs를 참조합니다. SignalR은 자바스크립트 코드가 자바스크립트 규칙을 준수할 수 있도록 자동으로 변경합니다. 이전 예제는 자바스크립트 `contosoChatHub` 코드에서 와 같이 참조될 것입니다.

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

**생성된 프록시를 사용하는 자바스크립트 클라이언트**

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

클라이언트에서 사용할 다른 이름을 지정하려면 특성을 `HubName` 추가합니다. 특성을 `HubName` 사용하면 JavaScript 클라이언트에서 camel 대/소문자에 대한 이름 변경이 없습니다.

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

**생성된 프록시를 사용하는 자바스크립트 클라이언트**

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a>다중 허브

응용 프로그램에서 여러 Hub 클래스를 정의할 수 있습니다. 이렇게 하면 연결이 공유되지만 그룹은 분리됩니다.

- 모든 클라이언트는 동일한 URL을 사용하여 서비스와 SignalR 연결을 설정합니다("/signalr" 또는 사용자 지정 URL을 지정한 경우) 해당 연결은 서비스에 의해 정의된 모든 Hubs에 사용됩니다.

    단일 클래스의 모든 Hub 기능을 정의하는 것과 비교하여 여러 Hubs의 성능 차이는 없습니다.
- 모든 허브는 동일한 HTTP 요청 정보를 가져옵니다.

    모든 허브가 동일한 연결을 공유하기 때문에 서버가 받는 유일한 HTTP 요청 정보는 SignalR 연결을 설정하는 원래 HTTP 요청에 들어오는 정보뿐입니다. 연결 요청을 사용하여 쿼리 문자열을 지정하여 클라이언트에서 서버로 정보를 전달하는 경우 다른 Hubs에 다른 쿼리 문자열을 제공할 수 없습니다. 모든 허브는 동일한 정보를 받게 됩니다.
- 생성된 JavaScript 프록시 파일에는 하나의 파일에 있는 모든 허브에 대한 프록시가 포함됩니다.

    자바 스크립트 프록시에 대한 자세한 내용은 [SignalR 허브 API 가이드 - 자바 스크립트 클라이언트 - 생성 된 프록시 및 당신을 위해 무엇을 참조하십시오](hubs-api-guide-javascript-client.md#genproxy).
- 그룹은 허브 내에서 정의됩니다.

    SignalR에서 연결된 클라이언트의 하위 집합으로 브로드캐스트할 명명된 그룹을 정의할 수 있습니다. 그룹은 각 허브에 대해 별도로 유지 관리됩니다. 예를 들어 "Administrators"라는 그룹에는 `ContosoChatHub` 클래스에 대한 하나의 클라이언트 집합이 포함되고 동일한 그룹 이름은 클래스에 대해 다른 클라이언트 집합을 참조합니다. `StockTickerHub`

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a>강력한 형식의 허브

클라이언트가 참조할 수 있는 허브 메서드에 대한 인터페이스를 정의하고 허브 메서드에서 Intellisense를 사용하도록 설정하려면 다음이 아닌 `Hub<T>` `Hub`(SignalR 2.1에 소개됨)에서 허브를 파생합니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a>클라이언트가 호출할 수 있는 Hub 클래스에서 메서드를 정의하는 방법

클라이언트에서 호출할 수 있도록 허브에 메서드를 노출하려면 다음 예제와 같이 public 메서드를 선언합니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

C# 메서드에서와 마찬가지로 복잡한 형식 및 배열을 포함하여 반환 형식 및 매개 변수를 지정할 수 있습니다. 매개 변수에서 수신하거나 호출자에게 반환하는 모든 데이터는 JSON을 사용하여 클라이언트와 서버 간에 통신되며 SignalR는 복잡한 개체와 개체 배열의 바인딩을 자동으로 처리합니다.

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a>자바 스크립트 클라이언트에서 메소드 이름의 낙타 대/소문자

기본적으로 JavaScript 클라이언트는 메서드 이름의 낙타 대/소문자 버전을 사용하여 Hub 메서드를 참조합니다. SignalR은 자바스크립트 코드가 자바스크립트 규칙을 준수할 수 있도록 자동으로 변경합니다.

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

**생성된 프록시를 사용하는 자바스크립트 클라이언트**

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

클라이언트에서 사용할 다른 이름을 지정하려면 특성을 `HubMethodName` 추가합니다.

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

**생성된 프록시를 사용하는 자바스크립트 클라이언트**

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a>비동기적으로 실행되는 경우

메서드가 장기 실행되거나 데이터베이스 조회 또는 웹 서비스 호출과 같이 대기가 포함된 작업을 수행해야 하는 경우 반환 대신 `void` [작업(반환](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 대신) 또는 [&lt;Task&gt; T](https://msdn.microsoft.com/library/dd321424.aspx) `T` 개체(반환 형식 대신)를 반환하여 Hub 메서드를 비동기로 만듭니다. 메서드에서 개체를 `Task` 반환하면 SignalR이 `Task` 완료될 때까지 기다렸다가 래핑되지 않은 결과를 클라이언트로 다시 보내므로 클라이언트에서 메서드 호출을 코딩하는 방법에 는 차이가 없습니다.

Hub 메서드를 비동기로 만들면 WebSocket 전송을 사용할 때 연결이 차단되지 않습니다. Hub 메서드가 동기적으로 실행되고 전송이 WebSocket인 경우 허브 메서드가 완료될 때까지 동일한 클라이언트에서 허브에 대한 메서드의 후속 호출이 차단됩니다.

다음 예제에서는 동기 또는 비동기적으로 실행되도록 코딩된 동일한 메서드를 보여 주며, 그 다음에는 두 버전 중 하나를 호출하는 데 적합한 JavaScript 클라이언트 코드가 표시됩니다.

**동기**

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

**비동기**

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

**생성된 프록시를 사용하는 자바스크립트 클라이언트**

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

ASP.NET 4.5에서 비동기 메서드를 사용하는 방법에 대한 자세한 내용은 [ASP.NET MVC 4에서 비동기 메서드 사용을](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)참조하십시오.

<a id="overloads"></a>

### <a name="defining-overloads"></a>오버로드 정의

메서드에 대한 오버로드를 정의하려면 각 오버로드의 매개 변수 수가 달라야 합니다. 다른 매개 변수 형식을 지정하는 것만으로 오버로드를 구별하면 Hub 클래스가 컴파일되지만 클라이언트가 오버로드 중 하나를 호출하려고 할 때 SignalR 서비스가 런타임에 예외를 throw합니다.

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a>허브 메서드 호출에서 진행률 보고

SignalR 2.1은 .NET 4.5에 도입된 [진행률 보고 패턴에](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) 대한 지원을 추가합니다. 진행률 보고를 구현하려면 `IProgress<T>` 클라이언트가 액세스할 수 있는 허브 메서드에 대한 매개 변수를 정의합니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

장기 실행 서버 메서드를 작성할 때는 허브 스레드를 차단하는 대신 Async/Await와 같은 비동기 프로그래밍 패턴을 사용하는 것이 중요합니다.

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a>Hub 클래스에서 클라이언트 메서드를 호출하는 방법

서버에서 클라이언트 메서드를 호출하려면 `Clients` Hub 클래스의 메서드에서 속성을 사용합니다. 다음 예제에서는 연결된 모든 `addNewMessageToPage` 클라이언트를 호출하는 서버 코드와 JavaScript 클라이언트에서 메서드를 정의하는 클라이언트 코드를 보여 주습니다.

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

클라이언트 메서드를 호출하는 것은 비동기 작업이며 `Task`을 반환합니다. `await`는 다음 용도로 사용합니다.

* 메시지가 오류 없이 전송되도록 합니다. 
* 시도 캐치 블록에서 오류를 catch하고 처리하도록 설정합니다.

**생성된 프록시를 사용하는 자바스크립트 클라이언트**

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

클라이언트 메서드에서 반환 값을 얻을 수 없습니다. 같은 `int x = Clients.All.add(1,1)` 구문이 작동하지 않습니다.

매개 변수에 대한 복잡한 형식과 배열을 지정할 수 있습니다. 다음 예제에서는 메서드 매개 변수에서 클라이언트에 복잡 한 형식을 전달 합니다.

**복잡한 개체를 사용하여 클라이언트 메서드를 호출하는 서버 코드**

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

**복잡한 개체를 정의하는 서버 코드**

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

**생성된 프록시를 사용하는 자바스크립트 클라이언트**

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a>RPC를 받을 클라이언트 선택

Client 속성은 RPC를 받을 클라이언트를 지정하기 위한 몇 가지 옵션을 제공하는 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) 개체를 반환합니다.

- 연결된 모든 클라이언트입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- 호출 클라이언트만.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- 호출 클라이언트를 제외한 모든 클라이언트입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- 연결 ID로 식별된 특정 클라이언트입니다.

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    이 예제는 호출 클라이언트를 호출하며 `addContosoChatMessageToPage` 을 `Clients.Caller`사용하는 것과 동일한 효과를 가짐을 가짐을 가시고 있습니다.
- 연결 ID로 식별된 지정된 클라이언트를 제외한 연결된 모든 클라이언트입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- 지정된 그룹의 연결된 모든 클라이언트입니다.

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- 연결 ID로 식별된 지정된 클라이언트를 제외한 지정된 그룹의 모든 연결된 클라이언트입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- 호출 클라이언트를 제외한 지정된 그룹의 연결된 모든 클라이언트입니다.

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- userId로 식별된 특정 사용자입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    기본적으로 이것은 `IPrincipal.Identity.Name`에서이지만 [IUserIdProvider의 구현을 전역 호스트에 등록하여](mapping-users-to-connections.md#IUserIdProvider)변경할 수 있습니다.
- 연결 아이디 목록의 모든 클라이언트 및 그룹입니다.

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- 그룹 목록입니다.

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- 이름으로 사용자입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- 사용자 이름 목록(SignalR 2.1에 소개).

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a>메서드 이름에 대한 컴파일 타임 유효성 검사가 없습니다.

지정한 메서드 이름은 동적 개체로 해석되므로 IntelliSense 또는 컴파일 타임 유효성 검사가 없습니다. 식은 런타임에 평가됩니다. 메서드 호출이 실행되면 SignalR은 메서드 이름과 매개 변수 값을 클라이언트에 보내고 클라이언트에 이름과 일치하는 메서드가 있는 경우 해당 메서드가 호출되고 매개 변수 값이 전달됩니다. 클라이언트에서 일치하는 메서드를 찾을 수 없는 경우 오류가 발생하지 않습니다. SignalR이 클라이언트 메서드를 호출할 때 장면 뒤에서 클라이언트에게 전송하는 데이터의 형식에 대한 자세한 내용은 [SignalR 소개를](../getting-started/introduction-to-signalr.md)참조하십시오.

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a>대/소문자 구분 메서드 이름 일치

메서드 이름 일치는 대/소문자를 구분하지 않습니다. 예를 들어 `Clients.All.addContosoChatMessageToPage` 서버에서 를 `AddContosoChatMessageToPage` `addcontosochatmessagetopage`실행하거나 `addContosoChatMessageToPage` 클라이언트에서 실행합니다.

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a>비동기 실행

호출하는 메서드가 비동기적으로 실행됩니다. 후속 코드 줄이 메서드 완료를 기다려야 한다고 지정하지 않는 한 SignalR이 클라이언트에 데이터 전송을 완료할 때까지 기다리지 않고 클라이언트에 대한 메서드 호출 후에 발생하는 모든 코드는 즉시 실행됩니다. 다음 코드 예제에서는 두 클라이언트 메서드를 순차적으로 실행하는 방법을 보여 주십니다.

**대기 중 사용(.NET 4.5)**

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

다음 코드 `await` 줄이 실행되기 전에 클라이언트 메서드가 끝날 때까지 기다리는 데 사용하는 경우 다음 코드 줄이 실행되기 전에 클라이언트가 실제로 메시지를 수신한다는 의미는 아닙니다. 클라이언트 메서드 호출의 "완료"는 SignalR이 메시지를 보내는 데 필요한 모든 작업을 수행했음을 의미합니다. 클라이언트가 메시지를 받았는지 확인해야 하는 경우 해당 메커니즘을 직접 프로그래밍해야 합니다. 예를 들어 Hub에서 `MessageReceived` 메서드를 코딩할 수 `addContosoChatMessageToPage` 있으며 클라이언트의 메서드에서 `MessageReceived` 클라이언트에서 수행해야 하는 작업을 수행한 후 호출할 수 있습니다. Hub에서 `MessageReceived` 실제 클라이언트 수신 및 원래 메서드 호출 처리에 따라 모든 작업을 수행할 수 있습니다.

### <a name="how-to-use-a-string-variable-as-the-method-name"></a>문자열 변수를 메서드 이름으로 사용하는 방법

문자열 변수를 메서드 `Clients.All` 이름으로 `Clients.Others` `Clients.Caller`사용하여 클라이언트 메서드를 호출하려면 `IClientProxy` [Invoke(메서드Name, args...)를](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)호출합니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a>허브 클래스에서 그룹 구성원을 관리하는 방법

SignalR의 그룹은 연결된 클라이언트의 지정된 하위 집합에 메시지를 브로드캐스트하는 방법을 제공합니다. 그룹에는 원하는 수의 클라이언트가 있을 수 있으며 클라이언트는 원하는 수의 그룹의 구성원이 될 수 있습니다.

그룹 구성원 자격을 관리하려면 [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) Hub 클래스의 `Groups` 속성에서 제공하는 [추가](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) 및 제거 메서드를 사용합니다. 다음 예제에서는 `Groups.Add` 클라이언트 `Groups.Remove` 코드에서 호출되는 Hub 메서드와 이를 호출하는 JavaScript 클라이언트 코드를 보여 주는 메서드를 보여 주며, 그 다음에는 클라이언트 코드를 호출합니다.

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

**생성된 프록시를 사용하는 자바스크립트 클라이언트**

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

명시적으로 그룹을 만들 필요가 없습니다. 실제로 그룹은 `Groups.Add`에 대한 호출에서 이름을 처음 지정할 때 자동으로 만들어지며, 마지막 연결을 멤버 자격에서 제거하면 삭제됩니다.

그룹 구성원 목록 또는 그룹 목록을 가져오는 API가 없습니다. [SignalR은 pub/sub 모델을](http://en.wikipedia.org/wiki/Publish/subscribe)기반으로 클라이언트 및 그룹에 메시지를 보내고 서버는 그룹 또는 그룹 구성원 의 목록을 유지 관리하지 않습니다. 이렇게 하면 웹 팜에 노드를 추가할 때마다 SignalR이 유지 관리하는 모든 상태를 새 노드로 전파해야 하므로 확장성을 최대화할 수 있습니다.

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a>메서드 추가 및 제거의 비동기 실행

및 `Groups.Add` `Groups.Remove` 메서드는 비동기적으로 실행됩니다. 그룹에 클라이언트를 추가하고 그룹을 사용하여 클라이언트에 즉시 메시지를 보내려면 메서드가 `Groups.Add` 먼저 끝나는지 확인해야 합니다. 다음 코드 예제에서는 이 작업을 수행하는 방법을 보여 주며 있습니다.

**그룹에 클라이언트를 추가한 다음 해당 클라이언트에 메시지를 전달합니다.**

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a>그룹 구성원 유지

SignalR은 사용자가 아닌 연결을 추적하므로 사용자가 연결을 설정할 때마다 사용자가 동일한 그룹에 있도록 하려면 사용자가 `Groups.Add` 새 연결을 설정할 때마다 호출해야 합니다.

일시적으로 연결이 끊어진 후 SignalR이 자동으로 연결을 복원할 수 있습니다. 이 경우 SignalR은 동일한 연결을 복원하고 새 연결을 설정하지 않으므로 클라이언트의 그룹 구성원이 자동으로 복원됩니다. 이는 그룹 구성원을 포함한 각 클라이언트의 연결 상태가 클라이언트에 반올림되기 때문에 일시적인 중단이 서버 재부팅 또는 실패의 결과인 경우에도 가능합니다. 연결이 종료되기 전에 서버가 다운되어 새 서버로 대체되면 클라이언트는 새 서버에 자동으로 다시 연결하고 구성원이 되는 그룹에 다시 등록할 수 있습니다.

연결이 끊긴 후 연결을 자동으로 복원할 수 없거나 연결이 시간 만점이거나 클라이언트가 연결이 끊어질 때(예: 브라우저가 새 페이지로 이동하는 경우) 그룹 구성원 자격이 손실됩니다. 다음에 사용자가 연결하면 새 연결이 됩니다. 동일한 사용자가 새 연결을 설정할 때 그룹 구성원 자격을 유지하려면 응용 프로그램에서 사용자와 그룹 간의 연결을 추적하고 사용자가 새 연결을 설정할 때마다 그룹 구성원 자격을 복원해야 합니다.

연결 및 다시 연결에 대한 자세한 내용은 이 항목의 후반부 [Hub 클래스에서 연결 수명 이벤트를 처리하는 방법을](#connectionlifetime) 참조하세요.

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a>단일 사용자 그룹

SignalR을 사용하는 응용 프로그램은 일반적으로 메시지를 보낸 사용자와 메시지를 수신해야 하는 사용자를 알기 위해 사용자와 연결 간의 연결을 추적해야 합니다. 그룹은 이를 위해 일반적으로 사용되는 두 패턴 중 하나에 사용됩니다.

- 단일 사용자 그룹입니다.

    사용자 이름을 그룹 이름으로 지정하고 사용자가 연결하거나 다시 연결할 때마다 그룹에 현재 연결 ID를 추가할 수 있습니다. 그룹에 보내는 사용자에게 메시지를 보냅니다. 이 방법의 단점은 그룹이 사용자가 온라인 또는 오프라인인지 확인할 수 있는 방법을 제공하지 않는다는 것입니다.
- 사용자 이름과 연결 ID 간의 연결을 추적합니다.

    각 사용자 이름과 하나 이상의 연결 아이디 간의 연결을 사전 또는 데이터베이스에 저장하고 사용자가 연결하거나 연결을 끊을 때마다 저장된 데이터를 업데이트할 수 있습니다. 사용자에게 메시지를 보내려면 연결 아이디를 지정합니다. 이 방법의 단점은 더 많은 메모리가 필요하다는 것입니다.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a>Hub 클래스에서 연결 수명 이벤트를 처리하는 방법

연결 수명 이벤트를 처리하는 일반적인 이유는 사용자가 연결되어 있는지 여부를 추적하고 사용자 이름과 연결 ID 간의 연결을 추적하기 위해서입니다. 클라이언트가 연결하거나 연결을 끊을 때 고유한 `OnConnected` `OnDisconnected`코드를 `OnReconnected` 실행하려면 다음 예제와 같이 Hub 클래스의 및 가상 메서드를 재정의합니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a>연결 됨, 연결이 끊긴 및 다시 연결해제된 경우

브라우저가 새 페이지로 이동할 때마다 새 연결이 설정되어야 하며, 이는 SignalR이 메서드 `OnConnected` 다음에 메서드를 `OnDisconnected` 실행한다는 것을 의미합니다. SignalR은 새 연결이 설정되면 항상 새 연결 ID를 만듭니다.

이 `OnReconnected` 메서드는 케이블이 일시적으로 연결이 끊어지고 연결이 중단되기 전에 다시 연결되는 경우와 같이 SignalR에서 자동으로 복구할 수 있는 연결 끊김이 있는 경우 호출됩니다. 이 `OnDisconnected` 메서드는 클라이언트연결이 끊어졌을 때 호출되며 브라우저가 새 페이지로 이동하는 경우와 같이 SignalR가 자동으로 다시 연결할 수 없습니다. 따라서 지정된 클라이언트에 대한 가능한 이벤트 `OnConnected` `OnReconnected`시퀀스는 은 `OnDisconnected`. 또는 `OnConnected` `OnDisconnected`. 지정된 연결에 `OnConnected` `OnDisconnected` `OnReconnected` 대한 시퀀스가 표시되지 않습니다.

서버가 `OnDisconnected` 다운되거나 앱 도메인이 재활용되는 경우와 같은 일부 시나리오에서는 메서드가 호출되지 않습니다. 다른 서버가 온라인상태이거나 App Domain이 재활용을 완료하면 일부 클라이언트가 다시 `OnReconnected` 연결하여 이벤트를 발생시킬 수 있습니다.

자세한 내용은 [SignalR의 연결 수명 이벤트 이해 및 처리를](handling-connection-lifetime-events.md)참조하십시오.

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a>호출자 상태가 채워지지 않음

연결 수명 이벤트 처리기 메서드는 서버에서 호출되므로 클라이언트에 `state` 개체에 넣은 상태는 서버의 `Caller` 속성에 채워지지 않습니다. 개체 및 `Caller` 속성에 대한 자세한 내용은 이 항목의 후반부에서 [클라이언트와 Hub 클래스 간에 상태를 전달하는 방법을](#passstate) 참조하세요. `state`

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a>Context 속성에서 클라이언트에 대 한 정보를 얻는 방법

클라이언트에 대한 정보를 얻으려면 `Context` Hub 클래스의 속성을 사용합니다. 속성은 `Context` 다음 정보에 대한 액세스를 제공하는 [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) 개체를 반환합니다.

- 호출 클라이언트의 연결 ID입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    연결 ID는 SignalR에서 할당하는 GUID입니다(사용자 고유의 코드에서 값을 지정할 수 없습니다). 각 연결에 대해 하나의 연결 ID가 있으며 응용 프로그램에 여러 Hub가 있는 경우 모든 Hubs에서 동일한 연결 ID가 사용됩니다.
- HTTP 헤더 데이터.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    에서 HTTP 헤더를 얻을 `Context.Headers`수도 있습니다. 동일한 것에 대한 여러 참조의 `Context.Headers` 이유는 먼저 만들어졌고 나중에 속성이 `Context.Headers` `Context.Request` 추가되었으며 이전 버전과의 호환성을 위해 유지되었기 때문입니다.
- 문자열 데이터를 쿼리합니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    `Context.QueryString`에서 쿼리 문자열 데이터를 얻을 수도 있습니다.

    이 속성에서 얻는 쿼리 문자열은 SignalR 연결을 설정한 HTTP 요청과 함께 사용된 문자열입니다. 클라이언트에서 서버로 클라이언트에 대한 데이터를 전달하는 편리한 방법입니다 연결을 구성하여 클라이언트에 쿼리 문자열 매개 변수를 추가할 수 있습니다. 다음 예제에서는 생성된 프록시를 사용할 때 JavaScript 클라이언트에 쿼리 문자열을 추가하는 한 가지 방법을 보여 주며 있습니다.

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    쿼리 문자열 매개 변수 설정에 대한 자세한 내용은 [JavaScript](hubs-api-guide-javascript-client.md) 및 [.NET](hubs-api-guide-net-client.md) 클라이언트에 대한 API 가이드를 참조하세요.

    SignalR에서 내부적으로 사용되는 다른 값과 함께 쿼리 문자열 데이터에서 연결에 사용되는 전송 방법을 찾을 수 있습니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    값은 `transportMethod` "웹 소켓", "서버SentEvents", "영원히프레임" 또는 "longPolling"입니다. `OnConnected` 이벤트 처리기 메서드에서 이 값을 확인 하면 일부 시나리오에서 처음에 연결에 대 한 최종 협상 된 전송 메서드가 아닌 전송 값을 얻을 수 있습니다. 이 경우 메서드는 예외를 throw 하 고 최종 전송 메서드가 설정 될 때 나중에 다시 호출 됩니다.
- 쿠키.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    에서 `Context.RequestCookies`쿠키를 얻을 수도 있습니다.
- 사용자 정보입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- 요청에 대한 HttpContext 개체 :

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    SignalR `HttpContext.Current` 연결에 대한 `HttpContext` 개체를 가져오는 대신 이 메서드를 사용합니다.

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a>클라이언트와 Hub 클래스 간에 상태를 전달하는 방법

클라이언트 프록시는 `state` 각 메서드 호출을 사용하여 서버에 전송할 데이터를 저장할 수 있는 개체를 제공합니다. 서버에서 클라이언트에서 호출되는 Hub `Clients.Caller` 메서드의 속성에서 이 데이터에 액세스할 수 있습니다. 속성은 `Clients.Caller` 연결 수명 이벤트 처리기 `OnConnected`메서드 `OnDisconnected`및 `OnReconnected`에 대해 채워지지 않습니다.

개체및속성에서 `state` 데이터를 만들거나 `Clients.Caller` 업데이트하는 것은 양방향으로 작동합니다. 서버에서 값을 업데이트할 수 있으며 클라이언트에 다시 전달됩니다.

다음 예제에서는 모든 메서드 호출을 사용 하 고 서버에 전송하기 위한 상태를 저장하는 JavaScript 클라이언트 코드를 보여 주며 있습니다.

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

다음 예제에서는 .NET 클라이언트에서 해당 코드를 보여 주며 있습니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

Hub 클래스에서 `Clients.Caller` 속성에서 이 데이터에 액세스할 수 있습니다. 다음 예제에서는 이전 예제에서 참조한 상태를 검색하는 코드를 보여 주며 있습니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> `state` 상태를 유지하기 위한 이 메커니즘은 또는 `Clients.Caller` 속성에 넣는 모든 것이 모든 메서드 호출과 함께 반올림되므로 많은 양의 데이터를 위한 것이 아닙니다. 사용자 이름이나 카운터와 같은 작은 항목에 유용합니다.

VB.NET 또는 강력한 형식의 허브에서는 호출자 상태 개체를 통해 `Clients.Caller`액세스할 수 없습니다. 대신, `Clients.CallerState` 사용 (SignalR 2.1에 도입):

**C에서 CallerState 사용 #**

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

**시각적 기본에서 CallerState 사용**

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a>Hub 클래스에서 오류를 처리하는 방법

Hub 클래스 메서드에서 발생하는 오류를 처리하려면 먼저 을 사용하여 `await`비동기 작업(예: 클라이언트 메서드 호출)의 예외를 "관찰"해야 합니다. 그런 다음 다음 방법 중 하나 이상을 사용합니다.

- try-catch 블록에서 메서드 코드를 래핑하고 예외 개체를 기록합니다. 디버깅을 위해 클라이언트에 예외를 보낼 수 있지만 보안상의 이유로 프로덕션 환경에서 클라이언트에 자세한 정보를 보내는 것은 권장되지 않습니다.
- [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) 메서드를 처리하는 허브 파이프라인 모듈을 만듭니다. 다음 예제에서는 오류를 기록하는 파이프라인 모듈과 허브 파이프라인에 모듈을 삽입하는 Startup.cs 코드를 보여 주십니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- 클래스를 `HubException` 사용합니다(SignalR 2에 도입). 이 오류는 모든 허브 호출에서 throw될 수 있습니다. `HubError` 생성자는 문자열 메시지와 추가 오류 데이터를 저장하기 위한 개체를 사용합니다. SignalR은 예외를 자동으로 직렬화하고 클라이언트로 보내며 허브 메서드 호출을 거부하거나 실패하는 데 사용됩니다.

    다음 코드 샘플에서는 허브 호출 `HubException` 중에 를 throw하는 방법과 JavaScript 및 .NET 클라이언트에서 예외를 처리하는 방법을 보여 줍니다.

    **HubException 클래스를 보여 주는 서버 코드**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    **허브에 HubException을 throw에 대한 응답을 보여주는 JavaScript 클라이언트 코드**

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    **허브에서 HubException을 throw에 대한 응답을 보여 주는 .NET 클라이언트 코드**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

허브 파이프라인 모듈에 대한 자세한 내용은 이 항목의 후반부에서 [허브 파이프라인을 사용자 지정하는 방법을](#hubpipeline) 참조하세요.

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a>추적을 활성화하는 방법

서버 측 추적을 사용하려면 이 예제와 같이 Web.config 파일에 system.diagnostics 요소를 추가합니다.

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

Visual Studio에서 응용 프로그램을 실행하면 **출력** 창에서 로그를 볼 수 있습니다.

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a>클라이언트 메서드를 호출하고 Hub 클래스 외부에서 그룹을 관리하는 방법

Hub 클래스가 아닌 다른 클래스에서 클라이언트 메서드를 호출하려면 Hub에 대한 SignalR 컨텍스트 개체에 대한 참조를 얻고 클라이언트에서 메서드를 호출하거나 그룹을 관리하는 데 사용합니다.

다음 샘플 `StockTicker` 클래스는 컨텍스트 개체를 가져옵니다. `updateStockPrice` `StockTickerHub`

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

수명이 긴 개체에서 컨텍스트를 여러 번 사용해야 하는 경우 매번 다시 가져오는 대신 참조를 한 번 받고 저장합니다. 컨텍스트를 한 번 받으면 SignalR이 Hub 메서드가 클라이언트 메서드를 호출하는 순서와 동일한 순서로 클라이언트에 메시지를 보냅니다. 허브에 대한 SignalR 컨텍스트를 사용하는 방법을 보여 주는 자습서의 경우 [ASP.NET SignalR을 사용하여 서버 브로드캐스트를](../getting-started/tutorial-server-broadcast-with-signalr.md)참조하십시오.

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a>클라이언트 메서드 호출

RPC를 받을 클라이언트를 지정할 수 있지만 Hub 클래스에서 호출할 때보다 옵션이 적습니다. 그 이유는 컨텍스트가 클라이언트의 특정 호출과 연결되지 않으므로 현재 연결 ID(예: `Clients.Others`또는 `Clients.Caller` `Clients.OthersInGroup`및)에 대한 지식이 필요한 메서드는 사용할 수 없습니다. 다음 옵션을 사용할 수 있습니다.

- 연결된 모든 클라이언트입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- 연결 ID로 식별된 특정 클라이언트입니다.

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- 연결 ID로 식별된 지정된 클라이언트를 제외한 연결된 모든 클라이언트입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- 지정된 그룹의 연결된 모든 클라이언트입니다.

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- 연결 ID로 식별된 지정된 클라이언트를 제외한 지정된 그룹의 모든 연결된 클라이언트입니다.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

Hub 클래스의 메서드에서 비 Hub 클래스로 호출하는 경우 현재 연결 ID를 전달하고 `Clients.Client`에서 `Clients.AllExcept`를 `Clients.Group` 사용하거나 `Clients.Others`을 `Clients.OthersInGroup`시뮬레이션할 `Clients.Caller`수 있습니다. 다음 예제에서 `MoveShapeHub` 클래스는 클래스를 시뮬레이션할 `Broadcaster` `Broadcaster` `Clients.Others`수 있도록 연결 ID를 클래스에 전달합니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a>그룹 구성원 관리

그룹 관리의 경우 Hub 클래스와 동일한 옵션이 있습니다.

- 그룹에 클라이언트 추가

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- 그룹에서 클라이언트 제거

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a>허브 파이프라인을 사용자 지정하는 방법

SignalR을 사용하면 허브 파이프라인에 사용자 고유의 코드를 삽입할 수 있습니다. 다음 예제에서는 클라이언트에서 수신된 각 들어오는 메서드 호출및 클라이언트에서 호출된 발신 메서드 호출을 기록하는 사용자 지정 Hub 파이프라인 모듈을 보여 주며, 이 모듈은 다음과 같은 것입니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

*Startup.cs* 파일의 다음 코드는 Hub 파이프라인에서 실행할 모듈을 등록합니다.

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

재정의할 수 있는 여러 가지 방법이 있습니다. 전체 목록은 [Hub파이프라인모듈 메서드](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)를 참조하십시오.
