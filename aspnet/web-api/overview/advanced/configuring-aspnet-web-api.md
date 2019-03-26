---
uid: web-api/overview/advanced/configuring-aspnet-web-api
title: ASP.NET Web API 2 구성 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 03/31/2014
ms.assetid: 9e10a700-8d91-4d2e-a31e-b8b569fe867c
msc.legacyurl: /web-api/overview/advanced/configuring-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 270268b77f398084169843e20b0a2bf9f1c2a011
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58423158"
---
<a name="configuring-aspnet-web-api-2"></a><span data-ttu-id="ed45c-102">ASP.NET Web API 2 구성</span><span class="sxs-lookup"><span data-stu-id="ed45c-102">Configuring ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="ed45c-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ed45c-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="ed45c-104">이 항목에서는 ASP.NET Web API를 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-104">This topic describes how to configure ASP.NET Web API.</span></span>

- [<span data-ttu-id="ed45c-105">구성 설정</span><span class="sxs-lookup"><span data-stu-id="ed45c-105">Configuration Settings</span></span>](#settings)
- [<span data-ttu-id="ed45c-106">Web API를 사용 하 여 ASP.NET 호스팅 구성</span><span class="sxs-lookup"><span data-stu-id="ed45c-106">Configuring Web API with ASP.NET Hosting</span></span>](#webhost)
- [<span data-ttu-id="ed45c-107">OWIN 자체 호스팅을 사용 하 여 Web API 구성</span><span class="sxs-lookup"><span data-stu-id="ed45c-107">Configuring Web API with OWIN Self-Hosting</span></span>](#selfhost)
- [<span data-ttu-id="ed45c-108">글로벌 웹 API 서비스</span><span class="sxs-lookup"><span data-stu-id="ed45c-108">Global Web API Services</span></span>](#services)
- [<span data-ttu-id="ed45c-109">-컨트롤러 구성</span><span class="sxs-lookup"><span data-stu-id="ed45c-109">Per-Controller Configuration</span></span>](#percontrollerconfig)

<a id="settings"></a>
## <a name="configuration-settings"></a><span data-ttu-id="ed45c-110">Configuration 설정</span><span class="sxs-lookup"><span data-stu-id="ed45c-110">Configuration Settings</span></span>

<span data-ttu-id="ed45c-111">웹 API 구성 설정에 정의 된 [HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx) 클래스.</span><span class="sxs-lookup"><span data-stu-id="ed45c-111">Web API configuration settings are defined in the [HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx) class.</span></span>

| <span data-ttu-id="ed45c-112">멤버</span><span class="sxs-lookup"><span data-stu-id="ed45c-112">Member</span></span> | <span data-ttu-id="ed45c-113">설명</span><span class="sxs-lookup"><span data-stu-id="ed45c-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ed45c-114">**DependencyResolver**</span><span class="sxs-lookup"><span data-stu-id="ed45c-114">**DependencyResolver**</span></span> | <span data-ttu-id="ed45c-115">컨트롤러에 대 한 종속성 주입을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-115">Enables dependency injection for controllers.</span></span> <span data-ttu-id="ed45c-116">참조 [Web API 종속성 확인자를 사용 하 여](dependency-injection.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-116">See [Using the Web API Dependency Resolver](dependency-injection.md).</span></span> |
| <span data-ttu-id="ed45c-117">**필터**</span><span class="sxs-lookup"><span data-stu-id="ed45c-117">**Filters**</span></span> | <span data-ttu-id="ed45c-118">작업 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-118">Action filters.</span></span> |
| <span data-ttu-id="ed45c-119">**포맷터**</span><span class="sxs-lookup"><span data-stu-id="ed45c-119">**Formatters**</span></span> | <span data-ttu-id="ed45c-120">[미디어 유형 포맷터](../formats-and-model-binding/media-formatters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-120">[Media-type formatters](../formats-and-model-binding/media-formatters.md).</span></span> |
| <span data-ttu-id="ed45c-121">**IncludeErrorDetailPolicy**</span><span class="sxs-lookup"><span data-stu-id="ed45c-121">**IncludeErrorDetailPolicy**</span></span> | <span data-ttu-id="ed45c-122">서버 HTTP 응답 메시지에 예외 메시지, 스택 추적 등의 오류 정보를 포함할지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-122">Specifies whether the server should include error details, such as exception messages and stack traces, in HTTP response messages.</span></span> <span data-ttu-id="ed45c-123">참조 [IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108))합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-123">See [IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108)).</span></span> |
| <span data-ttu-id="ed45c-124">**Initializer**</span><span class="sxs-lookup"><span data-stu-id="ed45c-124">**Initializer**</span></span> | <span data-ttu-id="ed45c-125">구성의 최종 초기화를 수행 하는 함수를 **HttpConfiguration**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-125">A function that performs final initialization of the **HttpConfiguration**.</span></span> |
| <span data-ttu-id="ed45c-126">**MessageHandlers**</span><span class="sxs-lookup"><span data-stu-id="ed45c-126">**MessageHandlers**</span></span> | <span data-ttu-id="ed45c-127">[HTTP 메시지 처리기](http-message-handlers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-127">[HTTP message handlers](http-message-handlers.md).</span></span> |
| <span data-ttu-id="ed45c-128">**ParameterBindingRules**</span><span class="sxs-lookup"><span data-stu-id="ed45c-128">**ParameterBindingRules**</span></span> | <span data-ttu-id="ed45c-129">컨트롤러 작업에서 매개 변수를 바인딩하는 규칙의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-129">A collection of rules for binding parameters on controller actions.</span></span> |
| <span data-ttu-id="ed45c-130">**속성**</span><span class="sxs-lookup"><span data-stu-id="ed45c-130">**Properties**</span></span> | <span data-ttu-id="ed45c-131">제네릭 속성 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-131">A generic property bag.</span></span> |
| <span data-ttu-id="ed45c-132">**경로**</span><span class="sxs-lookup"><span data-stu-id="ed45c-132">**Routes**</span></span> | <span data-ttu-id="ed45c-133">경로의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-133">The collection of routes.</span></span> <span data-ttu-id="ed45c-134">참조 [ASP.NET Web API에서에서 라우팅](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-134">See [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="ed45c-135">**서비스**</span><span class="sxs-lookup"><span data-stu-id="ed45c-135">**Services**</span></span> | <span data-ttu-id="ed45c-136">서비스의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-136">The collection of services.</span></span> <span data-ttu-id="ed45c-137">참조 [Services](#services)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-137">See [Services](#services).</span></span> |


## <a name="prerequisites"></a><span data-ttu-id="ed45c-138">전제 조건</span><span class="sxs-lookup"><span data-stu-id="ed45c-138">Prerequisites</span></span>

<span data-ttu-id="ed45c-139">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional 또는 Enterprise edition.</span><span class="sxs-lookup"><span data-stu-id="ed45c-139">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition.</span></span>

<a id="webhost"></a>
## <a name="configuring-web-api-with-aspnet-hosting"></a><span data-ttu-id="ed45c-140">Web API를 사용 하 여 ASP.NET 호스팅 구성</span><span class="sxs-lookup"><span data-stu-id="ed45c-140">Configuring Web API with ASP.NET Hosting</span></span>

<span data-ttu-id="ed45c-141">ASP.NET 응용 프로그램에서 Web API를 호출 하 여 구성 합니다 [GlobalConfiguration.Configure](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx) 에 **응용 프로그램\_시작** 메서드.</span><span class="sxs-lookup"><span data-stu-id="ed45c-141">In an ASP.NET application, configure Web API by calling [GlobalConfiguration.Configure](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx) in the **Application\_Start** method.</span></span> <span data-ttu-id="ed45c-142">합니다 **구성** 메서드는 형식의 단일 매개 변수를 사용 하 여 대리자 **HttpConfiguration**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-142">The **Configure** method takes a delegate with a single parameter of type **HttpConfiguration**.</span></span> <span data-ttu-id="ed45c-143">모든 대리자 내에서 구성을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-143">Perform all of your configuration inside the delegate.</span></span>

<span data-ttu-id="ed45c-144">익명 대리자를 사용 하는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-144">Here is an example using an anonymous delegate:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="ed45c-145">Visual Studio 2017에서 "ASP.NET 웹 응용 프로그램" 프로젝트 템플릿을 자동으로 설정 구성 코드에 "Web API"를 선택 합니다 **새 ASP.NET 프로젝트** 대화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-145">In Visual Studio 2017, the "ASP.NET Web Application" project template automatically sets up the configuration code, if you select "Web API" in the **New ASP.NET Project** dialog.</span></span>

[![](configuring-aspnet-web-api/_static/image2.png)](configuring-aspnet-web-api/_static/image1.png)

<span data-ttu-id="ed45c-146">프로젝트 템플릿은 앱 내에서 WebApiConfig.cs 파일을 만듭니다\_시작 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-146">The project template creates a file named WebApiConfig.cs inside the App\_Start folder.</span></span> <span data-ttu-id="ed45c-147">이 코드 파일에 Web API 구성 코드를 두어야 하는 대리자를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-147">This code file defines the delegate where you should put your Web API configuration code.</span></span>

![](configuring-aspnet-web-api/_static/image3.png)

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample2.cs?highlight=12)]

<span data-ttu-id="ed45c-148">추가 대리자를 호출 하는 코드 프로젝트 템플릿은 **응용 프로그램\_시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-148">The project template also adds the code that calls the delegate from **Application\_Start**.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample3.cs?highlight=5)]

<a id="selfhost"></a>
## <a name="configuring-web-api-with-owin-self-hosting"></a><span data-ttu-id="ed45c-149">OWIN 자체 호스팅을 사용 하 여 Web API 구성</span><span class="sxs-lookup"><span data-stu-id="ed45c-149">Configuring Web API with OWIN Self-Hosting</span></span>

<span data-ttu-id="ed45c-150">OWIN을 사용 하 여 자체 호스팅 인 경우 새로 만듭니다 **HttpConfiguration** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="ed45c-150">If you are self-hosting with OWIN, create a new **HttpConfiguration** instance.</span></span> <span data-ttu-id="ed45c-151">이 인스턴스에서 모든 구성을 수행 하 고 인스턴스를 전달 합니다 **Owin.UseWebApi** 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="ed45c-151">Perform any configuration on this instance, and then pass the instance to the **Owin.UseWebApi** extension method.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="ed45c-152">이 자습서 [여 ASP.NET Web API 2를 사용 하 여 OWIN](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md) 완료 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-152">The tutorial [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md) shows the complete steps.</span></span>

<a id="services"></a>
## <a name="global-web-api-services"></a><span data-ttu-id="ed45c-153">글로벌 웹 API 서비스</span><span class="sxs-lookup"><span data-stu-id="ed45c-153">Global Web API Services</span></span>

<span data-ttu-id="ed45c-154">합니다 **HttpConfiguration.Services** 컬렉션 Web API 컨트롤러 선택 및 콘텐츠 협상 같은 다양 한 작업을 수행 하는 데 사용 하는 글로벌 서비스 집합을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-154">The **HttpConfiguration.Services** collection contains a set of global services that Web API uses to perform various tasks, such as controller selection and content negotiation.</span></span>

> [!NOTE]
> <span data-ttu-id="ed45c-155">합니다 **Services** 컬렉션 서비스 검색 또는 종속성 주입을 위한 일반 용도의 메커니즘은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-155">The **Services** collection is not a general-purpose mechanism for service discovery or dependency injection.</span></span> <span data-ttu-id="ed45c-156">Web API 프레임 워크에 알려지지 않은 서비스 유형 저장 하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-156">It only stores service types that are known to the Web API framework.</span></span>


<span data-ttu-id="ed45c-157">합니다 **Services** 컬렉션 서비스의 기본 집합을 사용 하 여 초기화 되 고 사용자 고유의 사용자 지정 구현을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-157">The **Services** collection is initialized with a default set of services, and you can provide your own custom implementations.</span></span> <span data-ttu-id="ed45c-158">일부 서비스 인스턴스를 하나만 가질 수 있습니다 다른 여러 인스턴스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-158">Some services support multiple instances, while others can have only one instance.</span></span> <span data-ttu-id="ed45c-159">그러나 (컨트롤러 수준에서 서비스를 제공할 수도 있습니다; 참조 [-컨트롤러 구성](#percontrollerconfig)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-159">(However, you can also provide services at the controller level; see [Per-Controller Configuration](#percontrollerconfig).</span></span>

<span data-ttu-id="ed45c-160">단일 인스턴스 서비스</span><span class="sxs-lookup"><span data-stu-id="ed45c-160">Single-Instance Services</span></span>


| <span data-ttu-id="ed45c-161">서비스</span><span class="sxs-lookup"><span data-stu-id="ed45c-161">Service</span></span> | <span data-ttu-id="ed45c-162">설명</span><span class="sxs-lookup"><span data-stu-id="ed45c-162">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ed45c-163">**IActionValueBinder**</span><span class="sxs-lookup"><span data-stu-id="ed45c-163">**IActionValueBinder**</span></span> | <span data-ttu-id="ed45c-164">매개 변수에 대 한 바인딩을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-164">Gets a binding for a parameter.</span></span> |
| <span data-ttu-id="ed45c-165">**IApiExplorer**</span><span class="sxs-lookup"><span data-stu-id="ed45c-165">**IApiExplorer**</span></span> | <span data-ttu-id="ed45c-166">응용 프로그램에 의해 노출 된 Api의 설명을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-166">Gets descriptions of the APIs exposed by the application.</span></span> <span data-ttu-id="ed45c-167">참조 [Web API에 대 한 도움말 페이지 만들기](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-167">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| <span data-ttu-id="ed45c-168">**IAssembliesResolver**</span><span class="sxs-lookup"><span data-stu-id="ed45c-168">**IAssembliesResolver**</span></span> | <span data-ttu-id="ed45c-169">응용 프로그램에 대 한 어셈블리의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-169">Gets a list of the assemblies for the application.</span></span> <span data-ttu-id="ed45c-170">참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-170">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="ed45c-171">**IBodyModelValidator**</span><span class="sxs-lookup"><span data-stu-id="ed45c-171">**IBodyModelValidator**</span></span> | <span data-ttu-id="ed45c-172">미디어 유형 포맷터를 요청 본문에서 읽을 수 있는 모델의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-172">Validates a model that is read from the request body by a media-type formatter.</span></span> |
| <span data-ttu-id="ed45c-173">**IContentNegotiator**</span><span class="sxs-lookup"><span data-stu-id="ed45c-173">**IContentNegotiator**</span></span> | <span data-ttu-id="ed45c-174">콘텐츠 협상을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-174">Performs content negotiation.</span></span> |
| <span data-ttu-id="ed45c-175">**IDocumentationProvider**</span><span class="sxs-lookup"><span data-stu-id="ed45c-175">**IDocumentationProvider**</span></span> | <span data-ttu-id="ed45c-176">Api에 대 한 설명서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-176">Provides documentation for APIs.</span></span> <span data-ttu-id="ed45c-177">기본값은 **null**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-177">The default is **null**.</span></span> <span data-ttu-id="ed45c-178">참조 [Web API에 대 한 도움말 페이지 만들기](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-178">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| <span data-ttu-id="ed45c-179">**IHostBufferPolicySelector**</span><span class="sxs-lookup"><span data-stu-id="ed45c-179">**IHostBufferPolicySelector**</span></span> | <span data-ttu-id="ed45c-180">호스트 HTTP 메시지 엔터티 본문을 버퍼링 해야 하는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-180">Indicates whether the host should buffer HTTP message entity bodies.</span></span> |
| <span data-ttu-id="ed45c-181">**IHttpActionInvoker**</span><span class="sxs-lookup"><span data-stu-id="ed45c-181">**IHttpActionInvoker**</span></span> | <span data-ttu-id="ed45c-182">컨트롤러 작업을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-182">Invokes a controller action.</span></span> <span data-ttu-id="ed45c-183">참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-183">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="ed45c-184">**IHttpActionSelector**</span><span class="sxs-lookup"><span data-stu-id="ed45c-184">**IHttpActionSelector**</span></span> | <span data-ttu-id="ed45c-185">컨트롤러 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-185">Selects a controller action.</span></span> <span data-ttu-id="ed45c-186">참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-186">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="ed45c-187">**IHttpControllerActivator**</span><span class="sxs-lookup"><span data-stu-id="ed45c-187">**IHttpControllerActivator**</span></span> | <span data-ttu-id="ed45c-188">컨트롤러를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-188">Activates a controller.</span></span> <span data-ttu-id="ed45c-189">참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-189">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="ed45c-190">**IHttpControllerSelector**</span><span class="sxs-lookup"><span data-stu-id="ed45c-190">**IHttpControllerSelector**</span></span> | <span data-ttu-id="ed45c-191">컨트롤러를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-191">Selects a controller.</span></span> <span data-ttu-id="ed45c-192">참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-192">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="ed45c-193">**IHttpControllerTypeResolver**</span><span class="sxs-lookup"><span data-stu-id="ed45c-193">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="ed45c-194">응용 프로그램에서 Web API 컨트롤러 형식 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-194">Provides a list of the Web API controller types in the application.</span></span> <span data-ttu-id="ed45c-195">참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-195">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="ed45c-196">**ITraceManager**</span><span class="sxs-lookup"><span data-stu-id="ed45c-196">**ITraceManager**</span></span> | <span data-ttu-id="ed45c-197">추적 프레임 워크를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-197">Initializes the tracing framework.</span></span> <span data-ttu-id="ed45c-198">참조 [ASP.NET Web API에서에서 추적](../testing-and-debugging/tracing-in-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-198">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="ed45c-199">**ITraceWriter**</span><span class="sxs-lookup"><span data-stu-id="ed45c-199">**ITraceWriter**</span></span> | <span data-ttu-id="ed45c-200">추적 기록기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-200">Provides a trace writer.</span></span> <span data-ttu-id="ed45c-201">기본값은 no-op "추적 작성기입니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-201">The default is a "no-op" trace writer.</span></span> <span data-ttu-id="ed45c-202">참조 [ASP.NET Web API에서에서 추적](../testing-and-debugging/tracing-in-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-202">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="ed45c-203">**IModelValidatorCache**</span><span class="sxs-lookup"><span data-stu-id="ed45c-203">**IModelValidatorCache**</span></span> | <span data-ttu-id="ed45c-204">모델 유효성 검사기의 캐시를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-204">Provides a cache of model validators.</span></span> |

<span data-ttu-id="ed45c-205">다중 인스턴스 서비스</span><span class="sxs-lookup"><span data-stu-id="ed45c-205">Multiple-Instance Services</span></span>


|                 <span data-ttu-id="ed45c-206">서비스</span><span class="sxs-lookup"><span data-stu-id="ed45c-206">Service</span></span>                 |                                                                                                              <span data-ttu-id="ed45c-207">설명</span><span class="sxs-lookup"><span data-stu-id="ed45c-207">Description</span></span>                                                                                                               |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <span data-ttu-id="ed45c-208"><strong>IFilterProvider</strong></span><span class="sxs-lookup"><span data-stu-id="ed45c-208"><strong>IFilterProvider</strong></span></span>     |                                                                                           <span data-ttu-id="ed45c-209">컨트롤러 작업에 대 한 필터의 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-209">Returns a list of filters for a controller action.</span></span>                                                                                           |
|  <span data-ttu-id="ed45c-210"><strong>ModelBinderProvider</strong></span><span class="sxs-lookup"><span data-stu-id="ed45c-210"><strong>ModelBinderProvider</strong></span></span>   |                                                                                                <span data-ttu-id="ed45c-211">지정된 된 형식에 대 한 모델 바인더를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-211">Returns a model binder for a given type.</span></span>                                                                                                |
| <span data-ttu-id="ed45c-212"><strong>ModelMetadataProvider</strong></span><span class="sxs-lookup"><span data-stu-id="ed45c-212"><strong>ModelMetadataProvider</strong></span></span>  |                                                                                                     <span data-ttu-id="ed45c-213">모델에 대 한 메타 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-213">Provides metadata for a model.</span></span>                                                                                                     |
| <span data-ttu-id="ed45c-214"><strong>ModelValidatorProvider</strong></span><span class="sxs-lookup"><span data-stu-id="ed45c-214"><strong>ModelValidatorProvider</strong></span></span> |                                                                                                   <span data-ttu-id="ed45c-215">모델 유효성 검사기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-215">Provides a validator for a model.</span></span>                                                                                                    |
|  <span data-ttu-id="ed45c-216"><strong>ValueProviderFactory</strong></span><span class="sxs-lookup"><span data-stu-id="ed45c-216"><strong>ValueProviderFactory</strong></span></span>  | <span data-ttu-id="ed45c-217">값 공급자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-217">Creates a value provider.</span></span> <span data-ttu-id="ed45c-218">자세한 내용은 Mike Stall의 블로그 게시물을 참조 하세요. [WebAPI에서 사용자 지정 값 공급자를 만드는 방법](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)</span><span class="sxs-lookup"><span data-stu-id="ed45c-218">For more information, see Mike Stall's blog post [How to create a custom value provider in WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)</span></span> |

<span data-ttu-id="ed45c-219">사용자 지정 구현에는 다중 인스턴스 서비스를 추가 하려면 호출 **추가** 또는 **삽입** 에 **Services** 컬렉션:</span><span class="sxs-lookup"><span data-stu-id="ed45c-219">To add a custom implementation to a multi-instance service, call **Add** or **Insert** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="ed45c-220">호출 하는 단일 인스턴스 서비스 사용자 지정 구현으로 바꾸려면 **바꿉니다** 에 **Services** 컬렉션:</span><span class="sxs-lookup"><span data-stu-id="ed45c-220">To replace a single-instance service with a custom implementation, call **Replace** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample6.cs)]

<a id="percontrollerconfig"></a>
## <a name="per-controller-configuration"></a><span data-ttu-id="ed45c-221">-컨트롤러 구성</span><span class="sxs-lookup"><span data-stu-id="ed45c-221">Per-Controller Configuration</span></span>

<span data-ttu-id="ed45c-222">-컨트롤러 별로 다음 설정을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-222">You can override the following settings on a per-controller basis:</span></span>

- <span data-ttu-id="ed45c-223">미디어 유형 포맷터</span><span class="sxs-lookup"><span data-stu-id="ed45c-223">Media-type formatters</span></span>
- <span data-ttu-id="ed45c-224">매개 변수 바인딩 규칙</span><span class="sxs-lookup"><span data-stu-id="ed45c-224">Parameter binding rules</span></span>
- <span data-ttu-id="ed45c-225">서비스</span><span class="sxs-lookup"><span data-stu-id="ed45c-225">Services</span></span>

<span data-ttu-id="ed45c-226">이 위해 구현 하는 사용자 지정 특성을 정의 합니다 **IControllerConfiguration** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-226">To do so, define a custom attribute that implements the **IControllerConfiguration** interface.</span></span> <span data-ttu-id="ed45c-227">컨트롤러에 특성을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-227">Then apply the attribute to the controller.</span></span>

<span data-ttu-id="ed45c-228">다음 예제에서는 기본 미디어 유형 포맷터를 사용자 지정 포맷터를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-228">The following example replaces the default media-type formatters with a custom formatter.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="ed45c-229">합니다 **IControllerConfiguration.Initialize** 메서드는 두 개의 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-229">The **IControllerConfiguration.Initialize** method takes two parameters:</span></span>

- <span data-ttu-id="ed45c-230">**HttpControllerSettings** 개체</span><span class="sxs-lookup"><span data-stu-id="ed45c-230">An **HttpControllerSettings** object</span></span>
- <span data-ttu-id="ed45c-231">**HttpControllerDescriptor** 개체</span><span class="sxs-lookup"><span data-stu-id="ed45c-231">An **HttpControllerDescriptor** object</span></span>

<span data-ttu-id="ed45c-232">합니다 **HttpControllerDescriptor** 확인용으로 (즉, 두 명의 컨트롤러를 구분 하기 위해) 검사할 수 있는 컨트롤러에 대 한 설명을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-232">The **HttpControllerDescriptor** contains a description of the controller, which you can examine for informational purposes (say, to distinguish between two controllers).</span></span>

<span data-ttu-id="ed45c-233">사용 된 **HttpControllerSettings** 컨트롤러를 구성 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-233">Use the **HttpControllerSettings** object to configure the controller.</span></span> <span data-ttu-id="ed45c-234">이 개체는 구성 매개 변수-컨트롤러 별로 재정의할 수 있는 하위 집합을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-234">This object contains the subset of configuration parameters that you can override on a per-controller basis.</span></span> <span data-ttu-id="ed45c-235">변경 되지 않는 설정을 기본적으로 전역 **HttpConfiguration** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ed45c-235">Any settings that you don't change default to the global **HttpConfiguration** object.</span></span>
