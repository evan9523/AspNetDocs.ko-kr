---
uid: web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
title: ASP.NET Web API 2의 유닛 테스트 컨트롤러 | Microsoft Docs
author: MikeWasson
description: 이 항목에서는 Web API 2의 유닛 테스트 컨트롤러에 대 한 몇 가지 특정 기술에 대해 설명 합니다. 이 항목을 읽기 전에 자습서 단위를 읽을 수 있습니다.
ms.author: riande
ms.date: 06/11/2014
ms.assetid: 43a6cce7-a3ef-42aa-ad06-90d36d49f098
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: ee933cfc736a07b91c8f7feea2c4a2c64d200942
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240650"
---
# <a name="unit-testing-controllers-in-aspnet-web-api-2"></a>ASP.NET Web API 2의 유닛 테스트 컨트롤러

[Mike Wasson](https://github.com/MikeWasson)

> 이 항목에서는 Web API 2의 유닛 테스트 컨트롤러에 대 한 몇 가지 특정 기술에 대해 설명 합니다. 이 항목을 읽기 전에 솔루션에 단위 테스트 프로젝트를 추가 하는 방법을 보여 주는 자습서 [단위 테스트 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)를 읽어 볼 수 있습니다.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Web API 2
> - [Moq](https://github.com/Moq) 4.5.30

> [!NOTE]
> Moq를 사용 했지만 모든 모의 프레임 워크에 동일한 아이디어가 적용 됩니다. Moq 4.5.30 이상 버전은 Visual Studio 2017, Roslyn 및 .NET 4.5 이상 버전을 지원 합니다.

단위 테스트의 일반적인 패턴은 &quot; 정렬-동작 어설션입니다 &quot; .

- 정렬: 테스트를 실행 하기 위한 모든 필수 구성 요소를 설정 합니다.
- Act: 테스트를 수행 합니다.
- Assert: 테스트에 성공 했는지 확인 합니다.

정렬 단계에서 모의 개체 또는 스텁 개체를 사용 하는 경우가 많습니다. 이렇게 하면 종속성 수가 최소화 되므로 테스트는 한 가지 테스트를 중심으로 합니다.

웹 API 컨트롤러에서 단위 테스트를 수행 해야 하는 몇 가지 사항은 다음과 같습니다.

- 작업은 올바른 응답 유형을 반환 합니다.
- 잘못 된 매개 변수는 올바른 오류 응답을 반환 합니다.
- 작업은 리포지토리 또는 서비스 계층에서 올바른 메서드를 호출 합니다.
- 응답이 도메인 모델을 포함 하는 경우 모델 유형을 확인 합니다.

이러한 항목은 몇 가지 일반적인 테스트 이지만 컨트롤러 구현에 따라 구체적입니다. 특히 컨트롤러 작업에서 **HttpResponseMessage** 또는 **IHttpActionResult**를 반환 하는지 여부에 따라 큰 차이가 있습니다. 이러한 결과 형식에 대 한 자세한 내용은 [Web Api 2의 작업 결과](../getting-started-with-aspnet-web-api/action-results.md)를 참조 하세요.

## <a name="testing-actions-that-return-httpresponsemessage"></a>HttpResponseMessage를 반환 하는 테스트 작업

다음은 작업에서 **HttpResponseMessage**를 반환 하는 컨트롤러의 예입니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample1.cs)]

컨트롤러는 종속성 주입을 사용 하 여을 삽입 `IProductRepository` 합니다. 이렇게 하면 모의 리포지토리를 주입할 수 있으므로 컨트롤러를 더 쉽게 테스트할 수 있습니다. 다음 단위 테스트는 `Get` 메서드가 응답 본문에를 기록 하는지 확인 합니다 `Product` . `repository`가 모의 라고 가정 `IProductRepository` 합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample2.cs)]

컨트롤러에서 **요청** 및 **구성을** 설정 하는 것이 중요 합니다. 그렇지 않으면 **Argumentnullexception** 또는 **InvalidOperationException**를 사용 하 여 테스트가 실패 합니다.

## <a name="testing-link-generation"></a>테스트 링크 생성

`Post`메서드는 **urlhelper 링크** 를 호출 하 여 응답에 링크를 만듭니다. 이렇게 하려면 단위 테스트에서 약간의 설정이 필요 합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample3.cs)]

**Urlhelper** 클래스는 요청 URL 및 경로 데이터를 요구 하므로 테스트에서 이러한 값을 설정 해야 합니다. 또 다른 옵션은 모의 또는 스텁 **Urlhelper**입니다. 이 방법을 사용 하면 [ApiController](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) 의 기본값을 고정 값을 반환 하는 모의 또는 스텁 버전으로 바꿀 수 있습니다.

