---
title: ClaimsPrincipal.Current에서 마이그레이션
author: mjrousos
description: 현재 인증 된 사용자의 id 및 ASP.NET Core에서 클레임을 검색할 ClaimsPrincipal.Current에서 마이그레이션하는 방법에 알아봅니다.
ms.author: scaddie
ms.custom: mvc
ms.date: 05/04/2018
uid: migration/claimsprincipal-current
ms.openlocfilehash: 35c3389798041e141c45bf0a76fa9d7285212768
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039280"
---
# <a name="migrate-from-claimsprincipalcurrent"></a><span data-ttu-id="5245a-103">ClaimsPrincipal.Current에서 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="5245a-103">Migrate from ClaimsPrincipal.Current</span></span>

<span data-ttu-id="5245a-104">ASP.NET 4.x 프로젝트에서 사용 하도록 공통적으로 적용 되었습니다 [ClaimsPrincipal.Current](/dotnet/api/system.security.claims.claimsprincipal.current) 현재 검색할 사용자의 id 및 클레임을 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-104">In ASP.NET 4.x projects, it was common to use [ClaimsPrincipal.Current](/dotnet/api/system.security.claims.claimsprincipal.current) to retrieve the current authenticated user's identity and claims.</span></span> <span data-ttu-id="5245a-105">ASP.NET Core에서 더 이상이 속성이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-105">In ASP.NET Core, this property is no longer set.</span></span> <span data-ttu-id="5245a-106">종속 되었던는 코드를 다른 수단을 통해 현재 인증 된 사용자의 id를 가져오려면 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-106">Code that was depending on it needs to be updated to get the current authenticated user's identity through a different means.</span></span>

## <a name="context-specific-data-instead-of-static-data"></a><span data-ttu-id="5245a-107">정적 데이터 대신 상황에 맞는 데이터</span><span class="sxs-lookup"><span data-stu-id="5245a-107">Context-specific data instead of static data</span></span>

<span data-ttu-id="5245a-108">ASP.NET Core의 값이 모두를 사용 하는 경우 `ClaimsPrincipal.Current` 고 `Thread.CurrentPrincipal` 설정 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-108">When using ASP.NET Core, the values of both `ClaimsPrincipal.Current` and `Thread.CurrentPrincipal` aren't set.</span></span> <span data-ttu-id="5245a-109">이러한 두 속성은 ASP.NET Core는 일반적으로 방지 하는 정적 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-109">These properties both represent static state, which ASP.NET Core generally avoids.</span></span> <span data-ttu-id="5245a-110">ASP.NET Core의 아키텍처 상황에 맞는 서비스 컬렉션에서 종속성 (예: 현재 사용자의 id)를 검색 하는 것 대신 (사용 하 여 해당 [종속성 주입](xref:fundamentals/dependency-injection) (DI) 모델).</span><span class="sxs-lookup"><span data-stu-id="5245a-110">Instead, ASP.NET Core's architecture is to retrieve dependencies (like the current user's identity) from context-specific service collections (using its [dependency injection](xref:fundamentals/dependency-injection) (DI) model).</span></span> <span data-ttu-id="5245a-111">더 많은 이란 `Thread.CurrentPrincipal` 이므로 스레드 정적 일부 비동기 시나리오에서 변경 내용을 유지 되지 않을 수 있습니다 (및 `ClaimsPrincipal.Current` 호출 `Thread.CurrentPrincipal` 기본적으로).</span><span class="sxs-lookup"><span data-stu-id="5245a-111">What's more, `Thread.CurrentPrincipal` is thread static, so it may not persist changes in some asynchronous scenarios (and `ClaimsPrincipal.Current` just calls `Thread.CurrentPrincipal` by default).</span></span>

<span data-ttu-id="5245a-112">문제 스레드의 종류를 이해 하려면 정적 멤버는 비동기 시나리오에서 다음 코드 조각을 고려해 야 할 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-112">To understand the sorts of problems thread static members can lead to in asynchronous scenarios, consider the following code snippet:</span></span>

