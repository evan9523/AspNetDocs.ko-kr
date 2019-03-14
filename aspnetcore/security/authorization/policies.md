---
title: ASP.NET Core의 정책 기반 권한 부여
author: rick-anderson
description: ASP.NET Core 응용 프로그램에서 사용자 지정 권한 정책 처리기를 작성 및 사용해서 권한 부여 요구 사항을 적용하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 11/21/2017
uid: security/authorization/policies
ms.openlocfilehash: be4812487c92a16c44e3983b234bc9e31be65190
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57043620"
---
# <a name="policy-based-authorization-in-aspnet-core"></a>ASP.NET Core의 정책 기반 권한 부여

[역할 기반 권한 부여](xref:security/authorization/roles) 및 [클레임 기반 권한 부여](xref:security/authorization/claims) 는 내부적으로 요구 사항, 요구 사항 처리기, 그리고 미리 구성된 정책을 사용합니다. 이런 빌딩 블록들은 권한 부여 평가를 코드로 표현할 수 있는 기능을 지원합니다. 결과적으로 보다 풍부하고 재사용 가능하며 테스트 가능한 권한 부여 구조를 만들 수 있습니다.

권한 부여 정책은 하나 이상의 요구 사항으로 구성됩니다. 그리고 `Startup.ConfigureServices`에서 권한 부여 서비스 구성의 일부로 등록됩니다.

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=40-41,50-55,63,72)]

위의 예제는 "AtLeast21"이라는 정책을 생성합니다. 이 정책은 요구 사항의 &mdash; 매개 변수로 제공되는, 최소 연령을 뜻하는 단일 요구 사항을 갖습니다.

정책은 정책 이름이 지정된 `[Authorize]` 특성을 통해서 적용됩니다. 예를 들어 다음과 같습니다.

[!code-csharp[](policies/samples/PoliciesAuthApp1/Controllers/AlcoholPurchaseController.cs?name=snippet_AlcoholPurchaseControllerClass&highlight=4)]

## <a name="requirements"></a>요구 사항

권한 부여 요구 사항은 현재 사용자 보안 주체를 평가 하는 정책을 사용할 수 있는 데이터 매개 변수의 컬렉션입니다. 요구 사항인 단일 매개 변수는 "AtLeast21" 정책에서&mdash;최소 보존 기간입니다. 요구 사항 구현 [IAuthorizationRequirement](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationrequirement), 빈 표식을 인터페이스인 합니다. 매개 변수가 있는 최소 보존 기간 요구 사항이 다음과 같이 구현할 수 있습니다.

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Requirements/MinimumAgeRequirement.cs?name=snippet_MinimumAgeRequirementClass)]

권한 부여 정책에 여러 권한 부여 요구 사항이 있으면 모든 요구 사항을 정책 평가가 성공 하기 위해 전달 해야 합니다. 에 단일 권한 부여 정책에 추가 하는 여러 권한 부여 요구 사항을 처리 되는 즉, 한 **AND** 단위로 합니다.

> [!NOTE]
> 요구 사항이 데이터나 속성을 가져야 할 필요는 없습니다.

<a name="security-authorization-policies-based-authorization-handler"></a>

## <a name="authorization-handlers"></a>권한 부여 처리기

권한 부여 처리기는 요구 사항의 속성을 평가하는 역할을 담당합니다. 권한 부여 처리기는 제공된 [AuthorizationHandlerContext](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext)에 대해 요구 사항을 평가하여 접근 허용 여부를 결정합니다.

