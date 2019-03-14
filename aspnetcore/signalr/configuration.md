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
# <a name="aspnet-core-signalr-configuration"></a><span data-ttu-id="2bd71-103">ASP.NET Core SignalR 구성</span><span class="sxs-lookup"><span data-stu-id="2bd71-103">ASP.NET Core SignalR configuration</span></span>

## <a name="jsonmessagepack-serialization-options"></a><span data-ttu-id="2bd71-104">JSON/MessagePack 직렬화 옵션</span><span class="sxs-lookup"><span data-stu-id="2bd71-104">JSON/MessagePack serialization options</span></span>

<span data-ttu-id="2bd71-105">ASP.NET Core SignalR 메시지 인코딩에 대 한 두 가지 프로토콜을 지원 합니다. [JSON](https://www.json.org/) 하 고 [MessagePack](https://msgpack.org/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-105">ASP.NET Core SignalR supports two protocols for encoding messages: [JSON](https://www.json.org/) and [MessagePack](https://msgpack.org/index.html).</span></span> <span data-ttu-id="2bd71-106">각 프로토콜에 serialization 구성 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-106">Each protocol has serialization configuration options.</span></span>

<span data-ttu-id="2bd71-107">JSON serialization을 사용 하 여 서버에 구성할 수 있습니다 합니다 [AddJsonProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.jsonprotocoldependencyinjectionextensions.addjsonprotocol) 후 추가할 수 있는 확장 메서드 [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) 에서 프로그램 `Startup.ConfigureServices` 메서드.</span><span class="sxs-lookup"><span data-stu-id="2bd71-107">JSON serialization can be configured on the server using the [AddJsonProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.jsonprotocoldependencyinjectionextensions.addjsonprotocol) extension method, which can be added after [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) in your `Startup.ConfigureServices` method.</span></span> <span data-ttu-id="2bd71-108">`AddJsonProtocol` 메서드는 `options` 개체를 전달받는 대리자를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-108">The `AddJsonProtocol` method takes a delegate that receives an `options` object.</span></span> <span data-ttu-id="2bd71-109">이 개체의 [PayloadSerializerSettings](/dotnet/api/microsoft.aspnetcore.signalr.jsonhubprotocoloptions.payloadserializersettings) 속성은 JSON.NET의 `JsonSerializerSettings` 개체로, 인수 및 반환 값의 직렬화를 구성하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-109">The [PayloadSerializerSettings](/dotnet/api/microsoft.aspnetcore.signalr.jsonhubprotocoloptions.payloadserializersettings) property on that object is a JSON.NET `JsonSerializerSettings` object that can be used to configure serialization of arguments and return values.</span></span> <span data-ttu-id="2bd71-110">더 자세한 내용은 [JSON.NET 설명서](https://www.newtonsoft.com/json/help/html/Introduction.htm)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-110">See the [JSON.NET Documentation](https://www.newtonsoft.com/json/help/html/Introduction.htm) for more details.</span></span>

<span data-ttu-id="2bd71-111">예를 들어 기본 값인 "camelCase" 속성 이름 대신 "PascalCase" 속성 이름을 사용하도록 직렬화 변환기를 구성하려면 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-111">As an example, to configure the serializer to use "PascalCase" property names, instead of the default "camelCase" names, use the following code:</span></span>

```csharp
services.AddSignalR()
    .AddJsonProtocol(options => {
        options.PayloadSerializerSettings.ContractResolver = 
        new DefaultContractResolver();
    });
```

<span data-ttu-id="2bd71-112">.NET 클라이언트에서는 [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder)에 동일한 `AddJsonProtocol` 확장 메서드가 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-112">In the .NET client, the same `AddJsonProtocol` extension method exists on [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder).</span></span> <span data-ttu-id="2bd71-113">이 확장 메서드를 확인하려면 `Microsoft.Extensions.DependencyInjection` 네임스페이스를 임포트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-113">The `Microsoft.Extensions.DependencyInjection` namespace must be imported to resolve the extension method:</span></span>

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
> <span data-ttu-id="2bd71-114">현재 JavaScript 클라이언트에서는 JSON 직렬화를 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-114">It's not possible to configure JSON serialization in the JavaScript client at this time.</span></span>

### <a name="messagepack-serialization-options"></a><span data-ttu-id="2bd71-115">MessagePack 직렬화 옵션</span><span class="sxs-lookup"><span data-stu-id="2bd71-115">MessagePack serialization options</span></span>

<span data-ttu-id="2bd71-116">MessagePack 직렬화는 [AddMessagePackProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.msgpackprotocoldependencyinjectionextensions.addmessagepackprotocol) 호출에 대리자를 제공하여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-116">MessagePack serialization can be configured by providing a delegate to the [AddMessagePackProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.msgpackprotocoldependencyinjectionextensions.addmessagepackprotocol) call.</span></span> <span data-ttu-id="2bd71-117">더 자세한 내용은 [SignalR의 MessagePack](xref:signalr/messagepackhubprotocol)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-117">See [MessagePack in SignalR](xref:signalr/messagepackhubprotocol) for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="2bd71-118">현재 JavaScript 클라이언트에서는 MessagePack 직렬화를 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-118">It's not possible to configure MessagePack serialization in the JavaScript client at this time.</span></span>

## <a name="configure-server-options"></a><span data-ttu-id="2bd71-119">서버 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="2bd71-119">Configure server options</span></span>

<span data-ttu-id="2bd71-120">다음 표는 SignalR 허브를 구성하기 위한 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-120">The following table describes options for configuring SignalR hubs:</span></span>

| <span data-ttu-id="2bd71-121">옵션</span><span class="sxs-lookup"><span data-stu-id="2bd71-121">Option</span></span> | <span data-ttu-id="2bd71-122">기본값</span><span class="sxs-lookup"><span data-stu-id="2bd71-122">Default Value</span></span> | <span data-ttu-id="2bd71-123">설명</span><span class="sxs-lookup"><span data-stu-id="2bd71-123">Description</span></span> |
| ------ | ------------- | ----------- |
| `ClientTimeoutInterval` | <span data-ttu-id="2bd71-124">30초</span><span class="sxs-lookup"><span data-stu-id="2bd71-124">30 seconds</span></span> | <span data-ttu-id="2bd71-125">서버는 클라이언트를 고려 하는 경우이 간격 등 연결 유지 메시지를 수신 하지 않은 연결 끊김.</span><span class="sxs-lookup"><span data-stu-id="2bd71-125">The server will consider the client disconnected if it hasn't received a message (including keep-alive) in this interval.</span></span> <span data-ttu-id="2bd71-126">실제로이 구현 하는 방법으로 인해 연결이 끊어진 표시할 클라이언트에 대 한이 시간 제한 간격 보다 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-126">It could take longer than this timeout interval for the client to actually be marked disconnected, due to how this is implemented.</span></span> <span data-ttu-id="2bd71-127">권장된 값은 double을 `KeepAliveInterval` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-127">The recommended value is double the `KeepAliveInterval` value.</span></span>|
| `HandshakeTimeout` | <span data-ttu-id="2bd71-128">15초</span><span class="sxs-lookup"><span data-stu-id="2bd71-128">15 seconds</span></span> | <span data-ttu-id="2bd71-129">클라이언트가 이 시간 제한 내에 초기 핸드셰이크 메시지를 전송하지 않으면 연결이 닫힙니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-129">If the client doesn't send an initial handshake message within this time interval, the connection is closed.</span></span> <span data-ttu-id="2bd71-130">이 설정은 심각한 네트워크 지연으로 인해 핸드셰이크 시간 제한 오류가 발생하는 경우에만 수정해야 하는 고급 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-130">This is an advanced setting that should only be modified if handshake timeout errors are occurring due to severe network latency.</span></span> <span data-ttu-id="2bd71-131">핸드셰이크 프로세스에 대한 보다 자세한 내용은 [SignalR 허브 프로토콜 사양](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-131">For more detail on the handshake process, see the [SignalR Hub Protocol Specification](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md).</span></span> |
| `KeepAliveInterval` | <span data-ttu-id="2bd71-132">15초</span><span class="sxs-lookup"><span data-stu-id="2bd71-132">15 seconds</span></span> | <span data-ttu-id="2bd71-133">서버가 이 간격 내에 메시지를 전송하지 않으면 자동으로 ping 메시지가 전송되어 연결이 열린 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-133">If the server hasn't sent a message within this interval, a ping message is sent automatically to keep the connection open.</span></span> <span data-ttu-id="2bd71-134">`KeepAliveInterval`을 변경할 경우 클라이언트의 `ServerTimeout`/`serverTimeoutInMilliseconds` 설정도 변경하십시오.</span><span class="sxs-lookup"><span data-stu-id="2bd71-134">When changing `KeepAliveInterval`, change the `ServerTimeout`/`serverTimeoutInMilliseconds` setting on the client.</span></span> <span data-ttu-id="2bd71-135">권장되는 `ServerTimeout`/`serverTimeoutInMilliseconds` 값은 `KeepAliveInterval` 값의 두 배입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-135">The recommended `ServerTimeout`/`serverTimeoutInMilliseconds` value is double the `KeepAliveInterval` value.</span></span>  |
| `SupportedProtocols` | <span data-ttu-id="2bd71-136">설치된 모든 프로토콜</span><span class="sxs-lookup"><span data-stu-id="2bd71-136">All installed protocols</span></span> | <span data-ttu-id="2bd71-137">허브가 지원하는 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-137">Protocols supported by this hub.</span></span> <span data-ttu-id="2bd71-138">기본적으로 서버에 등록된 모든 프로토콜이 허용되지만 이 목록에서 프로토콜을 제거하여 개별 허브에 대해 특정 프로토콜을 비활성화시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-138">By default, all protocols registered on the server are allowed, but protocols can be removed from this list to disable specific protocols for individual hubs.</span></span> |
| `EnableDetailedErrors` | `false` | <span data-ttu-id="2bd71-139">이 값이 `true`면 Hub 메서드에서 예외가 발생할 경우 자세한 예외 메시지가 클라이언트로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-139">If `true`, detailed exception messages are returned to clients when an exception is thrown in a Hub method.</span></span> <span data-ttu-id="2bd71-140">예외 메시지에는 민감한 정보가 포함되어 있을 수 있으므로 기본값은 `false`입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-140">The default is `false`, as these exception messages can contain sensitive information.</span></span> |

<span data-ttu-id="2bd71-141">`Startup.ConfigureServices`에서 `AddSignalR` 호출에 옵션 대리자를 제공하여 모든 허브에 대한 옵션을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-141">Options can be configured for all hubs by providing an options delegate to the `AddSignalR` call in `Startup.ConfigureServices`.</span></span>

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

<span data-ttu-id="2bd71-142">단일 허브에 대한 옵션은 `AddSignalR`에 제공된 전역 옵션을 재정의하며 [AddHubOptions\<T>](/dotnet/api/microsoft.extensions.dependencyinjection.huboptionsdependencyinjectionextensions.addhuboptions)를 사용해서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-142">Options for a single hub override the global options provided in `AddSignalR` and can be configured using [AddHubOptions\<T>](/dotnet/api/microsoft.extensions.dependencyinjection.huboptionsdependencyinjectionextensions.addhuboptions):</span></span>

```csharp
services.AddSignalR().AddHubOptions<MyHub>(options =>
{
    options.EnableDetailedErrors = true;
});
```

### <a name="advanced-http-configuration-options"></a><span data-ttu-id="2bd71-143">고급 HTTP 구성 옵션</span><span class="sxs-lookup"><span data-stu-id="2bd71-143">Advanced HTTP configuration options</span></span>

<span data-ttu-id="2bd71-144">전송 및 메모리 버퍼 관리와 관련된 고급 설정을 구성하려면 `HttpConnectionDispatcherOptions`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-144">Use `HttpConnectionDispatcherOptions` to configure advanced settings related to transports and memory buffer management.</span></span> <span data-ttu-id="2bd71-145">이러한 옵션에 대 한 대리자를 전달 하 여 구성 됩니다 [MapHub\<T >](/dotnet/api/microsoft.aspnetcore.signalr.hubroutebuilder.maphub) 에서 `Startup.Configure`합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-145">These options are configured by passing a delegate to [MapHub\<T>](/dotnet/api/microsoft.aspnetcore.signalr.hubroutebuilder.maphub) in `Startup.Configure`.</span></span>

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

<span data-ttu-id="2bd71-146">다음 표에서 ASP.NET Core SignalR의 고급 HTTP 옵션을 구성 하는 것에 대 한 옵션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-146">The following table describes options for configuring ASP.NET Core SignalR's advanced HTTP options:</span></span>

| <span data-ttu-id="2bd71-147">옵션</span><span class="sxs-lookup"><span data-stu-id="2bd71-147">Option</span></span> | <span data-ttu-id="2bd71-148">기본값</span><span class="sxs-lookup"><span data-stu-id="2bd71-148">Default Value</span></span> | <span data-ttu-id="2bd71-149">설명</span><span class="sxs-lookup"><span data-stu-id="2bd71-149">Description</span></span> |
| ------ | ------------- | ----------- |
| `ApplicationMaxBufferSize` | <span data-ttu-id="2bd71-150">32KB</span><span class="sxs-lookup"><span data-stu-id="2bd71-150">32 KB</span></span> | <span data-ttu-id="2bd71-151">클라이언트로부터 수신하는 서버 버퍼의 최대 바이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-151">The maximum number of bytes received from the client that the server buffers.</span></span> <span data-ttu-id="2bd71-152">이 값을 늘리면 서버가 더 큰 메시지를 수신할 수 있지만 메모리 소비에 부정적인 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-152">Increasing this value allows the server to receive larger messages, but can negatively impact memory consumption.</span></span> |
| `AuthorizationData` | <span data-ttu-id="2bd71-153">허브 클래스에 적용된 `Authorize` 특성에서 자동으로 수집된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-153">Data automatically gathered from the `Authorize` attributes applied to the Hub class.</span></span> | <span data-ttu-id="2bd71-154">클라이언트가 허브에 연결할 권한이 있는지 확인하는 데 사용되는 [IAuthorizeData](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizedata) 개체의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-154">A list of [IAuthorizeData](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizedata) objects used to determine if a client is authorized to connect to the hub.</span></span> |
| `TransportMaxBufferSize` | <span data-ttu-id="2bd71-155">32KB</span><span class="sxs-lookup"><span data-stu-id="2bd71-155">32 KB</span></span> | <span data-ttu-id="2bd71-156">앱에서 전송하는 서버 버퍼의 최대 바이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-156">The maximum number of bytes sent by the app that the server buffers.</span></span> <span data-ttu-id="2bd71-157">이 값을 늘리면 서버가 더 큰 메시지를 전송할 수 있지만 메모리 소비에 부정적인 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-157">Increasing this value allows the server to send larger messages, but can negatively impact memory consumption.</span></span> |
| `Transports` | <span data-ttu-id="2bd71-158">모든 전송을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-158">All Transports are enabled.</span></span> | <span data-ttu-id="2bd71-159">클라이언트가 연결에 사용할 수 있는 전송을 제한할 수 있는 `HttpTransportType` 값들의 비트 마스크입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-159">A bitmask of `HttpTransportType` values that can restrict the transports a client can use to connect.</span></span> |
| `LongPolling` | <span data-ttu-id="2bd71-160">아래 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2bd71-160">See below.</span></span> | <span data-ttu-id="2bd71-161">롱 폴링 전송과 관련된 추가 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-161">Additional options specific to the Long Polling transport.</span></span> |
| `WebSockets` | <span data-ttu-id="2bd71-162">아래 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2bd71-162">See below.</span></span> | <span data-ttu-id="2bd71-163">WebSockets 전송과 관련된 추가 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-163">Additional options specific to the WebSockets transport.</span></span> |

<span data-ttu-id="2bd71-164">롱 폴링 전송에는 `LongPolling` 속성을 이용해서 구성할 수 있는 추가적인 옵션이 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-164">The Long Polling transport has additional options that can be configured using the `LongPolling` property:</span></span>

| <span data-ttu-id="2bd71-165">옵션</span><span class="sxs-lookup"><span data-stu-id="2bd71-165">Option</span></span> | <span data-ttu-id="2bd71-166">기본값</span><span class="sxs-lookup"><span data-stu-id="2bd71-166">Default Value</span></span> | <span data-ttu-id="2bd71-167">설명</span><span class="sxs-lookup"><span data-stu-id="2bd71-167">Description</span></span> |
| ------ | ------------- | ----------- |
| `PollTimeout` | <span data-ttu-id="2bd71-168">90초</span><span class="sxs-lookup"><span data-stu-id="2bd71-168">90 seconds</span></span> | <span data-ttu-id="2bd71-169">단일 폴링 요청을 종료하기 전에 서버가 메시지를 클라이언트에 전송할 때까지 대기하는 최대 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-169">The maximum amount of time the server waits for a message to send to the client before terminating a single poll request.</span></span> <span data-ttu-id="2bd71-170">이 값을 줄이면 클라이언트는 더 자주 새 폴링 요청을 발행합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-170">Decreasing this value causes the client to issue new poll requests more frequently.</span></span> |

<span data-ttu-id="2bd71-171">WebSocket 전송에는 `WebSockets` 속성을 이용해서 구성할 수 있는 추가적인 옵션이 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-171">The WebSocket transport has additional options that can be configured using the `WebSockets` property:</span></span>

| <span data-ttu-id="2bd71-172">옵션</span><span class="sxs-lookup"><span data-stu-id="2bd71-172">Option</span></span> | <span data-ttu-id="2bd71-173">기본값</span><span class="sxs-lookup"><span data-stu-id="2bd71-173">Default Value</span></span> | <span data-ttu-id="2bd71-174">설명</span><span class="sxs-lookup"><span data-stu-id="2bd71-174">Description</span></span> |
| ------ | ------------- | ----------- |
| `CloseTimeout` | <span data-ttu-id="2bd71-175">5초</span><span class="sxs-lookup"><span data-stu-id="2bd71-175">5 seconds</span></span> | <span data-ttu-id="2bd71-176">서버가 닫힌 후 클라이언트가 이 시간 제한 내에 닫기에 실패하면 연결이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-176">After the server closes, if the client fails to close within this time interval, the connection is terminated.</span></span> |
| `SubProtocolSelector` | `null` | <span data-ttu-id="2bd71-177">사용자 지정 값으로 `Sec-WebSocket-Protocol` 헤더를 설정하기 위해 사용할 수 있는 대리자입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-177">A delegate that can be used to set the `Sec-WebSocket-Protocol` header to a custom value.</span></span> <span data-ttu-id="2bd71-178">이 대리자는 클라이언트에서 요청한 값을 입력으로 받아서 원하는 값을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-178">The delegate receives the values requested by the client as input and is expected to return the desired value.</span></span> |

## <a name="configure-client-options"></a><span data-ttu-id="2bd71-179">클라이언트 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="2bd71-179">Configure client options</span></span>

<span data-ttu-id="2bd71-180">클라이언트 옵션은 `HubConnection` 자체뿐 아니라 (.NET 및 JavaScript 클라이언트에서 모두 사용 가능한) `HubConnectionBuilder` 유형에서 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-180">Client options can be configured on the `HubConnectionBuilder` type (available in both .NET and JavaScript clients), as well as on the `HubConnection` itself.</span></span>

### <a name="configure-logging"></a><span data-ttu-id="2bd71-181">로깅 구성</span><span class="sxs-lookup"><span data-stu-id="2bd71-181">Configure logging</span></span>

<span data-ttu-id="2bd71-182">.NET 클라이언트에서 로깅은 `ConfigureLogging` 메서드를 이용해서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-182">Logging is configured in the .NET Client using the `ConfigureLogging` method.</span></span> <span data-ttu-id="2bd71-183">로깅 공급자 및 필터는 서버와 동일한 방법으로 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-183">Logging providers and filters can be registered in the same way as they are on the server.</span></span> <span data-ttu-id="2bd71-184">자세한 내용은 [ASP.NET Core 로깅](xref:fundamentals/logging/index) 설명서를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-184">See the [Logging in ASP.NET Core](xref:fundamentals/logging/index) documentation for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="2bd71-185">로깅 공급자를 등록하는 데 필요한 패키지를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-185">In order to register Logging providers, you must install the necessary packages.</span></span> <span data-ttu-id="2bd71-186">전체 목록은 로깅 문서의 [기본 제공 로깅 공급자](xref:fundamentals/logging/index#built-in-logging-providers) 섹션을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-186">See the [Built-in logging providers](xref:fundamentals/logging/index#built-in-logging-providers) section of the docs for a full list.</span></span>

<span data-ttu-id="2bd71-187">예를 들어 콘솔 로깅을 사용하려면 `Microsoft.Extensions.Logging.Console` NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-187">For example, to enable Console logging, install the `Microsoft.Extensions.Logging.Console` NuGet package.</span></span> <span data-ttu-id="2bd71-188">`AddConsole` 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-188">Call the `AddConsole` extension method:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub")
    .ConfigureLogging(logging => {
        logging.SetMinimumLevel(LogLevel.Information);
        logging.AddConsole();
    })
    .Build();
```

<span data-ttu-id="2bd71-189">JavaScript 클라이언트에는 유사한 `configureLogging` 메서드가 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-189">In the JavaScript client, a similar `configureLogging` method exists.</span></span> <span data-ttu-id="2bd71-190">기록할 로그 메시지의 최소 수준을 나타내는 `LogLevel` 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-190">Provide a `LogLevel` value indicating the minimum level of log messages to produce.</span></span> <span data-ttu-id="2bd71-191">로그는 브라우저 콘솔 창에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-191">Logs are written to the browser console window.</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub")
    .configureLogging(signalR.LogLevel.Information)
    .build();
```

> [!NOTE]
> <span data-ttu-id="2bd71-192">로깅을 완전히 비활성화시키려면 `configureLogging` 메서드에서 `signalR.LogLevel.None`을 지정하십시오.</span><span class="sxs-lookup"><span data-stu-id="2bd71-192">To disable logging entirely, specify `signalR.LogLevel.None` in the `configureLogging` method.</span></span>

<span data-ttu-id="2bd71-193">JavaScript 클라이언트에서 사용 가능한 로그 수준은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-193">Log levels available to the JavaScript client are listed below.</span></span> <span data-ttu-id="2bd71-194">로그 수준을 이 값들 중 하나로 설정하면 해당 수준 **이상**의 메시지 로깅이 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-194">Setting the log level to one of these values enables logging of messages at **or above** that level.</span></span>

| <span data-ttu-id="2bd71-195">수준</span><span class="sxs-lookup"><span data-stu-id="2bd71-195">Level</span></span> | <span data-ttu-id="2bd71-196">설명</span><span class="sxs-lookup"><span data-stu-id="2bd71-196">Description</span></span> |
| ----- | ----------- |
| `None` | <span data-ttu-id="2bd71-197">메시지가 기록되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-197">No messages are logged.</span></span> |
| `Critical` | <span data-ttu-id="2bd71-198">전체 앱에서 발생한 오류를 나타내는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-198">Messages that indicate a failure in the entire app.</span></span> |
| `Error` | <span data-ttu-id="2bd71-199">현재 작업에서 발생한 오류를 나타내는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-199">Messages that indicate a failure in the current operation.</span></span> |
| `Warning` | <span data-ttu-id="2bd71-200">치명적이지 않은 문제를 나타내는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-200">Messages that indicate a non-fatal problem.</span></span> |
| `Information` | <span data-ttu-id="2bd71-201">정보 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-201">Informational messages.</span></span> |
| `Debug` | <span data-ttu-id="2bd71-202">디버깅에 유용한 진단 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-202">Diagnostic messages useful for debugging.</span></span> |
| `Trace` | <span data-ttu-id="2bd71-203">특정 문제를 진단하기 위해 의도된 매우 자세한 진단 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-203">Very detailed diagnostic messages designed for diagnosing specific issues.</span></span> |

### <a name="configure-allowed-transports"></a><span data-ttu-id="2bd71-204">허용되는 전송 구성</span><span class="sxs-lookup"><span data-stu-id="2bd71-204">Configure allowed transports</span></span>

<span data-ttu-id="2bd71-205">SignalR에서 사용되는 전송은 `WithUrl` 호출에서 (JavaScript에서는 `withUrl` 호출에서) 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-205">The transports used by SignalR can be configured in the `WithUrl` call (`withUrl` in JavaScript).</span></span> <span data-ttu-id="2bd71-206">`HttpTransportType` 값들의 비트 OR을 이용해서 클라이언트가 지정한 전송만 사용하도록 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-206">A bitwise-OR of the values of `HttpTransportType` can be used to restrict the client to only use the specified transports.</span></span> <span data-ttu-id="2bd71-207">기본적으로 모든 전송은 활성화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-207">All transports are enabled by default.</span></span>

<span data-ttu-id="2bd71-208">예를 들어 다음 코드는 서버-전송 이벤트 전송을 비활성화시키고 WebSocket 및 롱 폴링 연결만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-208">For example, to disable the Server-Sent Events transport, but allow WebSockets and Long Polling connections:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", HttpTransportType.WebSockets | HttpTransportType.LongPolling)
    .Build();
```

<span data-ttu-id="2bd71-209">JavaScript 클라이언트에서 전송은 `withUrl`에 제공되는 옵션 개체의 `transport` 필드를 설정하여 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-209">In the JavaScript client, transports are configured by setting the `transport` field on the options object provided to `withUrl`:</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", { transport: signalR.HttpTransportType.WebSockets | signalR.HttpTransportType.LongPolling })
    .build();
```

### <a name="configure-bearer-authentication"></a><span data-ttu-id="2bd71-210">전달자 인증 구성</span><span class="sxs-lookup"><span data-stu-id="2bd71-210">Configure bearer authentication</span></span>

<span data-ttu-id="2bd71-211">SignalR 요청과 함께 인증 데이터를 제공하려면 `AccessTokenProvider` 옵션(JavaScript에서는 `accessTokenFactory`를)을 이용해서 원하는 액세스 토큰을 반환하는 함수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-211">To provide authentication data along with SignalR requests, use the `AccessTokenProvider` option (`accessTokenFactory` in JavaScript) to specify a function that returns the desired access token.</span></span> <span data-ttu-id="2bd71-212">.NET 클라이언트에서는 액세스 토큰이 HTTP "Bearer Authentication" 토큰으로 전달됩니다(`Bearer` 형식의 `Authorization` 헤더를 통해).</span><span class="sxs-lookup"><span data-stu-id="2bd71-212">In the .NET Client, this access token is passed in as an HTTP "Bearer Authentication" token (Using the `Authorization` header with a type of `Bearer`).</span></span> <span data-ttu-id="2bd71-213">JavaScript 클라이언트에서는 브라우저의 API가 헤더 적용 기능을 제한하는 몇 가지 경우를 **제외**하면 (특히 서버-전송 이벤트 및 WebSockets 요청) 액세스 토큰이 전달자 토큰으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-213">In the JavaScript client, the access token is used as a Bearer token, **except** in a few cases where browser APIs restrict the ability to apply headers (specifically, in Server-Sent Events and WebSockets requests).</span></span> <span data-ttu-id="2bd71-214">이런 경우 액세스 토큰은 `access_token`이라는 쿼리 문자열 값으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-214">In these cases, the access token is provided as a query string value `access_token`.</span></span>

<span data-ttu-id="2bd71-215">.NET 클라이언트에서 `AccessTokenProvider` 옵션은 `WithUrl`에서 옵션 대리자를 이용해서 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-215">In the .NET client, the `AccessTokenProvider` option can be specified using the options delegate in `WithUrl`:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.AccessTokenProvider = async () => {
            // Get and return the access token.
        };
    })
    .Build();
