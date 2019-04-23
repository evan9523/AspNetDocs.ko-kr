---
uid: web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
title: ASP.NET Web API 2-ASP.NET에서에서 OData 쿼리 옵션을 지 원하는 4.x
author: MikeWasson
description: 코드 예제를 사용 하 여 개요 ASP.NET에 대 한 ASP.NET Web API 2에서 지 원하는 OData 쿼리 옵션을 표시 4.x 합니다.
ms.author: riande
ms.date: 02/04/2013
ms.custom: seoapril2019
ms.assetid: 50e6e62b-e72e-4a29-8293-4b67377bd21f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
msc.type: authoredcontent
ms.openlocfilehash: 428e4942e42436585049c1e84cd7b07a4a79c0d1
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59411568"
---
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a>ASP.NET Web API 2에서에서 OData 쿼리 옵션 지원

[Mike Wasson](https://github.com/MikeWasson)

코드 예제를 사용 하 여이 개요에서는 ASP.NET에 대 한 ASP.NET Web API 2에서 지원 되는 OData 쿼리 옵션을 보여 줍니다. 4.x 합니다. 

OData는 OData 쿼리를 수정 하는 매개 변수를 정의 합니다. 클라이언트는 요청 URI의 쿼리 문자열에서 이러한 매개 변수를 보냅니다. 예를 들어, 클라이언트가 결과 정렬 하려면 $orderby 매개 변수를 사용 합니다.

`http://localhost/Products?$orderby=Name`

이러한 매개 변수를 호출 하는 OData 사양 *쿼리 옵션*합니다. 프로젝트에서 모든 Web API 컨트롤러에 대 한 OData 쿼리 옵션을 설정할 수 있습니다. &#8212; 컨트롤러는 OData 끝점일 필요가 없습니다. 이 모든 Web API 응용 프로그램에 필터링 및 정렬을 등 기능을 추가 하는 편리한 방법을 제공 합니다.

항목을 쿼리 옵션을 사용 하도록 설정 하기 전에 [OData 보안 지침](odata-security-guidance.md)합니다.

- [OData 쿼리 옵션을 사용 하도록 설정](#enable)
- [예제 쿼리](#examples)
- [서버 기반 페이징](#server-paging)
- [쿼리 옵션을 제한합니다.](#limiting_query_options)
- [쿼리 옵션을 직접 호출](#ODataQueryOptions)
- [쿼리 유효성 검사](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a>OData 쿼리 옵션을 사용 하도록 설정

웹 API는 OData 쿼리 옵션을 지원합니다.

| 옵션 | 설명 |
| --- | --- |
| $expand | 관련된 엔터티 인라인을 확장합니다. |
| $filter | 부울 조건에 따라 결과 필터링 합니다. |
| $inlinecount | 응답에 일치 하는 항목의 총 수를 포함 하도록 서버를 알려 줍니다. (서버 쪽 페이징에 유용 합니다.) |
| $orderby | 결과 정렬합니다. |
| $select | 응답에 포함할 속성을 선택 합니다. |
| $skip | 처음 n 개 결과 건너뜁니다. |
| $top | 첫 번째 n만 결과 반환합니다. |

OData 쿼리 옵션을 사용 하려면 활성화 해야 합니다을 명시적으로 합니다. 전체 응용 프로그램에 대 한 전역적으로 있도록 수도 있고 특정 컨트롤러 또는 특정 작업에 대해 사용 하도록 설정 수 있습니다.

OData 쿼리 옵션을 전체적으로 설정 하려면 호출 **EnableQuerySupport** 에 **HttpConfiguration** 시작 시 클래스:

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

**EnableQuerySupport** 메서드를 사용 하면 반환 하는 모든 컨트롤러 작업에 대 한 전역적으로 쿼리 옵션을 **IQueryable** 형식입니다. 전체 응용 프로그램에 대해 사용 하도록 설정 하는 쿼리 옵션을 사용 하지 않으려는 경우 하도록 할 수 있습니다 특정 컨트롤러 작업에 대 한 추가 하 여 합니다 **[Queryable]** 작업 메서드에 특성입니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a>예제 쿼리

이 섹션에서는 OData 쿼리 옵션을 사용 하 여 가능한 쿼리 유형을 보여 줍니다. 쿼리 옵션에 대 한 특정 내용은 OData 설명서에서 참조 [www.odata.org](http://www.odata.org/)합니다.

$에 대 한 정보에 대 한 확장 및 $select을 참조 하세요 [$expand $select 사용 및 ASP.NET Web API OData의 $value](using-select-expand-and-value.md)합니다.

**클라이언트 기반 페이징**

큰 엔터티 집합에 대 한 클라이언트 결과의 수를 제한 해야 할 수도 있습니다. 예를 들어, 클라이언트는 결과의 다음 페이지를 가져오는 "다음" 링크를 사용 하 여 한 번에 10 개 항목을 표시할 수 있습니다. 이렇게 하려면 클라이언트 $top 및 $skip 옵션을 사용 합니다.

`http://localhost/Products?$top=10&$skip=20`

$Top 옵션 반환할 항목의 최대 수를 제공 하 고 $skip 옵션을 건너뛸 항목 수를 제공 합니다. 앞의 예제 항목 21-30 인출합니다.

**필터링**

$Filter 옵션에는 부울 식을 적용 하 여 결과 필터링 하는 클라이언트 수 있습니다. 필터 식이 모두 매우 강력 합니다. 논리 및 산술 연산자, 문자열 함수 및 날짜 함수의 포함 됩니다.

| "Toys" 같은 범주를 사용 하 여 모든 제품을 반환 합니다. | `http://localhost/Products?$filter=Category` eq 'Toys' |
| --- | --- |
| 10 보다 낮은 가격으로 모든 제품을 반환 합니다. | `http://localhost/Products?$filter=Price` lt 10 |
| 논리 연산자 모든 제품을 반환할 위치 가격 > = 5이 고 가격 < = 15입니다. | `http://localhost/Products?$filter=Price` ge 5와 보다 적거나 같은 가격 15 |
| 문자열 함수: 이름에 "zz"를 사용 하 여 모든 제품을 반환 합니다. | `http://localhost/Products?$filter=substringof('zz',Name)` |
| 날짜 함수: 2005 이후 ReleaseDate 사용 하 여 모든 제품을 반환 합니다. | `http://localhost/Products?$filter=year(ReleaseDate)` gt 2005 |

**정렬**

결과 정렬 하려면 $orderby 필터를 사용 합니다.

| 가격으로 정렬 합니다. | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| 내림차순 (가장 낮은 가장 높음) 가격으로 정렬 합니다. | `http://localhost/Products?$orderby=Price desc` |
| 범주별으로 정렬 한 다음 가격 범주 내에서 내림차순으로 정렬 합니다. | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a>서버 기반 페이징

보낼 않으려는 데이터베이스 수백만 개의 레코드를 포함 하는 경우 페이로드 하나에 모두 있습니다. 이 방지 하려면 서버가 단일 응답에 전송 되는 엔트리의 수를 제한할 수 있습니다. 페이징을 사용 하도록 서버를 설정 합니다 **PageSize** 속성에는 **Queryable** 특성입니다. 값에는 반환할 항목의 최대 수입니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

컨트롤러 OData 형식을 반환 하는 경우 응답 본문에는 데이터의 다음 페이지에 대 한 링크를 포함 됩니다.

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

클라이언트는이 링크를 사용 하 여 다음 페이지를 가져올 수 있습니다. 결과 집합에 있는 항목의 총 수에 알아보려면 "allpages" 클라이언트 $inlinecount 쿼리 옵션 값을 설정할 수 있습니다.

`http://localhost/Products?$inlinecount=allpages`

값 "allpages" 응답의 총 수를 포함 하도록 서버에 알려 줍니다.

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> 다음 페이지 링크 및 인라인 카운트는 모두 OData 포맷을 해야합니다. OData 링크 및 개수를 보유 하는 응답 본문의 특수 필드를 정의 하는 이유 때문입니다.


OData이 아닌 형식에 대 한 것도 가능에서 쿼리 결과 래핑하여 다음 페이지 링크 및 인라인 카운트를 지원 하기를 **PageResult&lt;T&gt;**  개체입니다. 그러나 더 많은 코드가 필요합니다. 예를 들면 다음과 같습니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

JSON 응답 예제는 다음과 같습니다.

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a>쿼리 옵션을 제한합니다.

쿼리 옵션을 여러 가지 제어 서버에서 실행 되는 쿼리 클라이언트를 제공 합니다. 경우에 따라 보안 또는 성능 이유로 사용할 수 있는 옵션을 제한 하는 것이 좋습니다. 합니다 **[Queryable]** 특성에 일부 기본 제공 속성에서이 대 한 합니다. 다음은 몇 가지 예입니다.

$Skip 및 $top, 페이징 및 아무 지원 하기 위해 허용:

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

데이터베이스에서 인덱싱되지 않은 속성에 대해 정렬을 방지 하기 위해 특정 속성에 의해서만 정렬할 수 있습니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

"Eq" 논리 함수가 되었지만 다른 논리 함수가 없는 허용:

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

모든 산술 연산자를 허용 하지 않습니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

생성 하 여 옵션을 전역적으로 제한할 수 있습니다는 **QueryableAttribute** 인스턴스를 전달 하는 **EnableQuerySupport** 함수:

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a>쿼리 옵션을 직접 호출

사용 하는 대신 합니다 **[Queryable]** 특성을 컨트롤러에 직접 쿼리 옵션을 호출할 수 있습니다. 이렇게 하려면 추가 된 **ODataQueryOptions** 컨트롤러 메서드의 매개 변수입니다. 필요 하지 않습니다는 경우에 **[Queryable]** 특성입니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

웹 API 채웁니다 합니다 **ODataQueryOptions** URI에서 쿼리 문자열입니다. 쿼리를 적용 하려면 전달를 **IQueryable** 에 **ApplyTo** 메서드. 메서드가 반환 하는 값 **IQueryable**합니다.

고급 시나리오에서는 되지 않은 경우는 **IQueryable** 쿼리 공급자를 검사할 수 있습니다는 **ODataQueryOptions** 쿼리 옵션을 다른 형식으로 변환 합니다. (예를 들어 RaghuRam Nadiminti 블로그 게시물을 참조 [변환 OData 쿼리를 HQL로](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx)에 포함 됩니다는 [샘플](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)

<a id="query-validation"></a>
## <a name="query-validation"></a>쿼리 유효성 검사

합니다 **[Queryable]** 특성의 쿼리 실행 하기 전에 유효성을 검사 합니다. 유효성 검사 단계에서 수행 되는 **QueryableAttribute.ValidateQuery** 메서드. 유효성 검사 프로세스를 사용자 지정할 수도 있습니다.

도 참조 하세요 [OData 보안 지침](odata-security-guidance.md)합니다.

즉 클래스 유효성 검사기 중 하나는 재정의에서 정의 하는 먼저 합니다 **Web.Http.OData.Query.Validators** 네임 스페이스입니다. 예를 들어, 다음 유효성 검사기 클래스 $orderby 옵션에 대 한 'desc' 옵션을 사용 하지 않도록 설정 합니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

하위 클래스를 **[Queryable]** 특성을 재정의 하는 **ValidateQuery** 메서드.

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

그런 다음 사용자 지정 특성 하거나 전역으로 설정 하거나-컨트롤러:

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

사용 중인 경우 **ODataQueryOptions** 직접 유효성 검사기에 옵션을 설정 합니다.

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
