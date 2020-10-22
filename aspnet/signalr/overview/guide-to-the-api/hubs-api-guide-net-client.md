---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: 'ASP.NET SignalR Hubs API 가이드-.NET 클라이언트 (c #) | Microsoft Docs'
author: bradygaster
description: 이 문서에서는 Windows 스토어 (WinRT), WPF, Silverlight, 단점 등 .NET 클라이언트에서 SignalR 버전 2 용 허브 API를 사용 하는 방법을 소개 합니다.
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345552"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="ac25c-103">ASP.NET SignalR Hubs API 가이드-.NET 클라이언트 (c #)</span><span class="sxs-lookup"><span data-stu-id="ac25c-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="ac25c-104">이 문서에서는 Windows 스토어 (WinRT), WPF, Silverlight, 콘솔 응용 프로그램 등의 .NET 클라이언트에서 SignalR 버전 2 용 허브 API를 사용 하는 방법을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-104">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
>
> <span data-ttu-id="ac25c-105">SignalR Hubs API를 사용 하면 서버에서 연결 된 클라이언트로 또는 클라이언트에서 서버로 Rpc (원격 프로시저 호출)를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="ac25c-106">서버 코드에서는 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="ac25c-107">클라이언트 코드에서는 서버에서 호출할 수 있는 메서드를 정의 하 고 서버에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="ac25c-108">SignalR는 모든 클라이언트에서 서버로의 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="ac25c-109">또한 SignalR는 영구 연결 이라고 하는 하위 수준 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="ac25c-110">SignalR, 허브 및 영구 연결에 대 한 소개 나 전체 SignalR 응용 프로그램을 빌드하는 방법을 보여 주는 자습서는 [SignalR-시작](../getting-started/index.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ac25c-110">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="ac25c-111">이 항목에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="ac25c-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="ac25c-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ac25c-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="ac25c-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="ac25c-113">.NET 4.5</span></span>
> - <span data-ttu-id="ac25c-114">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="ac25c-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="ac25c-115">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="ac25c-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="ac25c-116">이전 버전의 SignalR에 대 한 자세한 내용은 [SignalR 이전 버전](../older-versions/index.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ac25c-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="ac25c-117">질문 및 설명</span><span class="sxs-lookup"><span data-stu-id="ac25c-117">Questions and comments</span></span>
>
> <span data-ttu-id="ac25c-118">이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="ac25c-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="ac25c-119">자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="ac25c-120">개요</span><span class="sxs-lookup"><span data-stu-id="ac25c-120">Overview</span></span>

<span data-ttu-id="ac25c-121">이 문서는 다음 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="ac25c-122">클라이언트 설정</span><span class="sxs-lookup"><span data-stu-id="ac25c-122">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="ac25c-123">연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-123">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="ac25c-124">Silverlight 클라이언트에서 도메인 간 연결</span><span class="sxs-lookup"><span data-stu-id="ac25c-124">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="ac25c-125">연결을 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-125">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="ac25c-126">WPF 클라이언트에서 동시 연결의 최대 수를 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-126">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="ac25c-127">쿼리 문자열 매개 변수를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-127">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="ac25c-128">전송 방법을 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-128">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="ac25c-129">HTTP 헤더를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-129">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="ac25c-130">클라이언트 인증서를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-130">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="ac25c-131">허브 프록시를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-131">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="ac25c-132">서버에서 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-132">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="ac25c-133">매개 변수가 없는 메서드</span><span class="sxs-lookup"><span data-stu-id="ac25c-133">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="ac25c-134">매개 변수가 있는 메서드, 매개 변수 형식 지정</span><span class="sxs-lookup"><span data-stu-id="ac25c-134">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="ac25c-135">매개 변수가 있는 메서드, 매개 변수에 대 한 동적 개체 지정</span><span class="sxs-lookup"><span data-stu-id="ac25c-135">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="ac25c-136">처리기를 제거 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-136">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="ac25c-137">클라이언트에서 서버 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-137">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="ac25c-138">연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-138">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="ac25c-139">오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-139">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="ac25c-140">클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-140">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="ac25c-141">서버에서 호출할 수 있는 클라이언트 메서드에 대 한 WPF, Silverlight 및 콘솔 응용 프로그램 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="ac25c-141">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="ac25c-142">샘플 .NET 클라이언트 프로젝트는 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ac25c-142">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="ac25c-143">[gustavo-armenta/SignalR-](https://github.com/gustavo-armenta/SignalR-Samples) GitHub.com의 샘플 (WinRT, Silverlight, 콘솔 앱 예제).</span><span class="sxs-lookup"><span data-stu-id="ac25c-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="ac25c-144">GitHub.com의 [DamianEdwards/SignalR-MoveShapeDemo/MoveShape](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) (WPF 예제).</span><span class="sxs-lookup"><span data-stu-id="ac25c-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="ac25c-145">[SignalR/SignalR](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) 의 GitHub.com (콘솔 앱 예제).</span><span class="sxs-lookup"><span data-stu-id="ac25c-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="ac25c-146">서버 또는 JavaScript 클라이언트를 프로그래밍 하는 방법에 대 한 설명서는 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ac25c-146">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="ac25c-147">SignalR Hubs API 가이드-서버</span><span class="sxs-lookup"><span data-stu-id="ac25c-147">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="ac25c-148">SignalR Hubs API 가이드-JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ac25c-148">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="ac25c-149">API 참조 항목에 대 한 링크는 .NET 4.5 버전의 API에 대 한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-149">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="ac25c-150">.NET 4를 사용 하 [는 경우 .net 4 버전의 API 항목](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ac25c-150">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="ac25c-151">클라이언트 설치</span><span class="sxs-lookup"><span data-stu-id="ac25c-151">Client setup</span></span>

<span data-ttu-id="ac25c-152">[SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet 패키지를 설치 합니다 ( [SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) 패키지는 아님).</span><span class="sxs-lookup"><span data-stu-id="ac25c-152">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="ac25c-153">이 패키지는 .NET 4와 .NET 4.5 모두에 대해 WinRT, Silverlight, WPF, 콘솔 응용 프로그램 및 Windows Phone 클라이언트를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-153">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="ac25c-154">클라이언트에 있는 SignalR 버전이 서버에 있는 버전과 다른 경우 SignalR는 종종 차이점에 맞게 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-154">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="ac25c-155">예를 들어 SignalR 버전 2를 실행 하는 서버는 1.1. x가 설치 된 클라이언트 및 버전 2가 설치 된 클라이언트를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-155">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="ac25c-156">서버 버전과 클라이언트 버전의 차이가 너무 SignalR 클라이언트의 서버가 서버 보다 최신인 경우 `InvalidOperationException` 클라이언트는 연결을 설정 하려고 할 때 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-156">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="ac25c-157">오류 메시지는 " `You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X` "입니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-157">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="ac25c-158">연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-158">How to establish a connection</span></span>

<span data-ttu-id="ac25c-159">연결을 설정 하려면 먼저 개체를 만들고 `HubConnection` 프록시를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-159">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="ac25c-160">연결을 설정 하려면 `Start` 개체에서 메서드를 호출 합니다 `HubConnection` .</span><span class="sxs-lookup"><span data-stu-id="ac25c-160">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> <span data-ttu-id="ac25c-161">JavaScript 클라이언트의 경우에는 메서드를 호출 하 여 연결을 설정 하기 전에 이벤트 처리기를 하나 이상 등록 해야 `Start` 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-161">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="ac25c-162">.NET 클라이언트에는이 작업이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-162">This is not necessary for .NET clients.</span></span> <span data-ttu-id="ac25c-163">JavaScript 클라이언트의 경우 생성 된 프록시 코드는 서버에 있는 모든 허브에 대 한 프록시를 자동으로 만들고, 처리기를 등록 하면 클라이언트가 사용할 허브를 표시 하는 방법이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-163">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="ac25c-164">그러나 .NET 클라이언트의 경우에는 허브 프록시를 수동으로 만들 수 있으므로 SignalR은 사용자가 프록시를 만드는 허브를 사용 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-164">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>

<span data-ttu-id="ac25c-165">샘플 코드는 기본 "/signalr" URL을 사용 하 여 SignalR 서비스에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-165">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="ac25c-166">다른 기준 URL을 지정 하는 방법에 대 한 자세한 내용은 [ASP.NET SignalR HUBS API Guide-Server-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ac25c-166">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="ac25c-167">`Start`메서드는 비동기적으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-167">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="ac25c-168">연결이 설정 될 때까지 후속 코드 줄이 실행 되지 않도록 하려면 `await` ASP.NET 4.5 비동기 메서드 또는 `.Wait()` 동기 메서드에서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-168">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="ac25c-169">`.Wait()`WinRT 클라이언트에서를 사용 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ac25c-169">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="ac25c-170">Silverlight 클라이언트에서 도메인 간 연결</span><span class="sxs-lookup"><span data-stu-id="ac25c-170">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="ac25c-171">Silverlight 클라이언트에서 도메인 간 연결을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [도메인 경계에서 서비스를 사용할 수 있도록](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)설정을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ac25c-171">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="ac25c-172">연결을 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-172">How to configure the connection</span></span>

<span data-ttu-id="ac25c-173">연결을 설정 하기 전에 다음 옵션 중 하나를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-173">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="ac25c-174">동시 연결 제한.</span><span class="sxs-lookup"><span data-stu-id="ac25c-174">Concurrent connections limit.</span></span>
- <span data-ttu-id="ac25c-175">쿼리 문자열 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-175">Query string parameters.</span></span>
- <span data-ttu-id="ac25c-176">전송 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-176">The transport method.</span></span>
- <span data-ttu-id="ac25c-177">HTTP 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-177">HTTP headers.</span></span>
- <span data-ttu-id="ac25c-178">클라이언트 인증서.</span><span class="sxs-lookup"><span data-stu-id="ac25c-178">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="ac25c-179">WPF 클라이언트에서 동시 연결의 최대 수를 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-179">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="ac25c-180">WPF 클라이언트에서는 기본값 2에서 동시 연결의 최대 수를 늘려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-180">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="ac25c-181">권장 값은 10입니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-181">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

<span data-ttu-id="ac25c-182">자세한 내용은 [Servicepointmanager. DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ac25c-182">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="ac25c-183">쿼리 문자열 매개 변수를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-183">How to specify query string parameters</span></span>

<span data-ttu-id="ac25c-184">클라이언트에서 연결할 때 서버에 데이터를 전송 하려는 경우 연결 개체에 쿼리 문자열 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-184">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="ac25c-185">다음 예제에서는 클라이언트 코드에서 쿼리 문자열 매개 변수를 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-185">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="ac25c-186">다음 예에서는 서버 코드에서 쿼리 문자열 매개 변수를 읽는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-186">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="ac25c-187">전송 방법을 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-187">How to specify the transport method</span></span>

<span data-ttu-id="ac25c-188">연결 프로세스의 일부로 SignalR 클라이언트는 서버와 클라이언트 모두에서 지원 되는 최상의 전송을 결정 하기 위해 일반적으로 서버와 협상 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-188">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="ac25c-189">사용 하려는 전송을 이미 알고 있는 경우이 협상 프로세스를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-189">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="ac25c-190">전송 방법을 지정 하려면 전송 개체를 Start 메서드로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-190">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="ac25c-191">다음 예제에서는 클라이언트 코드에서 전송 메서드를 지정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-191">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

<span data-ttu-id="ac25c-192">[SignalR](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) 네임 스페이스에는 전송을 지정 하는 데 사용할 수 있는 다음과 같은 클래스가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-192">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="ac25c-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="ac25c-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="ac25c-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="ac25c-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="ac25c-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (서버와 클라이언트가 모두 .net 4.5을 사용 하는 경우에만 사용 가능)</span><span class="sxs-lookup"><span data-stu-id="ac25c-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="ac25c-196">[Autotransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (클라이언트와 서버 모두에서 지원 되는 최상의 전송을 자동으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="ac25c-197">이는 기본 전송입니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-197">This is the default transport.</span></span> <span data-ttu-id="ac25c-198">이를 메서드에 전달 하는 `Start` 것과 동일한 효과가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-198">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="ac25c-199">ForeverFrame 전송은 브라우저 에서만 사용 되므로이 목록에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-199">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="ac25c-200">서버 코드에서 전송 방법을 확인 하는 방법에 대 한 자세한 내용은 [ASP.NET SignalR HUBS API 가이드-서버-컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법](hubs-api-guide-server.md#contextproperty)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ac25c-200">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="ac25c-201">전송 및 대체에 대 한 자세한 내용은 [SignalR에 대 한 소개-전송 및 대체](../getting-started/introduction-to-signalr.md#transports)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ac25c-201">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="ac25c-202">HTTP 헤더를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-202">How to specify HTTP headers</span></span>

<span data-ttu-id="ac25c-203">HTTP 헤더를 설정 하려면 `Headers` 연결 개체의 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-203">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="ac25c-204">다음 예제에서는 HTTP 헤더를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-204">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="ac25c-205">클라이언트 인증서를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-205">How to specify client certificates</span></span>

<span data-ttu-id="ac25c-206">클라이언트 인증서를 추가 하려면 `AddClientCertificate` 연결 개체에서 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-206">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="ac25c-207">허브 프록시를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-207">How to create the Hub proxy</span></span>

<span data-ttu-id="ac25c-208">클라이언트에서 허브가 서버에서 호출할 수 있는 메서드를 정의 하 고 서버의 허브에서 메서드를 호출 하려면 연결 개체에 대해를 호출 하 여 허브에 대 한 프록시를 만듭니다 `CreateHubProxy` .</span><span class="sxs-lookup"><span data-stu-id="ac25c-208">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="ac25c-209">에 전달 하는 문자열 `CreateHubProxy` 은 허브 클래스의 이름 이거나, `HubName` 서버에서 사용 되는 경우 특성으로 지정 된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-209">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="ac25c-210">이름 일치 시 대/소문자는 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-210">Name matching is case-insensitive.</span></span>

<span data-ttu-id="ac25c-211">**서버의 허브 클래스**</span><span class="sxs-lookup"><span data-stu-id="ac25c-211">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="ac25c-212">**허브 클래스에 대 한 클라이언트 프록시 만들기**</span><span class="sxs-lookup"><span data-stu-id="ac25c-212">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

<span data-ttu-id="ac25c-213">허브 클래스를 특성으로 데코레이팅하는 경우 `HubName` 해당 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-213">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="ac25c-214">**서버의 허브 클래스**</span><span class="sxs-lookup"><span data-stu-id="ac25c-214">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="ac25c-215">**허브 클래스에 대 한 클라이언트 프록시 만들기**</span><span class="sxs-lookup"><span data-stu-id="ac25c-215">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

<span data-ttu-id="ac25c-216">`HubConnection.CreateHubProxy`동일한를 사용 하 여를 여러 번 호출 하는 경우 `hubName` 동일한 캐시 된 개체를 가져옵니다 `IHubProxy` .</span><span class="sxs-lookup"><span data-stu-id="ac25c-216">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="ac25c-217">서버에서 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-217">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="ac25c-218">서버에서 호출할 수 있는 메서드를 정의 하려면 프록시의 메서드를 사용 하 여 `On` 이벤트 처리기를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-218">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="ac25c-219">메서드 이름 일치는 대/소문자를 구분 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-219">Method name matching is case-insensitive.</span></span> <span data-ttu-id="ac25c-220">예를 들어 서버에 있는는 `Clients.All.UpdateStockPrice` `updateStockPrice` 클라이언트에서, 또는를 실행 합니다 `updatestockprice` `UpdateStockPrice` .</span><span class="sxs-lookup"><span data-stu-id="ac25c-220">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="ac25c-221">클라이언트 플랫폼 마다 UI를 업데이트 하는 메서드 코드를 작성 하는 방법에 대 한 요구 사항이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-221">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="ac25c-222">표시 된 예제는 WinRT (Windows 스토어 .NET) 클라이언트를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-222">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="ac25c-223">WPF, Silverlight 및 콘솔 응용 프로그램 예제는 [이 항목의 뒷부분](#wpfsl)에 나오는 별도의 섹션에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-223">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="ac25c-224">매개 변수가 없는 메서드</span><span class="sxs-lookup"><span data-stu-id="ac25c-224">Methods without parameters</span></span>

<span data-ttu-id="ac25c-225">처리 중인 메서드에 매개 변수가 없는 경우 메서드의 제네릭이 아닌 오버 로드를 사용 합니다 `On` .</span><span class="sxs-lookup"><span data-stu-id="ac25c-225">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="ac25c-226">**매개 변수 없이 클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="ac25c-226">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="ac25c-227">**매개 변수 없이 서버에서 호출 되는 메서드에 대 한 WinRT 클라이언트 코드 ([이 항목의 뒷부분에 나오는 WPF 및 Silverlight 예제 참조](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="ac25c-227">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="ac25c-228">매개 변수가 있는 메서드, 매개 변수 형식 지정</span><span class="sxs-lookup"><span data-stu-id="ac25c-228">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="ac25c-229">처리 중인 메서드에 매개 변수가 있는 경우 매개 변수의 형식을 메서드의 제네릭 형식으로 지정 합니다 `On` .</span><span class="sxs-lookup"><span data-stu-id="ac25c-229">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="ac25c-230">`On`최대 8 개의 매개 변수를 지정할 수 있도록 하는 메서드의 제네릭 오버 로드가 있습니다 (Windows Phone 7에서 4).</span><span class="sxs-lookup"><span data-stu-id="ac25c-230">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="ac25c-231">다음 예제에서는 하나의 매개 변수가 메서드로 전송 됩니다 `UpdateStockPrice` .</span><span class="sxs-lookup"><span data-stu-id="ac25c-231">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="ac25c-232">**매개 변수를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="ac25c-232">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="ac25c-233">**매개 변수에 사용 되는 스톡 클래스입니다.**</span><span class="sxs-lookup"><span data-stu-id="ac25c-233">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="ac25c-234">**매개 변수를 사용 하 여 서버에서 호출 된 메서드에 대 한 WinRT 클라이언트 코드 ([이 항목의 뒷부분에 나오는 WPF 및 Silverlight 예제 참조](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="ac25c-234">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="ac25c-235">매개 변수가 있는 메서드, 매개 변수에 대 한 동적 개체 지정</span><span class="sxs-lookup"><span data-stu-id="ac25c-235">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="ac25c-236">매개 변수를 메서드의 제네릭 형식으로 지정 하는 대신 `On` 매개 변수를 동적 개체로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-236">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="ac25c-237">**매개 변수를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="ac25c-237">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="ac25c-238">**매개 변수에 사용 되는 스톡 클래스입니다.**</span><span class="sxs-lookup"><span data-stu-id="ac25c-238">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="ac25c-239">**매개 변수에 대 한 동적 개체를 사용 하 여 매개 변수를 사용 하 여 서버에서 호출 된 메서드에 대 한 WinRT 클라이언트 코드 ([이 항목의 뒷부분에 나오는 WPF 및 Silverlight 예제 참조](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="ac25c-239">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="ac25c-240">처리기를 제거 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-240">How to remove a handler</span></span>

<span data-ttu-id="ac25c-241">처리기를 제거 하려면 해당 메서드를 호출 `Dispose` 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-241">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="ac25c-242">**서버에서 호출 된 메서드에 대 한 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="ac25c-242">**Client code for a method called from server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="ac25c-243">**처리기를 제거 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="ac25c-243">**Client code to remove the handler**</span></span>

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="ac25c-244">클라이언트에서 서버 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-244">How to call server methods from the client</span></span>

<span data-ttu-id="ac25c-245">서버에서 메서드를 호출 하려면 `Invoke` 허브 프록시에서 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-245">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="ac25c-246">서버 메서드에 반환 값이 없는 경우 메서드의 제네릭이 아닌 오버 로드를 사용 `Invoke` 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-246">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="ac25c-247">**반환 값이 없는 메서드에 대 한 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="ac25c-247">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="ac25c-248">**반환 값이 없는 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="ac25c-248">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="ac25c-249">서버 메서드에 반환 값이 있는 경우 반환 형식을 메서드의 제네릭 형식으로 지정 합니다 `Invoke` .</span><span class="sxs-lookup"><span data-stu-id="ac25c-249">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="ac25c-250">**반환 값을 가지 며 복합 형식 매개 변수를 사용 하는 메서드의 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="ac25c-250">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="ac25c-251">**매개 변수 및 반환 값에 사용 되는 스톡 클래스입니다.**</span><span class="sxs-lookup"><span data-stu-id="ac25c-251">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="ac25c-252">**ASP.NET 4.5 async 메서드에서 반환 값을 가지 며 복합 형식 매개 변수를 사용 하는 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="ac25c-252">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="ac25c-253">**동기 메서드에서 반환 값을 포함 하 고 복합 형식 매개 변수를 사용 하는 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="ac25c-253">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="ac25c-254">`Invoke`메서드는 비동기적으로 실행 되 고 개체를 반환 `Task` 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-254">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="ac25c-255">또는를 지정 하지 `await` 않으면 `.Wait()` 호출 하는 메서드의 실행이 완료 되기 전에 다음 코드 줄이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-255">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="ac25c-256">연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-256">How to handle connection lifetime events</span></span>

<span data-ttu-id="ac25c-257">SignalR는 처리할 수 있는 다음 연결 수명 이벤트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-257">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="ac25c-258">`Received`: 연결에서 데이터를 받을 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-258">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="ac25c-259">받은 데이터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-259">Provides the received data.</span></span>
- <span data-ttu-id="ac25c-260">`ConnectionSlow`: 클라이언트에서 느리거나 자주 삭제 되는 연결을 검색 하는 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-260">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="ac25c-261">`Reconnecting`: 기본 전송에서 다시 연결을 시작할 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-261">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="ac25c-262">`Reconnected`: 기본 전송이 다시 연결 되었을 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-262">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="ac25c-263">`StateChanged`: 연결 상태가 변경 될 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-263">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="ac25c-264">이전 상태와 새 상태를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-264">Provides the old state and the new state.</span></span> <span data-ttu-id="ac25c-265">연결 상태 값에 대 한 자세한 내용은 [Connectionstate 열거](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ac25c-265">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="ac25c-266">`Closed`: 연결을 끊을 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-266">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="ac25c-267">예를 들어 치명적이 지 않은 오류에 대 한 경고 메시지를 표시 하 고 연결을 속도 저하 하거나 자주 삭제 하는 등의 일시적인 연결 문제를 발생 시키려면 이벤트를 처리 `ConnectionSlow` 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-267">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="ac25c-268">자세한 내용은 [SignalR의 연결 수명 이벤트 이해 및 처리](handling-connection-lifetime-events.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ac25c-268">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="ac25c-269">오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-269">How to handle errors</span></span>

<span data-ttu-id="ac25c-270">서버에서 자세한 오류 메시지를 명시적으로 사용 하도록 설정 하지 않은 경우 오류 발생 후 SignalR에서 반환 하는 예외 개체는 오류에 대 한 최소 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-270">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="ac25c-271">예를 들어,에 대 한 호출이 `newContosoChatMessage` 실패 하면 오류 개체의 오류 메시지에는 `There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.` 보안을 위해 프로덕션 환경에서 클라이언트에 자세한 오류 메시지를 보내는 것이 권장 되지 않습니다. 그러나 문제 해결을 위해 자세한 오류 메시지를 사용 하려면 서버에서 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-271">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="ac25c-272">SignalR에서 발생 하는 오류를 처리 하기 위해 연결 개체에 대 한 이벤트 처리기를 추가할 수 있습니다 `Error` .</span><span class="sxs-lookup"><span data-stu-id="ac25c-272">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="ac25c-273">메서드 호출에서 발생 하는 오류를 처리 하려면 try-catch 블록에 코드를 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-273">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="ac25c-274">클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ac25c-274">How to enable client-side logging</span></span>

<span data-ttu-id="ac25c-275">클라이언트 쪽 로깅을 사용 하도록 설정 하려면 `TraceLevel` `TraceWriter` 연결 개체에서 및 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-275">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="ac25c-276">서버에서 호출할 수 있는 클라이언트 메서드에 대 한 WPF, Silverlight 및 콘솔 응용 프로그램 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="ac25c-276">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="ac25c-277">서버에서 호출할 수 있는 클라이언트 메서드를 정의 하기 위해 앞에서 보여 준 코드 샘플은 WinRT 클라이언트에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-277">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="ac25c-278">다음 샘플에서는 WPF, Silverlight 및 콘솔 응용 프로그램 클라이언트에 해당 하는 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ac25c-278">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="ac25c-279">매개 변수가 없는 메서드</span><span class="sxs-lookup"><span data-stu-id="ac25c-279">Methods without parameters</span></span>

<span data-ttu-id="ac25c-280">**매개 변수 없이 서버에서 호출 되는 메서드의 WPF 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="ac25c-280">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="ac25c-281">**매개 변수 없이 서버에서 호출 되는 메서드에 대 한 Silverlight 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="ac25c-281">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="ac25c-282">**매개 변수가 없는 서버에서 호출 되는 메서드에 대 한 콘솔 응용 프로그램 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="ac25c-282">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="ac25c-283">매개 변수가 있는 메서드, 매개 변수 형식 지정</span><span class="sxs-lookup"><span data-stu-id="ac25c-283">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="ac25c-284">**매개 변수를 사용 하 여 서버에서 호출 된 메서드의 WPF 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="ac25c-284">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="ac25c-285">**매개 변수를 사용 하 여 서버에서 호출 된 메서드에 대 한 Silverlight 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="ac25c-285">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="ac25c-286">**매개 변수를 사용 하 여 서버에서 호출 된 메서드에 대 한 콘솔 응용 프로그램 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="ac25c-286">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="ac25c-287">매개 변수가 있는 메서드, 매개 변수에 대 한 동적 개체 지정</span><span class="sxs-lookup"><span data-stu-id="ac25c-287">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="ac25c-288">**매개 변수에 대 한 동적 개체를 사용 하 여 매개 변수를 사용 하는 서버에서 호출 된 메서드의 WPF 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="ac25c-288">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="ac25c-289">**매개 변수에 대 한 동적 개체를 사용 하 여 매개 변수를 사용 하 여 서버에서 호출 된 메서드에 대 한 Silverlight 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="ac25c-289">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="ac25c-290">**매개 변수에 대 한 동적 개체를 사용 하 여 매개 변수를 사용 하 여 서버에서 호출 된 메서드에 대 한 콘솔 응용 프로그램 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="ac25c-290">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
