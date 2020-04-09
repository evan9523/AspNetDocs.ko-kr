---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: ASP.NET 웹 API 2의 특성 라우팅 | 마이크로 소프트 문서
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: bb68fe8e6769619029a3fa039d6f0d6f3303afbe
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675381"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="13cff-102">ASP.NET 웹 API 2의 특성 라우팅</span><span class="sxs-lookup"><span data-stu-id="13cff-102">Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="13cff-103">로 [마이크 와슨](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="13cff-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="13cff-104">*라우팅은* 웹 API가 URI를 작업에 일치시는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-104">*Routing* is how Web API matches a URI to an action.</span></span> <span data-ttu-id="13cff-105">웹 API 2는 특성 라우팅이라는 새로운 유형의 *라우팅을*지원합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-105">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="13cff-106">이름에서 알 수 있듯이 특성 라우팅은 특성을 사용하여 경로를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-106">As the name implies, attribute routing uses attributes to define routes.</span></span> <span data-ttu-id="13cff-107">특성 라우팅을 사용하면 웹 API의 URI를 보다 세한 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-107">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="13cff-108">예를 들어 리소스 계층구조를 설명하는 URI를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-108">For example, you can easily create URIs that describe hierarchies of resources.</span></span>

<span data-ttu-id="13cff-109">규칙 기반 라우팅이라고 하는 이전 라우팅 스타일은 여전히 완벽하게 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-109">The earlier style of routing, called convention-based routing, is still fully supported.</span></span> <span data-ttu-id="13cff-110">실제로 동일한 프로젝트에서 두 기술을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-110">In fact, you can combine both techniques in the same project.</span></span>

<span data-ttu-id="13cff-111">이 항목에서는 특성 라우팅을 사용하도록 설정하는 방법을 보여 주며 특성 라우팅에 대한 다양한 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-111">This topic shows how to enable attribute routing and describes the various options for attribute routing.</span></span> <span data-ttu-id="13cff-112">특성 라우팅을 사용하는 종단 간 자습서의 경우 [웹 API 2에서 특성 라우팅을 사용하여 REST API 만들기를](create-a-rest-api-with-attribute-routing.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="13cff-112">For an end-to-end tutorial that uses attribute routing, see [Create a REST API with Attribute Routing in Web API 2](create-a-rest-api-with-attribute-routing.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13cff-113">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="13cff-113">Prerequisites</span></span>

<span data-ttu-id="13cff-114">[비주얼 스튜디오 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) 커뮤니티, 전문가 또는 엔터프라이즈 에디션</span><span class="sxs-lookup"><span data-stu-id="13cff-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition</span></span>

<span data-ttu-id="13cff-115">또는 NuGet 패키지 관리자를 사용하여 필요한 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-115">Alternatively, use NuGet Package Manager to install the necessary packages.</span></span> <span data-ttu-id="13cff-116">Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자를**선택한 다음 **패키지 관리자 콘솔을**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-116">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="13cff-117">패키지 관리자 콘솔 창에 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-117">Enter the following command in the Package Manager Console window:</span></span>

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a><span data-ttu-id="13cff-118">특성 라우팅이 왜 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="13cff-118">Why Attribute Routing?</span></span>

<span data-ttu-id="13cff-119">웹 API의 첫 번째 릴리스는 *규칙 기반* 라우팅을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-119">The first release of Web API used *convention-based* routing.</span></span> <span data-ttu-id="13cff-120">해당 라우팅 유형에서는 기본적으로 매개 변수화된 문자열인 하나 이상의 경로 템플릿을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-120">In that type of routing, you define one or more route templates, which are basically parameterized strings.</span></span> <span data-ttu-id="13cff-121">프레임워크가 요청을 받으면 URI를 경로 템플릿과 일치시게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-121">When the framework receives a request, it matches the URI against the route template.</span></span> <span data-ttu-id="13cff-122">규칙 기반 라우팅에 대한 자세한 내용은 [ASP.NET 웹 API의 라우팅을](routing-in-aspnet-web-api.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="13cff-122">For more information about convention-based routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="13cff-123">규칙 기반 라우팅의 한 가지 장점은 템플릿이 한 곳에 정의되고 라우팅 규칙이 모든 컨트롤러에 일관되게 적용된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-123">One advantage of convention-based routing is that templates are defined in a single place, and the routing rules are applied consistently across all controllers.</span></span> <span data-ttu-id="13cff-124">안타깝게도 규칙 기반 라우팅은 RESTful API에서 일반적인 특정 URI 패턴을 지원하기 어렵게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-124">Unfortunately, convention-based routing makes it hard to support certain URI patterns that are common in RESTful APIs.</span></span> <span data-ttu-id="13cff-125">예를 들어 리소스에는 종종 하위 리소스가 포함됩니다: 고객이 주문을 하고, 영화에 액터가 있고, 책에 저자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-125">For example, resources often contain child resources: Customers have orders, movies have actors, books have authors, and so forth.</span></span> <span data-ttu-id="13cff-126">이러한 관계를 반영하는 URI를 만드는 것은 당연합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-126">It's natural to create URIs that reflect these relations:</span></span>

