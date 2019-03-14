---
title: ASP.NET Core SignalR에서 MessagePack 허브 프로토콜 사용
author: bradygaster
description: ASP.NET Core SignalR에 MessagePack 허브 프로토콜을 추가합니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.custom: mvc
ms.date: 06/04/2018
uid: signalr/messagepackhubprotocol
ms.openlocfilehash: da6eeeb51f5d0fc2ad69978688ad1c4ca4d63dab
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57060400"
---
# <a name="use-messagepack-hub-protocol-in-signalr-for-aspnet-core"></a><span data-ttu-id="c8159-103">ASP.NET Core SignalR에서 MessagePack 허브 프로토콜 사용</span><span class="sxs-lookup"><span data-stu-id="c8159-103">Use MessagePack Hub Protocol in SignalR for ASP.NET Core</span></span>

<span data-ttu-id="c8159-104">작성자: [Brennan Conroy](https://github.com/BrennanConroy)</span><span class="sxs-lookup"><span data-stu-id="c8159-104">By [Brennan Conroy](https://github.com/BrennanConroy)</span></span>

<span data-ttu-id="c8159-105">이 문서는 독자가 [시작하기](xref:tutorials/signalr)에서 설명하는 내용을 잘 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-105">This article assumes the reader is familiar with the topics covered in [Get Started](xref:tutorials/signalr).</span></span>

## <a name="what-is-messagepack"></a><span data-ttu-id="c8159-106">MessagePack이란?</span><span class="sxs-lookup"><span data-stu-id="c8159-106">What is MessagePack?</span></span>

<span data-ttu-id="c8159-107">[MessagePack](https://msgpack.org/index.html)은 빠르고 간결한 이진 직렬화 포맷입니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-107">[MessagePack](https://msgpack.org/index.html) is a binary serialization format that is fast and compact.</span></span> <span data-ttu-id="c8159-108">[JSON](https://www.json.org/)에 비해 크기가 작은 메시지를 생성하기 때문에 성능 및 대역폭이 중요한 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-108">It's useful when performance and bandwidth are a concern because it creates smaller messages compared to [JSON](https://www.json.org/).</span></span> <span data-ttu-id="c8159-109">이진 형식이므로 바이트가 MessagePack 파서를 거치지 않는 한 네트워크 추적 및 로그를 살펴보더라도 메시지를 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-109">Because it's a binary format, messages are unreadable when looking at network traces and logs unless the bytes are passed through a MessagePack parser.</span></span> <span data-ttu-id="c8159-110">SignalR은 MessagePack 형식을 기본으로 지원하며 클라이언트 및 서버에서 사용하기 위한 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-110">SignalR has built-in support for the MessagePack format, and provides APIs for the client and server to use.</span></span>

## <a name="configure-messagepack-on-the-server"></a><span data-ttu-id="c8159-111">서버에서 MessagePack 구성</span><span class="sxs-lookup"><span data-stu-id="c8159-111">Configure MessagePack on the server</span></span>

<span data-ttu-id="c8159-112">서버에서 MessagePack 허브 프로토콜을 사용하려면 앱에 `Microsoft.AspNetCore.SignalR.Protocols.MessagePack` 패키지를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-112">To enable the MessagePack Hub Protocol on the server, install the `Microsoft.AspNetCore.SignalR.Protocols.MessagePack` package in your app.</span></span> <span data-ttu-id="c8159-113">Startup.cs 파일에서 `AddSignalR` 호출에 `AddMessagePackProtocol`을 추가하여 서버에서 MessagePack 지원을 활성화시킵니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-113">In the Startup.cs file add `AddMessagePackProtocol` to the `AddSignalR` call to enable MessagePack support on the server.</span></span>

> [!NOTE]
> <span data-ttu-id="c8159-114">JSON은 기본적으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-114">JSON is enabled by default.</span></span> <span data-ttu-id="c8159-115">MessagePack을 추가하면 JSON 및 MessagePack 클라이언트에 대한 기능이 모두 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-115">Adding MessagePack enables support for both JSON and MessagePack clients.</span></span>

```csharp
services.AddSignalR()
    .AddMessagePackProtocol();
```

<span data-ttu-id="c8159-116">MessagePack이 데이터를 서식화하는 방법을 사용자 지정하려면 `AddMessagePackProtocol`에 구성 옵션을 위한 대리자를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-116">To customize how MessagePack will format your data, `AddMessagePackProtocol` takes a delegate for configuring options.</span></span> <span data-ttu-id="c8159-117">이 대리자에서 `FormatterResolvers` 속성을 이용하여 MessagePack 직렬화 옵션을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-117">In that delegate, the `FormatterResolvers` property can be used to configure MessagePack serialization options.</span></span> <span data-ttu-id="c8159-118">리졸버가 동작하는 방식에 대한 자세한 내용은 [MessagePack CSharp](https://github.com/neuecc/MessagePack-CSharp)의 MessagePack 라이브러리를 방문해보시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-118">For more information on how the resolvers work, visit the MessagePack library at [MessagePack-CSharp](https://github.com/neuecc/MessagePack-CSharp).</span></span> <span data-ttu-id="c8159-119">직렬화하고자 하는 개체에 특성을 적용하여 해당 개체를 처리하는 방식을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-119">Attributes can be used on the objects you want to serialize to define how they should be handled.</span></span>

```csharp
services.AddSignalR()
    .AddMessagePackProtocol(options =>
    {
        options.FormatterResolvers = new List<MessagePack.IFormatterResolver>()
        {
            MessagePack.Resolvers.StandardResolver.Instance
        };
    });
```

## <a name="configure-messagepack-on-the-client"></a><span data-ttu-id="c8159-120">클라이언트에서 MessagePack 구성</span><span class="sxs-lookup"><span data-stu-id="c8159-120">Configure MessagePack on the client</span></span>

> [!NOTE]
> <span data-ttu-id="c8159-121">JSON은 지원되는 클라이언트에 대해 기본적으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-121">JSON is enabled by default for the supported clients.</span></span> <span data-ttu-id="c8159-122">클라이언트는 단일 프로토콜만 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-122">Clients can only support a single protocol.</span></span> <span data-ttu-id="c8159-123">MessagePack 지원을 추가하면 기존에 구성된 모든 프로토콜이 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-123">Adding MessagePack support will replace any previously configured protocols.</span></span>

### <a name="net-client"></a><span data-ttu-id="c8159-124">.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="c8159-124">.NET client</span></span>

<span data-ttu-id="c8159-125">.NET 클라이언트에서 MessagePack을 활성화시키려면 `Microsoft.AspNetCore.SignalR.Protocols.MessagePack` 패키지를 설치하고 `HubConnectionBuilder`에서 `AddMessagePackProtocol`을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-125">To enable MessagePack in the .NET Client, install the `Microsoft.AspNetCore.SignalR.Protocols.MessagePack` package and call `AddMessagePackProtocol` on `HubConnectionBuilder`.</span></span>

```csharp
var hubConnection = new HubConnectionBuilder()
                        .WithUrl("/chatHub")
                        .AddMessagePackProtocol()
                        .Build();
```

> [!NOTE]
> <span data-ttu-id="c8159-126">서버와 마찬가지로 이 `AddMessagePackProtocol` 호출은 옵션을 구성하기 위한 대리자를 전달받습니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-126">This `AddMessagePackProtocol` call takes a delegate for configuring options just like the server.</span></span>

### <a name="javascript-client"></a><span data-ttu-id="c8159-127">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="c8159-127">JavaScript client</span></span>

<span data-ttu-id="c8159-128">JavaScript 클라이언트에 대 한 지원은 MessagePack가 제공 된 `@aspnet/signalr-protocol-msgpack` npm 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-128">MessagePack support for the JavaScript client is provided by the `@aspnet/signalr-protocol-msgpack` npm package.</span></span>

```console
npm install @aspnet/signalr-protocol-msgpack
```

<span data-ttu-id="c8159-129">npm 패키지를 설치한 뒤에 모듈을 JavaScript 모듈 로더를 통해서 직접 사용할 수도 있고 *node_modules\\@aspnet\signalr-protocol-msgpack\dist\browser\signalr-protocol-msgpack.js* 파일을 참조해서 브라우저로 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-129">After installing the npm package, the module can be used directly via a JavaScript module loader or imported into the browser by referencing the *node_modules\\@aspnet\signalr-protocol-msgpack\dist\browser\signalr-protocol-msgpack.js* file.</span></span> <span data-ttu-id="c8159-130">브라우저에서 `msgpack5` 라이브러리도 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-130">In a browser, the `msgpack5` library must also be referenced.</span></span> <span data-ttu-id="c8159-131">사용 된 `<script>` 대 한 참조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-131">Use a `<script>` tag to create a reference.</span></span> <span data-ttu-id="c8159-132">이 라이브러리는 *node_modules\msgpack5\dist\msgpack5.js*에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-132">The library can be found at *node_modules\msgpack5\dist\msgpack5.js*.</span></span>

> [!NOTE]
> <span data-ttu-id="c8159-133">`<script>` 요소를 사용할 때 순서가 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-133">When using the `<script>` element, the order is important.</span></span> <span data-ttu-id="c8159-134">*msgpack5.js*보다 *signalr-protocol-msgpack.js*를 먼저 참조하면 MessagePack을 이용해서 연결하려고 시도할 때 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-134">If *signalr-protocol-msgpack.js* is referenced before *msgpack5.js*, an error occurs when trying to connect with MessagePack.</span></span> <span data-ttu-id="c8159-135">*signalr.js*도 *signalr-protocol-msgpack.js*보다 먼저 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-135">*signalr.js* is also required before *signalr-protocol-msgpack.js*.</span></span>

```html
<script src="~/lib/signalr/signalr.js"></script>
<script src="~/lib/msgpack5/msgpack5.js"></script>
<script src="~/lib/signalr/signalr-protocol-msgpack.js"></script>
```

<span data-ttu-id="c8159-136">`HubConnectionBuilder`에 `.withHubProtocol(new signalR.protocols.msgpack.MessagePackHubProtocol())`을 추가하면 클라이언트가 서버에 연결할 때 MessagePack 프로토콜을 사용하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-136">Adding `.withHubProtocol(new signalR.protocols.msgpack.MessagePackHubProtocol())` to the `HubConnectionBuilder` will configure the client to use the MessagePack protocol when connecting to a server.</span></span>

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/chatHub")
    .withHubProtocol(new signalR.protocols.msgpack.MessagePackHubProtocol())
    .build();
```

> [!NOTE]
> <span data-ttu-id="c8159-137">현재 JavaScript 클라이언트에는 MessagePack 프로토콜에 대한 구성 옵션이 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8159-137">At this time, there are no configuration options for the MessagePack protocol on the JavaScript client.</span></span>

## <a name="related-resources"></a><span data-ttu-id="c8159-138">관련 자료</span><span class="sxs-lookup"><span data-stu-id="c8159-138">Related resources</span></span>

* [<span data-ttu-id="c8159-139">시작</span><span class="sxs-lookup"><span data-stu-id="c8159-139">Get Started</span></span>](xref:tutorials/signalr)
* [<span data-ttu-id="c8159-140">.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="c8159-140">.NET client</span></span>](xref:signalr/dotnet-client)
* [<span data-ttu-id="c8159-141">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="c8159-141">JavaScript client</span></span>](xref:signalr/javascript-client)