```csharp
// Create a ClaimsPrincipal and set Thread.CurrentPrincipal
var identity = new ClaimsIdentity();
identity.AddClaim(new Claim(ClaimTypes.Name, "User1"));
Thread.CurrentPrincipal = new ClaimsPrincipal(identity);

// Check the current user
Console.WriteLine($"Current user: {Thread.CurrentPrincipal?.Identity.Name}");

// For the method to complete asynchronously
await Task.Yield();

// Check the current user after
Console.WriteLine($"Current user: {Thread.CurrentPrincipal?.Identity.Name}");
```

<span data-ttu-id="5245a-113">위의 샘플 코드 집합 `Thread.CurrentPrincipal` 전과 비동기 호출을 기다린 후 해당 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-113">The preceding sample code sets `Thread.CurrentPrincipal` and checks its value before and after awaiting an asynchronous call.</span></span> <span data-ttu-id="5245a-114">`Thread.CurrentPrincipal` 관련이 합니다 *스레드* 는 속성을 설정 하 고 메서드는 await 뒤 다른 스레드에서 실행을 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-114">`Thread.CurrentPrincipal` is specific to the *thread* on which it's set, and the method is likely to resume execution on a different thread after the await.</span></span> <span data-ttu-id="5245a-115">따라서 `Thread.CurrentPrincipal` 은 present를 먼저 검사 하지만를 호출한 후 null 경우 `await Task.Yield()`합니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-115">Consequently, `Thread.CurrentPrincipal` is present when it's first checked but is null after the call to `await Task.Yield()`.</span></span>

<span data-ttu-id="5245a-116">앱의 DI 서비스 컬렉션에서 현재 사용자의 id를 가져오는 이므로 더 테스트도 테스트 identities를 쉽게 삽입할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-116">Getting the current user's identity from the app's DI service collection is more testable, too, since test identities can be easily injected.</span></span>

## <a name="retrieve-the-current-user-in-an-aspnet-core-app"></a><span data-ttu-id="5245a-117">ASP.NET Core 앱에서 현재 사용자를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-117">Retrieve the current user in an ASP.NET Core app</span></span>

<span data-ttu-id="5245a-118">현재 인증된 된 사용자를 검색 하는 방법은 여러 가지 `ClaimsPrincipal` 대신 ASP.NET Core에서 `ClaimsPrincipal.Current`:</span><span class="sxs-lookup"><span data-stu-id="5245a-118">There are several options for retrieving the current authenticated user's `ClaimsPrincipal` in ASP.NET Core in place of `ClaimsPrincipal.Current`:</span></span>