`/customers/1/orders`

<span data-ttu-id="13cff-127">이러한 유형의 URI는 규칙 기반 라우팅을 사용하여 만들기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-127">This type of URI is difficult to create using convention-based routing.</span></span> <span data-ttu-id="13cff-128">이 작업을 수행할 수 있지만 컨트롤러 나 리소스 유형이 많은 경우 결과가 잘 확장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-128">Although it can be done, the results don't scale well if you have many controllers or resource types.</span></span>

<span data-ttu-id="13cff-129">특성 라우팅을 사용하면 이 URI에 대한 경로를 정의하는 것이 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-129">With attribute routing, it's trivial to define a route for this URI.</span></span> <span data-ttu-id="13cff-130">컨트롤러 작업에 특성을 추가하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-130">You simply add an attribute to the controller action:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

<span data-ttu-id="13cff-131">다음은 특성 라우팅을 쉽게 만드는 몇 가지 다른 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-131">Here are some other patterns that attribute routing makes easy.</span></span>

<span data-ttu-id="13cff-132">**API 버전 관리**</span><span class="sxs-lookup"><span data-stu-id="13cff-132">**API versioning**</span></span>

<span data-ttu-id="13cff-133">이 예제에서는 "/api/v1/제품"이 "/api/v2/products"가 아닌 다른 컨트롤러로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-133">In this example, "/api/v1/products" would be routed to a different controller than "/api/v2/products".</span></span>

`/api/v1/products`
`/api/v2/products`

<span data-ttu-id="13cff-134">**오버로드된 URI 세그먼트**</span><span class="sxs-lookup"><span data-stu-id="13cff-134">**Overloaded URI segments**</span></span>

<span data-ttu-id="13cff-135">이 예제에서 "1"은 주문 번호이지만 컬렉션에 "보류 중"이 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-135">In this example, "1" is an order number, but "pending" maps to a collection.</span></span>

`/orders/1`
`/orders/pending`

<span data-ttu-id="13cff-136">**여러 매개 변수 유형**</span><span class="sxs-lookup"><span data-stu-id="13cff-136">**Multiple parameter types**</span></span>

<span data-ttu-id="13cff-137">이 예에서 "1"은 주문 번호이지만 "2013/06/16"은 날짜를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-137">In this example, "1" is an order number, but "2013/06/16" specifies a date.</span></span>

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a><span data-ttu-id="13cff-138">특성 라우팅 사용</span><span class="sxs-lookup"><span data-stu-id="13cff-138">Enabling Attribute Routing</span></span>

<span data-ttu-id="13cff-139">특성 라우팅을 사용하려면 구성 중에 **MapHttpAttributeRoutes를 호출합니다.**</span><span class="sxs-lookup"><span data-stu-id="13cff-139">To enable attribute routing, call **MapHttpAttributeRoutes** during configuration.</span></span> <span data-ttu-id="13cff-140">이 확장 메서드는 **System.Web.Http.HttpConfigurationExtensions** 클래스에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-140">This extension method is defined in the **System.Web.Http.HttpConfigurationExtensions** class.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

<span data-ttu-id="13cff-141">특성 라우팅을 규칙 [기반](routing-in-aspnet-web-api.md) 라우팅과 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-141">Attribute routing can be combined with [convention-based](routing-in-aspnet-web-api.md) routing.</span></span> <span data-ttu-id="13cff-142">규칙 기반 경로를 정의하려면 **MapHttpRoute** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-142">To define convention-based routes, call the **MapHttpRoute** method.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

