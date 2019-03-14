---
title: ASP.NET Core에서 LoggerMessage를 사용한 고성능 로깅
author: guardrex
description: LoggerMessage를 사용하여 고성능 로깅 시나리오에 적은 개체 할당을 필요로 하는 캐시 가능한 대리자를 만드는 방법을 알아봅니다.
ms.author: riande
ms.date: 11/03/2017
uid: fundamentals/logging/loggermessage
ms.openlocfilehash: a0080a20fed2d8fc295e55822c11d5731c6910ca
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048620"
---
# <a name="high-performance-logging-with-loggermessage-in-aspnet-core"></a>ASP.NET Core에서 LoggerMessage를 사용한 고성능 로깅

[Luke Latham](https://github.com/guardrex)으로

[LoggerMessage](/dotnet/api/microsoft.extensions.logging.loggermessage) 기능은 `LogInformation`, `LogDebug` 및 `LogError`와 같은 [로거 확장 메서드](/dotnet/api/Microsoft.Extensions.Logging.LoggerExtensions)에 비해 적은 개체 할당 및 감소된 계산 오버헤드를 필요로 하는 캐시 가능한 대리자를 만듭니다. 고성능 로깅 시나리오의 경우 `LoggerMessage` 패턴을 사용합니다.

`LoggerMessage`는 로거 확장 메서드에 비해 다음과 같은 성능 이점을 제공합니다.

* 로거 확장 메서드는 `object`에 대한 `int`와 같은 "boxing"(변환) 값 형식이 필요합니다. `LoggerMessage` 패턴은 정적 `Action` 필드 및 강력한 형식의 매개 변수가 있는 확장 메서드를 사용하여 boxing을 방지합니다.
* 로거 확장 메서드는 로그 메시지가 기록될 때마다 메시지 템플릿(명명된 형식 문자열)을 구문 분석해야 합니다. `LoggerMessage`는 메시지가 정의될 때 템플릿 구문 분석이 한번만 필요합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/loggermessage/sample/) ([다운로드 방법](xref:index#how-to-download-a-sample))

샘플 앱은 기본 견적 추적 시스템으로 `LoggerMessage` 기능을 보여 줍니다. 앱은 메모리 내 데이터베이스를 사용하여 견적을 추가하고 삭제합니다. 이러한 작업이 발생하는 대로 로그 메시지는 `LoggerMessage` 패턴을 사용하여 생성됩니다.

## <a name="loggermessagedefine"></a>LoggerMessage.Define

[Define(LogLevel, EventId, String)](/dotnet/api/microsoft.extensions.logging.loggermessage.define)은 메시지 로깅을 위한 `Action` 대리자를 만듭니다. `Define` 오버로드는 명명된 형식 문자열(템플릿)로 최대 6개의 형식 매개 변수 전달을 허용합니다.

`Define` 메서드에 제공된 문자열은 템플릿이며 보간된 문자열이 아닙니다. 자리 표시자는 형식이 지정된 순서로 채워집니다. 템플릿의 자리 표시자 이름은 템플릿에서 알기 쉽고 일관되어야 합니다. 구조적 로그 데이터 내에서 속성 이름으로 사용됩니다. 자리 표시자 이름으로 [파스칼식 대/소문자](/dotnet/standard/design-guidelines/capitalization-conventions)를 권장합니다. 예: `{Count}`, `{FirstName}`

각 로그 메시지는 `LoggerMessage.Define`에서 만들어진 정적 필드에 보관된 `Action`입니다. 예를 들어 샘플 앱은 인덱스 페이지의 GET 요청에 대한 로그 메시지를 설명하는 필드를 만듭니다(*Internal/LoggerExtensions.cs*).

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet1)]

`Action`의 경우 다음을 지정합니다.

* 로그 수준
* 정적 확장 메서드의 이름이 있는 고유한 이벤트 식별자([EventId](/dotnet/api/microsoft.extensions.logging.eventid))
* 메시지 템플릿(명명된 형식 문자열) 

