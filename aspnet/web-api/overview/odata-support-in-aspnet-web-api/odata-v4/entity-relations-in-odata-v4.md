---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
title: ASP.NET Web API 2.2를 사용 하는 OData v4의 엔터티 관계 Microsoft Docs
author: MikeWasson
description: 대부분의 데이터 집합은 엔터티 간의 관계를 정의 합니다. 고객에 게는 주문이 있습니다. 서적에는 작성자가 있습니다. 제품에는 공급자가 있습니다. 클라이언트는 OData를 사용 하 여 탐색할 수 있습니다 ...
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 72657550-ec09-4779-9bfc-2fb15ecd51c7
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: fbafb2b2346689271905db5790cdddeeb809b070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484463"
---
# <a name="entity-relations-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="fe727-104">ASP.NET Web API 2.2를 사용 하는 OData v4의 엔터티 관계</span><span class="sxs-lookup"><span data-stu-id="fe727-104">Entity Relations in OData v4 Using ASP.NET Web API 2.2</span></span>

<span data-ttu-id="fe727-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="fe727-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="fe727-106">대부분의 데이터 집합은 엔터티 간의 관계를 정의 합니다. 고객에 게는 주문이 있습니다. 서적에는 작성자가 있습니다. 제품에는 공급자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-106">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="fe727-107">클라이언트는 OData를 사용 하 여 엔터티 관계를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-107">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="fe727-108">제품을 제공 하는 경우 공급자를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-108">Given a product, you can find the supplier.</span></span> <span data-ttu-id="fe727-109">관계를 만들거나 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-109">You can also create or remove relationships.</span></span> <span data-ttu-id="fe727-110">예를 들어 제품의 공급 업체를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-110">For example, you can set the supplier for a product.</span></span>
>
> <span data-ttu-id="fe727-111">이 자습서에서는 ASP.NET Web API를 사용 하 여 OData v4에서 이러한 작업을 지 원하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-111">This tutorial shows how to support these operations in OData v4 using ASP.NET Web API.</span></span> <span data-ttu-id="fe727-112">자습서에서는 [ASP.NET Web API 2를 사용 하 여 OData V4 끝점 만들기](create-an-odata-v4-endpoint.md)자습서를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-112">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="fe727-113">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="fe727-113">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="fe727-114">웹 API 2.1</span><span class="sxs-lookup"><span data-stu-id="fe727-114">Web API 2.1</span></span>
> - <span data-ttu-id="fe727-115">OData v4</span><span class="sxs-lookup"><span data-stu-id="fe727-115">OData v4</span></span>
> - <span data-ttu-id="fe727-116">Visual Studio 2013 (Visual [Studio 2017 다운로드](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span><span class="sxs-lookup"><span data-stu-id="fe727-116">Visual Studio 2013 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="fe727-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="fe727-117">Entity Framework 6</span></span>
> - <span data-ttu-id="fe727-118">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="fe727-118">.NET 4.5</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="fe727-119">자습서 버전</span><span class="sxs-lookup"><span data-stu-id="fe727-119">Tutorial versions</span></span>
>
> <span data-ttu-id="fe727-120">OData 버전 3의 경우 [odata v3에서 엔터티 관계 지원](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="fe727-120">For the OData Version 3, see [Supporting Entity Relations in OData v3](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations).</span></span>

## <a name="add-a-supplier-entity"></a><span data-ttu-id="fe727-121">공급자 엔터티 추가</span><span class="sxs-lookup"><span data-stu-id="fe727-121">Add a Supplier Entity</span></span>

> [!NOTE]
> <span data-ttu-id="fe727-122">자습서에서는 [ASP.NET Web API 2를 사용 하 여 OData V4 끝점 만들기](create-an-odata-v4-endpoint.md)자습서를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-122">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>

<span data-ttu-id="fe727-123">먼저 관련 엔터티가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-123">First, we need a related entity.</span></span> <span data-ttu-id="fe727-124">모델 폴더에 `Supplier` 라는 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-124">Add a class named `Supplier` in the Models folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample1.cs)]

<span data-ttu-id="fe727-125">`Product` 클래스에 탐색 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-125">Add a navigation property to the `Product` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample2.cs?highlight=13-15)]

<span data-ttu-id="fe727-126">Entity Framework `ProductsContext` 클래스에 새 **Dbset** 을 추가 하 여 데이터베이스에 공급자 테이블을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-126">Add a new **DbSet** to the `ProductsContext` class, so that Entity Framework will include the Supplier table in the database.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample3.cs?highlight=10)]

<span data-ttu-id="fe727-127">WebApiConfig.cs에서 엔터티 데이터 모델에 &quot;Suppliers&quot; 엔터티 집합을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-127">In WebApiConfig.cs, add a &quot;Suppliers&quot; entity set to the entity data model:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample4.cs?highlight=6)]

## <a name="add-a-suppliers-controller"></a><span data-ttu-id="fe727-128">Suppliers 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="fe727-128">Add a Suppliers Controller</span></span>

<span data-ttu-id="fe727-129">Controllers 폴더에 `SuppliersController` 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-129">Add a `SuppliersController` class to the Controllers folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="fe727-130">이 컨트롤러에 대 한 CRUD 작업을 추가 하는 방법을 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-130">I won't show how to add CRUD operations for this controller.</span></span> <span data-ttu-id="fe727-131">이러한 단계는 Products 컨트롤러의 경우와 동일 합니다 ( [OData V4 끝점 만들기](create-an-odata-v4-endpoint.md)참조).</span><span class="sxs-lookup"><span data-stu-id="fe727-131">The steps are the same as for the Products controller (see [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md)).</span></span>

## <a name="getting-related-entities"></a><span data-ttu-id="fe727-132">관련 엔터티 가져오기</span><span class="sxs-lookup"><span data-stu-id="fe727-132">Getting Related Entities</span></span>

<span data-ttu-id="fe727-133">제품에 대 한 공급자를 가져오기 위해 클라이언트는 GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-133">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample6.cmd)]

<span data-ttu-id="fe727-134">이 요청을 지원 하려면 `ProductsController` 클래스에 다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-134">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample7.cs)]

<span data-ttu-id="fe727-135">이 메서드는 기본 명명 규칙을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-135">This method uses a default naming convention</span></span>

- <span data-ttu-id="fe727-136">메서드 이름: GetX, 여기서 X는 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-136">Method name: GetX, where X is the navigation property.</span></span>
- <span data-ttu-id="fe727-137">매개 변수 이름: *key*</span><span class="sxs-lookup"><span data-stu-id="fe727-137">Parameter name: *key*</span></span>

<span data-ttu-id="fe727-138">이 명명 규칙을 따르는 경우 Web API는 자동으로 HTTP 요청을 컨트롤러 메서드에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-138">If you follow this naming convention, Web API automatically maps the HTTP request to the controller method.</span></span>

<span data-ttu-id="fe727-139">예제 HTTP 요청:</span><span class="sxs-lookup"><span data-stu-id="fe727-139">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample8.cmd)]

