---
title: ASP.NET Core 기본 사항
author: rick-anderson
description: ASP.NET Core 앱을 구축하기 위한 기본적인 개념을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 02/14/2019
uid: fundamentals/index
---
# <a name="aspnet-core-fundamentals"></a><span data-ttu-id="30c89-103">ASP.NET Core 기본 사항</span><span class="sxs-lookup"><span data-stu-id="30c89-103">ASP.NET Core fundamentals</span></span>

<span data-ttu-id="30c89-104">이 문서는 ASP.NET Core 앱을 개발하는 방법을 이해하기 위한 주요 항목의 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-104">This article is an overview of key topics for understanding how to develop ASP.NET Core apps.</span></span>

## <a name="the-startup-class"></a><span data-ttu-id="30c89-105">Startup 클래스</span><span class="sxs-lookup"><span data-stu-id="30c89-105">The Startup class</span></span>

<span data-ttu-id="30c89-106">`Startup` 클래스에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-106">The `Startup` class is where:</span></span>

* <span data-ttu-id="30c89-107">앱에서 요구하는 서비스가 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-107">Any services required by the app are configured.</span></span>
* <span data-ttu-id="30c89-108">요청 처리 파이프라인이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-108">The request handling pipeline is defined.</span></span>

* <span data-ttu-id="30c89-109">서비스를 구성(또는 *등록*)하는 코드는 `Startup.ConfigureServices` 메서드에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-109">Code to configure (or *register*) services is added to the `Startup.ConfigureServices` method.</span></span> <span data-ttu-id="30c89-110">*서비스*는 앱에서 사용되는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-110">*Services* are components that are used by the app.</span></span> <span data-ttu-id="30c89-111">예를 들어, Entity Framework Core 컨텍스트 개체는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-111">For example, an Entity Framework Core context object is a service.</span></span>
* <span data-ttu-id="30c89-112">요청 처리 파이프라인을 구성하는 코드는 `Startup.Configure` 메서드에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-112">Code to configure the request handling pipeline is added to the `Startup.Configure` method.</span></span> <span data-ttu-id="30c89-113">해당 파이프라인은 일련의 *미들웨어* 구성 요소로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-113">The pipeline is composed as a series of *middleware* components.</span></span> <span data-ttu-id="30c89-114">예를 들어 미들웨어는 정적 파일에 대한 요청을 처리하거나 HTTP 요청을 HTTPS로 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-114">For example, a middleware might handle requests for static files or redirect HTTP requests to HTTPS.</span></span> <span data-ttu-id="30c89-115">각 미들웨어는 `HttpContext` 상에서 비동기 작업을 수행한 다음, 파이프라인의 다음 미들웨어를 호출하거나 요청을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-115">Each middleware performs asynchronous operations on an `HttpContext` and then either invokes the next middleware in the pipeline or terminates the request.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="30c89-116">샘플 `Startup` 클래스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-116">Here's a sample `Startup` class:</span></span>

[!code-csharp[](index/snapshots/2.x/Startup1.cs?highlight=3,12)]

::: moniker-end

<span data-ttu-id="30c89-117">자세한 내용은 [앱 시작](xref:fundamentals/startup)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30c89-117">For more information, see [App startup](xref:fundamentals/startup).</span></span>

## <a name="dependency-injection-services"></a><span data-ttu-id="30c89-118">종속성 주입(서비스)</span><span class="sxs-lookup"><span data-stu-id="30c89-118">Dependency injection (services)</span></span>

<span data-ttu-id="30c89-119">ASP.NET Core에는 구성된 서비스를 앱의 클래스에 사용할 수 있도록 만드는 기본 제공 DI(종속성 주입) 프레임워크가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-119">ASP.NET Core has a built-in dependency injection (DI) framework that makes configured services available to an app's classes.</span></span> <span data-ttu-id="30c89-120">클래스에서 서비스의 인스턴스를 가져오는 한 가지 방법은 필수 형식의 매개 변수를 사용하여 생성자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-120">One way to get an instance of a service in a class is to create a constructor with a parameter of the required type.</span></span> <span data-ttu-id="30c89-121">해당 매개 변수는 서비스 형식 또는 인터페이스일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-121">The parameter can be the service type or an interface.</span></span> <span data-ttu-id="30c89-122">DI 시스템에서는 런타임 시 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-122">The DI system provides the service at runtime.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="30c89-123">Entity Framework Core 컨텍스트 개체를 가져오는 데 DI를 사용하는 클래스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-123">Here's a class that uses DI to get an Entity Framework Core context object.</span></span> <span data-ttu-id="30c89-124">강조 표시된 줄은 생성자 주입의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-124">The highlighted line is an example of constructor injection:</span></span>

[!code-csharp[](index/snapshots/2.x/Index.cshtml.cs?highlight=5)]

::: moniker-end

<span data-ttu-id="30c89-125">DI가 기본 제공되면 원하는 경우 타사 IoC(Inversion of Control) 컨테이너에 플러그 인할 수 있도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-125">While DI is built in, it's designed to let you plug in a third-party Inversion of Control (IoC) container if you prefer.</span></span>

<span data-ttu-id="30c89-126">자세한 내용은 [종속성 주입](xref:fundamentals/dependency-injection)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-126">For more information, see [Dependency injection](xref:fundamentals/dependency-injection).</span></span>

