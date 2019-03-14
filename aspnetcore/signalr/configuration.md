---
title: ASP.NET Core SignalR 구성
author: bradygaster
description: ASP.NET Core SignalR 앱을 구성하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.custom: mvc
ms.date: 02/07/2019
uid: signalr/configuration
ms.openlocfilehash: f5449a15743c1f38c550fe30945bdc19f069e3f5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038190"
---
# <a name="aspnet-core-signalr-configuration"></a>ASP.NET Core SignalR 구성

## <a name="jsonmessagepack-serialization-options"></a>JSON/MessagePack 직렬화 옵션

ASP.NET Core SignalR 메시지 인코딩에 대 한 두 가지 프로토콜을 지원 합니다. [JSON](https://www.json.org/) 하 고 [MessagePack](https://msgpack.org/index.html)합니다. 각 프로토콜에 serialization 구성 옵션이 있습니다.

JSON serialization을 사용 하 여 서버에 구성할 수 있습니다 합니다 [AddJsonProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.jsonprotocoldependencyinjectionextensions.addjsonprotocol) 후 추가할 수 있는 확장 메서드 [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) 에서 프로그램 `Startup.ConfigureServices` 메서드. `AddJsonProtocol` 메서드는 `options` 개체를 전달받는 대리자를 받습니다. 이 개체의 [PayloadSerializerSettings](/dotnet/api/microsoft.aspnetcore.signalr.jsonhubprotocoloptions.payloadserializersettings) 속성은 JSON.NET의 `JsonSerializerSettings` 개체로, 인수 및 반환 값의 직렬화를 구성하는 데 사용할 수 있습니다. 더 자세한 내용은 [JSON.NET 설명서](https://www.newtonsoft.com/json/help/html/Introduction.htm)를 참고하시기 바랍니다.

예를 들어 기본 값인 "camelCase" 속성 이름 대신 "PascalCase" 속성 이름을 사용하도록 직렬화 변환기를 구성하려면 다음 코드를 사용합니다.

```csharp
services.AddSignalR()
    .AddJsonProtocol(options => {
        options.PayloadSerializerSettings.ContractResolver = 
        new DefaultContractResolver();
    });
```

.NET 클라이언트에서는 [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder)에 동일한 `AddJsonProtocol` 확장 메서드가 존재합니다. 이 확장 메서드를 확인하려면 `Microsoft.Extensions.DependencyInjection` 네임스페이스를 임포트해야 합니다.

```csharp
// At the top of the file:
using Microsoft.Extensions.DependencyInjection;

// When constructing your connection:
var connection = new HubConnectionBuilder()
    .AddJsonProtocol(options => {
        options.PayloadSerializerSettings.ContractResolver = 
            new DefaultContractResolver();
    })
    .Build();
```

> [!NOTE]
> 현재 JavaScript 클라이언트에서는 JSON 직렬화를 구성할 수 없습니다.

### <a name="messagepack-serialization-options"></a>MessagePack 직렬화 옵션

MessagePack 직렬화는 [AddMessagePackProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.msgpackprotocoldependencyinjectionextensions.addmessagepackprotocol) 호출에 대리자를 제공하여 구성할 수 있습니다. 더 자세한 내용은 [SignalR의 MessagePack](xref:signalr/messagepackhubprotocol)을 참고하시기 바랍니다.

> [!NOTE]
> 현재 JavaScript 클라이언트에서는 MessagePack 직렬화를 구성할 수 없습니다.

## <a name="configure-server-options"></a>서버 옵션 구성

다음 표는 SignalR 허브를 구성하기 위한 옵션을 설명합니다.

| 옵션 | 기본값 | 설명 |
| ------ | ------------- | ----------- |
| `ClientTimeoutInterval` | 30초 | 서버는 클라이언트를 고려 하는 경우이 간격 등 연결 유지 메시지를 수신 하지 않은 연결 끊김. 실제로이 구현 하는 방법으로 인해 연결이 끊어진 표시할 클라이언트에 대 한이 시간 제한 간격 보다 오래 걸릴 수 있습니다. 권장된 값은 double을 `KeepAliveInterval` 값입니다.|
| `HandshakeTimeout` | 15초 | 클라이언트가 이 시간 제한 내에 초기 핸드셰이크 메시지를 전송하지 않으면 연결이 닫힙니다. 이 설정은 심각한 네트워크 지연으로 인해 핸드셰이크 시간 제한 오류가 발생하는 경우에만 수정해야 하는 고급 설정입니다. 핸드셰이크 프로세스에 대한 보다 자세한 내용은 [SignalR 허브 프로토콜 사양](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md)을 참고하시기 바랍니다. |
| `KeepAliveInterval` | 15초 | 서버가 이 간격 내에 메시지를 전송하지 않으면 자동으로 ping 메시지가 전송되어 연결이 열린 상태로 유지됩니다. `KeepAliveInterval`을 변경할 경우 클라이언트의 `ServerTimeout`/`serverTimeoutInMilliseconds` 설정도 변경하십시오. 권장되는 `ServerTimeout`/`serverTimeoutInMilliseconds` 값은 `KeepAliveInterval` 값의 두 배입니다.  |
| `SupportedProtocols` | 설치된 모든 프로토콜 | 허브가 지원하는 프로토콜입니다. 기본적으로 서버에 등록된 모든 프로토콜이 허용되지만 이 목록에서 프로토콜을 제거하여 개별 허브에 대해 특정 프로토콜을 비활성화시킬 수 있습니다. |
| `EnableDetailedErrors` | `false` | 이 값이 `true`면 Hub 메서드에서 예외가 발생할 경우 자세한 예외 메시지가 클라이언트로 반환됩니다. 예외 메시지에는 민감한 정보가 포함되어 있을 수 있으므로 기본값은 `false`입니다. |

`Startup.ConfigureServices`에서 `AddSignalR` 호출에 옵션 대리자를 제공하여 모든 허브에 대한 옵션을 구성할 수 있습니다.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSignalR(hubOptions =>
    {
        hubOptions.EnableDetailedErrors = true;
        hubOptions.KeepAliveInterval = TimeSpan.FromMinutes(1);
    });
}
```

단일 허브에 대한 옵션은 `AddSignalR`에 제공된 전역 옵션을 재정의하며 [AddHubOptions\<T>](/dotnet/api/microsoft.extensions.dependencyinjection.huboptionsdependencyinjectionextensions.addhuboptions)를 사용해서 구성할 수 있습니다.

```csharp
services.AddSignalR().AddHubOptions<MyHub>(options =>
{
    options.EnableDetailedErrors = true;
});
```

### <a name="advanced-http-configuration-options"></a>고급 HTTP 구성 옵션

전송 및 메모리 버퍼 관리와 관련된 고급 설정을 구성하려면 `HttpConnectionDispatcherOptions`를 사용합니다. 이러한 옵션에 대 한 대리자를 전달 하 여 구성 됩니다 [MapHub\<T >](/dotnet/api/microsoft.aspnetcore.signalr.hubroutebuilder.maphub) 에서 `Startup.Configure`합니다.

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseSignalR((configure) => 
    {
        var desiredTransports = 
            HttpTransportType.WebSockets |
            HttpTransportType.LongPolling;

        configure.MapHub<MyHub>("/myhub", (options) => 
        {
            options.Transports = desiredTransports;
        });
    });
}
```

다음 표에서 ASP.NET Core SignalR의 고급 HTTP 옵션을 구성 하는 것에 대 한 옵션을 보여 줍니다.

| 옵션 | 기본값 | 설명 |
| ------ | ------------- | ----------- |
| `ApplicationMaxBufferSize` | 32KB | 클라이언트로부터 수신하는 서버 버퍼의 최대 바이트 수입니다. 이 값을 늘리면 서버가 더 큰 메시지를 수신할 수 있지만 메모리 소비에 부정적인 영향을 줄 수 있습니다. |
| `AuthorizationData` | 허브 클래스에 적용된 `Authorize` 특성에서 자동으로 수집된 데이터입니다. | 클라이언트가 허브에 연결할 권한이 있는지 확인하는 데 사용되는 [IAuthorizeData](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizedata) 개체의 목록입니다. |
| `TransportMaxBufferSize` | 32KB | 앱에서 전송하는 서버 버퍼의 최대 바이트 수입니다. 이 값을 늘리면 서버가 더 큰 메시지를 전송할 수 있지만 메모리 소비에 부정적인 영향을 줄 수 있습니다. |
| `Transports` | 모든 전송을 사용할 수 있습니다. | 클라이언트가 연결에 사용할 수 있는 전송을 제한할 수 있는 `HttpTransportType` 값들의 비트 마스크입니다. |
| `LongPolling` | 아래 내용을 참조하세요. | 롱 폴링 전송과 관련된 추가 옵션입니다. |
| `WebSockets` | 아래 내용을 참조하세요. | WebSockets 전송과 관련된 추가 옵션입니다. |

롱 폴링 전송에는 `LongPolling` 속성을 이용해서 구성할 수 있는 추가적인 옵션이 존재합니다.

| 옵션 | 기본값 | 설명 |
| ------ | ------------- | ----------- |
| `PollTimeout` | 90초 | 단일 폴링 요청을 종료하기 전에 서버가 메시지를 클라이언트에 전송할 때까지 대기하는 최대 시간입니다. 이 값을 줄이면 클라이언트는 더 자주 새 폴링 요청을 발행합니다. |

WebSocket 전송에는 `WebSockets` 속성을 이용해서 구성할 수 있는 추가적인 옵션이 존재합니다.

| 옵션 | 기본값 | 설명 |
| ------ | ------------- | ----------- |
| `CloseTimeout` | 5초 | 서버가 닫힌 후 클라이언트가 이 시간 제한 내에 닫기에 실패하면 연결이 종료됩니다. |
| `SubProtocolSelector` | `null` | 사용자 지정 값으로 `Sec-WebSocket-Protocol` 헤더를 설정하기 위해 사용할 수 있는 대리자입니다. 이 대리자는 클라이언트에서 요청한 값을 입력으로 받아서 원하는 값을 반환해야 합니다. |

## <a name="configure-client-options"></a>클라이언트 옵션 구성

클라이언트 옵션은 `HubConnection` 자체뿐 아니라 (.NET 및 JavaScript 클라이언트에서 모두 사용 가능한) `HubConnectionBuilder` 유형에서 구성할 수 없습니다.

### <a name="configure-logging"></a>로깅 구성

.NET 클라이언트에서 로깅은 `ConfigureLogging` 메서드를 이용해서 구성됩니다. 로깅 공급자 및 필터는 서버와 동일한 방법으로 등록할 수 있습니다. 자세한 내용은 [ASP.NET Core 로깅](xref:fundamentals/logging/index) 설명서를 참고하시기 바랍니다.

> [!NOTE]
> 로깅 공급자를 등록하는 데 필요한 패키지를 설치해야 합니다. 전체 목록은 로깅 문서의 [기본 제공 로깅 공급자](xref:fundamentals/logging/index#built-in-logging-providers) 섹션을 참고하시기 바랍니다.

예를 들어 콘솔 로깅을 사용하려면 `Microsoft.Extensions.Logging.Console` NuGet 패키지를 설치합니다. `AddConsole` 확장 메서드를 호출합니다.

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub")
    .ConfigureLogging(logging => {
        logging.SetMinimumLevel(LogLevel.Information);
        logging.AddConsole();
    })
    .Build();
```

JavaScript 클라이언트에는 유사한 `configureLogging` 메서드가 존재합니다. 기록할 로그 메시지의 최소 수준을 나타내는 `LogLevel` 값을 지정합니다. 로그는 브라우저 콘솔 창에 기록됩니다.

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub")
    .configureLogging(signalR.LogLevel.Information)
    .build();
```

> [!NOTE]
> 로깅을 완전히 비활성화시키려면 `configureLogging` 메서드에서 `signalR.LogLevel.None`을 지정하십시오.

JavaScript 클라이언트에서 사용 가능한 로그 수준은 다음과 같습니다. 로그 수준을 이 값들 중 하나로 설정하면 해당 수준 **이상**의 메시지 로깅이 활성화됩니다.

| 수준 | 설명 |
| ----- | ----------- |
| `None` | 메시지가 기록되지 않습니다. |
| `Critical` | 전체 앱에서 발생한 오류를 나타내는 메시지입니다. |
| `Error` | 현재 작업에서 발생한 오류를 나타내는 메시지입니다. |
| `Warning` | 치명적이지 않은 문제를 나타내는 메시지입니다. |
| `Information` | 정보 메시지입니다. |
| `Debug` | 디버깅에 유용한 진단 메시지입니다. |
| `Trace` | 특정 문제를 진단하기 위해 의도된 매우 자세한 진단 메시지입니다. |

### <a name="configure-allowed-transports"></a>허용되는 전송 구성

SignalR에서 사용되는 전송은 `WithUrl` 호출에서 (JavaScript에서는 `withUrl` 호출에서) 구성할 수 있습니다. `HttpTransportType` 값들의 비트 OR을 이용해서 클라이언트가 지정한 전송만 사용하도록 제한할 수 있습니다. 기본적으로 모든 전송은 활성화되어 있습니다.

예를 들어 다음 코드는 서버-전송 이벤트 전송을 비활성화시키고 WebSocket 및 롱 폴링 연결만 허용합니다.

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", HttpTransportType.WebSockets | HttpTransportType.LongPolling)
    .Build();
```

JavaScript 클라이언트에서 전송은 `withUrl`에 제공되는 옵션 개체의 `transport` 필드를 설정하여 구성합니다.

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", { transport: signalR.HttpTransportType.WebSockets | signalR.HttpTransportType.LongPolling })
    .build();
```

### <a name="configure-bearer-authentication"></a>전달자 인증 구성

SignalR 요청과 함께 인증 데이터를 제공하려면 `AccessTokenProvider` 옵션(JavaScript에서는 `accessTokenFactory`를)을 이용해서 원하는 액세스 토큰을 반환하는 함수를 지정합니다. .NET 클라이언트에서는 액세스 토큰이 HTTP "Bearer Authentication" 토큰으로 전달됩니다(`Bearer` 형식의 `Authorization` 헤더를 통해). JavaScript 클라이언트에서는 브라우저의 API가 헤더 적용 기능을 제한하는 몇 가지 경우를 **제외**하면 (특히 서버-전송 이벤트 및 WebSockets 요청) 액세스 토큰이 전달자 토큰으로 사용됩니다. 이런 경우 액세스 토큰은 `access_token`이라는 쿼리 문자열 값으로 제공됩니다.

.NET 클라이언트에서 `AccessTokenProvider` 옵션은 `WithUrl`에서 옵션 대리자를 이용해서 지정할 수 있습니다.

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.AccessTokenProvider = async () => {
            // Get and return the access token.
        };
    })
    .Build();
