---
title: ASP.NET Core 1.x에서 2.0으로 마이그레이션
author: scottaddie
description: 이 문서에서는 ASP.NET Core 1.x 프로젝트에서 ASP.NET Core 2.0으로 마이그레이션하기 위한 필수 구성 요소 및 일반적인 단계를 설명합니다.
ms.author: scaddie
ms.custom: mvc
ms.date: 10/24/2018
uid: migration/1x-to-2x/index
---
# <a name="migrate-from-aspnet-core-1x-to-20"></a><span data-ttu-id="ceb7a-103">ASP.NET Core 1.x에서 2.0으로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="ceb7a-103">Migrate from ASP.NET Core 1.x to 2.0</span></span>

<span data-ttu-id="ceb7a-104">작성자: [Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="ceb7a-104">By [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="ceb7a-105">이 문서에서는 기존 ASP.NET Core 1.x 프로젝트를 ASP.NET Core 2.0으로 업데이트하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-105">In this article, we walk you through updating an existing ASP.NET Core 1.x project to ASP.NET Core 2.0.</span></span> <span data-ttu-id="ceb7a-106">애플리케이션을 ASP.NET Core 2.0으로 마이그레이션하면 [여러 가지 새로운 기능 및 향상된 성능](xref:aspnetcore-2.0)을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-106">Migrating your application to ASP.NET Core 2.0 enables you to take advantage of [many new features and performance improvements](xref:aspnetcore-2.0).</span></span>

<span data-ttu-id="ceb7a-107">기존 ASP.NET Core 1.x 애플리케이션은 버전별 프로젝트 템플릿을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-107">Existing ASP.NET Core 1.x applications are based off of version-specific project templates.</span></span> <span data-ttu-id="ceb7a-108">ASP.NET Core 프레임워크가 진화함에 따라 프로젝트 템플릿 및 포함된 시작 코드도 함께 진화합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-108">As the ASP.NET Core framework evolves, so do the project templates and the starter code contained within them.</span></span> <span data-ttu-id="ceb7a-109">ASP.NET Core 프레임워크를 업데이트하는 것 외에도 애플리케이션에 대한 코드를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-109">In addition to updating the ASP.NET Core framework, you need to update the code for your application.</span></span>

<a name="prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="ceb7a-110">전제 조건</span><span class="sxs-lookup"><span data-stu-id="ceb7a-110">Prerequisites</span></span>

<span data-ttu-id="ceb7a-111">[ASP.NET Core 시작](xref:getting-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-111">See [Get Started with ASP.NET Core](xref:getting-started).</span></span>

<a name="tfm"></a>

## <a name="update-target-framework-moniker-tfm"></a><span data-ttu-id="ceb7a-112">TFM(대상 프레임워크 모니커) 업데이트</span><span class="sxs-lookup"><span data-stu-id="ceb7a-112">Update Target Framework Moniker (TFM)</span></span>

<span data-ttu-id="ceb7a-113">.NET Core를 대상으로 하는 프로젝트는 .NET Core 2.0보다 크거나 같은 버전의 [TFM](/dotnet/standard/frameworks#referring-to-frameworks)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-113">Projects targeting .NET Core should use the [TFM](/dotnet/standard/frameworks#referring-to-frameworks) of a version greater than or equal to .NET Core 2.0.</span></span> <span data-ttu-id="ceb7a-114">*.csproj* 파일에서 `<TargetFramework>` 노드를 검색하고 해당 내부 텍스트를 `netcoreapp2.0`으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-114">Search for the `<TargetFramework>` node in the *.csproj* file, and replace its inner text with `netcoreapp2.0`:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App.csproj?range=3)]

<span data-ttu-id="ceb7a-115">.NET Framework를 대상으로 하는 프로젝트는 .NET Framework 4.6.1보다 크거나 같은 버전의 TFM을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-115">Projects targeting .NET Framework should use the TFM of a version greater than or equal to .NET Framework 4.6.1.</span></span> <span data-ttu-id="ceb7a-116">*.csproj* 파일에서 `<TargetFramework>` 노드를 검색하고 해당 내부 텍스트를 `net461`로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-116">Search for the `<TargetFramework>` node in the *.csproj* file, and replace its inner text with `net461`:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App.csproj?range=4)]

> [!NOTE]
> <span data-ttu-id="ceb7a-117">.NET Core 2.0은 .NET Core 1.x보다 훨씬 더 큰 노출 영역을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-117">.NET Core 2.0 offers a much larger surface area than .NET Core 1.x.</span></span> <span data-ttu-id="ceb7a-118">.NET Core 1.x에 API가 없기 때문에 전적으로 .NET Framework를 대상으로 하는 경우 .NET Core 2.0을 대상으로 하는 것은 작동할 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-118">If you're targeting .NET Framework solely because of missing APIs in .NET Core 1.x, targeting .NET Core 2.0 is likely to work.</span></span>

<a name="global-json"></a>

## <a name="update-net-core-sdk-version-in-globaljson"></a><span data-ttu-id="ceb7a-119">global.json에서 .NET Core SDK 버전 업데이트</span><span class="sxs-lookup"><span data-stu-id="ceb7a-119">Update .NET Core SDK version in global.json</span></span>

<span data-ttu-id="ceb7a-120">솔루션이 특정 .NET Core SDK 버전을 대상으로 하기 위해 [*global.json*](/dotnet/core/tools/global-json) 파일에 의존하는 경우 해당 `version` 속성을 컴퓨터에 설치된 2.0 버전을 사용하도록 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-120">If your solution relies upon a [*global.json*](/dotnet/core/tools/global-json) file to target a specific .NET Core SDK version, update its `version` property to use the 2.0 version installed on your machine:</span></span>

[!code-json[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/global.json?highlight=3)]

<a name="package-reference"></a>

## <a name="update-package-references"></a><span data-ttu-id="ceb7a-121">패키지 참조 업데이트</span><span class="sxs-lookup"><span data-stu-id="ceb7a-121">Update package references</span></span>

<span data-ttu-id="ceb7a-122">1.x 프로젝트에서 *.csproj* 파일은 프로젝트에서 사용하는 각 NuGet 패키지를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-122">The *.csproj* file in a 1.x project lists each NuGet package used by the project.</span></span>

<span data-ttu-id="ceb7a-123">.NET Core 2.0을 대상으로 하는 ASP.NET Core 2.0 프로젝트에서 *.csproj* 파일의 단일 [metapackage](xref:fundamentals/metapackage) 참조는 패키지의 컬렉션을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-123">In an ASP.NET Core 2.0 project targeting .NET Core 2.0, a single [metapackage](xref:fundamentals/metapackage) reference in the *.csproj* file replaces the collection of packages:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App.csproj?range=8-10)]

<span data-ttu-id="ceb7a-124">ASP.NET Core 2.0 및 Entity Framework Core 2.0의 모든 기능은 metapackage에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-124">All the features of ASP.NET Core 2.0 and Entity Framework Core 2.0 are included in the metapackage.</span></span>

<span data-ttu-id="ceb7a-125">.NET Framework를 대상으로 하는 ASP.NET Core 2.0 프로젝트는 계속해서 개별 NuGet 패키지를 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-125">ASP.NET Core 2.0 projects targeting .NET Framework should continue to reference individual NuGet packages.</span></span> <span data-ttu-id="ceb7a-126">각 `<PackageReference />` 노드의 `Version` 특성을 2.0.0으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-126">Update the `Version` attribute of each `<PackageReference />` node to 2.0.0.</span></span>

<span data-ttu-id="ceb7a-127">예를 들어 다음은 .NET Framework를 대상으로 하는 일반적인 ASP.NET Core 2.0 프로젝트에 사용되는 `<PackageReference />` 노드의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-127">For example, here's the list of `<PackageReference />` nodes used in a typical ASP.NET Core 2.0 project targeting .NET Framework:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App.csproj?range=9-22)]

<a name="dot-net-cli-tool-reference"></a>

## <a name="update-net-core-cli-tools"></a><span data-ttu-id="ceb7a-128">.NET Core CLI 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="ceb7a-128">Update .NET Core CLI tools</span></span>

<span data-ttu-id="ceb7a-129">*.csproj* 파일에서 각 `<DotNetCliToolReference />` 노드의 `Version` 특성을 2.0.0으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-129">In the *.csproj* file, update the `Version` attribute of each `<DotNetCliToolReference />` node to 2.0.0.</span></span>

<span data-ttu-id="ceb7a-130">예를 들어 다음은 .NET Core 2.0을 대상으로 하는 일반적인 ASP.NET Core 2.0 프로젝트에 사용되는 CLI 도구의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-130">For example, here's the list of CLI tools used in a typical ASP.NET Core 2.0 project targeting .NET Core 2.0:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App.csproj?range=12-16)]

<a name="package-target-fallback"></a>

## <a name="rename-package-target-fallback-property"></a><span data-ttu-id="ceb7a-131">패키지 대상 대체 속성의 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="ceb7a-131">Rename Package Target Fallback property</span></span>

<span data-ttu-id="ceb7a-132">`PackageTargetFallback` 노드 및 변수에서 사용되는 1.x 프로젝트의 *.csproj* 파일:</span><span class="sxs-lookup"><span data-stu-id="ceb7a-132">The *.csproj* file of a 1.x project used a `PackageTargetFallback` node and variable:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App.csproj?range=5)]