```

<span data-ttu-id="2bd71-216">JavaScript 클라이언트에서는 `withUrl`에서 옵션 개체의 `accessTokenFactory` 필드를 설정하여 액세스 토큰을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-216">In the JavaScript client, the access token is configured by setting the `accessTokenFactory` field on the options object in `withUrl`:</span></span>

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

### <a name="configure-timeout-and-keep-alive-options"></a><span data-ttu-id="2bd71-217">시간 제한 및 연결 유지 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="2bd71-217">Configure timeout and keep-alive options</span></span>

<span data-ttu-id="2bd71-218">시간 제한 및 연결 유지 동작을 구성하기 위한 추가 옵션은 `HubConnection` 개체 자체에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-218">Additional options for configuring timeout and keep-alive behavior are available on the `HubConnection` object itself:</span></span>

| <span data-ttu-id="2bd71-219">.NET 옵션</span><span class="sxs-lookup"><span data-stu-id="2bd71-219">.NET Option</span></span> | <span data-ttu-id="2bd71-220">JavaScript 옵션</span><span class="sxs-lookup"><span data-stu-id="2bd71-220">JavaScript Option</span></span> | <span data-ttu-id="2bd71-221">기본값</span><span class="sxs-lookup"><span data-stu-id="2bd71-221">Default Value</span></span> | <span data-ttu-id="2bd71-222">설명</span><span class="sxs-lookup"><span data-stu-id="2bd71-222">Description</span></span> |
| ----------- | ----------------- | ------------- | ----------- |
| `ServerTimeout` | `serverTimeoutInMilliseconds` | <span data-ttu-id="2bd71-223">30초(30000밀리초)</span><span class="sxs-lookup"><span data-stu-id="2bd71-223">30 seconds (30,000 milliseconds)</span></span> | <span data-ttu-id="2bd71-224">서버 활동 시간 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-224">Timeout for server activity.</span></span> <span data-ttu-id="2bd71-225">서버가 이 시간 제한 내에 메시지를 전송하지 않으면 클라이언트는 서버 연결이 끊어졌다고 간주하고 `Closed` 이벤트(JavaScript에서는 `onclose` 이벤트)를  트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-225">If the server hasn't sent a message in this interval, the client considers the server disconnected and triggers the `Closed` event (`onclose` in JavaScript).</span></span> <span data-ttu-id="2bd71-226">이 값이 충분히 커야만 ping 메시지가 서버에서 전송**되고** 시간 제한 내에 클라이언트에 의해 수신될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-226">This value must be large enough for a ping message to be sent from the server **and** received by the client within the timeout interval.</span></span> <span data-ttu-id="2bd71-227">권장되는 값은 ping이 도착할 시간을 확보하기 위해 최소한 서버의 `KeepAliveInterval` 값의 두 배가 되는 숫자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-227">The recommended value is a number at least double the server's `KeepAliveInterval` value, to allow time for pings to arrive.</span></span> |
| `HandshakeTimeout` | <span data-ttu-id="2bd71-228">구성할 수 없음</span><span class="sxs-lookup"><span data-stu-id="2bd71-228">Not configurable</span></span> | <span data-ttu-id="2bd71-229">15초</span><span class="sxs-lookup"><span data-stu-id="2bd71-229">15 seconds</span></span> | <span data-ttu-id="2bd71-230">초기 서버 핸드셰이크에 대한 시간 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-230">Timeout for initial server handshake.</span></span> <span data-ttu-id="2bd71-231">서버가 이 시간 제한 내에 핸드셰이크 응답을 전송하지 않으면 클라이언트는 핸드셰이크를 취소하고 `Closed` 이벤트(JavaScript에서는 `onclose` 이벤트)를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-231">If the server doesn't send a handshake response in this interval, the client cancels the handshake and triggers the `Closed` event (`onclose` in JavaScript).</span></span> <span data-ttu-id="2bd71-232">이 설정은 심각한 네트워크 지연으로 인해 핸드셰이크 시간 제한 오류가 발생하는 경우에만 수정해야 하는 고급 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-232">This is an advanced setting that should only be modified if handshake timeout errors are occurring due to severe network latency.</span></span> <span data-ttu-id="2bd71-233">핸드셰이크 프로세스에 대한 자세한 내용은 [SignalR 허브 프로토콜 사양](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-233">For more detail on the Handshake process, see the [SignalR Hub Protocol Specification](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md).</span></span> |

<span data-ttu-id="2bd71-234">.NET 클라이언트에서 시간 제한 값은 `TimeSpan` 값으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-234">In the .NET Client, timeout values are specified as `TimeSpan` values.</span></span> <span data-ttu-id="2bd71-235">JavaScript 클라이언트에서 시간 제한 값은 기간을 나타내는 밀리초 단위의 숫자로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-235">In the JavaScript client, timeout values are specified as a number indicating the duration in milliseconds.</span></span>

### <a name="configure-additional-options"></a><span data-ttu-id="2bd71-236">추가 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="2bd71-236">Configure additional options</span></span>

<span data-ttu-id="2bd71-237">추가 옵션은 `HubConnectionBuilder`의 `WithUrl` 메서드(JavaScript에서는 `withUrl`)에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-237">Additional options can be configured in the `WithUrl` (`withUrl` in JavaScript) method on `HubConnectionBuilder`:</span></span>

| <span data-ttu-id="2bd71-238">.NET 옵션</span><span class="sxs-lookup"><span data-stu-id="2bd71-238">.NET Option</span></span> | <span data-ttu-id="2bd71-239">JavaScript 옵션</span><span class="sxs-lookup"><span data-stu-id="2bd71-239">JavaScript Option</span></span> | <span data-ttu-id="2bd71-240">기본값</span><span class="sxs-lookup"><span data-stu-id="2bd71-240">Default Value</span></span> | <span data-ttu-id="2bd71-241">설명</span><span class="sxs-lookup"><span data-stu-id="2bd71-241">Description</span></span> |
| ----------- | ----------------- | ------------- | ----------- |
| `AccessTokenProvider` | `accessTokenFactory` | `null` | <span data-ttu-id="2bd71-242">HTTP 요청에서 전달자 인증 토큰으로 제공된 문자열을 반환하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-242">A function returning a string that is provided as a Bearer authentication token in HTTP requests.</span></span> |
| `SkipNegotiation` | `skipNegotiation` | `false` | <span data-ttu-id="2bd71-243">이 값을 `true`로 설정하면 협상 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-243">Set this to `true` to skip the negotiation step.</span></span> <span data-ttu-id="2bd71-244">**WebSockets 전송이 유일하게 활성화된 전송인 경우에만 지원됩니다.**</span><span class="sxs-lookup"><span data-stu-id="2bd71-244">**Only supported when the WebSockets transport is the only enabled transport**.</span></span> <span data-ttu-id="2bd71-245">Azure SignalR Service를 사용하는 경우에는 이 설정을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-245">This setting can't be enabled when using the Azure SignalR Service.</span></span> |
| `ClientCertificates` | <span data-ttu-id="2bd71-246">구성할 수 없음 \*</span><span class="sxs-lookup"><span data-stu-id="2bd71-246">Not configurable \*</span></span> | <span data-ttu-id="2bd71-247">빈 값</span><span class="sxs-lookup"><span data-stu-id="2bd71-247">Empty</span></span> | <span data-ttu-id="2bd71-248">요청을 인증하기 위해 전송할 TLS 인증서의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-248">A collection of TLS certificates to send to authenticate requests.</span></span> |
| `Cookies` | <span data-ttu-id="2bd71-249">구성할 수 없음 \*</span><span class="sxs-lookup"><span data-stu-id="2bd71-249">Not configurable \*</span></span> | <span data-ttu-id="2bd71-250">빈 값</span><span class="sxs-lookup"><span data-stu-id="2bd71-250">Empty</span></span> | <span data-ttu-id="2bd71-251">모든 HTTP 요청과 함께 전송할 HTTP 쿠키의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-251">A collection of HTTP cookies to send with every HTTP request.</span></span> |
| `Credentials` | <span data-ttu-id="2bd71-252">구성할 수 없음 \*</span><span class="sxs-lookup"><span data-stu-id="2bd71-252">Not configurable \*</span></span> | <span data-ttu-id="2bd71-253">빈 값</span><span class="sxs-lookup"><span data-stu-id="2bd71-253">Empty</span></span> | <span data-ttu-id="2bd71-254">모든 HTTP 요청과 함께 전송할 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-254">Credentials to send with every HTTP request.</span></span> |
| `CloseTimeout` | <span data-ttu-id="2bd71-255">구성할 수 없음 \*</span><span class="sxs-lookup"><span data-stu-id="2bd71-255">Not configurable \*</span></span> | <span data-ttu-id="2bd71-256">5초</span><span class="sxs-lookup"><span data-stu-id="2bd71-256">5 seconds</span></span> | <span data-ttu-id="2bd71-257">Websocket에만 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-257">WebSockets only.</span></span> <span data-ttu-id="2bd71-258">클라이언트가 서버를 닫은 후 닫기 요청을 확인하기 위해 대기하는 최대 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-258">The maximum amount of time the client waits after closing for the server to acknowledge the close request.</span></span> <span data-ttu-id="2bd71-259">서버가 이 시간 내에 종료를 승인하지 않으면 클라이언트가 연결을 끊습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-259">If the server doesn't acknowledge the close within this time, the client disconnects.</span></span> |
| `Headers` | <span data-ttu-id="2bd71-260">구성할 수 없음 \*</span><span class="sxs-lookup"><span data-stu-id="2bd71-260">Not configurable \*</span></span> | <span data-ttu-id="2bd71-261">빈 값</span><span class="sxs-lookup"><span data-stu-id="2bd71-261">Empty</span></span> | <span data-ttu-id="2bd71-262">모든 HTTP 요청과 함께 전송할 추가 HTTP 헤더의 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-262">A dictionary of additional HTTP headers to send with every HTTP request.</span></span> |
| `HttpMessageHandlerFactory` | <span data-ttu-id="2bd71-263">구성할 수 없음 \*</span><span class="sxs-lookup"><span data-stu-id="2bd71-263">Not configurable \*</span></span> | `null` | <span data-ttu-id="2bd71-264">HTTP 요청을 전송하기 위해 사용되는 `HttpMessageHandler`를 구성하거나 대체하는 데 사용할 수 있는 대리자입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-264">A delegate that can be used to configure or replace the `HttpMessageHandler` used to send HTTP requests.</span></span> <span data-ttu-id="2bd71-265">WebSocket 연결에는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-265">Not used for WebSocket connections.</span></span> <span data-ttu-id="2bd71-266">이 대리자는 null이 아닌 값을 반환해야 하며 매개 변수로 기본값을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-266">This delegate must return a non-null value, and it receives the default value as a parameter.</span></span> <span data-ttu-id="2bd71-267">이 기본값의 설정을 수정하여 반환하거나 새로운 `HttpMessageHandler` 인스턴스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-267">Either modify settings on that default value and return it, or return a new `HttpMessageHandler` instance.</span></span> <span data-ttu-id="2bd71-268">**그렇지 않은 경우 처리기를 교체 해야 제공된 된 처리기에서 유지 하려는 설정을 복사, 구성된 옵션 (예: 쿠키 및 헤더) 새 처리기에 적용 되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="2bd71-268">**When replacing the handler make sure to copy the settings you want to keep from the provided handler, otherwise, the configured options (such as Cookies and Headers) won't apply to the new handler.**</span></span> |
| `Proxy` | <span data-ttu-id="2bd71-269">구성할 수 없음 \*</span><span class="sxs-lookup"><span data-stu-id="2bd71-269">Not configurable \*</span></span> | `null` | <span data-ttu-id="2bd71-270">HTTP 요청을 전송할 때 사용할 HTTP 프록시입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-270">An HTTP proxy to use when sending HTTP requests.</span></span> |
| `UseDefaultCredentials` | <span data-ttu-id="2bd71-271">구성할 수 없음 \*</span><span class="sxs-lookup"><span data-stu-id="2bd71-271">Not configurable \*</span></span> | `false` | <span data-ttu-id="2bd71-272">HTTP 및 WebSockets 요청에 대한 기본 자격 증명을 전송하려면 이 부울 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-272">Set this boolean to send the default credentials for HTTP and WebSockets requests.</span></span> <span data-ttu-id="2bd71-273">그러면 Windows 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-273">This enables the use of Windows authentication.</span></span> |
| `WebSocketConfiguration` | <span data-ttu-id="2bd71-274">구성할 수 없음 \*</span><span class="sxs-lookup"><span data-stu-id="2bd71-274">Not configurable \*</span></span> | `null` | <span data-ttu-id="2bd71-275">추가적인 WebSocket 옵션을 구성할 수 있는 대리자입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-275">A delegate that can be used to configure additional WebSocket options.</span></span> <span data-ttu-id="2bd71-276">옵션을 구성에 사용할 수 있는 [ClientWebSocketOptions](/dotnet/api/system.net.websockets.clientwebsocketoptions)의 인스턴스를 전달받습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-276">Receives an instance of [ClientWebSocketOptions](/dotnet/api/system.net.websockets.clientwebsocketoptions) that can be used to configure the options.</span></span> |

<span data-ttu-id="2bd71-277">별표(\*) 표시된 옵션은 브라우저 API의 제한으로 인해 JavaScript 클라이언트에서는 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-277">Options marked with an asterisk (\*) aren't configurable in the JavaScript client, due to limitations in browser APIs.</span></span>

<span data-ttu-id="2bd71-278">.NET 클라이언트에서 이 옵션들은 `WithUrl`에 제공되는 옵션 대리자를 이용해서 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-278">In the .NET Client, these options can be modified by the options delegate provided to `WithUrl`:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.Headers["Foo"] = "Bar";
        options.Cookies.Add(new Cookie(/* ... */);
        options.ClientCertificates.Add(/* ... */);
    })
    .Build();
```

<span data-ttu-id="2bd71-279">JavaScript 클라이언트에서 이 옵션들은 `withUrl`에 제공되는 JavaScript 개체를 통해서 제공될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd71-279">In the JavaScript Client, these options can be provided in a JavaScript object provided to `withUrl`:</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", {
        skipNegotiation: true,
        transport: signalR.HttpTransportType.WebSockets
    })
    .build();
```

## <a name="additional-resources"></a><span data-ttu-id="2bd71-280">추가 자료</span><span class="sxs-lookup"><span data-stu-id="2bd71-280">Additional resources</span></span>

* <xref:tutorials/signalr>
* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/dotnet-client>
* <xref:signalr/messagepackhubprotocol>
* <xref:signalr/supported-platforms>
