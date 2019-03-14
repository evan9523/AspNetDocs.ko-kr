---
title: ASP.NET Core 모듈
author: guardrex
description: ASP.NET Core 앱을 호스팅하기 위해 ASP.NET Core 모듈을 구성하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 02/26/2019
uid: host-and-deploy/aspnet-core-module
ms.openlocfilehash: 302cfb00127c223aeb5e51e4d0a9ef3cb69b10eb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029890"
---
# <a name="aspnet-core-module"></a><span data-ttu-id="7aadf-103">ASP.NET Core 모듈</span><span class="sxs-lookup"><span data-stu-id="7aadf-103">ASP.NET Core Module</span></span>

<span data-ttu-id="7aadf-104">작성자: [Tom Dykstra](https://github.com/tdykstra), [Rick Strahl](https://github.com/RickStrahl), [Chris Ross](https://github.com/Tratcher), [Rick Anderson](https://twitter.com/RickAndMSFT), [Sourabh Shirhatti](https://twitter.com/sshirhatti), [Justin Kotalik](https://github.com/jkotalik) 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="7aadf-104">By [Tom Dykstra](https://github.com/tdykstra), [Rick Strahl](https://github.com/RickStrahl), [Chris Ross](https://github.com/Tratcher), [Rick Anderson](https://twitter.com/RickAndMSFT), [Sourabh Shirhatti](https://twitter.com/sshirhatti), [Justin Kotalik](https://github.com/jkotalik), and [Luke Latham](https://github.com/guardrex)</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="7aadf-105">ASP.NET Core 모듈은 다음을 위해 IIS 파이프라인에 연결되는 네이티브 IIS 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-105">The ASP.NET Core Module is a native IIS module that plugs into the IIS pipeline to either:</span></span>

* <span data-ttu-id="7aadf-106">IIS 작업자 프로세스(`w3wp.exe`) 내부에 ASP.NET Core 앱을 호스트하며 [In-Process 호스팅 모델](#in-process-hosting-model)이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-106">Host an ASP.NET Core app inside of the IIS worker process (`w3wp.exe`), called the [in-process hosting model](#in-process-hosting-model).</span></span>
* <span data-ttu-id="7aadf-107">[Kestrel 서버](xref:fundamentals/servers/kestrel)를 실행하는 백 엔드 ASP.NET Core 앱으로 웹 요청을 전달하며 [Out-of-Process 호스팅 모델](#out-of-process-hosting-model)이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-107">Forward web requests to a backend ASP.NET Core app running the [Kestrel server](xref:fundamentals/servers/kestrel), called the [out-of-process hosting model](#out-of-process-hosting-model).</span></span>

<span data-ttu-id="7aadf-108">지원되는 Windows 버전:</span><span class="sxs-lookup"><span data-stu-id="7aadf-108">Supported Windows versions:</span></span>

* <span data-ttu-id="7aadf-109">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="7aadf-109">Windows 7 or later</span></span>
* <span data-ttu-id="7aadf-110">Windows Server 2008 R2 이상</span><span class="sxs-lookup"><span data-stu-id="7aadf-110">Windows Server 2008 R2 or later</span></span>

<span data-ttu-id="7aadf-111">In Process를 호스트하는 경우 모듈에서는 IIS HTTP Server(`IISHttpServer`)라는 IIS용 In Process 서버 구현을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-111">When hosting in-process, the module uses an in-process server implementation for IIS, called IIS HTTP Server (`IISHttpServer`).</span></span>

<span data-ttu-id="7aadf-112">Out-of-Process로 호스트하는 경우 모듈은 Kestrel에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-112">When hosting out-of-process, the module only works with Kestrel.</span></span> <span data-ttu-id="7aadf-113">모듈이 [HTTP.sys](xref:fundamentals/servers/httpsys)와 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-113">The module is incompatible with [HTTP.sys](xref:fundamentals/servers/httpsys).</span></span>

## <a name="hosting-models"></a><span data-ttu-id="7aadf-114">호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="7aadf-114">Hosting models</span></span>

### <a name="in-process-hosting-model"></a><span data-ttu-id="7aadf-115">In-Process 호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="7aadf-115">In-process hosting model</span></span>

<span data-ttu-id="7aadf-116">In-Process 호스팅용 앱을 구성하려면 `<AspNetCoreHostingModel>` 속성을 `InProcess` 값의 앱 프로젝트 파일에 추가합니다(Out-of-Process 호스팅은 `OutOfProcess`로 설정됨).</span><span class="sxs-lookup"><span data-stu-id="7aadf-116">To configure an app for in-process hosting, add the `<AspNetCoreHostingModel>` property to the app's project file with a value of `InProcess` (out-of-process hosting is set with `OutOfProcess`):</span></span>

```xml
<PropertyGroup>
  <AspNetCoreHostingModel>InProcess</AspNetCoreHostingModel>
</PropertyGroup>
```

<span data-ttu-id="7aadf-117">In-process 호스팅 모델은 .NET Framework를 대상으로 하는 ASP.NET Core 앱을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-117">The in-process hosting model isn't supported for ASP.NET Core apps that target the .NET Framework.</span></span>

<span data-ttu-id="7aadf-118">파일에 `<AspNetCoreHostingModel>` 속성이 없으면 기본값은 `OutOfProcess`입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-118">If the `<AspNetCoreHostingModel>` property isn't present in the file, the default value is `OutOfProcess`.</span></span>

<span data-ttu-id="7aadf-119">다음 특성은 In-Process로 호스팅할 때 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-119">The following characteristics apply when hosting in-process:</span></span>

* <span data-ttu-id="7aadf-120">IIS HTTP 서버(`IISHttpServer`)는 [Kestrel](xref:fundamentals/servers/kestrel) 서버 대신 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-120">IIS HTTP Server (`IISHttpServer`) is used instead of [Kestrel](xref:fundamentals/servers/kestrel) server.</span></span> <span data-ttu-id="7aadf-121">In Process의 경우 [CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host)는 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIIS*>를 호출하여 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-121">For in-process, [CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host) calls <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIIS*> to:</span></span>

  * <span data-ttu-id="7aadf-122">`IISHttpServer`를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-122">Register the `IISHttpServer`.</span></span>
  * <span data-ttu-id="7aadf-123">ASP.NET Core 모듈 뒤에서 실행될 때 서버가 수신 대기해야 하는 포트 및 기본 경로를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-123">Configure the port and base path the server should listen on when running behind the ASP.NET Core Module.</span></span>
  * <span data-ttu-id="7aadf-124">시작 오류를 캡처하도록 호스트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-124">Configure the host to capture startup errors.</span></span>

* <span data-ttu-id="7aadf-125">[requestTimeout 특성](#attributes-of-the-aspnetcore-element)이 In-Process 호스팅에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-125">The [requestTimeout attribute](#attributes-of-the-aspnetcore-element) doesn't apply to in-process hosting.</span></span>

* <span data-ttu-id="7aadf-126">앱 간의 앱 풀 공유는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-126">Sharing an app pool among apps isn't supported.</span></span> <span data-ttu-id="7aadf-127">앱당 하나의 앱 풀을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-127">Use one app pool per app.</span></span>

* <span data-ttu-id="7aadf-128">[웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)를 사용하거나 [app_offline.htm 파일을 배포에](xref:host-and-deploy/iis/index#locked-deployment-files) 수동으로 배치할 경우 열린 연결이 있으면 앱이 즉시 종료되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-128">When using [Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) or manually placing an [app_offline.htm file in the deployment](xref:host-and-deploy/iis/index#locked-deployment-files), the app might not shut down immediately if there's an open connection.</span></span> <span data-ttu-id="7aadf-129">예를 들어, WebSocket 연결은 앱 종료를 지연시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-129">For example, a websocket connection may delay app shut down.</span></span>

* <span data-ttu-id="7aadf-130">앱 및 설치된 런타임(x64 또는 x86)의 아키텍처(비트)는 앱 풀의 아키텍처와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-130">The architecture (bitness) of the app and installed runtime (x64 or x86) must match the architecture of the app pool.</span></span>

* <span data-ttu-id="7aadf-131">`WebHostBuilder`([CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host)를 사용하지 않고)를 사용하여 앱 호스트를 수동으로 설정하며 앱이 Kestrel 서버에서 직접 실행되는 경우(자체 호스트됨) `UseIISIntegration`를 호출하기 전에 `UseKestrel`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-131">If setting up the app's host manually with `WebHostBuilder` (not using [CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host)) and the app is ever run directly on the Kestrel server (self-hosted), call `UseKestrel` before calling `UseIISIntegration`.</span></span> <span data-ttu-id="7aadf-132">이 순서가 바뀌면 호스트가 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-132">If the order is reversed, the host fails to start.</span></span>

* <span data-ttu-id="7aadf-133">클라이언트의 연결 끊김이 검색되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-133">Client disconnects are detected.</span></span> <span data-ttu-id="7aadf-134">클라이언트의 연결이 끊어지면 [HttpContext.RequestAborted](xref:Microsoft.AspNetCore.Http.HttpContext.RequestAborted*) 취소 토큰이 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-134">The [HttpContext.RequestAborted](xref:Microsoft.AspNetCore.Http.HttpContext.RequestAborted*) cancellation token is cancelled when the client disconnects.</span></span>

* <span data-ttu-id="7aadf-135">ASP.NET Core 2.2.1 이하에서 <xref:System.IO.Directory.GetCurrentDirectory*>는 앱 디렉터리가 아닌 IIS에 의해 시작된 프로세스의 작업자 디렉터리를 반환합니다(예: *w3wp.exe*에 대한 *C:\Windows\System32\inetsrv*).</span><span class="sxs-lookup"><span data-stu-id="7aadf-135">In ASP.NET Core 2.2.1 or earlier, <xref:System.IO.Directory.GetCurrentDirectory*> returns the worker directory of the process started by IIS rather than the app's directory (for example, *C:\Windows\System32\inetsrv* for *w3wp.exe*).</span></span>

  <span data-ttu-id="7aadf-136">앱의 현재 디렉터리를 설정하는 샘플 코드는 [CurrentDirectoryHelpers 클래스](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/aspnet-core-module/samples_snapshot/2.x/CurrentDirectoryHelpers.cs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7aadf-136">For sample code that sets the app's current directory, see the [CurrentDirectoryHelpers class](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/aspnet-core-module/samples_snapshot/2.x/CurrentDirectoryHelpers.cs).</span></span> <span data-ttu-id="7aadf-137">`SetCurrentDirectory` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-137">Call the `SetCurrentDirectory` method.</span></span> <span data-ttu-id="7aadf-138"><xref:System.IO.Directory.GetCurrentDirectory*>에 대한 후속 호출은 앱의 디렉터리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-138">Subsequent calls to <xref:System.IO.Directory.GetCurrentDirectory*> provide the app's directory.</span></span>
  
* <span data-ttu-id="7aadf-139">In-process로 호스팅하는 경우 사용자를 초기화하기 위해 <xref:Microsoft.AspNetCore.Authentication.AuthenticationService.AuthenticateAsync*>를 내부적으로 호출하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-139">When hosting in-process, <xref:Microsoft.AspNetCore.Authentication.AuthenticationService.AuthenticateAsync*> isn't called internally to initialize a user.</span></span> <span data-ttu-id="7aadf-140">따라서 모든 인증 후에 클레임을 변환하는 데 사용되는 <xref:Microsoft.AspNetCore.Authentication.IClaimsTransformation> 구현은 기본적으로 활성화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-140">Therefore, an <xref:Microsoft.AspNetCore.Authentication.IClaimsTransformation> implementation used to transform claims after every authentication isn't activated by default.</span></span> <span data-ttu-id="7aadf-141"><xref:Microsoft.AspNetCore.Authentication.IClaimsTransformation> 구현으로 클레임을 변환할 때 <xref:Microsoft.Extensions.DependencyInjection.AuthenticationServiceCollectionExtensions.AddAuthentication*>을 호출하여 인증 서비스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-141">When transforming claims with an <xref:Microsoft.AspNetCore.Authentication.IClaimsTransformation> implementation, call <xref:Microsoft.Extensions.DependencyInjection.AuthenticationServiceCollectionExtensions.AddAuthentication*> to add authentication services:</span></span>

  ```csharp
  public void ConfigureServices(IServiceCollection services)
  {
      services.AddTransient<IClaimsTransformation, ClaimsTransformer>();
      services.AddAuthentication(IISServerDefaults.AuthenticationScheme);
  }
  
  public void Configure(IApplicationBuilder app)
  {
      app.UseAuthentication();
  }
  ```

### <a name="out-of-process-hosting-model"></a><span data-ttu-id="7aadf-142">Out-of-Process 호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="7aadf-142">Out-of-process hosting model</span></span>

<span data-ttu-id="7aadf-143">Out of Process 호스팅을 위한 앱을 구성하려면 프로젝트 파일에서 다음 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-143">To configure an app for out-of-process hosting, use either of the following approaches in the project file:</span></span>

* <span data-ttu-id="7aadf-144">`<AspNetCoreHostingModel>` 속성을 지정하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7aadf-144">Don't specify the `<AspNetCoreHostingModel>` property.</span></span> <span data-ttu-id="7aadf-145">파일에 `<AspNetCoreHostingModel>` 속성이 없으면 기본값은 `OutOfProcess`입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-145">If the `<AspNetCoreHostingModel>` property isn't present in the file, the default value is `OutOfProcess`.</span></span>
* <span data-ttu-id="7aadf-146">`<AspNetCoreHostingModel>` 속성 값을 `OutOfProcess`로 설정합니다(In Process 호스트팅은 `InProcess`로 설정됨).</span><span class="sxs-lookup"><span data-stu-id="7aadf-146">Set the value of the `<AspNetCoreHostingModel>` property to `OutOfProcess` (in-process hosting is set with `InProcess`):</span></span>

```xml
<PropertyGroup>
  <AspNetCoreHostingModel>OutOfProcess</AspNetCoreHostingModel>
</PropertyGroup>
```

<span data-ttu-id="7aadf-147">[Kestrel](xref:fundamentals/servers/kestrel) 서버는 IIS HTTP 서버(`IISHttpServer`) 대신 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-147">[Kestrel](xref:fundamentals/servers/kestrel) server is used instead of IIS HTTP Server (`IISHttpServer`).</span></span>

<span data-ttu-id="7aadf-148">Out of Process의 경우 [CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host)는 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*>를 호출하여 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-148">For out-of-process, [CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host) calls <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> to:</span></span>

* <span data-ttu-id="7aadf-149">ASP.NET Core 모듈 뒤에서 실행될 때 서버가 수신 대기해야 하는 포트 및 기본 경로를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-149">Configure the port and base path the server should listen on when running behind the ASP.NET Core Module.</span></span>
* <span data-ttu-id="7aadf-150">시작 오류를 캡처하도록 호스트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-150">Configure the host to capture startup errors.</span></span>

### <a name="hosting-model-changes"></a><span data-ttu-id="7aadf-151">호스팅 모델 변경</span><span class="sxs-lookup"><span data-stu-id="7aadf-151">Hosting model changes</span></span>

<span data-ttu-id="7aadf-152">`hostingModel` 설정이 *web.config* 파일에서 변경되면([web.config로 구성](#configuration-with-webconfig) 섹션에 설명되어 있음) 모듈은 IIS에 대한 작업자 프로세스를 재순환합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-152">If the `hostingModel` setting is changed in the *web.config* file (explained in the [Configuration with web.config](#configuration-with-webconfig) section), the module recycles the worker process for IIS.</span></span>

<span data-ttu-id="7aadf-153">IIS Express의 경우 모듈은 작업자 프로세스를 재순환하지 않고, 대신 현재 IIS Express 프로세스의 정상 종료를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-153">For IIS Express, the module doesn't recycle the worker process but instead triggers a graceful shutdown of the current IIS Express process.</span></span> <span data-ttu-id="7aadf-154">앱에 대한 다음 요청은 새 IIS Express 프로세스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-154">The next request to the app spawns a new IIS Express process.</span></span>

### <a name="process-name"></a><span data-ttu-id="7aadf-155">프로세스 이름</span><span class="sxs-lookup"><span data-stu-id="7aadf-155">Process name</span></span>

<span data-ttu-id="7aadf-156">`Process.GetCurrentProcess().ProcessName`은 `w3wp`/`iisexpress`(In-Process) 또는 `dotnet`(Out-of-Process)을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-156">`Process.GetCurrentProcess().ProcessName` reports `w3wp`/`iisexpress` (in-process) or `dotnet` (out-of-process).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="7aadf-157">ASP.NET Core 모듈은 백 엔드 ASP.NET Core 앱으로 웹 요청을 전달하는 IIS 파이프라인에 연결되는 네이티브 IIS 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-157">The ASP.NET Core Module is a native IIS module that plugs into the IIS pipeline to forward web requests to backend ASP.NET Core apps.</span></span>

<span data-ttu-id="7aadf-158">지원되는 Windows 버전:</span><span class="sxs-lookup"><span data-stu-id="7aadf-158">Supported Windows versions:</span></span>

* <span data-ttu-id="7aadf-159">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="7aadf-159">Windows 7 or later</span></span>
* <span data-ttu-id="7aadf-160">Windows Server 2008 R2 이상</span><span class="sxs-lookup"><span data-stu-id="7aadf-160">Windows Server 2008 R2 or later</span></span>

<span data-ttu-id="7aadf-161">모듈은 Kestrel에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-161">The module only works with Kestrel.</span></span> <span data-ttu-id="7aadf-162">모듈이 [HTTP.sys](xref:fundamentals/servers/httpsys)와 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-162">The module is incompatible with [HTTP.sys](xref:fundamentals/servers/httpsys).</span></span>

<span data-ttu-id="7aadf-163">ASP.NET Core 앱은 IIS 작업자 프로세스와 별도의 프로세스에서 실행되므로 이 모듈은 프로세스 관리도 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-163">Because ASP.NET Core apps run in a process separate from the IIS worker process, the module also handles process management.</span></span> <span data-ttu-id="7aadf-164">이 모듈은 첫 번째 요청이 들어올 때 ASP.NET Core 앱용 프로세스를 시작하고 충돌이 발생하면 앱을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-164">The module starts the process for the ASP.NET Core app when the first request arrives and restarts the app if it crashes.</span></span> <span data-ttu-id="7aadf-165">이는 [Windows Process Activation Service(WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was)로 관리되는 IIS에서 In Process로 실행되는 ASP.NET 4.x 앱에서 볼 수 있는 동작과 기본적으로 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-165">This is essentially the same behavior as seen with ASP.NET 4.x apps that run in-process in IIS that are managed by the [Windows Process Activation Service (WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was).</span></span>

<span data-ttu-id="7aadf-166">다음 다이어그램은 IIS, ASP.NET Core 모듈 및 앱 간의 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-166">The following diagram illustrates the relationship between IIS, the ASP.NET Core Module, and an app:</span></span>

![ASP.NET Core 모듈](aspnet-core-module/_static/ancm-outofprocess.png)

<span data-ttu-id="7aadf-168">요청은 웹에서 커널 모드 HTTP.sys 드라이버로 도착합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-168">Requests arrive from the web to the kernel-mode HTTP.sys driver.</span></span> <span data-ttu-id="7aadf-169">드라이버는 웹 사이트의 구성된 포트(일반적으로 80(HTTP) 또는 443(HTTPS))에서 IIS로 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-169">The driver routes the requests to IIS on the website's configured port, usually 80 (HTTP) or 443 (HTTPS).</span></span> <span data-ttu-id="7aadf-170">모듈은 포트 80 또는 443이 아닌 앱의 임의의 포트에서 Kestrel로 요청을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-170">The module forwards the requests to Kestrel on a random port for the app, which isn't port 80 or 443.</span></span>

<span data-ttu-id="7aadf-171">모듈은 시작 시 환경 변수를 통해 포트를 지정하고 IIS 통합 미들웨어는 `http://localhost:{port}`에서 수신 대기하도록 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-171">The module specifies the port via an environment variable at startup, and the IIS Integration Middleware configures the server to listen on `http://localhost:{port}`.</span></span> <span data-ttu-id="7aadf-172">추가 검사가 수행되고 모듈에서 시작되지 않은 요청은 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-172">Additional checks are performed, and requests that don't originate from the module are rejected.</span></span> <span data-ttu-id="7aadf-173">모듈은 HTTPS 전달을 지원하지 않으므로 HTTPS를 통해 IIS에서 수신된 경우에도 HTTP를 통해 요청이 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-173">The module doesn't support HTTPS forwarding, so requests are forwarded over HTTP even if received by IIS over HTTPS.</span></span>

<span data-ttu-id="7aadf-174">Kestrel이 모듈에서 요청을 선택한 후, 요청은 ASP.NET Core 미들웨어 파이프라인으로 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-174">After Kestrel picks up the request from the module, the request is pushed into the ASP.NET Core middleware pipeline.</span></span> <span data-ttu-id="7aadf-175">미들웨어 파이프라인은 요청을 처리하고 앱의 논리에 `HttpContext` 인스턴스로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-175">The middleware pipeline handles the request and passes it on as an `HttpContext` instance to the app's logic.</span></span> <span data-ttu-id="7aadf-176">IIS 통합에 의해 추가된 미들웨어는 체계, 원격 IP 및 경로 기준을 Kestrel에 요청을 전달하기 위한 계정으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-176">Middleware added by IIS Integration updates the scheme, remote IP, and pathbase to account for forwarding the request to Kestrel.</span></span> <span data-ttu-id="7aadf-177">앱의 응답은 IIS로 다시 전달되고, 요청을 시작한 HTTP 클라이언트에 다시 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-177">The app's response is passed back to IIS, which pushes it back out to the HTTP client that initiated the request.</span></span>

::: moniker-end

<span data-ttu-id="7aadf-178">Windows 인증 등의 많은 네이티브 모듈이 활성 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-178">Many native modules, such as Windows Authentication, remain active.</span></span> <span data-ttu-id="7aadf-179">ASP.NET Core 모듈을 사용하여 활성화된 IIS 모듈에 대해 자세히 알아보려면 <xref:host-and-deploy/iis/modules>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7aadf-179">To learn more about IIS modules active with the ASP.NET Core Module, see <xref:host-and-deploy/iis/modules>.</span></span>

<span data-ttu-id="7aadf-180">ASP.NET Core 모듈은 다음 작업을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-180">The ASP.NET Core Module can also:</span></span>

* <span data-ttu-id="7aadf-181">작업자 프로세스의 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-181">Set environment variables for the worker process.</span></span>
* <span data-ttu-id="7aadf-182">시작 문제를 해결하기 위해 stdout 출력을 파일 스토리지에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-182">Log stdout output to file storage for troubleshooting startup issues.</span></span>
* <span data-ttu-id="7aadf-183">Windows 인증 토큰을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-183">Forward Windows authentication tokens.</span></span>

## <a name="how-to-install-and-use-the-aspnet-core-module"></a><span data-ttu-id="7aadf-184">ASP.NET Core 모듈을 설치하고 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="7aadf-184">How to install and use the ASP.NET Core Module</span></span>

<span data-ttu-id="7aadf-185">ASP.NET Core 모듈을 설치하고 사용하는 방법에 대한 지침은 <xref:host-and-deploy/iis/index>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7aadf-185">For instructions on how to install and use the ASP.NET Core Module, see <xref:host-and-deploy/iis/index>.</span></span>

## <a name="configuration-with-webconfig"></a><span data-ttu-id="7aadf-186">web.config를 사용한 구성</span><span class="sxs-lookup"><span data-stu-id="7aadf-186">Configuration with web.config</span></span>

<span data-ttu-id="7aadf-187">ASP.NET Core 모듈은 사이트의 *web.config* 파일에 있는 `system.webServer` 노드의 `aspNetCore` 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-187">The ASP.NET Core Module is configured with the `aspNetCore` section of the `system.webServer` node in the site's *web.config* file.</span></span>

<span data-ttu-id="7aadf-188">다음 *web.config* 파일은 [프레임워크 종속 배포](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd)를 위해 게시되고 사이트 요청을 처리하도록 ASP.NET Core 모듈을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-188">The following *web.config* file is published for a [framework-dependent deployment](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd) and configures the ASP.NET Core Module to handle site requests:</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <location path="." inheritInChildApplications="false">
    <system.webServer>
      <handlers>
        <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
      </handlers>
      <aspNetCore processPath="dotnet" 
                  arguments=".\MyApp.dll" 
                  stdoutLogEnabled="false" 
                  stdoutLogFile=".\logs\stdout" 
                  hostingModel="InProcess" />
    </system.webServer>
  </location>
</configuration>
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModule" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath="dotnet" 
                arguments=".\MyApp.dll" 
                stdoutLogEnabled="false" 
                stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

::: moniker-end

<span data-ttu-id="7aadf-189">다음 *web.config*는 [자체 포함 배포](/dotnet/articles/core/deploying/#self-contained-deployments-scd)를 위해 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-189">The following *web.config* is published for a [self-contained deployment](/dotnet/articles/core/deploying/#self-contained-deployments-scd):</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <location path="." inheritInChildApplications="false">
    <system.webServer>
      <handlers>
        <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
      </handlers>
      <aspNetCore processPath=".\MyApp.exe" 
                  stdoutLogEnabled="false" 
                  stdoutLogFile=".\logs\stdout" 
                  hostingModel="InProcess" />
    </system.webServer>
  </location>
</configuration>
```

<span data-ttu-id="7aadf-190"><xref:System.Configuration.SectionInformation.InheritInChildApplications*> 속성이 `false`로 설정되어 [\<location>](/iis/manage/managing-your-configuration-settings/understanding-iis-configuration-delegation#the-concept-of-location) 요소 내에서 지정된 설정이 하위 디렉터리에 있는 앱에 상속되지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-190">The <xref:System.Configuration.SectionInformation.InheritInChildApplications*> property is set to `false` to indicate that the settings specified within the [\<location>](/iis/manage/managing-your-configuration-settings/understanding-iis-configuration-delegation#the-concept-of-location) element aren't inherited by apps that reside in a subdirectory of the app.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModule" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath=".\MyApp.exe" 
                stdoutLogEnabled="false" 
                stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

::: moniker-end

<span data-ttu-id="7aadf-191">앱이 [Azure App Service](https://azure.microsoft.com/services/app-service/)에 배포되면 `stdoutLogFile` 경로가 `\\?\%home%\LogFiles\stdout`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-191">When an app is deployed to [Azure App Service](https://azure.microsoft.com/services/app-service/), the `stdoutLogFile` path is set to `\\?\%home%\LogFiles\stdout`.</span></span> <span data-ttu-id="7aadf-192">이 경로는 서비스에서 자동으로 만들어진 위치인 *LogFiles* 폴더에 stdout 로그를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-192">The path saves stdout logs to the *LogFiles* folder, which is a location automatically created by the service.</span></span>

<span data-ttu-id="7aadf-193">IIS 하위 애플리케이션 구성에 대한 자세한 내용은 <xref:host-and-deploy/iis/index#sub-applications>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7aadf-193">For information on IIS sub-application configuration, see <xref:host-and-deploy/iis/index#sub-applications>.</span></span>

### <a name="attributes-of-the-aspnetcore-element"></a><span data-ttu-id="7aadf-194">aspNetCore 요소의 특성</span><span class="sxs-lookup"><span data-stu-id="7aadf-194">Attributes of the aspNetCore element</span></span>

::: moniker range=">= aspnetcore-2.2"

| <span data-ttu-id="7aadf-195">특성</span><span class="sxs-lookup"><span data-stu-id="7aadf-195">Attribute</span></span> | <span data-ttu-id="7aadf-196">설명</span><span class="sxs-lookup"><span data-stu-id="7aadf-196">Description</span></span> | <span data-ttu-id="7aadf-197">기본</span><span class="sxs-lookup"><span data-stu-id="7aadf-197">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="7aadf-198">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-198">Optional string attribute.</span></span></p><p><span data-ttu-id="7aadf-199">**processPath**에 지정된 실행 파일에 대한 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-199">Arguments to the executable specified in **processPath**.</span></span></p> | |
| `disableStartUpErrorPage` | <p><span data-ttu-id="7aadf-200">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-200">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="7aadf-201">true인 경우 **502.5 - 프로세스 실패** 페이지가 표시되지 않고 *web.config*에 구성된 502 상태 코드 페이지가 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-201">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="7aadf-202">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-202">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="7aadf-203">true인 경우 토큰은 %ASPNETCORE_PORT%에서 수신 대기하는 자식 프로세스에 요청별 헤더 'MS-ASPNETCORE-WINAUTHTOKEN'으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-203">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="7aadf-204">이 프로세스는 요청별로 이 토큰에서 CloseHandle을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-204">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `hostingModel` | <p><span data-ttu-id="7aadf-205">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-205">Optional string attribute.</span></span></p><p><span data-ttu-id="7aadf-206">호스팅 모델을 In-Process(`InProcess`) 또는 Out-of-Process(`OutOfProcess`)로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-206">Specifies the hosting model as in-process (`InProcess`) or out-of-process (`OutOfProcess`).</span></span></p> | `OutOfProcess` |
| `processesPerApplication` | <p><span data-ttu-id="7aadf-207">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-207">Optional integer attribute.</span></span></p><p><span data-ttu-id="7aadf-208">앱별로 스핀 업할 수 있는 **processPath** 설정에 지정된 프로세스의 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-208">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p><p><span data-ttu-id="7aadf-209">&dagger;In-Process 호스팅의 경우 이 값은 `1`로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-209">&dagger;For in-process hosting, the value is limited to `1`.</span></span></p><p><span data-ttu-id="7aadf-210">설정 `processesPerApplication`은 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-210">Setting `processesPerApplication` is discouraged.</span></span> <span data-ttu-id="7aadf-211">이 특성은 이후 릴리스에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-211">This attribute will be removed in a future release.</span></span></p> | <span data-ttu-id="7aadf-212">기본값: `1`</span><span class="sxs-lookup"><span data-stu-id="7aadf-212">Default: `1`</span></span><br><span data-ttu-id="7aadf-213">최소: `1`</span><span class="sxs-lookup"><span data-stu-id="7aadf-213">Min: `1`</span></span><br><span data-ttu-id="7aadf-214">최대: `100`&dagger;</span><span class="sxs-lookup"><span data-stu-id="7aadf-214">Max: `100`&dagger;</span></span> |
| `processPath` | <p><span data-ttu-id="7aadf-215">필수 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-215">Required string attribute.</span></span></p><p><span data-ttu-id="7aadf-216">HTTP 요청을 수신 대기하는 프로세스를 시작하는 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-216">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="7aadf-217">상대 경로가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-217">Relative paths are supported.</span></span> <span data-ttu-id="7aadf-218">경로가 `.`로 시작되면 경로는 사이트 루트의 상대 경로로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-218">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="7aadf-219">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-219">Optional integer attribute.</span></span></p><p><span data-ttu-id="7aadf-220">**processPath**에 지정된 프로세스의 분당 크래시 허용 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-220">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="7aadf-221">이 제한을 초과하면 모듈은 남은 시간 동안 프로세스 시작을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-221">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p><p><span data-ttu-id="7aadf-222">In-Process 호스팅에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-222">Not supported with in-process hosting.</span></span></p> | <span data-ttu-id="7aadf-223">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="7aadf-223">Default: `10`</span></span><br><span data-ttu-id="7aadf-224">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="7aadf-224">Min: `0`</span></span><br><span data-ttu-id="7aadf-225">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="7aadf-225">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="7aadf-226">선택적 시간 간격 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-226">Optional timespan attribute.</span></span></p><p><span data-ttu-id="7aadf-227">ASP.NET Core 모듈이 %ASPNETCORE_PORT%에서 수신 대기하는 프로세스의 응답을 기다리는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-227">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="7aadf-228">ASP.NET Core 2.1 이상 릴리스와 함께 제공되는 ASP.NET Core 모듈 버전에서는 `requestTimeout`이 전체 시간, 분, 초로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-228">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.1 or later, the `requestTimeout` is specified in hours, minutes, and seconds.</span></span></p><p><span data-ttu-id="7aadf-229">In-Process 호스팅에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-229">Doesn't apply to in-process hosting.</span></span> <span data-ttu-id="7aadf-230">In-Process 호스팅의 경우 모듈은 앱이 요청을 처리할 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-230">For in-process hosting, the module waits for the app to process the request.</span></span></p> | <span data-ttu-id="7aadf-231">기본값: `00:02:00`</span><span class="sxs-lookup"><span data-stu-id="7aadf-231">Default: `00:02:00`</span></span><br><span data-ttu-id="7aadf-232">최소: `00:00:00`</span><span class="sxs-lookup"><span data-stu-id="7aadf-232">Min: `00:00:00`</span></span><br><span data-ttu-id="7aadf-233">최대: `360:00:00`</span><span class="sxs-lookup"><span data-stu-id="7aadf-233">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="7aadf-234">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-234">Optional integer attribute.</span></span></p><p><span data-ttu-id="7aadf-235">*app_offline.htm* 파일이 검색될 때 실행 파일이 정상적으로 종료될 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-235">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="7aadf-236">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="7aadf-236">Default: `10`</span></span><br><span data-ttu-id="7aadf-237">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="7aadf-237">Min: `0`</span></span><br><span data-ttu-id="7aadf-238">최대: `600`</span><span class="sxs-lookup"><span data-stu-id="7aadf-238">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="7aadf-239">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-239">Optional integer attribute.</span></span></p><p><span data-ttu-id="7aadf-240">실행 파일이 포트에서 수신 대기하는 프로세스를 시작할 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-240">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="7aadf-241">이 시간 제한을 초과하면 모듈이 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-241">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="7aadf-242">모듈은 새 요청을 수신할 때 프로세스를 다시 시작하려고 하고, 마지막 롤링 기간(분)에 앱이 **rapidFailsPerMinute**번 시작에 실패한 경우가 아니면 이후 요청이 들어올 때 프로세스를 계속 다시 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-242">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p><p><span data-ttu-id="7aadf-243">값 0은 무한 시간 제한으로 간주되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="7aadf-243">A value of 0 (zero) is **not** considered an infinite timeout.</span></span></p> | <span data-ttu-id="7aadf-244">기본값: `120`</span><span class="sxs-lookup"><span data-stu-id="7aadf-244">Default: `120`</span></span><br><span data-ttu-id="7aadf-245">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="7aadf-245">Min: `0`</span></span><br><span data-ttu-id="7aadf-246">최대: `3600`</span><span class="sxs-lookup"><span data-stu-id="7aadf-246">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="7aadf-247">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-247">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="7aadf-248">true인 경우 **processPath**에 지정된 프로세스에 대한 **stdout** 및 **stderr**이 **stdoutLogFile**에 지정된 파일로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-248">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="7aadf-249">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-249">Optional string attribute.</span></span></p><p><span data-ttu-id="7aadf-250">**processPath**에 지정된 프로세스에서 **stdout** 및 **stderr**이 기록되는 상대 또는 절대 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-250">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="7aadf-251">상대 경로는 사이트 루트에 상대적인 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-251">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="7aadf-252">`.`로 시작하는 모든 경로는 사이트 루트에 상대적인 경로이고 다른 모든 경로는 절대 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-252">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="7aadf-253">경로에 제공된 모든 폴더는 로그 파일을 만들 때 모듈에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-253">Any folders provided in the path are created by the module when the log file is created.</span></span> <span data-ttu-id="7aadf-254">타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)은 밑줄 구분 기호를 사용하여 **stdoutLogFile** 경로의 마지막 세그먼트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-254">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="7aadf-255">`.\logs\stdout`이 값으로 제공되는 경우 예제 stdout 로그는 2018년 2월 5일 19시 41분 32초에 프로세스 ID 1934를 사용하여 저장될 경우 *logs* 폴더에 *stdout_20180205194132_1934.log*로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-255">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

::: moniker range="= aspnetcore-2.1"

| <span data-ttu-id="7aadf-256">특성</span><span class="sxs-lookup"><span data-stu-id="7aadf-256">Attribute</span></span> | <span data-ttu-id="7aadf-257">설명</span><span class="sxs-lookup"><span data-stu-id="7aadf-257">Description</span></span> | <span data-ttu-id="7aadf-258">기본</span><span class="sxs-lookup"><span data-stu-id="7aadf-258">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="7aadf-259">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-259">Optional string attribute.</span></span></p><p><span data-ttu-id="7aadf-260">**processPath**에 지정된 실행 파일에 대한 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-260">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <p><span data-ttu-id="7aadf-261">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-261">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="7aadf-262">true인 경우 **502.5 - 프로세스 실패** 페이지가 표시되지 않고 *web.config*에 구성된 502 상태 코드 페이지가 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-262">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="7aadf-263">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-263">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="7aadf-264">true인 경우 토큰은 %ASPNETCORE_PORT%에서 수신 대기하는 자식 프로세스에 요청별 헤더 'MS-ASPNETCORE-WINAUTHTOKEN'으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-264">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="7aadf-265">이 프로세스는 요청별로 이 토큰에서 CloseHandle을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-265">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processesPerApplication` | <p><span data-ttu-id="7aadf-266">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-266">Optional integer attribute.</span></span></p><p><span data-ttu-id="7aadf-267">앱별로 스핀 업할 수 있는 **processPath** 설정에 지정된 프로세스의 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-267">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p><p><span data-ttu-id="7aadf-268">설정 `processesPerApplication`은 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-268">Setting `processesPerApplication` is discouraged.</span></span> <span data-ttu-id="7aadf-269">이 특성은 이후 릴리스에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-269">This attribute will be removed in a future release.</span></span></p> | <span data-ttu-id="7aadf-270">기본값: `1`</span><span class="sxs-lookup"><span data-stu-id="7aadf-270">Default: `1`</span></span><br><span data-ttu-id="7aadf-271">최소: `1`</span><span class="sxs-lookup"><span data-stu-id="7aadf-271">Min: `1`</span></span><br><span data-ttu-id="7aadf-272">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="7aadf-272">Max: `100`</span></span> |
| `processPath` | <p><span data-ttu-id="7aadf-273">필수 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-273">Required string attribute.</span></span></p><p><span data-ttu-id="7aadf-274">HTTP 요청을 수신 대기하는 프로세스를 시작하는 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-274">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="7aadf-275">상대 경로가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-275">Relative paths are supported.</span></span> <span data-ttu-id="7aadf-276">경로가 `.`로 시작되면 경로는 사이트 루트의 상대 경로로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-276">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="7aadf-277">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-277">Optional integer attribute.</span></span></p><p><span data-ttu-id="7aadf-278">**processPath**에 지정된 프로세스의 분당 크래시 허용 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-278">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="7aadf-279">이 제한을 초과하면 모듈은 남은 시간 동안 프로세스 시작을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-279">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | <span data-ttu-id="7aadf-280">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="7aadf-280">Default: `10`</span></span><br><span data-ttu-id="7aadf-281">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="7aadf-281">Min: `0`</span></span><br><span data-ttu-id="7aadf-282">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="7aadf-282">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="7aadf-283">선택적 시간 간격 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-283">Optional timespan attribute.</span></span></p><p><span data-ttu-id="7aadf-284">ASP.NET Core 모듈이 %ASPNETCORE_PORT%에서 수신 대기하는 프로세스의 응답을 기다리는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-284">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="7aadf-285">ASP.NET Core 2.1 이상 릴리스와 함께 제공되는 ASP.NET Core 모듈 버전에서는 `requestTimeout`이 전체 시간, 분, 초로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-285">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.1 or later, the `requestTimeout` is specified in hours, minutes, and seconds.</span></span></p> | <span data-ttu-id="7aadf-286">기본값: `00:02:00`</span><span class="sxs-lookup"><span data-stu-id="7aadf-286">Default: `00:02:00`</span></span><br><span data-ttu-id="7aadf-287">최소: `00:00:00`</span><span class="sxs-lookup"><span data-stu-id="7aadf-287">Min: `00:00:00`</span></span><br><span data-ttu-id="7aadf-288">최대: `360:00:00`</span><span class="sxs-lookup"><span data-stu-id="7aadf-288">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="7aadf-289">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-289">Optional integer attribute.</span></span></p><p><span data-ttu-id="7aadf-290">*app_offline.htm* 파일이 검색될 때 실행 파일이 정상적으로 종료될 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-290">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="7aadf-291">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="7aadf-291">Default: `10`</span></span><br><span data-ttu-id="7aadf-292">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="7aadf-292">Min: `0`</span></span><br><span data-ttu-id="7aadf-293">최대: `600`</span><span class="sxs-lookup"><span data-stu-id="7aadf-293">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="7aadf-294">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-294">Optional integer attribute.</span></span></p><p><span data-ttu-id="7aadf-295">실행 파일이 포트에서 수신 대기하는 프로세스를 시작할 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-295">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="7aadf-296">이 시간 제한을 초과하면 모듈이 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-296">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="7aadf-297">모듈은 새 요청을 수신할 때 프로세스를 다시 시작하려고 하고, 마지막 롤링 기간(분)에 앱이 **rapidFailsPerMinute**번 시작에 실패한 경우가 아니면 이후 요청이 들어올 때 프로세스를 계속 다시 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-297">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p><p><span data-ttu-id="7aadf-298">값 0은 무한 시간 제한으로 간주되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="7aadf-298">A value of 0 (zero) is **not** considered an infinite timeout.</span></span></p> | <span data-ttu-id="7aadf-299">기본값: `120`</span><span class="sxs-lookup"><span data-stu-id="7aadf-299">Default: `120`</span></span><br><span data-ttu-id="7aadf-300">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="7aadf-300">Min: `0`</span></span><br><span data-ttu-id="7aadf-301">최대: `3600`</span><span class="sxs-lookup"><span data-stu-id="7aadf-301">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="7aadf-302">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-302">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="7aadf-303">true인 경우 **processPath**에 지정된 프로세스에 대한 **stdout** 및 **stderr**이 **stdoutLogFile**에 지정된 파일로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-303">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="7aadf-304">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-304">Optional string attribute.</span></span></p><p><span data-ttu-id="7aadf-305">**processPath**에 지정된 프로세스에서 **stdout** 및 **stderr**이 기록되는 상대 또는 절대 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-305">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="7aadf-306">상대 경로는 사이트 루트에 상대적인 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-306">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="7aadf-307">`.`로 시작하는 모든 경로는 사이트 루트에 상대적인 경로이고 다른 모든 경로는 절대 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-307">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="7aadf-308">모듈이 로그 파일을 만들려면 경로에 제공된 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-308">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="7aadf-309">타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)은 밑줄 구분 기호를 사용하여 **stdoutLogFile** 경로의 마지막 세그먼트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-309">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="7aadf-310">`.\logs\stdout`이 값으로 제공되는 경우 예제 stdout 로그는 2018년 2월 5일 19시 41분 32초에 프로세스 ID 1934를 사용하여 저장될 경우 *logs* 폴더에 *stdout_20180205194132_1934.log*로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-310">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

| <span data-ttu-id="7aadf-311">특성</span><span class="sxs-lookup"><span data-stu-id="7aadf-311">Attribute</span></span> | <span data-ttu-id="7aadf-312">설명</span><span class="sxs-lookup"><span data-stu-id="7aadf-312">Description</span></span> | <span data-ttu-id="7aadf-313">기본</span><span class="sxs-lookup"><span data-stu-id="7aadf-313">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="7aadf-314">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-314">Optional string attribute.</span></span></p><p><span data-ttu-id="7aadf-315">**processPath**에 지정된 실행 파일에 대한 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-315">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <p><span data-ttu-id="7aadf-316">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-316">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="7aadf-317">true인 경우 **502.5 - 프로세스 실패** 페이지가 표시되지 않고 *web.config*에 구성된 502 상태 코드 페이지가 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-317">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="7aadf-318">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-318">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="7aadf-319">true인 경우 토큰은 %ASPNETCORE_PORT%에서 수신 대기하는 자식 프로세스에 요청별 헤더 'MS-ASPNETCORE-WINAUTHTOKEN'으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-319">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="7aadf-320">이 프로세스는 요청별로 이 토큰에서 CloseHandle을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-320">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processesPerApplication` | <p><span data-ttu-id="7aadf-321">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-321">Optional integer attribute.</span></span></p><p><span data-ttu-id="7aadf-322">앱별로 스핀 업할 수 있는 **processPath** 설정에 지정된 프로세스의 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-322">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p><p><span data-ttu-id="7aadf-323">설정 `processesPerApplication`은 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-323">Setting `processesPerApplication` is discouraged.</span></span> <span data-ttu-id="7aadf-324">이 특성은 이후 릴리스에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-324">This attribute will be removed in a future release.</span></span></p> | <span data-ttu-id="7aadf-325">기본값: `1`</span><span class="sxs-lookup"><span data-stu-id="7aadf-325">Default: `1`</span></span><br><span data-ttu-id="7aadf-326">최소: `1`</span><span class="sxs-lookup"><span data-stu-id="7aadf-326">Min: `1`</span></span><br><span data-ttu-id="7aadf-327">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="7aadf-327">Max: `100`</span></span> |
| `processPath` | <p><span data-ttu-id="7aadf-328">필수 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-328">Required string attribute.</span></span></p><p><span data-ttu-id="7aadf-329">HTTP 요청을 수신 대기하는 프로세스를 시작하는 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-329">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="7aadf-330">상대 경로가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-330">Relative paths are supported.</span></span> <span data-ttu-id="7aadf-331">경로가 `.`로 시작되면 경로는 사이트 루트의 상대 경로로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-331">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="7aadf-332">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-332">Optional integer attribute.</span></span></p><p><span data-ttu-id="7aadf-333">**processPath**에 지정된 프로세스의 분당 크래시 허용 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-333">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="7aadf-334">이 제한을 초과하면 모듈은 남은 시간 동안 프로세스 시작을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-334">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | <span data-ttu-id="7aadf-335">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="7aadf-335">Default: `10`</span></span><br><span data-ttu-id="7aadf-336">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="7aadf-336">Min: `0`</span></span><br><span data-ttu-id="7aadf-337">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="7aadf-337">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="7aadf-338">선택적 시간 간격 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-338">Optional timespan attribute.</span></span></p><p><span data-ttu-id="7aadf-339">ASP.NET Core 모듈이 %ASPNETCORE_PORT%에서 수신 대기하는 프로세스의 응답을 기다리는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-339">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="7aadf-340">ASP.NET Core 2.0 이하 릴리스와 함께 제공되는 ASP.NET Core 모듈 버전에서는 `requestTimeout`을 전체 시간(분)으로만 지정해야 합니다. 그렇지 않으면 기본적으로 2분으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-340">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.0 or earlier, the `requestTimeout` must be specified in whole minutes only, otherwise it defaults to 2 minutes.</span></span></p> | <span data-ttu-id="7aadf-341">기본값: `00:02:00`</span><span class="sxs-lookup"><span data-stu-id="7aadf-341">Default: `00:02:00`</span></span><br><span data-ttu-id="7aadf-342">최소: `00:00:00`</span><span class="sxs-lookup"><span data-stu-id="7aadf-342">Min: `00:00:00`</span></span><br><span data-ttu-id="7aadf-343">최대: `360:00:00`</span><span class="sxs-lookup"><span data-stu-id="7aadf-343">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="7aadf-344">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-344">Optional integer attribute.</span></span></p><p><span data-ttu-id="7aadf-345">*app_offline.htm* 파일이 검색될 때 실행 파일이 정상적으로 종료될 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-345">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="7aadf-346">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="7aadf-346">Default: `10`</span></span><br><span data-ttu-id="7aadf-347">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="7aadf-347">Min: `0`</span></span><br><span data-ttu-id="7aadf-348">최대: `600`</span><span class="sxs-lookup"><span data-stu-id="7aadf-348">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="7aadf-349">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-349">Optional integer attribute.</span></span></p><p><span data-ttu-id="7aadf-350">실행 파일이 포트에서 수신 대기하는 프로세스를 시작할 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-350">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="7aadf-351">이 시간 제한을 초과하면 모듈이 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-351">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="7aadf-352">모듈은 새 요청을 수신할 때 프로세스를 다시 시작하려고 하고, 마지막 롤링 기간(분)에 앱이 **rapidFailsPerMinute**번 시작에 실패한 경우가 아니면 이후 요청이 들어올 때 프로세스를 계속 다시 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-352">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p> | <span data-ttu-id="7aadf-353">기본값: `120`</span><span class="sxs-lookup"><span data-stu-id="7aadf-353">Default: `120`</span></span><br><span data-ttu-id="7aadf-354">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="7aadf-354">Min: `0`</span></span><br><span data-ttu-id="7aadf-355">최대: `3600`</span><span class="sxs-lookup"><span data-stu-id="7aadf-355">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="7aadf-356">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-356">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="7aadf-357">true인 경우 **processPath**에 지정된 프로세스에 대한 **stdout** 및 **stderr**이 **stdoutLogFile**에 지정된 파일로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-357">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="7aadf-358">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-358">Optional string attribute.</span></span></p><p><span data-ttu-id="7aadf-359">**processPath**에 지정된 프로세스에서 **stdout** 및 **stderr**이 기록되는 상대 또는 절대 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-359">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="7aadf-360">상대 경로는 사이트 루트에 상대적인 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-360">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="7aadf-361">`.`로 시작하는 모든 경로는 사이트 루트에 상대적인 경로이고 다른 모든 경로는 절대 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-361">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="7aadf-362">모듈이 로그 파일을 만들려면 경로에 제공된 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-362">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="7aadf-363">타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)은 밑줄 구분 기호를 사용하여 **stdoutLogFile** 경로의 마지막 세그먼트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-363">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="7aadf-364">`.\logs\stdout`이 값으로 제공되는 경우 예제 stdout 로그는 2018년 2월 5일 19시 41분 32초에 프로세스 ID 1934를 사용하여 저장될 경우 *logs* 폴더에 *stdout_20180205194132_1934.log*로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-364">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

### <a name="setting-environment-variables"></a><span data-ttu-id="7aadf-365">환경 변수 설정</span><span class="sxs-lookup"><span data-stu-id="7aadf-365">Setting environment variables</span></span>

::: moniker range=">= aspnetcore-3.0"

<span data-ttu-id="7aadf-366">`processPath` 특성에서 프로세스에 대한 환경 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-366">Environment variables can be specified for the process in the `processPath` attribute.</span></span> <span data-ttu-id="7aadf-367">`<environmentVariables>` 컬렉션 요소의 `<environmentVariable>` 자식 요소를 사용하여 환경 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-367">Specify an environment variable with the `<environmentVariable>` child element of an `<environmentVariables>` collection element.</span></span> <span data-ttu-id="7aadf-368">이 섹션에 설정된 환경 변수가 시스템 환경 변수보다 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-368">Environment variables set in this section take precedence over system environment variables.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-3.0"

<span data-ttu-id="7aadf-369">`processPath` 특성에서 프로세스에 대한 환경 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-369">Environment variables can be specified for the process in the `processPath` attribute.</span></span> <span data-ttu-id="7aadf-370">`<environmentVariables>` 컬렉션 요소의 `<environmentVariable>` 자식 요소를 사용하여 환경 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-370">Specify an environment variable with the `<environmentVariable>` child element of an `<environmentVariables>` collection element.</span></span>

> [!WARNING]
> <span data-ttu-id="7aadf-371">이 섹션에 설정된 환경 변수가 동일한 이름으로 설정된 시스템 환경 변수와 충돌합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-371">Environment variables set in this section conflict with system environment variables set with the same name.</span></span> <span data-ttu-id="7aadf-372">환경 변수가 *web.config* 파일과 Windows의 시스템 수준에 모두 설정된 경우 *web.config* 파일의 값은 시스템 환경 변수 값(예: `ASPNETCORE_ENVIRONMENT: Development;Development`)에 추가되어 앱이 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-372">If an environment variable is set in both the *web.config* file and at the system level in Windows, the value from the *web.config* file becomes appended to the system environment variable value (for example, `ASPNETCORE_ENVIRONMENT: Development;Development`), which prevents the app from starting.</span></span>

::: moniker-end

<span data-ttu-id="7aadf-373">다음 예제에서는 두 개의 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-373">The following example sets two environment variables.</span></span> <span data-ttu-id="7aadf-374">`ASPNETCORE_ENVIRONMENT`는 앱의 환경을 `Development`로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-374">`ASPNETCORE_ENVIRONMENT` configures the app's environment to `Development`.</span></span> <span data-ttu-id="7aadf-375">앱 예외를 디버그할 때 [개발자 예외 페이지](xref:fundamentals/error-handling)를 강제로 로드하기 위해 개발자가 *web.config* 파일에서 이 값을 일시적으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-375">A developer may temporarily set this value in the *web.config* file in order to force the [Developer Exception Page](xref:fundamentals/error-handling) to load when debugging an app exception.</span></span> <span data-ttu-id="7aadf-376">`CONFIG_DIR`은 개발자가 앱 구성 파일을 로드할 경로를 생성하기 위해 시작 시 값을 읽는 코드를 작성한 사용자 정의 환경 변수의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-376">`CONFIG_DIR` is an example of a user-defined environment variable, where the developer has written code that reads the value on startup to form a path for loading the app's configuration file.</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile="\\?\%home%\LogFiles\stdout"
      hostingModel="InProcess">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
    <environmentVariable name="CONFIG_DIR" value="f:\application_config" />
  </environmentVariables>
</aspNetCore>
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile="\\?\%home%\LogFiles\stdout">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
    <environmentVariable name="CONFIG_DIR" value="f:\application_config" />
  </environmentVariables>
</aspNetCore>
```

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

> [!NOTE]
> <span data-ttu-id="7aadf-377">*web.config*에서 환경을 직접 설정하는 대안으로 게시 프로필(*.pubxml*) 또는 프로젝트 파일에 `<EnvironmentName>` 속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-377">An alternative to setting the environment directly in *web.config* is to include the `<EnvironmentName>` property in the publish profile (*.pubxml*) or project file.</span></span> <span data-ttu-id="7aadf-378">이 방법은 프로젝트가 게시될 때 *web.config*에 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-378">This approach sets the environment in *web.config* when the project is published:</span></span>
>
> ```xml
> <PropertyGroup>
>   <EnvironmentName>Development</EnvironmentName>
> </PropertyGroup>
> ```

::: moniker-end

> [!WARNING]
> <span data-ttu-id="7aadf-379">인터넷과 같은 신뢰할 수 없는 네트워크에 액세스할 수 없는 스테이징 및 테스트 서버에서는 `ASPNETCORE_ENVIRONMENT` 환경 변수를 `Development`로 설정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-379">Only set the `ASPNETCORE_ENVIRONMENT` environment variable to `Development` on staging and testing servers that aren't accessible to untrusted networks, such as the Internet.</span></span>

## <a name="appofflinehtm"></a><span data-ttu-id="7aadf-380">app_offline.htm</span><span class="sxs-lookup"><span data-stu-id="7aadf-380">app_offline.htm</span></span>

<span data-ttu-id="7aadf-381">응용 프로그램의 루트 디렉터리에서 이름이 *app_offline.htm*인 파일이 검색되면 ASP.NET Core 모듈은 앱을 자동으로 종료하고 들어오는 요청 처리를 중지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-381">If a file with the name *app_offline.htm* is detected in the root directory of an app, the ASP.NET Core Module attempts to gracefully shutdown the app and stop processing incoming requests.</span></span> <span data-ttu-id="7aadf-382">`shutdownTimeLimit`에 정의된 시간(초) 후에도 앱이 계속 실행되면 ASP.NET Core 모듈은 실행 중인 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-382">If the app is still running after the number of seconds defined in `shutdownTimeLimit`, the ASP.NET Core Module kills the running process.</span></span>

<span data-ttu-id="7aadf-383">*app_offline.htm* 파일이 있는 동안 ASP.NET Core 모듈은 *app_offline.htm* 파일의 콘텐츠를 다시 보내 요청에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-383">While the *app_offline.htm* file is present, the ASP.NET Core Module responds to requests by sending back the contents of the *app_offline.htm* file.</span></span> <span data-ttu-id="7aadf-384">*app_offline.htm* 파일이 제거되면 다음 요청이 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-384">When the *app_offline.htm* file is removed, the next request starts the app.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="7aadf-385">Out-of-Process 호스팅 모델을 사용할 때 열린 연결이 있으면 앱이 즉시 종료되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-385">When using the out-of-process hosting model, the app might not shut down immediately if there's an open connection.</span></span> <span data-ttu-id="7aadf-386">예를 들어, WebSocket 연결은 앱 종료를 지연시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-386">For example, a websocket connection may delay app shut down.</span></span>

::: moniker-end

## <a name="start-up-error-page"></a><span data-ttu-id="7aadf-387">시작 오류 페이지</span><span class="sxs-lookup"><span data-stu-id="7aadf-387">Start-up error page</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="7aadf-388">In process 및 out of process 호스팅은 모두 앱을 시작하지 못할 때 사용자 지정 오류 페이지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-388">Both in-process and out-of-process hosting produce custom error pages when they fail to start the app.</span></span>

<span data-ttu-id="7aadf-389">ASP.NET Core 모듈이 in-process 또는 out-of-process 요청 처리기를 찾지 못하면 *500.0 - In-Process/Out-of-process 처리기 로드 실패* 상태 코드 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-389">If the ASP.NET Core Module fails to find either the in-process or out-of-process request handler, a *500.0 - In-Process/Out-Of-Process Handler Load Failure* status code page appears.</span></span>

<span data-ttu-id="7aadf-390">in-process 호스팅의 경우 ASP.NET Core 모듈이 앱을 시작하지 못하면 *500.30 - 시작 실패* 상태 코드 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-390">For in-process hosting if the ASP.NET Core Module fails to start the app, a *500.30 - Start Failure* status code page appears.</span></span>

<span data-ttu-id="7aadf-391">out-of-process 호스팅의 경우 ASP.NET Core 모듈이 백 엔드 프로세스를 시작하지 못하거나 백 엔드 프로세스가 시작되지만 구성된 포트에서 수신 대기하지 못하면 *502.5 - 프로세스 실패* 상태 코드 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-391">For out-of-process hosting if the ASP.NET Core Module fails to launch the backend process or the backend process starts but fails to listen on the configured port, a *502.5 - Process Failure* status code page appears.</span></span>

<span data-ttu-id="7aadf-392">이 페이지를 표시하지 않고 기본 IIS 5xx 상태 코드 페이지로 되돌리려면 `disableStartUpErrorPage` 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-392">To suppress this page and revert to the default IIS 5xx status code page, use the `disableStartUpErrorPage` attribute.</span></span> <span data-ttu-id="7aadf-393">사용자 지정 오류 메시지 구성에 대한 자세한 내용은 [HTTP 오류 \<httpErrors>](/iis/configuration/system.webServer/httpErrors/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7aadf-393">For more information on configuring custom error messages, see [HTTP Errors \<httpErrors>](/iis/configuration/system.webServer/httpErrors/).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="7aadf-394">ASP.NET Core 모듈이 백 엔드 프로세스를 시작하지 못하거나 백 엔드 프로세스가 시작되지만 구성된 포트에서 수신 대기하지 못하면 *502.5 - 프로세스 실패* 상태 코드 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-394">If the ASP.NET Core Module fails to launch the backend process or the backend process starts but fails to listen on the configured port, a *502.5 - Process Failure* status code page appears.</span></span> <span data-ttu-id="7aadf-395">이 페이지를 표시하지 않고 기본 IIS 502 상태 코드 페이지로 되돌리려면 `disableStartUpErrorPage` 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-395">To suppress this page and revert to the default IIS 502 status code page, use the `disableStartUpErrorPage` attribute.</span></span> <span data-ttu-id="7aadf-396">사용자 지정 오류 메시지 구성에 대한 자세한 내용은 [HTTP 오류 \<httpErrors>](/iis/configuration/system.webServer/httpErrors/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7aadf-396">For more information on configuring custom error messages, see [HTTP Errors \<httpErrors>](/iis/configuration/system.webServer/httpErrors/).</span></span>

![502.5 프로세스 실패 상태 코드 페이지](aspnet-core-module/_static/ANCM-502_5.png)

::: moniker-end

## <a name="log-creation-and-redirection"></a><span data-ttu-id="7aadf-398">로그 만들기 및 리디렉션</span><span class="sxs-lookup"><span data-stu-id="7aadf-398">Log creation and redirection</span></span>

<span data-ttu-id="7aadf-399">ASP.NET Core 모듈은 `aspNetCore` 요소의 `stdoutLogEnabled` 및 `stdoutLogFile` 특성이 설정된 경우 stdout 및 stderr 콘솔 출력을 디스크로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-399">The ASP.NET Core Module redirects stdout and stderr console output to disk if the `stdoutLogEnabled` and `stdoutLogFile` attributes of the `aspNetCore` element are set.</span></span> <span data-ttu-id="7aadf-400">`stdoutLogFile` 경로의 모든 폴더는 로그 파일을 만들 때 모듈에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-400">Any folders in the `stdoutLogFile` path are created by the module when the log file is created.</span></span> <span data-ttu-id="7aadf-401">앱 풀에는 로그가 기록될 위치에 쓰기 권한이 있어야 합니다(`IIS AppPool\<app_pool_name>`을 사용하여 쓰기 권한 제공).</span><span class="sxs-lookup"><span data-stu-id="7aadf-401">The app pool must have write access to the location where the logs are written (use `IIS AppPool\<app_pool_name>` to provide write permission).</span></span>

<span data-ttu-id="7aadf-402">프로세스 재생/다시 시작이 발생하지 않는 한 로그는 회전되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-402">Logs aren't rotated, unless process recycling/restart occurs.</span></span> <span data-ttu-id="7aadf-403">로그에서 사용하는 디스크 공간을 제한하는 것은 호스터의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-403">It's the responsibility of the hoster to limit the disk space the logs consume.</span></span>

<span data-ttu-id="7aadf-404">stdout 로그는 앱 시작 문제를 해결하는 경우에만 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-404">Using the stdout log is only recommended for troubleshooting app startup issues.</span></span> <span data-ttu-id="7aadf-405">일반 앱 로깅을 위해 stdout 로그를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7aadf-405">Don't use the stdout log for general app logging purposes.</span></span> <span data-ttu-id="7aadf-406">ASP.NET Core 앱의 루틴 로깅에는 로그 파일 크기를 제한하고 로그를 회전하는 로깅 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-406">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="7aadf-407">자세한 내용은 [타사 로깅 공급자](xref:fundamentals/logging/index#third-party-logging-providers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7aadf-407">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

<span data-ttu-id="7aadf-408">로그 파일이 만들어질 때 타임스탬프 및 파일 확장명이 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-408">A timestamp and file extension are added automatically when the log file is created.</span></span> <span data-ttu-id="7aadf-409">로그 파일 이름은 타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)을 밑줄로 구분된 `stdoutLogFile` 경로의 마지막 세그먼트(일반적으로 *stdout*)에 추가하여 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-409">The log file name is composed by appending the timestamp, process ID, and file extension (*.log*) to the last segment of the `stdoutLogFile` path (typically *stdout*) delimited by underscores.</span></span> <span data-ttu-id="7aadf-410">`stdoutLogFile` 경로가 *stdout*으로 끝나는 경우 2018년 2월 5일 19시 42분 32초에 만들어진 PID 1934를 사용하는 앱에 대한 로그의 파일 이름은 *stdout_20180205194132_1934.log*입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-410">If the `stdoutLogFile` path ends with *stdout*, a log for an app with a PID of 1934 created on 2/5/2018 at 19:42:32 has the file name *stdout_20180205194132_1934.log*.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="7aadf-411">`stdoutLogEnabled`가 false이면 앱 시작 시 발생하는 오류가 캡처되어 최대 30KB의 이벤트 로그로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-411">If `stdoutLogEnabled` is false, errors that occur on app startup are captured and emitted to the event log up to 30 KB.</span></span> <span data-ttu-id="7aadf-412">시작 후에는 모든 추가 로그가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-412">After startup, all additional logs are discarded.</span></span>

::: moniker-end

<span data-ttu-id="7aadf-413">다음 샘플 `aspNetCore` 요소는 Azure App Service에서 호스트되는 앱에 대한 stdout 로깅을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-413">The following sample `aspNetCore` element configures stdout logging for an app hosted in Azure App Service.</span></span> <span data-ttu-id="7aadf-414">로컬 로깅에는 로컬 경로 또는 네트워크 공유 경로가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-414">A local path or network share path is acceptable for local logging.</span></span> <span data-ttu-id="7aadf-415">AppPool 사용자 ID에 제공된 경로에 쓸 수 있는 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-415">Confirm that the AppPool user identity has permission to write to the path provided.</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="true"
    stdoutLogFile="\\?\%home%\LogFiles\stdout"
    hostingModel="InProcess">
</aspNetCore>
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="true"
    stdoutLogFile="\\?\%home%\LogFiles\stdout">
</aspNetCore>
```

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

## <a name="enhanced-diagnostic-logs"></a><span data-ttu-id="7aadf-416">개선된 진단 로그</span><span class="sxs-lookup"><span data-stu-id="7aadf-416">Enhanced diagnostic logs</span></span>

<span data-ttu-id="7aadf-417">ASP.NET Core 모듈은 개선된 진단 로그를 제공하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-417">The ASP.NET Core Module is configurable to provide enhanced diagnostics logs.</span></span> <span data-ttu-id="7aadf-418">*web.config*의 `<aspNetCore>` 요소에 `<handlerSettings>` 요소를 추가합니다. `debugLevel`을 `TRACE`으로 설정하면 진단 정보의 충실도가 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-418">Add the `<handlerSettings>` element to the `<aspNetCore>` element in *web.config*. Setting the `debugLevel` to `TRACE` exposes a higher fidelity of diagnostic information:</span></span>

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="false"
    stdoutLogFile="\\?\%home%\LogFiles\stdout"
    hostingModel="InProcess">
  <handlerSettings>
    <handlerSetting name="debugFile" value="aspnetcore-debug.log" />
    <handlerSetting name="debugLevel" value="FILE,TRACE" />
  </handlerSettings>
</aspNetCore>
```

<span data-ttu-id="7aadf-419">디버그 수준 (`debugLevel`) 값은 수준과 위치를 모두 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-419">Debug level (`debugLevel`) values can include both the level and the location.</span></span>

<span data-ttu-id="7aadf-420">수준(최소한에서 가장 자세한 정보까지 순서대로 ):</span><span class="sxs-lookup"><span data-stu-id="7aadf-420">Levels (in order from least to most verbose):</span></span>

* <span data-ttu-id="7aadf-421">오류</span><span class="sxs-lookup"><span data-stu-id="7aadf-421">ERROR</span></span>
* <span data-ttu-id="7aadf-422">경고</span><span class="sxs-lookup"><span data-stu-id="7aadf-422">WARNING</span></span>
* <span data-ttu-id="7aadf-423">정보</span><span class="sxs-lookup"><span data-stu-id="7aadf-423">INFO</span></span>
* <span data-ttu-id="7aadf-424">TRACE</span><span class="sxs-lookup"><span data-stu-id="7aadf-424">TRACE</span></span>

<span data-ttu-id="7aadf-425">위치(여러 위치가 허용됨):</span><span class="sxs-lookup"><span data-stu-id="7aadf-425">Locations (multiple locations are permitted):</span></span>

* <span data-ttu-id="7aadf-426">CONSOLE</span><span class="sxs-lookup"><span data-stu-id="7aadf-426">CONSOLE</span></span>
* <span data-ttu-id="7aadf-427">EVENTLOG</span><span class="sxs-lookup"><span data-stu-id="7aadf-427">EVENTLOG</span></span>
* <span data-ttu-id="7aadf-428">파일</span><span class="sxs-lookup"><span data-stu-id="7aadf-428">FILE</span></span>

<span data-ttu-id="7aadf-429">처리기 설정은 환경 변수를 통해서도 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-429">The handler settings can also be provided via environment variables:</span></span>

* <span data-ttu-id="7aadf-430">`ASPNETCORE_MODULE_DEBUG_FILE` &ndash; 디버그 로그 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-430">`ASPNETCORE_MODULE_DEBUG_FILE` &ndash; Path to the debug log file.</span></span> <span data-ttu-id="7aadf-431">(기본값: *aspnetcore-debug.log*)</span><span class="sxs-lookup"><span data-stu-id="7aadf-431">(Default: *aspnetcore-debug.log*)</span></span>
* <span data-ttu-id="7aadf-432">`ASPNETCORE_MODULE_DEBUG` &ndash; 디버그 수준 설정.</span><span class="sxs-lookup"><span data-stu-id="7aadf-432">`ASPNETCORE_MODULE_DEBUG` &ndash; Debug level setting.</span></span>

> [!WARNING]
> <span data-ttu-id="7aadf-433">배포에서 문제를 해결하는 데 필요한 시간보다 오래 디버그 로깅을 사용하도록 설정하지 **마세요**.</span><span class="sxs-lookup"><span data-stu-id="7aadf-433">Do **not** leave debug logging enabled in the deployment for longer than required to troubleshoot an issue.</span></span> <span data-ttu-id="7aadf-434">로그의 크기는 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-434">The size of the log isn't limited.</span></span> <span data-ttu-id="7aadf-435">디버그 로그를 사용하도록 설정한 대로 두면 사용 가능한 디스크 공간이 소진되어 서버 또는 앱 서비스가 크래시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-435">Leaving the debug log enabled can exhaust the available disk space and crash the server or app service.</span></span>

::: moniker-end

<span data-ttu-id="7aadf-436">*web.config* 파일에 있는 `aspNetCore` 요소의 예제에 대해서는 [web.config를 사용한 구성](#configuration-with-webconfig)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7aadf-436">See [Configuration with web.config](#configuration-with-webconfig) for an example of the `aspNetCore` element in the *web.config* file.</span></span>

## <a name="proxy-configuration-uses-http-protocol-and-a-pairing-token"></a><span data-ttu-id="7aadf-437">프록시 구성은 HTTP 프로토콜 및 페어링 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-437">Proxy configuration uses HTTP protocol and a pairing token</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="7aadf-438">*호스팅에만 적용됩니다.*</span><span class="sxs-lookup"><span data-stu-id="7aadf-438">*Only applies to out-of-process hosting.*</span></span>

::: moniker-end

<span data-ttu-id="7aadf-439">ASP.NET Core 모듈과 Kestrel 사이에 만들어진 프록시는 HTTP 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-439">The proxy created between the ASP.NET Core Module and Kestrel uses the HTTP protocol.</span></span> <span data-ttu-id="7aadf-440">HTTP 사용은 모듈과 Kestrel 간의 트래픽이 네트워크 인터페이스에서 분리된 루프백 주소에서 발생하는 성능 최적화입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-440">Using HTTP is a performance optimization, where the traffic between the module and Kestrel takes place on a loopback address off of the network interface.</span></span> <span data-ttu-id="7aadf-441">서버에서 분리된 위치에서 모듈과 Kestrel 간 트래픽 도청의 위험은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-441">There's no risk of eavesdropping the traffic between the module and Kestrel from a location off of the server.</span></span>

<span data-ttu-id="7aadf-442">페어링 토큰은 Kestrel에서 받은 요청이 IIS에서 프록시되었으며 다른 원본에서 오지 않았다는 것을 보장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-442">A pairing token is used to guarantee that the requests received by Kestrel were proxied by IIS and didn't come from some other source.</span></span> <span data-ttu-id="7aadf-443">페어링 토큰은 모듈에 의해 생성되며 환경 변수(`ASPNETCORE_TOKEN`)로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-443">The pairing token is created and set into an environment variable (`ASPNETCORE_TOKEN`) by the module.</span></span> <span data-ttu-id="7aadf-444">페어링 토큰은 프록시된 모든 요청에서 헤더(`MS-ASPNETCORE-TOKEN`)로도 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-444">The pairing token is also set into a header (`MS-ASPNETCORE-TOKEN`) on every proxied request.</span></span> <span data-ttu-id="7aadf-445">IIS 미들웨어는 수신하는 각 요청을 검사하여 페어링 토큰 헤더 값이 환경 변수 값과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-445">IIS Middleware checks each request it receives to confirm that the pairing token header value matches the environment variable value.</span></span> <span data-ttu-id="7aadf-446">토큰 값이 일치하지 않는 경우 요청이 기록되고 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-446">If the token values are mismatched, the request is logged and rejected.</span></span> <span data-ttu-id="7aadf-447">페어링 토큰 환경 변수와 모듈과 Kestrel 간의 트래픽은 서버에서 분리된 위치에서 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-447">The pairing token environment variable and the traffic between the module and Kestrel aren't accessible from a location off of the server.</span></span> <span data-ttu-id="7aadf-448">페어링 토큰 값을 알지 못하면 공격자는 IIS 미들웨어에서 검사를 무시하는 요청을 전송할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-448">Without knowing the pairing token value, an attacker can't submit requests that bypass the check in the IIS Middleware.</span></span>

## <a name="aspnet-core-module-with-an-iis-shared-configuration"></a><span data-ttu-id="7aadf-449">IIS 공유 구성이 포함된 ASP.NET Core 모듈</span><span class="sxs-lookup"><span data-stu-id="7aadf-449">ASP.NET Core Module with an IIS Shared Configuration</span></span>

<span data-ttu-id="7aadf-450">ASP.NET Core 모듈 설치 관리자는 **TrustedInstaller** 계정의 권한으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-450">The ASP.NET Core Module installer runs with the privileges of the **TrustedInstaller** account.</span></span> <span data-ttu-id="7aadf-451">로컬 시스템 계정에는 IIS 공유 구성에서 사용하는 공유 경로에 대한 수정 권한이 없으므로 공유의 *applicationHost.config*에서 모듈 설정을 구성하려고 하면 설치 관리자에서 액세스 거부 오류가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-451">Because the local system account doesn't have modify permission for the share path used by the IIS Shared Configuration, the installer throws an access denied error when attempting to configure the module settings in the *applicationHost.config* file on the share.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="7aadf-452">IIS 설치와 동일한 머신에서 IIS 공유 구성을 사용하는 경우 `OPT_NO_SHARED_CONFIG_CHECK` 매개 변수를 `1`로 설정한 상태에서 ASP.NET Core Hosting Bundle 설치 관리자를 실행합니다</span><span class="sxs-lookup"><span data-stu-id="7aadf-452">When using an IIS Shared Configuration on the same machine as the IIS installation, run the ASP.NET Core Hosting Bundle installer with the `OPT_NO_SHARED_CONFIG_CHECK` parameter set to `1`:</span></span>

```console
dotnet-hosting-{VERSION}.exe OPT_NO_SHARED_CONFIG_CHECK=1
```

<span data-ttu-id="7aadf-453">공유 구성에 대한 경로가 IIS 설치와 동일한 머신에 있지 않으면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-453">When the path to the shared configuration isn't on the same machine as the IIS installation, follow these steps:</span></span>

1. <span data-ttu-id="7aadf-454">IIS 공유 구성을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-454">Disable the IIS Shared Configuration.</span></span>
1. <span data-ttu-id="7aadf-455">설치 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-455">Run the installer.</span></span>
1. <span data-ttu-id="7aadf-456">업데이트된 *applicationHost.config* 파일을 공유로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-456">Export the updated *applicationHost.config* file to the share.</span></span>
1. <span data-ttu-id="7aadf-457">IIS 공유 구성을 다시 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-457">Re-enable the IIS Shared Configuration.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="7aadf-458">IIS 공유 구성을 사용할 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-458">When using an IIS Shared Configuration, follow these steps:</span></span>

1. <span data-ttu-id="7aadf-459">IIS 공유 구성을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-459">Disable the IIS Shared Configuration.</span></span>
1. <span data-ttu-id="7aadf-460">설치 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-460">Run the installer.</span></span>
1. <span data-ttu-id="7aadf-461">업데이트된 *applicationHost.config* 파일을 공유로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-461">Export the updated *applicationHost.config* file to the share.</span></span>
1. <span data-ttu-id="7aadf-462">IIS 공유 구성을 다시 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-462">Re-enable the IIS Shared Configuration.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

## <a name="application-initialization"></a><span data-ttu-id="7aadf-463">애플리케이션 초기화</span><span class="sxs-lookup"><span data-stu-id="7aadf-463">Application Initialization</span></span>

<span data-ttu-id="7aadf-464">[IIS 애플리케이션 초기화](/iis/get-started/whats-new-in-iis-8/iis-80-application-initialization)는 앱 풀이 시작되거나 재활용될 때 HTTP 요청을 앱으로 보내는 IIS 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-464">[IIS Application Initialization](/iis/get-started/whats-new-in-iis-8/iis-80-application-initialization) is an IIS feature that sends an HTTP request to the app when the app pool starts or is recycled.</span></span> <span data-ttu-id="7aadf-465">요청은 앱이 시작되도록 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-465">The request triggers the app to start.</span></span> <span data-ttu-id="7aadf-466">애플리케이션 초기화는 [In Process 호스팅 모델](xref:fundamentals/servers/index#in-process-hosting-model) 및 [Out of Process 호스팅 모델](xref:fundamentals/servers/index#out-of-process-hosting-model)에서 ASP.NET Core 모듈 버전 2와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-466">Application Initialization can be used by both the [in-process hosting model](xref:fundamentals/servers/index#in-process-hosting-model) and [out-of-process hosting model](xref:fundamentals/servers/index#out-of-process-hosting-model) with the ASP.NET Core Module version 2.</span></span>

<span data-ttu-id="7aadf-467">애플리케이션 초기화를 사용하도록 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-467">To enable Application Initialization:</span></span>

1. <span data-ttu-id="7aadf-468">IIS 애플리케이션 초기화 역할 기능이 사용하도록 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-468">Confirm that the IIS Application Initialization role feature in enabled:</span></span>
   * <span data-ttu-id="7aadf-469">Windows 7 이상: **제어판** > **프로그램** > **프로그램 및 기능** > **Windows 기능 Windows 기능 사용/사용 안 함**(화면 왼쪽)으로 차례로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-469">On Windows 7 or later: Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span> <span data-ttu-id="7aadf-470">**인터넷 정보 서비스** > **World Wide Web 서비스** > **애플리케이션 개발 기능**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-470">Open **Internet Information Services** > **World Wide Web Services** > **Application Development Features**.</span></span> <span data-ttu-id="7aadf-471">**애플리케이션 초기화** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-471">Select the check box for **Application Initialization**.</span></span>
   * <span data-ttu-id="7aadf-472">Windows Server 2008 R2 이상에서는 **역할 및 기능 추가 마법사**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-472">On Windows Server 2008 R2 or later, open the **Add Roles and Features Wizard**.</span></span> <span data-ttu-id="7aadf-473">**역할 서비스 선택** 패널에 도달하면 **애플리케이션 개발** 노드를 열고 **애플리케이션 초기화** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-473">When you reach the **Select role services** panel, open the **Application Development** node and select the **Application Initialization** check box.</span></span>
1. <span data-ttu-id="7aadf-474">IIS 관리자의 **연결** 패널에서 **애플리케이션 풀**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-474">In IIS Manager, select **Application Pools** in the **Connections** panel.</span></span>
1. <span data-ttu-id="7aadf-475">목록에서 앱의 앱 풀을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-475">Select the app's app pool in the list.</span></span>
1. <span data-ttu-id="7aadf-476">**작업** 패널의 **애플리케이션 풀 편집**에서 **고급 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-476">Select **Advanced Settings** under **Edit Application Pool** in the **Actions** panel.</span></span>
1. <span data-ttu-id="7aadf-477">**시작 모드**를 **AlwaysRunning**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-477">Set **Start Mode** to **AlwaysRunning**.</span></span>
1. <span data-ttu-id="7aadf-478">**연결** 패널에서 **사이트** 노드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-478">Open the **Sites** node in the **Connections** panel.</span></span>
1. <span data-ttu-id="7aadf-479">앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-479">Select the app.</span></span>
1. <span data-ttu-id="7aadf-480">**작업** 패널의 **웹 사이트 관리**에서 **고급 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-480">Select **Advanced Settings** under **Manage Website** in the **Actions** panel.</span></span>
1. <span data-ttu-id="7aadf-481">**미리 로드 사용**을 **True**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-481">Set **Preload Enabled** to **True**.</span></span>

<span data-ttu-id="7aadf-482">자세한 내용은 [IIS 8.0 애플리케이션 초기화](/iis/get-started/whats-new-in-iis-8/iis-80-application-initialization)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7aadf-482">For more information, see [IIS 8.0 Application Initialization](/iis/get-started/whats-new-in-iis-8/iis-80-application-initialization).</span></span>

<span data-ttu-id="7aadf-483">[Out of Process 호스팅 모델](xref:fundamentals/servers/index#out-of-process-hosting-model)을 사용하는 앱은 외부 서비스를 사용하여 앱을 계속 실행하기 위해 앱을 주기적으로 ping해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-483">Apps that use the [out-of-process hosting model](xref:fundamentals/servers/index#out-of-process-hosting-model) must use an external service to periodically ping the app in order to keep it running.</span></span>

::: moniker-end

## <a name="module-version-and-hosting-bundle-installer-logs"></a><span data-ttu-id="7aadf-484">모듈 버전 및 호스팅 번들 설치 관리자 로그</span><span class="sxs-lookup"><span data-stu-id="7aadf-484">Module version and Hosting Bundle installer logs</span></span>

<span data-ttu-id="7aadf-485">설치된 ASP.NET Core 모듈의 버전을 확인하려면:</span><span class="sxs-lookup"><span data-stu-id="7aadf-485">To determine the version of the installed ASP.NET Core Module:</span></span>

1. <span data-ttu-id="7aadf-486">호스팅 시스템에서 *%windir%\System32\inetsrv*로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-486">On the hosting system, navigate to *%windir%\System32\inetsrv*.</span></span>
1. <span data-ttu-id="7aadf-487">*aspnetcore.dll* 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-487">Locate the *aspnetcore.dll* file.</span></span>
1. <span data-ttu-id="7aadf-488">파일을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-488">Right-click the file and select **Properties** from the contextual menu.</span></span>
1. <span data-ttu-id="7aadf-489">**세부 정보** 탭을 선택합니다. **파일 버전** 및 **제품 버전**은 설치된 모듈 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-489">Select the **Details** tab. The **File version** and **Product version** represent the installed version of the module.</span></span>

<span data-ttu-id="7aadf-490">모듈에 대한 호스팅 번들 설치 관리자 로그는 *C:\\Users\\%UserName%\\AppData\\Local\\Temp*에 있습니다. 파일 이름은 *dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log*로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-490">The Hosting Bundle installer logs for the module are found at *C:\\Users\\%UserName%\\AppData\\Local\\Temp*. The file is named *dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log*.</span></span>

## <a name="module-schema-and-configuration-file-locations"></a><span data-ttu-id="7aadf-491">모듈, 스키마 및 구성 파일 위치</span><span class="sxs-lookup"><span data-stu-id="7aadf-491">Module, schema, and configuration file locations</span></span>

### <a name="module"></a><span data-ttu-id="7aadf-492">Module</span><span class="sxs-lookup"><span data-stu-id="7aadf-492">Module</span></span>

<span data-ttu-id="7aadf-493">**IIS(x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="7aadf-493">**IIS (x86/amd64):**</span></span>

   * <span data-ttu-id="7aadf-494">%windir%\System32\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="7aadf-494">%windir%\System32\inetsrv\aspnetcore.dll</span></span>

   * <span data-ttu-id="7aadf-495">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="7aadf-495">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="7aadf-496">%ProgramFiles%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="7aadf-496">%ProgramFiles%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

   * <span data-ttu-id="7aadf-497">%ProgramFiles(x86)%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="7aadf-497">%ProgramFiles(x86)%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

::: moniker-end

<span data-ttu-id="7aadf-498">**IIS Express(x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="7aadf-498">**IIS Express (x86/amd64):**</span></span>

   * <span data-ttu-id="7aadf-499">%ProgramFiles%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="7aadf-499">%ProgramFiles%\IIS Express\aspnetcore.dll</span></span>

   * <span data-ttu-id="7aadf-500">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="7aadf-500">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="7aadf-501">%ProgramFiles%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="7aadf-501">%ProgramFiles%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

   * <span data-ttu-id="7aadf-502">%ProgramFiles(x86)%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="7aadf-502">%ProgramFiles(x86)%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

::: moniker-end

### <a name="schema"></a><span data-ttu-id="7aadf-503">스키마</span><span class="sxs-lookup"><span data-stu-id="7aadf-503">Schema</span></span>

<span data-ttu-id="7aadf-504">**IIS**</span><span class="sxs-lookup"><span data-stu-id="7aadf-504">**IIS**</span></span>

   * <span data-ttu-id="7aadf-505">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="7aadf-505">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="7aadf-506">%windir%\System32\inetsrv\config\schema\aspnetcore_schema_v2.xml</span><span class="sxs-lookup"><span data-stu-id="7aadf-506">%windir%\System32\inetsrv\config\schema\aspnetcore_schema_v2.xml</span></span>

::: moniker-end
<span data-ttu-id="7aadf-507">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="7aadf-507">**IIS Express**</span></span>

   * <span data-ttu-id="7aadf-508">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="7aadf-508">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="7aadf-509">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema_v2.xml</span><span class="sxs-lookup"><span data-stu-id="7aadf-509">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema_v2.xml</span></span>

::: moniker-end

### <a name="configuration"></a><span data-ttu-id="7aadf-510">구성하기</span><span class="sxs-lookup"><span data-stu-id="7aadf-510">Configuration</span></span>

<span data-ttu-id="7aadf-511">**IIS**</span><span class="sxs-lookup"><span data-stu-id="7aadf-511">**IIS**</span></span>

   * <span data-ttu-id="7aadf-512">%windir%\System32\inetsrv\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="7aadf-512">%windir%\System32\inetsrv\config\applicationHost.config</span></span>

<span data-ttu-id="7aadf-513">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="7aadf-513">**IIS Express**</span></span>

   * <span data-ttu-id="7aadf-514">Visual Studio: {APPLICATION ROOT}\\.vs\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="7aadf-514">Visual Studio: {APPLICATION ROOT}\\.vs\config\applicationHost.config</span></span>
   
   * <span data-ttu-id="7aadf-515">*iisexpress.exe* CLI: %USERPROFILE%\Documents\IISExpress\config\applicationhost.config</span><span class="sxs-lookup"><span data-stu-id="7aadf-515">*iisexpress.exe* CLI: %USERPROFILE%\Documents\IISExpress\config\applicationhost.config</span></span>

<span data-ttu-id="7aadf-516">*applicationHost.config* 파일에서 *aspnetcore*를 검색하여 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aadf-516">The files can be found by searching for *aspnetcore* in the *applicationHost.config* file.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7aadf-517">추가 자료</span><span class="sxs-lookup"><span data-stu-id="7aadf-517">Additional resources</span></span>

* <xref:host-and-deploy/iis/index>
* [<span data-ttu-id="7aadf-518">ASP.NET Core 모듈 GitHub 리포지토리(참조 소스)</span><span class="sxs-lookup"><span data-stu-id="7aadf-518">ASP.NET Core Module GitHub repository (reference source)</span></span>](https://github.com/aspnet/AspNetCoreModule)
* <xref:host-and-deploy/iis/modules>
