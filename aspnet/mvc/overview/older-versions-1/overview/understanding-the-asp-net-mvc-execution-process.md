---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: ASP.NET MVC 실행 프로세스 이해 | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET MVC 프레임워크가 브라우저 요청을 단계별로 처리하는 방법을 알아봅니다.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 48afbbe7349b80e0ed0b9bab987ae3ccda493aca
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541028"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a><span data-ttu-id="def58-103">ASP.NET MVC 실행 프로세스 이해</span><span class="sxs-lookup"><span data-stu-id="def58-103">Understanding the ASP.NET MVC Execution Process</span></span>

<span data-ttu-id="def58-104">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="def58-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="def58-105">ASP.NET MVC 프레임워크가 브라우저 요청을 단계별로 처리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="def58-105">Learn how the ASP.NET MVC framework processes a browser request step-by-step.</span></span>

<span data-ttu-id="def58-106">ASP.NET MVC 기반 웹 응용 프로그램에 대한 요청은 먼저 HTTP 모듈인 **UrlRoutingModule** 개체를 통과합니다.</span><span class="sxs-lookup"><span data-stu-id="def58-106">Requests to an ASP.NET MVC-based Web application first pass through the **UrlRoutingModule** object, which is an HTTP module.</span></span> <span data-ttu-id="def58-107">이 모듈에서는 요청을 구문 분석하고 경로 선택을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="def58-107">This module parses the request and performs route selection.</span></span> <span data-ttu-id="def58-108">**Url라우팅모듈** 개체는 현재 요청과 일치하는 첫 번째 경로 개체를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def58-108">The **UrlRoutingModule** object selects the first route object that matches the current request.</span></span> <span data-ttu-id="def58-109">경로 개체는 **RouteBase를**구현하는 클래스이며 일반적으로 **Route** 클래스의 인스턴스입니다. 일치하는 경로가 없는 경우 **UrlRoutingModule** 개체는 아무 작업도 수행하지 않으며 요청을 일반 ASP.NET 또는 IIS 요청 처리로 되돌릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def58-109">(A route object is a class that implements **RouteBase**, and is typically an instance of the **Route** class.) If no routes match, the **UrlRoutingModule** object does nothing and lets the request fall back to the regular ASP.NET or IIS request processing.</span></span>

<span data-ttu-id="def58-110">선택한 **경로** 개체에서 **Url라우팅모듈** 개체는 **라우트** 오브젝트와 연결된 **IRouteHandler** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="def58-110">From the selected **Route** object, the **UrlRoutingModule** object obtains the **IRouteHandler** object that is associated with the **Route** object.</span></span> <span data-ttu-id="def58-111">일반적으로 MVC 응용 프로그램에서 는 **MvcRouteHandler**의 인스턴스가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="def58-111">Typically, in an MVC application, this will be an instance of **MvcRouteHandler**.</span></span> <span data-ttu-id="def58-112">**IRouteHandler** 인스턴스는 **IHttpHandler** 개체를 만들고 **IHttpContext** 개체를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="def58-112">The **IRouteHandler** instance creates an **IHttpHandler** object and passes it the **IHttpContext** object.</span></span> <span data-ttu-id="def58-113">기본적으로 MVC에 대한 **IHttpHandler** 인스턴스는 **MvcHandler** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="def58-113">By default, the **IHttpHandler** instance for MVC is the **MvcHandler** object.</span></span> <span data-ttu-id="def58-114">그런 다음 **MvcHandler** 개체는 궁극적으로 요청을 처리할 컨트롤러를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def58-114">The **MvcHandler** object then selects the controller that will ultimately handle the request.</span></span>

> [!NOTE]
> <span data-ttu-id="def58-115">ASP.NET MVC 웹 응용 프로그램이 IIS 7.0에서 실행될 경우 MVC 프로젝트의 파일 확장명은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="def58-115">When an ASP.NET MVC Web application runs in IIS 7.0, no file name extension is required for MVC projects.</span></span> <span data-ttu-id="def58-116">그러나 IIS 6.0에서는 처리기의 요청에 따라 .mvc 파일 확장명을 ASP.NET ISAPI DLL에 매핑해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="def58-116">However, in IIS 6.0, the handler requires that you map the .mvc file name extension to the ASP.NET ISAPI DLL.</span></span>

<span data-ttu-id="def58-117">모듈과 처리기는 ASP.NET MVC 프레임워크의 진입점입니다.</span><span class="sxs-lookup"><span data-stu-id="def58-117">The module and handler are the entry points to the ASP.NET MVC framework.</span></span> <span data-ttu-id="def58-118">두 클래스에서는 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="def58-118">They perform the following actions:</span></span>