```

JavaScript 클라이언트에서는 `withUrl`에서 옵션 개체의 `accessTokenFactory` 필드를 설정하여 액세스 토큰을 구성합니다.

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", {
        accessTokenFactory: () => {
            // Get and return the access token.
            // This function can return a JavaScript Promise if asynchronous
            // logic is required to retrieve the access token.
        }
    })
    .build();
```

### <a name="configure-timeout-and-keep-alive-options"></a>시간 제한 및 연결 유지 옵션 구성

시간 제한 및 연결 유지 동작을 구성하기 위한 추가 옵션은 `HubConnection` 개체 자체에서 사용할 수 있습니다.

| .NET 옵션 | JavaScript 옵션 | 기본값 | 설명 |
| ----------- | ----------------- | ------------- | ----------- |
| `ServerTimeout` | `serverTimeoutInMilliseconds` | 30초(30000밀리초) | 서버 활동 시간 제한입니다. 서버가 이 시간 제한 내에 메시지를 전송하지 않으면 클라이언트는 서버 연결이 끊어졌다고 간주하고 `Closed` 이벤트(JavaScript에서는 `onclose` 이벤트)를  트리거합니다. 이 값이 충분히 커야만 ping 메시지가 서버에서 전송**되고** 시간 제한 내에 클라이언트에 의해 수신될 수 있습니다. 권장되는 값은 ping이 도착할 시간을 확보하기 위해 최소한 서버의 `KeepAliveInterval` 값의 두 배가 되는 숫자여야 합니다. |
| `HandshakeTimeout` | 구성할 수 없음 | 15초 | 초기 서버 핸드셰이크에 대한 시간 제한입니다. 서버가 이 시간 제한 내에 핸드셰이크 응답을 전송하지 않으면 클라이언트는 핸드셰이크를 취소하고 `Closed` 이벤트(JavaScript에서는 `onclose` 이벤트)를 트리거합니다. 이 설정은 심각한 네트워크 지연으로 인해 핸드셰이크 시간 제한 오류가 발생하는 경우에만 수정해야 하는 고급 설정입니다. 핸드셰이크 프로세스에 대한 자세한 내용은 [SignalR 허브 프로토콜 사양](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md)을 참고하시기 바랍니다. |

