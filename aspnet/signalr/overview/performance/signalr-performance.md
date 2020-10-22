---
uid: signalr/overview/performance/signalr-performance
title: SignalR 성능 | Microsoft Docs
author: bradygaster
description: SignalR 성능
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345281"
---
# <a name="signalr-performance"></a><span data-ttu-id="dafe9-103">SignalR 성능</span><span class="sxs-lookup"><span data-stu-id="dafe9-103">SignalR Performance</span></span>

<span data-ttu-id="dafe9-104">[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="dafe9-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="dafe9-105">이 항목에서는 SignalR 응용 프로그램의 성능을 설계, 측정 및 개선 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="dafe9-106">이 항목에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="dafe9-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="dafe9-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="dafe9-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="dafe9-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="dafe9-108">.NET 4.5</span></span>
> - <span data-ttu-id="dafe9-109">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="dafe9-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="dafe9-110">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="dafe9-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="dafe9-111">이전 버전의 SignalR에 대 한 자세한 내용은 [SignalR 이전 버전](../older-versions/index.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="dafe9-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="dafe9-112">질문 및 설명</span><span class="sxs-lookup"><span data-stu-id="dafe9-112">Questions and comments</span></span>
>
> <span data-ttu-id="dafe9-113">이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="dafe9-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="dafe9-114">자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="dafe9-115">SignalR 성능 및 크기 조정에 대 한 최근 프레젠테이션은 [ASP.NET SignalR를 사용 하 여 실시간 웹 크기 조정](https://channel9.msdn.com/Events/Build/2013/3-502)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="dafe9-115">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="dafe9-116">이 항목에는 다음과 같은 섹션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="dafe9-117">디자인 고려 사항</span><span class="sxs-lookup"><span data-stu-id="dafe9-117">Design considerations</span></span>](#design)
- [<span data-ttu-id="dafe9-118">성능을 위해 SignalR 서버 튜닝</span><span class="sxs-lookup"><span data-stu-id="dafe9-118">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="dafe9-119">성능 문제 해결</span><span class="sxs-lookup"><span data-stu-id="dafe9-119">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="dafe9-120">SignalR 성능 카운터 사용</span><span class="sxs-lookup"><span data-stu-id="dafe9-120">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="dafe9-121">다른 성능 카운터 사용</span><span class="sxs-lookup"><span data-stu-id="dafe9-121">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="dafe9-122">다른 리소스</span><span class="sxs-lookup"><span data-stu-id="dafe9-122">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="dafe9-123">디자인 고려 사항</span><span class="sxs-lookup"><span data-stu-id="dafe9-123">Design considerations</span></span>

<span data-ttu-id="dafe9-124">이 섹션에서는 SignalR 응용 프로그램을 디자인 하는 동안 구현할 수 있는 패턴을 설명 하 여 불필요 한 네트워크 트래픽을 생성 하 여 성능이 저하 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-124">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="dafe9-125">메시지 빈도 조정</span><span class="sxs-lookup"><span data-stu-id="dafe9-125">Throttling message frequency</span></span>

<span data-ttu-id="dafe9-126">실시간 게임 응용 프로그램과 같은 높은 빈도로 메시지를 전송 하는 응용 프로그램 에서도 대부분의 응용 프로그램은 몇 초 이상의 메시지를 보낼 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-126">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="dafe9-127">각 클라이언트에서 생성 하는 트래픽 양을 줄이기 위해 메시지 루프를 구현 하 여 고정 된 속도 보다 더 자주 메시지를 전송 하지 않습니다. 즉, 해당 시간 간격에 메시지가 전송 될 때마다 초당 전송 되는 메시지 수를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-127">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="dafe9-128">클라이언트와 서버 모두에서 메시지를 특정 속도로 제한 하는 예제 응용 프로그램은 SignalR를 사용 하는 [빈도가 높은 실시간](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="dafe9-128">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="dafe9-129">메시지 크기 줄이기</span><span class="sxs-lookup"><span data-stu-id="dafe9-129">Reducing message size</span></span>

<span data-ttu-id="dafe9-130">Serialize 된 개체의 크기를 줄여 SignalR 메시지의 크기를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-130">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="dafe9-131">서버 코드에서 전송 하지 않아도 되는 속성을 포함 하는 개체를 전송 하는 경우 특성을 사용 하 여 이러한 속성이 serialize 되지 않도록 `JsonIgnore` 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-131">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="dafe9-132">속성의 이름도 메시지에 저장 됩니다. 특성을 사용 하 여 속성의 이름을 줄일 수 있습니다 `JsonProperty` .</span><span class="sxs-lookup"><span data-stu-id="dafe9-132">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="dafe9-133">다음 코드 샘플에서는 클라이언트에 전송 되는 속성을 제외 하는 방법과 속성 이름을 단축 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-133">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="dafe9-134">**클라이언트에 전송 되는 데이터를 제외 하는 JsonIgnore 특성을 보여 주는 .NET server 코드와 메시지 크기를 줄이기 위해 Jsonpropery 특성**</span><span class="sxs-lookup"><span data-stu-id="dafe9-134">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="dafe9-135">클라이언트 코드에서 가독성/유지 관리를 유지 하기 위해 메시지를 받은 후 축약 된 속성 이름을 사용자에 게 친숙 한 이름으로 다시 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-135">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="dafe9-136">다음 코드 샘플에서는 메시지 계약 (매핑)을 정의 하 고 함수를 사용 하 여 `reMap` 최적화 된 메시지 클래스에 계약을 적용 하 여 약식 이름을 더 긴 이름으로 다시 매핑할 수 있는 한 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-136">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="dafe9-137">**사용자가 읽을 수 있는 이름에 축약 된 속성 이름을 다시 매핑하는 클라이언트 쪽 JavaScript 코드**</span><span class="sxs-lookup"><span data-stu-id="dafe9-137">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="dafe9-138">동일한 방법을 사용 하 여 클라이언트에서 서버로의 메시지 에서도 이름을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-138">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="dafe9-139">메시지 개체의 메모리 공간 (즉, 메시지에 사용 되는 메모리 양)을 줄이면 성능도 향상 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-139">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="dafe9-140">예를 들어의 전체 범위가 `int` 필요 하지 않은 경우 `short` 또는를 `byte` 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-140">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="dafe9-141">메시지는 서버 메모리의 메시지 버스에 저장 되므로 메시지 크기를 줄이면 서버 메모리 문제를 해결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-141">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="dafe9-142">성능을 위해 SignalR 서버 튜닝</span><span class="sxs-lookup"><span data-stu-id="dafe9-142">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="dafe9-143">다음 구성 설정을 사용 하 여 SignalR 응용 프로그램의 성능을 향상 시키기 위해 서버를 튜닝할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-143">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="dafe9-144">ASP.NET 응용 프로그램의 성능을 향상 시키는 방법에 대 한 일반적인 내용은 [ASP.NET 성능 향상](https://msdn.microsoft.com/library/ff647787.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="dafe9-144">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="dafe9-145">**SignalR 구성 설정**</span><span class="sxs-lookup"><span data-stu-id="dafe9-145">**SignalR configuration settings**</span></span>

- <span data-ttu-id="dafe9-146">**Defaultmessagebuffersize**: 기본적으로 SignalR는 연결 당 허브 당 1000 메시지를 메모리에 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-146">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="dafe9-147">많은 메시지를 사용 하는 경우이 값을 줄이면 메모리 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-147">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="dafe9-148">이 설정은 `Application_Start` ASP.NET 응용 프로그램의 이벤트 처리기 또는 `Configuration` 자체 호스팅 응용 프로그램의 OWIN startup 클래스 메서드에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-148">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="dafe9-149">다음 샘플에서는 사용 되는 서버 메모리 양을 줄이기 위해 응용 프로그램의 메모리 사용 공간을 줄이기 위해이 값을 줄이는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-149">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="dafe9-150">**기본 메시지 버퍼 크기를 줄이기 위한 Startup.cs의 .NET 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="dafe9-150">**.NET server code in Startup.cs for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="dafe9-151">**IIS 구성 설정**</span><span class="sxs-lookup"><span data-stu-id="dafe9-151">**IIS configuration settings**</span></span>

- <span data-ttu-id="dafe9-152">**응용 프로그램당 최대 동시 요청**수: 동시 IIS 요청 수를 늘리면 요청을 처리 하는 데 사용할 수 있는 서버 리소스가 늘어납니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-152">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="dafe9-153">기본값은 5000입니다. 이 설정을 늘리려면 관리자 권한 명령 프롬프트에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-153">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- <span data-ttu-id="dafe9-154">**ApplicationPool QueueLength**: 응용 프로그램 풀에 대 한 큐를 Http.sys 하는 최대 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-154">**ApplicationPool QueueLength**: This is the maximum number of requests that Http.sys queues for the application pool.</span></span> <span data-ttu-id="dafe9-155">큐가 가득 차면 새 요청은 503 "서비스를 사용할 수 없음" 응답을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-155">When the queue is full, new requests receive a 503 "Service Unavailable" response.</span></span> <span data-ttu-id="dafe9-156">기본값은 1000입니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-156">The default value is 1000.</span></span>

    <span data-ttu-id="dafe9-157">응용 프로그램을 호스팅하는 응용 프로그램 풀에서 작업자 프로세스의 큐 길이를 단축 하면 메모리 리소스가 절약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-157">Shortening the queue length for the worker process in the application pool hosting your application will conserve memory resources.</span></span> <span data-ttu-id="dafe9-158">자세한 내용은 [응용 프로그램 풀 관리, 조정 및 구성](https://technet.microsoft.com/library/cc745955.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="dafe9-158">For more information, see [Managing, Tuning, and Configuring Application Pools](https://technet.microsoft.com/library/cc745955.aspx).</span></span>

<span data-ttu-id="dafe9-159">**ASP.NET 구성 설정**</span><span class="sxs-lookup"><span data-stu-id="dafe9-159">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="dafe9-160">이 섹션에는 파일에서 설정할 수 있는 구성 설정이 포함 되어 있습니다 `aspnet.config` .</span><span class="sxs-lookup"><span data-stu-id="dafe9-160">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="dafe9-161">이 파일은 플랫폼에 따라 다음 두 위치 중 하나에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-161">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="dafe9-162">SignalR 성능을 향상 시킬 수 있는 ASP.NET 설정에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-162">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="dafe9-163">**CPU 당 최대 동시 요청**수:이 설정을 높이면 성능 병목 현상이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-163">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="dafe9-164">이 설정을 늘리려면 다음 구성 설정을 파일에 추가 합니다 `aspnet.config` .</span><span class="sxs-lookup"><span data-stu-id="dafe9-164">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="dafe9-165">**요청 큐 제한**: 총 연결 수가 설정을 초과 하는 경우 `maxConcurrentRequestsPerCPU` ASP.NET는 큐를 사용 하 여 요청을 제한 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-165">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="dafe9-166">큐의 크기를 늘리려면 설정을 늘릴 수 있습니다 `requestQueueLimit` .</span><span class="sxs-lookup"><span data-stu-id="dafe9-166">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="dafe9-167">이렇게 하려면 다음 구성 설정을 `processModel` 의 노드 (대신)에 추가 합니다 `config/machine.config` `aspnet.config` .</span><span class="sxs-lookup"><span data-stu-id="dafe9-167">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="dafe9-168">성능 문제 해결</span><span class="sxs-lookup"><span data-stu-id="dafe9-168">Troubleshooting performance issues</span></span>

<span data-ttu-id="dafe9-169">이 섹션에서는 응용 프로그램에서 성능 병목 지점을 찾는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-169">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="dafe9-170">WebSocket이 사용 되 고 있는지 확인 하는 중</span><span class="sxs-lookup"><span data-stu-id="dafe9-170">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="dafe9-171">SignalR는 클라이언트와 서버 간의 통신에 다양 한 전송을 사용할 수 있는 반면 WebSocket은 상당한 성능상의 이점을 제공 하며 클라이언트와 서버에서 지 원하는 경우 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-171">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="dafe9-172">클라이언트와 서버가 WebSocket에 대 한 요구 사항을 충족 하는지 확인 하려면 [전송 및 대체](../getting-started/introduction-to-signalr.md#transports)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="dafe9-172">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="dafe9-173">응용 프로그램에서 사용 되는 전송을 확인 하기 위해 브라우저 개발자 도구를 사용 하 고 로그를 검토 하 여 연결에 사용 되는 전송을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-173">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="dafe9-174">Internet Explorer 및 Chrome에서 브라우저 개발 도구를 사용 하는 방법에 대 한 자세한 내용은 [전송 및 대체](../getting-started/introduction-to-signalr.md#transports)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="dafe9-174">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="dafe9-175">SignalR 성능 카운터 사용</span><span class="sxs-lookup"><span data-stu-id="dafe9-175">Using SignalR performance counters</span></span>

<span data-ttu-id="dafe9-176">이 섹션에서는 패키지에 있는 SignalR 성능 카운터를 사용 하도록 설정 하 고 사용 하는 방법을 설명 합니다 `Microsoft.AspNet.SignalR.Utils` .</span><span class="sxs-lookup"><span data-stu-id="dafe9-176">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="dafe9-177">signalr.exe 설치</span><span class="sxs-lookup"><span data-stu-id="dafe9-177">Installing signalr.exe</span></span>

<span data-ttu-id="dafe9-178">SignalR.exe 이라는 유틸리티를 사용 하 여 서버에 성능 카운터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-178">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="dafe9-179">이 유틸리티를 설치 하려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-179">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="dafe9-180">Visual Studio에서 **도구**  >  **nuget 패키지 관리자**  >  **솔루션용 NuGet 패키지 관리** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-180">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="dafe9-181">**Signalr. 유틸리티**를 검색 하 고 설치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-181">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="dafe9-182">사용권 계약에 동의 하 여 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-182">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="dafe9-183">SignalR.exe는에 설치 됩니다 `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools` .</span><span class="sxs-lookup"><span data-stu-id="dafe9-183">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="dafe9-184">SignalR.exe를 사용 하 여 성능 카운터 설치</span><span class="sxs-lookup"><span data-stu-id="dafe9-184">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="dafe9-185">SignalR 성능 카운터를 설치 하려면 다음 매개 변수를 사용 하 여 관리자 권한 명령 프롬프트에서 SignalR.exe를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-185">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="dafe9-186">SignalR 성능 카운터를 제거 하려면 다음 매개 변수를 사용 하 여 관리자 권한 명령 프롬프트에서 SignalR.exe를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-186">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="dafe9-187">SignalR 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="dafe9-187">SignalR Performance counters</span></span>

<span data-ttu-id="dafe9-188">유틸리티 패키지는 다음 성능 카운터를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-188">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="dafe9-189">"Total" 카운터는 마지막 응용 프로그램 풀 또는 서버 다시 시작 이후의 이벤트 수를 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-189">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="dafe9-190">**연결 메트릭**</span><span class="sxs-lookup"><span data-stu-id="dafe9-190">**Connection metrics**</span></span>

<span data-ttu-id="dafe9-191">다음 메트릭은 발생 하는 연결 수명 이벤트를 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-191">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="dafe9-192">자세한 내용은 [연결 수명 이벤트 이해 및 처리](../guide-to-the-api/handling-connection-lifetime-events.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="dafe9-192">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="dafe9-193">**연결 된 연결**</span><span class="sxs-lookup"><span data-stu-id="dafe9-193">**Connections Connected**</span></span>
- <span data-ttu-id="dafe9-194">**연결이 다시 연결 되었습니다.**</span><span class="sxs-lookup"><span data-stu-id="dafe9-194">**Connections Reconnected**</span></span>
- <span data-ttu-id="dafe9-195">**연결 끊김**</span><span class="sxs-lookup"><span data-stu-id="dafe9-195">**Connections Disconnected**</span></span>
- <span data-ttu-id="dafe9-196">**현재 연결**</span><span class="sxs-lookup"><span data-stu-id="dafe9-196">**Connections Current**</span></span>

<span data-ttu-id="dafe9-197">**메시지 메트릭**</span><span class="sxs-lookup"><span data-stu-id="dafe9-197">**Message metrics**</span></span>

<span data-ttu-id="dafe9-198">다음 메트릭은 SignalR에서 생성 된 메시지 트래픽을 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-198">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="dafe9-199">**총 받은 연결 메시지**</span><span class="sxs-lookup"><span data-stu-id="dafe9-199">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="dafe9-200">**총 보낸 연결 메시지**</span><span class="sxs-lookup"><span data-stu-id="dafe9-200">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="dafe9-201">**받은 연결 메시지/초**</span><span class="sxs-lookup"><span data-stu-id="dafe9-201">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="dafe9-202">**전송 되는 연결 메시지/초**</span><span class="sxs-lookup"><span data-stu-id="dafe9-202">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="dafe9-203">**메시지 버스 메트릭**</span><span class="sxs-lookup"><span data-stu-id="dafe9-203">**Message bus metrics**</span></span>

<span data-ttu-id="dafe9-204">다음 메트릭은 내부 SignalR 메시지 버스, 들어오고 나가는 모든 SignalR 메시지가 배치 되는 큐를 통해 트래픽을 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-204">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="dafe9-205">메시지는 보내거나 브로드캐스트할 때 **게시** 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-205">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="dafe9-206">이 컨텍스트의 **구독자** 는 메시지 버스에 대 한 구독입니다. 이는 클라이언트 수와 서버 자체의 수와 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-206">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="dafe9-207">**할당 된 작업자** 는 활성 연결에 데이터를 전송 하는 구성 요소입니다. **사용 중인 작업자** 는 메시지를 전송 하는 작업자입니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-207">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="dafe9-208">**메시지 버스 총 수신 메시지**</span><span class="sxs-lookup"><span data-stu-id="dafe9-208">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="dafe9-209">**메시지 버스 받은 메시지/초**</span><span class="sxs-lookup"><span data-stu-id="dafe9-209">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="dafe9-210">**메시지 버스 총 게시 된 메시지**</span><span class="sxs-lookup"><span data-stu-id="dafe9-210">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="dafe9-211">**게시 된 메시지 버스 메시지/초**</span><span class="sxs-lookup"><span data-stu-id="dafe9-211">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="dafe9-212">**메시지 버스 구독자 최신**</span><span class="sxs-lookup"><span data-stu-id="dafe9-212">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="dafe9-213">**메시지 버스 구독자 합계**</span><span class="sxs-lookup"><span data-stu-id="dafe9-213">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="dafe9-214">**메시지 버스 구독자/초**</span><span class="sxs-lookup"><span data-stu-id="dafe9-214">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="dafe9-215">**메시지 버스 할당 된 작업자**</span><span class="sxs-lookup"><span data-stu-id="dafe9-215">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="dafe9-216">**메시지 버스 작업 중인 작업자**</span><span class="sxs-lookup"><span data-stu-id="dafe9-216">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="dafe9-217">**메시지 버스 항목 현재**</span><span class="sxs-lookup"><span data-stu-id="dafe9-217">**Message Bus Topics Current**</span></span>

<span data-ttu-id="dafe9-218">**오류 메트릭**</span><span class="sxs-lookup"><span data-stu-id="dafe9-218">**Error metrics**</span></span>

<span data-ttu-id="dafe9-219">다음 메트릭은 SignalR 메시지 트래픽에 의해 생성 된 오류를 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-219">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="dafe9-220">허브 **확인** 오류는 허브 또는 허브 메서드를 확인할 수 없을 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-220">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="dafe9-221">허브 **호출** 오류는 허브 메서드를 호출 하는 동안 throw 되는 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-221">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="dafe9-222">**전송** 오류는 HTTP 요청 또는 응답 중에 throw 된 연결 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-222">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="dafe9-223">**오류: 전체**</span><span class="sxs-lookup"><span data-stu-id="dafe9-223">**Errors: All Total**</span></span>
- <span data-ttu-id="dafe9-224">**오류: 모두/초**</span><span class="sxs-lookup"><span data-stu-id="dafe9-224">**Errors: All/Sec**</span></span>
- <span data-ttu-id="dafe9-225">**오류: 총 허브 해상도**</span><span class="sxs-lookup"><span data-stu-id="dafe9-225">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="dafe9-226">**오류: 허브 확인/초**</span><span class="sxs-lookup"><span data-stu-id="dafe9-226">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="dafe9-227">**오류: 총 허브 호출**</span><span class="sxs-lookup"><span data-stu-id="dafe9-227">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="dafe9-228">**오류: 허브 호출/초**</span><span class="sxs-lookup"><span data-stu-id="dafe9-228">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="dafe9-229">**오류: 총 전송**</span><span class="sxs-lookup"><span data-stu-id="dafe9-229">**Errors: Transport Total**</span></span>
- <span data-ttu-id="dafe9-230">**오류: Transport/Sec**</span><span class="sxs-lookup"><span data-stu-id="dafe9-230">**Errors: Transport/Sec**</span></span>

<a id="scaleout_metrics"></a>

<span data-ttu-id="dafe9-231">**확장 메트릭**</span><span class="sxs-lookup"><span data-stu-id="dafe9-231">**Scaleout metrics**</span></span>

<span data-ttu-id="dafe9-232">다음 메트릭은 확장 공급자에 의해 생성 된 트래픽 및 오류를 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-232">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="dafe9-233">이 컨텍스트의 **스트림은** 확장 공급자에서 사용 되는 배율 단위입니다. 이는 SQL Server 사용 되는 경우 테이블이 고 Service Bus 사용 되는 경우 토픽 이며 Redis가 사용 되는 경우 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-233">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="dafe9-234">각 스트림은 순차적 읽기 및 쓰기 작업을 보장 합니다. 단일 스트림은 잠재적 규모 병목 상태 이므로 병목 현상을 줄이기 위해 스트림 수를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-234">Each stream ensures ordered read and write operations; a single stream is a potential scale bottleneck, so the number of streams can be increased to help reduce that bottleneck.</span></span> <span data-ttu-id="dafe9-235">여러 스트림을 사용 하는 경우 SignalR은 지정 된 연결에서 전송 된 메시지의 순서를 확인 하는 방식으로 이러한 스트림에 메시지를 자동으로 배포 (분할) 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-235">If multiple streams are used, SignalR will automatically distribute (shard) messages across these streams in a way that ensures messages sent from any given connection are in order.</span></span>

<span data-ttu-id="dafe9-236">[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) 설정은 SignalR에 의해 유지 관리 되는 확장 send queue의 길이를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-236">The [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) setting controls the length of the scaleout send queue maintained by SignalR.</span></span> <span data-ttu-id="dafe9-237">이 값을 0 보다 큰 값으로 설정 하면 전송 큐에 있는 모든 메시지가 구성 된 메시징 후면판에 한 번에 하나씩 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-237">Setting it to a value greater than 0 will place all messages in a send queue to be sent one at a time to the configured messaging backplane.</span></span> <span data-ttu-id="dafe9-238">큐의 크기가 구성 된 길이를 초과 하는 경우 큐에 있는 메시지 수가 다시 설정 보다 [적을 때까지](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) 이후의 send 호출은 즉시 실패 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-238">If the size of the queue goes above the configured length, subsequent calls to send will fail immediately with an [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) until the number of messages in the queue is less than the setting again.</span></span> <span data-ttu-id="dafe9-239">구현 된 백플레인을 일반적으로 자체 큐 또는 흐름 제어를 포함 하기 때문에 기본적으로 큐는 사용 하지 않도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-239">Queueing is disabled by default because the implemented backplanes generally have their own queuing or flow-control in place.</span></span> <span data-ttu-id="dafe9-240">SQL Server의 경우 연결 풀링을 통해 한 번에 진행 되는 전송 수를 효과적으로 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-240">In the case of SQL Server, connection pooling effectively limits the number of sends going on at any one time.</span></span>

<span data-ttu-id="dafe9-241">기본적으로 SQL Server 및 Redis에는 하나의 스트림만 사용 되 고, Service Bus에는 5 개의 스트림이 사용 되며, 큐는 사용 하지 않도록 설정 되지만 SQL Server 및 Service Bus의 구성을 통해 이러한 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-241">By default, only one stream is used for SQL Server and Redis, five streams are used for Service Bus, and queueing is disabled, but these settings can be changed through configuration on SQL Server and Service Bus:</span></span>

<span data-ttu-id="dafe9-242">**SQL Server 후면판의 테이블 수 및 큐 길이를 구성 하기 위한 .NET Server 코드**</span><span class="sxs-lookup"><span data-stu-id="dafe9-242">**.NET Server Code for configuring table count and queue length for SQL Server backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

<span data-ttu-id="dafe9-243">**Service Bus 후면판의 토픽 수 및 큐 길이를 구성 하기 위한 .NET Server 코드**</span><span class="sxs-lookup"><span data-stu-id="dafe9-243">**.NET Server Code for configuring topic count and queue length for Service Bus backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

<span data-ttu-id="dafe9-244">**버퍼링** 스트림은 오류가 발생 한 상태로 입력 된 스트림입니다. 스트림이 오류가 발생 한 경우에는 스트림이 더 이상 오류가 발생 하지 않을 때까지 후면판에 전송 된 모든 메시지가 즉시 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-244">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="dafe9-245">**송신 큐 길이** 는 게시 되었지만 아직 보내지 않은 메시지 수입니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-245">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="dafe9-246">**확장 메시지 버스 수신 메시지/초**</span><span class="sxs-lookup"><span data-stu-id="dafe9-246">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="dafe9-247">**총 확장 스트림**</span><span class="sxs-lookup"><span data-stu-id="dafe9-247">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="dafe9-248">**확장 스트림 열기**</span><span class="sxs-lookup"><span data-stu-id="dafe9-248">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="dafe9-249">**확장 스트림 버퍼링**</span><span class="sxs-lookup"><span data-stu-id="dafe9-249">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="dafe9-250">**총 확장 오류**</span><span class="sxs-lookup"><span data-stu-id="dafe9-250">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="dafe9-251">**확장 오류/초**</span><span class="sxs-lookup"><span data-stu-id="dafe9-251">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="dafe9-252">**확장 송신 큐 길이**</span><span class="sxs-lookup"><span data-stu-id="dafe9-252">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="dafe9-253">이러한 카운터를 측정 하는 방법에 대 한 자세한 내용은 [SignalR 확장 with Azure Service Bus](scaleout-with-windows-azure-service-bus.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="dafe9-253">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="dafe9-254">다른 성능 카운터 사용</span><span class="sxs-lookup"><span data-stu-id="dafe9-254">Using other performance counters</span></span>

<span data-ttu-id="dafe9-255">다음 성능 카운터는 응용 프로그램의 성능을 모니터링 하는 데 유용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dafe9-255">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="dafe9-256">**메모리**</span><span class="sxs-lookup"><span data-stu-id="dafe9-256">**Memory**</span></span>

- <span data-ttu-id="dafe9-257">.NET CLR 메모리 \\ # 모든 힙의 바이트 수 (w3wp.exe의 경우)</span><span class="sxs-lookup"><span data-stu-id="dafe9-257">.NET CLR Memory\\# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="dafe9-258">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="dafe9-258">**ASP.NET**</span></span>

- <span data-ttu-id="dafe9-259">ASP.NET \Requests Current</span><span class="sxs-lookup"><span data-stu-id="dafe9-259">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="dafe9-260">ASP. NET\Queued에 대기</span><span class="sxs-lookup"><span data-stu-id="dafe9-260">ASP.NET\Queued</span></span>
- <span data-ttu-id="dafe9-261">ASP. NET\Rejected 됨</span><span class="sxs-lookup"><span data-stu-id="dafe9-261">ASP.NET\Rejected</span></span>

<span data-ttu-id="dafe9-262">**CPU**</span><span class="sxs-lookup"><span data-stu-id="dafe9-262">**CPU**</span></span>

- <span data-ttu-id="dafe9-263">프로세서 Information\Processor Time</span><span class="sxs-lookup"><span data-stu-id="dafe9-263">Processor Information\Processor Time</span></span>

<span data-ttu-id="dafe9-264">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="dafe9-264">**TCP/IP**</span></span>

- <span data-ttu-id="dafe9-265">TCPv6/연결 설정</span><span class="sxs-lookup"><span data-stu-id="dafe9-265">TCPv6/Connections Established</span></span>
- <span data-ttu-id="dafe9-266">TCPv4/연결 설정</span><span class="sxs-lookup"><span data-stu-id="dafe9-266">TCPv4/Connections Established</span></span>

<span data-ttu-id="dafe9-267">**웹 서비스**</span><span class="sxs-lookup"><span data-stu-id="dafe9-267">**Web Service**</span></span>

- <span data-ttu-id="dafe9-268">웹 서비스 \ 현재 연결</span><span class="sxs-lookup"><span data-stu-id="dafe9-268">Web Service\Current Connections</span></span>
- <span data-ttu-id="dafe9-269">웹 서비스 \ 최대 연결</span><span class="sxs-lookup"><span data-stu-id="dafe9-269">Web Service\Maximum Connections</span></span>

<span data-ttu-id="dafe9-270">**스레딩**</span><span class="sxs-lookup"><span data-stu-id="dafe9-270">**Threading**</span></span>

- <span data-ttu-id="dafe9-271">현재 논리 스레드의 .NET CLR 잠금 및 스레드 \\ 개수</span><span class="sxs-lookup"><span data-stu-id="dafe9-271">.NET CLR Locks And Threads\\# of current logical Threads</span></span>
- <span data-ttu-id="dafe9-272">현재 실제 스레드의 .NET CLR 잠금 및 스레드 \\ 개수</span><span class="sxs-lookup"><span data-stu-id="dafe9-272">.NET CLR Locks And Threads\\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="dafe9-273">관련 자료</span><span class="sxs-lookup"><span data-stu-id="dafe9-273">Other Resources</span></span>

<span data-ttu-id="dafe9-274">ASP.NET 성능 모니터링 및 튜닝에 대 한 자세한 내용은 다음 항목을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="dafe9-274">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="dafe9-275">[ASP.NET 성능 개요](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="dafe9-275">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="dafe9-276">IIS 7.5, IIS 7.0 및 IIS 6.0의 ASP.NET 스레드 사용</span><span class="sxs-lookup"><span data-stu-id="dafe9-276">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="dafe9-277">&lt;applicationPool &gt; 요소 (웹 설정)</span><span class="sxs-lookup"><span data-stu-id="dafe9-277">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