하나의 요구 사항에 [여러 개의 처리기](#security-authorization-policies-based-multiple-handlers) 가 존재할 수 있습니다. 처리기는 [AuthorizationHandler\<TRequirement>](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandler-1)를 상속받으며, 여기서 `TRequirement` 는 처리해야 할 요구 사항입니다. 또는 처리기를 구현할 수 있습니다 [IAuthorizationHandler](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationhandler) 요구 사항 둘 이상의 유형을 처리 하도록 합니다.

### <a name="use-a-handler-for-one-requirement"></a>한 가지 요구 사항에 대한 처리기 사용하기

<a name="security-authorization-handler-example"></a>

다음은 최소 연령 처리기에서 단일 요구 사항을 사용하는 일대일 관계의 예제입니다.

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/MinimumAgeHandler.cs?name=snippet_MinimumAgeHandlerClass)]

이 코드는 먼저 현재 사용자의 신원이 우리가 알고 있고 신뢰할 수 있는 발급자로부터 발급된 생년월일 클레임을 갖고 있는지부터 확인합니다. 만약 클레임이 누락되었다면 권한을 부여할 수 없으므로 완료된 작업이 반환됩니다. 반면 클레임이 존재할 경우, 사용자의 나이가 계산됩니다. 그리고 나이가 요구 사항에 의해 정의된 최소 연령을 만족할 경우 권한 부여가 성공한 것으로 간주됩니다. 권한 부여에 성공하면 만족한 요구 사항을 유일한 매개 변수로 전달하여 `context.Succeed`를 호출합니다.

### <a name="use-a-handler-for-multiple-requirements"></a>여러 요구 사항에 대한 처리기 사용하기

다음은 권한 처리기는 세 가지 유형의 요구 사항 처리할 수 있습니다-다 관계의 예입니다.

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/PermissionHandler.cs?name=snippet_PermissionHandlerClass)]

앞의 코드를 통과 [PendingRequirements](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.pendingrequirements#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_PendingRequirements)&mdash;성공으로 표시 되지 않습니다 요구 사항을 포함 하는 속성입니다. 에 대 한는 `ReadPermission` 요구 사항, 소유자 또는 스폰서 요청 된 리소스에 액세스 하는 사용자 여야 합니다. 경우에 `EditPermission` 또는 `DeletePermission` 요구 사항, 자신이 요청한 리소스에 액세스 하려면 소유자 여야 합니다.

<a name="security-authorization-policies-based-handler-registration"></a>

### <a name="handler-registration"></a>처리기 등록하기

처리기는 구성 과정 중 서비스 컬렉션에 등록됩니다. 예를 들어 다음과 같습니다.

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=40-41,50-55,63-65,72)]

각 처리기는 `services.AddSingleton<IAuthorizationHandler, YourHandlerClass>();` 호출을 통해서 서비스 컬렉션에 추가됩니다.

## <a name="what-should-a-handler-return"></a>처리기가 반환해야 하는 결과는?

본문의 [처리기 예제](#security-authorization-handler-example)에서 `Handle` 메서드가 아무런 값도 반환하지 않는다는 점에 주목하시기 바랍니다. 그렇다면 성공 혹은 실패 여부는 어떻게 확인할 수 있을까요?

* 처리기는 성공적으로 검증된 요구 사항을 `context.Succeed(IAuthorizationRequirement requirement)`에 매개 변수로 전달하여 호출함으로써 성공했음을 나타냅니다.

* 일반적으로 처리기는 실패를 처리할 필요가 없는데, 동일한 요구 사항에 대한 다른 처리기가 성공할 수도 있기 때문입니다.

* 다른 처리기의 성공 여부와 관계없이 무조건 실패한 것으로 나타내려면 `context.Fail`을 호출합니다.

[InvokeHandlersAfterFailure](/dotnet/api/microsoft.aspnetcore.authorization.authorizationoptions.invokehandlersafterfailure#Microsoft_AspNetCore_Authorization_AuthorizationOptions_InvokeHandlersAfterFailure) 속성이 (ASP.NET Core 1.1 이상에서 사용 가능) `false`로 설정되면 `context.Fail`이 호출될 경우 나머지 처리기들의 실행이 중단되고 즉시 빠져나갑니다. `InvokeHandlersAfterFailure`의 기본값은 `true`로, 이 경우 모든 처리기가 호출됩니다. 따라서 다른 처리기에서 `context.Fail`이 호출되는 경우에도, 로깅 같은 요구 사항의 부수적인 작업은 항상 수행됩니다.

<a name="security-authorization-policies-based-multiple-handlers"></a>

## <a name="why-would-i-want-multiple-handlers-for-a-requirement"></a>요구 사항에 대해 여러 개의 처기리가 필요한 이유는?

만약 **OR** 기반의 평가를 수행하고 싶다면 단일 요구 사항에 대해 여러 개의 처리기를 구현해야 합니다. 예를 들어, Microsoft에는 키 카드로만 열 수 있는 문이 있습니다. 만약 키 카드를 집에 두고 왔다면 접수원이 임시 스티커를 인쇄하고 대신 문을 열어줍니다. 이 시나리오의 경우, 요구 사항은 *BuildingEntry* 하나지만 여러 처리기가 단일 요구 사항을 각각 개별적으로 검토하게 됩니다.

*BuildingEntryRequirement.cs*

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Requirements/BuildingEntryRequirement.cs?name=snippet_BuildingEntryRequirementClass)]

