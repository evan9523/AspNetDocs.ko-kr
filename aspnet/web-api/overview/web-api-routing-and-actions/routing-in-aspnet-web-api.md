---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET 웹 API의 라우팅 | 마이크로 소프트 문서
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675756"
---
# <a name="routing-in-aspnet-web-api"></a><span data-ttu-id="5f6ef-102">ASP.NET Web API의 라우팅</span><span class="sxs-lookup"><span data-stu-id="5f6ef-102">Routing in ASP.NET Web API</span></span>

<span data-ttu-id="5f6ef-103">로 [마이크 와슨](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5f6ef-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="5f6ef-104">이 문서에서는 ASP.NET 웹 API가 HTTP 요청을 컨트롤러에 라우팅하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-104">This article describes how ASP.NET Web API routes HTTP requests to controllers.</span></span>

> [!NOTE]
> <span data-ttu-id="5f6ef-105">ASP.NET MVC에 익숙한 경우 웹 API 라우팅은 MVC 라우팅과 매우 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-105">If you are familiar with ASP.NET MVC, Web API routing is very similar to MVC routing.</span></span> <span data-ttu-id="5f6ef-106">주요 차이점은 Web API가 URI 경로가 아닌 HTTP 동사를 사용하여 작업을 선택한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-106">The main difference is that Web API uses the HTTP verb, not the URI path, to select the action.</span></span> <span data-ttu-id="5f6ef-107">웹 API에서 MVC 스타일 라우팅을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-107">You can also use MVC-style routing in Web API.</span></span> <span data-ttu-id="5f6ef-108">이 문서에서는 ASP.NET MVC에 대한 어떠한 지식도 가정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-108">This article does not assume any knowledge of ASP.NET MVC.</span></span>

## <a name="routing-tables"></a><span data-ttu-id="5f6ef-109">라우팅 테이블</span><span class="sxs-lookup"><span data-stu-id="5f6ef-109">Routing Tables</span></span>

<span data-ttu-id="5f6ef-110">ASP.NET 웹 API에서 *컨트롤러는* HTTP 요청을 처리하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-110">In ASP.NET Web API, a *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="5f6ef-111">컨트롤러의 공용 메서드를 *작업 메서드* 또는 단순히 *작업이라고*합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-111">The public methods of the controller are called *action methods* or simply *actions*.</span></span> <span data-ttu-id="5f6ef-112">웹 API 프레임워크가 요청을 받으면 요청을 작업에 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-112">When the Web API framework receives a request, it routes the request to an action.</span></span>

<span data-ttu-id="5f6ef-113">호출할 작업을 결정하기 위해 프레임워크는 *라우팅 테이블을*사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-113">To determine which action to invoke, the framework uses a *routing table*.</span></span> <span data-ttu-id="5f6ef-114">웹 API에 대한 Visual Studio 프로젝트 템플릿은 기본 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-114">The Visual Studio project template for Web API creates a default route:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="5f6ef-115">이 경로는 *\_앱 시작* 디렉터리에 배치되는 *WebApiConfig.cs* 파일에 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-115">This route is defined in the *WebApiConfig.cs* file, which is placed in the *App\_Start* directory:</span></span>

![](routing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="5f6ef-116">클래스에 `WebApiConfig` 대한 자세한 내용은 [웹 API 구성ASP.NET.](../advanced/configuring-aspnet-web-api.md)</span><span class="sxs-lookup"><span data-stu-id="5f6ef-116">For more information about the `WebApiConfig` class, see [Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span></span>

<span data-ttu-id="5f6ef-117">웹 API를 자체 호스트하는 경우 `HttpSelfHostConfiguration` 개체에 직접 라우팅 테이블을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-117">If you self-host Web API, you must set the routing table directly on the `HttpSelfHostConfiguration` object.</span></span> <span data-ttu-id="5f6ef-118">자세한 내용은 [웹 API 자체 호스트를](../older-versions/self-host-a-web-api.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-118">For more information, see [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span></span>

<span data-ttu-id="5f6ef-119">라우팅 테이블의 각 항목에는 *경로 템플릿이*포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-119">Each entry in the routing table contains a *route template*.</span></span> <span data-ttu-id="5f6ef-120">웹 API의 기본 경로 &quot;템플릿은 api/{컨트롤러}/{id}&quot;입니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-120">The default route template for Web API is &quot;api/{controller}/{id}&quot;.</span></span> <span data-ttu-id="5f6ef-121">이 템플릿에서 &quot;&quot; api는 리터럴 경로 세그먼트이고 {controller} 및 {id}는 자리 표시자 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-121">In this template, &quot;api&quot; is a literal path segment, and {controller} and {id} are placeholder variables.</span></span>

<span data-ttu-id="5f6ef-122">웹 API 프레임워크가 HTTP 요청을 받으면 라우팅 테이블의 경로 템플릿 중 하나에 대해 URI를 일치시키려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-122">When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table.</span></span> <span data-ttu-id="5f6ef-123">경로가 일치하지 않으면 클라이언트에 404 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-123">If no route matches, the client receives a 404 error.</span></span> <span data-ttu-id="5f6ef-124">예를 들어 다음 URI는 기본 경로와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-124">For example, the following URIs match the default route:</span></span>

- <span data-ttu-id="5f6ef-125">/api/연락처</span><span class="sxs-lookup"><span data-stu-id="5f6ef-125">/api/contacts</span></span>
- <span data-ttu-id="5f6ef-126">/api/연락처/1</span><span class="sxs-lookup"><span data-stu-id="5f6ef-126">/api/contacts/1</span></span>
- <span data-ttu-id="5f6ef-127">/api/제품/기즈모1</span><span class="sxs-lookup"><span data-stu-id="5f6ef-127">/api/products/gizmo1</span></span>

<span data-ttu-id="5f6ef-128">그러나 api &quot;&quot; 세그먼트가 없기 때문에 다음 URI가 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-128">However, the following URI does not match, because it lacks the &quot;api&quot; segment:</span></span>

- <span data-ttu-id="5f6ef-129">/연락처/1</span><span class="sxs-lookup"><span data-stu-id="5f6ef-129">/contacts/1</span></span>

> [!NOTE]
> <span data-ttu-id="5f6ef-130">경로에서 "api"를 사용하는 이유는 ASP.NET MVC 라우팅과의 충돌을 피하기 위해서입니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-130">The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing.</span></span> <span data-ttu-id="5f6ef-131">이렇게 하면 &quot;/연락처가&quot; MVC 컨트롤러로 이동하고 &quot;/api/연락처가&quot; 웹 API 컨트롤러로 이동하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-131">That way, you can have &quot;/contacts&quot; go to an MVC controller, and &quot;/api/contacts&quot; go to a Web API controller.</span></span> <span data-ttu-id="5f6ef-132">물론 이 규칙이 마음에 들지 않으면 기본 경로 테이블을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-132">Of course, if you don't like this convention, you can change the default route table.</span></span>

<span data-ttu-id="5f6ef-133">일치하는 경로가 발견되면 Web API는 컨트롤러와 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-133">Once a matching route is found, Web API selects the controller and the action:</span></span>

- <span data-ttu-id="5f6ef-134">컨트롤러를 찾기 위해 Web &quot;&quot; API는 *{controller}* 변수값에 컨트롤러를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-134">To find the controller, Web API adds &quot;Controller&quot; to the value of the *{controller}* variable.</span></span>
- <span data-ttu-id="5f6ef-135">작업을 찾기 위해 Web API는 HTTP 동사를 찾은 다음 해당 HTTP 동사 이름으로 이름이 시작되는 작업을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-135">To find the action, Web API looks at the HTTP verb, and then looks for an action whose name begins with that HTTP verb name.</span></span> <span data-ttu-id="5f6ef-136">예를 들어 GET 요청을 사용하면 &quot;웹 API는 GetContact&quot; &quot;&quot; 또는 GetAllContacts &quot;와 같이&quot;GetContact 로 접두번에 붙어 있는 작업을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-136">For example, with a GET request, Web API looks for an action prefixed with &quot;Get&quot;, such as &quot;GetContact&quot; or &quot;GetAllContacts&quot;.</span></span> <span data-ttu-id="5f6ef-137">이 규칙은 GET, POST, PUT, DELETE, HEAD, 옵션 및 패치 동사에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-137">This convention applies only to GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH verbs.</span></span> <span data-ttu-id="5f6ef-138">컨트롤러의 특성을 사용하여 다른 HTTP 동사를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-138">You can enable other HTTP verbs by using attributes on your controller.</span></span> <span data-ttu-id="5f6ef-139">나중에 그 예가 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-139">We'll see an example of that later.</span></span>
- <span data-ttu-id="5f6ef-140">*{id}와* 같은 경로 템플릿의 다른 자리 표시자 변수는 작업 매개 변수에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-140">Other placeholder variables in the route template, such as *{id},* are mapped to action parameters.</span></span>

<span data-ttu-id="5f6ef-141">예제를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-141">Let's look at an example.</span></span> <span data-ttu-id="5f6ef-142">다음 컨트롤러를 정의한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-142">Suppose that you define the following controller:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="5f6ef-143">다음은 각 HTTP에 대해 호출되는 작업과 함께 가능한 HTTP 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-143">Here are some possible HTTP requests, along with the action that gets invoked for each:</span></span>

| <span data-ttu-id="5f6ef-144">HTTP 동사</span><span class="sxs-lookup"><span data-stu-id="5f6ef-144">HTTP Verb</span></span> | <span data-ttu-id="5f6ef-145">URI 경로</span><span class="sxs-lookup"><span data-stu-id="5f6ef-145">URI Path</span></span> | <span data-ttu-id="5f6ef-146">작업</span><span class="sxs-lookup"><span data-stu-id="5f6ef-146">Action</span></span> | <span data-ttu-id="5f6ef-147">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5f6ef-147">Parameter</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5f6ef-148">GET</span><span class="sxs-lookup"><span data-stu-id="5f6ef-148">GET</span></span> | <span data-ttu-id="5f6ef-149">api/제품</span><span class="sxs-lookup"><span data-stu-id="5f6ef-149">api/products</span></span> | <span data-ttu-id="5f6ef-150">겟올프로덕스</span><span class="sxs-lookup"><span data-stu-id="5f6ef-150">GetAllProducts</span></span> | <span data-ttu-id="5f6ef-151">*(없음)*</span><span class="sxs-lookup"><span data-stu-id="5f6ef-151">*(none)*</span></span> |
| <span data-ttu-id="5f6ef-152">GET</span><span class="sxs-lookup"><span data-stu-id="5f6ef-152">GET</span></span> | <span data-ttu-id="5f6ef-153">api/제품/4</span><span class="sxs-lookup"><span data-stu-id="5f6ef-153">api/products/4</span></span> | <span data-ttu-id="5f6ef-154">제품비하이드</span><span class="sxs-lookup"><span data-stu-id="5f6ef-154">GetProductById</span></span> | <span data-ttu-id="5f6ef-155">4</span><span class="sxs-lookup"><span data-stu-id="5f6ef-155">4</span></span> |
| <span data-ttu-id="5f6ef-156">Delete</span><span class="sxs-lookup"><span data-stu-id="5f6ef-156">DELETE</span></span> | <span data-ttu-id="5f6ef-157">api/제품/4</span><span class="sxs-lookup"><span data-stu-id="5f6ef-157">api/products/4</span></span> | <span data-ttu-id="5f6ef-158">제품 삭제</span><span class="sxs-lookup"><span data-stu-id="5f6ef-158">DeleteProduct</span></span> | <span data-ttu-id="5f6ef-159">4</span><span class="sxs-lookup"><span data-stu-id="5f6ef-159">4</span></span> |
| <span data-ttu-id="5f6ef-160">POST</span><span class="sxs-lookup"><span data-stu-id="5f6ef-160">POST</span></span> | <span data-ttu-id="5f6ef-161">api/제품</span><span class="sxs-lookup"><span data-stu-id="5f6ef-161">api/products</span></span> | <span data-ttu-id="5f6ef-162">*(일치하지 않습니다)*</span><span class="sxs-lookup"><span data-stu-id="5f6ef-162">*(no match)*</span></span> |  |

<span data-ttu-id="5f6ef-163">URI의 *{id}* 세그먼트(있는 경우)가 작업의 *ID* 매개 변수에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-163">Notice that the *{id}* segment of the URI, if present, is mapped to the *id* parameter of the action.</span></span> <span data-ttu-id="5f6ef-164">이 예제에서 컨트롤러는 ID 매개 변수가 있는 메서드와 *매개* 변수가 없는 두 가지 GET 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-164">In this example, the controller defines two GET methods, one with an *id* parameter and one with no parameters.</span></span>

<span data-ttu-id="5f6ef-165">또한 컨트롤러가 Post를 정의하지 않으므로 POST 요청이 &quot;실패합니다... &quot; 메서드를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-165">Also, note that the POST request will fail, because the controller does not define a &quot;Post...&quot; method.</span></span>

## <a name="routing-variations"></a><span data-ttu-id="5f6ef-166">라우팅 변형</span><span class="sxs-lookup"><span data-stu-id="5f6ef-166">Routing Variations</span></span>

<span data-ttu-id="5f6ef-167">이전 섹션에서는 ASP.NET 웹 API에 대한 기본 라우팅 메커니즘을 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-167">The previous section described the basic routing mechanism for ASP.NET Web API.</span></span> <span data-ttu-id="5f6ef-168">이 섹션에서는 몇 가지 변형에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-168">This section describes some variations.</span></span>

### <a name="http-verbs"></a><span data-ttu-id="5f6ef-169">HTTP 동사</span><span class="sxs-lookup"><span data-stu-id="5f6ef-169">HTTP verbs</span></span>

<span data-ttu-id="5f6ef-170">HTTP 동사에 대 한 명명 규칙을 사용 하는 대신 다음 특성 중 하나를 사용 하 여 작업 메서드를 장식 하 여 작업에 대 한 HTTP 동사를 명시적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-170">Instead of using the naming convention for HTTP verbs, you can explicitly specify the HTTP verb for an action by decorating the action method with one of the following attributes:</span></span>

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

<span data-ttu-id="5f6ef-171">다음 예제에서는 메서드가 `FindProduct` GET 요청에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-171">In the following example, the `FindProduct` method is mapped to GET requests:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="5f6ef-172">작업에 대해 여러 HTTP 동사를 허용하거나 GET, PUT, POST, DELETE, HEAD, OPTIONS 및 PATCH `[AcceptVerbs]` 이외의 HTTP 동사를 허용하려면 HTTP 동사 목록을 사용하는 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-172">To allow multiple HTTP verbs for an action, or to allow HTTP verbs other than GET, PUT, POST, DELETE, HEAD, OPTIONS, and PATCH, use the `[AcceptVerbs]` attribute, which takes a list of HTTP verbs.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a><span data-ttu-id="5f6ef-173">작업 이름으로 라우팅</span><span class="sxs-lookup"><span data-stu-id="5f6ef-173">Routing by Action Name</span></span>

<span data-ttu-id="5f6ef-174">기본 라우팅 템플릿을 사용하는 Web API는 HTTP 동사를 사용하여 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-174">With the default routing template, Web API uses the HTTP verb to select the action.</span></span> <span data-ttu-id="5f6ef-175">그러나 작업 이름이 URI에 포함된 경로를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-175">However, you can also create a route where the action name is included in the URI:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="5f6ef-176">이 경로 템플릿에서 *{action}* 매개 변수는 컨트롤러의 작업 메서드이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-176">In this route template, the *{action}* parameter names the action method on the controller.</span></span> <span data-ttu-id="5f6ef-177">이 라우팅 스타일을 사용하면 특성을 사용하여 허용되는 HTTP 동사를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-177">With this style of routing, use attributes to specify the allowed HTTP verbs.</span></span> <span data-ttu-id="5f6ef-178">예를 들어 컨트롤러에 다음과 같은 메서드가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-178">For example, suppose your controller has the following method:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="5f6ef-179">이 경우 "api/제품/세부 정보/1"에 대한 GET `Details` 요청이 메서드에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-179">In this case, a GET request for "api/products/details/1" would map to the `Details` method.</span></span> <span data-ttu-id="5f6ef-180">이 라우팅 스타일은 ASP.NET MVC와 유사하며 RPC 스타일 API에 적합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-180">This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API.</span></span>

<span data-ttu-id="5f6ef-181">`[ActionName]` 특성을 사용하여 작업 이름을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-181">You can override the action name by using the `[ActionName]` attribute.</span></span> <span data-ttu-id="5f6ef-182">다음 예제에서는 API/제품/축소판/ID에 매핑하는 &quot;두*id*가지 작업이 있습니다. 하나는 GET을 지원하고 다른 하나는 POST를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-182">In the following example, there are two actions that map to &quot;api/products/thumbnail/*id*. One supports GET and the other supports POST:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a><span data-ttu-id="5f6ef-183">비작업</span><span class="sxs-lookup"><span data-stu-id="5f6ef-183">Non-Actions</span></span>

<span data-ttu-id="5f6ef-184">메서드가 작업으로 호출되지 않도록 하려면 특성을 `[NonAction]` 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-184">To prevent a method from getting invoked as an action, use the `[NonAction]` attribute.</span></span> <span data-ttu-id="5f6ef-185">이는 메서드가 라우팅 규칙과 일치하지 않더라도 메서드가 동작이 아님을 프레임워크에 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-185">This signals to the framework that the method is not an action, even if it would otherwise match the routing rules.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a><span data-ttu-id="5f6ef-186">추가 참고 자료</span><span class="sxs-lookup"><span data-stu-id="5f6ef-186">Further Reading</span></span>

<span data-ttu-id="5f6ef-187">이 항목에서는 라우팅에 대한 높은 수준의 보기를 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-187">This topic provided a high-level view of routing.</span></span> <span data-ttu-id="5f6ef-188">자세한 내용은 프레임워크가 [URI를](routing-and-action-selection.md)경로에 일치시키고 컨트롤러를 선택한 다음 호출할 작업을 선택하는 방법을 정확하게 설명하는 라우팅 및 작업 선택을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-188">For more detail, see [Routing and Action Selection](routing-and-action-selection.md), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.</span></span>
