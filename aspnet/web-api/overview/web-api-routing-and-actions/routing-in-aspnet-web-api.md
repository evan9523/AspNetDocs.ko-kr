---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET Web API에서 라우팅 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345197"
---
# <a name="routing-in-aspnet-web-api"></a><span data-ttu-id="68de1-102">ASP.NET Web API의 라우팅</span><span class="sxs-lookup"><span data-stu-id="68de1-102">Routing in ASP.NET Web API</span></span>

<span data-ttu-id="68de1-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="68de1-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="68de1-104">이 문서에서는 ASP.NET Web API는 컨트롤러에 HTTP 요청을 라우팅하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-104">This article describes how ASP.NET Web API routes HTTP requests to controllers.</span></span>

> [!NOTE]
> <span data-ttu-id="68de1-105">ASP.NET MVC에 익숙한 경우 Web API 라우팅은 MVC 라우팅과 매우 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-105">If you are familiar with ASP.NET MVC, Web API routing is very similar to MVC routing.</span></span> <span data-ttu-id="68de1-106">주요 차이점은 Web API는 URI 경로가 아니라 HTTP 동사를 사용 하 여 작업을 선택 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-106">The main difference is that Web API uses the HTTP verb, not the URI path, to select the action.</span></span> <span data-ttu-id="68de1-107">Web API에서 MVC 스타일 라우팅을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-107">You can also use MVC-style routing in Web API.</span></span> <span data-ttu-id="68de1-108">이 문서에서는 ASP.NET MVC에 대 한 지식이 있다고 가정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-108">This article does not assume any knowledge of ASP.NET MVC.</span></span>

## <a name="routing-tables"></a><span data-ttu-id="68de1-109">라우팅 테이블</span><span class="sxs-lookup"><span data-stu-id="68de1-109">Routing Tables</span></span>

<span data-ttu-id="68de1-110">ASP.NET Web API에서 *컨트롤러* 는 HTTP 요청을 처리 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-110">In ASP.NET Web API, a *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="68de1-111">컨트롤러의 공용 메서드를 *작업 메서드* 또는 간단히 *동작*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-111">The public methods of the controller are called *action methods* or simply *actions*.</span></span> <span data-ttu-id="68de1-112">웹 API 프레임 워크에서 요청을 받으면 요청을 작업으로 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-112">When the Web API framework receives a request, it routes the request to an action.</span></span>

<span data-ttu-id="68de1-113">호출할 동작을 결정 하기 위해 프레임 워크는 *라우팅 테이블*을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-113">To determine which action to invoke, the framework uses a *routing table*.</span></span> <span data-ttu-id="68de1-114">Web API 용 Visual Studio 프로젝트 템플릿은 기본 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-114">The Visual Studio project template for Web API creates a default route:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="68de1-115">이 경로는 *WebApiConfig.cs* 파일에 정의 되며, *앱 \_ 시작* 디렉터리에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-115">This route is defined in the *WebApiConfig.cs* file, which is placed in the *App\_Start* directory:</span></span>