샘플 앱의 인덱스 페이지에 대한 요청은 다음을 설정합니다.

* 로그 수준을 `Information`으로
* 이벤트 ID를 `IndexPageRequested` 메서드의 이름이 있는 `1`로
* 메시지 템플릿(명명된 형식 문자열)을 문자열로

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet5)]

구조적 로깅 저장소는 로깅을 보강하도록 이벤트 ID로 제공될 경우 이벤트 이름을 사용할 수 있습니다. 예를 들어 [Serilog](https://github.com/serilog/serilog-extensions-logging)는 이벤트 이름을 사용합니다.

`Action`은 강력한 형식의 확장 메서드를 통해 호출됩니다. `IndexPageRequested` 메서드는 샘플 앱에서 인덱스 페이지 GET 요청에 대한 메시지를 기록합니다.

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet9)]

`IndexPageRequested`는 *Pages/Index.cshtml.cs*에서 `OnGetAsync` 메서드의 로거에서 호출됩니다.

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=3)]

앱의 콘솔 출력을 검사합니다.

```console
info: LoggerMessageSample.Pages.IndexModel[1]
      => RequestId:0HL90M6E7PHK4:00000001 RequestPath:/ => /Index
      GET request for Index page
```

로그 메시지에 매개 변수를 전달하려면 정적 필드를 만들 때 최대 6개의 형식을 정의합니다. 샘플 앱은 `Action` 필드에 대한 `string` 형식을 정의하여 견적을 추가할 때 문자열을 기록합니다.

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet2)]

대리자의 로그 메시지 템플릿은 제공되는 형식에서 해당 자리 표시자 값을 받습니다. 샘플 앱은 견적 매개 변수가 `string`인 견적을 추가하기 위한 대리자를 정의합니다.

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet6)]

견적을 추가하기 위한 정적 확장 메서드, `QuoteAdded`는 견적 인수 값을 받고 `Action` 대리자에 전달합니다.

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet10)]

인덱스 페이지의 페이지 모델(*Pages/Index.cshtml.cs*)에서 `QuoteAdded`는 메시지를 기록하기 위해 호출됩니다.

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet3&highlight=6)]

앱의 콘솔 출력을 검사합니다.

```console
info: LoggerMessageSample.Pages.IndexModel[2]
      => RequestId:0HL90M6E7PHK5:0000000A RequestPath:/ => /Index
      Quote added (Quote = 'You can avoid reality, but you cannot avoid the consequences of avoiding reality. - Ayn Rand')
```

샘플 앱은 견적 삭제를 위한 `try`&ndash;`catch` 패턴을 구현합니다. 성공적인 삭제 작업에 대한 정보 메시지가 기록됩니다. 예외가 throw될 경우 삭제 작업에 대한 오류 메시지가 기록됩니다. 실패한 삭제 작업에 대한 로그 메시지는 예외 스택 추적(*Internal/LoggerExtensions.cs*)을 포함합니다.

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet3)]

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet7)]

`QuoteDeleteFailed`에서 예외가 대리자에 전달되는 방식을 참고합니다.

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet11)]

인덱스 페이지에 대한 페이지 모델에서 성공적인 견적 삭제는 로거에서 `QuoteDeleted` 메서드를 호출합니다. 삭제에 대한 견적을 찾을 수 없는 경우 `ArgumentNullException`이 throw됩니다. 예외는 `try`&ndash;`catch`문에 의해 트래핑되며 `catch` 블록에서 로거의 `QuoteDeleteFailed` 메서드를 호출하여 기록됩니다(*Pages/Index.cshtml.cs*).

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet5&highlight=14,18)]

견적이 성공적으로 삭제되면 앱의 콘솔 출력을 검사합니다.

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:00000016 RequestPath:/ => /Index
      Quote deleted (Quote = 'You can avoid reality, but you cannot avoid the consequences of avoiding reality. - Ayn Rand' Id = 1)
