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
# <a name="routing-in-aspnet-web-api"></a>ASP.NET Web API의 라우팅

로 [마이크 와슨](https://github.com/MikeWasson)

이 문서에서는 ASP.NET 웹 API가 HTTP 요청을 컨트롤러에 라우팅하는 방법을 설명합니다.

> [!NOTE]
> ASP.NET MVC에 익숙한 경우 웹 API 라우팅은 MVC 라우팅과 매우 유사합니다. 주요 차이점은 Web API가 URI 경로가 아닌 HTTP 동사를 사용하여 작업을 선택한다는 것입니다. 웹 API에서 MVC 스타일 라우팅을 사용할 수도 있습니다. 이 문서에서는 ASP.NET MVC에 대한 어떠한 지식도 가정하지 않습니다.

## <a name="routing-tables"></a>라우팅 테이블

ASP.NET 웹 API에서 *컨트롤러는* HTTP 요청을 처리하는 클래스입니다. 컨트롤러의 공용 메서드를 *작업 메서드* 또는 단순히 *작업이라고*합니다. 웹 API 프레임워크가 요청을 받으면 요청을 작업에 라우팅합니다.

호출할 작업을 결정하기 위해 프레임워크는 *라우팅 테이블을*사용합니다. 웹 API에 대한 Visual Studio 프로젝트 템플릿은 기본 경로를 만듭니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

이 경로는 *\_앱 시작* 디렉터리에 배치되는 *WebApiConfig.cs* 파일에 정의됩니다.

![](routing-in-aspnet-web-api/_static/image1.png)

클래스에 `WebApiConfig` 대한 자세한 내용은 [웹 API 구성ASP.NET.](../advanced/configuring-aspnet-web-api.md)

웹 API를 자체 호스트하는 경우 `HttpSelfHostConfiguration` 개체에 직접 라우팅 테이블을 설정해야 합니다. 자세한 내용은 [웹 API 자체 호스트를](../older-versions/self-host-a-web-api.md)참조하십시오.

라우팅 테이블의 각 항목에는 *경로 템플릿이*포함되어 있습니다. 웹 API의 기본 경로 &quot;템플릿은 api/{컨트롤러}/{id}&quot;입니다. 이 템플릿에서 &quot;&quot; api는 리터럴 경로 세그먼트이고 {controller} 및 {id}는 자리 표시자 변수입니다.

웹 API 프레임워크가 HTTP 요청을 받으면 라우팅 테이블의 경로 템플릿 중 하나에 대해 URI를 일치시키려고 시도합니다. 경로가 일치하지 않으면 클라이언트에 404 오류가 발생합니다. 예를 들어 다음 URI는 기본 경로와 일치합니다.

- /api/연락처
- /api/연락처/1
- /api/제품/기즈모1

그러나 api &quot;&quot; 세그먼트가 없기 때문에 다음 URI가 일치하지 않습니다.

- /연락처/1

> [!NOTE]
> 경로에서 "api"를 사용하는 이유는 ASP.NET MVC 라우팅과의 충돌을 피하기 위해서입니다. 이렇게 하면 &quot;/연락처가&quot; MVC 컨트롤러로 이동하고 &quot;/api/연락처가&quot; 웹 API 컨트롤러로 이동하도록 할 수 있습니다. 물론 이 규칙이 마음에 들지 않으면 기본 경로 테이블을 변경할 수 있습니다.

일치하는 경로가 발견되면 Web API는 컨트롤러와 작업을 선택합니다.

- 컨트롤러를 찾기 위해 Web &quot;&quot; API는 *{controller}* 변수값에 컨트롤러를 추가합니다.
- 작업을 찾기 위해 Web API는 HTTP 동사를 찾은 다음 해당 HTTP 동사 이름으로 이름이 시작되는 작업을 찾습니다. 예를 들어 GET 요청을 사용하면 &quot;웹 API는 GetContact&quot; &quot;&quot; 또는 GetAllContacts &quot;와 같이&quot;GetContact 로 접두번에 붙어 있는 작업을 찾습니다. 이 규칙은 GET, POST, PUT, DELETE, HEAD, 옵션 및 패치 동사에만 적용됩니다. 컨트롤러의 특성을 사용하여 다른 HTTP 동사를 활성화할 수 있습니다. 나중에 그 예가 살펴보겠습니다.
- *{id}와* 같은 경로 템플릿의 다른 자리 표시자 변수는 작업 매개 변수에 매핑됩니다.

예제를 살펴보겠습니다. 다음 컨트롤러를 정의한다고 가정합니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

다음은 각 HTTP에 대해 호출되는 작업과 함께 가능한 HTTP 요청입니다.

| HTTP 동사 | URI 경로 | 작업 | 매개 변수 |
| --- | --- | --- | --- |
| GET | api/제품 | 겟올프로덕스 | *(없음)* |
| GET | api/제품/4 | 제품비하이드 | 4 |
| Delete | api/제품/4 | 제품 삭제 | 4 |
| POST | api/제품 | *(일치하지 않습니다)* |  |

URI의 *{id}* 세그먼트(있는 경우)가 작업의 *ID* 매개 변수에 매핑됩니다. 이 예제에서 컨트롤러는 ID 매개 변수가 있는 메서드와 *매개* 변수가 없는 두 가지 GET 메서드를 정의합니다.

또한 컨트롤러가 Post를 정의하지 않으므로 POST 요청이 &quot;실패합니다... &quot; 메서드를 참조하십시오.

## <a name="routing-variations"></a>라우팅 변형

이전 섹션에서는 ASP.NET 웹 API에 대한 기본 라우팅 메커니즘을 설명했습니다. 이 섹션에서는 몇 가지 변형에 대해 설명합니다.

### <a name="http-verbs"></a>HTTP 동사

HTTP 동사에 대 한 명명 규칙을 사용 하는 대신 다음 특성 중 하나를 사용 하 여 작업 메서드를 장식 하 여 작업에 대 한 HTTP 동사를 명시적으로 지정할 수 있습니다.

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

다음 예제에서는 메서드가 `FindProduct` GET 요청에 매핑됩니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

작업에 대해 여러 HTTP 동사를 허용하거나 GET, PUT, POST, DELETE, HEAD, OPTIONS 및 PATCH `[AcceptVerbs]` 이외의 HTTP 동사를 허용하려면 HTTP 동사 목록을 사용하는 특성을 사용합니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a>작업 이름으로 라우팅

기본 라우팅 템플릿을 사용하는 Web API는 HTTP 동사를 사용하여 작업을 선택합니다. 그러나 작업 이름이 URI에 포함된 경로를 만들 수도 있습니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

이 경로 템플릿에서 *{action}* 매개 변수는 컨트롤러의 작업 메서드이름을 지정합니다. 이 라우팅 스타일을 사용하면 특성을 사용하여 허용되는 HTTP 동사를 지정합니다. 예를 들어 컨트롤러에 다음과 같은 메서드가 있다고 가정합니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

이 경우 "api/제품/세부 정보/1"에 대한 GET `Details` 요청이 메서드에 매핑됩니다. 이 라우팅 스타일은 ASP.NET MVC와 유사하며 RPC 스타일 API에 적합할 수 있습니다.

`[ActionName]` 특성을 사용하여 작업 이름을 재정의할 수 있습니다. 다음 예제에서는 API/제품/축소판/ID에 매핑하는 &quot;두*id*가지 작업이 있습니다. 하나는 GET을 지원하고 다른 하나는 POST를 지원합니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a>비작업

메서드가 작업으로 호출되지 않도록 하려면 특성을 `[NonAction]` 사용합니다. 이는 메서드가 라우팅 규칙과 일치하지 않더라도 메서드가 동작이 아님을 프레임워크에 나타냅니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a>추가 참고 자료

이 항목에서는 라우팅에 대한 높은 수준의 보기를 제공했습니다. 자세한 내용은 프레임워크가 [URI를](routing-and-action-selection.md)경로에 일치시키고 컨트롤러를 선택한 다음 호출할 작업을 선택하는 방법을 정확하게 설명하는 라우팅 및 작업 선택을 참조하십시오.
