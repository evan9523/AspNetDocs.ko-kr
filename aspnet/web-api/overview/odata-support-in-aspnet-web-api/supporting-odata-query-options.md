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
ms.lasthandoff: 10/06/2020
ms.locfileid: "86188633"
---
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a>ASP.NET Web API 2에서 OData 쿼리 옵션 지원

[Mike Wasson](https://github.com/MikeWasson)

이 개요 코드 예제에서는 ASP.NET 4. x의 ASP.NET Web API 2에서 지 원하는 OData 쿼리 옵션을 보여 줍니다. 

OData는 OData 쿼리를 수정 하는 데 사용할 수 있는 매개 변수를 정의 합니다. 클라이언트는 요청 URI의 쿼리 문자열에서 이러한 매개 변수를 보냅니다. 예를 들어 결과를 정렬 하기 위해 클라이언트는 $orderby 매개 변수를 사용 합니다.

`http://localhost/Products?$orderby=Name`

OData 사양에서는 이러한 매개 변수 *쿼리 옵션*을 호출 합니다. 컨트롤러가 OData 끝점이 될 필요 없이 프로젝트의 웹 API 컨트롤러에 대해 OData 쿼리 옵션을 사용 하도록 설정할 수 &#8212;. 이렇게 하면 웹 API 응용 프로그램에 대 한 필터링 및 정렬과 같은 기능을 편리 하 게 추가할 수 있습니다.

쿼리 옵션을 사용 하도록 설정 하기 전에 [OData 보안 지침](odata-security-guidance.md)항목을 참조 하세요.

- [OData 쿼리 옵션 사용](#enable)
- [예제 쿼리](#examples)
- [서버 기반 페이징](#server-paging)
- [쿼리 옵션 제한](#limiting_query_options)
- [직접 쿼리 옵션 호출](#ODataQueryOptions)
- [쿼리 유효성 검사](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a>OData 쿼리 옵션 사용

Web API는 다음과 같은 OData 쿼리 옵션을 지원 합니다.

| 옵션 | Description |
| --- | --- |
| $expand | 관련 엔터티를 인라인으로 확장 합니다. |
| $filter | 부울 조건에 따라 결과를 필터링 합니다. |
| $inlinecount | 응답에 일치 하는 엔터티의 총 개수를 포함 하도록 서버에 지시 합니다. 서버 쪽 페이징에 유용 합니다. |
| $orderby | 결과를 정렬 합니다. |
| $select | 응답에 포함할 속성을 선택 합니다. |
| $skip | 처음 n 개 결과를 건너뜁니다. |
| $top | 결과의 첫 번째 n 개만 반환 합니다. |

OData 쿼리 옵션을 사용 하려면 명시적으로 사용 하도록 설정 해야 합니다. 전체 응용 프로그램에 대해 전역적으로 사용 하도록 설정 하거나 특정 컨트롤러 또는 특정 작업에 대해 사용 하도록 설정할 수 있습니다.

OData 쿼리 옵션을 전역적으로 설정 하려면 시작 시 **Httpconfiguration** 클래스에서 **enablequerysupport** 를 호출 합니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

**Enablequerysupport** 메서드는 **IQueryable** 형식을 반환 하는 모든 컨트롤러 작업에 대해 전역적으로 쿼리 옵션을 사용 하도록 설정 합니다. 전체 응용 프로그램에 대해 쿼리 옵션을 사용 하지 않으려면 [쿼리 가능 **]** 특성을 동작 메서드에 추가 하 여 특정 컨트롤러 작업에 대해 쿼리 옵션을 사용 하도록 설정할 수 있습니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a>예제 쿼리

이 섹션에서는 OData 쿼리 옵션을 사용 하 여 가능한 쿼리 유형을 보여 줍니다. 쿼리 옵션에 대 한 자세한 내용은 [www.odata.org](http://www.odata.org/)의 OData 설명서를 참조 하세요.

$Expand 및 $select에 대 한 자세한 내용은 [$Value OData에서 $select, $expand 및 ASP.NET Web API 사용](using-select-expand-and-value.md)을 참조 하세요.

**클라이언트 구동 페이징**

대량 엔터티 집합의 경우 클라이언트에서 결과 수를 제한할 수 있습니다. 예를 들어 클라이언트는 다음 결과 페이지를 가져오기 위해 "다음" 링크를 포함 하 여 한 번에 10 개의 항목을 표시할 수 있습니다. 이를 위해 클라이언트는 $top 및 $skip 옵션을 사용 합니다.

`http://localhost/Products?$top=10&$skip=20`

$Top 옵션은 반환할 항목의 최대 수를 제공 하 고, $skip 옵션은 건너뛸 항목 수를 제공 합니다. 이전 예제에서는 21 ~ 30 개 항목을 인출 합니다.

**필터링**

$Filter 옵션을 사용 하면 클라이언트에서 부울 식을 적용 하 여 결과를 필터링 할 수 있습니다. 필터 식은 매우 강력 합니다. 여기에는 논리 및 산술 연산자, 문자열 함수 및 날짜 함수가 포함 됩니다.

| 범주가 "장난감"과 같은 모든 제품을 반환 합니다. | `http://localhost/Products?$filter=Category` eq ' 장난감 ' |
| --- | --- |
| 가격이 10 보다 작은 모든 제품을 반환 합니다. | `http://localhost/Products?$filter=Price` lt 10 |
| 논리 연산자: price >= 5 및 price <= 15 인 모든 제품을 반환 합니다. | `http://localhost/Products?$filter=Price` ge 5 및 Price le 15 |
| 문자열 함수: 이름에 "zz"가 있는 모든 제품을 반환 합니다. | `http://localhost/Products?$filter=substringof('zz',Name)` |
| 날짜 함수: 2005 이후의 ReleaseDate를 사용 하는 모든 제품을 반환 합니다. | `http://localhost/Products?$filter=year(ReleaseDate)` gt 2005 |

**정렬**

결과를 정렬 하려면 $orderby 필터를 사용 합니다.

| 가격을 기준으로 정렬 합니다. | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| 가격을 기준으로 내림차순으로 정렬 합니다 (최고부터 낮음). | `http://localhost/Products?$orderby=Price desc` |
| 범주별로 정렬 한 다음, 범주 내에서 내림차순으로 정렬 합니다. | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a>서버 기반 페이징

데이터베이스에 수백만 개의 레코드가 포함 되어 있는 경우 한 페이로드에 모두 전송 하지는 않습니다. 이를 방지 하기 위해 서버는 단일 응답으로 전송 되는 항목 수를 제한할 수 있습니다. 서버 페이징을 사용 하도록 설정 하려면 **쿼리** 가능한 특성의 **PageSize** 속성을 설정 합니다. 값은 반환할 최대 항목 수입니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

컨트롤러가 OData 형식을 반환 하는 경우 응답 본문에는 다음 데이터 페이지에 대 한 링크가 포함 됩니다.

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

클라이언트는이 링크를 사용 하 여 다음 페이지를 가져올 수 있습니다. 클라이언트는 결과 집합에 있는 총 항목 수를 확인 하기 위해 "allpages" 값을 사용 하 여 $inlinecount 쿼리 옵션을 설정할 수 있습니다.

`http://localhost/Products?$inlinecount=allpages`

"Allpages" 값은 응답의 총 개수를 포함 하도록 서버에 지시 합니다.

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> 다음-페이지 링크 및 인라인 개수에는 모두 OData 형식이 필요 합니다. 그 이유는 OData에서 링크 및 개수를 유지 하기 위해 응답 본문에 특수 필드를 정의 하기 때문입니다.

OData 형식이 아닌 경우 **PageResult &lt; T &gt; ** 개체에 쿼리 결과를 래핑하여 다음 페이지 링크 및 인라인 개수를 지원할 수 있습니다. 그러나 좀 더 많은 코드가 필요 합니다. 다음은 예제입니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

다음은 JSON 응답 예제입니다.

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a>쿼리 옵션 제한

쿼리 옵션을 통해 클라이언트는 서버에서 실행 되는 쿼리에 대해 많은 제어를 제공 합니다. 경우에 따라 보안 또는 성능상의 이유로 사용 가능한 옵션을 제한할 수 있습니다. **[쿼리 가능]** 특성에는이에 대 한 몇 가지 기본 제공 속성이 있습니다. 다음은 몇 가지 예제입니다.

$Skip 및 $top만 허용 하 여 페이징을 지원 합니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

데이터베이스에서 인덱싱되지 않은 속성의 정렬을 방지 하기 위해 특정 속성 으로만 순서를 지정할 수 있습니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

"Eq" 논리 함수를 허용 하지만 다른 논리 함수는 허용 하지 않습니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

산술 연산자를 허용 하지 않습니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

**QueryableAttribute** 인스턴스를 생성 하 여 **enablequerysupport** 함수에 전달 하 여 전역으로 옵션을 제한할 수 있습니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a>직접 쿼리 옵션 호출

**[쿼리할** 수 있는] 특성을 사용 하는 대신 컨트롤러에서 직접 쿼리 옵션을 호출할 수 있습니다. 이렇게 하려면 **ODataQueryOptions** 매개 변수를 컨트롤러 메서드에 추가 합니다. 이 경우 **[쿼리 가능]** 특성이 필요 하지 않습니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

Web API는 URI 쿼리 문자열에서 **ODataQueryOptions** 를 채웁니다. 쿼리를 적용 하려면 **IQueryable** 을 **applyto** 메서드에 전달 합니다. 메서드는 다른 **IQueryable**을 반환 합니다.

고급 시나리오의 경우 **IQueryable** 쿼리 공급자가 없으면 **ODataQueryOptions** 을 검토 하 고 쿼리 옵션을 다른 형식으로 변환할 수 있습니다. (예를 들어 RaghuRam Nadiminti의 블로그 게시물 [OData 쿼리를 HQL로 변환](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx)( [샘플](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt)도 포함)을 참조 하세요.)

<a id="query-validation"></a>
## <a name="query-validation"></a>쿼리 유효성 검사

[쿼리 가능 **]** 특성은 쿼리를 실행 하기 전에 유효성을 검사 합니다. 유효성 검사 단계는 **QueryableAttribute 쿼리** 메서드에서 수행 됩니다. 유효성 검사 프로세스를 사용자 지정할 수도 있습니다.

또한 [OData 보안 지침](odata-security-guidance.md)을 참조 하세요.

먼저, **web.config** 에 정의 된 유효성 검사기 클래스 중 하나를 재정의 합니다. 예를 들어 다음 유효성 검사기 클래스는 $orderby 옵션에 대 한 ' desc ' 옵션을 사용 하지 않도록 설정 합니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

**Validatequery** 메서드를 재정의 하는 **[쿼리할** 수 있는] 특성의 서브 클래스입니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

그런 다음 사용자 지정 특성을 전역으로 설정 하거나 controller 별로 설정 합니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

**ODataQueryOptions** 를 직접 사용 하는 경우 옵션에서 유효성 검사기를 설정 합니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