<span data-ttu-id="ceb7a-133">노드 및 변수의 이름을 모두 `AssetTargetFallback`으로 바꾸기:</span><span class="sxs-lookup"><span data-stu-id="ceb7a-133">Rename both the node and variable to `AssetTargetFallback`:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App.csproj?range=4)]

<a name="program-cs"></a>

## <a name="update-main-method-in-programcs"></a><span data-ttu-id="ceb7a-134">Program.cs의 Main 메서드 업데이트</span><span class="sxs-lookup"><span data-stu-id="ceb7a-134">Update Main method in Program.cs</span></span>

<span data-ttu-id="ceb7a-135">1.x 프로젝트에서 *Program.cs*의 `Main` 메서드는 다음과 같았습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-135">In 1.x projects, the `Main` method of *Program.cs* looked like this:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Program.cs?name=snippet_ProgramCs&highlight=8-19)]

<span data-ttu-id="ceb7a-136">2.0 프로젝트에서 *Program.cs*의 `Main` 메서드는 간소화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-136">In 2.0 projects, the `Main` method of *Program.cs* has been simplified:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Program.cs?highlight=8-11)]

<span data-ttu-id="ceb7a-137">이 새로운 2.0 패턴의 도입은 적극 권장되며 [EF(Entity Framework) Core 마이그레이션](xref:data/ef-mvc/migrations)과 같은 제품 기능을 작동하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-137">The adoption of this new 2.0 pattern is highly recommended and is required for product features like [Entity Framework (EF) Core Migrations](xref:data/ef-mvc/migrations) to work.</span></span> <span data-ttu-id="ceb7a-138">예를 들어 패키지 관리자 콘솔 창에서 `Update-Database` 또는 명령줄(ASP.NET Core 2.0으로 변환되는 프로젝트에서)에서 `dotnet ef database update` 실행은 다음 오류를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-138">For example, running `Update-Database` from the Package Manager Console window or `dotnet ef database update` from the command line (on projects converted to ASP.NET Core 2.0) generates the following error:</span></span>

