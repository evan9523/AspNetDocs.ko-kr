---
uid: web-api/overview/error-handling/web-api-global-error-handling
title: ASP.NET 웹 API 2 - ASP.NET 4.x의 전역 오류 처리
author: davidmatson
description: ASP.NET 4.x에 대한 ASP.NET 웹 API 2의 전역 오류 처리 개요입니다.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: bffd7863-f63b-4b23-a13c-372b5492e9fb
msc.legacyurl: /web-api/overview/error-handling/web-api-global-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 5ff54d2e4ed881ce927d0a401fb79d9b8bc5b8a1
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675425"
---
# <a name="global-error-handling-in-aspnet-web-api-2"></a>ASP.NET 웹 API 2의 글로벌 오류 처리

[데이비드 매슨,](https://github.com/davidmatson) [릭 앤더슨](https://twitter.com/RickAndMSFT)

이 항목에서는 ASP.NET 4.x에 대한 ASP.NET 웹 API 2의 전역 오류 처리에 대한 개요를 제공합니다. 오늘날 웹 API에서는 전 세계적으로 오류를 기록하거나 처리할 수 있는 쉬운 방법이 없습니다. 처리되지 않은 일부 예외는 [예외 필터를](exception-handling.md)통해 처리할 수 있지만 예외 필터가 처리할 수 없는 경우가 많습니다. 예를 들어:

1. 컨트롤러 생성자에서 throw된 예외
2. 메시지 처리기에서 throw된 예외
3. 라우팅 중에 throw된 예외
4. 응답 콘텐츠를 직렬화하는 동안 throw된 예외

이러한 예외를 기록하고 처리하는 간단하고 일관된 방법을 제공하고자 합니다. 

예외를 처리하는 두 가지 주요 사례가 있습니다. 후자의 경우는 스트리밍 응답 콘텐츠 중간에 예외가 throw되는 경우입니다. 이 경우 상태 코드, 헤더 및 부분 콘텐츠가 이미 와이어를 가로 질러 이동했기 때문에 새 응답 메시지를 보내기에는 너무 늦었기 때문에 연결을 중단하기만 하면 됩니다. 새 응답 메시지를 생성하기 위해 예외를 처리할 수 없지만 예외 로깅은 계속 지원됩니다. 오류를 감지할 수 있는 경우 다음과 같이 적절한 오류 응답을 반환할 수 있습니다.

[!code-csharp[Main](web-api-global-error-handling/samples/sample1.cs?highlight=6)]

### <a name="existing-options"></a>기존 옵션

[예외 필터](exception-handling.md)외에도 [메시지 처리기를](../advanced/http-message-handlers.md) 사용하여 모든 500수준 응답을 관찰할 수 있지만 원래 오류에 대한 컨텍스트가 없기 때문에 이러한 응답에 대해 사용하기가 어렵습니다. 메시지 처리기는 처리할 수 있는 서비스 케이스에 대한 예외 필터와 동일한 몇 가지 제한 사항이 있습니다. Web API에는 오류 조건을 캡처하는 추적 인프라가 있지만 추적 인프라는 진단을 위한 것이며 프로덕션 환경에서 실행하기 위해 설계되거나 적합하지 않습니다. 전역 예외 처리 및 로깅은 프로덕션 중에 실행되고 기존 모니터링 솔루션(예: [ELMAH)에](https://code.google.com/p/elmah/)연결될 수 있는 서비스여야 합니다.

### <a name="solution-overview"></a>솔루션 개요

 처리되지 않은 예외를 기록하고 처리하기 위해 두 개의 새로운 사용자 교체 가능한 서비스인 [IExceptionLogger](../releases/whats-new-in-aspnet-web-api-21.md) 및 IExceptionHandlerHandler를 제공합니다. 서비스는 매우 유사하며 두 가지 주요 차이점이 있습니다.

1. 여러 예외 로거를 등록하지만 단일 예외 처리기만 등록할 수 있습니다.
2. 연결을 중단하려고 하는 경우에도 예외 로거가 항상 호출됩니다. 예외 처리기는 보낼 응답 메시지를 선택할 수 있는 경우에만 호출됩니다.

두 서비스 모두 예외가 검색된 시점부터 관련 정보를 포함하는 예외 컨텍스트, 특히 [HttpRequestMessage,](https://msdn.microsoft.com/library/system.net.http.httprequestmessage(v=vs.110).aspx) [HttpRequestContext,](https://msdn.microsoft.com/library/system.web.http.controllers.httprequestcontext(v=vs.118).aspx)throw된 예외 및 예외 소스(아래 세부 정보)에 대한 액세스를 제공합니다.

### <a name="design-principles"></a>디자인 원칙

1. **주요 변경 사항 없음** 이 기능은 부 릴리스에 추가되기 때문에 솔루션에 영향을 주는 한 가지 중요한 제약 조건은 계약을 입력하거나 동작에 대한 주요 변경 내용이 없다는 것입니다. 이 제약 조건은 예외를 500개의 응답으로 전환하는 기존 catch 블록 측면에서 수행하려는 일부 정리를 배제했습니다. 이 추가 정리는 후속 주요 릴리스에서 고려할 수 있는 사항입니다. 이것이 중요한 경우 [웹 API 사용자 음성으로](http://aspnet.uservoice.com/forums/147201-asp-net-web-api/suggestions/5451321-add-flag-to-enable-iexceptionlogger-and-iexception)투표하십시오 ASP.NET.
2. **웹 API 구문과의 일관성 유지** Web API의 필터 파이프라인은 작업별, 컨트롤러별 또는 전역 범위에서 논리를 유연하게 적용하여 교차 절단 문제를 처리할 수 있는 좋은 방법입니다. 예외 필터를 포함한 필터에는 전역 범위에 등록된 경우에도 항상 작업 및 컨트롤러 컨텍스트가 있습니다. 이 계약은 필터에 적합하지만 전역으로 범위가 조정된 예외 필터도 작업 또는 컨트롤러 컨텍스트가 없는 메시지 처리기의 예외와 같은 일부 예외 처리 사례에 적합하지 않다는 것을 의미합니다. 예외 처리를 위해 필터에서 제공하는 유연한 범위 지정을 사용하려면 예외 필터가 필요합니다. 그러나 컨트롤러 컨텍스트 외부에서 예외를 처리해야 하는 경우 전체 전역 오류 처리(컨트롤러 컨텍스트 및 작업 컨텍스트 제약 조건이 없는 항목)에 대해 별도의 구문이 필요합니다.

### <a name="when-to-use"></a>사용 시기

- 예외 로거는 Web API에서 catch된 처리되지 않은 모든 예외를 확인하는 솔루션입니다.
- 예외 처리기는 Web API에서 catch한 처리되지 않은 예외에 대해 가능한 모든 응답을 사용자 지정하는 솔루션입니다.
- 예외 필터는 특정 작업 또는 컨트롤러와 관련된 하위 집합처리되지 않은 예외를 처리하는 가장 쉬운 솔루션입니다.

### <a name="service-details"></a>서비스 세부 정보

 예외 로거 및 처리기 서비스 인터페이스는 각각의 컨텍스트를 취하는 간단한 비동기 메서드입니다. 

[!code-csharp[Main](web-api-global-error-handling/samples/sample2.cs)]

 또한 이러한 두 인터페이스모두에 대한 기본 클래스도 제공합니다. 코어(동기화 또는 비동기) 메서드를 재정의하는 것은 권장 시간에 로그하거나 처리하는 데 필요한 모든 것입니다. 로깅의 `ExceptionLogger` 경우 기본 클래스는 코어 로깅 메서드가 각 예외에 대해 한 번만 호출되도록 합니다(나중에 호출 스택을 더 많이 전파하고 다시 catch되는 경우에도 마찬가지입니다). 기본 `ExceptionHandler` 클래스는 레거시 중첩된 catch 블록을 무시하고 호출 스택 맨 위에 있는 예외에 대해서만 코어 처리 메서드를 호출합니다. (이러한 기본 클래스의 단순화된 버전은 아래 부록에 있습니다.) 둘 `IExceptionLogger` `IExceptionHandler` 다 를 통해 예외에 대한 정보를 수신합니다. `ExceptionContext`

[!code-csharp[Main](web-api-global-error-handling/samples/sample3.cs)]

프레임워크가 예외 로거 또는 예외 처리기를 호출할 `Exception` 때 `Request`항상 및 을 제공합니다. 단위 테스트를 제외하고 항상 `RequestContext`을 제공합니다. 예외 필터에 `ControllerContext` 대한 `ActionContext` catch 블록에서 호출하는 경우에만 a 및 를 거의 제공하지 않습니다. 그것은 매우 드물게 `Response`(응답을 작성하려고하는 중간에 특정 IIS의 경우에만)를 제공하지 않습니다. 이러한 속성 중 일부는 예외 `null` 클래스의 멤버에 `null` 액세스하기 전에 확인하는 것은 소비자의 책임이 될 수 있으므로 주의하십시오.`CatchBlock` 는 예외를 본 catch 블록을 나타내는 문자열입니다. catch 블록 문자열은 다음과 같습니다.

- HttpServer (센드애싱크 방법)
- HttpControllerDispatcher(SendAsync 메서드)
- HttpBatchHandler (센타싱크 방법)
- IExceptionFilter(ApiController의 ExecuteAsync에서 예외 필터 파이프라인 처리)
- 오윈 호스트:

    - HttpMessageHandlerAdapter.버퍼응답콘텐츠Async(버퍼링 출력용)
    - HttpMessageHandlerAdapter.CopyResponse콘텐츠Async(스트리밍 출력용)
- 웹 호스트:

    - HttpControllerHandler.WriteBufferedResponse콘텐츠Async(버퍼링 출력용)
    - HttpControllerHandler.WriteStreamedResponse콘텐츠동기화(스트리밍 출력용)
    - HttpControllerHandler.WriteErrorResponseContentAsync (버퍼링된 출력 모드에서 오류 복구 실패의 경우)

catch 블록 문자열 목록은 정적 readonly 속성을 통해서도 사용할 수 있습니다. (코어 캐치 블록 문자열은 정적 ExceptionCatchBlocks에 있고 나머지는 OWIN 및 웹 호스트에 대해 각각 하나의 정적 클래스에 나타납니다.)`IsTopLevelCatchBlock` 호출 스택맨 맨 위에있는 예외를 처리하는 권장 패턴을 따르는 데 유용합니다. 예외를 중첩된 catch 블록이 발생하는 모든 곳에서 500개의 응답으로 전환하는 대신 예외 처리기는 호스트에서 보일 때까지 예외를 전파할 수 있습니다.

뿐만 `ExceptionContext`아니라, 로거는 전체를 `ExceptionLoggerContext`통해 하나의 정보를 가져옵니다 :

[!code-csharp[Main](web-api-global-error-handling/samples/sample4.cs)]

두 번째 `CanBeHandled`속성 , "로거는 처리할 수 없는 예외를 식별할 수 있습니다. 연결이 중단되고 새 응답 메시지를 보낼 수 없는 경우 로거가 호출되지만 처리기가 ***호출되지 않으며*** 로거가 이 속성에서 이 시나리오를 식별할 수 있습니다.

`ExceptionContext`에 추가로 처리기는 예외를 처리하기 위해 전체에 `ExceptionHandlerContext` 설정할 수 있는 속성을 하나 더 가져옵니다.

[!code-csharp[Main](web-api-global-error-handling/samples/sample5.cs)]

`Result` 예외 처리기는 속성을 작업 결과(예: [ExceptionResult,](https://msdn.microsoft.com/library/system.web.http.results.exceptionresult(v=vs.118).aspx) [InternalServerErrorResult,](https://msdn.microsoft.com/library/system.web.http.results.internalservererrorresult(v=vs.118).aspx) [StatusCodeResult](https://msdn.microsoft.com/library/system.web.http.results.statuscoderesult(v=vs.118).aspx)또는 사용자 지정 결과)로 설정하여 예외를 처리했음을 나타냅니다. 속성이 `Result` null이면 예외가 처리되지 않고 원래 예외가 다시 throw됩니다.

호출 스택 맨 위에 있는 예외의 경우 API 호출자에게 응답이 적절한지 확인하기 위해 추가 단계를 밟습니다. 예외가 호스트에 전파되면 호출자는 노란색 사망 화면또는 일반적으로 적절한 API 오류 응답이 아닌 HTML인 다른 호스트가 제공된 응답을 볼 수 있습니다. 이러한 경우 Result는 null이 아닌 것으로 시작되며 사용자 지정 예외 처리기가 명시적으로 다시 (처리되지 않음)으로 `null` 설정하는 경우에만 예외가 호스트에 전파됩니다. 이러한 `Result` `null` 경우설정은 다음 두 가지 시나리오에 유용할 수 있습니다.

1. OWIN은 웹 API 이전/외부에 등록된 미들웨어를 처리하는 사용자 지정 예외를 가진 웹 API를 호스팅했습니다.
2. 노란색 사망 화면이 실제로 처리되지 않은 예외에 대한 유용한 응답인 브라우저를 통한 로컬 디버깅입니다.

예외 로거와 예외 처리기 모두에 대해 로거 또는 처리기 자체가 예외를 throw하는 경우 복구할 수 없습니다. (예외가 전파되도록 하는 것 이외에는 더 나은 접근 방식이 있는 경우 이 페이지의 맨 아래에 피드백을 남겨 주세요.) 예외 로거 및 처리기에 대한 계약은 예외가 호출자에게 전파되도록 해서는 안 된다는 것입니다. 그렇지 않으면 예외가 호스트로 전파되어 ASP와 같은 HTML 오류가 발생하는 경우가 많습니다. NET의 노란색 화면)이 클라이언트로 다시 전송됩니다(일반적으로 JSON 또는 XML을 기대하는 API 호출자에게는 선호되지 않습니다).

## <a name="examples"></a>예

### <a name="tracing-exception-logger"></a>추적 예외 로거

아래 예외 로거는 구성된 추적 원본(Visual Studio의 디버그 출력 창 포함)에 예외 데이터를 보냅니다.

[!code-csharp[Main](web-api-global-error-handling/samples/sample6.cs)]

### <a name="custom-error-message-exception-handler"></a>사용자 지정 오류 메시지 예외 처리기

아래 예외 처리기는 지원에 문의하기 위한 전자 메일 주소를 포함하여 클라이언트에 대한 사용자 지정 오류 응답을 생성합니다.

[!code-csharp[Main](web-api-global-error-handling/samples/sample7.cs)]

## <a name="registering-exception-filters"></a>예외 필터 등록

"ASP.NET MVC 4 웹 응용 프로그램" 프로젝트 템플릿을 사용하여 프로젝트를 만드는 경우 `WebApiConfig` *App_Start* 폴더에 웹 API 구성 코드를 클래스 안에 넣습니다.

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

## <a name="appendix-base-class-details"></a>부록: 기본 클래스 세부 정보

[!code-csharp[Main](web-api-global-error-handling/samples/sample8.cs)]
