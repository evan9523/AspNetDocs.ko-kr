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
# <a name="attribute-routing-in-aspnet-web-api-2"></a>ASP.NET 웹 API 2의 특성 라우팅

로 [마이크 와슨](https://github.com/MikeWasson)

*라우팅은* 웹 API가 URI를 작업에 일치시는 방법입니다. 웹 API 2는 특성 라우팅이라는 새로운 유형의 *라우팅을*지원합니다. 이름에서 알 수 있듯이 특성 라우팅은 특성을 사용하여 경로를 정의합니다. 특성 라우팅을 사용하면 웹 API의 URI를 보다 세한 제어할 수 있습니다. 예를 들어 리소스 계층구조를 설명하는 URI를 쉽게 만들 수 있습니다.

규칙 기반 라우팅이라고 하는 이전 라우팅 스타일은 여전히 완벽하게 지원됩니다. 실제로 동일한 프로젝트에서 두 기술을 결합할 수 있습니다.

이 항목에서는 특성 라우팅을 사용하도록 설정하는 방법을 보여 주며 특성 라우팅에 대한 다양한 옵션을 설명합니다. 특성 라우팅을 사용하는 종단 간 자습서의 경우 [웹 API 2에서 특성 라우팅을 사용하여 REST API 만들기를](create-a-rest-api-with-attribute-routing.md)참조하십시오.

## <a name="prerequisites"></a>사전 요구 사항

[비주얼 스튜디오 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) 커뮤니티, 전문가 또는 엔터프라이즈 에디션

또는 NuGet 패키지 관리자를 사용하여 필요한 패키지를 설치합니다. Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자를**선택한 다음 **패키지 관리자 콘솔을**선택합니다. 패키지 관리자 콘솔 창에 다음 명령을 입력합니다.

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a>특성 라우팅이 왜 해야 합니까?

웹 API의 첫 번째 릴리스는 *규칙 기반* 라우팅을 사용했습니다. 해당 라우팅 유형에서는 기본적으로 매개 변수화된 문자열인 하나 이상의 경로 템플릿을 정의합니다. 프레임워크가 요청을 받으면 URI를 경로 템플릿과 일치시게 됩니다. 규칙 기반 라우팅에 대한 자세한 내용은 [ASP.NET 웹 API의 라우팅을](routing-in-aspnet-web-api.md)참조하십시오.

규칙 기반 라우팅의 한 가지 장점은 템플릿이 한 곳에 정의되고 라우팅 규칙이 모든 컨트롤러에 일관되게 적용된다는 것입니다. 안타깝게도 규칙 기반 라우팅은 RESTful API에서 일반적인 특정 URI 패턴을 지원하기 어렵게 만듭니다. 예를 들어 리소스에는 종종 하위 리소스가 포함됩니다: 고객이 주문을 하고, 영화에 액터가 있고, 책에 저자가 있습니다. 이러한 관계를 반영하는 URI를 만드는 것은 당연합니다.

`/customers/1/orders`

이러한 유형의 URI는 규칙 기반 라우팅을 사용하여 만들기가 어렵습니다. 이 작업을 수행할 수 있지만 컨트롤러 나 리소스 유형이 많은 경우 결과가 잘 확장되지 않습니다.

특성 라우팅을 사용하면 이 URI에 대한 경로를 정의하는 것이 간단합니다. 컨트롤러 작업에 특성을 추가하기만 하면 됩니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

다음은 특성 라우팅을 쉽게 만드는 몇 가지 다른 패턴입니다.

**API 버전 관리**

이 예제에서는 "/api/v1/제품"이 "/api/v2/products"가 아닌 다른 컨트롤러로 라우팅됩니다.

`/api/v1/products`
`/api/v2/products`

**오버로드된 URI 세그먼트**

이 예제에서 "1"은 주문 번호이지만 컬렉션에 "보류 중"이 매핑됩니다.

`/orders/1`
`/orders/pending`

**여러 매개 변수 유형**

이 예에서 "1"은 주문 번호이지만 "2013/06/16"은 날짜를 지정합니다.

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a>특성 라우팅 사용

특성 라우팅을 사용하려면 구성 중에 **MapHttpAttributeRoutes를 호출합니다.** 이 확장 메서드는 **System.Web.Http.HttpConfigurationExtensions** 클래스에 정의되어 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

특성 라우팅을 규칙 [기반](routing-in-aspnet-web-api.md) 라우팅과 결합할 수 있습니다. 규칙 기반 경로를 정의하려면 **MapHttpRoute** 메서드를 호출합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

웹 API 구성에 대한 자세한 내용은 [웹 API 2에 ASP.NET 구성을](../advanced/configuring-aspnet-web-api.md)참조하십시오.

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a>참고: 웹 API 1에서 마이그레이션

웹 API 2 이전에는 웹 API 프로젝트 템플릿이 다음과 같은 코드를 생성했습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

특성 라우팅을 사용하도록 설정하면 이 코드에서 예외가 발생합니다. 특성 라우팅을 사용하도록 기존 Web API 프로젝트를 업그레이드하는 경우 이 구성 코드를 다음으로 업데이트해야 합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> 자세한 내용은 [ASP.NET 호스팅을 통해 웹 API 구성을](../advanced/configuring-aspnet-web-api.md#webhost)참조하십시오.

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a>경로 특성 추가

다음은 특성을 사용하여 정의된 경로의 예입니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

문자열 &quot;고객/{customerId}/주문은&quot; 경로에 대 한 URI 템플릿입니다. 웹 API는 요청 URI를 템플릿에 일치시키려고 합니다. 이 예제에서 "고객" 및 "주문"은 리터럴 세그먼트이고 "{customerId}"는 변수 매개 변수입니다. 다음 URI는 이 템플릿과 일치합니다.

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

이 항목의 후반부에서 설명하는 제약 조건을 사용하여 일치를 제한할 수 [있습니다.](#constraints)

경로 템플릿의 &quot;{customerId}&quot; 매개 변수가 메서드의 *customerId* 매개 변수 의 이름과 일치합니다. Web API가 컨트롤러 작업을 호출하면 경로 매개 변수를 바인딩하려고 시도합니다. 예를 들어 URI인 `http://example.com/customers/1/orders`경우 Web API는 작업에서 *customerId* 매개 변수에 값 "1"을 바인딩하려고 시도합니다.

URI 템플릿에는 다음과 같은 여러 매개 변수가 있을 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

경로 특성이 없는 모든 컨트롤러 메서드는 규칙 기반 라우팅을 사용합니다. 이렇게 하면 동일한 프로젝트에서 두 가지 유형의 라우팅을 결합할 수 있습니다.

## <a name="http-methods"></a>HTTP 메서드

또한 웹 API는 요청의 HTTP 메서드(GET, POST 등)에 따라 작업을 선택합니다. 기본적으로 Web API는 컨트롤러 메서드 이름의 시작과 대/소문자를 구분하지 않는 일치를 찾습니다. 예를 들어, 명명된 `PutCustomers` 컨트롤러 메서드는 HTTP PUT 요청과 일치합니다.

메서드를 다음과 같은 특성으로 장식하여 이 규칙을 재정의할 수 있습니다.

- **[HttpDelete]**
- **[HttpGet]**
- **[HttpHead]**
- **[Http옵션]**
- **[Http패치]**
- **[HttpPost]**
- **[HttpPut]**

다음 예제는 CreateBook 메서드를 HTTP POST 요청에 매핑합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

비표준 메서드를 포함한 다른 모든 HTTP 메서드의 경우 HTTP 메서드 목록을 사용하는 **AcceptVerbs** 특성을 사용합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a>배관 접두사

컨트롤러의 경로는 모두 동일한 접두사로 시작하는 경우가 많습니다. 예를 들어:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

**[RoutePrefix]** 특성을 사용하여 전체 컨트롤러에 대한 공통 접두사를 설정할 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

메서드 특성에 물결표(~)를 사용하여 배관 접두사를 재정의합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

배관 접두사에는 매개 변수가 포함될 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a>배관 구속조건

경로 제약 조건을 사용하면 경로 템플릿의 매개 변수가 일치하는 방법을 제한할 수 있습니다. 일반 구문은 &quot;{매개 변수&quot;:제약 조건}입니다. 예를 들어:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

여기서 첫 번째 경로는 URI의 &quot;&quot; ID 세그먼트가 정수인 경우에만 선택됩니다. 그렇지 않으면 두 번째 경로가 선택됩니다.

다음 표에는 지원되는 제약 조건이 나열되어 있습니다.

| 제약 조건 | Description | 예제 |
| --- | --- | --- |
| alpha | 대문자 또는 소문자 라틴어 알파벳 문자(a-z, A-Z)와 일치합니다. | {x:알파} |
| bool | 부울 값과 일치합니다. | {x:bool} |
| Datetime | **DateTime** 값을 일치합니다. | {x:날짜 시간} |
| decimal | 소수점 값과 일치합니다. | {x:소수점} |
| double | 64비트 부동 점 값과 일치합니다. | {x:더블} |
| float | 32비트 부동 점 값과 일치합니다. | {x:float} |
| guid | GUID 값과 일치합니다. | {x:guid} |
| int | 32비트 정수 값과 일치합니다. | {x:int} |
| length | 지정된 길이 또는 지정된 길이 범위 내에서 문자열을 일치시면 됩니다. | {x:길이(6)} {x:길이(1,20)} |
| long | 64비트 정수 값과 일치합니다. | {x:long} |
| max | 정수와 최대값을 일치시다. | {x:최대(10)} |
| Maxlength | 최대 길이의 문자열과 일치합니다. | {x:최대길이(10)} |
| min | 정수와 최소 값을 일치시면 됩니다. | {x:min(10)} |
| 최소 길이 | 최소 길이의 문자열과 일치합니다. | {x:최소길이(10)} |
| range | 값 범위 내에서 정수를 일치합니다. | {x:범위(10,50)} |
| regex | 정규식과 일치합니다. | {x:정규식(^\\d{3}-\d{3}{4}-\d $)} |

min과 &quot;&quot;같은 일부 제약 조건은 괄호 안에 인수를 취합니다. 콜론으로 구분된 매개변수에 여러 구속조건을 적용할 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a>사용자 지정 경로 제약 조건

**IHttpRouteConstraint** 인터페이스를 구현 하여 사용자 지정 경로 제약 조건을 만들 수 있습니다. 예를 들어 다음 제약 조건은 매개 변수를 0이 아닌 정수 값으로 제한합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

다음 코드는 제약 조건을 등록하는 방법을 보여 주며 다음과 같은 방법을 보여 주며

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

이제 경로에 제약 조건을 적용할 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

**IInline제약** 해결사 인터페이스를 구현하여 전체 **DefaultInInConstraintResolver** 클래스를 대체할 수도 있습니다. 이렇게 하면 **IInlineConstraintResolver의** 구현이 특별히 추가되지 않는 한 모든 기본 제공 제약 조건이 대체됩니다.

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a>선택적 URI 매개 변수 및 기본값

경로 매개 변수에 물음표를 추가하여 URI 매개 변수를 선택적으로 만들 수 있습니다. 경로 매개 변수가 선택 사항인 경우 메서드 매개 변수에 대한 기본값을 정의해야 합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

이 예제에서는 `/api/books/locale/1033` `/api/books/locale` 동일한 리소스를 반환합니다.

또는 다음과 같이 경로 템플릿 내에서 기본값을 지정할 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

이는 이전 예제와 거의 동일하지만 기본값을 적용할 때 동작의 약간의 차이가 있습니다.

- 첫 번째 예제("{lcid:int?")에서 1033의 기본값은 메서드 매개 변수에 직접 할당되므로 매개 변수에 이 정확한 값이 있습니다.
- 두 번째 예제("{lcid:int=1033}")에서 "1033"의 기본값은 모델 바인딩 프로세스를 거칩니다. 기본 모델 바인더는 "1033"을 숫자 값 1033으로 변환합니다. 그러나 사용자 지정 모델 바인더를 연결하여 다른 작업을 수행할 수 있습니다.

대부분의 경우 파이프라인에 사용자 지정 모델 바인더가 없는 경우 두 양식은 동일합니다.

<a id="route-names"></a>
## <a name="route-names"></a>루트 이름

웹 API에서 모든 경로에는 이름이 있습니다. 경로 이름은 HTTP 응답에 링크를 포함할 수 있도록 링크를 생성하는 데 유용합니다.

경로 이름을 지정하려면 특성에 **Name** 속성을 설정합니다. 다음 예제에서는 경로 이름을 설정하는 방법과 링크를 생성할 때 경로 이름을 사용하는 방법을 보여 주며, 또한 경로 이름을 사용하는 방법을 보여 주며,

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a>경로 순서

프레임워크가 URI를 경로와 일치시키려고 하면 특정 순서로 경로를 평가합니다. 순서를 지정하려면 route 특성에 **Order** 속성을 설정합니다. 낮은 값이 먼저 평가됩니다. 기본 순서 값은 0입니다.

총 주문이 결정되는 방법은 다음과 같습니다.

1. 경로 특성의 **Order** 속성을 비교합니다.
2. 경로 템플릿의 각 URI 세그먼트를 살펴봅니다. 각 세그먼트에 대해 다음과 같이 주문하십시오.

    1. 리터럴 세그먼트.
    2. 구속조건이 있는 배관 매개변수입니다.
    3. 구속조건이 없는 배관 매개변수입니다.
    4. 구속조건이 있는 와일드카드 매개변수 세그먼트입니다.
    5. 제약 조건이 없는 와일드카드 매개변수 세그먼트입니다.
3. 넥타이의 경우 경로 템플릿의 대/소문자 구분 성 서수 문자열[비교(OrdinalIgnoreCase)에](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)의해 경로가 정렬됩니다.

다음 예를 참조하세요. 다음 컨트롤러를 정의한다고 가정합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

이러한 경로는 다음과 같이 정렬됩니다.

1. 주문/세부 정보
2. 주문/{id}
3. 주문/{고객 이름}
4. 주문/{\*날짜}
5. 주문/보류 중

"세부 정보"는 리터럴 세그먼트이며 "{id}" 앞에 표시되지만 **Order** 속성이 1이기 때문에 "보류 중"이 마지막으로 나타납니다. 이 예제에서는 "세부 정보" 또는 "보류 중"이라는 고객이 없다고 가정합니다. 일반적으로 모호한 경로를 피하십시오. 이 예제에서 더 나은 `GetByCustomer` 경로 템플릿은 "고객/{customerName}"입니다.