```

견적 삭제가 실패하면 앱의 콘솔 출력을 검사합니다. 예외는 로그 메시지에 포함되어 있습니다.

```console
fail: LoggerMessageSample.Pages.IndexModel[5]
      => RequestId:0HL90M6E7PHK5:00000010 RequestPath:/ => /Index
      Quote delete failed (Id = 999)
System.ArgumentNullException: Value cannot be null.
Parameter name: entity
   at Microsoft.EntityFrameworkCore.Utilities.Check.NotNull[T](T value, String parameterName)
   at Microsoft.EntityFrameworkCore.DbContext.Remove[TEntity](TEntity entity)
   at Microsoft.EntityFrameworkCore.Internal.InternalDbSet`1.Remove(TEntity entity)
   at LoggerMessageSample.Pages.IndexModel.<OnPostDeleteQuoteAsync>d__14.MoveNext() in 
      <PATH>\sample\Pages\Index.cshtml.cs:line 87
```

## <a name="loggermessagedefinescope"></a>LoggerMessage.DefineScope

[DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope)는 [로그 범위](xref:fundamentals/logging/index#log-scopes) 정의를 위한 `Func` 대리자를 만듭니다. `DefineScope` 오버로드는 명명된 형식 문자열(템플릿)로 최대 3개의 형식 매개 변수 전달을 허용합니다.

`Define` 메서드의 경우와 마찬가지로 `DefineScope` 메서드에 제공된 문자열은 템플릿이며 보간된 문자열이 아닙니다. 자리 표시자는 형식이 지정된 순서로 채워집니다. 템플릿의 자리 표시자 이름은 템플릿에서 알기 쉽고 일관되어야 합니다. 구조적 로그 데이터 내에서 속성 이름으로 사용됩니다. 자리 표시자 이름으로 [파스칼식 대/소문자](/dotnet/standard/design-guidelines/capitalization-conventions)를 권장합니다. 예: `{Count}`, `{FirstName}`

[DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) 메서드를 사용하여 일련의 로그 메시지에 적용하도록 [로그 범위](xref:fundamentals/logging/index#log-scopes)를 정의합니다.

샘플 앱에는 데이터베이스에서 모든 견적을 삭제하기 위한 **모두 지우기** 단추가 있습니다. 견적은 한 번에 하나를 제거하여 삭제됩니다. 견적이 삭제될 때마다 로거에서 `QuoteDeleted` 메서드가 호출됩니다. 로그 범위가 이러한 로그 메시지에 추가됩니다.

*appsettings.json*의 콘솔 로거 섹션에서 `IncludeScopes`를 사용하도록 설정합니다.

[!code-csharp[](loggermessage/sample/appsettings.json?highlight=3-5)]

로그 범위를 만들려면 범위에 대한 `Func` 대리자를 보유하는 필드를 추가합니다. 샘플 앱은 `_allQuotesDeletedScope`라는 필드를 만듭니다(*Internal/LoggerExtensions.cs*).

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet4)]

`DefineScope`를 사용하여 대리자를 만듭니다. 대리자가 호출되는 경우 템플릿 인수로 사용하기 위해 최대 세 개의 형식을 지정할 수 있습니다. 샘플 앱은 삭제된 견적의 수를 포함하는 메시지 템플릿을 사용합니다(`int` 형식).

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet8)]

로그 메시지에 대한 정적 확장 메서드를 제공합니다. 메시지 템플릿에 표시되는 명명된 속성에 대한 모든 형식 매개 변수를 포함합니다. 샘플 앱은 `_allQuotesDeletedScope`를 삭제하고 반환하는 데 `count`의 견적을 사용합니다.

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet12)]

범위는 `using` 블록에서 로깅 확장 호출을 래핑합니다.

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet4&highlight=5-6,14)]

앱의 콘솔 출력에서 로그 메시지를 검사합니다. 다음 결과는 포함된 로그 범위 메시지와 함께 삭제된 세 가지 견적을 보여 줍니다.

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 1' Id = 2)
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 2' Id = 3)
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 3' Id = 4)
```

## <a name="additional-resources"></a>추가 자료

* [로깅](xref:fundamentals/logging/index)
