---
title: ASP.NET Core가 있는 OWIN(Open Web Interface for .NET)
author: ardalis
description: ASP.NET Core에서 웹앱이 웹 서버에서 분리될 수 있도록 하는 OWIN(Open Web Interface for .NET)을 지원하는 방법을 알아봅니다.
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 12/18/2018
uid: fundamentals/owin
ms.openlocfilehash: 51982c7ebc4f66c2b0b73bf425d9ecbd0bf37826
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57065060"
---
# <a name="open-web-interface-for-net-owin-with-aspnet-core"></a>ASP.NET Core가 있는 OWIN(Open Web Interface for .NET)

작성자: [Steve Smith](https://ardalis.com/) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

ASP.NET Core는 OWIN(Open Web Interface for .NET)을 지원합니다. OWIN을 사용하면 웹 앱을 웹 서버에서 분리할 수 있습니다. 미들웨어를 파이프라인에서 사용하고 요청 및 관련된 응답을 처리하기 위한 표준 방법을 정의합니다. ASP.NET Core 애플리케이션 및 미들웨어는 OWIN 기반 애플리케이션, 서버 및 미들웨어와 상호 운용할 수 있습니다.

OWIN은 서로 다른 개체 모델이 있는 두 프레임워크를 함께 사용할 수 있도록 허용하는 분리 계층을 제공합니다. `Microsoft.AspNetCore.Owin` 패키지는 두 개의 어댑터 구현을 제공합니다.

* ASP.NET Core에서 OWIN으로 
* OWIN에서 ASP.NET Core로

이렇게 하면 ASP.NET Core를 OWIN 호환 가능한 서버/호스트를 기반으로 호스팅하거나 다른 OWIN 호환 가능한 구성 요소를 ASP.NET Core를 기반으로 실행되도록 할 수 있습니다.

> [!NOTE]
> 이러한 어댑터를 사용하면 성능 비용이 수반됩니다. ASP.NET Core 구성 요소만을 사용하는 앱은 `Microsoft.AspNetCore.Owin` 패키지 또는 어댑터를 사용하면 안 됩니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/owin/sample) ([다운로드 방법](xref:index#how-to-download-a-sample))

## <a name="running-owin-middleware-in-the-aspnet-core-pipeline"></a>ASP.NET Core 파이프라인에서 OWIN 미들웨어 실행

ASP.NET Core의 OWIN 지원은 `Microsoft.AspNetCore.Owin` 패키지의 일부로 배포됩니다. 이 패키지를 설치하여 OWIN 지원을 프로젝트로 가져올 수 있습니다.

OWIN 미들웨어는 `Func<IDictionary<string, object>, Task>` 인터페이스 및 특정 키 설정(예: `owin.ResponseBody`)이 필요한 [OWIN 사양](http://owin.org/spec/spec/owin-1.0.0.html)을 준수합니다. 다음과 같은 간단한 OWIN 미들웨어는 "Hello World"를 표시합니다.

```csharp
public Task OwinHello(IDictionary<string, object> environment)
{
    string responseText = "Hello World via OWIN";
    byte[] responseBytes = Encoding.UTF8.GetBytes(responseText);

    // OWIN Environment Keys: http://owin.org/spec/spec/owin-1.0.0.html
    var responseStream = (Stream)environment["owin.ResponseBody"];
    var responseHeaders = (IDictionary<string, string[]>)environment["owin.ResponseHeaders"];

    responseHeaders["Content-Length"] = new string[] { responseBytes.Length.ToString(CultureInfo.InvariantCulture) };
    responseHeaders["Content-Type"] = new string[] { "text/plain" };

    return responseStream.WriteAsync(responseBytes, 0, responseBytes.Length);
}
```

샘플 서명은 `Task`를 반환하고 OWIN에 필요한 `IDictionary<string, object>`를 수락합니다.

다음 코드는 `UseOwin` 확장 메서드로 `OwinHello` 미들웨어(위에 표시된)를 ASP.NET Core 파이프라인에 추가하는 방법을 보여줍니다.

```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseOwin(pipeline =>
    {
        pipeline(next => OwinHello);
    });
}
```

OWIN 파이프라인 내에서 수행하도록 기타 작업을 구성할 수 있습니다.

> [!NOTE]
> 응답 헤더는 응답 스트림에 대한 최초 작성 전에 수정되어야 합니다.

> [!NOTE]
> `UseOwin`에 대한 여러 번의 호출은 성능상의 이유로 권장되지 않습니다. OWIN 구성 요소는 함께 그룹화하는 경우 가장 잘 작동합니다.

```csharp
app.UseOwin(pipeline =>
{
    pipeline(async (next) =>
    {
        // do something before
        await OwinHello(new OwinEnvironment(HttpContext));
        // do something after
    });
});
```

<a name="hosting-on-owin"></a>

## <a name="using-aspnet-core-hosting-on-an-owin-based-server"></a>OWIN 기반 서버에서 호스팅하는 ASP.NET Core 사용

OWIN 기반 서버는 ASP.NET Core 앱을 호스팅할 수 있습니다. 이러한 서버는 [Nowin](https://github.com/Bobris/Nowin), .NET OWIN 웹 서버입니다. 이 문서에 대한 샘플에서는 Nowin을 참조하고 자체 호스팅 ASP.NET Core가 가능한 `IServer`를 만드는 데 사용하는 프로젝트를 추가했습니다.

[!code-csharp[](owin/sample/src/NowinSample/Program.cs?highlight=15)]

`IServer`는 `Features` 속성 및 `Start` 메서드가 필요한 인터페이스입니다.

`Start`는 서버 구성 및 시작을 담당하며 이 경우 IServerAddressesFeature에서 구문 분석된 주소를 설정하는 일련의 흐름 API 호출을 통해 수행됩니다. `_builder` 변수의 흐름 구성은 요청이 메서드의 앞부분에서 정의된 `appFunc`에 의해 처리되도록 지정합니다. 이 `Func`는 들어오는 요청을 처리하도록 각 요청마다 호출됩니다.

Nowin 서버를 쉽게 추가하고 구성하도록 `IWebHostBuilder` 확장도 추가합니다.

```csharp
using System;
using Microsoft.AspNetCore.Hosting.Server;
using Microsoft.Extensions.DependencyInjection;
using Nowin;
using NowinSample;

namespace Microsoft.AspNetCore.Hosting
{
    public static class NowinWebHostBuilderExtensions
    {
        public static IWebHostBuilder UseNowin(this IWebHostBuilder builder)
        {
            return builder.ConfigureServices(services =>
            {
                services.AddSingleton<IServer, NowinServer>();
            });
        }

        public static IWebHostBuilder UseNowin(this IWebHostBuilder builder, Action<ServerBuilder> configure)
        {
            builder.ConfigureServices(services =>
            {
                services.Configure(configure);
            });
            return builder.UseNowin();
        }
    }
}
```

이 항목이 준비되어 있으면 이 사용자 지정 서버를 통해 *Program.cs*의 확장을 호출하여 ASP.NET Core 앱을 실행합니다.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Hosting;

namespace NowinSample
{
    public class Program
    {
        public static void Main(string[] args)
        {
            var host = new WebHostBuilder()
                .UseNowin()
                .UseContentRoot(Directory.GetCurrentDirectory())
                .UseIISIntegration()
                .UseStartup<Startup>()
                .Build();

            host.Run();
        }
    }
}
```

[ASP.NET Core 서버](xref:fundamentals/servers/index)에 대해 자세히 알아봅니다.

## <a name="run-aspnet-core-on-an-owin-based-server-and-use-its-websockets-support"></a>OWIN 기반 서버에서 ASP.NET Core 실행 및 해당 WebSocket 지원 사용

ASP.NET Core에서 OWIN 기반 서버 기능을 활용할 수 있는 방법의 또 다른 예는 WebSocket과 같은 기능에 대한 액세스입니다. 이전 예제에서 사용되는 .NET OWIN 웹 서버에는 ASP.NET Core 애플리케이션에서 활용할 수 있는 기본 제공되는 웹 소켓에 대한 지원이 있습니다. 다음 예제에서는 웹 소켓을 지원하고 WebSocket을 통해 서버에 전송된 모든 항목을 다시 표시하는 단순한 웹앱을 보여 줍니다.

```csharp
public class Startup
{
    public void Configure(IApplicationBuilder app)
    {
        app.Use(async (context, next) =>
        {
            if (context.WebSockets.IsWebSocketRequest)
            {
                WebSocket webSocket = await context.WebSockets.AcceptWebSocketAsync();
                await EchoWebSocket(webSocket);
            }
            else
            {
                await next();
            }
        });

        app.Run(context =>
        {
            return context.Response.WriteAsync("Hello World");
        });
    }

    private async Task EchoWebSocket(WebSocket webSocket)
    {
        byte[] buffer = new byte[1024];
        WebSocketReceiveResult received = await webSocket.ReceiveAsync(
            new ArraySegment<byte>(buffer), CancellationToken.None);

        while (!webSocket.CloseStatus.HasValue)
        {
            // Echo anything we receive
            await webSocket.SendAsync(new ArraySegment<byte>(buffer, 0, received.Count), 
                received.MessageType, received.EndOfMessage, CancellationToken.None);

            received = await webSocket.ReceiveAsync(new ArraySegment<byte>(buffer), 
                CancellationToken.None);
        }

        await webSocket.CloseAsync(webSocket.CloseStatus.Value, 
            webSocket.CloseStatusDescription, CancellationToken.None);
    }
}
```

이 [샘플](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/owin/sample)은 이전 것과 동일한 `NowinServer`를 사용하여 구성됩니다. 유일한 차이점은 애플리케이션이 해당 `Configure` 메서드에서 구성되는 방식에 있습니다. [간단한 websocket 클라이언트](https://chrome.google.com/webstore/detail/simple-websocket-client/pfdhoblngboilpfeibdedpjgfnlcodoo?hl=en)를 사용하는 테스트는 다음 애플리케이션을 보여 줍니다.

![웹 소켓 테스트 클라이언트](owin/_static/websocket-test.png)

## <a name="owin-environment"></a>OWIN 환경

`HttpContext`를 사용하여 OWIN 환경을 구성할 수 있습니다.

```csharp

   var environment = new OwinEnvironment(HttpContext);
   var features = new OwinFeatureCollection(environment);
   ```

## <a name="owin-keys"></a>OWIN 키

OWIN은 HTTP 요청/응답 교환 전체에서 정보를 전달하는 `IDictionary<string,object>` 개체에 따라 달라집니다. ASP.NET Core는 아래에 나열된 키를 구현합니다. [기본 사양, 확장](http://owin.org/#spec) 및 [OWIN 키 지침 및 공통 키](http://owin.org/spec/spec/CommonKeys.html)를 참조하세요.

### <a name="request-data-owin-v100"></a>요청 데이터(OWIN v1.0.0)

| Key               | 값(형식) | 설명 |
| ----------------- | ------------ | ----------- |
| owin.RequestScheme | `String` |  |
| owin.RequestMethod  | `String` | |    
| owin.RequestPathBase  | `String` | |    
| owin.RequestPath | `String` | |     
| owin.RequestQueryString  | `String` | |    
| owin.RequestProtocol  | `String` | |    
| owin.RequestHeaders | `IDictionary<string,string[]>`  | |
| owin.RequestBody | `Stream`  | |

### <a name="request-data-owin-v110"></a>요청 데이터(OWIN v1.1.0)

| Key               | 값(형식) | 설명 |
| ----------------- | ------------ | ----------- |
| owin.RequestId | `String` | Optional |

### <a name="response-data-owin-v100"></a>응답 데이터(OWIN v1.0.0)

| Key               | 값(형식) | 설명 |
| ----------------- | ------------ | ----------- |
| owin.ResponseStatusCode | `int` | Optional |
| owin.ResponseReasonPhrase | `String` | Optional |
| owin.ResponseHeaders | `IDictionary<string,string[]>`  | |
| owin.ResponseBody | `Stream`  | |


### <a name="other-data-owin-v100"></a>기타 데이터(OWIN v1.0.0)

| Key               | 값(형식) | 설명 |
| ----------------- | ------------ | ----------- |
| owin.CallCancelled | `CancellationToken` |  |
| owin.Version  | `String` | |   


### <a name="common-keys"></a>공통 키

| Key               | 값(형식) | 설명 |
| ----------------- | ------------ | ----------- |
| ssl.ClientCertificate | `X509Certificate` |  |
| ssl.LoadClientCertAsync  | `Func<Task>` | |    
| server.RemoteIpAddress  | `String` | |    
| server.RemotePort | `String` | |     
| server.LocalIpAddress  | `String` | |    
| server.LocalPort  | `String` | |    
| server.IsLocal  | `bool` | |    
| server.OnSendingHeaders  | `Action<Action<object>,object>` | |


### <a name="sendfiles-v030"></a>SendFiles v0.3.0

| Key               | 값(형식) | 설명 |
| ----------------- | ------------ | ----------- |
| sendfile.SendAsync | [대리자 시그니처](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm) 참조 | 요청당 |


### <a name="opaque-v030"></a>불투명 v0.3.0

| Key               | 값(형식) | 설명 |
| ----------------- | ------------ | ----------- |
| opaque.Version | `String` |  |
| opaque.Upgrade | `OpaqueUpgrade` | [대리자 시그니처](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm) 참조 |
| opaque.Stream | `Stream` |  |
| opaque.CallCancelled | `CancellationToken` |  |


### <a name="websocket-v030"></a>WebSocket v0.3.0

| Key               | 값(형식) | 설명 |
| ----------------- | ------------ | ----------- |
| websocket.Version | `String` |  |
| websocket.Accept | `WebSocketAccept` | [대리자 시그니처](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm) 참조 |
| websocket.AcceptAlt |  | 비-사양 |
| websocket.SubProtocol | `String` | [RFC6455 Section 4.2.2](https://tools.ietf.org/html/rfc6455#section-4.2.2) 5.5단계 참조 |
| websocket.SendAsync | `WebSocketSendAsync` | [대리자 시그니처](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm) 참조  |
| websocket.ReceiveAsync | `WebSocketReceiveAsync` | [대리자 시그니처](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm) 참조  |
| websocket.CloseAsync | `WebSocketCloseAsync` | [대리자 시그니처](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm) 참조  |
| websocket.CallCancelled | `CancellationToken` |  |
| websocket.ClientCloseStatus | `int` | Optional |
| websocket.ClientCloseDescription | `String` | Optional |

## <a name="additional-resources"></a>추가 자료

* [미들웨어](xref:fundamentals/middleware/index)
* [서버](xref:fundamentals/servers/index)
