---
uid: web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
title: ASP.NET Web API 2-ASP.NET 4.x의 OData 쿼리 옵션 지원
author: MikeWasson
description: 코드 예제를 사용 하는 개요에서는 ASP.NET 4.x의 ASP.NET Web API 2에서 지 원하는 OData 쿼리 옵션을 보여 줍니다.
ms.author: riande
ms.date: 02/04/2013
ms.custom: seoapril2019
ms.assetid: 50e6e62b-e72e-4a29-8293-4b67377bd21f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
msc.type: authoredcontent
ms.openlocfilehash: 96820fab7ac89885058962f44ded86cb0184ee97
ms.sourcegitcommit: 4ed0b65ae32d9f35e42ee6296b877747e063df4d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "86188633"
---
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a><span data-ttu-id="19562-103">ASP.NET Web API 2에서 OData 쿼리 옵션 지원</span><span class="sxs-lookup"><span data-stu-id="19562-103">Supporting OData Query Options in ASP.NET Web API 2</span></span>

<span data-ttu-id="19562-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="19562-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="19562-105">이 개요 코드 예제에서는 ASP.NET 4. x의 ASP.NET Web API 2에서 지 원하는 OData 쿼리 옵션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="19562-105">This overview with code examples demonstrates the supporting OData Query Options in ASP.NET Web API 2 for ASP.NET 4.x.</span></span> 

<span data-ttu-id="19562-106">OData는 OData 쿼리를 수정 하는 데 사용할 수 있는 매개 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-106">OData defines parameters that can be used to modify an OData query.</span></span> <span data-ttu-id="19562-107">클라이언트는 요청 URI의 쿼리 문자열에서 이러한 매개 변수를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="19562-107">The client sends these parameters in the query string of the request URI.</span></span> <span data-ttu-id="19562-108">예를 들어 결과를 정렬 하기 위해 클라이언트는 $orderby 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-108">For example, to sort the results, a client uses the $orderby parameter:</span></span>

`http://localhost/Products?$orderby=Name`

<span data-ttu-id="19562-109">OData 사양에서는 이러한 매개 변수 *쿼리 옵션*을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-109">The OData specification calls these parameters *query options*.</span></span> <span data-ttu-id="19562-110">컨트롤러가 OData 끝점이 될 필요 없이 프로젝트의 웹 API 컨트롤러에 대해 OData 쿼리 옵션을 사용 하도록 설정할 수 &#8212;.</span><span class="sxs-lookup"><span data-stu-id="19562-110">You can enable OData query options for any Web API controller in your project &#8212; the controller does not need to be an OData endpoint.</span></span> <span data-ttu-id="19562-111">이렇게 하면 웹 API 응용 프로그램에 대 한 필터링 및 정렬과 같은 기능을 편리 하 게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-111">This gives you a convenient way to add features such as filtering and sorting to any Web API application.</span></span>

<span data-ttu-id="19562-112">쿼리 옵션을 사용 하도록 설정 하기 전에 [OData 보안 지침](odata-security-guidance.md)항목을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="19562-112">Before enabling query options, please read the topic [OData Security Guidance](odata-security-guidance.md).</span></span>

