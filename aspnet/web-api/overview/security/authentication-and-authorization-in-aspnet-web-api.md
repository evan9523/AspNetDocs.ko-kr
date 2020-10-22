---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: ASP.NET Web API의 인증 및 권한 부여 | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API의 인증 및 권한 부여에 대 한 일반적인 개요를 제공 합니다.
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345622"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a><span data-ttu-id="c6c9c-103">ASP.NET Web API의 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="c6c9c-103">Authentication and Authorization in ASP.NET Web API</span></span>

<span data-ttu-id="c6c9c-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c6c9c-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="c6c9c-105">Web API를 만들었지만 이제이에 대 한 액세스를 제어 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-105">You've created a web API, but now you want to control access to it.</span></span> <span data-ttu-id="c6c9c-106">이 문서 시리즈에서는 권한이 없는 사용자 로부터 web API를 보호 하기 위한 몇 가지 옵션을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-106">In this series of articles, we'll look at some options for securing a web API from unauthorized users.</span></span> <span data-ttu-id="c6c9c-107">이 시리즈는 인증 및 권한 부여를 모두 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-107">This series will cover both authentication and authorization.</span></span>

- <span data-ttu-id="c6c9c-108">*인증* 에서 사용자의 id를 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-108">*Authentication* is knowing the identity of the user.</span></span> <span data-ttu-id="c6c9c-109">예를 들어 Alice는 자신의 사용자 이름과 암호를 사용 하 여 로그인 하 고, 서버는 암호를 사용 하 여 Alice를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-109">For example, Alice logs in with her username and password, and the server uses the password to authenticate Alice.</span></span>
- <span data-ttu-id="c6c9c-110">*권한 부여* 는 사용자가 작업을 수행할 수 있는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-110">*Authorization* is deciding whether a user is allowed to perform an action.</span></span> <span data-ttu-id="c6c9c-111">예를 들어 Alice에 게는 리소스를 가져올 수 있는 권한이 있지만 리소스를 만들 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-111">For example, Alice has permission to get a resource but not create a resource.</span></span>

<span data-ttu-id="c6c9c-112">시리즈의 첫 번째 문서에서는 ASP.NET Web API의 인증 및 권한 부여에 대 한 일반적인 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-112">The first article in the series gives a general overview of authentication and authorization in ASP.NET Web API.</span></span> <span data-ttu-id="c6c9c-113">다른 항목에서는 Web API에 대 한 일반적인 인증 시나리오에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-113">Other topics describe common authentication scenarios for Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="c6c9c-114">이 시리즈를 검토 하 고 소중한 의견을 제공 해 주셔서 감사 합니다. Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-114">Thanks to the people who reviewed this series and provided valuable feedback: Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken.</span></span>

## <a name="authentication"></a><span data-ttu-id="c6c9c-115">인증</span><span class="sxs-lookup"><span data-stu-id="c6c9c-115">Authentication</span></span>

<span data-ttu-id="c6c9c-116">Web API는 호스트에서 인증이 발생 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-116">Web API assumes that authentication happens in the host.</span></span> <span data-ttu-id="c6c9c-117">웹 호스팅의 경우 호스트는 인증을 위해 HTTP 모듈을 사용 하는 IIS입니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-117">For web-hosting, the host is IIS, which uses HTTP modules for authentication.</span></span> <span data-ttu-id="c6c9c-118">IIS 또는 ASP.NET에 기본 제공 되는 인증 모듈을 사용 하도록 프로젝트를 구성 하거나 사용자 지정 인증을 수행 하는 사용자 고유의 HTTP 모듈을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-118">You can configure your project to use any of the authentication modules built in to IIS or ASP.NET, or write your own HTTP module to perform custom authentication.</span></span>