```
Unable to create an object of type '<Context>'. Add an implementation of 'IDesignTimeDbContextFactory<Context>' to the project, or see https://go.microsoft.com/fwlink/?linkid=851728 for additional patterns supported at design time.
```

<a name="add-modify-configuration"></a>

## <a name="add-configuration-providers"></a><span data-ttu-id="ceb7a-139">구성 공급자 추가</span><span class="sxs-lookup"><span data-stu-id="ceb7a-139">Add configuration providers</span></span>

<span data-ttu-id="ceb7a-140">1.x 프로젝트에서는 `Startup` 생성자를 통해 앱에 구성 공급자를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-140">In 1.x projects, adding configuration providers to an app was accomplished via the `Startup` constructor.</span></span> <span data-ttu-id="ceb7a-141">이 단계에는 `ConfigurationBuilder`의 인스턴스 만들기, 해당 공급자(환경 변수, 앱 설정 등) 로드 및 `IConfigurationRoot`의 멤버 초기화와 같은 작업이 포함되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-141">The steps involved creating an instance of `ConfigurationBuilder`, loading applicable providers (environment variables, app settings, etc.), and initializing a member of `IConfigurationRoot`.</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Startup.cs?name=snippet_1xStartup)]

<span data-ttu-id="ceb7a-142">위의 예제에서는 `IHostingEnvironment.EnvironmentName` 속성과 일치하는 *appsettings.\<EnvironmentName\>.json* 파일뿐만 아니라 *appsettings.json*의 구성 설정을 사용하여 `Configuration` 멤버를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-142">The preceding example loads the `Configuration` member with configuration settings from *appsettings.json* as well as any *appsettings.\<EnvironmentName\>.json* file matching the `IHostingEnvironment.EnvironmentName` property.</span></span> <span data-ttu-id="ceb7a-143">이러한 파일의 위치는 *Startup.cs*와 동일한 경로에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-143">The location of these files is at the same path as *Startup.cs*.</span></span>