<span data-ttu-id="fe727-140">HTTP 응답 예제:</span><span class="sxs-lookup"><span data-stu-id="fe727-140">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample9.cmd)]

### <a name="getting-a-related-collection"></a><span data-ttu-id="fe727-141">관련 컬렉션 가져오기</span><span class="sxs-lookup"><span data-stu-id="fe727-141">Getting a related collection</span></span>

<span data-ttu-id="fe727-142">이전 예제에서 제품에는 하나의 공급 업체가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-142">In the previous example, a product has one supplier.</span></span> <span data-ttu-id="fe727-143">탐색 속성은 컬렉션을 반환할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-143">A navigation property can also return a collection.</span></span> <span data-ttu-id="fe727-144">다음 코드는 공급자에 대 한 제품을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-144">The following code gets the products for a supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample10.cs)]

<span data-ttu-id="fe727-145">이 경우 메서드는 **SingleResult&lt;t** 대신 **IQueryable** 을 반환&gt;</span><span class="sxs-lookup"><span data-stu-id="fe727-145">In this case, the method returns an **IQueryable** instead of a **SingleResult&lt;T&gt;**</span></span>

<span data-ttu-id="fe727-146">예제 HTTP 요청:</span><span class="sxs-lookup"><span data-stu-id="fe727-146">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample11.cmd)]

