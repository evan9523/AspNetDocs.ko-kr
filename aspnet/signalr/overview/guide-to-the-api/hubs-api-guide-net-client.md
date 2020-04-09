---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET 시그널R 허브 API 가이드 - .NET 클라이언트(C#) | 마이크로 소프트 문서
author: bradygaster
description: 이 문서에서는 Windows 스토어(WinRT), WPF, 실버라이트 및 단점과 같은 .NET 클라이언트에서 SignalR 버전 2에 대한 허브 API를 사용하는 방법을 소개합니다.
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675930"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a>ASP.NET 시그널R 허브 API 가이드 - .NET 클라이언트(C#)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 Windows 스토어(WinRT), WPF, Silverlight 및 콘솔 응용 프로그램과 같은 .NET 클라이언트에서 SignalR 버전 2에 대한 허브 API를 사용하는 방법을 소개합니다.
>
> SignalR Hubs API를 사용하면 서버에서 연결된 클라이언트로, 클라이언트에서 서버로 원격 프로시저 호출(RPC)을 수행할 수 있습니다. 서버 코드에서 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다. 클라이언트 코드에서는 서버에서 호출할 수 있는 메서드를 정의하고 서버에서 실행되는 메서드를 호출합니다. SignalR은 모든 클라이언트-서버 배관을 처리합니다.
>
> SignalR는 또한 영구 연결이라는 하위 수준 API를 제공합니다. SignalR, 허브 및 영구 연결에 대한 소개 또는 전체 SignalR 응용 프로그램을 빌드하는 방법을 보여 주는 자습서의 경우 [SignalR - 시작](../getting-started/index.md)을 참조하십시오.
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

- [클라이언트 설정](#clientsetup)
- [연결을 설정하는 방법](#establishconnection)

    - [Silverlight 클라이언트의 교차 도메인 연결](#slcrossdomain)
- [연결을 구성하는 방법](#configureconnection)

    - [WPF 클라이언트에서 최대 동시 연결 수를 설정하는 방법](#maxconnections)
    - [쿼리 문자열 매개 변수를 지정하는 방법](#querystring)
    - [전송 방법을 지정하는 방법](#transport)
    - [HTTP 헤더를 지정하는 방법](#httpheaders)
    - [클라이언트 인증서를 지정하는 방법](#clientcertificate)
- [허브 프록시를 만드는 방법](#proxy)
- [서버가 호출할 수 있는 메서드를 클라이언트에서 정의하는 방법](#callclient)

    - [매개 변수가 없는 메서드](#clientmethodswithoutparms)
    - [매개 변수가 있는 방법, 매개 변수 형식 지정](#clientmethodswithparmtypes)
    - [매개 변수가 있는 메서드, 매개 변수에 대한 동적 개체 지정](#clientmethodswithdynamparms)
    - [처리기를 제거하는 방법](#removehandler)
- [클라이언트에서 서버 메서드를 호출하는 방법](#callserver)
- [연결 수명 이벤트를 처리하는 방법](#connectionlifetime)
- [오류 처리 방법](#handleerrors)
- [클라이언트 측 로깅을 활성화하는 방법](#logging)
- [서버가 호출할 수 있는 클라이언트 메서드에 대한 WPF, Silverlight 및 콘솔 응용 프로그램 코드 샘플](#wpfsl)

샘플 .NET 클라이언트 프로젝트의 경우 다음 리소스를 참조하십시오.

- GitHub.com (WinRT, 실버 라이트, 콘솔 응용 프로그램 예)에 [구스타보 - 아르멘타 / 신호 - 샘플.](https://github.com/gustavo-armenta/SignalR-Samples)
- [다미안 에드워즈 / 시그널R-무브 셰이프 데모 /](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) GitHub.com 이동 셰이프.데스크톱 (WPF 예).
- [시그널R / 마이크로 소프트.AspNet.SignalR.Client.GitHub.com 샘플](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) (콘솔 응용 프로그램 예).

서버 또는 JavaScript 클라이언트를 프로그래밍하는 방법에 대한 설명서는 다음 리소스를 참조하십시오.

- [시그널R 허브 API 가이드 - 서버](hubs-api-guide-server.md)
- [시그널R 허브 API 가이드 - 자바 스크립트 클라이언트](hubs-api-guide-javascript-client.md)

API 참조 항목에 대한 링크는 .NET 4.5 버전의 API에 대한 것입니다. .NET 4를 사용하는 경우 [.NET 4 버전의 API 항목을](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)참조하십시오.

<a id="clientsetup"></a>

## <a name="client-setup"></a>클라이언트 설치

[Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet 패키지를 [설치합니다(Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) 패키지가 아님). 이 패키지는 .NET 4 및 .NET 4.5 모두에 대해 WinRT, 실버라이트, WPF, 콘솔 응용 프로그램 및 Windows Phone 클라이언트를 지원합니다.

클라이언트에 있는 SignalR 버전이 서버에 있는 버전과 다른 경우 SignalR은 종종 차이에 적응할 수 있습니다. 예를 들어 SignalR 버전 2를 실행하는 서버는 1.1.x가 설치된 클라이언트와 버전 2가 설치된 클라이언트를 지원합니다. 서버의 버전과 클라이언트의 버전 간의 차이가 너무 크거나 클라이언트가 서버보다 최신 버전인 경우 SignalR은 클라이언트가 연결을 설정하려고 할 때 `InvalidOperationException` 예외를 throw합니다. 오류 메시지는 "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`입니다.

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>연결을 설정하는 방법

연결을 설정하려면 전에 개체를 `HubConnection` 만들고 프록시를 만들어야 합니다. 연결을 설정하려면 개체에서 `Start` 메서드를 `HubConnection` 호출합니다.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> JavaScript 클라이언트의 경우 연결을 설정하는 메서드를 `Start` 호출하기 전에 하나 이상의 이벤트 처리기를 등록해야 합니다. .NET 클라이언트에는 이 가 필요하지 않습니다. JavaScript 클라이언트의 경우 생성된 프록시 코드는 서버에 있는 모든 허브에 대한 프록시를 자동으로 생성하며 처리기를 등록하면 클라이언트가 사용할 허브를 지정하는 방법입니다. 그러나 .NET 클라이언트의 경우 허브 프록시를 수동으로 만들수 있으므로 SignalR은 프록시를 만드는 모든 허브를 사용한다고 가정합니다.

샘플 코드는 기본 "/signalr" URL을 사용하여 SignalR 서비스에 연결합니다. 다른 기본 URL을 지정하는 방법에 대한 자세한 내용은 [ASP.NET SignalR 허브 API 가이드 - 서버 - /signalr URL을](hubs-api-guide-server.md#signalrurl)참조하십시오.

메서드는 `Start` 비동기적으로 실행됩니다. 연결이 설정될 때까지 후속 코드 줄이 실행되지 않도록 하려면 `await` ASP.NET 4.5 비동기 메서드 `.Wait()` 또는 동기 메서드에서 사용합니다. WinRT 클라이언트에서는 사용하지 `.Wait()` 마십시오.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a>Silverlight 클라이언트의 교차 도메인 연결

Silverlight 클라이언트에서 도메인 간 연결을 사용하도록 설정하는 방법에 대한 자세한 내용은 [도메인 경계를 넘어 서비스를 사용할 수 있도록 설정합니다.](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>연결을 구성하는 방법

연결을 설정하기 전에 다음 옵션 중 을 지정할 수 있습니다.

- 동시 연결 제한.
- 문자열 매개 변수를 쿼리합니다.
- 전송 방법입니다.
- HTTP 헤더.
- 클라이언트 인증서입니다.

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a>WPF 클라이언트에서 최대 동시 연결 수를 설정하는 방법

WPF 클라이언트에서 기본값 2에서 최대 동시 연결 수를 늘려야 할 수 있습니다. 권장 값은 10입니다.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

자세한 내용은 [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)을 참조하십시오.

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>쿼리 문자열 매개 변수를 지정하는 방법

클라이언트가 연결할 때 서버에 데이터를 보내려면 연결 개체에 쿼리 문자열 매개 변수를 추가할 수 있습니다. 다음 예제에서는 클라이언트 코드에서 쿼리 문자열 매개 변수를 설정하는 방법을 보여 주며 있습니다.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

다음 예제에서는 서버 코드에서 쿼리 문자열 매개 변수를 읽는 방법을 보여 주입니다.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>전송 방법을 지정하는 방법

연결하는 프로세스의 일부로 SignalR 클라이언트는 일반적으로 서버와 협상하여 서버와 클라이언트 모두에서 지원되는 최상의 전송을 결정합니다. 사용하려는 전송을 이미 알고 있는 경우 이 협상 프로세스를 우회할 수 있습니다. 전송 메서드를 지정하려면 전송 개체를 Start 메서드로 전달합니다. 다음 예제에서는 클라이언트 코드에서 전송 메서드를 지정 하는 방법을 보여 주입니다.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

[Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) 네임스페이스에는 전송을 지정하는 데 사용할 수 있는 다음 클래스가 포함됩니다.

- [롱폴링교통](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [서버센트이벤트전송](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- [WebSocketTransport(서버와](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) 클라이언트 가 모두 .NET 4.5를 사용하는 경우에만 사용 가능)
- [자동](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) 전송(클라이언트와 서버 모두에서 지원되는 최상의 전송을 자동으로 선택합니다. 기본 전송입니다. 메서드에 `Start` 이 것을 전달하는 것은 아무 것도 전달하지 않는 것과 동일한 효과가 있습니다.)

ForeverFrame 전송은 브라우저에서만 사용되므로 이 목록에 포함되지 않습니다.

서버 코드에서 전송 방법을 확인하는 방법에 대한 자세한 내용은 [ASP.NET SignalR Hubs API 가이드 - 서버 - Context 속성에서 클라이언트에 대한 정보를 얻는 방법을](hubs-api-guide-server.md#contextproperty)참조하십시오. 전송 및 대체에 대한 자세한 내용은 [SignalR - 전송 및 대체 소개를](../getting-started/introduction-to-signalr.md#transports)참조하십시오.

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a>HTTP 헤더를 지정하는 방법

HTTP 헤더를 설정하려면 `Headers` 연결 개체에서 속성을 사용합니다. 다음 예제에서는 HTTP 헤더를 추가하는 방법을 보여 주며 있습니다.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a>클라이언트 인증서를 지정하는 방법

클라이언트 인증서를 추가하려면 `AddClientCertificate` 연결 개체에서 메서드를 사용합니다.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a>허브 프록시를 만드는 방법

Hub가 서버에서 호출할 수 있는 메서드를 정의하고 서버의 Hub에서 메서드를 호출하기 위해 연결 개체를 `CreateHubProxy` 호출하여 Hub에 대한 프록시를 만듭니다. 전달하는 `CreateHubProxy` 문자열은 Hub 클래스의 이름 또는 서버에서 사용된 경우 `HubName` 특성에 의해 지정된 이름입니다. 이름 일치 시 대/소문자는 구분하지 않습니다.

**서버의 허브 클래스**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**허브 클래스에 대한 클라이언트 프록시 만들기**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

Hub 클래스를 특성으로 `HubName` 장식하는 경우 해당 이름을 사용합니다.

**서버의 허브 클래스**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

**허브 클래스에 대한 클라이언트 프록시 만들기**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

동일한 `HubConnection.CreateHubProxy` `hubName`을 여러 번 호출하는 경우 동일한 `IHubProxy` 캐시된 개체를 가져옵니다.

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>서버가 호출할 수 있는 메서드를 클라이언트에서 정의하는 방법

서버가 호출할 수 있는 메서드를 정의하려면 `On` 프록시메서드를 사용하여 이벤트 처리기를 등록합니다.

메서드 이름 일치는 대/소문자를 구분하지 않습니다. 예를 들어 `Clients.All.UpdateStockPrice` 서버에서 를 `updateStockPrice` `updatestockprice`실행하거나 `UpdateStockPrice` 클라이언트에서 실행합니다.

클라이언트 플랫폼에 따라 UI를 업데이트하기 위해 메서드 코드를 작성하는 방법에 대한 요구 사항이 다릅니다. 표시된 예는 WinRT(Windows 스토어 .NET) 클라이언트에 대한 예입니다. WPF, Silverlight 및 콘솔 응용 프로그램 예제는 [이 항목의 후반부에 별도의 섹션에](#wpfsl)제공됩니다.

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a>매개 변수가 없는 메서드

처리하는 메서드에 매개 변수가 없는 경우 메서드의 비제네릭 `On` 오버로드를 사용합니다.

**매개 변수없이 클라이언트 메서드를 호출하는 서버 코드**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**매개 변수가 없는 서버에서 호출된 메서드에 대한 WinRT 클라이언트[코드(이 항목의 후반부 WPF 및 Silverlight 예제 참조)](#wpfsl)**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>매개 변수가 있는 메서드, 매개 변수 형식 지정

처리하는 메서드에 매개 변수가 있는 경우 매개 변수 형식을 `On` 메서드의 제네릭 유형으로 지정합니다. 최대 8개의 매개 `On` 변수를 지정할 수 있도록 하는 메서드의 일반 오버로드가 있습니다(Windows Phone 7의 경우 4개). 다음 예제에서는 하나의 매개 변수가 `UpdateStockPrice` 메서드로 전송됩니다.

**매개 변수를 사용하여 클라이언트 메서드를 호출하는 서버 코드**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**매개 변수에 사용되는 Stock 클래스**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

**매개 변수가 있는 서버에서 호출된 메서드에 대한 WinRT 클라이언트[코드(이 항목의 후반부 WPF 및 Silverlight 예제 참조)](#wpfsl)**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>매개 변수가 있는 메서드, 매개 변수에 대한 동적 개체 지정

`On` 매개 변수를 메서드의 제네릭 유형으로 지정하는 대신 매개 변수를 동적 개체로 지정할 수 있습니다.

**매개 변수를 사용하여 클라이언트 메서드를 호출하는 서버 코드**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**매개 변수에 사용되는 Stock 클래스**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

**매개 변수에 대 한 동적 개체를 사용 하 여 매개 변수가 있는 서버에서 호출 하는 메서드에 대 한 WinRT 클라이언트 코드[(이 항목의 후반부 WPF 및 Silverlight 예제 참조)](#wpfsl)**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a>처리기를 제거하는 방법

처리기를 제거하려면 해당 `Dispose` 메서드를 호출합니다.

**서버에서 호출된 메서드에 대한 클라이언트 코드**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**처리기를 제거하는 클라이언트 코드**

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>클라이언트에서 서버 메서드를 호출하는 방법

서버에서 메서드를 호출하려면 Hub `Invoke` 프록시에서 메서드를 사용합니다.

서버 메서드에 반환 값이 없는 경우 메서드의 비제네릭 오버로드를 `Invoke` 사용합니다.

**반환 값이 없는 메서드의 서버 코드**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**반환 값이 없는 메서드를 호출 하는 클라이언트 코드**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

서버 메서드에 반환 값이 있는 경우 반환 형식을 `Invoke` 메서드의 제네릭 유형으로 지정합니다.

**반환 값이 있고 복잡한 형식 매개 변수를 사용하는 메서드의 서버 코드**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**매개 변수 및 반환 값에 사용되는 Stock 클래스**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

**반환 값이 있고 ASP.NET 4.5 비동기 메서드에서 복잡한 형식 매개 변수를 사용하는 메서드를 호출하는 클라이언트 코드**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**클라이언트 코드는 반환 값이 있고 동기 메서드에서 복잡한 형식 매개 변수를 사용하는 메서드를 호출합니다.**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

메서드는 `Invoke` 비동기적으로 실행 하 고 `Task` 개체를 반환 합니다. 지정하지 `await` `.Wait()`않으면 호출하는 메서드가 실행을 완료하기 전에 다음 코드 줄이 실행됩니다.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>연결 수명 이벤트를 처리하는 방법

SignalR은 처리할 수 있는 다음과 같은 연결 수명 이벤트를 제공합니다.

- `Received`: 연결시 데이터가 수신될 때 발생합니다. 수신된 데이터를 제공합니다.
- `ConnectionSlow`: 클라이언트가 느리거나 자주 끊어지는 연결을 감지할 때 발생합니다.
- `Reconnecting`: 기본 전송이 다시 연결될 때 발생합니다.
- `Reconnected`: 기본 전송이 다시 연결될 때 발생합니다.
- `StateChanged`: 연결 상태가 변경될 때 발생합니다. 이전 상태와 새 상태를 제공합니다. 연결 상태 값에 대한 자세한 내용은 [연결 상태 열거](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)를 참조하십시오.
- `Closed`: 연결이 끊어졌을 때 발생합니다.

예를 들어 치명적이지는 않지만 연결 속도가 느려지거나 자주 끊어지는 등의 간헐적인 연결 문제가 발생하는 오류에 `ConnectionSlow` 대한 경고 메시지를 표시하려면 이벤트를 처리합니다.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

자세한 내용은 [SignalR의 연결 수명 이벤트 이해 및 처리를](handling-connection-lifetime-events.md)참조하십시오.

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>오류 처리 방법

서버에서 자세한 오류 메시지를 명시적으로 활성화하지 않으면 오류 후 SignalR이 반환하는 예외 개체에는 오류에 대한 최소한의 정보가 포함됩니다. 예를 들어 호출이 `newContosoChatMessage` 실패하는 경우 오류 개체의 오류`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`메시지에는 "프로덕션 환경에서 클라이언트에 자세한 오류 메시지를 보내는 것은 보안상의 이유로 권장되지 않지만 문제 해결을 위해 자세한 오류 메시지를 사용하도록 설정하려면 서버에서 다음 코드를 사용합니다.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

SignalR이 발생 시키는 오류를 처리 하려면 연결 `Error` 개체에 이벤트에 대 한 처리기를 추가할 수 있습니다.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

메서드 호출에서 오류를 처리 하려면 try-catch 블록에서 코드를 래핑 합니다.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>클라이언트 측 로깅을 활성화하는 방법

클라이언트 측 로깅을 사용하려면 연결 개체의 `TraceLevel` 및 `TraceWriter` 속성을 설정합니다.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a>서버가 호출할 수 있는 클라이언트 메서드에 대한 WPF, Silverlight 및 콘솔 응용 프로그램 코드 샘플

서버가 호출할 수 있는 클라이언트 메서드를 정의하기 위해 이전에 표시된 코드 샘플은 WinRT 클라이언트에 적용됩니다. 다음 샘플에서는 WPF, Silverlight 및 콘솔 응용 프로그램 클라이언트에 해당하는 코드를 보여 준다.

### <a name="methods-without-parameters"></a>매개 변수가 없는 메서드

**매개 변수가 없는 서버에서 호출된 메서드에 대한 WPF 클라이언트 코드**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**매개 변수가없는 서버에서 호출 된 메서드용 Silverlight 클라이언트 코드**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**매개 변수가 없는 서버에서 호출된 메서드에 대한 콘솔 응용 프로그램 클라이언트 코드**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>매개 변수가 있는 메서드, 매개 변수 형식 지정

**매개 변수가 있는 서버에서 호출된 메서드에 대한 WPF 클라이언트 코드**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**매개 변수가 있는 서버에서 호출된 메서드에 대한 Silverlight 클라이언트 코드**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**매개 변수가 있는 서버에서 호출된 메서드에 대한 콘솔 응용 프로그램 클라이언트 코드**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>매개 변수가 있는 메서드, 매개 변수에 대한 동적 개체 지정

**매개 변수에 대 한 동적 개체를 사용 하 여 매개 변수가 있는 서버에서 호출 하는 메서드에 대 한 WPF 클라이언트 코드**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**매개 변수에 대 한 동적 개체를 사용 하 여 매개 변수가 있는 서버에서 호출 하는 메서드에 대 한 Silverlight 클라이언트 코드**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**매개 변수에 대 한 동적 개체를 사용 하 여 매개 변수가 있는 서버에서 호출 하는 메서드에 대 한 콘솔 응용 프로그램 클라이언트 코드**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