* <span data-ttu-id="5245a-119">**ControllerBase.User**.</span><span class="sxs-lookup"><span data-stu-id="5245a-119">**ControllerBase.User**.</span></span> <span data-ttu-id="5245a-120">MVC 컨트롤러는 현재 인증 된 사용자로 액세스할 수 있는 해당 [사용자](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.user) 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-120">MVC controllers can access the current authenticated user with their [User](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.user) property.</span></span>
* <span data-ttu-id="5245a-121">**HttpContext.User**.</span><span class="sxs-lookup"><span data-stu-id="5245a-121">**HttpContext.User**.</span></span> <span data-ttu-id="5245a-122">현재에 대 한 액세스를 사용 하 여 구성 요소 `HttpContext` (예: 미들웨어)는 현재 사용자의 가져올 수 있습니다 `ClaimsPrincipal` 에서 [HttpContext.User](/dotnet/api/microsoft.aspnetcore.http.httpcontext.user)합니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-122">Components with access to the current `HttpContext` (middleware, for example) can get the current user's `ClaimsPrincipal` from [HttpContext.User](/dotnet/api/microsoft.aspnetcore.http.httpcontext.user).</span></span>
* <span data-ttu-id="5245a-123">**호출자에서 전달 된**합니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-123">**Passed in from caller**.</span></span> <span data-ttu-id="5245a-124">현재에 액세스 하지 않고 라이브러리 `HttpContext` 컨트롤러 또는 미들웨어 구성 요소에서 이라고 하 고 인수로 전달 하는 현재 사용자의 id를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-124">Libraries without access to the current `HttpContext` are often called from controllers or middleware components and can have the current user's identity passed as an argument.</span></span>
* <span data-ttu-id="5245a-125">**IHttpContextAccessor**.</span><span class="sxs-lookup"><span data-stu-id="5245a-125">**IHttpContextAccessor**.</span></span> <span data-ttu-id="5245a-126">ASP.NET Core로 마이그레이션되는 프로젝트는 너무 커서 모든 필요한 위치에 현재 사용자의 id를 쉽게 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-126">The project being migrated to ASP.NET Core may be too large to easily pass the current user's identity to all necessary locations.</span></span> <span data-ttu-id="5245a-127">이러한 경우 [IHttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextaccessor) 대 안으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-127">In such cases, [IHttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextaccessor) can be used as a workaround.</span></span> <span data-ttu-id="5245a-128">`IHttpContextAccessor` 현재 액세스할 수 `HttpContext` (있는 경우).</span><span class="sxs-lookup"><span data-stu-id="5245a-128">`IHttpContextAccessor` is able to access the current `HttpContext` (if one exists).</span></span> <span data-ttu-id="5245a-129">단기적인 해결책을 ASP.NET Core DI 기반 아키텍처를 사용 하 여 작동 하도록 아직 업데이트 되지 않은 코드에서 현재 사용자의 id를 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-129">A short-term solution to getting the current user's identity in code that hasn't yet been updated to work with ASP.NET Core's DI-driven architecture would be:</span></span>

  * <span data-ttu-id="5245a-130">확인 `IHttpContextAccessor` 를 호출 하 여 DI 컨테이너에서 사용 가능한 [AddHttpContextAccessor](https://github.com/aspnet/Hosting/issues/793) 에서 `Startup.ConfigureServices`합니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-130">Make `IHttpContextAccessor` available in the DI container by calling [AddHttpContextAccessor](https://github.com/aspnet/Hosting/issues/793) in `Startup.ConfigureServices`.</span></span>
  * <span data-ttu-id="5245a-131">인스턴스를 가져올 `IHttpContextAccessor` 시작 하는 동안 정적 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-131">Get an instance of `IHttpContextAccessor` during startup and store it in a static variable.</span></span> <span data-ttu-id="5245a-132">인스턴스를 이전에 정적 속성에서 현재 사용자를 검색 하는 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-132">The instance is made available to code that was previously retrieving the current user from a static property.</span></span>
  * <span data-ttu-id="5245a-133">현재 사용자의 검색 `ClaimsPrincipal` 를 사용 하 여 `HttpContextAccessor.HttpContext?.User`입니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-133">Retrieve the current user's `ClaimsPrincipal` using `HttpContextAccessor.HttpContext?.User`.</span></span> <span data-ttu-id="5245a-134">이 코드는 HTTP 요청 컨텍스트 외부에서 사용 되는 경우는 `HttpContext` null입니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-134">If this code is used outside of the context of an HTTP request, the `HttpContext` is null.</span></span>

<span data-ttu-id="5245a-135">마지막 옵션을 사용 하 여 `IHttpContextAccessor`, (정적 종속성 삽입 된 종속성을 선호) ASP.NET Core 원칙에 위배 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-135">The final option, using `IHttpContextAccessor`, is contrary to ASP.NET Core principles (preferring injected dependencies to static dependencies).</span></span> <span data-ttu-id="5245a-136">결국 정적에 대 한 종속성을 제거 하려면 `IHttpContextAccessor` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-136">Plan to eventually remove the dependency on the static `IHttpContextAccessor` helper.</span></span> <span data-ttu-id="5245a-137">이전에 사용 하는 많은 기존 ASP.NET 앱을 마이그레이션하는 경우 유용한 브리지, 하지만 수 있습니다 `ClaimsPrincipal.Current`합니다.</span><span class="sxs-lookup"><span data-stu-id="5245a-137">It can be a useful bridge, though, when migrating large existing ASP.NET apps that were previously using `ClaimsPrincipal.Current`.</span></span>
