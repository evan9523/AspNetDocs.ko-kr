---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET SignalR Hubs API 가이드-JavaScript 클라이언트 | Microsoft Docs
author: bradygaster
description: 이 문서에서는 JavaScript 클라이언트에서 SignalR 버전 2 용 허브 API를 사용 하는 방법을 소개 합니다. 예를 들어 브라우저 및 Windows 스토어 (WinJS)의
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345427"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a><span data-ttu-id="aa881-103">ASP.NET SignalR Hubs API 가이드-JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="aa881-103">ASP.NET SignalR Hubs API Guide - JavaScript Client</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="aa881-104">이 문서에서는 브라우저 및 WinJS (Windows 스토어) 응용 프로그램과 같은 JavaScript 클라이언트에서 SignalR 버전 2 용 허브 API를 사용 하는 방법을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-104">This document provides an introduction to using the Hubs API for SignalR version 2 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
>
> <span data-ttu-id="aa881-105">SignalR Hubs API를 사용 하면 서버에서 연결 된 클라이언트로 또는 클라이언트에서 서버로 Rpc (원격 프로시저 호출)를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="aa881-106">서버 코드에서는 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="aa881-107">클라이언트 코드에서는 서버에서 호출할 수 있는 메서드를 정의 하 고 서버에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="aa881-108">SignalR는 모든 클라이언트에서 서버로의 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="aa881-109">또한 SignalR는 영구 연결 이라고 하는 하위 수준 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="aa881-110">SignalR, 허브 및 영구 연결에 대 한 소개는 [SignalR 소개](../getting-started/introduction-to-signalr.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="aa881-110">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="aa881-111">이 항목에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="aa881-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="aa881-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="aa881-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="aa881-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="aa881-113">.NET 4.5</span></span>
> - <span data-ttu-id="aa881-114">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="aa881-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="aa881-115">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="aa881-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="aa881-116">이전 버전의 SignalR에 대 한 자세한 내용은 [SignalR 이전 버전](../older-versions/index.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="aa881-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="aa881-117">질문 및 설명</span><span class="sxs-lookup"><span data-stu-id="aa881-117">Questions and comments</span></span>
>
> <span data-ttu-id="aa881-118">이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="aa881-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="aa881-119">자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="aa881-120">개요</span><span class="sxs-lookup"><span data-stu-id="aa881-120">Overview</span></span>

<span data-ttu-id="aa881-121">이 문서는 다음 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="aa881-122">생성 된 프록시와 사용자를 위해 수행 하는 작업</span><span class="sxs-lookup"><span data-stu-id="aa881-122">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="aa881-123">생성 된 프록시를 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="aa881-123">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="aa881-124">클라이언트 설정</span><span class="sxs-lookup"><span data-stu-id="aa881-124">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="aa881-125">동적으로 생성 된 프록시를 참조 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-125">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="aa881-126">SignalR 생성 프록시에 대 한 물리적 파일을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-126">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="aa881-127">연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-127">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="aa881-128">$. hubConnection ()에서 생성 하는 것과 동일한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-128">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="aa881-129">시작 메서드의 비동기 실행</span><span class="sxs-lookup"><span data-stu-id="aa881-129">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="aa881-130">도메인 간 연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-130">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="aa881-131">연결을 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-131">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="aa881-132">쿼리 문자열 매개 변수를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-132">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="aa881-133">전송 방법을 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-133">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="aa881-134">허브 클래스에 대 한 프록시를 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-134">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="aa881-135">서버에서 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-135">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="aa881-136">클라이언트에서 서버 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-136">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="aa881-137">연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-137">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="aa881-138">오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-138">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="aa881-139">클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-139">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="aa881-140">서버 또는 .NET 클라이언트를 프로그래밍 하는 방법에 대 한 설명서는 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="aa881-140">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="aa881-141">SignalR Hubs API 가이드-서버</span><span class="sxs-lookup"><span data-stu-id="aa881-141">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="aa881-142">SignalR Hubs API 가이드-.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="aa881-142">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="aa881-143">SignalR 2 서버 구성 요소는 .net 4.5 에서만 사용할 수 있습니다. .net 4.0에는 SignalR 2 용 .NET 클라이언트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-143">The SignalR 2 server component is only available on .NET 4.5 (though there is a .NET client for SignalR 2 on .NET 4.0).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="aa881-144">생성 된 프록시와 사용자를 위해 수행 하는 작업</span><span class="sxs-lookup"><span data-stu-id="aa881-144">The generated proxy and what it does for you</span></span>

<span data-ttu-id="aa881-145">SignalR에서 생성 하는 프록시를 사용 하거나 사용 하지 않고 SignalR 서비스와 통신 하도록 JavaScript 클라이언트를 프로그래밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-145">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="aa881-146">프록시는 사용자가 연결 하는 데 사용 하는 코드의 구문을 간소화 하 고, 서버에서 호출 하는 메서드를 작성 하 고, 서버에서 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-146">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="aa881-147">서버 메서드를 호출 하는 코드를 작성할 때 생성 된 프록시를 사용 하면 로컬 함수를 실행 하는 것 처럼 보이는 구문을 사용할 수 있습니다. 대신을 작성할 수 있습니다 `serverMethod(arg1, arg2)` `invoke('serverMethod', arg1, arg2)` .</span><span class="sxs-lookup"><span data-stu-id="aa881-147">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="aa881-148">서버 메서드 이름을 잘못 입력 한 경우에는 생성 된 프록시 구문을 사용 하 여 즉각적인 있는 클라이언트 쪽 오류가 발생할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-148">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="aa881-149">또한 프록시를 정의 하는 파일을 수동으로 만드는 경우 서버 메서드를 호출 하는 코드를 작성할 수 있도록 IntelliSense 지원을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-149">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="aa881-150">예를 들어 서버에 다음과 같은 허브 클래스가 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-150">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="aa881-151">다음 코드 예제에서는 서버에서 메서드를 호출 `NewContosoChatMessage` 하 고 서버에서 메서드 호출을 수신 하는 JavaScript 코드를 보여 줍니다 `addContosoChatMessageToPage` .</span><span class="sxs-lookup"><span data-stu-id="aa881-151">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="aa881-152">**생성 된 프록시 사용**</span><span class="sxs-lookup"><span data-stu-id="aa881-152">**With the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="aa881-153">**생성 된 프록시 제외**</span><span class="sxs-lookup"><span data-stu-id="aa881-153">**Without the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="aa881-154">생성 된 프록시를 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="aa881-154">When to use the generated proxy</span></span>

<span data-ttu-id="aa881-155">서버에서 호출 하는 클라이언트 메서드에 대해 여러 이벤트 처리기를 등록 하려는 경우에는 생성 된 프록시를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-155">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="aa881-156">그렇지 않으면 코딩 기본 설정에 따라 생성 된 프록시를 사용 하거나 사용 하지 않도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-156">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="aa881-157">사용 하지 않도록 선택 하는 경우 `script` 클라이언트 코드의 요소에서 "signalr/hubs" URL을 참조할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-157">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="aa881-158">클라이언트 설치</span><span class="sxs-lookup"><span data-stu-id="aa881-158">Client setup</span></span>

<span data-ttu-id="aa881-159">JavaScript 클라이언트에는 jQuery 및 SignalR core JavaScript 파일에 대 한 참조가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-159">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="aa881-160">JQuery 버전은 1.7.2, 1.8.2 또는 1.9.1와 같은 1.6.4 또는 주 이후 버전 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-160">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="aa881-161">생성 된 프록시를 사용 하기로 결정 한 경우 SignalR 생성 된 프록시 JavaScript 파일에 대 한 참조도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-161">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="aa881-162">다음 예제에서는 생성 된 프록시를 사용 하는 HTML 페이지에서 참조의 모양을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-162">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="aa881-163">이러한 참조는 jQuery first, SignalR core 이후, SignalR 프록시가 마지막 순서로 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-163">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="aa881-164">동적으로 생성 된 프록시를 참조 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-164">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="aa881-165">앞의 예제에서 SignalR 생성 된 프록시에 대 한 참조는 물리적 파일이 아니라 동적으로 생성 되는 JavaScript 코드에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-165">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="aa881-166">SignalR는 프록시에 대 한 JavaScript 코드를 즉석에서 만들고 "/signalr/hubs" URL에 대 한 응답으로 클라이언트에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-166">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="aa881-167">메서드의 서버에서 SignalR 연결에 대해 다른 기준 URL을 지정한 경우 `MapSignalR` 동적으로 생성 된 프록시 파일의 url은 "/hubs"가 추가 된 사용자 지정 url입니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-167">If you specified a different base URL for SignalR connections on the server in your `MapSignalR` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="aa881-168">Windows 8 (Windows 스토어) JavaScript 클라이언트의 경우 동적으로 생성 되는 것이 아니라 실제 프록시 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-168">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="aa881-169">자세한 내용은이 항목의 뒷부분에 나오는 [SignalR 생성 된 프록시에 대 한 물리적 파일을 만드는 방법](#manualproxy) 을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="aa881-169">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>

<span data-ttu-id="aa881-170">ASP.NET MVC 4 또는 5 Razor 보기에서 물결표를 사용 하 여 프록시 파일 참조의 응용 프로그램 루트를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-170">In an ASP.NET MVC 4 or 5 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="aa881-171">MVC 5에서 SignalR를 사용 하는 방법에 대 한 자세한 내용은 [SignalR 및 mvc 5 시작](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="aa881-171">For more information about using SignalR in MVC 5, see [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="aa881-172">ASP.NET MVC 3 Razor 뷰에서 `Url.Content` 프록시 파일 참조에 대해를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-172">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="aa881-173">ASP.NET Web Forms 응용 프로그램에서 `ResolveClientUrl` 프록시 파일 참조에 사용 하거나, 앱 루트 상대 경로 (물결표로 시작)를 사용 하 여 ScriptManager를 통해 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-173">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="aa881-174">일반적인 규칙으로, CSS 또는 JavaScript 파일에 사용 하는 "/signalr/hubs" URL을 지정 하는 데 동일한 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-174">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="aa881-175">물결표를 사용 하지 않고 URL을 지정 하는 경우 일부 시나리오에서는 IIS Express를 사용 하 여 Visual Studio에서 테스트 하는 경우 응용 프로그램이 올바르게 작동 하지만 전체 IIS에 배포할 때 404 오류가 발생 하 고 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-175">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="aa881-176">자세한 내용은 MSDN 사이트에서 [Visual Studio for ASP.NET 웹 프로젝트의 웹 서버](https://msdn.microsoft.com/library/58wxa9w5.aspx) 에서 Root-Level 리소스에 대 한 **참조 확인** 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="aa881-176">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="aa881-177">디버그 모드에서 Visual Studio 2017을 사용 하 여 웹 프로젝트를 실행 하 고 Internet Explorer를 브라우저로 사용 하는 경우 **스크립트**의 **솔루션 탐색기** 에서 프록시 파일을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-177">When you run a web project in Visual Studio 2017 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Scripts**.</span></span>

<span data-ttu-id="aa881-178">파일의 내용을 보려면 **허브**를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-178">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="aa881-179">Visual Studio 2012 또는 2013 및 Internet Explorer를 사용 하지 않거나 디버그 모드가 아닌 경우 "/signalR/hubs" URL로 이동 하 여 파일의 내용을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-179">If you are not using Visual Studio 2012 or 2013 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="aa881-180">예를 들어 사이트가에서 실행 되는 경우 `http://localhost:56699` `http://localhost:56699/SignalR/hubs` 브라우저에서로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-180">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="aa881-181">SignalR 생성 프록시에 대 한 물리적 파일을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-181">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="aa881-182">동적으로 생성 된 프록시에 대 한 대 안으로 프록시 코드를 포함 하는 물리적 파일을 만들고 해당 파일을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-182">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="aa881-183">이러한 작업을 수행 하 여 캐싱 또는 번들 동작을 제어 하거나 서버 메서드를 코딩 하는 경우 IntelliSense를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-183">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="aa881-184">프록시 파일을 만들려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-184">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="aa881-185">[SignalR 유틸리티](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-185">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="aa881-186">명령 프롬프트를 열고 SignalR.exe 파일이 포함 된 *tools* 폴더로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-186">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="aa881-187">Tools 폴더는 다음 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-187">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. <span data-ttu-id="aa881-188">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-188">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="aa881-189">*.Dll* 의 경로는 일반적으로 프로젝트 폴더의 *bin* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-189">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="aa881-190">이 명령은 *signalr.exe*와 동일한 폴더에 *server.js* 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-190">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="aa881-191">*server.js* 파일을 프로젝트의 적절 한 폴더에 배치 하 고, 응용 프로그램에 맞게 이름을 바꾸고, "signalr/hubs" 참조 대신 해당 폴더에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-191">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="aa881-192">연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-192">How to establish a connection</span></span>

<span data-ttu-id="aa881-193">연결을 설정 하려면 먼저 연결 개체를 만들고 프록시를 만든 다음 서버에서 호출할 수 있는 메서드에 대 한 이벤트 처리기를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-193">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="aa881-194">프록시 및 이벤트 처리기를 설정 하는 경우 메서드를 호출 하 여 연결을 설정 합니다 `start` .</span><span class="sxs-lookup"><span data-stu-id="aa881-194">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="aa881-195">생성 된 프록시를 사용 하는 경우 생성 된 프록시 코드가 사용자에 게이를 수행 하므로 연결 개체를 직접 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-195">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="aa881-196">**생성 된 프록시를 사용 하 여 연결 설정**</span><span class="sxs-lookup"><span data-stu-id="aa881-196">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="aa881-197">**생성 된 프록시를 사용 하지 않고 연결 설정**</span><span class="sxs-lookup"><span data-stu-id="aa881-197">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="aa881-198">샘플 코드는 기본 "/signalr" URL을 사용 하 여 SignalR 서비스에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-198">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="aa881-199">다른 기준 URL을 지정 하는 방법에 대 한 자세한 내용은 [ASP.NET SignalR HUBS API Guide-Server-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="aa881-199">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="aa881-200">기본적으로 허브 위치는 현재 서버입니다. 다른 서버에 연결 하는 경우 다음 예제와 같이 메서드를 호출 하기 전에 URL을 지정 합니다 `start` .</span><span class="sxs-lookup"><span data-stu-id="aa881-200">By default, the hub location is the current server; if you are connecting to a different server, specify the URL before calling the `start` method, as shown in the following example:</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> <span data-ttu-id="aa881-201">일반적으로 메서드를 호출 하 여 연결을 설정 하기 전에 이벤트 처리기를 등록 `start` 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-201">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="aa881-202">연결을 설정한 후 일부 이벤트 처리기를 등록 하려는 경우에는이 작업을 수행할 수 있지만 메서드를 호출 하기 전에 이벤트 처리기를 하나 이상 등록 해야 합니다 `start` .</span><span class="sxs-lookup"><span data-stu-id="aa881-202">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="aa881-203">한 가지 이유는 응용 프로그램에 많은 허브가 있을 수 있지만,이 중 `OnConnected` 하나에만 사용 하려는 경우 모든 허브에서 이벤트를 트리거하지 않으려는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-203">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="aa881-204">연결이 설정 되 면 허브의 프록시에 클라이언트 메서드가 있으면 이벤트를 SignalR 알려 주는 것입니다 `OnConnected` .</span><span class="sxs-lookup"><span data-stu-id="aa881-204">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="aa881-205">메서드를 호출 하기 전에 이벤트 처리기를 등록 하지 않으면 `start` 허브에서 메서드를 호출할 수 있지만 허브의 메서드는 호출 되지 않으며 `OnConnected` 서버에서 클라이언트 메서드가 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-205">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="aa881-206">$. hubConnection ()에서 생성 하는 것과 동일한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-206">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="aa881-207">예제에서 볼 수 있듯이 생성 된 프록시를 사용 하는 경우은 `$.connection.hub` 연결 개체를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-207">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="aa881-208">이는 `$.hubConnection()` 생성 된 프록시를 사용 하지 않을 때를 호출 하 여 가져오는 것과 동일한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-208">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="aa881-209">생성 된 프록시 코드는 다음 문을 실행 하 여 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-209">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![생성 된 프록시 파일에서 연결 만들기](hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="aa881-211">생성 된 프록시를 사용 하는 경우 `$.connection.hub` 생성 된 프록시를 사용 하지 않는 경우 연결 개체로 수행할 수 있는 모든 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-211">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="aa881-212">시작 메서드의 비동기 실행</span><span class="sxs-lookup"><span data-stu-id="aa881-212">Asynchronous execution of the start method</span></span>

<span data-ttu-id="aa881-213">`start`메서드는 비동기적으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-213">The `start` method executes asynchronously.</span></span> <span data-ttu-id="aa881-214">[JQuery 지연 개체](http://api.jquery.com/category/deferred-object/)를 반환 합니다. 즉,, 등의 메서드를 호출 하 여 콜백 함수를 추가할 수 있습니다 `pipe` `done` `fail` .</span><span class="sxs-lookup"><span data-stu-id="aa881-214">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="aa881-215">서버 메서드 호출과 같이 연결이 설정 된 후에 실행 하려는 코드가 있는 경우 해당 코드를 콜백 함수에 넣거나 콜백 함수에서 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-215">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="aa881-216">`.done`콜백 메서드는 연결이 설정 된 후, `OnConnected` 서버의 이벤트 처리기 메서드에 있는 코드의 실행이 완료 된 후에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-216">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="aa881-217">앞의 예제에 있는 "현재 연결 된" 문을 메서드 호출 뒤의 다음 코드 줄로 입력 하면 `start` ( `.done` 콜백이 아닌) `console.log` 다음 예제와 같이 연결이 설정 되기 전에 줄이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-217">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![연결이 설정 된 후 실행 되는 코드를 작성 하는 잘못 된 방법](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="aa881-219">도메인 간 연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-219">How to establish a cross-domain connection</span></span>

<span data-ttu-id="aa881-220">일반적으로 브라우저에서에서 페이지를 로드 하는 경우 `http://contoso.com` SignalR 연결은에서 동일한 도메인에 `http://contoso.com/signalr` 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-220">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="aa881-221">에서 페이지가에 연결 되는 경우 `http://contoso.com` `http://fabrikam.com/signalr` 이는 도메인 간 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-221">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="aa881-222">보안상의 이유로 도메인 간 연결은 기본적으로 사용 하지 않도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-222">For security reasons, cross-domain connections are disabled by default.</span></span>

<span data-ttu-id="aa881-223">SignalR 1.x에서 도메인 간 요청은 단일 EnableCrossDomain 플래그에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-223">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="aa881-224">이 플래그는 JSONP 및 CORS 요청을 모두 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-224">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="aa881-225">유연성을 높이기 위해 SignalR의 서버 구성 요소에서 모든 CORS 지원이 제거 되었습니다. JavaScript 클라이언트는 여전히 CORS를 사용 하 여 브라우저에서 지 원하는 경우에는 CORS를 정상적으로 사용 하 고, 이러한 시나리오를 지원 하기 위해 새로운 OWIN 미들웨어를 사용할 수 있게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-225">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="aa881-226">클라이언트에서 JSONP가 필요한 경우 (이전 브라우저에서 도메인 간 요청을 지원 하려면 `EnableJSONP` 아래와 같이 개체에 대해를로 설정 하 여 명시적으로 사용 하도록 설정 해야 합니다 `HubConfiguration` `true` .</span><span class="sxs-lookup"><span data-stu-id="aa881-226">If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="aa881-227">JSONP는 CORS 보다 안전 하지 않으므로 기본적으로 사용 하지 않도록 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-227">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="aa881-228">**프로젝트에 Owin를 추가 하는 중입니다.** 이 라이브러리를 설치 하려면 패키지 관리자 콘솔에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-228">**Adding Microsoft.Owin.Cors to your project:** To install this library, run the following command in the Package Manager Console:</span></span>

`Install-Package Microsoft.Owin.Cors`

<span data-ttu-id="aa881-229">이 명령은 2.1.0 버전의 패키지를 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-229">This command will add the 2.1.0 version of the package to your project.</span></span>

### <a name="calling-usecors"></a><span data-ttu-id="aa881-230">UseCors 호출</span><span class="sxs-lookup"><span data-stu-id="aa881-230">Calling UseCors</span></span>

 <span data-ttu-id="aa881-231">다음 코드 조각에서는 SignalR 2에서 도메인 간 연결을 구현 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-231">The following code snippet demonstrates how to implement cross-domain connections in SignalR 2.</span></span>

<span data-ttu-id="aa881-232">**SignalR 2에서 도메인 간 요청 구현**</span><span class="sxs-lookup"><span data-stu-id="aa881-232">**Implementing cross-domain requests in SignalR 2**</span></span>

<span data-ttu-id="aa881-233">다음 코드에서는 SignalR 2 프로젝트에서 CORS 또는 JSONP를 사용 하도록 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-233">The following code demonstrates how to enable CORS or JSONP in a SignalR 2 project.</span></span> <span data-ttu-id="aa881-234">이 코드 샘플에서는 `Map` 대신 및를 사용 `RunSignalR` `MapSignalR` 하므로 cors 미들웨어는에 지정 된 경로의 모든 트래픽이 아닌 cors를 지원 해야 하는 SignalR 요청에 대해서만 실행 됩니다 `MapSignalR` . Map은 전체 응용 프로그램이 아닌 특정 URL 접두사에 대해 실행 해야 하는 다른 미들웨어에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-234">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) Map can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - <span data-ttu-id="aa881-235">`jQuery.support.cors`코드에서를 true로 설정 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="aa881-235">Don't set `jQuery.support.cors` to true in your code.</span></span>
>
>     ![JQuery를 true로 설정 하지 마세요.](hubs-api-guide-javascript-client/_static/image7.png)
>
>     <span data-ttu-id="aa881-237">SignalR는 CORS 사용을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-237">SignalR handles the use of CORS.</span></span> <span data-ttu-id="aa881-238">`jQuery.support.cors`True로 설정 하면 SignalR에서 브라우저가 CORS를 지원 한다고 가정 하기 때문에 JSONP를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-238">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="aa881-239">Localhost URL에 연결 하는 경우 Internet Explorer 10은 도메인 간 연결을 고려 하지 않으므로 서버에서 도메인 간 연결을 사용 하도록 설정 하지 않은 경우에도 응용 프로그램은 IE 10에서 로컬로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-239">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="aa881-240">Internet Explorer 9에서 도메인 간 연결을 사용 하는 방법에 대 한 자세한 내용은 [이 StackOverflow 스레드](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="aa881-240">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="aa881-241">Chrome에서 도메인 간 연결을 사용 하는 방법에 대 한 자세한 내용은 [이 StackOverflow 스레드](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="aa881-241">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="aa881-242">샘플 코드는 기본 "/signalr" URL을 사용 하 여 SignalR 서비스에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-242">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="aa881-243">다른 기준 URL을 지정 하는 방법에 대 한 자세한 내용은 [ASP.NET SignalR HUBS API Guide-Server-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="aa881-243">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="aa881-244">연결을 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-244">How to configure the connection</span></span>

<span data-ttu-id="aa881-245">연결을 설정 하기 전에 쿼리 문자열 매개 변수를 지정 하거나 전송 방법을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-245">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="aa881-246">쿼리 문자열 매개 변수를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-246">How to specify query string parameters</span></span>

<span data-ttu-id="aa881-247">클라이언트에서 연결할 때 서버에 데이터를 전송 하려는 경우 연결 개체에 쿼리 문자열 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-247">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="aa881-248">다음 예에서는 클라이언트 코드에서 쿼리 문자열 매개 변수를 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-248">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="aa881-249">**생성 된 프록시를 사용 하 여 시작 메서드를 호출 하기 전에 쿼리 문자열 값을 설정 합니다.**</span><span class="sxs-lookup"><span data-stu-id="aa881-249">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="aa881-250">**생성 된 프록시 없이 start 메서드를 호출 하기 전에 쿼리 문자열 값을 설정 합니다.**</span><span class="sxs-lookup"><span data-stu-id="aa881-250">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

<span data-ttu-id="aa881-251">다음 예에서는 서버 코드에서 쿼리 문자열 매개 변수를 읽는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-251">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="aa881-252">전송 방법을 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-252">How to specify the transport method</span></span>

<span data-ttu-id="aa881-253">연결 프로세스의 일부로 SignalR 클라이언트는 서버와 클라이언트 모두에서 지원 되는 최상의 전송을 결정 하기 위해 일반적으로 서버와 협상 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-253">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="aa881-254">사용할 전송을 이미 알고 있는 경우 메서드를 호출할 때 전송 방법을 지정 하 여이 협상 프로세스를 건너뛸 수 있습니다 `start` .</span><span class="sxs-lookup"><span data-stu-id="aa881-254">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="aa881-255">**전송 메서드를 지정 하는 클라이언트 코드 (생성 된 프록시 포함)**</span><span class="sxs-lookup"><span data-stu-id="aa881-255">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

<span data-ttu-id="aa881-256">**전송 메서드를 지정 하는 클라이언트 코드 (생성 된 프록시 제외)**</span><span class="sxs-lookup"><span data-stu-id="aa881-256">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

<span data-ttu-id="aa881-257">또는 SignalR에서 시도 하는 순서 대로 여러 전송 방법을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-257">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="aa881-258">**생성 된 프록시를 사용 하 여 사용자 지정 전송 대체 (fallback) 체계를 지정 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="aa881-258">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="aa881-259">**생성 된 프록시를 사용 하지 않고 사용자 지정 전송 대체 (fallback) 체계를 지정 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="aa881-259">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="aa881-260">전송 방법 지정에 다음 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-260">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="aa881-261">Websocket</span><span class="sxs-lookup"><span data-stu-id="aa881-261">"webSockets"</span></span>
- <span data-ttu-id="aa881-262">"foreverFrame"</span><span class="sxs-lookup"><span data-stu-id="aa881-262">"foreverFrame"</span></span>
- <span data-ttu-id="aa881-263">"serverSentEvents"</span><span class="sxs-lookup"><span data-stu-id="aa881-263">"serverSentEvents"</span></span>
- <span data-ttu-id="aa881-264">"고 폴링"</span><span class="sxs-lookup"><span data-stu-id="aa881-264">"longPolling"</span></span>

<span data-ttu-id="aa881-265">다음 예에서는 연결에서 사용 되는 전송 방법을 확인 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-265">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="aa881-266">**연결에서 사용 하는 전송 방법 (생성 된 프록시 포함)을 표시 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="aa881-266">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

<span data-ttu-id="aa881-267">**생성 된 프록시를 사용 하지 않고 연결에서 사용 되는 전송 방법을 표시 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="aa881-267">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

<span data-ttu-id="aa881-268">서버 코드에서 전송 방법을 확인 하는 방법에 대 한 자세한 내용은 [ASP.NET SignalR HUBS API 가이드-서버-컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법](hubs-api-guide-server.md#contextproperty)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="aa881-268">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="aa881-269">전송 및 대체에 대 한 자세한 내용은 [SignalR에 대 한 소개-전송 및 대체](../getting-started/introduction-to-signalr.md#transports)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="aa881-269">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="aa881-270">허브 클래스에 대 한 프록시를 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-270">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="aa881-271">사용자가 만드는 각 연결 개체는 하나 이상의 허브 클래스를 포함 하는 SignalR 서비스에 대 한 연결 정보를 캡슐화 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-271">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="aa881-272">허브 클래스와 통신 하려면 직접 만든 프록시 개체 (생성 된 프록시를 사용 하지 않는 경우) 또는 사용자를 위해 생성 된 프록시 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-272">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="aa881-273">클라이언트에서 프록시 이름은 카멜식 대/소문자를 구분 하는 허브 클래스 이름 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-273">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="aa881-274">SignalR는 JavaScript 코드가 JavaScript 규칙을 준수할 수 있도록 이러한 변경을 자동으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-274">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="aa881-275">**서버의 허브 클래스**</span><span class="sxs-lookup"><span data-stu-id="aa881-275">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

<span data-ttu-id="aa881-276">**허브에 대해 생성 된 클라이언트 프록시에 대 한 참조 가져오기**</span><span class="sxs-lookup"><span data-stu-id="aa881-276">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

<span data-ttu-id="aa881-277">**프록시를 생성 하지 않고 허브 클래스에 대 한 클라이언트 프록시를 만듭니다.**</span><span class="sxs-lookup"><span data-stu-id="aa881-277">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="aa881-278">허브 클래스를 특성으로 데코레이팅 하는 경우 `HubName` 대/소문자를 변경 하지 않고 정확한 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-278">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="aa881-279">**HubName 특성이 있는 서버의 허브 클래스**</span><span class="sxs-lookup"><span data-stu-id="aa881-279">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

<span data-ttu-id="aa881-280">**허브에 대해 생성 된 클라이언트 프록시에 대 한 참조 가져오기**</span><span class="sxs-lookup"><span data-stu-id="aa881-280">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

<span data-ttu-id="aa881-281">**프록시를 생성 하지 않고 허브 클래스에 대 한 클라이언트 프록시를 만듭니다.**</span><span class="sxs-lookup"><span data-stu-id="aa881-281">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="aa881-282">서버에서 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-282">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="aa881-283">서버에서 허브를 통해 호출할 수 있는 메서드를 정의 하려면 생성 된 프록시의 속성을 사용 하 여 허브 프록시에 이벤트 처리기를 추가 `client` 하거나 `on` 생성 된 프록시를 사용 하지 않는 경우 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-283">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="aa881-284">매개 변수는 복잡 한 개체 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-284">The parameters can be complex objects.</span></span>

<span data-ttu-id="aa881-285">메서드를 호출 하기 전에 이벤트 처리기를 추가 `start` 하 여 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-285">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="aa881-286">메서드를 호출한 후 이벤트 처리기를 추가 하려면 `start` 이 문서의 앞부분에서 [연결을 설정](#establishconnection) 하는 방법의 참고를 참조 하 고 생성 된 프록시를 사용 하지 않고 메서드를 정의 하는 데 표시 된 구문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-286">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="aa881-287">메서드 이름 일치는 대/소문자를 구분 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-287">Method name matching is case-insensitive.</span></span> <span data-ttu-id="aa881-288">예를 들어 서버에 있는는 `Clients.All.addContosoChatMessageToPage` `AddContosoChatMessageToPage` 클라이언트에서, 또는를 실행 합니다 `addContosoChatMessageToPage` `addcontosochatmessagetopage` .</span><span class="sxs-lookup"><span data-stu-id="aa881-288">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="aa881-289">**클라이언트에서 메서드 정의 (생성 된 프록시 포함)**</span><span class="sxs-lookup"><span data-stu-id="aa881-289">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

<span data-ttu-id="aa881-290">**클라이언트에서 메서드를 정의 하는 다른 방법 (생성 된 프록시 포함)**</span><span class="sxs-lookup"><span data-stu-id="aa881-290">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

<span data-ttu-id="aa881-291">**클라이언트에서 메서드를 정의 합니다 (생성 된 프록시를 사용 하지 않거나 시작 메서드를 호출한 후 추가 하는 경우).**</span><span class="sxs-lookup"><span data-stu-id="aa881-291">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

<span data-ttu-id="aa881-292">**클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="aa881-292">**Server code that calls the client method**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

<span data-ttu-id="aa881-293">다음 예제에서는 복합 개체를 메서드 매개 변수로 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-293">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="aa881-294">**클라이언트에서 생성 된 프록시를 사용 하 여 복잡 한 개체를 사용 하는 메서드를 정의 합니다.**</span><span class="sxs-lookup"><span data-stu-id="aa881-294">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

<span data-ttu-id="aa881-295">**클라이언트에서 생성 된 프록시 없이 복잡 한 개체를 사용 하는 메서드를 정의 합니다.**</span><span class="sxs-lookup"><span data-stu-id="aa881-295">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

<span data-ttu-id="aa881-296">**복합 개체를 정의 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="aa881-296">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

<span data-ttu-id="aa881-297">**복합 개체를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="aa881-297">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="aa881-298">클라이언트에서 서버 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-298">How to call server methods from the client</span></span>

<span data-ttu-id="aa881-299">클라이언트에서 서버 메서드를 호출 하려면 생성 된 프록시를 `server` 사용 하지 않는 경우 생성 된 프록시의 속성 또는 `invoke` 허브 프록시의 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-299">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="aa881-300">반환 값 또는 매개 변수는 복잡 한 개체 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-300">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="aa881-301">허브에 있는 메서드 이름의 카멜식 대/소문자 버전을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-301">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="aa881-302">SignalR는 JavaScript 코드가 JavaScript 규칙을 준수할 수 있도록 이러한 변경을 자동으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-302">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="aa881-303">다음 예에서는 반환 값이 없는 서버 메서드를 호출 하는 방법과 반환 값이 있는 서버 메서드를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-303">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="aa881-304">**HubMethodName 특성이 없는 서버 메서드**</span><span class="sxs-lookup"><span data-stu-id="aa881-304">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

<span data-ttu-id="aa881-305">**매개 변수에 전달 된 복합 개체를 정의 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="aa881-305">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

<span data-ttu-id="aa881-306">**생성 된 프록시를 사용 하 여 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="aa881-306">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

<span data-ttu-id="aa881-307">**생성 된 프록시를 사용 하지 않고 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="aa881-307">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

<span data-ttu-id="aa881-308">특성을 사용 하 여 허브 메서드를 데코레이팅하는 경우 `HubMethodName` 대/소문자를 변경 하지 않고 해당 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-308">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="aa881-309">HubMethodName 특성이 있는 **서버 메서드**</span><span class="sxs-lookup"><span data-stu-id="aa881-309">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

<span data-ttu-id="aa881-310">**생성 된 프록시를 사용 하 여 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="aa881-310">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="aa881-311">**생성 된 프록시를 사용 하지 않고 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="aa881-311">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

<span data-ttu-id="aa881-312">앞의 예제에서는 반환 값이 없는 서버 메서드를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-312">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="aa881-313">다음 예에서는 반환 값이 있는 서버 메서드를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-313">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="aa881-314">**반환 값을 포함 하는 메서드의 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="aa881-314">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

<span data-ttu-id="aa881-315">반환 값 **에 사용 되는 스톡 클래스입니다** .</span><span class="sxs-lookup"><span data-stu-id="aa881-315">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

<span data-ttu-id="aa881-316">**생성 된 프록시를 사용 하 여 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="aa881-316">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

<span data-ttu-id="aa881-317">**생성 된 프록시를 사용 하지 않고 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="aa881-317">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="aa881-318">연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-318">How to handle connection lifetime events</span></span>

<span data-ttu-id="aa881-319">SignalR는 처리할 수 있는 다음 연결 수명 이벤트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-319">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="aa881-320">`starting`: 연결을 통해 데이터를 보내기 전에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-320">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="aa881-321">`received`: 연결에서 데이터를 받을 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-321">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="aa881-322">받은 데이터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-322">Provides the received data.</span></span>
- <span data-ttu-id="aa881-323">`connectionSlow`: 클라이언트에서 느리거나 자주 삭제 되는 연결을 검색 하는 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-323">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="aa881-324">`reconnecting`: 기본 전송에서 다시 연결을 시작할 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-324">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="aa881-325">`reconnected`: 기본 전송이 다시 연결 되었을 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-325">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="aa881-326">`stateChanged`: 연결 상태가 변경 될 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-326">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="aa881-327">이전 상태와 새 상태 (연결, 연결, 다시 연결 또는 연결 끊김)를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-327">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="aa881-328">`disconnected`: 연결을 끊을 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-328">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="aa881-329">예를 들어, 눈에 띄는 지연을 일으킬 수 있는 연결 문제가 있을 때 경고 메시지를 표시 하려면 이벤트를 처리 `connectionSlow` 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-329">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="aa881-330">**생성 된 프록시를 사용 하 여 connectionSlow 이벤트를 처리 합니다.**</span><span class="sxs-lookup"><span data-stu-id="aa881-330">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

<span data-ttu-id="aa881-331">**생성 된 프록시를 사용 하지 않고 connectionSlow 이벤트를 처리 합니다.**</span><span class="sxs-lookup"><span data-stu-id="aa881-331">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

<span data-ttu-id="aa881-332">자세한 내용은 [SignalR의 연결 수명 이벤트 이해 및 처리](handling-connection-lifetime-events.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="aa881-332">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="aa881-333">오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-333">How to handle errors</span></span>

<span data-ttu-id="aa881-334">SignalR JavaScript 클라이언트는 `error` 에 대 한 처리기를 추가할 수 있는 이벤트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-334">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="aa881-335">또한 fail 메서드를 사용 하 여 서버 메서드 호출로 인해 발생 하는 오류에 대 한 처리기를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-335">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="aa881-336">서버에서 자세한 오류 메시지를 명시적으로 사용 하도록 설정 하지 않은 경우 오류 발생 후 SignalR에서 반환 하는 예외 개체는 오류에 대 한 최소 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-336">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="aa881-337">예를 들어,에 대 한 호출이 `newContosoChatMessage` 실패 하면 오류 개체의 오류 메시지에는 `There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.` 보안을 위해 프로덕션 환경에서 클라이언트에 자세한 오류 메시지를 보내는 것이 권장 되지 않습니다. 그러나 문제 해결을 위해 자세한 오류 메시지를 사용 하려면 서버에서 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-337">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

<span data-ttu-id="aa881-338">다음 예제에서는 오류 이벤트에 대 한 처리기를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-338">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="aa881-339">**생성 된 프록시를 사용 하 여 오류 처리기 추가**</span><span class="sxs-lookup"><span data-stu-id="aa881-339">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

<span data-ttu-id="aa881-340">**생성 된 프록시를 사용 하지 않고 오류 처리기 추가**</span><span class="sxs-lookup"><span data-stu-id="aa881-340">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

<span data-ttu-id="aa881-341">다음 예제에서는 메서드 호출에서 오류를 처리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-341">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="aa881-342">**생성 된 프록시를 사용 하 여 메서드 호출에서 오류를 처리 합니다.**</span><span class="sxs-lookup"><span data-stu-id="aa881-342">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

<span data-ttu-id="aa881-343">**생성 된 프록시를 사용 하지 않고 메서드 호출에서 오류를 처리 합니다.**</span><span class="sxs-lookup"><span data-stu-id="aa881-343">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="aa881-344">메서드 호출이 실패 하면 `error` 이벤트도 발생 하므로 `error` 메서드 처리기 및 `.fail` 메서드 콜백에서 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa881-344">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="aa881-345">클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="aa881-345">How to enable client-side logging</span></span>

<span data-ttu-id="aa881-346">연결에 대 한 클라이언트 쪽 로깅을 사용 하도록 설정 하려면 메서드를 호출 하 여 연결을 `logging` 설정 하기 전에 connection 개체의 속성을 설정 합니다 `start` .</span><span class="sxs-lookup"><span data-stu-id="aa881-346">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="aa881-347">**생성 된 프록시를 사용 하 여 로깅 사용**</span><span class="sxs-lookup"><span data-stu-id="aa881-347">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

<span data-ttu-id="aa881-348">**로깅 사용 (생성 된 프록시 제외)**</span><span class="sxs-lookup"><span data-stu-id="aa881-348">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="aa881-349">로그를 보려면 브라우저의 개발자 도구를 열고 콘솔 탭으로 이동 합니다. 이 작업을 수행 하는 방법을 보여 주는 단계별 지침 및 스크린 샷을 보여 주는 자습서는 ASP.NET Signalr를 사용 하 [여 서버 브로드캐스트-로깅 사용](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="aa881-349">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).</span></span>