## <a name="middleware"></a><span data-ttu-id="30c89-127">미들웨어</span><span class="sxs-lookup"><span data-stu-id="30c89-127">Middleware</span></span>

<span data-ttu-id="30c89-128">요청 처리 파이프라인은 일련의 미들웨어 구성 요소로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-128">The request handling pipeline is composed as a series of middleware components.</span></span> <span data-ttu-id="30c89-129">각 구성 요소는 `HttpContext` 상에서 비동기 작업을 수행한 다음, 파이프라인의 다음 미들웨어를 호출하거나 요청을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-129">Each component performs asynchronous operations on an `HttpContext` and then either invokes the next middleware in the pipeline or terminates the request.</span></span>

<span data-ttu-id="30c89-130">규칙에 따라 미들웨어 구성 요소는 `Startup.Configure` 메서드에서 `Use...` 확장 메서드를 호출하여 파이프라인에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-130">By convention, a middleware component is added to the pipeline by invoking its `Use...` extension method in the `Startup.Configure` method.</span></span> <span data-ttu-id="30c89-131">예를 들어 정적 파일을 렌더링하도록 설정하려면 `UseStaticFiles`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-131">For example, to enable rendering of static files, call `UseStaticFiles`.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="30c89-132">다음 예제에서 강조 표시된 코드는 요청 처리 파이프라인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-132">The highlighted code in the following example configures the request handling pipeline:</span></span>

[!code-csharp[](index/snapshots/2.x/Startup1.cs?highlight=14-16)]

::: moniker-end

<span data-ttu-id="30c89-133">ASP.NET Core는 풍부한 일련의 기본 제공 미들웨어를 포함하고 있으며, 사용자 지정 미들웨어를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-133">ASP.NET Core includes a rich set of built-in middleware, and you can write custom middleware.</span></span>

