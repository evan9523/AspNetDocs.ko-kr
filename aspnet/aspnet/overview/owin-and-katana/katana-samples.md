---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Katana 샘플 | Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: b8ce2b40a19e0429f1ccedb03b8f829582652d24
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57056400"
---
<a name="katana-samples"></a><span data-ttu-id="3a827-102">Katana 샘플</span><span class="sxs-lookup"><span data-stu-id="3a827-102">Katana Samples</span></span>
====================
<span data-ttu-id="3a827-103">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3a827-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="3a827-104">Katana 샘플</span><span class="sxs-lookup"><span data-stu-id="3a827-104">Katana Samples</span></span>

<span data-ttu-id="3a827-105">**ASP.NET 샘플 라우팅합니다** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span><span class="sxs-lookup"><span data-stu-id="3a827-105">**ASP.NET Routes Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span></span>  
<span data-ttu-id="3a827-106">일부 응용 프로그램에서 비 OWIN 구성 요소와 함께 Asp.Net 경로 테이블에는 OWIN 구성 요소를 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a827-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="3a827-107">이 샘플에서는 MapOwinPath 및 Microsoft.Owin.Host.SystemWeb 제공한 MapOwinRoute RouteCollection 확장 메서드를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3a827-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="3a827-108">**샘플 파이프라인 분기** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span><span class="sxs-lookup"><span data-stu-id="3a827-108">**Branching Pipelines Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span></span>  
<span data-ttu-id="3a827-109">다른 방법으로 요청을 처리 하는 분기 될 수 있는 OWIN 요청 처리 파이프라인 선형 할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a827-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="3a827-110">이 샘플에는 헤더와 같은 다른 요청 데이터 또는 요청 경로에 따라 파이프라인을 분기를 생성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3a827-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="3a827-111">이러한 구성 요소 Microsoft.Owin.Mapping nuget 패키지에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a827-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="3a827-112">**사용자 지정 서버 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span><span class="sxs-lookup"><span data-stu-id="3a827-112">**Custom Server Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span></span>  
<span data-ttu-id="3a827-113">자체 호스팅하는 경우 사용자 지정 OWIN 서버를 사용 하는 방법을 보여 줍니다. OWIN 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a827-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="3a827-114">**샘플을 포함** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span><span class="sxs-lookup"><span data-stu-id="3a827-114">**Embedded Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span></span>  
<span data-ttu-id="3a827-115">사용자 고유의 프로세스 내에서 일부 OWIN 서버를 실행할 수 있습니다 (&quot;자체 호스팅&quot;).</span><span class="sxs-lookup"><span data-stu-id="3a827-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="3a827-116">이 샘플에서는 Microsoft.Owin.Hosting nuget 패키지에서 제공 하는 도구를 사용 하 여 OWIN 응용 프로그램을 시작 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3a827-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="3a827-117">**HelloWorld 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span><span class="sxs-lookup"><span data-stu-id="3a827-117">**HelloWorld Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span></span>  
<span data-ttu-id="3a827-118">OWIN은 HTTP 서버에서 다양 한 서버 응용 프로그램 이식성을 수 있는 API 추상화를입니다.</span><span class="sxs-lookup"><span data-stu-id="3a827-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="3a827-119">이 샘플에서는 일부를 사용 하 여 Hello World 응용 프로그램을 작성 하는 방법을 보여 줍니다 **간단한 래퍼** ASP.NET 웹 서버에서 같은 원시 OWIN 추상화 및 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a827-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="3a827-120">**Hello World 원시 OWIN 예제** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span><span class="sxs-lookup"><span data-stu-id="3a827-120">**Hello World Raw OWIN Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span></span>  
<span data-ttu-id="3a827-121">이 샘플을 사용 하 여 Hello World 응용 프로그램을 작성 하는 방법에 설명 합니다 **원시** OWIN 추상화 및 Asp.Net과 같은 웹 서버에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a827-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="3a827-122">**SignalR 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span><span class="sxs-lookup"><span data-stu-id="3a827-122">**SignalR Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span></span>  
<span data-ttu-id="3a827-123">OWIN을 사용 하 여 SignalR 자체 호스트 하는 방법을 보여 줍니다 / Katana 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a827-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="3a827-124">자체 호스팅 SignalR에 대 한 자세한 내용은 참조 하세요. [자습서: SignalR 자체 호스팅](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a827-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="3a827-125">**정적 파일 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span><span class="sxs-lookup"><span data-stu-id="3a827-125">**Static Files Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span></span>  
<span data-ttu-id="3a827-126">OWIN을 사용 하 여 정적 파일에 대 한 HTTP 요청을 지 원하는 방법을 보여 줍니다 / Katana 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a827-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="3a827-127">**웹 API** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span><span class="sxs-lookup"><span data-stu-id="3a827-127">**Web API** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span></span>  
<span data-ttu-id="3a827-128">이 샘플에는 IIS에서 OWIN 호스트 OWIN 파이프라인에 Web API를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3a827-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="3a827-129">**웹 소켓 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span><span class="sxs-lookup"><span data-stu-id="3a827-129">**Web Socket Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span></span>  
<span data-ttu-id="3a827-130">사용 하 여 OWIN에서 Websocket을 지원 하는 방법을 보여 줍니다 합니다 [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3a827-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