*BadgeEntryHandler.cs*

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/BadgeEntryHandler.cs?name=snippet_BadgeEntryHandlerClass)]

*TemporaryStickerHandler.cs*

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/TemporaryStickerHandler.cs?name=snippet_TemporaryStickerHandlerClass)]

두 처리기가 모두 [등록되어 있는지](xref:security/authorization/policies#security-authorization-policies-based-handler-registration) 확인합니다. 정책이 `BuildingEntryRequirement` 를 평가할 때, 두 처리기 중 하나라도 성공하면 정책 평가가 성공한 것으로 간주됩니다.

## <a name="using-a-func-to-fulfill-a-policy"></a>func를 이용해서 정책 구성하기

코드로 정책을 표현해서 구성하는 편이 더 간단한 경우도 있습니다. 정책을 구성할 때 `RequireAssertion` 정책 빌더에 `Func<AuthorizationHandlerContext, bool>`을 전달할 수 있습니다.

예를 들어 이전 `BadgeEntryHandler`를 다음과 같이 다시 작성할 수도 있습니다.

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=52-53,57-63)]

## <a name="accessing-mvc-request-context-in-handlers"></a>처리기에서 MVC 요청 컨텍스트 접근하기

권한 부여 처리기에서 구현해야 하는 `HandleRequirementAsync` 메서드에는 `AuthorizationHandlerContext`와 처리해야 할 대상인 `TRequirement`라는 두 개의 매개 변수가 존재합니다. MVC나 Jabbr 같은 프레임워크는 `AuthorizationHandlerContext`의 `Resource` 속성에 자유롭게 개체를 추가해서 추가적인 정보를 전달할 수 있습니다.

예를 들어, MVC는 `Resource` 속성에 [AuthorizationFilterContext](/dotnet/api/?term=AuthorizationFilterContext)의 인스턴스를 전달합니다. 이 속성은 `HttpContext`나 `RouteData`를 비롯한, MVC 및 Razor 페이지가 제공하는 다양한 정보들에 대한 접근을 제공합니다.

`Resource` 속성을 사용하는 방식은 프레임워크에 따라서 달라집니다. 따라서 `Resource` 속성의 정보를 사용할 경우 권한 부여 정책이 특정 프레임워크를 대상으로 제한될 수 있습니다. 캐스팅 해야 합니다 `Resource` 사용 하 여 속성을 `is` 키워드를 하 고 확인 코드 충돌 하지 않도록 하려면 캐스팅 했습니다 사용 하 여는 `InvalidCastException` 다른 프레임 워크에서 실행할 때:

```csharp
// Requires the following import:
//     using Microsoft.AspNetCore.Mvc.Filters;
if (context.Resource is AuthorizationFilterContext mvcContext)
{
    // Examine MVC-specific things like routing data.
}
```
