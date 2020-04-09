---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: SignalR 사용자를 연결로 매핑 | 마이크로 소프트 문서
author: bradygaster
description: 이 항목에서는 사용자 및 해당 연결에 대한 정보를 유지하는 방법을 보여 주었습니다. 패트릭 플레처는이 주제를 작성하는 데 도움이. 이 항목에 사용된 소프트웨어 버전...
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675780"
---
# <a name="mapping-signalr-users-to-connections"></a><span data-ttu-id="10d3f-105">SignalR 사용자를 연결에 매핑</span><span class="sxs-lookup"><span data-stu-id="10d3f-105">Mapping SignalR Users to Connections</span></span>

<span data-ttu-id="10d3f-106">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="10d3f-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="10d3f-107">이 항목에서는 사용자 및 해당 연결에 대한 정보를 유지하는 방법을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-107">This topic shows how to retain information about users and their connections.</span></span>
>
> <span data-ttu-id="10d3f-108">패트릭 플레처는이 주제를 작성하는 데 도움이.</span><span class="sxs-lookup"><span data-stu-id="10d3f-108">Patrick Fletcher helped write this topic.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="10d3f-109">이 항목에 사용된 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="10d3f-109">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="10d3f-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="10d3f-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="10d3f-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="10d3f-111">.NET 4.5</span></span>
> - <span data-ttu-id="10d3f-112">시그널R 버전 2</span><span class="sxs-lookup"><span data-stu-id="10d3f-112">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="10d3f-113">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="10d3f-113">Previous versions of this topic</span></span>
>
> <span data-ttu-id="10d3f-114">이전 버전의 SignalR에 대한 자세한 내용은 [SignalR 이전 버전을](../older-versions/index.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="10d3f-114">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="10d3f-115">질문 및 의견</span><span class="sxs-lookup"><span data-stu-id="10d3f-115">Questions and comments</span></span>
>
> <span data-ttu-id="10d3f-116">이 자습서를 어떻게 좋아했는지, 그리고 페이지 하단의 댓글에서 개선할 수 있는 내용에 대한 피드백을 남겨주세요.</span><span class="sxs-lookup"><span data-stu-id="10d3f-116">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="10d3f-117">당신은 튜토리얼과 직접 관련이없는 질문이있는 경우, 당신은 [ASP.NET SignalR 포럼에](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 게시하거나 [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="10d3f-117">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="introduction"></a><span data-ttu-id="10d3f-118">소개</span><span class="sxs-lookup"><span data-stu-id="10d3f-118">Introduction</span></span>

<span data-ttu-id="10d3f-119">허브에 연결하는 각 클라이언트는 고유 연결 ID를 전달합니다. 허브 컨텍스트의 `Context.ConnectionId` 속성에서 이 값을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-119">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="10d3f-120">응용 프로그램에서 사용자를 연결 ID에 매핑하고 해당 매핑을 유지해야 하는 경우 다음 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-120">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- [<span data-ttu-id="10d3f-121">사용자 ID 공급자(SignalR 2)</span><span class="sxs-lookup"><span data-stu-id="10d3f-121">The User ID Provider (SignalR 2)</span></span>](#IUserIdProvider)
- <span data-ttu-id="10d3f-122">사전과 같은 [메모리 내 저장소](#inmemory)</span><span class="sxs-lookup"><span data-stu-id="10d3f-122">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="10d3f-123">각 사용자에 대한 신호 R 그룹</span><span class="sxs-lookup"><span data-stu-id="10d3f-123">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="10d3f-124">데이터베이스 테이블 또는 Azure 테이블 [저장소와](#database)같은 영구 외부 저장소</span><span class="sxs-lookup"><span data-stu-id="10d3f-124">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="10d3f-125">이러한 각 구현은 이 항목에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-125">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="10d3f-126">의 `OnConnected`에서 `OnDisconnected`및 `OnReconnected` 메서드를 `Hub` 사용하여 사용자 연결 상태를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-126">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="10d3f-127">응용 프로그램에 가장 적합한 방법은 다음을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-127">The best approach for your application depends on:</span></span>

- <span data-ttu-id="10d3f-128">응용 프로그램을 호스팅하는 웹 서버 의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-128">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="10d3f-129">현재 연결된 사용자 목록을 받아야 하는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-129">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="10d3f-130">응용 프로그램 또는 서버가 다시 시작될 때 그룹 및 사용자 정보를 유지해야 하는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-130">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="10d3f-131">외부 서버 호출 대기 시간이 문제인지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-131">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="10d3f-132">다음 표에서는 이러한 고려 사항에 적합한 방법을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-132">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="10d3f-133">두 개 이상의 서버</span><span class="sxs-lookup"><span data-stu-id="10d3f-133">More than one server</span></span> | <span data-ttu-id="10d3f-134">현재 연결된 사용자 목록 받기</span><span class="sxs-lookup"><span data-stu-id="10d3f-134">Get list of currently connected users</span></span> | <span data-ttu-id="10d3f-135">다시 시작한 후 정보 유지</span><span class="sxs-lookup"><span data-stu-id="10d3f-135">Persist information after restarts</span></span> | <span data-ttu-id="10d3f-136">최적의 성능</span><span class="sxs-lookup"><span data-stu-id="10d3f-136">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="10d3f-137">사용자 ID 공급자</span><span class="sxs-lookup"><span data-stu-id="10d3f-137">UserID Provider</span></span> | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="10d3f-138">메모리 내</span><span class="sxs-lookup"><span data-stu-id="10d3f-138">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="10d3f-139">단일 사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="10d3f-139">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| <span data-ttu-id="10d3f-140">영구, 외부</span><span class="sxs-lookup"><span data-stu-id="10d3f-140">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a><span data-ttu-id="10d3f-141">IUserID 공급자</span><span class="sxs-lookup"><span data-stu-id="10d3f-141">IUserID provider</span></span>

<span data-ttu-id="10d3f-142">이 기능을 사용하면 사용자가 새 인터페이스 IUserIdProvider를 통해 IRequest를 기반으로 하는 userId를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-142">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider.</span></span>

<span data-ttu-id="10d3f-143">**The IUserIdProvider**</span><span class="sxs-lookup"><span data-stu-id="10d3f-143">**The IUserIdProvider**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="10d3f-144">기본적으로 사용자의 이름을 `IPrincipal.Identity.Name` 사용자 이름으로 사용하는 구현이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-144">By default, there will be an implementation that uses the user's `IPrincipal.Identity.Name` as the user name.</span></span> <span data-ttu-id="10d3f-145">이를 변경하려면 응용 프로그램이 `IUserIdProvider` 시작될 때 전역 호스트에 구현을 등록하십시오.</span><span class="sxs-lookup"><span data-stu-id="10d3f-145">To change this, register your implementation of `IUserIdProvider` with the global host when your application starts:</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<span data-ttu-id="10d3f-146">허브 내에서 다음 API를 통해 이러한 사용자에게 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-146">From within a hub, you'll be able to send messages to these users via the following API:</span></span>

<span data-ttu-id="10d3f-147">**특정 사용자에게 메시지 보내기**</span><span class="sxs-lookup"><span data-stu-id="10d3f-147">**Sending a message to a specific user**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="10d3f-148">인메모리 스토리지</span><span class="sxs-lookup"><span data-stu-id="10d3f-148">In-memory storage</span></span>

<span data-ttu-id="10d3f-149">다음 예제에서는 메모리에 저장된 사전에서 연결 및 사용자 정보를 유지하는 방법을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-149">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="10d3f-150">사전은 연결 `HashSet` ID를 저장하는 데 a를 사용합니다. 사용자는 언제든지 SignalR 응용 프로그램에 두 개 이상의 연결을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-150">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="10d3f-151">예를 들어 여러 장치를 통해 연결하거나 두 개 이상의 브라우저 탭을 통해 연결된 사용자에게는 두 개 이상의 연결 ID가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-151">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="10d3f-152">응용 프로그램이 종료되면 모든 정보가 손실되지만 사용자가 연결을 다시 설정하면 다시 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-152">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="10d3f-153">각 서버에 별도의 연결 컬렉션이 있기 때문에 환경에 두 개 이상의 웹 서버가 포함되어 있으면 메모리 내 저장소가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-153">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="10d3f-154">첫 번째 예제에서는 사용자 연결을 연결하는 것을 관리하는 클래스를 보여 둡니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-154">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="10d3f-155">HashSet의 키는 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-155">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="10d3f-156">다음 예제에서는 허브에서 연결 매핑 클래스를 사용하는 방법을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-156">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="10d3f-157">클래스의 인스턴스는 변수 이름에 `_connections`저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-157">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="10d3f-158">단일 사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="10d3f-158">Single-user groups</span></span>

<span data-ttu-id="10d3f-159">각 사용자에 대한 그룹을 만든 다음 해당 사용자에게만 도달하려는 경우 해당 그룹에 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-159">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="10d3f-160">각 그룹의 이름은 사용자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-160">The name of each group is the name of the user.</span></span> <span data-ttu-id="10d3f-161">사용자에게 두 개 이상의 연결이 있는 경우 각 연결 ID가 사용자의 그룹에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-161">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="10d3f-162">사용자가 연결을 끊을 때 그룹에서 사용자를 수동으로 제거해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-162">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="10d3f-163">이 작업은 SignalR 프레임워크에 의해 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-163">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="10d3f-164">다음 예제에서는 단일 사용자 그룹을 구현하는 방법을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-164">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="10d3f-165">영구, 외부 스토리지</span><span class="sxs-lookup"><span data-stu-id="10d3f-165">Permanent, external storage</span></span>

<span data-ttu-id="10d3f-166">이 항목에서는 연결 정보를 저장하기 위해 데이터베이스 또는 Azure 테이블 저장소를 사용하는 방법을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-166">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="10d3f-167">이 방법은 각 웹 서버가 동일한 데이터 리포지토리와 상호 작용할 수 있기 때문에 여러 웹 서버가 있는 경우에 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-167">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="10d3f-168">웹 서버가 작동을 중지하거나 응용 프로그램이 `OnDisconnected` 다시 시작되면 메서드가 호출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-168">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="10d3f-169">따라서 데이터 리포지토리에 더 이상 유효하지 않은 연결 ID에 대한 레코드가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-169">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="10d3f-170">이러한 분리된 레코드를 정리하려면 응용 프로그램과 관련된 기간 외부에서 만든 연결을 무효화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-170">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="10d3f-171">이 섹션의 예제에는 연결이 만들어진 시기를 추적하는 값이 포함되어 있지만 백그라운드 프로세스로 수행하려고 할 수 있으므로 이전 레코드를 정리하는 방법을 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-171">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="10d3f-172">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="10d3f-172">Database</span></span>

<span data-ttu-id="10d3f-173">다음 예제에서는 데이터베이스에서 연결 및 사용자 정보를 유지하는 방법을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-173">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="10d3f-174">모든 데이터 액세스 기술을 사용할 수 있습니다. 그러나 아래 예제에서는 엔터티 프레임 워크를 사용 하 여 모델을 정의 하는 방법을 보여 주어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-174">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="10d3f-175">이러한 엔터티 모델은 데이터베이스 테이블 및 필드에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-175">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="10d3f-176">데이터 구조는 응용 프로그램의 요구 사항에 따라 크게 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-176">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="10d3f-177">첫 번째 예제에서는 여러 연결 엔터티와 연결할 수 있는 사용자 엔터티를 정의하는 방법을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-177">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

<span data-ttu-id="10d3f-178">그런 다음 허브에서 아래 표시된 코드로 각 연결 상태를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-178">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a><span data-ttu-id="10d3f-179">Azure 테이블 스토리지</span><span class="sxs-lookup"><span data-stu-id="10d3f-179">Azure table storage</span></span>

<span data-ttu-id="10d3f-180">다음 Azure 테이블 저장소 예제는 데이터베이스 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-180">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="10d3f-181">Azure 테이블 저장소 서비스를 시작하는 데 필요한 모든 정보는 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-181">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="10d3f-182">자세한 내용은 [.NET 에서 테이블 저장소를 사용하는 방법을 참조하십시오.](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)</span><span class="sxs-lookup"><span data-stu-id="10d3f-182">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="10d3f-183">다음 예제에서는 연결 정보를 저장하기 위한 테이블 엔터티를 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-183">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="10d3f-184">사용자 이름으로 데이터를 분할하고 연결 ID로 각 엔터티를 식별하므로 사용자는 언제든지 여러 연결을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-184">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

<span data-ttu-id="10d3f-185">허브에서 각 사용자의 연결 상태를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="10d3f-185">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