<span data-ttu-id="ceb7a-144">2.0 프로젝트에서 1.x 프로젝트에 포함된 기본 구성 코드는 백그라운드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-144">In 2.0 projects, the boilerplate configuration code inherent to 1.x projects runs behind-the-scenes.</span></span> <span data-ttu-id="ceb7a-145">예를 들어 환경 변수 및 앱 설정은 시작 시 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-145">For example, environment variables and app settings are loaded at startup.</span></span> <span data-ttu-id="ceb7a-146">동일한 *Startup.cs* 코드는 삽입된 인스턴스를 사용하여 `IConfiguration` 초기화로 축소됩니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-146">The equivalent *Startup.cs* code is reduced to `IConfiguration` initialization with the injected instance:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App/Startup.cs?name=snippet_2xStartup)]

<span data-ttu-id="ceb7a-147">`WebHostBuilder.CreateDefaultBuilder`를 추가하여 기본 공급자를 제거하려면 `ConfigureAppConfiguration` 내부의 `IConfigurationBuilder.Sources` 속성에서 `Clear` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-147">To remove the default providers added by `WebHostBuilder.CreateDefaultBuilder`, invoke the `Clear` method on the `IConfigurationBuilder.Sources` property inside of `ConfigureAppConfiguration`.</span></span> <span data-ttu-id="ceb7a-148">다시 공급자를 추가하려면 *Program.cs*에서 `ConfigureAppConfiguration` 메서드를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-148">To add providers back, utilize the `ConfigureAppConfiguration` method in *Program.cs*:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App/Program.cs?name=snippet_ProgramMainConfigProviders&highlight=9-14)]

