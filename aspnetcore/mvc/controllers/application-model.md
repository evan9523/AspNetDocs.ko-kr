---
title: ASP.NET Core에서 애플리케이션 모델 작업
author: ardalis
description: MVC 요소가 ASP.NET Core에서 작동하는 방법을 수정하려면 애플리케이션 모델을 읽고 조작하는 방법을 알아봅니다.
ms.author: riande
ms.date: 10/14/2016
uid: mvc/controllers/application-model
ms.openlocfilehash: f3e0aafa3e6a352c632e4abbf3943be61f11ea81
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57034960"
---
# <a name="work-with-the-application-model-in-aspnet-core"></a>ASP.NET Core에서 애플리케이션 모델 작업

작성자: [Steve Smith](https://ardalis.com/)

ASP.NET Core MVC는 MVC 앱의 구성 요소를 나타내는 *애플리케이션 모델*을 정의합니다. 이 모델을 읽고 조작하여 MVC 요소의 작동 방법을 수정할 수 있습니다. 기본적으로 MVC는 컨트롤러로 간주되는 클래스, 작업할 해당 클래스의 메서드 및 매개 변수 및 라우팅 작동 방법을 결정하는 특정 규칙을 따릅니다. 고유한 규칙을 만들고 전역으로 또는 특성으로 적용하여 앱의 요구 사항에 맞게 이 동작을 사용자 지정할 수 있습니다.

## <a name="models-and-providers"></a>모델 및 공급자

ASP.NET Core MVC 애플리케이션 모델에는 MVC 애플리케이션을 설명하는 추상 인터페이스 및 구체적인 구현 클래스가 모두 포함됩니다. 이 모델은 기본 규칙에 따라 앱의 컨트롤러, 작업, 작업 매개 변수, 경로 및 필터를 검색하는 MVC의 결과입니다. 애플리케이션 모델을 사용하여 기본 MVC 동작에서 다른 규칙을 따르도록 앱을 수정할 수 있습니다. 매개 변수, 이름, 경로 및 필터는 모두 작업 및 컨트롤러에 대한 구성 데이터로 사용됩니다.

ASP.NET Core MVC 애플리케이션 모델의 구조는 다음과 같습니다.

* ApplicationModel
    * 컨트롤러(ControllerModel)
        * 작업(ActionModel)
            * 매개 변수(ParameterModel)

모델의 각 수준에는 공통 `Properties` 컬렉션에 대한 액세스 권한이 있습니다. 하위 수준은 계층의 상위 수준에서 설정된 속성 값에 액세스하고 해당 값을 덮어쓸 수 있습니다. 속성은 작업을 만들 때 `ActionDescriptor.Properties`에 유지됩니다. 그러면 요청을 처리 중인 경우 규칙에서 추가하거나 수정한 모든 속성은 `ActionContext.ActionDescriptor.Properties`를 통해 액세스될 수 있습니다. 작업 기준으로 필터, 모델 바인더 등을 구성할 때 속성을 사용하는 것이 좋습니다.

> [!NOTE]
> 앱 시작이 완료되면 `ActionDescriptor.Properties` 컬렉션은 스레드에 대해 안전하지 않습니다(쓰기의 경우). 데이터를 안전하게 이 컬렉션에 추가할 때 규칙을 사용하는 것이 좋습니다.

### <a name="iapplicationmodelprovider"></a>IApplicationModelProvider

ASP.NET Core MVC는 공급자 패턴을 사용하여 애플리케이션 모델을 로드하며 [IApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.iapplicationmodelprovider) 인터페이스에 의해 정의됩니다. 이 섹션에서는 이 공급자가 작동하는 방법에 대한 내부 구현 세부 정보 중 일부를 다룹니다. 규칙을 사용하여 애플리케이션 모델을 활용하는 대부분의 앱이 수행해야 하는 고급 항목입니다.

`IApplicationModelProvider` 인터페이스의 구현은 서로 "래핑"합니다. 이 때 각 구현은 해당 `Order` 속성에 따라 오름차순으로 `OnProvidersExecuting`를 호출합니다. `OnProvidersExecuted` 메서드는 역순으로 호출됩니다. 프레임워크는 여러 공급자를 정의합니다.

First(`Order=-1000`):

* [`DefaultApplicationModelProvider`](/dotnet/api/microsoft.aspnetcore.mvc.internal.defaultapplicationmodelprovider)

Then(`Order=-990`):

* [`AuthorizationApplicationModelProvider`](/dotnet/api/microsoft.aspnetcore.mvc.internal.authorizationapplicationmodelprovider)
* [`CorsApplicationModelProvider`](/dotnet/api/microsoft.aspnetcore.mvc.cors.internal.corsapplicationmodelprovider)

> [!NOTE]
> `Order`에 대해 같은 값을 가진 두 공급자를 호출하는 순서는 정의되지 않으며 따라서 사용하지 않아야 합니다.

> [!NOTE]
> `IApplicationModelProvider`는 확장할 프레임워크 작성자를 위한 고급 개념입니다. 일반적으로 앱은 규칙을 사용해야 하고 프레임워크는 공급자를 사용해야 합니다. 중요한 차이점은 공급자가 항상 규칙 이전에 실행된다는 점입니다.

`DefaultApplicationModelProvider`는 ASP.NET Core MVC에서 사용하는 대부분의 기본 동작을 설정합니다. 해당 책임은 다음과 같습니다.

* 컨텍스트에 전역 필터 추가
* 컨텍스트에 컨트롤러 추가
* 작업으로 공용 컨트롤러 메서드 추가
* 컨텍스트에 작업 메서드 매개 변수 추가
* 경로 및 기타 특성 적용

일부 기본 제공 동작은 `DefaultApplicationModelProvider`에 의해 구현됩니다. 이 공급자는 [`ControllerModel`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.controllermodel)을 구성할 책임이 있습니다. 여기서는 [`ActionModel`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.actionmodel#Microsoft_AspNetCore_Mvc_ApplicationModels_ActionModel), [`PropertyModel`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.propertymodel) 및 [`ParameterModel`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.parametermodel#Microsoft_AspNetCore_Mvc_ApplicationModels_ParameterModel) 인스턴스를 차례로 참조합니다. `DefaultApplicationModelProvider` 클래스는 나중에 변경될 수 있는 내부 프레임워크 구현 세부 정보입니다. 

`AuthorizationApplicationModelProvider`는 `AuthorizeFilter` 및 `AllowAnonymousFilter` 특성과 연결된 동작을 적용할 책임이 있습니다. [이러한 특성에 대한 자세한 정보](xref:security/authorization/simple)

`CorsApplicationModelProvider`는 `IEnableCorsAttribute`, `IDisableCorsAttribute` 및 `DisableCorsAuthorizationFilter`와 연결된 동작을 구현합니다. [CORS에 대해 자세히 알아봅니다](xref:security/cors).

## <a name="conventions"></a>규칙

애플리케이션 모델은 전체 모델 또는 공급자를 재정의하기 보다는 모델의 동작을 사용자 지정하는 간단한 방법을 제공하는 규칙 추상화를 정의합니다. 앱의 동작을 수정할 때 이러한 추상화를 사용하는 것이 좋습니다. 규칙은 사용자 지정을 동적으로 적용하는 코드를 작성할 수 있는 방법을 제공합니다. [필터](xref:mvc/controllers/filters)는 프레임워크의 동작을 수정하는 방법을 제공하는 반면, 사용자 지정을 통해 전체 앱을 함께 연결하는 방법을 제어할 수 있습니다.

사용할 수 있는 규칙은 다음과 같습니다.

* [`IApplicationModelConvention`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.iapplicationmodelconvention)
* [`IControllerModelConvention`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.icontrollermodelconvention)
* [`IActionModelConvention`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.iactionmodelconvention)
* [`IParameterModelConvention`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.iparametermodelconvention)

MVC 옵션을 추가하거나 `Attribute`를 구현하고 컨트롤러, 작업 또는 작업 매개 변수([`Filters`](xref:mvc/controllers/filters)와 유사)에 적용하여 규칙을 적용합니다. 필터와 달리 각 요청의 일부가 아니라 앱을 시작하는 경우에만 규칙이 실행됩니다.

### <a name="sample-modifying-the-applicationmodel"></a>예제: Applicationmodel 수정

다음 규칙은 애플리케이션 모델에 속성을 추가하는 데 사용됩니다. 

[!code-csharp[](./application-model/sample/src/AppModelSample/Conventions/ApplicationDescription.cs)]

`Startup`의 `ConfigureServices`에 MVC를 추가할 경우 옵션으로 애플리케이션 모델 규칙을 적용합니다.

[!code-csharp[](./application-model/sample/src/AppModelSample/Startup.cs?name=ConfigureServices&highlight=5)]

속성은 컨트롤러 작업 내의 `ActionDescriptor` 속성 컬렉션에서 액세스할 수 있습니다.

[!code-csharp[](./application-model/sample/src/AppModelSample/Controllers/AppModelController.cs?name=AppModelController)]

### <a name="sample-modifying-the-controllermodel-description"></a>예제: ControllerModel 설명 수정

이전의 예제처럼 컨트롤러 모델은 사용자 지정 속성을 포함하도록 수정될 수도 있습니다. 그러면 애플리케이션 모델에 지정된 동일한 이름을 가진 기존 속성을 덮어씁니다. 다음과 같은 규칙 특성은 컨트롤러 수준에서 설명을 추가합니다.

[!code-csharp[](./application-model/sample/src/AppModelSample/Conventions/ControllerDescriptionAttribute.cs)]

이 규칙은 컨트롤러에 대한 특성으로 적용됩니다.

[!code-csharp[](./application-model/sample/src/AppModelSample/Controllers/DescriptionAttributesController.cs?name=ControllerDescription&highlight=1)]

이전 예제와 같이 동일한 방식으로 "설명" 속성에 액세스합니다.

### <a name="sample-modifying-the-actionmodel-description"></a>예제: ActionModel 설명 수정

개별 작업에 별도의 특성 규칙을 적용할 수 있습니다. 그러면 이미 애플리케이션 또는 컨트롤러 수준에서 적용되는 동작을 재정의합니다.

[!code-csharp[](./application-model/sample/src/AppModelSample/Conventions/ActionDescriptionAttribute.cs)]

이전 예제의 컨트롤러 내에 있는 작업에 이를 적용하면 컨트롤러 수준 규칙을 재정의하는 방법을 보여줍니다.

[!code-csharp[](./application-model/sample/src/AppModelSample/Controllers/DescriptionAttributesController.cs?name=DescriptionAttributesController&highlight=9)]

### <a name="sample-modifying-the-parametermodel"></a>예제: Parametermodel 수정

`BindingInfo`를 수정하는 작업 매개 변수에 다음 규칙을 적용할 수 있습니다. 다음과 같은 규칙의 매개 변수는 경로 매개 변수여야 합니다. 다른 잠재적인 바인딩 소스(예: 쿼리 문자열 값)는 무시됩니다.

[!code-csharp[](./application-model/sample/src/AppModelSample/Conventions/MustBeInRouteParameterModelConvention.cs)]

특성이 모든 작업 매개 변수에 적용될 수 있습니다.

[!code-csharp[](./application-model/sample/src/AppModelSample/Controllers/ParameterModelController.cs?name=ParameterModelController&highlight=5)]

### <a name="sample-modifying-the-actionmodel-name"></a>예제: ActionModel 이름 수정

다음 규칙은 적용되는 작업의 *이름*을 업데이트하도록 `ActionModel`을 수정합니다. 특성에 대한 매개 변수로 새 이름이 제공됩니다. 라우팅에서 이 새 이름을 사용하므로 이 작업 메서드에 연결하는 데 사용된 경로에 영향을 줍니다.

[!code-csharp[](./application-model/sample/src/AppModelSample/Conventions/CustomActionNameAttribute.cs)]

이 특성은 `HomeController`에서 작업 메서드에 적용됩니다.

[!code-csharp[](./application-model/sample/src/AppModelSample/Controllers/HomeController.cs?name=ActionModelConvention&highlight=2)]

메서드 이름이 `SomeName`이지만 특성은 메서드 이름을 사용하는 MVC 규칙을 재정의하 작업 이름을 `MyCoolAction`으로 바꿉니다. 따라서 이 작업에 도달하는 데 사용된 경로는 `/Home/MyCoolAction`입니다.

> [!NOTE]
> 이 예제는 기본적으로 기본 제공 [ActionName](/dotnet/api/microsoft.aspnetcore.mvc.actionnameattribute) 특성을 사용하는 것과 같습니다.

### <a name="sample-custom-routing-convention"></a>예제: 사용자 지정 라우팅 규칙

`IApplicationModelConvention`을 사용하여 라우팅 작동 방법을 사용자 지정할 수 있습니다. 예를 들어 다음 규칙은 컨트롤러의 네임스페이스를 해당 경로에 통합하고 네임스페이스의 `.`를 경로의 `/`로 바꿉니다.

[!code-csharp[](./application-model/sample/src/AppModelSample/Conventions/NamespaceRoutingConvention.cs)]

규칙은 시작에서 옵션으로 추가됩니다.

[!code-csharp[](./application-model/sample/src/AppModelSample/Startup.cs?name=ConfigureServices&highlight=6)]

> [!TIP]
> `services.Configure<MvcOptions>(c => c.Conventions.Add(YOURCONVENTION));`를 사용하는 `MvcOptions`에 액세스하여 [미들웨어](xref:fundamentals/middleware/index)에 규칙을 추가할 수 있습니다.

이 샘플에서는 컨트롤러의 이름에 "네임스페이스"가 있는 특성 라우팅을 사용하지 않는 경로에 이 규칙을 적용합니다. 다음 컨트롤러에서는 이 규칙을 보여줍니다.

[!code-csharp[](./application-model/sample/src/AppModelSample/Controllers/NamespaceRoutingController.cs?highlight=7-8)]

## <a name="application-model-usage-in-webapicompatshim"></a>WebApiCompatShim의 애플리케이션 모델 사용

ASP.NET Core MVC는 ASP.NET Web API 2에서 다른 규칙 집합을 사용합니다. 사용자 지정 규칙을 사용하여 Web API 앱의 해당 값과 일치되도록 ASP.NET Core MVC 앱의 동작을 수정할 수 있습니다. Microsoft는 이를 위해 [WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim/)을 제공합니다.

> [!NOTE]
> [ASP.NET Web API에서 마이그레이션](xref:migration/webapi)에 대해 자세히 알아봅니다.

Web API 호환성 Shim을 사용하려면 프로젝트에 패키지를 추가한 다음, `Startup`에서 `AddWebApiConventions`를 호출하여 MVC에 규칙을 추가해야 합니다.

```csharp
services.AddMvc().AddWebApiConventions();
```

shim에서 제공하는 규칙은 특정 특성에 적용되는 앱의 일부에만 적용됩니다. 다음과 같은 네 가지 특성이 컨트롤에 사용됩니다. 여기서 컨트롤러는 shim의 규칙에 의해 수정된 규칙을 포함해야 합니다.

* [UseWebApiActionConventionsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.webapicompatshim.usewebapiactionconventionsattribute)
* [UseWebApiOverloadingAttribute](/dotnet/api/microsoft.aspnetcore.mvc.webapicompatshim.usewebapioverloadingattribute)
* [UseWebApiParameterConventionsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.webapicompatshim.usewebapiparameterconventionsattribute)
* [UseWebApiRoutesAttribute](/dotnet/api/microsoft.aspnetcore.mvc.webapicompatshim.usewebapiroutesattribute)

### <a name="action-conventions"></a>작업 규칙

`UseWebApiActionConventionsAttribute`는 이름에 따라 작업에 HTTP 메서드를 매핑하는 데 사용됩니다(예: `Get`은 `HttpGet`에 매핑됨). 특성 라우팅을 사용하지 않는 작업에만 적용됩니다.

### <a name="overloading"></a>오버로딩

`UseWebApiOverloadingAttribute`는 `WebApiOverloadingApplicationModelConvention` 규칙을 적용하는 데 사용됩니다. 이 규칙은 작업 선택 프로세스에 `OverloadActionConstraint`를 추가합니다. 그러면 요청이 모든 필수 매개 변수를 충족하기 때문에 해당 작업에 대한 후보 작업을 제한합니다.

### <a name="parameter-conventions"></a>매개 변수 규칙

`UseWebApiParameterConventionsAttribute`는 `WebApiParameterConventionsApplicationModelConvention` 작업 규칙을 적용하는 데 사용됩니다. 이 규칙은 기본적으로 작업 매개 변수가 URI에서 바인딩될 때 사용되는 단순 형식을 지정합니다. 반면 복합 형식은 요청 본문에서 바인딩됩니다.

### <a name="routes"></a>경로

`WebApiApplicationModelConvention` 컨트롤러 규칙을 적용할지 여부는 `UseWebApiRoutesAttribute`가 제어합니다. 이 규칙을 사용하면 경로에 [영역](xref:mvc/controllers/areas)에 대한 지원을 추가하는 데 사용합니다.

호환성 패키지에는 규칙 집합 외에도 Web API에서 제공하는 클래스를 대체하는 `System.Web.Http.ApiController` 기본 클래스가 포함됩니다. 이렇게 하면 Web API용으로 작성되고 해당 `ApiController`에서 상속된 컨트롤러를 ASP.NET Core MVC에서 실행하는 동안 디자인할 때 작동시킬 수 있습니다. 이 기본 컨트롤러 클래스는 위에 나열된 모든 `UseWebApi*` 특성으로 데코레이팅됩니다. `ApiController`는 Web API에 있는 항목과 호환되는 속성, 메서드 및 결과 형식을 노출합니다.

## <a name="using-apiexplorer-to-document-your-app"></a>ApiExplorer를 사용하여 앱 문서화

애플리케이션 모델은 앱의 구조를 트래버스하는 데 사용할 수 있는 각 수준에서 [`ApiExplorer`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.apiexplorermodel) 속성을 노출합니다. [Swagger와 같은 도구를 사용하여 Web API용 도움말 페이지를 생성](xref:tutorials/web-api-help-pages-using-swagger)하는 데 사용할 수 있습니다. `ApiExplorer` 속성은 앱의 모델이 노출해야 하는 부분을 지정하도록 설정할 수 있는 `IsVisible` 속성을 노출합니다. 규칙을 사용하여 이 설정을 구성할 수 있습니다.

[!code-csharp[](./application-model/sample/src/AppModelSample/Conventions/EnableApiExplorerApplicationConvention.cs)]

이 접근 방식(및 필요한 경우 추가 규칙)을 사용하여 앱 내의 모든 수준에서 API 가시성을 사용하거나 사용하지 않도록 설정할 수 있습니다. 
