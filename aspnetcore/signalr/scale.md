---
title: ASP.NET Core SignalR 프로덕션 호스팅 및 크기 조정
author: bradygaster
description: 성능 및 ASP.NET Core SignalR을 사용 하는 앱의 확장 문제를 방지 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.custom: mvc
ms.date: 11/28/2018
uid: signalr/scale
ms.openlocfilehash: 4ac4509acc89d0091a3757c7cfbc9981614f29ad
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037740"
---
# <a name="aspnet-core-signalr-hosting-and-scaling"></a><span data-ttu-id="ef9a8-103">ASP.NET Core SignalR 호스팅 및 크기 조정</span><span class="sxs-lookup"><span data-stu-id="ef9a8-103">ASP.NET Core SignalR hosting and scaling</span></span>

<span data-ttu-id="ef9a8-104">하 여 [Andrew Stanton-nurse](https://twitter.com/anurse)하십시오 [Brady Gaster](https://twitter.com/bradygaster), 및 [Tom Dykstra](https://github.com/tdykstra),</span><span class="sxs-lookup"><span data-stu-id="ef9a8-104">By [Andrew Stanton-Nurse](https://twitter.com/anurse), [Brady Gaster](https://twitter.com/bradygaster), and [Tom Dykstra](https://github.com/tdykstra),</span></span>

<span data-ttu-id="ef9a8-105">이 문서에서는 호스팅 및 ASP.NET Core SignalR을 사용 하는 트래픽이 높은 앱에 대 한 고려 사항 크기 조정 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-105">This article explains hosting and scaling considerations for high-traffic apps that use ASP.NET Core SignalR.</span></span>

## <a name="tcp-connection-resources"></a><span data-ttu-id="ef9a8-106">TCP 연결 리소스</span><span class="sxs-lookup"><span data-stu-id="ef9a8-106">TCP connection resources</span></span>

<span data-ttu-id="ef9a8-107">웹 서버에서 지원할 수 있는 동시 TCP 연결 수가 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-107">The number of concurrent TCP connections that a web server can support is limited.</span></span> <span data-ttu-id="ef9a8-108">표준 HTTP 클라이언트를 사용 하 여 *임시* 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-108">Standard HTTP clients use *ephemeral* connections.</span></span> <span data-ttu-id="ef9a8-109">클라이언트 유휴 상태가 되 고 나중에 다시 열 때에 이러한 연결을 닫을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-109">These connections can be closed when the client goes idle and reopened later.</span></span> <span data-ttu-id="ef9a8-110">반면에 SignalR 연결 됩니다 *영구*합니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-110">On the other hand, a SignalR connection is *persistent*.</span></span> <span data-ttu-id="ef9a8-111">SignalR 연결 개방 클라이언트 유휴 상태가 되도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-111">SignalR connections stay open even when the client goes idle.</span></span> <span data-ttu-id="ef9a8-112">많은 클라이언트를 제공 하는 트래픽이 높은 앱에서 이러한 영구 연결의 최대 연결 수에 도달 하는 서버를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-112">In a high-traffic app that serves many clients, these persistent connections can cause servers to hit their maximum number of connections.</span></span>

<span data-ttu-id="ef9a8-113">영구 연결에는 또한 각 연결을 추적 하려면 일부 추가 메모리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-113">Persistent connections also consume some additional memory, to track each connection.</span></span>

<span data-ttu-id="ef9a8-114">SignalR에서 연결 관련 리소스를 많이 사용 된 동일한 서버에서 호스트 되는 다른 웹 앱에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-114">The heavy use of connection-related resources by SignalR can affect other web apps that are hosted on the same server.</span></span> <span data-ttu-id="ef9a8-115">SignalR을 열고 마지막으로 사용 가능한 TCP 연결을 보유를 동일한 서버의 다른 웹 앱에 사용 가능한 연결이 더 이상가입니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-115">When SignalR opens and holds the last available TCP connections, other web apps on the same server also have no more connections available to them.</span></span>

<span data-ttu-id="ef9a8-116">서버 연결을 부족 하면 임의 소켓 오류가 표시 됩니다 및 연결 오류를 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-116">If a server runs out of connections, you'll see random socket errors and connection reset errors.</span></span> <span data-ttu-id="ef9a8-117">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="ef9a8-117">For example:</span></span>

```
An attempt was made to access a socket in a way forbidden by its access permissions...
```

<span data-ttu-id="ef9a8-118">SignalR 리소스 사용량이 다른 웹 앱에서 오류가 발생 하지 않도록 하려면 다른 웹 앱 이외의 다른 서버에서 SignalR을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-118">To keep SignalR resource usage from causing errors in other web apps, run SignalR on different servers than your other web apps.</span></span>

<span data-ttu-id="ef9a8-119">SignalR 리소스 사용량 SignalR 앱에서 오류가 발생 하지 않도록 하려면 서버에 처리 해야 하는 연결 수를 제한 하려면 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-119">To keep SignalR resource usage from causing errors in a SignalR app, scale out to limit the number of connections a server has to handle.</span></span>

## <a name="scale-out"></a><span data-ttu-id="ef9a8-120">확장</span><span class="sxs-lookup"><span data-stu-id="ef9a8-120">Scale out</span></span>

<span data-ttu-id="ef9a8-121">SignalR을 사용 하는 앱 서버 팜에 대 한 문제를 발생 시킵니다는 해당 연결을 추적할 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-121">An app that uses SignalR needs to keep track of all its connections, which creates problems for a server farm.</span></span> <span data-ttu-id="ef9a8-122">서버를 추가 하 고 다른 서버에 대 한 알 수 없는 새 연결을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-122">Add a server, and it gets new connections that the other servers don't know about.</span></span> <span data-ttu-id="ef9a8-123">예를 들어 다음 다이어그램에 각 서버에서 SignalR는 다른 서버에서 연결을 인식 하지.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-123">For example, SignalR on each server in the following diagram is unaware of the connections on the other servers.</span></span> <span data-ttu-id="ef9a8-124">SignalR의 서버 중 하나에서 원하는 모든 클라이언트에 메시지를 보낼 때 메시지는만 해당 서버에 연결 된 클라이언트로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-124">When SignalR on one of the servers wants to send a message to all clients, the message only goes to the clients connected to that server.</span></span>

![SignalR을 백플레인 없이 크기 조정](scale/_static/scale-no-backplane.png)

<span data-ttu-id="ef9a8-126">이 문제를 해결 하기 위한 옵션은는 [Azure SignalR Service](#azure-signalr-service) 하 고 [백플레인 Redis](#redis-backplane)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-126">The options for solving this problem are the [Azure SignalR Service](#azure-signalr-service) and [Redis backplane](#redis-backplane).</span></span>

## <a name="azure-signalr-service"></a><span data-ttu-id="ef9a8-127">Azure SignalR Service</span><span class="sxs-lookup"><span data-stu-id="ef9a8-127">Azure SignalR Service</span></span>

<span data-ttu-id="ef9a8-128">Azure SignalR Service는를 백플레인으로 대신 프록시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-128">The Azure SignalR Service is a proxy rather than a backplane.</span></span> <span data-ttu-id="ef9a8-129">클라이언트가 서버에 연결을 시작할 때마다 클라이언트 서비스에 연결로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-129">Each time a client initiates a connection to the server, the client is redirected to connect to the service.</span></span> <span data-ttu-id="ef9a8-130">다음 다이어그램은 해당 프로세스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-130">That process is illustrated in the following diagram:</span></span>

![Azure SignalR Service에 연결](scale/_static/azure-signalr-service-one-connection.png)

<span data-ttu-id="ef9a8-132">서비스를 관리 하는 모든 클라이언트 연결에 다음 다이어그램에 표시 된 대로 각 서버에만 상수 소수의 서비스에 연결 해야 하는 동안 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-132">The result is that the service manages all of the client connections, while each server needs only a small constant number of connections to the service, as shown in the following diagram:</span></span>

![클라이언트는 서비스에 연결 된 서비스에 연결 된 서버](scale/_static/azure-signalr-service-multiple-connections.png)

<span data-ttu-id="ef9a8-134">이 방법은 스케일 아웃 Redis 백플레인 대안을 통해 여러 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-134">This approach to scale-out has several advantages over the Redis backplane alternative:</span></span>

* <span data-ttu-id="ef9a8-135">고정 세션을 라고도 [클라이언트 선호도](/iis/extensions/configuring-application-request-routing-arr/http-load-balancing-using-application-request-routing#step-3---configure-client-affinity)를 연결할 때 Azure SignalR Service로 클라이언트 즉시 리디렉션되는 때문에 필수가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-135">Sticky sessions, also known as [client affinity](/iis/extensions/configuring-application-request-routing-arr/http-load-balancing-using-application-request-routing#step-3---configure-client-affinity), is not required, because clients are immediately redirected to the Azure SignalR Service when they connect.</span></span>
* <span data-ttu-id="ef9a8-136">앱을 확장할 수는 SignalR 연결 개수에 관계 없이 처리 하는 Azure SignalR Service를 자동으로 조정 하는 동안 전송 메시지 수를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-136">A SignalR app can scale out based on the number of messages sent, while the Azure SignalR Service automatically scales to handle any number of connections.</span></span> <span data-ttu-id="ef9a8-137">예를 들어 수천 개의 클라이언트를 수 있지만 SignalR 앱만 연결 자체를 처리 하기 위해 여러 서버를 확장할 필요가 없습니다 초당 몇 가지 메시지를 전송 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-137">For example, there could be thousands of clients, but if only a few messages per second are sent, the SignalR app won't need to scale out to multiple servers just to handle the connections themselves.</span></span>
* <span data-ttu-id="ef9a8-138">SignalR 앱 SignalR 없이 웹 앱을 보다 훨씬 더 많은 연결 리소스를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-138">A SignalR app won't use significantly more connection resources than a web app without SignalR.</span></span>

<span data-ttu-id="ef9a8-139">이러한 이유로 Azure SignalR Service App Service, Vm 및 컨테이너를 포함 하 여 Azure에서 호스팅되는 모든 ASP.NET Core SignalR 앱에 대 한 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-139">For these reasons, we recommend the Azure SignalR Service for all ASP.NET Core SignalR apps hosted on Azure, including App Service, VMs, and containers.</span></span>

<span data-ttu-id="ef9a8-140">자세한 내용은 참조는 [Azure SignalR Service 설명서](/azure/azure-signalr/signalr-overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-140">For more information see the [Azure SignalR Service documentation](/azure/azure-signalr/signalr-overview).</span></span>

## <a name="redis-backplane"></a><span data-ttu-id="ef9a8-141">Redis 백플레인</span><span class="sxs-lookup"><span data-stu-id="ef9a8-141">Redis backplane</span></span>

<span data-ttu-id="ef9a8-142">[Redis](https://redis.io/) 는 게시/구독 모델을 사용 하 여 메시징 시스템을 지 원하는 메모리 내 키-값 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-142">[Redis](https://redis.io/) is an in-memory key-value store that supports a messaging system with a publish/subscribe model.</span></span> <span data-ttu-id="ef9a8-143">SignalR에서 Redis 백플레인에서 pub/sub 기능을 사용 하 여 다른 서버에 메시지를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-143">The SignalR Redis backplane uses the pub/sub feature to forward messages to other servers.</span></span> <span data-ttu-id="ef9a8-144">클라이언트가 연결 하면 연결 정보를 백플레인에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-144">When a client makes a connection, the connection information is passed to the backplane.</span></span> <span data-ttu-id="ef9a8-145">서버를 모든 클라이언트에 메시지를 송신 하려는 경우를 백플레인에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-145">When a server wants to send a message to all clients, it sends to the backplane.</span></span> <span data-ttu-id="ef9a8-146">백플레인에서 인식 및 연결 된 모든 클라이언트에 있는 서버.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-146">The backplane knows all connected clients and which servers they're on.</span></span> <span data-ttu-id="ef9a8-147">해당 서버를 통해 모든 클라이언트에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-147">It sends the message to all clients via their respective servers.</span></span> <span data-ttu-id="ef9a8-148">다음 다이어그램은이 프로세스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-148">This process is illustrated in the following diagram:</span></span>

![Redis 백 블 레인에 모든 클라이언트에 하나의 서버에서 보낸 메시지](scale/_static/redis-backplane.png)

<span data-ttu-id="ef9a8-150">Redis 백플레인에서 고유한 인프라에 호스트 된 앱에 대 한 권장 되는 수평 확장 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-150">The Redis backplane is the recommended scale-out approach for apps hosted on your own infrastructure.</span></span> <span data-ttu-id="ef9a8-151">Azure SignalR Service는 데이터 센터와 Azure 데이터 센터 간의 연결 대기 시간으로 인해 온-프레미스 앱을 사용 하 여 프로덕션 사용에 대 한 실제 옵션이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-151">Azure SignalR Service isn't a practical option for production use with on-premises apps due to connection latency between your data center and an Azure data center.</span></span>

<span data-ttu-id="ef9a8-152">앞서 언급 했 듯이 Azure SignalR Service 장점은 Redis 백플레인에서 단점:</span><span class="sxs-lookup"><span data-stu-id="ef9a8-152">The Azure SignalR Service advantages noted earlier are disadvantages for the Redis backplane:</span></span>

* <span data-ttu-id="ef9a8-153">고정 세션을 라고도 [클라이언트 선호도](/iis/extensions/configuring-application-request-routing-arr/http-load-balancing-using-application-request-routing#step-3---configure-client-affinity)에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-153">Sticky sessions, also known as [client affinity](/iis/extensions/configuring-application-request-routing-arr/http-load-balancing-using-application-request-routing#step-3---configure-client-affinity), is required.</span></span> <span data-ttu-id="ef9a8-154">연결 된 서버에서 시작 된 후 연결이 해당 서버의 상태를 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-154">Once a connection is initiated on a server, the connection has to stay on that server.</span></span>
* <span data-ttu-id="ef9a8-155">SignalR 앱을 몇 가지 메시지를 보내는 경우에 클라이언트의 수를 기준된으로 확장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-155">A SignalR app must scale out based on number of clients even if few messages are being sent.</span></span>
* <span data-ttu-id="ef9a8-156">SignalR 앱 SignalR 없이 웹 앱을 보다 훨씬 더 많은 연결 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-156">A SignalR app uses significantly more connection resources than a web app without SignalR.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef9a8-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ef9a8-157">Next steps</span></span>

<span data-ttu-id="ef9a8-158">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef9a8-158">For more information, see the following resources:</span></span>

* [<span data-ttu-id="ef9a8-159">Azure SignalR Service 설명서</span><span class="sxs-lookup"><span data-stu-id="ef9a8-159">Azure SignalR Service documentation</span></span>](/azure/azure-signalr/signalr-overview)
* [<span data-ttu-id="ef9a8-160">Redis 백플레인 설정</span><span class="sxs-lookup"><span data-stu-id="ef9a8-160">Set up a Redis backplane</span></span>](xref:signalr/redis-backplane)
