---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: ASP.NET 시그널R 허브 API 가이드 - 서버(C#) | 마이크로 소프트 문서
author: bradygaster
description: 이 문서에서는 SignalR 버전 2에 대한 ASP.NET SignalR Hubs API의 서버 측면을 프로그래밍하는 방법을 소개하며 코드 샘플을 시연합니다.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675804"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a><span data-ttu-id="96eb3-103">ASP.NET 시그널R 허브 API 가이드 - 서버(C#)</span><span class="sxs-lookup"><span data-stu-id="96eb3-103">ASP.NET SignalR Hubs API Guide - Server (C#)</span></span>

<span data-ttu-id="96eb3-104">로 [패트릭 플레처,](https://github.com/pfletcher) [톰 다이크스트라](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="96eb3-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="96eb3-105">이 문서에서는 SignalR 버전 2에 대한 ASP.NET SignalR Hubs API의 서버 측면을 프로그래밍하는 방법을 소개하며, 공통 옵션을 보여 주는 코드 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 2, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="96eb3-106">SignalR Hubs API를 사용하면 서버에서 연결된 클라이언트로, 클라이언트에서 서버로 원격 프로시저 호출(RPC)을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="96eb3-107">서버 코드에서 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="96eb3-108">클라이언트 코드에서는 서버에서 호출할 수 있는 메서드를 정의하고 서버에서 실행되는 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="96eb3-109">SignalR은 모든 클라이언트-서버 배관을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="96eb3-110">SignalR는 또한 영구 연결이라는 하위 수준 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="96eb3-111">SignalR, 허브 및 영구 연결에 대한 소개는 [SignalR 2 소개를](../getting-started/introduction-to-signalr.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="96eb3-111">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR 2](../getting-started/introduction-to-signalr.md).</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="96eb3-112">이 항목에 사용된 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="96eb3-112">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="96eb3-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="96eb3-113">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="96eb3-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="96eb3-114">.NET 4.5</span></span>
> - <span data-ttu-id="96eb3-115">시그널R 버전 2</span><span class="sxs-lookup"><span data-stu-id="96eb3-115">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="topic-versions"></a><span data-ttu-id="96eb3-116">주제 버전</span><span class="sxs-lookup"><span data-stu-id="96eb3-116">Topic versions</span></span>
> 
> <span data-ttu-id="96eb3-117">이전 버전의 SignalR에 대한 자세한 내용은 [SignalR 이전 버전을](../older-versions/index.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="96eb3-117">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="96eb3-118">질문 및 의견</span><span class="sxs-lookup"><span data-stu-id="96eb3-118">Questions and comments</span></span>
> 
> <span data-ttu-id="96eb3-119">이 자습서를 어떻게 좋아했는지, 그리고 페이지 하단의 댓글에서 개선할 수 있는 내용에 대한 피드백을 남겨주세요.</span><span class="sxs-lookup"><span data-stu-id="96eb3-119">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="96eb3-120">당신은 튜토리얼과 직접 관련이없는 질문이있는 경우, 당신은 [ASP.NET SignalR 포럼에](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 게시하거나 [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="96eb3-120">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="96eb3-121">개요</span><span class="sxs-lookup"><span data-stu-id="96eb3-121">Overview</span></span>

<span data-ttu-id="96eb3-122">이 문서는 다음 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-122">This document contains the following sections:</span></span>

- [<span data-ttu-id="96eb3-123">SignalR 미들웨어를 등록하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-123">How to register SignalR middleware</span></span>](#route)

    - [<span data-ttu-id="96eb3-124">/시그널러 URL</span><span class="sxs-lookup"><span data-stu-id="96eb3-124">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="96eb3-125">신호R 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="96eb3-125">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="96eb3-126">허브 클래스를 만들고 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-126">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="96eb3-127">허브 개체 수명</span><span class="sxs-lookup"><span data-stu-id="96eb3-127">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="96eb3-128">자바 스크립트 클라이언트에서 허브 이름의 낙타 케이스</span><span class="sxs-lookup"><span data-stu-id="96eb3-128">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="96eb3-129">다중 허브</span><span class="sxs-lookup"><span data-stu-id="96eb3-129">Multiple Hubs</span></span>](#multiplehubs)
    - [<span data-ttu-id="96eb3-130">강력한 형식의 허브</span><span class="sxs-lookup"><span data-stu-id="96eb3-130">Strongly-Typed Hubs</span></span>](#stronglytypedhubs)
- [<span data-ttu-id="96eb3-131">클라이언트가 호출할 수 있는 Hub 클래스에서 메서드를 정의하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-131">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="96eb3-132">자바 스크립트 클라이언트에서 메소드 이름의 낙타 대/소문자</span><span class="sxs-lookup"><span data-stu-id="96eb3-132">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="96eb3-133">비동기적으로 실행되는 경우</span><span class="sxs-lookup"><span data-stu-id="96eb3-133">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="96eb3-134">오버로드 정의</span><span class="sxs-lookup"><span data-stu-id="96eb3-134">Defining overloads</span></span>](#overloads)
    - [<span data-ttu-id="96eb3-135">허브 메서드 호출에서 진행률 보고</span><span class="sxs-lookup"><span data-stu-id="96eb3-135">Reporting progress from hub method invocations</span></span>](#progress)
- [<span data-ttu-id="96eb3-136">Hub 클래스에서 클라이언트 메서드를 호출하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-136">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="96eb3-137">RPC를 받을 클라이언트 선택</span><span class="sxs-lookup"><span data-stu-id="96eb3-137">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="96eb3-138">메서드 이름에 대한 컴파일 타임 유효성 검사가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-138">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="96eb3-139">대/소문자 구분 메서드 이름 일치</span><span class="sxs-lookup"><span data-stu-id="96eb3-139">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="96eb3-140">비동기 실행</span><span class="sxs-lookup"><span data-stu-id="96eb3-140">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="96eb3-141">허브 클래스에서 그룹 구성원을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-141">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="96eb3-142">메서드 추가 및 제거의 비동기 실행</span><span class="sxs-lookup"><span data-stu-id="96eb3-142">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="96eb3-143">그룹 구성원 유지</span><span class="sxs-lookup"><span data-stu-id="96eb3-143">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="96eb3-144">단일 사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="96eb3-144">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="96eb3-145">Hub 클래스에서 연결 수명 이벤트를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-145">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="96eb3-146">연결 됨, 연결이 끊긴 및 다시 연결해제된 경우</span><span class="sxs-lookup"><span data-stu-id="96eb3-146">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="96eb3-147">호출자 상태가 채워지지 않음</span><span class="sxs-lookup"><span data-stu-id="96eb3-147">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="96eb3-148">Context 속성에서 클라이언트에 대 한 정보를 얻는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-148">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="96eb3-149">클라이언트와 Hub 클래스 간에 상태를 전달하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-149">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="96eb3-150">Hub 클래스에서 오류를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-150">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="96eb3-151">클라이언트 메서드를 호출하고 Hub 클래스 외부에서 그룹을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-151">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="96eb3-152">클라이언트 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="96eb3-152">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="96eb3-153">그룹 구성원 관리</span><span class="sxs-lookup"><span data-stu-id="96eb3-153">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="96eb3-154">추적을 활성화하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-154">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="96eb3-155">허브 파이프라인을 사용자 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-155">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="96eb3-156">클라이언트를 프로그래밍하는 방법에 대한 설명서는 다음 리소스를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="96eb3-156">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="96eb3-157">시그널R 허브 API 가이드 - 자바 스크립트 클라이언트</span><span class="sxs-lookup"><span data-stu-id="96eb3-157">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)
- [<span data-ttu-id="96eb3-158">시그널R 허브 API 가이드 - .NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="96eb3-158">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="96eb3-159">SignalR 2의 서버 구성 요소는 .NET 4.5에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-159">The server components for SignalR 2 are only available in .NET 4.5.</span></span> <span data-ttu-id="96eb3-160">.NET 4.0을 실행하는 서버는 SignalR v1.x를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-160">Servers running .NET 4.0 must use SignalR v1.x.</span></span>

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a><span data-ttu-id="96eb3-161">SignalR 미들웨어를 등록하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-161">How to register SignalR middleware</span></span>

<span data-ttu-id="96eb3-162">클라이언트가 Hub에 연결하는 데 사용할 경로를 정의하려면 `MapSignalR` 응용 프로그램이 시작될 때 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-162">To define the route that clients will use to connect to your Hub, call the `MapSignalR` method when the application starts.</span></span> <span data-ttu-id="96eb3-163">`MapSignalR`는 클래스의 확장 `OwinExtensions` [메서드입니다.](https://msdn.microsoft.com/library/vstudio/bb383977.aspx)</span><span class="sxs-lookup"><span data-stu-id="96eb3-163">`MapSignalR` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `OwinExtensions` class.</span></span> <span data-ttu-id="96eb3-164">다음 예제에서는 OWIN 시작 클래스를 사용하여 SignalR 허브 경로를 정의하는 방법을 보여 주습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-164">The following example shows how to define the SignalR Hubs route using an OWIN startup class.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

<span data-ttu-id="96eb3-165">ASP.NET MVC 응용 프로그램에 SignalR 기능을 추가하는 경우 SignalR 경로가 다른 경로보다 앞에 추가되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-165">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="96eb3-166">자세한 내용은 [자습서: SignalR 2 및 MVC 5로 시작하기](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="96eb3-166">For more information, see [Tutorial: Getting Started with SignalR 2 and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="96eb3-167">/시그널러 URL</span><span class="sxs-lookup"><span data-stu-id="96eb3-167">The /signalr URL</span></span>

<span data-ttu-id="96eb3-168">기본적으로 클라이언트가 허브에 연결하는 데 사용할 경로 URL은 "/signalr"입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-168">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="96eb3-169">(이 URL을 자동으로 생성된 JavaScript 파일에 대한 "/시그널러/허브" URL과 혼동하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="96eb3-169">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="96eb3-170">생성된 프록시에 대한 자세한 내용은 [SignalR 허브 API 가이드 - JavaScript 클라이언트 - 생성된 프록시 및 프록시가 수행하는 작업을](hubs-api-guide-javascript-client.md#genproxy)참조하십시오.)</span><span class="sxs-lookup"><span data-stu-id="96eb3-170">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).)</span></span>

<span data-ttu-id="96eb3-171">이 기본 URL을 SignalR에 사용할 수 없게 만드는 특별한 상황이 있을 수 있습니다. 예를 들어 프로젝트에 *signalr라는* 폴더가 있고 이름을 변경하지 않으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-171">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="96eb3-172">이 경우 다음 예제와 같이 기본 URL을 변경할 수 있습니다(샘플 코드의 "/signalr"를 원하는 URL로 바꿉니다).</span><span class="sxs-lookup"><span data-stu-id="96eb3-172">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="96eb3-173">**URL을 지정하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="96eb3-173">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

<span data-ttu-id="96eb3-174">**URL을 지정하는 JavaScript 클라이언트 코드(생성된 프록시).**</span><span class="sxs-lookup"><span data-stu-id="96eb3-174">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

<span data-ttu-id="96eb3-175">**URL을 지정하는 JavaScript 클라이언트 코드(생성된 프록시 제외)**</span><span class="sxs-lookup"><span data-stu-id="96eb3-175">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="96eb3-176">**URL을 지정하는 .NET 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="96eb3-176">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="96eb3-177">신호 R 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="96eb3-177">Configuring SignalR Options</span></span>

<span data-ttu-id="96eb3-178">메서드의 오버로드를 `MapSignalR` 사용하면 사용자 지정 URL, 사용자 지정 종속성 확인자 및 다음 옵션을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-178">Overloads of the `MapSignalR` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="96eb3-179">브라우저 클라이언트에서 CORS 또는 JSONP를 사용하여 도메인 간 호출을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-179">Enable cross-domain calls using CORS or JSONP from browser clients.</span></span>

    <span data-ttu-id="96eb3-180">일반적으로 브라우저에서 페이지를 로드하는 경우 `http://contoso.com`에서 SignalR 연결이 동일한 `http://contoso.com/signalr`도메인에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-180">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="96eb3-181">에서 `http://contoso.com` 페이지가 `http://fabrikam.com/signalr`에 연결하는 경우 도메인 간 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-181">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="96eb3-182">보안상의 이유로 도메인 간 연결은 기본적으로 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-182">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="96eb3-183">자세한 내용은 [ASP.NET SignalR 허브 API 가이드 - JavaScript 클라이언트 - 도메인 간 연결을 설정하는 방법을](hubs-api-guide-javascript-client.md#crossdomain)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="96eb3-183">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](hubs-api-guide-javascript-client.md#crossdomain).</span></span>
- <span data-ttu-id="96eb3-184">자세한 오류 메시지를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-184">Enable detailed error messages.</span></span>

    <span data-ttu-id="96eb3-185">오류가 발생하면 SignalR의 기본 동작은 무슨 일이 있었는지에 대한 세부 정보없이 클라이언트에게 알림 메시지를 보내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-185">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="96eb3-186">악의적인 사용자가 응용 프로그램에 대한 공격에서 정보를 사용할 수 있으므로 프로덕션 환경에서는 자세한 오류 정보를 클라이언트에 보내는 것이 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-186">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="96eb3-187">문제 해결을 위해 이 옵션을 사용하여 보다 유용한 오류 보고를 일시적으로 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-187">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="96eb3-188">자동으로 생성된 자바스크립트 프록시 파일을 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-188">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="96eb3-189">기본적으로 허브 클래스에 대한 프록시가 있는 JavaScript 파일은 URL "/signalr/hubs"에 대한 응답으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-189">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="96eb3-190">JavaScript 프록시를 사용하지 않으려거나 이 파일을 수동으로 생성하고 클라이언트의 실제 파일을 참조하려는 경우 이 옵션을 사용하여 프록시 생성을 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-190">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="96eb3-191">자세한 내용은 [SignalR 허브 API 가이드 - JavaScript 클라이언트 - SignalR 생성 프록시에 대한 실제 파일을 만드는 방법을](hubs-api-guide-javascript-client.md#manualproxy)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="96eb3-191">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](hubs-api-guide-javascript-client.md#manualproxy).</span></span>

<span data-ttu-id="96eb3-192">다음 예제에서는 `MapSignalR` 메서드를 호출할 때 SignalR 연결 URL 및 이러한 옵션을 지정 하는 방법을 보여 주입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-192">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapSignalR` method.</span></span> <span data-ttu-id="96eb3-193">사용자 지정 URL을 지정하려면 예제의 "/signalr"를 사용하려는 URL로 바꿉습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-193">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="96eb3-194">허브 클래스를 만들고 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-194">How to create and use Hub classes</span></span>

<span data-ttu-id="96eb3-195">허브를 만들려면 [Microsoft.Aspnet.Signalr.Hub에서](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)파생된 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-195">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="96eb3-196">다음 예제에서는 채팅 응용 프로그램에 대 한 간단한 Hub 클래스를 보여 주다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-196">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

<span data-ttu-id="96eb3-197">이 예제에서는 연결된 클라이언트가 `NewContosoChatMessage` 메서드를 호출할 수 있으며, 이 경우 수신된 데이터는 연결된 모든 클라이언트에 브로드캐스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-197">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="96eb3-198">허브 개체 수명</span><span class="sxs-lookup"><span data-stu-id="96eb3-198">Hub object lifetime</span></span>

<span data-ttu-id="96eb3-199">Hub 클래스를 인스턴스화하거나 서버의 사용자 고유 코드에서 메서드를 호출하지 않습니다. SignalR 허브 파이프라인을 통해 모든 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-199">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="96eb3-200">SignalR은 클라이언트가 서버에 연결, 연결 해제 또는 메서드 호출을 할 때와 같이 Hub 작업을 처리해야 할 때마다 Hub 클래스의 새 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-200">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="96eb3-201">Hub 클래스의 인스턴스는 일시적이기 때문에 한 메서드 호출에서 다음 메서드 호출로 상태를 유지하는 데 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-201">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="96eb3-202">서버가 클라이언트에서 메서드 호출을 받을 때마다 Hub 클래스의 새 인스턴스가 메시지를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-202">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="96eb3-203">여러 연결 및 메서드 호출을 통해 상태를 유지하려면 데이터베이스 또는 Hub 클래스의 정적 변수 또는 에서 파생되지 `Hub`않는 다른 클래스와 같은 다른 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-203">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="96eb3-204">Hub 클래스의 정적 변수와 같은 메서드를 사용하여 메모리에 데이터를 유지하면 앱 도메인이 재활용될 때 데이터가 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-204">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="96eb3-205">Hub 클래스 외부에서 실행되는 고유한 코드에서 클라이언트에 메시지를 보내려면 Hub 클래스 인스턴스를 인스턴스화하여 클라이언트에 메시지를 보낼 수 없지만 Hub 클래스에 대한 SignalR 컨텍스트 개체에 대한 참조를 얻어서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-205">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="96eb3-206">자세한 내용은 [이 항목의 후반부Hub 클래스 외부에서 클라이언트 메서드를 호출하고 그룹을 관리하는 방법을](#callfromoutsidehub) 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96eb3-206">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="96eb3-207">자바 스크립트 클라이언트에서 허브 이름의 낙타 케이스</span><span class="sxs-lookup"><span data-stu-id="96eb3-207">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="96eb3-208">기본적으로 JavaScript 클라이언트는 클래스 이름의 낙타 대/소문자 버전을 사용하여 Hubs를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-208">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="96eb3-209">SignalR은 자바스크립트 코드가 자바스크립트 규칙을 준수할 수 있도록 자동으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-209">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="96eb3-210">이전 예제는 자바스크립트 `contosoChatHub` 코드에서 와 같이 참조될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-210">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="96eb3-211">**Server**</span><span class="sxs-lookup"><span data-stu-id="96eb3-211">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

<span data-ttu-id="96eb3-212">**생성된 프록시를 사용하는 자바스크립트 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="96eb3-212">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

<span data-ttu-id="96eb3-213">클라이언트에서 사용할 다른 이름을 지정하려면 특성을 `HubName` 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-213">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="96eb3-214">특성을 `HubName` 사용하면 JavaScript 클라이언트에서 camel 대/소문자에 대한 이름 변경이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-214">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="96eb3-215">**Server**</span><span class="sxs-lookup"><span data-stu-id="96eb3-215">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

<span data-ttu-id="96eb3-216">**생성된 프록시를 사용하는 자바스크립트 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="96eb3-216">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="96eb3-217">다중 허브</span><span class="sxs-lookup"><span data-stu-id="96eb3-217">Multiple Hubs</span></span>

<span data-ttu-id="96eb3-218">응용 프로그램에서 여러 Hub 클래스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-218">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="96eb3-219">이렇게 하면 연결이 공유되지만 그룹은 분리됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-219">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="96eb3-220">모든 클라이언트는 동일한 URL을 사용하여 서비스와 SignalR 연결을 설정합니다("/signalr" 또는 사용자 지정 URL을 지정한 경우) 해당 연결은 서비스에 의해 정의된 모든 Hubs에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-220">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="96eb3-221">단일 클래스의 모든 Hub 기능을 정의하는 것과 비교하여 여러 Hubs의 성능 차이는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-221">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="96eb3-222">모든 허브는 동일한 HTTP 요청 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-222">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="96eb3-223">모든 허브가 동일한 연결을 공유하기 때문에 서버가 받는 유일한 HTTP 요청 정보는 SignalR 연결을 설정하는 원래 HTTP 요청에 들어오는 정보뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-223">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="96eb3-224">연결 요청을 사용하여 쿼리 문자열을 지정하여 클라이언트에서 서버로 정보를 전달하는 경우 다른 Hubs에 다른 쿼리 문자열을 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-224">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="96eb3-225">모든 허브는 동일한 정보를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-225">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="96eb3-226">생성된 JavaScript 프록시 파일에는 하나의 파일에 있는 모든 허브에 대한 프록시가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-226">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="96eb3-227">자바 스크립트 프록시에 대한 자세한 내용은 [SignalR 허브 API 가이드 - 자바 스크립트 클라이언트 - 생성 된 프록시 및 당신을 위해 무엇을 참조하십시오](hubs-api-guide-javascript-client.md#genproxy).</span><span class="sxs-lookup"><span data-stu-id="96eb3-227">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).</span></span>
- <span data-ttu-id="96eb3-228">그룹은 허브 내에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-228">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="96eb3-229">SignalR에서 연결된 클라이언트의 하위 집합으로 브로드캐스트할 명명된 그룹을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-229">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="96eb3-230">그룹은 각 허브에 대해 별도로 유지 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-230">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="96eb3-231">예를 들어 "Administrators"라는 그룹에는 `ContosoChatHub` 클래스에 대한 하나의 클라이언트 집합이 포함되고 동일한 그룹 이름은 클래스에 대해 다른 클라이언트 집합을 참조합니다. `StockTickerHub`</span><span class="sxs-lookup"><span data-stu-id="96eb3-231">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a><span data-ttu-id="96eb3-232">강력한 형식의 허브</span><span class="sxs-lookup"><span data-stu-id="96eb3-232">Strongly-Typed Hubs</span></span>

<span data-ttu-id="96eb3-233">클라이언트가 참조할 수 있는 허브 메서드에 대한 인터페이스를 정의하고 허브 메서드에서 Intellisense를 사용하도록 설정하려면 다음이 아닌 `Hub<T>` `Hub`(SignalR 2.1에 소개됨)에서 허브를 파생합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-233">To define an interface for your hub methods that your client can reference (and enable Intellisense on your hub methods), derive your hub from `Hub<T>` (introduced in SignalR 2.1) rather than `Hub`:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="96eb3-234">클라이언트가 호출할 수 있는 Hub 클래스에서 메서드를 정의하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-234">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="96eb3-235">클라이언트에서 호출할 수 있도록 허브에 메서드를 노출하려면 다음 예제와 같이 public 메서드를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-235">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="96eb3-236">C# 메서드에서와 마찬가지로 복잡한 형식 및 배열을 포함하여 반환 형식 및 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-236">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="96eb3-237">매개 변수에서 수신하거나 호출자에게 반환하는 모든 데이터는 JSON을 사용하여 클라이언트와 서버 간에 통신되며 SignalR는 복잡한 개체와 개체 배열의 바인딩을 자동으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-237">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="96eb3-238">자바 스크립트 클라이언트에서 메소드 이름의 낙타 대/소문자</span><span class="sxs-lookup"><span data-stu-id="96eb3-238">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="96eb3-239">기본적으로 JavaScript 클라이언트는 메서드 이름의 낙타 대/소문자 버전을 사용하여 Hub 메서드를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-239">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="96eb3-240">SignalR은 자바스크립트 코드가 자바스크립트 규칙을 준수할 수 있도록 자동으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-240">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="96eb3-241">**Server**</span><span class="sxs-lookup"><span data-stu-id="96eb3-241">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="96eb3-242">**생성된 프록시를 사용하는 자바스크립트 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="96eb3-242">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="96eb3-243">클라이언트에서 사용할 다른 이름을 지정하려면 특성을 `HubMethodName` 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-243">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="96eb3-244">**Server**</span><span class="sxs-lookup"><span data-stu-id="96eb3-244">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="96eb3-245">**생성된 프록시를 사용하는 자바스크립트 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="96eb3-245">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="96eb3-246">비동기적으로 실행되는 경우</span><span class="sxs-lookup"><span data-stu-id="96eb3-246">When to execute asynchronously</span></span>

<span data-ttu-id="96eb3-247">메서드가 장기 실행되거나 데이터베이스 조회 또는 웹 서비스 호출과 같이 대기가 포함된 작업을 수행해야 하는 경우 반환 대신 `void` [작업(반환](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 대신) 또는 [&lt;Task&gt; T](https://msdn.microsoft.com/library/dd321424.aspx) `T` 개체(반환 형식 대신)를 반환하여 Hub 메서드를 비동기로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-247">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="96eb3-248">메서드에서 개체를 `Task` 반환하면 SignalR이 `Task` 완료될 때까지 기다렸다가 래핑되지 않은 결과를 클라이언트로 다시 보내므로 클라이언트에서 메서드 호출을 코딩하는 방법에 는 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-248">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="96eb3-249">Hub 메서드를 비동기로 만들면 WebSocket 전송을 사용할 때 연결이 차단되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-249">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="96eb3-250">Hub 메서드가 동기적으로 실행되고 전송이 WebSocket인 경우 허브 메서드가 완료될 때까지 동일한 클라이언트에서 허브에 대한 메서드의 후속 호출이 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-250">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="96eb3-251">다음 예제에서는 동기 또는 비동기적으로 실행되도록 코딩된 동일한 메서드를 보여 주며, 그 다음에는 두 버전 중 하나를 호출하는 데 적합한 JavaScript 클라이언트 코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-251">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="96eb3-252">**동기**</span><span class="sxs-lookup"><span data-stu-id="96eb3-252">**Synchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="96eb3-253">**비동기**</span><span class="sxs-lookup"><span data-stu-id="96eb3-253">**Asynchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="96eb3-254">**생성된 프록시를 사용하는 자바스크립트 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="96eb3-254">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="96eb3-255">ASP.NET 4.5에서 비동기 메서드를 사용하는 방법에 대한 자세한 내용은 [ASP.NET MVC 4에서 비동기 메서드 사용을](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="96eb3-255">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="96eb3-256">오버로드 정의</span><span class="sxs-lookup"><span data-stu-id="96eb3-256">Defining Overloads</span></span>

<span data-ttu-id="96eb3-257">메서드에 대한 오버로드를 정의하려면 각 오버로드의 매개 변수 수가 달라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-257">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="96eb3-258">다른 매개 변수 형식을 지정하는 것만으로 오버로드를 구별하면 Hub 클래스가 컴파일되지만 클라이언트가 오버로드 중 하나를 호출하려고 할 때 SignalR 서비스가 런타임에 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-258">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a><span data-ttu-id="96eb3-259">허브 메서드 호출에서 진행률 보고</span><span class="sxs-lookup"><span data-stu-id="96eb3-259">Reporting progress from hub method invocations</span></span>

<span data-ttu-id="96eb3-260">SignalR 2.1은 .NET 4.5에 도입된 [진행률 보고 패턴에](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) 대한 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-260">SignalR 2.1 adds support for the [progress reporting pattern](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) introduced in .NET 4.5.</span></span> <span data-ttu-id="96eb3-261">진행률 보고를 구현하려면 `IProgress<T>` 클라이언트가 액세스할 수 있는 허브 메서드에 대한 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-261">To implement progress reporting, define an `IProgress<T>` parameter for your hub method that your client can access:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

<span data-ttu-id="96eb3-262">장기 실행 서버 메서드를 작성할 때는 허브 스레드를 차단하는 대신 Async/Await와 같은 비동기 프로그래밍 패턴을 사용하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-262">When writing a long-running server method, it is important to use an asynchronous programming pattern like Async/ Await rather than blocking the hub thread.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="96eb3-263">Hub 클래스에서 클라이언트 메서드를 호출하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-263">How to call client methods from the Hub class</span></span>

<span data-ttu-id="96eb3-264">서버에서 클라이언트 메서드를 호출하려면 `Clients` Hub 클래스의 메서드에서 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-264">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="96eb3-265">다음 예제에서는 연결된 모든 `addNewMessageToPage` 클라이언트를 호출하는 서버 코드와 JavaScript 클라이언트에서 메서드를 정의하는 클라이언트 코드를 보여 주습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-265">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="96eb3-266">**Server**</span><span class="sxs-lookup"><span data-stu-id="96eb3-266">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

<span data-ttu-id="96eb3-267">클라이언트 메서드를 호출하는 것은 비동기 작업이며 `Task`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-267">Invoking a client method is an asynchronous operation and returns a `Task`.</span></span> <span data-ttu-id="96eb3-268">`await`는 다음 용도로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-268">Use `await`:</span></span>

* <span data-ttu-id="96eb3-269">메시지가 오류 없이 전송되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-269">To ensure the message is sent without error.</span></span> 
* <span data-ttu-id="96eb3-270">시도 캐치 블록에서 오류를 catch하고 처리하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-270">To enable catching and handling errors in a try-catch block.</span></span>

<span data-ttu-id="96eb3-271">**생성된 프록시를 사용하는 자바스크립트 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="96eb3-271">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

<span data-ttu-id="96eb3-272">클라이언트 메서드에서 반환 값을 얻을 수 없습니다. 같은 `int x = Clients.All.add(1,1)` 구문이 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-272">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="96eb3-273">매개 변수에 대한 복잡한 형식과 배열을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-273">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="96eb3-274">다음 예제에서는 메서드 매개 변수에서 클라이언트에 복잡 한 형식을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-274">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="96eb3-275">**복잡한 개체를 사용하여 클라이언트 메서드를 호출하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="96eb3-275">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

<span data-ttu-id="96eb3-276">**복잡한 개체를 정의하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="96eb3-276">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

<span data-ttu-id="96eb3-277">**생성된 프록시를 사용하는 자바스크립트 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="96eb3-277">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="96eb3-278">RPC를 받을 클라이언트 선택</span><span class="sxs-lookup"><span data-stu-id="96eb3-278">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="96eb3-279">Client 속성은 RPC를 받을 클라이언트를 지정하기 위한 몇 가지 옵션을 제공하는 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-279">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="96eb3-280">연결된 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-280">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="96eb3-281">호출 클라이언트만.</span><span class="sxs-lookup"><span data-stu-id="96eb3-281">Only the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="96eb3-282">호출 클라이언트를 제외한 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-282">All clients except the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- <span data-ttu-id="96eb3-283">연결 ID로 식별된 특정 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-283">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    <span data-ttu-id="96eb3-284">이 예제는 호출 클라이언트를 호출하며 `addContosoChatMessageToPage` 을 `Clients.Caller`사용하는 것과 동일한 효과를 가짐을 가짐을 가시고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-284">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="96eb3-285">연결 ID로 식별된 지정된 클라이언트를 제외한 연결된 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-285">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- <span data-ttu-id="96eb3-286">지정된 그룹의 연결된 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-286">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- <span data-ttu-id="96eb3-287">연결 ID로 식별된 지정된 클라이언트를 제외한 지정된 그룹의 모든 연결된 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-287">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- <span data-ttu-id="96eb3-288">호출 클라이언트를 제외한 지정된 그룹의 연결된 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-288">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- <span data-ttu-id="96eb3-289">userId로 식별된 특정 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-289">A specific user, identified by userId.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    <span data-ttu-id="96eb3-290">기본적으로 이것은 `IPrincipal.Identity.Name`에서이지만 [IUserIdProvider의 구현을 전역 호스트에 등록하여](mapping-users-to-connections.md#IUserIdProvider)변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-290">By default, this is `IPrincipal.Identity.Name`, but this can be changed by [registering an implementation of IUserIdProvider with the global host](mapping-users-to-connections.md#IUserIdProvider).</span></span>
- <span data-ttu-id="96eb3-291">연결 아이디 목록의 모든 클라이언트 및 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-291">All clients and groups in a list of connection IDs.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- <span data-ttu-id="96eb3-292">그룹 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-292">A list of groups.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- <span data-ttu-id="96eb3-293">이름으로 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-293">A user by name.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- <span data-ttu-id="96eb3-294">사용자 이름 목록(SignalR 2.1에 소개).</span><span class="sxs-lookup"><span data-stu-id="96eb3-294">A list of user names (introduced in SignalR 2.1).</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="96eb3-295">메서드 이름에 대한 컴파일 타임 유효성 검사가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-295">No compile-time validation for method names</span></span>

<span data-ttu-id="96eb3-296">지정한 메서드 이름은 동적 개체로 해석되므로 IntelliSense 또는 컴파일 타임 유효성 검사가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-296">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="96eb3-297">식은 런타임에 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-297">The expression is evaluated at run time.</span></span> <span data-ttu-id="96eb3-298">메서드 호출이 실행되면 SignalR은 메서드 이름과 매개 변수 값을 클라이언트에 보내고 클라이언트에 이름과 일치하는 메서드가 있는 경우 해당 메서드가 호출되고 매개 변수 값이 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-298">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="96eb3-299">클라이언트에서 일치하는 메서드를 찾을 수 없는 경우 오류가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-299">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="96eb3-300">SignalR이 클라이언트 메서드를 호출할 때 장면 뒤에서 클라이언트에게 전송하는 데이터의 형식에 대한 자세한 내용은 [SignalR 소개를](../getting-started/introduction-to-signalr.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="96eb3-300">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="96eb3-301">대/소문자 구분 메서드 이름 일치</span><span class="sxs-lookup"><span data-stu-id="96eb3-301">Case-insensitive method name matching</span></span>

<span data-ttu-id="96eb3-302">메서드 이름 일치는 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-302">Method name matching is case-insensitive.</span></span> <span data-ttu-id="96eb3-303">예를 들어 `Clients.All.addContosoChatMessageToPage` 서버에서 를 `AddContosoChatMessageToPage` `addcontosochatmessagetopage`실행하거나 `addContosoChatMessageToPage` 클라이언트에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-303">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="96eb3-304">비동기 실행</span><span class="sxs-lookup"><span data-stu-id="96eb3-304">Asynchronous execution</span></span>

<span data-ttu-id="96eb3-305">호출하는 메서드가 비동기적으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-305">The method that you call executes asynchronously.</span></span> <span data-ttu-id="96eb3-306">후속 코드 줄이 메서드 완료를 기다려야 한다고 지정하지 않는 한 SignalR이 클라이언트에 데이터 전송을 완료할 때까지 기다리지 않고 클라이언트에 대한 메서드 호출 후에 발생하는 모든 코드는 즉시 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-306">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="96eb3-307">다음 코드 예제에서는 두 클라이언트 메서드를 순차적으로 실행하는 방법을 보여 주십니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-307">The following code example shows how to execute two client methods sequentially.</span></span>

<span data-ttu-id="96eb3-308">**대기 중 사용(.NET 4.5)**</span><span class="sxs-lookup"><span data-stu-id="96eb3-308">**Using Await (.NET 4.5)**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="96eb3-309">다음 코드 `await` 줄이 실행되기 전에 클라이언트 메서드가 끝날 때까지 기다리는 데 사용하는 경우 다음 코드 줄이 실행되기 전에 클라이언트가 실제로 메시지를 수신한다는 의미는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-309">If you use `await` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="96eb3-310">클라이언트 메서드 호출의 "완료"는 SignalR이 메시지를 보내는 데 필요한 모든 작업을 수행했음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-310">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="96eb3-311">클라이언트가 메시지를 받았는지 확인해야 하는 경우 해당 메커니즘을 직접 프로그래밍해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-311">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="96eb3-312">예를 들어 Hub에서 `MessageReceived` 메서드를 코딩할 수 `addContosoChatMessageToPage` 있으며 클라이언트의 메서드에서 `MessageReceived` 클라이언트에서 수행해야 하는 작업을 수행한 후 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-312">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="96eb3-313">Hub에서 `MessageReceived` 실제 클라이언트 수신 및 원래 메서드 호출 처리에 따라 모든 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-313">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="96eb3-314">문자열 변수를 메서드 이름으로 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-314">How to use a string variable as the method name</span></span>

<span data-ttu-id="96eb3-315">문자열 변수를 메서드 `Clients.All` 이름으로 `Clients.Others` `Clients.Caller`사용하여 클라이언트 메서드를 호출하려면 `IClientProxy` [Invoke(메서드Name, args...)를](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)호출합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-315">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="96eb3-316">허브 클래스에서 그룹 구성원을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-316">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="96eb3-317">SignalR의 그룹은 연결된 클라이언트의 지정된 하위 집합에 메시지를 브로드캐스트하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-317">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="96eb3-318">그룹에는 원하는 수의 클라이언트가 있을 수 있으며 클라이언트는 원하는 수의 그룹의 구성원이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-318">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="96eb3-319">그룹 구성원 자격을 관리하려면 [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) Hub 클래스의 `Groups` 속성에서 제공하는 [추가](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) 및 제거 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-319">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="96eb3-320">다음 예제에서는 `Groups.Add` 클라이언트 `Groups.Remove` 코드에서 호출되는 Hub 메서드와 이를 호출하는 JavaScript 클라이언트 코드를 보여 주는 메서드를 보여 주며, 그 다음에는 클라이언트 코드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-320">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="96eb3-321">**Server**</span><span class="sxs-lookup"><span data-stu-id="96eb3-321">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

<span data-ttu-id="96eb3-322">**생성된 프록시를 사용하는 자바스크립트 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="96eb3-322">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

<span data-ttu-id="96eb3-323">명시적으로 그룹을 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-323">You don't have to explicitly create groups.</span></span> <span data-ttu-id="96eb3-324">실제로 그룹은 `Groups.Add`에 대한 호출에서 이름을 처음 지정할 때 자동으로 만들어지며, 마지막 연결을 멤버 자격에서 제거하면 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-324">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="96eb3-325">그룹 구성원 목록 또는 그룹 목록을 가져오는 API가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-325">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="96eb3-326">[SignalR은 pub/sub 모델을](http://en.wikipedia.org/wiki/Publish/subscribe)기반으로 클라이언트 및 그룹에 메시지를 보내고 서버는 그룹 또는 그룹 구성원 의 목록을 유지 관리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-326">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="96eb3-327">이렇게 하면 웹 팜에 노드를 추가할 때마다 SignalR이 유지 관리하는 모든 상태를 새 노드로 전파해야 하므로 확장성을 최대화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-327">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="96eb3-328">메서드 추가 및 제거의 비동기 실행</span><span class="sxs-lookup"><span data-stu-id="96eb3-328">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="96eb3-329">및 `Groups.Add` `Groups.Remove` 메서드는 비동기적으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-329">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="96eb3-330">그룹에 클라이언트를 추가하고 그룹을 사용하여 클라이언트에 즉시 메시지를 보내려면 메서드가 `Groups.Add` 먼저 끝나는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-330">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="96eb3-331">다음 코드 예제에서는 이 작업을 수행하는 방법을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-331">The following code example shows how to do that.</span></span>

<span data-ttu-id="96eb3-332">**그룹에 클라이언트를 추가한 다음 해당 클라이언트에 메시지를 전달합니다.**</span><span class="sxs-lookup"><span data-stu-id="96eb3-332">**Adding a client to a group and then messaging that client**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="96eb3-333">그룹 구성원 유지</span><span class="sxs-lookup"><span data-stu-id="96eb3-333">Group membership persistence</span></span>

<span data-ttu-id="96eb3-334">SignalR은 사용자가 아닌 연결을 추적하므로 사용자가 연결을 설정할 때마다 사용자가 동일한 그룹에 있도록 하려면 사용자가 `Groups.Add` 새 연결을 설정할 때마다 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-334">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="96eb3-335">일시적으로 연결이 끊어진 후 SignalR이 자동으로 연결을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-335">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="96eb3-336">이 경우 SignalR은 동일한 연결을 복원하고 새 연결을 설정하지 않으므로 클라이언트의 그룹 구성원이 자동으로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-336">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="96eb3-337">이는 그룹 구성원을 포함한 각 클라이언트의 연결 상태가 클라이언트에 반올림되기 때문에 일시적인 중단이 서버 재부팅 또는 실패의 결과인 경우에도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-337">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="96eb3-338">연결이 종료되기 전에 서버가 다운되어 새 서버로 대체되면 클라이언트는 새 서버에 자동으로 다시 연결하고 구성원이 되는 그룹에 다시 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-338">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="96eb3-339">연결이 끊긴 후 연결을 자동으로 복원할 수 없거나 연결이 시간 만점이거나 클라이언트가 연결이 끊어질 때(예: 브라우저가 새 페이지로 이동하는 경우) 그룹 구성원 자격이 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-339">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="96eb3-340">다음에 사용자가 연결하면 새 연결이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-340">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="96eb3-341">동일한 사용자가 새 연결을 설정할 때 그룹 구성원 자격을 유지하려면 응용 프로그램에서 사용자와 그룹 간의 연결을 추적하고 사용자가 새 연결을 설정할 때마다 그룹 구성원 자격을 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-341">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="96eb3-342">연결 및 다시 연결에 대한 자세한 내용은 이 항목의 후반부 [Hub 클래스에서 연결 수명 이벤트를 처리하는 방법을](#connectionlifetime) 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96eb3-342">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="96eb3-343">단일 사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="96eb3-343">Single-user groups</span></span>

<span data-ttu-id="96eb3-344">SignalR을 사용하는 응용 프로그램은 일반적으로 메시지를 보낸 사용자와 메시지를 수신해야 하는 사용자를 알기 위해 사용자와 연결 간의 연결을 추적해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-344">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="96eb3-345">그룹은 이를 위해 일반적으로 사용되는 두 패턴 중 하나에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-345">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="96eb3-346">단일 사용자 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-346">Single-user groups.</span></span>

    <span data-ttu-id="96eb3-347">사용자 이름을 그룹 이름으로 지정하고 사용자가 연결하거나 다시 연결할 때마다 그룹에 현재 연결 ID를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-347">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="96eb3-348">그룹에 보내는 사용자에게 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-348">To send messages to the user you send to the group.</span></span> <span data-ttu-id="96eb3-349">이 방법의 단점은 그룹이 사용자가 온라인 또는 오프라인인지 확인할 수 있는 방법을 제공하지 않는다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-349">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="96eb3-350">사용자 이름과 연결 ID 간의 연결을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-350">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="96eb3-351">각 사용자 이름과 하나 이상의 연결 아이디 간의 연결을 사전 또는 데이터베이스에 저장하고 사용자가 연결하거나 연결을 끊을 때마다 저장된 데이터를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-351">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="96eb3-352">사용자에게 메시지를 보내려면 연결 아이디를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-352">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="96eb3-353">이 방법의 단점은 더 많은 메모리가 필요하다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-353">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="96eb3-354">Hub 클래스에서 연결 수명 이벤트를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-354">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="96eb3-355">연결 수명 이벤트를 처리하는 일반적인 이유는 사용자가 연결되어 있는지 여부를 추적하고 사용자 이름과 연결 ID 간의 연결을 추적하기 위해서입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-355">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="96eb3-356">클라이언트가 연결하거나 연결을 끊을 때 고유한 `OnConnected` `OnDisconnected`코드를 `OnReconnected` 실행하려면 다음 예제와 같이 Hub 클래스의 및 가상 메서드를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-356">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="96eb3-357">연결 됨, 연결이 끊긴 및 다시 연결해제된 경우</span><span class="sxs-lookup"><span data-stu-id="96eb3-357">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="96eb3-358">브라우저가 새 페이지로 이동할 때마다 새 연결이 설정되어야 하며, 이는 SignalR이 메서드 `OnConnected` 다음에 메서드를 `OnDisconnected` 실행한다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-358">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="96eb3-359">SignalR은 새 연결이 설정되면 항상 새 연결 ID를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-359">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="96eb3-360">이 `OnReconnected` 메서드는 케이블이 일시적으로 연결이 끊어지고 연결이 중단되기 전에 다시 연결되는 경우와 같이 SignalR에서 자동으로 복구할 수 있는 연결 끊김이 있는 경우 호출됩니다. 이 `OnDisconnected` 메서드는 클라이언트연결이 끊어졌을 때 호출되며 브라우저가 새 페이지로 이동하는 경우와 같이 SignalR가 자동으로 다시 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-360">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="96eb3-361">따라서 지정된 클라이언트에 대한 가능한 이벤트 `OnConnected` `OnReconnected`시퀀스는 은 `OnDisconnected`. 또는 `OnConnected` `OnDisconnected`.</span><span class="sxs-lookup"><span data-stu-id="96eb3-361">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="96eb3-362">지정된 연결에 `OnConnected` `OnDisconnected` `OnReconnected` 대한 시퀀스가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-362">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="96eb3-363">서버가 `OnDisconnected` 다운되거나 앱 도메인이 재활용되는 경우와 같은 일부 시나리오에서는 메서드가 호출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-363">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="96eb3-364">다른 서버가 온라인상태이거나 App Domain이 재활용을 완료하면 일부 클라이언트가 다시 `OnReconnected` 연결하여 이벤트를 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-364">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="96eb3-365">자세한 내용은 [SignalR의 연결 수명 이벤트 이해 및 처리를](handling-connection-lifetime-events.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="96eb3-365">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="96eb3-366">호출자 상태가 채워지지 않음</span><span class="sxs-lookup"><span data-stu-id="96eb3-366">Caller state not populated</span></span>

<span data-ttu-id="96eb3-367">연결 수명 이벤트 처리기 메서드는 서버에서 호출되므로 클라이언트에 `state` 개체에 넣은 상태는 서버의 `Caller` 속성에 채워지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-367">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="96eb3-368">개체 및 `Caller` 속성에 대한 자세한 내용은 이 항목의 후반부에서 [클라이언트와 Hub 클래스 간에 상태를 전달하는 방법을](#passstate) 참조하세요. `state`</span><span class="sxs-lookup"><span data-stu-id="96eb3-368">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="96eb3-369">Context 속성에서 클라이언트에 대 한 정보를 얻는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-369">How to get information about the client from the Context property</span></span>

<span data-ttu-id="96eb3-370">클라이언트에 대한 정보를 얻으려면 `Context` Hub 클래스의 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-370">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="96eb3-371">속성은 `Context` 다음 정보에 대한 액세스를 제공하는 [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-371">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="96eb3-372">호출 클라이언트의 연결 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-372">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    <span data-ttu-id="96eb3-373">연결 ID는 SignalR에서 할당하는 GUID입니다(사용자 고유의 코드에서 값을 지정할 수 없습니다).</span><span class="sxs-lookup"><span data-stu-id="96eb3-373">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="96eb3-374">각 연결에 대해 하나의 연결 ID가 있으며 응용 프로그램에 여러 Hub가 있는 경우 모든 Hubs에서 동일한 연결 ID가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-374">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="96eb3-375">HTTP 헤더 데이터.</span><span class="sxs-lookup"><span data-stu-id="96eb3-375">HTTP header data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="96eb3-376">에서 HTTP 헤더를 얻을 `Context.Headers`수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-376">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="96eb3-377">동일한 것에 대한 여러 참조의 `Context.Headers` 이유는 먼저 만들어졌고 나중에 속성이 `Context.Headers` `Context.Request` 추가되었으며 이전 버전과의 호환성을 위해 유지되었기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-377">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="96eb3-378">문자열 데이터를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-378">Query string data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    <span data-ttu-id="96eb3-379">`Context.QueryString`에서 쿼리 문자열 데이터를 얻을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-379">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="96eb3-380">이 속성에서 얻는 쿼리 문자열은 SignalR 연결을 설정한 HTTP 요청과 함께 사용된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-380">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="96eb3-381">클라이언트에서 서버로 클라이언트에 대한 데이터를 전달하는 편리한 방법입니다 연결을 구성하여 클라이언트에 쿼리 문자열 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-381">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="96eb3-382">다음 예제에서는 생성된 프록시를 사용할 때 JavaScript 클라이언트에 쿼리 문자열을 추가하는 한 가지 방법을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-382">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    <span data-ttu-id="96eb3-383">쿼리 문자열 매개 변수 설정에 대한 자세한 내용은 [JavaScript](hubs-api-guide-javascript-client.md) 및 [.NET](hubs-api-guide-net-client.md) 클라이언트에 대한 API 가이드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96eb3-383">For more information about setting query string parameters, see the API guides for the [JavaScript](hubs-api-guide-javascript-client.md) and [.NET](hubs-api-guide-net-client.md) clients.</span></span>

    <span data-ttu-id="96eb3-384">SignalR에서 내부적으로 사용되는 다른 값과 함께 쿼리 문자열 데이터에서 연결에 사용되는 전송 방법을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-384">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    <span data-ttu-id="96eb3-385">값은 `transportMethod` "웹 소켓", "서버SentEvents", "영원히프레임" 또는 "longPolling"입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-385">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="96eb3-386">`OnConnected` 이벤트 처리기 메서드에서 이 값을 확인 하면 일부 시나리오에서 처음에 연결에 대 한 최종 협상 된 전송 메서드가 아닌 전송 값을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-386">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="96eb3-387">이 경우 메서드는 예외를 throw 하 고 최종 전송 메서드가 설정 될 때 나중에 다시 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-387">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="96eb3-388">쿠키.</span><span class="sxs-lookup"><span data-stu-id="96eb3-388">Cookies.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    <span data-ttu-id="96eb3-389">에서 `Context.RequestCookies`쿠키를 얻을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-389">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="96eb3-390">사용자 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-390">User information.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- <span data-ttu-id="96eb3-391">요청에 대한 HttpContext 개체 :</span><span class="sxs-lookup"><span data-stu-id="96eb3-391">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    <span data-ttu-id="96eb3-392">SignalR `HttpContext.Current` 연결에 대한 `HttpContext` 개체를 가져오는 대신 이 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-392">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="96eb3-393">클라이언트와 Hub 클래스 간에 상태를 전달하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-393">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="96eb3-394">클라이언트 프록시는 `state` 각 메서드 호출을 사용하여 서버에 전송할 데이터를 저장할 수 있는 개체를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-394">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="96eb3-395">서버에서 클라이언트에서 호출되는 Hub `Clients.Caller` 메서드의 속성에서 이 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-395">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="96eb3-396">속성은 `Clients.Caller` 연결 수명 이벤트 처리기 `OnConnected`메서드 `OnDisconnected`및 `OnReconnected`에 대해 채워지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-396">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="96eb3-397">개체및속성에서 `state` 데이터를 만들거나 `Clients.Caller` 업데이트하는 것은 양방향으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-397">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="96eb3-398">서버에서 값을 업데이트할 수 있으며 클라이언트에 다시 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-398">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="96eb3-399">다음 예제에서는 모든 메서드 호출을 사용 하 고 서버에 전송하기 위한 상태를 저장하는 JavaScript 클라이언트 코드를 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-399">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

<span data-ttu-id="96eb3-400">다음 예제에서는 .NET 클라이언트에서 해당 코드를 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-400">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

<span data-ttu-id="96eb3-401">Hub 클래스에서 `Clients.Caller` 속성에서 이 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-401">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="96eb3-402">다음 예제에서는 이전 예제에서 참조한 상태를 검색하는 코드를 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-402">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="96eb3-403">`state` 상태를 유지하기 위한 이 메커니즘은 또는 `Clients.Caller` 속성에 넣는 모든 것이 모든 메서드 호출과 함께 반올림되므로 많은 양의 데이터를 위한 것이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-403">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="96eb3-404">사용자 이름이나 카운터와 같은 작은 항목에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-404">It's useful for smaller items such as user names or counters.</span></span>

<span data-ttu-id="96eb3-405">VB.NET 또는 강력한 형식의 허브에서는 호출자 상태 개체를 통해 `Clients.Caller`액세스할 수 없습니다. 대신, `Clients.CallerState` 사용 (SignalR 2.1에 도입):</span><span class="sxs-lookup"><span data-stu-id="96eb3-405">In VB.NET or in a strongly-typed hub, the caller state object can't be accessed through `Clients.Caller`; instead, use `Clients.CallerState` (introduced in SignalR 2.1):</span></span>

<span data-ttu-id="96eb3-406">**C에서 CallerState 사용 #**</span><span class="sxs-lookup"><span data-stu-id="96eb3-406">**Using CallerState in C#**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

<span data-ttu-id="96eb3-407">**시각적 기본에서 CallerState 사용**</span><span class="sxs-lookup"><span data-stu-id="96eb3-407">**Using CallerState in Visual Basic**</span></span>

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="96eb3-408">Hub 클래스에서 오류를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-408">How to handle errors in the Hub class</span></span>

<span data-ttu-id="96eb3-409">Hub 클래스 메서드에서 발생하는 오류를 처리하려면 먼저 을 사용하여 `await`비동기 작업(예: 클라이언트 메서드 호출)의 예외를 "관찰"해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-409">To handle errors that occur in your Hub class methods, first ensure you "observe" any exceptions from async operations (such as invoking client methods) by using `await`.</span></span> <span data-ttu-id="96eb3-410">그런 다음 다음 방법 중 하나 이상을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-410">Then use one or more of the following methods:</span></span>

- <span data-ttu-id="96eb3-411">try-catch 블록에서 메서드 코드를 래핑하고 예외 개체를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-411">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="96eb3-412">디버깅을 위해 클라이언트에 예외를 보낼 수 있지만 보안상의 이유로 프로덕션 환경에서 클라이언트에 자세한 정보를 보내는 것은 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-412">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="96eb3-413">[OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) 메서드를 처리하는 허브 파이프라인 모듈을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-413">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="96eb3-414">다음 예제에서는 오류를 기록하는 파이프라인 모듈과 허브 파이프라인에 모듈을 삽입하는 Startup.cs 코드를 보여 주십니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-414">The following example shows a pipeline module that logs errors, followed by code in Startup.cs that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- <span data-ttu-id="96eb3-415">클래스를 `HubException` 사용합니다(SignalR 2에 도입).</span><span class="sxs-lookup"><span data-stu-id="96eb3-415">Use the `HubException` class (introduced in SignalR 2).</span></span> <span data-ttu-id="96eb3-416">이 오류는 모든 허브 호출에서 throw될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-416">This error can be thrown from any hub invocation.</span></span> <span data-ttu-id="96eb3-417">`HubError` 생성자는 문자열 메시지와 추가 오류 데이터를 저장하기 위한 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-417">The `HubError` constructor takes a string message, and an object for storing extra error data.</span></span> <span data-ttu-id="96eb3-418">SignalR은 예외를 자동으로 직렬화하고 클라이언트로 보내며 허브 메서드 호출을 거부하거나 실패하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-418">SignalR will auto-serialize the exception and send it to the client, where it will be used to reject or fail the hub method invocation.</span></span>

    <span data-ttu-id="96eb3-419">다음 코드 샘플에서는 허브 호출 `HubException` 중에 를 throw하는 방법과 JavaScript 및 .NET 클라이언트에서 예외를 처리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-419">The following code samples demonstrate how to throw a `HubException` during a Hub invocation, and how to handle the exception on JavaScript and .NET clients.</span></span>

    <span data-ttu-id="96eb3-420">**HubException 클래스를 보여 주는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="96eb3-420">**Server code demonstrating the HubException class**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    <span data-ttu-id="96eb3-421">**허브에 HubException을 throw에 대한 응답을 보여주는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="96eb3-421">**JavaScript client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    <span data-ttu-id="96eb3-422">**허브에서 HubException을 throw에 대한 응답을 보여 주는 .NET 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="96eb3-422">**.NET client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

<span data-ttu-id="96eb3-423">허브 파이프라인 모듈에 대한 자세한 내용은 이 항목의 후반부에서 [허브 파이프라인을 사용자 지정하는 방법을](#hubpipeline) 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96eb3-423">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="96eb3-424">추적을 활성화하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-424">How to enable tracing</span></span>

<span data-ttu-id="96eb3-425">서버 측 추적을 사용하려면 이 예제와 같이 Web.config 파일에 system.diagnostics 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-425">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

<span data-ttu-id="96eb3-426">Visual Studio에서 응용 프로그램을 실행하면 **출력** 창에서 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-426">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="96eb3-427">클라이언트 메서드를 호출하고 Hub 클래스 외부에서 그룹을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-427">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="96eb3-428">Hub 클래스가 아닌 다른 클래스에서 클라이언트 메서드를 호출하려면 Hub에 대한 SignalR 컨텍스트 개체에 대한 참조를 얻고 클라이언트에서 메서드를 호출하거나 그룹을 관리하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-428">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="96eb3-429">다음 샘플 `StockTicker` 클래스는 컨텍스트 개체를 가져옵니다. `updateStockPrice` `StockTickerHub`</span><span class="sxs-lookup"><span data-stu-id="96eb3-429">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

<span data-ttu-id="96eb3-430">수명이 긴 개체에서 컨텍스트를 여러 번 사용해야 하는 경우 매번 다시 가져오는 대신 참조를 한 번 받고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-430">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="96eb3-431">컨텍스트를 한 번 받으면 SignalR이 Hub 메서드가 클라이언트 메서드를 호출하는 순서와 동일한 순서로 클라이언트에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-431">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="96eb3-432">허브에 대한 SignalR 컨텍스트를 사용하는 방법을 보여 주는 자습서의 경우 [ASP.NET SignalR을 사용하여 서버 브로드캐스트를](../getting-started/tutorial-server-broadcast-with-signalr.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="96eb3-432">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="96eb3-433">클라이언트 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="96eb3-433">Calling client methods</span></span>

<span data-ttu-id="96eb3-434">RPC를 받을 클라이언트를 지정할 수 있지만 Hub 클래스에서 호출할 때보다 옵션이 적습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-434">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="96eb3-435">그 이유는 컨텍스트가 클라이언트의 특정 호출과 연결되지 않으므로 현재 연결 ID(예: `Clients.Others`또는 `Clients.Caller` `Clients.OthersInGroup`및)에 대한 지식이 필요한 메서드는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-435">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="96eb3-436">다음 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-436">The following options are available:</span></span>

- <span data-ttu-id="96eb3-437">연결된 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-437">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- <span data-ttu-id="96eb3-438">연결 ID로 식별된 특정 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-438">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- <span data-ttu-id="96eb3-439">연결 ID로 식별된 지정된 클라이언트를 제외한 연결된 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-439">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- <span data-ttu-id="96eb3-440">지정된 그룹의 연결된 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-440">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- <span data-ttu-id="96eb3-441">연결 ID로 식별된 지정된 클라이언트를 제외한 지정된 그룹의 모든 연결된 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-441">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

<span data-ttu-id="96eb3-442">Hub 클래스의 메서드에서 비 Hub 클래스로 호출하는 경우 현재 연결 ID를 전달하고 `Clients.Client`에서 `Clients.AllExcept`를 `Clients.Group` 사용하거나 `Clients.Others`을 `Clients.OthersInGroup`시뮬레이션할 `Clients.Caller`수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-442">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="96eb3-443">다음 예제에서 `MoveShapeHub` 클래스는 클래스를 시뮬레이션할 `Broadcaster` `Broadcaster` `Clients.Others`수 있도록 연결 ID를 클래스에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-443">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="96eb3-444">그룹 구성원 관리</span><span class="sxs-lookup"><span data-stu-id="96eb3-444">Managing group membership</span></span>

<span data-ttu-id="96eb3-445">그룹 관리의 경우 Hub 클래스와 동일한 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-445">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="96eb3-446">그룹에 클라이언트 추가</span><span class="sxs-lookup"><span data-stu-id="96eb3-446">Add a client to a group</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- <span data-ttu-id="96eb3-447">그룹에서 클라이언트 제거</span><span class="sxs-lookup"><span data-stu-id="96eb3-447">Remove a client from a group</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="96eb3-448">허브 파이프라인을 사용자 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="96eb3-448">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="96eb3-449">SignalR을 사용하면 허브 파이프라인에 사용자 고유의 코드를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-449">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="96eb3-450">다음 예제에서는 클라이언트에서 수신된 각 들어오는 메서드 호출및 클라이언트에서 호출된 발신 메서드 호출을 기록하는 사용자 지정 Hub 파이프라인 모듈을 보여 주며, 이 모듈은 다음과 같은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-450">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

<span data-ttu-id="96eb3-451">*Startup.cs* 파일의 다음 코드는 Hub 파이프라인에서 실행할 모듈을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-451">The following code in the *Startup.cs* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

<span data-ttu-id="96eb3-452">재정의할 수 있는 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96eb3-452">There are many different methods that you can override.</span></span> <span data-ttu-id="96eb3-453">전체 목록은 [Hub파이프라인모듈 메서드](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="96eb3-453">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