[Moq](https://github.com/Moq) 프레임 워크를 사용 하 여 테스트를 다시 작성해 보겠습니다. `Moq`테스트 프로젝트에 NuGet 패키지를 설치 합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample4.cs)]

이 버전에서는 모의 **Urlhelper** 가 상수 문자열을 반환 하므로 경로 데이터를 설정할 필요가 없습니다.

## <a name="testing-actions-that-return-ihttpactionresult"></a>IHttpActionResult를 반환 하는 테스트 작업

Web API 2에서 컨트롤러 동작은 ASP.NET MVC의 **Actionresult** 와 유사한 **IHttpActionResult**를 반환할 수 있습니다. **IHttpActionResult** 인터페이스는 HTTP 응답을 만들기 위한 명령 패턴을 정의 합니다. 컨트롤러는 직접 응답을 만드는 대신 **IHttpActionResult**를 반환 합니다. 나중에 파이프라인은 **IHttpActionResult** 를 호출 하 여 응답을 만듭니다. **HttpResponseMessage**에 필요한 많은 설치를 건너뛸 수 있으므로이 방법을 사용 하면 단위 테스트를 보다 쉽게 작성할 수 있습니다.

작업에서 **IHttpActionResult**를 반환 하는 예제 컨트롤러는 다음과 같습니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample5.cs)]

이 예제에서는 **IHttpActionResult**를 사용 하는 몇 가지 일반적인 패턴을 보여 줍니다. 테스트를 단위 테스트 하는 방법을 알아보겠습니다.

### <a name="action-returns-200-ok-with-a-response-body"></a>작업은 응답 본문으로 200 (OK)를 반환 합니다.

`Get`제품이 발견 되 면 메서드는를 호출 합니다 `Ok(product)` . 단위 테스트에서 반환 형식이 **Oknegotiatedcontentresult** 이 고 반환 된 제품에 올바른 ID가 있는지 확인 합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample6.cs)]

단위 테스트는 작업 결과를 실행 하지 않습니다. 작업 결과에서 HTTP 응답을 올바르게 생성 하는 것으로 간주할 수 있습니다. Web API 프레임 워크에는 고유한 단위 테스트가 포함 되어 있습니다.

### <a name="action-returns-404-not-found"></a>작업에서 404 (찾을 수 없음)을 반환 합니다.

`Get`제품을 찾을 수 없는 경우 메서드는를 호출 합니다 `NotFound()` . 이 경우 단위 테스트는 반환 형식이 **NotFoundResult**인지만 확인 합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample7.cs)]

### <a name="action-returns-200-ok-with-no-response-body"></a>작업은 응답 본문이 없는 200 (OK)를 반환 합니다.

`Delete`메서드는 `Ok()` 를 호출 하 여 빈 HTTP 200 응답을 반환 합니다. 이전 예제와 마찬가지로 단위 테스트는 반환 형식 (이 경우 **Okresult**)을 확인 합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample8.cs)]

### <a name="action-returns-201-created-with-a-location-header"></a>작업은 Location 헤더를 사용 하 여 201 (Created)을 반환 합니다.

`Post`메서드는 `CreatedAtRoute` 를 호출 하 여 Location 헤더에 URI가 있는 HTTP 201 응답을 반환 합니다. 단위 테스트에서 작업이 올바른 라우팅 값을 설정 하는지 확인 합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample9.cs)]

### <a name="action-returns-another-2xx-with-a-response-body"></a>작업은 응답 본문이 있는 다른 2xx를 반환 합니다.

`Put`메서드는 `Content` 를 호출 하 여 응답 본문이 포함 된 HTTP 202 (수락 됨) 응답을 반환 합니다. 이 경우 200 (OK)을 반환 하는 것과 유사 하지만 단위 테스트 에서도 상태 코드를 확인 해야 합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample10.cs)]

## <a name="additional-resources"></a>추가 리소스

- [유닛 테스트 ASP.NET Web API 2 Entity Framework 모의](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)
- [ASP.NET Web API 서비스에 대 한 테스트 작성](https://docs.microsoft.com/archive/blogs/youssefm/writing-tests-for-an-asp-net-web-api-service) (Youssef Moussaoui의 블로그 게시물).
- [경로 디버거를 사용하여 ASP.NET Web API 디버깅](https://blogs.msdn.com/b/webdev/archive/2013/04/04/debugging-asp-net-web-api-with-route-debugger.aspx)
