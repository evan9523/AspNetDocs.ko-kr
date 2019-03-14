---
title: ASP.NET Core에서 종속성 주입
author: guardrex
description: ASP.NET Core에서 종속성 주입을 구현하는 방법 및 사용 방법에 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 02/25/2019
uid: fundamentals/dependency-injection
ms.openlocfilehash: 5e1522e0819d989a7029c2928c1c33624c1774c7
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57058890"
---
# <a name="dependency-injection-in-aspnet-core"></a><span data-ttu-id="da454-103">ASP.NET Core에서 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="da454-103">Dependency injection in ASP.NET Core</span></span>

<span data-ttu-id="da454-104">작성자: [Steve Smith](https://ardalis.com/), [Scott Addie](https://scottaddie.com) 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="da454-104">By [Steve Smith](https://ardalis.com/), [Scott Addie](https://scottaddie.com), and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="da454-105">ASP.NET Core는 클래스와 해당 종속성 간의 [IoC(Inversion of Control)](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#dependency-inversion)를 실현하는 기술인 DI(종속성 주입) 소프트웨어 디자인 패턴을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-105">ASP.NET Core supports the dependency injection (DI) software design pattern, which is a technique for achieving [Inversion of Control (IoC)](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#dependency-inversion) between classes and their dependencies.</span></span>

<span data-ttu-id="da454-106">MVC 컨트롤러 내의 종속성 주입에 대한 자세한 내용은 <xref:mvc/controllers/dependency-injection>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da454-106">For more information specific to dependency injection within MVC controllers, see <xref:mvc/controllers/dependency-injection>.</span></span>

<span data-ttu-id="da454-107">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/dependency-injection/samples) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="da454-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/dependency-injection/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="overview-of-dependency-injection"></a><span data-ttu-id="da454-108">종속성 주입 개요</span><span class="sxs-lookup"><span data-stu-id="da454-108">Overview of dependency injection</span></span>

<span data-ttu-id="da454-109">‘종속성’은 다른 개체에 필요한 모든 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="da454-109">A *dependency* is any object that another object requires.</span></span> <span data-ttu-id="da454-110">앱의 다른 클래스가 종속된 `MyDependency` 클래스에서 `WriteMessage` 메서드를 사용하는 다음 코드를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="da454-110">Examine the following `MyDependency` class with a `WriteMessage` method that other classes in an app depend upon:</span></span>

```csharp
public class MyDependency
{
    public MyDependency()
    {
    }

    public Task WriteMessage(string message)
    {
        Console.WriteLine(
            $"MyDependency.WriteMessage called. Message: {message}");

        return Task.FromResult(0);
    }
}
```

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="da454-111">`MyDependency` 클래스의 인스턴스를 만들어 클래스에 `WriteMessage` 메서드를 사용할 수 있게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-111">An instance of the `MyDependency` class can be created to make the `WriteMessage` method available to a class.</span></span> <span data-ttu-id="da454-112">`MyDependency` 클래스는 `IndexModel` 클래스의 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="da454-112">The `MyDependency` class is a dependency of the `IndexModel` class:</span></span>

```csharp
public class IndexModel : PageModel
{
    MyDependency _dependency = new MyDependency();

    public async Task OnGetAsync()
    {
        await _dependency.WriteMessage(
            "IndexModel.OnGetAsync created this message.");
    }
}
```

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

<span data-ttu-id="da454-113">`MyDependency` 클래스의 인스턴스를 만들어 클래스에 `WriteMessage` 메서드를 사용할 수 있게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-113">An instance of the `MyDependency` class can be created to make the `WriteMessage` method available to a class.</span></span> <span data-ttu-id="da454-114">`MyDependency` 클래스는 `HomeController` 클래스의 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="da454-114">The `MyDependency` class is a dependency of the `HomeController` class:</span></span>

```csharp
public class HomeController : Controller
{
    MyDependency _dependency = new MyDependency();

    public async Task<IActionResult> Index()
    {
        await _dependency.WriteMessage(
            "HomeController.Index created this message.");

        return View();
    }
}
```

::: moniker-end

<span data-ttu-id="da454-115">이 클래스는 `MyDependency` 인스턴스를 만들고 이 인스턴스에 직접 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-115">The class creates and directly depends on the `MyDependency` instance.</span></span> <span data-ttu-id="da454-116">이전 예제와 같은 코드 종속성은 문제가 있으며 다음과 같은 이유로 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-116">Code dependencies (such as the previous example) are problematic and should be avoided for the following reasons:</span></span>

* <span data-ttu-id="da454-117">`MyDependency`를 다른 구현으로 바꾸려면 클래스를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-117">To replace `MyDependency` with a different implementation, the class must be modified.</span></span>
* <span data-ttu-id="da454-118">`MyDependency`에 종속성이 있으면 클래스에서 종속성을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-118">If `MyDependency` has dependencies, they must be configured by the class.</span></span> <span data-ttu-id="da454-119">여러 클래스가 `MyDependency`에 종속되어 있는 대형 프로젝트에서는 구성 코드가 앱 전체에 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-119">In a large project with multiple classes depending on `MyDependency`, the configuration code becomes scattered across the app.</span></span>
* <span data-ttu-id="da454-120">이 구현은 단위 테스트하기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-120">This implementation is difficult to unit test.</span></span> <span data-ttu-id="da454-121">앱에서 모의 또는 스텁 `MyDependency` 클래스를 사용해야 하지만, 이 방법에서는 가능하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-121">The app should use a mock or stub `MyDependency` class, which isn't possible with this approach.</span></span>

<span data-ttu-id="da454-122">종속성 주입은 다음을 통해 이러한 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-122">Dependency injection addresses these problems through:</span></span>

* <span data-ttu-id="da454-123">종속성 구현을 추상화하는 인터페이스 사용</span><span class="sxs-lookup"><span data-stu-id="da454-123">The use of an interface to abstract the dependency implementation.</span></span>
* <span data-ttu-id="da454-124">서비스 컨테이너에 종속성 등록.</span><span class="sxs-lookup"><span data-stu-id="da454-124">Registration of the dependency in a service container.</span></span> <span data-ttu-id="da454-125">ASP.NET Core는 서비스 컨테이너 [IServiceProvider](/dotnet/api/system.iserviceprovider)를 기본 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-125">ASP.NET Core provides a built-in service container, [IServiceProvider](/dotnet/api/system.iserviceprovider).</span></span> <span data-ttu-id="da454-126">서비스는 앱의 `Startup.ConfigureServices` 메서드에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-126">Services are registered in the app's `Startup.ConfigureServices` method.</span></span>
* <span data-ttu-id="da454-127">서비스를 사용되는 클래스의 생성자에 주입.</span><span class="sxs-lookup"><span data-stu-id="da454-127">*Injection* of the service into the constructor of the class where it's used.</span></span> <span data-ttu-id="da454-128">프레임워크는 종속성의 인스턴스를 만들고 더 이상 필요하지 않으면 삭제하는 작업을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-128">The framework takes on the responsibility of creating an instance of the dependency and disposing of it when it's no longer needed.</span></span>