<span data-ttu-id="ceb7a-149">이전 코드 조각의 `CreateDefaultBuilder` 메서드에서 사용하는 구성은 [여기](https://github.com/aspnet/MetaPackages/blob/rel/2.0.0/src/Microsoft.AspNetCore/WebHost.cs#L152)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-149">The configuration used by the `CreateDefaultBuilder` method in the preceding code snippet can be seen [here](https://github.com/aspnet/MetaPackages/blob/rel/2.0.0/src/Microsoft.AspNetCore/WebHost.cs#L152).</span></span>

<span data-ttu-id="ceb7a-150">자세한 내용은 [ASP.NET Core의 구성](xref:fundamentals/configuration/index)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-150">For more information, see [Configuration in ASP.NET Core](xref:fundamentals/configuration/index).</span></span>

<a name="db-init-code"></a>

## <a name="move-database-initialization-code"></a><span data-ttu-id="ceb7a-151">데이터베이스 초기화 코드 이동</span><span class="sxs-lookup"><span data-stu-id="ceb7a-151">Move database initialization code</span></span>

<span data-ttu-id="ceb7a-152">EF Core 1.x를 사용하는 1.x 프로젝트에서 `dotnet ef migrations add`와 같은 명령은 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-152">In 1.x projects using EF Core 1.x, a command such as `dotnet ef migrations add` does the following:</span></span>

1. <span data-ttu-id="ceb7a-153">`Startup` 인스턴스를 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-153">Instantiates a `Startup` instance</span></span>
1. <span data-ttu-id="ceb7a-154">`ConfigureServices` 메서드를 호출하여 종속성 주입을 통해 모든 서비스를 등록합니다(`DbContext` 형식 포함).</span><span class="sxs-lookup"><span data-stu-id="ceb7a-154">Invokes the `ConfigureServices` method to register all services with dependency injection (including `DbContext` types)</span></span>
1. <span data-ttu-id="ceb7a-155">필수 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-155">Performs its requisite tasks</span></span>

<span data-ttu-id="ceb7a-156">EF Core 2.0을 사용하는 2.0 프로젝트에서는 애플리케이션 서비스를 가져오기 위해 `Program.BuildWebHost`가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-156">In 2.0 projects using EF Core 2.0, `Program.BuildWebHost` is invoked to obtain the application services.</span></span> <span data-ttu-id="ceb7a-157">1.x와 달리 2.0 프로젝트에서는 `Startup.Configure`를 호출하는 데 부작용이 추가로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-157">Unlike 1.x, this has the additional side effect of invoking `Startup.Configure`.</span></span> <span data-ttu-id="ceb7a-158">1.x 앱이 `Configure` 메서드에서 데이터베이스 초기화 코드를 호출한 경우 예기치 않은 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-158">If your 1.x app invoked database initialization code in its `Configure` method, unexpected problems can occur.</span></span> <span data-ttu-id="ceb7a-159">예를 들어 데이터베이스가 아직 없는 경우 EF Core 마이그레이션 명령 실행 전에 시드 코드가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-159">For example, if the database doesn't yet exist, the seeding code runs before the EF Core Migrations command execution.</span></span> <span data-ttu-id="ceb7a-160">아직 데이터베이스가 없는 경우 이 문제가 `dotnet ef migrations list` 명령 실패의 원인이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-160">This problem causes a `dotnet ef migrations list` command to fail if the database doesn't yet exist.</span></span>

<span data-ttu-id="ceb7a-161">*Startup.cs*의 `Configure` 메서드에서 다음 1.x 시드 초기화 코드를 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-161">Consider the following 1.x seed initialization code in the `Configure` method of *Startup.cs*:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Startup.cs?name=snippet_ConfigureSeedData&highlight=8)]

<span data-ttu-id="ceb7a-162">2.0 프로젝트에서 `SeedData.Initialize` 호출을 *Program.cs*의 `Main` 메서드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-162">In 2.0 projects, move the `SeedData.Initialize` call to the `Main` method of *Program.cs*:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Program2.cs?name=snippet_Main2Code&highlight=10)]

<span data-ttu-id="ceb7a-163">2.0부터 `BuildWebHost`에서 웹 호스트를 빌드하고 구성하는 작업 외에 다른 작업을 수행하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-163">As of 2.0, it's bad practice to do anything in `BuildWebHost` except build and configure the web host.</span></span> <span data-ttu-id="ceb7a-164">애플리케이션 실행과 관련된 모든 작업은 `BuildWebHost`&mdash; 외부(보통 *Program.cs*의 `Main` 메서드)에서 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-164">Anything that's about running the application should be handled outside of `BuildWebHost` &mdash; typically in the `Main` method of *Program.cs*.</span></span>

<a name="view-compilation"></a>

## <a name="review-razor-view-compilation-setting"></a><span data-ttu-id="ceb7a-165">Razor 보기 컴파일 설정 검토</span><span class="sxs-lookup"><span data-stu-id="ceb7a-165">Review Razor view compilation setting</span></span>

<span data-ttu-id="ceb7a-166">빠른 애플리케이션 시작 시간 및 보다 작은 게시된 번들은 무엇보다도 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-166">Faster application startup time and smaller published bundles are of utmost importance to you.</span></span> <span data-ttu-id="ceb7a-167">이러한 이유로 [Razor 보기 컴파일](xref:mvc/views/view-compilation)은 ASP.NET Core 2.0에서 기본적으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-167">For these reasons, [Razor view compilation](xref:mvc/views/view-compilation) is enabled by default in ASP.NET Core 2.0.</span></span>

<span data-ttu-id="ceb7a-168">`MvcRazorCompileOnPublish` 속성을 true로 설정하는 것은 더 이상 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-168">Setting the `MvcRazorCompileOnPublish` property to true is no longer required.</span></span> <span data-ttu-id="ceb7a-169">보기 컴파일을 비활성화하는 경우가 아니면 *.csproj* 파일에서 속성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-169">Unless you're disabling view compilation, the property may be removed from the *.csproj* file.</span></span>

<span data-ttu-id="ceb7a-170">.NET Framework를 대상으로 하는 경우 여전히 명시적으로 *.csproj* 파일에서 [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation) NuGet 패키지를 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-170">When targeting .NET Framework, you still need to explicitly reference the [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation) NuGet package in your *.csproj* file:</span></span>

[!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App/AspNetCoreDotNetFx2.0App.csproj?range=15)]

<a name="app-insights"></a>

## <a name="rely-on-application-insights-light-up-features"></a><span data-ttu-id="ceb7a-171">Application Insights "강화" 기능 사용</span><span class="sxs-lookup"><span data-stu-id="ceb7a-171">Rely on Application Insights "light-up" features</span></span>