![](routing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="68de1-116">클래스에 대 한 자세한 내용은 `WebApiConfig` [ASP.NET Web API 구성](../advanced/configuring-aspnet-web-api.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="68de1-116">For more information about the `WebApiConfig` class, see [Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span></span>

<span data-ttu-id="68de1-117">Web API를 자체 호스트 하는 경우에는 개체에 직접 라우팅 테이블을 설정 해야 합니다 `HttpSelfHostConfiguration` .</span><span class="sxs-lookup"><span data-stu-id="68de1-117">If you self-host Web API, you must set the routing table directly on the `HttpSelfHostConfiguration` object.</span></span> <span data-ttu-id="68de1-118">자세한 내용은 [웹 API 자체 호스팅](../older-versions/self-host-a-web-api.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="68de1-118">For more information, see [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span></span>

<span data-ttu-id="68de1-119">라우팅 테이블의 각 항목에는 *경로 템플릿이*포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-119">Each entry in the routing table contains a *route template*.</span></span> <span data-ttu-id="68de1-120">Web API에 대 한 기본 경로 템플릿은 &quot; API/{controller}/{id}입니다 &quot; .</span><span class="sxs-lookup"><span data-stu-id="68de1-120">The default route template for Web API is &quot;api/{controller}/{id}&quot;.</span></span> <span data-ttu-id="68de1-121">이 템플릿에서 &quot; api &quot; 는 리터럴 경로 세그먼트이 고 {controller} 및 {id}는 자리 표시자 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-121">In this template, &quot;api&quot; is a literal path segment, and {controller} and {id} are placeholder variables.</span></span>

<span data-ttu-id="68de1-122">웹 API 프레임 워크는 HTTP 요청을 받으면 라우팅 테이블의 경로 템플릿 중 하나에 대해 URI를 일치 시 키 려 고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-122">When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table.</span></span> <span data-ttu-id="68de1-123">경로가 일치 하지 않으면 클라이언트에서 404 오류를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-123">If no route matches, the client receives a 404 error.</span></span> <span data-ttu-id="68de1-124">예를 들어 다음 Uri는 기본 경로와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-124">For example, the following URIs match the default route:</span></span>

- <span data-ttu-id="68de1-125">/api/연락처</span><span class="sxs-lookup"><span data-stu-id="68de1-125">/api/contacts</span></span>
- <span data-ttu-id="68de1-126">/api/contacts/1</span><span class="sxs-lookup"><span data-stu-id="68de1-126">/api/contacts/1</span></span>
- <span data-ttu-id="68de1-127">/api/products/gizmo1</span><span class="sxs-lookup"><span data-stu-id="68de1-127">/api/products/gizmo1</span></span>

<span data-ttu-id="68de1-128">그러나 다음 URI는 api 세그먼트가 없으므로 일치 하지 않습니다 &quot; &quot; .</span><span class="sxs-lookup"><span data-stu-id="68de1-128">However, the following URI does not match, because it lacks the &quot;api&quot; segment:</span></span>

- <span data-ttu-id="68de1-129">/contacts/1</span><span class="sxs-lookup"><span data-stu-id="68de1-129">/contacts/1</span></span>

> [!NOTE]
> <span data-ttu-id="68de1-130">경로에서 "api"를 사용 하는 이유는 ASP.NET MVC 라우팅과의 충돌을 방지 하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-130">The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing.</span></span> <span data-ttu-id="68de1-131">이러한 방식으로 &quot; /연락처를 &quot; MVC 컨트롤러로 이동 하 고///또는 &quot; 연락처를 &quot; 웹 api 컨트롤러로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-131">That way, you can have &quot;/contacts&quot; go to an MVC controller, and &quot;/api/contacts&quot; go to a Web API controller.</span></span> <span data-ttu-id="68de1-132">물론이 규칙을 원하지 않는 경우 기본 경로 테이블을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-132">Of course, if you don't like this convention, you can change the default route table.</span></span>

<span data-ttu-id="68de1-133">일치 하는 경로가 발견 되 면 Web API는 컨트롤러 및 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-133">Once a matching route is found, Web API selects the controller and the action:</span></span>

- <span data-ttu-id="68de1-134">웹 API는 컨트롤러를 찾기 위해 &quot; &quot; *{controller}* 변수 값에 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-134">To find the controller, Web API adds &quot;Controller&quot; to the value of the *{controller}* variable.</span></span>
- <span data-ttu-id="68de1-135">동작을 찾기 위해 Web API는 HTTP 동사를 찾은 다음 이름이 해당 HTTP 동사 이름으로 시작 하는 작업을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-135">To find the action, Web API looks at the HTTP verb, and then looks for an action whose name begins with that HTTP verb name.</span></span> <span data-ttu-id="68de1-136">예를 들어 GET 요청을 사용 하는 경우 Web API는 &quot; &quot; &quot; getcontact &quot; 또는 &quot; getallcontacts와 같이 get이 &quot; 접두사로 추가 된 작업을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-136">For example, with a GET request, Web API looks for an action prefixed with &quot;Get&quot;, such as &quot;GetContact&quot; or &quot;GetAllContacts&quot;.</span></span> <span data-ttu-id="68de1-137">이 규칙은 GET, POST, PUT, DELETE, HEAD, OPTIONS 및 PATCH 동사에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-137">This convention applies only to GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH verbs.</span></span> <span data-ttu-id="68de1-138">컨트롤러에서 특성을 사용 하 여 다른 HTTP 동사를 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-138">You can enable other HTTP verbs by using attributes on your controller.</span></span> <span data-ttu-id="68de1-139">이에 대 한 예제는 나중에 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-139">We'll see an example of that later.</span></span>
- <span data-ttu-id="68de1-140">경로 템플릿의 다른 자리 표시자 변수 (예: *{id}* )는 동작 매개 변수에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-140">Other placeholder variables in the route template, such as *{id},* are mapped to action parameters.</span></span>

<span data-ttu-id="68de1-141">예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-141">Let's look at an example.</span></span> <span data-ttu-id="68de1-142">다음 컨트롤러를 정의 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-142">Suppose that you define the following controller:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="68de1-143">다음은 각각에 대해 호출 되는 작업과 함께 가능한 몇 가지 HTTP 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-143">Here are some possible HTTP requests, along with the action that gets invoked for each:</span></span>

| <span data-ttu-id="68de1-144">HTTP 동사</span><span class="sxs-lookup"><span data-stu-id="68de1-144">HTTP Verb</span></span> | <span data-ttu-id="68de1-145">URI 경로</span><span class="sxs-lookup"><span data-stu-id="68de1-145">URI Path</span></span> | <span data-ttu-id="68de1-146">작업</span><span class="sxs-lookup"><span data-stu-id="68de1-146">Action</span></span> | <span data-ttu-id="68de1-147">매개 변수</span><span class="sxs-lookup"><span data-stu-id="68de1-147">Parameter</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="68de1-148">GET</span><span class="sxs-lookup"><span data-stu-id="68de1-148">GET</span></span> | <span data-ttu-id="68de1-149">a p i/제품</span><span class="sxs-lookup"><span data-stu-id="68de1-149">api/products</span></span> | <span data-ttu-id="68de1-150">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="68de1-150">GetAllProducts</span></span> | <span data-ttu-id="68de1-151">*없음을*</span><span class="sxs-lookup"><span data-stu-id="68de1-151">*(none)*</span></span> |
| <span data-ttu-id="68de1-152">GET</span><span class="sxs-lookup"><span data-stu-id="68de1-152">GET</span></span> | <span data-ttu-id="68de1-153">a p i/제품/4</span><span class="sxs-lookup"><span data-stu-id="68de1-153">api/products/4</span></span> | <span data-ttu-id="68de1-154">GetProductById</span><span class="sxs-lookup"><span data-stu-id="68de1-154">GetProductById</span></span> | <span data-ttu-id="68de1-155">4</span><span class="sxs-lookup"><span data-stu-id="68de1-155">4</span></span> |
| <span data-ttu-id="68de1-156">Delete</span><span class="sxs-lookup"><span data-stu-id="68de1-156">DELETE</span></span> | <span data-ttu-id="68de1-157">a p i/제품/4</span><span class="sxs-lookup"><span data-stu-id="68de1-157">api/products/4</span></span> | <span data-ttu-id="68de1-158">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="68de1-158">DeleteProduct</span></span> | <span data-ttu-id="68de1-159">4</span><span class="sxs-lookup"><span data-stu-id="68de1-159">4</span></span> |
| <span data-ttu-id="68de1-160">POST</span><span class="sxs-lookup"><span data-stu-id="68de1-160">POST</span></span> | <span data-ttu-id="68de1-161">a p i/제품</span><span class="sxs-lookup"><span data-stu-id="68de1-161">api/products</span></span> | <span data-ttu-id="68de1-162">*(일치 항목 없음)*</span><span class="sxs-lookup"><span data-stu-id="68de1-162">*(no match)*</span></span> |  |

<span data-ttu-id="68de1-163">URI의 *{id}* 세그먼트 (있는 경우)가 동작의 *id* 매개 변수에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-163">Notice that the *{id}* segment of the URI, if present, is mapped to the *id* parameter of the action.</span></span> <span data-ttu-id="68de1-164">이 예제에서 컨트롤러는 두 개의 GET 메서드를 정의 합니다. 하나는 *id* 매개 변수를 사용 하 고 다른 하나는 매개 변수를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-164">In this example, the controller defines two GET methods, one with an *id* parameter and one with no parameters.</span></span>

<span data-ttu-id="68de1-165">또한 컨트롤러에서 &quot; post ... 메서드를 정의 하지 않으므로 post 요청은 실패 합니다. &quot;</span><span class="sxs-lookup"><span data-stu-id="68de1-165">Also, note that the POST request will fail, because the controller does not define a &quot;Post...&quot; method.</span></span>

## <a name="routing-variations"></a><span data-ttu-id="68de1-166">라우팅 변형</span><span class="sxs-lookup"><span data-stu-id="68de1-166">Routing Variations</span></span>

<span data-ttu-id="68de1-167">이전 섹션에서는 ASP.NET Web API에 대 한 기본 라우팅 메커니즘에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-167">The previous section described the basic routing mechanism for ASP.NET Web API.</span></span> <span data-ttu-id="68de1-168">이 섹션에서는 몇 가지 변형에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-168">This section describes some variations.</span></span>

### <a name="http-verbs"></a><span data-ttu-id="68de1-169">HTTP 동사</span><span class="sxs-lookup"><span data-stu-id="68de1-169">HTTP verbs</span></span>

<span data-ttu-id="68de1-170">HTTP 동사에 대 한 명명 규칙을 사용 하는 대신 작업 메서드를 다음 특성 중 하나로 데코레이팅 하 여 동작에 대 한 HTTP 동사를 명시적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-170">Instead of using the naming convention for HTTP verbs, you can explicitly specify the HTTP verb for an action by decorating the action method with one of the following attributes:</span></span>

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

<span data-ttu-id="68de1-171">다음 예제에서 `FindProduct` 메서드는 GET 요청에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-171">In the following example, the `FindProduct` method is mapped to GET requests:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="68de1-172">작업에 대해 여러 HTTP 동사를 허용 하거나 GET, PUT, POST, DELETE, HEAD, OPTIONS 및 PATCH 이외의 HTTP 동사를 허용 하려면 `[AcceptVerbs]` http 동사 목록을 사용 하는 특성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-172">To allow multiple HTTP verbs for an action, or to allow HTTP verbs other than GET, PUT, POST, DELETE, HEAD, OPTIONS, and PATCH, use the `[AcceptVerbs]` attribute, which takes a list of HTTP verbs.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a><span data-ttu-id="68de1-173">작업 이름별 라우팅</span><span class="sxs-lookup"><span data-stu-id="68de1-173">Routing by Action Name</span></span>

<span data-ttu-id="68de1-174">기본 라우팅 템플릿을 사용 하는 경우 Web API는 HTTP 동사를 사용 하 여 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-174">With the default routing template, Web API uses the HTTP verb to select the action.</span></span> <span data-ttu-id="68de1-175">그러나 URI에 작업 이름이 포함 된 경로를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-175">However, you can also create a route where the action name is included in the URI:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="68de1-176">이 경로 템플릿에서 *{action}* 매개 변수는 컨트롤러의 동작 메서드 이름을로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-176">In this route template, the *{action}* parameter names the action method on the controller.</span></span> <span data-ttu-id="68de1-177">이 스타일의 라우팅을 사용 하 여 특성을 사용 하 여 허용 되는 HTTP 동사를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-177">With this style of routing, use attributes to specify the allowed HTTP verbs.</span></span> <span data-ttu-id="68de1-178">예를 들어 컨트롤러에 다음 메서드가 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-178">For example, suppose your controller has the following method:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="68de1-179">이 경우 "api/products/details/1"에 대 한 GET 요청은 `Details` 메서드에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-179">In this case, a GET request for "api/products/details/1" would map to the `Details` method.</span></span> <span data-ttu-id="68de1-180">이 라우팅 스타일은 ASP.NET MVC와 비슷하며 RPC 스타일 API에 적합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-180">This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API.</span></span>

<span data-ttu-id="68de1-181">특성을 사용 하 여 작업 이름을 재정의할 수 있습니다 `[ActionName]` .</span><span class="sxs-lookup"><span data-stu-id="68de1-181">You can override the action name by using the `[ActionName]` attribute.</span></span> <span data-ttu-id="68de1-182">다음 예제에서는 a p i/ &quot; 제품/축소판 그림/*id*에 매핑되는 두 가지 작업을 수행 합니다. 하나는 GET을 지원 하 고 다른 하나는 POST를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-182">In the following example, there are two actions that map to &quot;api/products/thumbnail/*id*. One supports GET and the other supports POST:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a><span data-ttu-id="68de1-183">비 작업</span><span class="sxs-lookup"><span data-stu-id="68de1-183">Non-Actions</span></span>

<span data-ttu-id="68de1-184">메서드가 동작으로 호출 되는 것을 방지 하려면 특성을 사용 `[NonAction]` 합니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-184">To prevent a method from getting invoked as an action, use the `[NonAction]` attribute.</span></span> <span data-ttu-id="68de1-185">이는 다른 방법으로 라우팅 규칙과 일치 하는 경우에도 메서드가 동작이 아니라는 프레임 워크에 신호를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-185">This signals to the framework that the method is not an action, even if it would otherwise match the routing rules.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a><span data-ttu-id="68de1-186">추가 정보</span><span class="sxs-lookup"><span data-stu-id="68de1-186">Further Reading</span></span>

<span data-ttu-id="68de1-187">이 항목에서는 라우팅에 대 한 개략적인 보기를 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="68de1-187">This topic provided a high-level view of routing.</span></span> <span data-ttu-id="68de1-188">자세한 내용은 [라우팅 및 작업 선택](routing-and-action-selection.md), 프레임 워크가 경로에 대 한 URI를 정확히 일치 하는 방식에 대해 설명 하 고, 컨트롤러를 선택한 다음 호출할 작업을 선택 하는 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="68de1-188">For more detail, see [Routing and Action Selection](routing-and-action-selection.md), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.</span></span>
