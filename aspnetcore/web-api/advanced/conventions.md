---
title: 웹 API 규칙 사용
author: pranavkm
description: ASP.NET Core에서 웹 API 규칙에 대해 알아봅니다.
monikerRange: '>= aspnetcore-2.2'
ms.author: scaddie
ms.custom: mvc
ms.date: 12/13/2018
uid: web-api/advanced/conventions
ms.openlocfilehash: 5ae96b213a19464045e1d0b1a76f8eb81089dc5b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029940"
---
# <a name="use-web-api-conventions"></a><span data-ttu-id="95473-103">웹 API 규칙 사용</span><span class="sxs-lookup"><span data-stu-id="95473-103">Use web API conventions</span></span>

<span data-ttu-id="95473-104">작성자: [Pranav Krishnamoorthy](https://github.com/pranavkm) 및 [Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="95473-104">By [Pranav Krishnamoorthy](https://github.com/pranavkm) and [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="95473-105">ASP.NET Core 2.2 이상에는 일반적인 [API 설명서](xref:tutorials/web-api-help-pages-using-swagger)를 추출하여 여러 작업, 컨트롤러 또는 어셈블리 내 모든 컨트롤러에 적용하는 방법이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95473-105">ASP.NET Core 2.2 and later includes a way to extract common [API documentation](xref:tutorials/web-api-help-pages-using-swagger) and apply it to multiple actions, controllers, or all controllers within an assembly.</span></span> <span data-ttu-id="95473-106">웹 API 규칙은 개별 작업을 [[ProducesResponseType]](xref:Microsoft.AspNetCore.Mvc.ProducesResponseTypeAttribute)으로 데코레이팅하는 대체자입니다.</span><span class="sxs-lookup"><span data-stu-id="95473-106">Web API conventions are a substitute for decorating individual actions with [[ProducesResponseType]](xref:Microsoft.AspNetCore.Mvc.ProducesResponseTypeAttribute).</span></span>

<span data-ttu-id="95473-107">규칙을 통해 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95473-107">A convention allows you to:</span></span>

* <span data-ttu-id="95473-108">특정 유형의 작업에서 반환되는 가장 일반적인 반환 형식 및 상태 코드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="95473-108">Define the most common return types and status codes returned from a specific type of action.</span></span>
* <span data-ttu-id="95473-109">정의된 표준에서 벗어나는 작업을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="95473-109">Identify actions that deviate from the defined standard.</span></span>

<span data-ttu-id="95473-110">ASP.NET Core MVC 2.2 이상에는 `Microsoft.AspNetCore.Mvc.DefaultApiConventions`의 기본 규칙 집합이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95473-110">ASP.NET Core MVC 2.2 and later includes a set of default conventions in `Microsoft.AspNetCore.Mvc.DefaultApiConventions`.</span></span> <span data-ttu-id="95473-111">규칙은 ASP.NET Core **API** 프로젝트 템플릿에서 제공되는 컨트롤러(*ValuesController.cs*)를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="95473-111">The conventions are based on the controller (*ValuesController.cs*) provided in the ASP.NET Core **API** project template.</span></span> <span data-ttu-id="95473-112">작업이 템플릿의 패턴을 따르는 경우, 기본 규칙을 성공적으로 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95473-112">If your actions follow the patterns in the template, you should be successful using the default conventions.</span></span> <span data-ttu-id="95473-113">기본 규칙이 요구 사항을 충족하지 못하는 경우 [웹 API 규칙 만들기](#create-web-api-conventions)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95473-113">If the default conventions don't meet your needs, see [Create web API conventions](#create-web-api-conventions).</span></span>

<span data-ttu-id="95473-114">런타임 시 <xref:Microsoft.AspNetCore.Mvc.ApiExplorer>가 규칙을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="95473-114">At runtime, <xref:Microsoft.AspNetCore.Mvc.ApiExplorer> understands conventions.</span></span> <span data-ttu-id="95473-115">`ApiExplorer`는 [OpenAPI](https://www.openapis.org/)(Swagger라고도 함) 문서 생성기와 통신하기 위한 MVC의 추상화입니다.</span><span class="sxs-lookup"><span data-stu-id="95473-115">`ApiExplorer` is MVC's abstraction to communicate with [OpenAPI](https://www.openapis.org/) (also known as Swagger) document generators.</span></span> <span data-ttu-id="95473-116">적용된 규칙의 특성은 작업과 연결되며 작업의 OpenAPI 설명서에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="95473-116">Attributes from the applied convention are associated with an action and are included in the action's OpenAPI documentation.</span></span> <span data-ttu-id="95473-117">[API 분석기](xref:web-api/advanced/analyzers)도 규칙을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="95473-117">[API analyzers](xref:web-api/advanced/analyzers) also understand conventions.</span></span> <span data-ttu-id="95473-118">작업이 색다른 경우(예를 들어 적용된 규칙에 의해 문서화되지 않은 상태 코드를 반환하는 경우) 경고는 상태 코드를 문서화할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="95473-118">If your action is unconventional (for example, it returns a status code that isn't documented by the applied convention), a warning encourages you to document the status code.</span></span>

<span data-ttu-id="95473-119">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/advanced/conventions/sample) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="95473-119">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/advanced/conventions/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="apply-web-api-conventions"></a><span data-ttu-id="95473-120">웹 API 규칙 적용</span><span class="sxs-lookup"><span data-stu-id="95473-120">Apply web API conventions</span></span>

<span data-ttu-id="95473-121">규칙이 구성되지 않으면 각 작업은 정확히 하나의 규칙과 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95473-121">Conventions don't compose; each action may be associated with exactly one convention.</span></span> <span data-ttu-id="95473-122">더 구체적인 규칙은 덜 구체적인 규칙보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="95473-122">More specific conventions take precedence over less specific conventions.</span></span> <span data-ttu-id="95473-123">동일한 우선순위의 둘 이상의 규칙이 작업에 적용되는 경우 선택은 명확하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95473-123">The selection is non-deterministic when two or more conventions of the same priority apply to an action.</span></span> <span data-ttu-id="95473-124">다음 옵션은 가장 구체적인 것에서 가장 덜 구체적인 것까지 작업에 규칙을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95473-124">The following options exist to apply a convention to an action, from the most specific to the least specific:</span></span>

1. <span data-ttu-id="95473-125">`Microsoft.AspNetCore.Mvc.ApiConventionMethodAttribute` &mdash; 개별 작업에 적용되며 규칙 형식 및 적용되는 규칙 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="95473-125">`Microsoft.AspNetCore.Mvc.ApiConventionMethodAttribute` &mdash; Applies to individual actions and specifies the convention type and the convention method that applies.</span></span>

    <span data-ttu-id="95473-126">다음 예제에서는 기본 규칙 유형의 `Microsoft.AspNetCore.Mvc.DefaultApiConventions.Put` 규칙 메서드가 `Update` 작업에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="95473-126">In the following example, the default convention type's `Microsoft.AspNetCore.Mvc.DefaultApiConventions.Put` convention method is applied to the `Update` action:</span></span>

    [!code-csharp[](conventions/sample/Controllers/ContactsConventionController.cs?name=snippet_ApiConventionMethod&highlight=3)]

    <span data-ttu-id="95473-127">`Microsoft.AspNetCore.Mvc.DefaultApiConventions.Put` 규칙 메서드는 다음 특성을 작업에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="95473-127">The `Microsoft.AspNetCore.Mvc.DefaultApiConventions.Put` convention method applies the following attributes to the action:</span></span>

    ```csharp
    [ProducesDefaultResponseType]
    [ProducesResponseType(204)]
    [ProducesResponseType(404)]
    [ProducesResponseType(400)]
    ```

<span data-ttu-id="95473-128">`[ProducesDefaultResponseType]`에 대한 자세한 내용은 [Default Response](https://swagger.io/docs/specification/describing-responses/#default)(기본 응답)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95473-128">For more information on `[ProducesDefaultResponseType]`, see [Default Response](https://swagger.io/docs/specification/describing-responses/#default).</span></span>

1. <span data-ttu-id="95473-129">&mdash; 컨트롤러에 `Microsoft.AspNetCore.Mvc.ApiConventionTypeAttribute`를 적용하면 컨트롤러에서 모든 작업에 지정된 규칙 유형을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="95473-129">`Microsoft.AspNetCore.Mvc.ApiConventionTypeAttribute` applied to a controller &mdash; Applies the specified convention type to all actions on the controller.</span></span> <span data-ttu-id="95473-130">규칙 메서드는 규칙 메서드가 적용되는 작업을 결정하는 힌트로 데코레이팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="95473-130">A convention method is decorated with hints that determine the actions to which the convention method applies.</span></span> <span data-ttu-id="95473-131">힌트에 대한 자세한 내용은 [웹 API 규칙 만들기](#create-web-api-conventions)를 참조하세요).</span><span class="sxs-lookup"><span data-stu-id="95473-131">For more information on hints, see [Create web API conventions](#create-web-api-conventions)).</span></span>

    <span data-ttu-id="95473-132">다음 예제에서는 *ContactsConventionController*의 모든 작업에 기본 규칙 집합이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="95473-132">In the following example, the default set of conventions is applied to all actions in *ContactsConventionController*:</span></span>

    [!code-csharp[](conventions/sample/Controllers/ContactsConventionController.cs?name=snippet_ApiConventionTypeAttribute&highlight=2)]

1. <span data-ttu-id="95473-133">&mdash; 어셈블리에 적용된 `Microsoft.AspNetCore.Mvc.ApiConventionTypeAttribute`는 현재 어셈블리의 모든 컨트롤러에 지정된 규칙 유형을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="95473-133">`Microsoft.AspNetCore.Mvc.ApiConventionTypeAttribute` applied to an assembly &mdash; Applies the specified convention type to all controllers in the current assembly.</span></span> <span data-ttu-id="95473-134">권장 사항으로 어셈블리 수준 특성을 *Startup.cs* 파일에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="95473-134">As a recommendation, apply assembly-level attributes in the *Startup.cs* file.</span></span>

    <span data-ttu-id="95473-135">다음 예제에서는 기본 규칙 집합이 어셈블리의 모든 컨트롤러에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="95473-135">In the following example, the default set of conventions is applied to all controllers in the assembly:</span></span>

    [!code-csharp[](conventions/sample/Startup.cs?name=snippet_ApiConventionTypeAttribute&highlight=1)]

## <a name="create-web-api-conventions"></a><span data-ttu-id="95473-136">웹 API 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="95473-136">Create web API conventions</span></span>

<span data-ttu-id="95473-137">기본 API 규칙이 요구 사항을 충족하지 못하는 경우 고유한 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95473-137">If the default API conventions don't meet your needs, create your own conventions.</span></span> <span data-ttu-id="95473-138">규칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="95473-138">A convention is:</span></span>

* <span data-ttu-id="95473-139">메서드가 있는 정적 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="95473-139">A static type with methods.</span></span>
* <span data-ttu-id="95473-140">작업에 [응답 형식](#response-types) 및 [명명 요구 사항](#naming-requirements)을 정의하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95473-140">Capable of defining [response types](#response-types) and [naming requirements](#naming-requirements) on actions.</span></span>

### <a name="response-types"></a><span data-ttu-id="95473-141">응답 형식</span><span class="sxs-lookup"><span data-stu-id="95473-141">Response types</span></span>

<span data-ttu-id="95473-142">이러한 메서드에는 `[ProducesResponseType]` 또는 `[ProducesDefaultResponseType]` 특성으로 주석이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="95473-142">These methods are annotated with `[ProducesResponseType]` or `[ProducesDefaultResponseType]` attributes.</span></span> <span data-ttu-id="95473-143">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="95473-143">For example:</span></span>

```csharp
public static class MyAppConventions
{
    [ProducesResponseType(200)]
    [ProducesResponseType(404)]
    public static void Find(int id)
    {
    }
}
```

<span data-ttu-id="95473-144">보다 구체적인 메타데이터 특성이 없는 경우 이 규칙을 어셈블리에 적용하면 다음과 같이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="95473-144">If more specific metadata attributes are absent, applying this convention to an assembly enforces that:</span></span>

* <span data-ttu-id="95473-145">규칙 메서드는 `Find`라는 작업에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="95473-145">The convention method applies to any action named `Find`.</span></span>
* <span data-ttu-id="95473-146">`id`라는 매개 변수는 `Find` 작업에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95473-146">A parameter named `id` is present on the `Find` action.</span></span>

### <a name="naming-requirements"></a><span data-ttu-id="95473-147">이름 지정 요구 사항</span><span class="sxs-lookup"><span data-stu-id="95473-147">Naming requirements</span></span>

<span data-ttu-id="95473-148">`[ApiConventionNameMatch]` 및 `[ApiConventionTypeMatch]` 특성은 적용할 작업을 결정하는 규칙 메서드에 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95473-148">The `[ApiConventionNameMatch]` and `[ApiConventionTypeMatch]` attributes can be applied to the convention method that determines the actions to which they apply.</span></span> <span data-ttu-id="95473-149">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="95473-149">For example:</span></span>

```csharp
[ProducesResponseType(200)]
[ProducesResponseType(404)]
[ApiConventionNameMatch(ApiConventionNameMatchBehavior.Prefix)]
public static void Find(
    [ApiConventionNameMatch(ApiConventionNameMatchBehavior.Suffix)]
    int id)
{ }
```

<span data-ttu-id="95473-150">앞의 예제에서:</span><span class="sxs-lookup"><span data-stu-id="95473-150">In the preceding example:</span></span>

* <span data-ttu-id="95473-151">메서드에 적용된 `Microsoft.AspNetCore.Mvc.ApiExplorer.ApiConventionNameMatchBehavior.Prefix` 옵션은 규칙이 "찾기"로 접두사가 지정된 모든 작업과 일치함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="95473-151">The `Microsoft.AspNetCore.Mvc.ApiExplorer.ApiConventionNameMatchBehavior.Prefix` option applied to the method indicates that the convention matches any action prefixed with "Find".</span></span> <span data-ttu-id="95473-152">일치하는 작업의 예로는 `Find`, `FindPet` 및 `FindById`가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95473-152">Examples of matching actions include `Find`, `FindPet`, and `FindById`.</span></span>
* <span data-ttu-id="95473-153">매개 변수에 적용된 `Microsoft.AspNetCore.Mvc.ApiExplorer.ApiConventionNameMatchBehavior.Suffix`는 규칙이 접미사 식별자로 끝나는 정확히 하나의 매개 변수와 메서드가 일치함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="95473-153">The `Microsoft.AspNetCore.Mvc.ApiExplorer.ApiConventionNameMatchBehavior.Suffix` applied to the parameter indicates that the convention matches methods with exactly one parameter ending in the suffix identifier.</span></span> <span data-ttu-id="95473-154">예제에는 `id` 또는 `petId`와 같은 매개 변수가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="95473-154">Examples include parameters such as `id` or `petId`.</span></span> <span data-ttu-id="95473-155">`ApiConventionTypeMatch`는 매개 변수 유형을 제한하는 형식에 유사하게 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95473-155">`ApiConventionTypeMatch` can be similarly applied to types to constrain the parameter type.</span></span> <span data-ttu-id="95473-156">`params[]` 인수는 명시적으로 일치할 필요가 없는 나머지 매개 변수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="95473-156">A `params[]` argument indicates remaining parameters that don't need to be explicitly matched.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="95473-157">추가 자료</span><span class="sxs-lookup"><span data-stu-id="95473-157">Additional resources</span></span>

* <xref:web-api/advanced/analyzers>
* <xref:tutorials/web-api-help-pages-using-swagger>