<span data-ttu-id="fe727-147">HTTP 응답 예제:</span><span class="sxs-lookup"><span data-stu-id="fe727-147">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample12.cmd)]

## <a name="creating-a-relationship-between-entities"></a><span data-ttu-id="fe727-148">엔터티 간 관계 만들기</span><span class="sxs-lookup"><span data-stu-id="fe727-148">Creating a Relationship Between Entities</span></span>

<span data-ttu-id="fe727-149">OData는 기존의 두 엔터티 간의 관계를 만들거나 제거 하는 것을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-149">OData supports creating or removing relationships between two existing entities.</span></span> <span data-ttu-id="fe727-150">OData v4 용어에서 관계는 &quot;참조&quot;입니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-150">In OData v4 terminology, the relationship is a &quot;reference&quot;.</span></span> <span data-ttu-id="fe727-151">(OData v3에서 관계를 *링크*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-151">(In OData v3, the relationship was called a *link*.</span></span> <span data-ttu-id="fe727-152">이 자습서에서는 프로토콜 차이가 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-152">The protocol differences don't matter for this tutorial.)</span></span>

<span data-ttu-id="fe727-153">참조에는 `/Entity/NavigationProperty/$ref`형식의 고유한 URI가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-153">A reference has its own URI, with the form `/Entity/NavigationProperty/$ref`.</span></span> <span data-ttu-id="fe727-154">예를 들어 다음은 제품과 공급자 간의 참조를 처리 하는 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-154">For example, here is the URI to address the reference between a product and its supplier:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample13.cmd)]

<span data-ttu-id="fe727-155">관계를 추가 하기 위해 클라이언트는이 주소에 POST 또는 PUT 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-155">To add a relationship, the client sends a POST or PUT request to this address.</span></span>

- <span data-ttu-id="fe727-156">탐색 속성이 단일 엔터티 (예: `Product.Supplier`) 인 경우에는를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-156">PUT if the navigation property is a single entity, such as `Product.Supplier`.</span></span>
- <span data-ttu-id="fe727-157">탐색 속성이 컬렉션인 경우 POST (예: `Supplier.Products`)</span><span class="sxs-lookup"><span data-stu-id="fe727-157">POST if the navigation property is a collection, such as `Supplier.Products`.</span></span>

<span data-ttu-id="fe727-158">요청의 본문에는 관계에 있는 다른 엔터티의 URI가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-158">The body of the request contains the URI of the other entity in the relation.</span></span> <span data-ttu-id="fe727-159">예제 요청은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-159">Here is an example request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample14.cmd)]

<span data-ttu-id="fe727-160">이 예제에서 클라이언트는 `/Products(6)/Supplier/$ref`에 PUT 요청을 보냅니다 .이는 ID = 6 인 제품의 `Supplier`에 대 한 $ref URI입니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-160">In this example, the client sends a PUT request to `/Products(6)/Supplier/$ref`, which is the $ref URI for the `Supplier` of the product with ID = 6.</span></span> <span data-ttu-id="fe727-161">요청이 성공 하면 서버는 204 (콘텐츠 없음) 응답을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-161">If the request succeeds, the server sends a 204 (No Content) response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample15.cmd)]

<span data-ttu-id="fe727-162">`Product`에 관계를 추가 하는 컨트롤러 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-162">Here is the controller method to add a relationship to a `Product`:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample16.cs)]

<span data-ttu-id="fe727-163">*NavigationProperty* 매개 변수는 설정할 관계를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-163">The *navigationProperty* parameter specifies which relationship to set.</span></span> <span data-ttu-id="fe727-164">엔터티에 대 한 탐색 속성이 두 개 이상 있는 경우 더 많은 `case` 문을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-164">(If there is more than one navigation property on the entity, you can add more `case` statements.)</span></span>