<span data-ttu-id="c6c9c-119">호스트는 사용자를 인증할 때 코드가 실행 되는 보안 컨텍스트를 나타내는 [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) 개체인 보안 *주체*를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-119">When the host authenticates the user, it creates a *principal*, which is an [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) object that represents the security context under which code is running.</span></span> <span data-ttu-id="c6c9c-120">호스트는 **system.threading.thread.currentprincipal**를 설정 하 여 현재 스레드에 보안 주체를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-120">The host attaches the principal to the current thread by setting **Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="c6c9c-121">보안 주체는 사용자에 대 한 정보를 포함 하는 연결 된 **id** 개체를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-121">The principal contains an associated **Identity** object that contains information about the user.</span></span> <span data-ttu-id="c6c9c-122">사용자가 인증 되 면 **Identity. isauthenticated** 속성은 **true**를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-122">If the user is authenticated, the **Identity.IsAuthenticated** property returns **true**.</span></span> <span data-ttu-id="c6c9c-123">익명 요청의 경우 **Isauthenticated** 는 **false**를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-123">For anonymous requests, **IsAuthenticated** returns **false**.</span></span> <span data-ttu-id="c6c9c-124">보안 주체에 대 한 자세한 내용은 [역할 기반 보안](https://msdn.microsoft.com/library/shz8h065.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-124">For more information about principals, see [Role-Based Security](https://msdn.microsoft.com/library/shz8h065.aspx).</span></span>

### <a name="http-message-handlers-for-authentication"></a><span data-ttu-id="c6c9c-125">인증에 대 한 HTTP 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="c6c9c-125">HTTP Message Handlers for Authentication</span></span>

<span data-ttu-id="c6c9c-126">인증을 위해 호스트를 사용 하는 대신 [HTTP 메시지 처리기](../advanced/http-message-handlers.md)에 인증 논리를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-126">Instead of using the host for authentication, you can put authentication logic into an [HTTP message handler](../advanced/http-message-handlers.md).</span></span> <span data-ttu-id="c6c9c-127">이 경우 메시지 처리기는 HTTP 요청을 검사 하 고 보안 주체를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-127">In that case, the message handler examines the HTTP request and sets the principal.</span></span>

<span data-ttu-id="c6c9c-128">인증에 메시지 처리기를 사용 해야 하는 경우는 언제 인가요?</span><span class="sxs-lookup"><span data-stu-id="c6c9c-128">When should you use message handlers for authentication?</span></span> <span data-ttu-id="c6c9c-129">몇 가지 장단점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-129">Here are some tradeoffs:</span></span>

- <span data-ttu-id="c6c9c-130">HTTP 모듈은 ASP.NET 파이프라인을 통해 이동 하는 모든 요청을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-130">An HTTP module sees all requests that go through the ASP.NET pipeline.</span></span> <span data-ttu-id="c6c9c-131">메시지 처리기는 Web API로 라우팅되는 요청만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-131">A message handler only sees requests that are routed to Web API.</span></span>
- <span data-ttu-id="c6c9c-132">특정 경로에 인증 체계를 적용할 수 있는 경로 단위 메시지 처리기를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-132">You can set per-route message handlers, which lets you apply an authentication scheme to a specific route.</span></span>
- <span data-ttu-id="c6c9c-133">HTTP 모듈은 IIS에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-133">HTTP modules are specific to IIS.</span></span> <span data-ttu-id="c6c9c-134">메시지 처리기는 호스트에 독립적 이므로 웹 호스팅 및 자체 호스팅 모두에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-134">Message handlers are host-agnostic, so they can be used with both web-hosting and self-hosting.</span></span>
- <span data-ttu-id="c6c9c-135">HTTP 모듈은 IIS 로깅, 감사 등에 참여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-135">HTTP modules participate in IIS logging, auditing, and so on.</span></span>
- <span data-ttu-id="c6c9c-136">HTTP 모듈은 파이프라인에서 이전에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-136">HTTP modules run earlier in the pipeline.</span></span> <span data-ttu-id="c6c9c-137">메시지 처리기에서 인증을 처리 하는 경우 처리기가 실행 될 때까지 보안 주체가 설정 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-137">If you handle authentication in a message handler, the principal does not get set until the handler runs.</span></span> <span data-ttu-id="c6c9c-138">또한 보안 주체는 응답이 메시지 처리기를 벗어날 때 이전 주체로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-138">Moreover, the principal reverts back to the previous principal when the response leaves the message handler.</span></span>

<span data-ttu-id="c6c9c-139">일반적으로 자체 호스팅을 지원 하지 않아도 되는 경우 HTTP 모듈이 더 나은 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-139">Generally, if you don't need to support self-hosting, an HTTP module is a better option.</span></span> <span data-ttu-id="c6c9c-140">자체 호스팅을 지원 해야 하는 경우에는 메시지 처리기를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-140">If you need to support self-hosting, consider a message handler.</span></span>

### <a name="setting-the-principal"></a><span data-ttu-id="c6c9c-141">보안 주체 설정</span><span class="sxs-lookup"><span data-stu-id="c6c9c-141">Setting the Principal</span></span>

<span data-ttu-id="c6c9c-142">응용 프로그램에서 사용자 지정 인증 논리를 수행 하는 경우 다음 두 위치에서 보안 주체를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-142">If your application performs any custom authentication logic, you must set the principal on two places:</span></span>

- <span data-ttu-id="c6c9c-143">**System.threading.thread.currentprincipal**.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-143">**Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="c6c9c-144">이 속성은 .NET에서 스레드의 보안 주체를 설정 하는 표준 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-144">This property is the standard way to set the thread's principal in .NET.</span></span>
- <span data-ttu-id="c6c9c-145">**HttpContext. 사용자**.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-145">**HttpContext.Current.User**.</span></span> <span data-ttu-id="c6c9c-146">이 속성은 ASP.NET에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-146">This property is specific to ASP.NET.</span></span>

<span data-ttu-id="c6c9c-147">다음 코드에서는 보안 주체를 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-147">The following code shows how to set the principal:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="c6c9c-148">웹 호스팅의 경우 두 위치 모두에서 보안 주체를 설정 해야 합니다. 그렇지 않으면 보안 컨텍스트가 일치 하지 않게 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-148">For web-hosting, you must set the principal in both places; otherwise the security context may become inconsistent.</span></span> <span data-ttu-id="c6c9c-149">그러나 자체 호스팅을 위해 **httpcontext.current** 는 null입니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-149">For self-hosting, however, **HttpContext.Current** is null.</span></span> <span data-ttu-id="c6c9c-150">따라서 코드에 호스트를 독립적으로 사용할 수 있도록 하려면 표시 된 대로 **httpcontext.current**에를 할당 하기 전에 null 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-150">To ensure your code is host-agnostic, therefore, check for null before assigning to **HttpContext.Current**, as shown.</span></span>

## <a name="authorization"></a><span data-ttu-id="c6c9c-151">권한 부여</span><span class="sxs-lookup"><span data-stu-id="c6c9c-151">Authorization</span></span>

<span data-ttu-id="c6c9c-152">권한 부여는 컨트롤러에 더 가깝게 파이프라인에서 나중에 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-152">Authorization happens later in the pipeline, closer to the controller.</span></span> <span data-ttu-id="c6c9c-153">이를 통해 리소스에 대 한 액세스 권한을 부여할 때 더 세부적인 선택을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-153">That lets you make more granular choices when you grant access to resources.</span></span>

- <span data-ttu-id="c6c9c-154">*권한 부여 필터* 는 컨트롤러 작업 이전에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-154">*Authorization filters* run before the controller action.</span></span> <span data-ttu-id="c6c9c-155">요청이 인증 되지 않은 경우 필터는 오류 응답을 반환 하 고 동작은 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-155">If the request is not authorized, the filter returns an error response, and the action is not invoked.</span></span>
- <span data-ttu-id="c6c9c-156">컨트롤러 작업 내에서 **ApiController** 속성을 사용 하 여 현재 보안 주체를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-156">Within a controller action, you can get the current principal from the **ApiController.User** property.</span></span> <span data-ttu-id="c6c9c-157">예를 들어 사용자 이름에 따라 리소스 목록을 필터링 하 여 해당 사용자에 게 속하는 리소스만 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-157">For example, you might filter a list of resources based on the user name, returning only those resources that belong to that user.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a><span data-ttu-id="c6c9c-158">[권한 부여] 특성 사용</span><span class="sxs-lookup"><span data-stu-id="c6c9c-158">Using the [Authorize] Attribute</span></span>

<span data-ttu-id="c6c9c-159">Web API는 기본 제공 권한 부여 필터 인 [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-159">Web API provides a built-in authorization filter, [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx).</span></span> <span data-ttu-id="c6c9c-160">이 필터는 사용자가 인증 되었는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-160">This filter checks whether the user is authenticated.</span></span> <span data-ttu-id="c6c9c-161">그렇지 않으면 동작을 호출 하지 않고 HTTP 상태 코드 401 (권한 없음)을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-161">If not, it returns HTTP status code 401 (Unauthorized), without invoking the action.</span></span>

<span data-ttu-id="c6c9c-162">전역, 컨트롤러 수준 또는 개별 작업 수준에서 필터를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-162">You can apply the filter globally, at the controller level, or at the level of individual actions.</span></span>

<span data-ttu-id="c6c9c-163">**전역적**으로: 모든 Web API 컨트롤러에 대 한 액세스를 제한 하려면 전역 필터 목록에 **AuthorizeAttribute** 필터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-163">**Globally**: To restrict access for every Web API controller, add the **AuthorizeAttribute** filter to the global filter list:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="c6c9c-164">**컨트롤러**: 특정 컨트롤러에 대 한 액세스를 제한 하려면 해당 필터를 컨트롤러에 특성으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-164">**Controller**: To restrict access for a specific controller, add the filter as an attribute to the controller:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="c6c9c-165">**작업**: 특정 작업에 대 한 액세스를 제한 하려면 작업 메서드에 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-165">**Action**: To restrict access for specific actions, add the attribute to the action method:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="c6c9c-166">또는 컨트롤러를 제한 한 다음 특성을 사용 하 여 특정 작업에 대 한 익명 액세스를 허용할 수 있습니다 `[AllowAnonymous]` .</span><span class="sxs-lookup"><span data-stu-id="c6c9c-166">Alternatively, you can restrict the controller and then allow anonymous access to specific actions, by using the `[AllowAnonymous]` attribute.</span></span> <span data-ttu-id="c6c9c-167">다음 예제에서 `Post` 메서드는 제한 되지만 `Get` 메서드는 익명 액세스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-167">In the following example, the `Post` method is restricted, but the `Get` method allows anonymous access.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="c6c9c-168">이전 예제에서 필터는 인증 된 사용자가 제한 된 메서드에 액세스할 수 있도록 허용 합니다. 익명 사용자만 유지 됩니다. 특정 사용자 또는 특정 역할의 사용자에 대 한 액세스를 제한할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-168">In the previous examples, the filter allows any authenticated user to access the restricted methods; only anonymous users are kept out. You can also limit access to specific users or to users in specific roles:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="c6c9c-169">Web API 컨트롤러에 대 한 **AuthorizeAttribute** 필터는 **system.web. Http** 네임 스페이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-169">The **AuthorizeAttribute** filter for Web API controllers is located in the **System.Web.Http** namespace.</span></span> <span data-ttu-id="c6c9c-170">Web API 컨트롤러와 호환 되지 않는 **system.web 네임 스페이스** 의 mvc 컨트롤러에 대 한 유사한 필터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-170">There is a similar filter for MVC controllers in the **System.Web.Mvc** namespace, which is not compatible with Web API controllers.</span></span>

### <a name="custom-authorization-filters"></a><span data-ttu-id="c6c9c-171">사용자 지정 권한 부여 필터</span><span class="sxs-lookup"><span data-stu-id="c6c9c-171">Custom Authorization Filters</span></span>

<span data-ttu-id="c6c9c-172">사용자 지정 권한 부여 필터를 작성 하려면 다음 형식 중 하나에서 파생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-172">To write a custom authorization filter, derive from one of these types:</span></span>

- <span data-ttu-id="c6c9c-173">**AuthorizeAttribute**.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-173">**AuthorizeAttribute**.</span></span> <span data-ttu-id="c6c9c-174">현재 사용자 및 사용자의 역할에 따라 권한 부여 논리를 수행 하려면이 클래스를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-174">Extend this class to perform authorization logic based on the current user and the user's roles.</span></span>
- <span data-ttu-id="c6c9c-175">**Authorizationfilterattribute**입니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-175">**AuthorizationFilterAttribute**.</span></span> <span data-ttu-id="c6c9c-176">이 클래스를 확장 하 여 현재 사용자 또는 역할을 기반으로 하지 않아도 되는 동기 권한 부여 논리를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-176">Extend this class to perform synchronous authorization logic that is not necessarily based on the current user or role.</span></span>
- <span data-ttu-id="c6c9c-177">**IAuthorizationFilter**.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-177">**IAuthorizationFilter**.</span></span> <span data-ttu-id="c6c9c-178">비동기 권한 부여 논리를 수행 하려면이 인터페이스를 구현 합니다. 예를 들어 권한 부여 논리가 비동기 i/o 또는 네트워크 호출을 수행 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-178">Implement this interface to perform asynchronous authorization logic; for example, if your authorization logic makes asynchronous I/O or network calls.</span></span> <span data-ttu-id="c6c9c-179">권한 부여 논리가 CPU 바인딩된 경우에는 비동기 메서드를 작성할 필요가 없기 때문에 **Authorizationfilterattribute**에서 파생 하는 것이 더 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-179">(If your authorization logic is CPU-bound, it is simpler to derive from **AuthorizationFilterAttribute**, because then you don't need to write an asynchronous method.)</span></span>

<span data-ttu-id="c6c9c-180">다음 다이어그램에서는 **AuthorizeAttribute** 클래스에 대 한 클래스 계층 구조를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-180">The following diagram shows the class hierarchy for the **AuthorizeAttribute** class.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a><span data-ttu-id="c6c9c-181">컨트롤러 작업 내부 권한 부여</span><span class="sxs-lookup"><span data-stu-id="c6c9c-181">Authorization Inside a Controller Action</span></span>

<span data-ttu-id="c6c9c-182">경우에 따라 요청을 계속 진행 하지만 보안 주체에 따라 동작을 변경 하도록 허용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-182">In some cases, you might allow a request to proceed, but change the behavior based on the principal.</span></span> <span data-ttu-id="c6c9c-183">예를 들어 반환 하는 정보는 사용자의 역할에 따라 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-183">For example, the information that you return might change depending on the user's role.</span></span> <span data-ttu-id="c6c9c-184">컨트롤러 메서드 내에서 **ApiController** 속성을 사용 하 여 현재 보안 주체를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c9c-184">Within a controller method, you can get the current principal from the **ApiController.User** property.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
