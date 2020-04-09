---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET 시그널R 허브 API 가이드 - .NET 클라이언트(C#) | 마이크로 소프트 문서
author: bradygaster
description: 이 문서에서는 Windows 스토어(WinRT), WPF, 실버라이트 및 단점과 같은 .NET 클라이언트에서 SignalR 버전 2에 대한 허브 API를 사용하는 방법을 소개합니다.
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675930"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="d2d55-103">ASP.NET 시그널R 허브 API 가이드 - .NET 클라이언트(C#)</span><span class="sxs-lookup"><span data-stu-id="d2d55-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="d2d55-104">이 문서에서는 Windows 스토어(WinRT), WPF, Silverlight 및 콘솔 응용 프로그램과 같은 .NET 클라이언트에서 SignalR 버전 2에 대한 허브 API를 사용하는 방법을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-104">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
>
> <span data-ttu-id="d2d55-105">SignalR Hubs API를 사용하면 서버에서 연결된 클라이언트로, 클라이언트에서 서버로 원격 프로시저 호출(RPC)을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="d2d55-106">서버 코드에서 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="d2d55-107">클라이언트 코드에서는 서버에서 호출할 수 있는 메서드를 정의하고 서버에서 실행되는 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="d2d55-108">SignalR은 모든 클라이언트-서버 배관을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="d2d55-109">SignalR는 또한 영구 연결이라는 하위 수준 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="d2d55-110">SignalR, 허브 및 영구 연결에 대한 소개 또는 전체 SignalR 응용 프로그램을 빌드하는 방법을 보여 주는 자습서의 경우 [SignalR - 시작](../getting-started/index.md)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d2d55-110">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="d2d55-111">이 항목에 사용된 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="d2d55-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="d2d55-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d2d55-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="d2d55-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="d2d55-113">.NET 4.5</span></span>
> - <span data-ttu-id="d2d55-114">시그널R 버전 2</span><span class="sxs-lookup"><span data-stu-id="d2d55-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="d2d55-115">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="d2d55-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="d2d55-116">이전 버전의 SignalR에 대한 자세한 내용은 [SignalR 이전 버전을](../older-versions/index.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d2d55-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="d2d55-117">질문 및 의견</span><span class="sxs-lookup"><span data-stu-id="d2d55-117">Questions and comments</span></span>
>
> <span data-ttu-id="d2d55-118">이 자습서를 어떻게 좋아했는지, 그리고 페이지 하단의 댓글에서 개선할 수 있는 내용에 대한 피드백을 남겨주세요.</span><span class="sxs-lookup"><span data-stu-id="d2d55-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="d2d55-119">당신은 튜토리얼과 직접 관련이없는 질문이있는 경우, 당신은 [ASP.NET SignalR 포럼에](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 게시하거나 [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="d2d55-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="d2d55-120">개요</span><span class="sxs-lookup"><span data-stu-id="d2d55-120">Overview</span></span>

<span data-ttu-id="d2d55-121">이 문서는 다음 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="d2d55-122">클라이언트 설정</span><span class="sxs-lookup"><span data-stu-id="d2d55-122">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="d2d55-123">연결을 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-123">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="d2d55-124">Silverlight 클라이언트의 교차 도메인 연결</span><span class="sxs-lookup"><span data-stu-id="d2d55-124">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="d2d55-125">연결을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-125">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="d2d55-126">WPF 클라이언트에서 최대 동시 연결 수를 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-126">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="d2d55-127">쿼리 문자열 매개 변수를 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-127">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="d2d55-128">전송 방법을 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-128">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="d2d55-129">HTTP 헤더를 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-129">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="d2d55-130">클라이언트 인증서를 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-130">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="d2d55-131">허브 프록시를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-131">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="d2d55-132">서버가 호출할 수 있는 메서드를 클라이언트에서 정의하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-132">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="d2d55-133">매개 변수가 없는 메서드</span><span class="sxs-lookup"><span data-stu-id="d2d55-133">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="d2d55-134">매개 변수가 있는 방법, 매개 변수 형식 지정</span><span class="sxs-lookup"><span data-stu-id="d2d55-134">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="d2d55-135">매개 변수가 있는 메서드, 매개 변수에 대한 동적 개체 지정</span><span class="sxs-lookup"><span data-stu-id="d2d55-135">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="d2d55-136">처리기를 제거하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-136">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="d2d55-137">클라이언트에서 서버 메서드를 호출하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-137">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="d2d55-138">연결 수명 이벤트를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-138">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="d2d55-139">오류 처리 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-139">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="d2d55-140">클라이언트 측 로깅을 활성화하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-140">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="d2d55-141">서버가 호출할 수 있는 클라이언트 메서드에 대한 WPF, Silverlight 및 콘솔 응용 프로그램 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="d2d55-141">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="d2d55-142">샘플 .NET 클라이언트 프로젝트의 경우 다음 리소스를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d2d55-142">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="d2d55-143">GitHub.com (WinRT, 실버 라이트, 콘솔 응용 프로그램 예)에 [구스타보 - 아르멘타 / 신호 - 샘플.](https://github.com/gustavo-armenta/SignalR-Samples)</span><span class="sxs-lookup"><span data-stu-id="d2d55-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="d2d55-144">[다미안 에드워즈 / 시그널R-무브 셰이프 데모 /](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) GitHub.com 이동 셰이프.데스크톱 (WPF 예).</span><span class="sxs-lookup"><span data-stu-id="d2d55-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="d2d55-145">[시그널R / 마이크로 소프트.AspNet.SignalR.Client.GitHub.com 샘플](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) (콘솔 응용 프로그램 예).</span><span class="sxs-lookup"><span data-stu-id="d2d55-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="d2d55-146">서버 또는 JavaScript 클라이언트를 프로그래밍하는 방법에 대한 설명서는 다음 리소스를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d2d55-146">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="d2d55-147">시그널R 허브 API 가이드 - 서버</span><span class="sxs-lookup"><span data-stu-id="d2d55-147">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="d2d55-148">시그널R 허브 API 가이드 - 자바 스크립트 클라이언트</span><span class="sxs-lookup"><span data-stu-id="d2d55-148">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="d2d55-149">API 참조 항목에 대한 링크는 .NET 4.5 버전의 API에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-149">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="d2d55-150">.NET 4를 사용하는 경우 [.NET 4 버전의 API 항목을](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d2d55-150">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="d2d55-151">클라이언트 설치</span><span class="sxs-lookup"><span data-stu-id="d2d55-151">Client setup</span></span>

<span data-ttu-id="d2d55-152">[Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet 패키지를 [설치합니다(Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) 패키지가 아님).</span><span class="sxs-lookup"><span data-stu-id="d2d55-152">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="d2d55-153">이 패키지는 .NET 4 및 .NET 4.5 모두에 대해 WinRT, 실버라이트, WPF, 콘솔 응용 프로그램 및 Windows Phone 클라이언트를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-153">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="d2d55-154">클라이언트에 있는 SignalR 버전이 서버에 있는 버전과 다른 경우 SignalR은 종종 차이에 적응할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-154">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="d2d55-155">예를 들어 SignalR 버전 2를 실행하는 서버는 1.1.x가 설치된 클라이언트와 버전 2가 설치된 클라이언트를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-155">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="d2d55-156">서버의 버전과 클라이언트의 버전 간의 차이가 너무 크거나 클라이언트가 서버보다 최신 버전인 경우 SignalR은 클라이언트가 연결을 설정하려고 할 때 `InvalidOperationException` 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-156">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="d2d55-157">오류 메시지는 "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-157">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="d2d55-158">연결을 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-158">How to establish a connection</span></span>

<span data-ttu-id="d2d55-159">연결을 설정하려면 전에 개체를 `HubConnection` 만들고 프록시를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-159">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="d2d55-160">연결을 설정하려면 개체에서 `Start` 메서드를 `HubConnection` 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-160">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> <span data-ttu-id="d2d55-161">JavaScript 클라이언트의 경우 연결을 설정하는 메서드를 `Start` 호출하기 전에 하나 이상의 이벤트 처리기를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-161">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="d2d55-162">.NET 클라이언트에는 이 가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-162">This is not necessary for .NET clients.</span></span> <span data-ttu-id="d2d55-163">JavaScript 클라이언트의 경우 생성된 프록시 코드는 서버에 있는 모든 허브에 대한 프록시를 자동으로 생성하며 처리기를 등록하면 클라이언트가 사용할 허브를 지정하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-163">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="d2d55-164">그러나 .NET 클라이언트의 경우 허브 프록시를 수동으로 만들수 있으므로 SignalR은 프록시를 만드는 모든 허브를 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-164">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>

<span data-ttu-id="d2d55-165">샘플 코드는 기본 "/signalr" URL을 사용하여 SignalR 서비스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-165">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="d2d55-166">다른 기본 URL을 지정하는 방법에 대한 자세한 내용은 [ASP.NET SignalR 허브 API 가이드 - 서버 - /signalr URL을](hubs-api-guide-server.md#signalrurl)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d2d55-166">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="d2d55-167">메서드는 `Start` 비동기적으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-167">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="d2d55-168">연결이 설정될 때까지 후속 코드 줄이 실행되지 않도록 하려면 `await` ASP.NET 4.5 비동기 메서드 `.Wait()` 또는 동기 메서드에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-168">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="d2d55-169">WinRT 클라이언트에서는 사용하지 `.Wait()` 마십시오.</span><span class="sxs-lookup"><span data-stu-id="d2d55-169">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="d2d55-170">Silverlight 클라이언트의 교차 도메인 연결</span><span class="sxs-lookup"><span data-stu-id="d2d55-170">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="d2d55-171">Silverlight 클라이언트에서 도메인 간 연결을 사용하도록 설정하는 방법에 대한 자세한 내용은 [도메인 경계를 넘어 서비스를 사용할 수 있도록 설정합니다.](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)</span><span class="sxs-lookup"><span data-stu-id="d2d55-171">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="d2d55-172">연결을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-172">How to configure the connection</span></span>

<span data-ttu-id="d2d55-173">연결을 설정하기 전에 다음 옵션 중 을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-173">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="d2d55-174">동시 연결 제한.</span><span class="sxs-lookup"><span data-stu-id="d2d55-174">Concurrent connections limit.</span></span>
- <span data-ttu-id="d2d55-175">문자열 매개 변수를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-175">Query string parameters.</span></span>
- <span data-ttu-id="d2d55-176">전송 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-176">The transport method.</span></span>
- <span data-ttu-id="d2d55-177">HTTP 헤더.</span><span class="sxs-lookup"><span data-stu-id="d2d55-177">HTTP headers.</span></span>
- <span data-ttu-id="d2d55-178">클라이언트 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-178">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="d2d55-179">WPF 클라이언트에서 최대 동시 연결 수를 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-179">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="d2d55-180">WPF 클라이언트에서 기본값 2에서 최대 동시 연결 수를 늘려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-180">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="d2d55-181">권장 값은 10입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-181">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

<span data-ttu-id="d2d55-182">자세한 내용은 [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d2d55-182">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="d2d55-183">쿼리 문자열 매개 변수를 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-183">How to specify query string parameters</span></span>

<span data-ttu-id="d2d55-184">클라이언트가 연결할 때 서버에 데이터를 보내려면 연결 개체에 쿼리 문자열 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-184">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="d2d55-185">다음 예제에서는 클라이언트 코드에서 쿼리 문자열 매개 변수를 설정하는 방법을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-185">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="d2d55-186">다음 예제에서는 서버 코드에서 쿼리 문자열 매개 변수를 읽는 방법을 보여 주입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-186">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="d2d55-187">전송 방법을 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-187">How to specify the transport method</span></span>

<span data-ttu-id="d2d55-188">연결하는 프로세스의 일부로 SignalR 클라이언트는 일반적으로 서버와 협상하여 서버와 클라이언트 모두에서 지원되는 최상의 전송을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-188">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="d2d55-189">사용하려는 전송을 이미 알고 있는 경우 이 협상 프로세스를 우회할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-189">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="d2d55-190">전송 메서드를 지정하려면 전송 개체를 Start 메서드로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-190">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="d2d55-191">다음 예제에서는 클라이언트 코드에서 전송 메서드를 지정 하는 방법을 보여 주입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-191">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

<span data-ttu-id="d2d55-192">[Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) 네임스페이스에는 전송을 지정하는 데 사용할 수 있는 다음 클래스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-192">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="d2d55-193">[롱폴링교통](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="d2d55-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="d2d55-194">[서버센트이벤트전송](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="d2d55-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="d2d55-195">[WebSocketTransport(서버와](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) 클라이언트 가 모두 .NET 4.5를 사용하는 경우에만 사용 가능)</span><span class="sxs-lookup"><span data-stu-id="d2d55-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="d2d55-196">[자동](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) 전송(클라이언트와 서버 모두에서 지원되는 최상의 전송을 자동으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="d2d55-197">기본 전송입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-197">This is the default transport.</span></span> <span data-ttu-id="d2d55-198">메서드에 `Start` 이 것을 전달하는 것은 아무 것도 전달하지 않는 것과 동일한 효과가 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="d2d55-198">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="d2d55-199">ForeverFrame 전송은 브라우저에서만 사용되므로 이 목록에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-199">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="d2d55-200">서버 코드에서 전송 방법을 확인하는 방법에 대한 자세한 내용은 [ASP.NET SignalR Hubs API 가이드 - 서버 - Context 속성에서 클라이언트에 대한 정보를 얻는 방법을](hubs-api-guide-server.md#contextproperty)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d2d55-200">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="d2d55-201">전송 및 대체에 대한 자세한 내용은 [SignalR - 전송 및 대체 소개를](../getting-started/introduction-to-signalr.md#transports)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d2d55-201">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="d2d55-202">HTTP 헤더를 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-202">How to specify HTTP headers</span></span>

<span data-ttu-id="d2d55-203">HTTP 헤더를 설정하려면 `Headers` 연결 개체에서 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-203">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="d2d55-204">다음 예제에서는 HTTP 헤더를 추가하는 방법을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-204">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="d2d55-205">클라이언트 인증서를 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-205">How to specify client certificates</span></span>

<span data-ttu-id="d2d55-206">클라이언트 인증서를 추가하려면 `AddClientCertificate` 연결 개체에서 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-206">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="d2d55-207">허브 프록시를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-207">How to create the Hub proxy</span></span>

<span data-ttu-id="d2d55-208">Hub가 서버에서 호출할 수 있는 메서드를 정의하고 서버의 Hub에서 메서드를 호출하기 위해 연결 개체를 `CreateHubProxy` 호출하여 Hub에 대한 프록시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-208">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="d2d55-209">전달하는 `CreateHubProxy` 문자열은 Hub 클래스의 이름 또는 서버에서 사용된 경우 `HubName` 특성에 의해 지정된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-209">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="d2d55-210">이름 일치 시 대/소문자는 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-210">Name matching is case-insensitive.</span></span>

<span data-ttu-id="d2d55-211">**서버의 허브 클래스**</span><span class="sxs-lookup"><span data-stu-id="d2d55-211">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="d2d55-212">**허브 클래스에 대한 클라이언트 프록시 만들기**</span><span class="sxs-lookup"><span data-stu-id="d2d55-212">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

<span data-ttu-id="d2d55-213">Hub 클래스를 특성으로 `HubName` 장식하는 경우 해당 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-213">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="d2d55-214">**서버의 허브 클래스**</span><span class="sxs-lookup"><span data-stu-id="d2d55-214">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="d2d55-215">**허브 클래스에 대한 클라이언트 프록시 만들기**</span><span class="sxs-lookup"><span data-stu-id="d2d55-215">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

<span data-ttu-id="d2d55-216">동일한 `HubConnection.CreateHubProxy` `hubName`을 여러 번 호출하는 경우 동일한 `IHubProxy` 캐시된 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-216">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="d2d55-217">서버가 호출할 수 있는 메서드를 클라이언트에서 정의하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-217">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="d2d55-218">서버가 호출할 수 있는 메서드를 정의하려면 `On` 프록시메서드를 사용하여 이벤트 처리기를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-218">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="d2d55-219">메서드 이름 일치는 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-219">Method name matching is case-insensitive.</span></span> <span data-ttu-id="d2d55-220">예를 들어 `Clients.All.UpdateStockPrice` 서버에서 를 `updateStockPrice` `updatestockprice`실행하거나 `UpdateStockPrice` 클라이언트에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-220">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="d2d55-221">클라이언트 플랫폼에 따라 UI를 업데이트하기 위해 메서드 코드를 작성하는 방법에 대한 요구 사항이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-221">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="d2d55-222">표시된 예는 WinRT(Windows 스토어 .NET) 클라이언트에 대한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-222">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="d2d55-223">WPF, Silverlight 및 콘솔 응용 프로그램 예제는 [이 항목의 후반부에 별도의 섹션에](#wpfsl)제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-223">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="d2d55-224">매개 변수가 없는 메서드</span><span class="sxs-lookup"><span data-stu-id="d2d55-224">Methods without parameters</span></span>

<span data-ttu-id="d2d55-225">처리하는 메서드에 매개 변수가 없는 경우 메서드의 비제네릭 `On` 오버로드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-225">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="d2d55-226">**매개 변수없이 클라이언트 메서드를 호출하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="d2d55-226">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="d2d55-227">**매개 변수가 없는 서버에서 호출된 메서드에 대한 WinRT 클라이언트[코드(이 항목의 후반부 WPF 및 Silverlight 예제 참조)](#wpfsl)**</span><span class="sxs-lookup"><span data-stu-id="d2d55-227">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="d2d55-228">매개 변수가 있는 메서드, 매개 변수 형식 지정</span><span class="sxs-lookup"><span data-stu-id="d2d55-228">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="d2d55-229">처리하는 메서드에 매개 변수가 있는 경우 매개 변수 형식을 `On` 메서드의 제네릭 유형으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-229">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="d2d55-230">최대 8개의 매개 `On` 변수를 지정할 수 있도록 하는 메서드의 일반 오버로드가 있습니다(Windows Phone 7의 경우 4개).</span><span class="sxs-lookup"><span data-stu-id="d2d55-230">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="d2d55-231">다음 예제에서는 하나의 매개 변수가 `UpdateStockPrice` 메서드로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-231">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="d2d55-232">**매개 변수를 사용하여 클라이언트 메서드를 호출하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="d2d55-232">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="d2d55-233">**매개 변수에 사용되는 Stock 클래스**</span><span class="sxs-lookup"><span data-stu-id="d2d55-233">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="d2d55-234">**매개 변수가 있는 서버에서 호출된 메서드에 대한 WinRT 클라이언트[코드(이 항목의 후반부 WPF 및 Silverlight 예제 참조)](#wpfsl)**</span><span class="sxs-lookup"><span data-stu-id="d2d55-234">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="d2d55-235">매개 변수가 있는 메서드, 매개 변수에 대한 동적 개체 지정</span><span class="sxs-lookup"><span data-stu-id="d2d55-235">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="d2d55-236">`On` 매개 변수를 메서드의 제네릭 유형으로 지정하는 대신 매개 변수를 동적 개체로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-236">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="d2d55-237">**매개 변수를 사용하여 클라이언트 메서드를 호출하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="d2d55-237">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="d2d55-238">**매개 변수에 사용되는 Stock 클래스**</span><span class="sxs-lookup"><span data-stu-id="d2d55-238">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="d2d55-239">**매개 변수에 대 한 동적 개체를 사용 하 여 매개 변수가 있는 서버에서 호출 하는 메서드에 대 한 WinRT 클라이언트 코드[(이 항목의 후반부 WPF 및 Silverlight 예제 참조)](#wpfsl)**</span><span class="sxs-lookup"><span data-stu-id="d2d55-239">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="d2d55-240">처리기를 제거하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-240">How to remove a handler</span></span>

<span data-ttu-id="d2d55-241">처리기를 제거하려면 해당 `Dispose` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-241">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="d2d55-242">**서버에서 호출된 메서드에 대한 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="d2d55-242">**Client code for a method called from server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="d2d55-243">**처리기를 제거하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="d2d55-243">**Client code to remove the handler**</span></span>

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="d2d55-244">클라이언트에서 서버 메서드를 호출하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-244">How to call server methods from the client</span></span>

<span data-ttu-id="d2d55-245">서버에서 메서드를 호출하려면 Hub `Invoke` 프록시에서 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-245">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="d2d55-246">서버 메서드에 반환 값이 없는 경우 메서드의 비제네릭 오버로드를 `Invoke` 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-246">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="d2d55-247">**반환 값이 없는 메서드의 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="d2d55-247">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="d2d55-248">**반환 값이 없는 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="d2d55-248">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="d2d55-249">서버 메서드에 반환 값이 있는 경우 반환 형식을 `Invoke` 메서드의 제네릭 유형으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-249">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="d2d55-250">**반환 값이 있고 복잡한 형식 매개 변수를 사용하는 메서드의 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="d2d55-250">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="d2d55-251">**매개 변수 및 반환 값에 사용되는 Stock 클래스**</span><span class="sxs-lookup"><span data-stu-id="d2d55-251">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="d2d55-252">**반환 값이 있고 ASP.NET 4.5 비동기 메서드에서 복잡한 형식 매개 변수를 사용하는 메서드를 호출하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="d2d55-252">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="d2d55-253">**클라이언트 코드는 반환 값이 있고 동기 메서드에서 복잡한 형식 매개 변수를 사용하는 메서드를 호출합니다.**</span><span class="sxs-lookup"><span data-stu-id="d2d55-253">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="d2d55-254">메서드는 `Invoke` 비동기적으로 실행 하 고 `Task` 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-254">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="d2d55-255">지정하지 `await` `.Wait()`않으면 호출하는 메서드가 실행을 완료하기 전에 다음 코드 줄이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-255">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="d2d55-256">연결 수명 이벤트를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-256">How to handle connection lifetime events</span></span>

<span data-ttu-id="d2d55-257">SignalR은 처리할 수 있는 다음과 같은 연결 수명 이벤트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-257">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="d2d55-258">`Received`: 연결시 데이터가 수신될 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-258">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="d2d55-259">수신된 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-259">Provides the received data.</span></span>
- <span data-ttu-id="d2d55-260">`ConnectionSlow`: 클라이언트가 느리거나 자주 끊어지는 연결을 감지할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-260">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="d2d55-261">`Reconnecting`: 기본 전송이 다시 연결될 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-261">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="d2d55-262">`Reconnected`: 기본 전송이 다시 연결될 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-262">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="d2d55-263">`StateChanged`: 연결 상태가 변경될 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-263">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="d2d55-264">이전 상태와 새 상태를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-264">Provides the old state and the new state.</span></span> <span data-ttu-id="d2d55-265">연결 상태 값에 대한 자세한 내용은 [연결 상태 열거](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d2d55-265">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="d2d55-266">`Closed`: 연결이 끊어졌을 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-266">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="d2d55-267">예를 들어 치명적이지는 않지만 연결 속도가 느려지거나 자주 끊어지는 등의 간헐적인 연결 문제가 발생하는 오류에 `ConnectionSlow` 대한 경고 메시지를 표시하려면 이벤트를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-267">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="d2d55-268">자세한 내용은 [SignalR의 연결 수명 이벤트 이해 및 처리를](handling-connection-lifetime-events.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d2d55-268">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="d2d55-269">오류 처리 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-269">How to handle errors</span></span>

<span data-ttu-id="d2d55-270">서버에서 자세한 오류 메시지를 명시적으로 활성화하지 않으면 오류 후 SignalR이 반환하는 예외 개체에는 오류에 대한 최소한의 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-270">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="d2d55-271">예를 들어 호출이 `newContosoChatMessage` 실패하는 경우 오류 개체의 오류`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`메시지에는 "프로덕션 환경에서 클라이언트에 자세한 오류 메시지를 보내는 것은 보안상의 이유로 권장되지 않지만 문제 해결을 위해 자세한 오류 메시지를 사용하도록 설정하려면 서버에서 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-271">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="d2d55-272">SignalR이 발생 시키는 오류를 처리 하려면 연결 `Error` 개체에 이벤트에 대 한 처리기를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-272">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="d2d55-273">메서드 호출에서 오류를 처리 하려면 try-catch 블록에서 코드를 래핑 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-273">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="d2d55-274">클라이언트 측 로깅을 활성화하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2d55-274">How to enable client-side logging</span></span>

<span data-ttu-id="d2d55-275">클라이언트 측 로깅을 사용하려면 연결 개체의 `TraceLevel` 및 `TraceWriter` 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-275">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="d2d55-276">서버가 호출할 수 있는 클라이언트 메서드에 대한 WPF, Silverlight 및 콘솔 응용 프로그램 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="d2d55-276">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="d2d55-277">서버가 호출할 수 있는 클라이언트 메서드를 정의하기 위해 이전에 표시된 코드 샘플은 WinRT 클라이언트에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-277">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="d2d55-278">다음 샘플에서는 WPF, Silverlight 및 콘솔 응용 프로그램 클라이언트에 해당하는 코드를 보여 준다.</span><span class="sxs-lookup"><span data-stu-id="d2d55-278">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="d2d55-279">매개 변수가 없는 메서드</span><span class="sxs-lookup"><span data-stu-id="d2d55-279">Methods without parameters</span></span>

<span data-ttu-id="d2d55-280">**매개 변수가 없는 서버에서 호출된 메서드에 대한 WPF 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="d2d55-280">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="d2d55-281">**매개 변수가없는 서버에서 호출 된 메서드용 Silverlight 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="d2d55-281">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="d2d55-282">**매개 변수가 없는 서버에서 호출된 메서드에 대한 콘솔 응용 프로그램 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="d2d55-282">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="d2d55-283">매개 변수가 있는 메서드, 매개 변수 형식 지정</span><span class="sxs-lookup"><span data-stu-id="d2d55-283">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="d2d55-284">**매개 변수가 있는 서버에서 호출된 메서드에 대한 WPF 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="d2d55-284">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="d2d55-285">**매개 변수가 있는 서버에서 호출된 메서드에 대한 Silverlight 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="d2d55-285">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="d2d55-286">**매개 변수가 있는 서버에서 호출된 메서드에 대한 콘솔 응용 프로그램 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="d2d55-286">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="d2d55-287">매개 변수가 있는 메서드, 매개 변수에 대한 동적 개체 지정</span><span class="sxs-lookup"><span data-stu-id="d2d55-287">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="d2d55-288">**매개 변수에 대 한 동적 개체를 사용 하 여 매개 변수가 있는 서버에서 호출 하는 메서드에 대 한 WPF 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="d2d55-288">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="d2d55-289">**매개 변수에 대 한 동적 개체를 사용 하 여 매개 변수가 있는 서버에서 호출 하는 메서드에 대 한 Silverlight 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="d2d55-289">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="d2d55-290">**매개 변수에 대 한 동적 개체를 사용 하 여 매개 변수가 있는 서버에서 호출 하는 메서드에 대 한 콘솔 응용 프로그램 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="d2d55-290">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
