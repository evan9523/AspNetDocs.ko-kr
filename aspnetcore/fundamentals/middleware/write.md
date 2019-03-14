---
title: 사용자 지정 ASP.NET Core 미들웨어 작성
author: rick-anderson
description: 사용자 지정 ASP.NET Core 미들웨어 작성 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 02/14/2019
uid: fundamentals/middleware/write
ms.openlocfilehash: 2c5577394a10370d92c8a83f9d806b63f3245c8b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57046240"
---
# <a name="write-custom-aspnet-core-middleware"></a>사용자 지정 ASP.NET Core 미들웨어 작성

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Steve Smith](https://ardalis.com/)

미들웨어는 요청 및 응답을 처리하는 앱 파이프라인으로 어셈블리되는 소프트웨어입니다. ASP.NET Core는 풍부한 기본 제공 미들웨어 구성 요소 세트를 제공하지만 일부 시나리오에서는 사용자 지정 미들웨어를 작성하려고 할 수 있습니다.

## <a name="middleware-class"></a>미들웨어 클래스

미들웨어는 일반적으로 클래스에서 캡슐화되고 확장 메서드로 노출됩니다. 쿼리 문자열에서 현재 요청에 대한 문화권을 설정하는 다음 미들웨어를 고려합니다.

[!code-csharp[](index/snapshot/Culture/StartupCulture.cs?name=snippet1)]

위의 샘플 코드는 미들웨어 구성 요소를 만드는 방법을 보여주는 데 사용됩니다. ASP.NET Core의 기본 제공 지역화 지원은 <xref:fundamentals/localization>을 참조하세요.

문화권을 전달하여 미들웨어를 테스트할 수 있습니다. 예를 들어, `http://localhost:7997/?culture=no`을 입력합니다.

다음 코드는 미들웨어 대리자를 클래스로 이동합니다.

[!code-csharp[](index/snapshot/Culture/RequestCultureMiddleware.cs)]

::: moniker range="< aspnetcore-2.0"

미들웨어 `Task` 메서드의 이름은 `Invoke`여야 합니다. ASP.NET 코어 2.0 이상에서는 이름이 `Invoke` 또는 `InvokeAsync`일 수 있습니다.

::: moniker-end

## <a name="middleware-extension-method"></a>미들웨어 확장 메서드

다음 확장 메서드는 <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder>를 통해 미들웨어를 공개합니다.

[!code-csharp[](index/snapshot/Culture/RequestCultureMiddlewareExtensions.cs)]

다음 코드는 `Startup.Configure`에서 미들웨어를 호출합니다.

[!code-csharp[](index/snapshot/Culture/Startup.cs?name=snippet1&highlight=5)]

미들웨어는 해당 생성자에서 해당 종속성을 노출하여 [명시적 종속성 원칙](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies)을 따라야 합니다. 미들웨어는 *애플리케이션 수명*당 한 번 생성됩니다. 요청 내에서 서비스를 미들웨어와 공유해야 하는 경우 [요청당 종속성](#per-request-dependencies) 섹션을 참조하세요.

미들웨어 구성 요소는 생성자 매개 변수를 통해 [DI(종속성 주입)](xref:fundamentals/dependency-injection)에서 해당 종속성을 확인할 수 있습니다. [UseMiddleware&lt;T&gt;](/dotnet/api/microsoft.aspnetcore.builder.usemiddlewareextensions.usemiddleware#Microsoft_AspNetCore_Builder_UseMiddlewareExtensions_UseMiddleware_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Type_System_Object___)는 추가 매개 변수를 직접 수락할 수도 있습니다.

## <a name="per-request-dependencies"></a>요청당 종속성

미들웨어는 요청당이 아닌 앱 시작 시 생성되므로 미들웨어 생성자에 의해 사용되는 *범위가 지정된* 수명 서비스는 각 요청 중에 다른 종속성 주입된 형식과 공유되지 않습니다. *범위가 지정된* 서비스를 미들웨어와 다른 형식 간에 공유해야 하는 경우 이러한 서비스를 `Invoke` 메서드의 서명에 추가합니다. `Invoke` 메서드는 DI로 채워지는 추가 매개 변수를 수락할 수 있습니다.

```csharp
public class CustomMiddleware
{
    private readonly RequestDelegate _next;

    public CustomMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    // IMyScopedService is injected into Invoke
    public async Task Invoke(HttpContext httpContext, IMyScopedService svc)
    {
        svc.MyProperty = 1000;
        await _next(httpContext);
    }
}
```

## <a name="additional-resources"></a>추가 자료

* <xref:fundamentals/middleware/index>
* <xref:migration/http-modules>
* <xref:fundamentals/startup>
* <xref:fundamentals/request-features>
* <xref:fundamentals/middleware/extensibility>
* <xref:fundamentals/middleware/extensibility-third-party-container>