- <span data-ttu-id="def58-119">MVC 웹 응용 프로그램에서 적절한 컨트롤러를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def58-119">Select the appropriate controller in an MVC Web application.</span></span>
- <span data-ttu-id="def58-120">특정 컨트롤러 인스턴스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="def58-120">Obtain a specific controller instance.</span></span>
- <span data-ttu-id="def58-121">컨트롤러의 **Execute** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="def58-121">Call the controller's **Execute** method.</span></span>

<span data-ttu-id="def58-122">다음은 MVC 웹 프로젝트의 실행 단계를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="def58-122">The following lists the stages of execution for an MVC Web project:</span></span>

- <span data-ttu-id="def58-123">응용 프로그램에 대한 첫 번째 요청 받기</span><span class="sxs-lookup"><span data-stu-id="def58-123">Receive first request for the application</span></span> 

    - <span data-ttu-id="def58-124">Global.asax 파일에서 **배관** 오브젝트가 **RouteTable** 오브젝트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="def58-124">In the Global.asax file, **Route** objects are added to the **RouteTable** object.</span></span>
- <span data-ttu-id="def58-125">라우팅 수행</span><span class="sxs-lookup"><span data-stu-id="def58-125">Perform routing</span></span> 

    - <span data-ttu-id="def58-126">**Url라우팅 모듈** 모듈은 **RouteTable** 컬렉션에서 첫 번째 일치 **하는 경로** 개체를 사용 하 여 **RouteData** 개체를 만든 다음 **요청 컨텍스트** **(IHttpContext)** 개체를 만드는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="def58-126">The **UrlRoutingModule** module uses the first matching **Route** object in the **RouteTable** collection to create the **RouteData** object, which it then uses to create a **RequestContext** (**IHttpContext**) object.</span></span>
- <span data-ttu-id="def58-127">MVC 요청 처리기 만들기</span><span class="sxs-lookup"><span data-stu-id="def58-127">Create MVC request handler</span></span> 

    - <span data-ttu-id="def58-128">**MvcRouteHandler** 개체는 **MvcHandler** 클래스의 인스턴스를 만들고 **RequestContext** 인스턴스를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="def58-128">The **MvcRouteHandler** object creates an instance of the **MvcHandler** class and passes it the **RequestContext** instance.</span></span>
- <span data-ttu-id="def58-129">컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="def58-129">Create controller</span></span> 

    - <span data-ttu-id="def58-130">**MvcHandler** 개체는 **RequestContext** 인스턴스를 사용하여 **IControllerFactory** 개체(일반적으로 **DefaultControllerFactory** 클래스의 인스턴스)를 식별하여 컨트롤러 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="def58-130">The **MvcHandler** object uses the **RequestContext** instance to identify the **IControllerFactory** object (typically an instance of the **DefaultControllerFactory** class) to create the controller instance with.</span></span>
- <span data-ttu-id="def58-131">컨트롤러 실행 - **MvcHandler** 인스턴스는 컨트롤러의 **Execute** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="def58-131">Execute controller - The **MvcHandler** instance calls the controller s **Execute** method.</span></span> |
- <span data-ttu-id="def58-132">작업 호출</span><span class="sxs-lookup"><span data-stu-id="def58-132">Invoke action</span></span> 

    - <span data-ttu-id="def58-133">대부분의 컨트롤러는 컨트롤러 기본 클래스에서 **상속됩니다.**</span><span class="sxs-lookup"><span data-stu-id="def58-133">Most controllers inherit from the **Controller** base class.</span></span> <span data-ttu-id="def58-134">이렇게 하는 컨트롤러의 경우 컨트롤러와 연결된 **ControllerActionInvoker** 개체는 호출할 컨트롤러 클래스의 작업 메서드를 결정한 다음 해당 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="def58-134">For controllers that do so, the **ControllerActionInvoker** object that is associated with the controller determines which action method of the controller class to call, and then calls that method.</span></span>
- <span data-ttu-id="def58-135">결과 실행</span><span class="sxs-lookup"><span data-stu-id="def58-135">Execute result</span></span> 

    - <span data-ttu-id="def58-136">일반적인 작업 메서드는 사용자 입력을 수신하고 적절한 응답 데이터를 준비한 다음 결과 형식을 반환하여 결과를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def58-136">A typical action method might receive user input, prepare the appropriate response data, and then execute the result by returning a result type.</span></span> <span data-ttu-id="def58-137">실행할 수 있는 기본 제공 결과 형식은 **ViewResult(뷰를** 렌더링하고 가장 자주 사용되는 결과 형식), **리디렉션ToRouteResult,** **리디렉션결과,** **ContentResult,** **JsonResult**및 **EmptyResult**입니다.</span><span class="sxs-lookup"><span data-stu-id="def58-137">The built-in result types that can be executed include the following: **ViewResult** (which renders a view and is the most-often used result type), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**, and **EmptyResult**.</span></span>
