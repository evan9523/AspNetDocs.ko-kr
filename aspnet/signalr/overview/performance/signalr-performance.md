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
# <a name="signalr-performance"></a><span data-ttu-id="d1191-103">SignalR 성능</span><span class="sxs-lookup"><span data-stu-id="d1191-103">SignalR Performance</span></span>

<span data-ttu-id="d1191-104">로 [패트릭 플레처](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="d1191-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="d1191-105">이 항목에서는 SignalR 응용 프로그램의 성능을 설계, 측정 및 개선하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="d1191-106">이 항목에 사용된 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="d1191-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="d1191-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d1191-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="d1191-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="d1191-108">.NET 4.5</span></span>
> - <span data-ttu-id="d1191-109">시그널R 버전 2</span><span class="sxs-lookup"><span data-stu-id="d1191-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="d1191-110">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="d1191-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="d1191-111">이전 버전의 SignalR에 대한 자세한 내용은 [SignalR 이전 버전을](../older-versions/index.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d1191-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="d1191-112">질문 및 의견</span><span class="sxs-lookup"><span data-stu-id="d1191-112">Questions and comments</span></span>
>
> <span data-ttu-id="d1191-113">이 자습서를 어떻게 좋아했는지, 그리고 페이지 하단의 댓글에서 개선할 수 있는 내용에 대한 피드백을 남겨주세요.</span><span class="sxs-lookup"><span data-stu-id="d1191-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="d1191-114">당신은 튜토리얼과 직접 관련이없는 질문이있는 경우, 당신은 [ASP.NET SignalR 포럼에](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 게시하거나 [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="d1191-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="d1191-115">SignalR 성능 및 확장에 대한 최근 프레젠테이션은 [ASP.NET SignalR로 실시간 웹 크기 조정을](https://channel9.msdn.com/Events/Build/2013/3-502)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d1191-115">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="d1191-116">이 항목에는 다음과 같은 섹션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="d1191-117">디자인 고려 사항</span><span class="sxs-lookup"><span data-stu-id="d1191-117">Design considerations</span></span>](#design)
- [<span data-ttu-id="d1191-118">SignalR 서버의 성능 조정</span><span class="sxs-lookup"><span data-stu-id="d1191-118">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="d1191-119">성능 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d1191-119">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="d1191-120">SignalR 성능 카운터 사용</span><span class="sxs-lookup"><span data-stu-id="d1191-120">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="d1191-121">다른 성능 카운터 사용</span><span class="sxs-lookup"><span data-stu-id="d1191-121">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="d1191-122">기타 리소스</span><span class="sxs-lookup"><span data-stu-id="d1191-122">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="d1191-123">디자인 고려 사항</span><span class="sxs-lookup"><span data-stu-id="d1191-123">Design considerations</span></span>

<span data-ttu-id="d1191-124">이 섹션에서는 SignalR 응용 프로그램을 디자인하는 동안 구현할 수 있는 패턴에 대해 설명하여 불필요한 네트워크 트래픽을 생성하여 성능이 저하되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-124">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="d1191-125">메시지 빈도 제한</span><span class="sxs-lookup"><span data-stu-id="d1191-125">Throttling message frequency</span></span>

<span data-ttu-id="d1191-126">실시간 게임 응용 프로그램과 같이 고주파로 메시지를 보내는 응용 프로그램에서도 대부분의 응용 프로그램은 초당 몇 개 이상의 메시지를 보낼 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-126">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="d1191-127">각 클라이언트가 생성하는 트래픽의 양을 줄이기 위해 큐를 구현하고 메시지를 고정 된 속도보다 더 자주 보내지 않는 메시지 루프를 구현 할 수 있습니다 (즉, 해당 시간 간격에 메시지가 있는 경우 매 초마다 특정 수의 메시지가 전송됩니다).</span><span class="sxs-lookup"><span data-stu-id="d1191-127">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="d1191-128">메시지를 클라이언트와 서버 모두에서 특정 속도로 제한하는 샘플 응용 프로그램의 경우 [SignalR을 사용하여 고주파 실시간을](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d1191-128">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="d1191-129">메시지 크기 줄이기</span><span class="sxs-lookup"><span data-stu-id="d1191-129">Reducing message size</span></span>

<span data-ttu-id="d1191-130">직렬화된 개체의 크기를 줄여 SignalR 메시지의 크기를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-130">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="d1191-131">서버 코드에서 전송할 필요가 없는 속성을 포함하는 개체를 보내는 경우 특성을 `JsonIgnore` 사용하여 해당 속성이 직렬화되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-131">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="d1191-132">속성 이름도 메시지에 저장됩니다. 속성의 이름은 특성을 `JsonProperty` 사용하여 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-132">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="d1191-133">다음 코드 샘플에서는 속성이 클라이언트로 전송되는 것을 제외하는 방법과 속성 이름을 줄이는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-133">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="d1191-134">**JsonIgnore 특성을 보여 주는 .NET 서버 코드는 클라이언트로 전송되는 데이터를 제외하고 JsonProperty 특성은 메시지 크기를 줄입니다.**</span><span class="sxs-lookup"><span data-stu-id="d1191-134">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="d1191-135">클라이언트 코드에서 가독성/유지 관리 가능성을 유지하기 위해 메시지를 받은 후 약식 속성 이름을 사용자 친화적인 이름으로 다시 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-135">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="d1191-136">다음 코드 샘플에서는 메시지 계약(매핑)을 정의하고 함수를 `reMap` 사용하여 최적화된 메시지 클래스에 계약을 적용하여 단축된 이름을 더 긴 이름으로 다시 매핑하는 한 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-136">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="d1191-137">**사람이 읽을 수 있는 이름으로 단축된 속성 이름을 다시 매핑하는 클라이언트 측 JavaScript 코드**</span><span class="sxs-lookup"><span data-stu-id="d1191-137">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="d1191-138">동일한 방법을 사용하여 클라이언트에서 서버로 메시지를 줄일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-138">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="d1191-139">메시지 개체의 메모리 사용 공간(즉, 메시지에 사용되는 메모리 양)을 줄이면 성능도 향상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-139">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="d1191-140">예를 들어, 전체 `int` 범위가 필요하지 않은 경우 `short` `byte` 대신 a 또는 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-140">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="d1191-141">메시지는 서버 메모리의 메시지 버스에 저장되므로 메시지 크기를 줄이면 서버 메모리 문제도 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-141">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="d1191-142">SignalR 서버의 성능 조정</span><span class="sxs-lookup"><span data-stu-id="d1191-142">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="d1191-143">다음 구성 설정을 사용하여 SignalR 응용 프로그램에서 더 나은 성능을 위해 서버를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-143">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="d1191-144">ASP.NET 응용 프로그램의 성능을 개선하는 방법에 대한 일반적인 내용은 [성능 ASP.NET 향상을](https://msdn.microsoft.com/library/ff647787.aspx)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d1191-144">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="d1191-145">**시그널R 구성 설정**</span><span class="sxs-lookup"><span data-stu-id="d1191-145">**SignalR configuration settings**</span></span>

- <span data-ttu-id="d1191-146">**DefaultMessageBufferSize**: 기본적으로 SignalR는 연결당 허브당 1000개의 메시지를 메모리에 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-146">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="d1191-147">큰 메시지를 사용 하는 경우 이 값을 줄임으로써 완화 될 수 있는 메모리 문제를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-147">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="d1191-148">이 설정은 ASP.NET `Application_Start` 응용 프로그램의 이벤트 처리기 또는 `Configuration` 자체 호스팅 응용 프로그램의 OWIN 시작 클래스 의 메서드에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-148">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="d1191-149">다음 샘플에서는 사용되는 서버 메모리 양을 줄이기 위해 응용 프로그램의 메모리 공간을 줄이기 위해 이 값을 줄이는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-149">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="d1191-150">**기본 메시지 버퍼 크기를 줄이기 위한 Startup.cs .NET 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="d1191-150">**.NET server code in Startup.cs for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="d1191-151">**IIS 구성 설정**</span><span class="sxs-lookup"><span data-stu-id="d1191-151">**IIS configuration settings**</span></span>

- <span data-ttu-id="d1191-152">**응용 프로그램당 최대 동시 요청:** 동시 IIS 요청 수를 늘리면 요청을 제공하는 데 사용할 수 있는 서버 리소스가 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-152">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="d1191-153">기본값은 5000입니다. 이 설정을 늘리려면 상승된 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-153">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- <span data-ttu-id="d1191-154">**응용 프로그램 풀 큐길이**: Http.sys가 응용 프로그램 풀에 대해 큐에 대기하는 최대 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-154">**ApplicationPool QueueLength**: This is the maximum number of requests that Http.sys queues for the application pool.</span></span> <span data-ttu-id="d1191-155">큐가 가득 차면 새 요청은 503 "서비스 사용 불가" 응답을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-155">When the queue is full, new requests receive a 503 "Service Unavailable" response.</span></span> <span data-ttu-id="d1191-156">기본값은 1000입니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-156">The default value is 1000.</span></span>

    <span data-ttu-id="d1191-157">응용 프로그램을 호스팅하는 응용 프로그램 풀에서 작업자 프로세스의 큐 길이를 줄이면 메모리 리소스가 절약됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-157">Shortening the queue length for the worker process in the application pool hosting your application will conserve memory resources.</span></span> <span data-ttu-id="d1191-158">자세한 내용은 [응용 프로그램 풀 관리, 튜닝 및 구성을](https://technet.microsoft.com/library/cc745955.aspx)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d1191-158">For more information, see [Managing, Tuning, and Configuring Application Pools](https://technet.microsoft.com/library/cc745955.aspx).</span></span>

<span data-ttu-id="d1191-159">**ASP.NET 구성 설정**</span><span class="sxs-lookup"><span data-stu-id="d1191-159">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="d1191-160">이 섹션에는 파일에서 설정할 수 `aspnet.config` 있는 구성 설정이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-160">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="d1191-161">이 파일은 플랫폼에 따라 두 위치 중 하나에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-161">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="d1191-162">SignalR 성능을 향상시킬 수 있는 ASP.NET 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-162">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="d1191-163">**CPU당 최대 동시 요청**: 이 설정을 늘리면 성능 병목 현상이 완화될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-163">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="d1191-164">이 설정을 늘리려면 다음 구성 설정을 `aspnet.config` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-164">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="d1191-165">**요청 대기열 제한**: 총 연결 수가 `maxConcurrentRequestsPerCPU` 설정을 초과하면 ASP.NET 큐를 사용하여 요청을 제한하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-165">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="d1191-166">큐 크기를 늘리려면 `requestQueueLimit` 설정을 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-166">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="d1191-167">이렇게 하려면 다음 구성 설정을 다음(대신) `processModel` `config/machine.config` `aspnet.config`노드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-167">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="d1191-168">성능 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d1191-168">Troubleshooting performance issues</span></span>

<span data-ttu-id="d1191-169">이 섹션에서는 응용 프로그램에서 성능 병목 현상을 찾는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-169">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="d1191-170">웹 소켓이 사용되고 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="d1191-170">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="d1191-171">SignalR은 클라이언트와 서버 간의 통신을 위해 다양한 전송을 사용할 수 있지만 WebSocket은 상당한 성능 이점을 제공하며 클라이언트와 서버가 이를 지원하는 경우 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-171">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="d1191-172">클라이언트와 서버가 WebSocket에 대한 요구 사항을 충족하는지 확인하려면 [전송 및 대체 를](../getting-started/introduction-to-signalr.md#transports)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d1191-172">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="d1191-173">응용 프로그램에서 사용되는 전송을 확인하려면 브라우저 개발자 도구를 사용하고 로그를 검사하여 연결에 사용되는 전송을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-173">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="d1191-174">인터넷 익스플로러 및 크롬에서 브라우저 개발 도구를 사용하는 방법에 대한 자세한 내용은 [전송 및 대체를](../getting-started/introduction-to-signalr.md#transports)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d1191-174">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="d1191-175">SignalR 성능 카운터 사용</span><span class="sxs-lookup"><span data-stu-id="d1191-175">Using SignalR performance counters</span></span>

<span data-ttu-id="d1191-176">이 섹션에서는 `Microsoft.AspNet.SignalR.Utils` 패키지에 있는 SignalR 성능 카운터를 사용하도록 설정하고 사용하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-176">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="d1191-177">시그널러(signalr.exe) 설치</span><span class="sxs-lookup"><span data-stu-id="d1191-177">Installing signalr.exe</span></span>

<span data-ttu-id="d1191-178">SignalR.exe라는 유틸리티를 사용하여 성능 카운터를 서버에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-178">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="d1191-179">이 유틸리티를 설치하려면 다음 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="d1191-179">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="d1191-180">비주얼 스튜디오에서 **솔루션에** > 대한 NuGet 패키지 관리자 관리 도구**NuGet 패키지 관리자를** > **선택합니다.**</span><span class="sxs-lookup"><span data-stu-id="d1191-180">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="d1191-181">**signalr.utils를 검색하고 설치를 선택합니다.**</span><span class="sxs-lookup"><span data-stu-id="d1191-181">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="d1191-182">패키지 설치를 위한 사용권 계약에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-182">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="d1191-183">시그널R.exe에 `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-183">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="d1191-184">SignalR.exe를 가진 성능 카운터 설치</span><span class="sxs-lookup"><span data-stu-id="d1191-184">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="d1191-185">SignalR 성능 카운터를 설치하려면 다음 매개 변수를 사용하여 상승된 명령 프롬프트에서 SignalR.exe를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-185">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="d1191-186">SignalR 성능 카운터를 제거하려면 다음 매개 변수를 사용하여 상승된 명령 프롬프트에서 SignalR.exe를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-186">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="d1191-187">시그널R 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="d1191-187">SignalR Performance counters</span></span>

<span data-ttu-id="d1191-188">유틸리티 패키지는 다음과 같은 성능 카운터를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-188">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="d1191-189">"Total" 카운터는 마지막 응용 프로그램 풀 또는 서버가 다시 시작된 이후의 이벤트 수를 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-189">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="d1191-190">**연결 메트릭**</span><span class="sxs-lookup"><span data-stu-id="d1191-190">**Connection metrics**</span></span>

<span data-ttu-id="d1191-191">다음 메트릭은 발생하는 연결 수명 이벤트를 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-191">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="d1191-192">자세한 내용은 [연결 수명 이벤트 이해 및 처리를](../guide-to-the-api/handling-connection-lifetime-events.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d1191-192">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="d1191-193">**연결된 연결**</span><span class="sxs-lookup"><span data-stu-id="d1191-193">**Connections Connected**</span></span>
- <span data-ttu-id="d1191-194">**연결이 다시 연결됨**</span><span class="sxs-lookup"><span data-stu-id="d1191-194">**Connections Reconnected**</span></span>
- <span data-ttu-id="d1191-195">**연결이 끊어졌습니다.**</span><span class="sxs-lookup"><span data-stu-id="d1191-195">**Connections Disconnected**</span></span>
- <span data-ttu-id="d1191-196">**연결 전류**</span><span class="sxs-lookup"><span data-stu-id="d1191-196">**Connections Current**</span></span>

<span data-ttu-id="d1191-197">**메시지 메트릭**</span><span class="sxs-lookup"><span data-stu-id="d1191-197">**Message metrics**</span></span>

<span data-ttu-id="d1191-198">다음 메트릭은 SignalR에서 생성된 메시지 트래픽을 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-198">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="d1191-199">**수신된 연결 메시지 합계**</span><span class="sxs-lookup"><span data-stu-id="d1191-199">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="d1191-200">**전송된 연결 메시지 총**</span><span class="sxs-lookup"><span data-stu-id="d1191-200">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="d1191-201">**수신된 연결 메시지/초**</span><span class="sxs-lookup"><span data-stu-id="d1191-201">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="d1191-202">**전송된 연결 메시지/초**</span><span class="sxs-lookup"><span data-stu-id="d1191-202">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="d1191-203">**메시지 버스 메트릭**</span><span class="sxs-lookup"><span data-stu-id="d1191-203">**Message bus metrics**</span></span>

<span data-ttu-id="d1191-204">다음 메트릭은 모든 수신 및 발신 SignalR 메시지가 배치되는 큐인 내부 SignalR 메시지 버스를 통해 트래픽을 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-204">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="d1191-205">메시지를 보내거나 브로드캐스트할 때 **게시됩니다.**</span><span class="sxs-lookup"><span data-stu-id="d1191-205">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="d1191-206">이 컨텍스트의 **구독자는** 메시지 버스의 구독입니다. 이는 클라이언트 수와 서버 자체의 수와 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-206">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="d1191-207">**할당된 작업자는** 활성 연결에 데이터를 보내는 구성 요소입니다. **바쁜 작업자는** 적극적으로 메시지를 보내는 작업자입니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-207">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="d1191-208">**메시지 버스 메시지 수신 합계**</span><span class="sxs-lookup"><span data-stu-id="d1191-208">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="d1191-209">**메시지 버스 메시지 수신/초**</span><span class="sxs-lookup"><span data-stu-id="d1191-209">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="d1191-210">**메시지 버스 메시지 게시 된 총**</span><span class="sxs-lookup"><span data-stu-id="d1191-210">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="d1191-211">**메시지 버스 메시지 게시/초**</span><span class="sxs-lookup"><span data-stu-id="d1191-211">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="d1191-212">**메시지 버스 구독자 최신**</span><span class="sxs-lookup"><span data-stu-id="d1191-212">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="d1191-213">**메시지 버스 구독자 합계**</span><span class="sxs-lookup"><span data-stu-id="d1191-213">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="d1191-214">**메시지 버스 구독자/초**</span><span class="sxs-lookup"><span data-stu-id="d1191-214">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="d1191-215">**메시지 버스 할당 된 작업자**</span><span class="sxs-lookup"><span data-stu-id="d1191-215">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="d1191-216">**메시지 버스 바쁜 작업자**</span><span class="sxs-lookup"><span data-stu-id="d1191-216">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="d1191-217">**메시지 버스 주제 현재**</span><span class="sxs-lookup"><span data-stu-id="d1191-217">**Message Bus Topics Current**</span></span>

<span data-ttu-id="d1191-218">**오류 메트릭**</span><span class="sxs-lookup"><span data-stu-id="d1191-218">**Error metrics**</span></span>

<span data-ttu-id="d1191-219">다음 메트릭은 SignalR 메시지 트래픽에서 생성된 오류를 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-219">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="d1191-220">**허브 또는 허브** 메서드를 확인할 수 없는 경우 허브 해결 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-220">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="d1191-221">**허브 호출** 오류는 허브 메서드를 호출하는 동안 throw된 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-221">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="d1191-222">**전송** 오류는 HTTP 요청 또는 응답 중에 발생한 연결 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-222">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="d1191-223">**오류: 모든 합계**</span><span class="sxs-lookup"><span data-stu-id="d1191-223">**Errors: All Total**</span></span>
- <span data-ttu-id="d1191-224">**오류: 모든/초**</span><span class="sxs-lookup"><span data-stu-id="d1191-224">**Errors: All/Sec**</span></span>
- <span data-ttu-id="d1191-225">**오류: 허브 해상도 합계**</span><span class="sxs-lookup"><span data-stu-id="d1191-225">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="d1191-226">**오류: 허브 해상도/초**</span><span class="sxs-lookup"><span data-stu-id="d1191-226">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="d1191-227">**오류: 허브 호출 합계**</span><span class="sxs-lookup"><span data-stu-id="d1191-227">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="d1191-228">**오류: 허브 호출/초**</span><span class="sxs-lookup"><span data-stu-id="d1191-228">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="d1191-229">**오류: 전송 총**</span><span class="sxs-lookup"><span data-stu-id="d1191-229">**Errors: Transport Total**</span></span>
- <span data-ttu-id="d1191-230">**오류: 전송/초**</span><span class="sxs-lookup"><span data-stu-id="d1191-230">**Errors: Transport/Sec**</span></span>

<a id="scaleout_metrics"></a>

<span data-ttu-id="d1191-231">**스케일아웃 메트릭**</span><span class="sxs-lookup"><span data-stu-id="d1191-231">**Scaleout metrics**</span></span>

<span data-ttu-id="d1191-232">다음 메트릭은 스케일아웃 공급자가 생성한 트래픽 및 오류를 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-232">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="d1191-233">이 컨텍스트의 **스트림은** 스케일아웃 공급자가 사용하는 축척 단위입니다. 이 테이블은 SQL Server를 사용하는 경우, 서비스 버스가 사용되는 경우 항목 및 Redis가 사용되는 경우 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-233">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="d1191-234">각 스트림은 정렬된 읽기 및 쓰기 작업을 보장합니다. 단일 스트림은 잠재적인 스케일 병목 현상이므로 스트림 수를 늘려 병목 현상을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-234">Each stream ensures ordered read and write operations; a single stream is a potential scale bottleneck, so the number of streams can be increased to help reduce that bottleneck.</span></span> <span data-ttu-id="d1191-235">여러 스트림을 사용하는 경우 SignalR은 지정된 연결에서 전송된 메시지가 순서대로 정렬되도록 하는 방식으로 이러한 스트림에 메시지를 자동으로 배포(샤드) 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-235">If multiple streams are used, SignalR will automatically distribute (shard) messages across these streams in a way that ensures messages sent from any given connection are in order.</span></span>

<span data-ttu-id="d1191-236">[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) 설정은 SignalR에서 유지 관리하는 스케일아웃 송신 큐의 길이를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-236">The [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) setting controls the length of the scaleout send queue maintained by SignalR.</span></span> <span data-ttu-id="d1191-237">값을 0보다 큰 값으로 설정하면 모든 메시지가 구성된 메시징 백플레인으로 한 번에 하나씩 전송될 송신 큐에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-237">Setting it to a value greater than 0 will place all messages in a send queue to be sent one at a time to the configured messaging backplane.</span></span> <span data-ttu-id="d1191-238">큐의 크기가 구성된 길이를 초과하면 큐의 메시지 수가 다시 설정보다 작을 때까지 보낼 후속 호출이 [InvalidOperationException을](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) 사용하여 즉시 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-238">If the size of the queue goes above the configured length, subsequent calls to send will fail immediately with an [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) until the number of messages in the queue is less than the setting again.</span></span> <span data-ttu-id="d1191-239">구현된 백플레인에는 일반적으로 자체 큐또는 플로우 제어가 있기 때문에 큐링은 기본적으로 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-239">Queueing is disabled by default because the implemented backplanes generally have their own queuing or flow-control in place.</span></span> <span data-ttu-id="d1191-240">SQL Server의 경우 연결 풀링은 한 번에 진행되는 전송 수를 효과적으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-240">In the case of SQL Server, connection pooling effectively limits the number of sends going on at any one time.</span></span>

<span data-ttu-id="d1191-241">기본적으로 SQL Server 및 Redis에는 하나의 스트림만 사용되며 서비스 버스에는 5개의 스트림이 사용되고 큐는 비활성화되지만 이러한 설정은 SQL Server 및 Service Bus의 구성을 통해 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-241">By default, only one stream is used for SQL Server and Redis, five streams are used for Service Bus, and queueing is disabled, but these settings can be changed through configuration on SQL Server and Service Bus:</span></span>

<span data-ttu-id="d1191-242">**SQL Server 백플레인의 테이블 수 및 큐 길이를 구성하기 위한 .NET 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="d1191-242">**.NET Server Code for configuring table count and queue length for SQL Server backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

<span data-ttu-id="d1191-243">**서비스 버스 백플레인에 대한 토픽 수 및 큐 길이를 구성하기 위한 .NET 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="d1191-243">**.NET Server Code for configuring topic count and queue length for Service Bus backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

<span data-ttu-id="d1191-244">**버퍼링** 스트림은 오류가 있는 상태로 들어간 스트림입니다. 스트림이 오류 상태에 있으면 백플레인으로 전송된 모든 메시지는 스트림에 더 이상 오류가 없을 때까지 즉시 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-244">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="d1191-245">**큐 보내기 길이는** 게시되었지만 아직 전송되지 않은 메시지 수입니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-245">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="d1191-246">**스케일아웃 메시지 버스 메시지 수신/초**</span><span class="sxs-lookup"><span data-stu-id="d1191-246">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="d1191-247">**스케일아웃 스트림 합계**</span><span class="sxs-lookup"><span data-stu-id="d1191-247">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="d1191-248">**스케일아웃 스트림 열기**</span><span class="sxs-lookup"><span data-stu-id="d1191-248">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="d1191-249">**스케일아웃 스트림 버퍼링**</span><span class="sxs-lookup"><span data-stu-id="d1191-249">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="d1191-250">**스케일아웃 오류 합계**</span><span class="sxs-lookup"><span data-stu-id="d1191-250">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="d1191-251">**스케일아웃 오류/초**</span><span class="sxs-lookup"><span data-stu-id="d1191-251">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="d1191-252">**스케일아웃 송신 큐 길이**</span><span class="sxs-lookup"><span data-stu-id="d1191-252">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="d1191-253">이러한 카운터가 측정하는 내용에 대한 자세한 내용은 [Azure Service Bus의 SignalR 확장을](scaleout-with-windows-azure-service-bus.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d1191-253">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="d1191-254">다른 성능 카운터 사용</span><span class="sxs-lookup"><span data-stu-id="d1191-254">Using other performance counters</span></span>

<span data-ttu-id="d1191-255">다음 성능 카운터는 응용 프로그램의 성능을 모니터링하는 데에도 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1191-255">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="d1191-256">**메모리**</span><span class="sxs-lookup"><span data-stu-id="d1191-256">**Memory**</span></span>

- <span data-ttu-id="d1191-257">모든 힙에서\\.NET CLR 메모리 # 바이트 (w3wp의 경우)</span><span class="sxs-lookup"><span data-stu-id="d1191-257">.NET CLR Memory\\# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="d1191-258">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="d1191-258">**ASP.NET**</span></span>

- <span data-ttu-id="d1191-259">ASP.NET\요청 현재</span><span class="sxs-lookup"><span data-stu-id="d1191-259">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="d1191-260">ASP.NET\큐</span><span class="sxs-lookup"><span data-stu-id="d1191-260">ASP.NET\Queued</span></span>
- <span data-ttu-id="d1191-261">ASP.NET\거부됨</span><span class="sxs-lookup"><span data-stu-id="d1191-261">ASP.NET\Rejected</span></span>

<span data-ttu-id="d1191-262">**Cpu**</span><span class="sxs-lookup"><span data-stu-id="d1191-262">**CPU**</span></span>

- <span data-ttu-id="d1191-263">프로세서 정보\프로세서 시간</span><span class="sxs-lookup"><span data-stu-id="d1191-263">Processor Information\Processor Time</span></span>

<span data-ttu-id="d1191-264">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="d1191-264">**TCP/IP**</span></span>

- <span data-ttu-id="d1191-265">TCPv6/연결 설정</span><span class="sxs-lookup"><span data-stu-id="d1191-265">TCPv6/Connections Established</span></span>
- <span data-ttu-id="d1191-266">TCPv4/연결 설정</span><span class="sxs-lookup"><span data-stu-id="d1191-266">TCPv4/Connections Established</span></span>

<span data-ttu-id="d1191-267">**웹 서비스**</span><span class="sxs-lookup"><span data-stu-id="d1191-267">**Web Service**</span></span>

- <span data-ttu-id="d1191-268">웹 서비스\현재 연결</span><span class="sxs-lookup"><span data-stu-id="d1191-268">Web Service\Current Connections</span></span>
- <span data-ttu-id="d1191-269">웹 서비스\최대 연결</span><span class="sxs-lookup"><span data-stu-id="d1191-269">Web Service\Maximum Connections</span></span>

<span data-ttu-id="d1191-270">**스레딩**</span><span class="sxs-lookup"><span data-stu-id="d1191-270">**Threading**</span></span>

- <span data-ttu-id="d1191-271">현재 논리 스레드의\\.NET CLR 잠금 및 스레드 #</span><span class="sxs-lookup"><span data-stu-id="d1191-271">.NET CLR Locks And Threads\\# of current logical Threads</span></span>
- <span data-ttu-id="d1191-272">현재 물리적 스레드의 .NET CLR 잠금 및 스레드\\#</span><span class="sxs-lookup"><span data-stu-id="d1191-272">.NET CLR Locks And Threads\\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="d1191-273">관련 자료</span><span class="sxs-lookup"><span data-stu-id="d1191-273">Other Resources</span></span>

<span data-ttu-id="d1191-274">ASP.NET 성능 모니터링 및 튜닝에 대한 자세한 내용은 다음 항목을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d1191-274">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="d1191-275">[ASP.NET 성능 개요](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="d1191-275">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="d1191-276">IIS 7.5, IIS 7.0 및 IIS 6.0에서 스레드 사용량을 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d1191-276">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="d1191-277">&lt;응용&gt; 프로그램풀 요소(웹 설정)</span><span class="sxs-lookup"><span data-stu-id="d1191-277">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