<span data-ttu-id="13cff-143">웹 API 구성에 대한 자세한 내용은 [웹 API 2에 ASP.NET 구성을](../advanced/configuring-aspnet-web-api.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="13cff-143">For more information about configuring Web API, see [Configuring ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md).</span></span>

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a><span data-ttu-id="13cff-144">참고: 웹 API 1에서 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="13cff-144">Note: Migrating From Web API 1</span></span>

<span data-ttu-id="13cff-145">웹 API 2 이전에는 웹 API 프로젝트 템플릿이 다음과 같은 코드를 생성했습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-145">Prior to Web API 2, the Web API project templates generated code like this:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

<span data-ttu-id="13cff-146">특성 라우팅을 사용하도록 설정하면 이 코드에서 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-146">If attribute routing is enabled, this code will throw an exception.</span></span> <span data-ttu-id="13cff-147">특성 라우팅을 사용하도록 기존 Web API 프로젝트를 업그레이드하는 경우 이 구성 코드를 다음으로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-147">If you upgrade an existing Web API project to use attribute routing, make sure to update this configuration code to the following:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> <span data-ttu-id="13cff-148">자세한 내용은 [ASP.NET 호스팅을 통해 웹 API 구성을](../advanced/configuring-aspnet-web-api.md#webhost)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="13cff-148">For more information, see [Configuring Web API with ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span></span>

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a><span data-ttu-id="13cff-149">경로 특성 추가</span><span class="sxs-lookup"><span data-stu-id="13cff-149">Adding Route Attributes</span></span>

<span data-ttu-id="13cff-150">다음은 특성을 사용하여 정의된 경로의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-150">Here is an example of a route defined using an attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

<span data-ttu-id="13cff-151">문자열 &quot;고객/{customerId}/주문은&quot; 경로에 대 한 URI 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-151">The string &quot;customers/{customerId}/orders&quot; is the URI template for the route.</span></span> <span data-ttu-id="13cff-152">웹 API는 요청 URI를 템플릿에 일치시키려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-152">Web API tries to match the request URI to the template.</span></span> <span data-ttu-id="13cff-153">이 예제에서 "고객" 및 "주문"은 리터럴 세그먼트이고 "{customerId}"는 변수 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-153">In this example, "customers" and "orders" are literal segments, and "{customerId}" is a variable parameter.</span></span> <span data-ttu-id="13cff-154">다음 URI는 이 템플릿과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-154">The following URIs would match this template:</span></span>

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

<span data-ttu-id="13cff-155">이 항목의 후반부에서 설명하는 제약 조건을 사용하여 일치를 제한할 수 [있습니다.](#constraints)</span><span class="sxs-lookup"><span data-stu-id="13cff-155">You can restrict the matching by using [constraints](#constraints), described later in this topic.</span></span>

<span data-ttu-id="13cff-156">경로 템플릿의 &quot;{customerId}&quot; 매개 변수가 메서드의 *customerId* 매개 변수 의 이름과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-156">Notice that the &quot;{customerId}&quot; parameter in the route template matches the name of the *customerId* parameter in the method.</span></span> <span data-ttu-id="13cff-157">Web API가 컨트롤러 작업을 호출하면 경로 매개 변수를 바인딩하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-157">When Web API invokes the controller action, it tries to bind the route parameters.</span></span> <span data-ttu-id="13cff-158">예를 들어 URI인 `http://example.com/customers/1/orders`경우 Web API는 작업에서 *customerId* 매개 변수에 값 "1"을 바인딩하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-158">For example, if the URI is `http://example.com/customers/1/orders`, Web API tries to bind the value "1" to the *customerId* parameter in the action.</span></span>

<span data-ttu-id="13cff-159">URI 템플릿에는 다음과 같은 여러 매개 변수가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-159">A URI template can have several parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

<span data-ttu-id="13cff-160">경로 특성이 없는 모든 컨트롤러 메서드는 규칙 기반 라우팅을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-160">Any controller methods that do not have a route attribute use convention-based routing.</span></span> <span data-ttu-id="13cff-161">이렇게 하면 동일한 프로젝트에서 두 가지 유형의 라우팅을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-161">That way, you can combine both types of routing in the same project.</span></span>

## <a name="http-methods"></a><span data-ttu-id="13cff-162">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="13cff-162">HTTP Methods</span></span>

<span data-ttu-id="13cff-163">또한 웹 API는 요청의 HTTP 메서드(GET, POST 등)에 따라 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-163">Web API also selects actions based on the HTTP method of the request (GET, POST, etc).</span></span> <span data-ttu-id="13cff-164">기본적으로 Web API는 컨트롤러 메서드 이름의 시작과 대/소문자를 구분하지 않는 일치를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-164">By default, Web API looks for a case-insensitive match with the start of the controller method name.</span></span> <span data-ttu-id="13cff-165">예를 들어, 명명된 `PutCustomers` 컨트롤러 메서드는 HTTP PUT 요청과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-165">For example, a controller method named `PutCustomers` matches an HTTP PUT request.</span></span>

<span data-ttu-id="13cff-166">메서드를 다음과 같은 특성으로 장식하여 이 규칙을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-166">You can override this convention by decorating the method with any the following attributes:</span></span>

- <span data-ttu-id="13cff-167">**[HttpDelete]**</span><span class="sxs-lookup"><span data-stu-id="13cff-167">**[HttpDelete]**</span></span>
- <span data-ttu-id="13cff-168">**[HttpGet]**</span><span class="sxs-lookup"><span data-stu-id="13cff-168">**[HttpGet]**</span></span>
- <span data-ttu-id="13cff-169">**[HttpHead]**</span><span class="sxs-lookup"><span data-stu-id="13cff-169">**[HttpHead]**</span></span>
- <span data-ttu-id="13cff-170">**[Http옵션]**</span><span class="sxs-lookup"><span data-stu-id="13cff-170">**[HttpOptions]**</span></span>
- <span data-ttu-id="13cff-171">**[Http패치]**</span><span class="sxs-lookup"><span data-stu-id="13cff-171">**[HttpPatch]**</span></span>
- <span data-ttu-id="13cff-172">**[HttpPost]**</span><span class="sxs-lookup"><span data-stu-id="13cff-172">**[HttpPost]**</span></span>
- <span data-ttu-id="13cff-173">**[HttpPut]**</span><span class="sxs-lookup"><span data-stu-id="13cff-173">**[HttpPut]**</span></span>

<span data-ttu-id="13cff-174">다음 예제는 CreateBook 메서드를 HTTP POST 요청에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-174">The following example maps the CreateBook method to HTTP POST requests.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

<span data-ttu-id="13cff-175">비표준 메서드를 포함한 다른 모든 HTTP 메서드의 경우 HTTP 메서드 목록을 사용하는 **AcceptVerbs** 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-175">For all other HTTP methods, including non-standard methods, use the **AcceptVerbs** attribute, which takes a list of HTTP methods.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a><span data-ttu-id="13cff-176">배관 접두사</span><span class="sxs-lookup"><span data-stu-id="13cff-176">Route Prefixes</span></span>

<span data-ttu-id="13cff-177">컨트롤러의 경로는 모두 동일한 접두사로 시작하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-177">Often, the routes in a controller all start with the same prefix.</span></span> <span data-ttu-id="13cff-178">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="13cff-178">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

<span data-ttu-id="13cff-179">**[RoutePrefix]** 특성을 사용하여 전체 컨트롤러에 대한 공통 접두사를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-179">You can set a common prefix for an entire controller by using the **[RoutePrefix]** attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

<span data-ttu-id="13cff-180">메서드 특성에 물결표(~)를 사용하여 배관 접두사를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-180">Use a tilde (~) on the method attribute to override the route prefix:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

<span data-ttu-id="13cff-181">배관 접두사에는 매개 변수가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-181">The route prefix can include parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a><span data-ttu-id="13cff-182">배관 구속조건</span><span class="sxs-lookup"><span data-stu-id="13cff-182">Route Constraints</span></span>

<span data-ttu-id="13cff-183">경로 제약 조건을 사용하면 경로 템플릿의 매개 변수가 일치하는 방법을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-183">Route constraints let you restrict how the parameters in the route template are matched.</span></span> <span data-ttu-id="13cff-184">일반 구문은 &quot;{매개 변수&quot;:제약 조건}입니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-184">The general syntax is &quot;{parameter:constraint}&quot;.</span></span> <span data-ttu-id="13cff-185">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="13cff-185">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

<span data-ttu-id="13cff-186">여기서 첫 번째 경로는 URI의 &quot;&quot; ID 세그먼트가 정수인 경우에만 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-186">Here, the first route will only be selected if the &quot;id&quot; segment of the URI is an integer.</span></span> <span data-ttu-id="13cff-187">그렇지 않으면 두 번째 경로가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-187">Otherwise, the second route will be chosen.</span></span>

<span data-ttu-id="13cff-188">다음 표에는 지원되는 제약 조건이 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-188">The following table lists the constraints that are supported.</span></span>

| <span data-ttu-id="13cff-189">제약 조건</span><span class="sxs-lookup"><span data-stu-id="13cff-189">Constraint</span></span> | <span data-ttu-id="13cff-190">Description</span><span class="sxs-lookup"><span data-stu-id="13cff-190">Description</span></span> | <span data-ttu-id="13cff-191">예제</span><span class="sxs-lookup"><span data-stu-id="13cff-191">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13cff-192">alpha</span><span class="sxs-lookup"><span data-stu-id="13cff-192">alpha</span></span> | <span data-ttu-id="13cff-193">대문자 또는 소문자 라틴어 알파벳 문자(a-z, A-Z)와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-193">Matches uppercase or lowercase Latin alphabet characters (a-z, A-Z)</span></span> | <span data-ttu-id="13cff-194">{x:알파}</span><span class="sxs-lookup"><span data-stu-id="13cff-194">{x:alpha}</span></span> |
| <span data-ttu-id="13cff-195">bool</span><span class="sxs-lookup"><span data-stu-id="13cff-195">bool</span></span> | <span data-ttu-id="13cff-196">부울 값과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-196">Matches a Boolean value.</span></span> | <span data-ttu-id="13cff-197">{x:bool}</span><span class="sxs-lookup"><span data-stu-id="13cff-197">{x:bool}</span></span> |
| <span data-ttu-id="13cff-198">Datetime</span><span class="sxs-lookup"><span data-stu-id="13cff-198">datetime</span></span> | <span data-ttu-id="13cff-199">**DateTime** 값을 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-199">Matches a **DateTime** value.</span></span> | <span data-ttu-id="13cff-200">{x:날짜 시간}</span><span class="sxs-lookup"><span data-stu-id="13cff-200">{x:datetime}</span></span> |
| <span data-ttu-id="13cff-201">decimal</span><span class="sxs-lookup"><span data-stu-id="13cff-201">decimal</span></span> | <span data-ttu-id="13cff-202">소수점 값과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-202">Matches a decimal value.</span></span> | <span data-ttu-id="13cff-203">{x:소수점}</span><span class="sxs-lookup"><span data-stu-id="13cff-203">{x:decimal}</span></span> |
| <span data-ttu-id="13cff-204">double</span><span class="sxs-lookup"><span data-stu-id="13cff-204">double</span></span> | <span data-ttu-id="13cff-205">64비트 부동 점 값과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-205">Matches a 64-bit floating-point value.</span></span> | <span data-ttu-id="13cff-206">{x:더블}</span><span class="sxs-lookup"><span data-stu-id="13cff-206">{x:double}</span></span> |
| <span data-ttu-id="13cff-207">float</span><span class="sxs-lookup"><span data-stu-id="13cff-207">float</span></span> | <span data-ttu-id="13cff-208">32비트 부동 점 값과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-208">Matches a 32-bit floating-point value.</span></span> | <span data-ttu-id="13cff-209">{x:float}</span><span class="sxs-lookup"><span data-stu-id="13cff-209">{x:float}</span></span> |
| <span data-ttu-id="13cff-210">guid</span><span class="sxs-lookup"><span data-stu-id="13cff-210">guid</span></span> | <span data-ttu-id="13cff-211">GUID 값과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-211">Matches a GUID value.</span></span> | <span data-ttu-id="13cff-212">{x:guid}</span><span class="sxs-lookup"><span data-stu-id="13cff-212">{x:guid}</span></span> |
| <span data-ttu-id="13cff-213">int</span><span class="sxs-lookup"><span data-stu-id="13cff-213">int</span></span> | <span data-ttu-id="13cff-214">32비트 정수 값과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-214">Matches a 32-bit integer value.</span></span> | <span data-ttu-id="13cff-215">{x:int}</span><span class="sxs-lookup"><span data-stu-id="13cff-215">{x:int}</span></span> |
| <span data-ttu-id="13cff-216">length</span><span class="sxs-lookup"><span data-stu-id="13cff-216">length</span></span> | <span data-ttu-id="13cff-217">지정된 길이 또는 지정된 길이 범위 내에서 문자열을 일치시면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-217">Matches a string with the specified length or within a specified range of lengths.</span></span> | <span data-ttu-id="13cff-218">{x:길이(6)} {x:길이(1,20)}</span><span class="sxs-lookup"><span data-stu-id="13cff-218">{x:length(6)} {x:length(1,20)}</span></span> |
| <span data-ttu-id="13cff-219">long</span><span class="sxs-lookup"><span data-stu-id="13cff-219">long</span></span> | <span data-ttu-id="13cff-220">64비트 정수 값과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-220">Matches a 64-bit integer value.</span></span> | <span data-ttu-id="13cff-221">{x:long}</span><span class="sxs-lookup"><span data-stu-id="13cff-221">{x:long}</span></span> |
| <span data-ttu-id="13cff-222">max</span><span class="sxs-lookup"><span data-stu-id="13cff-222">max</span></span> | <span data-ttu-id="13cff-223">정수와 최대값을 일치시다.</span><span class="sxs-lookup"><span data-stu-id="13cff-223">Matches an integer with a maximum value.</span></span> | <span data-ttu-id="13cff-224">{x:최대(10)}</span><span class="sxs-lookup"><span data-stu-id="13cff-224">{x:max(10)}</span></span> |
| <span data-ttu-id="13cff-225">Maxlength</span><span class="sxs-lookup"><span data-stu-id="13cff-225">maxlength</span></span> | <span data-ttu-id="13cff-226">최대 길이의 문자열과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-226">Matches a string with a maximum length.</span></span> | <span data-ttu-id="13cff-227">{x:최대길이(10)}</span><span class="sxs-lookup"><span data-stu-id="13cff-227">{x:maxlength(10)}</span></span> |
| <span data-ttu-id="13cff-228">min</span><span class="sxs-lookup"><span data-stu-id="13cff-228">min</span></span> | <span data-ttu-id="13cff-229">정수와 최소 값을 일치시면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-229">Matches an integer with a minimum value.</span></span> | <span data-ttu-id="13cff-230">{x:min(10)}</span><span class="sxs-lookup"><span data-stu-id="13cff-230">{x:min(10)}</span></span> |
| <span data-ttu-id="13cff-231">최소 길이</span><span class="sxs-lookup"><span data-stu-id="13cff-231">minlength</span></span> | <span data-ttu-id="13cff-232">최소 길이의 문자열과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-232">Matches a string with a minimum length.</span></span> | <span data-ttu-id="13cff-233">{x:최소길이(10)}</span><span class="sxs-lookup"><span data-stu-id="13cff-233">{x:minlength(10)}</span></span> |
| <span data-ttu-id="13cff-234">range</span><span class="sxs-lookup"><span data-stu-id="13cff-234">range</span></span> | <span data-ttu-id="13cff-235">값 범위 내에서 정수를 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-235">Matches an integer within a range of values.</span></span> | <span data-ttu-id="13cff-236">{x:범위(10,50)}</span><span class="sxs-lookup"><span data-stu-id="13cff-236">{x:range(10,50)}</span></span> |
| <span data-ttu-id="13cff-237">regex</span><span class="sxs-lookup"><span data-stu-id="13cff-237">regex</span></span> | <span data-ttu-id="13cff-238">정규식과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-238">Matches a regular expression.</span></span> | <span data-ttu-id="13cff-239">{x:정규식(^\\d{3}-\d{3}{4}-\d $)}</span><span class="sxs-lookup"><span data-stu-id="13cff-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span></span> |

<span data-ttu-id="13cff-240">min과 &quot;&quot;같은 일부 제약 조건은 괄호 안에 인수를 취합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-240">Notice that some of the constraints, such as &quot;min&quot;, take arguments in parentheses.</span></span> <span data-ttu-id="13cff-241">콜론으로 구분된 매개변수에 여러 구속조건을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-241">You can apply multiple constraints to a parameter, separated by a colon.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a><span data-ttu-id="13cff-242">사용자 지정 경로 제약 조건</span><span class="sxs-lookup"><span data-stu-id="13cff-242">Custom Route Constraints</span></span>

<span data-ttu-id="13cff-243">**IHttpRouteConstraint** 인터페이스를 구현 하여 사용자 지정 경로 제약 조건을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-243">You can create custom route constraints by implementing the **IHttpRouteConstraint** interface.</span></span> <span data-ttu-id="13cff-244">예를 들어 다음 제약 조건은 매개 변수를 0이 아닌 정수 값으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-244">For example, the following constraint restricts a parameter to a non-zero integer value.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

<span data-ttu-id="13cff-245">다음 코드는 제약 조건을 등록하는 방법을 보여 주며 다음과 같은 방법을 보여 주며</span><span class="sxs-lookup"><span data-stu-id="13cff-245">The following code shows how to register the constraint:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

<span data-ttu-id="13cff-246">이제 경로에 제약 조건을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-246">Now you can apply the constraint in your routes:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

<span data-ttu-id="13cff-247">**IInline제약** 해결사 인터페이스를 구현하여 전체 **DefaultInInConstraintResolver** 클래스를 대체할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-247">You can also replace the entire **DefaultInlineConstraintResolver** class by implementing the **IInlineConstraintResolver** interface.</span></span> <span data-ttu-id="13cff-248">이렇게 하면 **IInlineConstraintResolver의** 구현이 특별히 추가되지 않는 한 모든 기본 제공 제약 조건이 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-248">Doing so will replace all of the built-in constraints, unless your implementation of **IInlineConstraintResolver** specifically adds them.</span></span>

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a><span data-ttu-id="13cff-249">선택적 URI 매개 변수 및 기본값</span><span class="sxs-lookup"><span data-stu-id="13cff-249">Optional URI Parameters and Default Values</span></span>

<span data-ttu-id="13cff-250">경로 매개 변수에 물음표를 추가하여 URI 매개 변수를 선택적으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-250">You can make a URI parameter optional by adding a question mark to the route parameter.</span></span> <span data-ttu-id="13cff-251">경로 매개 변수가 선택 사항인 경우 메서드 매개 변수에 대한 기본값을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-251">If a route parameter is optional, you must define a default value for the method parameter.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

<span data-ttu-id="13cff-252">이 예제에서는 `/api/books/locale/1033` `/api/books/locale` 동일한 리소스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-252">In this example, `/api/books/locale/1033` and `/api/books/locale` return the same resource.</span></span>

<span data-ttu-id="13cff-253">또는 다음과 같이 경로 템플릿 내에서 기본값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-253">Alternatively, you can specify a default value inside the route template, as follows:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

<span data-ttu-id="13cff-254">이는 이전 예제와 거의 동일하지만 기본값을 적용할 때 동작의 약간의 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-254">This is almost the same as the previous example, but there is a slight difference of behavior when the default value is applied.</span></span>

- <span data-ttu-id="13cff-255">첫 번째 예제("{lcid:int?")에서 1033의 기본값은 메서드 매개 변수에 직접 할당되므로 매개 변수에 이 정확한 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-255">In the first example ("{lcid:int?}"), the default value of 1033 is assigned directly to the method parameter, so the parameter will have this exact value.</span></span>
- <span data-ttu-id="13cff-256">두 번째 예제("{lcid:int=1033}")에서 "1033"의 기본값은 모델 바인딩 프로세스를 거칩니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-256">In the second example ("{lcid:int=1033}"), the default value of "1033" goes through the model-binding process.</span></span> <span data-ttu-id="13cff-257">기본 모델 바인더는 "1033"을 숫자 값 1033으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-257">The default model-binder will convert "1033" to the numeric value 1033.</span></span> <span data-ttu-id="13cff-258">그러나 사용자 지정 모델 바인더를 연결하여 다른 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-258">However, you could plug in a custom model binder, which might do something different.</span></span>

<span data-ttu-id="13cff-259">대부분의 경우 파이프라인에 사용자 지정 모델 바인더가 없는 경우 두 양식은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-259">(In most cases, unless you have custom model binders in your pipeline, the two forms will be equivalent.)</span></span>

<a id="route-names"></a>
## <a name="route-names"></a><span data-ttu-id="13cff-260">루트 이름</span><span class="sxs-lookup"><span data-stu-id="13cff-260">Route Names</span></span>

<span data-ttu-id="13cff-261">웹 API에서 모든 경로에는 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-261">In Web API, every route has a name.</span></span> <span data-ttu-id="13cff-262">경로 이름은 HTTP 응답에 링크를 포함할 수 있도록 링크를 생성하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-262">Route names are useful for generating links, so that you can include a link in an HTTP response.</span></span>

<span data-ttu-id="13cff-263">경로 이름을 지정하려면 특성에 **Name** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-263">To specify the route name, set the **Name** property on the attribute.</span></span> <span data-ttu-id="13cff-264">다음 예제에서는 경로 이름을 설정하는 방법과 링크를 생성할 때 경로 이름을 사용하는 방법을 보여 주며, 또한 경로 이름을 사용하는 방법을 보여 주며,</span><span class="sxs-lookup"><span data-stu-id="13cff-264">The following example shows how to set the route name, and also how to use the route name when generating a link.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a><span data-ttu-id="13cff-265">경로 순서</span><span class="sxs-lookup"><span data-stu-id="13cff-265">Route Order</span></span>

<span data-ttu-id="13cff-266">프레임워크가 URI를 경로와 일치시키려고 하면 특정 순서로 경로를 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-266">When the framework tries to match a URI with a route, it evaluates the routes in a particular order.</span></span> <span data-ttu-id="13cff-267">순서를 지정하려면 route 특성에 **Order** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-267">To specify the order, set the **Order** property on the route attribute.</span></span> <span data-ttu-id="13cff-268">낮은 값이 먼저 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-268">Lower values are evaluated first.</span></span> <span data-ttu-id="13cff-269">기본 순서 값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-269">The default order value is zero.</span></span>

<span data-ttu-id="13cff-270">총 주문이 결정되는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-270">Here is how the total ordering is determined:</span></span>

1. <span data-ttu-id="13cff-271">경로 특성의 **Order** 속성을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-271">Compare the **Order** property of the route attribute.</span></span>
2. <span data-ttu-id="13cff-272">경로 템플릿의 각 URI 세그먼트를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-272">Look at each URI segment in the route template.</span></span> <span data-ttu-id="13cff-273">각 세그먼트에 대해 다음과 같이 주문하십시오.</span><span class="sxs-lookup"><span data-stu-id="13cff-273">For each segment, order as follows:</span></span>

    1. <span data-ttu-id="13cff-274">리터럴 세그먼트.</span><span class="sxs-lookup"><span data-stu-id="13cff-274">Literal segments.</span></span>
    2. <span data-ttu-id="13cff-275">구속조건이 있는 배관 매개변수입니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-275">Route parameters with constraints.</span></span>
    3. <span data-ttu-id="13cff-276">구속조건이 없는 배관 매개변수입니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-276">Route parameters without constraints.</span></span>
    4. <span data-ttu-id="13cff-277">구속조건이 있는 와일드카드 매개변수 세그먼트입니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-277">Wildcard parameter segments with constraints.</span></span>
    5. <span data-ttu-id="13cff-278">제약 조건이 없는 와일드카드 매개변수 세그먼트입니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-278">Wildcard parameter segments without constraints.</span></span>
3. <span data-ttu-id="13cff-279">넥타이의 경우 경로 템플릿의 대/소문자 구분 성 서수 문자열[비교(OrdinalIgnoreCase)에](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)의해 경로가 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-279">In the case of a tie, routes are ordered by a case-insensitive ordinal string comparison ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) of the route template.</span></span>

<span data-ttu-id="13cff-280">다음 예를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13cff-280">Here is an example.</span></span> <span data-ttu-id="13cff-281">다음 컨트롤러를 정의한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-281">Suppose you define the following controller:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

<span data-ttu-id="13cff-282">이러한 경로는 다음과 같이 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-282">These routes are ordered as follows.</span></span>

1. <span data-ttu-id="13cff-283">주문/세부 정보</span><span class="sxs-lookup"><span data-stu-id="13cff-283">orders/details</span></span>
2. <span data-ttu-id="13cff-284">주문/{id}</span><span class="sxs-lookup"><span data-stu-id="13cff-284">orders/{id}</span></span>
3. <span data-ttu-id="13cff-285">주문/{고객 이름}</span><span class="sxs-lookup"><span data-stu-id="13cff-285">orders/{customerName}</span></span>
4. <span data-ttu-id="13cff-286">주문/{\*날짜}</span><span class="sxs-lookup"><span data-stu-id="13cff-286">orders/{\*date}</span></span>
5. <span data-ttu-id="13cff-287">주문/보류 중</span><span class="sxs-lookup"><span data-stu-id="13cff-287">orders/pending</span></span>

<span data-ttu-id="13cff-288">"세부 정보"는 리터럴 세그먼트이며 "{id}" 앞에 표시되지만 **Order** 속성이 1이기 때문에 "보류 중"이 마지막으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-288">Notice that "details" is a literal segment and appears before "{id}", but "pending" appears last because the **Order** property is 1.</span></span> <span data-ttu-id="13cff-289">이 예제에서는 "세부 정보" 또는 "보류 중"이라는 고객이 없다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-289">(This example assumes there are no customers named "details" or "pending".</span></span> <span data-ttu-id="13cff-290">일반적으로 모호한 경로를 피하십시오.</span><span class="sxs-lookup"><span data-stu-id="13cff-290">In general, try to avoid ambiguous routes.</span></span> <span data-ttu-id="13cff-291">이 예제에서 더 나은 `GetByCustomer` 경로 템플릿은 "고객/{customerName}"입니다.</span><span class="sxs-lookup"><span data-stu-id="13cff-291">In this example, a better route template for `GetByCustomer` is "customers/{customerName}" )</span></span>
