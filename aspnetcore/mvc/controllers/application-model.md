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
# <a name="work-with-the-application-model-in-aspnet-core"></a><span data-ttu-id="682f2-103">ASP.NET Core에서 애플리케이션 모델 작업</span><span class="sxs-lookup"><span data-stu-id="682f2-103">Work with the application model in ASP.NET Core</span></span>

<span data-ttu-id="682f2-104">작성자: [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="682f2-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="682f2-105">ASP.NET Core MVC는 MVC 앱의 구성 요소를 나타내는 *애플리케이션 모델*을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-105">ASP.NET Core MVC defines an *application model* representing the components of an MVC app.</span></span> <span data-ttu-id="682f2-106">이 모델을 읽고 조작하여 MVC 요소의 작동 방법을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-106">You can read and manipulate this model to modify how MVC elements behave.</span></span> <span data-ttu-id="682f2-107">기본적으로 MVC는 컨트롤러로 간주되는 클래스, 작업할 해당 클래스의 메서드 및 매개 변수 및 라우팅 작동 방법을 결정하는 특정 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-107">By default, MVC follows certain conventions to determine which classes are considered to be controllers, which methods on those classes are actions, and how parameters and routing behave.</span></span> <span data-ttu-id="682f2-108">고유한 규칙을 만들고 전역으로 또는 특성으로 적용하여 앱의 요구 사항에 맞게 이 동작을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-108">You can customize this behavior to suit your app's needs by creating your own conventions and applying them globally or as attributes.</span></span>

## <a name="models-and-providers"></a><span data-ttu-id="682f2-109">모델 및 공급자</span><span class="sxs-lookup"><span data-stu-id="682f2-109">Models and Providers</span></span>

<span data-ttu-id="682f2-110">ASP.NET Core MVC 애플리케이션 모델에는 MVC 애플리케이션을 설명하는 추상 인터페이스 및 구체적인 구현 클래스가 모두 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-110">The ASP.NET Core MVC application model include both abstract interfaces and concrete implementation classes that describe an MVC application.</span></span> <span data-ttu-id="682f2-111">이 모델은 기본 규칙에 따라 앱의 컨트롤러, 작업, 작업 매개 변수, 경로 및 필터를 검색하는 MVC의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-111">This model is the result of MVC discovering the app's controllers, actions, action parameters, routes, and filters according to default conventions.</span></span> <span data-ttu-id="682f2-112">애플리케이션 모델을 사용하여 기본 MVC 동작에서 다른 규칙을 따르도록 앱을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-112">By working with the application model, you can modify your app to follow different conventions from the default MVC behavior.</span></span> <span data-ttu-id="682f2-113">매개 변수, 이름, 경로 및 필터는 모두 작업 및 컨트롤러에 대한 구성 데이터로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-113">The parameters, names, routes, and filters are all used as configuration data for actions and controllers.</span></span>

<span data-ttu-id="682f2-114">ASP.NET Core MVC 애플리케이션 모델의 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-114">The ASP.NET Core MVC Application Model has the following structure:</span></span>

* <span data-ttu-id="682f2-115">ApplicationModel</span><span class="sxs-lookup"><span data-stu-id="682f2-115">ApplicationModel</span></span>
    * <span data-ttu-id="682f2-116">컨트롤러(ControllerModel)</span><span class="sxs-lookup"><span data-stu-id="682f2-116">Controllers (ControllerModel)</span></span>
        * <span data-ttu-id="682f2-117">작업(ActionModel)</span><span class="sxs-lookup"><span data-stu-id="682f2-117">Actions (ActionModel)</span></span>
            * <span data-ttu-id="682f2-118">매개 변수(ParameterModel)</span><span class="sxs-lookup"><span data-stu-id="682f2-118">Parameters (ParameterModel)</span></span>

<span data-ttu-id="682f2-119">모델의 각 수준에는 공통 `Properties` 컬렉션에 대한 액세스 권한이 있습니다. 하위 수준은 계층의 상위 수준에서 설정된 속성 값에 액세스하고 해당 값을 덮어쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-119">Each level of the model has access to a common `Properties` collection, and lower levels can access and overwrite property values set by higher levels in the hierarchy.</span></span> <span data-ttu-id="682f2-120">속성은 작업을 만들 때 `ActionDescriptor.Properties`에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-120">The properties are persisted to the `ActionDescriptor.Properties` when the actions are created.</span></span> <span data-ttu-id="682f2-121">그러면 요청을 처리 중인 경우 규칙에서 추가하거나 수정한 모든 속성은 `ActionContext.ActionDescriptor.Properties`를 통해 액세스될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-121">Then when a request is being handled, any properties a convention added or modified can be accessed through `ActionContext.ActionDescriptor.Properties`.</span></span> <span data-ttu-id="682f2-122">작업 기준으로 필터, 모델 바인더 등을 구성할 때 속성을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-122">Using properties is a great way to configure your filters, model binders, etc. on a per-action basis.</span></span>

> [!NOTE]
> <span data-ttu-id="682f2-123">앱 시작이 완료되면 `ActionDescriptor.Properties` 컬렉션은 스레드에 대해 안전하지 않습니다(쓰기의 경우).</span><span class="sxs-lookup"><span data-stu-id="682f2-123">The `ActionDescriptor.Properties` collection isn't thread safe (for writes) once app startup has finished.</span></span> <span data-ttu-id="682f2-124">데이터를 안전하게 이 컬렉션에 추가할 때 규칙을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-124">Conventions are the best way to safely add data to this collection.</span></span>

### <a name="iapplicationmodelprovider"></a><span data-ttu-id="682f2-125">IApplicationModelProvider</span><span class="sxs-lookup"><span data-stu-id="682f2-125">IApplicationModelProvider</span></span>

<span data-ttu-id="682f2-126">ASP.NET Core MVC는 공급자 패턴을 사용하여 애플리케이션 모델을 로드하며 [IApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.iapplicationmodelprovider) 인터페이스에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-126">ASP.NET Core MVC loads the application model using a provider pattern, defined by the [IApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.iapplicationmodelprovider) interface.</span></span> <span data-ttu-id="682f2-127">이 섹션에서는 이 공급자가 작동하는 방법에 대한 내부 구현 세부 정보 중 일부를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-127">This section covers some of the internal implementation details of how this provider functions.</span></span> <span data-ttu-id="682f2-128">규칙을 사용하여 애플리케이션 모델을 활용하는 대부분의 앱이 수행해야 하는 고급 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-128">This is an advanced topic - most apps that leverage the application model should do so by working with conventions.</span></span>

<span data-ttu-id="682f2-129">`IApplicationModelProvider` 인터페이스의 구현은 서로 "래핑"합니다. 이 때 각 구현은 해당 `Order` 속성에 따라 오름차순으로 `OnProvidersExecuting`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-129">Implementations of the `IApplicationModelProvider` interface "wrap" one another, with each implementation calling `OnProvidersExecuting` in ascending order based on its `Order` property.</span></span> <span data-ttu-id="682f2-130">`OnProvidersExecuted` 메서드는 역순으로 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-130">The `OnProvidersExecuted` method is then called in reverse order.</span></span> <span data-ttu-id="682f2-131">프레임워크는 여러 공급자를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-131">The framework defines several providers:</span></span>

<span data-ttu-id="682f2-132">First(`Order=-1000`):</span><span class="sxs-lookup"><span data-stu-id="682f2-132">First (`Order=-1000`):</span></span>

* [`DefaultApplicationModelProvider`](/dotnet/api/microsoft.aspnetcore.mvc.internal.defaultapplicationmodelprovider)

<span data-ttu-id="682f2-133">Then(`Order=-990`):</span><span class="sxs-lookup"><span data-stu-id="682f2-133">Then (`Order=-990`):</span></span>

* [`AuthorizationApplicationModelProvider`](/dotnet/api/microsoft.aspnetcore.mvc.internal.authorizationapplicationmodelprovider)
* [`CorsApplicationModelProvider`](/dotnet/api/microsoft.aspnetcore.mvc.cors.internal.corsapplicationmodelprovider)

> [!NOTE]
> <span data-ttu-id="682f2-134">`Order`에 대해 같은 값을 가진 두 공급자를 호출하는 순서는 정의되지 않으며 따라서 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-134">The order in which two providers with the same value for `Order` are called is undefined, and therefore shouldn't be relied upon.</span></span>

> [!NOTE]
> <span data-ttu-id="682f2-135">`IApplicationModelProvider`는 확장할 프레임워크 작성자를 위한 고급 개념입니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-135">`IApplicationModelProvider` is an advanced concept for framework authors to extend.</span></span> <span data-ttu-id="682f2-136">일반적으로 앱은 규칙을 사용해야 하고 프레임워크는 공급자를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-136">In general, apps should use conventions and frameworks should use providers.</span></span> <span data-ttu-id="682f2-137">중요한 차이점은 공급자가 항상 규칙 이전에 실행된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-137">The key distinction is that providers always run before conventions.</span></span>

<span data-ttu-id="682f2-138">`DefaultApplicationModelProvider`는 ASP.NET Core MVC에서 사용하는 대부분의 기본 동작을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-138">The `DefaultApplicationModelProvider` establishes many of the default behaviors used by ASP.NET Core MVC.</span></span> <span data-ttu-id="682f2-139">해당 책임은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-139">Its responsibilities include:</span></span>

* <span data-ttu-id="682f2-140">컨텍스트에 전역 필터 추가</span><span class="sxs-lookup"><span data-stu-id="682f2-140">Adding global filters to the context</span></span>
* <span data-ttu-id="682f2-141">컨텍스트에 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="682f2-141">Adding controllers to the context</span></span>
* <span data-ttu-id="682f2-142">작업으로 공용 컨트롤러 메서드 추가</span><span class="sxs-lookup"><span data-stu-id="682f2-142">Adding public controller methods as actions</span></span>
* <span data-ttu-id="682f2-143">컨텍스트에 작업 메서드 매개 변수 추가</span><span class="sxs-lookup"><span data-stu-id="682f2-143">Adding action method parameters to the context</span></span>
* <span data-ttu-id="682f2-144">경로 및 기타 특성 적용</span><span class="sxs-lookup"><span data-stu-id="682f2-144">Applying route and other attributes</span></span>

<span data-ttu-id="682f2-145">일부 기본 제공 동작은 `DefaultApplicationModelProvider`에 의해 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-145">Some built-in behaviors are implemented by the `DefaultApplicationModelProvider`.</span></span> <span data-ttu-id="682f2-146">이 공급자는 [`ControllerModel`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.controllermodel)을 구성할 책임이 있습니다. 여기서는 [`ActionModel`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.actionmodel#Microsoft_AspNetCore_Mvc_ApplicationModels_ActionModel), [`PropertyModel`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.propertymodel) 및 [`ParameterModel`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.parametermodel#Microsoft_AspNetCore_Mvc_ApplicationModels_ParameterModel) 인스턴스를 차례로 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-146">This provider is responsible for constructing the [`ControllerModel`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.controllermodel), which in turn references [`ActionModel`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.actionmodel#Microsoft_AspNetCore_Mvc_ApplicationModels_ActionModel), [`PropertyModel`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.propertymodel), and [`ParameterModel`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.parametermodel#Microsoft_AspNetCore_Mvc_ApplicationModels_ParameterModel) instances.</span></span> <span data-ttu-id="682f2-147">`DefaultApplicationModelProvider` 클래스는 나중에 변경될 수 있는 내부 프레임워크 구현 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-147">The `DefaultApplicationModelProvider` class is an internal framework implementation detail that can and will change in the future.</span></span> 

<span data-ttu-id="682f2-148">`AuthorizationApplicationModelProvider`는 `AuthorizeFilter` 및 `AllowAnonymousFilter` 특성과 연결된 동작을 적용할 책임이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-148">The `AuthorizationApplicationModelProvider` is responsible for applying the behavior associated with the `AuthorizeFilter` and `AllowAnonymousFilter` attributes.</span></span> <span data-ttu-id="682f2-149">[이러한 특성에 대한 자세한 정보](xref:security/authorization/simple)</span><span class="sxs-lookup"><span data-stu-id="682f2-149">[Learn more about these attributes](xref:security/authorization/simple).</span></span>

<span data-ttu-id="682f2-150">`CorsApplicationModelProvider`는 `IEnableCorsAttribute`, `IDisableCorsAttribute` 및 `DisableCorsAuthorizationFilter`와 연결된 동작을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-150">The `CorsApplicationModelProvider` implements behavior associated with the `IEnableCorsAttribute` and `IDisableCorsAttribute`, and the `DisableCorsAuthorizationFilter`.</span></span> <span data-ttu-id="682f2-151">[CORS에 대해 자세히 알아봅니다](xref:security/cors).</span><span class="sxs-lookup"><span data-stu-id="682f2-151">[Learn more about CORS](xref:security/cors).</span></span>

## <a name="conventions"></a><span data-ttu-id="682f2-152">규칙</span><span class="sxs-lookup"><span data-stu-id="682f2-152">Conventions</span></span>

<span data-ttu-id="682f2-153">애플리케이션 모델은 전체 모델 또는 공급자를 재정의하기 보다는 모델의 동작을 사용자 지정하는 간단한 방법을 제공하는 규칙 추상화를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-153">The application model defines convention abstractions that provide a simpler way to customize the behavior of the models than overriding the entire model or provider.</span></span> <span data-ttu-id="682f2-154">앱의 동작을 수정할 때 이러한 추상화를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-154">These abstractions are the recommended way to modify your app's behavior.</span></span> <span data-ttu-id="682f2-155">규칙은 사용자 지정을 동적으로 적용하는 코드를 작성할 수 있는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-155">Conventions provide a way for you to write code that will dynamically apply customizations.</span></span> <span data-ttu-id="682f2-156">[필터](xref:mvc/controllers/filters)는 프레임워크의 동작을 수정하는 방법을 제공하는 반면, 사용자 지정을 통해 전체 앱을 함께 연결하는 방법을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-156">While [filters](xref:mvc/controllers/filters) provide a means of modifying the framework's behavior, customizations let you control how the whole app is wired together.</span></span>

<span data-ttu-id="682f2-157">사용할 수 있는 규칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-157">The following conventions are available:</span></span>

* [`IApplicationModelConvention`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.iapplicationmodelconvention)
* [`IControllerModelConvention`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.icontrollermodelconvention)
* [`IActionModelConvention`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.iactionmodelconvention)
* [`IParameterModelConvention`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.iparametermodelconvention)

<span data-ttu-id="682f2-158">MVC 옵션을 추가하거나 `Attribute`를 구현하고 컨트롤러, 작업 또는 작업 매개 변수([`Filters`](xref:mvc/controllers/filters)와 유사)에 적용하여 규칙을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-158">Conventions are applied by adding them to MVC options or by implementing `Attribute`s and applying them to controllers, actions, or action parameters (similar to [`Filters`](xref:mvc/controllers/filters)).</span></span> <span data-ttu-id="682f2-159">필터와 달리 각 요청의 일부가 아니라 앱을 시작하는 경우에만 규칙이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-159">Unlike filters, conventions are only executed when the app is starting, not as part of each request.</span></span>

### <a name="sample-modifying-the-applicationmodel"></a><span data-ttu-id="682f2-160">예제: Applicationmodel 수정</span><span class="sxs-lookup"><span data-stu-id="682f2-160">Sample: Modifying the ApplicationModel</span></span>

<span data-ttu-id="682f2-161">다음 규칙은 애플리케이션 모델에 속성을 추가하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-161">The following convention is used to add a property to the application model.</span></span> 

[!code-csharp[](./application-model/sample/src/AppModelSample/Conventions/ApplicationDescription.cs)]

<span data-ttu-id="682f2-162">`Startup`의 `ConfigureServices`에 MVC를 추가할 경우 옵션으로 애플리케이션 모델 규칙을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-162">Application model conventions are applied as options when MVC is added in `ConfigureServices` in `Startup`.</span></span>

[!code-csharp[](./application-model/sample/src/AppModelSample/Startup.cs?name=ConfigureServices&highlight=5)]

<span data-ttu-id="682f2-163">속성은 컨트롤러 작업 내의 `ActionDescriptor` 속성 컬렉션에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-163">Properties are accessible from the `ActionDescriptor` properties collection within controller actions:</span></span>

[!code-csharp[](./application-model/sample/src/AppModelSample/Controllers/AppModelController.cs?name=AppModelController)]

### <a name="sample-modifying-the-controllermodel-description"></a><span data-ttu-id="682f2-164">예제: ControllerModel 설명 수정</span><span class="sxs-lookup"><span data-stu-id="682f2-164">Sample: Modifying the ControllerModel Description</span></span>

<span data-ttu-id="682f2-165">이전의 예제처럼 컨트롤러 모델은 사용자 지정 속성을 포함하도록 수정될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-165">As in the previous example, the controller model can also be modified to include custom properties.</span></span> <span data-ttu-id="682f2-166">그러면 애플리케이션 모델에 지정된 동일한 이름을 가진 기존 속성을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-166">These will override existing properties with the same name specified in the application model.</span></span> <span data-ttu-id="682f2-167">다음과 같은 규칙 특성은 컨트롤러 수준에서 설명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-167">The following convention attribute adds a description at the controller level:</span></span>

[!code-csharp[](./application-model/sample/src/AppModelSample/Conventions/ControllerDescriptionAttribute.cs)]

<span data-ttu-id="682f2-168">이 규칙은 컨트롤러에 대한 특성으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-168">This convention is applied as an attribute on a controller.</span></span>

[!code-csharp[](./application-model/sample/src/AppModelSample/Controllers/DescriptionAttributesController.cs?name=ControllerDescription&highlight=1)]

<span data-ttu-id="682f2-169">이전 예제와 같이 동일한 방식으로 "설명" 속성에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-169">The "description" property is accessed in the same manner as in previous examples.</span></span>

### <a name="sample-modifying-the-actionmodel-description"></a><span data-ttu-id="682f2-170">예제: ActionModel 설명 수정</span><span class="sxs-lookup"><span data-stu-id="682f2-170">Sample: Modifying the ActionModel Description</span></span>

<span data-ttu-id="682f2-171">개별 작업에 별도의 특성 규칙을 적용할 수 있습니다. 그러면 이미 애플리케이션 또는 컨트롤러 수준에서 적용되는 동작을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-171">A separate attribute convention can be applied to individual actions, overriding behavior already applied at the application or controller level.</span></span>

[!code-csharp[](./application-model/sample/src/AppModelSample/Conventions/ActionDescriptionAttribute.cs)]

<span data-ttu-id="682f2-172">이전 예제의 컨트롤러 내에 있는 작업에 이를 적용하면 컨트롤러 수준 규칙을 재정의하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-172">Applying this to an action within the previous example's controller demonstrates how it overrides the controller-level convention:</span></span>

[!code-csharp[](./application-model/sample/src/AppModelSample/Controllers/DescriptionAttributesController.cs?name=DescriptionAttributesController&highlight=9)]

### <a name="sample-modifying-the-parametermodel"></a><span data-ttu-id="682f2-173">예제: Parametermodel 수정</span><span class="sxs-lookup"><span data-stu-id="682f2-173">Sample: Modifying the ParameterModel</span></span>

<span data-ttu-id="682f2-174">`BindingInfo`를 수정하는 작업 매개 변수에 다음 규칙을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-174">The following convention can be applied to action parameters to modify their `BindingInfo`.</span></span> <span data-ttu-id="682f2-175">다음과 같은 규칙의 매개 변수는 경로 매개 변수여야 합니다. 다른 잠재적인 바인딩 소스(예: 쿼리 문자열 값)는 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-175">The following convention requires that the parameter be a route parameter; other potential binding sources (such as query string values) are ignored.</span></span>

[!code-csharp[](./application-model/sample/src/AppModelSample/Conventions/MustBeInRouteParameterModelConvention.cs)]

<span data-ttu-id="682f2-176">특성이 모든 작업 매개 변수에 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-176">The attribute may be applied to any action parameter:</span></span>

[!code-csharp[](./application-model/sample/src/AppModelSample/Controllers/ParameterModelController.cs?name=ParameterModelController&highlight=5)]

### <a name="sample-modifying-the-actionmodel-name"></a><span data-ttu-id="682f2-177">예제: ActionModel 이름 수정</span><span class="sxs-lookup"><span data-stu-id="682f2-177">Sample: Modifying the ActionModel Name</span></span>

<span data-ttu-id="682f2-178">다음 규칙은 적용되는 작업의 *이름*을 업데이트하도록 `ActionModel`을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-178">The following convention modifies the `ActionModel` to update the *name* of the action to which it's applied.</span></span> <span data-ttu-id="682f2-179">특성에 대한 매개 변수로 새 이름이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-179">The new name is provided as a parameter to the attribute.</span></span> <span data-ttu-id="682f2-180">라우팅에서 이 새 이름을 사용하므로 이 작업 메서드에 연결하는 데 사용된 경로에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-180">This new name is used by routing, so it will affect the route used to reach this action method.</span></span>

[!code-csharp[](./application-model/sample/src/AppModelSample/Conventions/CustomActionNameAttribute.cs)]

<span data-ttu-id="682f2-181">이 특성은 `HomeController`에서 작업 메서드에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-181">This attribute is applied to an action method in the `HomeController`:</span></span>

[!code-csharp[](./application-model/sample/src/AppModelSample/Controllers/HomeController.cs?name=ActionModelConvention&highlight=2)]

<span data-ttu-id="682f2-182">메서드 이름이 `SomeName`이지만 특성은 메서드 이름을 사용하는 MVC 규칙을 재정의하 작업 이름을 `MyCoolAction`으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-182">Even though the method name is `SomeName`, the attribute overrides the MVC convention of using the method name and replaces the action name with `MyCoolAction`.</span></span> <span data-ttu-id="682f2-183">따라서 이 작업에 도달하는 데 사용된 경로는 `/Home/MyCoolAction`입니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-183">Thus, the route used to reach this action is `/Home/MyCoolAction`.</span></span>

> [!NOTE]
> <span data-ttu-id="682f2-184">이 예제는 기본적으로 기본 제공 [ActionName](/dotnet/api/microsoft.aspnetcore.mvc.actionnameattribute) 특성을 사용하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-184">This example is essentially the same as using the built-in [ActionName](/dotnet/api/microsoft.aspnetcore.mvc.actionnameattribute) attribute.</span></span>

### <a name="sample-custom-routing-convention"></a><span data-ttu-id="682f2-185">예제: 사용자 지정 라우팅 규칙</span><span class="sxs-lookup"><span data-stu-id="682f2-185">Sample: Custom Routing Convention</span></span>

<span data-ttu-id="682f2-186">`IApplicationModelConvention`을 사용하여 라우팅 작동 방법을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-186">You can use an `IApplicationModelConvention` to customize how routing works.</span></span> <span data-ttu-id="682f2-187">예를 들어 다음 규칙은 컨트롤러의 네임스페이스를 해당 경로에 통합하고 네임스페이스의 `.`를 경로의 `/`로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-187">For example, the following convention will incorporate Controllers' namespaces into their routes, replacing `.` in the namespace with `/` in the route:</span></span>

[!code-csharp[](./application-model/sample/src/AppModelSample/Conventions/NamespaceRoutingConvention.cs)]

<span data-ttu-id="682f2-188">규칙은 시작에서 옵션으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-188">The convention is added as an option in Startup.</span></span>

[!code-csharp[](./application-model/sample/src/AppModelSample/Startup.cs?name=ConfigureServices&highlight=6)]

> [!TIP]
> <span data-ttu-id="682f2-189">`services.Configure<MvcOptions>(c => c.Conventions.Add(YOURCONVENTION));`를 사용하는 `MvcOptions`에 액세스하여 [미들웨어](xref:fundamentals/middleware/index)에 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-189">You can add conventions to your [middleware](xref:fundamentals/middleware/index) by accessing `MvcOptions` using `services.Configure<MvcOptions>(c => c.Conventions.Add(YOURCONVENTION));`</span></span>

<span data-ttu-id="682f2-190">이 샘플에서는 컨트롤러의 이름에 "네임스페이스"가 있는 특성 라우팅을 사용하지 않는 경로에 이 규칙을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-190">This sample applies this convention to routes that are not using attribute routing where the controller has  "Namespace" in its name.</span></span> <span data-ttu-id="682f2-191">다음 컨트롤러에서는 이 규칙을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-191">The following controller demonstrates this convention:</span></span>

[!code-csharp[](./application-model/sample/src/AppModelSample/Controllers/NamespaceRoutingController.cs?highlight=7-8)]

## <a name="application-model-usage-in-webapicompatshim"></a><span data-ttu-id="682f2-192">WebApiCompatShim의 애플리케이션 모델 사용</span><span class="sxs-lookup"><span data-stu-id="682f2-192">Application Model Usage in WebApiCompatShim</span></span>

<span data-ttu-id="682f2-193">ASP.NET Core MVC는 ASP.NET Web API 2에서 다른 규칙 집합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-193">ASP.NET Core MVC uses a different set of conventions from ASP.NET Web API 2.</span></span> <span data-ttu-id="682f2-194">사용자 지정 규칙을 사용하여 Web API 앱의 해당 값과 일치되도록 ASP.NET Core MVC 앱의 동작을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-194">Using custom conventions, you can modify an ASP.NET Core MVC app's behavior to be consistent with that of a Web API app.</span></span> <span data-ttu-id="682f2-195">Microsoft는 이를 위해 [WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim/)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-195">Microsoft ships the [WebApiCompatShim](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.WebApiCompatShim/) specifically for this purpose.</span></span>

> [!NOTE]
> <span data-ttu-id="682f2-196">[ASP.NET Web API에서 마이그레이션](xref:migration/webapi)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-196">Learn more about [migration from ASP.NET Web API](xref:migration/webapi).</span></span>

<span data-ttu-id="682f2-197">Web API 호환성 Shim을 사용하려면 프로젝트에 패키지를 추가한 다음, `Startup`에서 `AddWebApiConventions`를 호출하여 MVC에 규칙을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-197">To use the Web API Compatibility Shim, you need to add the package to your project and then add the conventions to MVC by calling `AddWebApiConventions` in `Startup`:</span></span>

```csharp
services.AddMvc().AddWebApiConventions();
```

<span data-ttu-id="682f2-198">shim에서 제공하는 규칙은 특정 특성에 적용되는 앱의 일부에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-198">The conventions provided by the shim are only applied to parts of the app that have had certain attributes applied to them.</span></span> <span data-ttu-id="682f2-199">다음과 같은 네 가지 특성이 컨트롤에 사용됩니다. 여기서 컨트롤러는 shim의 규칙에 의해 수정된 규칙을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-199">The following four attributes are used to control which controllers should have their conventions modified by the shim's conventions:</span></span>

* [<span data-ttu-id="682f2-200">UseWebApiActionConventionsAttribute</span><span class="sxs-lookup"><span data-stu-id="682f2-200">UseWebApiActionConventionsAttribute</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.webapicompatshim.usewebapiactionconventionsattribute)
* [<span data-ttu-id="682f2-201">UseWebApiOverloadingAttribute</span><span class="sxs-lookup"><span data-stu-id="682f2-201">UseWebApiOverloadingAttribute</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.webapicompatshim.usewebapioverloadingattribute)
* [<span data-ttu-id="682f2-202">UseWebApiParameterConventionsAttribute</span><span class="sxs-lookup"><span data-stu-id="682f2-202">UseWebApiParameterConventionsAttribute</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.webapicompatshim.usewebapiparameterconventionsattribute)
* [<span data-ttu-id="682f2-203">UseWebApiRoutesAttribute</span><span class="sxs-lookup"><span data-stu-id="682f2-203">UseWebApiRoutesAttribute</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.webapicompatshim.usewebapiroutesattribute)

### <a name="action-conventions"></a><span data-ttu-id="682f2-204">작업 규칙</span><span class="sxs-lookup"><span data-stu-id="682f2-204">Action Conventions</span></span>

<span data-ttu-id="682f2-205">`UseWebApiActionConventionsAttribute`는 이름에 따라 작업에 HTTP 메서드를 매핑하는 데 사용됩니다(예: `Get`은 `HttpGet`에 매핑됨).</span><span class="sxs-lookup"><span data-stu-id="682f2-205">The `UseWebApiActionConventionsAttribute` is used to map the HTTP method to actions based on their name (for instance, `Get` would map to `HttpGet`).</span></span> <span data-ttu-id="682f2-206">특성 라우팅을 사용하지 않는 작업에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-206">It only applies to actions that don't use attribute routing.</span></span>

### <a name="overloading"></a><span data-ttu-id="682f2-207">오버로딩</span><span class="sxs-lookup"><span data-stu-id="682f2-207">Overloading</span></span>

<span data-ttu-id="682f2-208">`UseWebApiOverloadingAttribute`는 `WebApiOverloadingApplicationModelConvention` 규칙을 적용하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-208">The `UseWebApiOverloadingAttribute` is used to apply the `WebApiOverloadingApplicationModelConvention` convention.</span></span> <span data-ttu-id="682f2-209">이 규칙은 작업 선택 프로세스에 `OverloadActionConstraint`를 추가합니다. 그러면 요청이 모든 필수 매개 변수를 충족하기 때문에 해당 작업에 대한 후보 작업을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-209">This convention adds an `OverloadActionConstraint` to the action selection process, which limits candidate actions to those for which the request satisfies all non-optional parameters.</span></span>

### <a name="parameter-conventions"></a><span data-ttu-id="682f2-210">매개 변수 규칙</span><span class="sxs-lookup"><span data-stu-id="682f2-210">Parameter Conventions</span></span>

<span data-ttu-id="682f2-211">`UseWebApiParameterConventionsAttribute`는 `WebApiParameterConventionsApplicationModelConvention` 작업 규칙을 적용하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-211">The `UseWebApiParameterConventionsAttribute` is used to apply the `WebApiParameterConventionsApplicationModelConvention` action convention.</span></span> <span data-ttu-id="682f2-212">이 규칙은 기본적으로 작업 매개 변수가 URI에서 바인딩될 때 사용되는 단순 형식을 지정합니다. 반면 복합 형식은 요청 본문에서 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-212">This convention specifies that simple types used as action parameters are bound from the URI by default, while complex types are bound from the request body.</span></span>

### <a name="routes"></a><span data-ttu-id="682f2-213">경로</span><span class="sxs-lookup"><span data-stu-id="682f2-213">Routes</span></span>

<span data-ttu-id="682f2-214">`WebApiApplicationModelConvention` 컨트롤러 규칙을 적용할지 여부는 `UseWebApiRoutesAttribute`가 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-214">The `UseWebApiRoutesAttribute` controls whether the `WebApiApplicationModelConvention` controller convention is applied.</span></span> <span data-ttu-id="682f2-215">이 규칙을 사용하면 경로에 [영역](xref:mvc/controllers/areas)에 대한 지원을 추가하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-215">When enabled, this convention is used to add support for [areas](xref:mvc/controllers/areas) to the route.</span></span>

<span data-ttu-id="682f2-216">호환성 패키지에는 규칙 집합 외에도 Web API에서 제공하는 클래스를 대체하는 `System.Web.Http.ApiController` 기본 클래스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-216">In addition to a set of conventions, the compatibility package includes a `System.Web.Http.ApiController` base class that replaces the one provided by Web API.</span></span> <span data-ttu-id="682f2-217">이렇게 하면 Web API용으로 작성되고 해당 `ApiController`에서 상속된 컨트롤러를 ASP.NET Core MVC에서 실행하는 동안 디자인할 때 작동시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-217">This allows your controllers written for Web API and inheriting from its `ApiController` to work as they were designed, while running on ASP.NET Core MVC.</span></span> <span data-ttu-id="682f2-218">이 기본 컨트롤러 클래스는 위에 나열된 모든 `UseWebApi*` 특성으로 데코레이팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-218">This base controller class is decorated with all of the `UseWebApi*` attributes listed above.</span></span> <span data-ttu-id="682f2-219">`ApiController`는 Web API에 있는 항목과 호환되는 속성, 메서드 및 결과 형식을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-219">The `ApiController` exposes properties, methods, and result types that are compatible with those found in Web API.</span></span>

## <a name="using-apiexplorer-to-document-your-app"></a><span data-ttu-id="682f2-220">ApiExplorer를 사용하여 앱 문서화</span><span class="sxs-lookup"><span data-stu-id="682f2-220">Using ApiExplorer to Document Your App</span></span>

<span data-ttu-id="682f2-221">애플리케이션 모델은 앱의 구조를 트래버스하는 데 사용할 수 있는 각 수준에서 [`ApiExplorer`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.apiexplorermodel) 속성을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-221">The application model exposes an [`ApiExplorer`](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.apiexplorermodel) property at each level that can be used to traverse the app's structure.</span></span> <span data-ttu-id="682f2-222">[Swagger와 같은 도구를 사용하여 Web API용 도움말 페이지를 생성](xref:tutorials/web-api-help-pages-using-swagger)하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-222">This can be used to [generate help pages for your Web APIs using tools like Swagger](xref:tutorials/web-api-help-pages-using-swagger).</span></span> <span data-ttu-id="682f2-223">`ApiExplorer` 속성은 앱의 모델이 노출해야 하는 부분을 지정하도록 설정할 수 있는 `IsVisible` 속성을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-223">The `ApiExplorer` property exposes an `IsVisible` property that can be set to specify which parts of your app's model should be exposed.</span></span> <span data-ttu-id="682f2-224">규칙을 사용하여 이 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-224">You can configure this setting using a convention:</span></span>

[!code-csharp[](./application-model/sample/src/AppModelSample/Conventions/EnableApiExplorerApplicationConvention.cs)]

<span data-ttu-id="682f2-225">이 접근 방식(및 필요한 경우 추가 규칙)을 사용하여 앱 내의 모든 수준에서 API 가시성을 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="682f2-225">Using this approach (and additional conventions if required), you can enable or disable API visibility at any level within your app.</span></span> 
