---
uid: signalr/overview/getting-started/introduction-to-signalr
title: SignalR 소개 | Microsoft Docs
author: bradygaster
description: 이 문서에서는 SignalR 무엇 이며, 만들려는 솔루션 중 일부를 설명 합니다.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 76e8fd03292eafa4b0b579ee1746fb54b57ac66b
ms.sourcegitcommit: 45754124123403520b9fa2e706a4d1292494159b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643679"
---
# <a name="introduction-to-signalr"></a><span data-ttu-id="051ae-103">SignalR 소개</span><span class="sxs-lookup"><span data-stu-id="051ae-103">Introduction to SignalR</span></span>

<span data-ttu-id="051ae-104">[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="051ae-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="051ae-105">이 문서에서는 SignalR 무엇 이며, 만들려는 솔루션 중 일부를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-105">This article describes what SignalR is, and some of the solutions it was designed to create.</span></span> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="051ae-106">질문 및 설명</span><span class="sxs-lookup"><span data-stu-id="051ae-106">Questions and comments</span></span>
> 
> <span data-ttu-id="051ae-107">이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="051ae-107">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="051ae-108">자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-108">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr).</span></span>

## <a name="what-is-signalr"></a><span data-ttu-id="051ae-109">SignalR 란?</span><span class="sxs-lookup"><span data-stu-id="051ae-109">What is SignalR?</span></span>

<span data-ttu-id="051ae-110">ASP.NET SignalR는 응용 프로그램에 실시간 웹 기능을 추가 하는 프로세스를 간소화 하는 ASP.NET 개발자를 위한 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-110">ASP.NET SignalR is a library for ASP.NET developers that simplifies the process of adding real-time web functionality to applications.</span></span> <span data-ttu-id="051ae-111">실시간 웹 기능은 서버가 클라이언트에서 새 데이터를 요청할 때까지 대기 하는 것이 아니라 서버 코드에서 연결 된 클라이언트에 콘텐츠를 즉시 푸시하는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-111">Real-time web functionality is the ability to have server code push content to connected clients instantly as it becomes available, rather than having the server wait for a client to request new data.</span></span>

<span data-ttu-id="051ae-112">SignalR는 ASP.NET 응용 프로그램에 "실시간" 웹 기능을 추가 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-112">SignalR can be used to add any sort of "real-time" web functionality to your ASP.NET application.</span></span> <span data-ttu-id="051ae-113">채팅은 종종 예로 사용 되지만 전체적으로 더 많은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-113">While chat is often used as an example, you can do a whole lot more.</span></span> <span data-ttu-id="051ae-114">사용자가 새 데이터를 볼 수 있도록 웹 페이지를 새로 고치거 나 페이지에서 [긴 폴링을](http://en.wikipedia.org/wiki/Push_technology#Long_polling) 구현 하 여 새 데이터를 검색 하는 경우에는 SignalR을 사용 하는 후보가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-114">Any time a user refreshes a web page to see new data, or the page implements [long polling](http://en.wikipedia.org/wiki/Push_technology#Long_polling) to retrieve new data, it is a candidate for using SignalR.</span></span> <span data-ttu-id="051ae-115">예를 들면 대시보드 및 모니터링 응용 프로그램, 공동 작업 응용 프로그램 (예: 문서를 동시에 편집), 작업 진행률 업데이트 및 실시간 양식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-115">Examples include dashboards and monitoring applications, collaborative applications (such as simultaneous editing of documents), job progress updates, and real-time forms.</span></span>

<span data-ttu-id="051ae-116">또한 SignalR를 사용 하면 실시간 게임과 같이 서버에서 빈도가 높은 업데이트가 필요한 웹 응용 프로그램을 완전히 새로운 형식으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-116">SignalR also enables completely new types of web applications that require high frequency updates from the server, for example, real-time gaming.</span></span>

<span data-ttu-id="051ae-117">SignalR는 서버 쪽 .NET 코드에서 클라이언트 브라우저 (및 다른 클라이언트 플랫폼)의 JavaScript 함수를 호출 하는 서버-클라이언트 원격 프로시저 호출 (RPC)을 만들기 위한 간단한 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-117">SignalR provides a simple API for creating server-to-client remote procedure calls (RPC) that call JavaScript functions in client browsers (and other client platforms) from server-side .NET code.</span></span> <span data-ttu-id="051ae-118">SignalR에는 연결 관리 (예를 들어, 이벤트 연결 및 연결 끊기), 연결 그룹화를 위한 API도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-118">SignalR also includes API for connection management (for instance, connect and disconnect events), and grouping connections.</span></span>

![SignalR를 사용 하 여 메서드 호출](introduction-to-signalr/_static/image1.png)

<span data-ttu-id="051ae-120">SignalR은 연결 관리를 자동으로 처리하며, 대화방처럼 메시지를 연결된 모든 클라이언트에 동시에 브로드캐스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-120">SignalR handles connection management automatically, and lets you broadcast messages to all connected clients simultaneously, like a chat room.</span></span> <span data-ttu-id="051ae-121">메시지를 특정 클라이언트에 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-121">You can also send messages to specific clients.</span></span> <span data-ttu-id="051ae-122">클라이언트와 서버 간의 연결은 기존 HTTP 연결과 달리 영구적이며, 각 통신에 대해 다시 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-122">The connection between the client and server is persistent, unlike a classic HTTP connection, which is re-established for each communication.</span></span>

<span data-ttu-id="051ae-123">SignalR는 "서버 푸시" 기능을 지원 합니다 .이 기능은 서버 코드가 현재 웹에서 자주 사용 하는 요청-응답 모델 대신 RPC (원격 프로시저 호출)를 사용 하 여 브라우저에서 클라이언트 코드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-123">SignalR supports "server push" functionality, in which server code can call out to client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model common on the web today.</span></span>

<span data-ttu-id="051ae-124">SignalR 응용 프로그램은 기본 제공 및 타사 스케일 아웃 공급자를 사용 하 여 수천 개의 클라이언트로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-124">SignalR applications can scale out to thousands of clients using built-in, and third-party scale-out providers.</span></span>

<span data-ttu-id="051ae-125">기본 제공 공급자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-125">Built-in providers include:</span></span>
* [<span data-ttu-id="051ae-126">Service Bus</span><span class="sxs-lookup"><span data-stu-id="051ae-126">Service Bus</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [<span data-ttu-id="051ae-127">SQL Server</span><span class="sxs-lookup"><span data-stu-id="051ae-127">SQL Server</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [<span data-ttu-id="051ae-128">Redis</span><span class="sxs-lookup"><span data-stu-id="051ae-128">Redis</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

<span data-ttu-id="051ae-129">타사 공급자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-129">Third-party providers include:</span></span>
* <span data-ttu-id="051ae-130">[NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).</span><span class="sxs-lookup"><span data-stu-id="051ae-130">[NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).</span></span>

<span data-ttu-id="051ae-131">SignalR는 [GitHub](https://github.com/signalr)를 통해 액세스할 수 있는 오픈 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-131">SignalR is open-source, accessible through [GitHub](https://github.com/signalr).</span></span>

## <a name="signalr-and-websocket"></a><span data-ttu-id="051ae-132">SignalR 및 WebSocket</span><span class="sxs-lookup"><span data-stu-id="051ae-132">SignalR and WebSocket</span></span>

<span data-ttu-id="051ae-133">SignalR는 사용 가능한 경우 새 WebSocket 전송을 사용 하 고 필요한 경우 이전 전송으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-133">SignalR uses the new WebSocket transport where available and falls back to older transports where necessary.</span></span> <span data-ttu-id="051ae-134">WebSocket을 직접 사용 하 여 앱을 직접 작성할 수 있지만 SignalR를 사용 하면 구현 해야 할 많은 추가 기능이 이미 수행 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-134">While you could certainly write your app using WebSocket directly, using SignalR means that a lot of the extra functionality you would need to implement is already done for you.</span></span> <span data-ttu-id="051ae-135">가장 중요 한 점은 이전 클라이언트에 대 한 별도의 코드 경로를 만드는 방법에 대해 걱정할 필요 없이 WebSocket을 활용 하기 위해 앱을 코딩할 수 있음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-135">Most importantly, this means that you can code your app to take advantage of WebSocket without having to worry about creating a separate code path for older clients.</span></span> <span data-ttu-id="051ae-136">또한 SignalR는 websocket에 대 한 업데이트에 대해 걱정 하지 않아도 됩니다. SignalR가 기본 전송의 변경을 지원 하도록 업데이트 되므로 응용 프로그램에 WebSocket 버전 간에 일관 된 인터페이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-136">SignalR also shields you from having to worry about updates to WebSocket, since SignalR is updated to support changes in the underlying transport, providing your application a consistent interface across versions of WebSocket.</span></span>

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a><span data-ttu-id="051ae-137">전송 및 대체</span><span class="sxs-lookup"><span data-stu-id="051ae-137">Transports and fallbacks</span></span>

<span data-ttu-id="051ae-138">SignalR는 클라이언트와 서버 간의 실시간 작업을 수행 하는 데 필요한 일부 전송에 대 한 추상화입니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-138">SignalR is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="051ae-139">SignalR는 가능한 경우 WebSocket 연결을 설정 하려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-139">SignalR first attempts to establish a WebSocket connection if possible.</span></span> <span data-ttu-id="051ae-140">WebSocket은 다음을 포함 하 여 SignalR에 대 한 최적의 전송입니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-140">WebSocket is the optimal transport for SignalR because it has:</span></span>

* <span data-ttu-id="051ae-141">서버 메모리를 가장 효율적으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-141">The most efficient use of server memory.</span></span>
* <span data-ttu-id="051ae-142">가장 짧은 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-142">The lowest latency.</span></span>
* <span data-ttu-id="051ae-143">클라이언트와 서버 간의 전이중 통신과 같은 가장 기본적인 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-143">The most underlying features, such as full duplex communication between client and server.</span></span>
* <span data-ttu-id="051ae-144">가장 엄격한 요구 사항은 WebSocket에 서버가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-144">The most stringent requirements, WebSocket requires the server:</span></span>
  * <span data-ttu-id="051ae-145">Windows Server 2012 또는 Windows 8에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-145">Run on Windows Server 2012 or Windows 8.</span></span>
  * <span data-ttu-id="051ae-146">.NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="051ae-146">.NET Framework 4.5.</span></span>

<span data-ttu-id="051ae-147">이러한 요구 사항이 충족 되지 않으면 SignalR는 다른 전송을 사용 하 여 연결을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-147">If these requirements are not met, SignalR attempts to use other transports to make its connections.</span></span>

### <a name="html-5-transports"></a><span data-ttu-id="051ae-148">HTML 5 전송</span><span class="sxs-lookup"><span data-stu-id="051ae-148">HTML 5 transports</span></span>

<span data-ttu-id="051ae-149">이러한 전송은 [HTML 5](http://en.wikipedia.org/wiki/HTML5)에 대 한 지원에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-149">These transports depend on support for [HTML 5](http://en.wikipedia.org/wiki/HTML5).</span></span> <span data-ttu-id="051ae-150">클라이언트 브라우저에서 HTML 5 표준을 지원 하지 않는 경우 이전 전송이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-150">If the client browser does not support the HTML 5 standard, older transports will be used.</span></span>

- <span data-ttu-id="051ae-151">**Websocket** (서버와 브라우저가 모두 websocket을 지원할 수 있음을 나타냄).</span><span class="sxs-lookup"><span data-stu-id="051ae-151">**WebSocket** (if both the server and browser indicate they can support Websocket).</span></span> <span data-ttu-id="051ae-152">WebSocket은 클라이언트와 서버 간에 진정한 영구 양방향 연결을 설정 하는 유일한 전송입니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-152">WebSocket is the only transport that establishes a true persistent, two-way connection between client and server.</span></span> <span data-ttu-id="051ae-153">그러나 WebSocket에는 가장 엄격한 요구 사항이 있습니다. 최신 버전의 Microsoft Internet Explorer, Google Chrome 및 Mozilla Firefox 에서만 완전히 지원 되며 Opera 및 Safari와 같은 다른 브라우저에서는 부분 구현이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-153">However, WebSocket also has the most stringent requirements; it is fully supported only in the latest versions of Microsoft Internet Explorer, Google Chrome, and Mozilla Firefox, and only has a partial implementation in other browsers such as Opera and Safari.</span></span>
- <span data-ttu-id="051ae-154">**서버에서 이벤트를 보냈습니다**(브라우저에서 서버 전송 이벤트를 지 원하는 경우 기본적으로 Internet Explorer를 제외한 모든 브라우저).</span><span class="sxs-lookup"><span data-stu-id="051ae-154">**Server Sent Events**, also known as EventSource (if the browser supports Server Sent Events, which is basically all browsers except Internet Explorer.)</span></span>

### <a name="comet-transports"></a><span data-ttu-id="051ae-155">Comet 전송</span><span class="sxs-lookup"><span data-stu-id="051ae-155">Comet transports</span></span>

<span data-ttu-id="051ae-156">다음 전송은 [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) 웹 응용 프로그램 모델을 기반으로 합니다 .이 모델에서는 브라우저 또는 다른 클라이언트에서 장기 보유 HTTP 요청을 유지 관리 하며,이를 통해 클라이언트는 특정 클라이언트를 요청 하지 않고 클라이언트에 데이터를 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-156">The following transports are based on the [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) web application model, in which a browser or other client maintains a long-held HTTP request, which the server can use to push data to the client without the client specifically requesting it.</span></span>

- <span data-ttu-id="051ae-157">**영원히 Frame** (Internet Explorer에만 해당).</span><span class="sxs-lookup"><span data-stu-id="051ae-157">**Forever Frame** (for Internet Explorer only).</span></span> <span data-ttu-id="051ae-158">영원히 Frame은 서버의 끝점에 대 한 요청을 완료 하지 않는 숨겨진 IFrame을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-158">Forever Frame creates a hidden IFrame which makes a request to an endpoint on the server that does not complete.</span></span> <span data-ttu-id="051ae-159">그런 다음 서버는 즉시 실행 되는 클라이언트로 스크립트를 지속적으로 전송 하 여 서버에서 클라이언트로의 단방향 실시간 연결을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-159">The server then continually sends script to the client which is immediately executed, providing a one-way realtime connection from server to client.</span></span> <span data-ttu-id="051ae-160">클라이언트에서 서버로의 연결에서는 서버와 클라이언트 간의 별도 연결을 사용 하 고 표준 HTTP 요청과 마찬가지로 전송 해야 하는 각 데이터 조각에 대해 새 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-160">The connection from client to server uses a separate connection from the server to client connection, and like a standard HTTP request, a new connection is created for each piece of data that needs to be sent.</span></span>
- <span data-ttu-id="051ae-161">**Ajax 긴 폴링**.</span><span class="sxs-lookup"><span data-stu-id="051ae-161">**Ajax long polling**.</span></span> <span data-ttu-id="051ae-162">Long 폴링은 영구 연결을 만들지 않고 대신 서버가 응답할 때까지 열린 상태로 유지 되는 요청을 사용 하 여 서버를 폴링합니다. 그러면 연결이 닫히고 새 연결이 즉시 요청 됩니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-162">Long polling does not create a persistent connection, but instead polls the server with a request that stays open until the server responds, at which point the connection closes, and a new connection is requested immediately.</span></span> <span data-ttu-id="051ae-163">연결을 다시 설정 하는 동안 약간의 대기 시간이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-163">This may introduce some latency while the connection resets.</span></span>

<span data-ttu-id="051ae-164">구성에서 지원 되는 전송에 대 한 자세한 내용은 [지원 되는 플랫폼](supported-platforms.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="051ae-164">For more information on what transports are supported under which configurations, see [Supported Platforms](supported-platforms.md).</span></span>

### <a name="transport-selection-process"></a><span data-ttu-id="051ae-165">전송 선택 프로세스</span><span class="sxs-lookup"><span data-stu-id="051ae-165">Transport selection process</span></span>

<span data-ttu-id="051ae-166">다음 목록에서는 SignalR에서 사용할 전송을 결정 하는 데 사용 하는 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-166">The following list shows the steps that SignalR uses to decide which transport to use.</span></span>

1. <span data-ttu-id="051ae-167">브라우저가 Internet Explorer 8이 하 이면 긴 폴링이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-167">If the browser is Internet Explorer 8 or earlier, Long Polling is used.</span></span>
2. <span data-ttu-id="051ae-168">JSONP가 구성 된 경우 (즉, `jsonp` 연결이 시작 될 때 매개 변수가로 설정 된 경우 `true` ) 긴 폴링이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-168">If JSONP is configured (that is, the `jsonp` parameter is set to `true` when the connection is started), Long Polling is used.</span></span>
3. <span data-ttu-id="051ae-169">도메인 간 연결이 설정 되는 경우 (즉, SignalR 끝점이 호스팅 페이지와 동일한 도메인에 있지 않은 경우) 다음 조건을 충족 하는 경우 WebSocket이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-169">If a cross-domain connection is being made (that is, if the SignalR endpoint is not in the same domain as the hosting page), then WebSocket will be used if the following criteria are met:</span></span>

   - <span data-ttu-id="051ae-170">클라이언트는 CORS (크로스-원본 자원 공유)를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-170">The client supports CORS (Cross-Origin Resource Sharing).</span></span> <span data-ttu-id="051ae-171">CORS를 지 원하는 클라이언트에 대 한 자세한 내용은 [caniuse.com에서 cors](http://www.caniuse.com/CORS)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="051ae-171">For details on which clients support CORS, see [CORS at caniuse.com](http://www.caniuse.com/CORS).</span></span>
   - <span data-ttu-id="051ae-172">클라이언트가 WebSocket을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-172">The client supports WebSocket</span></span>
   - <span data-ttu-id="051ae-173">서버에서 WebSocket을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-173">The server supports WebSocket</span></span>

     <span data-ttu-id="051ae-174">이러한 조건 중 하나라도 충족 되지 않으면 긴 폴링이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-174">If any of these criteria are not met, Long Polling will be used.</span></span> <span data-ttu-id="051ae-175">도메인 간 연결에 대 한 자세한 내용은 [도메인 간 연결을 설정 하는 방법](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="051ae-175">For more information on cross-domain connections, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>
4. <span data-ttu-id="051ae-176">JSONP가 구성 되지 않은 경우 연결이 도메인이 아닌 경우 클라이언트와 서버에서 모두 지 원하는 경우 WebSocket이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-176">If JSONP is not configured and the connection is not cross-domain, WebSocket will be used if both the client and server support it.</span></span>
5. <span data-ttu-id="051ae-177">클라이언트나 서버에서 WebSocket을 지원 하지 않는 경우 사용할 수 있는 경우 서버에서 보낸 이벤트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-177">If either the client or server do not support WebSocket, Server Sent Events is used if it is available.</span></span>
6. <span data-ttu-id="051ae-178">서버에서 보낸 이벤트를 사용할 수 없는 경우 영원히 프레임을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-178">If Server Sent Events is not available, Forever Frame is attempted.</span></span>
7. <span data-ttu-id="051ae-179">계속 해 서 프레임에 오류가 발생 하면 긴 폴링이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-179">If Forever Frame fails, Long Polling is used.</span></span>

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a><span data-ttu-id="051ae-180">전송 모니터링</span><span class="sxs-lookup"><span data-stu-id="051ae-180">Monitoring transports</span></span>

<span data-ttu-id="051ae-181">허브에서 로깅을 사용 하도록 설정 하 고 브라우저에서 콘솔 창을 열어 응용 프로그램에서 사용 하는 전송을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-181">You can determine what transport your application is using by enabling logging on your hub, and opening the console window in your browser.</span></span>

<span data-ttu-id="051ae-182">브라우저에서 허브 이벤트에 대 한 로깅을 사용 하도록 설정 하려면 클라이언트 응용 프로그램에 다음 명령을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-182">To enable logging for your hub's events in a browser, add the following command to your client application:</span></span>

`$.connection.hub.logging = true;`

- <span data-ttu-id="051ae-183">Internet Explorer에서 F12 키를 눌러 개발자 도구를 열고 콘솔 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-183">In Internet Explorer, open the developer tools by pressing F12, and click the Console tab.</span></span>

    ![Microsoft Internet Explorer의 콘솔](introduction-to-signalr/_static/image2.png)
- <span data-ttu-id="051ae-185">Chrome에서 Ctrl + Shift + J를 눌러 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-185">In Chrome, open the console by pressing Ctrl+Shift+J.</span></span>

    ![Google Chrome의 콘솔](introduction-to-signalr/_static/image3.png)

<span data-ttu-id="051ae-187">콘솔 열기 및 로깅을 사용 하도록 설정 하면 SignalR에서 어떤 전송을 사용 하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-187">With the console open and logging enabled, you'll be able to see which transport is being used by SignalR.</span></span>

![WebSocket 전송을 보여 주는 Internet Explorer의 콘솔](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a><span data-ttu-id="051ae-189">전송 지정</span><span class="sxs-lookup"><span data-stu-id="051ae-189">Specifying a transport</span></span>

<span data-ttu-id="051ae-190">전송 협상은 특정 시간 및 클라이언트/서버 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-190">Negotiating a transport takes a certain amount of time and client/server resources.</span></span> <span data-ttu-id="051ae-191">클라이언트 기능을 알고 있는 경우 클라이언트 연결을 시작할 때 전송을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-191">If the client capabilities are known, then a transport can be specified when the client connection is started.</span></span> <span data-ttu-id="051ae-192">다음 코드 조각에서는 Ajax 긴 폴링 전송을 사용 하 여 연결을 시작 하는 방법을 보여 줍니다. 클라이언트에서 다른 프로토콜을 지원 하지 않는 것으로 알려진 경우에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-192">The following code snippet demonstrates starting a connection using the Ajax Long Polling transport, as would be used if it was known that the client did not support any other protocol:</span></span>

`connection.start({ transport: 'longPolling' });`

<span data-ttu-id="051ae-193">클라이언트가 특정 전송을 순서 대로 시도 하도록 하려면 대체 (fallback) 순서를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-193">You can specify a fallback order if you want a client to try specific transports in order.</span></span> <span data-ttu-id="051ae-194">다음 코드 조각에서는 WebSocket을 시도 하 고 실패 하 여 긴 폴링으로 직접 이동 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-194">The following code snippet demonstrates trying WebSocket, and failing that, going directly to Long Polling.</span></span>

`connection.start({ transport: ['webSockets','longPolling'] });`

<span data-ttu-id="051ae-195">전송을 지정 하는 문자열 상수는 다음과 같이 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-195">The string constants for specifying transports are defined as follows:</span></span>

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a><span data-ttu-id="051ae-196">연결 및 허브</span><span class="sxs-lookup"><span data-stu-id="051ae-196">Connections and Hubs</span></span>

<span data-ttu-id="051ae-197">SignalR API에는 클라이언트와 서버 간 통신을 위한 두 가지 모델 (영구 연결 및 허브)이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-197">The SignalR API contains two models for communicating between clients and servers: Persistent Connections and Hubs.</span></span>

<span data-ttu-id="051ae-198">연결은 단일 받는 사람, 그룹화 또는 브로드캐스트 메시지를 보내기 위한 간단한 끝점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-198">A Connection represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="051ae-199">PersistentConnection 클래스를 사용 하 여 .NET 코드에 표시 된 영구 연결 API를 통해 개발자는 SignalR가 노출 하는 하위 수준 통신 프로토콜에 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-199">The Persistent Connection API (represented in .NET code by the PersistentConnection class) gives the developer direct access to the low-level communication protocol that SignalR exposes.</span></span> <span data-ttu-id="051ae-200">연결 통신 모델 사용은 Windows Communication Foundation와 같은 연결 기반 Api를 사용 하는 개발자에 게 친숙 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-200">Using the Connections communication model will be familiar to developers who have used connection-based APIs such as Windows Communication Foundation.</span></span>

<span data-ttu-id="051ae-201">허브는 클라이언트와 서버에서 직접 메서드를 호출할 수 있도록 하는 연결 API를 기반으로 하는 더 높은 수준의 파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-201">A Hub is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span> <span data-ttu-id="051ae-202">SignalR는 클라이언트에서 서버에 대 한 메서드를 로컬 메서드로 호출할 수 있도록 하는 것 처럼 컴퓨터 경계 간 디스패치를 처리 하 고 그 반대의 경우도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-202">SignalR handles the dispatching across machine boundaries as if by magic, allowing clients to call methods on the server as easily as local methods, and vice versa.</span></span> <span data-ttu-id="051ae-203">허브 통신 모델 사용은 .NET Remoting과 같은 원격 호출 Api를 사용 하는 개발자에 게 친숙 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-203">Using the Hubs communication model will be familiar to developers who have used remote invocation APIs such as .NET Remoting.</span></span> <span data-ttu-id="051ae-204">또한 허브를 사용 하면 강력한 형식의 매개 변수를 메서드에 전달 하 여 모델 바인딩을 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-204">Using a Hub also allows you to pass strongly typed parameters to methods, enabling model binding.</span></span>

### <a name="architecture-diagram"></a><span data-ttu-id="051ae-205">아키텍처 다이어그램</span><span class="sxs-lookup"><span data-stu-id="051ae-205">Architecture diagram</span></span>

<span data-ttu-id="051ae-206">다음 다이어그램에서는 허브, 영구 연결 및 전송에 사용 되는 기본 기술 간의 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-206">The following diagram shows the relationship between Hubs, Persistent Connections, and the underlying technologies used for transports.</span></span>

![Api, 전송 및 클라이언트를 보여 주는 SignalR 아키텍처 다이어그램](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a><span data-ttu-id="051ae-208">허브 작동 방법</span><span class="sxs-lookup"><span data-stu-id="051ae-208">How Hubs work</span></span>

<span data-ttu-id="051ae-209">서버 쪽 코드에서 클라이언트의 메서드를 호출 하면 호출 될 메서드의 이름 및 매개 변수를 포함 하는 활성 전송에서 패킷이 전송 됩니다 (개체를 메서드 매개 변수로 보냈을 때 JSON을 사용 하 여 serialize).</span><span class="sxs-lookup"><span data-stu-id="051ae-209">When server-side code calls a method on the client, a packet is sent across the active transport that contains the name and parameters of the method to be called (when an object is sent as a method parameter, it is serialized using JSON).</span></span> <span data-ttu-id="051ae-210">클라이언트는 메서드 이름과 클라이언트 쪽 코드에 정의 된 메서드를 일치 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-210">The client then matches the method name to methods defined in client-side code.</span></span> <span data-ttu-id="051ae-211">일치 하는 항목이 있는 경우 클라이언트 메서드는 deserialize 된 매개 변수 데이터를 사용 하 여 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-211">If there is a match, the client method will be executed using the deserialized parameter data.</span></span>

<span data-ttu-id="051ae-212">Fiddler와 같은 도구를 사용 하 여 메서드 호출을 모니터링할 수 있습니다 [.](http://fiddler2.com/)</span><span class="sxs-lookup"><span data-stu-id="051ae-212">The method call can be monitored using tools like [Fiddler.](http://fiddler2.com/)</span></span> <span data-ttu-id="051ae-213">다음 이미지는 Fiddler의 로그 창에서 SignalR 서버에서 웹 브라우저 클라이언트로 전송 된 메서드 호출을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-213">The following image shows a method call sent from a SignalR server to a web browser client in the Logs pane of Fiddler.</span></span> <span data-ttu-id="051ae-214">호출 된 허브에서 메서드 호출을 보내고 `MoveShapeHub` 호출 되는 메서드를 호출 합니다 `updateShape` .</span><span class="sxs-lookup"><span data-stu-id="051ae-214">The method call is being sent from a hub called `MoveShapeHub`, and the method being invoked is called `updateShape`.</span></span>

![SignalR 트래픽을 보여 주는 Fiddler 로그 보기](introduction-to-signalr/_static/image6.png)

<span data-ttu-id="051ae-216">이 예제에서 허브 이름은 `H` 매개 변수로 식별 됩니다. 메서드 이름은 `M` 매개 변수로 식별 되며 메서드로 전송 되는 데이터는 매개 변수를 사용 하 여 식별 됩니다 `A` .</span><span class="sxs-lookup"><span data-stu-id="051ae-216">In this example, the hub name is identified with the `H` parameter; the method name is identified with the `M` parameter, and the data being sent to the method is identified with the `A` parameter.</span></span> <span data-ttu-id="051ae-217">이 메시지를 생성 한 응용 프로그램은 [빈도가 높은 실시간](tutorial-high-frequency-realtime-with-signalr.md) 자습서에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-217">The application that generated this message is created in the [High-Frequency Realtime](tutorial-high-frequency-realtime-with-signalr.md) tutorial.</span></span>

### <a name="choosing-a-communication-model"></a><span data-ttu-id="051ae-218">통신 모델 선택</span><span class="sxs-lookup"><span data-stu-id="051ae-218">Choosing a communication model</span></span>

<span data-ttu-id="051ae-219">대부분의 응용 프로그램은 허브 API를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-219">Most applications should use the Hubs API.</span></span> <span data-ttu-id="051ae-220">연결 API는 다음과 같은 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-220">The Connections API could be used in the following circumstances:</span></span>

- <span data-ttu-id="051ae-221">보낸 실제 메시지의 형식을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-221">The format of the actual message sent needs to be specified.</span></span>
- <span data-ttu-id="051ae-222">개발자는 원격 호출 모델 대신 메시징 및 디스패치 모델을 사용 하는 것이 선호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-222">The developer prefers to work with a messaging and dispatching model rather than a remote invocation model.</span></span>
- <span data-ttu-id="051ae-223">메시징 모델을 사용 하는 기존 응용 프로그램은 SignalR를 사용 하도록 포팅 됩니다.</span><span class="sxs-lookup"><span data-stu-id="051ae-223">An existing application that uses a messaging model is being ported to use SignalR.</span></span>
