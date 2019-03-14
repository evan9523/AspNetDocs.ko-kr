---
title: ASP.NET Core에서 세션 및 앱 상태
author: rick-anderson
description: 요청 간 세션 및 앱 상태를 유지하는 방법을 검색합니다.
ms.author: riande
ms.custom: mvc
ms.date: 06/14/2018
uid: fundamentals/app-state
ms.openlocfilehash: a510e4f49e158203dd7c5e1e0bd28472541f7925
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024980"
---
# <a name="session-and-app-state-in-aspnet-core"></a><span data-ttu-id="66b02-103">ASP.NET Core에서 세션 및 앱 상태</span><span class="sxs-lookup"><span data-stu-id="66b02-103">Session and app state in ASP.NET Core</span></span>

<span data-ttu-id="66b02-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT), [Steve Smith](https://ardalis.com/), [Diana LaRose](https://github.com/DianaLaRose) 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="66b02-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Steve Smith](https://ardalis.com/), [Diana LaRose](https://github.com/DianaLaRose), and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="66b02-105">HTTP는 상태 비저장 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-105">HTTP is a stateless protocol.</span></span> <span data-ttu-id="66b02-106">HTTP 요청은 추가 단계를 수행하지 않고 사용자 값 또는 앱 상태를 유지하지 않는 독립적인 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-106">Without taking additional steps, HTTP requests are independent messages that don't retain user values or app state.</span></span> <span data-ttu-id="66b02-107">이 문서에서는 요청 간 사용자 데이터와 앱 상태를 유지하는 몇 가지 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-107">This article describes several approaches to preserve user data and app state between requests.</span></span>

<span data-ttu-id="66b02-108">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/app-state/samples) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="66b02-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/app-state/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="state-management"></a><span data-ttu-id="66b02-109">상태 관리</span><span class="sxs-lookup"><span data-stu-id="66b02-109">State management</span></span>

<span data-ttu-id="66b02-110">상태는 여러 방법을 사용하여 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-110">State can be stored using several approaches.</span></span> <span data-ttu-id="66b02-111">각 방법은 이 항목 뒷부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-111">Each approach is described later in this topic.</span></span>

