---
uid: aspnet/overview/owin-and-katana/katana-samples
title: 카타나 샘플 | 마이크로 소프트 문서
author: rick-anderson
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 15cc1084b16db2619f2295ee21dec4f49eb2e354
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540443"
---
# <a name="katana-samples"></a><span data-ttu-id="aaf5b-102">Katana 샘플</span><span class="sxs-lookup"><span data-stu-id="aaf5b-102">Katana Samples</span></span>

<span data-ttu-id="aaf5b-103">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="aaf5b-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="aaf5b-104">Katana 샘플</span><span class="sxs-lookup"><span data-stu-id="aaf5b-104">Katana Samples</span></span>

<span data-ttu-id="aaf5b-105">**ASP.NET 경로 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span><span class="sxs-lookup"><span data-stu-id="aaf5b-105">**ASP.NET Routes Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span></span>  
<span data-ttu-id="aaf5b-106">일부 응용 프로그램에서는 Asp.Net 경로 테이블에 OWIN 구성 요소를 OWIN이 아닌 구성 요소와 나란히 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="aaf5b-107">이 샘플에서는 Microsoft.Owin.Host.SystemWeb에서 제공하는 RouteCollection 확장 메서드 인 MapOwinPath 및 MapOwinRoute를 사용하는 방법을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="aaf5b-108">**분기 파이프라인 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span><span class="sxs-lookup"><span data-stu-id="aaf5b-108">**Branching Pipelines Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span></span>  
<span data-ttu-id="aaf5b-109">OWIN 요청 처리 파이프라인은 선형일 필요는 없으며 다른 방식으로 요청을 처리하기 위해 분기될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="aaf5b-110">이 샘플에서는 요청 경로 또는 헤더와 같은 다른 요청 데이터를 기반으로 분기 파이프라인을 구성하는 방법을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="aaf5b-111">이러한 구성 요소는 Microsoft.Owin.Mapping 누젯 패키지에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="aaf5b-112">**사용자 지정 서버 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span><span class="sxs-lookup"><span data-stu-id="aaf5b-112">**Custom Server Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span></span>  
<span data-ttu-id="aaf5b-113">OWIN을 자체 호스팅할 때 사용자 지정 OWIN 서버를 사용하는 방법을 보여 주며</span><span class="sxs-lookup"><span data-stu-id="aaf5b-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="aaf5b-114">**임베디드 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span><span class="sxs-lookup"><span data-stu-id="aaf5b-114">**Embedded Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span></span>  
<span data-ttu-id="aaf5b-115">일부 OWIN 서버는 자체 프로세스(자체&quot;호스팅)에서&quot;실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="aaf5b-116">이 샘플에서는 Microsoft.Owin.Hosting nuget 패키지에서 제공하는 도구를 사용하여 OWIN 응용 프로그램을 시작하는 방법을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="aaf5b-117">**헬로월드 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span><span class="sxs-lookup"><span data-stu-id="aaf5b-117">**HelloWorld Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span></span>  
<span data-ttu-id="aaf5b-118">OWIN은 다양한 서버에서 응용 프로그램 이식성을 가능하게 하는 HTTP 서버 API 추상화입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="aaf5b-119">이 샘플에서는 원시 OWIN 추상화 주위에 몇 가지 **간단한 래퍼를** 사용하여 Hello World 응용 프로그램을 작성하고 ASP.NET 같은 웹 서버에서 실행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="aaf5b-120">**안녕하세요 세계 원시 OWIN 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span><span class="sxs-lookup"><span data-stu-id="aaf5b-120">**Hello World Raw OWIN Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span></span>  
<span data-ttu-id="aaf5b-121">이 샘플에서는 **원시** OWIN 추상화를 사용하여 Hello World 응용 프로그램을 작성하고 Asp.Net 같은 웹 서버에서 실행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="aaf5b-122">**시그널R 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span><span class="sxs-lookup"><span data-stu-id="aaf5b-122">**SignalR Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span></span>  
<span data-ttu-id="aaf5b-123">OWIN / 카타나를 사용하여 신호기를 자체 호스트하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="aaf5b-124">자체 호스팅 SignalR에 대한 자세한 내용은 [자습서: SignalR 자체 호스트](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="aaf5b-125">**정적 파일 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span><span class="sxs-lookup"><span data-stu-id="aaf5b-125">**Static Files Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span></span>  
<span data-ttu-id="aaf5b-126">OWIN / 카타나를 사용하여 정적 파일에 대한 HTTP 요청을 지원하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="aaf5b-127">**웹 API** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span><span class="sxs-lookup"><span data-stu-id="aaf5b-127">**Web API** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span></span>  
<span data-ttu-id="aaf5b-128">이 샘플에서는 IIS에서 OWIN을 호스팅하고 OWIN 파이프라인에 웹 API를 추가하는 방법을 보여 주며, 이 샘플에서는 OWIN 파이프라인에 웹 API를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="aaf5b-129">**웹 소켓 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span><span class="sxs-lookup"><span data-stu-id="aaf5b-129">**Web Socket Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span></span>  
<span data-ttu-id="aaf5b-130">[System.Net.WebSockets.WebSocket 클래스를](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) 사용하여 OWIN에서 웹 소켓을 지원하는 방법을 보여 주며</span><span class="sxs-lookup"><span data-stu-id="aaf5b-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
