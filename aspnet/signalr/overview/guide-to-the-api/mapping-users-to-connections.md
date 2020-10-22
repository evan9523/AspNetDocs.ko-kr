---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: SignalR 사용자를 연결에 매핑 | Microsoft Docs
author: bradygaster
description: 이 항목에서는 사용자와 해당 연결에 대 한 정보를 유지 하는 방법을 보여 줍니다. Patrick Fletcher에서이 항목을 작성 하는 데 도움이 되었습니다. 이 항목에 사용 되는 소프트웨어 버전
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345419"
---
# <a name="mapping-signalr-users-to-connections"></a><span data-ttu-id="7576a-105">SignalR 사용자를 연결에 매핑</span><span class="sxs-lookup"><span data-stu-id="7576a-105">Mapping SignalR Users to Connections</span></span>

<span data-ttu-id="7576a-106">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="7576a-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="7576a-107">이 항목에서는 사용자와 해당 연결에 대 한 정보를 유지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-107">This topic shows how to retain information about users and their connections.</span></span>
>
> <span data-ttu-id="7576a-108">Patrick Fletcher에서이 항목을 작성 하는 데 도움이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-108">Patrick Fletcher helped write this topic.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="7576a-109">이 항목에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="7576a-109">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="7576a-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="7576a-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="7576a-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="7576a-111">.NET 4.5</span></span>
> - <span data-ttu-id="7576a-112">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="7576a-112">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="7576a-113">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="7576a-113">Previous versions of this topic</span></span>
>
> <span data-ttu-id="7576a-114">이전 버전의 SignalR에 대 한 자세한 내용은 [SignalR 이전 버전](../older-versions/index.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="7576a-114">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="7576a-115">질문 및 설명</span><span class="sxs-lookup"><span data-stu-id="7576a-115">Questions and comments</span></span>
>
> <span data-ttu-id="7576a-116">이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="7576a-116">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="7576a-117">자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-117">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="introduction"></a><span data-ttu-id="7576a-118">소개</span><span class="sxs-lookup"><span data-stu-id="7576a-118">Introduction</span></span>

<span data-ttu-id="7576a-119">허브에 연결 하는 각 클라이언트는 고유한 연결 id를 전달 합니다. 허브 컨텍스트의 속성에서이 값을 검색할 수 있습니다 `Context.ConnectionId` .</span><span class="sxs-lookup"><span data-stu-id="7576a-119">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="7576a-120">응용 프로그램에서 사용자를 연결 id에 매핑하고 해당 매핑을 유지 해야 하는 경우 다음 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-120">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- [<span data-ttu-id="7576a-121">사용자 ID 공급자 (SignalR 2)</span><span class="sxs-lookup"><span data-stu-id="7576a-121">The User ID Provider (SignalR 2)</span></span>](#IUserIdProvider)
- <span data-ttu-id="7576a-122">사전 같은 [메모리 내 저장소](#inmemory)</span><span class="sxs-lookup"><span data-stu-id="7576a-122">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="7576a-123">각 사용자에 대 한 SignalR 그룹</span><span class="sxs-lookup"><span data-stu-id="7576a-123">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="7576a-124">데이터베이스 테이블 또는 Azure table storage와 같은 [영구 외부 저장소](#database)</span><span class="sxs-lookup"><span data-stu-id="7576a-124">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="7576a-125">이러한 각 구현은이 항목에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-125">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="7576a-126">`OnConnected`클래스의, 및 메서드를 사용 하 여 `OnDisconnected` `OnReconnected` `Hub` 사용자 연결 상태를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-126">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="7576a-127">응용 프로그램에 대 한 가장 좋은 방법은 다음에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-127">The best approach for your application depends on:</span></span>

- <span data-ttu-id="7576a-128">응용 프로그램을 호스팅하는 웹 서버의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-128">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="7576a-129">현재 연결 된 사용자의 목록을 가져와야 하는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-129">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="7576a-130">응용 프로그램 또는 서버를 다시 시작할 때 그룹 및 사용자 정보를 유지 해야 하는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-130">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="7576a-131">외부 서버 호출의 대기 시간이 문제 인지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-131">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="7576a-132">다음 표에서는 이러한 고려 사항에 대해 작동 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-132">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="7576a-133">둘 이상의 서버</span><span class="sxs-lookup"><span data-stu-id="7576a-133">More than one server</span></span> | <span data-ttu-id="7576a-134">현재 연결 된 사용자 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="7576a-134">Get list of currently connected users</span></span> | <span data-ttu-id="7576a-135">다시 시작한 후 정보 유지</span><span class="sxs-lookup"><span data-stu-id="7576a-135">Persist information after restarts</span></span> | <span data-ttu-id="7576a-136">최적의 성능</span><span class="sxs-lookup"><span data-stu-id="7576a-136">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="7576a-137">UserID 공급자</span><span class="sxs-lookup"><span data-stu-id="7576a-137">UserID Provider</span></span> | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="7576a-138">메모리 내</span><span class="sxs-lookup"><span data-stu-id="7576a-138">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="7576a-139">단일 사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="7576a-139">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| <span data-ttu-id="7576a-140">영구, 외부</span><span class="sxs-lookup"><span data-stu-id="7576a-140">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a><span data-ttu-id="7576a-141">IUserID 공급자</span><span class="sxs-lookup"><span data-stu-id="7576a-141">IUserID provider</span></span>

<span data-ttu-id="7576a-142">사용자는이 기능을 사용 하 여 새 interface IUserIdProvider를 통해 IRequest를 기반으로 하는 사용자 Id를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-142">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider.</span></span>

<span data-ttu-id="7576a-143">**IUserIdProvider**</span><span class="sxs-lookup"><span data-stu-id="7576a-143">**The IUserIdProvider**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="7576a-144">기본적으로 사용자의 사용자 이름으로 사용자를 사용 하는 구현이 있습니다 `IPrincipal.Identity.Name` .</span><span class="sxs-lookup"><span data-stu-id="7576a-144">By default, there will be an implementation that uses the user's `IPrincipal.Identity.Name` as the user name.</span></span> <span data-ttu-id="7576a-145">이를 변경 하려면 `IUserIdProvider` 응용 프로그램이 시작 될 때의 구현을 전역 호스트에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-145">To change this, register your implementation of `IUserIdProvider` with the global host when your application starts:</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<span data-ttu-id="7576a-146">허브 내에서 다음 API를 통해 이러한 사용자에 게 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-146">From within a hub, you'll be able to send messages to these users via the following API:</span></span>

<span data-ttu-id="7576a-147">**특정 사용자에 게 메시지 보내기**</span><span class="sxs-lookup"><span data-stu-id="7576a-147">**Sending a message to a specific user**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="7576a-148">메모리 내 저장소</span><span class="sxs-lookup"><span data-stu-id="7576a-148">In-memory storage</span></span>

<span data-ttu-id="7576a-149">다음 예에서는 메모리에 저장 된 사전에 연결 및 사용자 정보를 유지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-149">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="7576a-150">사전은를 사용 하 여 `HashSet` 연결 id를 저장 합니다. 사용자는 언제 든 지 SignalR 응용 프로그램에 대 한 연결을 둘 이상 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-150">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="7576a-151">예를 들어 여러 장치 또는 둘 이상의 브라우저 탭을 통해 연결 된 사용자에 게는 둘 이상의 연결 id가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-151">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="7576a-152">응용 프로그램이 종료 되 면 모든 정보가 손실 되지만 사용자가 연결을 다시 설정 하면 다시 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-152">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="7576a-153">각 서버에 별도의 연결 컬렉션이 있기 때문에 환경에 둘 이상의 웹 서버가 포함 된 경우에는 메모리 내 저장소가 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-153">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="7576a-154">첫 번째 예제에서는 연결에 대 한 사용자 매핑을 관리 하는 클래스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-154">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="7576a-155">HashSet의 키는 사용자의 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-155">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="7576a-156">다음 예제에서는 허브에서 연결 매핑 클래스를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-156">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="7576a-157">클래스의 인스턴스는 변수 이름에 저장 됩니다 `_connections` .</span><span class="sxs-lookup"><span data-stu-id="7576a-157">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="7576a-158">단일 사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="7576a-158">Single-user groups</span></span>

<span data-ttu-id="7576a-159">각 사용자에 대 한 그룹을 만든 다음 해당 사용자 에게만 도달 하려는 경우 해당 그룹에 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-159">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="7576a-160">각 그룹의 이름은 사용자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-160">The name of each group is the name of the user.</span></span> <span data-ttu-id="7576a-161">사용자가 두 개 이상의 연결을 사용 하는 경우 각 연결 id는 사용자 그룹에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-161">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="7576a-162">사용자가 연결을 끊을 때 그룹에서 사용자를 수동으로 제거 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-162">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="7576a-163">이 작업은 SignalR 프레임 워크에서 자동으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-163">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="7576a-164">다음 예제에서는 단일 사용자 그룹을 구현 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-164">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="7576a-165">영구, 외부 저장소</span><span class="sxs-lookup"><span data-stu-id="7576a-165">Permanent, external storage</span></span>

<span data-ttu-id="7576a-166">이 항목에서는 데이터베이스 또는 Azure table storage를 사용 하 여 연결 정보를 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-166">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="7576a-167">이 방법은 각 웹 서버가 동일한 데이터 저장소와 상호 작용할 수 있기 때문에 여러 웹 서버를 사용 하는 경우 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-167">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="7576a-168">웹 서버의 작동이 중지 되거나 응용 프로그램이 다시 시작 `OnDisconnected` 되 면 메서드가 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-168">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="7576a-169">따라서 데이터 리포지토리에 더 이상 유효 하지 않은 연결 id 레코드가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-169">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="7576a-170">이러한 분리 된 레코드를 정리 하려면 응용 프로그램과 관련 된 시간 범위 밖에 서 만들어진 모든 연결을 무효화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-170">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="7576a-171">이 섹션의 예에는 연결을 만들 때 추적 하는 값이 포함 되어 있지만이를 백그라운드 프로세스로 수행 하려는 경우에는 오래 된 레코드를 정리 하는 방법은 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-171">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="7576a-172">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="7576a-172">Database</span></span>

<span data-ttu-id="7576a-173">다음 예에서는 데이터베이스에서 연결 및 사용자 정보를 유지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-173">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="7576a-174">모든 데이터 액세스 기술을 사용할 수 있습니다. 그러나 다음 예에서는 Entity Framework를 사용 하 여 모델을 정의 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-174">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="7576a-175">이러한 엔터티 모델은 데이터베이스 테이블 및 필드에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-175">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="7576a-176">데이터 구조는 응용 프로그램의 요구 사항에 따라 크게 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-176">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="7576a-177">첫 번째 예제에서는 많은 연결 엔터티와 연결 될 수 있는 사용자 엔터티를 정의 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-177">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

<span data-ttu-id="7576a-178">그런 다음 허브에서 아래와 같은 코드를 사용 하 여 각 연결의 상태를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-178">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a><span data-ttu-id="7576a-179">Azure 테이블 스토리지</span><span class="sxs-lookup"><span data-stu-id="7576a-179">Azure table storage</span></span>

<span data-ttu-id="7576a-180">다음 Azure table storage 예는 데이터베이스 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-180">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="7576a-181">Azure Table Storage 서비스를 시작 하는 데 필요한 일부 정보는 포함 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-181">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="7576a-182">자세한 내용은 [.net에서 테이블 저장소를 사용 하는 방법을](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="7576a-182">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="7576a-183">다음 예에서는 연결 정보를 저장 하기 위한 테이블 엔터티를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-183">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="7576a-184">사용자 이름으로 데이터를 분할 하 고 각 엔터티를 연결 id로 식별 하므로 사용자는 언제 든 지 여러 연결을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-184">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

<span data-ttu-id="7576a-185">허브에서 각 사용자의 연결 상태를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="7576a-185">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