| <span data-ttu-id="66b02-112">스토리지 접근 방식</span><span class="sxs-lookup"><span data-stu-id="66b02-112">Storage approach</span></span> | <span data-ttu-id="66b02-113">스토리지 메커니즘</span><span class="sxs-lookup"><span data-stu-id="66b02-113">Storage mechanism</span></span> |
| ---------------- | ----------------- |
| [<span data-ttu-id="66b02-114">쿠키</span><span class="sxs-lookup"><span data-stu-id="66b02-114">Cookies</span></span>](#cookies) | <span data-ttu-id="66b02-115">HTTP 쿠키(서버 쪽 앱 코드를 사용하여 저장된 데이터 포함)</span><span class="sxs-lookup"><span data-stu-id="66b02-115">HTTP cookies (may include data stored using server-side app code)</span></span> |
| [<span data-ttu-id="66b02-116">세션 상태</span><span class="sxs-lookup"><span data-stu-id="66b02-116">Session state</span></span>](#session-state) | <span data-ttu-id="66b02-117">HTTP 쿠키 및 서버 쪽 앱 코드</span><span class="sxs-lookup"><span data-stu-id="66b02-117">HTTP cookies and server-side app code</span></span> |
| [<span data-ttu-id="66b02-118">TempData</span><span class="sxs-lookup"><span data-stu-id="66b02-118">TempData</span></span>](#tempdata) | <span data-ttu-id="66b02-119">HTTP 쿠키 또는 세션 상태</span><span class="sxs-lookup"><span data-stu-id="66b02-119">HTTP cookies or session state</span></span> |
| [<span data-ttu-id="66b02-120">쿼리 문자열</span><span class="sxs-lookup"><span data-stu-id="66b02-120">Query strings</span></span>](#query-strings) | <span data-ttu-id="66b02-121">HTTP 쿼리 문자열</span><span class="sxs-lookup"><span data-stu-id="66b02-121">HTTP query strings</span></span> |
| [<span data-ttu-id="66b02-122">숨겨진 필드</span><span class="sxs-lookup"><span data-stu-id="66b02-122">Hidden fields</span></span>](#hidden-fields) | <span data-ttu-id="66b02-123">HTTP 양식 필드</span><span class="sxs-lookup"><span data-stu-id="66b02-123">HTTP form fields</span></span> |
| [<span data-ttu-id="66b02-124">HttpContext.Items</span><span class="sxs-lookup"><span data-stu-id="66b02-124">HttpContext.Items</span></span>](#httpcontextitems) | <span data-ttu-id="66b02-125">서버 쪽 앱 코드</span><span class="sxs-lookup"><span data-stu-id="66b02-125">Server-side app code</span></span> |
| [<span data-ttu-id="66b02-126">캐시</span><span class="sxs-lookup"><span data-stu-id="66b02-126">Cache</span></span>](#cache) | <span data-ttu-id="66b02-127">서버 쪽 앱 코드</span><span class="sxs-lookup"><span data-stu-id="66b02-127">Server-side app code</span></span> |
| [<span data-ttu-id="66b02-128">종속성 주입</span><span class="sxs-lookup"><span data-stu-id="66b02-128">Dependency Injection</span></span>](#dependency-injection) | <span data-ttu-id="66b02-129">서버 쪽 앱 코드</span><span class="sxs-lookup"><span data-stu-id="66b02-129">Server-side app code</span></span> |

## <a name="cookies"></a><span data-ttu-id="66b02-130">쿠키</span><span class="sxs-lookup"><span data-stu-id="66b02-130">Cookies</span></span>

<span data-ttu-id="66b02-131">쿠키는 요청 간에 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-131">Cookies store data across requests.</span></span> <span data-ttu-id="66b02-132">쿠키는 모든 요청과 함께 전송되므로 해당 크기는 최소로 유지되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-132">Because cookies are sent with every request, their size should be kept to a minimum.</span></span> <span data-ttu-id="66b02-133">이상적으로 식별자만 앱에 저장된 데이터와 함께 쿠키에 저장되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-133">Ideally, only an identifier should be stored in a cookie with the data stored by the app.</span></span> <span data-ttu-id="66b02-134">대부분의 브라우저는 쿠키 크기를 4096바이트로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-134">Most browsers restrict cookie size to 4096 bytes.</span></span> <span data-ttu-id="66b02-135">제한된 수의 쿠키만 각 도메인에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-135">Only a limited number of cookies are available for each domain.</span></span>

<span data-ttu-id="66b02-136">쿠키는 변조될 수 있기 때문에 앱에서 유효성을 검사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-136">Because cookies are subject to tampering, they must be validated by the app.</span></span> <span data-ttu-id="66b02-137">쿠키는 사용자가 삭제할 수 있으며 클라이언트에서 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-137">Cookies can be deleted by users and expire on clients.</span></span> <span data-ttu-id="66b02-138">그러나 쿠키는 일반적으로 클라이언트에서 데이터 지속성의 가장 안정적인 형태입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-138">However, cookies are generally the most durable form of data persistence on the client.</span></span>

<span data-ttu-id="66b02-139">쿠키는 종종 개인 설정에 사용됩니다. 여기서 콘텐츠는 알려진 사용자에 대해 사용자 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-139">Cookies are often used for personalization, where content is customized for a known user.</span></span> <span data-ttu-id="66b02-140">사용자만 식별되고 대부분의 경우 인증되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-140">The user is only identified and not authenticated in most cases.</span></span> <span data-ttu-id="66b02-141">쿠키는 사용자의 이름, 계정 이름 또는 고유한 사용자 ID(예: GUID)를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-141">The cookie can store the user's name, account name, or unique user ID (such as a GUID).</span></span> <span data-ttu-id="66b02-142">사용자는 쿠키를 사용하여 선호하는 웹 사이트 배경색과 같은 사용자의 개인 설정에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-142">You can then use the cookie to access the user's personalized settings, such as their preferred website background color.</span></span>

<span data-ttu-id="66b02-143">쿠키를 발급하고 개인 정보 보호 문제를 다룰 때 [유럽 연합 GDPR(일반 데이터 보호 규정)](https://ec.europa.eu/info/law/law-topic/data-protection)에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-143">Be mindful of the [European Union General Data Protection Regulations (GDPR)](https://ec.europa.eu/info/law/law-topic/data-protection) when issuing cookies and dealing with privacy concerns.</span></span> <span data-ttu-id="66b02-144">자세한 내용은 [ASP.NET Core의 GDPR(일반 데이터 보호 규정) 지원](xref:security/gdpr)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66b02-144">For more information, see [General Data Protection Regulation (GDPR) support in ASP.NET Core](xref:security/gdpr).</span></span>

## <a name="session-state"></a><span data-ttu-id="66b02-145">세션 상태</span><span class="sxs-lookup"><span data-stu-id="66b02-145">Session state</span></span>

<span data-ttu-id="66b02-146">세션 상태는 사용자가 웹앱을 탐색하는 동안 사용자 데이터를 저장하기 위한 ASP.NET Core 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-146">Session state is an ASP.NET Core scenario for storage of user data while the user browses a web app.</span></span> <span data-ttu-id="66b02-147">세션 상태는 앱에서 유지 관리하는 저장소를 사용하여 클라이언트의 요청 간에 데이터를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-147">Session state uses a store maintained by the app to persist data across requests from a client.</span></span> <span data-ttu-id="66b02-148">세션 데이터는 캐시에 의해 백업되고 임시 데이터로 간주되므로 사이트는 세션 데이터 없이 계속 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-148">The session data is backed by a cache and considered ephemeral data&mdash;the site should continue to function without the session data.</span></span> <span data-ttu-id="66b02-149">중요한 애플리케이션 데이터는 사용자 데이터베이스에 저장되고 성능 최적화로 세션에 캐시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-149">Critical application data should be stored in the user database and cached in session only as a performance optimization.</span></span>

> [!NOTE]
> <span data-ttu-id="66b02-150">[SignalR Hub](xref:signalr/hubs)가 HTTP 컨텍스트와 독립적으로 실행될 수 있으므로, 세션은 [SignalR](xref:signalr/index) 앱에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-150">Session isn't supported in [SignalR](xref:signalr/index) apps because a [SignalR Hub](xref:signalr/hubs) may execute independent of an HTTP context.</span></span> <span data-ttu-id="66b02-151">예를 들어, 허브에서 긴 폴링 요청이 HTTP 컨텍스트 수명을 초과하여 계속 열려 있을 경우 이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-151">For example, this can occur when a long polling request is held open by a hub beyond the lifetime of the request's HTTP context.</span></span>

<span data-ttu-id="66b02-152">ASP.NET Core는 각 요청과 함께 앱으로 전송되는 세션 ID를 포함하는 쿠키를 클라이언트에 제공하여 세션 상태를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-152">ASP.NET Core maintains session state by providing a cookie to the client that contains a session ID, which is sent to the app with each request.</span></span> <span data-ttu-id="66b02-153">앱은 세션 ID를 사용하여 세션 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-153">The app uses the session ID to fetch the session data.</span></span>

<span data-ttu-id="66b02-154">세션 상태는 다음과 같은 동작을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-154">Session state exhibits the following behaviors:</span></span>

* <span data-ttu-id="66b02-155">세션 쿠키는 브라우저에 특정되기 때문에 브라우저 간에 세션이 공유되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-155">Because the session cookie is specific to the browser, sessions aren't shared across browsers.</span></span>
* <span data-ttu-id="66b02-156">세션 쿠키는 브라우저 세션이 끝나면 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-156">Session cookies are deleted when the browser session ends.</span></span>
* <span data-ttu-id="66b02-157">쿠키가 만료된 세션에 대해 수신되면 동일한 세션 쿠키를 사용하는 새 세션이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-157">If a cookie is received for an expired session, a new session is created that uses the same session cookie.</span></span>
* <span data-ttu-id="66b02-158">빈 세션은 유지되지 않습니다. 요청 간 세션을 유지하려면 세션에 하나 이상의 값이 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-158">Empty sessions aren't retained&mdash;the session must have at least one value set into it to persist the session across requests.</span></span> <span data-ttu-id="66b02-159">세션이 유지되지 않으면 새 요청마다 새 세션 ID가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-159">When a session isn't retained, a new session ID is generated for each new request.</span></span>
* <span data-ttu-id="66b02-160">앱은 마지막 요청 이후 제한된 시간 동안 세션을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-160">The app retains a session for a limited time after the last request.</span></span> <span data-ttu-id="66b02-161">앱은 세션 시간 제한을 설정하거나 20분의 기본값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-161">The app either sets the session timeout or uses the default value of 20 minutes.</span></span> <span data-ttu-id="66b02-162">세션 상태는 특정 세션과 관련된 사용자 데이터를 저장하되, 데이터가 세션 간에 영구 스토리지를 요구하지 않는 경우에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-162">Session state is ideal for storing user data that's specific to a particular session but where the data doesn't require permanent storage across sessions.</span></span>
* <span data-ttu-id="66b02-163">세션 데이터는 [ISession.Clear](/dotnet/api/microsoft.aspnetcore.http.isession.clear) 구현이 호출되거나 세션이 만료될 때 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-163">Session data is deleted either when the [ISession.Clear](/dotnet/api/microsoft.aspnetcore.http.isession.clear) implementation is called or when the session expires.</span></span>
* <span data-ttu-id="66b02-164">클라이언트 브라우저가 닫혔거나 세션 쿠키가 삭제 또는 클라이언트에서 만료되었을 때 앱 코드에 이를 알려주는 기본 메커니즘은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-164">There's no default mechanism to inform app code that a client browser has been closed or when the session cookie is deleted or expired on the client.</span></span>
<span data-ttu-id="66b02-165">ASP.NET Core MVC 및 Razor 페이지 템플릿에는 [GDPR(일반 데이터 보호 규정) 지원](xref:security/gdpr)에 대한 지원이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-165">The ASP.NET Core MVC and Razor pages templates include support for [General Data Protection Regulation (GDPR) support](xref:security/gdpr).</span></span> <span data-ttu-id="66b02-166">[세션 상태 쿠키는 필수 항목이 아니며](xref:security/gdpr#tempdata-provider-and-session-state-cookies-are-not-essential), 추적이 비활성화되면 세션 상태가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-166">[Session state cookies aren't essential](xref:security/gdpr#tempdata-provider-and-session-state-cookies-are-not-essential), session state isn't functional when tracking is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="66b02-167">중요한 데이터를 세션 상태에 저장하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="66b02-167">Don't store sensitive data in session state.</span></span> <span data-ttu-id="66b02-168">사용자는 브라우저를 닫지 않고 세션 쿠키를 지울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-168">The user might not close the browser and clear the session cookie.</span></span> <span data-ttu-id="66b02-169">일부 브라우저는 브라우저 창이 닫혀도 유효한 세션 쿠키를 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-169">Some browsers maintain valid session cookies across browser windows.</span></span> <span data-ttu-id="66b02-170">세션은 단일 사용자로 제한될 수 없으므로 다음 사용자는 동일한 세션 쿠키로 앱을 계속 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-170">A session might not be restricted to a single user&mdash;the next user might continue to browse the app with the same session cookie.</span></span>

<span data-ttu-id="66b02-171">메모리 내 캐시 공급자는 앱이 있는 서버의 메모리에 세션 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-171">The in-memory cache provider stores session data in the memory of the server where the app resides.</span></span> <span data-ttu-id="66b02-172">서버 팜 시나리오:</span><span class="sxs-lookup"><span data-stu-id="66b02-172">In a server farm scenario:</span></span>

* <span data-ttu-id="66b02-173">*고정 세션*을 사용하여 각 세션을 개별 서버의 특정 앱 인스턴스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-173">Use *sticky sessions* to tie each session to a specific app instance on an individual server.</span></span> <span data-ttu-id="66b02-174">[Azure App Service](https://azure.microsoft.com/services/app-service/)는 [ARR(애플리케이션 요청 라우팅)](/iis/extensions/planning-for-arr/using-the-application-request-routing-module)을 사용하여 기본적으로 고정 세션을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-174">[Azure App Service](https://azure.microsoft.com/services/app-service/) uses [Application Request Routing (ARR)](/iis/extensions/planning-for-arr/using-the-application-request-routing-module) to enforce sticky sessions by default.</span></span> <span data-ttu-id="66b02-175">그러나 고정 세션은 확장성에 영향을 주고 웹앱 업데이트를 복잡하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-175">However, sticky sessions can affect scalability and complicate web app updates.</span></span> <span data-ttu-id="66b02-176">더 나은 방법은 고정 세션이 필요 없는 Redis 또는 SQL Server 분산 캐시를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-176">A better approach is to use a Redis or SQL Server distributed cache, which doesn't require sticky sessions.</span></span> <span data-ttu-id="66b02-177">자세한 내용은 <xref:performance/caching/distributed>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66b02-177">For more information, see <xref:performance/caching/distributed>.</span></span>
* <span data-ttu-id="66b02-178">세션 쿠키는 [IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector)를 통해 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-178">The session cookie is encrypted via [IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector).</span></span> <span data-ttu-id="66b02-179">데이터 보호는 각 컴퓨터에서 세션 쿠키를 읽을 수 있도록 올바르게 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-179">Data Protection must be properly configured to read session cookies on each machine.</span></span> <span data-ttu-id="66b02-180">자세한 내용은 <xref:security/data-protection/introduction> 및 [키 스토리지 공급자](xref:security/data-protection/implementation/key-storage-providers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66b02-180">For more information, see <xref:security/data-protection/introduction> and [Key storage providers](xref:security/data-protection/implementation/key-storage-providers).</span></span>

### <a name="configure-session-state"></a><span data-ttu-id="66b02-181">세션 상태 구성</span><span class="sxs-lookup"><span data-stu-id="66b02-181">Configure session state</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="66b02-182">[Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에 포함된 [Microsoft.AspNetCore.Session](https://www.nuget.org/packages/Microsoft.AspNetCore.Session/) 패키지는 세션 상태 관리용 미들웨어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-182">The [Microsoft.AspNetCore.Session](https://www.nuget.org/packages/Microsoft.AspNetCore.Session/) package, which is included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app), provides middleware for managing session state.</span></span> <span data-ttu-id="66b02-183">세션 미들웨어를 활성화하려면 `Startup`은 다음을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-183">To enable the session middleware, `Startup` must contain:</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="66b02-184">[Microsoft.AspNetCore.Session](https://www.nuget.org/packages/Microsoft.AspNetCore.Session/) 패키지는 세션 상태 관리용 미들웨어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-184">The [Microsoft.AspNetCore.Session](https://www.nuget.org/packages/Microsoft.AspNetCore.Session/) package provides middleware for managing session state.</span></span> <span data-ttu-id="66b02-185">세션 미들웨어를 활성화하려면 `Startup`은 다음을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-185">To enable the session middleware, `Startup` must contain:</span></span>

::: moniker-end

* <span data-ttu-id="66b02-186">[IDistributedCache](/dotnet/api/microsoft.extensions.caching.distributed.idistributedcache) 메모리 캐시 중 하나</span><span class="sxs-lookup"><span data-stu-id="66b02-186">Any of the [IDistributedCache](/dotnet/api/microsoft.extensions.caching.distributed.idistributedcache) memory caches.</span></span> <span data-ttu-id="66b02-187">`IDistributedCache` 구현은 세션에 대한 백업 저장소로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-187">The `IDistributedCache` implementation is used as a backing store for session.</span></span> <span data-ttu-id="66b02-188">자세한 내용은 <xref:performance/caching/distributed>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66b02-188">For more information, see <xref:performance/caching/distributed>.</span></span>
* <span data-ttu-id="66b02-189">`ConfigureServices`의 [AddSession](/dotnet/api/microsoft.extensions.dependencyinjection.sessionservicecollectionextensions.addsession)에 대한 호출.</span><span class="sxs-lookup"><span data-stu-id="66b02-189">A call to [AddSession](/dotnet/api/microsoft.extensions.dependencyinjection.sessionservicecollectionextensions.addsession) in `ConfigureServices`.</span></span>
* <span data-ttu-id="66b02-190">`Configure`의 [UseSession](/dotnet/api/microsoft.aspnetcore.builder.sessionmiddlewareextensions#methods_)에 대한 호출.</span><span class="sxs-lookup"><span data-stu-id="66b02-190">A call to [UseSession](/dotnet/api/microsoft.aspnetcore.builder.sessionmiddlewareextensions#methods_) in `Configure`.</span></span>

<span data-ttu-id="66b02-191">다음 코드에서는 `IDistributedCache`의 기본 메모리 내 구현을 사용하여 메모리 내 세션 공급자를 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-191">The following code shows how to set up the in-memory session provider with a default in-memory implementation of `IDistributedCache`:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-state/samples/2.x/SessionSample/Startup.cs?name=snippet1&highlight=11,13-18,39)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](app-state/samples/1.x/SessionSample/Startup.cs?name=snippet1&highlight=5,7-12,19)]

::: moniker-end

<span data-ttu-id="66b02-192">미들웨어의 순서가 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-192">The order of middleware is important.</span></span> <span data-ttu-id="66b02-193">앞의 예에서 `UseMvc` 이후에 `UseSession`이 호출되면 `InvalidOperationException` 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-193">In the preceding example, an `InvalidOperationException` exception occurs when `UseSession` is invoked after `UseMvc`.</span></span> <span data-ttu-id="66b02-194">자세한 내용은 [미들웨어 순서 지정](xref:fundamentals/middleware/index#order)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66b02-194">For more information, see [Middleware Ordering](xref:fundamentals/middleware/index#order).</span></span>

<span data-ttu-id="66b02-195">[HttpContext.Session](/dotnet/api/microsoft.aspnetcore.http.httpcontext.session)은 세션 상태가 구성된 후에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-195">[HttpContext.Session](/dotnet/api/microsoft.aspnetcore.http.httpcontext.session) is available after session state is configured.</span></span>

<span data-ttu-id="66b02-196">`UseSession`이 호출되기 전에 `HttpContext.Session`에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-196">`HttpContext.Session` can't be accessed before `UseSession` has been called.</span></span>

<span data-ttu-id="66b02-197">앱이 응답 스트림에 쓰기 시작한 후에는 새 세션 쿠키가 있는 새 세션을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-197">A new session with a new session cookie can't be created after the app has begun writing to the response stream.</span></span> <span data-ttu-id="66b02-198">예외는 웹 서버 로그에 기록되며 브라우저에는 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-198">The exception is recorded in the web server log and not displayed in the browser.</span></span>

### <a name="load-session-state-asynchronously"></a><span data-ttu-id="66b02-199">세션 상태를 비동기적으로 로드</span><span class="sxs-lookup"><span data-stu-id="66b02-199">Load session state asynchronously</span></span>

<span data-ttu-id="66b02-200">ASP.NET Core에서 기본 세션 공급자는 [ISession.LoadAsync](/dotnet/api/microsoft.aspnetcore.http.isession.loadasync) 메서드가 [TryGetValue](/dotnet/api/microsoft.aspnetcore.http.isession.trygetvalue), [Set](/dotnet/api/microsoft.aspnetcore.http.isession.set) 또는 [Remove](/dotnet/api/microsoft.aspnetcore.http.isession.remove) 메서드 전에 명시적으로 호출된 경우에만 기본 [IDistributedCache](/dotnet/api/microsoft.extensions.caching.distributed.idistributedcache) 백업 저장소에서 비동기적으로 세션 레코드를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-200">The default session provider in ASP.NET Core loads session records from the underlying [IDistributedCache](/dotnet/api/microsoft.extensions.caching.distributed.idistributedcache) backing store asynchronously only if the [ISession.LoadAsync](/dotnet/api/microsoft.aspnetcore.http.isession.loadasync) method is explicitly called before the [TryGetValue](/dotnet/api/microsoft.aspnetcore.http.isession.trygetvalue), [Set](/dotnet/api/microsoft.aspnetcore.http.isession.set), or [Remove](/dotnet/api/microsoft.aspnetcore.http.isession.remove) methods.</span></span> <span data-ttu-id="66b02-201">`LoadAsync`가 먼저 호출되지 않은 경우 기본 세션 레코드가 동기적으로 로드되며, 이는 크기에 따라 성능 저하를 초래할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-201">If `LoadAsync` isn't called first, the underlying session record is loaded synchronously, which can incur a performance penalty at scale.</span></span>

<span data-ttu-id="66b02-202">이 패턴을 앱에 적용하려면 `LoadAsync` 메서드가 `TryGetValue`, `Set` 또는 `Remove` 이전에 호출되지 않은 경우 예외를 throw하는 버전으로 [DistributedSessionStore](/dotnet/api/microsoft.aspnetcore.session.distributedsessionstore) 및 [DistributedSession](/dotnet/api/microsoft.aspnetcore.session.distributedsession) 구현을 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-202">To have apps enforce this pattern, wrap the [DistributedSessionStore](/dotnet/api/microsoft.aspnetcore.session.distributedsessionstore) and [DistributedSession](/dotnet/api/microsoft.aspnetcore.session.distributedsession) implementations with versions that throw an exception if the `LoadAsync` method isn't called before `TryGetValue`, `Set`, or `Remove`.</span></span> <span data-ttu-id="66b02-203">서비스 컨테이너에 래핑된 버전을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-203">Register the wrapped versions in the services container.</span></span>

### <a name="session-options"></a><span data-ttu-id="66b02-204">세션 옵션</span><span class="sxs-lookup"><span data-stu-id="66b02-204">Session options</span></span>

<span data-ttu-id="66b02-205">세션 기본값을 재정의하려면 [SessionOptions](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-205">To override session defaults, use [SessionOptions](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions).</span></span>

::: moniker range=">= aspnetcore-2.0"

| <span data-ttu-id="66b02-206">옵션</span><span class="sxs-lookup"><span data-stu-id="66b02-206">Option</span></span> | <span data-ttu-id="66b02-207">설명</span><span class="sxs-lookup"><span data-stu-id="66b02-207">Description</span></span> |
| ------ | ----------- |
| [<span data-ttu-id="66b02-208">쿠키</span><span class="sxs-lookup"><span data-stu-id="66b02-208">Cookie</span></span>](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.cookie) | <span data-ttu-id="66b02-209">쿠키를 만드는 데 사용되는 설정을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-209">Determines the settings used to create the cookie.</span></span> <span data-ttu-id="66b02-210">[Name](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.name)의 기본값은 [SessionDefaults.CookieName](/dotnet/api/microsoft.aspnetcore.session.sessiondefaults.cookiename)(`.AspNetCore.Session`)입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-210">[Name](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.name) defaults to [SessionDefaults.CookieName](/dotnet/api/microsoft.aspnetcore.session.sessiondefaults.cookiename) (`.AspNetCore.Session`).</span></span> <span data-ttu-id="66b02-211">[Path](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.path)의 기본값은 [SessionDefaults.CookiePath](/dotnet/api/microsoft.aspnetcore.session.sessiondefaults.cookiepath)(`/`)입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-211">[Path](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.path) defaults to [SessionDefaults.CookiePath](/dotnet/api/microsoft.aspnetcore.session.sessiondefaults.cookiepath) (`/`).</span></span> <span data-ttu-id="66b02-212">[SameSite](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.samesite)의 기본값은 [SameSiteMode.Lax](/dotnet/api/microsoft.aspnetcore.http.samesitemode)(`1`)입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-212">[SameSite](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.samesite) defaults to [SameSiteMode.Lax](/dotnet/api/microsoft.aspnetcore.http.samesitemode) (`1`).</span></span> <span data-ttu-id="66b02-213">[HttpOnly](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.httponly)의 기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-213">[HttpOnly](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.httponly) defaults to `true`.</span></span> <span data-ttu-id="66b02-214">[IsEssential](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.isessential)의 기본값은 `false`입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-214">[IsEssential](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.isessential) defaults to `false`.</span></span> |
| [<span data-ttu-id="66b02-215">IdleTimeout</span><span class="sxs-lookup"><span data-stu-id="66b02-215">IdleTimeout</span></span>](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.idletimeout) | <span data-ttu-id="66b02-216">`IdleTimeout`은 콘텐츠가 삭제되기 전까지 세션이 유휴 상태일 수 있는 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-216">The `IdleTimeout` indicates how long the session can be idle before its contents are abandoned.</span></span> <span data-ttu-id="66b02-217">각 세션 액세스는 시간 제한을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-217">Each session access resets the timeout.</span></span> <span data-ttu-id="66b02-218">이 설정은 쿠키가 아닌 세션의 콘텐츠에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-218">This setting only applies to the content of the session, not the cookie.</span></span> <span data-ttu-id="66b02-219">기본값은 20분입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-219">The default is 20 minutes.</span></span> |
| [<span data-ttu-id="66b02-220">IOTimeout</span><span class="sxs-lookup"><span data-stu-id="66b02-220">IOTimeout</span></span>](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.iotimeout) | <span data-ttu-id="66b02-221">저장소에서 세션을 로드하거나 저장소로 다시 커밋할 수 있는 최대 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-221">The maximim amount of time allowed to load a session from the store or to commit it back to the store.</span></span> <span data-ttu-id="66b02-222">이 설정은 비동기 작업에만 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-222">This setting may only apply to asynchronous operations.</span></span> <span data-ttu-id="66b02-223">이 시간 제한은 [InfiniteTimeSpan](/dotnet/api/system.threading.timeout.infinitetimespan)을 사용하여 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-223">This timeout can be disabled using [InfiniteTimeSpan](/dotnet/api/system.threading.timeout.infinitetimespan).</span></span> <span data-ttu-id="66b02-224">기본값은 1분입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-224">The default is 1 minute.</span></span> |

<span data-ttu-id="66b02-225">세션은 쿠키를 사용하여 단일 브라우저에서 요청을 추적하고 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-225">Session uses a cookie to track and identify requests from a single browser.</span></span> <span data-ttu-id="66b02-226">기본적으로 이 쿠키는 `.AspNetCore.Session`이라고 하며 `/`의 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-226">By default, this cookie is named `.AspNetCore.Session`, and it uses a path of `/`.</span></span> <span data-ttu-id="66b02-227">쿠키 기본값은 도메인을 지정하지 않으므로([HttpOnly](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.httponly) 기본값이 `true`임으로) 페이지의 클라이언트 쪽 스크립트에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-227">Because the cookie default doesn't specify a domain, it isn't made available to the client-side script on the page (because [HttpOnly](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.httponly) defaults to `true`).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

| <span data-ttu-id="66b02-228">옵션</span><span class="sxs-lookup"><span data-stu-id="66b02-228">Option</span></span> | <span data-ttu-id="66b02-229">설명</span><span class="sxs-lookup"><span data-stu-id="66b02-229">Description</span></span> |
| ------ | ----------- |
| [<span data-ttu-id="66b02-230">CookieDomain</span><span class="sxs-lookup"><span data-stu-id="66b02-230">CookieDomain</span></span>](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.cookiedomain) | <span data-ttu-id="66b02-231">쿠키를 만드는 데 사용되는 도메인을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-231">Determines the domain used to create the cookie.</span></span> <span data-ttu-id="66b02-232">`CookieDomain`은 기본적으로 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-232">`CookieDomain` isn't set by default.</span></span> |
| [<span data-ttu-id="66b02-233">CookieHttpOnly</span><span class="sxs-lookup"><span data-stu-id="66b02-233">CookieHttpOnly</span></span>](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.cookiehttponly) | <span data-ttu-id="66b02-234">브라우저가 클라이언트 쪽 JavaScript의 쿠키 액세스를 허용할지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-234">Determines if the browser should allow the cookie to be accessed by client-side JavaScript.</span></span> <span data-ttu-id="66b02-235">기본값은 `true`이며, 이는 쿠키가 HTTP 요청에만 전달되고 페이지의 스크립트에는 제공되지 않음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-235">The default is `true`, which means the cookie is only passed to HTTP requests and isn't made available to script on the page.</span></span> |
| [<span data-ttu-id="66b02-236">CookieName</span><span class="sxs-lookup"><span data-stu-id="66b02-236">CookieName</span></span>](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.cookiename) | <span data-ttu-id="66b02-237">세션 ID를 유지하는 데 사용되는 쿠키 이름을 결정합니다</span><span class="sxs-lookup"><span data-stu-id="66b02-237">Determines the cookie name used to persist the session ID.</span></span> <span data-ttu-id="66b02-238">기본값은 [SessionDefaults.CookieName](/dotnet/api/microsoft.aspnetcore.session.sessiondefaults.cookiename)(`.AspNetCore.Session`)입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-238">The default is [SessionDefaults.CookieName](/dotnet/api/microsoft.aspnetcore.session.sessiondefaults.cookiename) (`.AspNetCore.Session`).</span></span> |
| [<span data-ttu-id="66b02-239">CookiePath</span><span class="sxs-lookup"><span data-stu-id="66b02-239">CookiePath</span></span>](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.cookiepath) | <span data-ttu-id="66b02-240">쿠키를 만드는 데 사용되는 경로를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-240">Determines the path used to create the cookie.</span></span> <span data-ttu-id="66b02-241">기본값은 [SessionDefaults.CookiePath](/dotnet/api/microsoft.aspnetcore.session.sessiondefaults.cookiepath)(`/`)입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-241">Defaults to [SessionDefaults.CookiePath](/dotnet/api/microsoft.aspnetcore.session.sessiondefaults.cookiepath) (`/`).</span></span> |
| [<span data-ttu-id="66b02-242">CookieSecure</span><span class="sxs-lookup"><span data-stu-id="66b02-242">CookieSecure</span></span>](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.cookiesecure) | <span data-ttu-id="66b02-243">쿠키를 HTTPS 요청에서만 전송할지를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-243">Determines if the cookie should only be transmitted on HTTPS requests.</span></span> <span data-ttu-id="66b02-244">기본값은 [CookieSecurePolicy.None](/dotnet/api/microsoft.aspnetcore.http.cookiesecurepolicy)(`2`)입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-244">The default is [CookieSecurePolicy.None](/dotnet/api/microsoft.aspnetcore.http.cookiesecurepolicy) (`2`).</span></span> |
| [<span data-ttu-id="66b02-245">IdleTimeout</span><span class="sxs-lookup"><span data-stu-id="66b02-245">IdleTimeout</span></span>](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.idletimeout) | <span data-ttu-id="66b02-246">`IdleTimeout`은 콘텐츠가 삭제되기 전까지 세션이 유휴 상태일 수 있는 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-246">The `IdleTimeout` indicates how long the session can be idle before its contents are abandoned.</span></span> <span data-ttu-id="66b02-247">각 세션 액세스는 시간 제한을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-247">Each session access resets the timeout.</span></span> <span data-ttu-id="66b02-248">이는 쿠키가 아닌 세션의 콘텐츠에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-248">Note this only applies to the content of the session, not the cookie.</span></span> <span data-ttu-id="66b02-249">기본값은 20분입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-249">The default is 20 minutes.</span></span> |

<span data-ttu-id="66b02-250">세션은 쿠키를 사용하여 단일 브라우저에서 요청을 추적하고 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-250">Session uses a cookie to track and identify requests from a single browser.</span></span> <span data-ttu-id="66b02-251">기본적으로 이 쿠키는 `.AspNet.Session`이라고 하며 `/`의 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-251">By default, this cookie is named `.AspNet.Session`, and it uses a path of `/`.</span></span>

::: moniker-end

<span data-ttu-id="66b02-252">쿠키 세션 기본값을 재정의하려면 `SessionOptions`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-252">To override cookie session defaults, use `SessionOptions`:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-state/samples_snapshot/2.x/SessionSample/Startup.cs?name=snippet1&highlight=13-18)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](app-state/samples_snapshot/1.x/SessionSample/Startup.cs?name=snippet1&highlight=5-9)]

::: moniker-end

<span data-ttu-id="66b02-253">앱은 [IdleTimeout](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.idletimeout) 속성을 사용하여 서버 캐시의 콘텐츠가 중단되기 전에 유휴 상태일 수 있는 세션의 기간을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-253">The app uses the [IdleTimeout](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.idletimeout) property to determine how long a session can be idle before its contents in the server's cache are abandoned.</span></span> <span data-ttu-id="66b02-254">이 속성은 쿠키 만료와 무관합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-254">This property is independent of the cookie expiration.</span></span> <span data-ttu-id="66b02-255">[세션 미들웨어](/dotnet/api/microsoft.aspnetcore.session.sessionmiddleware)를 통해 전달되는 각 요청은 시간 제한을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-255">Each request that passes through the [Session Middleware](/dotnet/api/microsoft.aspnetcore.session.sessionmiddleware) resets the timeout.</span></span>

<span data-ttu-id="66b02-256">세션 상태는 *잠그지 않음*입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-256">Session state is *non-locking*.</span></span> <span data-ttu-id="66b02-257">두 요청이 동시에 세션의 콘텐츠를 수정하려고 하는 경우 마지막 요청이 첫 번째 요청을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-257">If two requests simultaneously attempt to modify the contents of a session, the last request overrides the first.</span></span> <span data-ttu-id="66b02-258">`Session`은 *일관된 세션*으로 구현됩니다. 즉, 모든 콘텐츠는 함께 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-258">`Session` is implemented as a *coherent session*, which means that all the contents are stored together.</span></span> <span data-ttu-id="66b02-259">두 요청이 서로 다른 세션 값을 수정하려고 할 때 마지막 요청이 첫 번째 요청에 의해 수행된 세션 변경 내용을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-259">When two requests seek to modify different session values, the last request may override session changes made by the first.</span></span>

### <a name="set-and-get-session-values"></a><span data-ttu-id="66b02-260">세션 값 설정 및 가져오기</span><span class="sxs-lookup"><span data-stu-id="66b02-260">Set and get Session values</span></span>

<span data-ttu-id="66b02-261">세션 상태는 [HttpContext.Session](/dotnet/api/microsoft.aspnetcore.http.httpcontext.session)이 포함된 Razor Pages [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) 클래스 또는 MVC [Controller](/dotnet/api/microsoft.aspnetcore.mvc.controller) 클래스에서 액세스됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-261">Session state is accessed from a Razor Pages [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) class or MVC [Controller](/dotnet/api/microsoft.aspnetcore.mvc.controller) class with [HttpContext.Session](/dotnet/api/microsoft.aspnetcore.http.httpcontext.session).</span></span> <span data-ttu-id="66b02-262">이 속성은 [ISession](/dotnet/api/microsoft.aspnetcore.http.isession) 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-262">This property is an [ISession](/dotnet/api/microsoft.aspnetcore.http.isession) implementation.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="66b02-263">`ISession` 구현은 정수 및 문자열 값을 설정 및 검색하는 몇 가지 확장 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-263">The `ISession` implementation provides several extension methods to set and retrieve integer and string values.</span></span> <span data-ttu-id="66b02-264">확장 메서드는 [Microsoft.AspNetCore.Http.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.Http.Extensions/) 패키지가 프로젝트에서 참조될 때, [Microsoft.AspNetCore.Http](/dotnet/api/microsoft.aspnetcore.http) 네임스페이스에 있습니다(확장 메서드에 액세스하려면 `using Microsoft.AspNetCore.Http;` 문 추가).</span><span class="sxs-lookup"><span data-stu-id="66b02-264">The extension methods are in the [Microsoft.AspNetCore.Http](/dotnet/api/microsoft.aspnetcore.http) namespace (add a `using Microsoft.AspNetCore.Http;` statement to gain access to the extension methods) when the [Microsoft.AspNetCore.Http.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.Http.Extensions/) package is referenced by the project.</span></span> <span data-ttu-id="66b02-265">두 패키지 모두 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-265">Both packages are included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="66b02-266">`ISession` 구현은 정수 및 문자열 값을 설정 및 검색하는 몇 가지 확장 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-266">The `ISession` implementation provides several extension methods to set and retreive integer and string values.</span></span> <span data-ttu-id="66b02-267">확장 메서드는 [Microsoft.AspNetCore.Http.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.Http.Extensions/) 패키지가 프로젝트에서 참조될 때, [Microsoft.AspNetCore.Http](/dotnet/api/microsoft.aspnetcore.http) 네임스페이스에 있습니다(확장 메서드에 액세스하려면 `using Microsoft.AspNetCore.Http;` 문 추가).</span><span class="sxs-lookup"><span data-stu-id="66b02-267">The extension methods are in the [Microsoft.AspNetCore.Http](/dotnet/api/microsoft.aspnetcore.http) namespace (add a `using Microsoft.AspNetCore.Http;` statement to gain access to the extension methods) when the [Microsoft.AspNetCore.Http.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.Http.Extensions/) package is referenced by the project.</span></span>

::: moniker-end

<span data-ttu-id="66b02-268">`ISession` 확장명 메서드:</span><span class="sxs-lookup"><span data-stu-id="66b02-268">`ISession` extension methods:</span></span>

* [<span data-ttu-id="66b02-269">Get(ISession, String)</span><span class="sxs-lookup"><span data-stu-id="66b02-269">Get(ISession, String)</span></span>](/dotnet/api/microsoft.aspnetcore.http.sessionextensions.get)
* [<span data-ttu-id="66b02-270">GetInt32(ISession, String)</span><span class="sxs-lookup"><span data-stu-id="66b02-270">GetInt32(ISession, String)</span></span>](/dotnet/api/microsoft.aspnetcore.http.sessionextensions.getint32)
* [<span data-ttu-id="66b02-271">GetString(ISession, String)</span><span class="sxs-lookup"><span data-stu-id="66b02-271">GetString(ISession, String)</span></span>](/dotnet/api/microsoft.aspnetcore.http.sessionextensions.getstring)
* [<span data-ttu-id="66b02-272">SetInt32(ISession, String, Int32)</span><span class="sxs-lookup"><span data-stu-id="66b02-272">SetInt32(ISession, String, Int32)</span></span>](/dotnet/api/microsoft.aspnetcore.http.sessionextensions.setint32)
* [<span data-ttu-id="66b02-273">SetString(ISession, String, String)</span><span class="sxs-lookup"><span data-stu-id="66b02-273">SetString(ISession, String, String)</span></span>](/dotnet/api/microsoft.aspnetcore.http.sessionextensions.setstring)

<span data-ttu-id="66b02-274">다음 예제에서는 Razor Pages 페이지에서 `IndexModel.SessionKeyName` 키(샘플 앱의 `_Name`)의 세션 값을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-274">The following example retrieves the session value for the `IndexModel.SessionKeyName` key (`_Name` in the sample app) in a Razor Pages page:</span></span>

```csharp
@page
@using Microsoft.AspNetCore.Http
@model IndexModel

...

Name: @HttpContext.Session.GetString(IndexModel.SessionKeyName)
```

<span data-ttu-id="66b02-275">다음 예제에서는 정수와 문자열을 설정하고 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-275">The following example shows how to set and get an integer and a string:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-state/samples/2.x/SessionSample/Pages/Index.cshtml.cs?name=snippet1&highlight=18-19,22-23)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](app-state/samples/1.x/SessionSample/Controllers/HomeController.cs?name=snippet1&highlight=10-11,18-19)]

::: moniker-end

<span data-ttu-id="66b02-276">메모리 내 캐시를 사용하는 경우에도, 분산된 캐시 시나리오를 사용하려면 모든 세션 데이터를 직렬화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-276">All session data must be serialized to enable a distributed cache scenario, even when using the in-memory cache.</span></span> <span data-ttu-id="66b02-277">최소 문자열 및 숫자 직렬화가 제공됩니다([ISession](/dotnet/api/microsoft.aspnetcore.http.isession)의 메서드와 확장 메서드 참조).</span><span class="sxs-lookup"><span data-stu-id="66b02-277">Minimal string and number serializers are provided (see the methods and extension methods of [ISession](/dotnet/api/microsoft.aspnetcore.http.isession)).</span></span> <span data-ttu-id="66b02-278">복합 형식은 JSON과 같은 다른 메커니즘을 사용하여 사용자가 직렬화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-278">Complex types must be serialized by the user using another mechanism, such as JSON.</span></span>

<span data-ttu-id="66b02-279">다음 확장 메서드를 추가하여 직렬화 가능 개체를 설정하고 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-279">Add the following extension methods to set and get serializable objects:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-state/samples/2.x/SessionSample/Extensions/SessionExtensions.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](app-state/samples/1.x/SessionSample/Extensions/SessionExtensions.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="66b02-280">다음 예제에서는 확장 메서드를 사용하여 직렬화 가능 개체를 설정하고 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-280">The following example shows how to set and get a serializable object with the extension methods:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-state/samples/2.x/SessionSample/Pages/Index.cshtml.cs?name=snippet2)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](app-state/samples/1.x/SessionSample/Controllers/HomeController.cs?name=snippet2&highlight=4,12)]

::: moniker-end

## <a name="tempdata"></a><span data-ttu-id="66b02-281">TempData</span><span class="sxs-lookup"><span data-stu-id="66b02-281">TempData</span></span>

<span data-ttu-id="66b02-282">ASP.NET Core는 [Razor Pages 페이지 모델의 TempData 속성](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.tempdata) 또는 [MVC 컨트롤러의 TempData](/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata)를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-282">ASP.NET Core exposes the [TempData property of a Razor Pages page model](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.tempdata) or [TempData of an MVC controller](/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata).</span></span> <span data-ttu-id="66b02-283">이 속성은 해당 속성이 읽혀질 때까지만 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-283">This property stores data until it's read.</span></span> <span data-ttu-id="66b02-284">[Keep](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.itempdatadictionary.keep) 및 [Peek](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.itempdatadictionary.peek) 메서드를 사용하여 삭제 없이 데이터를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-284">The [Keep](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.itempdatadictionary.keep) and [Peek](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.itempdatadictionary.peek) methods can be used to examine the data without deletion.</span></span> <span data-ttu-id="66b02-285">TempData는 두 개 이상의 요청에 데이터가 필요한 리디렉션에 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-285">TempData is particularly useful for redirection when data is required for more than a single request.</span></span> <span data-ttu-id="66b02-286">TempData는 TempData 공급자가 쿠키 또는 세션 상태를 사용하여 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-286">TempData is implemented by TempData providers using either cookies or session state.</span></span>

### <a name="tempdata-providers"></a><span data-ttu-id="66b02-287">TempData 공급자</span><span class="sxs-lookup"><span data-stu-id="66b02-287">TempData providers</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="66b02-288">ASP.NET Core 2.0 이상에서 쿠키 기반 TempData 공급자는 TempData를 쿠키에 저장하는 데 기본적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-288">In ASP.NET Core 2.0 or later, the cookie-based TempData provider is used by default to store TempData in cookies.</span></span>

<span data-ttu-id="66b02-289">쿠키 데이터는 [IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector)를 사용하여 암호화되고, [Base64UrlTextEncoder](/dotnet/api/microsoft.aspnetcore.webutilities.base64urltextencoder)로 인코딩된 후 청크 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-289">The cookie data is encrypted using [IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector), encoded with [Base64UrlTextEncoder](/dotnet/api/microsoft.aspnetcore.webutilities.base64urltextencoder), then chunked.</span></span> <span data-ttu-id="66b02-290">쿠키가 청크 분할되므로 ASP.NET Core 1.x에서 확인한 단일 쿠키 크기 제한은 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-290">Because the cookie is chunked, the single cookie size limit found in ASP.NET Core 1.x doesn't apply.</span></span> <span data-ttu-id="66b02-291">암호화된 데이터를 압축하는 것은 [범죄](https://wikipedia.org/wiki/CRIME_(security_exploit)) 및 [위반](https://wikipedia.org/wiki/BREACH_(security_exploit)) 공격과 같은 보안 문제를 일으킬 수 있으므로 쿠키 데이터는 압축되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-291">The cookie data isn't compressed because compressing encrypted data can lead to security problems such as the [CRIME](https://wikipedia.org/wiki/CRIME_(security_exploit)) and [BREACH](https://wikipedia.org/wiki/BREACH_(security_exploit)) attacks.</span></span> <span data-ttu-id="66b02-292">쿠키 기반 TempData 공급자에 대한 자세한 내용은 [CookieTempDataProvider](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.cookietempdataprovider)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66b02-292">For more information on the cookie-based TempData provider, see [CookieTempDataProvider](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.cookietempdataprovider).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="66b02-293">ASP.NET Core 1.0 및 1.1에서는 세션 상태 TempData 공급자가 기본 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-293">In ASP.NET Core 1.0 and 1.1, the session state TempData provider is the default provider.</span></span>

::: moniker-end

### <a name="choose-a-tempdata-provider"></a><span data-ttu-id="66b02-294">TempData 공급자 선택</span><span class="sxs-lookup"><span data-stu-id="66b02-294">Choose a TempData provider</span></span>

<span data-ttu-id="66b02-295">TempData 공급자를 선택하는 데는 다음과 같은 몇 가지 고려 사항이 수반됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-295">Choosing a TempData provider involves several considerations, such as:</span></span>

1. <span data-ttu-id="66b02-296">앱이 이미 세션 상태를 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="66b02-296">Does the app already use session state?</span></span> <span data-ttu-id="66b02-297">그런 경우 세션 상태 TempData 공급자 사용에는 앱에 대한 추가 비용이 없습니다(데이터 크기 제외).</span><span class="sxs-lookup"><span data-stu-id="66b02-297">If so, using the session state TempData provider has no additional cost to the app (aside from the size of the data).</span></span>
2. <span data-ttu-id="66b02-298">앱은 상대적으로 적은 양의 데이터에 TempData만 제한적으로 사용합니까(최대 500바이트)?</span><span class="sxs-lookup"><span data-stu-id="66b02-298">Does the app use TempData only sparingly for relatively small amounts of data (up to 500 bytes)?</span></span> <span data-ttu-id="66b02-299">그런 경우 쿠키 TempData 공급자는 TempData를 전달하는 각 요청에 적은 비용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-299">If so, the cookie TempData provider adds a small cost to each request that carries TempData.</span></span> <span data-ttu-id="66b02-300">그렇지 않은 경우 세션 상태 TempData 공급자는 TempData가 사용될 때까지 각 요청에서 많은 양의 데이터를 왕복 작업하지 않도록 하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-300">If not, the session state TempData provider can be beneficial to avoid round-tripping a large amount of data in each request until the TempData is consumed.</span></span>
3. <span data-ttu-id="66b02-301">앱이 여러 서버의 서버 팜에서 실행됩니까?</span><span class="sxs-lookup"><span data-stu-id="66b02-301">Does the app run in a server farm on multiple servers?</span></span> <span data-ttu-id="66b02-302">그런 경우 데이터 보호 외부에서 쿠키 TempData 공급자를사용하는 데 필요한 추가 구성은 없습니다(<xref:security/data-protection/introduction> 및 [키 스토리지 공급자](xref:security/data-protection/implementation/key-storage-providers) 참조).</span><span class="sxs-lookup"><span data-stu-id="66b02-302">If so, there's no additional configuration required to use the cookie TempData provider outside of Data Protection (see <xref:security/data-protection/introduction> and [Key storage providers](xref:security/data-protection/implementation/key-storage-providers)).</span></span>

> [!NOTE]
> <span data-ttu-id="66b02-303">대부분의 웹 클라이언트(예: 웹 브라우저)는 각 쿠키의 최대 크기, 쿠키의 총 수 또는 둘 다에 제한을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-303">Most web clients (such as web browsers) enforce limits on the maximum size of each cookie, the total number of cookies, or both.</span></span> <span data-ttu-id="66b02-304">쿠키 TempData 공급자를 사용하는 경우 앱이 이러한 제한을 초과하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-304">When using the cookie TempData provider, verify the app won't exceed these limits.</span></span> <span data-ttu-id="66b02-305">데이터의 총 크기를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-305">Consider the total size of the data.</span></span> <span data-ttu-id="66b02-306">암호화 및 청크 분할로 인한 쿠키 크기 증가를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-306">Account for increases in cookie size due to encryption and chunking.</span></span>

### <a name="configure-the-tempdata-provider"></a><span data-ttu-id="66b02-307">TempData 공급자 구성</span><span class="sxs-lookup"><span data-stu-id="66b02-307">Configure the TempData provider</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="66b02-308">쿠키 기반 TempData 공급자는 기본적으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-308">The cookie-based TempData provider is enabled by default.</span></span>

<span data-ttu-id="66b02-309">세션 기반 TempData 공급자를 활성화하려면 [AddSessionStateTempDataProvider](/dotnet/api/microsoft.extensions.dependencyinjection.mvcviewfeaturesmvcbuilderextensions.addsessionstatetempdataprovider) 확장 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-309">To enable the session-based TempData provider, use the [AddSessionStateTempDataProvider](/dotnet/api/microsoft.extensions.dependencyinjection.mvcviewfeaturesmvcbuilderextensions.addsessionstatetempdataprovider) extension method:</span></span>

[!code-csharp[](app-state/samples_snapshot_2/2.x/SessionSample/Startup.cs?name=snippet1&highlight=11,13,32)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="66b02-310">다음 `Startup` 클래스 코드는 세션 기반 TempData 공급자를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-310">The following `Startup` class code configures the session-based TempData provider:</span></span>

[!code-csharp[](app-state/samples_snapshot_2/1.x/SessionSample/Startup.cs?name=snippet1&highlight=4,9)]

::: moniker-end

<span data-ttu-id="66b02-311">미들웨어의 순서가 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-311">The order of middleware is important.</span></span> <span data-ttu-id="66b02-312">앞의 예에서 `UseMvc` 이후에 `UseSession`이 호출되면 `InvalidOperationException` 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-312">In the preceding example, an `InvalidOperationException` exception occurs when `UseSession` is invoked after `UseMvc`.</span></span> <span data-ttu-id="66b02-313">자세한 내용은 [미들웨어 순서 지정](xref:fundamentals/middleware/index#order)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66b02-313">For more information, see [Middleware Ordering](xref:fundamentals/middleware/index#order).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="66b02-314">.NET Framework를 대상으로 하고 세션 기반 TempData 공급자를 사용하는 경우 [Microsoft.AspNetCore.Session](https://www.nuget.org/packages/Microsoft.AspNetCore.Session/) 패키지를 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-314">If targeting .NET Framework and using the session-based TempData provider, add the [Microsoft.AspNetCore.Session](https://www.nuget.org/packages/Microsoft.AspNetCore.Session/) package to the project.</span></span>

## <a name="query-strings"></a><span data-ttu-id="66b02-315">쿼리 문자열</span><span class="sxs-lookup"><span data-stu-id="66b02-315">Query strings</span></span>

<span data-ttu-id="66b02-316">제한된 양의 데이터는 새 요청의 쿼리 문자열에 추가하여 한 요청에서 다른 요청으로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-316">A limited amount of data can be passed from one request to another by adding it to the new request's query string.</span></span> <span data-ttu-id="66b02-317">이는 이메일 또는 소셜 네트워크를 통해 공유되도록 포함된 상태가 있는 링크를 허용하는 영구적인 방식으로 상태를 캡처하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-317">This is useful for capturing state in a persistent manner that allows links with embedded state to be shared through email or social networks.</span></span> <span data-ttu-id="66b02-318">URL 쿼리 문자열은 공용이므로 중요한 데이터에 쿼리 문자열을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="66b02-318">Because URL query strings are public, never use query strings for sensitive data.</span></span>

<span data-ttu-id="66b02-319">의도하지 않은 공유 외에도 쿼리 문자열에 데이터를 포함하면 사용자가 인증되는 동안 악성 사이트를 방문하도록 유도할 수 있는 [CSRF(교차 사이트 요청 위조)](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) 공격에 대한 기회를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-319">In addition to unintended sharing, including data in query strings can create opportunities for [Cross-Site Request Forgery (CSRF)](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) attacks, which can trick users into visiting malicious sites while authenticated.</span></span> <span data-ttu-id="66b02-320">공격자는 앱에서 사용자 데이터를 도용하거나 사용자를 대신하여 악의적인 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-320">Attackers can then steal user data from the app or take malicious actions on behalf of the user.</span></span> <span data-ttu-id="66b02-321">유지된 모든 앱 또는 세션 상태를 CSRF 공격으로부터 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-321">Any preserved app or session state must protect against CSRF attacks.</span></span> <span data-ttu-id="66b02-322">자세한 내용은 [교차 사이트 요청 위조(XSRF/CSRF) 공격 방지](xref:security/anti-request-forgery)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66b02-322">For more information, see [Prevent Cross-Site Request Forgery (XSRF/CSRF) attacks](xref:security/anti-request-forgery).</span></span>

## <a name="hidden-fields"></a><span data-ttu-id="66b02-323">숨겨진 필드</span><span class="sxs-lookup"><span data-stu-id="66b02-323">Hidden fields</span></span>

<span data-ttu-id="66b02-324">데이터는 숨겨진 양식 필드에 저장되고 다음 요청에서 다시 게시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-324">Data can be saved in hidden form fields and posted back on the next request.</span></span> <span data-ttu-id="66b02-325">이는 다중 페이지 폼에서 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-325">This is common in multi-page forms.</span></span> <span data-ttu-id="66b02-326">클라이언트는 잠재적으로 데이터를 변조할 수 있으므로 앱은 항상 숨겨진 필드에 저장된 데이터의 유효성을 다시 검사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-326">Because the client can potentially tamper with the data, the app must always revalidate the data stored in hidden fields.</span></span>

## <a name="httpcontextitems"></a><span data-ttu-id="66b02-327">HttpContext.Items</span><span class="sxs-lookup"><span data-stu-id="66b02-327">HttpContext.Items</span></span>

<span data-ttu-id="66b02-328">[HttpContext.Items](/dotnet/api/microsoft.aspnetcore.http.httpcontext.items) 컬렉션은 단일 요청을 처리하는 동안 데이터를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-328">The [HttpContext.Items](/dotnet/api/microsoft.aspnetcore.http.httpcontext.items) collection is used to store data while processing a single request.</span></span> <span data-ttu-id="66b02-329">컬렉션의 콘텐츠는 요청이 처리된 후 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-329">The collection's contents are discarded after a request is processed.</span></span> <span data-ttu-id="66b02-330">`Items` 컬렉션은 구성 요소 또는 미들웨어가 요청 중에 다른 시점에서 작동하고 매개 변수를 전달할 직접적인 방법이 없는 경우에 통신을 지원하기 위해 자주 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-330">The `Items` collection is often used to allow components or middleware to communicate when they operate at different points in time during a request and have no direct way to pass parameters.</span></span>

<span data-ttu-id="66b02-331">다음 예제에서 [미들웨어](xref:fundamentals/middleware/index)는 `Items` 컬렉션에 `isVerified`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-331">In the following example, [middleware](xref:fundamentals/middleware/index) adds `isVerified` to the `Items` collection.</span></span>

```csharp
app.Use(async (context, next) =>
{
    // perform some verification
    context.Items["isVerified"] = true;
    await next.Invoke();
});
```

<span data-ttu-id="66b02-332">파이프라인의 뒷부분에서 다른 미들웨어는 `isVerified` 값에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-332">Later in the pipeline, another middleware can access the value of `isVerified`:</span></span>

```csharp
app.Run(async (context) =>
{
    await context.Response.WriteAsync($"Verified: {context.Items["isVerified"]}");
});
```

<span data-ttu-id="66b02-333">단일 앱에서만 사용되는 미들웨어의 경우 `string` 키가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-333">For middleware that's only used by a single app, `string` keys are acceptable.</span></span> <span data-ttu-id="66b02-334">앱 인스턴스 간에 공유되는 미들웨어는 키 충돌을 방지하기 위해 고유한 개체 키를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-334">Middleware shared between app instances should use unique object keys to avoid key collisions.</span></span> <span data-ttu-id="66b02-335">다음 예제에서는 미들웨어 클래스에 정의된 고유한 개체 키를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-335">The following example shows how to use a unique object key defined in a middleware class:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-state/samples/2.x/SessionSample/Middleware/HttpContextItemsMiddleware.cs?name=snippet1&highlight=4,13)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](app-state/samples/1.x/SessionSample/Middleware/HttpContextItemsMiddleware.cs?name=snippet1&highlight=5,14)]

::: moniker-end

<span data-ttu-id="66b02-336">다른 코드는 미들웨어 클래스에 의해 노출된 키를 사용하여 `HttpContext.Items`에 저장된 값에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-336">Other code can access the value stored in `HttpContext.Items` using the key exposed by the middleware class:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-state/samples/2.x/SessionSample/Pages/Index.cshtml.cs?name=snippet3)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](app-state/samples/1.x/SessionSample/Controllers/HomeController.cs?name=snippet3)]

::: moniker-end

<span data-ttu-id="66b02-337">이 방법은 또한 코드에서 키 문자열을 사용하지 않아도 된다는 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-337">This approach also has the advantage of eliminating the use of key strings in the code.</span></span>

## <a name="cache"></a><span data-ttu-id="66b02-338">캐시</span><span class="sxs-lookup"><span data-stu-id="66b02-338">Cache</span></span>

<span data-ttu-id="66b02-339">캐싱은 데이터 저장 및 검색하는 효율적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-339">Caching is an efficient way to store and retrieve data.</span></span> <span data-ttu-id="66b02-340">앱은 캐시된 항목의 수명을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-340">The app can control the lifetime of cached items.</span></span>

<span data-ttu-id="66b02-341">캐시된 데이터는 특정 요청, 사용자 또는 세션과 연관되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-341">Cached data isn't associated with a specific request, user, or session.</span></span> <span data-ttu-id="66b02-342">**다른 사용자의 요청으로 검색될 수 있는 사용자별 데이터를 캐시하지 않도록 주의합니다.**</span><span class="sxs-lookup"><span data-stu-id="66b02-342">**Be careful not to cache user-specific data that may be retrieved by other users' requests.**</span></span>

<span data-ttu-id="66b02-343">자세한 내용은 <xref:performance/caching/response>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66b02-343">For more information, see <xref:performance/caching/response>.</span></span>

## <a name="dependency-injection"></a><span data-ttu-id="66b02-344">종속성 주입</span><span class="sxs-lookup"><span data-stu-id="66b02-344">Dependency Injection</span></span>

<span data-ttu-id="66b02-345">[종속성 주입](xref:fundamentals/dependency-injection)을 사용하여 모든 사용자에게 데이터를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-345">Use [Dependency Injection](xref:fundamentals/dependency-injection) to make data available to all users:</span></span>

1. <span data-ttu-id="66b02-346">데이터를 포함하는 서비스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-346">Define a service containing the data.</span></span> <span data-ttu-id="66b02-347">예를 들어 `MyAppData`라는 클래스가 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-347">For example, a class named `MyAppData` is defined:</span></span>

    ```csharp
    public class MyAppData
    {
        // Declare properties and methods
    }
    ```

2. <span data-ttu-id="66b02-348">`Startup.ConfigureServices`에 서비스 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-348">Add the service class to `Startup.ConfigureServices`:</span></span>

    ```csharp
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddSingleton<MyAppData>();
    }
    ```

3. <span data-ttu-id="66b02-349">데이터 서비스 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-349">Consume the data service class:</span></span>

    ::: moniker range=">= aspnetcore-2.0"

    ```csharp
    public class IndexModel : PageModel
    {
        public IndexModel(MyAppData myService)
        {
            // Do something with the service
            //    Examples: Read data, store in a field or property
        }
    }
    ```

    ::: moniker-end

    ::: moniker range="< aspnetcore-2.0"

    ```csharp
    public class HomeController : Controller
    {
        public HomeController(MyAppData myService)
        {
            // Do something with the service
            //    Examples: Read data, store in a field or property
        }
    }
    ```

    ::: moniker-end

## <a name="common-errors"></a><span data-ttu-id="66b02-350">일반적인 오류</span><span class="sxs-lookup"><span data-stu-id="66b02-350">Common errors</span></span>

* <span data-ttu-id="66b02-351">"'Microsoft.AspNetCore.Session.DistributedSessionStore'를 활성화하려고 시도하는 동안 'Microsoft.Extensions.Caching.Distributed.IDistributedCache' 형식에 대한 서비스를 확인할 수 없습니다."</span><span class="sxs-lookup"><span data-stu-id="66b02-351">"Unable to resolve service for type 'Microsoft.Extensions.Caching.Distributed.IDistributedCache' while attempting to activate 'Microsoft.AspNetCore.Session.DistributedSessionStore'."</span></span>

  <span data-ttu-id="66b02-352">이는 일반적으로는 하나 이상의 `IDistributedCache` 구현을 구성하는 데 실패하여 발생됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-352">This is usually caused by failing to configure at least one `IDistributedCache` implementation.</span></span> <span data-ttu-id="66b02-353">자세한 내용은 <xref:performance/caching/distributed> 및 <xref:performance/caching/memory>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66b02-353">For more information, see <xref:performance/caching/distributed> and <xref:performance/caching/memory>.</span></span>

* <span data-ttu-id="66b02-354">세션 미들웨어가 세션 유지에 실패할 경우(예: 백업 저장소를 사용할 수 없는 경우) 미들웨어는 예외를 기록하고 요청은 정상적으로 계속됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-354">In the event that the session middleware fails to persist a session (for example, if the backing store isn't available), the middleware logs the exception and the request continues normally.</span></span> <span data-ttu-id="66b02-355">이로 인해 예기치 않은 동작이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-355">This leads to unpredictable behavior.</span></span>

  <span data-ttu-id="66b02-356">예를 들어 사용자는 세션에 쇼핑 카트를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-356">For example, a user stores a shopping cart in session.</span></span> <span data-ttu-id="66b02-357">사용자가 카트에 항목을 추가하지만 커밋이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-357">The user adds an item to the cart but the commit fails.</span></span> <span data-ttu-id="66b02-358">앱은 실패에 대해 알지 못하므로 항목이 카트에 추가되었다고 보고하지만, 이는 사실이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-358">The app doesn't know about the failure so it reports to the user that the item was added to their cart, which isn't true.</span></span>

  <span data-ttu-id="66b02-359">권장되는 오류 확인 방법은 앱이 세션에 작성을 완료하면 앱 코드에서 `await feature.Session.CommitAsync();`를 호출하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-359">The recommended approach to check for errors is to call `await feature.Session.CommitAsync();` from app code when the app is done writing to the session.</span></span> <span data-ttu-id="66b02-360">백업 저장소를 사용할 수 없는 경우 `CommitAsync`에서 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-360">`CommitAsync` throws an exception if the backing store is unavailable.</span></span> <span data-ttu-id="66b02-361">`CommitAsync`가 실패하면 앱에서 예외를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-361">If `CommitAsync` fails, the app can process the exception.</span></span> <span data-ttu-id="66b02-362">`LoadAsync`는 같은 조건에서 데이터 저장소를 사용할 수 없는 경우 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b02-362">`LoadAsync` throws under the same conditions where the data store is unavailable.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="66b02-363">추가 자료</span><span class="sxs-lookup"><span data-stu-id="66b02-363">Additional resources</span></span>

<xref:host-and-deploy/web-farm>