<span data-ttu-id="da454-129">[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/dependency-injection/samples)에서 `IMyDependency` 인터페이스는 서비스가 앱에 제공하는 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-129">In the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/dependency-injection/samples), the `IMyDependency` interface defines a method that the service provides to the app:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](dependency-injection/samples/2.x/DependencyInjectionSample/Interfaces/IMyDependency.cs?name=snippet1)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](dependency-injection/samples/1.x/DependencyInjectionSample/Interfaces/IMyDependency.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="da454-130">이 인터페이스는 구체적인 형식 `MyDependency`에서 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-130">This interface is implemented by a concrete type, `MyDependency`:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](dependency-injection/samples/2.x/DependencyInjectionSample/Services/MyDependency.cs?name=snippet1)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](dependency-injection/samples/1.x/DependencyInjectionSample/Services/MyDependency.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="da454-131">`MyDependency`는 자신의 생성자에서 [ILogger&lt;TCategoryName&gt;](/dotnet/api/microsoft.extensions.logging.ilogger-1)을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-131">`MyDependency` requests an [ILogger&lt;TCategoryName&gt;](/dotnet/api/microsoft.extensions.logging.ilogger-1) in its constructor.</span></span> <span data-ttu-id="da454-132">종속성 주입을 연결된 방식으로 사용하는 일은 특별한 경우가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="da454-132">It's not unusual to use dependency injection in a chained fashion.</span></span> <span data-ttu-id="da454-133">요청된 각 종속성은 차례로 자체 종속성을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-133">Each requested dependency in turn requests its own dependencies.</span></span> <span data-ttu-id="da454-134">컨테이너는 그래프의 종속성을 해결하고 완전히 해결된 서비스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-134">The container resolves the dependencies in the graph and returns the fully resolved service.</span></span> <span data-ttu-id="da454-135">해결해야 하는 종속성이 모인 집합은 일반적으로 종속성 트리, 종속성 그래프 또는 개체 그래프라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-135">The collective set of dependencies that must be resolved is typically referred to as a *dependency tree*, *dependency graph*, or *object graph*.</span></span>

<span data-ttu-id="da454-136">`IMyDependency` 및 `ILogger<TCategoryName>`는 서비스 컨테이너에 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-136">`IMyDependency` and `ILogger<TCategoryName>` must be registered in the service container.</span></span> <span data-ttu-id="da454-137">`IMyDependency`는 `Startup.ConfigureServices`에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-137">`IMyDependency` is registered in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="da454-138">`ILogger<TCategoryName>`은 로깅 추상화 인프라에서 등록하므로, 프레임워크에서 기본적으로 등록한 [프레임워크 제공 서비스](#framework-provided-services)입니다.</span><span class="sxs-lookup"><span data-stu-id="da454-138">`ILogger<TCategoryName>` is registered by the logging abstractions infrastructure, so it's a [framework-provided service](#framework-provided-services) registered by default by the framework.</span></span>

<span data-ttu-id="da454-139">샘플 앱에서 `IMyDependency` 서비스는 구체적인 형식 `MyDependency`에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-139">In the sample app, the `IMyDependency` service is registered with the concrete type `MyDependency`.</span></span> <span data-ttu-id="da454-140">등록하면 서비스 수명이 단일 요청의 수명으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-140">The registration scopes the service lifetime to the lifetime of a single request.</span></span> <span data-ttu-id="da454-141">[서비스 수명](#service-lifetimes)에 대해서는 이 항목의 뒷부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-141">[Service lifetimes](#service-lifetimes) are described later in this topic.</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](dependency-injection/samples/2.x/DependencyInjectionSample/Startup.cs?name=snippet1&highlight=11)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](dependency-injection/samples/1.x/DependencyInjectionSample/Startup.cs?name=snippet1&highlight=5)]

::: moniker-end

> [!NOTE]
> <span data-ttu-id="da454-142">각 `services.Add{SERVICE_NAME}` 확장 메서드는 서비스를 추가(및 잠재적으로 구성)합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-142">Each `services.Add{SERVICE_NAME}` extension method adds (and potentially configures) services.</span></span> <span data-ttu-id="da454-143">예를 들어 `services.AddMvc()`는 Razor 페이지와 MVC에서 요청하는 서비스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-143">For example, `services.AddMvc()` adds the services Razor Pages and MVC require.</span></span> <span data-ttu-id="da454-144">앱에서 이 규칙을 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-144">We recommended that apps follow this convention.</span></span> <span data-ttu-id="da454-145">확장 메서드를 [Microsoft.Extensions.DependencyInjection](/dotnet/api/microsoft.extensions.dependencyinjection) 네임스페이스에 배치하여 서비스 등록 그룹을 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-145">Place extension methods in the [Microsoft.Extensions.DependencyInjection](/dotnet/api/microsoft.extensions.dependencyinjection) namespace to encapsulate groups of service registrations.</span></span>

<span data-ttu-id="da454-146">서비스의 생성자에 `string`과 같은 기본 형식이 필요한 경우 [구성](xref:fundamentals/configuration/index) 및 [옵션 패턴](xref:fundamentals/configuration/options)을 사용하여 기본 형식을 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-146">If the service's constructor requires a primitive, such as a `string`, the primitive can be injected by using [configuration](xref:fundamentals/configuration/index) or the [options pattern](xref:fundamentals/configuration/options):</span></span>

```csharp
public class MyDependency : IMyDependency
{
    public MyDependency(IConfiguration config)
    {
        var myStringValue = config["MyStringKey"];

        // Use myStringValue
    }

    ...
}
```

<span data-ttu-id="da454-147">서비스의 인스턴스는 서비스가 사용되는 클래스의 생성자를 통해 요청되고 전용 필드에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-147">An instance of the service is requested via the constructor of a class where the service is used and assigned to a private field.</span></span> <span data-ttu-id="da454-148">이 필드는 클래스 전체에서 필요에 따라 서비스에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-148">The field is used to access the service as necessary throughout the class.</span></span>

<span data-ttu-id="da454-149">샘플 앱에서는 `IMyDependency` 인스턴스가 요청되며 이 인스턴스는 서비스의 `WriteMessage` 메서드를 호출하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-149">In the sample app, the `IMyDependency` instance is requested and used to call the service's `WriteMessage` method:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](dependency-injection/samples/2.x/DependencyInjectionSample/Pages/Index.cshtml.cs?name=snippet1&highlight=3,6,13,29-30)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](dependency-injection/samples/1.x/DependencyInjectionSample/Controllers/MyDependencyController.cs?name=snippet1&highlight=3,5-8,13-14)]

::: moniker-end

## <a name="framework-provided-services"></a><span data-ttu-id="da454-150">프레임워크에서 제공한 서비스</span><span class="sxs-lookup"><span data-stu-id="da454-150">Framework-provided services</span></span>

<span data-ttu-id="da454-151">`Startup.ConfigureServices` 메서드는 Entity Framework Core 및 ASP.NET Core MVC와 같은 플랫폼 기능을 비롯해 앱이 사용하는 서비스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-151">The `Startup.ConfigureServices` method is responsible for defining the services the app uses, including platform features, such as Entity Framework Core and ASP.NET Core MVC.</span></span> <span data-ttu-id="da454-152">처음에 `ConfigureServices`에 제공된 `IServiceCollection`에는 정의된 다음과 같은 서비스가 있습니다([호스트 구성 방법](xref:fundamentals/index#host)에 따라).</span><span class="sxs-lookup"><span data-stu-id="da454-152">Initially, the `IServiceCollection` provided to `ConfigureServices` has the following services defined (depending on [how the host was configured](xref:fundamentals/index#host)):</span></span>

| <span data-ttu-id="da454-153">서비스 종류</span><span class="sxs-lookup"><span data-stu-id="da454-153">Service Type</span></span> | <span data-ttu-id="da454-154">수명</span><span class="sxs-lookup"><span data-stu-id="da454-154">Lifetime</span></span> |
| ------------ | -------- |
| [<span data-ttu-id="da454-155">Microsoft.AspNetCore.Hosting.Builder.IApplicationBuilderFactory</span><span class="sxs-lookup"><span data-stu-id="da454-155">Microsoft.AspNetCore.Hosting.Builder.IApplicationBuilderFactory</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.builder.iapplicationbuilderfactory) | <span data-ttu-id="da454-156">Transient</span><span class="sxs-lookup"><span data-stu-id="da454-156">Transient</span></span> |
| [<span data-ttu-id="da454-157">Microsoft.AspNetCore.Hosting.IApplicationLifetime</span><span class="sxs-lookup"><span data-stu-id="da454-157">Microsoft.AspNetCore.Hosting.IApplicationLifetime</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime) | <span data-ttu-id="da454-158">Singleton</span><span class="sxs-lookup"><span data-stu-id="da454-158">Singleton</span></span> |
| [<span data-ttu-id="da454-159">Microsoft.AspNetCore.Hosting.IHostingEnvironment</span><span class="sxs-lookup"><span data-stu-id="da454-159">Microsoft.AspNetCore.Hosting.IHostingEnvironment</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment) | <span data-ttu-id="da454-160">Singleton</span><span class="sxs-lookup"><span data-stu-id="da454-160">Singleton</span></span> |
| [<span data-ttu-id="da454-161">Microsoft.AspNetCore.Hosting.IStartup</span><span class="sxs-lookup"><span data-stu-id="da454-161">Microsoft.AspNetCore.Hosting.IStartup</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.istartup) | <span data-ttu-id="da454-162">Singleton</span><span class="sxs-lookup"><span data-stu-id="da454-162">Singleton</span></span> |
| [<span data-ttu-id="da454-163">Microsoft.AspNetCore.Hosting.IStartupFilter</span><span class="sxs-lookup"><span data-stu-id="da454-163">Microsoft.AspNetCore.Hosting.IStartupFilter</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter) | <span data-ttu-id="da454-164">Transient</span><span class="sxs-lookup"><span data-stu-id="da454-164">Transient</span></span> |
| [<span data-ttu-id="da454-165">Microsoft.AspNetCore.Hosting.Server.IServer</span><span class="sxs-lookup"><span data-stu-id="da454-165">Microsoft.AspNetCore.Hosting.Server.IServer</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.server.iserver) | <span data-ttu-id="da454-166">Singleton</span><span class="sxs-lookup"><span data-stu-id="da454-166">Singleton</span></span> |
| [<span data-ttu-id="da454-167">Microsoft.AspNetCore.Http.IHttpContextFactory</span><span class="sxs-lookup"><span data-stu-id="da454-167">Microsoft.AspNetCore.Http.IHttpContextFactory</span></span>](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextfactory) | <span data-ttu-id="da454-168">Transient</span><span class="sxs-lookup"><span data-stu-id="da454-168">Transient</span></span> |
| [<span data-ttu-id="da454-169">Microsoft.Extensions.Logging.ILogger&lt;T&gt;</span><span class="sxs-lookup"><span data-stu-id="da454-169">Microsoft.Extensions.Logging.ILogger&lt;T&gt;</span></span>](/dotnet/api/microsoft.extensions.logging.ilogger) | <span data-ttu-id="da454-170">Singleton</span><span class="sxs-lookup"><span data-stu-id="da454-170">Singleton</span></span> |
| [<span data-ttu-id="da454-171">Microsoft.Extensions.Logging.ILoggerFactory</span><span class="sxs-lookup"><span data-stu-id="da454-171">Microsoft.Extensions.Logging.ILoggerFactory</span></span>](/dotnet/api/microsoft.extensions.logging.iloggerfactory) | <span data-ttu-id="da454-172">Singleton</span><span class="sxs-lookup"><span data-stu-id="da454-172">Singleton</span></span> |
| [<span data-ttu-id="da454-173">Microsoft.Extensions.ObjectPool.ObjectPoolProvider</span><span class="sxs-lookup"><span data-stu-id="da454-173">Microsoft.Extensions.ObjectPool.ObjectPoolProvider</span></span>](/dotnet/api/microsoft.extensions.objectpool.objectpoolprovider) | <span data-ttu-id="da454-174">Singleton</span><span class="sxs-lookup"><span data-stu-id="da454-174">Singleton</span></span> |
| [<span data-ttu-id="da454-175">Microsoft.Extensions.Options.IConfigureOptions&lt;T&gt;</span><span class="sxs-lookup"><span data-stu-id="da454-175">Microsoft.Extensions.Options.IConfigureOptions&lt;T&gt;</span></span>](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1) | <span data-ttu-id="da454-176">Transient</span><span class="sxs-lookup"><span data-stu-id="da454-176">Transient</span></span> |
| [<span data-ttu-id="da454-177">Microsoft.Extensions.Options.IOptions&lt;T&gt;</span><span class="sxs-lookup"><span data-stu-id="da454-177">Microsoft.Extensions.Options.IOptions&lt;T&gt;</span></span>](/dotnet/api/microsoft.extensions.options.ioptions-1) | <span data-ttu-id="da454-178">Singleton</span><span class="sxs-lookup"><span data-stu-id="da454-178">Singleton</span></span> |
| [<span data-ttu-id="da454-179">System.Diagnostics.DiagnosticSource</span><span class="sxs-lookup"><span data-stu-id="da454-179">System.Diagnostics.DiagnosticSource</span></span>](/dotnet/core/api/system.diagnostics.diagnosticsource) | <span data-ttu-id="da454-180">Singleton</span><span class="sxs-lookup"><span data-stu-id="da454-180">Singleton</span></span> |
| [<span data-ttu-id="da454-181">System.Diagnostics.DiagnosticListener</span><span class="sxs-lookup"><span data-stu-id="da454-181">System.Diagnostics.DiagnosticListener</span></span>](/dotnet/core/api/system.diagnostics.diagnosticlistener) | <span data-ttu-id="da454-182">Singleton</span><span class="sxs-lookup"><span data-stu-id="da454-182">Singleton</span></span> |

<span data-ttu-id="da454-183">서비스 컬렉션 확장 메서드를 사용하여 서비스(및 필요한 경우 해당 종속 서비스)를 등록할 수 있는 경우 단일 `Add{SERVICE_NAME}` 확장 메서드를 사용하여 해당 서비스에 필요한 모든 서비스를 등록하는 것이 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="da454-183">When a service collection extension method is available to register a service (and its dependent services, if required), the convention is to use a single `Add{SERVICE_NAME}` extension method to register all of the services required by that service.</span></span> <span data-ttu-id="da454-184">다음 코드는 확장 메서드 [AddDbContext](/dotnet/api/microsoft.extensions.dependencyinjection.entityframeworkservicecollectionextensions.adddbcontext), [AddIdentity](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionextensions.addidentity) 및 [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc)를 사용하여 컨테이너에 서비스를 추가하는 방법을 보여 주는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="da454-184">The following code is an example of how to add additional services to the container using the extension methods [AddDbContext](/dotnet/api/microsoft.extensions.dependencyinjection.entityframeworkservicecollectionextensions.adddbcontext), [AddIdentity](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionextensions.addidentity), and [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc):</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDbContext<ApplicationDbContext>(options =>
        options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));

    services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();

    services.AddMvc();
}
```

<span data-ttu-id="da454-185">자세한 내용은 API 설명서에서 [ServiceCollection 클래스](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollection)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da454-185">For more information, see the [ServiceCollection Class](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollection) in the API documentation.</span></span>

## <a name="service-lifetimes"></a><span data-ttu-id="da454-186">서비스 수명</span><span class="sxs-lookup"><span data-stu-id="da454-186">Service lifetimes</span></span>

<span data-ttu-id="da454-187">등록된 각 서비스의 수명을 적절히 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-187">Choose an appropriate lifetime for each registered service.</span></span> <span data-ttu-id="da454-188">ASP.NET Core 서비스는 다음 수명을 사용하여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-188">ASP.NET Core services can be configured with the following lifetimes:</span></span>

<span data-ttu-id="da454-189">**Transient**</span><span class="sxs-lookup"><span data-stu-id="da454-189">**Transient**</span></span>

<span data-ttu-id="da454-190">Transient 수명 서비스는 요청할 때마다 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="da454-190">Transient lifetime services are created each time they're requested.</span></span> <span data-ttu-id="da454-191">이 수명은 간단한 상태 비저장 서비스에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-191">This lifetime works best for lightweight, stateless services.</span></span>

<span data-ttu-id="da454-192">**Scoped**</span><span class="sxs-lookup"><span data-stu-id="da454-192">**Scoped**</span></span>

<span data-ttu-id="da454-193">Scoped 수명 서비스는 요청당 한 번만 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="da454-193">Scoped lifetime services are created once per request.</span></span>

> [!WARNING]
> <span data-ttu-id="da454-194">미들웨어에서 범위가 지정된 서비스를 사용하는 경우 `Invoke` 또는 `InvokeAsync` 메서드에 서비스를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-194">When using a scoped service in a middleware, inject the service into the `Invoke` or `InvokeAsync` method.</span></span> <span data-ttu-id="da454-195">생성자 삽입은 서비스가 싱글톤처럼 작동하게 하므로 이러한 방법으로 삽입하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="da454-195">Don't inject via constructor injection because it forces the service to behave like a singleton.</span></span> <span data-ttu-id="da454-196">자세한 내용은 <xref:fundamentals/middleware/index>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da454-196">For more information, see <xref:fundamentals/middleware/index>.</span></span>

<span data-ttu-id="da454-197">**Singleton**</span><span class="sxs-lookup"><span data-stu-id="da454-197">**Singleton**</span></span>

<span data-ttu-id="da454-198">Singleton 수명 서비스는 처음 요청할 때(또는 `ConfigureServices`를 실행하고 서비스 등록에서 인스턴스를 지정하는 경우) 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-198">Singleton lifetime services are created the first time they're requested (or when `ConfigureServices` is run and an instance is specified with the service registration).</span></span> <span data-ttu-id="da454-199">모든 후속 요청에서는 같은 인스턴스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-199">Every subsequent request uses the same instance.</span></span> <span data-ttu-id="da454-200">앱에 singleton 동작이 필요한 경우 서비스 컨테이너에서 서비스 수명을 관리하도록 허용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-200">If the app requires singleton behavior, allowing the service container to manage the service's lifetime is recommended.</span></span> <span data-ttu-id="da454-201">singleton 디자인 패턴을 구현하는 경우 클래스의 개체 수명을 관리하는 사용자 코드를 제공하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="da454-201">Don't implement the singleton design pattern and provide user code to manage the object's lifetime in the class.</span></span>

> [!WARNING]
> <span data-ttu-id="da454-202">범위가 지정된 서비스를 singleton에서 해결하면 위험합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-202">It's dangerous to resolve a scoped service from a singleton.</span></span> <span data-ttu-id="da454-203">이 경우 후속 요청을 처리할 때 서비스가 잘못된 상태일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-203">It may cause the service to have incorrect state when processing subsequent requests.</span></span>

### <a name="constructor-injection-behavior"></a><span data-ttu-id="da454-204">생성자 주입 동작</span><span class="sxs-lookup"><span data-stu-id="da454-204">Constructor injection behavior</span></span>

<span data-ttu-id="da454-205">다음 두 가지 메커니즘으로 서비스를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-205">Services can be resolved by two mechanisms:</span></span>

* `IServiceProvider`
* <span data-ttu-id="da454-206">[ActivatorUtilities](/dotnet/api/microsoft.extensions.dependencyinjection.activatorutilities) &ndash; 종속성 주입 컨테이너에서 서비스 등록 없이 개체를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-206">[ActivatorUtilities](/dotnet/api/microsoft.extensions.dependencyinjection.activatorutilities) &ndash; Permits object creation without service registration in the dependency injection container.</span></span> <span data-ttu-id="da454-207">`ActivatorUtilities`는 태그 도우미, MVC 컨트롤러 및 모델 바인더와 같은 사용자용 추상화에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-207">`ActivatorUtilities` is used with user-facing abstractions, such as Tag Helpers, MVC controllers, and model binders.</span></span>

<span data-ttu-id="da454-208">생성자에는 종속성 주입으로 제공되지 않는 인수를 사용할 수 있지만, 인수에 기본값을 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-208">Constructors can accept arguments that aren't provided by dependency injection, but the arguments must assign default values.</span></span>

<span data-ttu-id="da454-209">`IServiceProvider` 또는 `ActivatorUtilities`로 서비스를 해결하는 경우 생성자 주입에 *public* 생성자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-209">When services are resolved by `IServiceProvider` or `ActivatorUtilities`, constructor injection requires a *public* constructor.</span></span>

<span data-ttu-id="da454-210">`ActivatorUtilities`로 서비스를 해결하는 경우 생성자 주입을 위해서는 적합한 생성자가 하나만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-210">When services are resolved by `ActivatorUtilities`, constructor injection requires that only one applicable constructor exists.</span></span> <span data-ttu-id="da454-211">생성자 오버로드가 지원되지만, 해당 인수가 모두 종속성 주입으로 처리될 수 있는 하나의 오버로드만 존재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-211">Constructor overloads are supported, but only one overload can exist whose arguments can all be fulfilled by dependency injection.</span></span>

## <a name="entity-framework-contexts"></a><span data-ttu-id="da454-212">Entity Framework 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="da454-212">Entity Framework contexts</span></span>

<span data-ttu-id="da454-213">Entity Framework 컨텍스트는 일반적으로 [범위가 지정된 수명](#service-lifetimes)을 사용하여 서비스 컨테이너에 추가됩니다. 이는 웹앱 데이터베이스 작업이 일반적으로 요청에 따라 범위가 지정되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="da454-213">Entity Framework contexts are usually added to the service container using the [scoped lifetime](#service-lifetimes) because web app database operations are normally scoped to the request.</span></span> <span data-ttu-id="da454-214">데이터베이스 컨텍스트를 등록할 때 <xref:Microsoft.Extensions.DependencyInjection.EntityFrameworkServiceCollectionExtensions.AddDbContext*> 오버로드로 수명이 지정되지 않으면 기본 수명이 범위가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-214">The default lifetime is scoped if a lifetime isn't specified by an <xref:Microsoft.Extensions.DependencyInjection.EntityFrameworkServiceCollectionExtensions.AddDbContext*> overload when registering the database context.</span></span> <span data-ttu-id="da454-215">지정된 수명의 서비스는 서비스보다 수명이 짧은 데이터베이스 컨텍스트를 사용해서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-215">Services of a given lifetime shouldn't use a database context with a shorter lifetime than the service.</span></span>

## <a name="lifetime-and-registration-options"></a><span data-ttu-id="da454-216">수명 및 등록 옵션</span><span class="sxs-lookup"><span data-stu-id="da454-216">Lifetime and registration options</span></span>

<span data-ttu-id="da454-217">이러한 수명 및 등록 옵션 간의 차이점을 살펴보려면 작업을 고유한 ID인 `OperationId`가 있는 operation으로 나타내는 다음 인터페이스를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="da454-217">To demonstrate the difference between the lifetime and registration options, consider the following interfaces that represent tasks as an operation with a unique identifier, `OperationId`.</span></span> <span data-ttu-id="da454-218">다음 인터페이스에 대해 작업 서비스의 수명을 구성하는 방법에 따라 컨테이너는 클래스에서 요청할 때 서비스의 같은 인스턴스나 다른 인스턴스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-218">Depending on how the lifetime of an operations service is configured for the following interfaces, the container provides either the same or a different instance of the service when requested by a class:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](dependency-injection/samples/2.x/DependencyInjectionSample/Interfaces/IOperation.cs?name=snippet1)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](dependency-injection/samples/1.x/DependencyInjectionSample/Interfaces/IOperation.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="da454-219">인터페이스는 `Operation` 클래스에 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-219">The interfaces are implemented in the `Operation` class.</span></span> <span data-ttu-id="da454-220">`Operation` 생성자는 제공되지 않는 경우 GUID를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-220">The `Operation` constructor generates a GUID if one isn't supplied:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](dependency-injection/samples/2.x/DependencyInjectionSample/Models/Operation.cs?name=snippet1)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](dependency-injection/samples/1.x/DependencyInjectionSample/Models/Operation.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="da454-221">`OperationService`는 등록되어 각각 다른 `Operation` 형식에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-221">An `OperationService` is registered that depends on each of the other `Operation` types.</span></span> <span data-ttu-id="da454-222">종속성 주입을 통해 `OperationService`를 요청하는 경우에는 종속 서비스의 수명에 따라 각 서비스의 새 인스턴스나 기존 인스턴스를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-222">When `OperationService` is requested via dependency injection, it receives either a new instance of each service or an existing instance based on the lifetime of the dependent service.</span></span>

* <span data-ttu-id="da454-223">요청할 때 임시 서비스가 생성되는 경우 `IOperationTransient` 서비스의 `OperationId`는 `OperationService`의 `OperationId`와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="da454-223">If transient services are created when requested, the `OperationId` of the `IOperationTransient` service is different than the `OperationId` of the `OperationService`.</span></span> <span data-ttu-id="da454-224">`OperationService`는 `IOperationTransient` 클래스의 새 인스턴스를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-224">`OperationService` receives a new instance of the `IOperationTransient` class.</span></span> <span data-ttu-id="da454-225">새 인스턴스는 다른 `OperationId`를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-225">The new instance yields a different `OperationId`.</span></span>
* <span data-ttu-id="da454-226">요청에 따라 범위가 지정된 서비스가 생성되는 경우 `IOperationScoped` 서비스는 요청 내의 `OperationService`와 `OperationId`가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-226">If scoped services are created per request, the `OperationId` of the `IOperationScoped` service is the same as that of `OperationService` within a request.</span></span> <span data-ttu-id="da454-227">전체 요청에서 두 서비스는 다른 `OperationId` 값을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-227">Across requests, both services share a different `OperationId` value.</span></span>
* <span data-ttu-id="da454-228">singleton 및 singleton 인스턴스 서비스가 한 번 생성되어 모든 요청과 모든 서비스에서 사용되는 경우 `OperationId`는 모든 서비스 요청에서 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="da454-228">If singleton and singleton-instance services are created once and used across all requests and all services, the `OperationId` is constant across all service requests.</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](dependency-injection/samples/2.x/DependencyInjectionSample/Services/OperationService.cs?name=snippet1)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](dependency-injection/samples/1.x/DependencyInjectionSample/Services/OperationService.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="da454-229">`Startup.ConfigureServices`에서 각 형식이 명명된 수명에 따라 컨테이너에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-229">In `Startup.ConfigureServices`, each type is added to the container according to its named lifetime:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](dependency-injection/samples/2.x/DependencyInjectionSample/Startup.cs?name=snippet1&highlight=12-15,18)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](dependency-injection/samples/1.x/DependencyInjectionSample/Startup.cs?name=snippet1&highlight=6-9,12)]

::: moniker-end

<span data-ttu-id="da454-230">`IOperationSingletonInstance` 서비스는 알려진 ID가 `Guid.Empty`인 특정 인스턴스를 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="da454-230">The `IOperationSingletonInstance` service is using a specific instance with a known ID of `Guid.Empty`.</span></span> <span data-ttu-id="da454-231">이 형식이 사용 중인지 확실히 알 수 있습니다(해당 GUID가 모두 0).</span><span class="sxs-lookup"><span data-stu-id="da454-231">It's clear when this type is in use (its GUID is all zeroes).</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="da454-232">샘플 앱에서는 개별 요청 내의 개체 수명과 요청 간의 개체 수명을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="da454-232">The sample app demonstrates object lifetimes within and between individual requests.</span></span> <span data-ttu-id="da454-233">샘플 앱의 `IndexModel`은 각 종류의 `IOperation` 형식과 `OperationService`를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-233">The sample app's `IndexModel` requests each kind of `IOperation` type and the `OperationService`.</span></span> <span data-ttu-id="da454-234">그런 다음, 페이지에서는 속성 할당을 통해 페이지 모델 클래스 및 서비스의 `OperationId` 값을 모두 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-234">The page then displays all of the page model class's and service's `OperationId` values through property assignments:</span></span>

[!code-csharp[](dependency-injection/samples/2.x/DependencyInjectionSample/Pages/Index.cshtml.cs?name=snippet1&highlight=7-11,14-18,21-25)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

<span data-ttu-id="da454-235">샘플 앱에서는 개별 요청 내의 개체 수명과 요청 간의 개체 수명을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="da454-235">The sample app demonstrates object lifetimes within and between individual requests.</span></span> <span data-ttu-id="da454-236">샘플 앱에는 각 종류의 `IOperation` 형식과 `OperationService`를 요청하는 `OperationsController`가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-236">The sample app includes an `OperationsController` that requests each kind of `IOperation` type and the `OperationService`.</span></span> <span data-ttu-id="da454-237">`Index` 작업은 서비스의 `OperationId` 값을 표시하기 위해 서비스를 `ViewBag`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-237">The `Index` action sets the services into the `ViewBag` for display of the service's `OperationId` values:</span></span>

[!code-csharp[](dependency-injection/samples/1.x/DependencyInjectionSample/Controllers/OperationsController.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="da454-238">다음 출력은 두 요청의 결과를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="da454-238">Two following output shows the results of two requests:</span></span>

<span data-ttu-id="da454-239">**첫 번째 요청:**:</span><span class="sxs-lookup"><span data-stu-id="da454-239">**First request:**</span></span>

<span data-ttu-id="da454-240">컨트롤러 작업:</span><span class="sxs-lookup"><span data-stu-id="da454-240">Controller operations:</span></span>

<span data-ttu-id="da454-241">Transient: d233e165-f417-469b-a866-1cf1935d2518</span><span class="sxs-lookup"><span data-stu-id="da454-241">Transient: d233e165-f417-469b-a866-1cf1935d2518</span></span>  
<span data-ttu-id="da454-242">Scoped: 5d997e2d-55f5-4a64-8388-51c4e3a1ad19</span><span class="sxs-lookup"><span data-stu-id="da454-242">Scoped: 5d997e2d-55f5-4a64-8388-51c4e3a1ad19</span></span>  
<span data-ttu-id="da454-243">Singleton: 01271bc1-9e31-48e7-8f7c-7261b040ded9</span><span class="sxs-lookup"><span data-stu-id="da454-243">Singleton: 01271bc1-9e31-48e7-8f7c-7261b040ded9</span></span>  
<span data-ttu-id="da454-244">인스턴스: 00000000-0000-0000-0000-000000000000</span><span class="sxs-lookup"><span data-stu-id="da454-244">Instance: 00000000-0000-0000-0000-000000000000</span></span>

<span data-ttu-id="da454-245">`OperationService` 작업:</span><span class="sxs-lookup"><span data-stu-id="da454-245">`OperationService` operations:</span></span>

<span data-ttu-id="da454-246">Transient: c6b049eb-1318-4e31-90f1-eb2dd849ff64</span><span class="sxs-lookup"><span data-stu-id="da454-246">Transient: c6b049eb-1318-4e31-90f1-eb2dd849ff64</span></span>  
<span data-ttu-id="da454-247">Scoped: 5d997e2d-55f5-4a64-8388-51c4e3a1ad19</span><span class="sxs-lookup"><span data-stu-id="da454-247">Scoped: 5d997e2d-55f5-4a64-8388-51c4e3a1ad19</span></span>  
<span data-ttu-id="da454-248">Singleton: 01271bc1-9e31-48e7-8f7c-7261b040ded9</span><span class="sxs-lookup"><span data-stu-id="da454-248">Singleton: 01271bc1-9e31-48e7-8f7c-7261b040ded9</span></span>  
<span data-ttu-id="da454-249">인스턴스: 00000000-0000-0000-0000-000000000000</span><span class="sxs-lookup"><span data-stu-id="da454-249">Instance: 00000000-0000-0000-0000-000000000000</span></span>

<span data-ttu-id="da454-250">**두 번째 요청**:</span><span class="sxs-lookup"><span data-stu-id="da454-250">**Second request:**</span></span>

<span data-ttu-id="da454-251">컨트롤러 작업:</span><span class="sxs-lookup"><span data-stu-id="da454-251">Controller operations:</span></span>

<span data-ttu-id="da454-252">Transient: b63bd538-0a37-4ff1-90ba-081c5138dda0</span><span class="sxs-lookup"><span data-stu-id="da454-252">Transient: b63bd538-0a37-4ff1-90ba-081c5138dda0</span></span>  
<span data-ttu-id="da454-253">Scoped: 31e820c5-4834-4d22-83fc-a60118acb9f4</span><span class="sxs-lookup"><span data-stu-id="da454-253">Scoped: 31e820c5-4834-4d22-83fc-a60118acb9f4</span></span>  
<span data-ttu-id="da454-254">Singleton: 01271bc1-9e31-48e7-8f7c-7261b040ded9</span><span class="sxs-lookup"><span data-stu-id="da454-254">Singleton: 01271bc1-9e31-48e7-8f7c-7261b040ded9</span></span>  
<span data-ttu-id="da454-255">인스턴스: 00000000-0000-0000-0000-000000000000</span><span class="sxs-lookup"><span data-stu-id="da454-255">Instance: 00000000-0000-0000-0000-000000000000</span></span>

<span data-ttu-id="da454-256">`OperationService` 작업:</span><span class="sxs-lookup"><span data-stu-id="da454-256">`OperationService` operations:</span></span>

<span data-ttu-id="da454-257">Transient: c4cbacb8-36a2-436d-81c8-8c1b78808aaf</span><span class="sxs-lookup"><span data-stu-id="da454-257">Transient: c4cbacb8-36a2-436d-81c8-8c1b78808aaf</span></span>  
<span data-ttu-id="da454-258">Scoped: 31e820c5-4834-4d22-83fc-a60118acb9f4</span><span class="sxs-lookup"><span data-stu-id="da454-258">Scoped: 31e820c5-4834-4d22-83fc-a60118acb9f4</span></span>  
<span data-ttu-id="da454-259">Singleton: 01271bc1-9e31-48e7-8f7c-7261b040ded9</span><span class="sxs-lookup"><span data-stu-id="da454-259">Singleton: 01271bc1-9e31-48e7-8f7c-7261b040ded9</span></span>  
<span data-ttu-id="da454-260">인스턴스: 00000000-0000-0000-0000-000000000000</span><span class="sxs-lookup"><span data-stu-id="da454-260">Instance: 00000000-0000-0000-0000-000000000000</span></span>

<span data-ttu-id="da454-261">어떤 `OperationId` 값이 요청 내 및 요청 간 달라지는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-261">Observe which of the `OperationId` values vary within a request and between requests:</span></span>

* <span data-ttu-id="da454-262">*Transient* 개체는 항상 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="da454-262">*Transient* objects are always different.</span></span> <span data-ttu-id="da454-263">첫 번째와 두 번째 요청 모두의 임시 `OperationId` 값은 두 `OperationService` 작업과 요청 간에 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="da454-263">Note that the transient `OperationId` value for both the first and second requests are different for both `OperationService` operations and across requests.</span></span> <span data-ttu-id="da454-264">각 서비스와 요청에 새 인스턴스가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-264">A new instance is provided to each service and request.</span></span>
* <span data-ttu-id="da454-265">*Scoped* 개체는 요청 내에서는 동일하지만 요청 간에는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="da454-265">*Scoped* objects are the same within a request but different across requests.</span></span>
* <span data-ttu-id="da454-266">*Singleton* 개체는 `ConfigureServices`에 `Operation` 인스턴스 제공 여부와 관계없이 모든 개체 및 모든 요청에 대해 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-266">*Singleton* objects are the same for every object and every request regardless of whether an `Operation` instance is provided in `ConfigureServices`.</span></span>

## <a name="call-services-from-main"></a><span data-ttu-id="da454-267">Main에서 서비스 호출</span><span class="sxs-lookup"><span data-stu-id="da454-267">Call services from main</span></span>

<span data-ttu-id="da454-268">[IServiceScopeFactory.CreateScope](/dotnet/api/microsoft.extensions.dependencyinjection.iservicescopefactory.createscope)와 함께 [IServiceScope](/dotnet/api/microsoft.extensions.dependencyinjection.iservicescope)를 만들어 앱 범위 내에서 범위가 지정된 서비스를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-268">Create an [IServiceScope](/dotnet/api/microsoft.extensions.dependencyinjection.iservicescope) with [IServiceScopeFactory.CreateScope](/dotnet/api/microsoft.extensions.dependencyinjection.iservicescopefactory.createscope) to resolve a scoped service within the app's scope.</span></span> <span data-ttu-id="da454-269">이 방법은 시작 시 범위가 지정된 서비스에 액세스하여 초기화 작업을 실행하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-269">This approach is useful to access a scoped service at startup to run initialization tasks.</span></span> <span data-ttu-id="da454-270">다음 예제에서는 `Program.Main`에서 `MyScopedService`에 대한 컨텍스트를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="da454-270">The following example shows how to obtain a context for the `MyScopedService` in `Program.Main`:</span></span>

```csharp
public static void Main(string[] args)
{
    var host = CreateWebHostBuilder(args).Build();

    using (var serviceScope = host.Services.CreateScope())
    {
        var services = serviceScope.ServiceProvider;

        try
        {
            var serviceContext = services.GetRequiredService<MyScopedService>();
            // Use the context here
        }
        catch (Exception ex)
        {
            var logger = services.GetRequiredService<ILogger<Program>>();
            logger.LogError(ex, "An error occurred.");
        }
    }

    host.Run();
}
```

## <a name="scope-validation"></a><span data-ttu-id="da454-271">범위 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="da454-271">Scope validation</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="da454-272">앱이 개발 환경에서 실행 중인 경우 기본 서비스 공급자가 다음을 확인하는 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-272">When the app is running in the Development environment, the default service provider performs checks to verify that:</span></span>

* <span data-ttu-id="da454-273">범위가 지정된 서비스는 루트 서비스 공급자를 통해 간접적 또는 직접으로 확인되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-273">Scoped services aren't directly or indirectly resolved from the root service provider.</span></span>
* <span data-ttu-id="da454-274">범위가 지정된 서비스는 직접 또는 간접적으로 싱글톤에 삽입되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-274">Scoped services aren't directly or indirectly injected into singletons.</span></span>

::: moniker-end

<span data-ttu-id="da454-275">루트 서비스 공급자는 [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider)를 호출할 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="da454-275">The root service provider is created when [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider) is called.</span></span> <span data-ttu-id="da454-276">루트 서비스 공급자의 수명은 공급자가 앱과 함께 시작되고 앱이 종료될 때 삭제되는 앱/서버의 수명에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-276">The root service provider's lifetime corresponds to the app/server's lifetime when the provider starts with the app and is disposed when the app shuts down.</span></span>

<span data-ttu-id="da454-277">범위가 지정된 서비스는 서비스를 만든 컨테이너에 의해 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-277">Scoped services are disposed by the container that created them.</span></span> <span data-ttu-id="da454-278">범위가 지정된 서비스가 루트 컨테이너에서 만들어지는 경우 서비스의 수명은 효과적으로 싱글톤으로 승격됩니다. 해당 서비스는 앱/서버가 종료될 때 루트 컨테이너에 의해서만 삭제되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="da454-278">If a scoped service is created in the root container, the service's lifetime is effectively promoted to singleton because it's only disposed by the root container when app/server is shut down.</span></span> <span data-ttu-id="da454-279">서비스 범위의 유효성 검사는 `BuildServiceProvider`가 호출될 경우 이러한 상황을 catch합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-279">Validating service scopes catches these situations when `BuildServiceProvider` is called.</span></span>

<span data-ttu-id="da454-280">자세한 내용은 <xref:fundamentals/host/web-host#scope-validation>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da454-280">For more information, see <xref:fundamentals/host/web-host#scope-validation>.</span></span>

## <a name="request-services"></a><span data-ttu-id="da454-281">요청 서비스</span><span class="sxs-lookup"><span data-stu-id="da454-281">Request Services</span></span>

<span data-ttu-id="da454-282">`HttpContext`의 ASP.NET Core 요청 내에서 사용할 수 있는 서비스는 [HttpContext.RequestServices](/dotnet/api/microsoft.aspnetcore.http.httpcontext.requestservices) 컬렉션을 통해 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-282">The services available within an ASP.NET Core request from `HttpContext` are exposed through the [HttpContext.RequestServices](/dotnet/api/microsoft.aspnetcore.http.httpcontext.requestservices) collection.</span></span>

<span data-ttu-id="da454-283">요청 서비스는 앱의 일부로 구성 및 요청된 서비스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="da454-283">Request Services represent the services configured and requested as part of the app.</span></span> <span data-ttu-id="da454-284">개체가 종속성을 지정한 경우에는 `ApplicationServices`가 아닌 `RequestServices`에 있는 형식으로 충족됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-284">When the objects specify dependencies, these are satisfied by the types found in `RequestServices`, not `ApplicationServices`.</span></span>

<span data-ttu-id="da454-285">일반적으로 앱은 이러한 속성을 직접 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-285">Generally, the app shouldn't use these properties directly.</span></span> <span data-ttu-id="da454-286">대신 클래스 생성자를 통해 클래스에 필요한 형식을 요청하고 프레임워크가 종속성을 주입하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-286">Instead, request the types that classes require via class constructors and allow the framework inject the dependencies.</span></span> <span data-ttu-id="da454-287">테스트하기 쉬운 클래스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-287">This yields classes that are easier to test.</span></span>

> [!NOTE]
> <span data-ttu-id="da454-288">`RequestServices` 컬렉션에 액세스하는 것보다 생성자 매개 변수로 종속성을 요청하는 것을 선호합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-288">Prefer requesting dependencies as constructor parameters to accessing the `RequestServices` collection.</span></span>

## <a name="design-services-for-dependency-injection"></a><span data-ttu-id="da454-289">종속성 주입을 위한 서비스 디자인</span><span class="sxs-lookup"><span data-stu-id="da454-289">Design services for dependency injection</span></span>

<span data-ttu-id="da454-290">모범 사례는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-290">Best practices are to:</span></span>

* <span data-ttu-id="da454-291">종속성 주입을 사용하여 종속성을 가져오도록 서비스를 디자인합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-291">Design services to use dependency injection to obtain their dependencies.</span></span>
* <span data-ttu-id="da454-292">상태 저장 정적 메서드 호출을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="da454-292">Avoid stateful, static method calls.</span></span>
* <span data-ttu-id="da454-293">서비스 내의 종속 클래스를 직접 인스턴스화하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="da454-293">Avoid direct instantiation of dependent classes within services.</span></span> <span data-ttu-id="da454-294">직접 인스턴스화는 코드를 특정 구현에 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-294">Direct instantiation couples the code to a particular implementation.</span></span>
* <span data-ttu-id="da454-295">앱 클래스를 작고 잘 구성되고 쉽게 테스트할 수 있도록 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da454-295">Make app classes small, well-factored, and easily tested.</span></span>

<span data-ttu-id="da454-296">클래스에 주입된 종속성이 너무 많아 보이면 일반적으로 클래스에 역할이 너무 많고 [SRP(단일 책임 원칙)](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#single-responsibility)를 위반하는 것일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-296">If a class seems to have too many injected dependencies, this is generally a sign that the class has too many responsibilities and is violating the [Single Responsibility Principle (SRP)](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#single-responsibility).</span></span> <span data-ttu-id="da454-297">해당 책임 몇 가지를 새로운 클래스로 이동하여 클래스를 리팩터링해 보세요.</span><span class="sxs-lookup"><span data-stu-id="da454-297">Attempt to refactor the class by moving some of its responsibilities into a new class.</span></span> <span data-ttu-id="da454-298">Razor 페이지의 페이지 모델 클래스 및 MVC 컨트롤러 클래스는 UI 고려 사항에 집중해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-298">Keep in mind that Razor Pages page model classes and MVC controller classes should focus on UI concerns.</span></span> <span data-ttu-id="da454-299">비즈니스 규칙 및 데이터 액세스 구현 세부 정보는 이러한 [별도의 문제](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#separation-of-concerns)에 적합한 클래스에 유지되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-299">Business rules and data access implementation details should be kept in classes appropriate to these [separate concerns](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#separation-of-concerns).</span></span>

### <a name="disposal-of-services"></a><span data-ttu-id="da454-300">서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="da454-300">Disposal of services</span></span>

<span data-ttu-id="da454-301">컨테이너는 만든 `IDisposable` 형식에 대해 `Dispose`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-301">The container calls `Dispose` for the `IDisposable` types it creates.</span></span> <span data-ttu-id="da454-302">인스턴스가 사용자 코드로 컨테이너에 추가된 경우에는 자동으로 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-302">If an instance is added to the container by user code, it isn't disposed automatically.</span></span>

```csharp
// Services that implement IDisposable:
public class Service1 : IDisposable {}
public class Service2 : IDisposable {}
public class Service3 : IDisposable {}

public interface ISomeService {}
public class SomeServiceImplementation : ISomeService, IDisposable {}

public void ConfigureServices(IServiceCollection services)
{
    // The container creates the following instances and disposes them automatically:
    services.AddScoped<Service1>();
    services.AddSingleton<Service2>();
    services.AddSingleton<ISomeService>(sp => new SomeServiceImplementation());

    // The container doesn't create the following instances, so it doesn't dispose of
    // the instances automatically:
    services.AddSingleton<Service3>(new Service3());
    services.AddSingleton(new Service3());
}
```

::: moniker range="= aspnetcore-1.0"

> [!NOTE]
> <span data-ttu-id="da454-303">ASP.NET Core 1.0에서 컨테이너는 만들지 않은 개체를 포함한 모든 `IDisposable` 개체에서 dispose를 호출했습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-303">In ASP.NET Core 1.0, the container calls dispose on *all* `IDisposable` objects, including those it didn't create.</span></span>

::: moniker-end

## <a name="default-service-container-replacement"></a><span data-ttu-id="da454-304">기본 서비스 컨테이너 바꾸기</span><span class="sxs-lookup"><span data-stu-id="da454-304">Default service container replacement</span></span>

<span data-ttu-id="da454-305">기본 제공 서비스 컨테이너는 프레임워크의 조건 및 대부분의 소비자 앱을 제공하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-305">The built-in service container is meant to serve the needs of the framework and most consumer apps.</span></span> <span data-ttu-id="da454-306">지원하지 않는 특정 기능이 필요하지 않는 한 기본 제공 컨테이너를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-306">We recommend using the built-in container unless you need a specific feature that it doesn't support.</span></span> <span data-ttu-id="da454-307">기본 제공 컨테이너에서 찾을 수 없는 타사 컨테이너에서 지원되는 일부 기능:</span><span class="sxs-lookup"><span data-stu-id="da454-307">Some of the features supported in 3rd party containers not found in the built-in container:</span></span>

* <span data-ttu-id="da454-308">속성 삽입</span><span class="sxs-lookup"><span data-stu-id="da454-308">Property injection</span></span>
* <span data-ttu-id="da454-309">이름을 기준으로 삽입</span><span class="sxs-lookup"><span data-stu-id="da454-309">Injection based on name</span></span>
* <span data-ttu-id="da454-310">자식 컨테이너</span><span class="sxs-lookup"><span data-stu-id="da454-310">Child containers</span></span>
* <span data-ttu-id="da454-311">사용자 지정 수명 관리</span><span class="sxs-lookup"><span data-stu-id="da454-311">Custom lifetime management</span></span>
* <span data-ttu-id="da454-312">초기화 지연에 대한 `Func<T>` 지원</span><span class="sxs-lookup"><span data-stu-id="da454-312">`Func<T>` support for lazy initialization</span></span>

<span data-ttu-id="da454-313">어댑터를 지원하는 일부 컨테이너의 목록은 [종속성 주입 readme.md 파일](https://github.com/aspnet/Extensions/tree/master/src/DependencyInjection)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da454-313">See the [Dependency Injection readme.md file](https://github.com/aspnet/Extensions/tree/master/src/DependencyInjection) for a list of some of the containers that support adapters.</span></span>

<span data-ttu-id="da454-314">다음 샘플은 기본 제공 컨테이너를 [Autofac](https://autofac.org/)로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-314">The following sample replaces the built-in container with [Autofac](https://autofac.org/):</span></span>

* <span data-ttu-id="da454-315">적절한 컨테이너 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-315">Install the appropriate container package(s):</span></span>

  * [<span data-ttu-id="da454-316">Autofac</span><span class="sxs-lookup"><span data-stu-id="da454-316">Autofac</span></span>](https://www.nuget.org/packages/Autofac/)
  * [<span data-ttu-id="da454-317">Autofac.Extensions.DependencyInjection</span><span class="sxs-lookup"><span data-stu-id="da454-317">Autofac.Extensions.DependencyInjection</span></span>](https://www.nuget.org/packages/Autofac.Extensions.DependencyInjection/)

* <span data-ttu-id="da454-318">컨테이너를 `Startup.ConfigureServices`에 구성하고 `IServiceProvider`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-318">Configure the container in `Startup.ConfigureServices` and return an `IServiceProvider`:</span></span>

    ```csharp
    public IServiceProvider ConfigureServices(IServiceCollection services)
    {
        services.AddMvc();
        // Add other framework services

        // Add Autofac
        var containerBuilder = new ContainerBuilder();
        containerBuilder.RegisterModule<DefaultModule>();
        containerBuilder.Populate(services);
        var container = containerBuilder.Build();
        return new AutofacServiceProvider(container);
    }
    ```

    <span data-ttu-id="da454-319">타사 컨테이너를 사용하려면 `Startup.ConfigureServices`가 `IServiceProvider`를 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-319">To use a 3rd party container, `Startup.ConfigureServices` must return `IServiceProvider`.</span></span>

* <span data-ttu-id="da454-320">`DefaultModule`에 Autofac을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-320">Configure Autofac in `DefaultModule`:</span></span>

    ```csharp
    public class DefaultModule : Module
    {
        protected override void Load(ContainerBuilder builder)
        {
            builder.RegisterType<CharacterRepository>().As<ICharacterRepository>();
        }
    }
    ```

<span data-ttu-id="da454-321">런타임 시 형식을 확인하고 종속성을 주입하는 데 Autofac이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-321">At runtime, Autofac is used to resolve types and inject dependencies.</span></span> <span data-ttu-id="da454-322">ASP.NET Core에서 Autofac을 사용하는 방법에 대한 자세한 내용은 [Autofac documentation](https://docs.autofac.org/en/latest/integration/aspnetcore.html)(Autofac 설명서)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da454-322">To learn more about using Autofac with ASP.NET Core, see the [Autofac documentation](https://docs.autofac.org/en/latest/integration/aspnetcore.html).</span></span>

### <a name="thread-safety"></a><span data-ttu-id="da454-323">스레드로부터의 안전성</span><span class="sxs-lookup"><span data-stu-id="da454-323">Thread safety</span></span>

<span data-ttu-id="da454-324">Singleton 서비스는 스레드로부터 안전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-324">Singleton services need to be thread safe.</span></span> <span data-ttu-id="da454-325">Singleton 서비스가 Transient 서비스에 대한 종속성을 갖는 경우 Transient 서비스는 Singleton에서 사용되는 방식에 따라 스레드로부터 안전해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-325">If a singleton service has a dependency on a transient service, the transient service may also need to be thread safe depending how it's used by the singleton.</span></span>

<span data-ttu-id="da454-326">[AddSingleton&lt;TService&gt;(IServiceCollection, Func&lt;IServiceProvider,TService&gt;)](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectionserviceextensions.addsingleton#Microsoft_Extensions_DependencyInjection_ServiceCollectionServiceExtensions_AddSingleton__1_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_Func_System_IServiceProvider___0__)의 두 번째 인수와 같은 단일 서비스의 팩터리 메서드는 스레드로부터 안전할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-326">The factory method of single service, such as the second argument to [AddSingleton&lt;TService&gt;(IServiceCollection, Func&lt;IServiceProvider,TService&gt;)](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectionserviceextensions.addsingleton#Microsoft_Extensions_DependencyInjection_ServiceCollectionServiceExtensions_AddSingleton__1_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_Func_System_IServiceProvider___0__), doesn't need to be thread-safe.</span></span> <span data-ttu-id="da454-327">형식(`static`) 생성자와 같이 이 메서드는 단일 스레드에서 한 번만 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="da454-327">Like a type (`static`) constructor, it's guaranteed to be called once by a single thread.</span></span>

## <a name="recommendations"></a><span data-ttu-id="da454-328">권장 사항</span><span class="sxs-lookup"><span data-stu-id="da454-328">Recommendations</span></span>

* <span data-ttu-id="da454-329">`async/await` 및 `Task` 기반 서비스 해결은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-329">`async/await` and `Task` based service resolution is not supported.</span></span> <span data-ttu-id="da454-330">C#은 비동기 생성자를 지원하지 않으므로, 서비스를 동기식으로 해결한 후 비동기 메서드를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-330">C# does not support asynchronous constructors, therefore the recommended pattern is to use asynchronous methods after synchronously resolving the service.</span></span>

* <span data-ttu-id="da454-331">데이터 및 구성을 서비스 컨테이너에 직접 저장하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="da454-331">Avoid storing data and configuration directly in the service container.</span></span> <span data-ttu-id="da454-332">예를 들어 사용자의 쇼핑 카트는 일반적으로 서비스 컨테이너에 추가하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-332">For example, a user's shopping cart shouldn't typically be added to the service container.</span></span> <span data-ttu-id="da454-333">구성은 [옵션 패턴](xref:fundamentals/configuration/options)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-333">Configuration should use the [options pattern](xref:fundamentals/configuration/options).</span></span> <span data-ttu-id="da454-334">마찬가지로 다른 일부 개체에 대한 액세스를 허용하기 위해서만 존재하는 “데이터 보유자” 개체를 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="da454-334">Similarly, avoid "data holder" objects that only exist to allow access to some other object.</span></span> <span data-ttu-id="da454-335">DI를 통해 실제 항목을 요청하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-335">It's better to request the actual item via DI.</span></span>

* <span data-ttu-id="da454-336">서비스에 정적으로 액세스(예를 들어 다른 곳에 사용하기 위해 [IApplicationBuilder.ApplicationServices](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.applicationservices)를 정적으로 입력)하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="da454-336">Avoid static access to services (for example, statically-typing [IApplicationBuilder.ApplicationServices](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.applicationservices) for use elsewhere).</span></span>

* <span data-ttu-id="da454-337">‘서비스 로케이터 패턴’을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="da454-337">Avoid using the *service locator pattern*.</span></span> <span data-ttu-id="da454-338">예를 들어 DI를 대신 사용할 수 있는 경우 서비스 인스턴스를 가져오기 위해 <xref:System.IServiceProvider.GetService*>를 호출하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="da454-338">For example, don't invoke <xref:System.IServiceProvider.GetService*> to obtain a service instance when you can use DI instead.</span></span> <span data-ttu-id="da454-339">피해야 하는 또 다른 서비스 로케이터 변형은 런타임에 종속성을 해결하는 팩터리를 주입하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="da454-339">Another service locator variation to avoid is injecting a factory that resolves dependencies at runtime.</span></span> <span data-ttu-id="da454-340">이러한 두 가지 방법 모두 [제어 반전](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#dependency-inversion) 전략을 혼합합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-340">Both of these practices mix [Inversion of Control](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#dependency-inversion) strategies.</span></span>

* <span data-ttu-id="da454-341">`HttpContext`(예: [IHttpContextAccessor.HttpContext](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextaccessor.httpcontext))에 정적으로 액세스하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="da454-341">Avoid static access to `HttpContext` (for example, [IHttpContextAccessor.HttpContext](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextaccessor.httpcontext)).</span></span>

<span data-ttu-id="da454-342">모든 권장 사항과 마찬가지로, 하나를 무시해야 하는 상황이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-342">Like all sets of recommendations, you may encounter situations where ignoring a recommendation is required.</span></span> <span data-ttu-id="da454-343">예외는 드물게 발생하며, 대부분 프레임워크 자체 내에서 특별한 경우에만 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="da454-343">Exceptions are rare&mdash;mostly special cases within the framework itself.</span></span>

<span data-ttu-id="da454-344">DI는 정적/전역 개체 액세스 패턴의 ‘대안’입니다.</span><span class="sxs-lookup"><span data-stu-id="da454-344">DI is an *alternative* to static/global object access patterns.</span></span> <span data-ttu-id="da454-345">고정 개체 액세스와 함께 사용할 경우 DI의 장점을 실현할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da454-345">You may not be able to realize the benefits of DI if you mix it with static object access.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="da454-346">추가 자료</span><span class="sxs-lookup"><span data-stu-id="da454-346">Additional resources</span></span>

* <xref:mvc/views/dependency-injection>
* <xref:mvc/controllers/dependency-injection>
* <xref:security/authorization/dependencyinjection>
* <xref:fundamentals/startup>
* <xref:fundamentals/middleware/extensibility>
* [<span data-ttu-id="da454-347">종속성 주입으로 ASP.NET Core에 정리 코드 작성(MSDN)</span><span class="sxs-lookup"><span data-stu-id="da454-347">Writing Clean Code in ASP.NET Core with Dependency Injection (MSDN)</span></span>](https://msdn.microsoft.com/magazine/mt703433.aspx)
* <span data-ttu-id="da454-348">[Container-Managed Application Design, Prelude: Where does the Container Belong?](https://blogs.msdn.microsoft.com/nblumhardt/2008/12/26/container-managed-application-design-prelude-where-does-the-container-belong/)(컨테이너 관리형 애플리케이션 디자인, 서막: 컨테이너는 어디에 속하는가?)</span><span class="sxs-lookup"><span data-stu-id="da454-348">[Container-Managed Application Design, Prelude: Where does the Container Belong?](https://blogs.msdn.microsoft.com/nblumhardt/2008/12/26/container-managed-application-design-prelude-where-does-the-container-belong/)</span></span>
* [<span data-ttu-id="da454-349">명시적 종속성 원칙</span><span class="sxs-lookup"><span data-stu-id="da454-349">Explicit Dependencies Principle</span></span>](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies)
* [<span data-ttu-id="da454-350">Inversion of Control 컨테이너 및 종속성 주입 패턴(Martin Fowler)</span><span class="sxs-lookup"><span data-stu-id="da454-350">Inversion of Control Containers and the Dependency Injection Pattern (Martin Fowler)</span></span>](https://www.martinfowler.com/articles/injection.html)
* <span data-ttu-id="da454-351">[How to register a service with multiple interfaces in ASP.NET Core DI](https://andrewlock.net/how-to-register-a-service-with-multiple-interfaces-for-in-asp-net-core-di/)(ASP.NET Core DI의 여러 인터페이스를 사용하여 서비스를 등록하는 방법)</span><span class="sxs-lookup"><span data-stu-id="da454-351">[How to register a service with multiple interfaces in ASP.NET Core DI](https://andrewlock.net/how-to-register-a-service-with-multiple-interfaces-for-in-asp-net-core-di/)</span></span>
