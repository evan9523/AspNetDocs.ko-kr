---
uid: signalr/overview/getting-started/introduction-to-signalr
title: 시그널R 소개 | 마이크로 소프트 문서
author: bradygaster
description: 이 문서에서는 SignalR이 무엇인지, 그리고 이를 만들도록 설계된 솔루션 중 일부에 대해 설명합니다.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 8dbc31a5c8d59fa55dc5b513c1a51d24d18a685f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675942"
---
# <a name="introduction-to-signalr"></a><span data-ttu-id="466ce-103">SignalR 소개</span><span class="sxs-lookup"><span data-stu-id="466ce-103">Introduction to SignalR</span></span>

<span data-ttu-id="466ce-104">로 [패트릭 플레처](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="466ce-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="466ce-105">이 문서에서는 SignalR이 무엇인지, 그리고 이를 만들도록 설계된 솔루션 중 일부에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-105">This article describes what SignalR is, and some of the solutions it was designed to create.</span></span> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="466ce-106">질문 및 의견</span><span class="sxs-lookup"><span data-stu-id="466ce-106">Questions and comments</span></span>
> 
> <span data-ttu-id="466ce-107">이 자습서를 어떻게 좋아했는지, 그리고 페이지 하단의 댓글에서 개선할 수 있는 내용에 대한 피드백을 남겨주세요.</span><span class="sxs-lookup"><span data-stu-id="466ce-107">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="466ce-108">당신은 튜토리얼과 직접 관련이없는 질문이있는 경우, 당신은 [ASP.NET SignalR 포럼에](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 게시하거나 [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr).</span><span class="sxs-lookup"><span data-stu-id="466ce-108">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr).</span></span>

## <a name="what-is-signalr"></a><span data-ttu-id="466ce-109">시그널R이란?</span><span class="sxs-lookup"><span data-stu-id="466ce-109">What is SignalR?</span></span>

<span data-ttu-id="466ce-110">ASP.NET SignalR은 응용 프로그램에 실시간 웹 기능을 추가하는 프로세스를 간소화하는 ASP.NET 개발자를 위한 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-110">ASP.NET SignalR is a library for ASP.NET developers that simplifies the process of adding real-time web functionality to applications.</span></span> <span data-ttu-id="466ce-111">실시간 웹 기능은 서버가 클라이언트가 새 데이터를 요청할 때까지 기다리지 않고 서버 코드가 연결된 클라이언트에 콘텐츠를 푸시하는 기능을 사용할 수 있게 되면 즉시 사용할 수 있도록 하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-111">Real-time web functionality is the ability to have server code push content to connected clients instantly as it becomes available, rather than having the server wait for a client to request new data.</span></span>

<span data-ttu-id="466ce-112">SignalR은 ASP.NET 응용 프로그램에 모든 종류의 "실시간" 웹 기능을 추가하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-112">SignalR can be used to add any sort of "real-time" web functionality to your ASP.NET application.</span></span> <span data-ttu-id="466ce-113">채팅은 종종 예로 사용되지만 훨씬 더 많은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-113">While chat is often used as an example, you can do a whole lot more.</span></span> <span data-ttu-id="466ce-114">사용자가 새 데이터를 보기 위해 웹 페이지를 새로 고치거나 페이지가 새 데이터를 검색하기 위해 [긴 폴링을](http://en.wikipedia.org/wiki/Push_technology#Long_polling) 구현할 때마다 SignalR을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-114">Any time a user refreshes a web page to see new data, or the page implements [long polling](http://en.wikipedia.org/wiki/Push_technology#Long_polling) to retrieve new data, it is a candidate for using SignalR.</span></span> <span data-ttu-id="466ce-115">예를 들어 대시보드 및 모니터링 응용 프로그램, 공동 작업 응용 프로그램(예: 문서 동시 편집), 작업 진행 률 업데이트 및 실시간 양식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-115">Examples include dashboards and monitoring applications, collaborative applications (such as simultaneous editing of documents), job progress updates, and real-time forms.</span></span>

<span data-ttu-id="466ce-116">SignalR은 또한 서버에서 고주파 업데이트가 필요한 완전히 새로운 유형의 웹 애플리케이션(예: 실시간 게임)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-116">SignalR also enables completely new types of web applications that require high frequency updates from the server, for example, real-time gaming.</span></span>

<span data-ttu-id="466ce-117">SignalR은 서버 측 .NET 코드에서 클라이언트 브라우저(및 기타 클라이언트 플랫폼)에서 JavaScript 함수를 호출하는 RPC(서버 간 원격 프로시저 호출)를 만들기 위한 간단한 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-117">SignalR provides a simple API for creating server-to-client remote procedure calls (RPC) that call JavaScript functions in client browsers (and other client platforms) from server-side .NET code.</span></span> <span data-ttu-id="466ce-118">SignalR에는 연결 관리(예: 이벤트 연결 및 연결 해제) 및 연결 그룹화용 API도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-118">SignalR also includes API for connection management (for instance, connect and disconnect events), and grouping connections.</span></span>

![SignalR을 사용 하 고 메서드를 호출](introduction-to-signalr/_static/image1.png)

<span data-ttu-id="466ce-120">SignalR은 연결 관리를 자동으로 처리하며, 대화방처럼 메시지를 연결된 모든 클라이언트에 동시에 브로드캐스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-120">SignalR handles connection management automatically, and lets you broadcast messages to all connected clients simultaneously, like a chat room.</span></span> <span data-ttu-id="466ce-121">메시지를 특정 클라이언트에 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-121">You can also send messages to specific clients.</span></span> <span data-ttu-id="466ce-122">클라이언트와 서버 간의 연결은 기존 HTTP 연결과 달리 영구적이며, 각 통신에 대해 다시 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-122">The connection between the client and server is persistent, unlike a classic HTTP connection, which is re-established for each communication.</span></span>

<span data-ttu-id="466ce-123">SignalR은 서버 코드가 현재 웹에서 일반적인 요청 응답 모델이 아니라 RPC(원격 프로시저 호출)를 사용하여 브라우저에서 클라이언트 코드에 호출할 수 있는 "서버 푸시" 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-123">SignalR supports "server push" functionality, in which server code can call out to client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model common on the web today.</span></span>

<span data-ttu-id="466ce-124">SignalR 애플리케이션은 기본 제공 및 타사 확장 공급자를 사용하여 수천 개의 클라이언트로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-124">SignalR applications can scale out to thousands of clients using built-in, and third-party scale-out providers.</span></span>

<span data-ttu-id="466ce-125">기본 제공 공급자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-125">Built-in providers include:</span></span>
* [<span data-ttu-id="466ce-126">Service Bus</span><span class="sxs-lookup"><span data-stu-id="466ce-126">Service Bus</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [<span data-ttu-id="466ce-127">SQL Server</span><span class="sxs-lookup"><span data-stu-id="466ce-127">SQL Server</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [<span data-ttu-id="466ce-128">Redis</span><span class="sxs-lookup"><span data-stu-id="466ce-128">Redis</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

<span data-ttu-id="466ce-129">타사 공급자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-129">Third-party providers include:</span></span>
* <span data-ttu-id="466ce-130">[N캐시](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).</span><span class="sxs-lookup"><span data-stu-id="466ce-130">[NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).</span></span>

<span data-ttu-id="466ce-131">SignalR은 [GitHub를](https://github.com/signalr)통해 액세스할 수 있는 오픈 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-131">SignalR is open-source, accessible through [GitHub](https://github.com/signalr).</span></span>

## <a name="signalr-and-websocket"></a><span data-ttu-id="466ce-132">시그널러 및 웹소켓</span><span class="sxs-lookup"><span data-stu-id="466ce-132">SignalR and WebSocket</span></span>

<span data-ttu-id="466ce-133">SignalR은 사용 가능한 경우 새 WebSocket 전송을 사용하며 필요한 경우 이전 전송으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-133">SignalR uses the new WebSocket transport where available and falls back to older transports where necessary.</span></span> <span data-ttu-id="466ce-134">WebSocket을 사용하여 앱을 직접 작성할 수 있지만 SignalR을 사용하면 구현해야 하는 많은 추가 기능이 이미 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-134">While you could certainly write your app using WebSocket directly, using SignalR means that a lot of the extra functionality you would need to implement is already done for you.</span></span> <span data-ttu-id="466ce-135">가장 중요한 것은 이전 클라이언트에 대한 별도의 코드 경로를 만들지 않고도 WebSocket을 활용하도록 앱을 코딩할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-135">Most importantly, this means that you can code your app to take advantage of WebSocket without having to worry about creating a separate code path for older clients.</span></span> <span data-ttu-id="466ce-136">또한 SignalR은 기본 전송의 변경 사항을 지원하도록 업데이트되어 응용 프로그램에 WebSocket 버전 간에 일관된 인터페이스를 제공하므로 WebSocket 업데이트에 대해 걱정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-136">SignalR also shields you from having to worry about updates to WebSocket, since SignalR is updated to support changes in the underlying transport, providing your application a consistent interface across versions of WebSocket.</span></span>

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a><span data-ttu-id="466ce-137">운송 및 대체</span><span class="sxs-lookup"><span data-stu-id="466ce-137">Transports and fallbacks</span></span>

<span data-ttu-id="466ce-138">SignalR은 클라이언트와 서버 간에 실시간 작업을 수행하는 데 필요한 일부 전송에 대한 추상화입니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-138">SignalR is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="466ce-139">SignalR 연결은 HTTP로 시작하여 사용 가능한 경우 WebSocket 연결로 승격됩니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-139">A SignalR connection starts as HTTP, and is then promoted to a WebSocket connection if it is available.</span></span> <span data-ttu-id="466ce-140">WebSocket은 서버 메모리를 가장 효율적으로 사용하고 대기 시간이 가장 낮으며 가장 기본적인 기능(예: 클라이언트와 서버 간의 전체 이중 통신)을 가지므로 SignalR에 이상적인 전송수단이지만, 가장 엄격한 요구 사항도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-140">WebSocket is the ideal transport for SignalR, since it makes the most efficient use of server memory, has the lowest latency, and has the most underlying features (such as full duplex communication between client and server), but it also has the most stringent requirements: WebSocket requires the server to be using Windows Server 2012 or Windows 8, and .NET Framework 4.5.</span></span> <span data-ttu-id="466ce-141">이러한 요구 사항이 충족되지 않으면 SignalR은 다른 전송을 사용하여 연결을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-141">If these requirements are not met, SignalR will attempt to use other transports to make its connections.</span></span>

### <a name="html-5-transports"></a><span data-ttu-id="466ce-142">HTML 5 전송</span><span class="sxs-lookup"><span data-stu-id="466ce-142">HTML 5 transports</span></span>

<span data-ttu-id="466ce-143">이러한 전송은 HTML [5에](http://en.wikipedia.org/wiki/HTML5)대한 지원에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-143">These transports depend on support for [HTML 5](http://en.wikipedia.org/wiki/HTML5).</span></span> <span data-ttu-id="466ce-144">클라이언트 브라우저가 HTML 5 표준을 지원하지 않는 경우 이전 전송이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-144">If the client browser does not support the HTML 5 standard, older transports will be used.</span></span>

- <span data-ttu-id="466ce-145">**WebSocket(서버와** 브라우저 가 모두 Websocket을 지원할 수 있음을 나타내는 경우)</span><span class="sxs-lookup"><span data-stu-id="466ce-145">**WebSocket** (if both the server and browser indicate they can support Websocket).</span></span> <span data-ttu-id="466ce-146">WebSocket은 클라이언트와 서버 간의 진정한 지속적 양방향 연결을 설정하는 유일한 전송입니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-146">WebSocket is the only transport that establishes a true persistent, two-way connection between client and server.</span></span> <span data-ttu-id="466ce-147">그러나 WebSocket에는 가장 엄격한 요구 사항도 있습니다. 그것은 완전히 마이크로 소프트 인터넷 익스플로러의 최신 버전에서 만 지원, 구글 크롬, 모질라 파이어 폭스, 오페라와 사파리와 같은 다른 브라우저에서 부분 구현만.</span><span class="sxs-lookup"><span data-stu-id="466ce-147">However, WebSocket also has the most stringent requirements; it is fully supported only in the latest versions of Microsoft Internet Explorer, Google Chrome, and Mozilla Firefox, and only has a partial implementation in other browsers such as Opera and Safari.</span></span>
- <span data-ttu-id="466ce-148">EventSource라고도 하는 **서버 전송 이벤트(브라우저가**Internet Explorer를 제외한 기본적으로 모든 브라우저인 서버 전송 이벤트를 지원하는 경우).</span><span class="sxs-lookup"><span data-stu-id="466ce-148">**Server Sent Events**, also known as EventSource (if the browser supports Server Sent Events, which is basically all browsers except Internet Explorer.)</span></span>

### <a name="comet-transports"></a><span data-ttu-id="466ce-149">혜성 수송</span><span class="sxs-lookup"><span data-stu-id="466ce-149">Comet transports</span></span>

<span data-ttu-id="466ce-150">다음 전송은 브라우저 또는 다른 클라이언트가 오래 유지된 HTTP 요청을 유지 관리하는 [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) 웹 응용 프로그램 모델을 기반으로 하며, 서버는 클라이언트가 특별히 요청하지 않고 클라이언트에 데이터를 푸시하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-150">The following transports are based on the [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) web application model, in which a browser or other client maintains a long-held HTTP request, which the server can use to push data to the client without the client specifically requesting it.</span></span>

- <span data-ttu-id="466ce-151">**영원히 프레임** (인터넷 익스플로러 전용).</span><span class="sxs-lookup"><span data-stu-id="466ce-151">**Forever Frame** (for Internet Explorer only).</span></span> <span data-ttu-id="466ce-152">Forever Frame은 완료되지 않은 서버의 끝점에 요청을 하는 숨겨진 IFrame을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-152">Forever Frame creates a hidden IFrame which makes a request to an endpoint on the server that does not complete.</span></span> <span data-ttu-id="466ce-153">그런 다음 서버는 즉시 실행되는 스크립트를 클라이언트로 계속 전송하여 서버에서 클라이언트로의 단방향 실시간 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-153">The server then continually sends script to the client which is immediately executed, providing a one-way realtime connection from server to client.</span></span> <span data-ttu-id="466ce-154">클라이언트에서 서버로의 연결은 서버에서 클라이언트 연결로의 별도의 연결을 사용하며 표준 HTTP 요청과 마찬가지로 전송해야 하는 각 데이터에 대해 새 연결이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-154">The connection from client to server uses a separate connection from the server to client connection, and like a standard HTTP request, a new connection is created for each piece of data that needs to be sent.</span></span>
- <span data-ttu-id="466ce-155">**아약스 긴 폴링**.</span><span class="sxs-lookup"><span data-stu-id="466ce-155">**Ajax long polling**.</span></span> <span data-ttu-id="466ce-156">긴 폴링은 영구 연결을 만들지 않지만 대신 서버가 응답할 때까지 열려 있는 요청으로 서버를 폴링하고, 이 시점에서 연결이 닫히고 새 연결이 즉시 요청됩니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-156">Long polling does not create a persistent connection, but instead polls the server with a request that stays open until the server responds, at which point the connection closes, and a new connection is requested immediately.</span></span> <span data-ttu-id="466ce-157">이렇게 하면 연결이 재설정되는 동안 약간의 대기 시간이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-157">This may introduce some latency while the connection resets.</span></span>

<span data-ttu-id="466ce-158">어떤 구성에서 지원되는 전송에 대한 자세한 내용은 [지원되는 플랫폼을](supported-platforms.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="466ce-158">For more information on what transports are supported under which configurations, see [Supported Platforms](supported-platforms.md).</span></span>

### <a name="transport-selection-process"></a><span data-ttu-id="466ce-159">운송 선택 프로세스</span><span class="sxs-lookup"><span data-stu-id="466ce-159">Transport selection process</span></span>

<span data-ttu-id="466ce-160">다음 목록은 SignalR에서 사용할 전송을 결정하는 데 사용하는 단계를 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-160">The following list shows the steps that SignalR uses to decide which transport to use.</span></span>

1. <span data-ttu-id="466ce-161">브라우저가 Internet Explorer 8 이전인 경우 긴 폴링이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-161">If the browser is Internet Explorer 8 or earlier, Long Polling is used.</span></span>
2. <span data-ttu-id="466ce-162">JSONP가 구성된 경우(즉, `jsonp` 매개 변수가 `true` 연결이 시작될 때로 설정됨) 긴 폴링이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-162">If JSONP is configured (that is, the `jsonp` parameter is set to `true` when the connection is started), Long Polling is used.</span></span>
3. <span data-ttu-id="466ce-163">도메인 간 연결이 이루어지는 경우(즉, SignalR 끝점이 호스팅 페이지와 동일한 도메인에 없는 경우) 다음 기준이 충족되면 WebSocket이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-163">If a cross-domain connection is being made (that is, if the SignalR endpoint is not in the same domain as the hosting page), then WebSocket will be used if the following criteria are met:</span></span>

   - <span data-ttu-id="466ce-164">클라이언트는 CORS(원본 간 리소스 공유)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-164">The client supports CORS (Cross-Origin Resource Sharing).</span></span> <span data-ttu-id="466ce-165">CORS를 지원하는 클라이언트에 대한 자세한 내용은 [caniuse.com CORS를](http://www.caniuse.com/CORS)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="466ce-165">For details on which clients support CORS, see [CORS at caniuse.com](http://www.caniuse.com/CORS).</span></span>
   - <span data-ttu-id="466ce-166">클라이언트는 웹 소켓을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-166">The client supports WebSocket</span></span>
   - <span data-ttu-id="466ce-167">서버는 웹 소켓을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-167">The server supports WebSocket</span></span>

     <span data-ttu-id="466ce-168">이러한 기준 중 어느 것이라도 충족되지 않으면 긴 폴링이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-168">If any of these criteria are not met, Long Polling will be used.</span></span> <span data-ttu-id="466ce-169">도메인 간 연결에 대한 자세한 내용은 [도메인 간 연결을 설정하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)참조하세요.</span><span class="sxs-lookup"><span data-stu-id="466ce-169">For more information on cross-domain connections, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>
4. <span data-ttu-id="466ce-170">JSONP가 구성되지 않고 연결이 도메인 간이 아닌 경우 클라이언트와 서버가 모두 지원하는 경우 WebSocket이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-170">If JSONP is not configured and the connection is not cross-domain, WebSocket will be used if both the client and server support it.</span></span>
5. <span data-ttu-id="466ce-171">클라이언트 또는 서버가 WebSocket을 지원하지 않는 경우 서버 전송 이벤트를 사용할 수 있는 경우 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-171">If either the client or server do not support WebSocket, Server Sent Events is used if it is available.</span></span>
6. <span data-ttu-id="466ce-172">서버 전송 이벤트를 사용할 수 없는 경우 영원히 프레임이 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-172">If Server Sent Events is not available, Forever Frame is attempted.</span></span>
7. <span data-ttu-id="466ce-173">영원히 프레임이 실패하면 긴 폴링이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-173">If Forever Frame fails, Long Polling is used.</span></span>

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a><span data-ttu-id="466ce-174">전송 모니터링</span><span class="sxs-lookup"><span data-stu-id="466ce-174">Monitoring transports</span></span>

<span data-ttu-id="466ce-175">허브에 로깅을 활성화하고 브라우저에서 콘솔 창을 열어 응용 프로그램이 사용하는 전송을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-175">You can determine what transport your application is using by enabling logging on your hub, and opening the console window in your browser.</span></span>

<span data-ttu-id="466ce-176">브라우저에서 허브 의 이벤트에 대한 로깅을 사용하려면 클라이언트 응용 프로그램에 다음 명령을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-176">To enable logging for your hub's events in a browser, add the following command to your client application:</span></span>

`$.connection.hub.logging = true;`

- <span data-ttu-id="466ce-177">인터넷 익스플로러에서 F12를 눌러 개발자 도구를 열고 콘솔 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-177">In Internet Explorer, open the developer tools by pressing F12, and click the Console tab.</span></span>

    ![마이크로소프트 인터넷 익스플로러의 콘솔](introduction-to-signalr/_static/image2.png)
- <span data-ttu-id="466ce-179">크롬에서 Ctrl+Shift+J를 눌러 본체를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-179">In Chrome, open the console by pressing Ctrl+Shift+J.</span></span>

    ![구글 크롬의 콘솔](introduction-to-signalr/_static/image3.png)

<span data-ttu-id="466ce-181">콘솔을 열고 로깅을 사용하도록 설정하면 SignalR에서 사용 중인 전송을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-181">With the console open and logging enabled, you'll be able to see which transport is being used by SignalR.</span></span>

![웹 소켓 전송을 보여주는 인터넷 익스플로러의 콘솔](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a><span data-ttu-id="466ce-183">전송 지정</span><span class="sxs-lookup"><span data-stu-id="466ce-183">Specifying a transport</span></span>

<span data-ttu-id="466ce-184">전송을 협상하는 데는 일정 한 시간과 클라이언트/서버 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-184">Negotiating a transport takes a certain amount of time and client/server resources.</span></span> <span data-ttu-id="466ce-185">클라이언트 기능이 알려진 경우 클라이언트 연결을 시작할 때 전송을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-185">If the client capabilities are known, then a transport can be specified when the client connection is started.</span></span> <span data-ttu-id="466ce-186">다음 코드 스니펫은 클라이언트가 다른 프로토콜을 지원하지 않는 것으로 알려진 경우와 마찬가지로 Ajax Long Polling 전송을 사용하여 연결을 시작하는 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-186">The following code snippet demonstrates starting a connection using the Ajax Long Polling transport, as would be used if it was known that the client did not support any other protocol:</span></span>

`connection.start({ transport: 'longPolling' });`

<span data-ttu-id="466ce-187">클라이언트가 특정 전송을 순서대로 시도하도록 하려면 대체 순서를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-187">You can specify a fallback order if you want a client to try specific transports in order.</span></span> <span data-ttu-id="466ce-188">다음 코드 스니펫은 WebSocket을 시도하고 실패하여 Long Polling로 직접 이동했음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-188">The following code snippet demonstrates trying WebSocket, and failing that, going directly to Long Polling.</span></span>

`connection.start({ transport: ['webSockets','longPolling'] });`

<span data-ttu-id="466ce-189">전송을 지정하기 위한 문자열 상수는 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-189">The string constants for specifying transports are defined as follows:</span></span>

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a><span data-ttu-id="466ce-190">연결 및 허브</span><span class="sxs-lookup"><span data-stu-id="466ce-190">Connections and Hubs</span></span>

<span data-ttu-id="466ce-191">SignalR API에는 클라이언트와 서버 간의 통신을 위한 두 가지 모델인 영구 연결 및 허브가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-191">The SignalR API contains two models for communicating between clients and servers: Persistent Connections and Hubs.</span></span>

<span data-ttu-id="466ce-192">연결은 단일 받는 사람, 그룹화된 메시지 또는 브로드캐스트 메시지를 보내기 위한 간단한 끝점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-192">A Connection represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="466ce-193">영구 연결 API(PersistentConnection 클래스에서 .NET 코드로 표시)는 개발자에게 SignalR이 노출하는 하위 수준 통신 프로토콜에 직접 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-193">The Persistent Connection API (represented in .NET code by the PersistentConnection class) gives the developer direct access to the low-level communication protocol that SignalR exposes.</span></span> <span data-ttu-id="466ce-194">연결 통신 모델을 사용하면 Windows 통신 재단과 같은 연결 기반 API를 사용한 개발자에게 익숙할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-194">Using the Connections communication model will be familiar to developers who have used connection-based APIs such as Windows Communication Foundation.</span></span>

<span data-ttu-id="466ce-195">허브는 클라이언트와 서버가 서로 직접 메서드를 호출할 수 있도록 하는 연결 API를 기반으로 구축된 보다 높은 수준의 파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-195">A Hub is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span> <span data-ttu-id="466ce-196">SignalR은 마치 마술처럼 시스템 경계를 넘어 디스패치를 처리하므로 클라이언트가 로컬 메서드처럼 쉽게 서버에서 메서드를 호출할 수 있으며 그 반대의 경우도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-196">SignalR handles the dispatching across machine boundaries as if by magic, allowing clients to call methods on the server as easily as local methods, and vice versa.</span></span> <span data-ttu-id="466ce-197">허브 통신 모델을 사용하면 .NET Remoting과 같은 원격 호출 API를 사용한 개발자에게 익숙할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-197">Using the Hubs communication model will be familiar to developers who have used remote invocation APIs such as .NET Remoting.</span></span> <span data-ttu-id="466ce-198">또한 Hub를 사용하면 강력하게 입력된 매개 변수를 메서드에 전달하여 모델 바인딩을 활성화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-198">Using a Hub also allows you to pass strongly typed parameters to methods, enabling model binding.</span></span>

### <a name="architecture-diagram"></a><span data-ttu-id="466ce-199">아키텍처 다이어그램</span><span class="sxs-lookup"><span data-stu-id="466ce-199">Architecture diagram</span></span>

<span data-ttu-id="466ce-200">다음 다이어그램에서는 허브, 영구 연결 및 전송에 사용되는 기본 기술 간의 관계를 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-200">The following diagram shows the relationship between Hubs, Persistent Connections, and the underlying technologies used for transports.</span></span>

![API, 전송 및 클라이언트를 보여 주며 SignalR 아키텍처 다이어그램](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a><span data-ttu-id="466ce-202">허브 작동 방식</span><span class="sxs-lookup"><span data-stu-id="466ce-202">How Hubs work</span></span>

<span data-ttu-id="466ce-203">서버 측 코드가 클라이언트에서 메서드를 호출하면 호출할 메서드의 이름과 매개 변수가 포함된 활성 전송을 통해 패킷이 전송됩니다(개체가 메서드 매개 변수로 전송되면 JSON을 사용하여 직렬화됩니다).</span><span class="sxs-lookup"><span data-stu-id="466ce-203">When server-side code calls a method on the client, a packet is sent across the active transport that contains the name and parameters of the method to be called (when an object is sent as a method parameter, it is serialized using JSON).</span></span> <span data-ttu-id="466ce-204">그런 다음 클라이언트는 메서드 이름을 클라이언트 쪽 코드에 정의된 메서드와 일치시다.</span><span class="sxs-lookup"><span data-stu-id="466ce-204">The client then matches the method name to methods defined in client-side code.</span></span> <span data-ttu-id="466ce-205">일치하는 경우 클라이언트 메서드는 직렬화된 매개 변수 데이터를 사용하여 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-205">If there is a match, the client method will be executed using the deserialized parameter data.</span></span>

<span data-ttu-id="466ce-206">메서드 호출은 [Fiddler와](http://fiddler2.com/) 같은 도구를 사용하여 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-206">The method call can be monitored using tools like [Fiddler.](http://fiddler2.com/)</span></span> <span data-ttu-id="466ce-207">다음 이미지는 Fiddler의 로그 창에서 SignalR 서버에서 웹 브라우저 클라이언트로 전송된 메서드 호출을 보여 주며,</span><span class="sxs-lookup"><span data-stu-id="466ce-207">The following image shows a method call sent from a SignalR server to a web browser client in the Logs pane of Fiddler.</span></span> <span data-ttu-id="466ce-208">메서드 호출은 호출된 `MoveShapeHub`허브에서 전송되고 있으며 호출되는 `updateShape`메서드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-208">The method call is being sent from a hub called `MoveShapeHub`, and the method being invoked is called `updateShape`.</span></span>

![SignalR 트래픽을 보여주는 피들러 로그의 보기](introduction-to-signalr/_static/image6.png)

<span data-ttu-id="466ce-210">이 예제에서는 허브 이름이 `H` 매개 변수로 식별됩니다. 메서드 이름은 `M` 매개 변수로 식별되고 메서드로 전송되는 데이터는 `A` 매개 변수로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-210">In this example, the hub name is identified with the `H` parameter; the method name is identified with the `M` parameter, and the data being sent to the method is identified with the `A` parameter.</span></span> <span data-ttu-id="466ce-211">이 메시지를 생성한 응용 프로그램은 [고주파 실시간](tutorial-high-frequency-realtime-with-signalr.md) 자습서에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-211">The application that generated this message is created in the [High-Frequency Realtime](tutorial-high-frequency-realtime-with-signalr.md) tutorial.</span></span>

### <a name="choosing-a-communication-model"></a><span data-ttu-id="466ce-212">통신 모델 선택</span><span class="sxs-lookup"><span data-stu-id="466ce-212">Choosing a communication model</span></span>

<span data-ttu-id="466ce-213">대부분의 응용 프로그램은 허브 API를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-213">Most applications should use the Hubs API.</span></span> <span data-ttu-id="466ce-214">연결 API는 다음과 같은 상황에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-214">The Connections API could be used in the following circumstances:</span></span>

- <span data-ttu-id="466ce-215">전송된 실제 메시지의 형식을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-215">The format of the actual message sent needs to be specified.</span></span>
- <span data-ttu-id="466ce-216">개발자는 원격 호출 모델보다는 메시징 및 디스패치 모델로 작업하는 것을 선호합니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-216">The developer prefers to work with a messaging and dispatching model rather than a remote invocation model.</span></span>
- <span data-ttu-id="466ce-217">메시징 모델을 사용하는 기존 응용 프로그램이 SignalR을 사용하도록 포팅되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="466ce-217">An existing application that uses a messaging model is being ported to use SignalR.</span></span>