<span data-ttu-id="ceb7a-172">애플리케이션 성능 계측의 손쉬운 설치는 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-172">Effortless setup of application performance instrumentation is important.</span></span> <span data-ttu-id="ceb7a-173">이제 Visual Studio 2017 도구에서 제공하는 [Application Insights](/azure/application-insights/app-insights-overview) "강화" 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-173">You can now rely on the new [Application Insights](/azure/application-insights/app-insights-overview) "light-up" features available in the Visual Studio 2017 tooling.</span></span>

<span data-ttu-id="ceb7a-174">Visual Studio 2017에서 만든 ASP.NET Core 1.1 프로젝트는 기본적으로 Application Insights를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-174">ASP.NET Core 1.1 projects created in Visual Studio 2017 added Application Insights by default.</span></span> <span data-ttu-id="ceb7a-175">*Program.cs* 및 *Startup.cs* 외부에서 Application Insights SDK를 직접 사용하지 않을 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-175">If you're not using the Application Insights SDK directly, outside of *Program.cs* and *Startup.cs*, follow these steps:</span></span>

1. <span data-ttu-id="ceb7a-176">.NET Core를 대상으로 하는 경우 *.csproj* 파일에서 다음 `<PackageReference />` 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-176">If targeting .NET Core, remove the following `<PackageReference />` node from the *.csproj* file:</span></span>

    [!code-xml[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App.csproj?range=10)]

2. <span data-ttu-id="ceb7a-177">.NET Core를 대상으로 하는 경우 *Program.cs*에서 `UseApplicationInsights` 확장 메서드 호출을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-177">If targeting .NET Core, remove the `UseApplicationInsights` extension method invocation from *Program.cs*:</span></span>

    [!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Program.cs?name=snippet_ProgramCsMain&highlight=8)]

3. <span data-ttu-id="ceb7a-178">*_Layout.cshtml*에서 Application Insights 클라이언트 쪽 API 호출을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-178">Remove the Application Insights client-side API call from *_Layout.cshtml*.</span></span> <span data-ttu-id="ceb7a-179">다음 두 코드 줄을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-179">It comprises the following two lines of code:</span></span>

    [!code-cshtml[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Views/Shared/_Layout.cshtml?range=1,19&dedent=4)]

<span data-ttu-id="ceb7a-180">Application Insights SDK를 직접 사용하는 경우 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-180">If you are using the Application Insights SDK directly, continue to do so.</span></span> <span data-ttu-id="ceb7a-181">2.0 [metapackage](xref:fundamentals/metapackage)에는 최신 버전의 Application Insights가 포함되어 있으므로 이전 버전을 참조하는 경우 패키지 다운그레이드 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-181">The 2.0 [metapackage](xref:fundamentals/metapackage) includes the latest version of Application Insights, so a package downgrade error appears if you're referencing an older version.</span></span>

<a name="auth-and-identity"></a>

## <a name="adopt-authenticationidentity-improvements"></a><span data-ttu-id="ceb7a-182">인증/ID 기능 향상 도입</span><span class="sxs-lookup"><span data-stu-id="ceb7a-182">Adopt authentication/Identity improvements</span></span>

<span data-ttu-id="ceb7a-183">ASP.NET Core 2.0에는 새 인증 모델 및 ASP.NET Core ID에 대한 몇 가지 주요 변경 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-183">ASP.NET Core 2.0 has a new authentication model and a number of significant changes to ASP.NET Core Identity.</span></span> <span data-ttu-id="ceb7a-184">개별 사용자 계정을 활성화하여 프로젝트를 만들거나 인증 또는 ID를 수동으로 추가한 경우 [ASP.NET Core 2.0으로 인증 및 ID 마이그레이션](xref:migration/1x-to-2x/identity-2x)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ceb7a-184">If you created your project with Individual User Accounts enabled, or if you have manually added authentication or Identity, see [Migrate Authentication and Identity to ASP.NET Core 2.0](xref:migration/1x-to-2x/identity-2x).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ceb7a-185">추가 자료</span><span class="sxs-lookup"><span data-stu-id="ceb7a-185">Additional resources</span></span>

* [<span data-ttu-id="ceb7a-186">ASP.NET Core 2.0의 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="ceb7a-186">Breaking Changes in ASP.NET Core 2.0</span></span>](https://github.com/aspnet/announcements/issues?page=1&q=is%3Aissue+is%3Aopen+label%3A2.0.0+label%3A%22Breaking+change%22&utf8=%E2%9C%93)