<span data-ttu-id="30c89-134">자세한 내용은 [미들웨어](xref:fundamentals/middleware/index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30c89-134">For more information, see [Middleware](xref:fundamentals/middleware/index).</span></span>

<a id="host"/>

## <a name="the-host"></a><span data-ttu-id="30c89-135">호스트</span><span class="sxs-lookup"><span data-stu-id="30c89-135">The host</span></span>

<span data-ttu-id="30c89-136">ASP.NET Core 앱은 시작 시 *호스트*를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-136">An ASP.NET Core app builds a *host* on startup.</span></span> <span data-ttu-id="30c89-137">호스트는 다음과 같은 앱의 리소스를 모두 캡슐화하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-137">The host is an object that encapsulates all of the the app's resources, such as:</span></span>

* <span data-ttu-id="30c89-138">HTTP 서버 구현</span><span class="sxs-lookup"><span data-stu-id="30c89-138">An HTTP server implementation</span></span>
* <span data-ttu-id="30c89-139">미들웨어 구성 요소</span><span class="sxs-lookup"><span data-stu-id="30c89-139">Middleware components</span></span>
* <span data-ttu-id="30c89-140">로깅</span><span class="sxs-lookup"><span data-stu-id="30c89-140">Logging</span></span>
* <span data-ttu-id="30c89-141">DI</span><span class="sxs-lookup"><span data-stu-id="30c89-141">DI</span></span>
* <span data-ttu-id="30c89-142">구성하기</span><span class="sxs-lookup"><span data-stu-id="30c89-142">Configuration</span></span>

<span data-ttu-id="30c89-143">하나의 개체에 앱의 모든 상호 종속적 리소스를 포함하는 주요 원인은 수명 관리 즉, 앱 시작 및 종료에 대한 제어 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-143">The main reason for including all of the app's interdependent resources in one object is lifetime management: control over app startup and graceful shutdown.</span></span>

<span data-ttu-id="30c89-144">호스트를 만드는 코드는 `Program.Main`에 포함되고 [작성기 패턴](https://wikipedia.org/wiki/Builder_pattern)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-144">The code to create a host is in `Program.Main` and follows the [builder pattern](https://wikipedia.org/wiki/Builder_pattern).</span></span> <span data-ttu-id="30c89-145">호스트의 일부인 각 리소스를 구성하는 메서드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-145">Methods are called to configure each resource that is part of the host.</span></span> <span data-ttu-id="30c89-146">호스트 개체를 모두 풀링하여 인스턴스화하는 작성기 메서드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-146">A builder method is called to pull it all together and instantiate the host object.</span></span>

::: moniker range="<= aspnetcore-2.2"

<span data-ttu-id="30c89-147">ASP.NET Core 2.x는 웹앱에서 웹 호스트(`WebHost` 클래스)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-147">ASP.NET Core 2.x uses Web Host (the `WebHost` class) for web apps.</span></span> <span data-ttu-id="30c89-148">프레임워크는 다음과 같은 옵션을 일반적으로 사용하여 호스트를 설정하는 `CreateDefaultBuilder` 확장 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-148">The framework provides `CreateDefaultBuilder` extension methods that set up a host with commonly used options, such as the following:</span></span>

* <span data-ttu-id="30c89-149">[Kestrel](#servers)을 웹 서버로 사용하고 IIS 통합을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-149">Use [Kestrel](#servers) as the web server and enable IIS integration.</span></span>
* <span data-ttu-id="30c89-150">*appsettings.json*, 환경 변수, 명령줄 인수 및 기타 원본의 구성을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-150">Load configuration from *appsettings.json*, environment variables, command line arguments, and other sources.</span></span>
* <span data-ttu-id="30c89-151">콘솔 및 디버그 공급 기업에 로깅 출력을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-151">Send logging output to the console and debug providers.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.0 <= aspnetcore-2.2"

<span data-ttu-id="30c89-152">호스트를 빌드하는 샘플 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-152">Here's sample code that builds a host:</span></span>

[!code-csharp[](index/snapshots/2.x/Program1.cs?highlight=9)]

<span data-ttu-id="30c89-153">자세한 내용은 [웹 호스트](xref:fundamentals/host/web-host)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30c89-153">For more information, see [Web Host](xref:fundamentals/host/web-host).</span></span>

::: moniker-end

::: moniker range="> aspnetcore-2.2"

<span data-ttu-id="30c89-154">ASP.NET Core 3.0의 웹앱에서 웹 호스트(`WebHost` 클래스) 또는 제네릭 호스트(`Host` 클래스)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-154">In ASP.NET Core 3.0, Web Host (`WebHost` class) or Generic Host (`Host` class) can be used in a web app.</span></span> <span data-ttu-id="30c89-155">제네릭 호스트를 사용하는 것이 좋고, 웹 호스트를 이전 버전과 호환 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-155">Generic Host is recommended, and Web Host is available for backwards compatibility.</span></span>

<span data-ttu-id="30c89-156">프레임워크는 다음과 같은 옵션을 일반적으로 사용하여 호스트를 설정하는 `CreateDefaultBuilder` 및 `ConfigureWebHostDefaults` 확장 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-156">The framework provides `CreateDefaultBuilder` and `ConfigureWebHostDefaults` extension methods that set up a host with commonly used options, such as the following:</span></span>

* <span data-ttu-id="30c89-157">[Kestrel](#servers)을 웹 서버로 사용하고 IIS 통합을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-157">Use [Kestrel](#servers) as the web server and enable IIS integration.</span></span>
* <span data-ttu-id="30c89-158">*appsettings.json*, *appsettings.[EnvironmentName].json*, 환경 변수 및 명령줄 인수의 구성을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-158">Load configuration from *appsettings.json*, *appsettings.[EnvironmentName].json*, environment variables, and command line arguments.</span></span>
* <span data-ttu-id="30c89-159">콘솔 및 디버그 공급 기업에 로깅 출력을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-159">Send logging output to the console and debug providers.</span></span>

<span data-ttu-id="30c89-160">호스트를 빌드하는 샘플 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-160">Here's sample code that builds a host.</span></span> <span data-ttu-id="30c89-161">일반적으로 사용되는 옵션을 사용하여 호스트를 설정하는 확장 메서드가 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-161">The extension methods that set up the host with commonly used options are highlighted.</span></span>

[!code-csharp[](index/snapshots/3.x/Program1.cs?highlight=9-10)]

<span data-ttu-id="30c89-162">자세한 내용은 [제네릭 호스트](xref:fundamentals/host/generic-host) 및 [웹 호스트](xref:fundamentals/host/web-host)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30c89-162">For more information, see [Generic Host](xref:fundamentals/host/generic-host) and [Web Host](xref:fundamentals/host/web-host)</span></span>

::: moniker-end

### <a name="advanced-host-scenarios"></a><span data-ttu-id="30c89-163">고급 호스트 시나리오</span><span class="sxs-lookup"><span data-stu-id="30c89-163">Advanced host scenarios</span></span>

::: moniker range=">= aspnetcore-2.1 <= aspnetcore-2.2"

<span data-ttu-id="30c89-164">웹 호스트는 HTTP 서버 구현을 포함하도록 설계되었으며 다른 종류의 .NET 앱에 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-164">Web Host is designed to include an HTTP server implementation, which isn't needed for other kinds of .NET apps.</span></span> <span data-ttu-id="30c89-165">2.1 버전에서부터 제네릭 호스트(`Host` 클래스)는 ASP.NET Core 앱&mdash;뿐만 아니라 모든 .NET Core 앱에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-165">Starting in 2.1, Generic Host (`Host` class) is available for any .NET Core app to use&mdash;not just ASP.NET Core apps.</span></span> <span data-ttu-id="30c89-166">제네릭 호스트를 통해 다른 형식의 앱에서 로깅, DI, 구성 및 앱 수명 관리와 같은 교차 편집 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-166">Generic Host lets you use cross-cutting features such as logging, DI, configuration, and app lifetime management in other types of apps.</span></span> <span data-ttu-id="30c89-167">자세한 내용은 [제네릭 호스트](xref:fundamentals/host/generic-host)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30c89-167">For more information, see [Generic Host](xref:fundamentals/host/generic-host).</span></span>

::: moniker-end

::: moniker range="> aspnetcore-2.2"

<span data-ttu-id="30c89-168">제네릭 호스트는 ASP.NET Core 앱&mdash;뿐만 아니라 모든 .NET Core 앱에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-168">Generic Host is available for any .NET Core app to use&mdash;not just ASP.NET Core apps.</span></span> <span data-ttu-id="30c89-169">제네릭 호스트를 통해 다른 형식의 앱에서 로깅, DI, 구성 및 앱 수명 관리와 같은 교차 편집 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-169">Generic Host lets you use cross-cutting features such as logging, DI, configuration, and app lifetime management in other types of apps.</span></span> <span data-ttu-id="30c89-170">자세한 내용은 [제네릭 호스트](xref:fundamentals/host/generic-host)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30c89-170">For more information, see [Generic Host](xref:fundamentals/host/generic-host).</span></span>

::: moniker-end

<span data-ttu-id="30c89-171">호스트를 사용하여 백그라운드 작업을 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-171">You can also use the host to run background tasks.</span></span> <span data-ttu-id="30c89-172">자세한 내용은 [백그라운드 작업](xref:fundamentals/host/hosted-services)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30c89-172">For more information, see [Background tasks](xref:fundamentals/host/hosted-services).</span></span>

## <a name="servers"></a><span data-ttu-id="30c89-173">서버</span><span class="sxs-lookup"><span data-stu-id="30c89-173">Servers</span></span>

<span data-ttu-id="30c89-174">ASP.NET Core 앱은 HTTP 요청을 수신하기 위해 HTTP 서버 구현을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-174">An ASP.NET Core app uses an HTTP server implementation to listen for HTTP requests.</span></span> <span data-ttu-id="30c89-175">해당 서버는 `HttpContext`에 구성된 일련의 [요청 기능](xref:fundamentals/request-features)으로 앱에 대한 요청을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-175">The server surfaces requests to the app as a set of [request features](xref:fundamentals/request-features) composed into an `HttpContext`.</span></span>

::: moniker range=">= aspnetcore-2.2"

# <a name="windowstabwindows"></a>[<span data-ttu-id="30c89-176">Windows</span><span class="sxs-lookup"><span data-stu-id="30c89-176">Windows</span></span>](#tab/windows)

<span data-ttu-id="30c89-177">ASP.NET Core는 다음과 같은 서버 구현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-177">ASP.NET Core provides the following server implementations:</span></span>

* <span data-ttu-id="30c89-178">*Kestrel*은 플랫폼 간 웹 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-178">*Kestrel* is a cross-platform web server.</span></span> <span data-ttu-id="30c89-179">Kestrel은 보통 [IIS](https://www.iis.net/)를 사용하여 역방향 프록시 구성에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-179">Kestrel is often run in a reverse proxy configuration using [IIS](https://www.iis.net/).</span></span> <span data-ttu-id="30c89-180">Kestrel은 ASP.NET Core 2.0 이상에서 인터넷에 직접 공개되는 공용 연결 에지 서버로 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-180">In ASP.NET Core 2.0 or later, Kestrel can be run as a public-facing edge server exposed directly to the Internet.</span></span>
* <span data-ttu-id="30c89-181">*IIS HTTP 서버*는 IIS를 사용하는 Windows용 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-181">*IIS HTTP Server* is a server for windows that uses IIS.</span></span> <span data-ttu-id="30c89-182">이 서버를 사용하면 ASP.NET Core 앱 및 IIS는 동일한 프로세스에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-182">With this server, the ASP.NET Core app and IIS run in the same process.</span></span>
* <span data-ttu-id="30c89-183">*HTTP.sys*는 IIS에서 사용되지 않는 Windows용 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-183">*HTTP.sys* is a server for Windows that isn't used with IIS.</span></span>

# <a name="macostabmacos"></a>[<span data-ttu-id="30c89-184">macOS</span><span class="sxs-lookup"><span data-stu-id="30c89-184">macOS</span></span>](#tab/macos)

<span data-ttu-id="30c89-185">ASP.NET Core는 *Kestrel* 플랫폼 간 서버 구현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-185">ASP.NET Core provides the *Kestrel* cross-platform server implementation.</span></span> <span data-ttu-id="30c89-186">Kestrel은 ASP.NET Core 2.0 이상에서 인터넷에 직접 공개되는 공용 연결 에지 서버로 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-186">In ASP.NET Core 2.0 or later, Kestrel can be run as a public-facing edge server exposed directly to the Internet.</span></span> <span data-ttu-id="30c89-187">Kestrel은 보통 [Nginx](https://nginx.org) 또는 [Apache](https://httpd.apache.org/)를 사용하여 역방향 프록시 구성에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-187">Kestrel is often run in a reverse proxy configuration with [Nginx](https://nginx.org) or [Apache](https://httpd.apache.org/).</span></span>

# <a name="linuxtablinux"></a>[<span data-ttu-id="30c89-188">Linux</span><span class="sxs-lookup"><span data-stu-id="30c89-188">Linux</span></span>](#tab/linux)

<span data-ttu-id="30c89-189">ASP.NET Core는 *Kestrel* 플랫폼 간 서버 구현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-189">ASP.NET Core provides the *Kestrel* cross-platform server implementation.</span></span> <span data-ttu-id="30c89-190">Kestrel은 ASP.NET Core 2.0 이상에서 인터넷에 직접 공개되는 공용 연결 에지 서버로 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-190">In ASP.NET Core 2.0 or later, Kestrel can be run as a public-facing edge server exposed directly to the Internet.</span></span> <span data-ttu-id="30c89-191">Kestrel은 보통 [Nginx](https://nginx.org) 또는 [Apache](https://httpd.apache.org/)를 사용하여 역방향 프록시 구성에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-191">Kestrel is often run in a reverse proxy configuration with [Nginx](https://nginx.org) or [Apache](https://httpd.apache.org/).</span></span>

---

::: moniker-end

::: moniker range="< aspnetcore-2.2"

# <a name="windowstabwindows"></a>[<span data-ttu-id="30c89-192">Windows</span><span class="sxs-lookup"><span data-stu-id="30c89-192">Windows</span></span>](#tab/windows)

<span data-ttu-id="30c89-193">ASP.NET Core는 다음과 같은 서버 구현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-193">ASP.NET Core provides the following server implementations:</span></span>

* <span data-ttu-id="30c89-194">*Kestrel*은 플랫폼 간 웹 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-194">*Kestrel* is a cross-platform web server.</span></span> <span data-ttu-id="30c89-195">Kestrel은 보통 [IIS](https://www.iis.net/)를 사용하여 역방향 프록시 구성에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-195">Kestrel is often run in a reverse proxy configuration using [IIS](https://www.iis.net/).</span></span> <span data-ttu-id="30c89-196">Kestrel은 ASP.NET Core 2.0 이상에서 인터넷에 직접 공개되는 공용 연결 에지 서버로 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-196">In ASP.NET Core 2.0 or later, Kestrel can be run as a public-facing edge server exposed directly to the Internet.</span></span>
* <span data-ttu-id="30c89-197">*HTTP.sys*는 IIS에서 사용되지 않는 Windows용 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-197">*HTTP.sys* is a server for Windows that isn't used with IIS.</span></span>

# <a name="macostabmacos"></a>[<span data-ttu-id="30c89-198">macOS</span><span class="sxs-lookup"><span data-stu-id="30c89-198">macOS</span></span>](#tab/macos)

<span data-ttu-id="30c89-199">ASP.NET Core는 *Kestrel* 플랫폼 간 서버 구현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-199">ASP.NET Core provides the *Kestrel* cross-platform server implementation.</span></span> <span data-ttu-id="30c89-200">Kestrel은 ASP.NET Core 2.0 이상에서 인터넷에 직접 공개되는 공용 연결 에지 서버로 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-200">In ASP.NET Core 2.0 or later, Kestrel can be run as a public-facing edge server exposed directly to the Internet.</span></span> <span data-ttu-id="30c89-201">Kestrel은 보통 [Nginx](https://nginx.org) 또는 [Apache](https://httpd.apache.org/)를 사용하여 역방향 프록시 구성에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-201">Kestrel is often run in a reverse proxy configuration with [Nginx](https://nginx.org) or [Apache](https://httpd.apache.org/).</span></span>

# <a name="linuxtablinux"></a>[<span data-ttu-id="30c89-202">Linux</span><span class="sxs-lookup"><span data-stu-id="30c89-202">Linux</span></span>](#tab/linux)

<span data-ttu-id="30c89-203">ASP.NET Core는 *Kestrel* 플랫폼 간 서버 구현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-203">ASP.NET Core provides the *Kestrel* cross-platform server implementation.</span></span> <span data-ttu-id="30c89-204">Kestrel은 ASP.NET Core 2.0 이상에서 인터넷에 직접 공개되는 공용 연결 에지 서버로 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-204">In ASP.NET Core 2.0 or later, Kestrel can be run as a public-facing edge server exposed directly to the Internet.</span></span> <span data-ttu-id="30c89-205">Kestrel은 보통 [Nginx](http://nginx.org) 또는 [Apache](https://httpd.apache.org/)를 사용하여 역방향 프록시 구성에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-205">Kestrel is often run in a reverse proxy configuration with [Nginx](http://nginx.org) or [Apache](https://httpd.apache.org/).</span></span>

---

::: moniker-end

<span data-ttu-id="30c89-206">자세한 내용은 [서버](xref:fundamentals/servers/index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30c89-206">For more information, see [Servers](xref:fundamentals/servers/index).</span></span>

## <a name="configuration"></a><span data-ttu-id="30c89-207">구성하기</span><span class="sxs-lookup"><span data-stu-id="30c89-207">Configuration</span></span>

<span data-ttu-id="30c89-208">ASP.NET Core는 정렬된 일련의 구성 공급 기업에서 이름-값 쌍으로 설정을 가져오는 구성 프레임워크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-208">ASP.NET Core provides a configuration framework that gets settings as name-value pairs from an ordered set of configuration providers.</span></span> <span data-ttu-id="30c89-209">*.json* 파일, *.xml* 파일, 환경 변수 및 명령줄 인수와 같은 다양한 원본의 기본 제공 구성 공급 기업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-209">There are built-in configuration providers for a variety of sources, such as *.json* files, *.xml* files, environment variables, and command-line arguments.</span></span> <span data-ttu-id="30c89-210">또는 사용자 지정 구성 공급 기업을 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-210">You can also write custom configuration providers.</span></span>

<span data-ttu-id="30c89-211">예를 들어 구성이 *appsettings.json* 및 환경 변수에서 제공되도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-211">For example, you could specify that configuration comes from *appsettings.json* and environment variables.</span></span> <span data-ttu-id="30c89-212">그런 다음, *ConnectionString* 값이 요청되면 프레임워크는 먼저 *appsettings.json* 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-212">Then when the value of *ConnectionString* is requested, the framework looks first in the *appsettings.json* file.</span></span> <span data-ttu-id="30c89-213">거기에서 값을 찾을 수 없을 뿐만 아니라 환경 변수에서도 찾을 수 없으면 환경 변수의 값이 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-213">If the value is found there but also in an environment variable, the value from the environment variable would take precedence.</span></span>

<span data-ttu-id="30c89-214">ASP.NET Core는 암호와 같은 기밀 구성 데이터를 관리하기 위해 [비밀 관리자 도구](xref:security/app-secrets)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-214">For managing confidential configuration data such as passwords, ASP.NET Core provides a [Secret Manager tool](xref:security/app-secrets).</span></span> <span data-ttu-id="30c89-215">프로덕션 비밀의 경우 [Azure Key Vault](/aspnet/core/security/key-vault-configuration)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-215">For production secrets, we recommend [Azure Key Vault](/aspnet/core/security/key-vault-configuration).</span></span>

<span data-ttu-id="30c89-216">자세한 내용은 [구성](xref:fundamentals/configuration/index)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30c89-216">For more information, see [Configuration](xref:fundamentals/configuration/index).</span></span>

## <a name="options"></a><span data-ttu-id="30c89-217">옵션</span><span class="sxs-lookup"><span data-stu-id="30c89-217">Options</span></span>

<span data-ttu-id="30c89-218">가능할 경우 ASP.NET Core는 구성 값을 저장하고 검색하기 위해 *옵션 패턴*을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-218">Where possible, ASP.NET Core follows the *options pattern* for storing and retrieving configuration values.</span></span> <span data-ttu-id="30c89-219">옵션 패턴은 클래스를 사용하여 관련 설정 그룹을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-219">The options pattern uses classes to represent groups of related settings.</span></span>

<span data-ttu-id="30c89-220">예를 들어 다음 코드에서는 WebSockets 옵션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-220">For example, the following code sets WebSockets options:</span></span>

```csharp
var options = new WebSocketOptions  
{  
   KeepAliveInterval = TimeSpan.FromSeconds(120),  
   ReceiveBufferSize = 4096
};  
app.UseWebSockets(options);
```

<span data-ttu-id="30c89-221">자세한 내용은 [옵션](xref:fundamentals/configuration/options)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30c89-221">For more information, see [Options](xref:fundamentals/configuration/options).</span></span>

## <a name="environments"></a><span data-ttu-id="30c89-222">환경</span><span class="sxs-lookup"><span data-stu-id="30c89-222">Environments</span></span>

<span data-ttu-id="30c89-223">*개발*, *준비* 및 *프로덕션*과 같은 실행 환경은 ASP.NET Core의 일급 개념입니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-223">Execution environments, such as *Development*, *Staging*, and *Production*, are a first-class notion in ASP.NET Core.</span></span> <span data-ttu-id="30c89-224">`ASPNETCORE_ENVIRONMENT` 환경 변수를 설정하여 앱을 실행 중인 환경을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-224">You can specify the environment an app is running in by setting the `ASPNETCORE_ENVIRONMENT` environment variable.</span></span> <span data-ttu-id="30c89-225">ASP.NET Core는 앱 시작 시 해당 환경 변수를 읽고 `IHostingEnvironment` 구현에서 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-225">ASP.NET Core reads that environment variable at app startup and stores the value in an `IHostingEnvironment` implementation.</span></span> <span data-ttu-id="30c89-226">환경 개체는 DI를 통해 앱에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-226">The environment object is available anywhere in the app via DI.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="30c89-227">`Startup` 클래스의 다음 샘플 코드는 개발 중에 실행할 때만 자세한 오류 정보를 제공하도록 앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-227">The following sample code from the `Startup` class configures the app to provide detailed error information only when it runs in development:</span></span>

[!code-csharp[](index/snapshots/2.x/Startup2.cs?highlight=3-6)]

::: moniker-end

<span data-ttu-id="30c89-228">자세한 내용은 [환경](xref:fundamentals/environments)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30c89-228">For more information, see [Environments](xref:fundamentals/environments).</span></span>

## <a name="logging"></a><span data-ttu-id="30c89-229">로깅</span><span class="sxs-lookup"><span data-stu-id="30c89-229">Logging</span></span>

<span data-ttu-id="30c89-230">ASP.NET Core는 다양한 기본 제공 및 타사 로깅 공급자와 함께 작동하는 로깅 API를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-230">ASP.NET Core supports a logging API that works with a variety of built-in and third-party logging providers.</span></span> <span data-ttu-id="30c89-231">지원되는 공급 기업에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-231">Available providers include the following:</span></span>

* <span data-ttu-id="30c89-232">콘솔</span><span class="sxs-lookup"><span data-stu-id="30c89-232">Console</span></span>
* <span data-ttu-id="30c89-233">디버그</span><span class="sxs-lookup"><span data-stu-id="30c89-233">Debug</span></span>
* <span data-ttu-id="30c89-234">Windows 이벤트 추적</span><span class="sxs-lookup"><span data-stu-id="30c89-234">Event Tracing on Windows</span></span>
* <span data-ttu-id="30c89-235">Windows 이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="30c89-235">Windows Event Log</span></span>
* <span data-ttu-id="30c89-236">TraceSource</span><span class="sxs-lookup"><span data-stu-id="30c89-236">TraceSource</span></span>
* <span data-ttu-id="30c89-237">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="30c89-237">Azure App Service</span></span>
* <span data-ttu-id="30c89-238">Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="30c89-238">Azure Application Insights</span></span>

<span data-ttu-id="30c89-239">DI에서 `ILogger` 개체를 가져오고 로그 메서드를 호출하여 앱 코드 어디서나 로그를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-239">Write logs from anywhere in an app's code by getting an `ILogger` object from DI and calling log methods.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="30c89-240">생성자 주입 및 로깅 메서드 호출을 강조 표시하고 `ILogger` 개체를 사용하는 샘플 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-240">Here's sample code that uses an `ILogger` object, with constructor injection and the logging method calls highlighted.</span></span>

[!code-csharp[](index/snapshots/2.x/TodoController.cs?highlight=5,13,17)]

::: moniker-end

<span data-ttu-id="30c89-241">`ILogger` 인터페이스를 통해 필드 개수에 관계 없이 로그 공급 기업에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-241">The `ILogger` interface lets you pass any number of fields to the logging provider.</span></span> <span data-ttu-id="30c89-242">필드는 일반적으로 메시지 문자열을 생성하는 데 사용되지만 공급 기업은 이를 별도 필드로 데이터 저장소에 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-242">The fields are commonly used to construct a message string, but the provider can also send them as separate fields to a data store.</span></span> <span data-ttu-id="30c89-243">이 기능을 사용하면 로그 공급 기업이 [구조적 로깅이라고도 하는 의미 체계 로깅](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging)을 구현할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-243">This feature makes it possible for logging providers to implement [semantic logging, also known as structured logging](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).</span></span>

<span data-ttu-id="30c89-244">자세한 내용은 [로깅](xref:fundamentals/logging/index)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30c89-244">For more information, see [Logging](xref:fundamentals/logging/index).</span></span>

## <a name="routing"></a><span data-ttu-id="30c89-245">라우팅</span><span class="sxs-lookup"><span data-stu-id="30c89-245">Routing</span></span>

<span data-ttu-id="30c89-246">*경로*는 처리기에 매핑되는 URL 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-246">A *route* is a URL pattern that is mapped to a handler.</span></span> <span data-ttu-id="30c89-247">처리기는 일반적으로 Razor 페이지, MVC 컨트롤러의 작업 메서드 또는 미들웨어와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-247">The handler is typically a Razor page, an action method in an MVC controller, or a middleware.</span></span> <span data-ttu-id="30c89-248">ASP.NET Core 라우팅을 사용하면 앱에서 사용되는 URL을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-248">ASP.NET Core routing gives you control over the URLs used by your app.</span></span>

<span data-ttu-id="30c89-249">자세한 내용은 [라우팅](xref:fundamentals/routing)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-249">For more information, see [Routing](xref:fundamentals/routing).</span></span>

## <a name="error-handling"></a><span data-ttu-id="30c89-250">오류 처리</span><span class="sxs-lookup"><span data-stu-id="30c89-250">Error handling</span></span>

<span data-ttu-id="30c89-251">ASP.NET Core에는 다음과 같은 오류를 처리하기 위한 기본 제공 기능이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-251">ASP.NET Core has built-in features for handling errors, such as:</span></span>

* <span data-ttu-id="30c89-252">개발자 예외 페이지</span><span class="sxs-lookup"><span data-stu-id="30c89-252">A developer exception page</span></span>
* <span data-ttu-id="30c89-253">사용자 지정 오류 페이지</span><span class="sxs-lookup"><span data-stu-id="30c89-253">Custom error pages</span></span>
* <span data-ttu-id="30c89-254">정적 상태 코드 페이지</span><span class="sxs-lookup"><span data-stu-id="30c89-254">Static status code pages</span></span>
* <span data-ttu-id="30c89-255">시작 예외 처리</span><span class="sxs-lookup"><span data-stu-id="30c89-255">Startup exception handling</span></span>

<span data-ttu-id="30c89-256">자세한 내용은 [오류 처리](xref:fundamentals/error-handling)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30c89-256">For more information, see [Error handling](xref:fundamentals/error-handling).</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="make-http-requests"></a><span data-ttu-id="30c89-257">HTTP 요청 만들기</span><span class="sxs-lookup"><span data-stu-id="30c89-257">Make HTTP requests</span></span>

<span data-ttu-id="30c89-258">`HttpClient` 인스턴스를 만들기 위해 `IHttpClientFactory`를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-258">An implementation of `IHttpClientFactory` is available for creating `HttpClient` instances.</span></span> <span data-ttu-id="30c89-259">팩터리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-259">The factory:</span></span>

* <span data-ttu-id="30c89-260">논리적 `HttpClient` 인스턴스를 구성하고 이름을 지정하기 위해 중앙 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-260">Provides a central location for naming and configuring logical `HttpClient` instances.</span></span> <span data-ttu-id="30c89-261">예를 들어, *github* 클라이언트는 GitHub에 액세스하도록 등록 및 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-261">For example, a *github* client can be registered and configured to access GitHub.</span></span> <span data-ttu-id="30c89-262">다른 용도로 기본 클라이언트를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-262">A default client can be registered for other purposes.</span></span>
* <span data-ttu-id="30c89-263">나가는 요청 미들웨어 파이프라인을 빌드하기 위해 여러 위임 처리기를 연결하고 등록하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-263">Supports registration and chaining of multiple delegating handlers to build an outgoing request middleware pipeline.</span></span> <span data-ttu-id="30c89-264">이 패턴은 ASP.NET Core에서 인바운드 미들웨어 파이프라인과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-264">This pattern is similar to the inbound middleware pipeline in ASP.NET Core.</span></span> <span data-ttu-id="30c89-265">패턴은 캐싱, 오류 처리, serialization 및 로깅을 포함하여 HTTP 요청을 둘러싼 교차 편집 문제를 관리할 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-265">The pattern provides a mechanism to manage cross-cutting concerns around HTTP requests, including caching, error handling, serialization, and logging.</span></span>
* <span data-ttu-id="30c89-266">일시적인 오류를 처리하기 위해 널리 사용되는 타사 라이브러리인 *Polly*와 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-266">Integrates with *Polly*, a popular third-party library for transient fault handling.</span></span>
* <span data-ttu-id="30c89-267">풀링 및 기본의 수명을 관리 수동으로 `HttpClient` 수명을 관리하는 경우 발생하는 일반적인 DNS 문제를 방지하려면 기본 `HttpClientMessageHandler` 인스턴스의 수명 및 풀링을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-267">Manages the pooling and lifetime of underlying `HttpClientMessageHandler` instances to avoid common DNS problems that occur when manually managing `HttpClient` lifetimes.</span></span>
* <span data-ttu-id="30c89-268">팩터리에서 만든 클라이언트를 통해 전송된 모든 요청에 대해 구성 가능한 로깅 환경(*ILogger*를 통해)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-268">Adds a configurable logging experience (via *ILogger*) for all requests sent through clients created by the factory.</span></span>

<span data-ttu-id="30c89-269">자세한 내용은 [HTTP 요청 만들기](xref:fundamentals/http-requests)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30c89-269">For more information, see [Make HTTP requests](xref:fundamentals/http-requests).</span></span>

::: moniker-end

## <a name="content-root"></a><span data-ttu-id="30c89-270">콘텐츠 루트</span><span class="sxs-lookup"><span data-stu-id="30c89-270">Content root</span></span>

<span data-ttu-id="30c89-271">콘텐츠 루트는 앱에서 사용되는 비공개 콘텐츠(예: Razor 파일)의 기본 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-271">The content root is the base path to any private content used by the app, such as its Razor files.</span></span> <span data-ttu-id="30c89-272">기본적으로 콘텐츠 루트는 앱을 호스트하는 실행 파일의 기본 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-272">By default, the content root is the base path for the executable hosting the app.</span></span> <span data-ttu-id="30c89-273">대체 위치는 [호스트를 빌드](#host)할 때 지정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-273">An alternative location can be specified when [building the host](#host).</span></span>

::: moniker range="<= aspnetcore-2.2"

<span data-ttu-id="30c89-274">자세한 내용은 [콘텐츠 루트](xref:fundamentals/host/web-host#content-root)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30c89-274">For more information, see [Content root](xref:fundamentals/host/web-host#content-root).</span></span>

::: moniker-end

::: moniker range="> aspnetcore-2.2"

<span data-ttu-id="30c89-275">자세한 내용은 [콘텐츠 루트](xref:fundamentals/host/generic-host#content-root)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30c89-275">For more information, see [Content root](xref:fundamentals/host/generic-host#content-root).</span></span>

::: moniker-end

## <a name="web-root"></a><span data-ttu-id="30c89-276">웹 루트</span><span class="sxs-lookup"><span data-stu-id="30c89-276">Web root</span></span>

<span data-ttu-id="30c89-277">웹 루트(*webroot*라고도 함)는 CSS, JavaScript 및 이미지 파일과 같은 공용 정적 리소스의 기본 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-277">The web root (also known as *webroot*) is the base path to public, static resources, such as CSS, JavaScript, and image files.</span></span> <span data-ttu-id="30c89-278">기본적으로 정적 파일 미들웨어는 웹 루트 디렉터리(및 하위 디렉터리)에 있는 파일만 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-278">The static files middleware will only serve files from the web root directory (and sub-directories) by default.</span></span> <span data-ttu-id="30c89-279">웹 루트 경로는 *\<content root>/wwwroot*를 기본값으로 지정하지만 [호스트를 빌드](#host)할 때 다른 위치를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-279">The web root path defaults to *\<content root>/wwwroot*, but a different location can be specified when [building the host](#host).</span></span>

<span data-ttu-id="30c89-280">Razor(*.cshtml*) 파일에서 물결표 슬래시 `~/`가 웹 루트를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-280">In Razor (*.cshtml*) files, the tilde-slash `~/` points to the web root.</span></span> <span data-ttu-id="30c89-281">`~/`에서 시작하는 경로를 가상 경로라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c89-281">Paths beginning with `~/` are referred to as virtual paths.</span></span>

<span data-ttu-id="30c89-282">자세한 내용은 [정적 파일](xref:fundamentals/static-files)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30c89-282">For more information, see [Static files](xref:fundamentals/static-files).</span></span>
