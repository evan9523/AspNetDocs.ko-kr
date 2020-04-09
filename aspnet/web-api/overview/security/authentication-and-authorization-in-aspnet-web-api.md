---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: ASP.NET 웹 API의 인증 및 권한 부여 | 마이크로 소프트 문서
author: MikeWasson
description: ASP.NET 웹 API에서 인증 및 권한 부여에 대한 일반적인 개요를 제공합니다.
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675864"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a><span data-ttu-id="c9d87-103">ASP.NET Web API의 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="c9d87-103">Authentication and Authorization in ASP.NET Web API</span></span>

<span data-ttu-id="c9d87-104">로 [마이크 와슨](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c9d87-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="c9d87-105">웹 API를 만들었지만 이제 웹 API에 대한 액세스를 제어하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-105">You've created a web API, but now you want to control access to it.</span></span> <span data-ttu-id="c9d87-106">이 문서 시리즈에서는 권한이 있는 사용자로부터 웹 API를 보호하기 위한 몇 가지 옵션을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-106">In this series of articles, we'll look at some options for securing a web API from unauthorized users.</span></span> <span data-ttu-id="c9d87-107">이 시리즈에서는 인증 및 권한 부여를 모두 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-107">This series will cover both authentication and authorization.</span></span>

- <span data-ttu-id="c9d87-108">*인증은* 사용자의 ID를 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-108">*Authentication* is knowing the identity of the user.</span></span> <span data-ttu-id="c9d87-109">예를 들어 Alice는 사용자 이름과 암호를 사용하여 로그인하고 서버는 암호를 사용하여 Alice를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-109">For example, Alice logs in with her username and password, and the server uses the password to authenticate Alice.</span></span>
- <span data-ttu-id="c9d87-110">*권한 부여는* 사용자가 작업을 수행할 수 있는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-110">*Authorization* is deciding whether a user is allowed to perform an action.</span></span> <span data-ttu-id="c9d87-111">예를 들어 Alice에는 리소스를 얻을 수 있지만 리소스를 만들 수 있는 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-111">For example, Alice has permission to get a resource but not create a resource.</span></span>

<span data-ttu-id="c9d87-112">시리즈의 첫 번째 문서에서는 ASP.NET 웹 API에서 인증 및 권한 부여에 대한 일반적인 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-112">The first article in the series gives a general overview of authentication and authorization in ASP.NET Web API.</span></span> <span data-ttu-id="c9d87-113">다른 항목에서는 Web API에 대한 일반적인 인증 시나리오를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-113">Other topics describe common authentication scenarios for Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="c9d87-114">릭 앤더슨, 레비 브로데릭, 배리 도란스, 톰 다이크스트라, 홍메이 게, 데이비드 맷슨, 다니엘 로스, 팀 티켄 등 이 시리즈를 검토하고 귀중한 피드백을 제공한 분들께 감사드립니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-114">Thanks to the people who reviewed this series and provided valuable feedback: Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken.</span></span>

## <a name="authentication"></a><span data-ttu-id="c9d87-115">인증</span><span class="sxs-lookup"><span data-stu-id="c9d87-115">Authentication</span></span>

<span data-ttu-id="c9d87-116">Web API는 인증이 호스트에서 발생한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-116">Web API assumes that authentication happens in the host.</span></span> <span data-ttu-id="c9d87-117">웹 호스팅의 경우 호스트는 인증을 위해 HTTP 모듈을 사용하는 IIS입니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-117">For web-hosting, the host is IIS, which uses HTTP modules for authentication.</span></span> <span data-ttu-id="c9d87-118">IIS 또는 ASP.NET 내장된 인증 모듈을 사용하도록 프로젝트를 구성하거나 사용자 지정 인증을 수행하기 위해 자체 HTTP 모듈을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-118">You can configure your project to use any of the authentication modules built in to IIS or ASP.NET, or write your own HTTP module to perform custom authentication.</span></span>

<span data-ttu-id="c9d87-119">호스트가 사용자를 인증하면 코드가 실행 중인 보안 컨텍스트를 나타내는 [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) 개체인 *보안 주체를*만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-119">When the host authenticates the user, it creates a *principal*, which is an [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) object that represents the security context under which code is running.</span></span> <span data-ttu-id="c9d87-120">호스트는 **Thread.CurrentPrincipal을**설정하여 현재 스레드에 주체를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-120">The host attaches the principal to the current thread by setting **Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="c9d87-121">보안 주체에는 사용자에 대한 정보가 포함된 연결된 **Identity** 개체가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-121">The principal contains an associated **Identity** object that contains information about the user.</span></span> <span data-ttu-id="c9d87-122">사용자가 인증된 경우 **Identity.Is인증** 속성은 **true를**반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-122">If the user is authenticated, the **Identity.IsAuthenticated** property returns **true**.</span></span> <span data-ttu-id="c9d87-123">익명 요청의 경우 **Is인증은** **false를 반환합니다.**</span><span class="sxs-lookup"><span data-stu-id="c9d87-123">For anonymous requests, **IsAuthenticated** returns **false**.</span></span> <span data-ttu-id="c9d87-124">보안 주체에 대한 자세한 내용은 [역할 기반 보안](https://msdn.microsoft.com/library/shz8h065.aspx)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="c9d87-124">For more information about principals, see [Role-Based Security](https://msdn.microsoft.com/library/shz8h065.aspx).</span></span>

### <a name="http-message-handlers-for-authentication"></a><span data-ttu-id="c9d87-125">인증을 위한 HTTP 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="c9d87-125">HTTP Message Handlers for Authentication</span></span>

<span data-ttu-id="c9d87-126">인증을 위해 호스트를 사용하는 대신 HTTP 메시지 [처리기에](../advanced/http-message-handlers.md)인증 논리를 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-126">Instead of using the host for authentication, you can put authentication logic into an [HTTP message handler](../advanced/http-message-handlers.md).</span></span> <span data-ttu-id="c9d87-127">이 경우 메시지 처리기는 HTTP 요청을 검사하고 보안 주체를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-127">In that case, the message handler examines the HTTP request and sets the principal.</span></span>

<span data-ttu-id="c9d87-128">인증에 메시지 처리기를 언제 사용해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="c9d87-128">When should you use message handlers for authentication?</span></span> <span data-ttu-id="c9d87-129">다음은 몇 가지 장단점입니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-129">Here are some tradeoffs:</span></span>

- <span data-ttu-id="c9d87-130">HTTP 모듈은 ASP.NET 파이프라인을 통과하는 모든 요청을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-130">An HTTP module sees all requests that go through the ASP.NET pipeline.</span></span> <span data-ttu-id="c9d87-131">메시지 처리기는 웹 API로 라우팅되는 요청만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-131">A message handler only sees requests that are routed to Web API.</span></span>
- <span data-ttu-id="c9d87-132">특정 경로에 인증 체계를 적용할 수 있는 경로별 메시지 처리기를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-132">You can set per-route message handlers, which lets you apply an authentication scheme to a specific route.</span></span>
- <span data-ttu-id="c9d87-133">HTTP 모듈은 IIS에만 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-133">HTTP modules are specific to IIS.</span></span> <span data-ttu-id="c9d87-134">메시지 처리기는 호스트에 구애받지 않으므로 웹 호스팅과 자체 호스팅모두에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-134">Message handlers are host-agnostic, so they can be used with both web-hosting and self-hosting.</span></span>
- <span data-ttu-id="c9d87-135">HTTP 모듈은 IIS 로깅, 감사 등에 참여합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-135">HTTP modules participate in IIS logging, auditing, and so on.</span></span>
- <span data-ttu-id="c9d87-136">HTTP 모듈은 파이프라인의 앞에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-136">HTTP modules run earlier in the pipeline.</span></span> <span data-ttu-id="c9d87-137">메시지 처리기에서 인증을 처리하는 경우 처리기가 실행될 때까지 보안 주체가 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-137">If you handle authentication in a message handler, the principal does not get set until the handler runs.</span></span> <span data-ttu-id="c9d87-138">또한 응답이 메시지 처리기를 떠날 때 주 서버는 이전 주 서버로 되돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-138">Moreover, the principal reverts back to the previous principal when the response leaves the message handler.</span></span>

<span data-ttu-id="c9d87-139">일반적으로 자체 호스팅을 지원할 필요가 없는 경우 HTTP 모듈이 더 나은 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-139">Generally, if you don't need to support self-hosting, an HTTP module is a better option.</span></span> <span data-ttu-id="c9d87-140">자체 호스팅을 지원해야 하는 경우 메시지 처리기를 고려하십시오.</span><span class="sxs-lookup"><span data-stu-id="c9d87-140">If you need to support self-hosting, consider a message handler.</span></span>

### <a name="setting-the-principal"></a><span data-ttu-id="c9d87-141">보안 주체 설정</span><span class="sxs-lookup"><span data-stu-id="c9d87-141">Setting the Principal</span></span>

<span data-ttu-id="c9d87-142">응용 프로그램에서 사용자 지정 인증 논리를 수행하는 경우 다음 두 위치에 보안 주체를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-142">If your application performs any custom authentication logic, you must set the principal on two places:</span></span>

- <span data-ttu-id="c9d87-143">**스레드.현재 주체**.</span><span class="sxs-lookup"><span data-stu-id="c9d87-143">**Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="c9d87-144">이 속성은 .NET에서 스레드의 주체를 설정하는 표준 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-144">This property is the standard way to set the thread's principal in .NET.</span></span>
- <span data-ttu-id="c9d87-145">**HttpContext.현재.사용자**.</span><span class="sxs-lookup"><span data-stu-id="c9d87-145">**HttpContext.Current.User**.</span></span> <span data-ttu-id="c9d87-146">이 속성은 ASP.NET 한정입니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-146">This property is specific to ASP.NET.</span></span>

<span data-ttu-id="c9d87-147">다음 코드는 보안 주체를 설정하는 방법을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-147">The following code shows how to set the principal:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="c9d87-148">웹 호스팅의 경우 두 위치에서 보안 주체를 설정해야 합니다. 그렇지 않으면 보안 컨텍스트가 일치하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-148">For web-hosting, you must set the principal in both places; otherwise the security context may become inconsistent.</span></span> <span data-ttu-id="c9d87-149">그러나 자체 호스팅의 경우 **HttpContext.Current는** null입니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-149">For self-hosting, however, **HttpContext.Current** is null.</span></span> <span data-ttu-id="c9d87-150">따라서 코드가 호스트에 불가지않는지 확인하려면 그림과 같이 **HttpContext.Current에**할당하기 전에 null을 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="c9d87-150">To ensure your code is host-agnostic, therefore, check for null before assigning to **HttpContext.Current**, as shown.</span></span>

## <a name="authorization"></a><span data-ttu-id="c9d87-151">권한 부여</span><span class="sxs-lookup"><span data-stu-id="c9d87-151">Authorization</span></span>

<span data-ttu-id="c9d87-152">권한 부여는 파이프라인의 나중에 컨트롤러에 더 가깝게 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-152">Authorization happens later in the pipeline, closer to the controller.</span></span> <span data-ttu-id="c9d87-153">이렇게 하면 리소스에 대한 액세스 권한을 부여할 때 보다 세부적인 선택을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-153">That lets you make more granular choices when you grant access to resources.</span></span>

- <span data-ttu-id="c9d87-154">*권한 부여 필터는* 컨트롤러 작업 전에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-154">*Authorization filters* run before the controller action.</span></span> <span data-ttu-id="c9d87-155">요청이 승인되지 않은 경우 필터는 오류 응답을 반환하고 작업이 호출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-155">If the request is not authorized, the filter returns an error response, and the action is not invoked.</span></span>
- <span data-ttu-id="c9d87-156">컨트롤러 작업 내에서 **ApiController.User** 속성에서 현재 보안 주체를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-156">Within a controller action, you can get the current principal from the **ApiController.User** property.</span></span> <span data-ttu-id="c9d87-157">예를 들어 사용자 이름을 기반으로 리소스 목록을 필터링하여 해당 사용자에 속한 리소스만 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-157">For example, you might filter a list of resources based on the user name, returning only those resources that belong to that user.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a><span data-ttu-id="c9d87-158">[권한 부여] 특성 사용</span><span class="sxs-lookup"><span data-stu-id="c9d87-158">Using the [Authorize] Attribute</span></span>

<span data-ttu-id="c9d87-159">웹 API는 기본 제공 권한 부여 필터인 [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-159">Web API provides a built-in authorization filter, [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx).</span></span> <span data-ttu-id="c9d87-160">이 필터는 사용자가 인증되었는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-160">This filter checks whether the user is authenticated.</span></span> <span data-ttu-id="c9d87-161">그렇지 않은 경우 작업을 호출하지 않고 HTTP 상태 코드 401(무단)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-161">If not, it returns HTTP status code 401 (Unauthorized), without invoking the action.</span></span>

<span data-ttu-id="c9d87-162">필터를 전역적으로, 컨트롤러 수준에서 또는 개별 작업 수준에서 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-162">You can apply the filter globally, at the controller level, or at the level of individual actions.</span></span>

<span data-ttu-id="c9d87-163">**전역 :** 모든 웹 API 컨트롤러에 대한 액세스를 제한하려면 **AuthorizeAttribute** 필터를 전역 필터 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-163">**Globally**: To restrict access for every Web API controller, add the **AuthorizeAttribute** filter to the global filter list:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="c9d87-164">**컨트롤러**: 특정 컨트롤러에 대한 액세스를 제한하려면 필터를 컨트롤러에 특성으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-164">**Controller**: To restrict access for a specific controller, add the filter as an attribute to the controller:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="c9d87-165">**작업**: 특정 작업에 대한 액세스를 제한하려면 작업 메서드에 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-165">**Action**: To restrict access for specific actions, add the attribute to the action method:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="c9d87-166">또는 특성을 사용하여 컨트롤러를 제한한 다음 특정 작업에 대한 `[AllowAnonymous]` 익명 액세스를 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-166">Alternatively, you can restrict the controller and then allow anonymous access to specific actions, by using the `[AllowAnonymous]` attribute.</span></span> <span data-ttu-id="c9d87-167">다음 예제에서는 메서드가 `Post` 제한되지만 메서드는 `Get` 익명 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-167">In the following example, the `Post` method is restricted, but the `Get` method allows anonymous access.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="c9d87-168">이전 예제에서는 필터를 사용하여 인증된 사용자가 제한된 메서드에 액세스할 수 있습니다. 익명 사용자만 유지됩니다. 특정 사용자 또는 특정 역할의 사용자에 대한 액세스를 제한할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-168">In the previous examples, the filter allows any authenticated user to access the restricted methods; only anonymous users are kept out. You can also limit access to specific users or to users in specific roles:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="c9d87-169">웹 API 컨트롤러에 대한 **권한 부여특성** 필터는 **System.Web.Http** 네임스페이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-169">The **AuthorizeAttribute** filter for Web API controllers is located in the **System.Web.Http** namespace.</span></span> <span data-ttu-id="c9d87-170">Web API 컨트롤러와 호환되지 않는 **System.Web.Mvc** 네임스페이스에는 MVC 컨트롤러에 대한 유사한 필터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-170">There is a similar filter for MVC controllers in the **System.Web.Mvc** namespace, which is not compatible with Web API controllers.</span></span>

### <a name="custom-authorization-filters"></a><span data-ttu-id="c9d87-171">사용자 지정 권한 부여 필터</span><span class="sxs-lookup"><span data-stu-id="c9d87-171">Custom Authorization Filters</span></span>

<span data-ttu-id="c9d87-172">사용자 지정 권한 부여 필터를 작성하려면 다음 형식 중 하나에서 파생합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-172">To write a custom authorization filter, derive from one of these types:</span></span>

- <span data-ttu-id="c9d87-173">**Attribute을 권한 부여합니다.**</span><span class="sxs-lookup"><span data-stu-id="c9d87-173">**AuthorizeAttribute**.</span></span> <span data-ttu-id="c9d87-174">현재 사용자 및 사용자의 역할에 따라 권한 부여 논리를 수행 하려면이 클래스를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-174">Extend this class to perform authorization logic based on the current user and the user's roles.</span></span>
- <span data-ttu-id="c9d87-175">**권한 부여필터특성**.</span><span class="sxs-lookup"><span data-stu-id="c9d87-175">**AuthorizationFilterAttribute**.</span></span> <span data-ttu-id="c9d87-176">이 클래스를 확장하여 현재 사용자 또는 역할에 반드시 기반하지 않는 동기 권한 부여 논리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-176">Extend this class to perform synchronous authorization logic that is not necessarily based on the current user or role.</span></span>
- <span data-ttu-id="c9d87-177">**I권한 부여 필터**.</span><span class="sxs-lookup"><span data-stu-id="c9d87-177">**IAuthorizationFilter**.</span></span> <span data-ttu-id="c9d87-178">비동기 권한 부여 논리를 수행 하려면이 인터페이스를 구현 합니다. 예를 들어 권한 부여 논리가 비동기 I/O 또는 네트워크 호출을 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-178">Implement this interface to perform asynchronous authorization logic; for example, if your authorization logic makes asynchronous I/O or network calls.</span></span> <span data-ttu-id="c9d87-179">권한 부여 논리가 CPU 바인딩된 경우 비동기 메서드를 작성할 필요가 없으므로 **AUTHORIZATIONFilterAttribute에서**파생하는 것이 더 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-179">(If your authorization logic is CPU-bound, it is simpler to derive from **AuthorizationFilterAttribute**, because then you don't need to write an asynchronous method.)</span></span>

<span data-ttu-id="c9d87-180">다음 다이어그램은 **AuthorizeAttribute** 클래스에 대한 클래스 계층 구조를 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-180">The following diagram shows the class hierarchy for the **AuthorizeAttribute** class.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a><span data-ttu-id="c9d87-181">컨트롤러 작업 내부 권한 부여</span><span class="sxs-lookup"><span data-stu-id="c9d87-181">Authorization Inside a Controller Action</span></span>

<span data-ttu-id="c9d87-182">경우에 따라 요청을 계속하도록 허용하지만 보안 주체에 따라 동작을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-182">In some cases, you might allow a request to proceed, but change the behavior based on the principal.</span></span> <span data-ttu-id="c9d87-183">예를 들어 반환하는 정보는 사용자의 역할에 따라 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-183">For example, the information that you return might change depending on the user's role.</span></span> <span data-ttu-id="c9d87-184">컨트롤러 메서드 내에서 **ApiController.User** 속성에서 현재 보안 주체를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d87-184">Within a controller method, you can get the current principal from the **ApiController.User** property.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