.NET 클라이언트에서 시간 제한 값은 `TimeSpan` 값으로 지정됩니다. JavaScript 클라이언트에서 시간 제한 값은 기간을 나타내는 밀리초 단위의 숫자로 지정됩니다.

### <a name="configure-additional-options"></a>추가 옵션 구성

추가 옵션은 `HubConnectionBuilder`의 `WithUrl` 메서드(JavaScript에서는 `withUrl`)에서 구성할 수 있습니다.

| .NET 옵션 | JavaScript 옵션 | 기본값 | 설명 |
| ----------- | ----------------- | ------------- | ----------- |
| `AccessTokenProvider` | `accessTokenFactory` | `null` | HTTP 요청에서 전달자 인증 토큰으로 제공된 문자열을 반환하는 함수입니다. |
| `SkipNegotiation` | `skipNegotiation` | `false` | 이 값을 `true`로 설정하면 협상 단계를 건너뜁니다. **WebSockets 전송이 유일하게 활성화된 전송인 경우에만 지원됩니다.** Azure SignalR Service를 사용하는 경우에는 이 설정을 사용할 수 없습니다. |
| `ClientCertificates` | 구성할 수 없음 * | 빈 값 | 요청을 인증하기 위해 전송할 TLS 인증서의 컬렉션입니다. |
| `Cookies` | 구성할 수 없음 * | 빈 값 | 모든 HTTP 요청과 함께 전송할 HTTP 쿠키의 컬렉션입니다. |
| `Credentials` | 구성할 수 없음 * | 빈 값 | 모든 HTTP 요청과 함께 전송할 자격 증명입니다. |
| `CloseTimeout` | 구성할 수 없음 * | 5초 | Websocket에만 해당됩니다. 클라이언트가 서버를 닫은 후 닫기 요청을 확인하기 위해 대기하는 최대 시간입니다. 서버가 이 시간 내에 종료를 승인하지 않으면 클라이언트가 연결을 끊습니다. |
| `Headers` | 구성할 수 없음 * | 빈 값 | 모든 HTTP 요청과 함께 전송할 추가 HTTP 헤더의 사전입니다. |
| `HttpMessageHandlerFactory` | 구성할 수 없음 * | `null` | HTTP 요청을 전송하기 위해 사용되는 `HttpMessageHandler`를 구성하거나 대체하는 데 사용할 수 있는 대리자입니다. WebSocket 연결에는 사용되지 않습니다. 이 대리자는 null이 아닌 값을 반환해야 하며 매개 변수로 기본값을 받습니다. 이 기본값의 설정을 수정하여 반환하거나 새로운 `HttpMessageHandler` 인스턴스를 반환합니다. **그렇지 않은 경우 처리기를 교체 해야 제공된 된 처리기에서 유지 하려는 설정을 복사, 구성된 옵션 (예: 쿠키 및 헤더) 새 처리기에 적용 되지 않습니다.** |
| `Proxy` | 구성할 수 없음 * | `null` | HTTP 요청을 전송할 때 사용할 HTTP 프록시입니다. |
| `UseDefaultCredentials` | 구성할 수 없음 * | `false` | HTTP 및 WebSockets 요청에 대한 기본 자격 증명을 전송하려면 이 부울 값을 설정합니다. 그러면 Windows 인증을 사용할 수 있습니다. |
| `WebSocketConfiguration` | 구성할 수 없음 * | `null` | 추가적인 WebSocket 옵션을 구성할 수 있는 대리자입니다. 옵션을 구성에 사용할 수 있는 [ClientWebSocketOptions](/dotnet/api/system.net.websockets.clientwebsocketoptions)의 인스턴스를 전달받습니다. |

별표(*) 표시된 옵션은 브라우저 API의 제한으로 인해 JavaScript 클라이언트에서는 구성할 수 없습니다.

.NET 클라이언트에서 이 옵션들은 `WithUrl`에 제공되는 옵션 대리자를 이용해서 수정할 수 있습니다.

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.Headers["Foo"] = "Bar";
        options.Cookies.Add(new Cookie(/* ... */);
        options.ClientCertificates.Add(/* ... */);
    })
    .Build();
```

JavaScript 클라이언트에서 이 옵션들은 `withUrl`에 제공되는 JavaScript 개체를 통해서 제공될 수 있습니다.

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", {
        skipNegotiation: true,
        transport: signalR.HttpTransportType.WebSockets
    })
    .build();
```

## <a name="additional-resources"></a>추가 자료

* <xref:tutorials/signalr>
* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/dotnet-client>
* <xref:signalr/messagepackhubprotocol>
* <xref:signalr/supported-platforms>
