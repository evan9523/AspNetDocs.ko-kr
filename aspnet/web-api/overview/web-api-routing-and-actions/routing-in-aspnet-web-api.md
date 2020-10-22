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
# <a name="routing-in-aspnet-web-api"></a>ASP.NET Web API의 라우팅

[Mike Wasson](https://github.com/MikeWasson)

이 문서에서는 ASP.NET Web API는 컨트롤러에 HTTP 요청을 라우팅하는 방법을 설명 합니다.

> [!NOTE]
> ASP.NET MVC에 익숙한 경우 Web API 라우팅은 MVC 라우팅과 매우 유사 합니다. 주요 차이점은 Web API는 URI 경로가 아니라 HTTP 동사를 사용 하 여 작업을 선택 한다는 것입니다. Web API에서 MVC 스타일 라우팅을 사용할 수도 있습니다. 이 문서에서는 ASP.NET MVC에 대 한 지식이 있다고 가정 하지 않습니다.

## <a name="routing-tables"></a>라우팅 테이블

ASP.NET Web API에서 *컨트롤러* 는 HTTP 요청을 처리 하는 클래스입니다. 컨트롤러의 공용 메서드를 *작업 메서드* 또는 간단히 *동작*이라고 합니다. 웹 API 프레임 워크에서 요청을 받으면 요청을 작업으로 라우팅합니다.

호출할 동작을 결정 하기 위해 프레임 워크는 *라우팅 테이블*을 사용 합니다. Web API 용 Visual Studio 프로젝트 템플릿은 기본 경로를 만듭니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

이 경로는 *WebApiConfig.cs* 파일에 정의 되며, *앱 \_ 시작* 디렉터리에 배치 됩니다.

![](routing-in-aspnet-web-api/_static/image1.png)

클래스에 대 한 자세한 내용은 `WebApiConfig` [ASP.NET Web API 구성](../advanced/configuring-aspnet-web-api.md)을 참조 하세요.

Web API를 자체 호스트 하는 경우에는 개체에 직접 라우팅 테이블을 설정 해야 합니다 `HttpSelfHostConfiguration` . 자세한 내용은 [웹 API 자체 호스팅](../older-versions/self-host-a-web-api.md)을 참조 하세요.

라우팅 테이블의 각 항목에는 *경로 템플릿이*포함 되어 있습니다. Web API에 대 한 기본 경로 템플릿은 &quot; API/{controller}/{id}입니다 &quot; . 이 템플릿에서 &quot; api &quot; 는 리터럴 경로 세그먼트이 고 {controller} 및 {id}는 자리 표시자 변수입니다.

웹 API 프레임 워크는 HTTP 요청을 받으면 라우팅 테이블의 경로 템플릿 중 하나에 대해 URI를 일치 시 키 려 고 시도 합니다. 경로가 일치 하지 않으면 클라이언트에서 404 오류를 수신 합니다. 예를 들어 다음 Uri는 기본 경로와 일치 합니다.

- /api/연락처
- /api/contacts/1
- /api/products/gizmo1

그러나 다음 URI는 api 세그먼트가 없으므로 일치 하지 않습니다 &quot; &quot; .

- /contacts/1

> [!NOTE]
> 경로에서 "api"를 사용 하는 이유는 ASP.NET MVC 라우팅과의 충돌을 방지 하기 위한 것입니다. 이러한 방식으로 &quot; /연락처를 &quot; MVC 컨트롤러로 이동 하 고///또는 &quot; 연락처를 &quot; 웹 api 컨트롤러로 이동할 수 있습니다. 물론이 규칙을 원하지 않는 경우 기본 경로 테이블을 변경할 수 있습니다.

일치 하는 경로가 발견 되 면 Web API는 컨트롤러 및 작업을 선택 합니다.

- 웹 API는 컨트롤러를 찾기 위해 &quot; &quot; *{controller}* 변수 값에 컨트롤러를 추가 합니다.
- 동작을 찾기 위해 Web API는 HTTP 동사를 찾은 다음 이름이 해당 HTTP 동사 이름으로 시작 하는 작업을 찾습니다. 예를 들어 GET 요청을 사용 하는 경우 Web API는 &quot; &quot; &quot; getcontact &quot; 또는 &quot; getallcontacts와 같이 get이 &quot; 접두사로 추가 된 작업을 찾습니다. 이 규칙은 GET, POST, PUT, DELETE, HEAD, OPTIONS 및 PATCH 동사에만 적용 됩니다. 컨트롤러에서 특성을 사용 하 여 다른 HTTP 동사를 사용 하도록 설정할 수 있습니다. 이에 대 한 예제는 나중에 살펴보겠습니다.
- 경로 템플릿의 다른 자리 표시자 변수 (예: *{id}* )는 동작 매개 변수에 매핑됩니다.

예를 살펴보겠습니다. 다음 컨트롤러를 정의 한다고 가정 합니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

다음은 각각에 대해 호출 되는 작업과 함께 가능한 몇 가지 HTTP 요청입니다.

| HTTP 동사 | URI 경로 | 작업 | 매개 변수 |
| --- | --- | --- | --- |
| GET | a p i/제품 | GetAllProducts | *없음을* |
| GET | a p i/제품/4 | GetProductById | 4 |
| Delete | a p i/제품/4 | DeleteProduct | 4 |
| POST | a p i/제품 | *(일치 항목 없음)* |  |

URI의 *{id}* 세그먼트 (있는 경우)가 동작의 *id* 매개 변수에 매핑됩니다. 이 예제에서 컨트롤러는 두 개의 GET 메서드를 정의 합니다. 하나는 *id* 매개 변수를 사용 하 고 다른 하나는 매개 변수를 포함 하지 않습니다.

또한 컨트롤러에서 &quot; post ... 메서드를 정의 하지 않으므로 post 요청은 실패 합니다. &quot;

## <a name="routing-variations"></a>라우팅 변형

이전 섹션에서는 ASP.NET Web API에 대 한 기본 라우팅 메커니즘에 대해 설명 했습니다. 이 섹션에서는 몇 가지 변형에 대해 설명 합니다.

### <a name="http-verbs"></a>HTTP 동사

HTTP 동사에 대 한 명명 규칙을 사용 하는 대신 작업 메서드를 다음 특성 중 하나로 데코레이팅 하 여 동작에 대 한 HTTP 동사를 명시적으로 지정할 수 있습니다.

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

다음 예제에서 `FindProduct` 메서드는 GET 요청에 매핑됩니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

작업에 대해 여러 HTTP 동사를 허용 하거나 GET, PUT, POST, DELETE, HEAD, OPTIONS 및 PATCH 이외의 HTTP 동사를 허용 하려면 `[AcceptVerbs]` http 동사 목록을 사용 하는 특성을 사용 합니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a>작업 이름별 라우팅

기본 라우팅 템플릿을 사용 하는 경우 Web API는 HTTP 동사를 사용 하 여 작업을 선택 합니다. 그러나 URI에 작업 이름이 포함 된 경로를 만들 수도 있습니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

이 경로 템플릿에서 *{action}* 매개 변수는 컨트롤러의 동작 메서드 이름을로 설정 합니다. 이 스타일의 라우팅을 사용 하 여 특성을 사용 하 여 허용 되는 HTTP 동사를 지정 합니다. 예를 들어 컨트롤러에 다음 메서드가 있다고 가정 합니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

이 경우 "api/products/details/1"에 대 한 GET 요청은 `Details` 메서드에 매핑됩니다. 이 라우팅 스타일은 ASP.NET MVC와 비슷하며 RPC 스타일 API에 적합할 수 있습니다.

특성을 사용 하 여 작업 이름을 재정의할 수 있습니다 `[ActionName]` . 다음 예제에서는 a p i/ &quot; 제품/축소판 그림/*id*에 매핑되는 두 가지 작업을 수행 합니다. 하나는 GET을 지원 하 고 다른 하나는 POST를 지원 합니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a>비 작업

메서드가 동작으로 호출 되는 것을 방지 하려면 특성을 사용 `[NonAction]` 합니다. 이는 다른 방법으로 라우팅 규칙과 일치 하는 경우에도 메서드가 동작이 아니라는 프레임 워크에 신호를 보냅니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a>추가 정보

이 항목에서는 라우팅에 대 한 개략적인 보기를 제공 했습니다. 자세한 내용은 [라우팅 및 작업 선택](routing-and-action-selection.md), 프레임 워크가 경로에 대 한 URI를 정확히 일치 하는 방식에 대해 설명 하 고, 컨트롤러를 선택한 다음 호출할 작업을 선택 하는 방법을 참조 하세요.