- [<span data-ttu-id="19562-113">OData 쿼리 옵션 사용</span><span class="sxs-lookup"><span data-stu-id="19562-113">Enabling OData Query Options</span></span>](#enable)
- [<span data-ttu-id="19562-114">예제 쿼리</span><span class="sxs-lookup"><span data-stu-id="19562-114">Example Queries</span></span>](#examples)
- [<span data-ttu-id="19562-115">서버 기반 페이징</span><span class="sxs-lookup"><span data-stu-id="19562-115">Server-Driven Paging</span></span>](#server-paging)
- [<span data-ttu-id="19562-116">쿼리 옵션 제한</span><span class="sxs-lookup"><span data-stu-id="19562-116">Limiting the Query Options</span></span>](#limiting_query_options)
- [<span data-ttu-id="19562-117">직접 쿼리 옵션 호출</span><span class="sxs-lookup"><span data-stu-id="19562-117">Invoking Query Options Directly</span></span>](#ODataQueryOptions)
- [<span data-ttu-id="19562-118">쿼리 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="19562-118">Query Validation</span></span>](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a><span data-ttu-id="19562-119">OData 쿼리 옵션 사용</span><span class="sxs-lookup"><span data-stu-id="19562-119">Enabling OData Query Options</span></span>

<span data-ttu-id="19562-120">Web API는 다음과 같은 OData 쿼리 옵션을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-120">Web API supports the following OData query options:</span></span>

| <span data-ttu-id="19562-121">옵션</span><span class="sxs-lookup"><span data-stu-id="19562-121">Option</span></span> | <span data-ttu-id="19562-122">설명</span><span class="sxs-lookup"><span data-stu-id="19562-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="19562-123">$expand</span><span class="sxs-lookup"><span data-stu-id="19562-123">$expand</span></span> | <span data-ttu-id="19562-124">관련 엔터티를 인라인으로 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-124">Expands related entities inline.</span></span> |
| <span data-ttu-id="19562-125">$filter</span><span class="sxs-lookup"><span data-stu-id="19562-125">$filter</span></span> | <span data-ttu-id="19562-126">부울 조건에 따라 결과를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-126">Filters the results, based on a Boolean condition.</span></span> |
| <span data-ttu-id="19562-127">$inlinecount</span><span class="sxs-lookup"><span data-stu-id="19562-127">$inlinecount</span></span> | <span data-ttu-id="19562-128">응답에 일치 하는 엔터티의 총 개수를 포함 하도록 서버에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-128">Tells the server to include the total count of matching entities in the response.</span></span> <span data-ttu-id="19562-129">서버 쪽 페이징에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-129">(Useful for server-side paging.)</span></span> |
| <span data-ttu-id="19562-130">$orderby</span><span class="sxs-lookup"><span data-stu-id="19562-130">$orderby</span></span> | <span data-ttu-id="19562-131">결과를 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-131">Sorts the results.</span></span> |
| <span data-ttu-id="19562-132">$select</span><span class="sxs-lookup"><span data-stu-id="19562-132">$select</span></span> | <span data-ttu-id="19562-133">응답에 포함할 속성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-133">Selects which properties to include in the response.</span></span> |
| <span data-ttu-id="19562-134">$skip</span><span class="sxs-lookup"><span data-stu-id="19562-134">$skip</span></span> | <span data-ttu-id="19562-135">처음 n 개 결과를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="19562-135">Skips the first n results.</span></span> |
| <span data-ttu-id="19562-136">$top</span><span class="sxs-lookup"><span data-stu-id="19562-136">$top</span></span> | <span data-ttu-id="19562-137">결과의 첫 번째 n 개만 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-137">Returns only the first n the results.</span></span> |

<span data-ttu-id="19562-138">OData 쿼리 옵션을 사용 하려면 명시적으로 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-138">To use OData query options, you must enable them explicitly.</span></span> <span data-ttu-id="19562-139">전체 응용 프로그램에 대해 전역적으로 사용 하도록 설정 하거나 특정 컨트롤러 또는 특정 작업에 대해 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-139">You can enable them globally for the entire application, or enable them for specific controllers or specific actions.</span></span>

<span data-ttu-id="19562-140">OData 쿼리 옵션을 전역적으로 설정 하려면 시작 시 **Httpconfiguration** 클래스에서 **enablequerysupport** 를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-140">To enable OData query options globally, call **EnableQuerySupport** on the **HttpConfiguration** class at startup:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

<span data-ttu-id="19562-141">**Enablequerysupport** 메서드는 **IQueryable** 형식을 반환 하는 모든 컨트롤러 작업에 대해 전역적으로 쿼리 옵션을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-141">The **EnableQuerySupport** method enables query options globally for any controller action that returns an **IQueryable** type.</span></span> <span data-ttu-id="19562-142">전체 응용 프로그램에 대해 쿼리 옵션을 사용 하지 않으려면 [쿼리 가능 **]** 특성을 동작 메서드에 추가 하 여 특정 컨트롤러 작업에 대해 쿼리 옵션을 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-142">If you don't want query options enabled for the entire application, you can enable them for specific controller actions by adding the **[Queryable]** attribute to the action method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a><span data-ttu-id="19562-143">예제 쿼리</span><span class="sxs-lookup"><span data-stu-id="19562-143">Example Queries</span></span>

<span data-ttu-id="19562-144">이 섹션에서는 OData 쿼리 옵션을 사용 하 여 가능한 쿼리 유형을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="19562-144">This section shows the types of queries that are possible using the OData query options.</span></span> <span data-ttu-id="19562-145">쿼리 옵션에 대 한 자세한 내용은 [www.odata.org](http://www.odata.org/)의 OData 설명서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="19562-145">For specific details about the query options, refer to the OData documentation at [www.odata.org](http://www.odata.org/).</span></span>

<span data-ttu-id="19562-146">$Expand 및 $select에 대 한 자세한 내용은 [$Value OData에서 $select, $expand 및 ASP.NET Web API 사용](using-select-expand-and-value.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="19562-146">For information about $expand and $select, see [Using $select, $expand, and $value in ASP.NET Web API OData](using-select-expand-and-value.md).</span></span>

<span data-ttu-id="19562-147">**클라이언트 구동 페이징**</span><span class="sxs-lookup"><span data-stu-id="19562-147">**Client-Driven Paging**</span></span>

<span data-ttu-id="19562-148">대량 엔터티 집합의 경우 클라이언트에서 결과 수를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-148">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="19562-149">예를 들어 클라이언트는 다음 결과 페이지를 가져오기 위해 "다음" 링크를 포함 하 여 한 번에 10 개의 항목을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-149">For example, a client might show 10 entries at a time, with "next" links to get the next page of results.</span></span> <span data-ttu-id="19562-150">이를 위해 클라이언트는 $top 및 $skip 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-150">To do this, the client uses the $top and $skip options.</span></span>

`http://localhost/Products?$top=10&$skip=20`

<span data-ttu-id="19562-151">$Top 옵션은 반환할 항목의 최대 수를 제공 하 고, $skip 옵션은 건너뛸 항목 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-151">The $top option gives the maximum number of entries to return, and the $skip option gives the number of entries to skip.</span></span> <span data-ttu-id="19562-152">이전 예제에서는 21 ~ 30 개 항목을 인출 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-152">The previous example fetches entries 21 through 30.</span></span>

<span data-ttu-id="19562-153">**필터링**</span><span class="sxs-lookup"><span data-stu-id="19562-153">**Filtering**</span></span>

<span data-ttu-id="19562-154">$Filter 옵션을 사용 하면 클라이언트에서 부울 식을 적용 하 여 결과를 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-154">The $filter option lets a client filter the results by applying a Boolean expression.</span></span> <span data-ttu-id="19562-155">필터 식은 매우 강력 합니다. 여기에는 논리 및 산술 연산자, 문자열 함수 및 날짜 함수가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19562-155">The filter expressions are quite powerful; they include logical and arithmetic operators, string functions, and date functions.</span></span>

| <span data-ttu-id="19562-156">범주가 "장난감"과 같은 모든 제품을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-156">Return all products with category equal to "Toys".</span></span> | <span data-ttu-id="19562-157">`http://localhost/Products?$filter=Category` eq ' 장난감 '</span><span class="sxs-lookup"><span data-stu-id="19562-157">`http://localhost/Products?$filter=Category` eq 'Toys'</span></span> |
| --- | --- |
| <span data-ttu-id="19562-158">가격이 10 보다 작은 모든 제품을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-158">Return all products with price less than 10.</span></span> | <span data-ttu-id="19562-159">`http://localhost/Products?$filter=Price` lt 10</span><span class="sxs-lookup"><span data-stu-id="19562-159">`http://localhost/Products?$filter=Price` lt 10</span></span> |
| <span data-ttu-id="19562-160">논리 연산자: price >= 5 및 price <= 15 인 모든 제품을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-160">Logical operators: Return all products where price >= 5 and price <= 15.</span></span> | <span data-ttu-id="19562-161">`http://localhost/Products?$filter=Price` ge 5 및 Price le 15</span><span class="sxs-lookup"><span data-stu-id="19562-161">`http://localhost/Products?$filter=Price` ge 5 and Price le 15</span></span> |
| <span data-ttu-id="19562-162">문자열 함수: 이름에 "zz"가 있는 모든 제품을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-162">String functions: Return all products with "zz" in the name.</span></span> | `http://localhost/Products?$filter=substringof('zz',Name)` |
| <span data-ttu-id="19562-163">날짜 함수: 2005 이후의 ReleaseDate를 사용 하는 모든 제품을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-163">Date functions: Return all products with ReleaseDate after 2005.</span></span> | <span data-ttu-id="19562-164">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span><span class="sxs-lookup"><span data-stu-id="19562-164">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span></span> |

<span data-ttu-id="19562-165">**정렬**</span><span class="sxs-lookup"><span data-stu-id="19562-165">**Sorting**</span></span>

<span data-ttu-id="19562-166">결과를 정렬 하려면 $orderby 필터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-166">To sort the results, use the $orderby filter.</span></span>

| <span data-ttu-id="19562-167">가격을 기준으로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-167">Sort by price.</span></span> | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| <span data-ttu-id="19562-168">가격을 기준으로 내림차순으로 정렬 합니다 (최고부터 낮음).</span><span class="sxs-lookup"><span data-stu-id="19562-168">Sort by price in descending order (highest to lowest).</span></span> | `http://localhost/Products?$orderby=Price desc` |
| <span data-ttu-id="19562-169">범주별로 정렬 한 다음, 범주 내에서 내림차순으로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-169">Sort by category, then sort by price in descending order within categories.</span></span> | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a><span data-ttu-id="19562-170">서버 기반 페이징</span><span class="sxs-lookup"><span data-stu-id="19562-170">Server-Driven Paging</span></span>

<span data-ttu-id="19562-171">데이터베이스에 수백만 개의 레코드가 포함 되어 있는 경우 한 페이로드에 모두 전송 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-171">If your database contains millions of records, you don't want to send them all in one payload.</span></span> <span data-ttu-id="19562-172">이를 방지 하기 위해 서버는 단일 응답으로 전송 되는 항목 수를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-172">To prevent this, the server can limit the number of entries that it sends in a single response.</span></span> <span data-ttu-id="19562-173">서버 페이징을 사용 하도록 설정 하려면 **쿼리** 가능한 특성의 **PageSize** 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-173">To enable server paging, set the **PageSize** property in the **Queryable** attribute.</span></span> <span data-ttu-id="19562-174">값은 반환할 최대 항목 수입니다.</span><span class="sxs-lookup"><span data-stu-id="19562-174">The value is the maximum number of entries to return.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

<span data-ttu-id="19562-175">컨트롤러가 OData 형식을 반환 하는 경우 응답 본문에는 다음 데이터 페이지에 대 한 링크가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19562-175">If your controller returns OData format, the response body will contain a link to the next page of data:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

<span data-ttu-id="19562-176">클라이언트는이 링크를 사용 하 여 다음 페이지를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-176">The client can use this link to fetch the next page.</span></span> <span data-ttu-id="19562-177">클라이언트는 결과 집합에 있는 총 항목 수를 확인 하기 위해 "allpages" 값을 사용 하 여 $inlinecount 쿼리 옵션을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-177">To learn the total number of entries in the result set, the client can set the $inlinecount query option with the value "allpages".</span></span>

`http://localhost/Products?$inlinecount=allpages`

<span data-ttu-id="19562-178">"Allpages" 값은 응답의 총 개수를 포함 하도록 서버에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-178">The value "allpages" tells the server to include the total count in the response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> <span data-ttu-id="19562-179">다음-페이지 링크 및 인라인 개수에는 모두 OData 형식이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-179">Next-page links and inline count both require OData format.</span></span> <span data-ttu-id="19562-180">그 이유는 OData에서 링크 및 개수를 유지 하기 위해 응답 본문에 특수 필드를 정의 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="19562-180">The reason is that OData defines special fields in the response body to hold the link and count.</span></span>

<span data-ttu-id="19562-181">OData 형식이 아닌 경우 \*\*PageResult &lt; T &gt; \*\* 개체에 쿼리 결과를 래핑하여 다음 페이지 링크 및 인라인 개수를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-181">For non-OData formats, it is still possible to support next-page links and inline count, by wrapping the query results in a **PageResult&lt;T&gt;** object.</span></span> <span data-ttu-id="19562-182">그러나 좀 더 많은 코드가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-182">However, it requires a bit more code.</span></span> <span data-ttu-id="19562-183">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="19562-183">Here is an example:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

<span data-ttu-id="19562-184">다음은 JSON 응답 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="19562-184">Here is an example JSON response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a><span data-ttu-id="19562-185">쿼리 옵션 제한</span><span class="sxs-lookup"><span data-stu-id="19562-185">Limiting the Query Options</span></span>

<span data-ttu-id="19562-186">쿼리 옵션을 통해 클라이언트는 서버에서 실행 되는 쿼리에 대해 많은 제어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-186">The query options give the client a lot of control over the query that is run on the server.</span></span> <span data-ttu-id="19562-187">경우에 따라 보안 또는 성능상의 이유로 사용 가능한 옵션을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-187">In some cases, you might want to limit the available options for security or performance reasons.</span></span> <span data-ttu-id="19562-188">**[쿼리 가능]** 특성에는이에 대 한 몇 가지 기본 제공 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-188">The **[Queryable]** attribute has some built in properties for this.</span></span> <span data-ttu-id="19562-189">다음은 몇 가지 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="19562-189">Here are some examples.</span></span>

<span data-ttu-id="19562-190">$Skip 및 $top만 허용 하 여 페이징을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-190">Allow only $skip and $top, to support paging and nothing else:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

<span data-ttu-id="19562-191">데이터베이스에서 인덱싱되지 않은 속성의 정렬을 방지 하기 위해 특정 속성 으로만 순서를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-191">Allow ordering only by certain properties, to prevent sorting on properties that are not indexed in the database:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

<span data-ttu-id="19562-192">"Eq" 논리 함수를 허용 하지만 다른 논리 함수는 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-192">Allow the "eq" logical function but no other logical functions:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

<span data-ttu-id="19562-193">산술 연산자를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-193">Do not allow any arithmetic operators:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

<span data-ttu-id="19562-194">**QueryableAttribute** 인스턴스를 생성 하 여 **enablequerysupport** 함수에 전달 하 여 전역으로 옵션을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-194">You can restrict options globally by constructing a **QueryableAttribute** instance and passing it to the **EnableQuerySupport** function:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a><span data-ttu-id="19562-195">직접 쿼리 옵션 호출</span><span class="sxs-lookup"><span data-stu-id="19562-195">Invoking Query Options Directly</span></span>

<span data-ttu-id="19562-196">**[쿼리할** 수 있는] 특성을 사용 하는 대신 컨트롤러에서 직접 쿼리 옵션을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-196">Instead of using the **[Queryable]** attribute, you can invoke the query options directly in your controller.</span></span> <span data-ttu-id="19562-197">이렇게 하려면 **ODataQueryOptions** 매개 변수를 컨트롤러 메서드에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-197">To do so, add an **ODataQueryOptions** parameter to the controller method.</span></span> <span data-ttu-id="19562-198">이 경우 **[쿼리 가능]** 특성이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-198">In this case, you don't need the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

<span data-ttu-id="19562-199">Web API는 URI 쿼리 문자열에서 **ODataQueryOptions** 를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="19562-199">Web API populates the **ODataQueryOptions** from the URI query string.</span></span> <span data-ttu-id="19562-200">쿼리를 적용 하려면 **IQueryable** 을 **applyto** 메서드에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-200">To apply the query, pass an **IQueryable** to the **ApplyTo** method.</span></span> <span data-ttu-id="19562-201">메서드는 다른 **IQueryable**을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-201">The method returns another **IQueryable**.</span></span>

<span data-ttu-id="19562-202">고급 시나리오의 경우 **IQueryable** 쿼리 공급자가 없으면 **ODataQueryOptions** 을 검토 하 고 쿼리 옵션을 다른 형식으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-202">For advanced scenarios, if you do not have an **IQueryable** query provider, you can examine the **ODataQueryOptions** and translate the query options into another form.</span></span> <span data-ttu-id="19562-203">(예를 들어 RaghuRam Nadiminti의 블로그 게시물 [OData 쿼리를 HQL로 변환](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx)( [샘플](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt)도 포함)을 참조 하세요.)</span><span class="sxs-lookup"><span data-stu-id="19562-203">(For example, see RaghuRam Nadiminti's blog post [Translating OData queries to HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), which also includes a [sample](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span></span>

<a id="query-validation"></a>
## <a name="query-validation"></a><span data-ttu-id="19562-204">쿼리 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="19562-204">Query Validation</span></span>

<span data-ttu-id="19562-205">[쿼리 가능 **]** 특성은 쿼리를 실행 하기 전에 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-205">The **[Queryable]** attribute validates the query before executing it.</span></span> <span data-ttu-id="19562-206">유효성 검사 단계는 **QueryableAttribute 쿼리** 메서드에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19562-206">The validation step is performed in the **QueryableAttribute.ValidateQuery** method.</span></span> <span data-ttu-id="19562-207">유효성 검사 프로세스를 사용자 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19562-207">You can also customize the validation process.</span></span>

<span data-ttu-id="19562-208">또한 [OData 보안 지침](odata-security-guidance.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="19562-208">Also see [OData Security Guidance](odata-security-guidance.md).</span></span>

<span data-ttu-id="19562-209">먼저, **web.config** 에 정의 된 유효성 검사기 클래스 중 하나를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-209">First, override one of the validator classes that is defined in the **Web.Http.OData.Query.Validators** namespace.</span></span> <span data-ttu-id="19562-210">예를 들어 다음 유효성 검사기 클래스는 $orderby 옵션에 대 한 ' desc ' 옵션을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-210">For example, the following validator class disables the 'desc' option for the $orderby option.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

<span data-ttu-id="19562-211">**Validatequery** 메서드를 재정의 하는 **[쿼리할** 수 있는] 특성의 서브 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="19562-211">Subclass the **[Queryable]** attribute to override the **ValidateQuery** method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

<span data-ttu-id="19562-212">그런 다음 사용자 지정 특성을 전역으로 설정 하거나 controller 별로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-212">Then set your custom attribute either globally or per-controller:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

<span data-ttu-id="19562-213">**ODataQueryOptions** 를 직접 사용 하는 경우 옵션에서 유효성 검사기를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="19562-213">If you are using **ODataQueryOptions** directly, set the validator on the options:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