<span data-ttu-id="fe727-165">*Link* 매개 변수는 공급자의 URI를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-165">The *link* parameter contains the URI of the supplier.</span></span> <span data-ttu-id="fe727-166">Web API는 요청 본문을 자동으로 구문 분석 하 여이 매개 변수의 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-166">Web API automatically parses the request body to get the value for this parameter.</span></span>

<span data-ttu-id="fe727-167">공급자를 조회 하려면 *링크* 매개 변수의 일부인 ID (또는 키)가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-167">To look up the supplier, we need the ID (or key), which is part of the *link* parameter.</span></span> <span data-ttu-id="fe727-168">이렇게 하려면 다음 도우미 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-168">To do this, use the following helper method:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample17.cs)]

<span data-ttu-id="fe727-169">기본적으로이 메서드는 OData 라이브러리를 사용 하 여 URI 경로를 세그먼트로 분할 하 고, 키를 포함 하는 세그먼트를 찾고, 키를 올바른 형식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-169">Basically, this method uses the OData library to split the URI path into segments, find the segment that contains the key, and convert the key into the correct type.</span></span>

## <a name="deleting-a-relationship-between-entities"></a><span data-ttu-id="fe727-170">엔터티 간 관계 삭제</span><span class="sxs-lookup"><span data-stu-id="fe727-170">Deleting a Relationship Between Entities</span></span>

<span data-ttu-id="fe727-171">관계를 삭제 하기 위해 클라이언트는 $ref URI에 HTTP DELETE 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-171">To delete a relationship, the client sends an HTTP DELETE request to the $ref URI:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample18.cmd)]

<span data-ttu-id="fe727-172">제품 및 공급자 간의 관계를 삭제 하는 컨트롤러 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-172">Here is the controller method to delete the relationship between a Product and a Supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample19.cs)]

<span data-ttu-id="fe727-173">이 경우 `Product.Supplier`는 일 대 다 관계의 &quot;1&quot; 끝 이므로 `Product.Supplier`를 `null`로 설정 하기만 하면 관계를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-173">In this case, `Product.Supplier` is the &quot;1&quot; end of a 1-to-many relation, so you can remove the relationship just by setting `Product.Supplier` to `null`.</span></span>

<span data-ttu-id="fe727-174">관계의 여러&quot; 끝 &quot;에서 클라이언트는 제거할 관련 엔터티를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-174">In the &quot;many&quot; end of a relationship, the client must specify which related entity to remove.</span></span> <span data-ttu-id="fe727-175">이렇게 하기 위해 클라이언트는 요청의 쿼리 문자열에 관련 엔터티의 URI를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-175">To do so, the client sends the URI of the related entity in the query string of the request.</span></span> <span data-ttu-id="fe727-176">예를 들어 "공급 업체 1"에서 "제품 1"을 제거 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-176">For example, to remove "Product 1" from "Supplier 1":</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample20.cmd?highlight=1)]

<span data-ttu-id="fe727-177">Web API에서이를 지원 하려면 `DeleteRef` 메서드에 추가 매개 변수를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-177">To support this in Web API, we need to include an extra parameter in the `DeleteRef` method.</span></span> <span data-ttu-id="fe727-178">`Supplier.Products` 관계에서 제품을 제거 하는 컨트롤러 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-178">Here is the controller method to remove a product from the `Supplier.Products` relation.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample21.cs)]

<span data-ttu-id="fe727-179">*키* 매개 변수는 공급자에 대 한 키이 고 *relatedKey* 매개 변수는 `Products` 관계에서 제거할 제품의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-179">The *key* parameter is the key for the supplier, and the *relatedKey* parameter is the key for the product to remove from the `Products` relationship.</span></span> <span data-ttu-id="fe727-180">Web API는 쿼리 문자열에서 키를 자동으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fe727-180">Note that Web API automatically gets the key from the query string.</span></span>
